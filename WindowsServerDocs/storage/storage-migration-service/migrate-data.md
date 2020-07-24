---
title: Migrieren eines Dateiservers mithilfe von Storage Migration Service
description: Kurze Beschreibung des Themas für Suchmaschinenergebnisse
author: jasongerend
ms.author: jgerend
manager: elizapo
ms.date: 03/25/2020
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: cd8c41e67baf0ffa0399e62ad2a697e4efa1433f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86965182"
---
# <a name="use-storage-migration-service-to-migrate-a-server"></a>Verwenden von Storage Migration Service zum Migrieren eines Servers

In diesem Thema wird erläutert, wie Sie einen Server, einschließlich seiner Dateien und Konfiguration, mithilfe von [Storage Migration Service](overview.md) und Windows Admin Center zu einem anderen Server migrieren. Die Migration dauert drei Schritte, nachdem Sie den Dienst installiert und alle erforderlichen Firewallports geöffnet haben: Inventarisieren der Server, übertragen von Daten und übernehmen an die neuen Server.

## <a name="step-0-install-storage-migration-service-and-check-firewall-ports"></a>Schritt 0: Installieren von Storage Migration Service und Überprüfen der Firewallports

Bevor Sie beginnen, installieren Sie den Speicher Migrationsdienst, und stellen Sie sicher, dass die erforderlichen Firewallports geöffnet sind.

1. Überprüfen Sie die Anforderungen an den [Speicher Migrationsdienst](overview.md#requirements) , und installieren Sie das [Windows Admin Center](../../manage/windows-admin-center/overview.md) auf Ihrem PC oder eine Management Server, sofern noch nicht geschehen. Wenn Sie in die Domäne eingebundenen Quell Computern migrieren, müssen Sie den Speicher Migrationsdienst auf einem Server installieren und ausführen, der der gleichen Domäne oder Gesamtstruktur wie die Quellcomputer beigetreten ist.
2. Stellen Sie im Windows Admin Center eine Verbindung zum Orchestrator-Server her, auf dem Windows Server 2019 ausgeführt wird. <br>Dies ist der Server, auf dem Sie den Speicher Migrationsdienst installieren und zum Verwalten der Migration verwenden. Wenn Sie nur einen Server migrieren, können Sie den Zielserver verwenden, sofern er Windows Server 2019 ausgeführt wird. Es wird empfohlen, einen separaten Orchestrierungs Server für multiservermigrationen zu verwenden.
3. Wechseln Sie zu **Server-Manager** (in Windows Admin Center) > **Storage Migration Service** , und wählen Sie **Installieren** aus, um den Speicher Migrationsdienst und die erforderlichen Komponenten zu installieren (siehe Abbildung 1).
    ![Screenshot der Seite "Storage Migration Service" mit der Installations Schaltfläche ](media/migrate/install.png) **Abbildung 1: Installieren von Storage Migration Service**
4. Installieren Sie den Speicher Migrationsdienst-Proxy auf allen Ziel Servern, auf denen Windows Server 2019 ausgeführt wird. Dadurch wird die Übertragungsgeschwindigkeit bei der Installation auf den Ziel Servern verdoppelt. <br>Stellen Sie hierzu im Windows Admin Center eine Verbindung mit dem Zielserver her, und navigieren Sie dann zu **Server-Manager** (im Windows Admin Center) > **Rollen und Features**, > **Features**, wählen Sie **Speicher Migrationsdienst-Proxy**aus, und wählen Sie dann **Installieren**aus.
5. Wenn Sie beabsichtigen, zu oder von Windows-Failoverclustern zu migrieren, installieren Sie die Failoverclustering-Tools auf dem Orchestrator-Server. <br>Stellen Sie hierzu im Windows Admin Center eine Verbindung mit dem Orchestrator-Server her, und navigieren Sie dann zu **Server-Manager** (im Windows Admin Center) > **Rollen und Features**> **Features**, > **Remoteserver-Verwaltungstools**, > **featureverwaltungtools**, wählen Sie **Failoverclustering-Tools**aus, und wählen Sie dann **Installieren**aus.
6. Stellen Sie auf allen Quell Servern und auf allen Ziel Servern, auf denen Windows Server 2012 R2 oder Windows Server 2016 ausgeführt wird, im Windows Admin Center eine Verbindung zu jedem Server her, navigieren Sie zu **Server-Manager** (in Windows Admin Center) > **Firewall**  >  **eingehende**Firewall-Regeln, und überprüfen Sie dann, ob die folgenden Regeln aktiviert sind:
    - Datei- und Druckerfreigabe (SMB eingehend)
    - Anmeldedienst (NP-in)
    - Windows Management Instrumentation (DCOM-In)
    - Windows Management Instrumentation (WMI-In)

   Wenn Sie Firewalls von Drittanbietern verwenden, sind die zu öffnenden eingehenden Port Bereiche TCP/445 (SMB), TCP/135 (RPC/DCOM Endpoint Mapper) und TCP 1025-65535 (kurzlebige RPC/DCOM-Ports). Die Ports für den Speicher Migrationsdienst sind TCP/28940 (Orchestrator) und TCP/28941 (Proxy).

7. Wenn Sie einen Orchestrator-Server zum Verwalten der Migration verwenden und Ereignisse oder ein Protokoll der übertragenden Daten herunterladen möchten, überprüfen Sie, ob die Firewallregel für die Datei-und Druckerfreigabe (SMB-in) ebenfalls auf diesem Server aktiviert ist.

## <a name="step-1-create-a-job-and-inventory-your-servers-to-figure-out-what-to-migrate"></a>Schritt 1: Erstellen eines Auftrags und Inventarisieren der Server, um herauszufinden, was migriert werden soll

In diesem Schritt geben Sie an, welche Server migriert werden sollen, und Scannen Sie anschließend, um Informationen zu Ihren Dateien und Konfigurationen zu sammeln.

1. Wählen Sie **Neuer Auftrag**, benennen Sie den Auftrag, und wählen Sie dann aus, ob Windows-Server und-Cluster oder Linux-Server mit Samba migriert werden sollen. Klicken Sie anschließend auf **OK**.
2. Geben Sie auf der Seite **Anmelde Informationen eingeben** Administrator Anmelde Informationen ein, die auf den Servern funktionieren, von denen Sie migrieren möchten, und klicken Sie dann auf **weiter**. <br>Wenn Sie von Linux-Servern migrieren, geben Sie stattdessen Anmelde Informationen auf den Seiten für **Samba-Anmelde** Informationen und **Linux-Anmelde** Informationen ein, einschließlich eines SSH-Kennworts oder privaten Schlüssels

3. Wählen Sie **Gerät hinzufügen**aus, geben Sie einen Quell Servernamen oder den Namen eines gruppierten Dateiservers ein, und klicken Sie dann auf **OK**. <br>Wiederholen Sie diesen Schritt für alle anderen Server, die Sie inventarisieren möchten.

4. Wählen Sie Überprüfung **starten**aus.<br>Die Seite wird aktualisiert und zeigt an, wann die Überprüfung beendet ist.
    ![Screenshot, der einen zu überprüfenden Server anzeigt ](media/migrate/inventory.png) **Abbildung 2: Inventarisierung von Servern**
5. Wählen Sie jeden Server aus, um die inventarisierten Freigaben, Konfigurationen, Netzwerkadapter und Volumes zu überprüfen. <br><br>Der Speicher Migrationsdienst überträgt keine Dateien oder Ordner, die mit dem Windows-Vorgang beeinträchtigt werden könnten. in diesem Release werden also Warnungen für alle Freigaben im Windows-Systemordner angezeigt. Sie müssen diese Freigaben während der Übertragungs Phase überspringen. Weitere Informationen finden Sie unter [welche Dateien und Ordner sind von Übertragungen ausgeschlossen](faq.md#what-files-and-folders-are-excluded-from-transfers).
6. Wählen Sie **weiter** aus, um mit der Datenübertragung fortzufahren.

## <a name="step-2-transfer-data-from-your-old-servers-to-the-destination-servers"></a>Schritt 2: übertragen von Daten von ihren alten Servern auf die Zielserver

In diesem Schritt übertragen Sie die Daten, nachdem Sie angegeben haben, wo Sie auf den Ziel Servern abgelegt werden sollen.

1. Geben Sie auf der Seite Anmelde Informationen für **Übertragungsdaten**  >  **eingeben** Administrator Anmelde Informationen ein, die auf den Ziel Servern funktionieren, zu denen Sie migrieren möchten, und klicken Sie dann auf **weiter**.
2. Auf der Seite **Zielgerät und Zuordnungen hinzufügen** wird der erste Quell Server aufgeführt. Geben Sie den Namen des Servers oder des gruppierten Dateiservers ein, zu dem Sie migrieren möchten, und wählen Sie dann **Gerät scannen**aus. Wenn Sie von einem in die Domäne eingebundenen Quellcomputer migrieren, muss der Zielserver der gleichen Domäne beitreten. Sie können auch auf "neuen virtuellen Azure-Computer erstellen" klicken und dann mit dem Assistenten einen neuen Zielserver in Azure bereitstellen. Dadurch wird automatisch die Größe Ihres virtuellen Computers, die Bereitstellung von Speicher, das Formatieren von Datenträgern, das beitreten zur Domäne und das Hinzufügen des Speicher Migrationsdienst-Proxy zu einem Windows Server 2019 Sie können zwischen virtuellen Computern unter Windows Server 2019 (empfohlen), Windows Server 2016 und Windows Server 2012 R2 jeder Größe auswählen und Managed Disks verwenden.

    > [!NOTE]
    > Wenn Sie "neuen virtuellen Azure-Computer erstellen" verwenden, benötigen Sie Folgendes:
    > - Ein gültiges Azure-Abonnement.
    > - Eine vorhandene Azure Compute-Ressourcengruppe, für die Sie über die Berechtigung erstellen verfügen.
    > - Eine vorhandene Azure-Virtual Network und ein Subnetz.
    > - Eine Azure Express Route-oder VPN-Lösung, die an die Virtual Network und das Subnetz gebunden ist, die die Konnektivität von dieser Azure-IaaS-VM mit Ihren lokalen Clients, Domänen Controllern, dem Computer mit dem Speicher Migrationsdienst Orchestrator, dem Windows Admin Center-Computer und dem zu migrierenden Quellcomputer zulässt.

    Im folgenden Video wird gezeigt, wie Sie mithilfe von Storage Migration Service zu Azure-VMS migrieren.
    > [!VIDEO https://www.youtube-nocookie.com/embed/k8Z9LuVL0xQ]

3. Ordnen Sie die Quellvolumes den Zielvolumes zu, deaktivieren Sie das Kontrollkästchen **einschließen** für alle Freigaben, die Sie nicht übertragen möchten (einschließlich administrativer Freigaben im Windows-Systemordner), und klicken Sie dann auf **weiter**.
   ![Screenshot, der einen Quell Server und seine Volumes und Freigaben anzeigt und an den Sie auf das Ziel Abbildung 3 übertragen werden ](media/migrate/transfer.png) **: einen Quell Server und an den Speicherort, an den der Speicher übertragen wird**
4. Fügen Sie einen Zielserver und Zuordnungen für alle weiteren Quell Server hinzu, und klicken Sie dann auf **weiter**.
5. Geben Sie auf der Seite **Übertragungs Einstellungen anpassen** an, ob lokale Benutzer und Gruppen auf den Quell Servern migriert werden sollen, und klicken Sie dann auf **weiter**. Auf diese Weise können Sie lokale Benutzer und Gruppen auf den Ziel Servern neu erstellen, damit die Datei-oder Freigabe Berechtigungen, die auf lokale Benutzer und Gruppen festgelegt sind, nicht verloren gehen. Im folgenden finden Sie die Optionen für die Migration lokaler Benutzer und Gruppen:

    - **Konten mit demselben Namen umbenennen** ist standardmäßig ausgewählt und migriert alle lokalen Benutzer und Gruppen auf dem Quell Server. Wenn lokale Benutzer oder Gruppen mit demselben Namen auf der Quelle und dem Ziel gefunden werden, werden Sie auf dem Ziel umbenannt, es sei denn, Sie sind integriert (z. b. der Administrator Benutzer und die Gruppe "Administratoren"). Verwenden Sie diese Einstellung nicht, wenn es sich bei dem Quell-oder Zielserver um einen Domänen Controller handelt.
    - Bei **der Wiederverwendung von Konten mit demselben Namen** werden die Namen Benutzer und Gruppen auf der Quelle und dem Ziel identisch benannt. Verwenden Sie diese Einstellung nicht, wenn es sich bei dem Quell-oder Zielserver um einen Domänen Controller handelt.
    - **Übertragen Sie keine Benutzer und Gruppen** , die die Migration lokaler Benutzer und Gruppen überspringen. Dies ist erforderlich, wenn es sich bei der Quelle oder dem Ziel um einen Domänen Controller handelt, oder wenn Sie Daten für DFS-Replikation (DFS-Replikation unterstützt keine lokalen Gruppen und Benutzer).

   > [!NOTE]
   > Migrierte Benutzerkonten werden auf dem Ziel deaktiviert und ein 127-Zeichen Kennwort zugewiesen, das sowohl komplex als auch zufällig ist. Daher müssen Sie Sie aktivieren und ein neues Kennwort zuweisen, wenn Sie nicht mehr verwenden möchten. Dadurch wird sichergestellt, dass alle alten Konten mit vergessenen und schwachen Kenn Wörtern auf der Quelle kein Sicherheitsproblem auf dem Ziel darstellen. Möglicherweise möchten Sie auch die [lokale Administrator Kennwort-Lösung (Runden)](https://www.microsoft.com/download/details.aspx?id=46899) als Möglichkeit zum Verwalten von lokalen Administrator Kennwörtern ansehen.

6. Wählen Sie überprüfen **, und klicken Sie dann** auf **weiter**.
7. Wählen Sie **Übertragung starten** , um die Datenübertragung zu starten<br>Wenn Sie das erste Mal übertragen, verschieben wir alle vorhandenen Dateien in einem Ziel in einen Sicherungsordner. Bei nachfolgenden Übertragungen aktualisieren wir das Ziel standardmäßig, ohne es zuerst zu sichern. <br>Außerdem ist der Storage Migration Service intelligent genug, um überlappende Freigaben zu umgehen – wir kopieren dieselben Ordner nicht zweimal in denselben Auftrag.
8. Überprüfen Sie nach Abschluss der Übertragung den Zielserver, um sicherzustellen, dass alles ordnungsgemäß übertragen wurde. Wählen Sie **nur Fehlerprotokoll** aus, wenn Sie ein Protokoll aller Dateien herunterladen möchten, die nicht übertragen wurden.

   > [!NOTE]
   > Wenn Sie einen Überwachungs Pfad für Übertragungen behalten möchten oder planen, mehr als eine Übertragung in einem Auftrag auszuführen, klicken Sie auf **Protokoll übertragen** oder die anderen Protokoll Speicheroptionen, um eine CSV-Kopie zu speichern. Bei jeder nachfolgenden Übertragung werden die Datenbankinformationen einer vorherigen Testlauf überschrieben.

An diesem Punkt haben Sie drei Möglichkeiten:

- **Fahren Sie mit dem nächsten Schritt**fort, sodass die Zielserver die Identitäten der Quell Server übernehmen.
- Beachten Sie, dass **die Migration komplett** ist, ohne die Identitäten der Quell Server zu übernehmen.
- Wird **erneut übertragen**, wobei nur Dateien kopiert werden, die seit der letzten Übertragung aktualisiert wurden.

Wenn Sie die Dateien mit Azure synchronisieren möchten, können Sie die Zielserver nach dem Übertragen von Dateien mit Azure-Dateisynchronisierung oder nach dem übertragen auf die Zielserver einrichten (Weitere Informationen finden Sie unter [Planning for a Azure-Dateisynchronisierung Deployment](/azure/storage/files/storage-sync-files-planning)).

## <a name="step-3-cut-over-to-the-new-servers"></a>Schritt 3: Ausschneiden zu den neuen Servern

In diesem Schritt können Sie die Quell Server auf die Zielserver übertragen und die IP-Adressen und Computernamen auf die Zielserver verschieben. Nachdem dieser Schritt abgeschlossen ist, greifen apps und Benutzer über die Namen und Adressen der Server, von denen aus migriert wurde, auf die neuen Server zu.

1. Wenn Sie vom Migrations Auftrag aus navigiert sind, navigieren Sie im Windows Admin Center zu **Server-Manager**  >  **Storage Migration Service** , und wählen Sie dann den Auftrag aus, den Sie ausführen möchten.
2. Wählen Sie auf der Seite zum Eingeben der Anmelde Informationen **für neue Server**  >  **Enter credentials** die Option **weiter** aus, um die zuvor eingegebenen Anmelde Informationen zu verwenden.

   Wenn es sich bei dem Ziel um einen Cluster Dateiserver handelt, müssen Sie möglicherweise Anmelde Informationen mit Berechtigungen angeben, um den Cluster aus der Domäne zu entfernen, und ihn dann wieder mit dem neuen Namen hinzufügen.

3. Geben Sie auf der Seite **Konfigurieren des umgebers** an, welcher Netzwerkadapter auf dem Ziel die Einstellungen der einzelnen Adapter auf der Quelle übernehmen soll. Dadurch wird die IP-Adresse von der Quelle zum Ziel im Rahmen der Umstellung verschoben, sodass der Quell Server eine neue DHCP-oder statische IP-Adresse hat. Sie haben die Möglichkeit, alle Netzwerk Migrationen oder bestimmte Schnittstellen zu überspringen.
4. Geben Sie an, welche IP-Adresse für den Quell Server verwendet werden soll, nachdem der Umstellung seine Adresse zum Ziel verschoben hat. Sie können DHCP oder eine statische Adresse verwenden. Wenn eine statische Adresse verwendet wird, muss das neue Subnetz mit dem alten Subnetz identisch sein, oder der Umstellung schlägt fehl.
    ![Screenshot, der einen Quell Server und seine IP-Adressen und Computernamen anzeigt und nach dem Umschalter Abbildung 4 ersetzt wird ](media/migrate/cutover.png) **: ein Quell Server und die Art und Weise, wie die Netzwerkkonfiguration zum Ziel** wechselt
5. Geben Sie an, wie der Quell Server umbenannt werden soll, nachdem der Zielserver seinen Namen übernommen hat. Sie können einen zufällig generierten Namen verwenden oder einen selbst eingeben. Wählen Sie **Weiter**aus.
6. Wählen Sie auf der Seite Einstellungen für den **Umschalter anpassen** die Option **weiter** aus.
7. Wählen **Sie überprüfen** auf der Seite **Quell-und Zielgerät** überprüfen aus, und klicken Sie dann auf **weiter**.
8. Wenn Sie bereit sind, den Umschalter auszuführen, wählen Sie die Option **Start**Seite aus. <br>Benutzer und Apps können Unterbrechungen auftreten, während die Adressen und Namen verschoben werden und die Server mehrmals neu gestartet werden, aber andernfalls von der Migration nicht betroffen sind. Wie lange es dauert, hängt von der Art und Weise ab, wie schnell der Server neu gestartet wird, sowie von Active Directory und DNS-Replikations Zeiten.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Übersicht über den Speicher Migrationsdienst](overview.md)
- [Häufig gestellte Fragen (FAQ) zu Storage Migration Services](faq.md)
- [Planung für die Bereitstellung einer Azure-Dateisynchronisierung](/azure/storage/files/storage-sync-files-planning)
