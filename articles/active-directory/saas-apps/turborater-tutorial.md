---
title: 'Zelfstudie: Azure Active Directory-integratie met TurboRater | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en TurboRater.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: abb116b8-8024-4cc6-bc81-f32ef490ea17
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/03/2017
ms.author: jeedes
ms.openlocfilehash: 3dfa824d680f7014ee63b8c83d26dc29d42c7fe9
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39437291"
---
# <a name="tutorial-azure-active-directory-integration-with-turborater"></a>Zelfstudie: Azure Active Directory-integratie met TurboRater

In deze zelfstudie leert u hoe u TurboRater integreren met Azure Active Directory (Azure AD).

TurboRater integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot TurboRater heeft.
- U kunt uw gebruikers automatisch ophalen aangemeld bij TurboRater (Single Sign-On) met hun Azure AD-accounts inschakelen.
- U kunt uw accounts in één centrale locatie - Azure portal beheren.

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met TurboRater, moet u de volgende items:

- Een Azure AD-abonnement
- Een TurboRater eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u [een proefversie van één maand krijgen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. TurboRater uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-turborater-from-the-gallery"></a>TurboRater uit de galerie toe te voegen
Voor het configureren van de integratie van TurboRater in Azure AD, moet u TurboRater uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen TurboRater uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop nieuwe toepassing][3]

1. Typ in het zoekvak **TurboRater**, selecteer **TurboRater** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![TurboRater in de lijst met resultaten](./media/turborater-tutorial/tutorial_turborater_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en Azure AD eenmalige aanmelding testen

In deze sectie maakt u configureert en test Azure AD eenmalige aanmelding met TurboRater op basis van een testgebruiker 'Julia steen' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in TurboRater is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in TurboRater tot stand worden gebracht.

In TurboRater, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met TurboRater, moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Maak een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Maak een testgebruiker TurboRater](#create-a-turborater-test-user)**  : als u wilt een equivalent van Britta Simon in TurboRater die is gekoppeld aan de Azure AD-weergave van de gebruiker hebben.
1. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#test-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw toepassing TurboRater.

**Voor het configureren van Azure AD eenmalige aanmelding met TurboRater, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **TurboRater** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.
 
    ![In het dialoogvenster voor eenmalige aanmelding](./media/turborater-tutorial/tutorial_turborater_samlbase.png)

1. Op de **TurboRater domein en URL's** sectie, voert u de volgende stappen uit:

    ![TurboRater domein en URL's, eenmalige aanmelding informatie](./media/turborater-tutorial/tutorial_turborater_url.png)

    a. In de **id** tekstvak typt u de waarde als: `https://www.itcdataservices.com`
 
    b. In de **antwoord-URL** tekstvak typt u de waarde als:
    
    | Omgeving | URL |
    | ---------------| --------------- |    
    | Testen  | `https://ratingqa.itcdataservices.com/webservices/imp/saml/login` |
    | Live  | `https://www.itcratingservices.com/webservices/imp/saml/login` |

1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/turborater-tutorial/tutorial_turborater_certificate.png) 

1. Klik op **opslaan** knop.

    ![Configureren van eenmalige aanmelding opslaan](./media/turborater-tutorial/tutorial_general_400.png)

1. Het configureren van eenmalige aanmelding op **TurboRater** zijde, moet u voor het verzenden van de gedownloade **Metadata XML** naar [TurboRater ondersteuningsteam](https://www.getitc.com/support). Ze stelt u deze optie om de SAML SSO-verbinding instellen goed aan beide zijden.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl het instellen van de app!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de  **Configuratie** sectie aan de onderkant. U kunt meer lezen over de documentatie voor embedded-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Maak een testgebruiker Azure AD

Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

   ![Maak een testgebruiker Azure AD][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de Azure portal, in het linkerdeelvenster klikt u op de **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/turborater-tutorial/create_aaduser_01.png)

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/turborater-tutorial/create_aaduser_02.png)

1. Om te openen de **gebruiker** in het dialoogvenster, klikt u op **toevoegen** aan de bovenkant van de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/turborater-tutorial/create_aaduser_03.png)

1. In de **gebruiker** dialoogvenster vak, voer de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/turborater-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
  
### <a name="create-a-turborater-test-user"></a>Maak een testgebruiker TurboRater

Als u wilt dat Azure AD-gebruikers zich aanmelden bij TurboRater, moeten ze worden ingericht voor TurboRater.  
In het geval van TurboRater is inrichten een handmatige taak.
Voor het maken van een gebruiker, neem contact op met [TurboRater ondersteuningsteam](https://www.getitc.com/support).

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen aan TurboRater.

![De de gebruikersrol toewijzen][200] 

**Als u wilt Britta Simon aan TurboRater toewijst, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **TurboRater**.

    ![De koppeling TurboRater in de lijst met toepassingen](./media/turborater-tutorial/tutorial_turborater_app.png)  

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie maakt testen u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Wanneer u op de tegel TurboRater in het toegangsvenster, u moet u automatisch aangemeld bij uw toepassing TurboRater.
Zie voor meer informatie over het toegangsvenster, [Inleiding tot het toegangsvenster](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)



<!--Image references-->

[1]: ./media/turborater-tutorial/tutorial_general_01.png
[2]: ./media/turborater-tutorial/tutorial_general_02.png
[3]: ./media/turborater-tutorial/tutorial_general_03.png
[4]: ./media/turborater-tutorial/tutorial_general_04.png

[100]: ./media/turborater-tutorial/tutorial_general_100.png

[200]: ./media/turborater-tutorial/tutorial_general_200.png
[201]: ./media/turborater-tutorial/tutorial_general_201.png
[202]: ./media/turborater-tutorial/tutorial_general_202.png
[203]: ./media/turborater-tutorial/tutorial_general_203.png

