---
title: Vorbereiten des Quell Servers für Windows Server Essentials Migration1
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: f5861ae9-77cb-4d37-b4c5-8f0757213385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d7a718e9e84866b6a1f626499b7e2bec58de498f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80852403"
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Vorbereiten des Quell Servers für Windows Server Essentials Migration1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Führen Sie vorab folgende Schritte aus, um sicherzustellen, dass eine erfolgreiche Migration der Einstellungen und Daten vom Quellserver zum Zielserver möglich ist.  
  
#### <a name="to-prepare-for-migration"></a>So bereiten Sie die Migration vor  
  

1.  [Sichern des Quell Servers](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren der aktuellsten Service Packs](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Auswerten der Integrität des Quell Servers](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [Ausführen des Tools zum Vorbereiten der Migration auf dem Quell Server](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Erstellen eines Plans für die Migration von Branchen Anwendungen](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [Sichern des Quell Servers](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren der aktuellsten Service Packs](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Auswerten der Integrität des Quell Servers](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [Ausführen des Tools zum Vorbereiten der Migration auf dem Quell Server](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Erstellen eines Plans für die Migration von Branchen Anwendungen](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="back-up-your-source-server"></a><a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>Sichern des Quell Servers  
 Sichern Sie den Quellserver, bevor Sie mit dem Migrationsprozess beginnen. Durch diese Sicherung schützen Sie sich vor Datenverlusten, wenn während der Migration ein nicht behebbarer Fehler auftritt.  
  
##### <a name="to-back-up-the-source-server"></a>So sichern Sie den Zielserver  
  
1.  Führen Sie eine vollständige Sicherung des Quellservers durch. Weitere Informationen zum Sichern von Windows Small Business Server 2011 Essentials finden Sie unter [Weitere Informationen zum Einrichten der Server Sicherung](https://technet.microsoft.com/library/server-backup-support-1.aspx).  
  
2.  Überprüfen Sie, ob die Sicherung erfolgreich ausgeführt wurde. Zum Prüfen der Integrität der Sicherung wählen Sie beliebige Dateien der Sicherung aus und stellen diese an einem anderen Speicherort wieder her. Überprüfen Sie dann, ob die wiederhergestellten Dateien mit den Originaldateien identisch sind.  
  
###  <a name="install-the-most-recent-service-packs"></a><a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>Installieren der aktuellsten Service Packs  
 Sie müssen vor der Migration die neuesten Updates und Service Packs auf dem Quellserver installieren.  
  
###  <a name="evaluate-the-health-of-the-source-server"></a><a name="BKMK_UseWindowsBestPracticeAnalyzer"></a>Auswerten der Integrität des Quell Servers  
 Es ist wichtig, dass Sie die Integrität des Quellservers auswerten, bevor Sie mit der Migration beginnen. Verwenden Sie die folgenden Verfahren, um sicherzustellen, dass die Updates aktuell sind, um einen Systemintegritätsbericht zu generieren und das Windows Server Solutions Best Practice Analyzer (BPA) auszuführen.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>Laden Sie kritische und Sicherheits-Updates herunter und installieren sie sie.  
 Durch das Installieren von kritischen und Sicherheits-Updates auf dem Quellserver wird sichergestellt, dass Ihre Migration erfolgreich wird und hilft dabei, Ihr Netzwerk während der Migration zu schützen.  
  
###### <a name="to-check-for-the-latest-updates"></a>So überprüfen Sie die neuesten Updates  
  
1.  Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Programme** und klicken Sie dann auf **Windows Update**.  
  
2.  Klicken Sie auf **Nach Updates suchen**.  
  
3.  Wenn entsprechende Updates ermittelt werden, klicken Sie auf **Updates installieren**.  
  
#### <a name="check-the-alert-viewer-for-critical-errors"></a>Überprüfen Sie die Meldungsanzeige auf schwerwiegende Fehler  
 Sie können die Meldungsanzeige auf dem Dashboard auf schwerwiegende Fehler überprüfen.  
  
#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Führen Sie den Best Practices Analyzer für Windows Server Solutions aus  
 Sie können den Best Practices Analyzer (BPA) für Windows Server Solutions ausführen, um sicherzustellen, dass keine Probleme auf Ihrem Server, Netzwerk, oder Ihrer Domäne vor Beginn des Migrationsvorgangs vorliegen. Das BPA erfasst Konfigurationsinformationen aus den folgenden Quellen:  
  
-   Active Directory&reg; Windows-Verwaltungsinstrumentation (WMI)  
  
-   Registrierung  
  
-   IIS-Metabase (Internet Information Services, Internetinformationsdienste)  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>So analysieren Sie den Quellserver mithilfe des BPA für Windows Server Solutions  
  
1. Laden Sie die [Windows Server-Lösungen Best Practices Analyzer](https://www.microsoft.com/download/details.aspx?id=15556) im Microsoft Download Center herunter, und installieren Sie Sie.  
  
2. Gehen Sie nach dem Abschluss des Downloads auf **Start**, **Alle Programme** und dann auf **SBS Best Practices Analyzer Tool**.  
  
   > [!NOTE]
   >  Suchen Sie vor dem Überprüfen des Servers nach Updates.  
  
3. Klicken Sie im Navigationsbereich auf **Überprüfung starten**.  
  
4. Geben Sie im Detailbereich die Überprüfungsbezeichnung ein und klicken Sie dann auf **Überprüfung starten**. Die Überprüfungsbezeichnung ist der Name des Überprüfungsberichts, z. B. **SBS BPA Scan 1Jul2012**.  
  
5. Nachdem die Überprüfung abgeschlossen ist, klicken Sie auf **Bericht für diese Bewährte Methoden-Überprüfung anzeigen**.  
  
   Nach dem Sammeln von Informationen zur Server-Konfiguration überprüft der Windows Server Solutions BPA, ob die Informationen korrekt sind und wird dann Administratoren eine Liste von Informationen und Problemen nach Schweregrad sortiert anzeigen. Die Liste beschreibt jedes Problem und bietet eine Empfehlung oder eine mögliche Lösung. Folgende drei Berichtstypen sind verfügbar:  
  
|Berichttyp|Beschreibung|  
|-----------------|-----------------|  
|Listenberichte|Zeigt Berichte in einer eindimensionalen Liste an.|  
|Strukturberichte|Zeigt Berichte in einer hierarchischen Liste an.|  
|Andere Berichte|Zeigt Berichte wie z. B. ein Laufzeitprotokoll an.|  
  
 Wenn Sie die Beschreibung und Lösungen für ein Problem anzeigen möchten, klicken Sie im Bericht auf das betreffende Problem. Nicht alle Probleme, die von Windows SB 2011 Essentials BPA gemeldet werden, wirken sich auf die Migration aus. Sie sollten jedoch möglichst viele der Probleme beheben, um eine erfolgreiche Migration sicherzustellen.  
  
####  <a name="synchronize-the-source-server-time-with-an-external-time-source"></a><a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>Synchronisieren der Quell Server Uhrzeit mit einer externen Zeit Quelle  
 Die Uhrzeit auf dem Quellserver darf maximal fünf Minuten von der Uhrzeit auf dem Zielserver abweichen, und die Datums- und Zeitzone muss auf beiden Servern gleich sein. Wenn der Quellserver einen virtuellen Computer ausführt, müssen das Datum, die Uhrzeit und die Zeitzone auf dem Hostserver diesen Angaben auf dem Quell- und dem Zielserver entsprechen. Um sicherzustellen, dass Windows Server Essentials erfolgreich installiert wurde, müssen Sie die Uhrzeit des Quell Servers mit dem NTP-Server (Network Time Protocol) im Internet synchronisieren.  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>So synchronisieren Sie die Uhrzeit des Quellservers mit dem NTP-Server  
  
1.  Melden Sie sich mit einem Domänenadministratorkonto und -kennwort am Quellserver an.  
  
2.  Klicken Sie auf **Start**, dann auf **Ausführen**, geben Sie im Textfeld **cmd** ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Geben Sie an der Eingabeaufforderung w32tm /config /syncfromflags:domhier /reliable:no /update ein, und drücken Sie die EINGABETASTE.  
  
4.  Geben Sie an der Eingabeaufforderung net stop w32time ein, und drücken Sie die EINGABETASTE.  
  
5.  Geben Sie an der Eingabeaufforderung net start w32time ein, und drücken Sie die EINGABETASTE.  
  
> [!IMPORTANT]
>  Während der Installation von Windows Server Essentials haben Sie die Möglichkeit, die Uhrzeit auf dem Ziel Server zu überprüfen und ggf. zu ändern. Stellen Sie sicher, dass die Uhrzeit höchstens fünf Minuten von der Uhrzeit auf dem Quellserver abweicht. Nachdem die Installation abgeschlossen ist, wird der Zielserver mit dem NTP-Server synchronisiert. Alle Computer, die Mitglied der Domäne sind (einschließlich des Quellservers) werden mit dem Zielserver synchronisiert, der die Rolle des Betriebsmasters für den PDC-Emulator (Primary Domain Controller, primärer Domänencontroller) ausübt.  
  
###  <a name="run-the-migration-preparation-tool-on-the-source-server"></a><a name="BKMK_MPT"></a>Ausführen des Tools zum Vorbereiten der Migration auf dem Quell Server  
 Sie können keine Installation im Migrationsmodus durchführen, ohne zuerst auf dem Quellserver das Tool zum Vorbereiten der Migration auszuführen. Mit diesem Tool können Sie den Quell Server und die Domäne für die Migration zu Windows Server Essentials vorbereiten.  
  
> [!IMPORTANT]
>  Sichern Sie den Quellserver, bevor Sie das Tool zum Vorbereiten der Migration ausführen. Keine der Änderungen, die das Tool zum Vorbereiten der Migration am Schema vornimmt, können rückgängig gemacht werden. Wenn während der Migration Probleme auftreten, können Sie den Quellserver nur in den Zustand vor der Ausführung des Tools zurücksetzen, indem Sie den Server aus einer Systemsicherung wiederherstellen.  
  
 Um das Tool zur Vorbereitung der Migration ausführen zu können, müssen Sie Mitglied der Gruppen %%amp;quot;Organisations-Admins%%amp;quot;, %%amp;quot;Schema-Admins%%amp;quot; und %%amp;quot;Domänen-Admins%%amp;quot; sein.  
  
##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>So überprüfen Sie, ob Sie über die geeigneten Berechtigungen zum Ausführen des Tools auf dem Quellserver verfügen  
  
1. Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
  
2. Klicken Sie In der Konsolenstruktur zum Erweitern der Domäne und klicken Sie dann auf **Benutzer**.  
  
3. Klicken Sie mit der rechten Maustaste auf das Administratorkonto, das Sie für die Migration verwenden, und klicken Sie dann auf **Eigenschaften**.  
  
4. Klicken Sie auf die Registerkarte **Mitglied von**, und vergewissern Sie sich dann, dass die Gruppen "Organisations-Admins", "Schema-Admins" und "Domänen-Admins" im Textfeld **Mitglied von** aufgelistet werden.  
  
5. Wenn diese Gruppen nicht aufgelistet werden, klicken Sie auf **Hinzufügen** und fügen dann jede Gruppe hinzu, die nicht aufgelistet wird.  
  
   > [!NOTE]
   > - Möglicherweise wird ein Berechtigungsfehler angezeigt, wenn der Anmeldedienst nicht gestartet wurde.  
   >   -   Sie müssen sich vom Server abmelden und sich dann erneut anmelden, damit die Änderungen wirksam werden.  
  
    Mithilfe der neuesten Version des Windows Update-Agents können Sie sicherstellen, dass das Serverupdate ordnungsgemäß ausgeführt wird.  
  
   Mithilfe der neuesten Version des Windows Update-Agents können Sie sicherstellen, dass das Serverupdate ordnungsgemäß ausgeführt wird.  
  
   Bevor Sie Windows Update-Agent auf dem Quell Server installieren können, müssen Sie zuerst Windows PowerShell 2,0 und Microsoft Baseline Configuration Analyzer 2,0 installieren.  
  
-   Informationen zum herunterladen und Installieren von Windows PowerShell 2,0 finden Sie im [Artikel 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483) der Microsoft Knowledge Base.  
  
-   Informationen zum herunterladen und Installieren von Microsoft Baseline Configuration Analyzer 2,0 finden Sie unter [Microsoft Baseline Configuration Analyzer 2,0](https://go.microsoft.com/fwlink/p/?LinkId=241484) im Microsoft Download Center.  
  
-   Informationen zum herunterladen und Installieren der neuesten Version von Windows Update-Agent finden Sie im [Artikel 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493) in der Microsoft Knowledge Base.  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>So installieren Sie das Tool zum Vorbereiten der Migration auf dem Quellserver und führen es aus  
  
1. Fügen Sie Windows Server Essentials DVD1 in das DVD-Laufwerk auf dem Quell Server ein.  
  
2. Öffnen Sie den Windows-Explorer, navigieren Sie auf der DVD zum Ordner **\support\tools**, und doppelklicken Sie auf die Datei **sourcetool.msi**.  
  
   > [!NOTE]
   > - Wenn das Tool zum Vorbereiten der Migration bereits auf dem Server installiert ist, führen Sie es über das **Start**-Menü aus.  
   >   -   Für eine reibungslose Migration wird empfohlen, immer das aktuellste Update zu installieren.  
  
    Der Assistent installiert das Tool zum Vorbereiten der Migration auf dem Quellserver. Nachdem die Installation abgeschlossen ist, wird das Tool zum Vorbereiten der Migration automatisch ausgeführt, und es installiert die neuesten Updates.  
  
3. Wählen Sie im Tool zum Vorbereiten der Migration die Option **Ich verfüge über eine Datensicherung und bin bereit, den Vorgang fortzusetzen** aus, und klicken Sie dann auf **Weiter**.  
  
   > [!WARNING]
   >  Wenn Sie eine Fehlermeldung im Zusammenhang mit einer Hotfixinstallation erhalten, finden Sie weitere Informationen unter Methode 2: Umbenennen des Ordners "Catroot2" in [Artikel 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672) in der Microsoft Knowledge Base.  
  
    Die Quelldomäne wird durch Erweitern des Active Directory-Schemas für die Migration vorbereitet. Klicken Sie nach Abschluss des Vorgangs auf **Weiter**, um fortzufahren.  
  
4. Nach dem Vorbereiten der Quelldomäne überprüft das Tool zum Vorbereiten der Migration den Quellserver auf zwei Typen potenzieller Probleme.  
  
   - **Fehler** Auf dem Quell Server gefundene Probleme, die die Migration blockieren können oder bewirken, dass die Migration fehlschlägt. Befolgen Sie die Anweisungen in der Fehlermeldung, um die Probleme zu beheben, und klicken Sie dann auf **Erneut überprüfen**.  
  
   - **Warnungen** Auf dem Quell Server gefundene Probleme, die während der Migration funktionale Probleme verursachen können. Es wird dringend empfohlen, die Probleme vor dem Fortsetzen der Migration anhand der Anweisungen in der Fehlermeldung zu beheben.  
  
     Nachdem Sie alle Fehler behoben oder bestätigt haben, klicken Sie auf **Weiter**.  
  
5. Klicken Sie im Tool zum Vorbereiten der Migration auf **Fertig stellen**.  
  
6. Wenn das Tool zum Vorbereiten der Migration abgeschlossen ist, werden Sie möglicherweise aufgefordert, den Quell Server neu zu starten, bevor Sie mit der Migration zu Windows Server Essentials beginnen können.  
  
> [!NOTE]
>  Sie müssen das Tool zum Vorbereiten der Migration innerhalb von zwei Wochen nach der Installation von Windows Server Essentials auf dem Zielserver erfolgreich auf dem Quell Server ausführen. Andernfalls wird die Installation von Windows Server Essentials auf dem Ziel Server blockiert. In diesem Fall müssen Sie das Tool zum Vorbereiten der Migration erneut auf dem Quellserver ausführen.  
  
###  <a name="create-a-plan-to-migrate-line-of-business-applications"></a><a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a>Erstellen eines Plans für die Migration von Branchen Anwendungen  
 Eine Branchenanwendung ist eine wichtige Computeranwendung, die für den Geschäftsbetrieb unabdingbar ist. Dabei kann es sich z. B. um Buchhaltungs-, Supply Chain Management- oder Ressourcenplanungsanwendungen handeln.  
  
 Wenn Sie die Migration Ihrer Branchenanwendungen planen, beraten Sie sich mit dem Branchenanwendungsanbieter, um die geeignete Methode zum Migrieren der einzelnen Anwendungen zu ermitteln. Außerdem müssen Sie das Medium ermitteln, das zum Installieren der Branchenanwendungen auf dem Zielserver verwendet wird.  
  
> [!NOTE]
>  Wenn Sie das Windows Small Business Server 2011 Essentials SDK verwendet haben, um ein angepasstes Systemintegritäts-oder Warnungs-Add-in zu entwickeln, und Sie das Add-in weiterhin mit Windows Server Essentials verwenden möchten, müssen Sie auch das Add-in aktualisieren und auf dem Ziel Server bereitstellen.  
  
