---
title: Azure AD UX-Webdesign in AD FS
description: Im folgenden Dokument wird beschrieben, wie Sie die Anmeldung von AD FS Formularen ändern, damit Sie der Azure AD Benutzer Darstellung ähnelt.
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 25ba9505f3f93fb236d6e60e49efc4206482f977
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70866008"
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Verwenden eines Azure AD UX-Webdesigns in Active Directory-Verbunddienste (AD FS)
Der Anmeldevorgang von AD FS Formularen spiegelt derzeit nicht die Anmeldung bei Azure/O365 wider.  Um Endbenutzern eine einheitlichere und reibungslose Darstellung zu bieten, haben wir das folgende Cascading Stylesheet-Webdesign veröffentlicht, das auf Ihre AD FS Server angewendet werden kann.  Derzeit sieht die Formular Anmeldung für AD FS unter Windows Server 2016 wie folgt aus:

![Aktuelle Anmeldung](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


Mit dem neuen Stylesheet sieht die Benutzererfahrung eher wie die Anmelde Erfahrung von Azure und Office 365 aus.

## <a name="download-the-css-style-sheet"></a>Herunterladen des CSS-Stylesheets
Sie können das Webdesign von folgendem GitHub- [Speicherort](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi)herunterladen.


## <a name="enabling-the-new-web-theme"></a>Aktivieren des neuen Webdesigns
Um das neue Webdesign zu aktivieren, verwenden Sie das folgende Verfahren:

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>So aktivieren Sie das neue Azure AD UX-Webdesign in AD FS
1. Starten Sie PowerShell als Administrator.
2. Erstellen Sie ein neues Webdesign mithilfe von PowerShell:`New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3. Legen Sie das neue Design mithilfe von PowerShell als aktives Design fest:  `Set-AdfsWebConfig -ActiveThemeName custom`
   ![PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4. Testen Sie die Anmeldung, indem Sie zu https://<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![Sign-on wechseln.](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

> ! Nebenbei Sie müssen sicherstellen, dass "idpinitiatedsignon aktiviert ist.  Er ist standardmäßig nicht aktiviert.  Verwenden Sie den folgenden PowerShell-Befehl, um "idpinitiatedsignon zu aktivieren:`Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>Bild Empfehlungen
Wenn Sie die zentrierte Benutzeroberfläche aktivieren, können Sie die gleichen Images für Hintergrund und Logo verwenden, die Sie möglicherweise bereits für Azure Active Directory Unternehmens Branding besitzen. Im Allgemeinen gelten die gleichen Empfehlungen für Größe, Verhältnis und Format.

### <a name="logo"></a>Logo

Beschreibung | Einschränkungen | Empfehlungen
------- | ------- | ----------
Das Logo wird oben im Anmelde Panel angezeigt. | Transparentes JPG oder PNG<br>Maximale Höhe: 36 px<br>Maximale Breite: 245 px | Verwenden Sie das Logo Ihrer Organisation hier.<br>Verwenden Sie ein transparentes Bild. Gehen Sie nicht davon aus, dass der Hintergrund weiß ist.<br>Fügen Sie im Bild keine Auffüll Zeichen um Ihr Logo hinzu, da Ihr Logo unverhältnismäßig klein aussehen wird.

### <a name="background"></a>Hintergrund

Beschreibung | Einschränkungen | Empfehlungen
------- | ------- | ----------
Diese Option wird im Hintergrund der Anmeldeseite angezeigt, ist in der Mitte des sichtbaren Bereichs verankert, und skaliert und mit dem Bildschirm, um das Browserfenster auszufüllen.    <br>Auf schmalen Bildschirmen, wie z. b. Mobiltelefonen, wird dieses Bild nicht angezeigt.<br>Beim Laden der Seite wird auf dieses Bild eine schwarze Maske mit 0,55 Deckkraft angewendet. | JPG oder PNG<br>Bild Dimensionen: 1920 x 1080 px<br>Dateigröße: &lt;300 KB | <br>Verwenden Sie Bilder, bei denen es keinen starken Fokus hat. Das nicht transparente Anmeldeformular wird über dem Mittelpunkt dieses Bilds angezeigt und kann abhängig von der Größe des Browserfensters einen beliebigen Teil des Bilds abdecken.<br>Halten Sie die Dateigröße gering, um schnelle Ladezeiten sicherzustellen.

## <a name="next-steps"></a>Nächste Schritte
- [AD FS Anpassung in Windows Server 2016](AD-FS-Customization-in-Windows-Server-2016.md)
- [Erweiterte Anpassung](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [Benutzerdefinierte Webdesigns](Custom-Web-Themes-in-AD-FS.md)
