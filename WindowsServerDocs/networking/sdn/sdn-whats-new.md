---
title: Neuerungen in SDN für WindowsServer
description: Dieses Thema enthält Informationen zu neuen Software Defined Networking-Features für Windows Server 1709
manager: dougkim
ms.prod: windows-server-threshold
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: efad919b-e9e7-4a0c-b373-e68a092f93b5
ms.author: pashort
author: shortpatti
ms.date: 10/02/2018
ms.openlocfilehash: aef2bc32f249550d4e8d33d4b871ca98010e2f49
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446288"
---
# <a name="whats-new-in-sdn-for-windows-server-2019"></a>Neues in SDN für Windows Server 2019

>Gilt für: Windows Server (Semi-Annual Channel)


|                         **Funktion**                          |                                                                                                                                                                                         **Beschreibung**                                                                                                                                                                                         | **Neue oder aktualisierte** |
|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| [Verschlüsselter Netzwerke](vnet-encryption/sdn-vnet-encryption.md) | Verschlüsselung des virtuellen Netzwerks ermöglicht die Verschlüsselung der virtuellen Netzwerkdatenverkehr zwischen virtuellen Computern, die miteinander kommunizieren, in Subnetzen, die als "Verschlüsselung aktiviert." Es nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat. |       Neu       |
|    [Firewall-Überwachung](security/sdn-firewall-auditing.md)    |                                                                                            Für die Überwachung von Firewall ist eine neue Funktion für die SDN-Firewall in Windows Server-2019. Wenn Sie SDN-Firewall aktivieren, ruft beliebigen Flow von SDN-Firewall-Regeln (ACLs), die Protokollierung aktiviert ist verarbeitet aufgezeichnet.                                                                                            |       Neu       |
| [Peering von virtuellen Netzwerken](vnet-peering/sdn-vnet-peering.md)  |                                                                                                                      Peering in virtuellen Netzwerken können Sie die nahtlose Verbindung von zwei virtuellen Netzwerken. Nach für verbindungszwecke, dem Peering werden die virtuellen Netzwerke als eine angezeigt.                                                                                                                      |       Neu       |
|           [Ausgehender Datenverkehr softwaremessung](manage/sdn-egress.md)            |                  Dieses neue Feature in Windows Server-2019 ermöglicht SDN nutzungsverbrauchseinheiten für ausgehende Datenübertragungen zu bieten. Mit diesem Feature hinzugefügt wird berechnet Netzwerkcontroller behält eine Whitelist pro virtuellem Netzwerk, der alle IP-Adressbereiche in SDN verwendet, und erwägen Sie jedes Paket, das für ein Ziel, die nicht in einem dieser Bereiche sein gebunden ausgehende Datenübertragungen an.                   |       Neu       |

---



