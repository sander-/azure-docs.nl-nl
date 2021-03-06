---
title: Verklarende woordenlijst - Face-API-Service
titleSuffix: Azure Cognitive Services
description: De verklarende woordenlijst verklaart de termen die u kunt tegenkomen wanneer u met de Face-API-Service werkt.
services: cognitive-services
author: SteveMSFT
manager: cgronlun
ms.service: cognitive-services
ms.component: face-api
ms.topic: conceptual
ms.date: 03/01/2018
ms.author: sbowles
ms.openlocfilehash: 215b780bc403ab2df40567c3eb5a7ae86c9fe130
ms.sourcegitcommit: f10653b10c2ad745f446b54a31664b7d9f9253fe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/18/2018
ms.locfileid: "46127360"
---
# <a name="glossary"></a>Woordenlijst

## <a name="a"></a>A

#### <a name="attributes"></a>Kenmerken

Kenmerken zijn optioneel in de [detectie](#Detection-Face-Detection) resultaten, zoals [leeftijd](#Age-Attribute), [geslacht](#Gender-Attribute), [head houding](#Head-Pose-Attribute), [gezichtshaar](#Facial-Hair-Attribute), [Glimlachende](#Smile-Attribute).
Ze kunnen worden opgehaald van de [detectie](#Detection-Face-Detection) API door de queryparameters op te geven: returnFaceAttributes. Kenmerken voorzien van extra informatie met betrekking tot het geselecteerde [gezichten](#Face); naast de [face ID](#Face-ID) en de [rechthoek](#Face-Rectangle).

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="age-attribute"></a>Leeftijd (kenmerk)

Leeftijd is een van de [kenmerken](#Attributes) met de beschrijving van de leeftijd van een bepaald gezicht. Het leeftijdkenmerk is optioneel in de [detectie](#Detection-Face-Detection) resulteert en kan worden beheerd met een [detectie](#Detection-Face-Detection) aanvraag door de parameter returnFaceAttributes op te geven.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

## <a name="b"></a>B

## <a name="c"></a>C

#### <a name="candidate"></a>Kandidaat

Kandidaten zijn in feite [identificatie](#Identification) resultaten (bijvoorbeeld geïdentificeerde personen en het niveau van vertrouwen in detecties). Een kandidaat wordt vertegenwoordigd door de [PersonID](#Person-ID) en [vertrouwen](#Confidence), waarmee wordt aangegeven dat de persoon die wordt geïdentificeerd met een hoge mate van vertrouwen.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - identificeren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).

#### <a name="confidence"></a>Betrouwbaarheid

Vertrouwen is een meting onthullen de overeenkomsten tussen [gezichten](#Face) of [persoon](#Person) in numerieke waarden, die wordt gebruikt in [identificatie](#Identification), en [ verificatie](#Verification) om aan te geven van de overeenkomsten van de resultaten van gezocht, geïdentificeerd en gecontroleerd.

Raadpleeg voor meer informatie de volgende handleidingen: [Face - Zoek vergelijkbare](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [geconfronteerd - identificeren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [geconfronteerd: controleren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

## <a name="d"></a>D

#### <a name="detectionface-detection"></a>Detectie-/ Gezichtsherkenning

Gezichtsdetectie is de actie van het zoeken naar gezichten in afbeeldingen. Gebruikers kunnen een installatiekopie uploaden of een afbeeldings-URL opgeven in de aanvraag. De gedetecteerde gezichten worden geretourneerd met [face id's](#Face-ID) die wijzen op een unieke identiteit in de Face-API. De rechthoeken de face-locaties in de afbeelding in pixels, evenals de optionele aangeven [kenmerken](#Attributes) voor elk gezicht zoals [leeftijd](#Age-Attribute), [geslacht](#Gender-Attribute), [head houding ](#Head-Pose-Attribute), [gezichtshaar](#Facial-Hair-Attribute) en [Glimlachende](#Smile-Attribute).

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

## <a name="e"></a>E

## <a name="f"></a>F

#### <a name="face"></a>Face

Face is een geïntegreerde term voor de resultaten die zijn afgeleid van de Face-API die zijn gerelateerd aan gedetecteerde gezichten. Uiteindelijk face wordt vertegenwoordigd door de identiteit van een uniforme ([Face ID](#Face-ID)), een bepaald gebied in afbeeldingen ([Gezichtsrechthoek](#Face-Rectangle)), en extra face gerelateerde [kenmerken](#Face-Attributes-Facial-Attributes), zoals [leeftijd](#Age-Attribute), [geslacht](#Gender-Attribute), [oriëntatiepunten](#Face-Landmarks-Facial-Landmarks) en [head houding](#Head-Pose-Attribute). Bovendien gezichten kunnen worden geretourneerd van [detectie](#Detection-Face-Detection).

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="face-api"></a>Face-API

Face-API is een cloud-gebaseerde API biedt de meest geavanceerde algoritmen voor gezichtsdetectie en herkenning. De belangrijkste functionaliteit van de Face-API kan worden onderverdeeld in twee categorieën: face [detectie](#Detection-Face-Detection) met [kenmerken](#Face-Attributes-Facial-Attributes), en face [erkenning](#Recognition).

Raadpleeg voor meer informatie de volgende handleidingen: [Face-API-overzicht](./Overview.md), [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236), [Face - Zoek vergelijkbare](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [geconfronteerd - groep](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238), [Geconfronteerd - identificeren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [geconfronteerd: controleren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

#### <a name="face-attributesfacial-attributes"></a>Face kenmerken/videodetectie kenmerken

Raadpleeg [kenmerken](#Attributes).

#### <a name="face-id"></a>Gezichts-id

Face ID is afgeleid van de [detectie](#Detection-Face-Detection) resultaten, waarin een tekenreeks vertegenwoordigt een [face](#Face) in [Face-API](#Face-API).

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="face-landmarksfacial-landmarks"></a>Oriëntatiepunten/videodetectie Gezichtsoriëntatiepunten

Er zijn oriëntatiepunten optioneel in de [detectie](#Detection-Face-Detection) resultaten; semantische gezichtsherkenning punten, zoals de ogen, nose en mond vandaan te houden (zoals geïllustreerd in de volgende afbeelding). Oriëntatiepunten kunnen worden beheerd met een [detectie](#Detection-Face-Detection) aanvraag door de Booleaanse nummer returnFaceLandmarks. Als returnFaceLandmarks is ingesteld als waar, wordt de geretourneerde gezichten oriëntatiepunt kenmerken hebben.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

![HowToDetectFace](./Images/landmarks.1.jpg)

#### <a name="face-rectangle"></a>Gezichtsrechthoek

Gezichtsrechthoek is afgeleid van de [detectie](#Detection-Face-Detection) resultaten, die een rechtop rechthoek (links, boven, breedte, hoogte) in afbeeldingen in pixels. De linkerbovenhoek van een [face](#Face) (links, top), naast de breedte en hoogte geeft aan dat de face-grootten in x en y-as respectievelijk.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="facial-hair-attribute"></a>Gezichtshaar (kenmerk)

Gezichtshaar is een van de [kenmerken](#Attributes) gebruikt om te beschrijven de gezichtshaar lengte van de beschikbare gezichten. Het kenmerk gezichtshaar is optioneel in de [detectie](#Detection-Face-Detection) resulteert en kan worden beheerd met een [detectie](#Detection-Face-Detection) aanvraag door returnFaceAttributes. Als returnFaceAttributes 'facialHair' bevat, wordt de geretourneerde gezichten gezichtshaar kenmerken hebben.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="facelist"></a>FaceList

FaceList is een verzameling van [PersistedFace](#PersistedFace) en is de maateenheid [Zoek vergelijkbare](#Find-Similar). Een FaceList wordt geleverd met een [FaceList ID](#FaceList-ID), en andere kenmerken zoals [naam](#Name) en [gebruikersgegevens](#UserData-User-Data).

Raadpleeg voor meer informatie de volgende handleidingen: [FaceList - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524b), [FaceList - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524c).

#### <a name="facelist-id"></a>FaceList-ID

FaceList-ID is een door de gebruiker opgegeven-tekenreeks die wordt gebruikt als een id van een [FaceList](#FaceList). De FaceList-ID moet uniek zijn binnen het abonnement.

Raadpleeg voor meer informatie de volgende handleidingen: [FaceList - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524b), [FaceList - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524c).

#### <a name="find-similar"></a>Zoek vergelijkbare

Deze API wordt gebruikt om zoekquery soortgelijke gezichten op basis van een verzameling van gezichten wordt uitgevoerd. Query gezichten en face verzamelingen worden weergegeven als [face id's](#Face-ID) of [FceList ID](#FaceList-ID)/[LargeFaceList ID](#LargeFaceList-ID) in de aanvraag. Geretourneerde resultaten zijn gezochte soortgelijke gezichten, vertegenwoordigd door [face id's](#Face-ID) of [PersistedFace-id's](#PersistedFace-ID).

Raadpleeg voor meer informatie de volgende handleidingen: [Face - Zoek vergelijkbare](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [LargeFaceList - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a157b68d2de3616c086f2cc), [FaceList - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524b).

## <a name="g"></a>G

#### <a name="gender-attribute"></a>Geslacht (kenmerk)

Geslacht is een van de [kenmerken](#Attributes) gebruikt om te beschrijven het geslacht van de beschikbare gezichten. Het kenmerk geslacht is optioneel in de [detectie](#Detection-Face-Detection) resulteert en kan worden beheerd met een [detectie](#Detection-Face-Detection) aanvraag door returnFaceAttributes. Als returnfaceAttributes 'geslacht' bevat, wordt de geretourneerde gezichten geslacht kenmerken hebben.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="grouping"></a>Groeperen

Gezichtsgroepering is de groepering van een verzameling van gezichten wordt uitgevoerd op basis van gezichtsherkenning overeenkomsten. Face verzamelingen worden aangeduid met de face ID verzamelingen in de aanvraag. Als gevolg van groepering, soortgelijke gezichten zijn gegroepeerd als [groepen](#Groups), en gezichten die niet vergelijkbaar met een andere vlak zijn worden samengevoegd als een rommelige groep. Er is op het meest [rommelige groep](#Messy-Group) in het resultaat groepering.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - groep](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).

#### <a name="groups"></a>Groepen

Groepen zijn afgeleid van de [groeperen](#Grouping) resultaten. Elke groep bevat een verzameling soortgelijke gezichten, waarin gezichten worden aangeduid met [face id's](#Face-ID).

Raadpleeg voor meer informatie de handleiding [geconfronteerd - groep](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).

## <a name="h"></a>H

#### <a name="head-pose-attribute"></a>Ga met zich meebrengen (kenmerk)

HEAD houding is een van de [kenmerken](#Attributes) dat staat voor face-afdrukstand in 3D-ruimte op basis van rollen, inspiratie en plafondmontagemethoden hoeken, zoals wordt weergegeven in de volgende afbeelding. De waardebereiken van de rol en zijn [-180, 180] en [tussen-90 en, 90] yaw in graden. In de huidige versie, de presentatie-waarde geretourneerd van detectie is altijd 0. Het kenmerk head houding is optioneel in de [detectie](#Detection-Face-Detection) resulteert en kan worden beheerd met een [detectie](#Detection-Face-Detection) aanvraag door de parameter returnFaceAttributes. Als de parameter returnFaceAttributes bevat 'headPose', heeft de geretourneerde gezichten head kenmerken met zich meebrengen.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

![GlossaryHeadPose](./Images/headpose.1.jpg)

## <a name="i"></a>I

#### <a name="identification"></a>Identificatie

Identificatie is het identificeren van een of meer gezichten in een LargePersonGroup/PersonGroup.
Een [PersonGroup](#PersonGroup)/[LargePersonGroup](#LargePersonGroup) is een verzameling van [personen](#Person).
Gezichten en de LargePersonGroup/PersonGroup worden vertegenwoordigd door [face id's](#Face-ID) en [LargePersonGroup-id's](#LargePersonGroup-ID)/[PersonGroup-id's](#PersonGroup-ID) respectievelijk in de de aanvraag.
Geïdentificeerde resultaten zijn [kandidaten](#Candidate), vertegenwoordigd door [personen](#Person) met vertrouwen.
Meerdere gezichten in de invoer afzonderlijk worden beschouwd, en elk gezicht heeft een eigen geïdentificeerde resultaat.

> [!NOTE]
> De LargePersonGroup/PersonGroup moet zijn voordat de identificatie worden getraind. Als de LargePersonGroup/PersonGroup niet is getraind, of de training [status](#Status-Train) wordt niet weergegeven als 'geslaagd' (dat wil zeggen ' actief', 'mislukt' of 'time'), het aanvraagantwoord is 400.
> 

Raadpleeg voor meer informatie de volgende handleidingen: [geconfronteerd - identificeren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [LargePersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adcba3a7b9412a4d53f40), [LargePersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acdee6ac60f11b48b5a9d), [ LargePersonGroup - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599ae2d16ac60f11b48b5aa4), [PersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c), [PersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244), [PersonGroup - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249).

#### <a name="isidentical"></a>IsIdentical

IsIdentical is een Boole-veld van [verificatie](#Verification) resultaten die aangeeft of twee gezichten bij dezelfde persoon horen.

Raadpleeg voor meer informatie de handleiding [geconfronteerd: controleren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

## <a name="j"></a>D

## <a name="k"></a>K

## <a name="l"></a>L

#### <a name="landmarks"></a>Oriëntatiepunten

Raadpleeg [geconfronteerd oriëntatiepunten](#Face-Landmarks-Facial-Landmarks).

#### <a name="largefacelist"></a>LargeFaceList

LargeFaceList is een verzameling van [PersistedFace](#PersistedFace) en is de maateenheid [Zoek vergelijkbare](#Find-Similar). Een LargeFaceList wordt geleverd met een [LargeFaceList ID](#LargeFaceList-ID), en andere kenmerken zoals [naam](#Name) en [gebruikersgegevens](#UserData-User-Data).

Raadpleeg voor meer informatie de volgende handleidingen: [LargeFaceList - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a157b68d2de3616c086f2cc), [LargeFaceList - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a15827cd2de3616c086f2ce), [LargeFaceList - lijst Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a158db4d2de3616c086f2d6).

#### <a name="largefacelist-id"></a>LargeFaceList-ID

LargeFaceList-ID is een door de gebruiker opgegeven-tekenreeks die wordt gebruikt als een id van een [LargeFaceList](#LargeFaceList). De LargeFaceList-ID moet uniek zijn binnen het abonnement.

Raadpleeg voor meer informatie de volgende handleidingen: [LargeFaceList - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a157b68d2de3616c086f2cc), [LargeFaceList - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a15827cd2de3616c086f2ce).

#### <a name="largepersongroup"></a>LargePersonGroup

LargePersonGroup is een verzameling van [personen](#Person) en is de maateenheid [identificatie](#Identification). Een LargePersonGroup wordt geleverd met een [LargePersonGroup ID](#LargePersonGroup-ID), en andere kenmerken zoals [naam](#Name) en [gebruikersgegevens](#UserData-User-Data).

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acdee6ac60f11b48b5a9d), [LargePersonGroup - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acebb6ac60f11b48b5a9e), [LargePersonGroup persoon - lijst](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adda06ac60f11b48b5aa1).

#### <a name="largepersongroup-id"></a>LargePersonGroup-ID

LargePersonGroup-ID is een door de gebruiker opgegeven-tekenreeks die wordt gebruikt als een id van een [LargePersonGroup](#LargePersonGroup). De LargePersonGroup-ID moet uniek zijn binnen het abonnement.

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acdee6ac60f11b48b5a9d), [LargePersonGroup - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acebb6ac60f11b48b5a9e).

## <a name="m"></a>M

#### <a name="messy-group"></a>Rommelige groep

Rommelige groep is afgeleid van de [groeperen](#Grouping) resultaten; die niet vergelijkbaar met een andere vlak gezichten bevat. Elk gezicht in een rommelige groep wordt aangegeven door de [face ID](#Face-ID).

Raadpleeg voor meer informatie de handleiding [geconfronteerd - groep](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238).

## <a name="n"></a>N

#### <a name="name-person"></a>Naam (persoon)

De naam is een gebruiksvriendelijke beschrijvende tekenreeks voor [persoon](#Person). In tegenstelling tot de [ID van de persoon](#Person-ID), de naam van mensen in een groep kan worden gedupliceerd.

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adcba3a7b9412a4d53f40), [LargePersonGroup persoon - ophalen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599add376ac60f11b48b5aa0), [PersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c), [ Ophalen van de persoon die PersonGroup -](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523f).

#### <a name="name-largepersongrouppersongroup"></a>Naam (LargePersonGroup/PersonGroup)

De naam is ook een gebruiksvriendelijke beschrijvende tekenreeks voor [LargePersonGroup](#LargePersonGroup)/[PersonGroup](#PersonGroup). In tegenstelling tot de [LargePersonGroup ID](#LargePersonGroup-ID)/[PersonGroup ID](#PersonGroup-ID), de naam van LargePersonGroups/PersonGroups binnen een abonnement kan worden gedupliceerd.

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acdee6ac60f11b48b5a9d), [LargePersonGroup - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acebb6ac60f11b48b5a9e), [PersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244), [ PersonGroup - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395246).

## <a name="o"></a>O

## <a name="p"></a>P

#### <a name="persistedface"></a>PersistedFace

PersistedFace is een gegevensstructuur in Face-API. PersistedFace wordt geleverd met een [PersistedFace ID](#PersistedFace-ID), en andere kenmerken zoals [naam](#Name), en [gebruikersgegevens](#UserData-User-Data).

Raadpleeg voor meer informatie de volgende handleidingen: [LargeFaceList - Face toevoegen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a158c10d2de3616c086f2d3), [FaceList - Face toevoegen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250), [LargePersonGroup persoon - Face toevoegen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adf2a3a7b9412a4d53f42), [ PersonGroup persoon - toevoegen Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b).

#### <a name="person-id"></a>ID van de persoon

ID van de persoon wordt gegenereerd wanneer een [PersistedFace](#PersistedFace) is gemaakt. Een tekenreeks is gemaakt voor deze gezicht in [Face-API](#Face-API).

Raadpleeg voor meer informatie de volgende handleidingen: [LargeFaceList - Face toevoegen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a158c10d2de3616c086f2d3), [FaceList - Face toevoegen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395250), [LargePersonGroup persoon - Face toevoegen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adf2a3a7b9412a4d53f42), [ PersonGroup persoon - toevoegen Face](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523b).

#### <a name="person"></a>Person

Persoon is een gegevensstructuur die worden beheerd in de Face-API. Persoon wordt geleverd met een [ID van de persoon](#Person-ID), en andere kenmerken zoals [naam](#Name), een verzameling van [PersistedFace](#PersistedFace), en [gebruikersgegevens](#UserData-User-Data).

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adcba3a7b9412a4d53f40), [LargePersonGroup persoon - ophalen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599add376ac60f11b48b5aa0), [PersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c), [ Ophalen van de persoon die PersonGroup -](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523f).

#### <a name="person-id"></a>ID van de persoon

ID van de persoon wordt gegenereerd wanneer een [persoon](#Person) is gemaakt. Een tekenreeks is gemaakt voor deze persoon in [Face-API](#Face-API).

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adcba3a7b9412a4d53f40), [LargePersonGroup persoon - ophalen](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599add376ac60f11b48b5aa0), [PersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c), [ Ophalen van de persoon die PersonGroup -](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523f).

#### <a name="persongroup"></a>PersonGroup

PersonGroup is een verzameling van [personen](#Person) en is de maateenheid [identificatie](#Identification). Een PersonGroup wordt geleverd met een [PersonGroup ID](#PersonGroup-ID), en andere kenmerken zoals [naam](#Name) en [gebruikersgegevens](#UserData-User-Data).

Raadpleeg voor meer informatie de volgende handleidingen: [PersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244), [PersonGroup - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395246), [PersonGroup persoon - lijst](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395241).

#### <a name="persongroup-id"></a>PersonGroup-ID

PersonGroup-ID is een door de gebruiker opgegeven-tekenreeks die wordt gebruikt als een id van een [PersonGroup](#PersonGroup). De groeps-ID moet uniek zijn binnen het abonnement.

Raadpleeg voor meer informatie de volgende handleidingen: [PersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244), [PersonGroup - Get](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395246).

#### <a name="pose-attribute"></a>Met zich meebrengen (kenmerk)

Raadpleeg [opleveren, Head](#Head-Pose-Attribute).

## <a name="q"></a>Q

## <a name="r"></a>R

#### <a name="recognition"></a>Erkenning

Herkenning is een populaire module voor face-technologieën, zoals [Zoek vergelijkbare](#Find-Similar), [groeperen](#Grouping), [identificeren](#Identification),[hetzelfde of niet verifiëren dat twee gezichten ](#Verification).

Raadpleeg voor meer informatie de volgende handleidingen: [Face - Zoek vergelijkbare](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395237), [geconfronteerd - groep](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395238), [geconfronteerd - identificeren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239), [geconfronteerd: controleren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

#### <a name="rectangle-face"></a>Rechthoek (gezicht)

Raadpleeg [gezichtsrechthoek](#Face-Rectangle).

## <a name="s"></a>S

#### <a name="smile-attribute"></a>Lach (kenmerk)

Glimlach is een van de [kenmerken](#Attributes) gebruikt om te beschrijven van de expressie glimlach van de beschikbare gezichten. Het kenmerk glimlach is optioneel in de [detectie](#Detection-Face-Detection) resulteert en kan worden beheerd met een [detectie](#Detection-Face-Detection) aanvraag door returnFaceAttributes. Als returnFaceAttributes bevat 'glimlach', wordt de geretourneerde gezichten glimlach kenmerken hebben.

Raadpleeg voor meer informatie de handleiding [geconfronteerd - detecteren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395236).

#### <a name="similar-face-searching"></a>Vergelijkbare gezichten zoeken

Raadpleeg [Zoek vergelijkbare](#Find-Similar).

#### <a name="status-train"></a>Status (Train)

De status is een tekenreeks die wordt gebruikt om te beschrijven de procedure voor het [Training LargeFaceList/LargePersonGroups/PersonGroups](#Train), met inbegrip van notstarted, 'actief', 'geslaagd', 'is mislukt'.

Raadpleeg voor meer informatie de handleiding [LargeFaceList - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a158422d2de3616c086f2d1), [LargePersonGroup - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599ae2d16ac60f11b48b5aa4), [PersonGroup - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249).

#### <a name="subscription-key"></a>Abonnementssleutel

De abonnementssleutel is een tekenreeks die u nodig hebt om op te geven als een queryreeks-parameter om de Face-API's aanroepen. De abonnementssleutel kan worden gevonden op de pagina Mijn abonnementen nadat u zich aanmeldt bij Microsoft Cognitive Services-portal. Er zijn twee sleutels die zijn gekoppeld aan elk abonnement: een primaire sleutel en een secundaire sleutel. Beide kunnen worden gebruikt om aan te roepen API identiek. U moet de abonnementssleutels om veilig te houden en kunt u abonnementssleutels opnieuw genereren op elk gewenst moment op Mijn abonnementen pagina ook.

## <a name="t"></a>T

#### <a name="train-largefacelistlargepersongrouppersongroup"></a>Train (LargeFaceList/LargePersonGroup/PersonGroup)

Deze API wordt gebruikt voor het vooraf verwerken van de [LargeFaceList](#LargeFaceList)/[LargePersonGroup](#LargePersonGroup)/[PersonGroup](#PersonGroup) om te controleren of de [zoeken Vergelijkbare](#Find-Similar)/[identificatie](#Identification) prestaties. Als de training niet wordt beheerd, of de [Training Status](#Status-Train) wordt niet weergegeven als is voltooid, de id voor deze PersonGroup zal leiden tot fouten.

Raadpleeg voor meer informatie de volgende handleidingen: [LargeFaceList - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/5a158422d2de3616c086f2d1), [LargePersonGroup - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599ae2d16ac60f11b48b5aa4), [PersonGroup - Train](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395249), [geconfronteerd - identificeren ](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395239).

## <a name="u"></a>U

#### <a name="userdatauser-data"></a>UserData/gebruikersgegevens

Gebruikersgegevens is extra informatie die is gekoppeld aan [persoon](#Person) en [PersonGroup](#PersonGroup)/[LargePersonGroup](#LargePersonGroup). Gebruikersgegevens is ingesteld door gebruikers gegevens gemakkelijker te gebruiken, te begrijpen en houd er rekening mee.

Raadpleeg voor meer informatie de volgende handleidingen: [LargePersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acdee6ac60f11b48b5a9d), [LargePersonGroup - Update](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599acfc83a7b9412a4d53f3f), [LargePersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599adcba3a7b9412a4d53f40), [LargePersonGroup persoon - Update](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/599ade043a7b9412a4d53f41), [PersonGroup - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395244), [PersonGroup - Update](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039524a), [PersonGroup persoon - maken](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523c), [ Bijwerken van de persoon die PersonGroup -](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f30395242).

## <a name="v"></a>V

#### <a name="verification"></a>Verificatie

Deze API wordt gebruikt om te controleren of twee gezichten hetzelfde of niet zijn. Beide gezichten worden weergegeven als id's in de aanvraag te maken krijgt. Geverifieerd resultaten bevatten een Boole-veld ([isIdentical](#Is-Identical)) waarmee wordt aangegeven hetzelfde als de waarde true en een numeriek veld ([vertrouwen](#Confidence)) die wijzen op het niveau van betrouwbaarheid.

Raadpleeg voor meer informatie de handleiding [geconfronteerd: controleren](https://westus.dev.cognitive.microsoft.com/docs/services/563879b61984550e40cbbe8d/operations/563879b61984550f3039523a).

## <a name="w"></a>W

## <a name="x"></a>X

## <a name="y"></a>J

## <a name="z"></a>Z
