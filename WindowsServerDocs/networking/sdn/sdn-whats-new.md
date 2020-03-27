---
title: Neues in Sdn für Windows Server
description: Dieses Thema enthält Informationen zu neuen Software-Defined Networking-Features für Windows Server 1709.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-hv-switch
ms.topic: get-started-article
ms.assetid: efad919b-e9e7-4a0c-b373-e68a092f93b5
ms.author: lizross
author: eross-msft
ms.date: 10/02/2018
ms.openlocfilehash: 32828cc6c46903e0841dcdae55f69df6a0cac252
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80317445"
---
# <a name="whats-new-in-sdn-for-windows-server-2019"></a>Neues in SDN für Windows Server 2019

>Gilt für: Windows Server (halbjährlicher Kanal)


|                         **Feature**                          |                                                                                                                                                                                         **Beschreibung**                                                                                                                                                                                         | **Neu/aktualisiert** |
|--------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------|
| [Verschlüsselte Netzwerke](vnet-encryption/sdn-vnet-encryption.md) | Die Verschlüsselung virtueller Netzwerke ermöglicht die Verschlüsselung des Datenverkehrs von virtuellen Netzwerken zwischen virtuellen Computern, die in Subnetzen, die als "Verschlüsselung aktiviert" gekennzeichnet sind, miteinander kommunizieren. Es nutzt auch Datagram Transport Layer Security (DTLS) im virtuellen Subnetz, um Pakete zu verschlüsseln. DTLS schützt vor Abhörversuchen, Manipulation und Fälschung durch jeden, der Zugriff auf das physische Netzwerk hat. |       Neu       |
|    [Firewallüberwachung](security/sdn-firewall-auditing.md)    |                                                                                            Die firewallüberwachung ist eine neue Funktion für die Sdn-Firewall in Windows Server 2019. Wenn Sie die Sdn-Firewall aktivieren, werden alle Flows aufgezeichnet, die von Sdn-Firewallregeln (ACLs) mit aktivierter Protokollierung verarbeitet werden.                                                                                            |       Neu       |
| [Peering von virtuellen Netzwerken](vnet-peering/sdn-vnet-peering.md)  |                                                                                                                      Das Peering virtueller Netzwerke ermöglicht das nahtlose Verbinden von zwei virtuellen Netzwerken. Nach dem Peer werden die virtuellen Netzwerke zu konnektivitätszwecken als eins angezeigt.                                                                                                                      |       Neu       |
|           [Ausgangs Messung](manage/sdn-egress.md)            |                  Dieses neue Feature in Windows Server 2019 ermöglicht Sdn das anbieten von Nutzungs Zählern für ausgehende Datenübertragungen. Wenn dieses Feature hinzugefügt wurde, hält der Netzwerk Controller eine Whitelist pro Virtual Network aller im SDN verwendeten IP-Adressbereiche vor und berücksichtigt alle Pakete, die für ein Ziel, das nicht in einem dieser Bereiche enthalten ist, für ausgehende Datenübertragungen in Rechnung gestellt werden.                   |       Neu       |

---



