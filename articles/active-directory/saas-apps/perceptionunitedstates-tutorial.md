---
title: 'Zelfstudie: Azure Active Directory-integratie met perceptie Verenigde Staten (niet-UltiPro) | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en perceptie Verenigde Staten (niet-UltiPro).
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.reviewer: joflore
ms.assetid: b4a8f026-cb5f-41eb-9680-68eddc33565e
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: jeedes
ms.openlocfilehash: 8c29d054f2e4e9ff4b57785a57e5c6ea512623a6
ms.sourcegitcommit: 11d8ce8cd720a1ec6ca130e118489c6459e04114
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 12/04/2018
ms.locfileid: "52840656"
---
# <a name="tutorial-azure-active-directory-integration-with-perception-united-states-non-ultipro"></a>Zelfstudie: Azure Active Directory-integratie met perceptie Verenigde Staten (niet-UltiPro)

In deze zelfstudie leert u hoe u perceptie Verenigde Staten (niet-UltiPro) integreren met Azure Active Directory (Azure AD).

Perceptie Verenigde Staten (niet-UltiPro) integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang hebben naar perceptie Verenigde Staten (niet-UltiPro).
- U kunt uw gebruikers automatisch ophalen aangemeld op perceptie Verenigde Staten (niet-UltiPro) (Single Sign-On) met hun Azure AD-accounts inschakelen.
- U kunt uw accounts in één centrale locatie - Azure portal beheren.

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met perceptie Verenigde Staten (niet-UltiPro), moet u de volgende items:

- Een Azure AD-abonnement
- Een perceptie Verenigde Staten (niet-UltiPro) eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u [een proefversie van één maand krijgen](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Perceptie Verenigde Staten (niet-UltiPro) uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-perception-united-states-non-ultipro-from-the-gallery"></a>Perceptie Verenigde Staten (niet-UltiPro) uit de galerie toe te voegen
Als u wilt de integratie van perceptie Verenigde Staten (niet-UltiPro) in Azure AD configureert, moet u perceptie Verenigde Staten (niet-UltiPro) toevoegen vanuit de galerie aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen perceptie Verenigde Staten (niet-UltiPro) uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![De Azure Active Directory-knop][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![De blade Enterprise-toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![De knop nieuwe toepassing][3]

1. Typ in het zoekvak **perceptie Verenigde Staten (niet-UltiPro)**, selecteer **perceptie Verenigde Staten (niet-UltiPro)** van resultaat deelvenster klik vervolgens op **toevoegen** om toe te voegen de de toepassing.

    ![Perceptie Verenigde Staten (niet-UltiPro) in de lijst met resultaten](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Configureren en Azure AD eenmalige aanmelding testen

In deze sectie maakt u configureert en test Azure AD eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro) op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in de perceptie Verenigde Staten (niet-UltiPro) is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in de perceptie Verenigde Staten (niet-UltiPro) tot stand worden gebracht.

In perceptie Verenigde Staten (niet-UltiPro), wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro), moet u de volgende bouwstenen voltooien:

1. **[Azure AD eenmalige aanmelding configureren](#configure-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Maak een Azure AD-testgebruiker](#create-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Maak een testgebruiker perceptie Verenigde Staten (niet-UltiPro)](#create-a-perception-united-states-non-ultipro-test-user)**  - hebben een equivalent van Britta Simon in perceptie Verenigde Staten (niet-UltiPro) die is gekoppeld aan de Azure AD-weergave van de gebruiker.
1. **[Toewijzen van de Azure AD-testgebruiker](#assign-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#test-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configure-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw toepassing perceptie Verenigde Staten (niet-UltiPro).

**Voor het configureren van Azure AD eenmalige aanmelding met perceptie Verenigde Staten (niet-UltiPro), moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **perceptie Verenigde Staten (niet-UltiPro)** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Koppeling voor eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.
 
    ![In het dialoogvenster voor eenmalige aanmelding](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_samlbase.png)

1. Op de **perceptie Verenigde Staten (niet-UltiPro)-domein en URL's** sectie, voert u de volgende stappen uit:

    ![Perceptie Verenigde Staten (niet-UltiPro)-domein en URL's eenmalige aanmelding informatie](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_url.png)

    a. In de **id** tekstvak typt u de URL: `https://perception.kanjoya.com/sp`

    b. In de **antwoord-URL** tekstvak, een URL met behulp van het volgende patroon: `https://perception.kanjoya.com/sso?idp=<entity_id>`

    > [!NOTE] 
    > De waarde is niet echt. U kunt de waarde wordt bijgewerkt met de werkelijke antwoord-URL, die later in de zelfstudie wordt uitgelegd.
 
1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **Metadata XML** en sla het bestand met metagegevens op uw computer.

    ![De downloadkoppeling certificaat](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_certificate.png) 

1. Klik op **opslaan** knop.

    ![Configureren van eenmalige aanmelding opslaan](./media/perceptionunitedstates-tutorial/tutorial_general_400.png)

1. Op de **perceptie Verenigde Staten (niet-UltiPro) configuratie** sectie, klikt u op **configureren perceptie Verenigde Staten (niet-UltiPro)** openen **aanmelding configureren** venster . Kopiëren de **SAML entiteit-ID** uit de **Naslaggids sectie.**

    a. De **perceptie Verenigde Staten (niet-UltiPro)** toepassing vereist de **SAML entiteit-ID** waarde die u hebt gekopieerd, naar de URI-codering krijgen. Als u de uri-gecodeerde waarde, gebruikt u de volgende koppeling:**http://www.url-encode-decode.com/**.

    b. Nadat u de uri gecodeerde waarde combineren met de **antwoord-URL** zoals vermeld hieronder:

    `https://perception.kanjoya.com/sso?idp=<URI encooded entity_id>`
    
    c. Plak de bovenstaande waarde in de **antwoord-URL** -tekstvak in **perceptie Verenigde Staten (niet-UltiPro)-domein en URL's** sectie.

    ![Perceptie Verenigde Staten (niet-UltiPro)-configuratie](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_configure.png) 

1. In een ander browservenster, meld u aan bij uw bedrijf perceptie Verenigde Staten (niet-UltiPro) site als beheerder.

1. Klik in de belangrijkste werkbalk **Accountinstellingen**.

    ![Perceptie Verenigde Staten (niet-UltiPro) gebruiker](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_user.png)

1. Op de **Accountinstellingen** pagina, voert u de volgende stappen uit:

    ![Perceptie Verenigde Staten (niet-UltiPro) gebruiker](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_account.png)

    a. In de **bedrijfsnaam** tekstvak, typ de naam van de **bedrijf**.
    
    b. In de **accountnaam** tekstvak, typ de naam van de **Account**.

    c. In **standaard antwoordadres e** tekst typt u de geldige **e**.

    d. Selecteer **id-Provider voor eenmalige aanmelding** als **SAML 2.0**.

1. Op de **SSO-configuratie** pagina, voert u de volgende stappen uit:

    ![Perceptie Verenigde Staten (niet-UltiPro) SSOConfig](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_ssoconfig.png)

    a. Selecteer **SAML NameID Type** als **e**.

    b. In de **SSO configuratienaam** tekstvak, typ de naam van uw **configuratie**.
    
    c. In **identiteit providernaam** tekstvak, plak de waarde van **SAML entiteit-ID**, die u hebt gekopieerd vanuit Azure portal. 

    d. In **SAML domein tekstvak**, voert u het domein, zoals **@contoso.com**.

    e. Klik op **opnieuw uploaden** het uploaden van de **Metadata XML** bestand.

    f. Klik op **Update**.


> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl het instellen van de app!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de  **Configuratie** sectie aan de onderkant. U kunt meer lezen over de documentatie voor embedded-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="create-an-azure-ad-test-user"></a>Maak een testgebruiker Azure AD

Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

   ![Maak een testgebruiker Azure AD][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de Azure portal, in het linkerdeelvenster klikt u op de **Azure Active Directory** knop.

    ![De Azure Active Directory-knop](./media/perceptionunitedstates-tutorial/create_aaduser_01.png)

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen**, en klik vervolgens op **alle gebruikers**.

    !['Gebruikers en groepen' en 'Alle gebruikers' koppelingen](./media/perceptionunitedstates-tutorial/create_aaduser_02.png)

1. Om te openen de **gebruiker** in het dialoogvenster, klikt u op **toevoegen** aan de bovenkant van de **alle gebruikers** in het dialoogvenster.

    ![De knop toevoegen](./media/perceptionunitedstates-tutorial/create_aaduser_03.png)

1. In de **gebruiker** dialoogvenster vak, voer de volgende stappen uit:

    ![Het dialoogvenster gebruiker](./media/perceptionunitedstates-tutorial/create_aaduser_04.png)

    a. In de **naam** in het vak **BrittaSimon**.

    b. In de **gebruikersnaam** typt u het e-mailadres van gebruiker Britta Simon.

    c. Selecteer de **wachtwoord weergeven** selectievakje en noteer de waarde die wordt weergegeven in de **wachtwoord** vak.

    d. Klik op **Create**.
  
### <a name="create-a-perception-united-states-non-ultipro-test-user"></a>Maak een testgebruiker perceptie Verenigde Staten (niet-UltiPro)

In deze sectie maakt u een gebruiker met de naam Britta Simon in perceptie Verenigde Staten (niet-UltiPro). Werken met [perceptie Verenigde Staten (niet-UltiPro)-ondersteuningsteam](https://www.ultimatesoftware.com/Contact/ContactUs) om toe te voegen de gebruikers in het platform, Perception Verenigde Staten (niet-UltiPro).

### <a name="assign-the-azure-ad-test-user"></a>De Azure AD-testgebruiker toewijzen

In deze sectie schakelt u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen aan perceptie Verenigde Staten (niet-UltiPro).

![De de gebruikersrol toewijzen][200] 

**Als u wilt toewijzen Britta Simon naar perceptie Verenigde Staten (niet-UltiPro), moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **perceptie Verenigde Staten (niet-UltiPro)**.

    ![De koppeling perceptie Verenigde Staten (niet-UltiPro) in de lijst met toepassingen](./media/perceptionunitedstates-tutorial/tutorial_perceptionunitedstates_app.png)  

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![De koppeling 'Gebruikers en groepen'][202]

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Het deelvenster toewijzing toevoegen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.
    
### <a name="test-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie maakt testen u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Wanneer u op de tegel perceptie Verenigde Staten (niet-UltiPro) in het toegangsvenster, u moet u automatisch aangemeld bij uw toepassing perceptie Verenigde Staten (niet-UltiPro).
Zie voor meer informatie over het toegangsvenster, [Inleiding tot het toegangsvenster](../user-help/active-directory-saas-access-panel-introduction.md). 

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)



<!--Image references-->

[1]: ./media/perceptionunitedstates-tutorial/tutorial_general_01.png
[2]: ./media/perceptionunitedstates-tutorial/tutorial_general_02.png
[3]: ./media/perceptionunitedstates-tutorial/tutorial_general_03.png
[4]: ./media/perceptionunitedstates-tutorial/tutorial_general_04.png

[100]: ./media/perceptionunitedstates-tutorial/tutorial_general_100.png

[200]: ./media/perceptionunitedstates-tutorial/tutorial_general_200.png
[201]: ./media/perceptionunitedstates-tutorial/tutorial_general_201.png
[202]: ./media/perceptionunitedstates-tutorial/tutorial_general_202.png
[203]: ./media/perceptionunitedstates-tutorial/tutorial_general_203.png

