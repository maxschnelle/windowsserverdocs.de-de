---
title: Verschlüsselung des virtuellen Netzwerks
description: Verschlüsselung des virtuellen Netzwerks ermöglicht die Verschlüsselung der virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern, die miteinander kommunizieren, in Subnetzen, die als "Verschlüsselung aktiviert."
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: pashort
author: shortpatti
ms.date: 08/08/2018
ms.openlocfilehash: f2f50ae3146854e2ef6081b0c400a474b53dcf66
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851081"
---
# <a name="virtual-network-encryption"></a>Verschlüsselung des virtuellen Netzwerks

>Gilt für: Windows Server

Verschlüsselung des virtuellen Netzwerks ermöglicht die Verschlüsselung der virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern, die miteinander kommunizieren, in Subnetzen, die als "Verschlüsselung aktiviert." Es nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

Verschlüsselung für virtuelle Netzwerke sind erforderlich:
- Verschlüsselungszertifikate, die auf jedem der SDN-fähige Hyper-V-Hosts installiert werden.
- Ein Objekt mit Anmeldeinformationen in den Netzwerkcontroller verweisen auf den Fingerabdruck des Zertifikats.
- Konfiguration auf alle virtuellen Netzwerke enthalten, Subnetze, die Verschlüsselung erforderlich ist.

Nach Aktivieren der Verschlüsselung in einem Subnetz wird neben jeder Verschlüsselung auf Anwendungsebene, die auch ausgeführt werden kann, automatisch alle Netzwerkdatenverkehr innerhalb dieses Subnetzes verschlüsselt.  Datenverkehr, der zwischen Subnetzen, überschreitet, auch wenn markiert als verschlüsselte, wird automatisch unverschlüsselt gesendet. Jeglicher Datenverkehr, der die Begrenzung des virtuellen Netzwerks überschreitet, ruft auch unverschlüsselt gesendet.

>[!TIP]
>Wenn Sie nur im Subnetz verschlüsselte Kommunikation zwischen Anwendungen einschränken müssen, können Sie die Zugriffssteuerungslisten (ACLs) verwenden, nur um die Kommunikation im aktuellen Subnetz zuzulassen. Weitere Informationen finden Sie unter [verwenden Zugriffssteuerungslisten (ACLs) zum Verwalten von Datencenter-Netzwerk fließt der Datenverkehr](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow).

### <a name="next-steps"></a>Nächste Schritte

[Konfigurieren der Verschlüsselung für ein virtuelles Netzwerk](https://docs.microsoft.com/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption)

