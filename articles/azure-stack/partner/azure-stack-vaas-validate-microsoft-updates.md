---
title: Software-updates van Microsoft in Azure Stack-validatie als een Service valideren | Microsoft Docs
description: Informatie over het valideren van software-updates van Microsoft met validatie als een Service.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 1/14/2019
ms.author: mabrigg
ms.reviewer: johnhas
ROBOTS: NOINDEX
ms.openlocfilehash: bcb56789b2781cd1d081af8c112222a1f1269a74
ms.sourcegitcommit: 70471c4febc7835e643207420e515b6436235d29
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 01/15/2019
ms.locfileid: "54304887"
---
# <a name="validate-software-updates-from-microsoft"></a>Valideren van software-updates van Microsoft

[!INCLUDE [Azure_Stack_Partner](./includes/azure-stack-partner-appliesto.md)]

Microsoft brengt regelmatig updates voor de Azure Stack-software. Deze updates zijn bedoeld om Azure Stack coengineering partners. De updates zijn opgegeven in vooraf van openbaar beschikbaar. U kunt de updates op basis van uw oplossing controleren en feedback naar Microsoft.

[!INCLUDE [azure-stack-vaas-workflow-validation-completion](includes/azure-stack-vaas-workflow-validation-completion.md)]

## <a name="apply-monthly-update"></a>Maandelijkse update van toepassing

[!INCLUDE [azure-stack-vaas-workflow-section_update-azs](includes/azure-stack-vaas-workflow-section_update-azs.md)]

## <a name="create-a-workflow"></a>Een werkstroom maken

Update validaties gebruiken dezelfde werkstroom als **oplossing validatie**.

## <a name="run-tests"></a>Tests uitvoeren

1. Update validaties gebruiken dezelfde werkstroom als **oplossing validatie**. 

2. Volg de instructies op [oplossing validatie uitvoeren test](azure-stack-vaas-validate-oem-package.md#run-package-validation-tests). Selecteer in plaats daarvan de volgende tests:
    - Maandelijks Azure Stack-Update-verificatie
    - Engine voor cloud-simulatie

U hoeft niet te pakket zich voor validaties update aanvragen.

## <a name="next-steps"></a>Volgende stappen

- [Controleren en beheren van tests in de portal VaaS](azure-stack-vaas-monitor-test.md)