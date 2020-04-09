---
title: Einrichten der geografischen Redundanz mit SQL Server-Replikation
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 54106ae635d44368542986c7c469560981f9888a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855843"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>Einrichten der geografischen Redundanz mit SQL Server-Replikation


> [!IMPORTANT]  
> Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern der Konfigurationsdaten verwenden möchten, können Sie SQL Server 2008 oder höher verwenden.
  
Wenn Sie SQL Server als AD FS Konfigurations Datenbank verwenden, können Sie mithilfe SQL Server Replikation Geor\-Redundanz für Ihre AD FS Farm einrichten. Geor\-Redundanz repliziert Daten zwischen zwei geografisch entfernten Standorten, sodass Anwendungen von einem Standort zu einem anderen wechseln können. Auf diese Weise können Sie bei einem Ausfall eines Standorts weiterhin alle Konfigurationsdaten am zweiten Standort verfügbar haben. Weitere Informationen finden Sie im Abschnitt "SQL Server geografische Redundanz" in der Verbund [Server Farm unter Verwendung SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md).  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Installieren und konfigurieren Sie eine SQL Server-Farm. Weitere Informationen finden Sie unter [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Vergewissern Sie sich auf dem ersten SQL Server, dass der SQL Server-Agent-Dienst ausgeführt wird und auf automatischen Start festgelegt ist.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>Erstellen Sie die zweite \(Replikat\) SQL Server für Geor\-Redundanz.  
  
1. Installieren Sie SQL Server \(Weitere Informationen finden Sie unter [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Kopieren Sie die sich ergebenden Skriptdateien "| atedb. SQL" und "setberechtigungs Datei" auf den SQL-Replikat  
  
2. Sicherstellen, dass SQL Server-Agent-Dienst ausgeführt wird und auf automatischen Start eingestellt ist  
  
3. Führen Sie **Export\-adfsdeploymentsqlscript** auf dem primären AD FS Knoten aus, um die Dateien "anatedb. SQL" und "setberechtigungs. SQL" zu erstellen.  Beispiel:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. Kopieren Sie die Skripts auf den sekundären Server.  Öffnen Sie das Skript "deedb. SQL" in **SQL Management Studio** , und klicken Sie auf **Ausführen**.
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. Öffnen Sie in **SQL Management Studio** das Skript setberechtigungs. SQL, und klicken Sie auf **Ausführen**.
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> Sie können auch den folgenden Befehl in der Befehlszeile verwenden. 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>Erstellen von Verleger Einstellungen auf dem ersten SQL Server  
  
1. Klicken Sie in der SQL Server Management Studio unter **Replikation**mit der rechten Maustaste auf **Lokale Veröffentlichungen** , und wählen Sie **neue Veröffentlichung...** 
   , ![geografische Redundanz einrichten](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. Klicken Sie auf dem Bildschirm Assistent für neue Veröffentlichung auf **weiter**.</br>
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. Wählen Sie auf der Seite **Verteiler** die Option Lokaler Server als Verteiler, und klicken Sie auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. Geben Sie auf der Seite **Momentaufnahme** Ordner \\\sql1\repldata anstelle des Standard Ordners ein. \(Hinweis: Sie müssen diese Freigabe möglicherweise selbst erstellen\).  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. Wählen Sie **AdfsConfigurationV3** als Veröffentlichungs Datenbank aus, und klicken Sie auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. Wählen Sie unter **Veröffentlichungstyp**die Option **Mergeveröffentlichung** aus, **und klicken Sie**  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. Wählen Sie unter **Abonnenten Typen** **SQL Server 2008 oder** höher aus, und klicken Sie auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. Wählen Sie auf der Seite **Artikel** den Knoten **Tabellen** aus, um alle Tabellen auszuwählen, und klicken Sie dann auf **\-Tabelle syncproperties-Tabelle überprüfen** \(diese nicht repliziert werden sollte\)</br>
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. Wählen Sie auf der Seite **Artikel** den Knoten **benutzerdefinierte Funktionen** aus, um alle benutzerdefinierten Funktionen auszuwählen, und klicken Sie auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. Klicken Sie auf der Seite **Artikel Probleme** auf **weiter**.  
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. Klicken Sie auf der Seite **Tabellenzeilen filtern** auf **weiter**.  
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. Wählen Sie auf der Seite **Momentaufnahmen-Agent** die Option Standardwert direkt und 14 Tage aus, und klicken Sie **dann auf weiter**.  
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    Möglicherweise müssen Sie ein Domänen Konto für den SQL-Agent erstellen. Verwenden Sie die Schritte unter [Konfigurieren der SQL-Anmeldung für das Domänen Konto "Azure-\\SQLAgent](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) ", um eine SQL-Anmeldung für diesen neuen AD-Benutzer zu erstellen und bestimmte Berechtigungen zuzuweisen.  
  
13. Klicken Sie auf der Seite **Agentsicherheit** auf **Sicherheitseinstellungen** , und geben Sie den Benutzernamen\/Kennwort eines Domänen Kontos ein, das für den SQL-Agent erstellt\) \(, und klicken Sie auf **OK**.  Klicken Sie auf **Weiter**.  
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. Klicken Sie auf der Seite **Aktionen des Assistenten** auf **weiter**.   
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. Geben Sie auf der Seite **Assistenten abschließen** einen Namen für Ihre Veröffentlichung ein, und klicken Sie auf **Fertig**stellen. 
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. Nachdem die Veröffentlichung erstellt wurde, sollte der Status erfolgreich angezeigt werden.  Klicken Sie auf **Schließen**.
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. Klicken Sie im SQL Server Management Studio mit der rechten Maustaste auf die neue Veröffentlichung, und klicken Sie auf **Replikations Monitor starten**.  
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>Erstellen von Abonnement Einstellungen für das Replikat SQL Server  
Stellen Sie sicher, dass Sie die Herausgeber Einstellungen auf dem ersten SQL Server wie oben beschrieben erstellt haben, und führen Sie dann das folgende Verfahren aus:  
  
1. Klicken Sie auf dem **Replikat**SQL Server in SQL Server Management Studio unter Replikation mit der rechten Maustaste auf **Lokale Abonnements** , und wählen Sie **Neues Abonnement...** aus. ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. Klicken Sie auf der Seite **Assistent für neue Abonnements** auf **weiter**.
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. Wählen Sie auf der Seite **Veröffentlichung** in der Dropdown-Dropdown-Gruppe den Verleger aus.  Erweitern Sie **AdfsConfigurationV3** , und wählen Sie den Namen der oben erstellten Veröffentlichung aus, und klicken Sie auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. Wählen Sie auf der Seite **Merge-Agent Speicherort** die Option **jeden Agent auf seinem Abonnenten ausführen \(Pullabonnements\)** \(der Standard\) und klicken Sie **dann auf weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> Dies bestimmt, zusammen mit dem Abonnementtyp unten, die Konflikt Auflösungs Logik. Weitere Informationen \(finden Sie unter [erkennen und Auflösen von mergereplikationskonflikten](https://technet.microsoft.com/library/ms151191.aspx). </br>
 
5. Wählen Sie auf der Seite **Abonnenten** die Option **AdfsConfigurationV3** als Abonnenten Datenbank aus, und klicken Sie auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. Klicken Sie auf der Seite **Merge-Agent Sicherheit** auf **...** , und geben Sie den Benutzernamen und das Kennwort eines Domänen\) \(Kontos ein, das für den SQL-Agent erstellt wurde, indem Sie das Feld mit den Auslassungs Zeichen verwenden, und klicken Sie auf **weiter**.
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. Wählen Sie unter **Synchronisierungs Zeitplan**fort **laufend ausführen** aus, und klicken Sie auf **weiter** 
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. Klicken Sie unter **Abonnements initialisieren**auf **weiter**.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. Wählen Sie unter **Abonnementtyp** **Client** aus, und klicken Sie auf **weiter**.  
  
   Diese Auswirkungen werden [hier](https://technet.microsoft.com/library/ms151191.aspx) und [hier](https://technet.microsoft.com/library/ms151170.aspx)dokumentiert.  Im Grunde nehmen wir die einfache Konfliktlösung "First to Publisher WINS" und müssen nicht erneut für andere Abonnenten veröffentlicht werden.  
   ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. Vergewissern Sie sich, dass auf der Seite **Aktionen des Assistenten** **die Option Abonnement** wird aktiviert ist, und klicken Sie auf **weiter** 
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. Klicken Sie auf der Seite **Assistenten abschließen** auf **Fertig**stellen. 
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. Nachdem das Abonnement den Erstellungs Vorgang abgeschlossen hat, sollte der Erfolg angezeigt werden. Klicken Sie auf **Schließen**. 
    ![Einrichten der geografischen Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>Überprüfen des Initialisierungs Prozesses und der Replikation  
  
1.  Klicken Sie auf dem primären SQL Server mit der rechten\-auf den Knoten **Replikation** , und klicken Sie auf **Replikations Monitor**  
  
2.  Klicken Sie im **Replikations Monitor**auf die Veröffentlichung.  
  
3.  Klicken Sie mit der rechten Maustaste auf der Registerkarte **alle Abonnements** auf **Details**.  
  
    Sie sollten in der Lage sein, unter **Aktionen** für die erste Replikation viele Einträge anzuzeigen.  
  
4.  Darüber hinaus können Sie unter dem Knoten **SQL Server-Agent\\Aufträge** sehen, wie der Auftrag\(s\) geplant ist, um die Vorgänge des Veröffentlichungs\/Abonnements auszuführen.  Es werden nur lokale Aufträge angezeigt. Vergewissern Sie sich daher, dass der Verleger und der Abonnent die Problembehandlung durchführen.  Klicken Sie mit der rechten\-auf einen Auftrag, und wählen Sie **Verlauf anzeigen** , um Ausführungs Verlauf und Ergebnisse anzuzeigen.  
  
## <a name="configure-sql-login-for-the-domain-account-contososqlagent"></a><a name="sqlagent"></a>Konfigurieren der SQL-Anmeldung für das Domänen Konto\\SQLAgent  
  
1.  Erstellen Sie eine neue Anmeldung auf dem primären und dem Replikat SQL Server mit dem Namen "\\SQLAgent" \(dem Namen des neuen Domänen Benutzers, der in den obigen Verfahren auf der Seite " **Agentsicherheit** " erstellt und konfiguriert wurde.\)  
  
2.  Klicken Sie in SQL Server mit der rechten\-auf den Anmelde Namen, den Sie erstellt haben, und wählen Sie Eigenschaften aus. Ordnen Sie dann auf der Registerkarte **Benutzer Zuordnung** diese Anmeldung den **adfsconfiguration** -und **adfsartefaktdatenbanken** mit den Rollen Public und DB\_genevaservice zu Ordnen Sie diese Anmeldung außerdem der Verteilungs Datenbank zu, und fügen Sie die Rolle "DB\_Owner" für die Verteilungs-und die adfsconfiguration  Dies gilt sowohl für den primären als auch für den SQL Server-Replikat Server. Weitere Informationen finden Sie unter [Sicherheitsmodell des Replikations-Agents](https://technet.microsoft.com/library/ms151868.aspx).  
  
3.  Geben Sie dem entsprechenden Domänen Konto Lese-und Schreibberechtigungen für die Freigabe, die als Verteiler konfiguriert ist.  Stellen Sie sicher, dass Sie Lese-und Schreibberechtigungen sowohl für die Freigabe Berechtigungen als auch für die lokalen Dateiberechtigungen festlegen.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>Konfigurieren Sie AD FS Knoten\(s\), um auf die SQL Server Replikat Farm zu verweisen.  
Nachdem Sie georedundanz eingerichtet haben, können die AD FS Farm-Knoten so konfiguriert werden, dass Sie auf Ihr Replikat SQL Server Farm mit den standardmäßigen AD FS "Join"-Farm Funktionen verweisen, entweder über die Benutzeroberfläche des AD FS Konfigurations-Assistenten oder mithilfe von Windows PowerShell.  
  
Wenn Sie die Benutzeroberfläche des AD FS Konfigurations-Assistenten verwenden, wählen Sie Verbund **Server zu einer Verbund Serverfarm hinzufügen**aus. **Do NOT** Wählen Sie nicht **die Option ersten Verbund Server in einer Verbund Serverfarm erstellen aus**.  
  
Wenn Sie Windows PowerShell verwenden, führen Sie **\-adfsfarmnode hinzufügen**aus. Führen Sie **install\-adfsfarm** **nicht** aus.  
  
Wenn Sie dazu aufgefordert werden, geben Sie den Host-und Instanznamen des Replikat SQL Server und **nicht** den ursprünglichen SQL Server an.  
