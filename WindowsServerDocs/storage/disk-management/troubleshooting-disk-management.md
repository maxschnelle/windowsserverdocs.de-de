---
title: 'Datenträgerverwaltung: Problembehandlung'
description: In diesem Artikel wird die Problembehandlung bei der Datenträgerverwaltung beschrieben
ms.date: 12/22/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c234828706d999fe049626a2fd98db70e612766f
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192738"
---
# <a name="troubleshooting-disk-management"></a>Datenträgerverwaltung: Problembehandlung

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012

In diesem Thema werden einige allgemeine Probleme behandelt, die bei der Datenträgerverwaltung auftreten können.

> [!TIP]
> Wenn Sie eine Fehlermeldung erhalten oder etwas nicht funktioniert, befolgen Sie diese Prozeduren: keine Panik! Auf eine Fülle von Informationen ist die [Microsoft-Community](https://answers.microsoft.com/en-us/windows) site – suchen Sie die [Dateien, Ordner und Speicher](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) aus, und wenn Sie weitere Hilfe benötigen, senden, gibt es eine Frage und von Microsoft oder anderen Mitgliedern der der Community versucht, die helfen. Wenn Sie Feedback zum Verbessern der in diesen Themen haben, wir würden uns über Ihre anregungen! Beantworten Sie einfach die *ist diese Seite hilfreich?* Eingabeaufforderung ein, und lassen Sie alle Kommentare, dort oder aber in der öffentlichen Kommentare Thread am Ende dieses Themas.

## <a name="a-disks-status-is-not-initialized-or-the-disk-is-missing"></a>Der Status eines Datenträgers ist nicht initialisiert oder der Datenträger ist nicht vorhanden

![Datenträgerverwaltung, die mit einer unbekannten Datenträger, der initialisiert werden muss.](media\uninitialized-disk.PNG)

**Ursache:** Wenn Sie einen Datenträger verfügen, die nicht im Datei-Explorer angezeigt, und finden Sie in der Datenträgerverwaltung als *nicht initialisiert*, möglicherweise weil der Datenträger nicht über eine gültige Datenträger-Signatur verfügt. Im Grunde bedeutet dies, dass der Datenträger nicht initialisiert und formatiert wurde, oder die Formatierung des Laufwerks irgendwie beschädigt wurde. 

Es ist auch möglich, dass sich Hardware- oder Probleme, die unter Verwendung des Datenträgers hat, aber wir dazu kommen in einigen Abschnitten.

**Lösung:**   die Lösung ist einfach, wenn das Laufwerk ist ein völlig neues, und nur werden, löschen alle Daten darauf initialisiert muss – Siehe [neue Datenträger initialisieren](initialize-new-disks.md). Allerdings besteht eine hohe Wahrscheinlichkeit, die Sie dies bereits versucht haben, und es funktioniert nicht. Oder vielleicht haben Sie einen der Datenträger ist voll, wichtiger Dateien und nicht den Datenträger initialisieren Sie sie löschen möchten.

Es gibt eine Reihe von Gründen, die ein Datenträger fehlt oder nicht initialisiert, wobei eine häufige Ursache, weil der Datenträger fehlerhaft ist, kann, ein. Nur so viele, die Sie tun können, um eine fehlerhafte Festplatte zu beheben, aber hier sind einige Schritte, um zu versuchen, festzustellen, ob wir behoben werden können. Funktioniert Sie der Datenträger nach einem der folgenden Schritte aus, nicht kümmern Sie sich den nächsten Schritten, einfach wieder starten Sie, zu Feiern Sie und vielleicht aktualisieren Sie Ihrer Sicherungen.

1. Betrachten Sie den Datenträger in der Datenträgerverwaltung aus. Wenn anscheinend *Offline* wie hier gezeigt, versuchen Sie es rechtsklickt und **Online**.

    ![Datenträger, die als offline angezeigt](media/offline-disk.png)
1. Wenn der Datenträger wird, in der Datenträgerverwaltung als angezeigt *Online*, und verfügt über eine primäre Partition, die als aufgeführt ist *fehlerfrei*, wie dargestellt, das ist hier ein gutes Zeichen.

    ![Dargestellt als online über einen fehlerfreien Datenträger](media/healthy-volume.png)
    - Wenn die Partition ein Dateisystem, aber kein Laufwerkbuchstabe (z. B. "e:") verfügt, finden Sie unter [ändern Sie einen Laufwerkbuchstaben](change-a-drive-letter.md) einen Laufwerkbuchstaben manuell hinzufügen.
    - Wenn kein Dateisystem (NTFS, ReFS, FAT32 oder ExFAT) und Sie wissen, der Datenträger ist leer, mit der rechten Maustaste in der Partitions, und wählen **Format**. Formatieren eines Datenträgers löscht alle Daten auf, sodass dies nicht tun, wenn Sie versuchen, zum Wiederherstellen von Dateien vom Datenträger - stattdessen mit dem nächsten Schritt fortfahren.
1. Wenn Sie über eine externe Festplatte, und trennen Sie den Datenträger verfügen, schließen Sie ihn, und wählen Sie dann **Aktion** > **Datenträger neu einlesen**. 
2. Herunterfahren auf Ihrem PC, deaktivieren Sie die externe Festplatte (sofern es sich um einen externen Datenträger mit einer Netzkabel ist), und klicken Sie dann Ihren PC und der Datenträger wieder aktivieren.
    Um Ihren PC unter Windows 10 zu deaktivieren, wählen Sie die Schaltfläche "Start", wählen Sie den Netzschalter betätigen, und wählen Sie dann **Herunterfahren**.
1. Schließen Sie den Datenträger an einen anderen USB-Anschluss, der direkt auf Ihrem PC (nicht auf einen Hub) ist.
    Manchmal USB-Datenträger nicht genügend Leistung erhalten, von einigen Ports oder andere Probleme mit bestimmten Ports. Dies ist besonders häufig bei USB-Hubs, aber manchmal bestehen die Unterschiede zwischen Ports auf einem PC, also ein paar unterschiedliche Ports versuchen, sie haben.
1. Versuchen Sie es ein anderes Kabel.
    Es klingt vielleicht verrückte, aber das Kabel viel fehl, so dass Sie möglicherweise mit einem anderen Kabel, geben Sie den Datenträger. Wenn Sie einen internen Datenträger in einem desktop-PC haben, müssen Sie wahrscheinlich Ihre PCs vor dem Wechseln der Kabel heruntergefahren: finden in der Dokumentation Ihres Computers für.
1. Überprüfen Sie Geräte-Manager Probleme.
    Drücken Sie und halten Sie die Schaltfläche "Start", und wählen Sie dann im Kontextmenü der Geräte-Manager (oder mit der rechten Maustaste). Suchen Sie nach Geräten mit einem Ausrufezeichen neben sie oder andere Probleme, doppelklicken Sie auf dem Gerät, und klicken Sie dann lesen Sie den Status zu.

    Es folgt eine Liste der [Fehlercodes im Geräte-Manager](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows), aber wählen Sie einen Ansatz, der manchmal funktioniert mit der rechten Maustaste das Gerät problematische **deinstallieren Gerät**, und klicken Sie dann **Aktion**  >  **Nach geänderter Hardware suchen**.
    ![Geräte-Manager ein unbekanntes USB-Gerät anzeigt](media\device-manager.PNG)
1. Schließen Sie den Datenträger in einem anderen PC aus.
    
    Wenn der Datenträger auf einem anderen PC nicht funktioniert, ist es ein guten Zeichen dafür, die es ist ein Fehler mit dem Datenträger und nicht auf Ihrem PC passiert. Absolut keinen Spaß, wissen wir. Es gibt einige weitere Schritte Sie, in versuchen können [externe USB-Laufwerk Fehler "Sie müssen den Datenträger initialisieren, bevor Logical Disk Manager darauf zugreifen können"](https://social.technet.microsoft.com/Forums/windows/en-US/2b069948-82e9-49ef-bbb7-e44ec7bfebdb/forum-faq-external-usb-drive-error-you-must-initialize-the-disk-before-logical-disk-manager-can?forum=w7itprohardware), kann es sein, Zeit zu suchen, und bitten Sie um Hilfe bei der [fürMicrosoft-Community](https://answers.microsoft.com/en-us/windows) -Website oder wenden Sie sich an den Datenträgerhersteller Ihres.

    Wenn Sie nur funktioniert nicht, es gibt auch apps, die beim Wiederherstellen von Daten aus der fehlerhaften Festplatte ausprobieren können, oder wenn die Dateien wirklich wichtig sind, können Sie ein Lab Daten Recovery, um zu versuchen, sie wiederherzustellen bezahlen. Wenn Sie etwas, das funktioniert für Sie feststellen, teilen Sie uns im Kommentarabschnitt unten.

> [!IMPORTANT]
> Datenträger ein recht häufig Fehler auf, daher es wichtig ist, alle Dateien regelmäßig zu sichern, die, denen Sie interessieren. Wenn Sie einen Datenträger, der manchmal nicht angezeigt wird, oder Fehler meldet verfügen, berücksichtigen Sie dies auf eine Erinnerung, überprüfen Sie Ihre backup-Methoden. Es ist in Ordnung, wenn Sie ein wenig hinter sind – alle vorhanden schon. Die beste Lösung für die Sicherung ist, die Sie verwenden, damit wir Ihnen empfehlen, die für Sie gefunden, die funktioniert und bleiben Sie dabei.

> [!TIP]
Informationen dazu, wie Sie apps, die in Windows integriert sind, zum Sichern von Dateien auf einem externen Laufwerk wie z. B. ein USB-Laufwerk verwenden, finden Sie unter [sichern und Wiederherstellen von Dateien](https://support.microsoft.com/help/17143/windows-10-back-up-your-files). Sie können auch Dateien in Microsoft OneDrive speichern, die Dateien von Ihrem PC in die Cloud synchronisiert. Wenn es sich bei einem Festplattenausfall, bleibe Sie erhalten alle Dateien, die Sie in OneDrive aus OneDrive.com speichern können. Weitere Informationen finden Sie unter [OneDrive auf Ihrem PC](https://support.microsoft.com/help/17184/windows-10-onedrive).

## <a name="a-basic-or-dynamic-disks-status-is-unreadable"></a>Status eines dynamischen Datenträgers lautet nicht lesbar

**Ursache:**  der einfache oder dynamische Datenträger kann nicht zugegriffen werden, und möglicherweise ausgefallen, Hardwarefehler, Beschädigung oder e/a-Fehler. Die Datenträgerkopie der Datenträgerkonfigurationsdatenbank des Systems ist möglicherweise beschädigt. Ein Fehlersymbol wird auf Datenträgern angezeigt mit dem Status **Unlesbar**.

Datenträger zeigen eventuell auch den Status **Unlesbar** an, während sie hochfahren oder wenn die Datenträgerverwaltung erneut alle Datenträger auf dem System scannt. In einigen Fällen ist bei einem nicht lesbaren Datenträger ein Fehler aufgetreten und kann nicht rückgängig gemacht werden. Bei dynamischen Datenträgern entsteht der Status **Unlesbar** normalerweise durch eine Beschädigung oder einen E/A-Fehler für einen Teil des Datenträgers, anstatt eines Ausfalls des gesamten Datenträgers.

**Lösung:**  die Datenträger neu einlesen und Neustarten des Computers aus, um festzustellen, ob der Datenträgerstatus ändert. Versuchen Sie außerdem die Schritte zur Problembehandlung, die in beschriebenen [der Status eines Datenträgers ist nicht initialisiert oder der Datenträger fehlt vollständig](#a-disks-status-is-not-initialized-or-the-disk-is-missing).

## <a name="a-dynamic-disks-status-is-foreign"></a>Status eines dynamischen Datenträgers lautet "Fremd"

**Ursache:**  der **Fremd** Status angezeigt, wenn Sie einen dynamischen Datenträger auf dem lokalen Computer von einem anderen Computer PC verschieben. Ein Warnsymbol wird auf Datenträgern angezeigt mit dem Status **Fremd**.

In einigen Fällen kann ein Datenträger, der bereits mit dem System verbunden war, den Status **Fremd** anzeigen. Konfigurationsdaten für dynamische Datenträger werden auf allen dynamischen Datenträgern gespeichert. Die Informationen darüber, welche Datenträger dem System angehören gehen daher verloren, wenn alle dynamischen Datenträger fehlschlagen.

**Lösung:**  Systemkonfiguration des Computers, damit Sie Daten auf dem Datenträger zugreifen können den Datenträger hinzugefügt. Um einen Datenträger zur Systemkonfiguration Ihres Computers hinzufügen, importieren Sie den fremden Datenträger (Klicken Sie mit der rechten Maustaste auf den Datenträger und dann auf **Fremde Datenträger importieren**). Alle vorhandenen Volumes auf dem fremden Datenträger werden sichtbar, wenn Sie den Datenträger importieren. 

## <a name="a-dynamic-disks-status-is-online-errors"></a>Status eines dynamischen Datenträgers lautet "Online (Fehler)"

**Ursache:**  der dynamische Datenträger verfügt über e/a-Fehler in einem Bereich des Datenträgers. Auf dem dynamischen Datenträger mit Fehlern wird ein Warnsymbol angezeigt.

**Lösung:**   , wenn die e/a-Fehler nur vorübergehend auftreten, reaktivieren Sie den Datenträger aus, um damit zurückzugeben **Online** Status.

## <a name="a-dynamic-disks-status-is-offline-or-missing"></a>Status eines dynamischen Datenträgers ist Offline oder nicht vorhanden

**Ursache:**  ein **Offline** dynamischer Datenträger ist möglicherweise beschädigt oder vorübergehend nicht verfügbar. Ein Fehlersymbol wird auf dem offline aufgelisteten Datenträger angezeigt.

Wenn der Datenträgerstatus **Offline** ist und sich der Status der Festplatte auf **Fehlt** ändert, war der Datenträger vor kurzem auf dem System noch verfügbar, befindet sich aber dort nicht mehr oder kann nicht mehr identifiziert werden. Der fehlende Datenträger ist möglicherweise beschädigt, ausgeschaltet oder getrennt.

**Lösung:** Um einen Datenträger zu bringen, der Offline und nicht über wieder online ist:

1. Beheben Sie alle Datenträger-, Controller- oder Kabelprobleme. 
2. Stellen Sie sicher, dass die physische Festplatte eingeschaltet, eingesteckt oder mit dem Computer verbunden ist. 
3. Verwenden Sie anschließend den Befehl **Datenträger reaktivieren**, um den Datenträger wieder online zu schalten.
4. Wiederholen Sie die Schritte zur Problembehandlung, die in beschriebenen [der Status eines Datenträgers ist nicht initialisiert oder der Datenträger fehlt vollständig](#a-disks-status-is-not-initialized-or-the-disk-is-missing).
5. Wenn der Datenträger weiterhin den Status **Offline** anzeigt und der Datenträgername **Fehlt** und Sie feststellen, dass der Datenträger ein Problem hat, das nicht repariert werden kann, entfernen Sie den Datenträger aus dem System. Klicken Sie mit der rechten Maustaste auf den Datenträger, und klicken Sie dann auf **Entfernen eines Datenträgers**. Bevor Sie den Datenträger entfernen können, müssen Sie jedoch alle Volumes (oder Spiegel) auf dem Datenträger löschen. Sie können alle gespiegelten Volumes auf dem Datenträger durch das Entfernen der Spiegelung, anstatt des gesamten Volumes speichern. Das Löschen eines Volumes löscht alle Daten auf dem Datenträger, daher sollten Sie einen Datenträger nur dann entfernen, wenn Sie absolut sicher sind, dass der Datenträger verloren ist.

**Um einen Datenträger zu bringen, die Offline und ist immer noch mit dem Namen Datenträger \# (nicht "fehlt") wieder online, versuchen Sie eine oder mehrere der folgenden Verfahren:**

1. Klicken Sie mit der rechten Maustaste in der Datenträgerverwaltung auf die Festplatte, und klicken Sie dann auf **Festplatte reaktivieren**, um die Festplatte in den Status "Online" zurückzuversetzen. Wenn der Datenträger weiterhin den Status **Offline** anzeigt, überprüfen Sie die Kabel und den Controller, und stellen Sie sicher, dass der physische Datenträger fehlerfrei ist. Beheben Sie alle Probleme, und versuchen Sie, den Datenträger erneut zu reaktivieren. Wenn eine erneute Aktivierung auf dem Datenträger erfolgreich ist, sollten alle Volumes auf dem Datenträger automatisch den Status **Fehlerfrei** anzeigen.
2. Überprüfen Sie in der Ereignisanzeigealle Fehler in Bezug auf Datenträger wie "No good config copies". Wenn diese Fehler im Ereignisprotokoll angezeigt werden, wenden Sie sich an [Microsoft Product Support Services](https://msdn.microsoft.com/library/aa263468(v=vs.60).aspx).

3. Versuchen Sie, den Datenträger auf einen anderen Computer zu verschieben. Wenn Sie den Datenträger auf **Online** auf einem anderen Computer wechseln können, liegt das Problem wahrscheinlich an der Konfiguration des Computers, auf dem der Datenträger nicht **Online** geht.

4. Versuchen Sie, die Datenträger auf einen anderen Computer mit dynamischen Datenträgern zu verschieben. Importieren Sie den Datenträger auf den Computer, und verschieben Sie den Datenträger zurück auf den Computer, auf den er nicht **Online** schalten konnte. 

## <a name="a-basic-or-dynamic-volumes-status-is-failed"></a>Status eines dynamischen Volumes ist fehlgeschlagen.

**Ursache:**   der dynamischen Volumes nicht automatisch gestartet werden, der Datenträger ist beschädigt oder das Dateisystem beschädigt ist. Außer wenn der Datenträger bzw. das Dateisystem repariert werden kann, bedeutet der **Fehler**-Status ein Verlust der Daten.

**Lösung:**

Wenn das Volume eines Basisvolumes mit ist **Fehler** Status:

- Stellen Sie sicher, dass die zugrunde liegende physische Festplatte eingeschaltet, eingesteckt oder mit dem Computer verbunden ist.
- Wiederholen Sie die Schritte zur Problembehandlung, die in beschriebenen [der Status eines Datenträgers ist nicht initialisiert oder der Datenträger fehlt vollständig](#a-disks-status-is-not-initialized-or-the-disk-is-missing).

Wenn das Volume ein dynamisches Volumes mit dem Status **Fehler** ist:

-   Stellen Sie sicher, dass die zugrunde liegenden Datenträger online sind. Falls nicht, schalten Sie den Datenträger auf den Status **Online**. Wenn dies erfolgreich ist, startet das Volume automatisch neu und gibt den Status **Fehlerfrei** an. Wenn der dynamische Datenträger wieder den Status **Online** anzeigt, aber die dynamischen Volumes nicht auf den Status **Fehlerfrei** zurückkehren, können Sie das Volume manuell erneut reaktivieren.
-   Wenn der dynamische Datenträger ein gespiegeltes oder RAID-5-Volume mit veralteten Daten ist, startet das Schalten des zugrunde liegenden Datenträgers auf online nicht automatisch das Volume erneut. Wenn die Datenträger, die die aktuellen Daten enthalten, getrennt werden, bringen Sie diese Datenträger zuerst auf den Status Online (damit die Daten synchronisiert werden können). Starten Sie andernfalls das gespiegelte oder RAID-5-Volume manuell, und führen Sie dann das Tool zur Fehlerüberprüfung oder Chkdsk.exe aus.
- Wiederholen Sie die Schritte zur Problembehandlung, die in beschriebenen [der Status eines Datenträgers ist nicht initialisiert oder der Datenträger fehlt vollständig](#a-disks-status-is-not-initialized-or-the-disk-is-missing).

## <a name="a-basic-or-dynamic-volumes-status-is-unknown"></a>Status eines dynamischen Volumes lautet "Unbekannt"

**Ursache:**   der **unbekannte** Status angezeigt, wenn der Bootsektor, für das Volume (möglicherweise aufgrund eines Virus) beschädigt ist, und Sie können Daten auf dem Volume nicht mehr zugreifen. Der Status **Unbekannt** wird angezeigt, wenn Sie einen neuen Datenträger installieren und der Assistent zum Erstellen einer Datenträgersignatur nicht erfolgreich abgeschlossen wurde.

**Lösung**  den Datenträger zu initialisieren. Anweisungen finden Sie unter [Neue Datenträger initialisieren](initialize-new-disks.md).

## <a name="a-dynamic-volumes-status-is-data-incomplete"></a>Status eines dynamischen Volumes ist Daten unvollständig

**Ursache:** Sie einige verschoben, aber nicht alle Datenträger auf einem Volume mit mehreren Datenträgern. Daten auf diesem Volume werden zerstört, es sei denn, Sie verschieben und importieren die verbleibenden Datenträger, die dieses Volume enthalten.

**Lösung:**

1. Verschieben Sie alle Datenträger, die das Volume mit mehreren Datenträgern auf dem Computer enthalten.
2. Importieren der Datenträger. Informationen zum Verschieben und Importieren von Datenträgern finden Sie unter [Datenträger auf einen anderen Computer verschieben](move-disks-to-another-computer.md).

Wenn Sie das Volume mit mehreren Datenträgern nicht mehr benötigen, können Sie den Datenträger importieren und neue Volumes erstellen. Gehen Sie hierzu wie folgt vor:

1. Klicken Sie mit der rechten Maustaste auf das Volume mit dem Status **Fehler** oder **Fehlerhafte Redundanz** und klicken Sie dann auf **Volume löschen**.
2. Klicken Sie mit der rechten Maustaste auf den Datenträger, und klicken Sie dann auf **Neues Volume**.

## <a name="a-dynamic-volumes-status-is-healthy-at-risk"></a>Status eines dynamischen Volumes ist fehlerfrei (Risiko)

**Ursache:**   gibt an, dass das dynamische Volume derzeit verfügbar ist, aber auf dem zugrunde liegenden dynamischen Datenträger e/a-Fehler erkannt wurden. Wenn ein E/A-Fehler auf einem beliebigen Teil eines dynamischen Datenträgers erkannt wird, zeigen alle Volumes auf dem Datenträger den Status **Fehlerfrei (Risiko)** und ein Warnsymbol wird auf dem Volume angezeigt.

Wenn der Status des Volumes **Fehlerfrei (Risiko)** ist, ist der zugrunde liegende Status des Datenträgers in der Regel **Online (Fehler)** .

**Lösung:**  
1. Schalten Sie den zugrunde liegenden Datenträger auf den Status **Online**. Sobald der Datenträger wieder den Status **Online** anzeigt, sollte das Volume wieder den Status **Fehlerfrei** anzeigen. Wenn der Status **Fehlerfrei (Risiko)** weiterhin auftritt, kann der Datenträger beschädigt sein. 

2. Sichern Sie die Daten und ersetzen Sie den Datenträger so bald wie möglich. 

## <a name="cannot-manage-striped-volumes-using-disk-management-or-diskpart"></a>Mithilfe der Datenträgerverwaltung oder DiskPart Stripesetvolumes können nicht verwaltet werden.

**Ursache:**   Verwaltungsprodukte für einige nicht-Microsoft-Datenträger ersetzt Microsoft Logical Disk Manager (LDM) für die erweiterte datenträgerverwaltung, bei denen die LDM deaktiviert werden kann.

**Lösung:**   , wenn Sie Verwaltungssoftware für nicht-Microsoft-Datenträger verwenden, die LDM deaktiviert hat, Sie müssen Hersteller des für die Datenträger für nicht-Microsoft-Verwaltungssoftware und Unterstützung bei der Behandlung von Problemen mit dem Datenträger die Konfiguration.

## <a name="disk-management-cannot-start-the-virtual-disk-service"></a>Datenträgerverwaltung kann nicht Dienst für virtuelle Datenträger gestartet werden.

**Ursache:**   Wenn auf ein Remotecomputer Virtual Disk Service (VDS) nicht unterstützt, oder wenn Sie eine Verbindung mit dem Remotecomputer herstellen können, weil er von der Windows-Firewall blockiert wird, Sie diesen Fehler erhalten können.

**Lösung:**

1. Wenn der Remotecomputer VDS unterstützt, können Sie Windows Defender Firewall konfigurieren, um eine VDS-Verbindungen zuzulassen. Wenn der Remotecomputer VDS nicht unterstützt, können Sie mit der Remotedesktopverbindung eine Verbindung herstellen, und die Datenträgerverwaltung direkt auf dem Remotecomputer ausführen.
2. Zum Verwalten von Datenträgern auf Remotecomputern, die VDS unterstützen, müssen Sie die Windows Defender Firewall auf dem lokalen Computer (auf dem der Datenträger ausgeführt wird) und dem Remotecomputer konfigurieren.
3. Konfigurieren Sie auf dem lokalen Computer Windows Defender Firewall und aktivieren Sie die Remotevolumeverwaltungsausnahme.


> [!NOTE]
> Die Remotevolumeverwaltungsausnahme enthält Ausnahmen für Vds.exe, Vdsldr.exe und TCP-Port 135.


 > [!NOTE]
 > Remoteverbindungen in Arbeitsgruppen werden nicht unterstützt. Sowohl der lokale Computer als auch der Remotecomputer müssen Domänenmitglieder sein.