---
title: Instellen van SSL-versleuteling en verificatie voor Apache Kafka in Azure HDInsight
description: SSL-codering voor communicatie tussen Kafka-clients en Kafka-brokers ook tussen Kafka-brokers instellen. SSL-verificatie voor clients instellen.
services: hdinsight
author: hrasheed-msft
ms.reviewer: jasonh
ms.service: hdinsight
ms.custom: hdinsightactive
ms.topic: conceptual
ms.date: 01/15/2019
ms.author: hrasheed
ms.openlocfilehash: 665b439fb1ca0b907ea7385369f64d255e8e42e6
ms.sourcegitcommit: a1cf88246e230c1888b197fdb4514aec6f1a8de2
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54355554"
---
# <a name="setup-secure-sockets-layer-ssl-encryption-and-authentication-for-apache-kafka-in-azure-hdinsight"></a>Setup van Secure Sockets Layer (SSL)-codering en -verificatie voor Apache Kafka in Azure HDInsight

In dit artikel wordt beschreven hoe u SSL-versleuteling van Apache Kafka-clients tot Apache Kafka-brokers en ook tussen Apache Kafka-brokers instellen. Het biedt ook de stappen die nodig zijn voor verificatie van de installatie van clients (soms aangeduid als wederzijdse SSL).

## <a name="server-setup"></a>Installatie van de server

De eerste stap is het instellen van de sleutelopslagplaats en de truststore op de Kafka-brokers en de certificeringsinstantie (CA) en de broker-certificaten importeren naar deze stores.

> [!Note] 
> Deze handleiding worden zelfondertekende certificaten gebruikt, maar de veiligste oplossing is het gebruik van certificaten van vertrouwde certificeringsinstanties.

1. Maak een map met de naam van ssl en het serverwachtwoord exporteren als een omgevingsvariabele. Voor de rest van deze handleiding, Vervang `<server_password>` met het werkelijke beheerderswachtwoord voor de server.

    ```bash
    $export SRVPASS=<server_password>
    $mkdir ssl
    $cd ssl
    ```

2. Maak vervolgens een java keystore (kafka.server.keystore.jks) en een CA-certificaat.

    ```bash
    $keytool -genkey -keystore kafka.server.keystore.jks -validity 365 -storepass $SRVPASS -keypass $SRVPASS -dname "CN=wn0-umakaf.xvbseke35rbuddm4fyvhm2vz2h.cx.internal.cloudapp.net" -storetype pkcs12
    ```

3. Vervolgens maakt u een aanvraag voor Certificaatondertekening ophalen van het certificaat dat is gemaakt in de vorige stap die is ondertekend door de CA.

    ```bash
    $keytool -keystore kafka.server.keystore.jks -certreq -file cert-file -storepass $SRVPASS -keypass $SRVPASS
    ```

4. Nu de aanvraag voor Certificaatondertekening verzenden naar de CA en ophalen van dit certificaat dat is ondertekend. Omdat we een zelfondertekend certificaat gebruikt, wordt het certificaat ondertekent met behulp van onze CA de `openssl` opdracht.

    ```bash
    $openssl x509 -req -CA ca-cert -CAkey ca-key -in cert-file -out cert-signed -days 365 -CAcreateserial -passin pass:$SRVPASS
    ```

5. Maken van een vertrouwensrelatie store en importeer het certificaat van de CA.

    ```bash
    $keytool -keystore kafka.server.truststore.jks -alias CARoot -import -file ca-cert -storepass $SRVPASS -keypass $SRVPASS -noprompt
    ```

6. De openbare CA-certificaat importeren in de sleutelopslag.

    ```bash
    $keytool -keystore kafka.server.keystore.jks -alias CARoot -import -file ca-cert -storepass $SRVPASS -keypass $SRVPASS -noprompt
    ```

7. Het ondertekende certificaat importeren in de sleutelopslag.

    ```bash
    $keytool -keystore kafka.server.keystore.jks -alias CARoot -import -file ca-cert -storepass $SRVPASS -keypass $SRVPASS -noprompt//output is "Certificate reply was added to keystore"
    ```

Het ondertekende certificaat importeren in de sleutelopslag, is de laatste stap die nodig zijn voor de truststore en keystore voor een Kafka-broker configureren.

## <a name="update-configuration-to-use-ssl-and-restart-brokers"></a>Configuratie voor het gebruik van SSL en opnieuw opstarten brokers bijwerken

We hebben elke Kafka broker met een keystore en truststore en de juiste certificaten zijn geïmporteerd.  Vervolgens verwante eigenschappen van Kafka-configuratie met behulp van Ambari wijzigen en opnieuw opstarten van het Kafka-brokers.

1. Meld u aan bij Azure portal en selecteer uw Azure HDInsight Apache Kafka-cluster.
1. Ga naar de UI Ambari door te klikken op **Ambari home** onder **Clusterdashboards**.
1. Onder **Kafka-Broker** stelt de **listeners** eigenschap `PLAINTEXT://localhost:9092,SSL://localhost:9093`
1. Onder **kafka-broker geavanceerde** stelt de **security.inter.broker.protocol** eigenschap `SSL`

    ![Eigenschappen van een kafka-ssl-configuratie, in Ambari bewerken](./media/apache-kafka-ssl-encryption-authentication/editing-configuration-ambari.png)

1. Onder **aangepaste kafka-broker** stelt de **ssl.client.auth** eigenschap `required`. Deze stap is alleen vereist als het instellen van verificatie, evenals de versleuteling.

    ![Eigenschappen van een kafka-ssl-configuratie, in Ambari bewerken](./media/apache-kafka-ssl-encryption-authentication/editing-configuration-ambari2.png)

1. Configuratie-eigenschappen toevoegen aan de Kafka `server.properties` bestand voor het adverteren van IP-adressen in plaats van het volledig FULLY Qualified Domain Name ().

    ```bash
    IP_ADDRESS=$(hostname -i)
    echo advertised.listeners=$IP_ADDRESS
    sed -i.bak -e '/advertised/{/advertised@/!d;}' /usr/hdp/current/kafka-broker/conf/server.properties
    echo "advertised.listeners=PLAINTEXT://$IP_ADDRESS:9092,SSL://$IP_ADDRESS:9093" >> /usr/hdp/current/kafka-broker/conf/server.properties
    echo "ssl.keystore.location=/home/sshuser/ssl/kafka.server.keystore.jks" >> /usr/hdp/current/kafka-broker/conf/server.properties
    echo "ssl.keystore.password=<server_password>" >> /usr/hdp/current/kafka-broker/conf/server.properties
    echo "ssl.key.password=<server_password>" >> /usr/hdp/current/kafka-broker/conf/server.properties
    echo "ssl.truststore.location=/home/sshuser/ssl/kafka.server.truststore.jks" >> /usr/hdp/current/kafka-broker/conf/server.properties
    echo "ssl.truststore.password=<server_password>" >> /usr/hdp/current/kafka-broker/conf/server.properties
    ```

1. Om te verifiëren of de wijzigingen zijn aangebracht correct desgewenst kunt u controleren dat de volgende regels zijn aanwezig in de Kafka `server.properties` bestand.

    ```bash
    advertised.listeners=PLAINTEXT://10.0.0.11:9092,SSL://10.0.0.11:9093
    ssl.keystore.location=/home/sshuser/ssl/kafka.server.keystore.jks
    ssl.keystore.password=<server_password>
    ssl.key.password=<server_password>
    ssl.truststore.location=/home/sshuser/ssl/kafka.server.truststore.jks
    ssl.truststore.password=<server_password>
    ```

1. Start opnieuw op alle Kafka-brokers.

## <a name="client-setup-with-authentication"></a>Clientinstallatie (met behulp van verificatie)

> [!Note]
> De volgende stappen zijn alleen vereist als u beide SSL-versleuteling instelt **en** verificatie. Als u versleuteling alleen instelt, gaat u naar [installatie van de Client zonder verificatie](apache-kafka-ssl-encryption-authentication.md#client-setup-without-authentication)

1. Exporteer het wachtwoord van de client. Vervang `<client_password>` met de werkelijke beheerderswachtwoord op de clientcomputer Kafka.

    ```bash
    $export CLIPASS=<client_password>
    $cd ssl
    ```

1. Maak een java keystore en een ondertekend certificaat krijgen voor de broker. Kopieer vervolgens het certificaat naar de virtuele machine waarop de CA wordt uitgevoerd.

    ```bash
    $keytool -genkey -keystore kafka.client.keystore.jks -validity 365 -storepass $CLIPASS -keypass $CLIPASS -dname "CN=mylaptop1" -alias my-local-pc1 -storetype pkcs12

    $keytool -keystore kafka.client.keystore.jks -certreq -file client-cert-sign-request -alias my-local-pc1 -storepass $CLIPASS -keypass $CLIPASS

    $scp client-cert-sign-request3 sshuser@wn0-umakaf:~/tmp1/client-cert-sign-request
    ```

1. Schakel over naar de CA-computer (wn0) om te ondertekenen certificaat van de client.

    ```bash
    $cd ssl
    $openssl x509 -req -CA ca-cert -CAkey ca-key -in /tmp1/client-cert-sign-request -out /tmp1/client-cert-signed -days 365 -CAcreateserial -passin pass:<server_password>
    ```

1. Ga naar de clientcomputer (hn1) en navigeer naar de `~/ssl` map. Kopieer het ondertekende certificaat naar de client-computer.

    ```bash
    #copy signed cert to client machine
    $scp -i ~/kafka-security.pem sshuser@wn0-umakaf:/tmp1/client-cert-signed

    #copy signed cert to client machine
    $scp -i ~/kafka-security.pem sshuser@wn0-umakaf:/home/sshuser/ssl/ca-cert

    #Import CA cert to trust store 
    $keytool -keystore kafka.client.truststore.jks -alias CARoot -import -file ca-cert -storepass $CLIPASS -keypass $CLIPASS -noprompt

    #Import CA cert to key store
    $keytool -keystore kafka.client.keystore.jks -alias CARoot -import -file ca-cert -storepass $CLIPASS -keypass $CLIPASS -noprompt

    #Import signed client (cert client-cert-signed1) to keystore
    $keytool -keystore kafka.client.keystore.jks -import -file client-cert-signed -alias my-local-pc1 -storepass $CLIPASS -keypass $CLIPASS -noprompt
    ```

1. Bekijk het bestand `client-ssl-auth.properties` met de opdracht `$cat client-ssl-auth.properties`. Het moet beschikken over de volgende regels:

    ```bash
    security.protocol=SSL
    ssl.truststore.location=/home/sshuser/ssl/kafka.client.truststore.jks
    ssl.truststore.password=<client_password>
    ssl.keystore.location=/home/sshuser/ssl/kafka.client.keystore.jks
    ssl.keystore.password=<client_password>
    ssl.key.password=<client_password>
    ```

## <a name="client-setup-without-authentication"></a>Installatie van de client (zonder verificatie)

1. Exporteer het wachtwoord van de client. Vervang `<client_password>` met de werkelijke beheerderswachtwoord op de clientcomputer Kafka.

    ```bash
    $export CLIPASS=<client_password>
    $cd ssl
    ```

1. Ga naar de clientcomputer (hn1) en navigeer naar de `~/ssl` map. Kopieer het ondertekende certificaat naar de client-computer.

    ```bash
    #copy signed cert to client machine
    $scp -i ~/kafka-security.pem sshuser@wn0-umakaf:/home/sshuser/ssl/ca-cert .

    #NOW IMPORT CA cert to trust store
    $keytool -keystore kafka.client.truststore.jks -alias CARoot -import -file ca-cert -storepass $CLIPASS -keypass $CLIPASS -noprompt

    #Import CA cert to key store
    $keytool -keystore kafka.client.keystore.jks -alias CARoot -import -file ca-cert -storepass $CLIPASS -keypass $CLIPASS -noprompt
    ```

1. Bekijk het bestand `client-ssl-auth.properties` met de opdracht `$cat client-ssl-auth.properties`. Het moet beschikken over de volgende regels:

    ```bash
    security.protocol=SSL
    ssl.truststore.location=/home/sshuser/ssl/kafka.client.truststore.jks
    ssl.truststore.password=<client_password>
    ```

## <a name="next-steps"></a>Volgende stappen

* [Wat is Apache Kafka in HDInsight?](/../azure/hdinsight/kafka/apache-kafka-introduction)