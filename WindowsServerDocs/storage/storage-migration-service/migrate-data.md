---
title: Migrieren eines Dateiservers mithilfe von Storage Migration Service
description: Kurze Beschreibung des Themas für Suchmaschinenergebnisse
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 02/13/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 7cec2a9c805208baceff8a8afe22a20fd2859edd
ms.sourcegitcommit: e2b565ce85a97c0c51f6dfe7041f875a265b35dd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2019
ms.locfileid: "69584842"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>Verwenden von Storage Migration Service zum Migrieren eines Servers

In diesem Thema wird erläutert, wie Sie einen Server, einschließlich seiner Dateien und Konfiguration, mithilfe von [Storage Migration Service](overview.md) und Windows Admin Center zu einem anderen Server migrieren. Die Migration dauert drei Schritte, nachdem Sie den Dienst installiert und alle erforderlichen Firewallports geöffnet haben: Inventarisieren der Server, übertragen von Daten und übernehmen an die neuen Server.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>Schritt 0: Installieren von Storage Migration Service und Überprüfen der Firewallports

Bevor Sie beginnen, installieren Sie den Speicher Migrationsdienst, und stellen Sie sicher, dass die erforderlichen Firewallports geöffnet sind.

1. Überprüfen Sie die Anforderungen an den [Speicher Migrationsdienst](overview.md#requirements) , und installieren Sie das [Windows Admin Center](../../manage/windows-admin-center/understand/windows-admin-center.md) auf Ihrem PC oder eine Management Server, sofern noch nicht geschehen.
2. Stellen Sie im Windows Admin Center eine Verbindung zum Orchestrator-Server her, auf dem Windows Server 2019 ausgeführt wird. <br>Dies ist der Server, auf dem Sie den Speicher Migrationsdienst installieren und zum Verwalten der Migration verwenden. Wenn Sie nur einen Server migrieren, können Sie den Zielserver verwenden, sofern er Windows Server 2019 ausgeführt wird. Es wird empfohlen, einen separaten Orchestrierungs Server für multiservermigrationen zu verwenden.
1. Wechseln Sie zu **Server-Manager** (in Windows Admin Center) > **Storage Migration Service** , und wählen Sie **Installieren** aus, um den Speicher Migrationsdienst und die erforderlichen Komponenten zu installieren (siehe Abbildung 1).
    ![Screenshot der Seite "Storage Migration Service" mit der Installations](media/migrate/install.png) Schaltfläche **Abbildung 1: Installieren von Storage Migration Service**
1. Installieren Sie den Speicher Migrationsdienst-Proxy auf allen Ziel Servern, auf denen Windows Server 2019 ausgeführt wird. Dadurch wird die Übertragungsgeschwindigkeit bei der Installation auf den Ziel Servern verdoppelt. <br>Stellen Sie hierzu im Windows Admin Center eine Verbindung mit dem Zielserver her, und navigieren Sie dann zu **Server-Manager** (im Windows Admin Center) > **Rollen und Features**, wählen Sie **Speicher Migrationsdienst-Proxy**aus, und klicken Sie dann auf **Installieren**.
1. Stellen Sie auf allen Quell Servern und auf allen Ziel Servern, auf denen Windows Server 2012 R2 oder Windows Server 2016 ausgeführt wird, im Windows Admin Center eine Verbindung mit jedem Server her, und navigieren Sie zu **Server-Manager** (im Windows Admin Center) > **Firewall**  > .  **Eingehende Regeln**, und überprüfen Sie dann, ob die folgenden Regeln aktiviert sind:
    - Datei- und Druckerfreigabe (SMB eingehend)
    - Anmeldedienst (NP-in)
    - Windows-Verwaltungsinstrumentation (DCOM-in)
    - Windows-Verwaltungsinstrumentation (WMI-In)

   > [!NOTE]
   > Wenn Sie Firewalls von Drittanbietern verwenden, sind die zu öffnenden eingehenden Port Bereiche TCP/445 (SMB), TCP/135 (RPC/DCOM Endpoint Mapper) und TCP 1025-65535 (kurzlebige RPC/DCOM-Ports). Die Ports für den Speicher Migrationsdienst sind TCP/28940 (Orchestrator) und TCP/28941 (Proxy).

1. Wenn Sie einen Orchestrator-Server zum Verwalten der Migration verwenden und Ereignisse oder ein Protokoll der übertragenden Daten herunterladen möchten, überprüfen Sie, ob die Firewallregel für die Datei-und Druckerfreigabe (SMB-in) ebenfalls auf diesem Server aktiviert ist.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>Schritt 1: Erstellen eines Auftrags und Inventarisieren der Server, um herauszufinden, was migriert werden soll

In diesem Schritt geben Sie an, welche Server migriert werden sollen, und Scannen Sie anschließend, um Informationen zu Ihren Dateien und Konfigurationen zu sammeln.

1. Wählen Sie **Neuer Auftrag**aus, benennen Sie den Auftrag, und klicken Sie dann auf **OK**.
1. Geben Sie auf der Seite **Anmelde Informationen eingeben** Administrator Anmelde Informationen ein, die auf den Servern funktionieren, von denen Sie migrieren möchten, und klicken Sie dann auf **weiter**.
1. Wählen Sie **Gerät hinzufügen**aus, geben Sie einen Quell Servernamen ein, und klicken Sie dann auf **OK**. <br>Wiederholen Sie dies für alle anderen Server, die Sie inventarisieren möchten.
1. Wählen Sie Überprüfung **starten**aus.<br>Die Seite wird aktualisiert und zeigt an, wann die Überprüfung beendet ist.
    ![Screenshot, der einen zu überprüfenden](media/migrate/inventory.png) **Server anzeigt Abbildung 2: Inventarisierung von Servern**
1. Wählen Sie jeden Server aus, um die inventarisierten Freigaben, Konfigurationen, Netzwerkadapter und Volumes zu überprüfen. <br><br>Der Speicher Migrationsdienst überträgt keine Dateien oder Ordner, die mit dem Windows-Vorgang beeinträchtigt werden könnten. in diesem Release werden also Warnungen für alle Freigaben im Windows-Systemordner angezeigt. Sie müssen diese Freigaben während der Übertragungs Phase überspringen. Weitere Informationen finden Sie unter [welche Dateien und Ordner sind von Übertragungen ausgeschlossen](faq.md#what-files-and-folders-are-excluded-from-transfers).
1. Wählen Sie **weiter** aus, um mit der Datenübertragung fortzufahren.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>Schritt 2: Übertragen von Daten von ihren alten Servern auf die Zielserver

In diesem Schritt übertragen Sie die Daten, nachdem Sie angegeben haben, wo Sie auf den Ziel Servern abgelegt werden sollen.

1. Geben Sie auf der Seite Anmelde Informationen für **Übertragungsdaten** > **eingeben** Administrator Anmelde Informationen ein, die auf den Ziel Servern funktionieren, zu denen Sie migrieren möchten, und klicken Sie dann auf **weiter**.
2. Auf der Seite **Zielgerät und Zuordnungen hinzufügen** wird der erste Quell Server aufgeführt. Geben Sie den Namen des Servers ein, zu dem Sie migrieren möchten, und wählen Sie dann **Gerät scannen**aus.
3. Ordnen Sie die Quellvolumes den Zielvolumes zu, deaktivieren Sie das Kontrollkästchen **einschließen** für alle Freigaben, die Sie nicht übertragen möchten (einschließlich administrativer Freigaben im Windows-Systemordner), und klicken Sie dann auf **weiter**.
   ![Screenshot, der einen Quell Server und seine Volumes und Freigaben anzeigt und an den Sie in der Ziel](media/migrate/transfer.png) **Abbildung 3 übertragen werden: Einen Quell Server und an den Speicherort, an den der Speicher übertragen wird**
4. Fügen Sie einen Zielserver und Zuordnungen für alle weiteren Quell Server hinzu, und klicken Sie dann auf **weiter**.
5. Passen Sie die Übertragungs Einstellungen optional an, und klicken Sie dann auf **weiter**.
6. Wählen Sie überprüfen, und klicken Sie dann auf **weiter**.
7. Wählen Sie **Übertragung starten** , um die Datenübertragung zu starten<br>Wenn Sie das erste Mal übertragen, verschieben wir alle vorhandenen Dateien in einem Ziel in einen Sicherungsordner. Bei nachfolgenden Übertragungen aktualisieren wir das Ziel standardmäßig, ohne es zuerst zu sichern. <br>Außerdem ist der Storage Migration Service intelligent genug, um überlappende Freigaben zu umgehen – wir kopieren dieselben Ordner nicht zweimal in denselben Auftrag.
8. Überprüfen Sie nach Abschluss der Übertragung den Zielserver, um sicherzustellen, dass alles ordnungsgemäß übertragen wurde. Wählen Sie **nur Fehlerprotokoll** aus, wenn Sie ein Protokoll aller Dateien herunterladen möchten, die nicht übertragen wurden.

   > [!NOTE]
   > Wenn Sie einen Audit-Trail für Übertragungen behalten möchten oder planen, mehr als eine Übertragung in einem Auftrag auszuführen, klicken Sie auf **Protokoll übertragen** , um eine CSV-Kopie zu speichern. Bei jeder nachfolgenden Übertragung werden die Datenbankinformationen einer vorherigen Testlauf überschrieben. 

An diesem Punkt haben Sie drei Möglichkeiten:

- **Fahren Sie mit dem nächsten Schritt**fort, sodass die Zielserver die Identitäten der Quell Server übernehmen.
- Beachten Sie, dass **die Migration komplett** ist, ohne die Identitäten der Quell Server zu übernehmen.
- Wird **erneut übertragen**, wobei nur Dateien kopiert werden, die seit der letzten Übertragung aktualisiert wurden.

Wenn Sie die Dateien mit Azure synchronisieren möchten, können Sie die Zielserver nach dem Übertragen von Dateien mit Azure-Dateisynchronisierung oder nach dem übertragen auf die Zielserver einrichten (Weitere Informationen finden Sie unter [Planning for a Azure-Dateisynchronisierung Deployment](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)).

## <a name="step-3-optionally-cut-over-to-the-new-servers"></a>Schritt 3: Optional an die neuen Server überspringen

In diesem Schritt können Sie die Quell Server auf die Zielserver übertragen und die IP-Adressen und Computernamen auf die Zielserver verschieben. Nachdem dieser Schritt abgeschlossen ist, greifen apps und Benutzer über die Namen und Adressen der Server, von denen aus migriert wurde, auf die neuen Server zu.

 1. Wenn Sie vom Migrations Auftrag aus navigiert sind, navigieren Sie im Windows Admin Center zu **Server-Manager** > **Storage Migration Service** , und wählen Sie dann den Auftrag aus, den Sie ausführen möchten. 
 1. Wählen Sie auf der Seite zum**eingeben der Anmelde** Informationen **für neue Server** > die Option **weiter** aus, um die zuvor eingegebenen Anmelde Informationen zu verwenden.
 1. Geben Sie auf der Seite **Konfigurieren** des umgebers an, welche Netzwerkadapter für die einzelnen Quell Geräteeinstellungen übernommen werden sollen. Dadurch wird die IP-Adresse von der Quelle zum Ziel als Teil des umgebers verschoben.
 1. Geben Sie an, welche IP-Adresse für den Quell Server verwendet werden soll, nachdem der Umstellung seine Adresse zum Ziel verschoben hat. Sie können DHCP oder eine statische Adresse verwenden. Wenn eine statische Adresse verwendet wird, muss das neue Subnetz mit dem alten Subnetz identisch sein, oder der Umstellung schlägt fehl.
    ![Screenshot, der einen Quell Server und seine IP-Adressen und Computernamen anzeigt und nach dem Umstellung](media/migrate/cutover.png)
     **-Wert 4 ersetzt wird: Einen Quell Server und die Art und Weise, wie die Netzwerkkonfiguration auf das Ziel verschoben wird**
 1. Geben Sie an, wie der Quell Server umbenannt werden soll, nachdem der Zielserver seinen Namen übernommen hat. Sie können einen zufällig generierten Namen verwenden oder einen selbst eingeben. Klicken Sie dann auf **weiter**.
 1. Wählen Sie auf der Seite Einstellungen für den **Umschalter anpassen** die Option **weiter** aus.
 1. Wählen Sie überprüfen auf der Seite **Quell-und Zielgerät** überprüfen aus, und klicken Sie dann auf **weiter**.
 1. Wenn Sie bereit sind, den Umschalter auszuführen, wählen Sie die Option **Start**Seite aus. <br>Benutzer und Apps können Unterbrechungen auftreten, während die Adressen und Namen verschoben werden und die Server mehrmals neu gestartet werden, aber andernfalls von der Migration nicht betroffen sind. Wie lange es dauert, hängt von der Art und Weise ab, wie schnell der Server neu gestartet wird, sowie von Active Directory und DNS-Replikations Zeiten.

## <a name="see-also"></a>Siehe auch

- [Übersicht über den Speicher Migrationsdienst](overview.md)
- [Häufig gestellte Fragen (FAQ) zu Storage Migration Services](faq.md)
- [Planen einer Azure-Dateisynchronisierung Bereitstellung](https://docs.microsoft.com/azure/storage/files/storage-sync-files-planning)
