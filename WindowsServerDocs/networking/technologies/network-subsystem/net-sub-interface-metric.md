---
title: Konfigurieren der Reihenfolge von Netzwerkschnittstellen
description: Dieses Thema ist Teil des Leitfadens Netzwerk-Subsystem zur Leistungsoptimierung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 18bc9a268b4e69e4b87b6b1e310f1162473adb10
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821771"
---
# <a name="configure-the-order-of-network-interfaces"></a>Konfigurieren der Reihenfolge von Netzwerkschnittstellen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die Schnittstellenmetrik können Sie in Windows Server 2016 und Windows 10 um die Reihenfolge der Netzwerkschnittstellen zu konfigurieren.

Dies ist anders als in früheren Versionen von Windows und Windows Server, der Sie die Bindungsreihenfolge der Netzwerkkarten zu konfigurieren, mit der Benutzeroberfläche oder die Befehle zulässig **INetCfgComponentBindings**und **INetCfgComponentBindings::MoveAfter**. Diese beiden Methoden für die Sortierung der Netzwerkschnittstellen sind nicht in Windows Server 2016 und Windows 10 verfügbar.

Stattdessen können Sie die neue Methode zum Festlegen der aufgelisteten Reihenfolge von Netzwerkadaptern Schnittstellenmetrik der einzelnen Adapter konfigurieren. Sie können die Schnittstellenmetrik konfigurieren, mit der [Set-NetIPInterface](https://docs.microsoft.com/powershell/module/nettcpip/set-netipinterface) Windows PowerShell-Befehl.

Wenn Datenverkehr Netzwerkrouten werden ausgewählt und konfiguriert haben die **"InterfaceMetric"** Parameter der **Set-NetIPInterface** Befehl, der die gesamte Metrik, die verwendet wird, um zu bestimmen, die Schnittstelle Einstellung ist die Summe der Routemetrik und der Schnittstelle. In der Regel bevorzugt Schnittstellenmetrik einer bestimmten Schnittstelle an, wie die Verwendung von verbunden werden, wenn beide kabelgebundenen und drahtlosen sind verfügbar.

Das folgende Windows PowerShell-Befehlsbeispiel zeigt die Verwendung dieses Parameters.

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

Die Reihenfolge, in der Adapter in einer Liste angezeigt werden, wird durch die IPv4- oder IPv6-Schnittstellenmetrik bestimmt.  Weitere Informationen finden Sie unter [GetAdaptersAddresses Funktion](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).
