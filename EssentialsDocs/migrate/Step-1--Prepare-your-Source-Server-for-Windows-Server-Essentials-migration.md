---
title: 'Schritt 1: Vorbereiten des Quellservers für die Migration zu Windows Server Essentials'
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 244c8a06-04c6-4863-8b52-974786455373
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f5696c473a8fcb04a60b9a4b6c51ac206a6ef0de
ms.sourcegitcommit: 2f072c0c02e3e0deae331ca64b375d63b89d0522
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2020
ms.locfileid: "83404585"
---
# <a name="step-1-prepare-your-source-server-for-windows-server-essentials-migration"></a>Schritt 1: Vorbereiten des Quellservers für die Migration zu Windows Server Essentials

> Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials

In diesem Thema wird erläutert, wie Sie den Quellserver sichern, die Systemintegrität des Quellservers prüfen, die aktuellen Service Packs und Fixes installieren und die Netzwerkkonfiguration überprüfen.

## <a name="to-prepare-for-migration"></a>So bereiten Sie die Migration vor
 Führen Sie vorab folgende Schritte aus, um sicherzustellen, dass eine erfolgreiche Migration der Einstellungen und Daten vom Quellserver zum Zielserver möglich ist.

1.  [Sichern des Quell Servers](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_BackUpYourSourceServerToPrepareForMigration)

2.  [Installieren der aktuellsten Service Packs](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_InstallTheMostRecentServicePacksToPrepareForMigration)

3.  [Einstellung "Anmelden als Dienst Konto" Löschen](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_DeleteSvcAcctSetting)

4.  [Bewerten Sie die Integrität des Quellservers](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_EvaluateHealth)

5.  [Aufstellen eines Plans für die Migration von Branchenanwendungen](Step-1--Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md#BKMK_MigrateLOB)

###  <a name="back-up-your-source-server"></a><a name="BKMK_BackUpYourSourceServerToPrepareForMigration"></a>Sichern des Quell Servers
 Sichern Sie den Quellserver, bevor Sie mit dem Migrationsprozess beginnen. Durch diese Sicherung schützen Sie sich vor Datenverlusten, wenn während der Migration ein nicht behebbarer Fehler auftritt.

##### <a name="to-back-up-the-source-server"></a>So sichern Sie den Zielserver

1. Verwenden Sie eine der Ressourcen in der folgenden Tabelle, um eine vollständige Sicherung des Quellservers auszuführen.

2. Überprüfen Sie, ob die Sicherung erfolgreich ausgeführt wurde. Zum Prüfen der Integrität der Sicherung wählen Sie beliebige Dateien der Sicherung aus und stellen diese an einem anderen Speicherort wieder her. Überprüfen Sie dann, ob die wiederhergestellten Dateien mit den Originaldateien identisch sind.

   |Produkt|Resource|
   |---|---|
   |Windows Small Business Server 2003|[Sichern und Wiederherstellen von Windows Small Business Server 2003](https://msdn.microsoft.com/library/cc875809.aspx)
   |Windows Small Business Server 2008|[Sichern und Wiederherstellen von Daten in Windows Small Business Server 2008](https://technet.microsoft.com/library/cc527505\(WS.10\).aspx)
   |Windows Server 2008 Foundation|[Sicherung und Wiederherstellung](https://technet.microsoft.com/library/cc754097\(WS.10\).aspx)
   |Windows Small Business Server 2011 Essentials|[Weitere Informationen zum Einrichten der Serversicherung](https://technet.microsoft.com/library/server-backup-support-1.aspx)
   |Windows Small Business Server 2011 Standard|[Verwalten der Serversicherung](https://technet.microsoft.com/library/cc527488.aspx)
   |Windows Server Essentials|[Verwalten der Sicherung und Wiederherstellung in Windows Server Essentials](https://technet.microsoft.com/library/jj713536.aspx)

###  <a name="install-the-most-recent-service-packs"></a><a name="BKMK_InstallTheMostRecentServicePacksToPrepareForMigration"></a>Installieren der aktuellsten Service Packs
 Sie müssen vor der Migration die neuesten Updates und Service Packs auf dem Quellserver installieren.

###  <a name="delete-the-log-on-as-a-service-account-setting"></a><a name="BKMK_DeleteSvcAcctSetting"></a>Einstellung "Anmelden als Dienst Konto" Löschen
 Wenn Sie von Windows Small Business Server 2003 oder Windows Server 2003 migrieren, löschen Sie die Kontoeinstellung **Anmelden als Dienst** aus der Gruppenrichtlinie.

##### <a name="to-delete-the-log-on-as-a-service-account-setting"></a>So löschen Sie die Einstellung "Anmelden als Dienst Konto"

1.  Klicken Sie zum Öffnen des Tools **Gruppenrichtlinienverwaltung** auf **Start**, klicken Sie auf **Systemsteuerung**, klicken Sie auf **Verwaltung**, und klicken Sie dann auf **Gruppenrichtlinienverwaltung**.

2.  Klicken Sie mit der rechten Maustaste auf **Standard-Domänencontrollerrichtlinie**, und klicken Sie dann auf **Bearbeiten**.

3.  Navigieren Sie zu **Computerkonfigurationen\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**.

4.  Doppelklicken Sie im Detailbereich auf **Anmelden als Dienst**.

5.  Deaktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

6.  Löschen Sie \\ \localhost\sysvol \\<Domain Name \> \scripz\ SBS_LOGIN_SCRIPT. bat.

###  <a name="evaluate-the-health-of-the-source-server"></a><a name="BKMK_EvaluateHealth"></a>Auswerten der Integrität des Quell Servers
 Es ist wichtig, dass Sie die Integrität des Quellservers auswerten, bevor Sie mit der Migration beginnen. Verwenden Sie die folgenden Verfahren, um sicherzustellen, dass die Updates aktuell sind, um einen Systemintegritätsbericht zu generieren und das Windows Server Solutions Best Practice Analyzer (BPA) auszuführen.

#### <a name="download-and-install-critical-and-security-updates"></a>Laden Sie kritische und Sicherheits-Updates herunter und installieren sie sie.
 Durch das Installieren von kritischen und Sicherheits-Updates auf dem Quellserver wird sichergestellt, dass Ihre Migration erfolgreich wird und hilft dabei, Ihr Netzwerk während der Migration zu schützen.

###### <a name="to-check-for-the-latest-updates"></a>So überprüfen Sie die neuesten Updates

1.  Klicken Sie auf dem Quellserver auf **Start**, klicken Sie auf **Programme** und klicken Sie dann auf **Windows Update**.

2.  Klicken Sie auf **Nach Updates suchen**.

3.  Wenn entsprechende Updates ermittelt werden, klicken Sie auf **Updates installieren**.

#### <a name="run-the-best-practices-analyzer"></a>Ausführen des Best Practices Analyzer
 Sie können den Best Practices Analyzer (BPA) ausführen, um sicherzustellen, dass vor Beginn des Migrationsvorgangs keine Probleme auf dem Server, im Netzwerk, oder in der Domäne vorliegen. Das BPA erfasst Konfigurationsinformationen aus den folgenden Quellen:

-   Active Directory Windows Management Instrumentation (WMI)

-   Registrierung

-   IIS (Internet Information Services)

###### <a name="to-use-the-bpa-to-analyze-your-source-server"></a>So verwenden Sie den BPA zum Analysieren des Quellservers

1. Die folgende Tabelle enthält Links zum Microsoft Download Center, wo Sie den Best Practices Analyzer (BPA) für den Quellserver herunterladen und installieren können.


   |             Wenn auf dem Quell Server ausgeführt wird             |                                                     Sie können die BPA-Tools von                                                      |
   |----------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------|
   |                     Windows SBS 2003                     | [Best Practices Analyzer-Website für Microsoft Windows Small Business Server 2003](https://www.microsoft.com/download/details.aspx?id=5334) |
   |                     Windows SBS 2008                     | [Best Practices Analyzer-Website für Microsoft Windows Small Business Server 2008](https://www.microsoft.com/download/details.aspx?id=6231) |
   | Windows SBS 2011 Essentials oder Windows SBS 2011 Standard |          [Best Practices Analyzer-Website für Windows Server-Lösungen](https://www.microsoft.com/download/details.aspx?id=15556)           |
   |     Windows Server Essentials oder Windows Server 2012     |                                                          Das Server-Dashboard                                                           |


2. Gehen Sie nach dem Abschluss des Downloads auf **Start**, **Alle Programme** und dann auf **SBS Best Practices Analyzer Tool**.

   > [!NOTE]
   >  Suchen Sie vor dem Überprüfen des Servers nach Updates.

3. Klicken Sie im Navigationsbereich auf **Überprüfung starten**.

    Wenn auf dem Quell Server Windows Server Essentials ausgeführt wird, gehen Sie wie folgt vor:

   1.  Melden Sie sich auf dem Zielserver als Administrator an und öffnen Sie das Dashboard.

   2.  Klicken Sie im Dashboard auf die Registerkarte **Geräte**.

   3.  Klicken Sie im Bereich Tasks für <**Server**auf  > **Tasks** **Best Practices Analyzer**.

4. Geben Sie im Detailbereich die Überprüfungsbezeichnung ein und klicken Sie dann auf **Überprüfung starten**. Die Überprüfungsbezeichnung ist der Name des Überprüfungsberichts, z. B. **SBS BPA Scan 1Jul2013**.

5. Nachdem die Überprüfung abgeschlossen ist, klicken Sie auf **Bericht für diese Bewährte Methoden-Überprüfung anzeigen**.

   Nachdem das BPA-Tool Informationen zur Serverkonfiguration gesammelt hat, überprüft es, ob die Informationen korrekt sind, und legt dann den Administratoren eine Liste der Informationen und Probleme nach Schweregrad sortiert vor. Die Liste beschreibt jedes Problem und bietet eine Empfehlung oder eine mögliche Lösung. Folgende drei Berichtstypen sind verfügbar:

|Berichtstyp|Beschreibung
|-----------------|-----------------
|Listenberichte|Zeigt Berichte in einer eindimensionalen Liste an.
|Strukturberichte|Zeigt Berichte in einer hierarchischen Liste an.

Wenn Sie die Beschreibung und Lösungen für ein Problem anzeigen möchten, klicken Sie im Bericht auf das betreffende Problem. Nicht alle vom BPA-Tool erfassten Probleme wirken sich auf die Migration aus, Sie sollten jedoch möglichst viele der Probleme beheben, um eine erfolgreiche Migration sicherzustellen.

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

###  <a name="create-a-plan-to-migrate-line-of-business-applications"></a><a name="BKMK_MigrateLOB"></a>Erstellen eines Plans für die Migration von Branchen Anwendungen
 Eine Branchenanwendung ist eine wichtige Computeranwendung, die für den Geschäftsbetrieb unabdingbar ist. Dabei kann es sich z. B. um Buchhaltungs-, Supply Chain Management- oder Ressourcenplanungsanwendungen handeln.

 Wenn Sie die Migration Ihrer Branchenanwendungen planen, beraten Sie sich mit dem Branchenanwendungsanbieter, um die geeignete Methode zum Migrieren der einzelnen Anwendungen zu ermitteln. Außerdem müssen Sie das Medium ermitteln, das zum Installieren der Branchenanwendungen auf dem Zielserver verwendet wird.

> [!NOTE]
>  Wenn Sie das Windows Small Business Server 2011 Essentials SDK verwendet haben, um ein angepasstes Systemintegritäts-oder Warnungs-Add-in zu entwickeln, und Sie das Add-in weiterhin mit Windows Server Essentials verwenden möchten, müssen Sie auch das Add-in aktualisieren und auf dem Ziel Server bereitstellen.


### <a name="create-a-plan-to-migrate-email-hosted-on-windows-sbs-2011-windows-sbs-2008-and-windows-sbs-2003"></a>Erstellen eines Plans zum Migrieren von auf Windows SBS 2011, Windows SBS 2008 und Windows SBS 2003 gehosteten E-Mails
 In Windows SBS 2011, Windows SBS 2008 und Windows SBS 2003 wird der E-Mail-Dienst über den Microsoft Exchange Server bereitgestellt. Windows Server Essentials bietet jedoch keinen e-Mail-Posteingangs Dienst. Wenn Sie derzeit einen Server mit Windows SSB 2011, Windows SSB 2008 oder Windows SSB 2003 zum Hosten der e-Mail-Adresse Ihres Unternehmens verwenden, müssen Sie zu einer alternativen lokalen oder gehosteten Lösung migrieren.

> [!NOTE]
>  Nachdem Sie den Quellserver aktualisiert und für die Migration vorbereitet haben, ist es empfehlenswert, eine Sicherung des aktualisierten Servers zu erstellen, bevor Sie mit der Migration fortfahren.

#### <a name="migrate-email-to-microsoft-office-365"></a>Migrieren von E-Mails zu Microsoft Office 365
 Wenn Sie sich für Microsoft Office 365 als E-Mail-Lösung für Ihre Domäne entschieden haben, folgen Sie den Anweisungen unter [Migrieren aller Postfächer zur Cloud mit einer Exchange-Übernahmemigration](https://help.outlook.com/140/ms.exch.ecp.emailmigrationwizardexchangelearnmore.aspx) , um die E-Mail-Migration zu Office 365 zu starten. Es wird empfohlen, die e-Mail-Migration abzuschließen, bevor Sie Windows Server Essentials installieren.

> [!NOTE]
>  Der Schritt zum Entfernen des lokalen Exchange-Servers auf dem Quell Server ist obligatorisch, wenn Sie Windows Server Essentials in Office 365 integrieren möchten. Informationen zum Migrieren der öffentlichen Ordner von Exchange Server zu Office 365 finden Sie im Blogbeitrag [Microsoft Exchange 2013 Public Folders Migration Scripts for Office 365](https://blogs.technet.com/b/fmustafa/archive/2013/04/11/microsoft-exchange-2013-public-folders-migration-scripts-for-office-365.aspx).
>
>  Nachdem Sie die Installation durchgeführt haben, sollten Sie das Office 365-Integrations Feature in Windows Server Essentials aktivieren, indem Sie den Task " **in Microsoft Office 365 integrieren** " ausführen.

> [!IMPORTANT]
>  Um eine Verbindung des Office 365-Migrationstools mit Exchange Server auf dem Quellserver zu ermöglichen, müssen Sie auf dem Quellserver RPC über HTTP aktivieren. Informationen zum Aktivieren von RPC über HTTP finden Sie unter [Erstmaliges Bereitstellen von RPC über HTTP in Small Business Server 2003 (Standard oder Premium)](https://technet.microsoft.com/library/bb123622%28EXCHG.65%29.aspx). Wenn das Office 365-Migrationstool nach dem Aktivieren von RPC über HTTP nicht ordnungsgemäß ausgeführt werden kann, zeigen Sie die Einstellung **ValidPorts** in der Registrierung unter HKEY_LOCAL_MACHINE\Software\Microsoft\Rpc\RpcProxy an, und stellen sicher, dass der vollqualifizierte Domänenname (Fully Qualified Domain Name, FQDN) für den Quellserver dort aufgeführt ist. Wenn der FQDN nicht aufgeführt ist, fügen Sie ihn anhand des folgenden Beispiels manuell hinzu:
>
>  remote. *contoso*.com:6001-6002;remote. *contoso*.com:6004 (ersetzen Sie *contoso* durch den Namen Ihrer Domäne).

#### <a name="migrate-email-to-another-on-premises-exchange-server"></a>Migrieren von E-Mail zu einem anderen lokalen Exchange-Server
 Informationen zum Migrieren von e-Mails zu einem anderen lokalen Exchange-Server finden Sie unter [integrieren eines lokalen Exchange-Servers in Windows Server Essentials](https://technet.microsoft.com/library/jj200172.aspx). Es wird empfohlen, dass Sie den neuen lokalen Exchange-Server nach der Installation von Windows Server Essentials einrichten und dann die e-Mail-Migration abschließen, bevor Sie den Quell Server herabstufen.

> [!NOTE]
>  Der Windows Small Business Server-POP3-Connector ist nicht in Exchange Server enthalten. Nach der Migration von Daten zu einem anderen Exchange-Server kann POP3-Connector-Funktion nicht mehr genutzt werden.

> [!NOTE]
>  Nachdem Sie den Quellserver aktualisiert und für die Migration vorbereitet haben, sollten Sie eine Sicherung des aktualisierten Servers erstellen, bevor Sie mit der Migration fortfahren.

## <a name="next-steps"></a>Nächste Schritte
 Sie haben ihren Quell Server für die Migration zu Windows Server Essentials vorbereitet.  Gehen Sie jetzt zu [Schritt 2: Installieren von Windows Server Essentials als neuer Replikat Domänen Controller](Step-2--Install-Windows-Server-Essentials-as-a-new-replica-domain-controller.md).

Alle Schritte finden Sie unter [Migrieren zu Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).

