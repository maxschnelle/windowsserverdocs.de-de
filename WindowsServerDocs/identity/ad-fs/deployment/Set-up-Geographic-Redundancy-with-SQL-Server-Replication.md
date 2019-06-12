---
title: Einrichten der geografischen Redundanz mit der SQL Server-Replikation
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: active-directory-federation-services
ms.author: billmath
ms.assetId: 7b9f9a4f-888c-4358-bacd-3237661b1935
ms.openlocfilehash: 00880d06835fad08538f634fdf2868146fc23b1a
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442918"
---
# <a name="setup-geographic-redundancy-with-sql-server-replication"></a>Einrichten der geografischen Redundanz mit der SQL Server-Replikation


> [!IMPORTANT]  
> Wenn Sie eine AD FS-Farm erstellen und SQL Server zum Speichern Ihrer Konfigurationsdaten verwenden möchten, können Sie SQLServer 2008 oder höher.
  
Wenn Sie SQL Server als Ihrem AD FS-Konfigurationsdatenbank verwenden, können Sie georeplikation einrichten\-Redundanz für Ihre AD FS-Farm mit SQL Server-Replikation. Geografische\-Redundanz Daten zwischen zwei geografisch entfernten Standorten repliziert, sodass Anwendungen, die von einem Standort zu einer anderen wechseln können. Auf diese Weise bei einem der Ausfall eines Standorts möglich weiterhin alle verfügbaren Konfigurationsdaten am zweiten Standort. Weitere Informationen finden Sie im Abschnitt"geografische Redundanz SQLServer" im [Federation Server Farm mithilfe von SQL Server](../design/Federation-Server-Farm-Using-SQL-Server.md).  
  
## <a name="prerequisites"></a>Vorraussetzungen  
Installieren und Konfigurieren einer SQL Server-Farm. Weitere Informationen finden Sie unter [https://technet.microsoft.com/evalcenter/hh225126.aspx](https://technet.microsoft.com/evalcenter/hh225126.aspx). Stellen Sie sicher, dass der SQL Server-Agent-Dienst ausgeführt wird, und auf automatischen Start festgelegt, auf dem ersten SQL-Server.  
  
## <a name="create-the-second-replica-sql-server-for-geo-redundancy"></a>Erstellen Sie den zweiten \(Replikat\) SQL Server für georedundante\-Redundanz  
  
1. Installieren von SQL Server \(Weitere Informationen finden Sie unter [ https://technet.microsoft.com/evalcenter/hh225126.aspx ](https://technet.microsoft.com/evalcenter/hh225126.aspx). Kopieren Sie die resultierenden CreateDB.sql und SetPermissions.sql-Skriptdateien mit der Replikat-SQL-Server.  
  
2. Stellen Sie sicher, dass SQL Server-Agent-Dienst ausgeführt wird, und legen Sie auf den automatischen start  
  
3. Führen Sie **exportieren\-AdfsDeploymentSQLScript** auf dem primären AD FS-Knoten, um CreateDB.sql und SetPermissions.sql Dateien zu erstellen.  Zum Beispiel:`PS:\>Export-AdfsDeploymentSQLScript -DestinationFolder . –ServiceAccountName CONTOSO\gmsa1$`.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql2.png)
  
4. Kopieren Sie die Skripts auf den sekundären Server.  Öffnen des Skripts CreateDB.sql in **SQL Management Studio** , und klicken Sie auf **Execute**.
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql4.png)

5. Öffnen Sie das Skript SetPermissions.sql in **SQL Management Studio** , und klicken Sie auf **Execute**.
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql6.png) 

   

> [!NOTE]
> Sie können auch die folgenden über die Befehlszeile verwenden. 
> 
>    `c:\>sqlcmd –i CreateDB.sql`  
> 
>    `c:\>sqlcmd –i SetPermissions.sql` 
> 
> ## <a name="create-publisher-settings-on-the-initial-sql-server"></a>Erstellen Sie verlegereinstellungen, in der ersten SQL Server  
  
1. Von der SQL Server Management Studio unter **Replikation**, klicken Sie mit der rechten Maustaste auf **lokale Veröffentlichungen** , und wählen Sie **neue Veröffentlichung... ** 
    ![Geografische Redundanz einrichten](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql7.png) </br>  

2. Klicken Sie auf dem Bildschirm des Assistenten für neue Veröffentlichung auf **Weiter**.</br>
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql8.png) </br> 
  
3. Auf **Verteiler** Seite, wählen Sie die lokalen Server als Verteiler aus, und klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql9.png) </br>   

4. Auf der **Momentaufnahme** Ordner geben \\\SQL1\repldata anstelle der Standardordner. \(ANMERKUNG: Möglicherweise müssen Sie diese Freigabe selbst erstellen\).  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql10.png) </br>   
  
5. Wählen Sie **AdfsConfigurationV3** als Veröffentlichungsdatenbank, und klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql11.png) </br>
  
6. Auf **Veröffentlichungstyp**, wählen Sie **Mergeveröffentlichung** , und klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql12.png) </br>
  
7. Auf **Abonnententypen**, wählen Sie **SQLServer 2008 oder höher** , und klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql13.png) </br> 

8. Auf der **Artikel** Seite **Tabellen** Knoten aus, um alle Tabellen, wählen Sie dann **aufheben\-überprüfen SyncProperties** Tabelle \(dieser darf nicht sein. repliziert\)</br>
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql14.png) </br>    
  
9. Auf der **Artikel** Seite **benutzerdefinierte Funktionen** Knoten, wählen alle benutzerdefinierten Funktionen aus, und klicken Sie auf **Weiter**...  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql15.png) </br>    

10. Auf der **Probleme mit Artikeln** auf **Weiter**.  
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql16.png) </br>   

11. Auf der **Tabellenzeilen filtern** auf **Weiter**.  
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql17.png) </br>   
12. Auf der **Momentaufnahme-Agent** Seite standardmäßig direkt und 14 Tage aus, klicken Sie auf **Weiter**.  
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql18.png) </br>   
    Möglicherweise müssen Sie ein Domänenkonto für den SQLServerAgent zu erstellen. Verwenden Sie die Schritte in [Konfigurieren von SQL-Anmeldung für das Domänenkonto, das CONTOSO\\Sqlagent](Set-up-Geographic-Redundancy-with-SQL-Server-Replication.md#sqlagent) SQL-Anmeldung für diesen neuen AD-Benutzer erstellen und bestimmte Berechtigungen zuweisen.  
  
13. Auf der **Agentsicherheit** auf **Sicherheitseinstellungen** und geben Sie den Benutzernamen\/Kennwort eines Domänenkontos \(nicht um ein GMSA\) für die SQL-Agent erstellt und Klicken Sie auf **OK**.  Klicken Sie auf **Weiter**.  
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql19.png) </br>  

14. Auf der **Aktionen des Assistenten** auf **Weiter**.   
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql20.png) </br>

15. Auf der **schließen Sie den Assistenten** Seite, geben Sie einen Namen für die Veröffentlichung aus, und klicken Sie auf **Fertig stellen**. 
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql21.png) </br>  

16. Der Status des Erfolgs sollte angezeigt werden, nachdem die Veröffentlichung erstellt wurde.  Klicken Sie auf **Schließen**.
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql22.png) </br>  

17. Zurück in SQL Server Management Studio, mit der Maustaste der neuen Veröffentlichung, und klicken Sie auf **Replikationsmonitor starten**.  
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql23.png) </br> 
  
## <a name="create-subscription-settings-on-the-replica-sql-server"></a>Erstellen von Einstellungen auf dem SQL Server-Replikat  
Stellen Sie sicher, dass Sie die Einstellungen für den Verleger in der ersten SQL Server erstellt, wie oben beschrieben, und klicken Sie dann die folgenden Schritte aus:  
  
1. Auf dem Replikat SQL Server, SQL Server Management Studio unter **Replikation**, klicken Sie mit der rechten Maustaste auf **lokale Abonnements** , und wählen Sie **neues Abonnement...** . ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql24.png) </br>  

2. Auf der **Assistenten für neue Abonnements** auf **Weiter**.
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql25.png) </br>   
  
3. Auf der **Veröffentlichung** Seite, wählen Sie den Herausgeber aus der Dropdownliste aus.  Erweitern Sie **AdfsConfigurationV3** und wählen Sie den Namen der zuvor erstellten Veröffentlichung, und klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql26.png) </br> 
  
4. Auf der **Speicherort des Merge-Agent** Seite **jeden Agent auf seinem Abonnenten ausführen \(Pullabonnements\)**  \(standardmäßig\) , und klicken Sie auf  **Nächste**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql27.png) </br> Dies bestimmt, zusammen mit den Abonnementtyp, die weiter unten wird die Logik zur konfliktlösung. \(Weitere Informationen finden Sie unter [erkennen und Resolve Merge Replication Conflicts](https://technet.microsoft.com/library/ms151191.aspx). </br>
 
5. Auf der **Abonnenten** Seite **AdfsConfigurationV3** als Abonnentendatenbank, und klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql28.png) </br> 
  
6. Auf der **Sicherheit für den Merge-Agent** auf **...**  , und geben Sie den Benutzernamen und das Kennwort eines Domänenkontos \(nicht um ein GMSA\) erstellt für den SQL-Agent mithilfe der Auslassungspunkte im Feld und klicken Sie auf **Weiter**.
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql30.png) </br> 
  
7. Auf **Synchronisierungszeitplan**, wählen Sie **dauerhaft ausführen** , und klicken Sie auf **Weiter**. 
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql31.png) </br> 
 
8. Auf **Abonnements initialisieren**, klicken Sie auf **Weiter**.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql32.png) </br> 
  
9. Auf **Abonnementtyp**, wählen Sie **Client** , und klicken Sie auf **Weiter**.  
  
   Dies wirkt sich sind dokumentiert [hier](https://technet.microsoft.com/library/ms151191.aspx) und [hier](https://technet.microsoft.com/library/ms151170.aspx).  Im Wesentlichen nehmen wir die einfachen "first zum Verleger gewinnt" konfliktlösung, und wir müssen nicht für andere Abonnenten erneut veröffentlichen.  
   ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql33.png) </br>
   
10. Auf der **Aktionen des Assistenten** Seite **erstellen Sie das Abonnement** aktiviert ist, und klicken Sie auf **Weiter**. 
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql34.png) </br>

11. Auf der **schließen Sie den Assistenten** auf **Fertig stellen**. 
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql35.png) </br>

12. Wenn das Abonnement der Erstellungsvorgang abgeschlossen ist, sollte erfolgreich angezeigt werden. Klicken Sie auf **Schließen**. 
    ![Richten Sie die geografische Redundanz](media/Set-up-Geographic-Redundancy-with-SQL-Server-Replication/sql36.png) </br>
  
## <a name="verify-the-process-of-initialization-and-replication"></a>Überprüfen Sie den Prozess der Initialisierung und Replikation  
  
1.  Auf dem primären SQLServer rechten\-klicken Sie auf die **Replikation** Knoten, und klicken Sie auf **Replikationsmonitor starten**.  
  
2.  In **Replikationsmonitor**, klicken Sie auf die Veröffentlichung.  
  
3.  Auf der **alle Abonnements** Registerkarte, klicken Sie mit der rechten Maustaste auf und **Details anzeigen**.  
  
    Sie sollten möglicherweise viele Einträge unter finden Sie unter **Aktionen** für die erste Replikation.  
  
4.  Darüber hinaus finden Sie unter den **SQL Server-Agent\\Aufträge** Knoten aus, um den Auftrag\(s\) das Ausführungsintervall für die Vorgänge der Veröffentlichung\/Abonnement.  Nur lokale Aufträge werden so angezeigt, also stellen Sie sicher auf dem Verleger und dem Abonnenten für die Problembehandlung.  Rechts\-klicken Sie auf einen Auftrag, und wählen Sie **Versionsgeschichte** Ausführungsverlauf anzeigen und die Ergebnisse.  
  
## <a name="sqlagent"></a>Konfigurieren von SQL-Anmeldung für das Domänenkonto, das CONTOSO\\Sqlagent  
  
1.  Erstellen Sie eine neue Anmeldung auf der primären und Replikat SQL Server mit dem Namen CONTOSO\\Sqlagent \(der Namen des neuen Domänenbenutzers in erstellt und konfiguriert die **Agentsicherheit** Seite in den oben beschriebenen.\)  
  
2.  Direkt in SQL Server,\-klicken Sie auf die Anmeldung, die Sie erstellt haben, und wählen Sie die Eigenschaften, klicken Sie dann unter dem **Benutzerzuordnung** Registerkarte, die dieser Anmeldung zu **AdfsConfiguration** und **AdfsArtifact**  Datenbanken mit öffentlichen und Db\_Genevaservice Rollen. Auch die Verteilungsdatenbank dieser Anmeldung zugeordnet und Hinzufügen von Db\_Rolle "Besitzer" für die Verteilung und Adfsconfiguration Tabellen.  Hierzu ggf. auf primären und Replikat-SQL-Server. Weitere Informationen finden Sie unter [Replication Agent Security Model](https://technet.microsoft.com/library/ms151868.aspx).  
  
3.  Geben Sie die entsprechende Domäne Konto Lese- und Schreibberechtigungen für die Freigabe, die als Verteiler konfiguriert.  Stellen Sie sicher, dass Sie lesen und Berechtigungen sowohl auf die Freigabeberechtigungen und die Berechtigungen für die lokale Datei schreiben.  
  
## <a name="configure-ad-fs-nodes-to-point-to-the-sql-server-replica-farm"></a>Konfigurieren von AD FS-Knoten\(s\) , zeigen Sie auf der SQL Server-Replikat-Farm  
Nun, da Sie die geografische Redundanz eingerichtet haben, können die AD FS-farmknoten zeigen Sie auf der Replikat-SQL Server-Farm mithilfe der standardmäßigen AD FS "beitreten" Farm Funktionen, entweder über die AD FS-Konfiguration-Assistenten-Benutzeroberfläche oder mithilfe von Windows PowerShell konfiguriert werden.  
  
Wenn Sie die AD FS-Konfiguration-Assistenten-Benutzeroberfläche verwenden, wählen Sie **Hinzufügen eines Verbundservers zu einer Verbundserverfarm**. **Nicht** wählen **Erstellen des ersten Verbundservers in einer Verbundserverfarm**.  
  
Wenn Sie Windows PowerShell verwenden, führen Sie **hinzufügen\-AdfsFarmNode**. **Nicht** ausführen **installieren\-AdfsFarm**.  
  
Geben Sie bei Aufforderung die hostanwendung und Instanz-Namen des Replikats an SQL Server, **nicht** der ersten SqlServer.  
