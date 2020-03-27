---
title: Virtual Network Verschlüsselung
description: Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: 7da0f509-7b02-4a0f-90fb-d97c83a2bc4e
ms.author: lizross
author: eross-msft
ms.date: 08/08/2018
ms.openlocfilehash: 8e12e5ff8a1ce8403e9d13d215f26f46352b17d1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309757"
---
# <a name="virtual-network-encryption"></a>Virtual Network Verschlüsselung

>Gilt für: Windows Server

Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren. Es nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat.

Die Verschlüsselung virtueller Netzwerke erfordert Folgendes:
- Auf jedem der Sdn-aktivierten Hyper-V-Hosts sind Verschlüsselungs Zertifikate installiert.
- Ein Anmelde Informationen-Objekt im Netzwerk Controller, das auf den Fingerabdruck des Zertifikats verweist.
- Die Konfiguration der einzelnen virtuellen Netzwerke enthält Subnetze, für die eine Verschlüsselung erforderlich ist.

Wenn Sie die Verschlüsselung in einem Subnetz aktivieren, wird der gesamte Netzwerk Datenverkehr in diesem Subnetz zusätzlich zu sämtlichen Verschlüsselung auf Anwendungsebene, die möglicherweise auch stattfindet, automatisch verschlüsselt.  Datenverkehr zwischen Subnetzen, auch wenn Sie als verschlüsselt gekennzeichnet ist, wird automatisch unverschlüsselt gesendet. Sämtlicher Datenverkehr, der die Grenze des virtuellen Netzwerks überschreitet, wird auch unverschlüsselt gesendet.

>[!TIP]
>Wenn Sie Anwendungen darauf beschränken müssen, nur im verschlüsselten Subnetz zu kommunizieren, können Sie Access Control Listen (ACLs) nur verwenden, um die Kommunikation innerhalb des aktuellen Subnetzes zuzulassen. Weitere Informationen finden [Sie unter Verwenden von Access Control Listen (ACLs) zum Verwalten des Netzwerk Datenverkehrs Flusses des Daten](https://docs.microsoft.com/windows-server/networking/sdn/manage/use-acls-for-traffic-flow)Centers.

### <a name="next-steps"></a>Nächste Schritte

[Konfigurieren der Verschlüsselung für ein virtuelles Netzwerk](https://docs.microsoft.com/windows-server/networking/sdn/vnet-encryption/sdn-config-vnet-encryption)

