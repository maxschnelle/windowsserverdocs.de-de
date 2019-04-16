---
title: Konfigurieren Sie die Reihenfolge von Netzwerkschnittstellen
description: Dieses Thema ist Teil der Netzwerk-Subsystem-Leistungsoptimierung Anleitung für Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 3266328c-ca82-40d2-90ca-854b7088ccaa
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2edf9d312e50a0fd8485e0032dee8413675367cf
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-the-order-of-network-interfaces"></a>Konfigurieren Sie die Reihenfolge von Netzwerkschnittstellen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In Windows Server 2016 und Windows 10 können Sie die Schnittstellenmetrik so konfigurieren Sie die Reihenfolge von Netzwerkschnittstellen.

Dies ist anders als in früheren Versionen von Windows und Windows Server, der Sie die Bindungsreihenfolge der Netzwerkkarten zu konfigurieren, über die Benutzeroberfläche oder die Befehle zulässig **INetCfgComponentBindings** und **INetCfgComponentBindings::MoveAfter**. Diese beiden Methoden für die Anordnung von Netzwerkschnittstellen sind nicht in Windows Server 2016 und Windows 10 verfügbar.

Stattdessen können Sie die neue Methode zum Festlegen der aufgelisteten Reihenfolge der Netzwerkadapter durch Konfigurieren der Schnittstellenmetrik der einzelnen Adapter. Sie können die Schnittstellenmetrik konfigurieren, mit der [Set-NetIPInterface](https://docs.microsoft.com/en-us/powershell/module/nettcpip/set-netipinterface) Windows PowerShell-Befehl.

Wenn Netzwerk-Datenverkehr Routen werden ausgewählt und konfiguriert die **"InterfaceMetric"** -Parameter von der **Set-NetIPInterface** Befehl, der allgemeine Metrik, die verwendet wird, um die Voreinstellungen für die Benutzeroberfläche zu ermitteln ist die Summe der die Routemetrik und der Schnittstellenmetrik. In der Regel bevorzugt Schnittstellenmetrik einer bestimmten Schnittstelle an, z. B. mit kabelgebundenen, wenn sowohl kabelgebundene und drahtlose verfügbar sind.

Beispiel für den folgende Windows PowerShell-Befehl zeigt die Verwendung dieses Parameters.

    Set-NetIPInterface -InterfaceIndex 12 -InterfaceMetric 15

Die Reihenfolge der Adapter in einer Liste wird durch die IPv4- oder IPv6-Schnittstellenmetrik bestimmt.  Weitere Informationen finden Sie unter [GetAdaptersAddresses Funktion](https://msdn.microsoft.com/library/windows/desktop/aa365915%28v=vs.85%29.aspx?f=255&MSPPError=-2147217396).

Links zu allen Themen in diesem Handbuch finden Sie [Optimieren der Leistung mit Subsystem](net-sub-performance-top.md).
