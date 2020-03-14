---
title: 'Datenträgerverwaltung: Problembehandlung'
description: In diesem Artikel erfährst du, wie du Probleme bei der Datenträgerverwaltung behandelst.
ms.date: 12/20/2019
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 7eeb462d31391a228ec0e89afb09673ef14b51cf
ms.sourcegitcommit: 0a0a45bec6583162ba5e4b17979f0b5a0c179ab2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/13/2020
ms.locfileid: "79323442"
---
# <a name="troubleshooting-disk-management"></a>Datenträgerverwaltung: Problembehandlung

> **Gilt für:** Windows 10, Windows 8.1, Windows 7, Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden einige allgemeine Probleme behandelt, die bei der Datenträgerverwaltung auftreten können, sowie mögliche Problembehandlungsschritte.

> [!TIP]
> Sollte beim Ausführen der hier erläuterten Schritte ein Fehler angezeigt werden oder etwas nicht funktionieren, ist das nicht weiter schlimm. Dieses Thema ist nur der erste Schritt, den du ausprobieren solltest. Auf der [Microsoft-Community](https://answers.microsoft.com/en-us/windows)-Website findest du im Abschnitt [Dateien, Ordner und Speicher](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) außerdem eine Menge weiterer Informationen über eine Vielzahl von Hardware- und Softwarekonfigurationen, mit denen du es möglicherweise zu tun hast. Wenn du weitere Hilfe benötigst, stelle dort eine Frage, [wende dich an den Microsoft-Support](https://support.microsoft.com/contactus/),oder kontaktiere den Hersteller deiner Hardware.

## <a name="how-to-open-disk-management"></a>Öffnen der Datenträgerverwaltung

Bevor wir uns mit den kniffligen Dingen beschäftigen, gelangst du folgendermaßen ganz einfach zur Datenträgerverwaltung, falls du noch nicht dort bist:

1. Gib **Computerverwaltung** in das Suchfeld auf der Taskleiste ein, halte **Computerverwaltung** gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle anschließend **Als Administrator ausführen** > **Ja** aus.
2. Nachdem die Computerverwaltung geöffnet wurde, wechsle zu **Speicher** > **Datenträgerverwaltung**.

## <a name="disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps"></a>Fehlende oder nicht initialisierte Datenträger sowie allgemeine Problembehandlungsschritte

![In der Datenträgerverwaltung wird ein unbekannter Datenträger angezeigt, der initialisiert werden muss.](media/uninitialized-disk.PNG)

**Ursache:** Wenn einer deiner Datenträger im Datei-Explorer nicht angezeigt wird und in der Datenträgerverwaltung als *Nicht initialisiert* angegeben ist, besitzt er möglicherweise keine gültige Datenträgersignatur. Das bedeutet im Wesentlichen, dass der Datenträger noch nie initialisiert und formatiert wurde oder dass die Formatierung des Laufwerks beschädigt ist. 

Es ist auch denkbar, dass für den Datenträger ein Hardware- oder Anschlussproblem vorliegt. Darauf gehen wir weiter unten in diesem Artikel ein.

**Lösung:**   Falls das Laufwerk neu ist und lediglich initialisiert werden muss, wodurch alle darauf vorhandenen Daten gelöscht werden, ist die Lösung ganz einfach (siehe: [Initialisieren neuer Datenträger](initialize-new-disks.md)). Vielleicht hast du diese Option aber bereits erfolglos ausprobiert. Oder auf deinem Datenträger befinden sich wichtige Dateien, sodass du den Datenträger nicht initialisieren möchtest, da diese Daten dadurch verloren gehen.

Dass ein Datenträger oder eine Speicherkarte fehlt oder sich nicht initialisieren lässt, kann verschiedene Gründe haben. Eine häufige Ursache ist ein fehlerhafter Datenträger. Im Falle eines fehlerhaften Datenträgers gibt es nicht allzu viele Korrekturmöglichkeiten. Im Anschluss findest du jedoch ein paar Schritte, mit denen sich das Problem möglicherweise beheben lässt. Sollte der Datenträger nach einem dieser Schritte wieder funktionieren, kannst du dich entspannt zurücklehnen und die restlichen Schritte ignorieren (und vielleicht deine Datensicherung auf den neuesten Stand bringen).

1. Sieh dir den Datenträger in der Datenträgerverwaltung an. Wird er wie hier zu sehen als *Offline* angezeigt, klicke mit der rechten Maustaste darauf, und wähle **Online** aus.

    ![Als offline angezeigter Datenträger](media/offline-disk.png)
2. Wenn der Datenträger in der Datenträgerverwaltung als *Online* angezeigt wird und über eine primäre Partition mit dem Status *Fehlerfrei* verfügt (wie hier zu sehen), ist das ein gutes Zeichen.

    ![Als online angezeigter Datenträger mit fehlerfreiem Volume](media/healthy-volume.png)
    - Falls eine Partition über ein Dateisystem, aber über keinen Laufwerkbuchstaben (beispielsweise „E:“) verfügt, erfährst du unter [Ändern eines Laufwerkbuchstabens](change-a-drive-letter.md), wie du manuell einen Laufwerkbuchstaben hinzufügst.
    - Falls eine Partition über kein Dateisystem verfügt (als RAW anstelle von NTFS, ReFS, FAT32 oder ExFAT aufgelistet ist) und du weißt, dass der Datenträger leer ist, halte die Partition gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle dann **Formatieren** aus. Beim Formatieren eines Datenträgers werden alle darauf vorhandenen Daten gelöscht. Führe diesen Schritt also nicht aus, wenn du Dateien des Datenträgers wiederherstellen möchtest. Fahre in diesem Fall direkt mit dem nächsten Schritt fort.
    - Wenn die Partition als *Nicht zugeordnet* aufgelistet ist und du weißt, dass sie leer ist, halte die nicht zugeordnete Partition gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle dann **Neues einfaches Volume** aus. Folge anschließend den Anweisungen zum Erstellen eines Volumes im freien Speicherplatz. Führe diesen Schritt nicht aus, wenn du Dateien der Partition wiederherstellen möchtest. Fahre in diesem Fall direkt mit dem nächsten Schritt fort.

    > [!NOTE]
    > Ignoriere alle Partitionen, die als **EFI-Systempartition** oder **Wiederherstellungspartition** aufgelistet sind. Diese Partitionen enthalten viele wirklich wichtige Dateien, die dein PC benötigt, um ordnungsgemäß zu funktionieren. Du solltest sie einfach in Ruhe ihre Arbeit erledigen lassen, damit sie deinen PC starten und dir helfen, Probleme zu beheben.
3. Falls du über einen externen Datenträger verfügst, der nicht angezeigt wird, stecke ihn aus und wieder ein, und wähle anschließend **Aktion** > **Datenträger neu einlesen** aus. 
4. Fahre deinen PC herunter, schalte deine externe Festplatte aus (sofern es sich um ein Exemplar mit Netzkabel handelt), und schalte PC und Festplatte wieder ein.
    Wähle zum Ausschalten eines PCs unter Windows 10 die Schaltfläche „Start“, die Schaltfläche „Ein/Aus“ und anschließend **Herunterfahren** aus.
5. Schließe den Datenträger an einen anderen USB-Anschluss an, der sich direkt an deinem PC befindet (nicht an einem Hub).
    Manchmal reicht die Stromversorgung bestimmter Anschlüsse für den Betrieb eines USB-Datenträgers nicht aus, oder es liegt ein anderes Problem mit bestimmten Anschlüssen vor. Dies ist besonders häufig bei USB-Hubs der Fall, manchmal gibt es aber auch Unterschiede zwischen den Anschlüssen eines PCs. Daher empfiehlt es sich, nach Möglichkeit verschiedene Anschlüsse ausprobieren.
6. Versuche es mit einem anderen Kabel.
    Kabel sind eine häufige Fehlerquelle. Verwende daher ein anderes Kabel, um den Datenträger anzuschließen. Bei einem internen Datenträger musst du vor dem Kabeltausch wahrscheinlich zuerst deinen PC herunterfahren. Ausführlichere Informationen findest du im Handbuch deines PCs.
7. Überprüfe im Geräte-Manager, ob Probleme vorliegen.
    Halte die Schaltfläche „Start“ gedrückt (oder klicke mit der rechten Maustaste darauf), und wähle im Kontextmenü die Option „Geräte-Manager“ aus. Suche nach Geräten mit einem Ausrufezeichen oder anderen Problemen, doppelklicke auf das betroffene Gerät, und sieh dir den Status an.

    Eine Liste mit Fehlercodes im Geräte-Manager findest du [hier](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows). Manchmal reicht es aber auch, ein betroffenes Gerät auszuwählen und zu halten (oder mit der rechten Maustaste darauf zu drücken) und anschließend **Gerät deinstallieren** auszuwählen, gefolgt von **Aktion** > **Nach geänderter Hardware suchen**.

    ![Geräte-Manager mit unbekanntem USB-Gerät](media/device-manager.PNG)
8. Schließe den Datenträger an einen anderen PC an.
    
    Sollte der Datenträger an einem anderen PC nicht funktionieren, liegt wahrscheinlich ein Problem mit dem Datenträger vor (nicht mit deinem PC). Auch das ist aber natürlich nicht gerade erfreulich. Unter [Forum FAQ: External USB drive error „You must initialize the disk before Logical Disk Manager can access it“](https://social.technet.microsoft.com/Forums/windows/en-US/2b069948-82e9-49ef-bbb7-e44ec7bfebdb/forum-faq-external-usb-drive-error-you-must-initialize-the-disk-before-logical-disk-manager-can?forum=w7itprohardware) (Forum-FAQ: Fehler im Zusammenhang mit einem externen Datenträger: „Sie müssen den Datenträger initialisieren, damit die Verwaltung logischer Datenträger darauf zugreifen kann.“) findest du noch ein paar weitere Schritte, die du versuchen kannst. Möglicherweise ist es nun aber an der Zeit, die Website der [Microsoft-Community](https://answers.microsoft.com/en-us/windows/forum/windows_10-files?sort=lastreplydate&dir=desc&tab=All&status=all&mod=&modAge=&advFil=&postedAfter=&postedBefore=&threadType=all&isFilterExpanded=true&tm=1514405359639) zu durchsuchen und dort um Hilfe zu bitten oder sich an den Hersteller deines Datenträgers oder den [Microsoft-Support](https://support.microsoft.com/contactus/) zu wenden.

    Für den Fall, dass es dir nicht gelingt, das Laufwerk in Betrieb zu nehmen, gibt es Apps, die versuchen können, Daten eines fehlerhaften Datenträgers wiederherzustellen, und falls die Daten wirklich wichtig sind, kannst du auch die Dienste eines kostenpflichtigen Datenwiederherstellers in Anspruch nehmen. Solltest du eine für dich geeignete Lösung finden, hinterlasse doch weiter unten einen entsprechenden Kommentar.

> [!IMPORTANT]
> Datenträgerfehler sind keine Seltenheit. Wichtige Dateien sollten daher regelmäßig gesichert werden. Wenn einer deiner Datenträger manchmal nicht angezeigt wird oder Fehler verursacht, solltest du am besten gleich deine Sicherungsmethoden überprüfen. Es macht nichts, wenn du bei deiner Datensicherung etwas hintendran bist. Damit bist du nicht allein. Die beste Sicherungslösung ist eine, die du auch verwendest. Wir empfehlen daher, eine passende Lösung zu suchen und diese konsequent zu verwenden.
> 
> [!TIP]
> Wie du in Windows integrierte Apps verwendest, um Dateien auf einem externen Laufwerk (etwa auf einem USB-Laufwerk) zu sichern, erfährst du unter [Sichern und Wiederherstellen in Windows 10](https://support.microsoft.com/help/17143/windows-10-back-up-your-files). Du kannst Dateien auch auf Microsoft OneDrive speichern. Bei dieser Variante werden Dateien von deinem PC mit der Cloud synchronisiert. Bei einem Ausfall deiner Festplatte stehen die auf OneDrive gespeicherten Dateien weiterhin auf „OneDrive.com“ zur Verfügung. Weitere Informationen findest du unter [OneDrive auf dem PC](https://support.microsoft.com/help/17184/windows-10-onedrive).

## <a name="a-basic-or-dynamic-disks-status-is-unreadable"></a>Der Status einer Basisfestplatte oder eines dynamischen Datenträgers lautet „Nicht lesbar“.

**Ursache:**  Auf die Basisfestplatte oder den dynamischen Datenträger kann nicht zugegriffen werden, was möglicherweise auf einen Hardwarefehler, eine Beschädigung oder auf E/A-Fehler zurückzuführen ist. Die datenträgerspezifische Kopie der Datenträgerkonfigurationsdatenbank des Systems ist möglicherweise beschädigt. Für Datenträger mit dem Status **Unlesbar** wird ein Fehlersymbol angezeigt.

Der Status **Unlesbar** wird für Datenträger ggf. auch beim Hochfahren angezeigt oder wenn die Datenträgerverwaltung alle Datenträger des Systems neu einliest. In manchen Fällen ist ein nicht lesbarer Datenträger ausgefallen und nicht wiederherstellbar. Bei dynamischen Datenträgern ist der Status **Unlesbar** in der Regel auf eine Beschädigung oder auf ein E/A-Fehler für einen Teil des Datenträgers zurückzuführen (nicht auf den Ausfall des gesamten Datenträgers).

**Lösung:**  Lies die Datenträger neu ein, oder starte den Computer neu, um festzustellen, ob sich der Datenträgerstatus ändert. Probiere auch die unter [Ein Datenträger hat den Status „Nicht initialisiert“, oder der Datenträger fehlt.](#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps) beschriebenen Problembehandlungsschritte aus.

## <a name="a-dynamic-disks-status-is-foreign"></a>Der Status eines dynamischen Datenträgers lautet „Fremd“.

**Ursache:**  Der Status **Fremd** wird angezeigt, wenn Sie einen dynamischen Datenträger von einem anderen PC auf den lokalen Computer verschieben. Für Datenträger mit dem Status **Fremd** wird ein Warnsymbol angezeigt.

In bestimmten Fällen kann für einen Datenträger, der bereits mit dem System verbunden war, der Status **Fremd** angezeigt werden. Konfigurationsdaten für dynamische Datenträger werden auf allen dynamischen Datenträgern gespeichert. Die Informationen darüber, welche Datenträger dem System angehören, gehen daher verloren, wenn alle dynamischen Datenträger ausfallen.

**Lösung:**  Füge den Datenträger der Systemkonfiguration deines Computers hinzu, um auf die Daten des Datenträgers zugreifen zu können. Importiere dazu den fremden Datenträger, indem du ihn gedrückt hältst (oder mit der rechten Maustaste darauf klickst), und anschließend auf **Fremde Datenträger importieren** klickst. Durch Importieren des fremden Datenträgers werden alle darauf vorhandenen Volumes sichtbar. 

## <a name="a-dynamic-disks-status-is-online-errors"></a>Der Status eines dynamischen Datenträgers lautet „Online (Fehler)“.

**Ursache:**  Es liegen E/A-Fehler für einen Bereich des dynamischen Datenträgers vor. Für den fehlerhaften dynamischen Datenträger wird ein Warnsymbol angezeigt.

**Lösung:**   Wenn die E/A-Fehler nur vorübergehend auftreten, reaktiviere den Datenträger, damit er wieder den Status **Online** hat.

## <a name="a-dynamic-disks-status-is-offline-or-missing"></a>Der Status eines dynamischen Datenträgers lautet „Offline“ oder „Fehlt“.

**Ursache:**  Ein als **Offline** aufgeführter dynamischer Datenträger ist möglicherweise beschädigt oder vorübergehend nicht verfügbar. Für den als offline angegebenen dynamischen Datenträger wird ein Fehlersymbol angezeigt.

Wenn der Datenträgerstatus **Offline** lautet und sich der Name des Datenträgers in **Fehlt** ändert, war der Datenträger vor Kurzem noch im System verfügbar, kann aber nun nicht mehr gefunden oder identifiziert werden. Der fehlende Datenträger ist möglicherweise beschädigt, ausgeschaltet oder nicht angeschlossen.

**Lösung:** So schaltest du einen Datenträger mit dem Status „Offline“ oder „Fehlt“ wieder online:

1. Behebe alle Datenträger-, Controller- oder Kabelprobleme. 
2. Vergewissere dich, dass der physische Datenträger eingeschaltet, eingesteckt und mit dem Computer verbunden ist. 
3. Führe anschließend den Befehl **Datenträger reaktivieren** aus, um den Datenträger wieder online zu schalten.
4. Probiere die unter [Ein Datenträger hat den Status „Nicht initialisiert“, oder der Datenträger fehlt.](#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps) beschriebenen Problembehandlungsschritte aus.
5. Wenn der Datenträger weiterhin den Status **Offline** hat, der Datenträgername weiterhin **Fehlt** lautet und du zu dem Schluss kommst, dass das Problem des Datenträgers nicht behebbar ist, kannst du den Datenträger aus dem System entfernen, indem du ihn gedrückt hältst (oder mit der rechten Maustaste darauf klickst), und anschließend auf **Datenträger entfernen** klickst. Um den Datenträger entfernen zu können, musst du allerdings erst alle Volumes (oder Spiegelungen) auf dem Datenträger löschen. Du kannst gespiegelte Volumes auf dem Datenträger retten, indem du die Spiegelung entfernst (anstelle des gesamten Volumes). Beim Löschen eines Volumes werden alle Daten des Volumes gelöscht. Daher solltest du einen Datenträger nur entfernen, wenn du absolut sicher bist, dass der Datenträger endgültig beschädigt und nicht mehr verwendbar ist.

**Ein Datenträger, der offline ist und immer noch „Datenträger \#“ (also nicht „Fehlt“) heißt, kann möglicherweise mit einer der folgenden Methoden wieder online geschaltet werden:**

1. Halte in der Datenträgerverwaltung den Datenträger gedrückt (oder klicke mit der rechten Maustaste darauf), und klicke anschließend auf **Datenträger reaktivieren**, um den Datenträger wieder online zu schalten. Falls der Datenträgerstatus weiterhin **Offline** lautet, überprüfe die Kabel und den Datenträgercontroller, und vergewissere dich, dass der physische Datenträger fehlerfrei ist. Behebe alle Probleme, und versuche dann erneut, den Datenträger zu reaktivieren. Ist die Reaktivierung des Datenträgers erfolgreich, sollten alle Volumes auf dem Datenträger automatisch wieder den Status **Fehlerfrei** haben.
2. Überprüfe die Ereignisprotokolle in der Ereignisanzeige auf datenträgerbezogene Fehler wie etwa „No good config copies“ (Keine geeigneten Konfigurationskopien vorhanden). Sollte das Ereignisprotokoll diesen Fehler enthalten, wende dich an den [Microsoft-Produktsupport](https://msdn.microsoft.com/library/aa263468(v=vs.60).aspx).

3. Teste den Datenträger an einem anderen Computer. Lässt sich der Datenträger an einem anderen Computer **online** schalten, ist das Problem mit hoher Wahrscheinlichkeit auf die Konfiguration des Computers zurückzuführen, auf dem sich der Datenträger nicht **online** schalten lässt.

4. Teste den Datenträger an einem anderen Computer mit dynamischen Datenträgern. Importiere den Datenträger auf diesem Computer, und verschiebe ihn anschließend wieder auf den Computer, auf dem er sich nicht **online** schalten ließ. 

## <a name="a-basic-or-dynamic-volumes-status-is-failed"></a>Der Status einer Basisvolumes oder eines dynamischen Volumes lautet „Fehlerhaft“.

**Ursache:**   Die Basisfestplatte oder das dynamische Volume kann nicht automatisch gestartet werden, der Datenträger ist beschädigt, oder das Dateisystem ist beschädigt. Falls der Datenträger oder das Dateisystem nicht repariert werden kann, ist beim Status **Fehlerhaft** mit Datenverlusten zu rechnen.

**Lösung:**

Wenn es sich bei dem Volume um eine Basisvolume mit dem Status **Fehlerhaft** handelt:

- Vergewissere dich, dass der zugrunde liegende physische Datenträger eingeschaltet, eingesteckt und mit dem Computer verbunden ist.
- Probiere die unter [Ein Datenträger hat den Status „Nicht initialisiert“, oder der Datenträger fehlt.](#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps) beschriebenen Problembehandlungsschritte aus.

Wenn es sich bei dem Volume um ein dynamisches Volume mit dem Status **Fehlerhaft** handelt:

-   Vergewissere dich, dass die zugrunde liegenden Datenträger online sind. Falls nicht, schalte die Datenträger wieder **online**. Daraufhin sollte das Volume automatisch neu starten und wieder den Status **Fehlerfrei** haben. Falls der dynamische Datenträger wieder den Status **Online** hat, das dynamische Volume aber nicht zum Status **Fehlerfrei** zurückkehrt, können Sie das Volume manuell reaktivieren.
-   Wenn das dynamische Volume ein gespiegeltes Volume oder ein RAID-5-Volume mit veralteten Daten ist, wird das Volume nicht automatisch neu gestartet, wenn der zugrunde liegende Datenträger wieder online geschaltet wird. Wurde die Verbindung mit den Datenträgern getrennt, die über aktuelle Daten verfügen, müssen diese Datenträger zuerst online geschaltet werden, damit die Daten synchronisiert werden können. Starte andernfalls das gespiegelte Volume bzw. das RAID-5-Volume manuell neu, und führe dann das Fehlerüberprüfungstool oder „Chkdsk.exe“ aus.
- Probiere die unter [Ein Datenträger hat den Status „Nicht initialisiert“, oder der Datenträger fehlt.](#disks-that-are-missing-or-not-initialized-plus-general-troubleshooting-steps) beschriebenen Problembehandlungsschritte aus.

## <a name="a-basic-or-dynamic-volumes-status-is-unknown"></a>Der Status eines Basisvolumes oder eines dynamischen Volumes lautet „Unbekannt“.

**Ursache:**   Der Status **Unbekannt** tritt auf, wenn der Startsektor für das Volume beschädigt wurde (etwa durch einen Virus). In diesem Fall kannst du nicht mehr auf die Daten auf dem Volume zugreifen. Der Status **Unbekannt** tritt auch auf, wenn du einen neuen Datenträger installierst und den Assistenten zum Erstellen einer Datenträgersignatur nicht erfolgreich abschließt.

**Lösung:**   Initialisiere den Datenträger. Eine entsprechende Anleitung findest du unter [Initialisieren neuer Datenträger](initialize-new-disks.md).

## <a name="a-dynamic-volumes-status-is-data-incomplete"></a>Der Status eines dynamischen Volumes lautet „Die Daten sind nicht vollständig“.

**Ursache:** Du hast einige, aber nicht alle Datenträger eines Volumes mit mehreren Datenträgern verschoben. Die Daten auf diesem Volume werden vernichtet, es sei denn, du verschiebst und importierst die übrigen Datenträger, die dieses Volume enthalten.

**Lösung:**

1. Verschiebe alle Datenträger, aus denen sich das Volume mit mehreren Datenträgern zusammensetzt, auf den Computer.
2. Importiere die Datenträger. Informationen zum Verschieben und Importieren von Datenträgern findest du unter [Move Disks to Another Computer](move-disks-to-another-computer.md) (Verschieben von Datenträgern auf einen anderen Computer).

Solltest du das Volume mit mehreren Datenträgern nicht mehr benötigen, kannst du den Datenträger importieren und darauf neue Volumes erstellen. Gehen Sie hierzu wie folgt vor:

1. Halte das Volume mit dem Status **Fehlerhaft** oder **Fehlerhafte Redundanz** gedrückt (oder klicke mit der rechten Maustaste darauf), und klicke anschließend auf **Volume löschen**.
2. Halte den Datenträger gedrückt (oder klicke mit der rechten Maustaste darauf), und klicke dann auf **Neues Volume**.

## <a name="a-dynamic-volumes-status-is-healthy-at-risk"></a>Der Status eines dynamischen Volumes lautet „Fehlerfrei (Risiko)“.

**Ursache:**   Dieser Status bedeutet, dass aktuell auf das dynamische Volume zugegriffen werden kann, für den zugrunde liegenden dynamischen Datenträger jedoch E/A-Fehler erkannt wurden. Wenn für einen Teil eines dynamischen Datenträgers ein E/A-Fehler erkannt wird, erhalten alle Volumes auf dem Datenträger den Status **Fehlerfrei (Risiko)** , und es wird ein Warnsymbol für das Volume angezeigt.

Wenn der Status des Volumes **Fehlerfrei (Risiko)** lautet, hat ein zugrunde liegender Datenträger in der Regel den Status **Online (Fehler)** .

**Lösung:**  
1. Stelle für den zugrunde liegenden Datenträger den Status **Online** wieder her. Wenn der Datenträger wieder den Status **Online** hat, sollte das Volume wieder den Status **Fehlerfrei** haben. Sollte der Status **Fehlerfrei (Risiko)** bestehen bleiben, ist der Datenträger möglicherweise fehlerhaft. 

2. Sichere die Daten, und ersetze den Datenträger baldmöglichst.

## <a name="cannot-manage-striped-volumes-using-disk-management-or-diskpart"></a>Stripesetvolumes können nicht über die Datenträgerverwaltung oder mithilfe von DiskPart verwaltet werden.

**Ursache:**   Die Verwaltung logischer Datenträger (Logical Disk Manager, LDM) von Microsoft wurde durch einige Microsoft-fremde Produkte für die erweiterte Datenträgerverwaltung ersetzt, was dazu führen kann, dass die Verwaltung logischer Datenträger deaktiviert wird.

**Lösung:**   Wenn du Microsoft-fremde Datenträgerverwaltungssoftware verwendest und LDM dadurch deaktiviert wurde, bitte den Anbieter der Microsoft-fremden Software um Unterstützung bei der Behandlung der Probleme mit der Datenträgerkonfiguration.

## <a name="disk-management-cannot-start-the-virtual-disk-service"></a>Die Datenträgerverwaltung kann den Dienst für virtuelle Datenträger nicht starten.

**Ursache:**   Dieser Fehler kann auftreten, wenn ein Remotecomputer den Dienst für virtuelle Datenträger (Virtual Disk Service, VDS) nicht unterstützt oder du keine Verbindung mit dem Remotecomputer herstellen kannst, weil dies von der Windows-Firewall blockiert wird.

**Lösung:**

1. Wenn der Remotecomputer VDS unterstützt, kannst du Windows Defender Firewall so konfigurieren, dass VDS-Verbindungen zugelassen werden. Wenn der Remotecomputer VDS nicht unterstützt, kannst du eine Remotedesktopverbindung mit ihm herstellen und die Datenträgerverwaltung direkt auf dem Remotecomputer ausführen.
2. Um Datenträger auf Remotecomputern mit VDS-Unterstützung verwalten zu können, muss Windows Defender Firewall sowohl auf dem lokalen Computer (auf dem du die Datenträgerverwaltung ausführst) als auch auf dem Remotecomputer konfiguriert werden.
3. Konfiguriere Windows Defender Firewall auf dem lokalen Computer, um die Ausnahme für die Remotevolumeverwaltung zu aktivieren.

> [!NOTE]
> Die Ausnahme für die Remotevolumeverwaltung enthält Ausnahmen für „Vds.exe“, „Vdsldr.exe“ und den TCP-Port 135.

> [!NOTE]
> Remoteverbindungen in Arbeitsgruppen werden nicht unterstützt. Sowohl der lokale Computer als auch der Remotecomputer muss einer Domäne angehören.

Siehe auch

- [Freigeben von Laufwerksspeicherplatz unter Windows 10](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)