---
title: 'Zelfstudie: Azure Active Directory-integratie met Zscaler bèta | Microsoft Docs'
description: Informatie over het configureren van eenmalige aanmelding tussen Azure Active Directory en Zscaler Beta.
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: 56b846ae-a1e7-45ae-a79d-992a87f075ba
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: jeedes
ms.openlocfilehash: 29637f8a733e9f92f37144491bef4ab4ba5aae07
ms.sourcegitcommit: 1d850f6cae47261eacdb7604a9f17edc6626ae4b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "39433357"
---
# <a name="tutorial-azure-active-directory-integration-with-zscaler-beta"></a>Zelfstudie: Azure Active Directory-integratie met Zscaler Beta

In deze zelfstudie leert u hoe u Zscaler bèta integreren met Azure Active Directory (Azure AD).

Zscaler bèta integreren met Azure AD biedt u de volgende voordelen:

- U kunt beheren in Azure AD die toegang tot de Zscaler heeft bèta
- U kunt uw gebruikers automatisch ophalen aangemeld bij Zscaler Beta (Single Sign-On) inschakelen met hun Azure AD-accounts
- U kunt uw accounts in één centrale locatie - Azure portal beheren

Als u wilt graag meer informatie over de integratie van de SaaS-app met Azure AD, Zie [wat is toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Vereisten

Voor het configureren van Azure AD-integratie met Zscaler Bèta, moet u de volgende items:

- Een Azure AD-abonnement
- Een Zscaler bèta eenmalige aanmelding ingeschakeld abonnement

> [!NOTE]
> Als u wilt testen van de stappen in deze zelfstudie, raden we niet met behulp van een productie-omgeving.

Als u wilt testen van de stappen in deze zelfstudie, moet u deze aanbevelingen volgen:

- Gebruik uw productie-omgeving, niet als dat nodig is.
- Als u geen een proefversie Azure AD-omgeving hebt, kunt u een proefversie van één maand hier downloaden: [proefversie aanbieding](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Scenariobeschrijving
In deze zelfstudie test u de Azure AD eenmalige aanmelding in een testomgeving. Het scenario in deze zelfstudie bestaat uit twee belangrijkste bouwstenen:

1. Zscaler bèta uit de galerie toe te voegen
1. Configureren en testen van Azure AD eenmalige aanmelding

## <a name="adding-zscaler-beta-from-the-gallery"></a>Zscaler bèta uit de galerie toe te voegen
Voor het configureren van de integratie van Zscaler Beta in Azure AD, moet u Zscaler bèta uit de galerie toevoegen aan uw lijst met beheerde SaaS-apps.

**Als u wilt toevoegen Zscaler bèta uit de galerie, moet u de volgende stappen uitvoeren:**

1. In de  **[Azure-portal](https://portal.azure.com)**, klik in het navigatievenster aan de linkerkant op **Azure Active Directory** pictogram. 

    ![Active Directory][1]

1. Navigeer naar **bedrijfstoepassingen**. Ga vervolgens naar **alle toepassingen**.

    ![Toepassingen][2]
    
1. Nieuwe toepassing toevoegen, klikt u op **nieuwe toepassing** knop boven aan het dialoogvenster.

    ![Toepassingen][3]

1. Typ in het zoekvak **Zscaler Bèta**.

    ![Het maken van een Azure AD-testgebruiker](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_search.png)

1. Selecteer in het deelvenster resultaten **Zscaler Bèta**, en klik vervolgens op **toevoegen** om toe te voegen van de toepassing.

    ![Het maken van een Azure AD-testgebruiker](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Configureren en testen van Azure AD eenmalige aanmelding
In deze sectie configureert u en test Azure AD eenmalige aanmelding met Zscaler Beta op basis van een testgebruiker 'Britta Simon' genoemd.

Voor eenmalige aanmelding om te werken, moet Azure AD om te weten wat de gebruiker equivalent in de bètafase Zscaler is aan een gebruiker in Azure AD. Met andere woorden, moet een koppeling relatie tussen een Azure AD-gebruiker en de gerelateerde gebruiker in de bètafase Zscaler tot stand worden gebracht.

In de bètafase Zscaler, wijs de waarde van de **gebruikersnaam** in Azure AD als de waarde van de **gebruikersnaam** de relatie van de koppeling tot stand brengen.

Om te configureren en testen van Azure AD eenmalige aanmelding met Zscaler Bèta, moet u de volgende bouwstenen voltooien:

1. **[Configureren van Azure AD eenmalige aanmelding](#configuring-azure-ad-single-sign-on)**  : als u wilt dat uw gebruikers kunnen deze functie gebruiken.
1. **[Proxy-instellingen configureren](#configuring-proxy-settings)**  : als u wilt de proxy-instellingen in Internet Explorer configureren
1. **[Het maken van een Azure AD-testgebruiker](#creating-an-azure-ad-test-user)**  - voor het testen van Azure AD eenmalige aanmelding met Britta Simon.
1. **[Het maken van een testgebruiker Zscaler Bèta](#creating-a-zscaler-beta-test-user)**  : als u wilt een equivalent van Britta Simon hebben in de bètafase Zscaler die is gekoppeld aan de Azure AD-weergave van de gebruiker.
1. **[Toewijzen van de Azure AD-testgebruiker](#assigning-the-azure-ad-test-user)**  - Britta Simon gebruik van Azure AD eenmalige aanmelding inschakelen.
1. **[Eenmalige aanmelding testen](#testing-single-sign-on)**  : als u wilt controleren of de configuratie werkt.

### <a name="configuring-azure-ad-single-sign-on"></a>Azure AD eenmalige aanmelding configureren

In deze sectie maakt u schakelt Azure AD eenmalige aanmelding in de Azure-portal en configureren van eenmalige aanmelding in uw toepassing Zscaler Beta.

**Voor het configureren van Azure AD eenmalige aanmelding met Zscaler Bèta, moet u de volgende stappen uitvoeren:**

1. In de Azure-portal op de **Zscaler Bèta** toepassingspagina integratie, klikt u op **eenmalige aanmelding**.

    ![Eenmalige aanmelding configureren][4]

1. Op de **eenmalige aanmelding** dialoogvenster, selecteer **modus** als **SAML gebaseerde aanmelding** eenmalige aanmelding inschakelen.
 
    ![Eenmalige aanmelding configureren](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_samlbase.png)

1. Op de **Zscaler bèta-domein en URL's** sectie, voert u de volgende stappen uit:

    ![Eenmalige aanmelding configureren](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_url.png)

    Typ in het tekstvak aanmeldings-URL de URL die wordt gebruikt door uw gebruikers aan te melden aan uw toepassing Zscaler Beta.

    > [!NOTE] 
    > U moet deze waarde bijwerken met de werkelijke aanmeldings-URL. Neem contact op met [Zscaler bèta-Client-ondersteuningsteam](https://www.zscaler.com/company/contact) deze waarde op te halen. 

1. Op de **SAML-handtekeningcertificaat** sectie, klikt u op **Certificate(Base64)** en slaat u het certificaatbestand op uw computer.

    ![Eenmalige aanmelding configureren](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_certificate.png) 

1. Klik op **opslaan** knop.

    ![Eenmalige aanmelding configureren](./media/zscaler-beta-tutorial/tutorial_general_400.png)

1. Op de **Zscaler bèta configuratie** sectie, klikt u op **configureren Zscaler Bèta** openen **aanmelding configureren** venster. Kopiëren de **Single Sign-On Service URL voor SAML** uit de **Naslaggids sectie.**

    ![Eenmalige aanmelding configureren](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_configure.png) 

1. In een ander browservenster aanmelden bij uw bedrijf Zscaler bèta site als beheerder.

1. Klik in het menu aan de bovenkant op **beheer**.
   
    ![Beheer](./media/zscaler-beta-tutorial/ic800206.png "beheer")

1. Onder **beheren beheerders en rollen**, klikt u op **gebruikers beheren & verificatie**.   
            
    ![Gebruikers & verificatie beheren](./media/zscaler-beta-tutorial/ic800207.png "gebruikers & verificatie beheren")

1. In de **verificatie-opties kiezen voor uw organisatie** sectie, voert u de volgende stappen uit:   
                
    ![Verificatie](./media/zscaler-beta-tutorial/ic800208.png "verificatie")
   
    a. Selecteer **verifiëren met behulp van SAML Single Sign-On**.

    b. Klik op **configureren van eenmalige SAML-aanmelding Parameters**.

1. Op de **configureren SAML Single Sign-On Parameters** dialoogvenster pagina, voer de volgende stappen uit en klik vervolgens op **gedaan**

    ![Single Sign-On](./media/zscaler-beta-tutorial/ic800209.png "Single Sign-On")
    
    a. Plak de **Single Sign-On Service URL voor SAML** waarde die u hebt gekopieerd vanuit de Azure portal in de **URL van de SAML-Portal waarmee gebruikers worden verzonden voor verificatie** tekstvak.
    
    b. In de **aanmeldingsnaam die het kenmerk** tekstvak, type **NameID**.
    
    c. Als u wilt uw gedownloade certificaat uploaden, klikt u op **Zscaler pem**.
    
    d. Selecteer **SAML automatische inrichting inschakelen**.

1. Op de **gebruikersverificatie configureren** dialoogvenster pagina, voert u de volgende stappen uit:

    ![Beheer](./media/zscaler-beta-tutorial/ic800210.png "beheer")
    
    a. Klik op **Opslaan**.

    b. Klik op **nu activeren**.

## <a name="configuring-proxy-settings"></a>Proxy-instellingen configureren
### <a name="to-configure-the-proxy-settings-in-internet-explorer"></a>De proxy-instellingen in Internet Explorer configureren

1. Start **Internet Explorer**.

1. Selecteer **Internetopties** uit de **extra** menu voor open de **Internetopties** dialoogvenster.   
    
     ![Internetopties](./media/zscaler-beta-tutorial/ic769492.png "Internetopties")

1. Klik op de **verbindingen** tabblad.   
  
     ![Verbindingen](./media/zscaler-beta-tutorial/ic769493.png "verbindingen")

1. Klik op **LAN-instellingen** openen de **LAN-instellingen** dialoogvenster.

1. In het gedeelte van de server Proxy de volgende stappen uitvoeren:   
   
    ![Proxyserver](./media/zscaler-beta-tutorial/ic769494.png "proxyserver")

    a. Selecteer **een proxyserver gebruiken voor uw LAN**.

    b. Typ in het tekstvak adres **gateway.zscalerbeta.net**.

    c. Typ in het tekstvak poort **80**.

    d. Selecteer **proxyserver niet gebruiken voor lokale adressen**.

    e. Klik op **OK** sluiten de **Local Area Network (LAN)-instellingen** dialoogvenster.

1. Klik op **OK** sluiten de **Internetopties** dialoogvenster.

> [!TIP]
> U kunt nu een beknopte versie van deze instructies binnen lezen de [Azure-portal](https://portal.azure.com), terwijl het instellen van de app!  Na het toevoegen van deze app uit de **Active Directory > bedrijfstoepassingen** sectie, klikt u op de **Single Sign-On** tabblad en toegang tot de ingesloten documentatie via de  **Configuratie** sectie aan de onderkant. U kunt meer lezen over de documentatie voor embedded-functie: [embedded-documentatie voor Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Het maken van een Azure AD-testgebruiker
Het doel van deze sectie is het maken van een testgebruiker in Azure portal Britta Simon genoemd.

![Azure AD-gebruiker maken][100]

**Als u wilt een testgebruiker maken in Azure AD, moet u de volgende stappen uitvoeren:**

1. In de **Azure-portal**, klik op het navigatiedeelvenster links **Azure Active Directory** pictogram.

    ![Het maken van een Azure AD-testgebruiker](./media/zscaler-beta-tutorial/create_aaduser_01.png) 

1. Als u wilt weergeven in de lijst met gebruikers, gaat u naar **gebruikers en groepen** en klikt u op **alle gebruikers**.
    
    ![Het maken van een Azure AD-testgebruiker](./media/zscaler-beta-tutorial/create_aaduser_02.png) 

1. Om te openen de **gebruiker** dialoogvenster, klikt u op **toevoegen** boven aan het dialoogvenster.
 
    ![Het maken van een Azure AD-testgebruiker](./media/zscaler-beta-tutorial/create_aaduser_03.png) 

1. Op de **gebruiker** dialoogvenster pagina, voert u de volgende stappen uit:
 
    ![Het maken van een Azure AD-testgebruiker](./media/zscaler-beta-tutorial/create_aaduser_04.png) 

    a. In de **naam** tekstvak, type **BrittaSimon**.

    b. In de **gebruikersnaam** tekstvak, type de **e-mailadres** van BrittaSimon.

    c. Selecteer **wachtwoord weergeven** en noteer de waarde van de **wachtwoord**.

    d. Klik op **Create**.
 
### <a name="creating-a-zscaler-beta-test-user"></a>Het maken van een gebruiker Zscaler bètaversie testen

Om in te schakelen in Azure AD-gebruikers zich aanmelden bij Zscaler Bèta, moeten ze worden ingericht op Zscaler Beta. In het geval van Zscaler bèta is inrichten een handmatige taak.

### <a name="to-configure-user-provisioning-perform-the-following-steps"></a>Als u wilt inrichten van gebruikers configureren, moet u de volgende stappen uitvoeren:

1. Meld u aan bij uw **Zscaler Bèta** tenant.

1. Klik op **beheer**.   
   
    ![Beheer](./media/zscaler-beta-tutorial/ic781035.png "beheer")

1. Klik op **Gebruikersbeheer**.   
        
     ![Voeg](./media/zscaler-beta-tutorial/ic781036.png "toevoegen")

1. In de **gebruikers** tabblad **toevoegen**.
      
    ![Voeg](./media/zscaler-beta-tutorial/ic781037.png "toevoegen")

1. In de sectie toevoegen van gebruiker door de volgende stappen uitvoeren:
        
    ![Gebruiker toevoegen](./media/zscaler-beta-tutorial/ic781038.png "gebruiker toevoegen")
   
    a. Type de **UserID**, **weergavenaam gebruiker**, **wachtwoord**, **wachtwoord bevestigen**, en selecteer vervolgens **groepen**en de **afdeling** van een geldige Azure AD-account die u inrichten wilt.

    b. Klik op **Opslaan**.

> [!NOTE]
> U kunt andere hulpprogramma's voor Zscaler bèta gebruiker-account maken of geleverd door Zscaler bèta-API's gebruiken voor het inrichten van gebruikersaccounts van de Azure AD.

### <a name="assigning-the-azure-ad-test-user"></a>Toewijzen aan de gebruiker van de test Azure AD

In deze sectie maakt inschakelen u Britta Simon gebruiken Azure eenmalige aanmelding door toegang te verlenen aan Zscaler Bèta.

![Gebruiker toewijzen][200] 

**Britta Simon om aan te wijzen Zscaler Bèta, moet u de volgende stappen uitvoeren:**

1. Open de weergave toepassingen in de Azure-portal en gaat u naar de mapweergave en Ga naar **bedrijfstoepassingen** klikt u vervolgens op **alle toepassingen**.

    ![Gebruiker toewijzen][201] 

1. Selecteer in de lijst met toepassingen, **Zscaler Bèta**.

    ![Eenmalige aanmelding configureren](./media/zscaler-beta-tutorial/tutorial_zscalerbeta_app.png) 

1. Klik in het menu aan de linkerkant op **gebruikers en groepen**.

    ![Gebruiker toewijzen][202] 

1. Klik op **toevoegen** knop. Selecteer vervolgens **gebruikers en groepen** op **toevoegen toewijzing** dialoogvenster.

    ![Gebruiker toewijzen][203]

1. Op **gebruikers en groepen** dialoogvenster, selecteer **Britta Simon** in de lijst gebruikers.

1. Klik op **Selecteer** op knop **gebruikers en groepen** dialoogvenster.

1. Klik op **toewijzen** op knop **toevoegen toewijzing** dialoogvenster.
    
### <a name="testing-single-sign-on"></a>Eenmalige aanmelding testen

In deze sectie maakt testen u uw Azure AD eenmalige aanmelding configuratie met behulp van het toegangsvenster.

Wanneer u op de bètaversie van de Zscaler-tegel in het toegangsvenster, u moet u automatisch aangemeld bij uw toepassing Zscaler Beta.
Zie voor meer informatie over het toegangsvenster, [Inleiding tot het toegangsvenster](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Aanvullende resources

* [Lijst met zelfstudies over het integreren van SaaS-Apps met Azure Active Directory](tutorial-list.md)
* [What is application access and single sign-on with Azure Active Directory?](../manage-apps/what-is-single-sign-on.md) (Wat houden toegang tot toepassingen en eenmalige aanmelding met Azure Active Directory in?)

<!--Image references-->

[1]: ./media/zscaler-beta-tutorial/tutorial_general_01.png
[2]: ./media/zscaler-beta-tutorial/tutorial_general_02.png
[3]: ./media/zscaler-beta-tutorial/tutorial_general_03.png
[4]: ./media/zscaler-beta-tutorial/tutorial_general_04.png

[100]: ./media/zscaler-beta-tutorial/tutorial_general_100.png

[200]: ./media/zscaler-beta-tutorial/tutorial_general_200.png
[201]: ./media/zscaler-beta-tutorial/tutorial_general_201.png
[202]: ./media/zscaler-beta-tutorial/tutorial_general_202.png
[203]: ./media/zscaler-beta-tutorial/tutorial_general_203.png

