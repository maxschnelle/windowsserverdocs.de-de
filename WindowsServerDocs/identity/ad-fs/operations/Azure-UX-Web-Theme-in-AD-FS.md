---
title: Azure AD-UX-Design in AD FS
description: "Im folgende Dokument wird beschrieben, wie Sie die AD FS Forms-Anmeldung zu ändern, sodass sie die Azure AD-Benutzeroberfläche ähnelt."
author: billmath
ms.author: billmath
manager: femila
ms.date: 10/24/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: e7bac1db17eb4facc7643fe0db0ccf00c119a45d
ms.sourcegitcommit: 9278435cbfa8dbeb30d0557ed0d27832b154edd2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/09/2018
---
# <a name="using-an-azure-ad-ux-web-theme-in-active-directory-federation-services"></a>Verwenden ein Azure AD-UX-Design in Active Directory-Verbunddienste
Melden Sie sich die AD FS-Formulare spiegeln derzeit nicht die Azure oder O365 anmelden.  Um eine nahtlose und einheitliche Erfahrung für Endbenutzer bereitstellen, haben wir die folgenden cascading Stylesheet Web-Design veröffentlicht, die auf Ihre AD FS-Server angewendet werden können.  Derzeit die Forms-Anmeldung für AD FS in Windows Server2016 sieht wie folgt:

![Aktuelle Anmeldung](media/Azure-UX-Web-Theme-in-AD-FS/one.png)


Mit dem neuen Stylesheet sucht die Benutzeroberfläche wie die Azure und Office365-Anmeldung Umgebungen.

## <a name="download-the-css-style-sheet"></a>Laden Sie das CSS-Stylesheet
Sie können das Design aus den folgenden Github herunterladen [Speicherort ](https://github.com/Microsoft/adfsWebCustomization/tree/master/centeredUi).


## <a name="enabling-the-new-web-theme"></a>Aktivieren das neue Webdesign
So aktivieren Sie das neue Webdesign gehen:

### <a name="to-enable-the-new-azure-ad-ux-web-theme-in-ad-fs"></a>So aktivieren Sie die neue Azure AD-UX Design in AD FS
1.  Starten Sie PowerShell als Administrator
2.  Erstellen Sie eine neue Webdesign mithilfe von PowerShell:  `New-AdfsWebTheme –Name custom –StyleSheet @{path="c:\NewTheme.css"}`
3.  Legen Sie das neue Design als das aktive Design mithilfe von PowerShell: <ph x="1">"Set-AdfsWebConfig – ActiveThemeName Custom"
! [</ph>PowerShell](media/Azure-UX-Web-Theme-in-AD-FS/two.png)
4.  Testen der Anmeldung, indem Sie zu https://<AD FS name.domain>/adfs/ls/idpinitiatedsignon.htm ![anmelden](media/Azure-UX-Web-Theme-in-AD-FS/three.png)

>! [HINWEIS] Sie müssen sicherstellen, dass die Idpinitiatedsignon aktiviert wurde.  Es ist nicht standardmäßig aktiviert.  Zum Aktivieren der Idpinitiatedsignon verwenden Sie des folgenden PowerShell-Befehls:  `Set-AdfsProperties –EnableIdpInitiatedSignonPage $True`

## <a name="image-recommendations"></a>Bild-Empfehlungen
Im Folgenden sind die Empfehlungen für das Hintergrundbild und das Logobild:

### <a name="logo"></a>Logo
- Wert 24 px fest Höhe, 256px maximale Breite
- Abstand um das Logo in das Element nicht hinzugefügt werden.  Stellen Sie sicher, dass das Element Hintergrund transparent ist.

### <a name="background"></a>Hintergrund
- Größe von 1024 x 1080 Pixel mit einer Dateigröße von höchstens 200KB.  Verwenden Sie die höchste Auflösung Seitenverhältnis 16:9/16:10, die die Bildgröße unter die Beschränkung bleibt.

## <a name="next-steps"></a>Nächste Schritte
- [AD FS-Anpassung in Windows Server 2016](AD-FS-Customization-in-Windows-Server-2016.md)
- [Erweiterte Anpassung](Advanced-Customization-of-AD-FS-Sign-in-Pages.md)
- [Benutzerdefinierte Webdesigns](Custom-Web-Themes-in-AD-FS.md)
