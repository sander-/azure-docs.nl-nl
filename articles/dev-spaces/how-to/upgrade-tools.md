---
title: Upgrade uitvoeren van hulpprogramma's voor Azure Dev Spaces | Microsoft Docs
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.component: azds-kubernetes
author: zr-msft
ms.author: zarhoads
ms.date: 07/03/2018
ms.topic: article
ms.technology: azds-kubernetes
description: Snelle Kubernetes-ontwikkeling met containers en microservices in Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure-Containerservice, containers
ms.openlocfilehash: 3d7e82903400d8aab0d33628af2b404583cb42a7
ms.sourcegitcommit: 275eb46107b16bfb9cf34c36cd1cfb000331fbff
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/15/2018
ms.locfileid: "51706346"
---
# <a name="how-to-upgrade-azure-dev-spaces-tools"></a>Upgrade uitvoeren van hulpprogramma's voor Azure Dev Spaces

Als er een nieuwe versie is en u gebruikt al Azure Dev Spaces, dan moet u mogelijk uw clienthulpprogramma's voor Azure Dev Spaces upgraden.

## <a name="update-the-azure-cli"></a>Bijwerken van de Azure CLI

Als u de nieuwste Azure CLI hebt bijgewerkt, krijgt u ook de meest recente versie van de Dev Spaces CLI-extensie.

U hoeft de vorige versie niet te verwijderen, maar slechts de juiste download te vinden op [Azure CLI](/cli/azure/install-azure-cli?view=azure-cli-latest).


## <a name="update-the-dev-spaces-cli-extension-and-command-line-tools"></a>Bijwerken van de Dev Spaces CLI-extensie en de opdrachtregelprogramma's

Voer de volgende opdracht uit:

```cmd
az aks use-dev-spaces -n <your-aks-cluster> -g <your-aks-cluster-resource-group> --update
```

## <a name="update-the-vs-code-extension"></a>Bijwerken van de VS Code-extensie

Eenmaal geïnstalleerd wordt de extensie automatisch bijgewerkt. U moet mogelijk de extensie opnieuw laden voor het gebruik van de nieuwe functies. Open in Visual Studio Code, in het deelvenster **extensies** kies de **Azure Dev Spaces** extensies, en kies **opnieuw laden**.

## <a name="update-the-visual-studio-extension"></a>De Visual Studio-extensie bijwerken

Zoals met andere extensies en updates, toont Visual Studio een melding wanneer er een update beschikbaar is voor de Visual Studio Tools voor Kubernetes, waar Azure Dev Spaces onderdeel van is. Zoek naar een vlagpictogram in de rechterbovenhoek van het scherm.

Voor het bijwerken van de hulpprogramma's in Visual Studio, kiest u de **Extra > extensies en Updates** menu item en aan de linkerkant, kies **Updates**. Zoek **Visual Studio-hulpprogramma's voor Kubernetes** en kies de **Update** knop.

## <a name="next-steps"></a>Volgende stappen

Test de nieuwe hulpprogramma's door een nieuw cluster te maken. Probeer de snelstartgidsen en zelfstudies op [Azure Dev Spaces](/azure/dev-spaces).

> [!WARNING]
> Azure Dev Spaces in bestaande clusters worden niet onmiddellijk de bijgewerkt, dus om er zeker van zijn dat u de meest recente versie gebruikt op al uw Azure-implementaties, maakt u een nieuw cluster na de upgrade van de hulpprogramma's.
