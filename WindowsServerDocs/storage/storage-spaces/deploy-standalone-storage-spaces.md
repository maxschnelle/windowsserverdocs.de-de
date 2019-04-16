---
title: Bereitstellen von Speicherplätzen auf einem eigenständigen server
description: Beschreibt, wie Sie "Speicherplätze" auf einem eigenständigen Windows Server 2012-basierte Server bereitstellen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage-spaces
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 40265e767ac9aca05386c0893def259aca3a5633
ms.sourcegitcommit: e73fbe1046a8bd2bf4f24ccffc11465ad8dfab1d
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/07/2019
ms.locfileid: "8992533"
---
# Bereitstellen von Speicherplätzen auf einem eigenständigen server

>Gilt für: WindowsServer 2019, WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

In diesem Thema wird das Bereitstellen von Speicherplätzen auf einem eigenständigen Server beschrieben. Informationen dazu, wie Sie ein gruppierter Speicherplatz zu erstellen finden Sie unter [Bereitstellen einen Storage Spaces-Cluster in Windows Server 2012 R2](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>).

Um ein Speicherplatz zu erstellen, müssen Sie zunächst eine oder mehrere Speicherpools erstellen. Ein Speicherpool ist eine Sammlung von physischen Datenträgern. Ein Speicherpool ermöglicht Speicher Aggregation, flexibles Kapazitätserweiterung und delegierte Verwaltung.

Aus einem Speicherpool können Sie eine oder mehrere virtuelle Festplatten erstellen. Diese virtuellen Laufwerke werden auch als *"Speicherplätze"* bezeichnet. Ein Speicherplatz wird auf das Windows-Betriebssystem, wie ein regulärer Datenträger aus, den Sie erstellen können Volumes formatiert. Wenn Sie eine virtuelle Festplatte über die Datei- und Speicherdienste-Benutzeroberfläche erstellen, können Sie konfigurieren, des resilienztyps (einfacher, Spiegelung oder Parität), die Bereitstellung ("thin" oder "feste"), und eine. Über Windows PowerShell können Sie zusätzliche Parameter wie die Anzahl der Spalten, die Interleave-Wert und im Pool mit welcher physische Festplatten festlegen. Informationen dazu, diese zusätzlichen Parameter, finden Sie im [New-VirtualDisk](https://docs.microsoft.com/powershell/module/storage/new-virtualdisk?view=win10-ps) und [Was Spalten sind und wie entscheidet "Speicherplätze" zu verwenden, wie viele?](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx%23what_are_columns_and_how_does_storage_spaces_decide_how_many_to_use) in direkte Speicherplätze häufig gestellte Fragen (FAQS).

>[!NOTE]
>Sie können kein Speicherplatz verwenden, um Windows-Betriebssystems zu hosten.

Von einem virtuellen Datenträger können Sie ein oder mehrere Volumes erstellen. Wenn Sie ein Volume erstellen, können Sie die Größe, den Laufwerkbuchstaben oder Ordner, Dateisystem (NTFS-Dateisystem oder robustes Dateisystem (ReFS)), Zuordnungseinheiten und eine optionale Volumebezeichnung konfigurieren.

Die folgende Abbildung zeigt den Storage Spaces-Workflow.

![Storage Spaces-workflow](media/deploy-standalone-storage-spaces/storage-spaces-workflow.png)

**Abbildung 1: Storage Spaces-workflow**

>[!NOTE]
>Dieses Thema enthält Beispiel für Windows PowerShell-Cmdlets, die Sie verwenden können, um einige der beschriebenen Verfahren zu automatisieren. Weitere Informationen finden Sie in [PowerShell](https://docs.microsoft.com/powershell/scripting/powershell-scripting?view=powershell-6).

## Voraussetzungen

Um Storage Spaces auf einem eigenständigen Server von Windows Server 2012−based zu verwenden, stellen Sie sicher, dass der physische Datenträger, die Sie verwenden möchten, die folgenden Voraussetzungen erfüllen.

> [!IMPORTANT]
> Wenn Sie erfahren, wie Sie direkte Speicherplätze in einem Failovercluster bereitstellen möchten, finden Sie unter [Bereitstellen einen Storage Spaces-Cluster in Windows Server 2012 R2](<https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>). Eine Failover Cluster-Bereitstellung verfügt über verschiedene Voraussetzungen, wie z. B. unterstützte Bus Datenträgertypen unterstützten resilienztypen und die erforderliche Mindestanzahl von Laufwerken.

|Bereich|Anforderung|Anmerkungen|
|---|---|---|
|Bus Datenträgertypen|-Serial Attached SCSI (SAS)<br>-Serial Advanced Technology Attachment (SATA)<br>-iSCSI und Fibre Channel-Controller. |Sie können auch die USB-Laufwerke. Es ist jedoch nicht optimal, USB-Laufwerken in einer Server-Umgebung verwenden.<br>"Speicherplätze" wird auf iSCSI und Fibre Channel (FC)-Controller unterstützt, solange der virtuelle Datenträger über diesen erstellt nicht stabilen (einfach mit einer beliebigen Anzahl von Spalten) sind.<br>|
|Datenträgerkonfiguration|-Physische Datenträger müssen mindestens 4 GB werden.<br>-Datenträger müssen leer und nicht formatiert sein. Volumes nicht erstellt werden.||
|HBA-Aspekte|– Einfache Hostbusadapter (HBA), die RAID-Funktionen nicht unterstützen werden empfohlen.<br>– Wenn RAID-fähig müssen HBA in nicht-RAID-Modus mit allen RAID-Funktionen deaktiviert werden<br>-Adapter müssen nicht abstrahieren der physische Datenträger, Zwischenspeichern von Daten oder verbergen alle angeschlossenen Geräte. Dazu gehören Gehäuse-Dienste, die von angeschlossenen gerade eine-Bündel-der Festplatten (JBOD)-Geräten bereitgestellt werden. |"Speicherplätze" ist nur mit HBA kompatibel, in denen können Sie vollständig alle RAID-Funktionen deaktivieren.|
|JBOD-Speicherserver|-JBOD-Speicherserver sind optional<br>-Speicherplätze mit zertifiziert Gehäuse in Windows Server-Katalog aufgeführt empfohlen<br>– Wenn Sie eine JBOD-Speicherserver verwenden, sich an den Speicherhersteller überprüfen, ob das Gehäuse "Speicherplätze", um sicherzustellen, dass alle Funktionen unterstützt<br>– Um festzustellen, ob die JBOD-Speicherserver Gehäuse und Steckplatz Identifizierung unterstützt, führen Sie die folgenden Windows PowerShell-Cmdlet aus:<br><br>`Get-PhysicalDisk \| ? {$_.BusType –eq "SAS"} \| fc`<br><br>Enthalten die Felder **EnclosureNumber** und **SlotNumber** Werte, unterstützt das Gehäuse diese Features.||

Um die Anzahl der physischen Datenträger und das gewünschte resilienztyp für einen eigenständigen Server-Bereitstellung planen, verwenden Sie die folgenden Richtlinien.

|Resilienztyp|Datenträger-Anforderungen|Gründe für die Verwendung|
|---|---|---|
|**Einfach**<br><br>-Streifen Daten auf physische Datenträger<br>-Maximiert Datenträgerkapazität und erhöht den Durchsatz<br>-Keine resilienz (schützt nicht vor Ausfall der Festplatte)<br><br><br><br><br><br><br>|Erfordert mindestens eine physische Festplatte.|Verwenden Sie nicht auf Host unersetzlich betrachten Daten. Einfache Leerzeichen schützen nicht vor.<br><br>Verwenden Sie zum Host temporären oder einfach neu erstellten Daten zu einem Sonderpreis.<br><br>Geeignet für High-End-Workloads, in denen resilienz ist nicht erforderlich, oder bereits von der Anwendung bereitgestellt wird.|
|**Spiegel**<br><br>-Zwei oder drei Kopien der Daten in einer Gruppe von physischen Datenträgern speichert<br>-Erhöht die Zuverlässigkeit, aber reduziert Kapazität. Duplizierung tritt bei jedem Schreibvorgang. Leerstellen, die durch Spiegelung Streifen auch die Daten auf mehrere physische Laufwerke.<br>– Größere Datendurchsatz und geringere Zugriffslatenz als Parität<br>-Verwendet dirty Region (DRT) zum Nachverfolgen von Änderungen zu den Laufwerken im Pool nachverfolgen. Wenn das System über ein ungeplantes Herunterfahren fortgesetzt wird, und die Leerzeichen wieder online geschaltet werden, stellt DRT Datenträger im Pool konsistent.|Erfordert mindestens zwei physische Datenträger vor dem Ausfall der Festplatte schützen.<br><br>Erfordert mindestens fünf physische Datenträger von zwei gleichzeitige Datenträgerfehlern zu schützen.|Verwenden Sie für die meisten Bereitstellungen. Beispielsweise eignen sich Spiegelung Leerzeichen für eine allgemeine Dateifreigabe oder eine virtuelle Festplatte (VHD)-Bibliothek.|
|**Parität**<br><br>-Daten und Parität auf physische Datenträger Streifen<br>-Zuverlässigkeit erhöht, wenn es mit einem einfachen Speicherplatz verglichen, aber etwas Kapazität reduziert<br>-Resilienz über Journaling erhöht. Dadurch wird die Beschädigung von Daten zu verhindern, wenn ein ungeplantes Herunterfahren auftritt.|Erfordert mindestens drei physische Datenträger vor dem Ausfall der Festplatte schützen.|Bei Workloads, die hochgradig sequenzielle, z. B. Archiv oder Sicherung verwendet.|

## Schritt 1: Erstellen Sie einen Speicherpool

Müssen Sie die erste Gruppe verfügbaren physischen Datenträger in einen oder mehrere Speicher-Pools.

1. Wählen Sie im Navigationsbereich Server-Manager **Datei- und Speicherdienste**.

2. Wählen Sie im Navigationsbereich die **Speicher-Pools** -Seite.
    
    Standardmäßig sind verfügbare Datenträger in einem Pool enthalten, mit dem Namen des *primordial* Pools. Wenn kein primordial Pool unter **SPEICHERPOOLS**aufgeführt ist, bedeutet dies, dass der Speicher die Anforderungen für direkte Speicherplätze nicht erfüllt. Stellen Sie sicher, dass die Datenträger, die Anforderungen erfüllen, die im Abschnitt Voraussetzungen beschrieben werden.
    
    >[!TIP]
    >Wenn Sie die **Primordial** Speicherpool auswählen, werden die verfügbaren physischen Datenträgern unter **PHYSISCHE Datenträger**aufgelistet.

3. Wählen Sie unter **SPEICHERPOOLS**die **Aufgaben** aus, und wählen Sie dann die **Neue Speicherpool**. Der neue Speicher-Pool-Assistent wird geöffnet.

4. Wählen Sie auf der Seite **Vorbereitung** **Weiter**.

5. Geben Sie einen Namen und optional eine Beschreibung für den Speicherpool, wählen Sie die Gruppe der verfügbaren physischen Datenträger, die Sie verwenden möchten, und wählen Sie dann **Weiter**, auf der Seite **Geben Sie einen Speicher-Pool-Namen und -Subsystem** .

6. Führen Sie die folgenden, und wählen Sie dann **als Nächstes**auf der Seite **physische Datenträger für den Speicherpool auswählen** :
    
    1. Wählen Sie das Kontrollkästchen neben jedem physischen Datenträger, den im Speicherpool enthalten sein sollen.
    
    2. Wenn Sie eine festlegen möchten, oder weitere Datenträger als hot Reserve, unter **Zuweisung**, wählen Sie den Dropdownpfeil, wählen Sie dann **Hot Ersatz**.

7. Stellen Sie sicher, dass die Einstellungen korrekt sind, und Sie dann **Erstellen wählen**, auf der Seite **bestätigen-Auswahl** .

8. Stellen Sie sicher, dass alle Aufgaben abgeschlossen, und wählen Sie dann **Schließen**, auf der Seite **Ergebnisse anzeigen** .
    
    >[!NOTE]
    >Wenn Sie direkt mit dem nächsten Schritt fortfahren, können Sie optional das Kontrollkästchen **Erstellen Sie einen virtuellen Datenträger, wenn dieser Assistent geschlossen wird** auswählen.

9. Unter **SPEICHERPOOLS**stellen Sie sicher, dass die neuen Speicherpool aufgeführt ist.

### Entsprechende Windows PowerShell-Befehle zum Erstellen von Speicher-pools

Führen die folgenden Windows PowerShell-Cmdlet oder Cmdlets dieselbe Funktion wie im vorherigen Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden, aufgrund der Formatierung von Einschränkungen.

Das folgende Beispiel zeigt, welche physische Datenträger im primordial Pool verfügbar sind.

```PowerShell
Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk | Where-Object CanPool -eq $True
```

Das folgende Beispiel erstellt einen neuen Speicherpool mit dem Namen *StoragePool1* , die alle verfügbaren Datenträger verwendet.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk –CanPool $True)
```

Das folgende Beispiel erstellt einen neuen Speicherpool *StoragePool1*, die vier der verfügbaren Datenträger verwendet.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName “Storage Spaces*” –PhysicalDisks (Get-PhysicalDisk PhysicalDisk1, PhysicalDisk2, PhysicalDisk3, PhysicalDisk4)
```

Die folgende Beispiel-Sequenz von Cmdlets veranschaulicht das hinzufügen einen verfügbaren physischen Datenträger *PhysicalDisk5* als solches dem Speicherpool *StoragePool1*.

```PowerShell
$PDToAdd = Get-PhysicalDisk –FriendlyName PhysicalDisk5
Add-PhysicalDisk –StoragePoolFriendlyName StoragePool1 –PhysicalDisks $PDToAdd –Usage HotSpare
```

## Schritt 2: Erstellen einer virtuellen Festplatte

Als Nächstes müssen Sie einen oder mehrere virtuelle Datenträger aus dem Speicherpool erstellen. Wenn Sie eine virtuelle Festplatte erstellen, können Sie auswählen, wie die Daten über die physische Datenträger angeordnet sind. Dies betrifft, Zuverlässigkeit und Leistung. Sie können auch auswählen, ob Sie Datenträger oder behoben-schlanke zu erstellen.

1. Stellen Sie der Assistent für neue virtuelle Datenträger nicht bereits geöffnet ist, auf der Seite **Speicherpools** im Server-Manager ist unter **SPEICHERPOOLS**, sicher, dass die gewünschten Speicherpool aktiviert ist.

2. Klicken Sie unter **Virtuellen Datenträger**wählen Sie die **Aufgaben** aus, und wählen Sie dann **Neuer virtueller Datenträger**. Der Assistent für neue virtuelle Datenträger wird geöffnet.

3. Wählen Sie auf der Seite **Vorbereitung** **Weiter**.

4. Klicken Sie auf der Seite **Wählen Sie den Speicherpool** wählen Sie die gewünschten Speicherpool, und wählen Sie dann **Weiter**.

5. Geben Sie auf der Seite **Geben Sie den Namen des virtuellen Datenträgers** einen Namen und optional eine Beschreibung, und wählen Sie dann **Weiter**.

6. Wählen Sie auf der Seite **Wählen Sie das Speicherlayout** das gewünschte Layout, und wählen Sie dann **Weiter**.
    
    >[!NOTE]
    >Wenn Sie ein Layout auswählen, in denen Sie nicht genügend physische Datenträger verfügen, erhalten Sie eine Fehlermeldung angezeigt, wenn Sie **als Nächstes**auswählen. Informationen dazu, welches Layout und die Datenträger-Anforderungen finden Sie unter [Voraussetzungen](#prerequisites)).

7. Wenn Sie die **Spiegelung** als das Speicherlayout ausgewählt, und Sie fünf oder mehr Laufwerken im Pool haben, wird die Seite **Konfigurieren Sie die resilienz-Einstellungen** angezeigt. Wählen Sie eine der folgenden Optionen aus:
    
      - **Zwei-Wege-Spiegelung**
      - **Drei-Wege-Spiegelung**

8. Auf der Seite **Geben Sie die Art der Bereitstellung** eines der folgenden Optionen auswählen, und wählen Sie dann **Weiter**.
    
      - **Thin**
        
        Mit der Bereitstellung von thin wird Speicherplatz auf Basis bei Bedarf zugewiesen. Dadurch wird die Verwendung der verfügbaren Speicher. Aber da dies zu viel Speicher zuweisen kann, müssen Sie sorgfältig überwachen wie viel Speicherplatz verfügbar ist.
    
      - **Behoben**
        
        Mit festen Bereitstellung ist die Speicherkapazität sofort, zum Zeitpunkt reserviert, wenn eine virtuelle Festplatte erstellt wird. Daher behoben Bereitstellung verwendet Platz aus dem Speicherpool, der die Größe des virtuellen Datenträgers entspricht.
    
    >[!TIP]
    >Mit direkten Speicherplätzen können Sie beide und behoben-schlanke virtuellen Datenträger im gleichen Speicherpool erstellen. Beispielsweise können Sie eine schlanke virtuelle Festplatte zum Hosten einer Datenbank und die feste bereitgestellt virtuellen Laufwerks, um die zugehörigen Protokolldateien zu hosten.

9. Gehen Sie auf der Seite **Geben Sie die Größe des virtuellen Datenträgers** wie folgt:
    
    Wenn Sie die schlanke speicherzuweisung im vorherigen Schritt ausgewählt haben, geben Sie im Feld **Größe des virtuellen Datenträgers** eine virtuelle Größe, wählen Sie die Einheiten (**MB**, **GB**oder **TB**), und wählen Sie **als Nächstes**.
    
    Wenn Sie die feste Bereitstellung im vorherigen Schritt ausgewählt haben, wählen Sie eine der folgenden:
    
      - **Geben Sie Größe**
        
        Um eine Größe anzugeben, geben Sie einen Wert im Feld **Größe des virtuellen Datenträger** , und wählen Sie dann die Einheiten (**MB**, **GB**oder **TB**).
        
        Wenn Sie ein Speicherlayout als einfache verwenden, verwendet der virtuelle Datenträger mehr Speicherplatz als die Größe, die Sie angeben. Um einen möglichen Fehler zu vermeiden, in denen die Größe des Volumes Pool freier Speicherplatz überschreitet, können Sie das Kontrollkästchen **Erstellen den größten virtuellen Datenträger möglich ist, bis der angegebenen Größe** auswählen.
    
      - **Maximale Größe**
        
        Wählen Sie diese Option, um eine virtuelle Festplatte zu erstellen, die die maximale Kapazität im Speicherpool verwendet.

10. Stellen Sie sicher, dass die Einstellungen korrekt sind, und Sie dann **Erstellen wählen**, auf der Seite **bestätigen-Auswahl** .

11. Stellen Sie sicher, dass alle Aufgaben abgeschlossen, und wählen Sie dann **Schließen**, auf der Seite **Ergebnisse anzeigen** .
    
    >[!TIP]
    >Standardmäßig ist das Kontrollkästchen **Erstellen Sie ein Volume, wenn dieser Assistent geschlossen wird** aktiviert. Dadurch gelangen Sie direkt mit dem nächsten Schritt.

### Entsprechende Windows PowerShell-Befehle zum Erstellen von virtueller Festplatten

Führen die folgenden Windows PowerShell-Cmdlet oder Cmdlets dieselbe Funktion wie im vorherigen Verfahren. Geben Sie jedes Cmdlet in einer einzelnen Zeile, auch wenn sie über mehrere Zeilen umgebrochen angezeigt werden, aufgrund der Formatierung von Einschränkungen.

Das folgende Beispiel erstellt einen 50 GB virtuellen Datenträger mit dem Namen *VirtualDisk1* auf einen Speicherpool mit dem Namen *StoragePool1*.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB)
```

Das folgende Beispiel erstellt einen gespiegelten virtuellen Datenträger, die mit dem Namen *VirtualDisk1* auf einen Speicherpool mit dem Namen *StoragePool1*. Die Festplatte verwendet den Speicherpool maximale Speicherkapazität.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –ResiliencySettingName Mirror –UseMaximumSize
```

Das folgende Beispiel erstellt einen 50 GB virtuellen Datenträger mit dem Namen *VirtualDisk1* auf einen Speicherpool mit dem Namen *StoragePool1*. Die Festplatte verwendet den thin provisioning-Typ.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB) –ProvisioningType Thin
```

Das folgende Beispiel erstellt einen virtuellen Datenträger, die mit dem Namen *VirtualDisk1* auf einen Speicherpool mit dem Namen *StoragePool1*. Der virtuelle Datenträger verwendet drei-Wege-Spiegelung und eine feste Größe von 20 GB.

>[!NOTE]
>Sie müssen mindestens fünf physische Datenträger im Speicherpool für dieses Cmdlets funktionieren. (Dies schließt keine Datenträger, die als hot Reserve zugewiesen werden.)

```PowerShell
New-VirtualDisk -StoragePoolFriendlyName StoragePool1 -FriendlyName VirtualDisk1 -ResiliencySettingName Mirror -NumberOfDataCopies 3 -Size 20GB -ProvisioningType Fixed
```

## Schritt 3: Erstellen Sie ein volume

Als Nächstes müssen Sie ein Volume von der virtuellen Festplatte erstellen. Sie können weisen Sie eine optionale Laufwerkbuchstaben oder einen Ordner und dann das Volume mit einem Dateisystem formatieren.

1. Wenn der Assistent für neue Volumes nicht bereits geöffnet ist, auf der Seite **Speicherpools** im Server-Manager unter **Virtuellen Datenträger**ist mit der rechten Maustaste die gewünschten virtuellen Datenträgers, und wählen Sie dann die **Neue Volume**.
    
    Der Assistent für neue Volumes wird geöffnet.

2. Wählen Sie auf der Seite **Vorbereitung** **Weiter**.

3. Führen Sie die folgenden, und wählen Sie dann **als Nächstes**auf der Seite **Wählen Sie die Server und Datenträger** .
    
    1. Wählen Sie im Bereich **Server** des Servers, auf dem Sie das Volume bereitstellen möchten.
    
    2. Wählen Sie im Bereich **Datenträger** den virtuellen Datenträger, auf dem Sie das Volume erstellen möchten.

4. Klicken Sie auf der Seite **Geben Sie die Größe des Volumes** Geben Sie eine Volumegröße die Einheiten (**MB**, **GB**oder **TB**) Geben Sie an, und wählen Sie dann **Weiter**.

5. Konfigurieren Sie die gewünschte Option auf der Seite **weisen auf einen Laufwerkbuchstaben oder einen Ordner** , und wählen Sie dann **Weiter**.

6. Führen Sie die folgenden, und wählen Sie dann **als Nächstes**auf der Seite **Dateisystemeinstellungen auswählen** .
    
    1. Wählen Sie in der Liste **Dateisystem** **NTFS** oder **ReFS**.
    
    2. Übernehmen Sie die Einstellung **Standard** , oder legen Sie die Größe der Zuordnungseinheit, in der Liste **Zuordnungseinheit** .
        
        >[!NOTE]
        >Weitere Informationen zu Zuordnungseinheit finden Sie in der [Standard-Clustergröße für NTFS, FAT und ExFAT](https://support.microsoft.com/help/140365/default-cluster-size-for-ntfs-fat-and-exfat).

    
    3. Geben Sie im Feld **Volumebezeichnung** optional einen Volume Beschriftung Namen, z. B. **HR-Daten**.

7. Stellen Sie sicher, dass die Einstellungen korrekt sind, und Sie dann **Erstellen wählen**, auf der Seite **bestätigen-Auswahl** .

8. Stellen Sie sicher, dass alle Aufgaben abgeschlossen, und wählen Sie dann **Schließen**, auf der Seite **Ergebnisse anzeigen** .

9. Wählen Sie die **Volumes** -Seite, um sicherzustellen, dass das Volume, im Server-Manager erstellt wurde. Das Volume wird unter dem Server aufgeführt, in dem es erstellt wurde. Sie können auch sicherstellen, dass das Volume in Windows Explorer ist.

### Entsprechende Windows PowerShell-Befehle zum Erstellen von volumes

Die folgenden Windows PowerShell-Cmdlet führt die gleiche Funktion wie im vorherigen Verfahren. Geben Sie den Befehl in einer einzelnen Zeile.

Im folgenden Beispiel wird die Datenträger für virtuelle Datenträger *VirtualDisk1*initialisiert, erstellt eine Partition mit Laufwerkbuchstabe zugewiesen und dann das Volume mit dem standardmäßigen NTFS-Dateisystem formatiert.

```PowerShell
Get-VirtualDisk –FriendlyName VirtualDisk1 | Get-Disk | Initialize-Disk –Passthru | New-Partition –AssignDriveLetter –UseMaximumSize | Format-Volume
```

## Weitere Informationen

- [Speicherplätze](overview.md)
- [Speicher-Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/storage/index?view=win10-ps)
- [Gruppierte Speicherplätze bereitstellen](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11))
- [Häufig gestellte Fragen (FAQ) "Speicherplätze"](https://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx)
