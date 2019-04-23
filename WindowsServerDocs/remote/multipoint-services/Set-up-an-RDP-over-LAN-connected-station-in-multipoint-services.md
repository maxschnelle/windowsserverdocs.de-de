---
title: Einrichten einer Station RDP-Over-LAN-Verbindung in MultiPoint Services
description: Erfahren Sie, wie Sie eine RDP-Over-LAN-System in MultiPoint Services einrichten
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60e1a025-c2fb-4708-a3ff-c44c223a3224
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: 8d2f1644918f1a581c1bcab181cd084e12c6b576
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59843701"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>Einrichten einer Station RDP-Over-LAN-Verbindung in MultiPoint Services
Eine Station RDP-Over-LAN verbunden ist, eine thin Client, Sie traditionelle Desktop- oder Laptopcomputer, die in einem lokalen Netzwerk (LAN) mit MultiPoint Services verbindet, mit der Remote Desktop Protocol (RDP). Weitere Informationen zu diesen und anderen Station-Typen finden Sie unter [MultiPoint-Stationen](MultiPoint-services-Stations.md).  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>Zum Einrichten einer MultiPoint-Station mit einem Computer oder einen thin-Client in einem LAN  
  
1.  Aktivieren Sie auf dem Computer, auf dem MultiPoint Services ausgeführt wird.  
  
2.  Stellen Sie sicher, dass der MultiPoint Server-Computer mit dem LAN, die von einem Switch, Router oder anderen Netzwerkgerät verbunden ist und eine korrekte IP-Adresse. (Eine IP-Adresse, die mit 169.254. (eine APIPA-Adresse) beginnt möglicherweise angeben, gibt es ein Problem mit der LAN-Verbindung oder dass der DHCP-Server nicht erreichbar oder nicht ordnungsgemäß funktioniert.)  
  
3.  Verbinden Sie den Clientcomputer oder einen thin-Client mit dem LAN.  
  
4.  Aktivieren Sie auf dem Clientcomputer oder einen thin-Client.  
  
5.  Klicken Sie auf dem Clientcomputer oder ein thin-Client starten Sie Remotedesktopverbindung oder einer ähnlichen Anwendung, und geben Sie den Namen oder die IP-Adresse des Computers, auf dem MultiPoint Services ausgeführt wird.

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>Einrichten von Windows 10-Gerät für die Remoteverwaltung mithilfe von Connectordienste
Jedem PC oder Laptop unter Windows 10 kann remote verwaltet werden, solange:
- die Connectordienste wurden aktiviert  
- der Computer wurde auf verwalteten Computern, auf dem MultiPoint-Server hinzugefügt.  

Folgendermaßen Sie auf dem PC mit Windows 10 vor, um MultiPoint-Connector zu aktivieren:

1. Klicken Sie in das Suchfeld Geben Sie "Turn Windows features ein- oder ausschalten", und wählen Sie die richtige Suchergebnis. 

2. In der Liste der Funktionen ermöglichen **MultiPoint-Connector**. Dadurch können MultiPoint-Connector-Diensten, die zum Verwalten des Geräts erforderlich sind. 

Auf dem MultiPoint-Server:
1. Öffnen Sie MultiPoint-Manager, und wählen Sie entweder **hinzufügen oder Entfernen von PCs** oder **hinzufügen und Entfernen von MultiPoint Services**.

2. Wählen Sie die Sie verwalten möchten und klicken Sie auf Remotecomputern **OK**.  Sie werden aufgefordert, Administratoranmeldeinformationen auf den Remotecomputern.  Sobald dies geschehen ist, sehen Sie die Remotecomputern auf der Registerkarte "home MultiPoint-Manager".

Wenn erfolgreich Satz von Dashboard-Manager Benutzer arbeiten, auf dem verwalteten Gerät überwachen kann.

> [!IMPORTANT]  
> Beim Überwachen von verwalteten können nicht Administratrive Benutzer von Windows 10-Geräte mit Ausnahme der Server überwacht werden, die Einstellungen entsprechend geändert wurden. Finden Sie unter [Bearbeiten von servereinstellungen](Edit-Server-Settings.md)