---
title: AD FS Kennwort Angriffsschutz
description: In diesem Dokument wird beschrieben, wie AD FS-Benutzer vor Angriffen durch das Kennwort zu schützen
author: billmath
manager: mtillman
ms.reviewer: andandyMSFT
ms.date: 11/15/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: de1af9712b54c977c591953c68eec506c80d3cdd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822001"
---
# <a name="ad-fs-password-attack-protection"></a>AD FS Kennwort Angriffsschutz

## <a name="what-is-a-password-attack"></a>Was ist ein Kennwortangriff?

Eine Voraussetzung für das einmaliges Anmelden im Verbund ist die Verfügbarkeit von Endpunkten zur Authentifizierung über das Internet. Die Verfügbarkeit von authentifizierungsendpunkte im Internet kann Benutzer die Anwendungen zugreifen, selbst wenn diese nicht in einem Unternehmensnetzwerk befinden. 

Dies bedeutet jedoch auch, dass einige risikoteilnehmer können die verbundendpunkte verfügbar über das Internet nutzen und diese Endpunkte verwenden, versuchen Sie es aus, und bestimmen Kennwörter oder DOS-Angriffe zu erstellen. Ein solcher Angriff, die immer öfter wenden heißt eine **Kennwortangriff**. 

Es gibt 2 Typen von häufigen Kennwortangriffen. Kennwort Sprühende Angriffen und Brute-force-Kennwortangriffs. 

### <a name="password-spray-attack"></a>Sprühende Kennwortangriff
Bei einem Angriff Kennwort Sprühende versucht diese risikoteilnehmer die am häufigsten verwendeten Kennwörter über viele verschiedene Konten und Dienste für den Zugriff auf alle Ressourcen ein Kennwort geschützt, die sie finden können. In der Regel umfassen diese viele Organisationen und Identitätsanbieter. Beispielsweise verwendet ein Angreifer eine gängiger Toolkit zum Auflisten aller Benutzer in mehreren Organisationen aus, und wiederholen dann "P@$$w0rd" und "Password1" für all diese Konten. Um Ihnen die Idee erteilen, kann ein Angriff aussehen:

|Zielbenutzer|Zielkennwort|
|-----|-----|-----|
|User1@org1.com|Password1|
|User2@org1.com|Password1|
|User1@org2.com|Password1|
|User2@org2.com|Password1|
|…|…|
|User1@org1.com|P@$$w0rd|
|User2@org1.com|P@$$w0rd|
|User1@org2.com|P@$$w0rd|
|User2@org2.com|P@$$w0rd|

Dieser Angriff QuarantŠneprozesse Erkennungstechniken für die meisten umgangen, da von der Aussichtspunkt der ein einzelner Benutzer oder Unternehmen, der Angriff nur einen isolierten Anmeldefehler aussieht.

Angreifer verwenden, ist es ein Spiel Zahlen: sie wissen, dass es einige Kennwörter ein, die häufig verwendeten vorhanden sind.  Der Angreifer erhält einige Erfolge für alle tausend Konten, die angegriffen, und dies genügt, um effektiv zu sein. Sie verwenden die Konten, zum Abrufen von Daten aus e-Mails, Sammeln von Kontaktinformationen, und Senden von Phishing-Links oder nur Kennwort Sprühende Zielgruppe zu erweitern. Die Angreifer nicht weniger wichtig, die die ursprünglichen Ziele werden, sondern nur, dass sie mit einigem Erfolg haben, die sie nutzen können.

Sie verwenden die Konten, zum Abrufen von Daten aus e-Mails, Sammeln von Kontaktinformationen, und Senden von Phishing-Links oder nur Kennwort Sprühende Zielgruppe zu erweitern. Die Angreifer nicht weniger wichtig, die die ursprünglichen Ziele werden, sondern nur, dass sie mit einigem Erfolg haben, die sie nutzen können.

Aber mit wenigen Schritten konfigurieren die AD FS und ordnungsgemäß AD FS-Endpunkte für diese Art von Angriffen geschützt werden können. Dieser Artikel behandelt die 3 Bereiche, die für den Schutz vor diesen Angriffen ordnungsgemäß konfiguriert werden müssen.

### <a name="brute-force-password-attack"></a>Kennwort Brute-Force-Angriff 
Bei dieser Form von Angriff versucht ein Angreifer mehrere Kennwortversuche für eine bestimmte Reihe von Konten. In vielen Fällen werden diese Konten für Benutzer vorgesehen, die innerhalb der Organisation eine höhere Zugriffsebene verfügen. Diese können Führungskräfte innerhalb der Organisation oder Administratoren sein, die kritischen Infrastrukturen zu verwalten.  

Diese Art von Angriff könnte auch DOS-Muster führen. Dies könnte auf Dienstebene, in dem AD FS eine große Anzahl von Anforderungen aufgrund von unzureichenden Anzahl von Servern verarbeiten kann, oder möglicherweise auf einer Benutzerebene, in denen ein Benutzer aus ihrem Konto gesperrt wird.  

## <a name="securing-ad-fs-against-password-attacks"></a>Sichern von AD FS gegen Angriffe auf Kennwörter 
 
Aber mit wenigen Schritten konfigurieren die AD FS und ordnungsgemäß AD FS-Endpunkte für diese Arten von Angriffen geschützt werden können. Dieser Artikel behandelt die 3 Bereiche, die für den Schutz vor diesen Angriffen ordnungsgemäß konfiguriert werden müssen. 


- Ebene 1, Baseline: Dies sind die grundlegenden Einstellungen, die auf eine AD FS-Server, um sicherzustellen, dass Angreifer brute-Force-Angriff Verbund-Benutzer kann nicht konfiguriert werden müssen. 
- Ebene 2, das extranet schützen: Hierbei handelt es sich um die Einstellungen, die konfiguriert werden müssen, um sicherzustellen, dass die extranet-Zugriff konfiguriert ist, um sichere Protokolle, Authentifizierungsrichtlinien und entsprechende Anwendungen zu verwenden. 
- Ebene 3, verschieben, ohne Kennwort für den Extranetzugriff: Diese sind erweiterte Einstellungen und Richtlinien zum Aktivieren des Zugriffs auf verbundene Ressourcen mit sicherer Anmeldeinformationen statt Kennwörter, die anfällig für Angriffe sind. 

## <a name="level-1-baseline"></a>Ebene 1: Baseline

1. Wenn AD FS 2016 implementieren [extranet der smart Lockout](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md) Extranet der smart Lockout verfolgt der vertrauten Standorte und kann einen gültige Benutzer über kommen, wenn sie erfolgreich zuvor von diesem Speicherort angemeldet haben. Verwenden smart extranetsperre, können Sie sicherstellen, dass Angreifer nicht brute-Force kann greifen die Benutzer an und zur gleichen Zeit berechtigten Benutzer produktiv arbeiten können.
    - Wenn Sie nicht in AD FS 2016 sind, wird dringend empfohlen [upgrade](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) mit AD FS 2016. Es ist eine einfache Aktualisierung von AD FS 2012 R2. Wenn Sie AD FS 2012 R2 verwenden, implementieren Sie [extranetsperre](../../ad-fs/operations/Configure-AD-FS-Extranet-Soft-Lockout-Protection.md). Ein Nachteil dieses Ansatzes ist, dass gültige Benutzer bei extranet-Zugriff blockiert werden können, wenn Sie in einem brute-Force-Muster sind. AD FS unter Server 2016 muss dieser Nachteil nicht.

2. Monitor & blockieren verdächtiger IP-Adressen 
    - Wenn Sie Azure AD Premium verfügen, implementieren Sie Connect Health für AD FS und der [riskante IP-Adresse Bericht](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health-adfs#risky-ip-report-public-preview) Benachrichtigungen, die er bereitstellt.
        
        a. Lizenzierung ist nicht für alle Benutzer und erfordert 25 Lizenzen/AD FS/WAP-Server, der möglicherweise für einen Kunden einfach.
    
        b. Sie können jetzt IP-Adressen untersuchen, die große Anzahl von fehlgeschlagenen Anmeldungen generieren
    
        c. Dies müssen Sie zum Aktivieren der Überwachung für Ihre AD FS-Server.

3.  Hiermit blockieren Sie verdächtige IP-Adressen.  Dadurch wird möglicherweise DOS-Angriffe verhindert.

    a. Wenn es sich um 2016 verwenden die [ *Extranet gesperrt IP-Adressen* ](../../ad-fs/operations/configure-ad-fs-banned-ip.md) featureflags, alle Anforderungen aus der IP-Adressen blockieren von #3 (oder manuellen Analyse).

    b. Wenn Sie AD FS 2012 R2 und früher verwenden, blockieren Sie die IP-Adresse direkt auf Exchange Online und optional in Ihrer Firewall.

4. Wenn Sie Azure AD Premium verfügen, verwenden Sie [Schutz von Kennwörtern in Azure AD](https://docs.microsoft.com/azure/active-directory/authentication/concept-password-ban-bad-on-premises) um zu verhindern, dass zu erraten von Kennwörtern in Azure AD abrufen  

    a. Beachten Sie, dass Ihre zu erraten von Kennwörtern können sie mit nur 1 bis 3 geknackt werden kann. Diese Funktion verhindert, dass diese vom vorbereiten. 

    b. Unsere Vorschau-Statistik abrufen fast 20 – 50 % der neuen Kennwörter blockiert festgelegt wird. Dies bedeutet, dass % der Benutzer leicht erraten werden Kennwörter anfällig sind.

## <a name="level-2-protect-your-extranet"></a>Ebene 2: Schützen Sie Ihre extranet

5. Verschieben Sie auf die moderne Authentifizierung für alle Clients, die aus dem extranet auf. E-Mail-Clients sind ein wichtiger Aspekt. 

    a. Sie müssen auf Outlook Mobile für mobile Geräte zu verwenden. Die neue native Mail-app für iOS unterstützt auch die modernen Authentifizierung. 

    b. Sie benötigen, Outlook 2013 (mit der neuesten CU-Patches) oder Outlook 2016 zu verwenden.

6.  Aktivieren der MFA für alle extranet-Zugriff. Dadurch erhalten Sie den Schutz für alle extranet-Zugriff hinzugefügt.

    a.  Wenn Sie Azure AD Premium verfügen, verwenden Sie [bedingtem Azure AD-Richtlinien](https://docs.microsoft.com/azure/active-directory/conditional-access/overview) steuern.  Dies ist besser als die Implementierung von der Regeln in AD FS.  Dies ist da moderne Clientanwendungen für häufigere erzwungen werden.  In diesem Fall auf Azure AD bei der Anforderung eines neues Zugriffstokens (in der Regel einmal pro Stunde) mithilfe eines aktualisierungstokens abzurufen.  

    b.  Wenn Sie keine Azure AD Premium oder zusätzliche apps in AD FS, mit denen Sie Internet Access basierend, implementieren Sie MFA (möglicherweise Azure MFA und AD FS 2016) und führen Sie eine [globale MFA-Richtlinie](../../ad-fs/operations/configure-authentication-policies.md#to-configure-multi-factor-authentication-globally) für alle extranet-Zugriff.
 
## <a name="level-3-move-to-password-less-for-extranet-access"></a>Ebene 3: Wechsel zu Kennwort weniger für extranet-Zugriff

7. Verschieben Sie in Windows 10, und verwenden [Hello For Business](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification).

8. Für andere Geräte, wenn es sich um AD FS 2016 können Sie [Azure MFA-OTP](../../ad-fs/operations/configure-ad-fs-and-azure-mfa.md) als der erste Faktor und das Kennwort als die 2. Stufe. 

9.  Für mobile Geräte, wenn Sie nur die MDM-verwalteten Geräten zulassen können [Zertifikate](../../ad-fs/operations/configure-user-certificate-authentication.md) , die der Benutzer nicht anmelden. 
 
## <a name="urgent-handling"></a>Dringende Behandlung

Wenn die AD FS-Umgebung angegriffen aktiv ist, sollte die folgenden Schritte aus wie möglich implementiert werden:

 - Deaktivieren Sie U/P-Endpunkt in AD FS und müssen Sie sich alle Benutzer-VPN-Zugriff oder in Ihrem Netzwerk sein. Dazu müssen Sie Schritt **auf Ebene 2 #1a** abgeschlossen. Andernfalls werden alle internen Outlook-Anforderungen immer noch über die Cloud über EXO-Proxy-Authentifizierung weitergeleitet werden
 - Wenn der Angriff nur über EXO stammen, können Sie deaktivieren, Standardauthentifizierung für Exchange-Protokolle (POP, IMAP, SMTP, Exchange-Webdienste usw.) verwenden die Authentifizierungsrichtlinien, diese Protokolle und die Authentifizierungsmethoden verwendet werden, die große Mehrheit dieser Art von Angriffen. Darüber hinaus werden die Client-Zugriffsregeln in EXO- und pro Postfach-Protokoll-Aktivierung sind ausgewertete nach der Authentifizierung und wird nicht daran, die Angriffe helfen. 
 - Bieten Sie selektiv extranet-Zugriff mithilfe von Ebene-3 #1 bis 3.

## <a name="next-steps"></a>Nächste Schritte

- [Ein Upgrade auf AD FS-Server 2016](../../ad-fs/deployment/upgrading-to-ad-fs-in-windows-server.md) 
- [Intelligente extranetsperre in AD FS 2016](../../ad-fs/operations/Configure-AD-FS-Extranet-Smart-Lockout-Protection.md)
- [Konfigurieren von Richtlinien für bedingten Zugriff](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)
- [Kennwortschutz für Azure AD](https://docs.microsoft.com/azure/active-directory/authentication/howto-password-ban-bad-on-premises)
