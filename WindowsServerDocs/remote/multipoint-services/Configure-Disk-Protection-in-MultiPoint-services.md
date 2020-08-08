---
title: Konfigurieren von Datenträgerschutz in MultiPoint Services
description: Erfahren Sie, wie Sie den Datenträger Schutz für Multipoint Services einrichten.
ms.topic: article
ms.assetid: bd9bf5b9-e481-499b-9c15-7ee5a4f470c4
author: evaseydl
manager: scottman
ms.author: evas
ms.date: 08/04/2016
ms.openlocfilehash: d244fd5e49e03cf336fb9d6f027e175e38bf66e1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944380"
---
# <a name="configure-disk-protection"></a>Konfigurieren des Datenträger Schutzes
Sie können den Datenträger Schutz in Multipoint Services verwenden, um Ihr System Volume vor unbeabsichtigten Updates zu schützen, die Beibehaltung von Windows-Updates zu planen, während der Datenträger Schutz aktiv ist, den Datenträger Schutz vorübergehend zu deaktivieren und den Datenträger Schutz zu deinstallieren.

Wenn Sie den Datenträger Schutz in Multipoint Services aktivieren, können Sie das System Volume (das Laufwerk, auf dem Windows installiert ist, normalerweise C:), schützen. aus unerwünschten Änderungen. Wenn der Datenträger Schutz aktiviert ist, werden an dem System Volume vorgenommene Änderungen an einem temporären Speicherort gespeichert, sodass der Computer durch einfaches Neustarten des Computers verworfen wird und das System automatisch wieder in den vorherigen bekannten Zustand zurückversetzt wird.

Der Administrator kann auf einfache Weise Software installieren oder Konfigurationsänderungen vornehmen, indem der Datenträger Schutz vorübergehend deaktiviert wird. Um das System mit Windows-Updates und Antimalwaredefinitionen auf dem aktuellen Stand zu halten, plant der Datenträger Schutz ein Wartungsfenster, um Updates herunterzuladen und zu installieren. Der Administrator kann auch ein benutzerdefiniertes Skript bereitstellen, das während des Wartungs Fensters ausgeführt werden soll, um die Wartungsanforderungen über Windows Update hinaus zu erfüllen

## <a name="enable-disk-protection"></a>Aktivieren des Datenträger Schutzes
Bevor Sie den Datenträger Schutz aktivieren, stellen Sie sicher, dass alle Anwendungen und Treiber installiert und auf dem neuesten Stand sind, und verschieben Sie die Benutzerprofile auf ein Volume, das nicht geschützt wird. Wenn Sie manuelle Updates vornehmen müssen, nachdem Sie den Datenträger Schutz aktiviert haben, können Sie den Datenträger Schutz temporär deaktivieren. Es ist jedoch am einfachsten, das System in einen idealen Zustand zu bringen, bevor der Datenträger Schutz aktiviert ist.


1.  Melden Sie sich bei dem Server, auf dem Multipoint Services ausgeführt wird, als Administrator an.

2.  Vor dem Aktivieren des Datenträger Schutzes:

    -   Stellen Sie sicher, dass sich das Multipoint Services-System genau in dem Zustand befindet, in dem er bleiben soll. Stellen Sie beispielsweise sicher, dass installierte Software, Systemeinstellungen und Updates korrekt sind.

    -   Verschieben Sie Benutzerprofile auf ein nicht geschütztes Volume, oder richten Sie einen freigegebenen Datei Speicherort vom System Volume ein, wie unter [Aktivieren der Dateifreigabe in Multipoint Services](Enable-file-sharing-in-MultiPoint-services.md)beschrieben.

3.  Öffnen Sie auf dem **Start** Bildschirm den **Multipoint-Manager**.

4.  Klicken Sie auf die Registerkarte **Startseite** , klicken Sie auf Datenträger **Schutz aktivieren**und dann auf **OK**.

Wenn der Datenträger Schutz zum ersten Mal aktiviert wird, wird das System durch Installieren eines Treibers und Erstellen einer Cachedatei auf dem System Volume vorbereitet. Die Cachedatei speichert temporär alle Änderungen, die am System Volume vorgenommen werden, während der Datenträger Schutz aktiv ist. Da Systemupdates in der Cachedatei gespeichert werden, ändern Sie nicht den geschützten Inhalt des Volumes außerhalb der Cachedatei. Jedes Mal, wenn das System gestartet wird, wird die Cachedatei zurückgesetzt. Dadurch werden alle Änderungen verworfen, die seit dem vorherigen Systemstart gespeichert wurden. Folglich startet das System immer denselben Zustand wie bei Aktivierung des Datenträger Schutzes.

Windows muss einige Systemdateien aktualisieren – einschließlich der System Page File, dem Speicherort des Absturz Abbilds und der Ereignisprotokolle. Diese Dateien werden nicht verworfen, wenn der Datenträger Schutz aktiviert ist. Um dies zu erreichen, wird ein neues Volume mit dem Namen "dkonservig" erstellt, wenn der Datenträger Schutz zum ersten Mal aktiviert wird, und diese Dateien werden auf dieses Volume verschoben. Die dbeibehaltene Partition ist nicht geschützt, sodass Schreibvorgänge in diese Dateien durch Neustarts beibehalten werden, auch wenn der Datenträger Schutz aktiviert ist.

## <a name="schedule-software-updates"></a>Planen von Software Updates
Wenn Windows für die automatische Installation von Windows-Updates konfiguriert ist, werden diese Updates vom Datenträger Schutz zum konfigurierten Zeitpunkt zugelassen, und die Updates werden nicht verworfen. Wenn Windows Updates beispielsweise 3:00 Uhr geplant sind, prüft der Datenträger Schutz jeden Tag um 3:00 Uhr nach Updates. Wenn Updates gefunden werden, wird der Datenträger Schutz von Multipoint Services vorübergehend deaktiviert, die Updates werden angewendet, und der Datenträger Schutz wird erneut aktiviert.

1.  Zeigen Sie im Multipoint-Manager die Registerkarte **Start** an, und klicken Sie dann auf **Software Updates planen**.

2.  Klicken Sie im Dialogfeld Software Updates planen **auf Aktualisieren unter**, und wählen Sie eine Uhrzeit für Updates aus, z. b. **3:00 Uhr**.

3.  Aktivieren Sie das Kontrollkästchen **Windows Update ausführen** .

4.  Wenn Ihre Organisation ein eigenes Update Skript ausführt, aktivieren Sie das Kontrollkästchen **das folgende Programm ausführen** , und geben Sie den Speicherort des Aktualisierungs Skripts Ihrer Organisation an.

5.  Wählen Sie eine maximale Zeit für das Ausführen von Updates aus.

6.  **Wenn Sie fertig**sind, wählen Sie aus, ob das System auf den vorherigen Energiezustand zurückkehren oder nach dem Anwenden von Updates heruntergefahren werden soll.

7.  Klicken Sie auf **OK**.

## <a name="temporarily-disable-disk-protection"></a>Temporäres Deaktivieren des Datenträger Schutzes
Wenn ein Administrator Software installieren, Systemeinstellungen ändern oder andere Wartungs Tasks ausführen muss, die Systemupdates umfassen, können Sie den Datenträger Schutz temporär deaktivieren. Nachdem die Änderungen vorgenommen wurden, aktivieren Sie den Datenträger Schutz erneut. Während des Systemneustarts behält das System seinen Status bei Aktivierung des Datenträger Schutzes bei.

1.  Klicken Sie im Multipoint-Manager auf die Registerkarte **Start** .

2.  Klicken Sie auf der Registerkarte Startseite auf Datenträger **Schutz deaktivieren**, und klicken Sie dann auf **OK**.

> [!NOTE]
> Denken Sie daran, den Datenträger Schutz nach Abschluss der Wartung erneut zu aktivieren. Das System wird erst dann wieder geschützt, wenn der Administrator den Datenträger Schutz explizit erneut aktiviert.

## <a name="uninstall-disk-protection"></a>Datenträger Schutz deinstallieren
Wenn Sie den Datenträger Schutz deinstallieren, werden der Treiber und die Cachedatei entfernt. Daher sollten Sie diesen Vorgang nur ausführen, wenn Sie den Datenträger Schutz langfristig nicht mehr verwenden möchten. Wenn Sie einfach Wartungsarbeiten durchführen oder den Schutz vorübergehend verhindern möchten, verwenden Sie stattdessen den Task "Datenträger Schutz deaktivieren".

Sie können den Datenträger Schutz unabhängig davon deinstallieren, ob er aktiviert oder deaktiviert ist.

1.  Klicken Sie im Multipoint-Manager auf die Registerkarte **Start** .

2.  Klicken Sie auf der Registerkarte Startseite auf Datenträger **Schutz deinstallieren**, und klicken Sie dann auf **OK**.

    Nachdem Sie auf **OK**geklickt haben, wird der Computer neu gestartet. Der Vorgang zur Deinstallation erfordert mehrere Neustarts, in denen der Treiber und die Cachedatei entfernt werden. Die dbeibehaltene Partition bleibt, und die pagefile, der Speicherort des Absturz Abbilds und die Ereignisprotokoll Dateien bleiben für die Verwendung der dbeibehaltenen Partition konfiguriert.