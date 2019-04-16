---
title: "Datenträgerverwaltung: Problembehandlung"
description: "In diesem Artikel wird die Problembehandlung bei der Datenträgerverwaltung beschrieben"
ms.date: 10/12/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e4b361631799dccbc2b77fb5aa909052532a057d
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="troubleshooting-disk-management"></a>Datenträgerverwaltung: Problembehandlung

> **Gilt für**: Windows 10, Windows 8.1, Windows Server (Semi-Annual Channel), Windows Server 10, Windows Server8.1 R2, Windows Server 2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden einige allgemeine Probleme behandelt, die bei der Datenträgerverwaltung auftreten können.

<a id="BKMK_1"></a>

## <a name="partitions-on-basic-disks-added-to-the-system-do-not-appear-in-the-disk-management-volume-list-view"></a>Partitionen auf Basisfestplatten, die dem System hinzugefügt wurden, werden nicht in der Volumelistenansicht der Datenträgerverwaltung aufgeführt.

**Ursache:** Volumes auf Basisfestplatten, die dem System hinzugefügt werden, werden nicht automatisch bereitgestellt und erhalten nicht standardmäßig einen Laufwerkbuchstaben.
Dynamische Datenträger werden als **Fremd** angezeigt, wenn sie dem System hinzugefügt werden. Um die Volumes zu verwenden, importieren Sie die **fremden** Datenträger, und schalten Sie dann die Volumes **Online**.
Wechselmediengeräte (wie Zip-Laufwerke, Jaz-Laufwerke) und optische Datenträger (etwa CD-ROM und DVD-RAM) werden immer automatisch vom System bereitgestellt.

**Lösung:** Stellen Sie manuell die Basisvolumes bereit, indem Sie ihnen Laufwerkbuchstaben oder Bereitstellungspunkte mit der Datenträgerverwaltung oder mit den Befehlen [DiskPart](http://go.microsoft.com/fwlink/?LinkId=64110) oder [Mountvol](http://go.microsoft.com/fwlink/?LinkId=64111) zuweisen.

<a id="BKMK_2"></a>

## <a name="a-basic-disks-status-is-not-initialized"></a>Der Status einer Basisfestplatte lautet "Nicht initialisiert".

**Ursache:** Der Datenträger enthält keine gültige Signatur. Nach der Installation eines neuen Datenträgers muss das Betriebssystem eine Datenträgersignatur, die Markierung am Ende der Sektoren (auch „Signature Word” genannt) und einen Master Boot Record oder eine GUID-Partitionstabelle schreiben, bevor Sie auf dem Datenträger Partitionen erstellen kann. Wenn Sie nach der Installation eines neuen Datenträgers zuerst die Datenträgerverwaltung starten, wird ein Assistent angezeigt, der eine Liste mit den neuen Datenträgern enthält, die vom Betriebssystem erkannt werden. Wenn Sie den Assistenten abbrechen, bevor die Datenträgersignatur geschrieben wird, bleibt der Datenträgerstatus **Nicht initialisiert**.

**Lösung:** Den Datenträger initialisieren. Der Datenträgerstatus wechselt kurz zu **Initialisierung** und dann zu **Online**-Status. Weitere Informationen zum Initialisieren eines Datenträgers finden Sie unter [Neue Datenträger initialisieren](initialize-new-disks.md). 

<a id="BKMK_3"></a>

## <a name="a-basic-or-dynamic-disks-status-is-unreadable"></a>Der Status einer Basisfestplatte oder eines dynamischen Datenträgers lautet "Nicht lesbar".

**Ursache:** Auf den dynamischen Datenträger kann nicht zugegriffen werden, was möglicherweise durch einen Hardwarefehler, eine Beschädigung oder einen E/A-Fehler verursacht ist. Die Datenträgerkopie der Datenträgerkonfigurationsdatenbank des Systems ist möglicherweise beschädigt. Ein Fehlersymbol wird auf Datenträgern angezeigt mit dem Status **Unlesbar**.

Datenträger zeigen eventuell auch den Status **Unlesbar** an, während sie hochfahren oder wenn die Datenträgerverwaltung erneut alle Datenträger auf dem System scannt. In einigen Fällen ist bei einem nicht lesbaren Datenträger ein Fehler aufgetreten und kann nicht rückgängig gemacht werden. Bei dynamischen Datenträgern entsteht der Status **Unlesbar** normalerweise durch eine Beschädigung oder einen E/A-Fehler für einen Teil des Datenträgers, anstatt eines Ausfalls des gesamten Datenträgers.

**Lösung:** Scannen Sie die Datenträger erneut oder starten Sie den Computer erneut, um festzustellen, ob der Datenträgerstatus wechselt.

<a id="BKMK_4"></a>

## <a name="a-dynamic-disks-status-is-foreign"></a>Der Status eines dynamischen Datenträgers lautet "Fremd".

**Ursache:** Der Status **Fremd** wird angezeigt, wenn Sie einen dynamischen Datenträger von einem Computer mit Windows2000, Windows XP Professional, Windows XP 64-Bit-Edition oder einem Windows Server2003-Betriebssystem auf den lokalen Computer verschieben. Ein Warnsymbol wird auf Datenträgern angezeigt mit dem Status **Fremd**.

In einigen Fällen kann ein Datenträger, der bereits mit dem System verbunden war, den Status **Fremd** anzeigen. Konfigurationsdaten für dynamische Datenträger werden auf allen dynamischen Datenträgern gespeichert. Die Informationen darüber, welche Datenträger dem System angehören gehen daher verloren, wenn alle dynamischen Datenträger fehlschlagen.

**Lösung:** Fügen Sie den Datenträger zur Systemkonfiguration des Computers hinzu,, sodass Sie auf die Daten auf dem Datenträger zugreifen können. Um einen Datenträger zur Systemkonfiguration Ihres Computers hinzufügen, importieren Sie den fremden Datenträger (Klicken Sie mit der rechten Maustaste auf den Datenträger und dann auf **Fremde Datenträger importieren**). Alle vorhandenen Volumes auf dem fremden Datenträger werden sichtbar, wenn Sie den Datenträger importieren. 

<a id="BKMK_5"></a>

## <a name="a-dynamic-disks-status-is-online-errors"></a>Der Status eines dynamischen Datenträgers lautet "Online (Fehler)".

**Ursache:** Der dynamische Datenträger weist E/A-Fehler in einem Bereich des Datenträgers auf. Auf dem dynamischen Datenträger mit Fehlern wird ein Warnsymbol angezeigt.

**Lösung:** Wenn die E/A-Fehler nur vorübergehend auftreten, reaktivieren Sie den Datenträger erneut auf den **Online**-Status.

<a id="BKMK_6"></a>

## <a name="a-dynamic-disks-status-is-offline-or-missing"></a>Der Status eines dynamischen Datenträgers ist "Offline" oder "Fehlend".

**Ursache:** Ein als **Offline** aufgelisteter dynamischer Datenträger ist möglicherweise beschädigt oder vorübergehend nicht verfügbar. Ein Fehlersymbol wird auf dem offline aufgelisteten Datenträger angezeigt.

Wenn der Datenträgerstatus **Offline** ist und sich der Status der Festplatte auf **Fehlt** ändert, war der Datenträger vor kurzem auf dem System noch verfügbar, befindet sich aber dort nicht mehr oder kann nicht mehr identifiziert werden. Der fehlende Datenträger ist möglicherweise beschädigt, ausgeschaltet oder getrennt.

**Lösung:** So bringen Sie einen Datenträger der „Offline” oder „Fehlend” ist wieder Online:
1. Beheben Sie alle Datenträger-, Controller- oder Kabelprobleme. 
2. Stellen Sie sicher, dass die physische Festplatte eingeschaltet, eingesteckt oder mit dem Computer verbunden ist. 
3. Verwenden Sie anschließend den Befehl **Datenträger reaktivieren**, um den Datenträger wieder online zu schalten.

4. Wenn der Datenträger weiterhin den Status **Offline** anzeigt und der Datenträgername **Fehlt** und Sie feststellen, dass der Datenträger ein Problem hat, das nicht repariert werden kann, entfernen Sie den Datenträger aus dem System. Klicken Sie mit der rechten Maustaste auf den Datenträger, und klicken Sie dann auf **Entfernen eines Datenträgers**. Bevor Sie den Datenträger entfernen können, müssen Sie jedoch alle Volumes (oder Spiegel) auf dem Datenträger löschen. Sie können alle gespiegelten Volumes auf dem Datenträger durch das Entfernen der Spiegelung, anstatt des gesamten Volumes speichern. Das Löschen eines Volumes löscht alle Daten auf dem Datenträger, daher sollten Sie einen Datenträger nur dann entfernen, wenn Sie absolut sicher sind, dass der Datenträger verloren ist.

**Um einen Datenträger zurückzubringen, der offline ist und weiterhin den Namen Datenträger \# hat (nicht "Fehlend") führen Sie eine oder mehrere der folgenden Verfahren durch:**

1. Klicken Sie mit der rechten Maustaste in der Datenträgerverwaltung auf die Festplatte, und klicken Sie dann auf **Festplatte reaktivieren**, um die Festplatte in den Status "Online" zurückzuversetzen. Wenn der Datenträger weiterhin den Status **Offline** anzeigt, überprüfen Sie die Kabel und den Controller, und stellen Sie sicher, dass der physische Datenträger fehlerfrei ist. Beheben Sie alle Probleme, und versuchen Sie, den Datenträger erneut zu reaktivieren. Wenn eine erneute Aktivierung auf dem Datenträger erfolgreich ist, sollten alle Volumes auf dem Datenträger automatisch den Status **Fehlerfrei** anzeigen.
2. Überprüfen Sie in der Ereignisanzeigealle Fehler in Bezug auf Datenträger wie "No good config copies". Wenn diese Fehler im Ereignisprotokoll angezeigt werden, wenden Sie sich an [Microsoft Product Support Services](https://msdn.microsoft.com/library/aa263468(v=vs.60).aspx).

3. Versuchen Sie, den Datenträger auf einen anderen Computer zu verschieben. Wenn Sie den Datenträger auf **Online** auf einem anderen Computer wechseln können, liegt das Problem wahrscheinlich an der Konfiguration des Computers, auf dem der Datenträger nicht **Online** geht.

4. Versuchen Sie, die Datenträger auf einen anderen Computer mit dynamischen Datenträgern zu verschieben. Importieren Sie den Datenträger auf den Computer, und verschieben Sie den Datenträger zurück auf den Computer, auf den er nicht **Online** schalten konnte. 

<a id="BKMK_7"></a>

## <a name="a-basic-or-dynamic-volumes-status-is-failed"></a>Der Status eines dynamischen Volumes lautet "Fehlerhaft".

**Ursache:** Das Basis-oder dynamische Volume kann nicht automatisch gestartet werden, der Datenträger ist beschädigt oder das Dateisystem ist beschädigt. Außer wenn der Datenträger bzw. das Dateisystem repariert werden kann, bedeutet der **Fehler**-Status ein Verlust der Daten.

**Lösung:** Wenn das Volume ein Basisvolumes mit dem Status **Fehler** ist:

-   Stellen Sie sicher, dass die zugrunde liegende physische Festplatte eingeschaltet, eingesteckt oder mit dem Computer verbunden ist. Auf Basisvolumes ist keine weitere Aktion des Benutzers möglich.

    Wenn das Volume ein dynamisches Volumes mit dem Status **Fehler** ist: 
-   Stellen Sie sicher, dass die zugrunde liegenden Datenträger online sind. Falls nicht, schalten Sie den Datenträger auf den Status **Online**. Wenn dies erfolgreich ist, startet das Volume automatisch neu und gibt den Status **Fehlerfrei** an. Wenn der dynamische Datenträger wieder den Status **Online** anzeigt, aber die dynamischen Volumes nicht auf den Status **Fehlerfrei** zurückkehren, können Sie das Volume manuell erneut reaktivieren. 
    
-   Wenn der dynamische Datenträger ein gespiegeltes oder RAID-5-Volume mit veralteten Daten ist, startet das Schalten des zugrunde liegenden Datenträgers auf online nicht automatisch das Volume erneut. Wenn die Datenträger, die die aktuellen Daten enthalten, getrennt werden, bringen Sie diese Datenträger zuerst auf den Status Online (damit die Daten synchronisiert werden können). Starten Sie andernfalls das gespiegelte oder RAID-5-Volume manuell, und führen Sie dann das Tool zur Fehlerüberprüfung oder Chkdsk.exe aus.

<a id="BKMK_8"></a>

## <a name="a-basic-or-dynamic-volumes-status-is-unknown"></a>Der Status einer Basisfestplatte oder eines dynamischen Datenträgers lautet "Unbekannt".

**Ursache:** Der Status **Unbekannt** wird angezeigt, wenn der Startsektor für das Volume beschädigt ist (z.B. durch einen Virus) und Sie nicht mehr auf die Daten auf dem Volume zugreifen können. Der Status **Unbekannt** wird angezeigt, wenn Sie einen neuen Datenträger installieren und der Assistent zum Erstellen einer Datenträgersignatur nicht erfolgreich abgeschlossen wurde.

**Lösung:** Den Datenträger initialisieren. Anweisungen finden Sie unter [Neue Datenträger initialisieren](initialize-new-disks.md). 

<a id="BKMK_9"></a>

## <a name="a-dynamic-volumes-status-is-data-incomplete"></a>Der Status eines dynamischen Volumes lautet "Die Daten sind nicht vollständig".

**Ursache:** Sie haben einige, jedoch nicht alle Datenträger auf einem Volume mit mehreren Datenträgern verschoben. Daten auf diesem Volume werden zerstört, es sei denn, Sie verschieben und importieren die verbleibenden Datenträger, die dieses Volume enthalten.

**Lösung:**  
1. Verschieben Sie alle Datenträger, die das Volume mit mehreren Datenträgern auf dem Computer enthalten.

2. Importieren der Datenträger. Informationen zum Verschieben und Importieren von Datenträgern finden Sie unter [Datenträger auf einen anderen Computer verschieben](move-disks-to-another-computer.md).

Wenn Sie das Volume mit mehreren Datenträgern nicht mehr benötigen, können Sie den Datenträger importieren und neue Volumes erstellen. Gehen Sie hierzu wie folgt vor: 

1. Klicken Sie mit der rechten Maustaste auf das Volume mit dem Status **Fehler** oder **Fehlerhafte Redundanz** und klicken Sie dann auf **Volume löschen**. 

2. Klicken Sie mit der rechten Maustaste auf den Datenträger, und klicken Sie dann auf **Neues Volume**.

<a id="BKMK_10"></a>

## <a name="a-dynamic-volumes-status-is-healthy-at-risk"></a>Der Status eines dynamischen Volumes lautet "Fehlerfrei (Risiko)".

**Ursache:** Dies weist darauf hin, dass das auf dynamische Volume zugegriffen werden kann, aber auf dem zugrunde liegenden dynamischen Datenträger E/A-Fehler erkannt wurden. Wenn ein E/A-Fehler auf einem beliebigen Teil eines dynamischen Datenträgers erkannt wird, zeigen alle Volumes auf dem Datenträger den Status **Fehlerfrei (Risiko)** und ein Warnsymbol wird auf dem Volume angezeigt.

Wenn der Status des Volumes **Fehlerfrei (Risiko)**ist, ist der zugrunde liegende Status des Datenträgers in der Regel **Online (Fehler)**.

**Lösung:**  
1. Schalten Sie den zugrunde liegenden Datenträger auf den Status **Online**. Sobald der Datenträger wieder den Status **Online** anzeigt, sollte das Volume wieder den Status **Fehlerfrei** anzeigen. Wenn der Status **Fehlerfrei (Risiko)** weiterhin auftritt, kann der Datenträger beschädigt sein. 

2. Sichern Sie die Daten und ersetzen Sie den Datenträger so bald wie möglich. 

<a id="BKMK_11"></a>

## <a name="cannot-manage-striped-volumes-using-disk-management-or-diskpart"></a>Die Verwaltung eines Stripeset-Volumes mithilfe der Datenträgerverwaltung oder DiskPart ist nicht möglich.

**Ursache:** Einige nicht von Microsoft entwickelten Verwaltungsprodukte ersetzen Microsoft Logical Disk Manager (LDM) für die erweiterte Datenträgerverwaltung, die LDM deaktiviert können.

**Lösung:** Wenn Sie nicht von Microsoft entwickelte Datenträgerverwaltungssoftware verwenden, die LDM deaktiviert, müssen Sie den Anbieter der nicht von Microsoft entwickelten Datenträgerverwaltungssoftware zur Unterstützung bei der Behandlung von Problemen mit der Datenträgerkonfiguration kontaktieren.

<a id="BKMK_virtdisk"></a>

## <a name="disk-management-cannot-start-the-virtual-disk-service"></a>Die Datenträgerverwaltung kann den Dienst für virtuelle Datenträger nicht starten.

**Ursache:** Wenn ein Remotecomputer Virtual Disk Service (VDS) nicht unterstützt oder wenn Sie keine Verbindung zum Remotecomputer herstellen können, da sie von Windows-Firewall blockiert wird, können Sie diesen Fehler erhalten.

**Lösung:**  
1. Wenn der Remotecomputer VDS unterstützt, können Sie Windows Defender Firewall konfigurieren, um eine VDS-Verbindungen zuzulassen. Wenn der Remotecomputer VDS nicht unterstützt, können Sie mit der Remotedesktopverbindung eine Verbindung herstellen, und die Datenträgerverwaltung direkt auf dem Remotecomputer ausführen.

2. Zum Verwalten von Datenträgern auf Remotecomputern, die VDS unterstützen, müssen Sie die Windows Defender Firewall auf dem lokalen Computer (auf dem der Datenträger ausgeführt wird) und dem Remotecomputer konfigurieren.

3. Konfigurieren Sie auf dem lokalen Computer Windows Defender Firewall und aktivieren Sie die Remotevolumeverwaltungsausnahme.

<br />

> [!NOTE]
> Die Remotevolumeverwaltungsausnahme enthält Ausnahmen für Vds.exe, Vdsldr.exe und TCP-Port 135.

<br />

 > [!NOTE]
 > Remoteverbindungen in Arbeitsgruppen werden nicht unterstützt. Sowohl der lokale Computer als auch der Remotecomputer müssen Domänenmitglieder sein.