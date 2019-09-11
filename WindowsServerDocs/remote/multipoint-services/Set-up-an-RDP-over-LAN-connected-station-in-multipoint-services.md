---
title: Einrichten einer verbundenen RDP-over-LAN-Station in Multipoint Services
description: Erfahren Sie, wie Sie ein RDP-over-LAN-System in Multipoint Services einrichten.
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
ms.openlocfilehash: 40899b277ae60169a0eca34b359172941e5391fb
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871563"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>Einrichten einer verbundenen RDP-over-LAN-Station in Multipoint Services
Eine RDP-over-LAN-Station ist ein Thin Client, herkömmlicher Desktop oder Laptop Computer, der mithilfe des Remotedesktopprotokoll (RDP) eine Verbindung mit Multipoint Services in einem LAN (Local Area Network) herstellt. Weitere Informationen zu diesem und anderen Stations Typen finden Sie unter [Multipoint-Stationen](MultiPoint-services-Stations.md).  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>So richten Sie eine Multipoint-Station mit einem Computer oder einem Thin Client auf einem LAN ein  
  
1.  Schalten Sie den Computer ein, auf dem Multipoint Services ausgeführt wird.  
  
2.  Stellen Sie sicher, dass der Multipoint-Server Computer von einem Switch, einem Router oder einem anderen Netzwerkgerät mit dem LAN verbunden ist und über eine passende IP-Adresse verfügt. (Eine IP-Adresse, die mit 169,254 beginnt (eine APIPA-Adresse), weist möglicherweise darauf hin, dass ein Problem mit der LAN-Verbindung vorliegt oder der DHCP-Server nicht erreicht werden kann oder nicht ordnungsgemäß funktioniert.)  
  
3.  Verbinden Sie den Client Computer oder den Thin Client mit dem LAN.  
  
4.  Schalten Sie den Client Computer oder den Thin Client ein.  
  
5.  Starten Sie auf dem Client Computer oder Thin Client Remotedesktopverbindung oder eine entsprechende Anwendung, und geben Sie den Namen oder die IP-Adresse des Computers ein, auf dem Multipoint Services ausgeführt wird.

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>Einrichten eines Windows 10-Geräts für die Remote Verwaltung mithilfe von Connector-Diensten
Alle PCs oder Laptops, auf denen Windows 10 ausgeführt wird, können Remote verwaltet werden:
- die Connector-Dienste wurden aktiviert.  
- der Computer wurde den verwalteten Computern auf dem Multipoint-Server hinzugefügt.  

Führen Sie auf dem PC mit Windows 10 die folgenden Schritte aus, um den Multipoint-Connector zu aktivieren:

1. Geben Sie im Suchfeld "Windows-Funktionen ein-oder ausschalten" ein, und wählen Sie das richtige Suchergebnis aus. 

2. Aktivieren Sie in der Liste der Funktionen den **Multipoint-Connector**. Dadurch werden Multipoint-Connector-Dienste aktiviert, die für die Verwaltung des Geräts erforderlich sind. 

Auf dem Multipoint-Server:
1. Öffnen Sie Multipoint-Manager, und wählen Sie entweder **persönliche Computer hinzufügen oder entfernen** oder **Multipoint Services hinzufügen oder entfernen**aus.

2. Wählen Sie die Remote Computer aus, die Sie verwalten möchten, und klicken Sie auf **OK**.  Sie werden auf den Remote Computern zur Eingabe von Administrator Anmelde Informationen aufgefordert.  Nachdem dies geschehen ist, werden die Remote Computer auf der Registerkarte "Start" von Multipoint Manager angezeigt.

Wenn der Dashboard-Manager erfolgreich eingerichtet wurde, kann er Benutzer überwachen, die auf dem verwalteten Gerät arbeiten.

> [!IMPORTANT]  
> Beim Überwachen verwalteter Windows 10-Geräte administratrive können Benutzer nur dann überwacht werden, wenn die Servereinstellungen entsprechend geändert wurden. Siehe [Bearbeiten von Server Einstellungen](Edit-Server-Settings.md)