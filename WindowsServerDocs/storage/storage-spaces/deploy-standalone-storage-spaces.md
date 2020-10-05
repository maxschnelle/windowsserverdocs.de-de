---
title: Bereitstellen von Speicherplätzen auf einem eigenständigen Server
description: Hier wird beschrieben, wie Speicherplätze auf einem eigenständigen Windows Server 2012-basierten Server bereitgestellt werden.
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4758cc67c1dd5dc77ecacf1a8229d59f27eac60e
ms.sourcegitcommit: 00406560a665a24d5a2b01c68063afdba1c74715
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2020
ms.locfileid: "91716867"
---
# <a name="deploy-storage-spaces-on-a-stand-alone-server"></a>Bereitstellen von Speicherplätzen auf einem eigenständigen Server

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird beschrieben, wie Sie Speicherplätze auf einem eigenständigen Server bereitstellen. Weitere Informationen zum Erstellen eines Cluster Speicherplatzes finden Sie unter Bereitstellen [eines Speicherplätze-Clusters unter Windows Server 2012 R2](</previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>).

Um einen Speicherplatz zu erstellen, müssen Sie zuerst einen oder mehrere Speicherpools erstellen. Ein Speicherpool ist eine Gruppe physischer Datenträger. Speicherpools ermöglichen eine Speicheraggregation, eine flexible Kapazitätserweiterung und eine delegierte Verwaltung.

Aus einem Speicherpool können Sie einzelne oder mehrere virtuelle Datenträger erstellen. Diese virtuellen Datenträger werden auch als *Speicherplätze* bezeichnet. Ein Speicherplatz wird vom Windows-Betriebssystem als ein normaler Datenträger angesehen, von dem Sie formatierte Volumes erstellen können. Wenn Sie einen virtuellen Datenträger über die Benutzeroberfläche "Datei- und Speicherdienste" erstellen, können Sie den Resilienztyp (einfach, Spiegeln oder Parität), den Bereitstellungstyp (schlank oder fest) und die Größe konfigurieren. Über Windows PowerShell können Sie zusätzliche Parameter, wie die Anzahl der Spalten, den Überlappungswert und die im Pool zu verwendenden physischen Datenträger festlegen. Weitere Informationen zu diesen zusätzlichen Parametern finden Sie unter [New-virtualdisk](/powershell/module/storage/new-virtualdisk?view=win10-ps) und im [Windows Server Storage-Forum](/answers/topics/windows-server-storage.html).

> [!NOTE]
> Ein Speicherplatz kann nicht zum Hosten des Windows-Betriebssystems verwendet werden.

Von einem virtuellen Datenträger können Sie einzelne oder mehrere Volumes erstellen. Wenn Sie ein Volume erstellen, können Sie die Größe, den Laufwerk Buchstaben oder-Ordner, das Dateisystem (NTFS-Dateisystem oder Refs), die Größe der Zuordnungs Einheit und eine optionale Volumebezeichnung konfigurieren.

In der folgenden Abbildung ist der Speicherplatz-Workflow dargestellt.

![Speicherplätze – Workflow](media/deploy-standalone-storage-spaces/storage-spaces-workflow.png)

**Abbildung 1: Speicherplätze-Workflow**

> [!NOTE]
> Dieses Thema enthält Windows PowerShell-Beispiel-Cmdlets, mit denen Sie einige der beschriebenen Vorgehensweisen automatisieren können. Weitere Informationen finden Sie unter [PowerShell](/powershell/scripting/powershell-scripting?view=powershell-6).

## <a name="prerequisites"></a>Voraussetzungen

Wenn Sie Speicherplätze auf einem eigenständigen Windows Server 2012-basierten Server verwenden möchten, stellen Sie sicher, dass die physischen Datenträger, die Sie verwenden möchten, die folgenden Voraussetzungen erfüllen.

> [!IMPORTANT]
> Weitere Informationen zum Bereitstellen von Speicherplätzen auf einem Failovercluster finden Sie unter Bereitstellen [eines Speicherplätze-Clusters unter Windows Server 2012 R2](</previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/mt270997(v%3dws.11)>). Für eine failoverclusterbereitstellung gelten andere Voraussetzungen, z. b. unterstützte Daten trägerbus Typen, unterstützte resilienztypen und die erforderliche Mindestanzahl von Datenträgern

|Bereich|Anforderung|Notizen|
|---|---|---|
|Datenträgerbustypen|– Serial Attached SCSI (SAS)<br>– Serial Advanced Technology Attachment (SATA)<br>– iSCSI und Fibre Channel-Controller |Sie können auch USB-Laufwerke verwenden. Es ist jedoch nicht optimal, USB-Laufwerke in einer Serverumgebung zu verwenden.<br>Speicherplätze werden auf iSCSI-und Fibre Channel (FC)-Controllern unterstützt, solange die darauf erstellten virtuellen Datenträger nicht stabil sind (einfach mit einer beliebigen Anzahl von Spalten).<br>|
|Datenträgerkonfiguration|-Der physische Datenträger muss mindestens 4 GB groß sein.<br>-Datenträger müssen leer und nicht formatiert sein. Erstellen Sie keine Volumes||
|HBA-Überlegungen|– Einfache Hostbusadapter (HBAs), die keine RAID-Funktionalität unterstützen, werden empfohlen.<br>– Wenn HBAs RAID-fähig sind, müssen sie sich im Nicht-RAID-Modus befinden, in dem alle RAID-Funktionalitäten deaktiviert sind.<br>– Adapter dürfen die physischen Datenträger, Cachedaten oder alle angeschlossenen Geräte nicht abstrahieren. Dies gilt auch für Gehäusedienste, die von angeschlossenen JBOD-Geräten bereitgestellt werden. |Speicherplätze sind nur mit HBAs kompatibel, wenn Sie die gesamte RAID-Funktionalität vollständig deaktivieren können.|
|JBOD-Gehäuse|-JBOD-Gehäuse sind optional<br>-Empfohlen zur Verwendung von Speicherplätzen Certified-Gehäusen, die im Windows Server-Katalog aufgelistet sind<br>Wenn Sie ein JBOD-Gehäuse verwenden, überprüfen Sie bei Ihrem Speicher Anbieter, ob das Gehäuse Speicherplätze unterstützt, um eine vollständige Funktionalität sicherzustellen.<br>-Führen Sie das folgende Windows PowerShell-Cmdlet aus, um zu bestimmen, ob das JBOD-Gehäuse Gehäuse-und Slot-Identifizierung unterstützt:<br><br> "Get-PhysicalDisk" \| ? {$_. BusType – EQ "SAS"} \| FC <br> | Wenn die Felder " **einclosurenumber** " und " **SlotNumber** " Werte enthalten, unterstützt das Gehäuse diese Funktionen.|

Bei der Planung der Anzahl der physischen Datenträger und des gewünschten Resilienztyps für eine eigenständige Serverbereitstellung halten Sie sich an folgende Richtlinien.

|Resilienztyp|Datenträgeranforderungen|Verwendung|
|---|---|---|
|**Einfach**<br><br>-Streifen Daten auf physischen Datenträgern<br>-Maximiert Datenträger Kapazität und erhöht den Durchsatz<br>-Keine Resilienz (schützt nicht vor Datenträger Fehlern)<br><br><br><br><br><br><br>|Erfordert mindestens einen physischen Datenträger.|Nicht zum Hosten unersetzbarer Daten verwenden. Einfache Leerzeichen schützen nicht vor Datenträger Fehlern.<br><br>Zum Hosten temporärer oder leicht wiederherstellbarer Daten zu reduzierten Kosten geeignet.<br><br>Geeignet für hochleistungsfähige Workloads, bei denen Resilienz nicht erforderlich ist oder bereits von der Anwendung bereitgestellt wird.|
|**Spiegel**<br><br>-Speichert zwei oder drei Kopien der Daten auf der Gruppe physischer Datenträger.<br>-Erhöht die Zuverlässigkeit, verringert jedoch die Kapazität. Bei jedem Schreibvorgang wird dupliziert. Außerdem verteilt ein Spiegelspeicherplatz die Daten über mehrere physische Datenträger.<br>-Größerer Datendurchsatz und geringere Zugriffs Latenz als Parität<br>-Verwendet die Änderungs Bereichs Überwachung (Dirty Region Tracking, DRT), um Änderungen an den Datenträgern im Pool nachzuverfolgen. Wenn das System ungeplant heruntergefahren wurde und dann den Betrieb wieder aufnimmt und die Speicherplätze wieder online geschaltet werden, stimmt DRT die Datenträger im Pool erneut aufeinander ab.|Erfordert mindestens zwei physische Datenträger, um vor dem Ausfall einzelner Datenträger geschützt zu sein.<br><br>Erfordert mindestens fünf physische Datenträger, um vor dem gleichzeitigen Ausfall zweier Datenträger geschützt zu sein.|Wird für die meisten Bereitstellungen verwendet. Spiegelspeicherplätze sind beispielsweise für eine allgemeine Dateifreigabe oder eine virtuelle Festplattenbibliothek (Virtual Hard Disk, VHD) geeignet.|
|**Parität**<br><br>-Streifen Daten und Paritätsinformationen auf physischen Datenträgern<br>-Erhöht die Zuverlässigkeit beim Vergleich mit einem einfachen Raum, verringert jedoch die Kapazität etwas<br>– Erhöht Resilienz durch Journaling Dadurch kann eine Beschädigung der Daten verhindert werden, wenn das System unplanmäßig heruntergefahren wird.|Erfordert mindestens drei physische Datenträger, um vor dem Ausfall einzelner Datenträger geschützt zu sein.|Geeignet für stark sequenzielle Arbeitsauslastungen, z. B. bei Archiven oder Backups.|

## <a name="step-1-create-a-storage-pool"></a>Schritt 1: Erstellen eines Speicherpools

Zuerst müssen Sie die verfügbaren physischen Datenträger in einzelne oder mehrere Speicherpools zusammenfassen.

1. Wählen Sie im Navigationsbereich Server-Manager die Option **Datei-und Speicherdienste**aus.

2. Wählen Sie im Navigationsbereich die Seite **Speicher Pools** aus.

    Verfügbare Datenträger werden standardmäßig in einem *ursprünglichen* Pool eingefügt. Wenn unter **SPEICHERPOOLS** kein ursprünglicher Pool aufgeführt ist, bedeutet das, dass der Speicher die Anforderungen für Speicherplätze nicht erfüllt. Stellen Sie sicher, dass die Datenträger die Anforderungen erfüllen, die im Abschnitt "Voraussetzungen" erläutert sind.

    > [!TIP]
    > Wenn Sie den ursprünglichen Speicherpool (**Primordial**) auswählen, werden die verfügbaren physischen Datenträger unter **PHYSISCHE DATENTRÄGER** aufgelistet.

3. Klicken Sie unter **Speicher Pools**auf die Liste **Aufgaben** , und wählen Sie dann **neuer Speicher Pool**aus. Der Assistent für neue Speicherpools wird geöffnet.

4. Wählen Sie **auf der Seite** Vorbereitung die Option **weiter**aus.

5. Geben Sie auf der Seite **Speicherpool Name und Subsystem angeben** einen Namen und optional eine Beschreibung für den Speicherpool ein, wählen Sie die Gruppe verfügbarer physischer Datenträger aus, die Sie verwenden möchten, und klicken Sie dann auf **weiter**.

6. Führen Sie auf der Seite physische Datenträger **für den Speicherpool auswählen** die folgenden Schritte aus, und klicken Sie dann auf **weiter**:

    1. Aktivieren Sie das Kontrollkästchen neben jedem physischen Datenträger, den Sie in den Speicherpool einfügen möchten.

    2. Wenn Sie einen oder mehrere Datenträger als Hotspares festlegen möchten, klicken Sie unter **Zuordnung**auf den Dropdown Pfeil, und wählen Sie dann **Hot Spare**aus.

7. Überprüfen Sie auf der Seite **Auswahl bestätigen** , ob die Einstellungen richtig sind, und wählen Sie dann **Erstellen**aus.

8. Überprüfen Sie auf der Seite **Ergebnisse anzeigen** , ob alle Aufgaben abgeschlossen sind, und wählen Sie dann **Schließen**aus.

    > [!NOTE]
    > Sie haben auch die Möglichkeit, direkt mit dem nächsten Schritt fortzufahren, wenn Sie das Kontrollkästchen **Virtuellen Datenträger erstellen, wenn dieser Assistent geschlossen wird** aktivieren.

9. Prüfen Sie unter **SPEICHERPOOLS**, ob der neue Speicherpool aufgeführt ist.

### <a name="windows-powershell-equivalent-commands-for-creating-storage-pools"></a>Entsprechende Windows PowerShell-Befehle zum Erstellen von Speicherpools

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

Im folgenden Beispiel sehen Sie, welche physischen Datenträger im ursprünglichen Pool verfügbar sind.

```PowerShell
Get-StoragePool -IsPrimordial $true | Get-PhysicalDisk -CanPool $True
```

Im folgenden Beispiel wird ein neuer Speicherpool mit dem Namen *StoragePool1* erstellt, der alle verfügbaren Datenträger verwendet.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName "Windows Storage*" –PhysicalDisks (Get-PhysicalDisk –CanPool $True)
```

Im folgenden Beispiel wird ein neuer Speicherpool, *StoragePool1*, erstellt, der vier der verfügbaren Datenträger verwendet.

```PowerShell
New-StoragePool –FriendlyName StoragePool1 –StorageSubsystemFriendlyName "Windows Storage*" –PhysicalDisks (Get-PhysicalDisk PhysicalDisk1, PhysicalDisk2, PhysicalDisk3, PhysicalDisk4)
```

Die folgende Cmdlet-Beispielsequenz zeigt, wie der verfügbare physische Datenträger *PhysicalDisk5* als Hotspare zum Speicherpool *StoragePool1* hinzugefügt wird.

```PowerShell
$PDToAdd = Get-PhysicalDisk –FriendlyName PhysicalDisk5
Add-PhysicalDisk –StoragePoolFriendlyName StoragePool1 –PhysicalDisks $PDToAdd –Usage HotSpare
```

## <a name="step-2-create-a-virtual-disk"></a>Schritt 2: Erstellen eines virtuellen Datenträgers

Als Nächstes erstellen Sie einzelne oder mehrere virtuelle Datenträger aus dem Speicherpool. Beim Erstellen eines virtuellen Datenträgers können Sie entscheiden, wie die Daten über die physischen Datenträger verteilt werden. Sowohl die Zuverlässigkeit als auch die Leistung werden davon beeinflusst. Sie können außerdem wählen, ob Sie Datenträger mit schlanker oder fester Bereitstellung erstellen.

1. Wenn der Assistent für neue virtuelle Datenträger nicht bereits geöffnet ist, stellen Sie im Server-Manager auf der Seite **Speicherpools** unter **SPEICHERPOOLS** sicher, dass der gewünschte Speicherpool ausgewählt ist.

2. Klicken Sie unter **virtuelle**Datenträger auf die Liste **Aufgaben** , und wählen Sie dann **neuer virtueller**Datenträger aus. Der Assistent für neue virtuelle Datenträger wird geöffnet.

3. Wählen Sie **auf der Seite** Vorbereitung die Option **weiter**aus.

4. Wählen Sie auf der Seite **Speicherpool auswählen** den gewünschten Speicherpool aus, und klicken Sie dann auf **weiter**.

5. Geben Sie auf der Seite **Geben Sie den Namen des virtuellen** Datenträgers an einen Namen und optional eine Beschreibung ein, und klicken Sie auf **weiter**.

6. Wählen Sie auf der Seite **Wählen Sie das Speicher Layout** aus das gewünschte Layout aus, und klicken Sie dann auf **weiter**.

    > [!NOTE]
    > Wenn Sie ein Layout auswählen, bei dem nicht genügend physische Datenträger vorhanden sind, erhalten Sie eine Fehlermeldung, wenn Sie auf **weiter**klicken. Informationen dazu, welches Layout und welche Datenträger Anforderungen zu verwenden sind, finden Sie unter [Voraussetzungen](#prerequisites).

7. Wenn Sie **Spiegelung** als Speicher Layout ausgewählt haben und im Pool mindestens fünf Datenträger vorhanden sind, wird die Seite **resilienzeinstellungen konfigurieren** angezeigt. Wählen Sie eine der folgenden Optionen aus:

      - **Zwei-Wege-Spiegelung**
      - **Drei-Wege-Spiegelung**

8. Wählen Sie auf der Seite **Bereitstellungstyp angeben** eine der folgenden Optionen aus, und klicken Sie dann auf **weiter**.

   - **Dünn**

     Bei einer schlanken Bereitstellung wird Speicher nur auf Bedarf zugeordnet. Dadurch wird die Nutzung des verfügbaren Speichers optimiert. Da auf diese Weise aber eine übermäßige Zuteilung des Speichers möglich ist, müssen Sie sorgfältig überwachen, wie viel Speicherplatz verfügbar ist.

   - **Festen**

     Bei einer festen Bereitstellung wird die Speicherkapazität sofort beim Erstellen eines virtuellen Datenträgers zugeteilt. Daher entspricht der Speicherplatz, der bei einer festen Bereitstellung aus dem Speicherpool verwendet wird, der Größe des virtuellen Datenträgers.

     > [!TIP]
     > Mit Speicherplätzen können Sie im selben Speicherpool virtuelle Datenträger sowohl mit schlanker als auch fester Bereitstellung erstellen. Sie können beispielsweise sowohl einen virtuellen Datenträger mit schlanker Bereitstellung als Host für eine Datenbank als auch einen virtuellen Datenträger mit fester Bereitstellung als Host für die zugehörigen Protokolldateien verwenden.

9. Auf der Seite **Geben Sie die Größe des virtuellen Datenträgers an** gehen Sie folgendermaßen vor:

    Wenn Sie im vorherigen Schritt eine schlanke Bereitstellung ausgewählt haben, geben Sie im Feld **Größe des virtuellen** Datenträgers eine Größe für den virtuellen Datenträger ein, wählen Sie die Einheiten (**MB**, **GB**oder **TB**) aus, und klicken Sie dann auf **weiter**.

    Wenn Sie im vorherigen Schritt eine Fixed-Bereitstellung ausgewählt haben, wählen Sie eine der folgenden Aktionen aus:

      - **Größe angeben**

        Um eine Größe anzugeben, geben Sie im Feld **Größe des virtuellen** Datenträgers einen Wert ein, und wählen Sie dann die Einheiten (**MB**, **GB**oder **TB**) aus.

        Wenn Sie keine einfache Speicheranordnung verwenden, nutzt der virtuelle Datenträger mehr freien Speicher als die von Ihnen angegebene Größe. Um einen potenziellen Fehler zu vermeiden, wenn die Größe des Volumes den freien Speicher des Speicherpools überschreitet, können Sie das Kontrollkästchen **Datenträger mit maximal möglicher Größe erstellen (bis zur angegebenen Größe)** aktivieren.

      - **Maximale Größe**

        Wählen Sie diese Option, um einen virtuellen Datenträger zu erstellen, der die maximale Kapazität des Speicherpools nutzt.

10. Überprüfen Sie auf der Seite **Auswahl bestätigen** , ob die Einstellungen richtig sind, und wählen Sie dann **Erstellen**aus.

11. Überprüfen Sie auf der Seite **Ergebnisse anzeigen** , ob alle Aufgaben abgeschlossen sind, und wählen Sie dann **Schließen**aus.

    > [!TIP]
    > Das Kontrollkästchen **Volume erstellen, wenn dieser Assistent geschlossen wird** ist standardmäßig aktiviert. Daraufhin wird direkt zum nächsten Schritt weitergeleitet.

### <a name="windows-powershell-equivalent-commands-for-creating-virtual-disks"></a>Entsprechende Windows PowerShell-Befehle zum Erstellen von virtuellen Datenträgern

Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.

Im folgenden Beispiel wird 50 ein virtueller Datenträger mit dem Namen " *Bezeichnung virtualdisk1* " in einem Speicherpool mit dem Namen *StoragePool1*erstellt.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB)
```

Im folgenden Beispiel wird ein gespiegelter virtueller Datenträger mit dem Namen *Bezeichnung virtualdisk1* in einem Speicherpool namens *StoragePool1*erstellt. Der Datenträger verwendet die maximale Speicherkapazität des Speicherpools.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –ResiliencySettingName Mirror –UseMaximumSize
```

Im folgenden Beispiel wird ein virtueller Datenträger mit einer Größe von 50 GB mit dem Namen *Bezeichnung virtualdisk1* in einem Speicherpool mit dem Namen *StoragePool1*erstellt. Für den Datenträger wird der schlanke Bereitstellungstyp verwendet.

```PowerShell
New-VirtualDisk –StoragePoolFriendlyName StoragePool1 –FriendlyName VirtualDisk1 –Size (50GB) –ProvisioningType Thin
```

Im folgenden Beispiel wird ein virtueller Datenträger mit dem Namen *Bezeichnung virtualdisk1* in einem Speicherpool mit dem Namen *StoragePool1*erstellt. Der Datenträger nutzt die Drei-Wege-Spiegelung und hat eine feste Größe von 20 GB.

> [!NOTE]
> Damit dieses Cmdlet funktioniert, müssen mindestens fünf physische Datenträger im Speicherpool vorhanden sein. (Datenträger, die als Hotspares zugeteilt sind, sind davon ausgeschlossen.)

```PowerShell
New-VirtualDisk -StoragePoolFriendlyName StoragePool1 -FriendlyName VirtualDisk1 -ResiliencySettingName Mirror -NumberOfDataCopies 3 -Size 20GB -ProvisioningType Fixed
```

## <a name="step-3-create-a-volume"></a>Schritt 3: Erstellen eines Volumes

Als Nächstes erstellen Sie ein Volume aus dem virtuellen Datenträger. Sie können einen optionalen Laufwerk Buchstaben oder-Ordner zuweisen und dann das Volume mit einem Dateisystem formatieren.

1. Wenn der Assistent für neue Volumes nicht bereits geöffnet ist, klicken Sie in Server-Manager auf der Seite **Speicher Pools** unter **virtuelle**Datenträger mit der rechten Maustaste auf den gewünschten virtuellen Datenträger, und wählen Sie dann **Neues Volume**aus.

    Der Assistent für neue Volumes wird geöffnet.

2. Wählen Sie **auf der Seite** Vorbereitung die Option **weiter**aus.

3. Führen Sie auf der Seite **Server und** Datenträger auswählen die folgenden Schritte aus, und klicken Sie dann auf **weiter**.

    1. Wählen Sie im Bereich **Server** den Server aus, auf dem Sie das Volume bereitstellen möchten.

    2. Wählen Sie **im Bereich Datenträger den virtuellen** Datenträger aus, auf dem Sie das Volume erstellen möchten.

4. Geben Sie auf der Seite **Geben Sie die Größe des** Volumes an eine Volumegröße ein, geben Sie die Einheiten (**MB**, **GB**oder **TB**) an, und klicken Sie dann auf **weiter**.

5. Konfigurieren Sie auf der Seite **einem Laufwerk Buchstaben oder Ordner zuweisen** die gewünschte Option, und klicken Sie dann auf **weiter**.

6. Führen Sie auf der Seite **Datei Systemeinstellungen auswählen** die folgenden Schritte aus, und klicken Sie dann auf **weiter**.

    1. Wählen Sie in der Liste **Dateisystem** entweder **NTFS** oder **Refs**aus.

    2. In der Liste **Größe der Zuordnungseinheiten** behalten Sie entweder die Einstellung **Standard** bei, oder legen Sie eine Größe für die Zuordnungseinheiten fest.

        > [!NOTE]
        > Weitere Informationen zur Größe der Zuordnungseinheiten finden Sie unter [Default cluster size for NTFS, FAT, and exFAT](https://support.microsoft.com/help/140365/default-cluster-size-for-ntfs-fat-and-exfat).


    3. Sie können auch im Feld **Volumebezeichnung** einen Namen für das Volume eingeben, z. B. **HR Data**.

7. Überprüfen Sie auf der Seite **Auswahl bestätigen** , ob die Einstellungen richtig sind, und wählen Sie dann **Erstellen**aus.

8. Überprüfen Sie auf der Seite **Ergebnisse anzeigen** , ob alle Aufgaben abgeschlossen sind, und wählen Sie dann **Schließen**aus.

9. Wählen Sie in Server-Manager die Seite **Volumes** aus, um zu überprüfen, ob das Volume erstellt wurde. Das Volume wird unter dem Server aufgeführt, auf dem es erstellt wurde. Sie können auch prüfen, ob das Volume im Windows-Explorer zu finden ist.

### <a name="windows-powershell-equivalent-commands-for-creating-volumes"></a>Entsprechende Windows PowerShell-Befehle zum Erstellen von Volumes

Das folgende Windows PowerShell-Cmdlet führt die gleiche Funktion wie das vorherige Verfahren aus. Geben Sie den Befehl in einer einzelnen Zeile ein.

Im folgenden Beispiel werden die Datenträger für den virtuellen Datenträger *VirtualDisk1* initialisiert, eine Partition mit einem zugewiesenen Laufwerkbuchstaben wird erstellt, und das Volume wird dann mit dem Standard-NTFS-Dateisystem formatiert.

```PowerShell
Get-VirtualDisk –FriendlyName VirtualDisk1 | Get-Disk | Initialize-Disk –Passthru | New-Partition –AssignDriveLetter –UseMaximumSize | Format-Volume
```

## <a name="additional-information"></a>Zusätzliche Informationen

- [Speicherplätze](overview.md)
- [Speicher-Cmdlets in Windows PowerShell](/powershell/module/storage/index?view=win10-ps)
- [„Bereitstellen von Clusterspeicherplätzen“](/previous-versions/windows/it-pro/windows-server-2012-r2-and-2012/jj822937(v%3dws.11))
- [Windows Server-Speicher Forum](/answers/topics/windows-server-storage.html)
