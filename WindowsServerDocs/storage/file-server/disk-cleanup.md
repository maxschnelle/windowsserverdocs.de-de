---
title: Verwenden die Datenträgerbereinigung unter WindowsServer
description: Erfahren Sie, wie Sie die Befehlszeilenoptionen verwenden, um die Datenträgerbereinigung-Tool (Cleanmgr.exe) zum automatischen Bereinigen von bestimmte Dateien zu konfigurieren.
ms.prod: windows-server-threshold
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: fbec7cd2b8312f03998cfb27b739d0866d3a47c5
ms.sourcegitcommit: 545dcfc23a81943e129565d0ad188263092d85f6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2019
ms.locfileid: "67407669"
---
# <a name="using-disk-cleanup-on-windows-server"></a>Verwenden die Datenträgerbereinigung unter WindowsServer

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Das Tool die Datenträgerbereinigung löscht nicht benötigte Dateien in einer Windows Server-Umgebung. Dieses Tool ist standardmäßig unter Windows Server-2019 und Windows Server 2016 verfügbar, aber möglicherweise müssen Sie einige manuelle Schritte ausführen, um sie in früheren Versionen von Windows Server zu aktivieren.

Um die Datenträgerbereinigung-Tool zu starten, führen Sie den Befehl Cleanmgr.exe oder wählen Sie **starten**Option **Windows-Verwaltung**, und wählen Sie dann **Datenträgerbereinigung**.

Sie können auch die Datenträgerbereinigung ausführen, mit der [cleanmgr aus Windows-Befehl](../../administration/windows-commands/cleanmgr.md) und Befehlszeilenoptionen verwenden, um anzugeben, dass bestimmte Dateien Datenträgerbereinigung bereinigt.

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>Datenträgerbereinigung auf eine frühere Version von Windows Server zu aktivieren, indem Sie die Desktopdarstellung installieren

Gehen Sie zum Hinzufügen von Rollen und Features-Assistenten zu verwenden, um die Desktopdarstellung installieren, auf einem Server mit Windows Server 2012 R2 oder früher die Datenträgerbereinigung ebenfalls installiert.

1. Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

   - Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

   - Wechseln Sie zu **starten** , und wählen Sie die Kachel Server-Manager.

1. Auf der **verwalten** wählen Sie im Menü hinzufügen **Rollen und Features**.

1. Auf der **vor dem Beginn** Seite, stellen Sie sicher, dass der Zielserver und die Netzwerkumgebung für das Feature vorbereitet sind, die Sie installieren möchten. Wählen Sie **Weiter** aus.

1. Auf der **Installationstyp** Seite **rollenbasierte oder featurebasierte Installation** alle Webparts-Funktionen auf einem einzelnen Server installieren. Wählen Sie **Weiter** aus.

1. Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, oder wählen Sie eine Offline-VHD aus. Wählen Sie **Weiter** aus.

1. Auf der **Serverrollen auswählen** Seite **Weiter**.

1. Auf der **Funktionen auswählen** Seite **Benutzeroberfläche und Infrastruktur**, und wählen Sie dann **Desktopdarstellung**.

1. In **Hinzufügen von Funktionen, die für die Desktopdarstellung erforderlich sind?** Option **Features hinzufügen**.

1. Die Installation fortzusetzen, und klicken Sie dann das System neu starten.

1. Überprüfen Sie, ob die **Datenträgerbereinigung** Optionsfeld aus, die im Dialogfeld "Eigenschaften" angezeigt wird.

   ![Dialogfeld "Eigenschaften", mit der Datenträgerbereinigung-Option auf den Datenträger](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>Manuelles Hinzufügen von Datenträgerbereinigung zu einer früheren Version von Windows Server

Der Datenträgerbereinigung-Tool (cleanmgr.exe) nicht vorhanden, für Windows Server 2012 R2 oder früher, es sei denn, Sie Feature "Desktopdarstellung" installiert haben.

Cleanmgr.exe verwenden zu können, installieren Sie die Desktopdarstellung, wie zuvor beschrieben, oder kopieren Sie zwei Dateien, die bereits auf dem Server, cleanmgr.exe und cleanmgr.exe.mui vorhanden sind. Verwenden Sie in der folgende Tabelle, um die Dateien für Ihr Betriebssystem zu suchen.

| Betriebssystem  | Architecture  | Speicherort  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64 Bit | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64 Bit | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

Suchen von cleanmgr.exe und verschieben Sie die Datei **%systemroot%\System32**.

Suchen von cleanmgr.exe.mui und verschieben Sie die Dateien in **%systemroot%\System32\en-US**.

Sie können die Datenträger-Bereinigungstool Cleanmgr.exe-Eingabeaufforderung ausführen oder indem Sie auf jetzt starten **starten** und eingeben **Cleanmgr** in der Suchleiste.

Damit der Datenträgerbereinigung-Schaltfläche, die auf einem Datenträger des Dialogfeld "Eigenschaften" angezeigt werden, müssen Sie auch das Feature Desktopdarstellung installieren.

## <a name="additional-references"></a>Weitere Verweise

[Freigeben von Speicherplatz auf dem Laufwerk in Windows 10](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
