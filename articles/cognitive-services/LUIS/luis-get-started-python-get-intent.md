---
title: Intentie ophalen, Python
titleSuffix: Language Understanding - Azure Cognitive Services
description: In deze snelstart leest u hoe u utterances doorgeeft aan een LUIS-eindpunt en intenties en entiteiten terugkrijgt.
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.component: language-understanding
ms.topic: quickstart
ms.date: 09/10/2018
ms.author: diberry
ms.openlocfilehash: e4601b5b6156ace897df65cd42159a1193f8194a
ms.sourcegitcommit: 9fb6f44dbdaf9002ac4f411781bf1bd25c191e26
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/08/2018
ms.locfileid: "53100120"
---
# <a name="quickstart-get-intent-using-python"></a>Snelstart: Intentie ophalen met behulp van Python
In deze snelstart leest u hoe u utterances doorgeeft aan een LUIS-eindpunt en intenties en entiteiten terugkrijgt.

[!INCLUDE [Quickstart introduction for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-intro-para.md)]

## <a name="prerequisites"></a>Vereisten

* [Python 3.6](https://www.python.org/downloads/) of later.
* [Visual Studio Code](https://code.visualstudio.com/)

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-luis-repo-note.md)]

## <a name="get-luis-key"></a>LUIS-sleutel ophalen

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-get-key-para.md)]

## <a name="get-intent-with-browser"></a>De intentie via een browser ophalen

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-browser-para.md)]

## <a name="get-intent--programmatically"></a>De intentie programmatisch ophalen

U kunt Python gebruiken voor toegang tot de resultaten die u in het browservenster in de vorige stap hebt gezien.

1. Kopieer een van de volgende codefragmenten naar een bestand met de naam `quickstart-call-endpoint.py`:

   [!code-python[Console app code that calls a LUIS endpoint for Python 2.7](~/samples-luis/documentation-samples/quickstarts/analyze-text/python/2.x/quickstart-call-endpoint-2-7.py)]

   [!code-python[Console app code that calls a LUIS endpoint for Python 3.6](~/samples-luis/documentation-samples/quickstarts/analyze-text/python/3.x/quickstart-call-endpoint-3-6.py)]

2. Vervang de waarde van het veld `Ocp-Apim-Subscription-Key` door de sleutel van uw LUIS-eindpunt.

3. Installeer afhankelijkheden met `pip install requests`.

4. Voer het script uit met behulp van `python ./quickstart-call-endpoint.py`. De uitvoer bestaat uit de JSON die u eerder hebt gezien in het browservenster.

## <a name="luis-keys"></a>LUIS-sleutels

[!INCLUDE [Use authoring key for endpoint](../../../includes/cognitive-services-luis-qs-endpoint-key-usage-para.md)]

## <a name="clean-up-resources"></a>Resources opschonen
Verwijder het Python-bestand. 

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Utterances toevoegen](luis-get-started-python-add-utterance.md)
