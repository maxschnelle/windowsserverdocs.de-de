---
title: Virtual Network Verschlüsselung
description: Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren.
manager: grcusanz
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: anpaul
author: AnirbanPaul
ms.date: 08/08/2018
ms.openlocfilehash: 72062d002e5530031a99e3b742507277ed5ec490
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87990072"
---
# <a name="virtual-network-encryption"></a>Virtual Network Verschlüsselung

>Gilt für: Windows Server

Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren. Sie nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

Die Verschlüsselung virtueller Netzwerke erfordert Folgendes:
- Auf jedem der Sdn-aktivierten Hyper-V-Hosts sind Verschlüsselungs Zertifikate installiert.
- Ein Anmelde Informationen-Objekt im Netzwerk Controller, das auf den Fingerabdruck des Zertifikats verweist.
- Die Konfiguration der einzelnen virtuellen Netzwerke enthält Subnetze, für die eine Verschlüsselung erforderlich ist.

Wenn Sie die Verschlüsselung in einem Subnetz aktivieren, wird der gesamte Netzwerk Datenverkehr in diesem Subnetz zusätzlich zu sämtlichen Verschlüsselung auf Anwendungsebene, die möglicherweise auch stattfindet, automatisch verschlüsselt.  Datenverkehr zwischen Subnetzen, auch wenn Sie als verschlüsselt gekennzeichnet ist, wird automatisch unverschlüsselt gesendet. Sämtlicher Datenverkehr, der die Grenze des virtuellen Netzwerks überschreitet, wird auch unverschlüsselt gesendet.

>[!TIP]
>Wenn Sie Anwendungen darauf beschränken müssen, nur im verschlüsselten Subnetz zu kommunizieren, können Sie Access Control Listen (ACLs) nur verwenden, um die Kommunikation innerhalb des aktuellen Subnetzes zuzulassen. Weitere Informationen finden [Sie unter Verwenden von Access Control Listen (ACLs) zum Verwalten des Netzwerk Datenverkehrs Flusses des Daten](../manage/use-acls-for-traffic-flow.md)Centers.

### <a name="next-steps"></a>Nächste Schritte

[Konfigurieren der Verschlüsselung für ein virtuelles Netzwerk](./sdn-config-vnet-encryption.md)