---
title: REST-API van Azure Blockchain Workbench gebruiken
description: Scenario's voor het gebruik van de REST-API van Azure Blockchain Workbench
services: azure-blockchain
keywords: ''
author: PatAltimore
ms.author: patricka
ms.date: 11/14/2018
ms.topic: article
ms.service: azure-blockchain
ms.reviewer: zeyadr
manager: femila
ms.openlocfilehash: c1a9b526f08f330d62c30dd1d676e95460aee6c2
ms.sourcegitcommit: a4e4e0236197544569a0a7e34c1c20d071774dd6
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 11/15/2018
ms.locfileid: "51712344"
---
# <a name="using-the-azure-blockchain-workbench-rest-api"></a>REST-API van Azure Blockchain Workbench gebruiken

De REST-API van Azure Blockchain Workbench biedt ontwikkelaars en IT-medewerkers een manier voor het bouwen van uitgebreide integraties voor blockchain-toepassingen. In dit document worden verschillende belangrijke methoden van de REST-API van Workbench beschreven. Stel dat een ontwikkelaar een aangepaste blockchain-client wil maken. Met deze blockchain-client kunnen ingelogde gebruikers hun toegewezen blockchain-applicaties bekijken en gebruiken. De client stelt gebruikers in de gelegenheid exemplaren van contracten te bekijken en actie te ondernemen op smart contracts. De client gebruikt de Workbench REST API in de context van de ingelogde gebruiker om de volgende acties uit te voeren:

* Lijst met toepassingen weergeven
* Lijst met werkstromen voor een toepassing weergeven
* Lijst met exemplaren van smarts contracts voor een werkstroom weergeven
* Lijst met beschikbare acties voor een contract weergeven
* Een actie voor een contract uitvoeren

De voorbeeld blockchain-toepassingen die in de scenario's worden gebruikt kunnen worden [gedownload uit GitHub](https://github.com/Azure-Samples/blockchain).

## <a name="list-applications"></a>Lijst met toepassingen weergeven

Zodra een gebruiker zich bij de blockchain-client heeft aangemeld, is de eerste taak om alle Blockchain Workbench-toepassingen voor de gebruiker op te halen. In dit scenario heeft de gebruiker toegang tot twee toepassingen:

1. [Asset-overdracht](https://github.com/Azure-Samples/blockchain/blob/master/blockchain-workbench/application-and-smart-contract-samples/asset-transfer/readme.md)
2. [Gekoeld transport](https://github.com/Azure-Samples/blockchain/blob/master/blockchain-workbench/application-and-smart-contract-samples/refrigerated-transportation/readme.md)

Gebruik de [GET-API voor toepassingen](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/applications/applicationsget):

``` http
GET /api/v1/applications
Authorization : Bearer {access token}
```

Het antwoord geeft een lijst van alle blockchain-toepassingen waartoe een gebruiker toegang in Blockchain Workbench heeft. Blockchain Workbench-beheerders krijgen alle blockchain-toepassingen. Niet-Workbench beheerders krijgen alle blockchains waarvoor ze ten minste één bijbehorende toepassingsrol of een bijbehorende instantie voor smart contractexemplaren hebben.

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/applications?skip=2",
    "applications": [
        {
            "id": 1,
            "name": "AssetTransfer",
            "description": "Allows transfer of assets between a buyer and a seller, with appraisal/inspection functionality",
            "displayName": "Asset Transfer",
            "createdByUserId": 1,
            "createdDtTm": "2018-04-28T05:59:14.4733333",
            "enabled": true,
            "applicationRoles": null
        },
        {
            "id": 2,
            "name": "RefrigeratedTransportation",
            "description": "Application to track end-to-end transportation of perishable goods.",
            "displayName": "Refrigerated Transportation",
            "createdByUserId": 7,
            "createdDtTm": "2018-04-28T18:25:38.71",
            "enabled": true,
            "applicationRoles": null
        }
    ]
}
```

## <a name="list-workflows-for-an-application"></a>Lijst met werkstromen voor een toepassing weergeven

Zodra een gebruiker de gewenste blockchain-toepassing selecteert (zoals **Asset Transfer**), haalt de blockchain-client alle workflows van de specifieke blockchain-toepassing op. Gebruikers kunnen vervolgens de toepasselijke workflow selecteren voordat alle smart contractinstanties voor de workflow worden getoond. Elke blockchain-toepassing heeft een of meer workflows en elke workflow heeft nul of meer smart contractinstanties. Voor een blockchain-clienttoepassing die slechts één workflow heeft, raden we aan de gebruikerservaringsstroom over te slaan, zodat gebruikers de juiste workflow kunnen selecteren. In dit geval heeft **Asset Transfer** slechts één werkstroom, ook wel genoemd **Asset Transfer**.

Gebruik de [GET-API voor werkstromen van toepassingen](https://docs.microsoft.com/rest/api/azure-blockchain-workbench/applications/workflowsget):

``` http
GET /api/v1/applications/{applicationId}/workflows
Authorization: Bearer {access token}
```

Het antwoord geeft een overzicht van alle workflows van de gespecificeerde blockchain-toepassing waartoe een gebruiker toegang heeft in Blockchain Workbench. Blockchain Workbench-beheerders krijgen elke blockchain-workflow. Niet-Workbench-beheerders krijgen alle werkstromen waarvoor ze ten minste één bijbehorende toepassingsrol hebben of die zijn gekoppeld aan een rol van een smart contractinstantie.

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/applications/1/workflows?skip=1",
    "workflows": [
        {
            "id": 1,
            "name": "AssetTransfer",
            "description": "Handles the business logic for the asset transfer scenario",
            "displayName": "Asset Transfer",
            "applicationId": 1,
            "constructorId": 1,
            "startStateId": 1
        }
    ]
}
```

## <a name="list-smart-contract-instances-for-a-workflow"></a>Lijst met exemplaren van smart contracts voor een workflow weergeven

Zodra een gebruiker de toepasselijke workflow selecteert, in dit geval **Asset Transfer**, haalt de blockchain-client alle smart contractinstanties voor de opgegeven workflow op. U kunt deze informatie gebruiken om alle smart contractinstanties voor de workflow te tonen. Of u kunt gebruikers toestaan om diep in een van de getoonde smart contractinstanties te duiken. Overweeg in dit voorbeeld dat een gebruiker interactie wil hebben met een van de smart contractinstanties om actie te ondernemen.

Gebruik de [GET-API voor contracten](/rest/api/azure-blockchain-workbench/contractsv2/contractsget):

``` http
GET api/v1/contracts?workflowId={workflowId}
Authorization: Bearer {access token}
```

Het antwoord vermeldt alle smart contractinstanties van de opgegeven workflow. Workbench-beheerders krijgen alle slimme contractinstanties. Niet-Workbench-beheerders krijgen alle smart contractexemplaren waarvoor ze ten minste één bijbehorende toepassingsrol hebben of die zijn gekoppeld aan een slimme contractinstantie-rol.

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/contracts?skip=3&workflowId=1",
    "contracts": [
        {
            "id": 1,
            "provisioningStatus": 2,
            "connectionID": 1,
            "ledgerIdentifier": "0xbcb6127be062acd37818af290c0e43479a153a1c",
            "deployedByUserId": 1,
            "workflowId": 1,
            "contractCodeId": 1,
            "contractProperties": [
                {
                    "workflowPropertyId": 1,
                    "value": "0"
                },
                {
                    "workflowPropertyId": 2,
                    "value": "My first car"
                },
                {
                    "workflowPropertyId": 3,
                    "value": "54321"
                },
                {
                    "workflowPropertyId": 4,
                    "value": "0"
                },
                {
                    "workflowPropertyId": 5,
                    "value": "0x0000000000000000000000000000000000000000"
                },
                {
                    "workflowPropertyId": 6,
                    "value": "0x0000000000000000000000000000000000000000"
                },
                {
                    "workflowPropertyId": 7,
                    "value": "0x0000000000000000000000000000000000000000"
                },
                {
                    "workflowPropertyId": 8,
                    "value": "0xd882530eb3d6395e697508287900c7679dbe02d7"
                }
            ],
            "transactions": [
                {
                    "id": 1,
                    "connectionId": 1,
                    "transactionHash": "0xf3abb829884dc396e03ae9e115a770b230fcf41bb03d39457201449e077080f4",
                    "blockID": 241,
                    "from": "0xd882530eb3d6395e697508287900c7679dbe02d7",
                    "to": null,
                    "value": 0,
                    "isAppBuilderTx": true
                }
            ],
            "contractActions": [
                {
                    "id": 1,
                    "userId": 1,
                    "provisioningStatus": 2,
                    "timestamp": "2018-04-29T23:41:14.9333333",
                    "parameters": [
                        {
                            "name": "Description",
                            "value": "My first car"
                        },
                        {
                            "name": "Price",
                            "value": "54321"
                        }
                    ],
                    "workflowFunctionId": 1,
                    "transactionId": 1,
                    "workflowStateId": 1
                }
            ]
        }
    ]
}
```

## <a name="list-available-actions-for-a-contract"></a>Lijst met beschikbare acties voor een contract weergeven

Zodra een gebruiker besluit om diep in een contract te duiken, kan de blockchain-client vervolgens de beschikbare gebruikersacties weergeven, gegeven de staat van het contract. In dit voorbeeld bekijkt de gebruiker alle beschikbare acties voor een nieuw smart contract dat ze hebben gemaakt:

* Modify: hiermee kan de gebruiker de beschrijving en prijs van een asset aanpassen.
* Beëindigen: hiermee kan de gebruiker het contract van een asset beëindigen.

Gebruik de [GET-API voor contractacties](/rest/api/azure-blockchain-workbench/contractsv2/contractactionget):

``` http
GET /api/v1/contracts/{contractId}/actions
Authorization: Bearer {access token}
```

Het antwoord geeft een overzicht van alle acties die een gebruiker kan ondernemen in de huidige staat van de opgegeven instantie van een smart contract. Gebruikers krijgen alle toepasselijke acties als de gebruiker een gekoppelde toepassingsrol heeft of is gekoppeld aan een smart contractinstantie-rol voor de huidige status van de opgegeven instantie van een smart contract.

``` http
HTTP/1.1 200 OK
Content-type: application/json
{
    "nextLink": "/api/v1/contracts/1/actions?skip=2",
    "workflowFunctions": [
        {
            "id": 2,
            "name": "Modify",
            "description": "Modify the description/price attributes of this asset transfer instance",
            "displayName": "Modify",
            "parameters": [
                {
                    "id": 1,
                    "name": "description",
                    "description": "The new description of the asset",
                    "displayName": "Description",
                    "type": {
                        "id": 2,
                        "name": "string",
                        "elementType": null,
                        "elementTypeId": 0
                    }
                },
                {
                    "id": 2,
                    "name": "price",
                    "description": "The new price of the asset",
                    "displayName": "Price",
                    "type": {
                        "id": 3,
                        "name": "money",
                        "elementType": null,
                        "elementTypeId": 0
                    }
                }
            ],
            "workflowId": 1
        },
        {
            "id": 3,
            "name": "Terminate",
            "description": "Used to cancel this particular instance of asset transfer",
            "displayName": "Terminate",
            "parameters": [],
            "workflowId": 1
        }
    ]
}
```

## <a name="execute-an-action-for-a-contract"></a>Een actie voor een contract uitvoeren

Een gebruiker kan vervolgens beslissen om actie te ondernemen voor de opgegeven instantie van een smart contract. Overweeg in dit geval het scenario waarbij een gebruiker de beschrijving en prijs van een asset wil wijzigen in de volgende actie:

* Beschrijving: 'My updated car'
* Prijs: 54321

Gebruik de [POST-API voor contractacties](/rest/api/azure-blockchain-workbench/contractsv2/contractactionpost):

``` http
POST /api/v1/contracts/{contractId}/actions
Authorization: Bearer {access token}
actionInformation: {
    "workflowFunctionId": 2,
    "workflowActionParameters": [
        {
            "name": "description",
            "value": "My updated car"
        },
        {
            "name": "price",
            "value": "54321"
        }
    ]
}
```

Gebruikers kunnen de actie alleen uitvoeren op basis van de huidige status van de opgegeven instantie voor een smart contract en de bijbehorende toepassingsrol van de gebruiker of de rol van de smart contractinstantie. Als het bericht succesvol is, wordt een HTTP 200 OK-antwoord geretourneerd zonder inhoudelijk antwoord.

``` http
HTTP/1.1 200 OK
Content-type: application/json
```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Naslaginformatie over de REST-API van Azure Blockchain Workbench](https://docs.microsoft.com/rest/api/azure-blockchain-workbench)
