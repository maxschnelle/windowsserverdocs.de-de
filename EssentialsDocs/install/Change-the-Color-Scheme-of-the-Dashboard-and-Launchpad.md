---
title: Ändern des Farbschemas für das Dashboard und das Launchpad
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b2913e51-7979-4d48-a431-d2ec5f1042be
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: a3ffac0b89a62b04b73aada0a49cb755c7e7bd9a
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312287"
---
# <a name="change-the-color-scheme-of-the-dashboard-and-launchpad"></a>Ändern des Farbschemas für das Dashboard und das Launchpad

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können das Farbschema für das Dashboard und das Launchpad ändern, indem Sie die zu verwendenden Farben in einer XML-formatierten Datei definieren, diese XML-Datei in einem Ordner auf dem Server installieren und den Namen der XML-Datei in einem Registrierungseintrag angeben.  
  
## <a name="create-the-xml-file"></a>Erstellen der XML-Datei  
 Im folgenden Beispiel wird der mögliche Inhalt der XML-Datei dargestellt:  
  
```xml  
<DashboardTheme xmlns="https://www.microsoft.com/HSBS/Dashboard/Branding/2010">  
  
  <!-- Hex color values overwriting default SKU theme colors -->  
  
    <SplashScreenBackgroundColor HexValue="FFFFFFFF"/>  
    <SplashScreenBorderColor HexValue="FF000000"/>  
    <MainHeaderBackgroundColor HexValue="FF414141"/>  
    <MainTabBackgroundColor HexValue="FFFFFFFF"/>  
    <MainTabFontColor HexValue="FF999999"/>  
    <MainTabHoverFontColor HexValue="FF0072BC"/>  
    <MainTabSelectedFontColor HexValue="FF0072BC"/>  
    <MainButtonPressedBackgroundColor HexValue="FF0072BC"/>  
    <MainButtonFontColor HexValue="FFFFFFFF"/>  
    <MainButtonBorderColor HexValue="FF6E6E6E"/>  
    <ScrollButtonBackgroundColor HexValue="FFF0F0F0"/>  
    <ScrollButtonArrowColor HexValue="FF999999"/>  
    <ScrollButtonHoverBackgroundColor HexValue="FF999999"/>  
    <ScrollButtonHoverArrowColor HexValue="FF6E6E6E"/>  
    <ScrollButtonSelectedBackgroundColor HexValue="FF6E6E6E"/>  
    <ScrollButtonSelectedArrowColor HexValue="FFFFFFFF"/>  
    <ScrollButtonDisabledBackgroundColor HexValue="FFF8F8F8"/>  
    <ScrollButtonDisabledArrowColor HexValue="FFCCCCCC"/>  
    <AlertTextBlockBackground HexValue="FFFFFFFF"/>  
    <AlertTextBlockFont HexValue="FF000000"/>  
    <FontColor HexValue="FF000000"/>  
    <SubTabBarBackgroundColor HexValue="FFFFFFFF"/>  
    <SubTabBackgroundColor HexValue="FFFFFFFF"/>  
    <SubTabSelectedBackgroundColor HexValue="FF414141"/>  
    <SubTabBorderColor HexValue="FF787878"/>  
    <SubTabFontColor HexValue="FF787878"/>  
    <SubTabHoverFontColor HexValue="FF0072BC"/>  
    <SubTabPressedFontColor HexValue="FFFFFFFF"/>  
    <ListViewColor HexValue="FFFFFFFF"/>  
    <PageBorderColor HexValue="FF999999"/>      
    <LaunchpadButtonHoverBorderColor HexValue="FF6BA0B4"/>  
    <LaunchpadButtonHoverBackgroundColor HexValue="FF41788F"/>  
    <ClientArrowColor HexValue="FFFFFFFF"/>  
    <ClientGlyphColor HexValue="FFFFFFFF"/>  
    <SplitterColor HexValue="FF83C6E2"/>  
    <HomePageBackColor     HexValue="FFFFFFFF"/>  
    <CategoryNotExpandedBackColor HexValue="FFFFB343"/>  
    <CategoryExpandedBackColor HexValue="FFF26522"/>  
    <CategoryNotExpandedForeColor HexValue="FF2A2A2A"/>  
    <CategoryExpandedForeColor HexValue="FFFFFFFF"/>  
    <HomePageTaskListForeColor    HexValue="FF2A2A2A"/>  
    <HomePageTaskListBackColor HexValue="FFEAEAEA"/>  
    <HomePageTaskListHoverForeColor      HexValue="FF2A2A2A"/>  
    <HomePageTaskListItemBorderColor     HexValue="FF999999"/>  
    <HomePageTaskListSelectedForeColor   HexValue="FFFFFFFF"/>  
    <HomePageTaskListSelectedBackColor   HexValue="FFF26522"/>  
    <HomePageTaskDetailStatusForeColor   HexValue="FFF26522"/>  
    <HomePageTaskDetailDescriptionForeColor     HexValue="FF2A2A2A"/>  
    <HomePageLinkForeColor HexValue="FF0072BC"/>  
    <HomePageLinkSelectedForeColor HexValue="FF0054A6"/>  
    <HomePageLinkHoverForeColor   HexValue="FF0072BC"/>  
    <PropertyFormForeColor HexValue="FF2A2A2A"/>  
    <PropertyFormTabHoverColor HexValue="FF0072BC"/>  
    <PropertyFormTabSelectedColor HexValue="FFFFFFFF"/>  
    <PropertyFormTabSelectedBackColor HexValue="FF414141"/>  
    <TaskPanelBackColor HexValue="FFFFFFFF"/>  
    <TaskPanelItemForeColor HexValue="FF2A2A2A"/>  
    <TaskPanelGroupTitleForeColor HexValue="FF2A2A2A"/>  
    <TaskPanelGroupTitleBackColor HexValue="FFCCCCCC"/>  
    <DashboardClientBackColor HexValue="FF004050"/>  
    <DashboardClientTitleColor HexValue="FFFFFFFF"/>  
    <DashboardClientOptionsForeColor HexValue="FFFFFFFF"/>  
    <DashboardClientOptionsItemForeColor HexValue="FF2A2A2A"/>  
    <DashboardClientHelpForeColor HexValue="FF0054A6"/>  
    <ClientSignInForeColor HexValue="FFFFFFFF"/>  
    <ClientSignInWaterMarkForeColor HexValue="FF999999"/>  
    <ClientSignInUserNameForeColor HexValue="FF2A2A2A"/>  
    <ClientSignInPassWordSpecificBackColor HexValue="FFCCCCCC"/>  
    <ClientSignInButtonBackColor HexValue="FF004050"/>  
    <ClientSignInPassWordForeColor HexValue="FF2A2A2A"/>  
    <LaunchPadBackColor HexValue="FF004050"/>  
    <LaunchPadPageTitleColor HexValue="FFFFFFFF"/>  
    <LaunchPadItemForeColor HexValue="FFFFFFFF"/>  
  <LaunchPadItemHoverColor HexValue="33FFFFFF"/>  
  <LaunchPadItemIconBackgroundColor HexValue="F2004050"/>  
</DashboardTheme >  
  
```  
  
> [!IMPORTANT]
>  Die XML-Elemente müssen in der Reihenfolge angegeben werden, die im vorherigen Beispiel aufgeführt ist.  
  
> [!NOTE]
>  Alle Werte für das HexValue-Attribut sind Beispiele von Hexadezimalwerten für Farben. Sie können den Hexadezimalwert einer beliebigen Farbe, die Sie verwenden möchten, eingeben.  
  
 Verwenden Sie Editor oder Visual Studio 2010, um die XML-Datei mit den Tags für die anzupassenden Bereiche zu erstellen. Der Datei kann ein beliebiger Name zugewiesen werden, sie muss lediglich die Erweiterung XML aufweisen. Eine Beschreibung der Bereiche von Dashboard und Launchpad, die angepasst werden können, finden Sie unter [Bereiche von Dashboard und Launchpad, die geändert werden können](Change-the-Color-Scheme-of-the-Dashboard-and-Launchpad.md#BKMK_Dashboard).  
  
#### <a name="to-install-the-xml-file"></a>So installieren Sie die XML-Datei  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **regedit** ein, und klicken Sie dann auf die Anwendung **Regedit**.  
  
3.  Erweitern Sie im linken Bereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft** und **Windows Server**. Wenn der Schlüssel **OEM** nicht vorhanden ist, müssen Sie ihn mit den folgenden Schritten erstellen:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Geben Sie **OEM** als Namen des Schlüssels ein.  
  
4.  Klicken Sie mit der rechten Maustaste auf **OEM**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
5.  Geben Sie **CustomColorScheme** als Namen der Zeichenfolge ein, und drücken Sie dann die **EINGABETASTE**.  
  
6.  Klicken Sie im rechten Bereich mit der rechten Maustaste auf **CustomColorScheme**, und klicken Sie auf **Ändern**.  
  
7.  Klicken Sie auf den Namen der Datei, und klicken Sie dann auf **OK**.  
  
8.  Kopieren Sie die Datei nach "%programFiles%\Windows Server\Bin\OEM". Wenn das Verzeichnis "OEM" nicht vorhanden ist, erstellen Sie es.  
  
##  <a name="dashboard-and-launchpad-areas-that-can-be-changed"></a><a name="BKMK_Dashboard"></a>Bereiche von Dashboard und Launchpad, die geändert werden können  
 In diesem Abschnitt werden Beispiele für anpassbare Bereiche des Dashboards und des Launchpads aufgeführt.  
  
### <a name="examples"></a>Beispiele  
  
####  <a name="figure-1-sign-in-page-of-the-dashboard"></a><a name="BKMK_Figure1"></a>Abbildung 1: Anmeldeseite des Dashboards  
 ![Windows Server Essentials-Dashboard](media/SBS8_ADK_Dashboard_Signin_RC.png "SBS8_ADK_Dashboard_Signin_RC")  
  
####  <a name="figure-2-launchpad"></a><a name="BKMK_Figure2"></a>Abbildung 2: launchpad  
 ![Windows SSB-Launchpad&#45;-Anmeldung](media/SBS8_ADK_LaunchpadSignin2.png "SBS8_ADK_LaunchpadSignin2")  
  
####  <a name="figure-3-sign-in-page-of-the-launchpad"></a><a name="BKMK_Figure3"></a>Abbildung 3: Anmeldeseite des Launchpad  
 ![Windows Server Essentials-launchpad](media/SBS8_ADK_Launchpad_Signin_RC.png "SBS8_ADK_Launchpad_Signin_RC")  
  
####  <a name="figure-4-dashboard-text"></a><a name="BKMK_Figure4"></a>Abbildung 4: dashboardtext  
 ![Windows Server Essentials-Navigationsbereich](media/SBS8_ADK_Navigation_RC.png "SBS8_ADK_Navigation_RC")  
  
####  <a name="figure-5-subtab-border"></a><a name="BKMK_Figure5"></a>Abbildung 5: Rahmen für untergeordnete Registerkarten  
 ![Windows SSB-Dashboard-unter Registerkarten Rahmen](media/SBS8_ADK_DashboardSubtabborder.png "SBS8_ADK_DashboardSubtabborder")  
  
####  <a name="figure-6-task-pane"></a><a name="BKMK_Figure6"></a>Abbildung 6: Aufgabenbereich  
 ![Aufgabenbereich des Windows SSB-Dashboards](media/SBS8_ADK_DashboardTaskPane.png "SBS8_ADK_DashboardTaskPane")  
  
####  <a name="figure-7a-product-splash-screen"></a><a name="BKMK_Figure9"></a>Abbildung 7a: Begrüßungsbildschirm des Produkts  
 ![Windows Server Essentials-Begrüßungsbildschirm](media/SBS8_ADK_productspalshscreen_RC.png "SBS8_ADK_productspalshscreen_RC")  
  
#### <a name="figure-7b-home-page"></a>Abbildung 7b: Startseite  
 ![Windows Server Essentials-Startseite](media/SBS8_ADK_Dashboard_HomePage_RC.png "SBS8_ADK_Dashboard_HomePage_RC")  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)