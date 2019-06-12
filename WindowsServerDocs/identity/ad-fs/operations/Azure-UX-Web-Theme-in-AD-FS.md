---
title: Azure AD-UX-Webdesign in AD FS
description: Das folgende Dokument beschreibt, wie Sie die AD FS Forms-Anmeldung zu ändern, sodass sie die Azure AD-Benutzeroberfläche ähnelt.
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1064084fe357e54d7230f58e486aa4e62958f6ae
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445013"
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Verwenden ein Azure AD-UX-Web-Design in Active Directory-Verbunddienste
Die AD FS forms Sign in derzeit spiegelt keine Azure oder O365-Anmeldung.  Um eine nahtlose und einheitliche Erfahrung für Endbenutzer zu gewährleisten, haben wir die folgenden kaskadierenden Web Stylesheetdesign veröffentlicht, die auf AD FS-Server angewendet werden können.  Derzeit die Forms-Anmeldung für AD FS unter Windows Server 2016 sieht wie folgt aus:

![Aktuelle Anmeldung](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


Mit dem neuen Stylesheet sieht die Azure- und Office 365-Anmeldung Benutzeroberflächen eher die benutzerfreundlichkeit.

## <a name="download-the-css-style-sheet"></a>Laden Sie das CSS-Stylesheet
Sie können das Webdesign aus den folgenden Github [Speicherort](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi).


## <a name="enabling-the-new-web-theme"></a>Aktivieren das neue Webdesign
Verwenden Sie zum aktivieren das neue Webdesign wie folgt vor:

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>So aktivieren Sie das neue Azure AD-UX-Webdesign in AD FS
1. Starten Sie PowerShell als Administrator
2. Erstellen Sie ein neues Webdesign mithilfe von PowerShell ein:  `New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3. Legen Sie das neue Design als das aktive Design mithilfe von PowerShell ein:  `Set-AdfsWebConfig -ActiveThemeName custom`
   ![PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4. Testen Sie die Anmeldung, indem Sie zu https://<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![anmelden](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> ! [HINWEIS] Sie müssen sicherstellen, dass diese "idpinitiatedsignon" aktiviert wurde.  Es ist nicht standardmäßig aktiviert.  So aktivieren Sie "idpinitiatedsignon" mit dem folgenden PowerShell-Befehl:  `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>Image-Empfehlungen
Aktivieren die zentrierte Benutzeroberfläche können Sie die gleichen Bilder für den Hintergrund und das Logo, die Sie möglicherweise bereits für Azure Active Directory-Unternehmensbranding verwenden. Im Allgemeinen gelten dieselben Empfehlungen für die Größe, Verhältnis und Format.

### <a name="logo"></a>Logo

Beschreibung | Einschränkungen | Empfehlungen
------- | ------- | ----------
Das Logo wird auf den Bereich der Anmeldung angezeigt. | Transparente JPG- oder PNG-Datei<br>Max. Höhe: 36 px<br>Max. Breite: 245 px | Verwenden Sie hier das Logo Ihrer Organisation.<br>Verwenden Sie ein transparentes Bild. Denken Sie nicht, dass der Hintergrund weiß ist.<br>Fügen Sie keine Auffüllung rund um Ihr Logo im Bild oder Ihr Logo unverhältnismäßig klein aussehen wird.

### <a name="background"></a>Hintergrund

Beschreibung | Einschränkungen | Empfehlungen
------- | ------- | ----------
Diese Option wird im Hintergrund der Anmeldeseite angezeigt, ist in die Mitte des sichtbaren Bereichs, skaliert und Kulturen, füllen Sie das Browserfenster verankert.    <br>Auf schmalen Bildschirmen, z.B. von Mobiltelefonen wird dieses Bild nicht angezeigt.<br>Wenn die Seite geladen wird, wird eine schwarze Maske mit einer Deckkraft von 0,55 auf dieses Bild angewendet. | JPG- oder PNG<br>Bildmaße: 1920 x 1080 Pixel<br>Dateigröße: &lt; 300 KB | <br>Verwenden von Images, gibt es keine starke Betreff Schwerpunkt. Das nicht transparente Anmeldeformular wird über dem Mittelpunkt dieses Bilds angezeigt und kann einen beliebigen Teil der Abbildung ist abhängig von der Größe des Browserfensters abdecken.<br>Halten Sie die Dateigröße klein, um schnelle Ladezeiten sicherzustellen.

## <a name="next-steps"></a>Nächste Schritte
- [AD FS-Anpassung unter WindowsServer 2016](AD-FS-Customization-in-Windows-Server-2016.md)
- [Erweiterte Anpassung](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [Benutzerdefinierte Webdesigns](Custom-Web-Themes-in-AD-FS.md)
