---
title: Einrichten der geografischen Redundanz mit der SQL Server-Replikation
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: a9f29c1eb19a8241eac5afb5c87581e6c988c3c8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>Einrichten der geografischen Redundanz mit der SQL Server-Replikation

>Gilt für: Windows Server 2016, Windows Server2012 R2

> [!IMPORTANT]  
> Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQLServer 2008 oder höher.
  
Wenn Sie SQL Server als Ihre AD FS-Konfigurationsdatenbank verwenden, können Sie Geo\ Redundanz für die SQL Server-Replikation mit AD FS-Farm einrichten. Geo\ Redundanz repliziert Daten zwischen zwei geografisch weit voneinander entfernten Standorten, sodass Anwendungen von einem Standort zu einem anderen wechseln können. Auf diese Weise kann bei einem Ausfall eines Standorts weiterhin alle verfügbaren Konfigurationsdaten am zweiten Standort haben. Weitere Informationen finden Sie im Abschnitt"geografischen Redundanz SQLServer" in [Federation Server Farm mithilfe von SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Installieren und Konfigurieren einer SQL Server-Farm. Weitere Informationen finden Sie unter [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Klicken Sie auf die ursprüngliche SQL Server stellen Sie sicher, dass der SQL Server-Agent-Dienst ausgeführt wird, und auf den automatischen Start festgelegt.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>Erstellen Sie die zweite \(replica\) SQL Server für die Geo\-Redundanz  
  
1.  Installieren von SQL Server \ (Weitere Informationen finden Sie unter [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Kopieren Sie die resultierenden Skriptdateien CreateDB.sql und SetPermissions.sql mit dem Replikat SqlServer.  
  
2.  Stellen Sie sicher, dass SQL Server-Agent-Dienst ausgeführt wird, und legen Sie auf den automatischen Start  
  
3.  Führen Sie **Export\ AdfsDeploymentSQLScript** auf dem primären AD FS-Knoten CreateDB.sql und SetPermissions.sql-Dateien zu erstellen.  Beispiel:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql2.png)
  
4.  Kopieren Sie die Skripts auf dem sekundären Server.  Öffnen Sie das Skript "CreateDB.sql" in **SQL Management Studio**, und klicken Sie auf **Execute**.
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql4.png)

5. Öffnen Sie das Skript SetPermissions.sql in in **SQL Management Studio**, und klicken Sie auf **Execute**.
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql6.png) 

   

>[!NOTE]
>Sie können auch die folgenden Elemente aus der Befehlszeile verwenden. 
>
>    `c:\>sqlcmd –i CreateDB.sql`  
>  
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
## <a name="create-publisher-settings-on-the-initial-sql-server"></a>Erstellen von Publisher-Einstellungen auf dem ursprünglichen SQL Server  
  
1.  Von der SQL Server Management Studio unter **Replikation**, klicken Sie mit der rechten Maustaste auf **lokale Publikationen**, und wählen Sie **neue Publikation... **<ph x="4">
![</ph> Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql7.png) </br>  

2.  Klicken Sie auf dem Bildschirm des Assistenten für neue Publikation auf **Weiter**.</br>
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql8.png) </br> 
  
3.  Auf **Verteiler** Seite lokalen Server als Verteiler und auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql9.png) </br>   

4.  Auf der **Snapshot** Ordner geben \\\SQL1\repldata anstelle von Standardordner. \ (Hinweis: Möglicherweise müssen Sie diese Freigabe Yourself\ erstellen).  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql10.png) </br>   
  
5.  Wählen Sie **AdfsConfigurationV3** als Publikationsdatenbank und auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql11.png) </br>
  
6.  Auf **Publikationstyp**, wählen Sie **Mergepublikation**, und klicken Sie auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql12.png) </br>
  
7.  Auf **Abonnententypen**, wählen Sie **SQLServer 2008 oder höher**, und klicken Sie auf **Weiter**.  
 ![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql13.png) </br> 

8.  Auf der **Artikel** Seite **Tabellen** Knoten, wählen Sie dann alle Tabellen **Un\ Kontrollkästchen SyncProperties** Tabelle \ (diese sollten Replicated\ nicht.)</br>
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql14.png) </br>    
  
9.  Auf der **Artikel** Seite **benutzerdefinierten Funktionen** Knoten alle benutzerdefinierten Funktionen auswählen und auf **Weiter**...  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql15.png) </br>    

10. Auf der **Artikel Probleme** auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql16.png) </br>   

11. Auf der **Tabellenzeilen filtern** auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql17.png) </br>   
12. Auf der **Snapshot-Agent** Seite, wählen Sie die Standardeinstellungen der sofortigen und 14Tage, klicken Sie auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql18.png) </br>   
Möglicherweise müssen Sie ein Domänenkonto für den SQL-Agent erstellen. Verwenden Sie die Schrittein [konfigurieren SQL-Anmeldung für das Domänenkonto CONTOSO\\sqlagent](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) SQL-Anmeldung für diesen neuen Active Directory-Benutzer und spezielle Berechtigungen.  
  
13. Auf der **Agentsicherheit** auf **Sicherheitseinstellungen** und geben Sie die Username\/Kennwort für ein Domänenkonto \ (und nicht GMSA\) erstellt, für die SQL-Agent und auf **OK**.  Klicken Sie auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql19.png) </br>  

14. Auf der **Aktionen des Assistenten** auf **Weiter**.   
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql20.png) </br>

15. Auf der **Abschließen des Assistenten** Seite, geben Sie einen Namen für die Publikation, und klicken Sie auf **Fertig stellen**. 
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql21.png) </br>  

16. Nach dem Erstellen der Publikation sollten Sie den Status der Erfolg sehen.  Klicken Sie auf **schließen **.
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql22.png) </br>  

17. Zurück in SQL Server Management Studio Maustaste auf die neue Publikation, und klicken Sie auf **Replikationsmonitor starten**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>Erstellen von abonnementeinstellungen für das SQL Server-Replikat  
Stellen Sie sicher, dass Sie die herausgebereinstellungen auf dem ursprünglichen SQL Server erstellt, wie oben beschrieben, und führen Sie das folgende Verfahren:  
  
1.  Für das SQL Server-Replikat von SQL Server Management Studio unter **Replikation**, klicken Sie mit der rechten Maustaste auf **lokale Abonnements**, und wählen Sie **neues Abonnement... **. ![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql24.png) </br>  

2.  Auf der **Assistenten für neue Abonnements** auf **Weiter**.
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql25.png) </br>   
  
3.  Auf der **Publikation** Seite, wählen Sie den Herausgeber aus der Dropdownliste aus.  Erweitern Sie **AdfsConfigurationV3** und wählen Sie den Namen der oben erstellten Publikation, und klicken Sie auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql26.png) </br> 
  
4.  Auf der **Merge-Agent-Speicherort** Seite **führen Sie jeden Agent an die Abonnenten \(pull subscriptions\)** \(the default\), und klicken Sie auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql27.png) </br> Bestimmen Sie zusammen mit folgenden Abonnementtyp die Logik der Konflikt Auflösung. \ (Weitere Informationen finden Sie unter [erkennen und beheben Zusammenführen von Replikationskonflikten](https://technet.microsoft.com/library/ms151191.aspx). </br>
 
5.  Auf der **Abonnenten** Seite **AdfsConfigurationV3** als Abonnentendatenbank, und klicken Sie dann auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql28.png) </br> 
  
6.  Auf der **Merge-Agent-Sicherheit** auf **... **, und geben Sie den Benutzernamen und das Kennwort eines Domänenkontos \ (und nicht GMSA\), die für den SQL-Agent mithilfe das Kästchen Ellipsen erstellt und und klicken Sie auf **Weiter**.
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql30.png) </br> 
  
7.  Auf **Synchronisierungszeitplan**, wählen Sie **fortlaufend ausführen**, und klicken Sie auf **Weiter**. 
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql31.png) </br> 
 
8.  Auf **Abonnements initialisieren**, klicken Sie auf **Weiter**.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql32.png) </br> 
  
9.  Auf **Abonnementtyp**, wählen Sie **Client**, und klicken Sie auf **Weiter**.  
  
    Dies wirkt sich dokumentiert sind [hier](https://technet.microsoft.com/library/ms151191.aspx) und [hier](https://technet.microsoft.com/library/ms151170.aspx).  Im Wesentlichen nehmen wir die Auflösung des Konflikts für einfache "zuerst Herausgeber Wins", und wir müssen nicht für andere Abonnenten erneut veröffentlichen müssen.  
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql33.png) </br>
   
10. Auf der **Aktionen des Assistenten** sicher, dass Seite **erstellen Sie das Abonnement** aktiviert ist, und klicken Sie auf **Weiter**. 
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql34.png) </br>

11. Auf der **Abschließen des Assistenten** auf **Fertig stellen**. 
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql35.png) </br>

12. Nachdem das Abonnement den Erstellungsprozess abgeschlossen ist, sollten Sie Erfolg sehen. Klicken Sie auf **schließen **. 
![Einrichten der geografischen Redundanz](media\Set-up-Geographic-Redundancy-with-SQL-Server-Replication\sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>Überprüfen Sie den Prozess der Initialisierung und Replikation  
  
1.  Auf dem primären SQL-Server klicken Sie auf die **Replikation** Knoten, und klicken Sie dann auf **Replikationsmonitor starten**.  
  
2.  In **Replikationsmonitor**, klicken Sie auf die Publikation.  
  
3.  Auf der **alle Abonnements** Registerkarte, klicken Sie mit der rechten Maustaste auf und **Details anzeigen**.  
  
    Sie können viele Einträge unter angezeigt werden müssten **Aktionen** für die erste Replikation.  
  
4.  Sie können darüber hinaus sehen Sie unter der **SQL Server-Agent\\Jobs** Knoten finden in der Job\(s\) zum Ausführen der Vorgänge des Publication\/Abonnements geplant.  Nur lokale Aufträge werden so angezeigt, stellen Sie daher sicher, dass Sie für die Problembehandlung auf dem Verleger und Abonnenten überprüfen.  Mit der rechten Maustaste auf einen Auftrag und wählen Sie **Verlauf anzeigen** Ansicht Ausführungsverlauf und die Ergebnisse.  
  
## <a name="sqlagent"></a>Konfigurieren der SQL-Anmeldung für das Domänenkonto CONTOSO\\sqlagent  
  
1.  Erstellen Sie eine neue Anmeldung auf dem primären und dem Replikat SQL Server mit dem Namen CONTOSO\\sqlagent \ (der Namen der neuen Domäne erstellt und konfiguriert die **Agentsicherheit** Seite in das oben beschriebene Verfahren. \)  
  
2.  In SQL Server, klicken Sie auf den Benutzernamen, die Sie erstellt haben, und wählen Eigenschaften, klicken Sie dann unter der **Benutzerzuordnung** Registerkarte, die dieser Anmeldung zugeordnet **AdfsConfiguration** und **AdfsArtifact** Datenbanken mit öffentlichen und Db\_genevaservice Rollen. Außerdem ordnen Sie dieses Protokoll in Verteilungsdatenbank und Db\_owner Rolle für die Verteilung und "adfsconfiguration"-Tabellen.  Dies ggf. auf primären und Replikat mit SqlServer. Weitere Informationen finden Sie unter [Replikations-Agent-Sicherheitsmodell](https://technet.microsoft.com/library/ms151868.aspx).  
  
3.  Geben Sie die entsprechende Domäne Konto Lese- und Schreibberechtigungen für die Freigabe als Verteiler konfiguriert.  Stellen Sie sicher, dass Sie gelesen und sowohl auf die Freigabe-als auch die lokalen Berechtigungen Schreibberechtigungen.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>Konfigurieren von AD FS-node\(s\) auf dem SQL Server-Replikat-farm  
Nun, dass Sie geografischen Redundanz eingerichtet haben, können die AD FS-Farmknoten konfiguriert werden, dass auf der Replikat-SQL Server-Farm mithilfe der standardmäßigen AD FS "Join" Farm Funktionen, entweder von der AD FS-Konfiguration-Assistenten-Benutzeroberfläche oder mithilfe von Windows PowerShell verweisen.  
  
Wenn Sie die AD FS-Konfiguration-Assistenten-Benutzeroberfläche verwenden, wählen Sie **Hinzufügen eines Verbundservers zu einer Verbundserverfarm**. **Nicht** wählen **Erstellen des ersten Verbundservers in einer Verbundserverfarm**.  
  
Wenn Sie Windows PowerShell verwenden, führen Sie **Add-AdfsFarmNode**. **Nicht** ausführen **Install\ AdfsFarm**.  
  
Wenn Sie aufgefordert werden, geben Sie den Host und Instanz Namen der SQL Server-Replikat **nicht** die ursprüngliche SqlServer.  
