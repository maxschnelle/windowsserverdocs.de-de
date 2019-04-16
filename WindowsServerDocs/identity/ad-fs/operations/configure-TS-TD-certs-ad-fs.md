---
title: "Abrufen und Konfigurieren von Tokensignatur- und Tokenentschlüsselungszertifikate für AD FS"
description: "In diesem Dokument wird beschrieben, wie zum Abrufen und konfigurieren Sie die Terminaldienste- und TD Zertifikate für AD FS"
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 0d7f8ba4efb74a377f9f9d748949a934398ebefc
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>Abrufen und Konfigurieren von Terminaldienste- und TD Zertifikate für AD FS

Dieses Thema beschreibt die Aufgaben und Verfahren, die Sie ausführen können, um sicherzustellen, dass Ihre AD FS Tokensignatur- und tokenentschlüsselungszertifikate auf dem neuesten Stand sind.

Token-Signaturzertifikate Standard X509 sind Zertifikate, die verwendet werden, um sichere aller Token zu signieren, die vom Verbundserver ausgestellt. Tokenverschlüsselungszertifikate Standard X509 sind Zertifikate, die Entschlüsselung aller eingehenden Token verwendet werden. Sie sind auch in den Verbundmetadaten veröffentlicht.

Weitere Informationen finden Sie unter [Zertifikatanforderungen](../design/ad-fs-requirements.md#BKMK_1)

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>Bestimmen Sie, ob die Zertifikate von AD FS automatisch erneuert
Standardmäßig wird AD FS so konfiguriert, dass sowohl zum Zeitpunkt der Erstkonfiguration als auch bei der Zertifikate, deren Ablaufdatum nähern Tokensignatur- und tokenentschlüsselungszertifikate automatisch generiert wird.

Sie können die folgenden Windows PowerShell-Befehl ausführen:`Get-AdfsProperties`.
  
  ![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
Die Eigenschaft AutoCertificateRollover beschreibt, ob AD FS konfiguriert ist, um Tokensignatur- und Token entschlüsseln Zertifikate automatisch zu erneuern.

Wenn AutoCertificateRollover auf "true" festgelegt ist, wird die AD FS-Zertifikate erneuert und in AD FS automatisch konfiguriert. Nachdem das neue Zertifikat konfiguriert ist, müssen um zu einen Ausfall vermeiden Sie sicherstellen, dass jedes Verbundpartner (dargestellt in der AD FS-Farm von Vertrauensstellungen der vertrauenden Seite oder Anspruchsanbieter-Vertrauensstellungen) mit dieses neuen Zertifikats aktualisiert wird.
    
Wenn AD FS nicht konfiguriert wurde, erneuern Tokensignatur- und Token entschlüsseln Zertifikate automatisch (sofern AutoCertificateRollover auf "false" festgelegt ist), AD FS wird nicht automatisch generieren oder starten Sie mit neuen Tokensignatur- oder Token Entschlüsseln von Zertifikaten. Sie müssen diese Aufgaben manuell ausführen.
    
Wenn AD FS konfiguriert ist, dass Tokensignatur- und Token entschlüsseln Zertifikate automatisch verlängern (AutoCertificateRollover ist auf "true" festgelegt), können Sie ermitteln, wann erneuert werden:

CertificateGenerationThreshold wird beschrieben, wie viele Tage im Voraus über das Zertifikat nicht nach Datum ein neues Zertifikat generiert wird.

CertificatePromotionThreshold bestimmt, wie viele Tage nach dem das neue Zertifikat generiert wird, dass es zum primären Zertifikat werden heraufgestuft werden soll (in anderen Worten: AD FS wird gestartet, verwenden sie zum Signieren von Token ausgestellt und Entschlüsselung von Token vom Identitätsanbieter).

![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
Wenn AD FS konfiguriert ist, dass Tokensignatur- und Token entschlüsseln Zertifikate automatisch verlängern (AutoCertificateRollover ist auf "true" festgelegt), können Sie ermitteln, wann erneuert werden:

 - **CertificateGenerationThreshold** wird beschrieben, wie viele Tage im Voraus über das Zertifikat nicht nach Datum ein neues Zertifikat generiert wird.
 - **CertificatePromotionThreshold** bestimmt, wie viele Tage nach dem das neue Zertifikat generiert wird, dass es zum primären Zertifikat werden heraufgestuft werden soll (in anderen Worten: AD FS wird gestartet, verwenden sie zum Signieren von Token ausgestellt und Entschlüsselung von Token Identität Anbieter).

## <a name="determine-when-the-current-certificates-expire"></a>Bestimmen Sie, wann die aktuellen Zertifikate ablaufen
Sie können das folgende Verfahren verwenden, um den primären Tokensignatur- und das Token Entschlüsseln von Zertifikaten zu identifizieren und um zu bestimmen, wann die aktuellen Zertifikate ablaufen.

Sie können die folgenden Windows PowerShell-Befehl ausführen: `Get-AdfsCertificate –CertificateType token-signing` (oder `Get-AdfsCertificate –CertificateType token-decrypting `). Oder Sie können die aktuellen Zertifikate in der MMC untersuchen: Service -> Zertifikate.

![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

Das Zertifikat für die der **IsPrimary** Wert **True** ist das Zertifikat, das derzeit AD FS verwendet wird.

Das Datum angezeigt, für die **nicht nach** ist das Datum nach dem ein neues primäres Tokens signieren oder Entschlüsseln von Zertifikat konfiguriert werden muss.

Um die Dienstkontinuität sicherzustellen, müssen alle Verbundpartner (dargestellt in der AD FS-Farm von Vertrauensstellungen der vertrauenden Seite oder Anspruchsanbieter-Vertrauensstellungen) die neue Tokensignatur- und tokenentschlüsselungszertifikate vor diesem Ablauf nutzen. Wir empfehlen, beginnen Sie mit der Planung für diesen Prozess mindestens 60Tage im Voraus.

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>Generieren ein neues selbstsigniertes Zertifikat manuell vor Ablauf der Toleranzperiode
Die folgenden Schrittekönnen Sie um ein neues selbstsigniertes Zertifikat manuell vor Ablauf der Toleranzperiode generieren.

1. Stellen Sie sicher, dass Sie für den primären AD FS-Server angemeldet sind.
2. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: `Add-PSSnapin "microsoft.adfs.powershell"`
3. Optional können Sie die aktuellen Signaturzertifikate in AD FS überprüfen. Führen Sie dazu den folgenden Befehl:`Get-ADFSCertificate –CertificateType token-signing`. Sehen Sie sich die Ausgabe des Befehls nicht nach dem Datum der alle aufgelisteten Zertifikate angezeigt.
4. Um ein neues Zertifikat zu generieren, führen Sie den folgenden Befehl zum Erneuern und aktualisieren die Zertifikate auf dem AD FS-Server:`Update-ADFSCertificate –CertificateType token-signing`.
5. Überprüfen Sie die Aktualisierung durch erneutes Ausführen des folgenden Befehls aus: `Get-ADFSCertificate –CertificateType token-signing`
6. Zwei Zertifikate sollte jetzt angezeigt werden, von denen verfügt über eine **nicht nach** Datum, etwa ein Jahr in der Zukunft und für die die **IsPrimary** Wert ist **False**.

>[!IMPORTANT]
>Um eine dienstunterbrechung zu vermeiden, aktualisieren Sie die Zertifikatinformationen in Azure AD durch Ausführen der Schrittein der Update Azure AD mit einem gültigen Zertifikat signieren von Token.

## <a name="if-youre-not-using-self-signed-certificates"></a>Wenn Sie keine selbstsignierten Zertifikate verwenden...
Wenn Sie nicht mithilfe des automatisch generierte, selbstsignierte Tokensignatur- und tokenentschlüsselungszertifikate sind, müssen Sie erneuern und diese Zertifikate manuell konfigurieren.

Sie müssen zunächst ein neues Zertifikat von der Zertifizierungsstelle zu erhalten und in den lokalen Computer persönlichen Zertifikatspeicher auf jedem Verbundserver importieren. Anweisungen finden Sie in der [Importieren eines Zertifikats](https://technet.microsoft.com/library/cc754489.aspx) Artikel.

Dann müssen Sie das Zertifikat als das sekundäre AD FS Tokensignaturzertifikat oder Entschlüsselungszertifikat konfigurieren. (Sie konfigurieren sie als sekundäre Zertifikat zu Ihrem Verbundpartner genügend Zeit für das neue Zertifikat zu verwenden, bevor Sie es zum primären Zertifikat heraufstufen).

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>So konfigurieren Sie ein neues Zertifikat als sekundäre Zertifikat
1. Öffnen Sie PowerShell, und führen Sie Folgendes: `Set-ADFSProperties -AutoCertificateRollover $false`
2. Sie haben nach dem das Zertifikat importieren. Öffnen der **AD FS-Verwaltungs** Konsole.
3. Erweitern Sie **Service** und wählen Sie dann **Zertifikate**.
4. Klicken Sie im Aktionsbereich auf **hinzufügen Token-Signing Certificate**.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. Wählen Sie das neue Zertifikat aus der Liste der angezeigten Zertifikate, und klicken Sie dann auf OK.
6.  Öffnen Sie PowerShell, und führen Sie Folgendes: `Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>Stellen Sie sicher, dass das neue Zertifikat einen privaten Schlüssel zugeordnet sind, dass der AD FS-Dienstkonto erhält Berechtigungen zum Lesen Sie und den privaten Schlüssel. Überprüfen Sie dies auf jedem Verbundserver. Dazu, das Zertifikate-Snap-In mit der rechten Maustaste in des neuen Zertifikats, klicken Sie auf alle Tasks, und klicken Sie dann auf Privatschlüssel verwalten.

Nachdem Sie ausreichend Zeit für die Verbundserverproxy-Partner, nutzen Sie das neue Zertifikat (Ziehen Sie die Verbundmetadaten oder senden sie den öffentlichen Schlüssel des neuen Zertifikats) erlaubt haben, müssen Sie das sekundäre Zertifikat zum primären Zertifikat bewerben.

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>Das neue Zertifikat vom sekundären zum primären heraufstufen

1. Öffnen der **AD FS-Verwaltungs** Konsole.
2. Erweitern Sie **Service** und wählen Sie dann **Zertifikate**.
3. Klicken Sie auf der sekundären Tokensignaturzertifikat.
4. In der **Aktionen** Bereich, klicken Sie auf **Hauptadresse**. Klicken Sie auf "Ja", zur Bestätigung aufgefordert.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>Aktualisieren von Verbundpartner

### <a name="partners-who-can-consume-federation-metadata"></a>Partner, die Verbundmetadaten genutzt werden können
Wenn Sie verlängert haben, und konfigurieren Sie einen neuen Tokensignatur- oder tokenentschlüsselungszertifikat, Sie müssen sicherstellen, dass die alle Ihre Verbundpartner (Unternehmen oder Konto Organisation Ressourcenpartner, die von der vertrauenden Seite in Ihrer AD FS vorliegen eines Drittanbieters Vertrauensstellungen und Anspruchsanbieter-Vertrauensstellungen) haben Sie die neue Zertifikate ausgewählt haben.

### <a name="partners-who-can-not-consume-federation-metadata"></a>Partner, die Verbundmetadaten verwenden kann
Wenn Ihre Verbundpartner die Verbundmetadaten verwenden können, müssen Sie manuell sie den öffentlichen Schlüssel des neuen Zertifikats Tokensignaturzertifikate/tokenentschlüsselungs-senden. Senden Sie Ihre öffentliche Schlüssel des neuen Zertifikats (.cer Datei oder wenn Sie die gesamte Kette aufnehmen möchten. p7b) aller Ihrer Organisation oder ein Konto Organisation Ressourcenpartner (dargestellt in Ihrer AD FS von Vertrauensstellungen der vertrauenden Seite Party vertraut, und Ansprüche Anbieter Vertrauensstellungen). Haben Sie die Partnern Änderungen auf ihrer Seite neue Zertifikate vertrauen zu implementieren.

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>Bewerben Sie zur primären (wenn AutoCertificateRollover "false" festgelegt ist)
Wenn **AutoCertificateRollover** läuft **False**, AD FS wird nicht automatisch generieren oder Start mit der neuen Token signieren oder Token entschlüsseln Zertifikate. Sie müssen diese Aufgaben manuell ausführen.
Bewerben Sie nach dem möglich, dass eine ausreichende Zeitspanne allen Ihren Partnern Verbund nutzen Sie das neue sekundäre Zertifikat, das sekundäre Zertifikat zum primären (im MMC-Snap-In, klicken Sie auf der sekundären Tokensignatur-Zertifikat, und klicken Sie im Aktionsbereich auf **Als primär festlegen**.)

## <a name="updating-azure-ad"></a>Aktualisieren von Azure AD
AD FS bietet einzelne anmelden den Zugriff auf Microsoft-Clouddienste wie Office365 durch Benutzer über ihre vorhandenen AD DS-Anmeldeinformationen zu authentifizieren.  Weitere Informationen zur Verwendung von Zertifikaten finden Sie unter [Verbundserverproxy-Zertifikate für Office365 und Azure AD erneuern](https://docs.microsoft.com/en-us/azure/active-directory/connect/active-directory-aadconnect-o365-certs).