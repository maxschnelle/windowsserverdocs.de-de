---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: 'AD FS: Schnelles Wiederherstellungstool'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/02/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 525ba403473a9de522d9ab30662adc868b17b88d
ms.sourcegitcommit: c02756b7f5c92bf5018e17192f6fffb4754b0f06
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2019
ms.locfileid: "67533509"
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS: Schnelles Wiederherstellungstool

## <a name="overview"></a>Übersicht
Durch das Einrichten einer AD FS-Farm wird derzeit AD FS hoch verfügbar gemacht. Manche Organisationen möchten eine Möglichkeit, einen einzelnen Server AD FS-Bereitstellung verfügen, beseitigt die Notwendigkeit, mehrere AD FS-Servern und Netzwerklastenausgleich-Infrastruktur, aber dennoch einige Assurance der Dienst kann schnell wiederhergestellt werden, wenn ein Problem vorliegt.
Das neue AD FS eine schnelle Wiederherstellung-Tool bietet eine Möglichkeit zum Wiederherstellen von AD FS-Daten ohne eine vollständige Sicherung und Wiederherstellung des Betriebssystems oder des Systemstatus. Sie können das neue Tool verwenden, um AD FS-Konfiguration in Azure oder an einem lokalen Speicherort zu exportieren.  Dann können Sie die exportierten Daten auf einer neuen AD FS-Installation anwenden, duplizieren die AD FS-Umgebung oder neu erstellen. 

## <a name="scenarios"></a>Szenarien
Die AD FS eine schnelle Wiederherstellung-Tool kann in den folgenden Szenarien verwendet werden:

1. Wiederherstellen Sie AD FS-Funktionen schnell, nachdem ein problem
    - Verwenden Sie das Tool, eine cold standby-Installation von AD FS zu erstellen, die anstelle von AD FS-Server online schnell bereitgestellt werden kann
2. Identische Umgebungen für Test- und produktionsumgebungen bereitstellen
    - Verwenden Sie das Tool aus, um schnell eine genaue Kopie der Produktions-AD FS in einer testumgebung zu erstellen oder eine überprüfte Testkonfiguration schnell in die Produktion bereitstellen

## <a name="what-is-backed-up"></a>Was wird gesichert
Das Tool sichert die folgenden AD FS-Konfiguration
    
- AD FS-Konfigurationsdatenbank (SQL oder WID)
- Konfigurationsdatei (befindet sich im Ordner "ADFS")
- Automatisch generierte token signieren und Entschlüsseln von Zertifikaten und privaten Schlüsseln (aus dem Active Directory-DKM-Container)
- SSL-Zertifikat und eine extern registrierte Zertifikate (Tokensignatur-, tokenentschlüsselung und Dienst-Kommunikation) und den zugehörigen privaten Schlüssel (Hinweis: private Schlüssel müssen exportierbar sein und Ausführen des Skripts müssen Berechtigungen für den Zugriff)
- Eine Liste der benutzerdefinierte Authentifizierungsanbieter, Attributspeicher und lokales Anspruchsanbieter-Vertrauensstellungen, die installiert werden.

## <a name="how-to-use-the-tool"></a>Gewusst wie: Verwenden Sie das tool
Zuerst [herunterladen](https://go.microsoft.com/fwlink/?LinkId=825646) und installieren Sie die MSI-Datei auf dem AD FS-Server.  

Führen Sie den folgenden Befehl an einer PowerShell-Eingabeaufforderung ein:

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Wenn Sie die Windows integrierten Datenbank (WID) verwenden, muss dieses Tool auf dem primären AD FS-Server ausgeführt werden.  Sie können die `Get-AdfsSyncProperties` PowerShell-Cmdlet, um zu bestimmen, ob der Server auf möchten, ist der primäre Server.

### <a name="system-requirements"></a>Systemanforderungen

- Dieses Tool kann für AD FS in Windows Server 2012 R2 und höher. 
- Das erforderliche .NET Framework ist mindestens 4.0. 
- Die Wiederherstellung muss für AD FS-Server die gleiche Version wie die Sicherung ausgeführt werden, und, die der gleiche Active Directory-Konto als das AD FS-Dienstkonto verwendet.

## <a name="create-a-backup"></a>Erstellen Sie eine Sicherung
Verwenden Sie das Backup-AD FS-Cmdlet, um eine Sicherung zu erstellen. Dieses Cmdlet, sichert der AD FS-Konfiguration, die Datenbank, die SSL-Zertifikate, die usw. ab. 

Der Benutzer muss mindestens ein lokaler Administrator aus, um dieses Cmdlet auszuführen sein. Zum Sichern des Active Directory-DKM-Containers (in der standardmäßigen AD FS-Konfiguration erforderlich) der Benutzer muss Domänen-Admins sein, die Anmeldeinformationen des AD FS-Dienstkonto übergeben muss, oder hat Zugriff auf die DKM-Container.  Wenn Sie ein gMSA-Konto verwenden, kann der Benutzer muss Domänen-Admins sein oder über die Berechtigungen für den Container verfügen; Sie können keine gruppenverwalteten Dienstkonto-Anmeldeinformationen angeben. 

Die Sicherung wird nach dem Muster "AdfsBackup_ID_Date-Time" benannt. Enthält die Versionsnummer, Datum und Uhrzeit, die die Sicherung durchgeführt wurde.
Das Cmdlet verwendet die folgenden Parameter:
    
Parametersätze

![AD FS: Schnelles Wiederherstellungstool](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>Ausführliche Beschreibung

- **BackupDKM** -sichert der Active Directory-DKM-Container, die AD FS-Schlüssel in der Standardkonfiguration (automatisch generierte Token, Signieren und Entschlüsseln von Zertifikaten) enthält. Dabei wird ein AD-Tool "Ldifde" So exportieren Sie die AD-Container und allen seinen Unterstrukturen verwendet.

- -**StorageType &lt;Zeichenfolge&gt;**  – der Typ des Speichers, die die Benutzer verwenden möchte. "FileSystem" gibt an, dass der Benutzer möchte, um es in einen Ordner zu speichern, lokal oder im Netzwerk "Azure" gibt an, möchte, dass der Benutzer in Azure Storage-Container zu speichern, wenn der Benutzer die Sicherung ausführt, wählen Sie den Sicherungsspeicherort entweder im Dateisystem oder in der die Cloud. Für Azure verwendet werden muss Azure Storage-Anmeldeinformationen an das Cmdlet übergeben werden. Die speicheranmeldeinformationen enthält, den Kontonamen und Schlüssel. Darüber hinaus muss ein Containername auch in übergeben werden. Wenn der Container nicht vorhanden ist, wird es während der Sicherung erstellt. Für das Dateisystem verwendet werden muss ein Storage-Pfad angegeben werden. In diesem Verzeichnis wird ein neues Verzeichnis für die einzelnen Sicherungen erstellt werden. Jedes Verzeichnis erstellt, werden die gesicherten Dateien enthalten. 

- **EncryptionPassword &lt;Zeichenfolge&gt;**  -das Kennwort, das mit der alle gesicherten Dateien zu verschlüsseln, bevor sie gespeichert werden soll

- **AzureConnectionCredentials &lt;Pscredential&gt;**  -den Kontonamen und Schlüssel für Azure Storage-Konto

- **AzureStorageContainer &lt;Zeichenfolge&gt;**  -Speichercontainer, in dem die Sicherung in Azure gespeichert wird,

- **StoragePath &lt;Zeichenfolge&gt;**  – der Speicherort die Sicherungen gespeichert werden soll

- **ServiceAccountCredential &lt;Pscredential&gt;**  – gibt an, das Dienstkonto für den AD FS-Dienst, die derzeit ausgeführte verwendet wird. Dieser Parameter ist nur erforderlich, wenn der Benutzer die DKM sichern möchten, ist kein Domänenadministrator und hat keinen Zugriff auf den Inhalt des Containers. 

- **BackupComment &lt;string []&gt;**  -eine Informationszeichenfolge zur Sicherung, die während der Wiederherstellung, ähnelt dem Konzept für die Benennung von Hyper-V-Prüfpunkt angezeigt werden. Der Standardwert ist eine leere Zeichenfolge

 
## <a name="backup-examples"></a>Beispiele für die Sicherung
Es folgen Beispiele von Sicherungen für für die Verwendung der AD FS schnelle-Restore-Tool.

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-and-has-access-to-the-dkm-container-contents-either-domain-admin-or-delegated"></a>Sichern der AD FS-Konfiguration mit der DKM, in das Dateisystem und Zugriff auf die DKM-Container-Inhalte (entweder Domänen-Admins oder delegierten)

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>Sichern der AD FS-Konfiguration, mit der DKM, in das Dateisystem mit dem Dienstkonto-Anmeldeinformationen, mit lokalen Administratorrechten ausführen

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Sichern Sie die AD FS-Konfiguration ohne die DKM in den Azure-Speichercontainer.

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>Sichern der AD FS-Konfiguration ohne die DKM in das Dateisystem

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>Wiederherstellen aus einer Sicherung
Verwenden Sie zum Anwenden einer Konfigurations mit Backup-AD FS zu einer neuen AD FS-Installation erstellt das Cmdlet "Restore-AD FS" ein.

Dieses Cmdlet erstellt eine neue AD FS-Farm, die mit dem Cmdlet `Install-AdfsFarm` und wieder her, die AD FS-Konfiguration, Datenbank, Zertifikate usw.  Wenn der AD FS-Serverrolle nicht auf dem Server installiert wurde, wird das Cmdlet installiert.  Das Cmdlet überprüft den Speicherort für die Wiederherstellung für vorhandene Sicherungen und fordert den Benutzer auf eine geeignete Sicherung basierend auf Datum/Uhrzeit der Aufnahme und Sicherung kommentieren, die der Benutzer auf die Sicherung angefügt haben möglicherweise auswählen. Es gibt mehrere AD FS-Konfigurationen mit verschiedenen Verbund-Dienstnamen, wird der Benutzer aufgefordert, zuerst den entsprechenden AD FS-Konfiguration auswählen.
Der Benutzer hat sowohl lokale als auch Administratorrechte, um dieses Cmdlet auszuführen.


>[!NOTE] 
>Vor der Verwendung der AD FS schnelle-Wiederherstellungstool, stellen Sie sicher, dass der Server mit der Domäne vor dem Wiederherstellen der Sicherung verbunden ist. 

Das Cmdlet verwendet die folgenden Parameter: 

![AD FS: Schnelles Wiederherstellungstool](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>Ausführliche Beschreibung

- **StorageType &lt;Zeichenfolge&gt;**  – der Typ des Speichers, die die Benutzer verwenden möchte.
 "FileSystem" gibt an, dass der Benutzer möchte in einem Ordner lokal zu speichern oder im Netzwerk "Azure" gibt an, dass der Benutzer möchte, um sie in den Azure Storage-Container speichern

- **DecryptionPassword &lt;Zeichenfolge&gt;**  -das Kennwort, das verwendet wurde, um alle gesicherten Dateien zu verschlüsseln. 

- **AzureConnectionCredentials &lt;Pscredential&gt;**  -den Kontonamen und Schlüssel für Azure Storage-Konto

- **AzureStorageContainer &lt;Zeichenfolge&gt;**  -Speichercontainer, in dem die Sicherung in Azure gespeichert wird,

- **StoragePath &lt;Zeichenfolge&gt;**  – der Speicherort die Sicherungen gespeichert werden soll

- **ADFSName &lt; Zeichenfolge &gt;**  -der Name des Verbunds, der wurde gesichert und wiederhergestellt werden soll. Wenn dieser nicht angegeben Wert und wird nur eine verbunddienstname dann, die verwendet werden. Es ist mehr als ein Verbunddienst gesichert, um den Speicherort, und dann der Benutzer wird aufgefordert, eine der gesicherten Verbunddienste auszuwählen.

- **ServiceAccountCredential &lt; Pscredential &gt;**  – gibt an, das Dienstkonto, die verwendet werden, für den neuen AD FS-Dienst wiederhergestellt wird 

- **GroupServiceAccountIdentifier &lt;Zeichenfolge&gt;**  -das GMSA, die der Benutzer möchte, verwenden Sie für den neuen AD FS-Dienst wiederhergestellt wird. In der Standardeinstellung Wenn weder um die gesicherten bereitgestellt wird wird Kontoname verwendet, wenn GMSA, else war der Benutzer, zum Füllen eines Dienstkontos aufgefordert wird

- **DBConnectionString &lt;Zeichenfolge&gt;**  : Wenn der Benutzer eine andere Datenbank zum Wiederherstellen verwenden möchten und klicken Sie dann sie die SQL-Verbindungszeichenfolge oder einen Typ WID für Ihre übergeben werden sollte

- **Force &lt;"bool"&gt;**  -überspringen Sie die Anweisungen, die das Tool möglicherweise, wenn die Sicherung ausgewählt wird

- **RestoreDKM &lt;"bool"&gt;**  – die DKM-Container in AD wiederherstellen, sollte festgelegt werden, wenn eine neue AD und die DKM ursprünglich gesichert wurde.

## <a name="restore-examples"></a>Beispiele für Restore

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Wiederherstellen der AD FS-Konfigurations ohne die DKM aus dem Azure-Speichercontainer

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>Wiederherstellen der AD FS-Konfigurations ohne die DKM aus dem Dateisystem
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>Wiederherstellen der AD FS-Konfiguration mit die DKM in das Dateisystem 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>Wiederherstellen von AD FS-Konfiguration auf WID

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>Wiederherstellen von AD FS-Konfiguration mit SQL

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>Stellt den AD FS-Konfiguration mit der angegebenen GMSA

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>Wiederherstellen der AD FS-Konfiguration mit den angegebenen Dienst-Konto-Anmeldeinformationen

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>Informationen zum Verschlüsselungsschlüssel
Alle Sicherungsdaten werden verschlüsselt, bevor Sie in die Cloud verschieben oder im Dateisystem speichern.  

Jedes Dokument, das erstellt wird, als Teil der Sicherung mithilfe von AES-256 verschlüsselt wird. Das Kennwort in das Tool übergeben wird als eine Passphrase verwendet, um ein neues Kennwort ein, die mithilfe der Rfc2898DeriveBytes-Klasse zu generieren. 

RNGCryptoServiceProvider-Klasse wird verwendet, um den Salt-Wert verwendet, die mit AES und der Rfc2898DeriveBytes-Klasse zu generieren. 

## <a name="log-files"></a>Protokolldateien
Jedes Mal, wenn eine Sicherung oder Wiederherstellung ausgeführt wird, wird eine Protokolldatei erstellt. Diese finden Sie unter folgendem Speicherort:

- **%localappdata%\ADFSRapidRecreationTool**

>[!NOTE]
> Beim Durchführen einer Wiederherstellung, die eine PostRestore_Instructions-Datei mit einer Übersicht über die zusätzliche Authentifizierung-Anbieter erstellt werden kann, Attribut speichert, und lokale Anspruchsanbieter-Vertrauensstellungen manuell installiert werden, vor dem Starten des AD FS-Diensts.

## <a name="version-release-history"></a>Verlauf der Versionsveröffentlichungen

### <a name="version-10820"></a>Version 1.0.82.0
Version: Juli 2019

**Behobene Probleme:**
- Programmfehlerbehebung für AD FS service Kontonamen, die LDAP-Escape-Zeichen enthalten.


### <a name="version-10810"></a>Version: 1.0.81.0
Version: April 2019

**Behobene Probleme:**


- Fehlerbehebungen für Zertifikat sichern und Wiederherstellen
- Zusätzliche Ablaufverfolgungsinformationen in die Protokolldatei


### <a name="version-10750"></a>Version: 1.0.75.0
Version: August 2018

**Behobene Probleme:**
* Aktualisieren Sie bei Verwendung den Switch - BackupDKM Backup-AD FS.  Das Tool bestimmt, ob der aktuelle Kontext auf die DKM-Container zugreifen.  Wenn dies der Fall ist, wird es entweder über Domänenadministratorrechte oder Anmeldeinformationen für das Dienstkonto keine erforderlich.  Dadurch können automatisierte Sicherungen erfolgen ohne explizit Bereitstellen von Anmeldeinformationen oder als ein Domänenadministratorkonto ausgeführt wird.

### <a name="version-10730"></a>Version: 1.0.73.0
Version: August 2018

**Behobene Probleme:**
* Aktualisieren Sie die Verschlüsselungsalgorithmen, sodass die Anwendung die FIPS-konform ist
    
    >[!NOTE]
    > Auf alte Sicherungen funktionieren nicht mit der neuen Version aufgrund von Änderungen in Verschlüsselungsalgorithmen gemäß FIPS-Kompatibilität
    
* Hinzufügen von Unterstützung für SQL-Cluster, die mithilfe der Mergereplikation

### <a name="version-10720"></a>Version: 1.0.72.0
Version: Juli 2018

**Behobene Probleme:**

   - Fehlerbehebung: Korrigiert die. MSI-Installationsprogramm, um direkte Upgrades zu unterstützen. 

### <a name="10180"></a>1.0.18.0
Version: Juli 2018

**Behobene Probleme:**

   - Programmfehlerbehebung: Behandeln Sie Kennwörter für Dienstkonten, die Sonderzeichen enthalten (z. B. "&")
   - Programmfehlerbehebung: Wiederherstellung schlägt fehl, da Microsoft.IdentityServer.Servicehost.exe.config von einem anderen Prozess verwendet wird


### <a name="1000"></a>1.0.0.0
Veröffentlicht: Oktober 2016

Erste Version von AD FS eine schnelle Wiederherstellung-Tool
