---
title: Sichern Sie Ihre Windows-Servern über Windows Admin Center mit Azure Backup
description: Verwenden Sie Windows Admin Center (Projekt Honolulu) und Backup Windows Server mit Azure-Sicherung
ms.technology: manage
ms.topic: article
author: saurabhsensharma
ms.author: saurse
ms.date: 03/25/2019
ms.localizationpriority: low
ms.prod: windows-server-threshold
ms.openlocfilehash: 3983d0b65bc69ef9fd40f3c8e196d40534b1b8f9
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296910"
---
# Sichern Sie Ihre Windows-Servern über Windows Admin Center mit Azure Backup

>Gilt für: Windows Admin Center-Vorschau, Windows Admin Center

[Weitere Informationen über die Integration von Azure finden Sie im Windows Admin Center.](../plan/azure-integration-options.md)

Windows Admin Center optimiert den Prozess zum Sichern von Windows-Servern in Azure und Schutz vor unbeabsichtigte oder böswillige gelöschter, eine Beschädigung und sogar Ransomware. Um den Setup zu automatisieren, können Sie das Windows Admin Center-Gateway verbinden

Verwenden Sie die folgende Informationen zum Konfigurieren von Sicherung für Sie Windows Server und erstellen eine Sicherung-Richtlinie zum Sichern des Servers Volumes und den Status der Windows-System aus dem Windows Admin Center.

## Was ist Azure Backup, und wie funktioniert es mit Windows Admin Center? 

**Azure Backup** ist der Azure-basierte können Sie sichern (oder schützen) und Wiederherstellen von Daten in der Microsoft-Cloud. Azure Backup ersetzt Ihrer vorhandenen lokalen oder externen backup-Lösung mit einer Cloud-basierte Lösung, die eine zuverlässige, sichere und Kosten Wettbewerbsvorteil ist.
[Erfahren Sie mehr über Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Azure Backup bietet mehrere Komponenten, die Sie herunterladen und Bereitstellen auf dem entsprechenden Computer, Server oder in der Cloud. Die Komponente oder Agent, die Sie bereitstellen, hängt davon ab, was Sie schützen möchten. Alle Azure Backup-Komponenten (unabhängig davon, ob schützen Sie Daten lokal sind oder in Azure) können verwendet werden, Sichern von Daten zu einem Recovery Services Vault in Azure.

Die Integration von Azure Backup im Windows Admin Center ist ideal für das Sichern von Volumes und die Windows-System Zustand lokale Windows physischen oder virtuellen Server. Dies sorgt für einen umfassenden Mechanismus zur Sicherung Dateiserver, Domänencontroller und IIS-Webserver.

Windows Admin Center stellt die Integration Azure Backup, über das systemeigene **Backup** -Tool zur Verfügung. Das **Backup** -Tool bietet, Einrichtung, Verwaltung und Überwachung Umgebungen, um schnell zu starten, Sichern von Servern, führen Sie allgemeine Sicherung und Wiederherstellung und zum Überwachen des backup Integrität der von Windows-Servern.

## Erforderliche Komponenten und Planung

- Ein Azure-Konto mit mindestens ein aktives Abonnement
- Das Ziel von Windows Server, auf denen Sie möchten Sicherung müssen Zugriff auf das Internet zu Azure
- [Verbinden Sie das Windows Admin Center-Gateway auf Azure](azure-integration.md)

Um den Workflow zum Sichern Ihrer Windows-Server zu starten, Öffnen einer Server-Verbindungs, klicken Sie auf dem **Backup** -Tool, und führen Sie die unten aufgeführten Schritte.

## Einrichten von Azure-Sicherung
Wenn Sie für die **Sicherung** Tool, das für die Verbindung mit einem auf dem Azure Backup noch nicht aktiviert ist klicken, würden Sie die Willkommensseite **, Azure Backup** sehen. Klicken Sie auf die Schaltfläche **Azure Backup einrichten** . Dadurch wird der Azure Backup-Setup-Assistent geöffnet. Führen Sie die Schritte im Assistenten zum Sichern des Servers unten aufgeführt.

Wenn Azure Backup bereits konfiguriert ist, wird durch Klicken auf das Tool **Sicherung** **Sicherung Dashboard**geöffnet. Siehe Abschnitt ([Verwaltung und Überwachung](#management-and-monitoring)) zu ermitteln, Vorgänge und Aufgaben, die über das Dashboard ausgeführt werden können.

### Schritt 1: Anmeldung bei Microsoft Azure
Sie Azure-Konto anzumelden. 

> [!NOTE]
> Wenn Sie das Windows Admin Center-Gateway mit Azure verbunden haben, sollten Sie automatisch in Azure angemeldet sein. Klicken Sie auf **Abmeldung** weiter als anderer Benutzer anmelden.

### Schritt 2: Einrichten von Azure Backup
Wählen Sie die entsprechenden Einstellungen für Azure Backup, wie unten beschrieben

 - **Abonnement-Id:** Das Azure-Abonnement Sichern des Windows-Servers in Azure verwenden möchten. Alle Azure Ressourcen wie der Azure-Ressourcengruppe, wird die Recovery Services Vault in das ausgewählte Abonnement erstellt.
 - **Tresor:** Die Recovery Services Vault, in denen der Server Sicherungen gespeichert werden. Sie können aus vorhandenen Depots auswählen, oder Windows Admin Center erstellt ein neues Depot.  
 - **Ressourcengruppe:** Der Azure-Ressourcengruppe ist ein Container für eine Sammlung von Ressourcen. Die Recovery Services Vault erstellt oder in der angegebenen Ressourcengruppe enthalten sind. Sie können aus vorhandenen Ressourcengruppen auswählen, oder Windows Admin Center wird ein neues Konto erstellen.
 - **Speicherort:** Der Azure-Region, in denen die Recovery Services Vault erstellt wird. Es wird empfohlen, die Azure-Region des nächstgelegenen an den Windows-Server auszuwählen.

### Wählen Sie Schritt 3: Backup Elemente und Zeitplan aus

- Wählen Sie, was Sie von Ihrem Server zu sichern, Sie möchten. Windows Admin Center können Sie aus einer Kombination des **Volumes** und den **Status des Windows-System** , bietet Ihnen die geschätzte Größe der Daten, die ausgewählt werden für die Sicherung auswählen.

> [!NOTE]
> Die erste Sicherung ist eine vollständige Sicherung aller ausgewählten Daten. Allerdings nachfolgenden Sicherungen inkrementeller Natur sind und nur die Änderungen an den Daten übertragen, seit der letzten Sicherung.

- Wählen Sie aus mehreren voreingestellten **Sicherung Zeitpläne** für Sie Systemzustand bzw. Volumes.

### Schritt 4: Geben Sie Verschlüsselung Passphrase

- Geben Sie eine **Verschlüsselung Passphrase** Ihrer Wahl (mindestens 16 Zeichen).  **Azure Backup** schützt Ihre backup-Daten mit einer Passphrase benutzerkonfigurierten und Benutzer verwaltetes Verschlüsselung. Die Verschlüsselung Passphrase ist erforderlich, um Azure Backup Daten wiederherzustellen.

> [!NOTE]
> Die Passphrase muss an einem sicheren externen Ort wie z. B. einem anderen Server oder den [Azure dem Schlüsseltresor](https://docs.microsoft.com/azure/key-vault/quick-create-portal)gespeichert werden. Microsoft kann nicht store die Passphrase und abgerufen werden sollen oder nicht die Passphrase zurückgesetzt, wenn es verloren oder vergessen.

- Überprüfen Sie alle Einstellungen, und klicken Sie auf **Übernehmen**

Windows Admin Center wird dann die folgenden Vorgänge auszuführen.

1. Erstellen Sie ein Azure-Ressourcengruppe, wenn es nicht bereits vorhanden ist
2. Erstellen Sie eine Azure Recovery Services Vault gemäß der Angabe
3. Installieren und Microsoft Azure Recovery Services-Agent zum Tresor registrieren
4. Erstellen Sie die Sicherung und Aufbewahrung Zeitplan gemäß den ausgewählten Optionen, und ordnen Sie diese mit dem Windows-Server.

## Verwaltung und Überwachung

Nachdem Sie erfolgreich Setup Azure Backup haben, würde die **Sicherung Dashboard** angezeigt, wenn Sie das Tool Sicherung für eine vorhandene Server-Verbindung öffnen. Sie können die folgenden Aufgaben aus dem **Sicherung-Dashboard** ausführen.

- **Zugriff auf den Azure-Tresor:** Sie können auf den Link **Recovery Services Vault** in der Registerkarte " **Übersicht** " **Backup-Dashboard** zum Tresor im Azure weitergeleitet werden, um einen [umfassenden Satz von Management-Vorgänge](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server) auszuführen klicken.
- **Führen Sie eine ad-hoc-Sicherung:** Klicken Sie auf **Jetzt sichern,** um eine ad-hoc-Sicherung zu ergreifen. 
- **Monitor Aufträge und Konfigurieren von Benachrichtigung:** Navigieren Sie zur Registerkarte **Aufträge** des Dashboards für kontinuierliches überwachen oder vergangene Aufträge und [Konfigurieren von warnungsbenachrichtigungen](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server#configuring-notifications-for-alerts) , erhalten Sie e-Mails für alle Fehler Aufträge oder andere backup dateibezogene Warnungen.
- **Ansicht Wiederherstellungspunkte und Wiederherstellen von Daten:** Klicken Sie auf der Registerkarte " **Wiederherstellungspunkte** " des Dashboards für die Wiederherstellungspunkte anzeigen, und klicken auf **Daten wiederherstellen** Schritte, die Sie Daten von Azure wiederhergestellt.