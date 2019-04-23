---
title: AD FS-Problembehandlung - Idp-initiierten anmelden
description: Dieses Dokument beschreibt, wie Sie die Problembehandlung für die AD FS-Anmeldeseite auf der Seite.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 61e9adc708e95a6ab4a82550280737b2f4bad0a1
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844941"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS-Problembehandlung - Idp-initiierten anmelden
Die AD FS-anmelden-Seite kann verwendet werden, um zu testen, und zwar unabhängig davon, ob Authentifizierung funktioniert.  Dies erfolgt durch Navigieren zur Seite, und melden Sie sich.  Darüber hinaus können wir die Anmeldeseite verwenden, um sicherzustellen, dass alle vertrauende SAML 2.0-Seiten aufgeführt sind.

## <a name="enable-the-idp-intiated-sign-on-page"></a>Aktivieren Sie die Idp-initiiert-Anmeldeseite
Standardmäßig muss AD FS unter Windows 2016 nicht die Anmeldung auf der Seite aktiviert.  Um sie zu aktivieren können Sie den PowerShell-Befehl Set-AdfsProperties.  Verwenden Sie das folgende Verfahren, um die Seite zu aktivieren:

1.  Öffnen von Windows PowerShell
2.  Geben Sie ein: `Get-AdfsProperties` und die EINGABETASTE drücken
3.  Überprüfen Sie, ob **EnableIdpInitiatedSignonPage** auf "false" festgelegt ist !["false"](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  Geben Sie in PowerShell:  `Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  Sie werden feststellen, dass eine Bestätigung, also Geben Sie Get-AdfsProperties erneut, und überprüfen Sie, ob **EnableIdpInitatedSignonPage** wird festgelegt auf "true".
!["True"](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>Authentifizierung testen
Verwenden Sie das folgende Verfahren, um AD FS-Authentifizierung mit der Anmeldeseite Idp-Initiated zu testen.

1.  Öffnen Sie einen Webbrowser, und navigieren Sie zu der Idp-Anmeldeseite angezeigt.  Beispiel:  https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  Sie werden aufgefordert, sich anmelden.  Geben Sie Ihre Anmeldeinformationen ein.
![Anmelden](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  Wenn dies erfolgreich war. sollte Sie angemeldet sein.


## <a name="test-authentication-using-a-seamless-logon-experience"></a>Testen Sie die Authentifizierung über eine nahtlose Anmeldung
Sie können die nahtlose anmeldeerfahrung testen, indem Sie sicherstellen, dass die URL für Ihren AD FS-Servern die lokalen Intranetzone die Internet-Optionen hinzugefügt werden.  Gehen Sie folgendermaßen vor:

1.  Klicken Sie auf einem Windows 10-Client klicken Sie auf Start, und geben Sie Internetoptionen, und wählen Sie die Internetoptionen.
2.   Klicken Sie auf der Registerkarte "Sicherheit", klicken Sie auf dem lokalen Intranet, und klicken Sie auf die Schaltfläche "Websites".
![Nahtlose](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  Klicken Sie auf „Erweitert“.
2.  Geben Sie die Url ein, und klicken Sie auf Hinzufügen.  Klicken Sie auf Schließen.
![Url hinzufügen](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  Klicken Sie auf Ok.  Klicken Sie auf Ok.  Dies sollte die Internetoptionen schließen.
2.  Öffnen Sie einen Webbrowser, und navigieren Sie zu der Idp-Anmeldeseite angezeigt.  Beispiel:  https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  Klicken Sie auf die Schaltfläche zur Anmeldung.  Sie sollte automatisch anmelden und nicht zur Eingabe von Anmeldeinformationen aufgefordert.
![Nahtlose](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)