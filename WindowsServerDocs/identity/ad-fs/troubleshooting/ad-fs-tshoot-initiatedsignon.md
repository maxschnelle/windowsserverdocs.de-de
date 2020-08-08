---
title: 'AD FS Problembehandlung: durch IDP initiierte Anmeldung'
description: In diesem Dokument wird beschrieben, wie Sie Probleme bei der AD FS Anmeldeseite beheben.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/03/2017
ms.topic: article
ms.openlocfilehash: 4eb39b697b3dd31dc0a6e3581bdb33437b462197
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87969707"
---
# <a name="ad-fs-troubleshooting---idp-initiated-sign-on"></a>AD FS Problembehandlung: durch IDP initiierte Anmeldung
Mithilfe der AD FS Anmeldeseite können Sie überprüfen, ob die Authentifizierung funktioniert.  Dies erfolgt durch Navigieren zur Seite und anmelden.  Außerdem können wir die Anmeldeseite verwenden, um zu überprüfen, ob alle vertrauenden Seiten von SAML 2,0 aufgeführt sind.

## <a name="enable-the-idp-initiated-sign-on-page"></a>Aktivieren der IDP-initiierten Anmeldeseite
Standardmäßig ist für AD FS in Windows 2016 die Anmeldeseite nicht aktiviert.  Um es zu aktivieren, können Sie den PowerShell-Befehl Set-adfsproperties verwenden.  Verwenden Sie das folgende Verfahren, um die Seite zu aktivieren:

1.  Öffnen von Windows PowerShell
2.  EINGABETASTE: `Get-AdfsProperties` drücken Sie die EINGABETASTE
3.  Vergewissern Sie sich, dass **enableidpinitiatedsignonpage** auf false false festgelegt ist. ![](media/ad-fs-tshoot-initiatedsignon/idp2.png)
4.  Geben Sie in PowerShell Folgendes ein:`Set-AdfsProperties -EnableIdpInitiatedSignonPage $true`
5.  Es wird keine Bestätigung angezeigt. Geben Sie daher Get-adfsproperties erneut ein, und überprüfen Sie, ob **enableidpinitatedsignonpage** auf true festgelegt ist.
![Wahr](media/ad-fs-tshoot-initiatedsignon/idp4.png)

## <a name="test-authentication"></a>Authentifizierung testen
Verwenden Sie das folgende Verfahren, um AD FS Authentifizierung mit der IDP-initiierten Anmeldeseite zu testen.

1.  Öffnen Sie einen Webbrowser, und navigieren Sie zur IDP-Anmeldeseite.  Beispiel: https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
2.  Sie sollten aufgefordert werden, sich anzumelden.  Geben Sie Ihre Anmeldeinformationen ein.
![Anmelden](media/ad-fs-tshoot-initiatedsignon/idp5.png)
3.  Wenn dies erfolgreich war, sollten Sie angemeldet sein.


## <a name="test-authentication-using-a-seamless-logon-experience"></a>Testen der Authentifizierung mithilfe einer nahtlosen Anmeldung
Sie können die nahtlose Anmeldung testen, indem Sie sicherstellen, dass die URL für Ihre AD FS Server der lokalen Intranetzone ihrer Internetoptionen hinzugefügt wird.  Gehen Sie dazu wie folgt vor:

1.  Klicken Sie auf einem Windows 10-Client auf Start, geben Sie Internetoptionen ein, und wählen Sie Internetoptionen aus.
2.   Klicken Sie auf die Registerkarte Sicherheit, klicken Sie auf Lokales Intranet, und klicken Sie auf die Schaltfläche Sites.
![Naht](media/ad-fs-tshoot-initiatedsignon/idp8.png)
1.  Klicken Sie auf Erweitert.
2.  Geben Sie die URL ein, und klicken Sie auf Hinzufügen  Klicken Sie auf "Schließen".
![URL hinzufügen](media/ad-fs-tshoot-initiatedsignon/idp9.png)
1.  Klicken Sie auf "OK".  Klicken Sie auf "OK".  Dadurch sollten die Internetoptionen geschlossen werden.
2.  Öffnen Sie einen Webbrowser, und navigieren Sie zur IDP-Anmeldeseite.  Beispiel: https://sts.contoso.com/adfs/ls/idpinitiatedsignon.htm
3.  Klicken Sie auf die Schaltfläche anmelden.  Sie sollten sich automatisch anmelden und nicht zur Eingabe von Anmelde Informationen aufgefordert werden.
![Naht](media/ad-fs-tshoot-initiatedsignon/idp6.png)

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
