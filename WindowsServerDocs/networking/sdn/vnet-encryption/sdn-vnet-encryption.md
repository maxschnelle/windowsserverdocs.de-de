---
title: Virtuelles Netzwerk-Verschlüsselung
description: Dieses Thema enthält Informationen zur virtuellen Netzwerk-Verschlüsselung für die Software Defined Networking in Windows Server
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: grcusanz
ms.openlocfilehash: 425cc1cff8c7241aeec7764b60c89b4586fd323b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="virtual-network-encryption"></a>Virtuelles Netzwerk-Verschlüsselung

>Gilt für: Windows Server

Virtuelle Netzwerk-Verschlüsselung bietet die Möglichkeit für den virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern verschlüsselt werden, die innerhalb der Subnetze miteinander kommunizieren können, die als "Verschlüsselung aktiviert" gekennzeichnet sind.

Dieses Feature nutzt Datagram Transport Layer Security (DTLS) auf das virtuelle Subnetz aus, um die Pakete zu verschlüsseln.  DTLS bietet Schutz vor Lauschangriffe, Manipulationen und Fälschung von jedem Benutzer mit Zugriff auf das physische Netzwerk.

Virtuelle Netzwerk Verschlüsselung benötigt ein Verschlüsselungszertifikat auf jedem der SDN installiert werden aktiviert Hyper-V-Hosts ein Anmeldeinformationsobjekt in den Netzwerkcontroller einen Verweis auf den Fingerabdruck dieses Zertifikats und -Konfiguration auf den einzelnen virtuellen Netzwerken Anfordern der Verschlüsselung Subnetze enthalten.

Sobald die Verschlüsselung in einem Subnetz aktiviert ist, werden alle Netzwerkdatenverkehr innerhalb eines Subnetzes automatisch verschlüsselt.  Dies wird zusätzlich zu allen Verschlüsselung auf Anwendungsebene sein, die auch stattfinden kann.  Schneidet zwischen Subnetzen, selbst wenn beide Subnetze gekennzeichnet sind verschlüsselter Datenverkehr wird automatisch unverschlüsselt gesendet.  Datenverkehr, der die virtuellen Netzwerk-Grenze überschreitet, wird auch unverschlüsselt gesendet.

Informationen zum Konfigurieren von virtuellen Netzwerk-Verschlüsselung finden Sie unter [Verschlüsselung konfigurieren, damit ein virtuelles Netzwerk](sdn-config-vnet-encryption.md).

Wenn Sie Anwendungen nur im Subnetz verschlüsselte Kommunikation einschränken müssen.  Zugriffssteuerungslisten (ACLs) können Sie nur die Kommunikation innerhalb des aktuellen Subnetzes zulassen.  

Weitere Informationen zum Konfigurieren der Access Control Lists, finden Sie unter [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Netzwerkdatenverkehrsflusses](../manage/use-acls-for-traffic-flow.md).