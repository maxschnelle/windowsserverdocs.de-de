---
title: Erkennen, aktivieren und Deaktivieren von SMBv1, SMBv2 und SMBv3 in Windows
description: Beschreibt das Aktivieren und Deaktivieren des Server Message Block-Protokolls (SMBv1, SMBv2 und SMBv3) in Windows-Client-und-Server Umgebungen.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 40ab29a115735e6c37bb7c7449980b94090565f3
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961072"
---
# <a name="how-to-detect-enable-and-disable-smbv1-smbv2-and-smbv3-in-windows"></a>Erkennen, aktivieren und Deaktivieren von SMBv1, SMBv2 und SMBv3 in Windows

## <a name="summary"></a>Zusammenfassung

In diesem Artikel wird beschrieben, wie Sie Server Message Block (SMB) Version 1 (SMBv1), SMB Version 2 (SMBv2) und SMB Version 3 (SMBv3) auf den SMB-Client-und-Server Komponenten aktivieren und deaktivieren. 

> [!IMPORTANT]
> Es wird empfohlen, SMBv2 oder SMBv3 **nicht** zu deaktivieren. Deaktivieren Sie SMBv2 oder SMBv3 nur als temporäres Problem Behandlungs Measure. Lassen Sie SMBv2 oder SMBv3 nicht deaktiviert.  

In Windows 7 und Windows Server 2008 R2 werden bei der Deaktivierung von SMBv2 die folgenden Funktionen deaktiviert: 
 
- Anfordern von Anforderungen: ermöglicht das Senden mehrerer SMB 2-Anforderungen als einzelne Netzwerk Anforderung.    
- Größere Lese-und Schreibvorgänge-bessere Verwendung schnellerer Netzwerke    
- Zwischenspeichern von Ordner-und Dateieigenschaften-Clients behalten lokale Kopien von Ordnern und Dateien bei    
- Dauerhafte Handles: ermöglichen der Verbindung, um eine transparente Verbindung mit dem Server herzustellen, wenn eine temporäre Trennung vorliegt    
- Verbesserte Nachrichten Signierung: HMAC SHA-256 ersetzt MD5 als Hash Algorithmus.    
- Verbesserte Skalierbarkeit für die Dateifreigabe: die Anzahl von Benutzern, Freigaben und geöffneten Dateien pro Server wurde erheblich erhöht.    
- Unterstützung für symbolische Verknüpfungen    
- Client-Oplock-Leasingmodell: schränkt die zwischen Client und Server übertragenen Daten ein, verbessert die Leistung bei Netzwerken mit hoher Latenz und erhöht die Skalierbarkeit von SMB-Servern.    
- Unterstützung großer MTU-für die vollständige Nutzung von 10-gigabye (GB) Ethernet    
- Verbesserte Energieeffizienz: Clients mit geöffneten Dateien auf einem Server können in den Standbymodus wechseln.    

In Windows 8, Windows 8.1, Windows 10, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 deaktiviert die Deaktivierung von SMBv3 die folgende Funktionalität (und außerdem die SMBv2-Funktionalität, die in der vorherigen Liste beschrieben wird): 
 
- Transparentes Failover: Clients stellen während Wartung oder Failover keine Unterbrechung der Cluster Knoten wieder her.    
- Scale Out – gleichzeitigen Zugriff auf freigegebene Daten auf allen Datei Cluster Knoten     
- Multichannel-Aggregation der Netzwerkbandbreite und Fehlertoleranz, wenn mehrere Pfade zwischen Client und Server verfügbar sind  
- SMB Direct – bietet RDMA-Netzwerkunterstützung für eine sehr hohe Leistung mit geringer Latenz und geringer CPU-Auslastung.    
- Verschlüsselung – bietet eine End-to-End-Verschlüsselung und schützt vor dem eavesdrop in nicht vertrauenswürdigen Netzwerken.    
- Verzeichnis Leasing: verbessert die Reaktionszeiten von Anwendungen in Zweigstellen durch Caching    
- Leistungsoptimierungen-Optimierungen für kleine zufällige e/a-Vorgänge mit Lese-/Schreibzugriff

##  <a name="more-information"></a>Weitere Informationen

Das SMBv2-Protokoll wurde in Windows Vista und Windows Server 2008 eingeführt.

Das SMBv3-Protokoll wurde in Windows 8 und Windows Server 2012 eingeführt.

Weitere Informationen zu den Funktionen der SMBv2-und SMBv3-Funktionen finden Sie in den folgenden Artikeln:

[Server Message Block (Übersicht)](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/hh831795(v=ws.11))

[Neues in SMB](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/ff625695(v=ws.10))  

## <a name="how-to-gracefully-remove-smb-v1-in-windows-81-windows-10-windows-2012-r2-windows-server-2016-and-windows-server-2019"></a>Vorgehensweise zum ordnungsgemäßen Entfernen von SMB V1 in Windows 8.1, Windows 10, Windows 2012 R2, Windows Server 2016 und Windows Server 2019

#### <a name="powershell-methods"></a>PowerShell-Methoden

##### <a name="smb-v1-client-and-server"></a>SMB v1 (Client und Server)

- Auf 

  ```PowerShell
  Get-WindowsFeature FS-SMB1
  ```

- Ier 

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

- Aktivieren Sie: 

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName smb1protocol
  ```

#### <a name="windows-server-2012-r2-windows-server-2016-windows-server-2019-server-manager-method-for-disabling-smb"></a>Windows Server 2012 R2, Windows Server 2016, Windows Server 2019: Server-Manager Methode zum Deaktivieren von SMB

##### <a name="smb-v1"></a>SMB v1

![Server-Manager-Dashboard-Methode](media/detect-enable-and-disable-smbv1-v2-v3-1.png)

#### <a name="windows-81-and-windows-10-powershell-method"></a>Windows 8.1 und Windows 10: PowerShell-Methode

##### <a name="smb-v1-protocol"></a>SMB v1-Protokoll

- Auf 
  
  ```PowerShell
  Get-WindowsOptionalFeature –Online –FeatureName SMB1Protocol
  ```

- Ier 

  ```PowerShell
  Disable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

- Aktivieren Sie: 

  ```PowerShell
  Enable-WindowsOptionalFeature -Online -FeatureName SMB1Protocol
  ```

##### <a name="smb-v2v3protocol-only-disables-smb-v2v3-server"></a>SMB v2/v3-Protokoll (nur der SMB v2/v3-Server wird deaktiviert)

- Auf 
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- Ier 
  
  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $false
  ```

- Aktivieren Sie:

  ```PowerShell
  Set-SmbServerConfiguration –EnableSMB2Protocol $true
  ```

#### <a name="windows-81-and-windows-10-add-or-remove-programs-method"></a>Windows 8.1 und Windows 10: Methode zum Hinzufügen oder Entfernen von Programmen

![Client Methode zum Hinzufügen und Entfernen von Programmen](media/detect-enable-and-disable-smbv1-v2-v3-2.png)

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-server"></a>Erkennen von Status, aktivieren und Deaktivieren von SMB-Protokollen auf dem SMB-Server

### <a name="for-windows-8-and-windows-server-2012"></a>Für Windows 8 und Windows Server 2012

Mit Windows 8 und Windows Server 2012 wird das neue Windows PowerShell-Cmdlet " **Set-smbserverconfiguration** " eingeführt. Mit dem-Cmdlet können Sie die SMBv1-, SMBv2-und SMBv3-Protokolle für die Serverkomponente aktivieren bzw. deaktivieren.  

> [!NOTE]   
> Wenn Sie SMBv2 in Windows 8 oder Windows Server 2012 aktivieren oder deaktivieren, ist SMBv3 ebenfalls aktiviert oder deaktiviert. Dieses Verhalten tritt auf, weil diese Protokolle denselben Stapel gemeinsam verwenden.     

Sie müssen den Computer nach dem Ausführen des Cmdlets " **Set-smbserverconfiguration** " nicht neu starten. 

##### <a name="smb-v1-on-smb-server"></a>SMB v1 auf SMB-Server

- Auf 
  
  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB1Protocol
  ```

- Ier 

  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $false
  ```

- Aktivieren Sie: 
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB1Protocol $true
  ```

Weitere Informationen finden Sie unter [Server Speicher bei Microsoft](https://techcommunity.microsoft.com/t5/Storage-at-Microsoft/Stop-using-SMB1/ba-p/425858). 
##### <a name="smb-v2v3-on-smb-server"></a>SMB v2/v3 auf dem SMB-Server

- Auf

  ```PowerShell
  Get-SmbServerConfiguration | Select EnableSMB2Protocol
  ```

- Ier 
  
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $false
  ```

- Aktivieren Sie:
  
  ```PowerShell
  Set-SmbServerConfiguration -EnableSMB2Protocol $true
  ```

### <a name="for-windows-7-windows-server-2008-r2-windows-vista-and-windows-server-2008"></a>Für Windows 7, Windows Server 2008 R2, Windows Vista und Windows Server 2008

Zum Aktivieren oder Deaktivieren von SMB-Protokollen auf einem SMB-Server, auf dem Windows 7, Windows Server 2008 R2, Windows Vista oder Windows Server 2008 ausgeführt wird, verwenden Sie Windows PowerShell oder den Registrierungs-Editor. 

#### <a name="powershell-methods"></a>PowerShell-Methoden

> [!NOTE]
> Diese Methode erfordert PowerShell 2,0 oder eine höhere Version von PowerShell.

##### <a name="smb-v1-on-smb-server"></a>SMB v1 auf SMB-Server

Auf

```PowerShell
Get-Item HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath}
```

Standardkonfiguration = aktiviert (es wurde kein Registrierungsschlüssel erstellt), daher wird kein Server Message Block-Wert zurückgegeben.

Ier

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 0 –Force
```

Aktivieren Sie:  

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB1 -Type DWORD -Value 1 –Force
```  

**Hinweis** Sie müssen den Computer neu starten, nachdem Sie diese Änderungen vorgenommen haben. Weitere Informationen finden Sie unter [Server Speicher bei Microsoft](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858). 
##### <a name="smb-v2v3-on-smb-server"></a>SMB v2/v3 auf dem SMB-Server

Auf  

```PowerShell
Get-ItemProperty HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters | ForEach-Object {Get-ItemProperty $_.pspath} 
```

Ier

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 0 –Force  
```

Aktivieren Sie:

```PowerShell
Set-ItemProperty -Path "HKLM:\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters" SMB2 -Type DWORD -Value 1 –Force 
```

> [!NOTE]
> Sie müssen den Computer neu starten, nachdem Sie diese Änderungen vorgenommen haben. 

#### <a name="registry-editor"></a>Registrierungs-Editor

> [!IMPORTANT]
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/help/322756) für den Fall, dass Probleme auftreten.
 
Um SMBv1 auf dem SMB-Server zu aktivieren oder zu deaktivieren, konfigurieren Sie den folgenden Registrierungsschlüssel:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB1
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created)
```

Um SMBv2 auf dem SMB-Server zu aktivieren oder zu deaktivieren, konfigurieren Sie den folgenden Registrierungsschlüssel: 

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters**

```
Registry entry: SMB2
REG_DWORD: 0 = Disabled
REG_DWORD: 1 = Enabled
Default: 1 = Enabled (No registry key is created) 
```

> [!NOTE]
> Sie müssen den Computer neu starten, nachdem Sie diese Änderungen vorgenommen haben. 

## <a name="how-to-detect-status-enable-and-disable-smb-protocols-on-the-smb-client"></a>Erkennen von Status, aktivieren und Deaktivieren von SMB-Protokollen auf dem SMB-Client

### <a name="for-windows-vista-windows-server-2008-windows-7-windows-server-2008-r2-windows-8-and-windows-server-2012"></a>Für Windows Vista, Windows Server 2008, Windows 7, Windows Server 2008 R2, Windows 8 und Windows Server 2012

> [!NOTE]
> Wenn Sie SMBv2 in Windows 8 oder Windows Server 2012 aktivieren oder deaktivieren, ist SMBv3 ebenfalls aktiviert oder deaktiviert. Dieses Verhalten tritt auf, weil diese Protokolle denselben Stapel gemeinsam verwenden. 

##### <a name="smb-v1-on-smb-client"></a>SMB v1 auf dem SMB-Client

- Detect
  
  ```cmd
  sc.exe qc lanmanworkstation
  ```

- Ier
  
  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= disabled
  ```

- Aktivieren Sie:

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb10 start= auto
  ```

Weitere Informationen finden Sie unter [Server Speicher bei Microsoft](https://techcommunity.microsoft.com/t5/storage-at-microsoft/stop-using-smb1/ba-p/425858) . 
##### <a name="smb-v2v3-on-smb-client"></a>SMB v2/v3 auf dem SMB-Client

- Auf

  ```cmd
  sc.exe qc lanmanworkstation
  ```

- Ier

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/nsi
  sc.exe config mrxsmb20 start= disabled 
  ```

- Aktivieren Sie:

  ```cmd
  sc.exe config lanmanworkstation depend= bowser/mrxsmb10/mrxsmb20/nsi
  sc.exe config mrxsmb20 start= auto
  ```

> [!NOTE]
> - Sie müssen diese Befehle an einer Eingabeaufforderung mit erhöhten Rechten ausführen.    
> - Sie müssen den Computer neu starten, nachdem Sie diese Änderungen vorgenommen haben.    
 

## <a name="disable-smbv1-server-with-group-policy"></a>SMBv1-Server mit Gruppenrichtlinie deaktivieren

Mit diesem Verfahren wird das folgende neue Element in der Registrierung konfiguriert:

**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\LanmanServer\Parameters** 

- Registrierungs Eintrag: **Server Message Block** 
- REG_DWORD: **0** = deaktiviert   

Führen Sie die folgenden Schritte aus, um dies mithilfe Gruppenrichtlinie zu konfigurieren:
 
1. Öffnen Sie die **Gruppenrichtlinien-Verwaltungskonsole**. Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt (GPO, Group Policy Object), das das neue Einstellungselement enthalten soll, und klicken Sie dann auf **Bearbeiten**.

2. Erweitern Sie in der Konsolen **Struktur unter Computer Konfiguration**den Ordner **Einstellungen** , und erweitern Sie dann den Ordner **Windows-Einstellungen** .

3. Klicken Sie mit der rechten Maustaste auf den Knoten **Registrierung**, zeigen Sie auf **Neu**, und wählen Sie **Registrierungselement**.

   ![Registrierung-neues Registrierungs Element](media/detect-enable-and-disable-smbv1-v2-v3-3.png)    
 
Wählen Sie im Dialogfeld **neue Registrierungs Eigenschaften**Folgendes aus: 
 
- **Aktion**: Erstellen    
- **Hive**: HKEY_LOCAL_MACHINE    
- **Schlüssel Pfad**: system\currentcontrolset\services\lanmanserver\parameters    
- **Wertname**: Server Message Block    
- **Werttyp**: REG_DWORD    
- **Wertdaten**: 0    
 
![Neue Registrierungs Eigenschaften: Allgemein](media/detect-enable-and-disable-smbv1-v2-v3-4.png)

Dadurch werden die SMBv1-Server Komponenten deaktiviert. Diese Gruppenrichtlinie muss auf alle erforderlichen Arbeitsstationen, Server und Domänen Controller in der Domäne angewendet werden.

> [!NOTE]
> [WMI-Filter](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc947846(v=ws.10)) können auch so festgelegt werden, dass nicht unterstützte Betriebssysteme oder ausgewählte Ausschlüsse wie Windows XP ausgeschlossen werden.

> [!IMPORTANT]
> Gehen Sie vorsichtig vor, wenn Sie diese Änderungen auf Domänen Controllern durchführen, auf denen ältere Windows XP-oder ältere Linux-und Drittanbieter Systeme (die SMBv2 oder SMBv3 nicht unterstützen) Zugriff auf SYSVOL oder andere Dateifreigaben benötigen, in denen SMB v1 deaktiviert wird.     

## <a name="disable-smbv1-client-with-group-policy"></a>SMBv1-Client mit Gruppenrichtlinie deaktivieren

Um den SMBv1-Client zu deaktivieren, muss der Registrierungsschlüssel der Dienste aktualisiert werden, um den Start von **MRxSMB10** zu deaktivieren. Anschließend muss die Abhängigkeit von **MRxSMB10** aus dem Eintrag für " **LanmanWorkstation** " entfernt werden, sodass er normal gestartet werden kann, ohne dass **MRxSMB10** zum ersten Mal gestartet werden muss.

Dadurch werden die Standardwerte in den folgenden 2 Elementen in der Registrierung aktualisiert und ersetzt: 

**HKEY_LOCAL_MACHINE \system\currentcontrolset\services\mrxsmb10** 

Registrierungs Eintrag: **Start** REG_DWORD: **4**= deaktiviert

**HKEY_LOCAL_MACHINE \system\currentcontrolset\services\lanmanworkstation** 

Registrierungs Eintrag: **DependOnService** REG_MULTI_SZ: **"Bowser", "MRxSmb20", "NSI"**   

> [!NOTE]
> Der Standard MRxSMB10, der nun als Abhängigkeit entfernt wurde.

Führen Sie die folgenden Schritte aus, um dies mithilfe Gruppenrichtlinie zu konfigurieren:
 
1. Öffnen Sie die **Gruppenrichtlinien-Verwaltungskonsole**. Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt (GPO, Group Policy Object), das das neue Einstellungselement enthalten soll, und klicken Sie dann auf **Bearbeiten**.

2. Erweitern Sie in der Konsolen **Struktur unter Computer Konfiguration**den Ordner **Einstellungen** , und erweitern Sie dann den Ordner **Windows-Einstellungen** .

3. Klicken Sie mit der rechten Maustaste auf den Knoten **Registrierung**, zeigen Sie auf **Neu**, und wählen Sie **Registrierungselement**.    

4. Wählen Sie im Dialogfeld **neue Registrierungs Eigenschaften** Folgendes aus: 
 
   - **Aktion**: Aktualisieren
   - **Hive**: HKEY_LOCAL_MACHINE
   - **Schlüssel Pfad**: system\currentcontrolset\services\mrxsmb10
   - **Wertname**: Start
   - **Werttyp**: REG_DWORD
   - **Wertdaten**: 4
 
   ![Start Eigenschaften: Allgemein](media/detect-enable-and-disable-smbv1-v2-v3-5.png)

5. Entfernen Sie dann die Abhängigkeit von der **MRxSMB10** , die gerade deaktiviert wurde.

   Wählen Sie im Dialogfeld **neue Registrierungs Eigenschaften** Folgendes aus: 
 
   - **Aktion**: ersetzen
   - **Hive**: HKEY_LOCAL_MACHINE
   - **Schlüssel Pfad**: system\currentcontrolset\services\lanmanworkstation
   - **Wertname**: DependOnService
   - **Werttyp**: REG_MULTI_SZ 
   - **Wertdaten**:
      - Bowsermodus
      - MRxSmb20
      - NSI
 
   > [!NOTE]
   > Diese drei Zeichen folgen enthalten keine Aufzählungs Zeichen (siehe den folgenden Screenshot).

   ![DependOnService-Eigenschaften](media/detect-enable-and-disable-smbv1-v2-v3-6.png) 

   Der Standardwert umfasst **MRxSMB10** in vielen Versionen von Windows. Wenn Sie diese also durch diese mehrwertige Zeichenfolge ersetzen, wird **MRxSMB10** als Abhängigkeit für **LanmanServer** entfernt, und von vier Standardwerten bis zu diesen drei Werten weiter oben.

   > [!NOTE]
   > Wenn Sie Gruppenrichtlinien-Verwaltungskonsole verwenden, müssen Sie keine Anführungszeichen oder Kommas verwenden. Geben Sie einfach jeden Eintrag in einzelne Zeilen ein.

6. Starten Sie die Zielsysteme neu, um die Deaktivierung von SMB v1 abzuschließen.

### <a name="summary"></a>Zusammenfassung

Wenn sich alle Einstellungen im gleichen Gruppenrichtlinie Objekt (GPO) befinden, zeigt Gruppenrichtlinie Verwaltung die folgenden Einstellungen an.

![Gruppenrichtlinienverwaltungs-Editor Registrierung](media/detect-enable-and-disable-smbv1-v2-v3-7.png) 

### <a name="testing-and-validation"></a>Tests und Validierung

Nachdem diese konfiguriert wurden, können Sie die Richtlinie replizieren und aktualisieren. Führen Sie **gpupdate/force** an der Eingabeaufforderung aus, und überprüfen Sie dann die Zielcomputer, um sicherzustellen, dass die Registrierungs Einstellungen ordnungsgemäß angewendet werden. Stellen Sie sicher, dass SMB v2 und SMB V3 für alle anderen Systeme in der Umgebung funktionieren.

> [!NOTE]
> Vergessen Sie nicht, die Zielsysteme neu zu starten.
