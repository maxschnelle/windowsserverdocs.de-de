---
title: Migrieren der WSUS-Datenbank von (interne Windows-Datenbank) zu SQL
description: 'Thema zu Windows Server Update Service (WSUS): Migrieren der WSUS-Datenbank (SUSDB) von einer internen Windows-Daten Bank Instanz zu einer lokalen oder Remote Instanz von SQL Server.'
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: get-started article
ms.assetid: 90e3464c-49d8-4861-96db-ee6f8a09g7dr
author: coreyp-at-msft
ms.author: coreyp
manager: dougkim
ms.date: 07/25/2018
ms.openlocfilehash: 0977aa1fd9a6848bd7b85bb592b6a82556277e72
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361578"
---
>Gilt für: Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>Migrieren der WSUS-Datenbank von wid zu SQL

Führen Sie die folgenden Schritte aus, um die WSUS-Datenbank (SUSDB) von einer internen Windows-Daten Bank Instanz zu einer lokalen oder Remote Instanz von SQL Server zu migrieren.

## <a name="prerequisites"></a>Erforderliche Komponenten

- SQL-Instanz. Hierbei kann es sich um den **MSSQLSERVER** -Standard Server oder um eine benutzerdefinierte Instanz handeln.
- SQL Server Management Studio
- WSUS mit installierter wid-Rolle
- IIS (Dies ist normalerweise der Fall, wenn Sie WSUS über Server-Manager installieren). Er ist noch nicht installiert. er muss sein.

## <a name="migrating-the-wsus-database"></a>Migrieren der WSUS-Datenbank

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>IIS-und WSUS-Dienste auf dem WSUS-Server abbrechen

Führen Sie in PowerShell (mit erhöhten Rechten) Folgendes aus:

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>Trennen von SUSDB von der internen Windows-Datenbank

#### <a name="using-sql-management-studio"></a>Verwenden von SQL Management Studio

1. Klicken Sie mit der rechten Maustaste auf **SUSDB** - @ no__t-2 **Tasks** - @ no__t-5 Klicken Sie auf **Detach**: ![image1 @ no__t-8
2. Aktivieren Sie **vorhandene Verbindungen löschen** , und klicken Sie auf **OK** (optional, wenn aktive Verbindungen vorhanden sind).
    ![image2 @ no__t-1

#### <a name="using-command-prompt"></a>Verwenden der Eingabeaufforderung

> [!IMPORTANT]
> Diese Schritte zeigen, wie Sie die WSUS-Datenbank (SUSDB) mit dem Hilfsprogramm **sqlcmd** von der internen Windows-Daten Bank Instanz trennen. Weitere Informationen zum **sqlcmd** -Hilfsprogramm finden Sie unter [sqlcmd Utility](https://go.microsoft.com/fwlink/?LinkId=81183).
> 1. Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten
> 2. Führen Sie den folgenden SQL-Befehl aus, um die WSUS-Datenbank (SUSDB) von der internen Windows-Daten Bank Instanz mit dem **sqlcmd** -Hilfsprogramm zu trennen:

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>Kopieren Sie die SUSDB-Dateien in die SQL Server

1. Kopieren Sie **SUSDB. mdf** und **SUSDB\_Log.ldf** aus dem Ordner "wid Data" ( **% System Drive%** \* * windows\wid\data * *) in den SQL-instanzdatenordner.

> [!TIP]
> Wenn der SQL-instanzordner z. b. " **c:\Programme\Microsoft SQL server\mssql12." lautet, Mssqlserver\mssql**und der Ordner "wid Data" lautet " **c:\windows\wid\data** ". Kopieren Sie die SUSDB-Dateien aus " **c:\windows\wid\data** " in " **c:\Programme\Microsoft SQL server\mssql12.". MSSQLSERVER\MSSQL\Data**

### <a name="attach-susdb-to-the-sql-instance"></a>Anfügen von SUSDB an die SQL-Instanz

1. Klicken Sie in **SQL Server Management Studio**unter dem **Instanzknoten** mit der rechten Maustaste auf **Datenbanken**, und klicken Sie dann auf **Anfügen**.
    ![image3 @ no__t-1
2. Klicken Sie im Feld **Datenbanken** anfügen unter anzufügende **Datenbanken auf**die Schaltfläche **Hinzufügen** , suchen Sie nach der Datei **SUSDB. mdf** (aus dem Ordner wid kopiert), und klicken Sie dann auf **OK**.
    ![image4 @ no__t-1 ![image5 @ no__t-3

> [!TIP]
> Dies kann auch mithilfe von Transact-SQL durchgeführt werden.  Anweisungen zum Anfügen [einer Datenbank](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) finden Sie in der SQL-Dokumentation.
>
> Beispiel (Verwenden von Pfaden aus dem vorherigen Beispiel):
> ```sql
>    USE master;
>    GO
>    CREATE DATABASE SUSDB
>    ON
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Data\SUSDB.mdf'),
>        (FILENAME = 'C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Log\SUSDB_Log.ldf')
>        FOR ATTACH;
>    GO
>```

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>Überprüfen von SQL Server und Daten Bank Anmeldungen und-Berechtigungen

#### <a name="sql-server-login-permissions"></a>Anmelde Berechtigungen SQL Server

Überprüfen Sie nach dem Anfügen der SUSDB, ob **NT-Autorität \ Netzwerkdienst** über Anmelde Berechtigungen für die Instanz von SQL Server verfügt, indem Sie folgende Schritte ausführen:

1. Gehe zu SQL Server Management Studio
2. Öffnen der Instanz
3. Klicken Sie auf **Sicherheit**
4. Klicken Sie auf **Anmeldungen** .

Das Konto **NT-Autorität \ Netzwerkdienst** sollte aufgeführt werden. Wenn dies nicht der Fall ist, müssen Sie diese hinzufügen, indem Sie einen neuen Anmelde Namen hinzufügen.

> [!IMPORTANT]
> Wenn sich die SQL-Instanz auf einem anderen Computer als WSUS befindet, muss das Computer Konto des WSUS-Servers im Format **[FQDN] \\ [wsuscomputername] $** aufgeführt werden.  Wenn dies nicht der Fall ist, können Sie mit den folgenden Schritten hinzugefügt werden, indem Sie NT-Autorität **\ Netzwerkdienst** durch das Computer Konto des WSUS-Servers ersetzen ( **[FQDN] \\ [wsuscomputername] $** ). Dies ist ***zusätzlich zum*** erteilen von Berechtigungen für die **NT-Autorität \ Netzwerkdienst**

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>Hinzufügen von NT-Autorität \ Netzwerkdienst und erteilen von Berechtigungen

1. Klicken Sie mit der rechten Maustaste auf **Anmeldungen** , und klicken Sie auf **neue Anmeldung.**
    ![image6 @ no__t-1
2. Geben Sie auf der Seite **Allgemein** den **Anmelde Namen** (**NT-Autorität \ Netzwerkdienst**) ein, und legen Sie die **Standarddatenbank** auf SUSDB fest.
    ![image7 @ no__t-1
3. Vergewissern Sie sich, dass auf der Seite **Server Rollen** die Option **Public** und **sysadmin** ausgewählt ist.
    ![image8 @ no__t-1
4. Auf der Seite **Benutzer Zuordnung** :
    - Unter **Benutzer, die dieser Anmeldung zugeordnet**sind: Wählen Sie **SUSDB** aus.
    - Unter **database Role Membership für: SUSDB @ no__t-0. Stellen Sie sicher, dass Folgendes aktiviert ist:
        - **public**
        - **WebService** ![image9 @ no__t-2
5. Klicken Sie auf **OK**.

Nun sollte NT- **Autorität \ Netzwerkdienst** unter Anmeldungen angezeigt werden.
![image10 @ no__t-1

#### <a name="database-permissions"></a>Daten Bank Berechtigungen

1. Klicken Sie mit der rechten Maustaste auf die SUSDB.
2. **Eigenschaften** auswählen
3. Klicken Sie auf **Berechtigungen**

Das Konto **NT-Autorität \ Netzwerkdienst** sollte aufgeführt werden.

1. Wenn dies nicht der Fall ist, fügen Sie das Konto hinzu.
2. Geben Sie im Textfeld Anmelde Name den WSUS-Computer im folgenden Format ein:
    > [Vollständig **] \\ [wsuscomputername] $**
3. Vergewissern Sie sich, dass die **Standarddatenbank** auf **SUSDB**festgelegt ist.

    > [!TIP]
    > Im folgenden Beispiel lautet der FQDN " **Contosto.com** ", und der WSUS-Computername lautet " **wsusmachine**":
    >
    > ![image11](images/image11.png)

4. Wählen Sie auf der Seite **Benutzer Zuordnung** unter **"Benutzer, die dieser Anmeldung zugeordnet sind"** die **SUSDB** -Datenbank aus.
5. Überprüfen Sie den **Webdienst** unter dem  **"Mitgliedschaft in Daten Bank Rolle für: SUSDB "** : ![image12 @ no__t-2
6. Klicken Sie auf **OK** , um Einstellungen zu speichern.
    > [!NOTE]
    > Möglicherweise müssen Sie den SQL-Dienst neu starten, damit die Änderungen wirksam werden.

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>Bearbeiten Sie die Registrierung, um WSUS auf die SQL Server Instanz zu verweisen.

> [!IMPORTANT]
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/en-us/help/322756) für den Fall, dass Probleme auftreten.

1. Klicken Sie auf **Start** und **Ausführen**, geben Sie **regedit** ein, und klicken Sie dann auf **OK**.
2. Suchen Sie den folgenden Schlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UpdateServices\Server\Setup\SqlServerName**
3. Geben Sie im Textfeld **Wert** **[Servername] \\ [InstanceName]** ein, und klicken Sie dann auf **OK**. Wenn der Instanzname die Standard Instanz ist, geben Sie **[Servername]** ein.
4. Suchen Sie den folgenden Schlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update services\server\setup\installierte Rolle services\updateservices-widdatabase** ![image13 @ no__t-2
5. Benennen Sie den Schlüssel in **updateservices-Database** ![image41 @ no__t-2 um.

    > [!NOTE]
    > Wenn Sie diesen Schlüssel nicht aktualisieren, versucht **WSUSutil** , die wid anstelle der SQL-Instanz zu bedienen, zu der Sie migriert haben.

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>Starten der IIS-und WSUS-Dienste auf dem WSUS-Server

Führen Sie in PowerShell (mit erhöhten Rechten) Folgendes aus:

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> Wenn Sie die WSUS-Konsole verwenden, schließen Sie Sie, und starten Sie Sie neu.

## <a name="uninstalling-the-wid-role-not-recommended"></a>Deinstallieren der wid-Rolle (nicht empfohlen)

> [!WARNING]
> Durch das Entfernen der wid-Rolle wird auch ein Daten Bank Ordner ( **%systemdrive%\Programme\Update services\database**) entfernt, der Skripts enthält, die von "WSUSutil. exe" für Aufgaben nach der Installation benötigt werden. Wenn Sie die wid-Rolle deinstallieren möchten, stellen Sie sicher, dass Sie den Ordner **%systemdrive%\Programme\Update services\database** vorab sichern.

Mithilfe von PowerShell:

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

Nachdem die wid-Rolle entfernt wurde, überprüfen Sie, ob der folgende Registrierungsschlüssel vorhanden ist: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update services\server\setup\installierte Rolle services\updateservices-Database**