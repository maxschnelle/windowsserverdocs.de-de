---
title: Bereitstellen von Speicherplätzen auf einem eigenständigen server
description: Beschreibt, wie zum Bereitstellen von Speicherplätzen auf einem eigenständigen Windows Server 2012-basierte Server.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-spaces
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: f9b5d2b0d5acfcbde52131c29704e38d835d048e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66447553"
---
# <a name="deploy-storage-spaces-on-a-stand-alone-server"></a>Bereitstellen von Speicherplätzen auf einem eigenständigen server

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird beschrieben, wie Speicherplätze auf einem eigenständigen Server bereitgestellt. Informationen zum Erstellen eines clusterspeicherplatzes finden Sie unter [stellen einen Speicherplätze-Cluster in Windows Server 2012 R2](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>).

Um einen Speicherplatz zu erstellen, müssen Sie zuerst einen oder mehrere Speicherpools erstellen. Ein Speicherpool ist eine Gruppe physischer Datenträger. Speicherpools ermöglichen eine Speicheraggregation, eine flexible Kapazitätserweiterung und eine delegierte Verwaltung.

Aus einem Speicherpool können Sie einzelne oder mehrere virtuelle Datenträger erstellen. Diese virtuellen Datenträger werden auch als *Speicherplätze* bezeichnet. Ein Speicherplatz wird vom Windows-Betriebssystem als ein normaler Datenträger angesehen, von dem Sie formatierte Volumes erstellen können. Wenn Sie einen virtuellen Datenträger über die Benutzeroberfläche "Datei- und Speicherdienste" erstellen, können Sie den Resilienztyp (einfach, Spiegeln oder Parität), den Bereitstellungstyp (schlank oder fest) und die Größe konfigurieren. Über Windows PowerShell können Sie zusätzliche Parameter, wie die Anzahl der Spalten, den Überlappungswert und die im Pool zu verwendenden physischen Datenträger festlegen. Informationen zu diesen zusätzlichen Parametern finden Sie unter [New-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/new-virtualdisk?view=win10-ps) und [Was sind Spalten und wie Storage Spaces entscheiden, wie viele verwenden?](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx%23what_are_columns_and_how_does_storage_spaces_decide_how_many_to_use) in Storage Spaces häufig gestellte Fragen (FAQ).

>[!NOTE]
>Sie können keinen Speicherplatz zum Hosten des Windows-Betriebssystems verwenden.

Von einem virtuellen Datenträger können Sie einzelne oder mehrere Volumes erstellen. Wenn Sie ein Volume erstellen, können Sie die Größe, Laufwerkbuchstaben oder Ordner, Dateisystem (NTFS-Dateisystem oder Resilient File System (ReFS)), Größe der Zuordnungseinheit und eine optionale Volumebezeichnung konfigurieren.

In der folgenden Abbildung ist der Speicherplatz-Workflow dargestellt.

![Speicherplätze – Workflow](media/deploy-standalone-storage-spaces/storage-spaces-workflow.png)

**Abbildung 1: Speicherplätze-workflow**

>[!NOTE]
>Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6).

## <a name="prerequisites"></a>Vorraussetzungen

Wenn Speicherplätze auf einem eigenständigen Windows Server-2012−based-Server verwenden möchten, stellen Sie sicher, dass die physischen Datenträger, die Sie verwenden möchten, die folgenden Voraussetzungen erfüllen.

> [!IMPORTANT]
> Wenn Sie möchten erfahren Sie, wie zum Bereitstellen von Speicherplätzen auf einem Failovercluster finden Sie unter [stellen einen Speicherplätze-Cluster in Windows Server 2012 R2](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>). Bereitstellung auf einem Failovercluster verfügt über unterschiedliche Voraussetzungen, z. B. die unterstützten datenträgerbustypen, unterstützten resilienztypen und die erforderliche Mindestanzahl von Datenträgern.

|Bereich|Anforderung|Hinweise|
|---|---|---|
|Datenträgerbustypen|-Serial Attached SCSI (SAS)<br>-Serial Advanced Technology Attachment (SATA)<br>-iSCSI und Fibre Channel-Controller. |Sie können auch USB-Laufwerke verwenden. Es ist jedoch nicht optimal, USB-Laufwerke in einer serverumgebung zu verwenden.<br>Speicherplätze wird auf iSCSI und Fibre Channel (FC)-Controller unterstützt, solange der virtuelle Datenträger erstellt basierend auf diesen nicht stabil ist (einfach mit einer beliebigen Anzahl von Spalten).<br>|
|Datenträgerkonfiguration|– Physische Datenträger müssen über mindestens 4 GB sein.<br>– Datenträger müssen leer und unformatiert sein. Erstellen Sie keine Volumes||
|HBA-Überlegungen|-Einfache Hostbusadapter (HBAs), die keine RAID-Funktionalität unterstützen werden empfohlen.<br>– Wenn RAID-fähig ist, müssen HBAs im nicht-RAID-Modus mit allen RAID-Funktionalität deaktiviert sein<br>-Adapter müssen nicht abstrahiert die physischen Datenträger und Cachedaten oder angeschlossene Geräte überdecken. Dies gilt auch für Gehäusedienste, die von angeschlossenen JBOD-Geräten bereitgestellt werden. |Speicherplätze sind nur mit HBAs kompatibel, wenn Sie die gesamte RAID-Funktionalität vollständig deaktivieren können.|
|JBOD-Gehäuse|-JBOD-Gehäuse sind optional<br>-Empfohlen zertifiziert für die Verwendung von Speicherplätzen Gehäusen, die auf Windows Server-Katalog aufgelistet<br>– Wenn Sie einem JBOD-Gehäuse verwenden, vergewissern Sie sich mit Ihrem Speicherhersteller, dass das Gehäuse Speicherplätze, um sicherzustellen, dass vollständige Funktionalität unterstützt<br>– Um zu bestimmen, ob das JBOD-Gehäuse Gehäuse-und steckplatzidentifizierung unterstützt, führen Sie das folgende Windows PowerShell-Cmdlet aus:<br><br>`Get-PhysicalDisk \| ? {$_.BusType –eq "SAS"} \| fc`<br><br>Wenn die **EnclosureNumber** und **SlotNumber** Felder Werte enthalten, und klicken Sie dann das Gehäuse diese Funktionen unterstützt.||

Bei der Planung der Anzahl der physischen Datenträger und des gewünschten Resilienztyps für eine eigenständige Serverbereitstellung halten Sie sich an folgende Richtlinien.

|Resilienztyp|Datenträgeranforderungen|Verwendung|
|---|---|---|
|**Einfache**<br><br>-Verteilt Daten über mehrere physische Datenträger<br>-Maximiert die Datenträgerkapazität und erhöht den Durchsatz<br>– Keine resilienz (schützt nicht vor Datenträgerfehlern)<br><br><br><br><br><br><br>|Erfordert mindestens einen physischen Datenträger.|Nicht zum Hosten unersetzbarer Daten verwenden. Für einfache Speicherplätze schützen nicht vor Datenträgerfehlern.<br><br>Zum Hosten temporärer oder leicht wiederherstellbarer Daten zu reduzierten Kosten geeignet.<br><br>Geeignet für hochleistungsfähige Workloads, in denen resilienz ist nicht erforderlich, oder wird bereits von der Anwendung bereitgestellt.|
|**Spiegel**<br><br>– Speichert zwei oder drei Kopien der Daten über eine Gruppe von physischen Datenträgern<br>– Erhöht die Zuverlässigkeit, aber verringert die Kapazität. Bei jedem Schreibvorgang wird dupliziert. Außerdem verteilt ein Spiegelspeicherplatz die Daten über mehrere physische Datenträger.<br>-Größerer Datendurchsatz und geringere Zugriffslatenz als Parität<br>– Verwendet dirty Region tracking (DRT), um Änderungen an den Datenträgern im Pool nachzuverfolgen. Wenn das System ungeplant heruntergefahren wurde und dann den Betrieb wieder aufnimmt und die Speicherplätze wieder online geschaltet werden, stimmt DRT die Datenträger im Pool erneut aufeinander ab.|Erfordert mindestens zwei physische Datenträger, um vor dem Ausfall einzelner Datenträger geschützt zu sein.<br><br>Erfordert mindestens fünf physische Datenträger, um vor dem gleichzeitigen Ausfall zweier Datenträger geschützt zu sein.|Wird für die meisten Bereitstellungen verwendet. Spiegelspeicherplätze sind beispielsweise für eine allgemeine Dateifreigabe oder eine virtuelle Festplattenbibliothek (Virtual Hard Disk, VHD) geeignet.|
|**Parity**<br><br>-Verteilt Daten und Paritätsinformationen auf physische Datenträger<br>– Erhöht die Zuverlässigkeit im Vergleich zu einem einfachen Speicherplatz, sondern verringert die Kapazität geringfügig<br>– Erhöht die resilienz durch Journaling. Dadurch kann eine Beschädigung der Daten verhindert werden, wenn das System unplanmäßig heruntergefahren wird.|Erfordert mindestens drei physische Datenträger, um vor dem Ausfall einzelner Datenträger geschützt zu sein.|Geeignet für stark sequenzielle Arbeitsauslastungen, z. B. bei Archiven oder Backups.|

## <a name="step-1-create-a-storage-pool"></a>Schritt 1: Erstellen eines Speicherpools

Zuerst müssen Sie die verfügbaren physischen Datenträger in einzelne oder mehrere Speicherpools zusammenfassen.

1. Wählen Sie im Navigationsbereich des Server-Manager **Datei- und Speicherdienste**.

2. Wählen Sie im Navigationsbereich die **Speicherpools** Seite.
    
    Verfügbare Datenträger werden standardmäßig in einem *ursprünglichen* Pool eingefügt. Wenn unter **SPEICHERPOOLS** kein ursprünglicher Pool aufgeführt ist, bedeutet das, dass der Speicher die Anforderungen für Speicherplätze nicht erfüllt. Stellen Sie sicher, dass die Datenträger die Anforderungen erfüllen, die im Abschnitt "Voraussetzungen" erläutert sind.
    
    >[!TIP]
    >Wenn Sie den ursprünglichen Speicherpool (**Primordial**) auswählen, werden die verfügbaren physischen Datenträger unter **PHYSISCHE DATENTRÄGER** aufgelistet.

3. Klicken Sie unter **SPEICHERPOOLS**, wählen die **Aufgaben** aus, und wählen Sie dann **neuer Speicherpool**. Die Assistenten für neue Speicherpools wird geöffnet.

4. Auf der **vor dem Beginn** Seite **Weiter**.

5. Auf der **Geben Sie einen Speicher-Pool-Name und Subsystem** Seite, geben Sie einen Namen und optional eine Beschreibung für den Speicherpool, und wählen Sie die Gruppe verfügbarer physischer Datenträger, die Sie verwenden möchten, und wählen Sie dann **Weiter**.

6. Auf der **physische Laufwerke für den Speicherpool auswählen** Seite gehen Sie folgendermaßen vor, und wählen Sie dann **Weiter**:
    
    1. Aktivieren Sie das Kontrollkästchen neben jedem physischen Datenträger, den Sie in den Speicherpool einfügen möchten.
    
    2. Wenn Sie einen oder mehrere Datenträger unter als Hotspares festlegen möchten **Zuordnung**, wählen Sie den Dropdown-Pfeil, und wählen Sie dann **Hotspare**.

7. Auf der **Auswahl bestätigen** Seite, stellen Sie sicher, dass die Einstellungen richtig sind, und Sie dann wählen **erstellen**.

8. Auf der **Ergebnisanzeige** Seite, stellen Sie sicher, dass alle Aufgaben abgeschlossen, und Sie dann wählen **schließen**.
    
    >[!NOTE]
    >Sie haben auch die Möglichkeit, direkt mit dem nächsten Schritt fortzufahren, wenn Sie das Kontrollkästchen **Virtuellen Datenträger erstellen, wenn dieser Assistent geschlossen wird** aktivieren.

9. Prüfen Sie unter **SPEICHERPOOLS**, ob der neue Speicherpool aufgeführt ist.

### <a name="windows-powershell-equivalent-commands-for-creating-storage-pools"></a>Gleichwertige Windows PowerShell-Befehle zum Erstellen von Speicherpools

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

Im folgenden Beispiel sehen Sie, welche physischen Datenträger im ursprünglichen Pool verfügbar sind.

```PowerShell
Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk | Where-Object CanPool -eq $True
```

Das folgende Beispiel erstellt einen neuen Speicherpool mit dem Namen *StoragePool1* , die alle verfügbaren Datenträger verwendet.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk –CanPool $True)
```

Das folgende Beispiel erstellt einen neuen Speicherpool *StoragePool1*, vier der verfügbaren Datenträger verwendet.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk PhysicalDisk1, PhysicalDisk2, PhysicalDisk3, PhysicalDisk4)
```

Die folgende Cmdlet-Beispielsequenz zeigt, wie der verfügbare physische Datenträger *PhysicalDisk5* als Hotspare zum Speicherpool *StoragePool1* hinzugefügt wird.

```PowerShell
$PDToAdd = Get-PhysicalDisk –FriendlyName PhysicalDisk5
Add-PhysicalDisk –StoragePoolFriendlyName StoragePool1 –PhysicalDisks $PDToAdd –Usage HotSpare
```

## <a name="step-2-create-a-virtual-disk"></a>Schritt 2: Erstellen eines virtuellen Datenträgers

Als Nächstes erstellen Sie einzelne oder mehrere virtuelle Datenträger aus dem Speicherpool. Beim Erstellen eines virtuellen Datenträgers können Sie entscheiden, wie die Daten über die physischen Datenträger verteilt werden. Sowohl die Zuverlässigkeit als auch die Leistung werden davon beeinflusst. Sie können außerdem wählen, ob Sie Datenträger mit schlanker oder fester Bereitstellung erstellen.

1. Wenn der Assistent für neue virtuelle Datenträger nicht bereits geöffnet ist, stellen Sie im Server-Manager auf der Seite **Speicherpools** unter **SPEICHERPOOLS** sicher, dass der gewünschte Speicherpool ausgewählt ist.

2. Klicken Sie unter **virtuelle Datenträger**, wählen die **Aufgaben** aus, und wählen Sie dann **neuer virtueller Datenträger**. Die Assistenten für neue virtuelle Datenträger wird geöffnet.

3. Auf der **vor dem Beginn** Seite **Weiter**.

4. Auf der **wählen Sie den Speicherpool** Seite, wählen Sie den gewünschten Speicherpool aus, und wählen Sie dann **Weiter**.

5. Auf der **Geben Sie den Namen des virtuellen Datenträgers** Seite, geben Sie einen Namen und optional eine Beschreibung ein, und wählen **Weiter**.

6. Auf der **wählen Sie das Speicherlayout** Seite, wählen Sie das gewünschte Layout und dann **Weiter**.
    
    >[!NOTE]
    >Wenn Sie ein Layout, in dem Sie verfügen nicht über genügend physische Datenträger, auswählen, erhalten Sie eine Fehlermeldung, bei der Auswahl **Weiter**. Informationen dazu, welche Anordnung zu verwenden und die speicherplatzanforderungen finden Sie unter [Voraussetzungen](#prerequisites)).

7. Wenn Sie ausgewählt haben **Spiegel** wie das Speicherlayout, und Sie über mindestens fünf Datenträger im Pool haben die **resilienzeinstellungen konfigurieren** Seite wird angezeigt. Wählen Sie eine der folgenden Optionen aus:
    
      - **Zwei-Wege-Spiegelung**
      - **Drei-Wege-Spiegelung**

8. Auf der **Geben Sie die Bereitstellung** Seite, wählen Sie eine der folgenden Optionen aus, und wählen Sie dann **Weiter**.
    
   - **Dünn**
        
     Bei einer schlanken Bereitstellung wird Speicher nur auf Bedarf zugeordnet. Dadurch wird die Nutzung des verfügbaren Speichers optimiert. Da auf diese Weise aber eine übermäßige Zuteilung des Speichers möglich ist, müssen Sie sorgfältig überwachen, wie viel Speicherplatz verfügbar ist.
    
   - **behoben**
        
     Bei einer festen Bereitstellung wird die Speicherkapazität sofort beim Erstellen eines virtuellen Datenträgers zugeteilt. Daher entspricht der Speicherplatz, der bei einer festen Bereitstellung aus dem Speicherpool verwendet wird, der Größe des virtuellen Datenträgers.
    
     >[!TIP]
     >Mit Speicherplätzen können Sie im selben Speicherpool virtuelle Datenträger sowohl mit schlanker als auch fester Bereitstellung erstellen. Sie können beispielsweise sowohl einen virtuellen Datenträger mit schlanker Bereitstellung als Host für eine Datenbank als auch einen virtuellen Datenträger mit fester Bereitstellung als Host für die zugehörigen Protokolldateien verwenden.

9. Auf der Seite **Geben Sie die Größe des virtuellen Datenträgers an** gehen Sie folgendermaßen vor:
    
    Wenn Sie schlanke speicherzuweisung im vorherigen Schritt der **Größe des virtuellen Datenträgers** ein, geben Sie die Größe des virtuellen Datenträgers ein, wählen Sie die Einheiten (**MB**, **GB**, oder **TB** ), und wählen Sie dann **Weiter**.
    
    Wenn Sie die feste speicherzuweisung im vorherigen Schritt ausgewählt haben, wählen Sie eine der folgenden:
    
      - **Größe angeben**
        
        Um die Größe anzugeben, geben Sie einen Wert in der **Größe des virtuellen Datenträgers** Feld, und wählen Sie die Einheiten (**MB**, **GB**, oder **TB**).
        
        Wenn Sie keine einfache Speicheranordnung verwenden, nutzt der virtuelle Datenträger mehr freien Speicher als die von Ihnen angegebene Größe. Um einen potenziellen Fehler zu vermeiden, wenn die Größe des Volumes den freien Speicher des Speicherpools überschreitet, können Sie das Kontrollkästchen **Datenträger mit maximal möglicher Größe erstellen (bis zur angegebenen Größe)** aktivieren.
    
      - **Maximale Größe**
        
        Wählen Sie diese Option, um einen virtuellen Datenträger zu erstellen, der die maximale Kapazität des Speicherpools nutzt.

10. Auf der **Auswahl bestätigen** Seite, stellen Sie sicher, dass die Einstellungen richtig sind, und Sie dann wählen **erstellen**.

11. Auf der **Ergebnisanzeige** Seite, stellen Sie sicher, dass alle Aufgaben abgeschlossen, und Sie dann wählen **schließen**.
    
    >[!TIP]
    >Das Kontrollkästchen **Volume erstellen, wenn dieser Assistent geschlossen wird** ist standardmäßig aktiviert. Daraufhin wird direkt zum nächsten Schritt weitergeleitet.

### <a name="windows-powershell-equivalent-commands-for-creating-virtual-disks"></a>Gleichwertige Windows PowerShell-Befehle für die Erstellung von virtuellen Datenträgern

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

Das folgende Beispiel erstellt einen virtueller 50-GB-Datenträger, die mit dem Namen *VirtualDisk1* auf einem Speicherpool mit dem Namen *StoragePool1*.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB)
```

Das folgende Beispiel erstellt einen gespiegelten virtuellen Datenträger mit dem Namen *VirtualDisk1* auf einem Speicherpool mit dem Namen *StoragePool1*. Der Datenträger verwendet die maximale Speicherkapazität des Speicherpools.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –ResiliencySettingName Mirror –UseMaximumSize
```

Das folgende Beispiel erstellt einen virtueller 50-GB-Datenträger, die mit dem Namen *VirtualDisk1* auf einem Speicherpool mit dem Namen *StoragePool1*. Für den Datenträger wird der schlanke Bereitstellungstyp verwendet.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB) –ProvisioningType Thin
```

Das folgende Beispiel erstellt einen virtuellen Datenträger mit dem Namen *VirtualDisk1* auf einem Speicherpool mit dem Namen *StoragePool1*. Der Datenträger nutzt die Drei-Wege-Spiegelung und hat eine feste Größe von 20 GB.

>[!NOTE]
>Damit dieses Cmdlet funktioniert, müssen mindestens fünf physische Datenträger im Speicherpool vorhanden sein. (Datenträger, die als Hotspares zugeteilt sind, sind davon ausgeschlossen.)

```PowerShell
New-VirtualDisk -StoragePoolFriendlyName StoragePool1 -FriendlyName VirtualDisk1 -ResiliencySettingName Mirror -NumberOfDataCopies 3 -Size 20GB -ProvisioningType Fixed
```

## <a name="step-3-create-a-volume"></a>Schritt 3: Erstellen eines Volumes

Als Nächstes erstellen Sie ein Volume aus dem virtuellen Datenträger. Sie können weisen einen optionalen Laufwerkbuchstaben oder Ordner und dann das Volume mit einem Dateisystem formatieren.

1. Wenn der Assistent für neue Volumes nicht bereits geöffnet ist die **Speicherpools** im Server-Manager unter Seite **virtuelle Datenträger**mit der rechten Maustaste auf den gewünschten virtuellen Datenträger, und wählen Sie dann **neues Volume**.
    
    Der Assistent für neue Volumes wird geöffnet.

2. Auf der **vor dem Beginn** Seite **Weiter**.

3. Auf der **Server und Datenträger auswählen** Seite gehen Sie folgendermaßen vor, und wählen Sie dann **Weiter**.
    
    1. In der **Server** Bereich, wählen Sie den Server, auf dem Sie das Volume bereitstellen möchten.
    
    2. In der **Datenträger** Bereich, wählen Sie den virtuellen Datenträger, auf denen das Volume erstellt werden sollen.

4. Auf der **Geben Sie die Größe des Volumes** geben eine Volumegröße ein, geben Sie die Einheiten (**MB**, **GB**, oder **TB**), und wählen Sie dann auf **Weiter**.

5. Auf der **einen Laufwerksbuchstaben oder Ordner zuweisen** Seite, konfigurieren Sie die gewünschte Option aus, und wählen Sie dann **Weiter**.

6. Auf der **Dateisystemeinstellungen auswählen** Seite gehen Sie folgendermaßen vor, und wählen Sie dann **Weiter**.
    
    1. In der **Dateisystem** Liste, wählen Sie entweder **NTFS** oder **ReFS**.
    
    2. In der Liste **Größe der Zuordnungseinheiten** behalten Sie entweder die Einstellung **Standard** bei, oder legen Sie eine Größe für die Zuordnungseinheiten fest.
        
        >[!NOTE]
        >Weitere Informationen zur Größe der Zuordnungseinheiten finden Sie unter [Standard Clustergröße für NTFS, FAT und ExFAT](https://support.microsoft.com/help/140365/default-cluster-size-for-ntfs-fat-and-exfat).

    
    3. Sie können auch im Feld **Volumebezeichnung** einen Namen für das Volume eingeben, z. B. **HR Data**.

7. Auf der **Auswahl bestätigen** Seite, stellen Sie sicher, dass die Einstellungen richtig sind, und Sie dann wählen **erstellen**.

8. Auf der **Ergebnisanzeige** Seite, stellen Sie sicher, dass alle Aufgaben abgeschlossen, und Sie dann wählen **schließen**.

9. Um sicherzustellen, dass das Volume, im Server-Manager erstellt wurde, wählen Sie die **Volumes** Seite. Das Volume wird unter dem Server aufgeführt, auf dem es erstellt wurde. Sie können auch prüfen, ob das Volume im Windows-Explorer zu finden ist.

### <a name="windows-powershell-equivalent-commands-for-creating-volumes"></a>Gleichwertige Windows PowerShell-Befehle zum Erstellen von volumes

Das folgende Windows PowerShell-Cmdlet führt dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie den Befehl in einer einzelnen Zeile ein.

Im folgenden Beispiel werden die Datenträger für den virtuellen Datenträger *VirtualDisk1* initialisiert, eine Partition mit einem zugewiesenen Laufwerkbuchstaben wird erstellt, und das Volume wird dann mit dem Standard-NTFS-Dateisystem formatiert.

```PowerShell
Get-VirtualDisk –FriendlyName VirtualDisk1 | Get-Disk | Initialize-Disk –Passthru | New-Partition –AssignDriveLetter –UseMaximumSize | Format-Volume
```

## <a name="additional-information"></a>Weitere Informationen

- [Speicherplätze](overview.md)
- [Speicher-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/index?view=win10-ps)
- [Bereitstellen von Clusterspeicherplätzen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11))
- [Speicherplätze: häufig gestellte Fragen (FAQ)](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)
