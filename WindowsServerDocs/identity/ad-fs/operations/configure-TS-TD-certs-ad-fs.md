---
title: Abrufen und Konfigurieren von Tokensignatur- und Tokenentschlüsselungszertifikaten für AD FS
description: In diesem Dokument wird beschrieben, wie zum Abrufen und konfigurieren Sie die TS- und TD Zertifikate für AD FS
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 10/23/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: d16a886c9fb8f88748ffe732a75f0fd6a32c3702
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820211"
---
# <a name="obtain-and-configure-ts-and-td-certificates-for-ad-fs"></a>Abrufen Sie und konfigurieren Sie die TS-"und" TD-Zertifikate für AD FS

Dieses Thema beschreibt die Aufgaben und Verfahren, die Sie ausführen können, um sicherzustellen, dass Ihre AD FS-Tokensignaturzertifikat und token-entschlüsselungszertifikate auf dem neuesten Stand sind.

Token-Signaturzertifikate standard X509 sind Zertifikate, die verwendet werden, um alle Token sicher signiert wird, die der verbungsserver ausstellt. Tokenentschlüsselungszertifikate sind standard X509 Zertifikate, die verwendet werden, um alle eingehenden Token entschlüsselt. Sie werden auch in den Verbundmetadaten veröffentlicht.

Weitere Informationen finden Sie [Zertifikatanforderungen](../design/ad-fs-requirements.md#BKMK_1)

## <a name="determine-whether-ad-fs-renews-the-certificates-automatically"></a>Bestimmen Sie, ob AD FS die Zertifikate automatisch erneuert
Standardmäßig ist AD FS so konfiguriert, dass sowohl zum Zeitpunkt der Erstkonfiguration als auch bei der die Zertifikate dem Ablaufdatum nähern Tokensignatur- und tokenentschlüsselungszertifikate automatisch generiert wird.

Sie können die folgenden Windows PowerShell-Befehl ausführen: `Get-AdfsProperties`.
  
  ![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts1.png)
  
Die Eigenschaft "autocertificaterollover" beschreibt, ob es sich bei AD FS Tokensignatur- und tokenentschlüsselungszertifikaten automatisch erneuern konfiguriert ist.

Wenn "autocertificaterollover" auf "true" festgelegt ist, werden die AD FS-Zertifikate erneuert und in AD FS automatisch konfiguriert werden. Sobald das neue Zertifikat konfiguriert ist, um die zu einen Ausfall vermeiden müssen, dass jeder Verbundpartner (dargestellt in AD FS-Farm durch Vertrauensstellungen der vertrauenden Seite oder Anspruchsanbieter-Vertrauensstellungen) mit diesem neuen Zertifikat aktualisiert wird.
    
Wenn AD FS nicht konfiguriert, Signieren von token zu erneuern und token entschlüsseln Zertifikate automatisch (Wenn "autocertificaterollover" auf "false" festgelegt ist), AD FS wird nicht automatisch generieren oder nutzen Sie neue Tokensignatur- oder tokenentschlüsselungszertifikaten. Sie müssen diese Aufgaben manuell ausführen.
    
Wenn Sie AD FS so konfiguriert ist, um Tokensignatur- und tokenentschlüsselungszertifikaten automatisch erneuern (AutoCertificateRollover ist auf "true" festgelegt), können Sie bestimmen, wann diese erneuert werden:

CertificateGenerationThreshold wird beschrieben, wie viele Tage im Voraus des Zertifikats nicht nach Datum ein neues Zertifikat generiert wird.

CertificatePromotionThreshold bestimmt, wie viele Tage nach der das neue Zertifikat generiert wird, dass er das primäre Zertifikat werden höher gestuft werden (das heißt, AD FS wird gestartet, zum Signieren von ausgestellten Token und Entschlüsselung von Token vom Identitätsanbieter).

![Get-ADFSProperties](media/configure-TS-TD-certs-ad-fs/ts2.png)
  
Wenn Sie AD FS so konfiguriert ist, um Tokensignatur- und tokenentschlüsselungszertifikaten automatisch erneuern (AutoCertificateRollover ist auf "true" festgelegt), können Sie bestimmen, wann diese erneuert werden:

 - **CertificateGenerationThreshold** wird beschrieben, wie viele Tage im Voraus des Zertifikats nicht nach Datum ein neues Zertifikat generiert wird.
 - **CertificatePromotionThreshold** bestimmt, wie viele Tage nach der das neue Zertifikat generiert wird, dass er das primäre Zertifikat werden höher gestuft werden (das heißt, AD FS wird gestartet, zum Signieren von ausgestellten Token und Entschlüsselung von Token aus der Identität Anbieter).

## <a name="determine-when-the-current-certificates-expire"></a>Bestimmen Sie die aktuellen Zertifikate wann ablaufen
Sie können das folgende Verfahren verwenden, um die primäre Tokensignatur- und tokenentschlüsselungszertifikaten zu identifizieren und um zu bestimmen, wann die aktuellen Zertifikate ablaufen.

Sie können die folgenden Windows PowerShell-Befehl ausführen: `Get-AdfsCertificate –CertificateType token-signing` (oder `Get-AdfsCertificate –CertificateType token-decrypting `). Oder Sie können die aktuellen Zertifikate in der MMC überprüfen: Dienst -> Zertifikate.

![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts3.png)

Das Zertifikat für die die **IsPrimary** Wert wird festgelegt, um **"true"** ist das Zertifikat, das AD FS zurzeit verwendet wird.

Das Datum angezeigt, die für die **nicht nach** ist das Datum, die mit dem ein neues primäres Token signieren oder Entschlüsseln der Zertifikat so konfiguriert werden muss.

Um die Dienstkontinuität zu gewährleisten, müssen alle Verbundpartnern (dargestellt in AD FS-Farm durch Vertrauensstellungen der vertrauenden Seite oder Anspruchsanbieter-Vertrauensstellungen) die neue Tokensignatur- und tokenentschlüsselungszertifikate vor diesem Ablauf nutzen. Es wird empfohlen, dass Sie beginnen mit der Planung für diesen Prozess mindestens 60 Tage im voraus.

## <a name="generating-a-new-self-signed-certificate-manually-prior-to-the-end-of-the-grace-period"></a>Generieren ein neues selbstsigniertes Zertifikat manuell vor Ablauf der Toleranzperiode
Sie können die folgenden Schritte aus verwenden, um ein neues selbstsigniertes Zertifikat vor Ablauf der Toleranzperiode manuell zu generieren.

1. Stellen Sie sicher, dass Sie auf dem primären AD FS-Server angemeldet sind.
2. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: `Add-PSSnapin "microsoft.adfs.powershell"`
3. Optional können Sie die aktuellen Signaturzertifikate in AD FS überprüfen. Führen Sie zu diesem Zweck den folgenden Befehl: `Get-ADFSCertificate –CertificateType token-signing`. Sehen Sie sich die Ausgabe des Befehls, um die Daten nicht nach der aufgeführten Zertifikate anzuzeigen.
4. Um ein neues Zertifikat zu generieren, führen Sie den folgenden Befehl zum Erneuern und aktualisieren Sie die Zertifikate auf dem AD FS-Server: `Update-ADFSCertificate –CertificateType token-signing`.
5. Überprüfen Sie das Update aus, indem Sie den folgenden Befehl erneut ausführen: `Get-ADFSCertificate –CertificateType token-signing`
6. Nun sollten zwei Zertifikate aufgeführt, denen eine **nicht nach** Datum, etwa ein Jahr in der Zukunft und für den die **IsPrimary** Wert ist **"false"**.

>[!IMPORTANT]
>Um eine dienstunterbrechung zu vermeiden, aktualisieren Sie die Zertifikatinformationen in Azure AD durch die Schritte, die in ausgeführt wie Update in Azure AD mit einem gültigen Token-signing-Zertifikat.

## <a name="if-youre-not-using-self-signed-certificates"></a>Wenn Sie keine selbstsignierten Zertifikate verwenden...
Wenn Sie nicht über das standardmäßige, die automatisch generierte, selbstsignierte Tokensignatur- und tokenentschlüsselungszertifikate sind, müssen Sie erneuern und diese Zertifikate manuell konfigurieren.

Sie müssen zuerst ein neues Zertifikat von Ihrer Zertifizierungsstelle abrufen und importieren sie in den lokalen Computerspeicher des persönlichen Zertifikatspeicher auf jedem Verbundserver. Anweisungen finden Sie in der [Importieren eines Zertifikats](https://technet.microsoft.com/library/cc754489.aspx) Artikel.

Dann müssen Sie dieses Zertifikat als das sekundäre AD FS-Tokensignaturzertifikat oder Entschlüsselungszertifikat konfigurieren. (Sie konfigurieren sie als sekundäres Zertifikat zu Ihrem Verbundpartnern genügend Zeit für das neue Zertifikat nutzen, bevor Sie es zum primären Zertifikat heraufstufen).

### <a name="to-configure-a-new-certificate-as-a-secondary-certificate"></a>So konfigurieren Sie ein neues Zertifikat als sekundäres Zertifikat
1. Öffnen Sie PowerShell, und führen Sie Folgendes aus: `Set-ADFSProperties -AutoCertificateRollover $false`
2. Nachdem Sie das Zertifikat importiert haben. Öffnen der **AD FS-Verwaltung** Konsole.
3. Erweitern Sie **Service** und wählen Sie dann **Zertifikate**.
4. Klicken Sie im Aktionsbereich auf **Add Token-Signing Certificate**.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts4.png)</br>
5. Wählen Sie das neue Zertifikat aus der Liste der angezeigten Zertifikate aus, und klicken Sie dann auf OK.
6.  Öffnen Sie PowerShell, und führen Sie Folgendes aus: `Set-ADFSProperties -AutoCertificateRollover $true`

>[!WARNING]
>Stellen Sie sicher, dass das neue Zertifikat einen privaten Schlüssel zugeordnet ist, dass die Berechtigungen der AD FS-Dienstkonto Berechtigungen zum Lesen Sie und den privaten Schlüssel. Überprüfen Sie dies auf jedem Verbundserver aus. Klicken Sie dazu in das Zertifikate-Snap-in mit der rechten Maustaste in des neuen Zertifikats, klicken Sie auf alle Aufgaben, und klicken Sie dann auf Privatschlüssel verwalten.

Sobald Sie genügend Zeit für die Verbundpartner nutzen Sie das neue Zertifikat (sie Ihre Verbundmetadaten abrufen oder Sie senden sie den öffentlichen Schlüssel für das neue Zertifikat) erlaubt haben, müssen Sie das sekundäre Zertifikat zum primären Zertifikat höher stufen.

### <a name="to-promote-the-new-certificate-from-secondary-to-primary"></a>Das neue Zertifikat vom sekundären zum primären heraufzustufen.

1. Öffnen der **AD FS-Verwaltung** Konsole.
2. Erweitern Sie **Service** und wählen Sie dann **Zertifikate**.
3. Klicken Sie auf das sekundäre Tokensignaturzertifikat.
4. In der **Aktionen** Bereich, klicken Sie auf **als primär festlegen**. Klicken Sie auf "Ja", in der bestätigungsaufforderung.
![Get-ADFSCertificate](media/configure-TS-TD-certs-ad-fs/ts5.png)</br>


## <a name="updating-federation-partners"></a>Aktualisieren von Verbundpartnern

### <a name="partners-who-can-consume-federation-metadata"></a>Partner, die Metadaten des Verbunds nutzen können
Wenn Sie erneuert haben, und konfigurieren Sie einen neuen Tokensignatur oder tokenentschlüsselungszertifikat, Sie müssen sicherstellen, dass die alle Ihre Verbundpartnern (Organisation oder Konto Organisation Ressourcenpartner, die in Ihrer AD FS, durch die Verwendung dargestellt werden eines Drittanbieters, Vertrauensstellungen und Anspruchsanbieter-Vertrauensstellungen) haben Sie die neuen Zertifikate abgerufen.

### <a name="partners-who-can-not-consume-federation-metadata"></a>Partner, die nicht-Verbundmetadaten nutzen können
Wenn Ihre Verbundpartnern Ihrer Verbundmetadaten nutzen können, müssen Sie manuell sie den öffentlichen Schlüssel für Ihr neues Tokensignaturzertifikat / tokenentschlüsselungszertifikate Zertifikat senden. Senden von neuen öffentlichen Schlüssel des Zertifikats (CER-Datei oder wenn Sie die gesamte Kette einschließen möchten. p7b) aller Ihrer ressourcenorganisation oder Organisation Kontopartner (dargestellt in Ihrer AD FS durch Vertrauensstellungen der vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen). Haben Sie die Partner, die Implementierung von Änderungen auf ihrer Seite, um die neuen Zertifikate zu vertrauen.

### <a name="promote-to-primary-if-autocertificaterollover-is-false"></a>Hochstufen Sie auf primären Server, (Wenn "autocertificaterollover" auf "false" ist)
Wenn **"autocertificaterollover"** nastaven NA hodnotu **"false"**, AD FS wird nicht automatisch generieren oder Start mit der neuen Tokensignatur oder token entschlüsseln Zertifikate. Sie müssen diese Aufgaben manuell ausführen.
Nach dem ermöglicht ein ausreichenden Zeitraum für alle Ihre Verbundpartnern, nutzen Sie die neuen sekundären Zertifikats dieser sekundären Zertifikats zum primären Replikat (im MMC-Snap-in, klicken Sie auf das sekundäre Tokensignaturzertifikat, Zertifikat, und klicken Sie im Aktionsbereich auf höher stufen **Als primär festlegen**.)

## <a name="updating-azure-ad"></a>Aktualisieren von Azure AD
AD FS bietet einmaliges Anmelden auf Microsoft-Clouddienste wie Office 365 Authentifizierung der Benutzer über ihren vorhandenen Anmeldeinformationen des AD DS.  Weitere Informationen zur Verwendung von Zertifikaten finden Sie unter [Erneuern von verbundzertifikaten für Office 365 und Azure AD](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-o365-certs).