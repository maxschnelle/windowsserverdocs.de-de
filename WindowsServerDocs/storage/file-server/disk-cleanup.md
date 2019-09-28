---
title: Verwenden der Datenträger Bereinigung unter Windows Server
description: Erfahren Sie, wie Sie mithilfe von Befehlszeilenoptionen das Tool für die Datenträger Bereinigung (cleanmgr. exe) so konfigurieren, dass bestimmte Dateien automatisch bereinigt werden.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: 2de3452a3528122beb26f403fb0c73d7ff13efd7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402113"
---
# <a name="using-disk-cleanup-on-windows-server"></a>Verwenden der Datenträger Bereinigung unter Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Das Tool für die Datenträger Bereinigung löscht unnötige Dateien in einer Windows Server-Umgebung. Dieses Tool ist standardmäßig unter Windows Server 2019 und Windows Server 2016 verfügbar, aber Sie müssen möglicherweise einige manuelle Schritte durchführen, um es in früheren Versionen von Windows Server zu aktivieren.

Führen Sie zum Starten des Tools für die Datenträger Bereinigung entweder den Befehl "cleanmgr. exe" aus, oder klicken Sie auf **Start**, wählen Sie **Windows-Verwaltungs Tools**und dann Datenträger **Bereinigung**aus.

Sie können auch die Datenträger Bereinigung mithilfe des [Windows-Befehls von cleanmgr](../../administration/windows-commands/cleanmgr.md) ausführen und mithilfe von Befehlszeilenoptionen angeben, dass bestimmte Dateien durch die Datenträger Bereinigung bereinigt werden.

## <a name="enable-disk-cleanup-on-an-earlier-version-of-windows-server-by-installing-the-desktop-experience"></a>Aktivieren Sie die Datenträger Bereinigung auf einer früheren Version von Windows Server, indem Sie die Desktop Darstellung installieren.

Führen Sie diese Schritte aus, um den Assistenten zum Hinzufügen von Rollen und Features zum Installieren der Desktop Darstellung auf einem Server mit Windows Server 2012 R2 oder früher zu verwenden. auf diese Weise wird auch die Datenträger Bereinigung installiert

1. Wenn der Server-Manager bereits geöffnet ist, fahren Sie mit dem nächsten Schritt fort. Ist der Server-Manager noch nicht geöffnet, öffnen Sie ihn mit einer der folgenden Aktionen.

   - Starten Sie auf dem Windows-Desktop den Server-Manager, indem Sie in der Windows-Taskleiste auf **Server-Manager** klicken.

   - Wechseln Sie zu **Start** , und wählen Sie die Server-Manager-Kachel aus.

1. Wählen Sie im Menü **Verwalten** die Option **Rollen und Features**hinzufügen aus.

1. Überprüfen Sie auf der Seite **Vorbemerkungen** , ob der Zielserver und die Netzwerkumgebung für das Feature vorbereitet sind, das Sie installieren möchten. Wählen Sie **Weiter** aus.

1. Wählen Sie auf der Seite **Installationstyp auswählen** die Option **rollenbasierte oder featurebasierte Installation** aus, um alle Teile Features auf einem einzelnen Server zu installieren. Wählen Sie **Weiter** aus.

1. Wählen Sie auf der Seite **Zielserver auswählen** einen Server aus dem Serverpool aus, oder wählen Sie eine Offline-VHD aus. Wählen Sie **Weiter** aus.

1. Wählen Sie auf der Seite **Server Rollen auswählen** die Option **weiter**aus.

1. Wählen Sie auf der Seite **Features auswählen** die Option **Benutzeroberfläche und Infrastruktur**aus, und wählen Sie dann **Desktop**Darstellung aus.

1. Wählen Sie unter **Features hinzufügen, die für die Desktop Darstellung erforderlich sind? die**Option **Features hinzufügen**aus.

1. Fahren Sie mit der Installation fort, und starten Sie das System neu.

1. Vergewissern Sie sich, dass das Optionsfeld Datenträger **Bereinigung** im Dialogfeld Eigenschaften von angezeigt wird.

   ![Datenträger Eigenschaften-Dialogfeld mit Datenträger Bereinigungs](media/diskpropswcleanup.png)

## <a name="manually-add-disk-cleanup-to-an-earlier-version-of-windows-server"></a>Manuelles Hinzufügen der Datenträger Bereinigung zu einer früheren Version von Windows Server

Das Tool für die Datenträger Bereinigung (cleanmgr. exe) ist auf Windows Server 2012 R2 oder früher nicht vorhanden, es sei denn, Sie haben das Desktop Darstellung-Feature installiert.

Um "cleanmgr. exe" zu verwenden, installieren Sie die Desktop Darstellung wie zuvor beschrieben, oder kopieren Sie zwei Dateien, die bereits auf dem Server vorhanden sind, "cleanmgr. exe" und "cleanmgr. exe. MUI". Verwenden Sie die folgende Tabelle, um die Dateien für das Betriebssystem zu suchen.

| Betriebssystem  | Architektur  | Speicherort  |
| ----------------- | -------------- | --------------- |
| Windows Server 2008 R2 | 64 Bit | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr_31bf3856ad364e35_6.1.7600.16385_none_c9392808773cd7da\cleanmgr.exe 
| Windows Server 2008 R2 | 64 Bit | C:\Windows\winsxs\amd64_microsoft-windows-cleanmgr.resources_31bf3856ad364e35_6.1.7600.16385_en-us_b9cb6194b257cc63\cleanmgr.exe.mui |

Suchen Sie "cleanmgr. exe", und verschieben Sie die Datei in " **%SystemRoot%\System32**".

Suchen Sie nach "cleanmgr. exe. MUI", und verschieben Sie die Dateien in " **%systemroot%\System32\en-US**".

Sie können jetzt das Tool für die Datenträger Bereinigung starten, indem Sie "cleanmgr. exe" über die Eingabeaufforderung ausführen oder indem Sie auf **Start** klicken und in der Suchleiste **cleanmgr** eingeben.

Damit die Schaltfläche Datenträger Bereinigung im Eigenschaften Dialogfeld eines Datenträgers angezeigt wird, müssen Sie auch das Feature Desktop Darstellung installieren.

## <a name="additional-references"></a>Weitere Verweise

[Freigeben von Laufwerk Speicher in Windows 10](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)

[cleanmgr](../../administration/windows-commands/cleanmgr.md)
