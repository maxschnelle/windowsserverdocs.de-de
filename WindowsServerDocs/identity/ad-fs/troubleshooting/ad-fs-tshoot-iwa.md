---
title: 'AD FS Problembehandlung: integrierte Windows-Authentifizierung'
description: Dieses Dokument beschreibt die Problembehandlung für die integrierte Windows-Authentifizierung.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 02/21/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 98f6c2e39b2a5eeab76103c1ae477dde785a0e04
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385393"
---
# <a name="ad-fs-troubleshooting---integrated-windows-authentication"></a>AD FS Problembehandlung: integrierte Windows-Authentifizierung
Die integrierte Windows-Authentifizierung ermöglicht es Benutzern, sich mit Ihren Windows-Anmelde Informationen anzumelden und einmaliges Anmelden (Single-Sign-on, SSO) mithilfe von Kerberos oder NTLM auszuführen.

## <a name="reason-integrated-windows-authentication-fails"></a>Grund für die integrierte Windows-Authentifizierung
Es gibt drei Hauptgründe, warum die integrierte Windows-Authentifizierung fehlschlägt. Die Überladungen sind:
    - Falsche Konfiguration des Dienst Prinzipal namens (SPN)
    - Kanal Bindungs Token
    - Internet Explorer-Konfiguration

## <a name="spn-misconfiguration"></a>SPN-Fehlkonfiguration
Ein Dienst Prinzipal Name (Service Principal Name, SPN) ist ein eindeutiger Bezeichner einer Dienst Instanz. SPNs werden von der Kerberos-Authentifizierung verwendet, um eine Dienst Instanz einem Dienst Anmelde Konto zuzuordnen. Dadurch kann eine Client Anwendung anfordern, dass der Dienst ein Konto authentifiziert, auch wenn der Client nicht über den Kontonamen verfügt.

Ein Beispiel für einen SPN, der mit AD FS verwendet wird, sieht wie folgt aus:
1. Ein Webbrowser fragt Active Directory ab, um zu bestimmen, welches Dienst Konto ausgeführt wird STS.contoso.com
2. Active Directory teilt dem Browser mit, dass es sich um das AD FS Dienst Konto handelt.
3. Der Browser erhält ein Kerberos-Ticket für das AD FS-Dienst Konto.

Wenn für das AD FS-Dienst Konto ein falsch konfigurierter oder falscher SPN vorliegt, kann dies zu Problemen führen.  Bei der Betrachtung von Netzwerk Ablauf Verfolgungen werden möglicherweise Fehler wie z. b. krb-Fehler angezeigt: KRB5KDC_ERR_S_PRINCIPAL_UNKNOWN.

Mithilfe von Netzwerk Ablauf Verfolgungen (z. b. wireshark) können Sie feststellen, welcher SPN vom Browser aufgelöst werden soll. Anschließend können Sie das Befehlszeilen Tool Setspn-Q <spn> verwenden, um einen Suchvorgang für den SPN durchzuführen.  Sie wird möglicherweise nicht gefunden, oder Sie kann einem anderen Konto zugewiesen werden, außer dem AD FS-Dienst Konto.

![Verbund](media/ad-fs-tshoot-iwa/iwa3.png)

Sie können den SPN überprüfen, indem Sie sich die Eigenschaften des AD FS-Dienst Kontos ansehen.

![Verbund](media/ad-fs-tshoot-iwa/iwa1.png)

## <a name="channel-binding-token"></a>Kanal Bindungs Token
Wenn sich eine Client Anwendung derzeit mithilfe von Kerberos, Digest oder NTLM mithilfe von HTTPS beim Server authentifiziert, wird zunächst ein Transport Level Security (TLS)-Kanal eingerichtet, und die Authentifizierung erfolgt mithilfe dieses Kanals. 

Das channelbindungstoken ist eine Eigenschaft des TLS-gesicherten äußeren Kanals und wird verwendet, um den äußeren Kanal an eine Konversation über den Client authentifizierten inneren Kanal zu binden.

Wenn ein "man-in-the-Middle"-Angriff stattfindet und der SSL-Datenverkehr deverschlüsselt und erneut verschlüsselt wird, stimmt der Schlüssel nicht mit dem Schlüssel identisch.  AD FS wird feststellen, dass sich zwischen dem Web-Browse r und dem selbst etwas befindet, das sich in der Mitte befindet.  Dadurch tritt bei der Kerberos-Authentifizierung ein Fehler auf, und der Benutzer wird anstelle eines einmaligen Anmeldens in einem 401-Dialogfeld aufgefordert.

Dies kann folgende Ursachen haben:
 - alles zwischen dem Browser und dem AD FS
 - Fiddler
 - Reverseproxys mit SSL

Standardmäßig ist für AD FS dieser Wert auf "zulassen" festgelegt.  Sie können diese Einstellung mithilfe von PowerShell-Cmdlet ändern `Set-ADFSProperties -ExtendProtectionTokenCheck`

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
