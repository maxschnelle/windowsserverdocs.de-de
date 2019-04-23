---
title: Migration der WSUS-Datenbank (interne Windows-Datenbank) WID mit SQL
description: Windows Server Update Service (WSUS)-Thema – wie Sie die WSUS-Datenbank (SUSDB) mit einer lokalen oder Remote-Instanz von SQL Server von einer internen Windows-Datenbank-Instanz zu migrieren.
ms.prod: windows-server-threshold
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
ms.openlocfilehash: ed6f695947fc17d2e96b5282b3a67a221bb0140d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858031"
---
>Gilt für: Windows Server 2012, Windows Server 2012 R2, Windows Server 2016

# <a name="migrating-the-wsus-database-from-wid-to-sql"></a>Migrieren Sie die WSUS-Datenbank aus der internen Windows-Datenbank zu SQL

Verwenden Sie die folgenden Schritte aus die WSUS-Datenbank (SUSDB) zu migrieren von einer internen Windows-Datenbank-Instanz mit einer lokalen oder Remote-Instanz von SQL Server.

## <a name="prerequisites"></a>Vorraussetzungen

- SQL-Instanz. Dies kann die Standardeinstellung sein **MSSQLServer** oder eine benutzerdefinierte Instanz.
- SQL Server Management Studio
- WSUS mit WID-Rolle installiert sein
- IIS (Dies ist normalerweise enthalten beim Installieren von WSUS über Server-Manager). Es ist noch nicht installiert, werden muss.

## <a name="migrating-the-wsus-database"></a>Migration der WSUS-Datenbank

### <a name="stop-the-iis-and-wsus-services-on-the-wsus-server"></a>Beenden Sie die IIS und WSUS-Dienste auf dem WSUS-server

Führen Sie in PowerShell (mit erhöhten Rechten):

```powershell
    Stop-Service IISADMIN
    Stop-Service WsusService
```

### <a name="detach-susdb-from-the-windows-internal-database"></a>Trennen Sie die SUSDB aus der internen Windows-Datenbank

#### <a name="using-sql-management-studio"></a>Mithilfe von SQL Management Studio

1. Mit der rechten Maustaste **SUSDB** - &gt; **Aufgaben** - &gt; klicken Sie auf **trennen**: ![image1](images/image1.png)
2. Überprüfen Sie **vorhandene Verbindungen löschen** , und klicken Sie auf **OK** (optional, wenn aktive Verbindungen existieren).
    ![image2](images/image2.png)

#### <a name="using-command-prompt"></a>Verwenden der Eingabeaufforderung

> [!IMPORTANT]
> Diese Schritte zeigen, wie Sie die WSUS-Datenbank (SUSDB) zu trennen von der internen Windows-Datenbank-Instanz mithilfe der **Sqlcmd** Hilfsprogramm. Weitere Informationen zu den **Sqlcmd** Hilfsprogramm finden Sie unter [Hilfsprogramms "Sqlcmd"](https://go.microsoft.com/fwlink/?LinkId=81183).
1. Öffnen Sie eine Eingabeaufforderung mit erhöhten rechten
2. Führen den folgenden SQL-Befehl zum Trennen der WSUS-Datenbank (SUSDB) aus der internen Windows-Datenbank-Instanz, indem die **Sqlcmd** Hilfsprogramm:

```batchfile
        sqlcmd -S \\.\pipe\Microsoft##WID\tsql\query
        use master
        GO
        alter database SUSDB set single_user with rollback immediate
        GO
        sp_detach_db SUSDB
        GO
```

### <a name="copy-the-susdb-files-to-the-sql-server"></a>Kopieren Sie die SUSDB-Dateien mit der SQL Server

1. Kopie **"susdb.mdf"** und **SUSDB\_log.ldf** aus dem Ordner WID-Daten (**%SystemDrive%**\** Windows\WID\Data **) auf die Daten der SQL-Instanz Ordner.

> [!TIP]
> Wenn der SQL-Instanz-Ordner ist z. B. **c:\Programme\Microsoft c:\Programme\Microsoft SQL Server\MSSQL12. MSSQLSERVER\MSSQL**, und die WID-Datenordner **C:\Windows\WID\Data,** kopieren Sie die SUSDB-Dateien aus **C:\Windows\WID\Data** zu **c:\Programme\Microsoft SQL Server \MSSQL12. MSSQLSERVER\MSSQL\Data**

### <a name="attach-susdb-to-the-sql-instance"></a>Fügen Sie die SUSDB an die SQL-Instanz

1. In **SQL Server Management Studio**unter der **Instanz** Knoten mit der rechten Maustaste **Datenbanken**, und klicken Sie dann auf **Anfügen**.
    ![image3](images/image3.png)
2. In der **Datenbanken anfügen** Feld unter **anzufügende Datenbanken**, klicken Sie auf die **hinzufügen** zu suchen, die **"susdb.mdf"** Datei (kopiert aus der WID-Ordner), und klicken Sie dann auf **OK**.
    ![image4](images/image4.png) ![image5](images/image5.png)

> [!TIP]
> Dies kann auch erfolgen mithilfe von Transact-Sql.  Informieren Sie sich die [SQL-Dokumentation zum Anfügen einer Datenbank](https://docs.microsoft.com/sql/relational-databases/databases/attach-a-database) für dessen Anweisungen.
>
> Beispiel (mit Pfade aus dem vorherigen Beispiel):
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

### <a name="verify-sql-server-and-database-logins-and-permissions"></a>Überprüfen Sie, ob SQLServer und Datenbank-Anmeldenamen und Berechtigungen

#### <a name="sql-server-login-permissions"></a>SQL Server-Login-Berechtigungen

Stellen Sie sicher, die nach dem Anfügen der SUSDB **NT AUTHORITY\NETWORK SERVICE** hat Login-Berechtigungen verfügen, mit der Instanz von SQL Server wie folgt:

1. Wechseln Sie in SQL Server Management Studio
2. Öffnen die Instanz
3. Klicken Sie auf **Sicherheit**
4. Klicken Sie auf **Anmeldungen**

Die **NT AUTHORITY\NETWORK SERVICE** Konto sollte aufgeführt sein. Wenn sie nicht der Fall ist, müssen Sie sie durch das Hinzufügen von neuen Anmeldenamen hinzuzufügen.

> [!IMPORTANT]
> Wenn die SQL-Instanz auf einem anderen Computer aus WSUS ist, sollte der WSUS-Server-Computerkonto im Format aufgelistet werden **[FQDN]\\[WSUSComputerName] $**.  Wenn nicht, die folgenden Schritte verwendet werden können, um sie hinzuzufügen, und Ersetzen Sie dabei **NT AUTHORITY\NETWORK SERVICE** mit dem WSUS-Server-Computerkonto (**[FQDN]\\[WSUSComputerName] $**) wäre dies ***zusätzlich zu*** Rechte für **NT AUTHORITY\NETWORK SERVICE**

##### <a name="adding-nt-authoritynetwork-service-and-granting-it-rights"></a>Hinzufügen von NT AUTHORITY\NETWORK SERVICE, und erteilen der Rechte

1. Mit der rechten Maustaste **Anmeldungen** , und klicken Sie auf **neue Anmeldung...**
    ![image6](images/image6.png)
2. Auf der **allgemeine** Seite, füllen Sie die **Anmeldename** (**NT AUTHORITY\NETWORK SERVICE**), und legen Sie die **Standarddatenbank** zu SUSDB.
    ![image7](images/image7.png)
3. Auf der **Serverrollen** Seite **öffentliche** und **Sysadmin** ausgewählt sind.
    ![image8](images/image8.png)
4. Auf der **Benutzerzuordnung** Seite:
    - Klicken Sie unter **Benutzer zugeordnet, die dieser Anmeldung**: Wählen Sie **SUSDB**
    - Klicken Sie unter **Mitgliedschaft in Datenbankrolle für: SUSDB**, stellen Sie sicher, Folgendes überprüft:
        - **public**
        - **WebService** ![image9](images/image9.png)
5. Klicken Sie auf **OK**.

Sie sollten jetzt sehen **NT AUTHORITY\NETWORK SERVICE** unter den Anmeldenamen.
![image10](images/image10.png)

#### <a name="database-permissions"></a>Datenbankberechtigungen

1. Mit der rechten Maustaste der SUSDB
2. Wählen Sie **Eigenschaften**
3. Klicken Sie auf **Berechtigungen**

Die **NT AUTHORITY\NETWORK SERVICE** Konto sollte aufgeführt sein.

1. Wenn sie nicht der Fall ist, fügen Sie das Konto ein.
2. Geben Sie auf das Textfeld Benutzername den WSUS-Computer in folgendem Format ein:
    > [**FQDN]\\[WSUSComputerName]$**
3. Überprüfen Sie, ob die **Standarddatenbank** nastaven NA hodnotu **SUSDB**.

    > [!TIP]
    > Im folgenden Beispiel wird der FQDN **Contosto.com** und ist der Name des WSUS-Computers **WsusMachine**:
    >
    > ![Image11](images/image11.png)

4. Auf der **Benutzerzuordnung** Seite die **SUSDB** -Datenbank unter **"Von Benutzer, die dieser Anmeldung zugeordnet"**
5. Überprüfen Sie **Webservice** unter der **"Mitgliedschaft in Datenbankrolle für: SUSDB"**: ![image12](images/image12.png)
6. Klicken Sie auf **OK** um Einstellungen zu speichern.
    > [!NOTE]
    > Sie müssen den SQL-Dienst für die Änderungen wirksam werden neu.

### <a name="edit-the-registry-to-point-wsus-to-the-sql-server-instance"></a>Bearbeiten Sie die Registrierung Punkt WSUS für die SQL Server-Instanz

> [!IMPORTANT]
> Die Schritte in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie Änderungen vornehmen, müssen [sichern Sie die Registrierung für die Wiederherstellung](https://support.microsoft.com/en-us/help/322756) für den Fall, dass Probleme auftreten.

1. Klicken Sie auf **Start** und **Ausführen**, geben Sie **regedit** ein, und klicken Sie dann auf **OK**.
2. Suchen Sie nach den folgenden Schlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\UpdateServices\Server\Setup\SqlServerName**
3. In der **Wert** Textfeld **[ServerName]\\[Instanzname]**, und klicken Sie dann auf **OK**. Wenn Sie den Namen der Instanz die Standardinstanz ist, geben Sie **[ServerName]**.
4. Suchen Sie nach den folgenden Schlüssel: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed Rolle Services\UpdateServices-WidDatabase** ![image13](images/image13.png)
5. Benennen Sie die Taste, um **UpdateServices-Database** ![image41](images/image14.png)

    > [!NOTE]
    > Wenn Sie nicht diesen Schlüssel, klicken Sie dann aktualisieren **Tools "WSUSUTIL"** wird versucht, die SQL-Instanz, die auf die Sie migriert haben, anstatt die WID-service.

### <a name="start-the-iis-and-wsus-services-on-the-wsus-server"></a>Starten Sie die IIS und WSUS-Dienste auf dem WSUS-server

Führen Sie in PowerShell (mit erhöhten Rechten):

```powershell
    Start-Service IISADMIN
    Start-Service WsusService
```

> [!NOTE]
> Wenn Sie die WSUS-Konsole verwenden, schließen, und starten Sie ihn neu.

## <a name="uninstalling-the-wid-role-not-recommended"></a>Deinstallieren die WID-Rolle (nicht empfohlen)

> [!WARNING]
> Entfernen der Rolle WID auch einen Datenbankordner entfernt (**%SystemDrive%\Programme\Microsoft c:\Programme\Update Services\Database**), der WSUSUtil.exe für Aufgaben nach der Installation erforderlichen Skripts enthält. Wenn Sie zum Deinstallieren der Rolle WID, achten Sie darauf Sie sichern die **%SystemDrive%\Programme\Microsoft c:\Programme\Update Services\Database** Ordner im voraus.

Mithilfe von PowerShell:

```powershell
Uninstall-WindowsFeature -Name 'Windows-Internal-Database'
```

Nachdem die WID-Rolle entfernt wurde, stellen Sie sicher, dass der folgende Registrierungsschlüssel vorhanden ist: **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Update Services\Server\Setup\Installed Rolle Services\UpdateServices-Datenbank**