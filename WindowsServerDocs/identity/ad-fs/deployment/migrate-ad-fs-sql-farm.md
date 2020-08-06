---
title: Migrieren einer AD FS 2,0-SQL-Farm mit Verbund Server
description: Enthält Informationen zum Migrieren einer AD FS Server-SQL-Farm mit 2,0 zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3de9f6f55a93c51c02eadf293b850d40e644586f
ms.sourcegitcommit: de8fea497201d8f3d995e733dfec1d13a16cb8fa
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87864241"
---
# <a name="migrate-an-ad-fs-20-sql-farm"></a>Migrieren einer AD FS 2,0-SQL-Farm  
Dieses Dokument enthält ausführliche Informationen zum Migrieren einer AD FS 2,0-SQL-Farm zu Windows Server 2012.


## <a name="migrate-a-sql-server-farm"></a>Migrieren einer SQL Server-Farm  
 Führen Sie das folgende Verfahren aus, um eine SQL Server-Farm zu Windows Server 2012 zu migrieren:  
  
1.  Überprüfen Sie für jeden Server in Ihrer SQL Server Farm die Verfahren unter [Migrieren einer SQL Server Farm](prepare-to-migrate-a-sql-server-farm.md).  
  
2.  Entfernen Sie alle Server in Ihrer SQL Server-Farm aus dem Lastenausgleich.  
  
3.  Führen Sie ein Upgrade des Betriebssystems auf diesem Server in Ihrer SQL Server Farm von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installieren von Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134246(v=ws.11)).  
  
> [!IMPORTANT]
>  Durch das Upgrade des Betriebssystems geht die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS-Konfiguration manuell erstellen und die verbleibenden AD FS-Einstellungen wiederherstellen, um die Verbundservermigration abzuschließen.  
  
4. Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem Server in der SQL Server-Farm, indem Sie AD FS-Cmdlets von Windows PowerShell verwenden, um einen Server zu einer vorhandenen Farm hinzuzufügen.  
  
> [!IMPORTANT]
>  Sie müssen Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration zu erstellen, wenn Sie Ihre AD FS-Konfigurationsdatenbank mithilfe von SQL Server speichern.  

  - Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: `$fscredential = Get-Credential` .  
  - Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm auf die Migration notiert haben.  
  - Führen Sie den folgenden Befehl `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"` aus:, wobei `Data Source` der Wert der Datenquelle in dem Wert der Verbindungs Zeichenfolge für den Richtlinien Speicher in der folgenden Datei ist: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` .  
  
5. Fügen Sie den Server, den Sie soeben für Windows Server 2012 aktualisiert haben, dem Load Balancer hinzu.  
  
6. Wiederholen Sie die Schritte 2 bis 6 für die restlichen Knoten in Ihrer SQL Server-Farm.  
  
7. Wenn alle Server in Ihrer SQL Server Farm auf Windows Server 2012 aktualisiert werden, stellen Sie alle verbleibenden AD FS Anpassungen wieder her, z. b. benutzerdefinierte Attribut Speicher.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0-Verbund Servers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2,0-Verbund Servers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren des AD FS 2,0-Verbund Server Proxys](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)
