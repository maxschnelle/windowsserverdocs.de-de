---
ms.assetid: 4deff06a-d0ef-4e5a-9701-5911ba667201
title: 'AD FS: Schnelles Wiederherstellungstool'
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 02/20/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cd1cc8dab07288ba73c507bc551f089bb79502bc
ms.sourcegitcommit: 36d7b1dfd7da8e9f303d007a628e76149de000f2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/21/2018
---
# <a name="ad-fs-rapid-restore-tool"></a>AD FS: Schnelles Wiederherstellungstool

>Gilt für: Windows Server 2016, Windows Server2012 R2

## <a name="overview"></a>(Übersicht)
Heute wird AD FS mit hoher Verfügbarkeit, indem eine AD FS-Farm einrichten. Einige Unternehmen möchten eine Möglichkeit, einen Einzelserver AD FS-Bereitstellung haben, mehrere AD FS-Server und den Netzwerklastenausgleich-Infrastruktur, während Sie gleichzeitig einige überflüssig Sicherheitsgrad, den Dienst kann wiederhergestellt werden, schnell, wenn ein Problem vorliegt.
Das neue AD FS Rapid Restore-Tool bietet eine Möglichkeit zum Wiederherstellen von AD FS-Daten ohne eine vollständige Sicherung und Wiederherstellung des Betriebssystems oder des Systemstatus. Das neue Tool können Sie AD FS-Konfiguration in Azure oder an einem lokalen Speicherort exportieren.  Dann können Sie die exportierten Daten zu einer neuen AD FS-Installation anwenden, die AD FS-Umgebung duplizieren oder neu erstellen. 

## <a name="scenarios"></a>Szenarien
Das AD FS schnelle Restore-Tool kann in den folgenden Szenarien verwendet werden:

1. Schnelle Wiederherstellung der AD FS-Funktionen nach dem ein Problem aufgetreten
    - Verwenden Sie das Tool eine cold standby-Installation von AD FS zu erstellen, die schnell anstelle online AD FS-Server bereitgestellt werden kann
2. Identische Test- und produktionsumgebungen Umgebungen bereitstellen
    - Verwenden Sie das Tool, um schnell eine exakte Kopie der Produktion AD FS in einer testumgebung zu erstellen oder schnell bereitstellen eine überprüften Testkonfiguration für die Produktion

## <a name="what-is-backed-up"></a>Was wird gesichert
Das Tool sichert die folgenden AD FS-Konfiguration
    
- AD FS-Konfigurationsdatenbank (SQL oder WID)
- Konfigurationsdatei (befindet sich im AD FS-Ordner)
- Automatisch generierte token signieren und Entschlüsseln von Zertifikaten und privaten Schlüssel (aus dem Active Directory-DKM-Container)
- SSL-Zertifikat sowie alle extern registrierte Zertifikate (Tokensignatur-, tokenentschlüsselungs- und die Kommunikation zwischen der) und die zugehörigen privaten Schlüssel (Hinweis: private Schlüssel müssen exportierbar sein und der Benutzer die Ausführung des Skripts muss über Berechtigungen für den Zugriff)
- Eine Liste der benutzerdefinierten Authentifizierungsanbieter, Attributspeicher und lokalen Anspruchsanbieter-Vertrauensstellungen, die installiert werden.

## <a name="how-to-use-the-tool"></a>Zum Verwenden der Tools
Zuerst wird [herunterladen](https://go.microsoft.com/fwlink/?LinkId=825646) und installieren Sie die MSI-Datei mit dem AD FS-Server.  

>[!NOTE]
>Das AD FS schnelle-Restore-Tool ist nicht FIPS-konform.

Führen Sie eine PowerShell-Eingabeaufforderung den folgenden Befehl:

```powershell
import-module 'C:\Program Files (x86)\ADFS Rapid Recreation Tool\ADFSRapidRecreationTool.dll'
```

>[!NOTE] 
>Wenn Sie die integrierte Windows Database (WID) verwenden, muss dieses Tool auf dem primären AD FS-Server ausgeführt werden soll.  Sie können die `Get-SyncProperties` PowerShell-Cmdlet, um zu bestimmen, ob der Server Sie auf sind, ist der primäre Server.

### <a name="system-requirements"></a>Systemanforderungen

- Dieses Tool kann für AD FS unter Windows Server 2012 R2 und höher. 
- Die erforderliche .NET Framework ist mindestens 4.0. 
- Die Wiederherstellung auf einem AD FS-Server die gleiche Version wie der Sicherung vorgenommen werden, und der gleiche Active Directory-Konto als AD FS-Dienstkonto verwendet.

## <a name="create-a-backup"></a>Erstellen Sie eine Sicherung
Um eine Sicherung erstellen, verwenden Sie das Cmdlet "Backup-AD FS". Dieses Cmdlet sichert die AD FS-Konfiguration, die Datenbank, die SSL-Zertifikate, die usw. ab. 

Der Benutzer muss über mindestens einen lokalen Administrator dieses Cmdlet ausgeführt werden. Zum Sichern des DKM für Active Directory-Containers (in der standardmäßigen AD FS-Konfiguration erforderlich) der Benutzer muss auch die Domänen-Admins sein, oder die Anmeldeinformationen des AD FS-Dienstkontos übergeben muss.

Die Sicherung wird nach dem Muster "AdfsBackup_ID_Date Time" benannt werden. Es enthält die Versionsnummer, Datum und Uhrzeit, zu der die Sicherung beendet wurde.
Das Cmdlet verwendet die folgenden Parameter:
    
Parametersätze

![AD FS: Schnelles Wiederherstellungstool](media/AD-FS-Rapid-Restore-Tool/parameter1.png)

### <a name="detailed-description"></a>Detaillierte Beschreibung

- **BackupDKM** -sichert die DKM für Active Directory-Container, der die AD FS-Schlüssel in der Standardkonfiguration (automatisch generierte Token, Signieren und Entschlüsseln von Zertifikaten) enthält. Hier wird ein AD-Tool "Ldifde", um der Active Directory-Container und alle seine Unterstrukturen exportieren.

- -**StorageType &lt;Zeichenfolge&gt; ** -den Typ des Speichers, die die Benutzer verwenden möchte. "FileSystem" gibt an, dass der Benutzer in einem Ordner lokal oder im Netzwerk "Azure" gibt an, den der Benutzer möchte in der Azure Storage-Container zu speichern, wenn der Benutzer die Sicherung ausführt, wählen Sie den Sicherungsspeicherort an, das Dateisystem oder in der Cloud speichern möchte. Für Azure verwendet werden sollten die Azure Storage-Anmeldeinformationen an das Cmdlet übergeben werden. Die Speicher-Anmeldeinformationen enthält den Namen und den Schlüssel. Darüber hinaus muss ein Container auch in übergeben werden. Wenn der Container nicht vorhanden ist, wird sie während der Sicherung erstellt. Für das Dateisystem verwendet werden muss ein Speicherpfad gewährt werden. In diesem Verzeichnis wird ein neues Verzeichnis für jede Sicherung erstellt. Jedes Verzeichnis erstellt haben, wird die gesicherten Dateien enthalten. 

- **Verschlüsselungskennwort &lt;Zeichenfolge&gt; ** -das Kennwort, die verwendet werden, um alle gesicherten Dateien zu verschlüsseln, bevor diese gespeichert werden

- **AzureConnectionCredentials &lt;Pscredential&gt; ** -Kontoname und Schlüssel für die Azure-Speicherkonto

- **AzureStorageContainer &lt;Zeichenfolge&gt; ** -Speichercontainer, in dem die Sicherung in Azure gespeichert,

- **StoragePath &lt;Zeichenfolge&gt; ** -Speicherort Sicherungen gespeichert werden soll

- **ServiceAccountCredential &lt;Pscredential&gt; ** -gibt an, das Dienstkonto für den AD FS-Dienst, der derzeit verwendet wird. Dieser Parameter ist nur erforderlich, wenn der Benutzer die DKM sichern möchten, und ist nicht Domain-Admin.

- **BackupComment &lt;string []&gt; ** -eine informative Zeichenfolge über die Sicherung, die während der Wiederherstellung, ähnelt dem Konzept für die Benennung von Hyper-V-Prüfpunkt angezeigt werden. Der Standardwert ist eine leere Zeichenfolge

 
## <a name="backup-examples"></a>Beispiele für die Sicherung
Im folgenden finden Backup Beispiele für die Verwendung von AD FS schnelle Wiederherstellung des.

### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-while-running-as-the-domain-admin"></a>Sichern der AD FS-Konfiguration mit der DKM, auf das Dateisystem, während der Ausführung als den Domänen-Admins

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM
```
 
### <a name="backup-the-ad-fs-configuration-with-the-dkm-to-the-file-system-with-the-service-account-credential-running-as-local-admin"></a>Sicherung der AD FS-Konfiguration mit der DKM, auf das Dateisystem mit dem Konto Dienstanmeldeinformationen als lokaler Administrator ausgeführt

```powershell
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)" -BackupDKM -ServiceAccountCredential $cred
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-azure-storage-container"></a>Sichern Sie die AD FS-Konfiguration, ohne die DKM auf den Azure-Speicher-Container.

```powershell
Backup-ADFS -StorageType "Azure" -AzureConnectionCredentials $cred -AzureStorageContainer "adfsbackups"  -EncryptionPassword "password" -BackupComment "Clean Install of ADFS"
```

### <a name="backup-the-ad-fs-configuration-without-the-dkm-to-the-file-system"></a>Sichern der AD FS-Konfiguration, ohne die DKM auf das Dateisystem

```powershell   
Backup-ADFS -StorageType "FileSystem" -StoragePath "C:\Users\administrator\testExport\" -EncryptionPassword "password" -BackupComment "Clean Install of ADFS (FS)"
```

## <a name="restore-from-backup"></a>Wiederherstellen aus einer Sicherung
Verwenden Sie zum Anwenden einer Konfigurations mit Sicherung ADFS zu einer neuen AD FS-Installation erstellt das Restore-AD FS-Cmdlet.

Dieses Cmdlet erstellt eine neue AD FS-Farm mithilfe des Cmdlets `Install-AdfsFarm` und AD FS-Konfiguration, Datenbank, Zertifikate usw. wiederhergestellt. Wenn der AD FS-Serverrolle nicht auf dem Server installiert wurde, wird das Cmdlet installiert.  Das Cmdlet überprüft den Speicherort für die Wiederherstellung für die vorhandenen Sicherungen und fordert den Benutzer zum Auswählen einer geeigneten Sicherung basierend auf Datum und Uhrzeit der Aufnahme und Sicherung Kommentar, den der Benutzer auf die Sicherung angeschlossen haben möglicherweise. Wenn mehrere AD FS-Konfigurationen mit verschiedenen Federation Service Namen vorhanden sind, wird der Benutzer aufgefordert, zunächst die entsprechenden AD FS-Konfiguration auswählen.
Der Benutzer hat, sowohl lokal als auch der Administrator dieses Cmdlet ausführen.


>[!NOTE] 
>Vor der Verwendung von AD FS schnelle Recovery Tool, stellen Sie sicher, dass die Server der Domäne vor dem Wiederherstellen der Sicherung angehört. 

Das Cmdlet verwendet die folgenden Parameter: 

![AD FS: Schnelles Wiederherstellungstool](media/AD-FS-Rapid-Restore-Tool/parameter2.png)

### <a name="detailed-description"></a>Detaillierte Beschreibung

- **StorageType &lt;Zeichenfolge&gt; ** -den Typ des Speichers, die die Benutzer verwenden möchte.
 "FileSystem" weist darauf hin, dass der Benutzer es in einem Ordner lokal speichern möchte oder im Netzwerk "Azure" gibt an, dass der Benutzer in der Azure Storage-Container speichern möchte

- **DecryptionPassword &lt;Zeichenfolge&gt; ** -das Kennwort, das verwendet wurde, um alle gesicherten Dateien zu verschlüsseln. 

- **AzureConnectionCredentials &lt;Pscredential&gt; ** -Kontoname und Schlüssel für die Azure-Speicherkonto

- **AzureStorageContainer &lt;Zeichenfolge&gt; ** -Speichercontainer, in dem die Sicherung in Azure gespeichert,

- **StoragePath &lt;Zeichenfolge&gt; ** -Speicherort Sicherungen gespeichert werden soll

- **ADFSName &lt; Zeichenfolge &gt; ** -der Name des Verbunddiensts, die gesichert und wiederhergestellt werden soll. Wenn dies nicht angegeben wird, und gibt es wird nur ein verbunddienstname und klicken Sie dann, verwendet werden. Befindet sich mehr als ein Verbunddienst zu dem Speicherort gesichert, und der Benutzer wird aufgefordert, einen gesicherten Verbunddienste auswählen.

- **ServiceAccountCredential &lt; Pscredential &gt; ** -gibt an, das Dienstkonto, das für den neuen AD FS-Dienst wiederhergestellten verwendet wird 

- **GroupServiceAccountIdentifier &lt;Zeichenfolge&gt; ** -der GMSA, die der Benutzer möchte, verwenden Sie für den neuen AD FS-Dienst wiederhergestellt wird. Standardmäßig Wenn weder die gesicherten angegeben ist wird Kontonamen verwendet, wenn GMSA, andere der Benutzer aufgefordert wird war, setzen Sie in ein Dienstkonto

- **DBConnectionString &lt;Zeichenfolge&gt; ** – Wenn der Benutzer eine andere Datenbank für die Wiederherstellung verwenden möchten und klicken Sie dann die SQL-Verbindungszeichenfolge oder der Typ in der internen Windows-Datenbank für Ihre übergeben sie sollten

- **Force &lt;Bool&gt; ** -überspringen Sie die Anweisungen, die das Tool ggf., nachdem die Sicherung ausgewählt ist

- **RestoreDKM &lt;Bool&gt; ** - Wiederherstellen der DKM-Container mit der AD, sollte festgelegt werden, wenn auf eine neue Anzeige und die DKM anfänglich gesichert wurde.

## <a name="restore-examples"></a>Beispiele für die Wiederherstellung

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-azure-storage-container"></a>Wiederherstellen von AD FS-Konfiguration, ohne die DKM aus dem Azure-Speicher-Container

```powershell
Restore-ADFS -StorageType "Azure" -AzureConnectionCredential $cred -DecryptionPassword "password" -AzureStorageContainer "adfsbackups"
```

### <a name="restore-the-ad-fs-configuration-without-the-dkm-from-the-file-system"></a>Wiederherstellen von AD FS-Konfiguration, ohne die DKM aus dem Dateisystem
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password"
```

### <a name="restore-the-ad-fs-configuration-with-the-dkm-to-the-file-system"></a>Wiederherstellen von AD FS-Konfiguration mit den DKM auf das Dateisystem 
 
```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -RestoreDKM
```

### <a name="restore-the-ad-fs-configuration-to-wid"></a>Die AD FS-Konfiguration WID wiederherstellen

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "WID"
``` 

### <a name="restore-the-ad-fs-configuration-to-sql"></a>Wiederherstellen von AD FS-Konfiguration zu SQL

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -DBConnectionString "Data Source=TESTMACHINE\SQLEXPRESS; Integrated Security=True"
```

### <a name="restores-the-ad-fs-configuration-with-the-specified-gmsa"></a>Der AD FS-Konfiguration mit den angegebenen GMSA wiederhergestellt

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -GroupServiceAccountIdentifier "mangupd1\adfsgmsa$"
```
### <a name="restore-the-ad-fs-configuration-with-the-specified-service-account-creds"></a>Wiederherstellen von AD FS-Konfiguration mit den angegebenen Dienst Konto-Anmeldeinformationen

```powershell
Restore-ADFS -StorageType "FileSystem" -StoragePath "C:\uSERS\administrator\testExport\" -DecryptionPassword "password" -ServiceAccountCredential $cred
```

## <a name="encryption-information"></a>Von Verschlüsselungsinformationen
Alle backup Daten werden verschlüsselt, bevor Sie in die Cloud verschieben oder speichern es im Dateisystem.  

Jedes Dokument, das erstellt wird, als Teil der Sicherung verschlüsselt ist mit AES-256. Das Kennwort in das Tool übergeben wird als eine Passphrase verwendet, um ein neues Kennwort ein, die mit der Klasse Rfc2898DeriveBytes zu generieren. 

RngCryptoServiceProvider wird verwendet, um anhand der Algorithmen AES und die Klasse Rfc2898DeriveBytes Meerwasser zu generieren. 

## <a name="log-files"></a>Protokolldateien
Jedes Mal, wenn eine Sicherung oder Wiederherstellung ausgeführt wird, wird eine Protokolldatei erstellt. Diese finden Sie unter folgendem Speicherort:

- **%LocalAppData%\ADFSRapidRecreationTool**

>[!NOTE]
> Wenn Attribut mit dem Wiederherstellungsvorgang, die eine PostRestore_Instructions-Datei erstellt werden kann, enthält eine Übersicht über die zusätzliche Authentifizierungsanbieter, gespeichert werden. und lokalen Anspruchsanbieter-Vertrauensstellungen, manuell installiert werden, bevor der AD FS-Dienst wird gestartet.
