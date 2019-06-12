---
title: Vorbereiten des Quellservers für Windows Server Essentials migration1
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f5861ae9-77cb-4d37-b4c5-8f0757213385
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 93f5bdb615adf56b81a1c4c93f802f6da4e48c1b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66432611"
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Vorbereiten des Quellservers für Windows Server Essentials migration1

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Führen Sie vorab folgende Schritte aus, um sicherzustellen, dass eine erfolgreiche Migration der Einstellungen und Daten vom Quellserver zum Zielserver möglich ist.  
  
#### <a name="to-prepare-for-migration"></a>So bereiten Sie die Migration vor  
  

1.  [Sichern des Quellservers](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren Sie die neuesten Servicepacks](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Bewerten Sie die Integrität des Quellservers](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [Führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Erstellen Sie einen Plan zum Migrieren von Line-of-Business-Anwendungen](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [Sichern des Quellservers](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren Sie die neuesten Servicepacks](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Bewerten Sie die Integrität des Quellservers](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [Führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Erstellen Sie einen Plan zum Migrieren von Line-of-Business-Anwendungen](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a> Sichern des Quellservers  
 Sichern Sie den Quellserver, bevor Sie mit dem Migrationsprozess beginnen. Durch diese Sicherung schützen Sie sich vor Datenverlusten, wenn während der Migration ein nicht behebbarer Fehler auftritt.  
  
##### <a name="to-back-up-the-source-server"></a>So sichern Sie den Zielserver  
  
1.  Führen Sie eine vollständige Sicherung des Quellservers durch. Weitere Informationen zum Sichern von Windows Small Business Server 2011 Essentials finden Sie unter [erfahren Sie mehr über das Einrichten der serversicherung](https://technet.microsoft.com/library/server-backup-support-1.aspx).  
  
2.  Überprüfen Sie, ob die Sicherung erfolgreich ausgeführt wurde. Zum Prüfen der Integrität der Sicherung wählen Sie beliebige Dateien der Sicherung aus und stellen diese an einem anderen Speicherort wieder her. Überprüfen Sie dann, ob die wiederhergestellten Dateien mit den Originaldateien identisch sind.  
  
###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a> Installieren Sie die neuesten Servicepacks  
 Sie müssen vor der Migration die neuesten Updates und Service Packs auf dem Quellserver installieren.  
  
###  <a name="BKMK_UseWindowsBestPracticeAnalyzer"></a> Bewerten Sie die Integrität des Quellservers  
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
  
-   Active Directory® Windows Management Instrumentation (Windows-Verwaltungsinstrumentation, WMI)  
  
-   Registrierung  
  
-   IIS-Metabase (Internet Information Services, Internetinformationsdienste)  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>So analysieren Sie den Quellserver mithilfe des BPA für Windows Server Solutions  
  
1. Herunterladen und Installieren der [Windows Server Solutions Best Practices Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=15556) im Microsoft Download Center.  
  
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
  
 Wenn Sie die Beschreibung und Lösungen für ein Problem anzeigen möchten, klicken Sie im Bericht auf das betreffende Problem. Nicht alle, die den BPA für Windows SBS 2011 Essentials erfassten Probleme wirken, aber Sie sollten möglichst viele der Probleme beheben, wie möglich, um sicherzustellen, dass die Migration erfolgreich ist.  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a> Synchronisieren der quellserveruhrzeit mit einer externen Zeitquelle  
 Die Uhrzeit auf dem Quellserver darf maximal fünf Minuten von der Uhrzeit auf dem Zielserver abweichen, und die Datums- und Zeitzone muss auf beiden Servern gleich sein. Wenn der Quellserver einen virtuellen Computer ausführt, müssen das Datum, die Uhrzeit und die Zeitzone auf dem Hostserver diesen Angaben auf dem Quell- und dem Zielserver entsprechen. Um sicherzustellen, dass Windows Server Essentials erfolgreich installiert wurde, müssen Sie die Uhrzeit des Quellservers mit dem Network Time Protocol (NTP)-Server im Internet synchronisieren.  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>So synchronisieren Sie die Uhrzeit des Quellservers mit dem NTP-Server  
  
1.  Melden Sie sich mit einem Domänenadministratorkonto und -kennwort am Quellserver an.  
  
2.  Klicken Sie auf **Start**, dann auf **Ausführen**, geben Sie im Textfeld **cmd** ein, und drücken Sie dann die EINGABETASTE.  
  
3.  Geben Sie an der Eingabeaufforderung den Befehl w32tm/config / DOMHIER / reliable: keine/Update, und drücken Sie dann die EINGABETASTE.  
  
4.  Geben Sie an der Eingabeaufforderung net Stop w32time, und drücken Sie dann die EINGABETASTE.  
  
5.  Geben Sie an der Eingabeaufforderung net Start w32time, und drücken Sie dann die EINGABETASTE.  
  
> [!IMPORTANT]
>  Während der Installation von Windows Server Essentials müssen Sie die Gelegenheit, überprüfen die Zeit auf dem Zielserver, und ändern Sie ihn bei Bedarf. Stellen Sie sicher, dass die Uhrzeit höchstens fünf Minuten von der Uhrzeit auf dem Quellserver abweicht. Nachdem die Installation abgeschlossen ist, wird der Zielserver mit dem NTP-Server synchronisiert. Alle Computer, die Mitglied der Domäne sind (einschließlich des Quellservers) werden mit dem Zielserver synchronisiert, der die Rolle des Betriebsmasters für den PDC-Emulator (Primary Domain Controller, primärer Domänencontroller) ausübt.  
  
###  <a name="BKMK_MPT"></a> Führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver  
 Sie können keine Installation im Migrationsmodus durchführen, ohne zuerst auf dem Quellserver das Tool zum Vorbereiten der Migration auszuführen. Dieses Tool dient zum Vorbereiten von den Quellserver und die Domäne zu Windows Server Essentials migriert werden.  
  
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
  
   Bevor Sie Windows Update-Agent auf dem Quellserver installieren können, müssen Sie zuerst Windows PowerShell 2.0 und Microsoft Baseline Configuration Analyzer 2.0 installieren.  
  
-   Zum Herunterladen und installieren Sie Windows PowerShell 2.0, finden Sie unter [Artikel 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483) in der Microsoft Knowledge Base.  
  
-   Zum Herunterladen und installieren Microsoft Baseline Configuration Analyzer 2.0, finden Sie unter den [Microsoft Baseline Configuration Analyzer 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484) im Microsoft Download Center.  
  
-   Zum Herunterladen und installieren die neueste Version von Windows Update-Agent, finden Sie unter [Artikel 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493) in der Microsoft Knowledge Base.  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>So installieren Sie das Tool zum Vorbereiten der Migration auf dem Quellserver und führen es aus  
  
1. Fügen Sie Windows Server Essentials-DVD1 in das DVD-Laufwerk auf dem Quellserver an.  
  
2. Öffnen Sie den Windows-Explorer, navigieren Sie auf der DVD zum Ordner **\support\tools**, und doppelklicken Sie auf die Datei **sourcetool.msi**.  
  
   > [!NOTE]
   > - Wenn das Tool zum Vorbereiten der Migration bereits auf dem Server installiert ist, führen Sie es über das **Start**-Menü aus.  
   >   -   Für eine reibungslose Migration wird empfohlen, immer das aktuellste Update zu installieren.  
  
    Der Assistent installiert das Tool zum Vorbereiten der Migration auf dem Quellserver. Nachdem die Installation abgeschlossen ist, wird das Tool zum Vorbereiten der Migration automatisch ausgeführt, und es installiert die neuesten Updates.  
  
3. Wählen Sie im Tool zum Vorbereiten der Migration die Option **Ich verfüge über eine Datensicherung und bin bereit, den Vorgang fortzusetzen** aus, und klicken Sie dann auf **Weiter**.  
  
   > [!WARNING]
   >  Wenn Sie eine Fehlermeldung bezüglich einer Hotfixinstallation angezeigt wird, finden Sie unter Methode 2: Umbenennen des Ordners "Catroot2" im [Artikel 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672) in der Microsoft Knowledge Base.  
  
    Die Quelldomäne wird durch Erweitern des Active Directory-Schemas für die Migration vorbereitet. Klicken Sie nach Abschluss des Vorgangs auf **Weiter**, um fortzufahren.  
  
4. Nach dem Vorbereiten der Quelldomäne überprüft das Tool zum Vorbereiten der Migration den Quellserver auf zwei Typen potenzieller Probleme.  
  
   - **Fehler** Probleme gefunden werden, auf dem Quellserver, die die Migration blockiert oder dazu führen, dass die Migration zu können. Befolgen Sie die Anweisungen in der Fehlermeldung, um die Probleme zu beheben, und klicken Sie dann auf **Erneut überprüfen**.  
  
   - **Warnungen** Probleme gefunden werden, auf dem Quellserver, die zu Funktionsproblemen während der Migration führen können. Es wird dringend empfohlen, die Probleme vor dem Fortsetzen der Migration anhand der Anweisungen in der Fehlermeldung zu beheben.  
  
     Nachdem Sie alle Fehler behoben oder bestätigt haben, klicken Sie auf **Weiter**.  
  
5. Klicken Sie im Tool zum Vorbereiten der Migration auf **Fertig stellen**.  
  
6. Wenn das Tool zum Vorbereiten der Migration abgeschlossen ist, werden Sie möglicherweise aufgefordert, den Quellserver neu zu starten, bevor Sie die Migration zu Windows Server Essentials beginnen können.  
  
> [!NOTE]
>  Sie müssen bei einer erfolgreiche Ausführung von Tool zum Vorbereiten der Migration auf dem Quellserver innerhalb von zwei Wochen nach der Installation von Windows Server Essentials auf dem Zielserver ausführen. Andernfalls wird die Installation von Windows Server Essentials auf dem Zielserver blockiert. In diesem Fall müssen Sie das Tool zum Vorbereiten der Migration erneut auf dem Quellserver ausführen.  
  
###  <a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a> Erstellen Sie einen Plan zum Migrieren von Line-of-Business-Anwendungen  
 Eine Branchenanwendung ist eine wichtige Computeranwendung, die für den Geschäftsbetrieb unabdingbar ist. Dabei kann es sich z. B. um Buchhaltungs-, Supply Chain Management- oder Ressourcenplanungsanwendungen handeln.  
  
 Wenn Sie die Migration Ihrer Branchenanwendungen planen, beraten Sie sich mit dem Branchenanwendungsanbieter, um die geeignete Methode zum Migrieren der einzelnen Anwendungen zu ermitteln. Außerdem müssen Sie das Medium ermitteln, das zum Installieren der Branchenanwendungen auf dem Zielserver verwendet wird.  
  
> [!NOTE]
>  Wenn Sie zum Entwickeln von Windows Small Business Server 2011 Essentials SDK verwendet ein angepasstes Systemintegritäts- oder Warnungs-Add-In, und Sie weiterhin das Add-in in Windows Server Essentials verwenden möchten, müssen Sie auch das Add-in aktualisieren und auf dem Zielserver bereitstellen.  
  
