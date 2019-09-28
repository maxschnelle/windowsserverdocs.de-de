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
ms.openlocfilehash: 3c43d26868f39896ec8632397dc0fce1dfe2dd2a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408285"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2,0-wid-Farm  
Dieses Dokument enthält ausführliche Informationen zum Migrieren einer AD FS 2,0-SQL-Farm zu Windows Server 2012.


## <a name="migrate-a-sql-server-farm"></a>Migrieren einer SQL Server-Farm  
 Führen Sie das folgende Verfahren aus, um eine SQL Server-Farm zu Windows Server 2012 zu migrieren:  
  
1.  Überprüfen Sie für jeden Server in Ihrer SQL Server Farm die Verfahren unter [Migrieren einer SQL Server Farm](prepare-to-migrate-a-sql-server-farm.md).  
  
2.  Entfernen Sie alle Server in Ihrer SQL Server-Farm aus dem Lastenausgleich.  
  
3.  Führen Sie ein Upgrade des Betriebssystems auf diesem Server in Ihrer SQL Server Farm von Windows Server 2008 R2 oder Windows Server 2008 auf Windows Server 2012 aus. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Aufgrund des Betriebssystem Upgrades geht die AD FS Konfiguration auf diesem Server verloren, und die Server Rolle AD FS 2,0 wird entfernt. Stattdessen wird die Windows Server 2012 AD FS Server-Rolle installiert, aber Sie ist nicht konfiguriert. Sie müssen die ursprüngliche AD FS Konfiguration manuell erstellen und die verbleibenden AD FS Einstellungen wiederherstellen, um die Verbund Servermigration abzuschließen.  
  
4. Erstellen Sie die ursprüngliche AD FS Konfiguration auf diesem Server in Ihrer SQL Server-Farm, indem Sie AD FS Windows PowerShell-Cmdlets verwenden, um einer vorhandenen Farm einen Server hinzuzufügen.  
  
> [!IMPORTANT]
>  Sie müssen Windows PowerShell verwenden, um die ursprüngliche AD FS Konfiguration zu erstellen, wenn Sie SQL Server verwenden, um die AD FS Konfigurations Datenbank zu speichern.  

  - Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl aus: `$fscredential = Get-Credential`.  
  - Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm auf die Migration notiert haben.  
  - Führen Sie den folgenden Befehl aus: `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`, wobei `Data Source` der Wert der Datenquelle im Wert der Verbindungs Zeichenfolge für den Richtlinien Speicher in der folgenden Datei ist: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`.  
  
5. Fügen Sie den Server, den Sie soeben für Windows Server 2012 aktualisiert haben, dem Load Balancer hinzu.  
  
6. Wiederholen Sie die Schritte 2 bis 6 für die verbleibenden Knoten in Ihrer SQL Server Farm.  
  
7. Wenn alle Server in Ihrer SQL Server Farm auf Windows Server 2012 aktualisiert werden, stellen Sie alle verbleibenden AD FS Anpassungen wieder her, z. b. benutzerdefinierte Attribut Speicher.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)



