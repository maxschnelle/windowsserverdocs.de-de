---
title: Verwenden der Datenträgerbereinigung unter Windows Server
description: Erfahren Sie, wie Sie mithilfe von Befehlszeilenoptionen das Tool für die Datenträgerbereinigung („cleanmgr.exe“) so konfigurieren, dass bestimmte Dateien automatisch bereinigt werden.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: bb93ec15fd138ee65797c9d27413552c3a1759a6
ms.sourcegitcommit: 3a3d62f938322849f81ee9ec01186b3e7ab90fe0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/23/2020
ms.locfileid: "75949673"
---
# <a name="using-disk-cleanup-on-windows-server"></a>Verwenden der Datenträgerbereinigung unter Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Das Tool für die Datenträgerbereinigung löscht unnötige Dateien in einer Windows Server-Umgebung. Dieses Tool ist standardmäßig unter Windows Server 2019 und Windows Server 2016 verfügbar, aber Sie müssen möglicherweise einige manuelle Schritte durchführen, um es für frühere Versionen von Windows Server zu aktivieren.

Führen Sie zum Starten des Tools für die Datenträgerbereinigung entweder den Befehl „cleanmgr.exe“ aus, oder wählen Sie **Start** und **Windows-Verwaltungstools** aus. Wählen Sie dann **Datenträgerbereinigung** aus.

Sie können die Datenträgerbereinigung auch mithilfe des Windows-Befehls [cleanmgr](../../administration/windows-commands/cleanmgr.md) ausführen und mit Befehlszeilenoptionen angeben, dass bestimmte Dateien mit der Datenträgerbereinigung bereinigt werden.

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>Aktivieren der Datenträgerbereinigung für eine frühere Version von Windows Server durch Installieren der Desktopdarstellung

Führen Sie diese Schritte aus, um den Assistenten zum Hinzufügen von Rollen und Features zum Installieren der Desktopdarstellung auf einem Server mit Windows Server 2012 R2 oder früher zu verwenden. Auf diese Weise wird auch die Datenträgerbereinigung installiert.

1. Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

   - Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

   - Navigieren Sie zu **Start**, und wählen Sie die Kachel „Server-Manager“ aus.

1. Klicken Sie im Menü **Verwalten** auf **Rollen und Funktionen hinzufügen**.

1. Vergewissern Sie sich auf der Seite **Vorbemerkungen**, dass der Zielserver und die Netzwerkumgebung für das zu installierende Feature vorbereitet sind. Wählen Sie **Weiter** aus.

1. Wählen Sie auf der Seite **Installationstyp auswählen** die Option **Rollenbasierte oder featurebasierte Installation** aus, um Features auf einem einzelnen Server zu installieren. Wählen Sie **Weiter** aus.

1. Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, oder wählen Sie eine Offline-VHD aus. Wählen Sie **Weiter** aus.

1. Wählen Sie **Weiter** auf der Seite **Serverrollen auswählen** aus.

1. Wählen Sie auf der Seite **Features auswählen** die Option **Benutzeroberfläche und Infrastruktur** aus, und wählen Sie dann **Desktopdarstellung** aus.

1. Klicken Sie unter **Features hinzufügen, die für Desktopdarstellung erforderlich sind?** auf **Features hinzufügen**.

1. Fahren Sie mit der Installation fort, und starten Sie das System dann neu.

1. Vergewissern Sie sich, dass im Dialogfeld „Eigenschaften“ das Optionsfeld **Datenträgerbereinigung** angezeigt wird.

   ![Dialogfeld „Datenträgereigenschaften“ mit Option „Datenträgerbereinigung“](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>Manuelles Hinzufügen von Datenträgerbereinigung zu einer früheren Version von Windows Server

Das Tool für die Datenträgerbereinigung („cleanmgr.exe“) ist unter Windows Server 2012 R2 oder früher nicht vorhanden, es sei denn, Sie haben das Feature „Desktopdarstellung“ installiert.

Um „cleanmgr.exe“ zu verwenden, installieren Sie die Desktopdarstellung wie zuvor beschrieben, oder kopieren Sie zwei Dateien, die bereits auf dem Server vorhanden sind: „cleanmgr.exe“ und „cleanmgr.exe.mui“. Verwenden Sie die folgende Tabelle, um die Dateien für Ihr Betriebssystem zu suchen.

| Betriebssystem  | Architektur  | Speicherort  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64 Bit | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64 Bit | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

Suchen Sie die Datei „cleanmgr.exe“, und verschieben Sie die Datei in **%systemroot%\System32**.

Suchen Sie die Datei „cleanmgr.exe.mui“, und verschieben Sie die Dateien in **%systemroot%\System32\en-US**.

Sie können jetzt das Tool für die Datenträgerbereinigung starten, indem Sie „cleanmgr.exe“ über die Eingabeaufforderung ausführen. Sie können auch auf **Start** klicken und dann **Cleanmgr** in die Suchleiste eingeben.

Damit die Schaltfläche Datenträgerbereinigung im Dialogfeld „Eigenschaften“ eines Datenträgers angezeigt wird, müssen Sie auch das Feature „Desktopdarstellung“ installieren.

## <a name="additional-references"></a>Weitere Verweise

[Freigeben von Laufwerksspeicherplatz unter Windows 10](https://support.microsoft.com/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
