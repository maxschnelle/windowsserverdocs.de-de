---
title: Migrieren einer AD FS 2.0-Verbundserver-SQL-Serverfarm
description: "Enthält Informationen zur Migration einer SQL-Farm in AD FS 2.0-Server zu Windows Server 2012"
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 8433219850793aa34b646a3bf14cba42d3de4988
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2.0 WID-farm  
Dieses Dokument enthält ausführliche Informationen zur Migration einer AD FS 2.0-SQL-Farm zu Windows Server 2012.


## <a name="migrate-a-sql-server-farm"></a>Migrieren einer SQL Server-farm  
 Um eine SQL Server-Farm zu Windows Server 2012 migrieren, führen Sie die folgenden Schritte aus:  
  
1.  Für jeden Server in der SQL Server-Farm, überprüfen Sie, und führen Sie die Verfahren in [migrieren eine SQL Server-Farm](prepare-to-migrate-a-sql-server-farm.md).  
  
2.  Entfernen Sie alle Server in der SQL Server-Farm aus dem Lastenausgleich.  
  
3.  Aktualisieren Sie das Betriebssystem auf diesem Server in der SQL Server-Farm von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis einer Aktualisierung des Betriebssystems der AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber es ist nicht konfiguriert. Sie müssen manuell erstellen die ursprüngliche AD FS-Konfiguration und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
4.  Die ursprüngliche AD FS-Konfiguration auf diesem Server in der SQL Server-Farm mit AD FS Windows PowerShell-Cmdlets zum Hinzufügen eines Servers zu einer vorhandenen Farm zu erstellen.  
  
> [!IMPORTANT]
>  Sie müssen Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration zu erstellen, wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank verwenden.  

  - Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl: `$fscredential = Get-Credential`.  
  - Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm für die Migration notiert haben.  
  - Führen Sie den folgenden Befehl: `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`, wobei `Data Source` den Datenquellenwert im Richtlinie Store den Wert Verbindungszeichenfolge in der folgenden Datei: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`.  
  
5.  Fügen Sie den Server, den Sie gerade auf Windows Server 2012 auf das Lastenausgleichsmodul aktualisiert.  
  
6.  Wiederholen Sie die Schritte 2 bis 6 für die verbleibenden Knoten in der SQL Server-Farm.  
  
7.  Wenn alle Server in der SQL Server-Farm auf Windows Server 2012 aktualisiert werden, stellen Sie alle verbleibenden AD FS-Anpassungen, z. B. benutzerdefinierte Attributspeicher wieder her.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration der AD FS 2.0-Verbundserver-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)



