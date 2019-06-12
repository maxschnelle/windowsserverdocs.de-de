---
title: Migrieren Sie eine AD FS 2.0-Verbundserver-SQL-Serverfarm
description: Enthält Informationen zum Migrieren einer SQL-Farm in AD FS 2.0-Server auf Windows Server 2012
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: afecbf80d78688b66b2392647ea3195be95e9f54
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445616"
---
# <a name="migrate-an-ad-fs-20-wid-farm"></a>Migrieren einer AD FS 2.0-WID-farm  
Dieses Dokument enthält ausführliche Informationen zur Migration von einer AD FS 2.0-SQL-Farm zu Windows Server 2012.


## <a name="migrate-a-sql-server-farm"></a>Migrieren einer SQL Server-Farm  
 Um eine SQL Server-Farm zu Windows Server 2012 zu migrieren, führen Sie die folgenden Schritte aus:  
  
1.  Klicken Sie für jeden Server in der SQL Server-Farm, überprüfen Sie, und führen Sie die Verfahren in [migrieren eine SQL Server-Farm](prepare-to-migrate-a-sql-server-farm.md).  
  
2.  Entfernen Sie alle Server in Ihrer SQL Server-Farm aus dem Lastenausgleich.  
  
3.  Aktualisieren Sie das Betriebssystem auf diesem Server in der SQL Server-Farm von Windows Server 2008 R2 oder Windows Server 2008 zu Windows Server 2012. Weitere Informationen finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx).  
  
> [!IMPORTANT]
>  Als Ergebnis der Aktualisierung des Betriebssystems die AD FS-Konfiguration auf diesem Server verloren und die AD FS 2.0-Serverrolle wird entfernt. Wird stattdessen die Windows Server 2012 AD FS-Serverrolle installiert, aber nicht konfiguriert ist. Sie müssen manuell die ursprüngliche AD FS-Konfiguration erstellen und Wiederherstellen der verbleibenden AD FS-Einstellungen, um die verbundservermigration abzuschließen.  
  
4. Erstellen Sie die ursprüngliche AD FS-Konfiguration auf diesem Server in der SQL Server-Farm mit AD FS Windows PowerShell-Cmdlets, zu einer vorhandenen Farm einen Server hinzuzufügen.  
  
> [!IMPORTANT]
>  Sie müssen Windows PowerShell verwenden, um die ursprüngliche AD FS-Konfiguration zu erstellen, wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank verwenden.  

  - Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl: `$fscredential = Get-Credential`.  
  - Geben Sie den Namen und das Kennwort des Dienstkontos ein, die Sie beim Vorbereiten der SQL Server-Farm auf die Migration notiert haben.  
  - Führen Sie den folgenden Befehl: `Add-AdfsFarmNode -ServiceAccountCredential $fscredential -SQLConnectionString "Data Source=<Data Source>;Integrated Security=True"`, wobei `Data Source` der Datenquellenwert in der Richtlinie für Store-Verbindungszeichenfolgenwert in der folgenden Datei: `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config`.  
  
5. Fügen Sie den Server, den Sie für den Load Balancer nur auf Windows Server 2012 aktualisiert.  
  
6. Wiederholen Sie die Schritte 2 bis 6 für die übrigen Knoten in der SQL Server-Farm.  
  
7. Wenn alle Server in der SQL Server-Farm auf Windows Server 2012 aktualisiert werden, stellen Sie alle verbleibenden AD FS-Anpassungen, z. B. benutzerdefinierte Attributspeicher wieder her.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2.0-Verbundservers](prepare-to-migrate-ad-fs-fed-server.md)   
 [Vorbereiten der Migration von AD FS 2.0-Verbundserver-Server-Proxy](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren des AD FS 2.0-Verbundservers](migrate-the-ad-fs-fed-server.md)   
 [Migrieren der AD FS 2.0-Verbundserver-Server-Proxy](migrate-the-ad-fs-2-fed-server-proxy.md)   
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)



