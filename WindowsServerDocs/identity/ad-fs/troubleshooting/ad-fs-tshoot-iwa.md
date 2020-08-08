---
title: 'AD FS Problembehandlung: integrierte Windows-Authentifizierung'
description: Dieses Dokument beschreibt die Problembehandlung für die integrierte Windows-Authentifizierung.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.openlocfilehash: 4c1823e1cbfc58e50c7231293b846c31480e01a6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87954156"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>AD FS Problembehandlung: integrierte Windows-Authentifizierung
Die integrierte Windows-Authentifizierung ermöglicht es Benutzern, sich mit Ihren Windows-Anmelde Informationen anzumelden und einmaliges Anmelden (Single-Sign-on, SSO) mithilfe von Kerberos oder NTLM auszuführen.

## <a name="reason-integrated-windows-authentication-fails"></a>Grund für die integrierte Windows-Authentifizierung
Es gibt drei Hauptgründe, warum die integrierte Windows-Authentifizierung fehlschlägt. Sie lauten wie folgt:
    - Falsche Konfiguration des Dienst Prinzipal namens (SPN)
    - Kanal Bindungs Token
    - Internet Explorer-Konfiguration

## <a name="spn-misconfiguration"></a>SPN-Fehlkonfiguration
Ein Dienst Prinzipal Name (Service Principal Name, SPN) ist ein eindeutiger Bezeichner einer Dienst Instanz. SPNs werden von der Kerberos-Authentifizierung verwendet, um eine Dienst Instanz einem Dienst Anmelde Konto zuzuordnen. Dadurch kann eine Client Anwendung anfordern, dass der Dienst ein Konto authentifiziert, auch wenn der Client nicht über den Kontonamen verfügt.

Ein Beispiel für einen SPN, der mit AD FS verwendet wird, sieht wie folgt aus:
1. Ein Webbrowser fragt Active Directory ab, um zu bestimmen, welches Dienst Konto ausgeführt wird STS.contoso.com
2. Active Directory teilt dem Browser mit, dass es sich um das AD FS Dienst Konto handelt.
3. Der Browser erhält ein Kerberos-Ticket für das AD FS-Dienst Konto.

Wenn für das AD FS-Dienst Konto ein falsch konfigurierter oder falscher SPN vorliegt, kann dies zu Problemen führen.  Wenn Sie sich Netzwerk Ablauf Verfolgungen ansehen, werden möglicherweise Fehler wie "krb-Fehler: KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN" angezeigt.

Mithilfe von Netzwerk Ablauf Verfolgungen (z. b. wireshark) können Sie feststellen, welcher SPN vom Browser aufgelöst werden soll. Anschließend können Sie mit dem Befehlszeilen Tool Setspn-Q <spn> eine Suche nach diesem SPN durchführen.  Sie wird möglicherweise nicht gefunden, oder Sie kann einem anderen Konto zugewiesen werden, außer dem AD FS-Dienst Konto.

![Verbund](media/ad-fs-tshoot-iwa/iwa3.png)

Sie können den SPN überprüfen, indem Sie sich die Eigenschaften des AD FS-Dienst Kontos ansehen.

![Verbund](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>Kanal Bindungs Token
Aktuell wird zunächst ein Transport Level Security (TLS)-Kanal eingerichtet und eine Authentifizierung über diesen Kanal durchgeführt, wenn sich eine Clientanwendung mit Kerberos, Hashwert oder NTLM mit HTTPS im Server authentifiziert.

Das channelbindungstoken ist eine Eigenschaft des TLS-gesicherten äußeren Kanals und wird verwendet, um den äußeren Kanal an eine Konversation über den Client authentifizierten inneren Kanal zu binden.

Wenn ein "man-in-the-Middle"-Angriff stattfindet und der SSL-Datenverkehr deverschlüsselt und erneut verschlüsselt wird, stimmt der Schlüssel nicht mit dem Schlüssel identisch.  AD FS wird feststellen, dass sich zwischen dem Web-Browse r und dem selbst etwas befindet, das sich in der Mitte befindet.  Dadurch tritt bei der Kerberos-Authentifizierung ein Fehler auf, und der Benutzer wird anstelle eines einmaligen Anmeldens in einem 401-Dialogfeld aufgefordert.

Dies kann folgende Ursachen haben:
 - alles zwischen dem Browser und dem AD FS
 - Fiddler
 - Reverseproxys mit SSL

Standardmäßig ist für AD FS dieser Wert auf "zulassen" festgelegt.  Sie können diese Einstellung mithilfe von PowerShell-Cmdlet ändern.`Set-ADFSProperties -ExtendProtectionTokenCheck`

Weitere Informationen hierzu finden Sie unter [bewährte Methoden für die sichere Planung und Bereitstellung von AD FS](../../ad-fs/design/best-practices-for-secure-planning-and-deployment-of-ad-fs.md).

## <a name="internet-explorer-configuration"></a>Internet Explorer-Konfiguration
Internet Explorer wird standardmäßig wie folgt verwendet:

1. Internet Explorer empfängt eine 401-Antwort von AD FS mit dem Wort aushandeln in der Kopfzeile.
2. Dies weist den Webbrowser an, ein Kerberos-oder NTLM-Ticket zu erhalten, das an AD FS zurückgesendet werden soll.
3. Standardmäßig versucht Internet Explorer, dies (spnetgo) ohne Benutzerinteraktion auszuführen, wenn sich das Wort aushandeln in der Kopfzeile befindet.  Dies funktioniert nur für Intranetsites.

Es gibt zwei Haupt Dinge, die dies verhindern können.
   - Aktivieren der integrierten Windows-Authentifizierung ist nicht in den Eigenschaften von IE aktiviert.  Diese befindet sich unter "Internet Optionen" > "Erweiterte > Sicherheit".

   ![Verbund](media/ad-fs-tshoot-iwa/iwa4.png)

   - Sicherheitszonen sind nicht ordnungsgemäß konfiguriert.
       - Voll qualifizierte Domänen Namen befinden sich nicht in der Intranetzone
       - AD FS-URL befindet sich nicht in der Intranetzone.

      ![Verbund](media/ad-fs-tshoot-iwa/iwa5.png)
## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)
