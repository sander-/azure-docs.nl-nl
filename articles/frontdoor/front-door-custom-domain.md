---
title: Zelfstudie - Een aangepast domein toevoegen aan uw Azure Front Door-configuratie| Microsoft Docs
description: In deze zelfstudie leert u hoe u een aangepast domein aan Azure Front Door kunt toevoegen.
services: frontdoor
documentationcenter: ''
author: sharad4u
editor: ''
ms.service: frontdoor
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 09/10/2018
ms.author: sharadag
ms.openlocfilehash: 0e1c5e4c3e4b40fd04ca9d48aba9b1e5194d4261
ms.sourcegitcommit: dede0c5cbb2bd975349b6286c48456cfd270d6e9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/16/2019
ms.locfileid: "54330922"
---
# <a name="tutorial-add-a-custom-domain-to-your-front-door"></a>Zelfstudie: Een aangepast domein aan uw Front Door toevoegen
In deze zelfstudie ziet u hoe u een aangepast domein aan uw Front Door kunt toevoegen. Als u Azure Front Door Service gebruikt voor het leveren van toepassingen, is een aangepast domein nodig als u wilt dat uw eigen domeinnaam zichtbaar is in de aanvraag van uw eindgebruiker. Een zichtbare domeinnaam kan handig zijn voor uw klanten en nuttig zijn voor branding-doelen.

Nadat u een Front Door maakt, wordt standaard de front-endhost,(een subdomein van `azurefd.net`) in de URL opgenomen voor het leveren van Front Door-inhoud van uw back-end (bijvoorbeeld https:\//contoso.azurefd.net/activeusers.htm). Voor uw gemak biedt Azure Front Door de mogelijkheid om een aangepast domein te koppelen met een standaardhost. Met deze optie levert u uw inhoud met een aangepast domein in uw URL in plaats van een domeinnaam die eigendom is van Front Door (bijvoorbeeld https:\//www.contoso.com/photo.png). 

In deze zelfstudie leert u het volgende:
> [!div class="checklist"]
> - Een CNAME DNS-record maken.
> - Het aangepaste domein koppelen aan uw Front Door.
> - Het aangepaste domein verifiëren.

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Vereisten

Voordat u de stappen in deze zelfstudie kunt voltooien, moet u een Front Door maken. Zie voor meer informatie [Quickstart: Een Front Door maken](quickstart-create-front-door.md).

Als u nog geen aangepast domein hebt, moet u er eerst een aanschaffen bij een domeinprovider. Zie bijvoorbeeld [Een aangepaste domeinnaam kopen](https://docs.microsoft.com/azure/app-service/manage-custom-dns-buy-domain).

Als u van Azure gebruikmaakt voor het hosten van uw [DNS-domeinen](https://docs.microsoft.com/azure/dns/dns-overview), moet u het domeinnaam-systeem van de domeinprovider (DNS) naar een Azure DNS overdragen. Zie [Delegate a domain to Azure DNS](https://docs.microsoft.com/azure/dns/dns-delegate-domain-azure-dns) (Een domein aan Azure DNS overdragen) voor meer informatie. Als u van een domeinprovider gebruikmaakt voor het afhandelen van uw DNS-domein, gaat u verder met [Een DNS CNAME-record maken](#create-a-cname-dns-record).


## <a name="create-a-cname-dns-record"></a>Een CNAME DNS-record maken

Voordat u een aangepast domein met uw Front Door kunt gebruiken, moet u eerst een record met een canonieke naam (CNAME) maken bij uw domeinprovider om te verwijzen naar de standaard front-endhost van uw Front Door (bijvoorbeeld contoso.azurefd.net). Een CNAME-record is een soort DNS-record dat een brondomeinnaam toewijst aan een doeldomeinnaam. De domeinnaam van de bron is uw aangepaste domeinnaam voor Azure Front Door Service en de domeinnaam van het doel is de standaardhostnaam van uw Front Door. Nadat Front Door het CNAME-record controleert dat u maakt, wordt verkeer dat is geadresseerd aan het aangepaste brondomein (zoals www.contoso.com) gerouteerd naar de opgegeven bestemming met standaard front-endhost van uw Front Door (zoals contoso.azureedge.net). 

Een aangepast domein en het subdomein kunnen worden slechts aan één Front Door tegelijk worden gekoppeld. U kunt echter verschillende subdomeinen uit het aangepaste domein gebruiken voor verschillende Front Doors met behulp van meerdere CNAME-records. U kunt ook een aangepast domein met verschillende subdomeinen toewijzen aan dezelfde Front Door.


## <a name="map-the-temporary-afdverify-sub-domain"></a>Het tijdelijke onderliggende afdverify-domein toewijzen

Wanneer u een bestaand domein toewijst dat in productie is genomen, zijn er speciale overwegingen. Terwijl u uw aangepaste domein in het Azure Portal registreert, kan een korte periode van uitvaltijd voor het domein optreden. Om te voorkomen dat het webverkeer wordt onderbroken, moet u eerst uw aangepaste domein aan de standaard frond-endhost van uw Front Door het Azure afdverify-subdomein toewijzen om een tijdelijke CNAME-toewijzing te maken. Met deze methode kunnen gebruikers zonder onderbreking toegang krijgen tot uw domein terwijl de DNS-toewijzing wordt uitgevoerd.

U kunt ook uw aangepaste domein rechtstreeks aan uw Front Door toewijzen, als u uw aangepaste domein voor het eerst gebruikt en er geen productieverkeer op wordt uitgevoerd. Ga door naar [Permanent aangepast domein toewijzen](#map-the-permanent-custom-domain).

Om een CNAME-record te maken met het afdverify-subdomein:

1. Meld u aan bij de website van de domeinprovider voor uw aangepaste domein.

2. Zoek de pagina voor het beheren van DNS-records door de documentatie van de provider te raadplegen, of te zoeken naar gebieden van de website met het label **Domeinnaam**, **DNS**, of **Serverbeheernaam**. 

3. Maak een CNAME-record vermelding voor uw aangepaste domein en vul de velden in, zoals wordt weergegeven in de volgende tabel (veldnamen kunnen verschillen):

    | Bron                    | Type  | Doel                     |
    |---------------------------|-------|---------------------------------|
    | afdverify.www.contoso.com | CNAME | afdverify.contoso.azurefd.net |

    - Bron: Voer de naam van uw aangepaste domein, met inbegrip van het subdomein afdverify, in de volgende indeling in: afdverify._&lt;aangepaste domeinnaam&gt;_. Bijvoorbeeld afdverify.www.contoso.com.

    - Type: Voer *CNAME* in.

    - Bestemming: Voer uw standaard front-endhost voor Front Door, inclusief de afdverify-subdomein, in de volgende indeling in: afdverify._&lt;naam van eindpunt&gt;_.azurefd.net. Bijvoorbeeld afdverify.contoso.azurefd.net.

4. Sla uw wijzigingen op.

Bijvoorbeeld: de procedure voor de registrar van een GoDaddy-domein is als volgt:

1. Meld u aan en selecteer het aangepaste domein dat u wilt gebruiken.

2. Selecteer in de sectie Domeinen **Alle beheren**, selecteer daarna **DNS** | **Zones beheren**.

3. Voer bij **Domeinnaam** uw aangepaste domein in en selecteer **Zoeken**.

4. Selecteer op de pagina **DNS-beheer** **toevoegen**, selecteer daarna **CNAME** in de **Type**-lijst.

5. Vul de volgende velden van het CNAME-item in:

    - Type: Laat *CNAME* geselecteerd.

    - Host: Voer het subdomein in van uw aangepaste domein dat moet worden gebruikt, met inbegrip van de naam van het afdverify-subdomein. Bijvoorbeeld afdverify.www.

    - Verwijst naar: Voer de hostnaam van uw standaard front-endhost voor Front Door in, inclusief de afdverify-subdomeinnaam. Bijvoorbeeld afdverify.contoso.azurefd.net. 

    - TTL: Laat *1 uur* geselecteerd.

6. Selecteer **Opslaan**.
 
    De CNAME-vermelding wordt toegevoegd aan de tabel DNS-records.


## <a name="associate-the-custom-domain-with-your-front-door"></a>Het aangepaste domein koppelen aan uw Front Door

Nadat u uw aangepaste domein hebt geregistreerd, kunt u dit toevoegen aan uw Front Door.

1. Meld u aan bij de [Azure Portal](https://portal.azure.com/) en blader naar de Front Door met de front-endhost die u wilt toewijzen aan een aangepast domein.
    
2. Klik op de pagina **Front Door-ontwerper** op ‘+’ om een aangepast domein toe te voegen.
    
3. Geef **Aangepast domein** op. 

4. Bij **Front-endhost** staat de front-endhost die als bestemmingsdomein van uw CNAME-record moet worden gebruikt, al ingevuld op basis van uw Front Door: *&lt;standaardhostnaam&gt;*.azurefd.net. De naam kan niet worden gewijzigd.

5. Bij **Aangepaste hostnaam** voert u de naam van uw aangepaste domein in, inclusief het subdomein, om dit te gebruiken als het brondomein van uw CNAME-record. Bijvoorbeeld: www.contoso.com of cdn.contoso.com. Gebruik niet de naam van het afdverify-subdomein.

6. Selecteer **Toevoegen**.

   Azure controleert of het CNAME-record bestaat dat u voor de domeinnaam hebt ingevoerd. Als de CNAME juist is, wordt uw aangepaste domein gevalideerd.

>[!WARNING]
> U **moet** zorgen dat alle front-endhosts (inclusief aangepaste domeinen) in uw Front Door een regel voor doorsturen hebben waaraan een standaardpad (‘/\*’) is gekoppeld. Er moet dus in al uw regels voor doorsturen minimaal een routeringsregel voor al uw front-endhosts op het standaardpad (‘/\*’) zijn gedefinieerd. Als dit niet het geval is, kan dit tot gevolg hebben dat het verkeer van uw eindgebruikers niet goed wordt gerouteerd.

## <a name="verify-the-custom-domain"></a>Het aangepaste domein verifiëren

Nadat u de registratie van uw aangepaste domein hebt voltooid, controleert u of het aangepaste domein verwijst naar uw standaard front-endhost van uw Front Door.
 
Ga naar het adres van het bestand met behulp van het aangepaste domein in uw browser. Bijvoorbeeld, als uw aangepaste domein robotics.contoso.com is, moet de URL naar het bestand in de cache moet vergelijkbaar zijn met de volgende URL: http:\//robotics.contoso.com/my-public-container/my-file.jpg. Controleer of het resultaat hetzelfde is als wanneer u de Front Door rechtstreeks benadert via *&lt;Front Door-host&gt;*.azurefd.net.


## <a name="map-the-permanent-custom-domain"></a>Permanent aangepast domein toewijzen

Als u hebt gecontroleerd dat het subdomein afdverify met succes is toegewezen aan uw Front Door (of als u een nieuwe aangepast gebruikt domein dat niet in productie is), kunt u vervolgens het aangepaste domein rechtstreeks toewijzen aan de  standaard front-endhost van uw Front Door.

Maken van een CNAME-record voor uw aangepaste domein:

1. Meld u aan bij de website van de domeinprovider voor uw aangepaste domein.

2. Zoek de pagina voor het beheren van DNS-records door de documentatie van de provider te raadplegen, of te zoeken naar gebieden van de website met het label **Domeinnaam**, **DNS**, of **Serverbeheernaam**. 

3. Maak een CNAME-record vermelding voor uw aangepaste domein en vul de velden in, zoals wordt weergegeven in de volgende tabel (veldnamen kunnen verschillen):

    | Bron          | Type  | Doel           |
    |-----------------|-------|-----------------------|
    | www.contoso.com | CNAME | contoso.azurefd.net |

    - Bron: Voer de naam in van uw aangepaste domein (bijvoorbeeld www.contoso.com).

    - Type: Voer *CNAME* in.

    - Bestemming: Voer de standaard front-endhost van uw Front Door in. Deze moet de volgende indeling hebben:_&lt;hostnaam&gt;_. azureedge.net. Bijvoorbeeld contoso.azurefd.net.

4. Sla uw wijzigingen op.

5. Als u eerder een tijdelijk afdverify-subdomein CNAME-record hebt gemaakt, moet u dit verwijderen. 

6. Als u dit aangepaste domein voor het eerst in de productieomgeving gebruikt, volg dan de stappen voor [Het aangepaste domein koppelen aan uw Front Door](#associate-the-custom-domain-with-your-front-door) en [Het aangepaste domein verifiëren](#verify-the-custom-domain).

Bijvoorbeeld: de procedure voor de registrar van een GoDaddy-domein is als volgt:

1. Meld u aan en selecteer het aangepaste domein dat u wilt gebruiken.

2. Selecteer in de sectie Domeinen **Alle beheren**, selecteer daarna **DNS** | **Zones beheren**.

3. Voer bij **Domeinnaam** uw aangepaste domein in en selecteer **Zoeken**.

4. Selecteer op de pagina **DNS-beheer** **toevoegen**, selecteer daarna **CNAME** in de **Type**-lijst.

5. Vul de volgende velden van de CNAME-vermelding in:

    - Type: Laat *CNAME* geselecteerd.

    - Host: Voer het subdomein van uw aangepaste domein in dat u wilt gebruiken. Bijvoorbeeld www of profiel.

    - Verwijst naar: Voer de standaardhostnaam in van uw Front Door. Bijvoorbeeld contoso.azurefd.net. 

    - TTL: Laat *1 uur* geselecteerd.

6. Selecteer **Opslaan**.
 
    De CNAME-vermelding wordt toegevoegd aan de tabel DNS-records.

7. Als u een afdverify CNAME-record hebt, selecteer dan het potloodpictogram ernaast en daarna het prullenbak-pictogram.

8. Selecteer **Verwijderen** om het CNAME-record te verwijderen.


## <a name="clean-up-resources"></a>Resources opschonen

In de voorgaande stappen hebt u een aangepast domein toegevoegd aan een Front Door. Als u uw Front Door niet langer met een aangepast domein wilt koppelen, kunt u het aangepaste domein verwijderen door deze stappen uit te voeren:
 
1. Selecteer in uw Front Door-ontwerper het aangepaste domein dat u wilt verwijderen.

2. Klik in het contextmenu voor het aangepaste domein op Verwijderen.  

   Het aangepaste domein is ontkoppeld van het eindpunt.


## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie heeft u het volgende geleerd:

> [!div class="checklist"]
> - Een CNAME DNS-record maken.
> - Het aangepaste domein koppelen aan uw Front Door.
> - Het aangepaste domein verifiëren.