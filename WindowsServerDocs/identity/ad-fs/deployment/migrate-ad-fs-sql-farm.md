---
title: Migrieren einer AD FS 2,0-SQL-Farm mit Verbund Server
description: Enthält Informationen zum Migrieren einer AD FS Server-SQL-Farm mit 2,0 zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.openlocfilehash: f63a797a30d363b8662dfcc6bfcac46f79dc3eb0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87938199"
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
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md) -Verbund Servers [Vorbereiten der Migration des Verbund Server Proxys von AD FS 2,0](prepare-to-migrate-ad-fs-fed-proxy.md) [Migrieren des AD FS 2,0](migrate-the-ad-fs-fed-server.md) Verbund Servers migrieren des [AD FS 2,0](migrate-the-ad-fs-2-fed-server-proxy.md) Verbund Server Proxy [Migrieren der AD FS 1,1-Web-Agents](migrate-the-ad-fs-web-agent.md)
