---
title: "Vorbereiten des Quellservers für Windows Server Essentials migration1"
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.openlocfilehash: 929c7506c78667646e429c4f28df7e5642c575ab
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="prepare-your-source-server-for-windows-server-essentials-migration1"></a>Vorbereiten des Quellservers für Windows Server Essentials migration1

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Führen Sie die folgenden vorläufige Schritteaus, um sicherzustellen, dass die Einstellungen und Daten auf dem Quellserver erfolgreich zum Zielserver migrieren.  
  
#### <a name="to-prepare-for-migration"></a>Zur Vorbereitung der Migration  
  

1.  [Sichern des Quellservers](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren Sie die neuesten Servicepacks](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Bewerten Sie die Integrität des Quellservers](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [Führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Erstellen eines Plans zum Migrieren von Branchen-Apps](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

1.  [Sichern des Quellservers](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren Sie die neuesten Servicepacks](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Bewerten Sie die Integrität des Quellservers](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_UseWindowsBestPracticeAnalyzer)  
  
4.  [Führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MPT)  
  
5.  [Erstellen eines Plans zum Migrieren von Branchen-Apps](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_PlanToMigrateLineOfBusinessApplications)  

  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>Sichern des Quellservers  
 Sichern Sie den Quellserver vor dem Beginn des Migrationsvorgangs besteht. Erstellen einer Sicherung können Sie Ihre Daten vor Datenverlust zu schützen, tritt ein nicht behebbarer Fehler während der Migration.  
  
##### <a name="to-back-up-the-source-server"></a>So sichern Sie den Quellserver  
  
1.  Führen Sie eine vollständige Sicherung des Quellservers. Weitere Informationen zum Sichern von Windows Small Business Server2011 Essentials finden Sie unter [erfahren Sie mehr über das Einrichten der serversicherung](https://technet.microsoft.com/library/server-backup-support-1.aspx).  
  
2.  Stellen Sie sicher, dass die Sicherung erfolgreich ausgeführt wurde. Um die Integrität der Sicherung zu testen, wählen Sie zufällige Dateien aus der Sicherung an einem alternativen Speicherort wiederherstellen und stellen Sie sicher, dass die wiederhergestellten Dateien mit den Originaldateien identisch sind.  
  
###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>Installieren Sie die neuesten Servicepacks  
 Sie müssen die neuesten Updates und Servicepacks auf dem Quellserver vor der Migration installieren.  
  
###  <a name="BKMK_UseWindowsBestPracticeAnalyzer"></a>Bewerten Sie die Integrität des Quellservers  
 Es ist wichtig, dass die Integrität des Quellservers auswerten, überprüfen Sie vor der Migration. Verwenden Sie die folgenden Verfahren, um sicherzustellen, dass die Updates aktuell sind, um einen Systemintegritätsbericht zu generieren und die Windows Server Solutions Best Practice Analyzer (BPA) ausführen.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>Herunterladen und Installieren von kritischen und Sicherheit Updates  
 Installieren von kritischen und Sicherheits-Updates auf dem Quellserver wird sichergestellt, dass die Migration erfolgreich wird und schützt das Netzwerk während der Migration.  
  
###### <a name="to-check-for-the-latest-updates"></a>So überprüfen Sie die neuesten Updates  
  
1.  Klicken Sie auf dem Quellserver auf **starten**, klicken Sie auf **alle Programme**, und klicken Sie dann auf **Windows Update**.  
  
2.  Klicken Sie auf **nach Updates suchen**.  
  
3.  Wenn Updates verfügbar sind, klicken Sie auf **Updates installieren**.  
  
#### <a name="check-the-alert-viewer-for-critical-errors"></a>Überprüfen Sie die Meldungsanzeige auf schwerwiegende Fehler  
 Sie können die Meldungsanzeige auf dem Dashboard schwerwiegende Fehler überprüfen.  
  
#### <a name="run-the-windows-server-solutions-best-practices-analyzer"></a>Führen Sie die Windows Server Solutions Best Practices Analyzer  
 Sie können die Windows Server Solutions Best Practices Analyzer (BPA) um sicherzustellen, dass vor Beginn des Migrationsvorgangs keine Probleme auf Ihrem Server, Netzwerk oder Domäne vorliegen ausführen. Das BPA erfasst Konfigurationsinformationen aus den folgenden Quellen:  
  
-   Aktive Directory® Windows-Verwaltungsinstrumentation (WMI)  
  
-   Die Registrierung  
  
-   Die Metabase von Internetinformationsdienste (Internet Information Services, IIS)  
  
###### <a name="to-use-the-windows-server-solutions-bpa-to-analyze-your-source-server"></a>Verwenden Sie Windows Server Solutions BPA zum Analysieren des Quellservers  
  
1.  Herunterladen und Installieren der [Windows Server Solutions Best Practices Analyzer](https://www.microsoft.com/en-us/download/details.aspx?id=15556) im Microsoft Download Center.  
  
2.  Nachdem der Download abgeschlossen ist, klicken Sie auf **starten**, zeigen Sie auf **alle Programme**, und klicken Sie dann auf **SBS Best Practices Analyzer Tool**.  
  
    > [!NOTE]
    >  Suchen Sie nach Updates, bevor Sie den Server überprüfen.  
  
3.  Klicken Sie im Navigationsbereich auf **Überprüfung starten**.  
  
4.  Geben Sie im Detailbereich die überprüfungsbezeichnung ein, und klicken Sie dann auf **Überprüfung starten**. Die überprüfungsbezeichnung ist der Name des Überprüfungsberichts, z.B. **SBS BPA Scan 1.Jul 2012**.  
  
5.  Nachdem die Überprüfung abgeschlossen ist, klicken Sie auf **Bericht für diese bewährte Methoden-Überprüfung anzeigen**.  
  
 Nach dem Sammeln von Informationen zur Konfiguration, die Windows Server Solutions BPA überprüft, ob die Informationen korrekt ist und zeigt den Administratoren dann eine Liste mit Informationen und Problemen nach Schweregrad sortiert. Die Liste beschreibt jedes Problem und bietet eine Empfehlung oder eine mögliche Lösung. Drei Berichtstypen sind verfügbar:  
  
|Berichtstyp|Beschreibung|  
|-----------------|-----------------|  
|Berichte|Zeigt Berichte in einer eindimensionalen Liste an.|  
|Struktur-Berichte|Zeigt Berichte in einer hierarchischen Liste an.|  
|Andere Berichte|Zeigt Berichte wie z.B. ein Laufzeitprotokoll an.|  
  
 Die Beschreibung und Lösungen für ein Problem anzeigen möchten, klicken Sie auf das Problem in den Bericht. Nicht alle Probleme, die die Windows SBS 2011 Essentials-BPA gemeldeten Einfluss auf die Migration, aber Sie sollten möglichst viele der Probleme beheben, wie möglich, um sicherzustellen, dass die Migration erfolgreich ist.  
  
####  <a name="BKMK_SynchronizeTheSourceServerTimeWithAnExternalTimeSource"></a>Synchronisieren der quellserveruhrzeit mit einer externen Zeitquelle  
 Die Zeit auf dem Quellserver muss innerhalb von fünf Minuten von der Uhrzeit auf dem Zielserver festgelegt werden, und das Datum und die Zeitzone müssen auf beiden Servern gleich sein. Wenn der Quellserver in einem virtuellen Computer ausgeführt wird, müssen das Datum, Uhrzeit und Zeitzone auf dem Hostserver, die von den Quellserver und Zielserver entsprechen. Um sicherzustellen, dass Windows Server Essentials erfolgreich installiert wurde, müssen Sie die Uhrzeit des Quellservers mit dem Server Netzwerkzeitprotokoll (NTP) auf das Internet synchronisieren.  
  
###### <a name="to-synchronize-the-source-server-time-with-the-ntp-server"></a>Um die Uhrzeit des Quellservers mit dem NTP-Server synchronisieren  
  
1.  Melden Sie sich auf dem Quellserver mit einem Domänenadministratorkonto und -Kennwort an.  
  
2.  Klicken Sie auf **starten**, klicken Sie auf **ausführen**, Typ **Cmd** in das Textfeld, und drücken Sie dann die EINGABETASTE.  
  
3.  Geben Sie an der Eingabeaufforderung w32tm /config /syncfromflags: Domhier//reliable: keine /update, und drücken Sie dann die EINGABETASTE.  
  
4.  Klicken Sie an der Eingabeaufforderung Geben Sie net Stop w32time, und drücken Sie dann die EINGABETASTE.  
  
5.  Klicken Sie an der Eingabeaufforderung Geben Sie net Start w32time, und drücken Sie dann die EINGABETASTE.  
  
> [!IMPORTANT]
>  Während der Installation von Windows Server Essentials haben Sie die Möglichkeit, die Uhrzeit auf dem Zielserver zu überprüfen und ändern, bei Bedarf. Stellen Sie sicher, dass die Uhrzeit höchstens fünf Minuten von der Zeit, die auf dem Quellserver festgelegt ist. Wenn die Installation abgeschlossen ist, wird der Zielserver mit dem NTP synchronisiert. Alle Domänencomputern, einschließlich des Quellservers, synchronisieren, auf den Zielserver, bei dem die Rolle der primären Domäne Domänencontroller (PDC)-Emulatormaster angenommen wird.  
  
###  <a name="BKMK_MPT"></a>Führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver  
 Sie können keine Installation im Migrationsmodus durchführen, ohne zuerst das Tool zum Vorbereiten der Migration auf dem Quellserver auszuführen. Dieses Tool bereitet den Quellserver und die Domäne für Windows Server Essentials die Migration vorbereiten.  
  
> [!IMPORTANT]
>  Sichern Sie den Quellserver, bevor Sie das Tool zum Vorbereiten der Migration ausführen. Alle Änderungen, die Tool zum Vorbereiten der Migration am Schema vornimmt, können rückgängig gemacht werden. Wenn Sie während der Migration Probleme auftreten, ist die einzige Möglichkeit zum Zurückgeben der Quellserver in den Zustand vor dem Ausführen des Tools zum Wiederherstellen des Servers aus einer Sicherung.  
  
 Führen Sie das Tool zum Vorbereiten der Migration müssen Sie Mitglied der Gruppe Organisations-Admins, der Gruppe Schema-Admins und Domänen-Admins sein.  
  
##### <a name="to-verify-that-you-have-the-appropriate-permissions-to-run-the-tool-on-the-source-server"></a>Um sicherzustellen, dass Sie die entsprechenden Berechtigungen zum Ausführen des Tools auf dem Quellserver verfügen  
  
1.  Klicken Sie auf dem Quellserver auf **starten**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**.  
  
2.  In der Konsolenstruktur zum Erweitern der Domäne klicken, und klicken Sie dann auf **Benutzer**.  
  
3.  Mit der rechten Maustaste des Administratorkonto an, die Sie für die Migration verwenden, und klicken Sie dann auf **Eigenschaften**.  
  
4.  Klicken Sie auf die **Mitglied von** Registerkarte, und stellen Sie sicher, dass Organisations-Admins, Schema-Admins und Domänen-Admins, in aufgeführt sind der **Mitglied** Textfeld.  
  
5.  Wenn diese Gruppen nicht aufgelistet sind, klicken Sie auf **hinzufügen**, und fügen dann jede Gruppe, die nicht aufgeführt ist.  
  
    > [!NOTE]
    >  -   Sie können ein Berechtigungsfehler angezeigt, wenn der Netlogon-Dienst nicht gestartet wurde.  
    > -   Sie müssen abmelden und wieder anmelden, den Server für die Änderungen wirksam werden.  
  
     Sie können die neueste Version von Windows Update-Agent verwenden, um sicherzustellen, dass das Serverupdate ordnungsgemäß funktioniert.  
  
 Sie können die neueste Version von Windows Update-Agent verwenden, um sicherzustellen, dass das Serverupdate ordnungsgemäß funktioniert.  
  
 Bevor Sie Windows Update-Agent auf dem Quellserver installieren können, müssen Sie zuerst Windows PowerShell 2.0 und Microsoft Baseline Configuration Analyzer 2.0 installieren.  
  
-   Informationen zum Herunterladen und Installieren von Windows PowerShell 2.0, finden Sie unter [Artikel 968929](https://go.microsoft.com/fwlink/p/?LinkId=241483) in der Microsoft Knowledge Base.  
  
-   Informationen zum Herunterladen und Installieren von Microsoft Baseline Configuration Analyzer 2.0, finden Sie unter der [Microsoft Baseline Configuration Analyzer 2.0](https://go.microsoft.com/fwlink/p/?LinkId=241484) im Microsoft Download Center.  
  
-   Informationen zum Herunterladen und Installieren der neuesten Version von Windows Update-Agent, finden Sie unter [Artikel 949104](https://go.microsoft.com/fwlink/p/?LinkId=237493) in der Microsoft Knowledge Base.  
  
##### <a name="to-install-and-run-the-migration-preparation-tool-on-the-source-server"></a>Installieren und führen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver  
  
1.  Legen Sie Windows Server Essentials-DVD1 in das DVD-Laufwerk auf dem Quellserver.  
  
2.  Öffnen Sie Windows Explorer, navigieren Sie zu den **\support\tools** Ordner der DVD ein, und doppelklicken Sie dann auf die **sourcetool.msi** Datei.  
  
    > [!NOTE]
    >  -   Wenn das Tool zum Vorbereiten der Migration bereits auf dem Server installiert ist, führen Sie das Tool aus dem **starten** Menü.  
    > -   Um sicherzustellen, dass Sie mögliche Migration am besten vorbereitet sind, empfiehlt es sich, dass Sie immer das neueste Update installieren möchten.  
  
     Der Assistent installiert das Tool zum Vorbereiten der Migration auf dem Quellserver. Wenn die Installation abgeschlossen ist, wird das Tool zum Vorbereiten der Migration wird automatisch ausgeführt und die neuesten Updates installiert.  
  
3.  Wählen Sie in der Tool zum Vorbereiten der Migration **ich über eine datensicherung und bin bereit, um den Vorgang fortzusetzen**, und klicken Sie dann auf **Weiter**.  
  
    > [!WARNING]
    >  Wenn Sie eine Fehlermeldung bezüglich einer Hotfixinstallation angezeigt wird, finden Sie unter Methode 2: Umbenennen des Ordners "Catroot2" im [Artikel 822798](https://go.microsoft.com/FWLink/p/?LinkID=118672) in der Microsoft Knowledge Base.  
  
     Das Tool zum Vorbereiten der Migration wird die Quelldomäne für die Migration vorbereitet, durch die Erweiterung des Active Directory-Schemas. Nachdem der Vorgang abgeschlossen ist, klicken Sie auf **Weiter** um den Vorgang fortzusetzen.  
  
4.  Nach dem Vorbereiten der Quelldomäne, sucht das Tool zum Vorbereiten der Migration den Quellserver um zwei Typen potenzieller Probleme zu identifizieren.  
  
    -   **Fehler** Probleme gefunden werden, auf dem Quellserver, die die Migration blockiert oder dazu führen, dass die Migration fehlschlagen können. Folgen Sie den Anweisungen in der Fehlermeldung, die Probleme zu beheben, und klicken Sie auf **erneut überprüfen**.  
  
    -   **Warnungen** Probleme gefunden werden, auf dem Quellserver, die funktionalen Problemen während der Migration führen können. Es wird dringend empfohlen, dass Sie die Anweisungen in der Fehlermeldung zum Beheben der Probleme, bevor Sie mit der Migration ausführen.  
  
     Nachdem Sie behoben oder bestätigt, alle Probleme haben, klicken Sie auf **Weiter**.  
  
5.  Klicken Sie in der Tool zum Vorbereiten der Migration auf **Fertig stellen**.  
  
6.  Wenn das Tool zum Vorbereiten der Migration abgeschlossen ist, können Sie aufgefordert, den Quellserver neu starten, bevor Sie mit der Migration zu Windows Server Essentials beginnen können.  
  
> [!NOTE]
>  Sie müssen eine erfolgreiche Ausführung des Tool zum Vorbereiten der Migration auf dem Quellserver innerhalb von zwei Wochen nach der Installation von Windows Server Essentials auf dem Zielserver ausführen. Andernfalls wird die Installation von Windows Server Essentials auf dem Zielserver blockiert. In diesem Fall müssen Sie das Tool zum Vorbereiten der Migration auf dem Quellserver erneut ausführen.  
  
###  <a name="BKMK_PlanToMigrateLineOfBusinessApplications"></a>Erstellen eines Plans zum Migrieren von Branchen-Apps  
 Eine Line-of-Business (LOB)-Anwendung eine wichtige Anwendung ist entscheidend für ein Unternehmen ausgeführt. Z.B. buchhaltungs-, Supply Chain-Verwaltung, und Planen der Ressource.  
  
 Wenn Sie Ihre Branchenanwendungen zu migrieren möchten, wenden Sie sich an dem Branchenanwendungsanbieter, um die geeignete Methode zum Migrieren der einzelnen Anwendungen zu ermitteln. Sie müssen auch die Medien suchen, die zum Installieren der Branchenanwendungen auf dem Zielserver verwendet wird.  
  
> [!NOTE]
>  Wenn Sie zum Entwickeln von Windows Small Business Server2011 Essentials SDK verwendet ein angepasstes Systemintegritäts- oder Warnungs-Add-In, und Sie weiterhin das Add-In mit Windows Server Essentials verwenden möchten, müssen Sie auch das Add-In aktualisieren und auf dem Zielserver bereitstellen.  
  
