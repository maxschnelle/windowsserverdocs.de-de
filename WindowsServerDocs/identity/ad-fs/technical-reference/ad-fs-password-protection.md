---
title: Schutz von AD FS Kenn Wort Angriffen
description: In diesem Dokument wird beschrieben, wie AD FS Benutzer vor Kenn Wort Angriffen geschützt werden.
author: billmath
manager: mtillman
ms.reviewer: andandyMSFT
ms.date: 11/15/2018
ms.topic: article
ms.author: billmath
ms.openlocfilehash: c17ef0524ed873c8a3d506df75542848e2c4bca7
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956157"
---
# <a name="ad-fs-password-attack-protection"></a>Schutz von AD FS Kenn Wort Angriffen

## <a name="what-is-a-password-attack"></a>Was ist ein Kenn Wort Angriff?

Eine Voraussetzung für Verbund Single Sign-on ist die Verfügbarkeit von Endpunkten zur Authentifizierung über das Internet. Die Verfügbarkeit von Authentifizierungs Endpunkten im Internet ermöglicht Benutzern den Zugriff auf die Anwendungen, auch wenn Sie sich nicht in einem Unternehmensnetzwerk befinden.

Dies bedeutet jedoch auch, dass einige schlechte Akteure die im Internet verfügbaren Verbund Endpunkte nutzen und diese Endpunkte verwenden können, um Kenn Wörter zu ermitteln und zu ermitteln oder Denial-of-Service-Angriffe zu erzeugen. Ein solcher Angriff, der häufiger wird, wird als Kenn **Wort Angriff**bezeichnet.

Es gibt zwei Arten von häufigen Kenn Wort Angriffen. Kenn Wort Sprüh Angriff & Brute-Force-Kenn Wort Angriff.

### <a name="password-spray-attack"></a>Kenn Wort Sprüh Angriff
Bei einem Kenn Wort Sprüh Angriff versuchen diese böswilligen Akteure, die gängigsten Kenn Wörter für viele verschiedene Konten und Dienste zu verwenden, um Zugriff auf die Kenn Wort geschützten Ressourcen zu erhalten, die Sie finden. Diese umfassen in der Regel viele verschiedene Organisationen und Identitäts Anbieter. Ein Angreifer verwendet beispielsweise ein häufig verfügbares Toolkit, um alle Benutzer in mehreren Organisationen aufzulisten, und versucht dann, "P@ $ $w 0rd" und "Password1" für alle diese Konten zu verwenden. Ein Angriff könnte beispielsweise wie folgt aussehen:


|  Ziel Benutzer   | Ziel Kennwort |
|----------------|-----------------|
| User1@org1.com |    Password1    |
| User2@org1.com |    Password1    |
| User1@org2.com |    Password1    |
| User2@org2.com |    Password1    |
|       …        |        …        |
| User1@org1.com |    P@$$w0rd     |
| User2@org1.com |    P@$$w0rd     |
| User1@org2.com |    P@$$w0rd     |
| User2@org2.com |    P@$$w0rd     |

Dieses Angriffsmuster geht vor den meisten Erkennungs Techniken, da der Angriff vom Standpunkt eines einzelnen Benutzers oder Unternehmens aus wie eine isolierte fehlgeschlagene Anmeldung aussieht.

Bei Angreifern ist es ein Zahlen Spiel: Sie wissen, dass es einige Kenn Wörter gibt, die sehr häufig vorkommen.  Der Angreifer erhält einen Erfolg für alle tausend Konten, die angegriffen werden, und das ist ausreichend, um effektiv zu sein. Sie verwenden die Konten zum erhalten von Daten aus e-Mails, zum Sammeln von Kontaktinformationen und zum Senden von phishinglinks oder zum Erweitern der Zielgruppe für Kenn Wort Sprays. Die Angreifer kümmern sich nicht darum, wer die ursprünglichen Ziele sind – nur, dass Sie einen Erfolg haben, den Sie nutzen können.

Indem Sie jedoch einige Schritte ausführen, um die AD FS und das Netzwerk ordnungsgemäß zu konfigurieren, können AD FS Endpunkte gegen diese Art von Angriffen geschützt werden. Dieser Artikel befasst sich mit drei Bereichen, die ordnungsgemäß konfiguriert werden müssen, um diese Angriffe zu schützen.

### <a name="brute-force-password-attack"></a>Brute-Force-Kenn Wort Angriff
Bei dieser Art von Angriff versucht ein Angreifer mehrere Kenn Wort Versuche für einen Zielsatz von Konten. In vielen Fällen werden diese Konten für Benutzer bestimmt, die über eine höhere Zugriffsebene innerhalb der Organisation verfügen. Dabei kann es sich um Führungskräfte innerhalb der Organisation oder Administratoren handeln, die die kritische Infrastruktur verwalten.

Diese Art von Angriff kann auch zu DOS-Mustern führen. Dies kann auf dem Service Level erfolgen, auf dem AD FS eine große Anzahl von Anforderungen aufgrund unzureichender Anzahl von Servern nicht verarbeiten kann oder sich auf einer Benutzerebene befinden kann, bei der ein Benutzer von seinem Konto gesperrt ist.

## <a name="securing-ad-fs-against-password-attacks"></a>Sichern von AD FS vor Kenn Wort Angriffen

Indem Sie jedoch einige Schritte ausführen, um die AD FS und das Netzwerk ordnungsgemäß zu konfigurieren, können AD FS Endpunkte gegen diese Art von Angriffen geschützt werden. Dieser Artikel befasst sich mit drei Bereichen, die ordnungsgemäß konfiguriert werden müssen, um diese Angriffe zu schützen.


- Ebene 1, Baseline: Hierbei handelt es sich um die grundlegenden Einstellungen, die auf einem AD FS-Server konfiguriert werden müssen, um sicherzustellen, dass böswillige Benutzer keine Brute-Force-Angriff für Angriffe
- Ebene 2: Schützen des Extranet: Dies sind die Einstellungen, die konfiguriert werden müssen, um sicherzustellen, dass der Extranetzugriff konfiguriert ist, um sichere Protokolle, Authentifizierungs Richtlinien und geeignete Anwendungen zu verwenden.
- Ebene 3: in Kennwort für den Extranetzugriff verschieben: Dies sind erweiterte Einstellungen und Richtlinien, um den Zugriff auf Verbund Ressourcen mit sichereren Anmelde Informationen anstelle von Kenn Wörtern zu ermöglichen, die anfällig für Angriffe sind.

## <a name="level-1-baseline"></a>Ebene 1: Baseline

1. Wenn ADFS 2016 [, implementieren Sie die Smart Sperrungs](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md) -Extranet-Extranet-Smart Sperrungs, die vertraute Standorte nachverfolgt, und ermöglicht es einem gültigen Benutzer, zu kommen, wenn er sich zuvor erfolgreich von diesem Speicherort angemeldet hat. Durch die Verwendung von Extranet Smart Lockout können Sie sicherstellen, dass böswillige Akteure nicht in der Lage sind, Brute-Force-Angriffe der Benutzer durchzusetzen, und gleichzeitig den legitimen Benutzer produktiv machen können.
    - Wenn Sie nicht AD FS 2016, wird dringend empfohlen, ein [Upgrade](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) auf AD FS 2016 durchzuführen. Es handelt sich um einen einfachen Upgradepfad von AD FS 2012 R2. Wenn Sie AD FS 2012 R2 haben, implementieren Sie [extranetsperre](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md). Ein Nachteil dieses Ansatzes ist, dass gültige Benutzer möglicherweise für den Extranetzugriff blockiert werden, wenn Sie ein Brute-Force-Muster haben. AD FS auf Server 2016 hat diesen Nachteil nicht.

2. Überwachung & blockieren verdächtiger IP-Adressen
    - Wenn Sie Azure AD Premium haben, implementieren Sie Connect Health für AD FS, und verwenden Sie die von ihr bereitgestellten [riskanten IP-Berichts](/azure/active-directory/connect-health/active-directory-aadconnect-health-adfs#risky-ip-report-public-preview) Benachrichtigungen.

        a. Die Lizenzierung ist nicht für alle Benutzer vorgesehen und erfordert 25 Lizenzen/AD FS/WAP-Server, die für einen Kunden leicht leicht sind.

        b. Nun können Sie IP-Adressen untersuchen, die eine große Anzahl fehlerhafter Anmeldungen erzeugen.

        c. Dies erfordert, dass Sie die Überwachung auf Ihren AD FS-Servern aktivieren.

3.  Blockieren verdächtiger IP-Adressen.  Dies blockiert potenziell DOS-Angriffe.

    a. Wenn auf 2016, verwenden Sie das Feature für das [*extranetverbot*](../../ad-fs/operations/configure-ad-fs-banned-ip.md) für gesperrte IP-Adressen, um alle Anforderungen von IP-Adressen zu blockieren, die durch #3 gekennzeichnet sind (oder manuell

    b. Wenn Sie sich AD FS 2012 R2 oder niedriger befinden, blockieren Sie die IP-Adresse direkt in Exchange Online und optional in Ihrer Firewall.

4. Wenn Sie über Azure AD Premium verfügen, verwenden Sie [Azure AD Kenn Wort Schutz](/azure/active-directory/authentication/concept-password-ban-bad-on-premises) , um zu verhindern, dass zu berücksichtigende Kenn Wörter in Azure AD

    a. Beachten Sie, dass Sie, wenn Sie über schämier Bare Kenn Wörter verfügen, diese mit nur 1-3 versuchen erreichen können. Diese Funktion verhindert, dass diese festgelegt werden.

    b. Aus unseren Vorschau Statistiken werden fast 20-50% der neuen Kenn Wörter blockiert. Dies impliziert, dass% der Benutzer anfällig für leicht erraten Kenn Wörter sind.

## <a name="level-2-protect-your-extranet"></a>Ebene 2: Schützen Ihres Extranet

5. Wechseln Sie zur modernen Authentifizierung für alle Clients, die auf das Extranet zugreifen. E-Mail-Clients sind eine große Rolle.

    a. Sie müssen Outlook Mobile für mobile Geräte verwenden. Die neue IOS Native Mail-App unterstützt auch die moderne Authentifizierung.

    b. Sie müssen Outlook 2013 (mit den neuesten Cu-Patches) oder Outlook 2016 verwenden.

6. Aktivieren Sie MFA für den gesamten Extranetzugriff. Dadurch erhalten Sie zusätzlichen Schutz für alle extranetzugriffe.

   a.  Wenn Sie über Azure AD Premium verfügen, verwenden Sie [Azure AD Richtlinien für bedingten Zugriff](/azure/active-directory/conditional-access/overview) , um dies zu steuern.  Dies ist besser als das Implementieren der Regeln in AD FS.  Der Grund hierfür ist, dass moderne Client-apps häufiger erzwungen werden.  Dies geschieht bei Azure AD, wenn ein neues Zugriffs Token (in der Regel stündlich) mit einem Aktualisierungs Token angefordert wird.

   b.  Wenn Sie nicht über Azure AD Premium verfügen oder über zusätzliche apps auf AD FS verfügen, für die Sie internetbasierten Zugriff zulassen, implementieren Sie MFA (kann auch Azure MFA sein AD FS 2016), und führen Sie eine [globale MFA-Richtlinie](../../ad-fs/operations/configure-authentication-policies.md#to-configure-multi-factor-authentication-globally) für den gesamten Extranetzugriff durch.

## <a name="level-3-move-to-password-less-for-extranet-access"></a>Ebene 3: für den Extranetzugriff auf das Kennwort weniger verschieben

7. Wechseln Sie zu Windows 10, und verwenden Sie [Hello for Business](/windows/security/identity-protection/hello-for-business/hello-identity-verification).

8. Bei anderen Geräten können Sie, wenn Sie auf AD FS 2016, [Azure MFA OTP](../../ad-fs/operations/configure-ad-fs-and-azure-mfa.md) als ersten Faktor und Kennwort als 2. Faktor verwenden.

9. Wenn Sie für mobile Geräte nur MDM-verwaltete Geräte zulassen, können Sie den Benutzer mit [Zertifikaten](../../ad-fs/operations/configure-user-certificate-authentication.md) anmelden.

## <a name="urgent-handling"></a>Dringende Behandlung

Wenn die AD FS Umgebung aktiv ist, sollten Sie die folgenden Schritte ausführen:

 - Deaktivieren Sie den U/P-Endpunkt in AD FS, und fordern Sie alle Benutzer zu VPN, um Zugriff zu erhalten Dies erfordert, dass Schritt **Ebene 2 #1a** abgeschlossen ist. Andernfalls werden alle internen Outlook-Anforderungen weiterhin über die Cloud über die Exo-Proxy Authentifizierung weitergeleitet.
 - Wenn der Angriff nur über "Exo" erfolgt, können Sie die Standard Authentifizierung für Exchange-Protokolle (Pop, IMAP, SMTP, EWS usw.) mithilfe von Authentifizierungs Richtlinien deaktivieren. diese Protokolle und Authentifizierungsmethoden werden bei den meisten dieser Angriffe verwendet. Außerdem werden die Client Zugriffsregeln in der "Exo"-und Post Fach Protokoll-Aktivierung nach der Authentifizierung ausgewertet und helfen nicht bei der Vermeidung von Angriffen.
 - Stellen Sie selektiv Extranetzugriff mithilfe von Ebene 3 #1-3 bereit.

## <a name="next-steps"></a>Nächste Schritte

- [Upgrade auf AD FS Server 2016](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md)
- [Extranet Smart Sperrungs in AD FS 2016](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [Konfigurieren von Richtlinien für bedingten Zugriff](/azure/active-directory/conditional-access/overview)
- [Azure AD Kenn Wort Schutz](/azure/active-directory/authentication/howto-password-ban-bad-on-premises)
