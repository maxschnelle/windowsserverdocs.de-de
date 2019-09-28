---
title: Abrufen und Konfigurieren von Tokensignatur-und tokenentschlüsselungszertifikaten für AD FS
description: In diesem Dokument wird beschrieben, wie Sie die TS-und TD-Zertifikate für AD FS abrufen und konfigurieren.
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c544f956983357bdcaaaf2e5ee5b4ab5f80abb6e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407480"
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>Abrufen und Konfigurieren von TS-und TD-Zertifikaten für AD FS

In diesem Thema werden Aufgaben und Prozeduren beschrieben, die Sie ausführen können, um sicherzustellen, dass Ihre AD FS Tokensignatur-und tokenentschlüsselungszertifikate aktuell sind

Tokensignaturzertifikate sind X509-Standardzertifikate, mit denen alle Token, die der Verbund Server ausgibt, sicher signiert werden. Tokenentschlüsselungszertifikate sind Standard-X509-Zertifikate, die verwendet werden, um eingehende Token zu entschlüsseln. Sie werden auch in Verbund Metadaten veröffentlicht.

Weitere Informationen finden Sie unter [Zertifikat Anforderungen](../design/ad-fs-requirements.md#BKMK_1) .

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>Bestimmen, ob AD FS die Zertifikate automatisch erneuert
Standardmäßig ist AD FS so konfiguriert, dass Tokensignaturzertifikate und tokenentschlüsselungszertifikate automatisch generiert werden, und zwar sowohl zum Zeitpunkt der Erstkonfiguration als auch nach dem Ablaufdatum der Zertifikate.

Sie können den folgenden Windows PowerShell-Befehl ausführen `Get-AdfsProperties`:.
  
  ![Get-ADF sproperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
Die autocertificaterollover-Eigenschaft beschreibt, ob AD FS so konfiguriert ist, dass die Tokensignatur und die tokenentschlüsselungszertifikate automatisch erneuert werden.

Wenn autocertificaterollover auf true festgelegt ist, werden die AD FS Zertifikate in AD FS automatisch erneuert und konfiguriert. Nachdem das neue Zertifikat konfiguriert wurde, müssen Sie zur Vermeidung eines Ausfalls sicherstellen, dass jeder Verbund Partner (der in Ihrer AD FS Farm durch Vertrauens Stellungen der vertrauenden Seite oder Anspruchs Anbieter-Vertrauens Stellungen dargestellt wird) mit diesem neuen Zertifikat aktualisiert wird.
    
Wenn AD FS nicht für das automatische Erneuern von Tokensignierung und tokenentschlüsselungszertifikaten konfiguriert ist ("autocertificaterollover" ist auf "false" festgelegt), werden von AD FS nicht automatisch neue Tokensignatur-oder tokenentschlüsselungszertifikate generiert oder gestartet. Diese Aufgaben müssen manuell ausgeführt werden.
    
Wenn AD FS für das automatische Erneuern von Tokensignierung und tokenentschlüsselungszertifikate konfiguriert ist (autocertificaterollover ist auf true festgelegt), können Sie bestimmen, wann Sie erneuert werden:

Certificategenerationthreshold: gibt an, wie viele Tage vor dem Datum, an dem das Zertifikat nicht nach dem Datum generiert wird, ein neues Zertifikat generiert wird.

Mit "certificatepromotionthreshold" wird festgelegt, wie viele Tage nach dem Generieren des neuen Zertifikats der Dienst als primäres Zertifikat herauf gestuft wird (d. h. AD FS mit der Verwendung beginnen, um Token zu signieren, die es ausgibt, und Token von Identitäts Anbietern entschlüsseln).

![Get-ADF sproperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
Wenn AD FS für das automatische Erneuern von Tokensignierung und tokenentschlüsselungszertifikate konfiguriert ist (autocertificaterollover ist auf true festgelegt), können Sie bestimmen, wann Sie erneuert werden:

 - **Certificategenerationthreshold** : gibt an, wie viele Tage vor dem Datum, an dem das Zertifikat nicht nach dem Datum generiert wird, ein neues Zertifikat generiert wird.
 - Mit " **certificatepromotionthreshold** " wird festgelegt, wie viele Tage nach dem Generieren des neuen Zertifikats das neue Zertifikat generiert wird, damit es als primäres AD FS Zertifikat herauf gestuft wird Anbieter).

## <a name="determine-when-the-current-certificates-expire"></a>Bestimmen, wann die aktuellen Zertifikate ablaufen
Mithilfe des folgenden Verfahrens können Sie die primären tokensignier-und tokenentschlüsselungszertifikate identifizieren und ermitteln, wann die aktuellen Zertifikate ablaufen.

Sie können den folgenden Windows PowerShell-Befehl ausführen `Get-AdfsCertificate –CertificateType token-signing` : ( `Get-AdfsCertificate –CertificateType token-decrypting `oder). Oder Sie können die aktuellen Zertifikate in der MMC untersuchen: Dienst > Zertifikate.

![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

Das Zertifikat, für das der **IsPrimary** -Wert auf **true** festgelegt ist, ist das Zertifikat, das zurzeit von AD FS verwendet wird.

Das für " **Not after** " angezeigte Datum ist das Datum, an dem ein neues primäres tokensignier-oder Entschlüsselungszertifikat konfiguriert werden muss.

Um die Dienst Kontinuität zu gewährleisten, müssen alle Verbund Partner, die in Ihrer AD FS Farm durch Vertrauens Stellungen der vertrauenden Seite oder Anspruchs Anbieter-Vertrauens Stellungen dargestellt werden, die neuen Tokensignatur-und tokenentschlüsselungszertifikate vor diesem Ablauf nutzen Es wird empfohlen, dass Sie mindestens 60 Tage im Voraus mit der Planung für diesen Prozess beginnen.

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>Manuelles Erstellen eines neuen selbst signierten Zertifikats vor dem Ende der Toleranz Periode
Sie können die folgenden Schritte ausführen, um vor dem Ende der Toleranz Periode manuell ein neues selbst signiertes Zertifikat zu generieren.

1. Stellen Sie sicher, dass Sie am primären AD FS Server angemeldet sind.
2. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus:`Add-PSSnapin "microsoft.adfs.powershell"`
3. Optional können Sie die aktuellen Signatur Zertifikate in AD FS überprüfen. Führen Sie hierzu den folgenden Befehl aus: `Get-ADFSCertificate –CertificateType token-signing`. Sehen Sie sich die Ausgabe des Befehls an, um das Datum der nicht nach aufgeführten Zertifikate anzuzeigen.
4. Um ein neues Zertifikat zu generieren, führen Sie den folgenden Befehl aus, um die Zertifikate auf dem AD FS- `Update-ADFSCertificate –CertificateType token-signing`Server zu erneuern und zu aktualisieren:.
5. Überprüfen Sie das Update, indem Sie den folgenden Befehl erneut ausführen:`Get-ADFSCertificate –CertificateType token-signing`
6. Nun sollten zwei Zertifikate aufgeführt werden, von denen eine **nicht nach** dem Datum ungefähr ein Jahr in der Zukunft liegt und für die der **IsPrimary** -Wert **false**ist.

>[!IMPORTANT]
>Um einen Dienstausfall zu vermeiden, aktualisieren Sie die Zertifikat Informationen auf Azure AD, indem Sie die Schritte im Thema Aktualisieren von Azure AD mit einem gültigen Tokensignaturzertifikat ausführen.

## <a name="if-youre-not-using-self-signed-certificates"></a>Wenn Sie keine selbst signierten Zertifikate verwenden...
Wenn Sie nicht die standardmäßig automatisch generierten, selbst signierten Tokensignatur-und tokenentschlüsselungszertifikate verwenden, müssen Sie diese Zertifikate manuell erneuern und konfigurieren.

Zunächst müssen Sie ein neues Zertifikat von Ihrer Zertifizierungsstelle abrufen und es in den persönlichen Zertifikat Speicher des lokalen Computers auf jedem Verbund Server importieren. Anweisungen hierzu finden Sie im Artikel [Importieren eines Zertifikats](https://technet.microsoft.com/library/cc754489.aspx) .

Anschließend müssen Sie dieses Zertifikat als sekundäres AD FS Tokensignaturzertifikat oder-Entschlüsselungs Zertifikat konfigurieren. (Sie konfigurieren es als sekundäres Zertifikat, damit Ihre Verbund Partner genug Zeit haben, dieses neue Zertifikat zu nutzen, bevor Sie es auf das primäre Zertifikat herauf Stufen.)

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>So konfigurieren Sie ein neues Zertifikat als sekundäres Zertifikat
1. Öffnen Sie PowerShell, und führen Sie Folgendes aus:`Set-ADFSProperties -AutoCertificateRollover $false`
2. Nachdem Sie das Zertifikat importiert haben. Öffnen Sie die **AD FS-Verwaltungs** Konsole.
3. Erweitern Sie **Dienst** , und wählen Sie dann **Zertifikate**aus.
4. Klicken Sie im Aktionsbereich auf **Tokensignaturzertifikat hinzufügen**.
![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. Wählen Sie das neue Zertifikat aus der Liste der angezeigten Zertifikate aus, und klicken Sie dann auf OK.
6.  Öffnen Sie PowerShell, und führen Sie Folgendes aus:`Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>Stellen Sie sicher, dass dem neuen Zertifikat ein privater Schlüssel zugeordnet ist und dass dem AD FS-Dienst Konto Leseberechtigungen für den privaten Schlüssel erteilt wurden. Überprüfen Sie dies auf jedem Verbund Server. Klicken Sie hierzu im Zertifikat-Snap-in mit der rechten Maustaste auf das neue Zertifikat, klicken Sie auf alle Tasks, und klicken Sie dann auf private Schlüssel verwalten.

Wenn Sie genügend Zeit haben, damit Ihre Verbund Partner Ihr neues Zertifikat nutzen können (indem Sie entweder Ihre Verbund Metadaten abrufen oder Sie den öffentlichen Schlüssel Ihres neuen Zertifikats senden), müssen Sie das sekundäre Zertifikat auf das primäre Zertifikat herauf Stufen.

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>Herauf Stufen des neuen Zertifikats vom sekundären zum primären Replikat

1. Öffnen Sie die **AD FS-Verwaltungs** Konsole.
2. Erweitern Sie **Dienst** , und wählen Sie dann **Zertifikate**aus.
3. Klicken Sie auf das sekundäre Tokensignaturzertifikat.
4. Klicken Sie im **Aktions** Bereich auf **als primär festlegen**. Klicken Sie in der Bestätigungsaufforderung auf Ja.
![Get-adfscertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>Aktualisieren von Verbund Partnern

### <a name="partners-who-can-consume-federation-metadata"></a>Partner, die Verbund Metadaten nutzen können
Wenn Sie ein neues Tokensignaturzertifikat oder-tokenentschlüsselungszertifikat erneuert und konfiguriert haben, müssen Sie sicherstellen, dass alle Verbund Partner (Ressourcen Organisation oder Konto Organisations Partner, die in Ihrer AD FS durch Vertrauens Stellungen der vertrauenden Seite dargestellt werden, und Anspruchs Anbieter-Vertrauens Stellungen) haben die neuen Zertifikate übernommen.

### <a name="partners-who-can-not-consume-federation-metadata"></a>Partner, die keine Verbund Metadaten nutzen können
Wenn Ihre Verbund Partner ihre Verbund Metadaten nicht nutzen können, müssen Sie Sie manuell den öffentlichen Schlüssel Ihres neuen Zertifikats zum Signieren/tokenentschlüsselungszertifikat senden. Senden Sie den öffentlichen Schlüssel des neuen Zertifikats (CER-Datei oder. p7b, wenn Sie die gesamte Kette einbeziehen möchten) in alle Ihre Partner Organisations-oder Konto Organisations Partner (in Ihrer AD FS durch Vertrauens Stellungen der vertrauenden Seite und Anspruchs Anbieter-Vertrauens Stellungen dargestellt). Lassen Sie die Partner Änderungen auf Ihrer Seite implementieren, um den neuen Zertifikaten zu vertrauen.

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>Herauf Stufen zum primären Replikat (wenn autocertificaterollover false ist)
Wenn **autocertificaterollover** auf **false**festgelegt ist, werden von AD FS nicht automatisch neue Tokensignaturzertifikate oder tokenentschlüsselungszertifikate generiert oder gestartet. Diese Aufgaben müssen manuell ausgeführt werden.
Nachdem Sie für alle Verbund Partner einen ausreichenden Zeitraum für die Nutzung des neuen sekundären Zertifikats zugelassen haben, Stufen Sie dieses sekundäre Zertifikat zum primären Zertifikat herauf (Klicken Sie im MMC-Snap-in auf das sekundäre Tokensignaturzertifikat, und klicken Sie im Aktionsbereich auf **Als primär festlegen**.)

## <a name="updating-azure-ad"></a>Aktualisieren von Azure AD
AD FS bietet Single Sign-on Zugriff auf Microsoft Cloud Services wie z. b. Office 365, indem Benutzer über Ihre vorhandenen AD DS Anmelde Informationen authentifiziert werden.  Weitere Informationen zur Verwendung von Zertifikaten finden Sie unter Erneuern von Verbund [Zertifikaten für Office 365 und Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs).