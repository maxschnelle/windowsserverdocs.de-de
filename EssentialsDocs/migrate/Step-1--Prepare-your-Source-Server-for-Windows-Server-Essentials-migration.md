---
title: "Schritt1: Vorbereiten der Quelle für Windows Server Essentials-Migrations"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 244c8a06-04c6-4863-8b52-974786455373
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 2efb1badde6d0ca11bc3b7526fdfb377d9f95d3f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>Schritt1: Vorbereiten der Quelle für Windows Server Essentials-Migrations

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

In diesem Thema wird erläutert, wie Sichern Sie den Quellserver, bewerten die Systemintegrität des Quellservers, der neuesten Servicepacks und Fixes installieren und Überprüfen der Netzwerkkonfiguration.  
  
## <a name="to-prepare-for-migration"></a>Zur Vorbereitung der Migration  
 Führen Sie die folgenden vorläufige Schritteaus, um sicherzustellen, dass die Einstellungen und Daten auf dem Quellserver erfolgreich zum Zielserver migrieren.  
  
1.  [Sichern des Quellservers](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)  
  
2.  [Installieren Sie die neuesten Servicepacks](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)  
  
3.  [Löschen Sie das Protokoll auf als eine Einstellung für das Konto](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)  
  
4.  [Bewerten Sie die Integrität des Quellservers](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)  
  
5.  [Erstellen eines Plans zum Migrieren von Branchen-Apps](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)  
  
###  <a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>Sichern des Quellservers  
 Sichern Sie den Quellserver vor dem Beginn des Migrationsvorgangs besteht. Erstellen einer Sicherung können Sie Ihre Daten vor Datenverlust zu schützen, tritt ein nicht behebbarer Fehler während der Migration.  
  
##### <a name="to-back-up-the-source-server"></a>So sichern Sie den Quellserver  
  
1.  Verwenden Sie eine der Ressourcen in der folgenden Tabelle, um Sie bei einer vollständigen Sicherung des Quellservers zu unterstützen.  
  
2.  Stellen Sie sicher, dass die Sicherung erfolgreich ausgeführt wurde. Um die Integrität der Sicherung zu testen, wählen Sie zufällige Dateien aus der Sicherung an einem alternativen Speicherort wiederherstellen und stellen Sie sicher, dass die wiederhergestellten Dateien mit den Originaldateien identisch sind.  
  
   |Produkt|Ressource|
   |---|---|
   |Windows Small Business Server2003|[Sichern und Wiederherstellen von Windows Small Business Server2003](https://msdn.microsoft.com/library/cc875809.aspx) 
   |Windows Small Business Server2008|[Sichern und Wiederherstellen von Daten auf Windows Small Business Server2008](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server2008 Foundation|[Sicherung und Wiederherstellung](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)  
   |Windows Small Business Server2011 Essentials|[Weitere Informationen zum Einrichten von Server-Sicherung](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows Small Business Server2011 Standard|[Verwalten von Server-Sicherung](https://technet.microsoft.com/library/cc527488.aspx)  
   |Windows Server Essentials|[Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>Installieren Sie die neuesten Servicepacks  
 Sie müssen die neuesten Updates und Servicepacks auf dem Quellserver vor der Migration installieren.  
  
###  <a name="BKMK_DeleteSvcAcctSetting"></a>Löschen Sie das Protokoll auf als eine Einstellung für das Konto  
 Wenn Sie von Windows Small Business Server2003 oder Windows Server2003 migrieren, löschen Sie die **Anmelden als Dienst** Kontoeinstellung von der Gruppenrichtlinie.  
  
##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>So löschen Sie das Ereignisprotokoll auf als eine Einstellung für das Konto  
  
1.  Zum Öffnen der **Group Policy Management** Tool, klicken Sie auf **starten**, klicken Sie auf **Systemsteuerung**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Group Policy Management**.  
  
2.  Mit der rechten Maustaste **Standarddomänencontroller-Richtlinie**, und klicken Sie dann auf **bearbeiten **.  
  
3.  Navigieren Sie zu **Computer Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**.  
  
4.  Doppelklicken Sie im Detailbereich auf **Anmelden als Dienst**.  
  
5.  Deaktivieren der **diese Richtlinieneinstellungen definieren** Kontrollkästchen.  
  
6.  Löschen Sie \\\localhost\SYSVOL\\ < Domainname\ > \scripts\SBS_LOGIN_SCRIPT.bat.  
  
###  <a name="BKMK_EvaluateHealth"></a>Bewerten Sie die Integrität des Quellservers  
 Es ist wichtig, dass die Integrität des Quellservers auswerten, überprüfen Sie vor der Migration. Verwenden Sie die folgenden Verfahren, um sicherzustellen, dass die Updates aktuell sind, um einen Systemintegritätsbericht zu generieren und die Windows Server Solutions Best Practice Analyzer (BPA) ausführen.  
  
#### <a name="download-and-install-critical-and-security-updates"></a>Herunterladen und Installieren von kritischen und Sicherheit Updates  
 Installieren von kritischen und Sicherheits-Updates auf dem Quellserver wird sichergestellt, dass die Migration erfolgreich wird und schützt das Netzwerk während der Migration.  
  
###### <a name="to-check-for-the-latest-updates"></a>So überprüfen Sie die neuesten Updates  
  
1.  Klicken Sie auf dem Quellserver auf **starten**, klicken Sie auf **alle Programme**, und klicken Sie dann auf **Windows Update**.  
  
2.  Klicken Sie auf **nach Updates suchen**.  
  
3.  Wenn Updates verfügbar sind, klicken Sie auf **Updates installieren**.  
  
#### <a name="run-the-best-practices-analyzer"></a>Ausführen des Best Practices Analyzer  
 Sie können den Best Practices Analyzer (BPA) um sicherzustellen, dass vor Beginn des Migrationsvorgangs keine Probleme auf Ihrem Server, Netzwerk oder Domäne vorliegen ausführen. Das BPA erfasst Konfigurationsinformationen aus den folgenden Quellen:  
  
-   Active Directory Windows-Verwaltungsinstrumentation (WMI)  
  
-   Die Registrierung  
  
-   Internetinformation Services (IIS)  
  
###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>So verwenden Sie den BPA zum Analysieren des Quellservers  
  
1.  Die folgende Tabelle enthält Links zu dem Microsoft Download Center können Sie herunterladen und installieren den Best Practices Analyzer (BPA) für den Quellserver aus.  
  
   |Wenn auf dem Quellserver ausgeführt wird|Sie können die BPA-Tools aus abrufen.|
   |---|---|
   |Windows SBS 2003|[Microsoft Windows Small Business Server2003 Best Practices Analyzer-Website](https://www.microsoft.com/download/details.aspx?id=5334)
   |Windows SBS 2008|[Microsoft Windows Small Business Server2008 Best Practices Analyzer-Website](https://www.microsoft.com/download/details.aspx?id=6231)  
   |Windows SBS 2011 Essentials oder Windows SBS 2011 Standard|[Windows Server Solutions Best Practices Analyzer-Website](https://www.microsoft.com/download/details.aspx?id=15556) 
   |Windows Server Essentials oder Windows Server 2012|Das Server-Dashboard  
  
2.  Nachdem der Download abgeschlossen ist, klicken Sie auf **starten**, zeigen Sie auf **alle Programme**, und klicken Sie dann auf **SBS Best Practices Analyzer Tool**.  
  
    > [!NOTE]
    >  Suchen Sie nach Updates, bevor Sie den Server überprüfen.  
  
3.  Klicken Sie im Navigationsbereich auf **Überprüfung starten**.  
  
     Wenn der Quellserver Windows Server Essentials ausgeführt wird, führen Sie folgende Schritteaus:  
  
    1.  Melden Sie sich auf den Zielserver als Administrator, und öffnen Sie das Dashboard.  
  
    2.  Klicken Sie auf dem Dashboard auf der **Geräte** Registerkarte.  
  
    3.  In den <**Server** >**Aufgaben** Bereich, klicken Sie auf **Best Practices Analyzer**.  
  
4.  Geben Sie im Detailbereich die überprüfungsbezeichnung ein, und klicken Sie dann auf **Überprüfung starten**. Die überprüfungsbezeichnung ist der Name des Überprüfungsberichts, z.B. **SBS BPA Scan 1.Jul 2013**.  
  
5.  Nachdem die Überprüfung abgeschlossen ist, klicken Sie auf **Bericht für diese bewährte Methoden-Überprüfung anzeigen**.  
  
 Nachdem das BPA-Tool Informationen zur Serverkonfiguration gesammelt hat, überprüft er, dass die Informationen korrekt und zeigt den Administratoren dann eine Liste mit Informationen und Problemen nach Schweregrad sortiert. Die Liste beschreibt jedes Problem und bietet eine Empfehlung oder eine mögliche Lösung. Drei Berichtstypen sind verfügbar:  
  
|Berichtstyp|Beschreibung
|-----------------|----------------- 
|Berichte|Zeigt Berichte in einer eindimensionalen Liste an. 
|Struktur-Berichte|Zeigt Berichte in einer hierarchischen Liste an.

Die Beschreibung und Lösungen für ein Problem anzeigen möchten, klicken Sie auf das Problem in den Bericht. Nicht alle Probleme, die vom BPA-Tool gemeldet werden Einfluss auf die Migration sollten, Sie jedoch beheben möglichst viele der Probleme wie möglich, um sicherzustellen, dass die Migration erfolgreich ist.  
  
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
  
###  <a name="BKMK_MigrateLOB"></a>Erstellen eines Plans zum Migrieren von Branchen-Apps  
 Eine Line-of-Business (LOB)-Anwendung eine wichtige Anwendung ist entscheidend für ein Unternehmen ausgeführt. Z.B. buchhaltungs-, Supply Chain-Verwaltung, und Planen der Ressource.  
  
 Wenn Sie Ihre Branchenanwendungen zu migrieren möchten, wenden Sie sich an dem Branchenanwendungsanbieter, um die geeignete Methode zum Migrieren der einzelnen Anwendungen zu ermitteln. Sie müssen auch die Medien suchen, die zum Installieren der Branchenanwendungen auf dem Zielserver verwendet wird.  
  
> [!NOTE]
>  Wenn Sie zum Entwickeln von Windows Small Business Server2011 Essentials SDK verwendet ein angepasstes Systemintegritäts- oder Warnungs-Add-In, und Sie weiterhin das Add-In mit Windows Server Essentials verwenden möchten, müssen Sie auch das Add-In aktualisieren und auf dem Zielserver bereitstellen.  
  
  
### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>Erstellen eines Plans zum Migrieren von E-Mail auf Windows SBS 2011, Windows SBS 2008 und Windows SBS 2003 gehostet  
 In Windows SBS 2011, Windows SBS 2008 und Windows SBS 2003 wird die E-Mail über den Microsoft Exchange-Server bereitgestellt. Windows Server Essentials bietet jedoch keine E-Mail-Posteingangsdienst. Wenn Sie derzeit einen Server mit Windows SBS 2011, Windows SBS 2008 oder Windows SBS 2003 zum Hosten Ihrer E-Mails des Unternehmens s verwenden, Sie müssen zum Migrieren zu einer alternativen lokalen oder gehosteten Lösung.  
  
> [!NOTE]
>  Nachdem Sie aktualisiert und des Quellservers für die Migration vorbereiten, empfehlen wir, dass Sie eine Sicherung des aktualisierten Servers erstellen, bevor Sie den Migrationsprozess fortzusetzen.  
  
#### <a name="migrate-email-to-microsoft-office-365"></a>Migrieren von E-Mails zu Microsoft Office365  
 Wenn Sie sich für Microsoft Office365 als E-Mail-Lösung für Ihre Domäne entschieden haben, führen Sie die Anleitung im [Migrieren aller Postfächer zur Cloud mit einer Exchange-Übernahmemigration](http://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx) um die E-Mail-Migration zu Office365 zu starten. Es wird empfohlen, dass Sie die E-Mail-Migration vor der Installation von Windows Server Essentials ausführen.  
  
> [!NOTE]
>  Der Schrittzum Entfernen des lokalen Exchange-Server auf dem Quellserver ist erforderlich, wenn Sie Windows Server Essentials in Office365 integrieren möchten. Informationen zur Vorgehensweise beim Migrieren der öffentlichen Ordner von Exchange Server zu Office365 finden Sie im Blogbeitrag [Microsoft Exchange 2013 Public Folders Migration Scripts for Office365](http://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx).  
>   
>  Nach Abschluss die Installation Sie aktivieren die Integration von Office365-Feature in Windows Server Essentials durch Ausführen der **in Microsoft Office365 integrieren** Aufgabe.  
  
> [!IMPORTANT]
>  Damit können die Office365-Migrationstools mit Exchange Server herstellen, auf dem Quellserver ausgeführt wird, müssen Sie RPC über HTTP auf dem Quellserver aktivieren. Informationen zur Vorgehensweise beim Aktivieren von RPC über HTTP finden Sie unter [zum Bereitstellen von RPC über HTTP in Small Business Server2003 (Standard oder Premium) erstmalig](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx). Wenn Sie das Office365-Migrationstool nach dem Aktivieren von RPC über HTTP erfolgreich ausführen können, Anzeigen der **ValidPorts** -Einstellung in der Registrierung unter hkey_local_machine\Software\microsoft\rpc\rpcproxy an, und stellen Sie sicher, dass der vollständig qualifizierten Domänennamen (FQDN) für den Quellserver aufgeführt ist. Wenn der FQDN nicht aufgeführt ist, fügen sie mithilfe der im folgenden Beispiel wird manuell hinzu:  
>   
>  Remote. *Contoso*.com:6001-6002; remote. *Contoso*.com: 6004 (ersetzen Sie *Contoso* mit dem Namen Ihrer Domäne).  
  
#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>Migrieren von E-Mails zu einem anderen lokalen Exchange-Server  
 Weitere Informationen zum Migrieren von E-Mail zu einem anderen Exchange-Server lokal, finden Sie unter [Integration eines lokalen Exchange-Servers in Windows Server Essentials](https://technet.microsoft.com/library/jj200172.aspx). Es wird empfohlen, dass Sie den neuen lokalen Exchange-Server einrichten, nach der Installation von Windows Server Essentials, und schließen Sie dann die E-Mail-Migration, bevor Sie den Quellserver herabstufen.  
  
> [!NOTE]
>  Windows Small Business Server POP3-Connector ist nicht mit Exchange-Server enthalten. Nach der Migration von E-Mail-Daten zu einem anderen Exchange-Server können Sie den POP3-Connector-Feature nicht mehr verwenden.  
  
> [!NOTE]
>  Nachdem Sie aktualisiert und des Quellservers für die Migration vorbereiten, sollten Sie eine Sicherung des aktualisierten Servers erstellen, bevor Sie den Migrationsprozess fortzusetzen.  
  
## <a name="next-steps"></a>Nächste Schritte  
 Sie haben den Quellserver für die Migration zu Windows Server Essentials vorbereitet.  Lesen Sie jetzt [Schritt2: Installieren von Windows Server Essentials als einen neuen Replikatdomänencontroller](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md).  

Alle Schrittefinden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

