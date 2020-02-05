---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: 'AD FS: Schnelles Wiederherstellungstool'
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/02/2019
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 8b47cdc4770b1ed6478d1502ed5264164e99352b
ms.sourcegitcommit: a33404f92867089bb9b0defcd50960ff231eef3f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/04/2020
ms.locfileid: "77013045"
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS: Schnelles Wiederherstellungstool

## <a name="overview"></a>Übersicht
Heute wird AD FS durch das Einrichten einer AD FS-Farm hoch verfügbar gemacht. Einige Organisationen möchten eine Möglichkeit haben, einen einzelnen Server AD FS Bereitstellung zu haben, wodurch mehrere AD FS Server und Netzwerk Lastenausgleich-Infrastruktur entfällt, während gleichzeitig sichergestellt ist, dass der Dienst bei einem Problem schnell wieder hergestellt werden kann.
Mit dem neuen AD FS Rapid Restore Tool können AD FS Daten wieder hergestellt werden, ohne dass eine vollständige Sicherung und Wiederherstellung des Betriebssystems oder des Systemstatus erforderlich ist. Sie können das neue Tool verwenden, um AD FS Konfiguration entweder in Azure oder an einen lokalen Speicherort zu exportieren.  Anschließend können Sie die exportierten Daten auf eine neue AD FS Installation anwenden und die AD FS Umgebung neu erstellen oder duplizieren. 

## <a name="scenarios"></a>Szenarien
Das AD FS Tool für die schnelle Wiederherstellung kann in den folgenden Szenarien verwendet werden:

1. AD FS Funktionalität nach einem Problem schnell wiederherstellen
    - Verwenden Sie das Tool, um eine kalt Standby-Installation von AD FS zu erstellen, die direkt anstelle des Online AD FS Servers bereitgestellt werden kann.
2. Bereitstellen identischer Test-und Produktionsumgebungen
    - Verwenden Sie das Tool, um schnell eine genaue Kopie der Produktions AD FS in einer Testumgebung zu erstellen oder eine validierte Testkonfiguration schnell in der Produktionsumgebung bereitzustellen.

>[!NOTE] 
>Wenn Sie die SQL-Mergereplikation oder Always on-Verfügbarkeits Gruppen verwenden, wird das Tool für die schnelle Wiederherstellung nicht unterstützt. Es wird empfohlen, SQL-basierte Sicherungen und eine Sicherung des SSL-Zertifikats als Alternative zu verwenden.

## <a name="what-is-backed-up"></a>Was wird gesichert?
Das Tool sichert die folgenden AD FS Konfiguration.
    
- AD FS Konfigurations Datenbank (SQL oder WID)
- Konfigurationsdatei (befindet sich in AD FS Ordner)
- Automatisch generierte Tokensignatur-und entschlüsselungszertifikate und private Schlüssel (aus dem Active Directory DKM-Container)
- SSL-Zertifikat und alle extern registrierten Zertifikate (Tokensignatur, tokenentschlüsselung und Dienst Kommunikation) und zugehörige private Schlüssel (Hinweis: private Schlüssel müssen exportierbar sein, und der Benutzer, der das Skript ausgeführt hat, muss über Zugriffsberechtigungen verfügen)
- Eine Liste mit den benutzerdefinierten Authentifizierungs Anbietern, Attribut speichern und lokalen Anspruchs Anbieter-Vertrauens Stellungen, die installiert werden.

## <a name="how-to-use-the-tool"></a>Verwenden des Tools
[Laden Sie](https://go.microsoft.com/fwlink/?LinkId=825646) zunächst die MSI-Datei auf Ihren AD FS Server herunter, und installieren Sie Sie.  

Führen Sie den folgenden Befehl an einer PowerShell-Eingabeaufforderung aus:

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Wenn Sie die integrierte Windows-Datenbank (WID) verwenden, muss dieses Tool auf dem primären AD FS Server ausgeführt werden.  Mit dem `Get-AdfsSyncProperties` PowerShell-Cmdlet können Sie ermitteln, ob es sich bei dem Server, auf dem Sie sich befinden, um den primären Server handelt.

### <a name="system-requirements"></a>System requirements (Systemanforderungen)

- Dieses Tool funktioniert für AD FS in Windows Server 2012 R2 und höher. 
- Die erforderliche .NET Framework-Version ist mindestens 4,0. 
- Die Wiederherstellung muss auf einem AD FS Server mit derselben Version wie die Sicherung durchgeführt werden, die dasselbe Active Directory Konto wie das AD FS Dienst Konto verwendet.

## <a name="create-a-backup"></a>Erstellen einer Sicherung
Verwenden Sie das Backup-ADFS-Cmdlet, um eine Sicherung zu erstellen. Dieses Cmdlet sichert die AD FS Konfiguration, Datenbank, SSL-Zertifikate usw. 

Der Benutzer muss mindestens ein lokaler Administrator sein, um dieses Cmdlet ausführen zu können. Zum Sichern des Active Directory DKM-Containers (erforderlich in der standardmäßigen AD FS Konfiguration) muss der Benutzer entweder Domänen Administrator sein, muss die Anmelde Informationen des AD FS Dienst Kontos übergeben oder Zugriff auf den DKM-Container haben.  Wenn Sie ein GMSA-Konto verwenden, muss der Benutzer ein Domänen Administrator sein oder über Berechtigungen für den Container verfügen. die GMSA-Anmelde Informationen können nicht bereitgestellt werden. 

Die Sicherung wird gemäß dem Muster "adfsBackup_ID_Date-Time" benannt. Sie enthält die Versionsnummer, das Datum und die Uhrzeit, zu der die Sicherung abgeschlossen wurde.
Das-Cmdlet übernimmt die folgenden Parameter:
    
Parameter Sätze

![AD FS: Schnelles Wiederherstellungstool](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>Ausführliche Beschreibung

- **Backupdkm** : sichert den Active Directory DKM-Container, der die AD FS Schlüssel in der Standardkonfiguration enthält (automatisch generierte tokensignier-und entschlüsselungszertifikate). Dabei wird ein Ad-Tool "Ldifde" verwendet, um den AD-Container und alle zugehörigen Unterstrukturen zu exportieren.

- -**StorageType &lt;Zeichenfolge&gt;** -der Typ des Speichers, den der Benutzer verwenden möchte. "File System" gibt an, dass der Benutzer ihn lokal oder im Netzwerk "Azure Azure Storage" in einem Ordner speichern möchte, wenn der Benutzer die Sicherung durchführt, und wählt den Sicherungs Speicherort aus, entweder im Datei System oder im Cloud. Damit Azure verwendet werden kann, müssen Azure Storage Anmelde Informationen an das Cmdlet übergeben werden. Die Speicher Anmelde Informationen enthalten den Kontonamen und den Schlüssel. Zusätzlich muss auch ein Container Name übergebenen werden. Wenn der Container nicht vorhanden ist, wird er während der Sicherung erstellt. Damit das Dateisystem verwendet werden kann, muss ein Speicherpfad angegeben werden. In diesem Verzeichnis wird für jede Sicherung ein neues Verzeichnis erstellt. Jedes erstellte Verzeichnis enthält die gesicherten Dateien. 

- **Verschlüsselungskennwort &lt;Zeichenfolge&gt;** : das Kennwort, das verwendet wird, um alle gesicherten Dateien vor dem Speichern zu verschlüsseln.

- **Azureconnection-Anmelde Informationen &lt;PSCredential&gt;** -der Kontoname und Schlüssel für das Azure-Speicherkonto

- **Azurestoragecontainer &lt;Zeichenfolge&gt;** -der Speicher Container, in dem die Sicherung in Azure gespeichert wird.

- **Storagepath &lt;Zeichenfolge&gt;** -der Speicherort, in dem die Sicherungen gespeichert werden.

- **Serviceaccountcredential &lt;PSCredential&gt;** : gibt das Dienst Konto an, das für den derzeit ausgelaufenden AD FS-Dienst verwendet wird. Dieser Parameter ist nur erforderlich, wenn der Benutzer DKM sichern und nicht als Domänen Administrator oder nicht auf den Inhalt des Containers zugreifen möchte. 

- **Backupcomment &lt;Zeichenfolge []&gt;** -eine Informations Zeichenfolge zur Sicherung, die während der Wiederherstellung angezeigt wird, ähnlich wie das Konzept der Hyper-V-Prüf Punkt Benennung. Der Standardwert ist eine leere Zeichenfolge.

 
## <a name="backup-examples"></a>Beispiele für Sicherungen
Im folgenden finden Sie Sicherungs Beispiele für die Verwendung des AD FS Tool für die schnelle Wiederherstellung.

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-and-has-access-to-the-dkm-container-contents-either-domain-admin-or-delegated"></a>Sichern Sie die AD FS Konfiguration mit der DKM-Datei im Datei System, und haben Sie Zugriff auf den Inhalt des DKM-Containers (entweder Domänen Administrator oder delegiert).

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>Sichern Sie die AD FS Konfiguration mit der DKM-Datei im Dateisystem mit den Anmelde Informationen des Dienst Kontos, die als lokaler Administrator ausgeführt werden.

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Sichern Sie die AD FS Konfiguration ohne DKM im Container Azure Storage.

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>Sichern der AD FS Konfiguration ohne DKM im Datei System

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>Aus Sicherung wiederherstellen
Verwenden Sie das Cmdlet Restore-ADFS, um eine Konfiguration, die mithilfe von Backup-ADFS erstellt wurde, auf eine neue AD FS-Installation anzuwenden.

Dieses Cmdlet erstellt eine neue AD FS Farm mithilfe des-Cmdlets `Install-AdfsFarm` und stellt die AD FS Konfiguration, Datenbank, Zertifikate usw. wieder her.  Wenn die AD FS Rolle nicht auf dem Server installiert wurde, wird Sie vom Cmdlet installiert.  Mit dem-Cmdlet wird der Wiederherstellungs Speicherort für vorhandene Sicherungen überprüft, und der Benutzer wird aufgefordert, eine geeignete Sicherung basierend auf dem Datum und der Uhrzeit der Erstellung und jedem Sicherungs Kommentar, den der Benutzer möglicherweise an die Sicherung angefügt hat, auszuwählen. Wenn mehrere AD FS Konfigurationen mit unterschiedlichen Verbund Dienstnamen vorhanden sind, wird der Benutzer aufgefordert, zuerst die entsprechende AD FS Konfiguration auszuwählen.
Der Benutzer muss sowohl lokal als auch Domänen Administrator sein, um dieses Cmdlet ausführen zu können.


>[!NOTE] 
>Stellen Sie vor dem Wiederherstellen der Sicherung sicher, dass der Server der Domäne hinzugefügt wird, bevor Sie das AD FS Tool für die schnelle Wiederherstellung verwenden. 

Das-Cmdlet übernimmt die folgenden Parameter: 

![AD FS: Schnelles Wiederherstellungstool](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>Ausführliche Beschreibung

- **StorageType &lt;Zeichenfolge&gt;** -der Typ des Speichers, den der Benutzer verwenden möchte.
 "File System" gibt an, dass der Benutzer ihn lokal oder im Netzwerk "Azure" in einem Ordner speichern möchte, wenn der Benutzer ihn im Azure Storage Container speichern möchte.

- **Decryptionpassword &lt;Zeichenfolge&gt;** -das Kennwort, das zum Verschlüsseln aller gesicherten Dateien verwendet wurde. 

- **Azureconnection-Anmelde Informationen &lt;PSCredential&gt;** -der Kontoname und Schlüssel für das Azure-Speicherkonto

- **Azurestoragecontainer &lt;Zeichenfolge&gt;** -der Speicher Container, in dem die Sicherung in Azure gespeichert wird.

- **Storagepath &lt;Zeichenfolge&gt;** -der Speicherort, in dem die Sicherungen gespeichert werden.

- **Adfsname &lt; Zeichenfolge &gt;** -der Name des Verbunds, der gesichert und wieder hergestellt werden soll. Wenn diese nicht bereitgestellt wird und nur ein Verbund Dienst Name vorhanden ist, wird dieser verwendet. Wenn mehrere Verbund Dienste am Standort gesichert sind, wird der Benutzer aufgefordert, einen der gesicherten Verbund Dienste auszuwählen.

- **Serviceaccountcredential &lt; PSCredential &gt;** : gibt das Dienst Konto an, das für den neuen AD FS Dienst, der wieder hergestellt wird, verwendet wird. 

- **Groupserviceaccountidentifier &lt;Zeichenfolge&gt;** -der GMSA, den der Benutzer für den neuen AD FS Dienst verwenden möchte, der wieder hergestellt wird. Wenn keines der beiden bereitgestellt wird, wird der gesicherte Konto Name verwendet, wenn es sich um ein GMSA handelt, andernfalls wird der Benutzer aufgefordert, ein Dienst Konto einzufügen.

- **DbConnectionString &lt;Zeichenfolge&gt;** : Wenn der Benutzer eine andere Datenbank für die Wiederherstellung verwenden möchte, sollten Sie die SQL-Verbindungs Zeichenfolge oder den Typ in wid für wid übergeben.

- **Erzwingen &lt;bool&gt;** -überspringen Sie die Eingabe Aufforderungen, die das Tool möglicherweise hat, nachdem die Sicherung ausgewählt wurde.

- **Restoredkm &lt;bool&gt;** -stellen Sie den DKM-Container in der AD-Datenbank wieder her, sollte festgelegt werden, wenn Sie zu einer neuen AD-Installation wechseln und DKM anfänglich gesichert wurde.

## <a name="restore-examples"></a>Wiederherstellungs Beispiele

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Stellen Sie die AD FS Konfiguration ohne DKM aus dem Azure Storage Container wieder her.

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>Wiederherstellen der AD FS Konfiguration ohne DKM aus dem Datei System
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>Stellen Sie die AD FS Konfiguration mit der DKM-Datei im Datei System wieder her. 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>Wiederherstellen der AD FS Konfiguration in wid

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>Wiederherstellen der AD FS Konfiguration in SQL

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>Stellt die AD FS Konfiguration mit dem angegebenen GMSA wieder her.

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>Stellen Sie die AD FS Konfiguration mit den angegebenen Dienst Konto-Anmelde Einstellungen wieder her.

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>Verschlüsselungs Informationen
Alle Sicherungsdaten werden verschlüsselt, bevor Sie in die Cloud übertragen oder im Dateisystem gespeichert werden.  

Jedes Dokument, das als Teil der Sicherung erstellt wird, wird mit AES-256 verschlüsselt. Das an das Tool übergebene Kennwort wird als Passphrase zum Generieren eines neuen Kennworts mithilfe der Rfc2898DeriveBytes-Klasse verwendet. 

RNGCryptoServiceProvider wird zum Generieren des Salt verwendet, das von AES und der Rfc2898DeriveBytes-Klasse verwendet wird. 

## <a name="log-files"></a>Protokolldateien
Jedes Mal, wenn eine Sicherung oder Wiederherstellung ausgeführt wird, wird eine Protokolldatei erstellt. Diese finden Sie unter folgendem Speicherort:

- **%LocalAppData%\adfsrapidrecreationtool**

>[!NOTE]
> Beim Ausführen einer Wiederherstellung kann eine PostRestore_Instructions Datei erstellt werden, die eine Übersicht über die zusätzlichen Authentifizierungs Anbieter, Attribut Speicher und lokalen Anspruchs Anbieter-Vertrauens Stellungen enthält, die vor dem Starten des AD FS Dienstanbieters manuell installiert werden müssen.

## <a name="version-release-history"></a>Versions Veröffentlichungs Verlauf

### <a name="version-10820"></a>Version 1.0.82.0
Release: 2019

**Behobene Probleme:**
- Programmfehler Behebung für AD FS Dienst Kontonamen, die LDAP-Escapezeichen enthalten


### <a name="version-10810"></a>Version: 1.0.81.0
Release: 2019

**Behobene Probleme:**


- Fehlerbehebungen für die Zertifikat Sicherung und-Wiederherstellung
- Zusätzliche Ablauf Verfolgungs Informationen in der Protokolldatei


### <a name="version-10750"></a>Version: 1.0.75.0
Release: 2018

**Behobene Probleme:**
* Aktualisieren Sie Backup-ADFS bei Verwendung des Schalters "-backupdkm".  Das Tool bestimmt, ob der aktuelle Kontext Zugriff auf den DKM-Container hat.  Wenn dies der Fall ist, sind keine Domänen Administratorrechte oder Dienst Konto-Anmelde Informationen erforderlich.  Dadurch können automatisierte Sicherungen erfolgen, ohne explizit Anmelde Informationen bereitzustellen oder als Domänen Administrator Konto ausgeführt zu werden.

### <a name="version-10730"></a>Version: 1.0.73.0
Release: 2018

**Behobene Probleme:**
* Aktualisieren der Verschlüsselungsalgorithmen, damit die Anwendung mit der Konformität kompatibel ist
    
    >[!NOTE]
    > Alte Sicherungen funktionieren aufgrund von Änderungen an Verschlüsselungsalgorithmen gemäß der Konformität gemäß der Konformität nicht mit der neuen Version.
    
* Unterstützung für SQL-Cluster mit Mergereplikation hinzufügen

### <a name="version-10720"></a>Version: 1.0.72.0
Release: 2018

**Behobene Probleme:**

   - Programmfehler Behebung: korrigiert. MSI-Installationsprogramm zur Unterstützung von direkten Upgrades 

### <a name="10180"></a>1.0.18.0
Release: 2018

**Behobene Probleme:**

   - Programmfehler Behebung: behandeln Sie Dienst Konto Kennwörter, die Sonderzeichen enthalten (d.h. "&").
   - Programmfehler Behebung: bei der Wiederherstellung tritt ein Fehler auf, weil Microsoft. identityserver. ServiceHost. exe. config von einem anderen Prozess verwendet wird.


### <a name="1000"></a>1.0.0.0
Veröffentlicht: Oktober 2016

Erste Version von AD FS Tool für die schnelle Wiederherstellung
