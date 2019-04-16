---
title: Container-Netzwerke (Übersicht)
description: Dieses Thema bietet eine Übersicht über den Netzwerkstapel für Windows-Container und enthält Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von Container-Netzwerken.
manager: ravirao
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-sdn
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 318659e5-e4a5-4e46-99d6-211dfc46f6b8
ms.author: pashort
author: jmesser81
ms.openlocfilehash: fd2f022948208d4aacce2994ff053e77384b28fc
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="container-networking-overview"></a>Container-Netzwerke (Übersicht)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema bietet eine Übersicht über den Netzwerkstapel für Windows-Container und enthält Links zu weiteren Anleitungen zum Erstellen, konfigurieren und Verwalten von Container-Netzwerken.

Windows Server-Container sind eine einfache Methode zur Betriebssystemvirtualisierung dar verwendet, um Anwendungen oder Dienste von anderen Diensten zu trennen, die auf demselben containerhost ausgeführt werden. Um dies zu ermöglichen, verfügt jeder Container eine eigene Ansicht der das Betriebssystem, Prozesse, Dateisystem, Registrierung und IP-Adressen.

Windows-Containern funktionieren ähnlich wie virtuelle Maschinen in Bezug auf Netzwerke. Jeder Container verfügt über einen virtuellen Netzwerkadapter, der mit einem virtuellen Switch verbunden ist, über den eingehender und ausgehender Datenverkehr weitergeleitet wird. Um die Isolation zwischen Containern auf demselben Host zu erzwingen, ist ein Netzwerkbereich erstellt, für jeden Windows Server- und Hyper-V-Container, in dem der Netzwerkadapter für den Container installiert wird. Windows Server-Container verwenden eine Host-vNIC für die Verbindung mit dem virtuellen Switch. Hyper-V-Container verwenden eine synthetische VM-NIC (nicht verfügbar gemacht, die Utility-VM), um mit dem virtuellen Switch verbinden. 

Containerendpunkte können an einen lokalen Host-Netzwerk (z.B. NAT), dem physischen Netzwerk oder ein Overlay virtuelles Netzwerk erstellt, die durch den Microsoft Software Defined Networking (SDN)-Stapel angefügt werden. 

Weitere Informationen zum Erstellen und Verwalten von Containernetzwerke für die Überlagerung/SDN-Bereitstellungen finden Sie in der [Windows-Container Netzwerke](https://msdn.microsoft.com/en-us/virtualization/windowscontainers/management/container_networking) Handbuch in MSDN.

Weitere Informationen zum Erstellen und Verwalten von Containernetzwerke für die Überlagerung virtuelle Netzwerke mit SDN finden Sie unter [Verbinden von containerendpunkten mit einem virtuellen mandantennetzwerk ](../../manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md). 