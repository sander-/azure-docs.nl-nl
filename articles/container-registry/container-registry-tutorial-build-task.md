---
title: 'Zelfstudie: builds van containerinstallatiekopieën automatiseren - Azure Container Registry-taken'
description: In deze zelfstudie leert u hoe u een Azure Container Registry-taak configureert om builds van containerinstallatiekopieën automatisch te activeren in de cloud wanneer u broncode naar een Git-opslagplaats doorvoert.
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: tutorial
ms.date: 09/24/2018
ms.author: danlep
ms.custom: seodec18, mvc
ms.openlocfilehash: 3dc602589dc3a909ea2a2cf2925d37df0a97605b
ms.sourcegitcommit: c2e61b62f218830dd9076d9abc1bbcb42180b3a8
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/15/2018
ms.locfileid: "53436242"
---
# <a name="tutorial-automate-container-image-builds-in-the-cloud-when-you-commit-source-code"></a>Zelfstudie: builds van containerinstallatiekopieën in de cloud automatiseren bij het doorvoeren van broncode

Naast een [quick-taak](container-registry-tutorial-quick-task.md) biedt ACR Tasks ondersteuning voor geautomatiseerde builds van Docker-containerinstallatiekopieën met de *build-taak*. In deze zelfstudie leert u hoe u de Azure CLI gebruikt om een taak te maken die builds van installatiekopieën automatisch activeert in de cloud wanneer u broncode naar een Git-opslagplaats doorvoert.

In deze zelfstudie, het tweede deel in de serie, leert u het volgende:

> [!div class="checklist"]
> * Een taak maken
> * De taak testen
> * Taakstatus weergeven
> * De taak activeren met een code-doorvoer

In deze zelfstudie wordt ervan uitgegaan dat u de stappen in de [vorige zelfstudie](container-registry-tutorial-quick-task.md) hebt voltooid. Als u dit nog niet hebt gedaan, voert u de stappen in de sectie [Vereisten](container-registry-tutorial-quick-task.md#prerequisites) van de vorige zelfstudie uit voordat u doorgaat.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u de Azure CLI lokaal wilt gebruiken, moet u Azure CLI versie **2.0.46** of hoger hebben geïnstalleerd  en zijn aangemeld met [az login][az-login]. Voer `az --version` uit om de versie te bekijken. Als u de CLI wilt installeren of upgraden, raadpleegt u [Azure CLI installeren][azure-cli].

## <a name="prerequisites"></a>Vereisten

### <a name="get-sample-code"></a>Voorbeeldcode ophalen

In deze zelfstudie wordt ervan uitgegaan dat u de stappen in de [vorige zelfstudie](container-registry-tutorial-quick-task.md) hebt voltooid en dat u de voorbeeldopslagplaats hebt gesplitst en gekloond. Als u dit nog niet hebt gedaan, voert u de stappen in de sectie [Vereisten](container-registry-tutorial-quick-task.md#prerequisites) van de vorige zelfstudie uit voordat u doorgaat.

### <a name="container-registry"></a>Containerregister

U moet een Azure-containerregister in uw Azure-abonnement hebben om deze zelfstudie te voltooien. Als u een register nodig hebt, raadpleegt u de [vorige zelfstudie](container-registry-tutorial-quick-task.md) of [Quickstart: een containerregister maken met de Azure-CLI](container-registry-get-started-azure-cli.md).

## <a name="overview-of-acr-tasks"></a>Overzicht van de ACR-taken

Een taak definieert de eigenschappen van een geautomatiseerde build, met inbegrip van de locatie van de broncode van de containerinstallatiekopie en de gebeurtenis die de build activeert. Als een in de taak gedefinieerde gebeurtenis optreedt, zoals het doorvoeren van gegevens naar een Git-opslagplaats, initieert ACR Tasks een build van een containerinstallatiekopie in de cloud. Het stuurt dan vervolgens standaard een met succes gebouwde installatiekopie naar het Azure-containerregister dat is opgegeven in de taak.

ACR Tasks ondersteunt momenteel de volgende triggers:

* Doorvoeren naar een Git-opslagplaats
* Basisinstallatiekopieën bijwerken

## <a name="create-a-build-task"></a>Een build-taak maken

In deze sectie maakt u eerst een persoonlijk toegangstoken (PAT) van een GitHub voor gebruik met ACR Tasks. Vervolgens maakt u een taak die een build activeert wanneer code wordt doorgevoerd naar uw fork van de opslagplaats.

### <a name="create-a-github-personal-access-token"></a>Een persoonlijk toegangstoken van GitHub maken

Om een build op een doorvoer naar een Git-opslagplaats te activeren, heeft ACR Tasks een persoonlijk toegangstoken (PAT) nodig voor toegang tot de opslagplaats. Volg deze stappen om een PAT te genereren in GitHub:

1. Navigeer naar de pagina PAT maken op GitHub op https://github.com/settings/tokens/new
1. Geef een korte **beschrijving** voor het token op, bijvoorbeeld 'Demo ACR Tasks'
1. Onder **opslagplaats** schakelt u **opslagplaats:status** en **public_repo** in

   ![Schermafbeelding van de pagina Persoonlijk toegangstoken genereren in GitHub][build-task-01-new-token]

1. Selecteer de knop **Token genereren** (u wordt mogelijk gevraagd om uw wachtwoord te bevestigen)
1. Kopieer en bewaar het gegenereerde token in een **beveiligde locatie** (u gebruikt dit token bij het definiëren van een taak in de volgende sectie)

   ![Schermafbeelding van het gegeneerde persoonlijke toegangstoken in GitHub][build-task-02-generated-token]

### <a name="create-the-build-task"></a>De build-taak maken

Nu u de stappen hebt voltooid die nodig zijn om ACR Tasks in te schakelen om toewijzingsstatus te lezen en webhooks te maken in een opslagplaats, kunt u een taak maken die een build van een containerinstallatiekopie activeert op doorvoeracties naar de opslagplaats.

Vul eerst deze shell-omgevingsvariabelen met waarden die geschikt zijn voor uw omgeving. Hoewel deze stap strikt genomen niet vereist is, vereenvoudigt u hiermee de uitvoering van meerregelige Azure CLI-opdrachten in deze zelfstudie. Als u deze omgevingsvariabelen niet invult, moet u elke bijbehorende waarde handmatig vervangen wanneer deze wordt weergegeven in de voorbeeldopdrachten.

```azurecli-interactive
ACR_NAME=<registry-name>        # The name of your Azure container registry
GIT_USER=<github-username>      # Your GitHub user account name
GIT_PAT=<personal-access-token> # The PAT you generated in the previous section
```

Maak nu de taak door de volgende [az acr task create][az-acr-task-create]-opdracht uit te voeren:

```azurecli-interactive
az acr task create \
    --registry $ACR_NAME \
    --name taskhelloworld \
    --image helloworld:{{.Run.ID}} \
    --context https://github.com/$GIT_USER/acr-build-helloworld-node.git \
    --branch master \
    --file Dockerfile \
    --git-access-token $GIT_PAT
```

> [!IMPORTANT]
> Als u eerder taken hebt gemaakt tijdens de preview met de opdracht `az acr build-task`, moeten deze taken opnieuw worden gemaakt met de opdracht [az acr task][az-acr-task].

Deze taak geeft aan dat elke keer dat code wordt doorgevoerd naar de *master*-vertakking in de opslagplaats zoals is opgegeven door `--context`, ACR Tasks dan de containerinstallatiekopie van de code in die vertakking bouwt. Er wordt gebruikgemaakt van het Dockerfile dat is opgegeven door `--file` vanuit de hoofdmap van de opslagplaats. Het argument `--image` geeft een parameterwaarde van `{{.Run.ID}}` aan voor het versiegedeelte van de tag van de installatiekopie, zodat de gebouwde installatiekopie correleert met een specifieke build en uniek is gelabeld.

De uitvoer van een geslaagde [az acr task create][az-acr-task-create]-opdracht is vergelijkbaar met het volgende:

```console
$ az acr task create \
>     --registry $ACR_NAME \
>     --name taskhelloworld \
>     --image helloworld:{{.Run.ID}} \
>     --context https://github.com/$GIT_USER/acr-build-helloworld-node.git \
>     --branch master \
>     --file Dockerfile \
>     --git-access-token $GIT_PAT
{
  "agentConfiguration": {
    "cpu": 2
  },
  "creationDate": "2018-09-14T22:42:32.972298+00:00",
  "id": "/subscriptions/<Subscription ID>/resourceGroups/myregistry/providers/Microsoft.ContainerRegistry/registries/myregistry/tasks/taskhelloworld",
  "location": "westcentralus",
  "name": "taskhelloworld",
  "platform": {
    "architecture": "amd64",
    "os": "Linux",
    "variant": null
  },
  "provisioningState": "Succeeded",
  "resourceGroup": "myregistry",
  "status": "Enabled",
  "step": {
    "arguments": [],
    "baseImageDependencies": null,
    "contextPath": "https://github.com/gituser/acr-build-helloworld-node",
    "dockerFilePath": "Dockerfile",
    "imageNames": [
      "helloworld:{{.Run.ID}}"
    ],
    "isPushEnabled": true,
    "noCache": false,
    "type": "Docker"
  },
  "tags": null,
  "timeout": 3600,
  "trigger": {
    "baseImageTrigger": {
      "baseImageTriggerType": "Runtime",
      "name": "defaultBaseimageTriggerName",
      "status": "Enabled"
    },
    "sourceTriggers": [
      {
        "name": "defaultSourceTriggerName",
        "sourceRepository": {
          "branch": "master",
          "repositoryUrl": "https://github.com/gituser/acr-build-helloworld-node",
          "sourceControlAuthProperties": null,
          "sourceControlType": "GitHub"
        },
        "sourceTriggerEvents": [
          "commit"
        ],
        "status": "Enabled"
      }
    ]
  },
  "type": "Microsoft.ContainerRegistry/registries/tasks"
}
```

## <a name="test-the-build-task"></a>De build-taak testen

U hebt nu een taak die uw build definieert. Als u de build-pipeline wilt testen, activeert u een build handmatig door de opdracht [az acr task run][az-acr-task-run] uit te voeren:

```azurecli-interactive
az acr task run --registry $ACR_NAME --name taskhelloworld
```

Met de opdracht `az acr task run` streamt u standaard de logboekuitvoer naar de console wanneer u de opdracht uitvoert.

```console
$ az acr task run --registry $ACR_NAME --name taskhelloworld

2018/09/17 22:51:00 Using acb_vol_9ee1f28c-4fd4-43c8-a651-f0ed027bbf0e as the home volume
2018/09/17 22:51:00 Setting up Docker configuration...
2018/09/17 22:51:02 Successfully set up Docker configuration
2018/09/17 22:51:02 Logging in to registry: myregistry.azurecr.io
2018/09/17 22:51:03 Successfully logged in
2018/09/17 22:51:03 Executing step: build
2018/09/17 22:51:03 Obtaining source code and scanning for dependencies...
2018/09/17 22:51:05 Successfully obtained source code and scanned for dependencies
Sending build context to Docker daemon  23.04kB
Step 1/5 : FROM node:9-alpine
9-alpine: Pulling from library/node
Digest: sha256:8dafc0968fb4d62834d9b826d85a8feecc69bd72cd51723c62c7db67c6dec6fa
Status: Image is up to date for node:9-alpine
 ---> a56170f59699
Step 2/5 : COPY . /src
 ---> 5f574fcf5816
Step 3/5 : RUN cd /src && npm install
 ---> Running in b1bca3b5f4fc
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN helloworld@1.0.0 No repository field.

up to date in 0.078s
Removing intermediate container b1bca3b5f4fc
 ---> 44457db20dac
Step 4/5 : EXPOSE 80
 ---> Running in 9e6f63ec612f
Removing intermediate container 9e6f63ec612f
 ---> 74c3e8ea0d98
Step 5/5 : CMD ["node", "/src/server.js"]
 ---> Running in 7382eea2a56a
Removing intermediate container 7382eea2a56a
 ---> e33cd684027b
Successfully built e33cd684027b
Successfully tagged myregistry.azurecr.io/helloworld:da2
2018/09/17 22:51:11 Executing step: push
2018/09/17 22:51:11 Pushing image: myregistry.azurecr.io/helloworld:da2, attempt 1
The push refers to repository [myregistry.azurecr.io/helloworld]
4a853682c993: Preparing
[...]
4a853682c993: Pushed
[...]
da2: digest: sha256:c24e62fd848544a5a87f06ea60109dbef9624d03b1124bfe03e1d2c11fd62419 size: 1366
2018/09/17 22:51:21 Successfully pushed image: myregistry.azurecr.io/helloworld:da2
2018/09/17 22:51:21 Step id: build marked as successful (elapsed time in seconds: 7.198937)
2018/09/17 22:51:21 Populating digests for step id: build...
2018/09/17 22:51:22 Successfully populated digests for step id: build
2018/09/17 22:51:22 Step id: push marked as successful (elapsed time in seconds: 10.180456)
The following dependencies were found:
- image:
    registry: myregistry.azurecr.io
    repository: helloworld
    tag: da2
    digest: sha256:c24e62fd848544a5a87f06ea60109dbef9624d03b1124bfe03e1d2c11fd62419
  runtime-dependency:
    registry: registry.hub.docker.com
    repository: library/node
    tag: 9-alpine
    digest: sha256:8dafc0968fb4d62834d9b826d85a8feecc69bd72cd51723c62c7db67c6dec6fa
  git:
    git-head-revision: 68cdf2a37cdae0873b8e2f1c4d80ca60541029bf


Run ID: da2 was successful after 27s
```

## <a name="trigger-a-build-with-a-commit"></a>Een build activeren met een doorvoer

Nu u de taak hebt getest door deze handmatig uit te voeren, gaat u deze automatisch activeren met een wijziging in de broncode.

Controleer eerst of u zich bevindt in de map waarin de lokale kloon van de [opslagplaats][sample-repo] staat:

```azurecli-interactive
cd acr-build-helloworld-node
```

Voer vervolgens de volgende opdrachten uit om een nieuw bestand te maken, door te voeren en pushen naar uw fork van de opslagplaats op GitHub:

```azurecli-interactive
echo "Hello World!" > hello.txt
git add hello.txt
git commit -m "Testing ACR Tasks"
git push origin master
```

U wordt mogelijk gevraagd om uw GitHub-referenties op te geven wanneer u de opdracht `git push` uitvoert. Geef uw GitHub-gebruikersnaam op en voer het persoonlijke toegangstoken (PAT) in dat u eerder hebt gemaakt voor het wachtwoord.

```console
$ git push origin master
Username for 'https://github.com': <github-username>
Password for 'https://githubuser@github.com': <personal-access-token>
```

Zodra u een doorvoer naar de opslagplaats hebt gepusht, wordt de webhook die is gemaakt door ACE Tasks geactiveerd en wordt een build in Azure Container Registry in gang gezet. Geef de logboeken weer voor de taak die momenteel wordt uitgevoerd om de voortgang van de build te verifiëren en controleren:

```azurecli-interactive
az acr task logs --registry $ACR_NAME
```

De uitvoer is vergelijkbaar met de volgende, waarin de op dit moment uitgevoerde (of de laatst uitgevoerde) taak wordt getoond:

```console
$ az acr task logs --registry $ACR_NAME
Showing logs of the last created run.
Run ID: da4

[...]

Run ID: da4 was successful after 38s
```

## <a name="list-builds"></a>Builds weergeven

Voor een overzicht van de taken die ACR Tasks heeft voltooid voor het register, voert u de opdracht [az acr task-list-runs][az-acr-task-list-runs] uit:

```azurecli-interactive
az acr task list-runs --registry $ACR_NAME --output table
```

De uitvoer van de opdracht ziet er ongeveer als volgt uit. De runs die ACR Tasks heeft uitgevoerd, worden weergegeven. 'Git Commit' wordt weergegeven in de kolom TRIGGER voor de meest recente taak:

```console
$ az acr task list-runs --registry $ACR_NAME --output table

RUN ID    TASK             PLATFORM    STATUS     TRIGGER     STARTED               DURATION
--------  --------------  ----------  ---------  ----------  --------------------  ----------
da4       taskhelloworld  Linux       Succeeded  Git Commit  2018-09-17T23:03:45Z  00:00:44
da3       taskhelloworld  Linux       Succeeded  Manual      2018-09-17T22:55:35Z  00:00:35
da2       taskhelloworld  Linux       Succeeded  Manual      2018-09-17T22:50:59Z  00:00:32
da1                       Linux       Succeeded  Manual      2018-09-17T22:29:59Z  00:00:57
```

## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie leert u hoe u een taak gebruikt om builds van containerinstallatiekopieën automatisch te activeren in Azure wanneer u broncode naar een Git-opslagplaats doorvoert. Ga verder naar de volgende zelfstudie voor informatie over het maken van taken die builds activeren wanneer de basisinstallatiekopie van de containerinstallatiekopie wordt bijgewerkt.

> [!div class="nextstepaction"]
> [Builds automatiseren op basis van installatiekopie-update](container-registry-tutorial-base-image-update.md)

<!-- LINKS - External -->
[sample-repo]: https://github.com/Azure-Samples/acr-build-helloworld-node

<!-- LINKS - Internal -->
[azure-cli]: /cli/azure/install-azure-cli
[az-acr-task]: /cli/azure/acr#az-acr-task
[az-acr-task-create]: /cli/azure/acr#az-acr-task-create
[az-acr-task-run]: /cli/azure/acr#az-acr-task-run
[az-acr-task-list-runs]: /cli/azure/acr#az-acr-task-list-runs
[az-login]: /cli/azure/reference-index#az-login

<!-- IMAGES -->
[build-task-01-new-token]: ./media/container-registry-tutorial-build-tasks/build-task-01-new-token.png
[build-task-02-generated-token]: ./media/container-registry-tutorial-build-tasks/build-task-02-generated-token.png
