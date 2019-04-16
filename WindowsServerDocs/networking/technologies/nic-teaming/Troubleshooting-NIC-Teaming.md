---
title: Problembehandlung bei der NIC-Teamvorgang
description: Dieses Thema enthält Informationen zur Problembehandlung beim NIC-Teamvorgang in Windows Server2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-nict
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fdee02ec-3a7e-473e-9784-2889dc1b6dbb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 634ec1a5eee0cd661ca89c2673e5b74abd458cd6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="troubleshooting-nic-teaming"></a>Problembehandlung bei der NIC-Teamvorgang

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält Informationen zur Problembehandlung beim NIC-Teaming, und enthält die folgenden Abschnitte, die mögliche Ursachen von Problemen mit NIC-Teamvorgang zu beschreiben.  
  
-   [Hardware, die Spezifikation entsprechen nicht](#bkmk_hardware)  
  
-   [Sicherheitsfeatures physischen Switch](#bkmk_switch)  
  
-   [Mit WindowsPowerShell aktivieren und deaktivieren](#bkmk_ps)  
  
## <a name="bkmk_hardware"></a>Hardware, die Spezifikation entsprechen nicht  
Beim hardwareimplementierungen von Standardprotokollen Spezifikation nicht entsprechen, NIC-Teaming Leistung möglicherweise beeinträchtigt.  
  
Während des normalen Betriebs möglicherweise NIC-Teaming Pakete aus der IP-Adresse, jedoch mit Zugriff auf mehrere andere Quelle Media Control (MAC)-Adressen senden. Entsprechend Protocol-Standards müssen die Empfänger dieser Pakete die IP-Adresse des Hosts oder virtuellen Computer in Reaktion auf die MAC-Adresse, von der das Paket empfangen wurde, anstatt eine bestimmte MAC-Adresse aufgelöst.  Clients, die die Adresse Auflösung Protokolle, IPv4s-Protokoll ARP (Address Resolution) oder des IPv6-Neighbor Discovery-Protokoll (NDP), ordnungsgemäß implementieren sendet Pakete mit dem richtigen Ziel-MAC-Adresse (die MAC-Adresse des virtuellen Computers oder der Host, der die IP-Adresse besitzt).  
  
Einige Hardware eingebettet, jedoch die Adresse Resolution-Protokolle nicht richtig implementiert, und auch möglicherweise nicht explizit eine IP-Adresse aufzulösen einer MAC-Adresse mit ARP oder NDP.  Ein Storage Area Network (SAN) Controller ist ein Beispiel für ein Gerät, das auf diese Weise ausgeführt werden kann. Nicht übereinstimmende Geräte die Quell-MAC-Adresse, die enthalten ist ein empfangenes Paket kopieren und verwenden, die als Ziel-MAC-Adresse in die entsprechenden ausgehenden Pakete.  
  
Dies führt dazu, dass Pakete, die zu einem falschen Ziel-MAC-Adresse gesendet werden. Aus diesem Grund werden die Pakete vom virtuellen Hyper-V-Switch gelöscht, da sie keine bekannten Ziel übereinstimmen.  
  
Wenn Sie Probleme haben Probleme beim Herstellen einer Verbindung mit SAN-Domänencontroller oder andere Hardware eingebettet, sollten Paket erfasst werden und zu bestimmen, ob die Hardware ordnungsgemäß ARP oder NDP implementiert, und wenden Sie sich an Ihren Hardwarehersteller für Unterstützung.  
  
## <a name="bkmk_switch"></a>Sicherheitsfeatures physischen Switch  
Je nach Konfiguration möglicherweise NIC-Teaming Pakete aus der IP-Adresse mit mehreren anderen Quelle MAC-Adressen senden.  Dies kann insbesondere dann, wenn der Schalter nicht bekannt ist, sind die Ports in einem Team von Features auf dem physischen Switch z.B. dynamische ARP-Überprüfung oder IP-Quelle zu schützen, Sicherheit Reise. Dies kann vorkommen, wenn Sie NIC-Teaming-Switch unabhängigen Modus konfigurieren.  Überprüfen Sie die Switch-Protokolle, um festzustellen, ob die Switch-Sicherheitsfeatures Konnektivitätsprobleme mit NIC-Teamvorgang verursacht werden.  
  
## <a name="bkmk_ps"></a>Deaktivieren und Aktivieren von Netzwerkadapter mithilfe von Windows PowerShell  
Eine häufige Ursache für einen NIC-Team zu Fehlern ist, dass die teamschnittstelle deaktiviert ist. In vielen Fällen ist die Schnittstelle versehentlich deaktiviert, wenn die folgende Sequenz von Windows PowerShell-Befehle ausgeführt wird:  
  
```  
Disable-NetAdapter *  
Enable-NetAdapter *  
```  
  
Diese Abfolge von Befehlen wird nicht alle der NetAdapters ermöglichen, die deaktiviert.  
  
Dies liegt daran deaktivieren alle zugrunde liegenden physischen Member NICs bewirkt, dass der NIC-Team-Benutzeroberfläche entfernt wird und nicht mehr im Get-NetAdapter angezeigt. Aus diesem Grund die **Enable-NetAdapter \ *** Befehl nicht das NIC-Team aktivieren, da diese Karte entfernt wird.  
  
Die **Enable-NetAdapter \ *** Befehl, jedoch ermöglicht das Mitglied NICs, wodurch dann (nach kurzer Zeit) der Team-Benutzeroberfläche neu erstellt werden. In diesem Fall ist der teamschnittstelle weiterhin im Status "deaktiviert", da es nicht erneut aktiviert wurde. Die teamschnittstelle aktivieren, nachdem es neu erstellt wird, wird Datenverkehr Datenfluss erneut beginnen kann.  
  
## <a name="see-also"></a>Siehe auch  
[NIC-Teamvorgang](NIC-Teaming.md)  
  


