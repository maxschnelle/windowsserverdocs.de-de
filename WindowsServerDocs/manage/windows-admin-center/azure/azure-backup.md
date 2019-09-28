---
title: Sichern Sie Ihre Windows-Server aus dem Windows Admin Center mit Azure Backup
description: Verwenden des Windows Admin Centers (Project Honolulu) zum Sichern von Windows-Servern mit Azure Backup
ms.technology: manage
ms.topic: article
author: saurabhsensharma
ms.author: saurse
ms.date: 03/25/2019
ms.localizationpriority: low
ms.prod: windows-server
ms.openlocfilehash: 77171e638fa1eb8c612bdc168868d8286ed23bb6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357404"
---
# <a name="backup-your-windows-servers-from-windows-admin-center-with-azure-backup"></a>Sichern Sie Ihre Windows-Server aus dem Windows Admin Center mit Azure Backup

>Gilt für: Windows Admin Center Preview, Windows Admin Center

[Erfahren Sie mehr über die Azure-Integration in Windows Admin Center.](../plan/azure-integration-options.md)

Windows Admin Center optimiert den Prozess der Sicherung Ihrer Windows-Server in Azure und schützt Sie vor versehentlichen oder bösartigen Löschungen, Beschädigungen und sogar Ransomware. Um den Setup zu automatisieren, können Sie das Windows Admin Center-Gateway verbinden

Verwenden Sie die folgenden Informationen zum Konfigurieren der Sicherung für Ihren Windows-Server, und erstellen Sie eine Sicherungs Richtlinie zum Sichern der Server Volumes und des Windows-System Status aus dem Windows Admin Center.

## <a name="what-is-azure-backup-and-how-does-it-work-with-windows-admin-center"></a>Was ist Azure Backup und wie funktioniert es mit dem Windows Admin Center? 

**Azure Backup** ist der Azure-basierte Dienst, den Sie zum Sichern (bzw. schützen) und Wiederherstellen Ihrer Daten in der Microsoft-Cloud verwenden können. Azure Backup ersetzt ihre vorhandene lokale oder externe Sicherungs Lösung durch eine cloudbasierte Lösung, die zuverlässig, sicher und kostengünstig ist.
[Erfahren Sie mehr über Azure Backup](https://docs.microsoft.com/azure/backup/backup-overview).

Azure Backup bietet mehrere Komponenten, die Sie herunterladen und auf dem entsprechenden Computer, Server oder in der Cloud bereitstellen. Die Komponente oder der Agent, die Sie bereitstellen, hängt davon ab, was Sie schützen möchten. Alle Azure Backup Komponenten (unabhängig davon, ob Sie Daten lokal oder in Azure schützen) können verwendet werden, um Daten in einem Recovery Services Tresor in Azure zu sichern.

Die Integration von Azure Backup in das Windows Admin Center eignet sich ideal für das Sichern von Volumes und den lokalen Windows-System Status von physischen oder virtuellen Windows-Servern. Dies stellt einen umfassenden Mechanismus zum Sichern von Dateiservern, Domänen Controllern und IIS-Webservern dar.

Das Windows Admin Center macht die Azure Backup Integration über das Native **Sicherungs** Tool verfügbar. Das **Sicherungs** Tool ermöglicht die Einrichtung, Verwaltung und Überwachung, um schnell mit der Sicherung Ihrer Server zu beginnen, häufige Sicherungs-und Wiederherstellungs Vorgänge durchzuführen und den Gesamt Sicherungs Zustand Ihrer Windows-Server zu überwachen.

## <a name="prerequisites-and-planning"></a>Erforderliche Komponenten und Planung

- Ein Azure-Konto mit mindestens einem aktiven Abonnement
- Die Ziel-Windows-Server, die Sie sichern möchten, müssen über Internet Zugang zu Azure verfügen.
- [Verbinden Ihres Windows Admin Center-Gateways mit Azure](azure-integration.md)

Um den Workflow zum Sichern Ihres Windows-Servers zu starten, öffnen Sie eine Server Verbindung, klicken Sie auf das **Sicherungs** Tool, und führen Sie die unten aufgeführten Schritte aus.

## <a name="setup-azure-backup"></a>Setup-Azure Backup
Wenn Sie auf das **Sicherungs** Tool für eine Server Verbindung klicken, auf der Azure Backup noch nicht aktiviert ist, sehen Sie den Bildschirm **Willkommen bei Azure Backup** . Klicken Sie auf die Schaltfläche **Azure Backup einrichten** . Dadurch wird der Azure Backup Setup-Assistenten geöffnet. Führen Sie die unten aufgeführten Schritte im Assistenten aus, um den Server zu sichern.

Wenn Azure Backup bereits konfiguriert ist, wird das **Backup-Dashboard**durch Klicken auf das **Sicherungs** Tool geöffnet. Informationen zu Vorgängen und Tasks, die über das Dashboard ausgeführt werden können, finden Sie im Abschnitt ([Verwaltung und Überwachung](#management-and-monitoring)).

### <a name="step-1-login-to-microsoft-azure"></a>Schritt 1: Anmelden bei Microsoft Azure
Melden Sie sich bei Ihrem Azure-Konto an. 

> [!NOTE]
> Wenn Sie Ihr Windows Admin Center-Gateway mit Azure verbunden haben, sollten Sie automatisch bei Azure angemeldet werden. Sie können auf **Abmelden** klicken, um sich als anderer Benutzer anzumelden.

### <a name="step-2-set-up-azure-backup"></a>Schritt 2: Einrichten Azure Backup
Wählen Sie die entsprechenden Einstellungen für Azure Backup wie unten beschrieben aus.

 - **Abonnement-ID:** Das Azure-Abonnement, das Sie für die Sicherung Ihres Windows Servers in Azure verwenden möchten. Alle Azure-Ressourcen, z. b. die Azure-Ressourcengruppe Recovery Services, werden im ausgewählten Abonnement erstellt.
 - **Blicken** Der Recovery Services Tresor, in dem die Sicherungen der Server gespeichert werden. Sie können aus vorhandenen Tresoren auswählen, oder das Windows Admin Center erstellt einen neuen Tresor.  
 - **Ressourcengruppe:** Die Azure-Ressourcengruppe ist ein Container für eine Sammlung von Ressourcen. Der Recovery Services Tresor wird erstellt oder ist in der angegebenen Ressourcengruppe enthalten. Sie können aus vorhandenen Ressourcengruppen auswählen, oder das Windows Admin Center erstellt ein neues.
 - **Pfad:** Die Azure-Region, in der der Recovery Services Tresor erstellt wird. Es wird empfohlen, die Azure-Region, die dem Windows-Server am nächsten ist, auszuwählen.

### <a name="step-3-select-backup-items-and-schedule"></a>Schritt 3: Sicherungselemente und Zeitplan auswählen

- Wählen Sie aus, was Sie auf Ihrem Server sichern möchten. Mithilfe des Windows Admin Centers können Sie eine Kombination aus **Volumes** und dem **Windows-System Status** auswählen und gleichzeitig die geschätzte Größe der Daten angeben, die für die Sicherung ausgewählt werden.

> [!NOTE]
> Die erste Sicherung ist eine vollständige Sicherung aller ausgewählten Daten. Nachfolgende Sicherungen sind jedoch inkrementell und übertragen nur die Änderungen an den Daten seit der letzten Sicherung.

- Wählen Sie aus mehreren vordefinierten **Sicherungs Zeitplänen** für Ihren System Status und/oder Volumes aus.

### <a name="step-4-enter-encryption-passphrase"></a>Schritt 4: Verschlüsselungs Passphrase eingeben

- Geben Sie eine **Verschlüsselungs Passphrase** Ihrer Wahl ein (mindestens 16 Zeichen).  **Azure Backup** sichert Ihre Sicherungsdaten mit einer vom Benutzer konfigurierten und von der Benutzer verwalteten Verschlüsselungs Passphrase. Die Verschlüsselungs Passphrase ist erforderlich, um Daten aus Azure Backup wiederherzustellen.

> [!NOTE]
> Die Passphrase muss an einem sicheren externen Speicherort gespeichert werden, z. b. auf einem anderen Server oder dem [Azure Key Vault](https://docs.microsoft.com/azure/key-vault/quick-create-portal). Microsoft speichert die Passphrase nicht und kann die Passphrase nicht abrufen oder zurücksetzen, wenn Sie verloren geht oder vergessen wird.

- Überprüfen Sie alle Einstellungen, und klicken Sie auf **anwenden** .

Das Windows Admin Center führt dann die folgenden Vorgänge aus:

1. Erstellen Sie eine Azure-Ressourcengruppe, wenn Sie nicht bereits vorhanden ist.
2. Erstellen eines Azure Recovery Services-Tresors wie angegeben
3. Installieren und Registrieren des Microsoft Azure Recovery Services-Agents für den Tresor
4. Erstellen Sie den Sicherungs-und Beibehaltungs Zeitplan gemäß den ausgewählten Optionen, und ordnen Sie diese dem Windows-Server zu.

## <a name="management-and-monitoring"></a>Verwaltung und Überwachung

Wenn Sie Azure Backup erfolgreich eingerichtet haben, wird das Backup- **Dashboard** angezeigt, wenn Sie das Sicherungs Tool für eine vorhandene Server Verbindung öffnen. Sie können die folgenden Aufgaben über das **Backup-Dashboard** ausführen.

- **Greifen Sie auf den Tresor in Azure zu:** Sie können auf den Link **Recovery Services** Tresor auf der Registerkarte " **Übersicht** " des **Sicherungs Dashboards** klicken, um den Tresor in Azure zu erstellen und einen [umfangreichen Satz von Verwaltungs Vorgängen](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server) auszuführen.
- **Führen Sie eine Ad-hoc-Sicherung aus:** Klicken Sie auf **jetzt sichern** , um eine Ad-hoc-Sicherung durchführen. 
- **Überwachen von Aufträgen und Konfigurieren von Warn Benachrichtigungen:** Navigieren Sie zur Registerkarte **Aufträge** des Dashboards, um laufende oder vergangene Aufträge zu überwachen, und [Konfigurieren Sie Warn Benachrichtigungen](https://docs.microsoft.com/azure/backup/backup-azure-manage-windows-server#configuring-notifications-for-alerts) , um e-Mails für fehlerhafte Aufträge oder andere Sicherungs relevante Warnungen zu erhalten.
- **Anzeigen von Wiederherstellungs Punkten und Wiederherstellen von Daten:** Klicken Sie im Dashboard auf die Registerkarte **Wiederherstellungspunkte** , um die Wiederherstellungspunkte anzuzeigen, und klicken Sie auf **Daten wiederherstellen** , um die Daten aus Azure wiederherzustellen.