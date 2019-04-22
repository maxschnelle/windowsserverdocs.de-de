---
title: AD FS-Problembehandlung – integrierte Windows-Authentifizierung
description: In diesem Dokument wird beschrieben, wie integrierte Windows-Authentifizierung zu beheben
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 91f252f5b0eca0f4c44e0b1a4564037298bf023c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814061"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>AD FS-Problembehandlung – integrierte Windows-Authentifizierung
Integrierte Windows-Authentifizierung kann Benutzer sich mit ihren Windows-Anmeldeinformationen und die benutzerfreundlichkeit-einmaliges Anmelden (SSO) mit Kerberos oder NTLM anzumelden.

## <a name="reason-integrated-windows-authentication-fails"></a>Integrierte Windows-Authentifizierung Grund ein Fehler auftritt
Es gibt drei Hauptgründe dafür, warum die integrierte Windows-Authentifizierung fehl. Die Überladungen sind:
    - Dienstprinzipal Name(SPN) Fehlkonfiguration
    - Kanalbindungstoken
    - Internet Explorer-Konfiguration

## <a name="spn-misonfiguration"></a>SPN-misonfiguration
Ein Dienstprinzipalname (SPN) ist ein eindeutiger Bezeichner einer Dienstinstanz. SPNs werden durch die Kerberos-Authentifizierung verwendet, ein Dienstkonto für die Anmeldung eine Dienstinstanz zugeordnet. Dadurch wird eine Client-Anwendung, um anzufordern, dass der Dienst ein Konto zu authentifizieren, auch wenn der Client keinen den Kontonamen.

Ein Beispiel einer ein SPN wird verwendet, mit AD FS ist wie folgt:
1. Ein Webbrowser fragt Active Directory, um zu bestimmen, welches Dienstkonto "STS.contoso.com" ausgeführt wird
2. Active Directory informiert den Browser, dass es sich um die AD FS-Dienstkonto ist.
3. Der Browser wird ein Kerberos-Ticket für das AD FS-Dienstkonto angezeigt.

Wenn das AD FS-Dienstkonto ein falsch konfigurierter oder den falschen SPN verfügt, kann dies Probleme verursachen.  Betrachten netzwerkablaufverfolgungsdaten, werden möglicherweise Fehler wie z. B. KRB Fehler angezeigt: KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

Mithilfe der netzwerkablaufverfolgungen (z. B. Wireshark) Sie können bestimmen, welche SPN der Browser versucht, zu beheben, und klicken Sie dann über die Befehlszeile, Setspn – Q tool <spn>, erreichen Sie eine Suche auf, dass dieser SPN.  Nicht gefunden werden kann, oder er kann auf ein anderes Konto als das AD FS-Dienstkonto zugewiesen werden.

![integriert](media/ad-fs-tshoot-iwa/iwa3.png)

Sie können den SPN überprüfen, indem Sie über die Eigenschaften des AD FS-Dienstkontos.

![integriert](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>Kanalbindungstoken
Derzeit Wenn eine Clientanwendung selbst auf dem Server mit Kerberos, Hashwert oder NTLM mit HTTPS authentifiziert wird, wird zunächst ein Transport Level Security (TLS)-Kanal eingerichtet und Authentifizierung erfolgt über diesen Kanal. 

Der Channel Binding Token ist eine Eigenschaft des CBT-gesicherten außenkanals und wird verwendet, um des außenkanals an eine Konversation über den clientauthentifizierten inneren Kanal zu binden.

Befindet sich einem "Man-in-the-Middle"-Angriffe, die auftreten, und sie werden de--Verschlüsselung und erneute Verschlüsselung der SSL-Datenverkehr, und der Schlüssel stimmen nicht überein.  AD FS bestimmt, dass etwas in der Mitte zwischen dem Web durchsuchen r und sich selbst befinden.  Dies bewirkt, dass die Kerberos-Authentifizierung fehlschlägt, und der Benutzer wird aufgefordert werden, mit einem 401 Dialogfeld anstelle von SSO-Funktionen.

Dies kann die Ursache von sein:
 - alles zwischen dem Browser und AD FS sitzen
 - Fiddler
 - Ausführen von SSL-bridging Reverseproxys

Standardmäßig hat AD FS auf "zulassen" festgelegt.  Sie können diese Einstellung mithilfe der PowerShell-Cmdlet ändern. `Set-ADFSProperties -ExtendProtectionTokenCheck`

Weitere Informationen zu dieser finden Sie unter [bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md).

## <a name="internet-explorer-configuration"></a>Internet Explorer-Konfiguration
Standardmäßig werden InternetExplorer müssen wie folgt:

1. InternetExplorer wird eine 401-Antwort von AD FS mit dem Wort "NEGOTIATE" in der Kopfzeile erhalten.
2. Dies weist den Webbrowser, um ein Kerberos oder NTLM-Ticket zum Zurücksenden an AD FS zu erhalten.
3. Standardmäßig versucht Internet Explorer diese (SPNEGO) ohne Eingreifen des Benutzers zu tun, wenn das Wort NEGOTIATE im Header.  Es funktioniert nur für Websites im Intranet.

Es gibt 2 Dinge, die dies Happeing verhindern können.
   - Integrierte Windows-Authentifizierung aktivieren, wird in den Eigenschaften von IE nicht überprüft.  Diese finden Sie unter "Internetoptionen" -> Erweitert -> Sicherheit.
![integrated](media/ad-fs-tshoot-iwa/iwa4.png)
   
   - Sicherheitszonen sind nicht ordnungsgemäß konfiguriert.
       - Bei FQDNs wird nicht in der Intranetzone
       - AD FS-URL ist nicht in der Intranetzone.

![integriert](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)