---
title: Problembehandlung beim NIC-Teamvorgang
description: Dieses Thema enthält Informationen zur Problembehandlung beim NIC-Teamvorgang in Windows Server 2016.
manager: dougkim
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
ms.date: 09/13/2018
ms.openlocfilehash: d39dc6a4dcf5dca8186b0599fb479ed5ae684e0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856251"
---
# <a name="troubleshooting-nic-teaming"></a>Problembehandlung beim NIC-Teamvorgang

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema werden Möglichkeiten zum Beheben von NIC-Teamvorgang, z. B. Hardware- und physischen Switch Wertpapiere besprochen.  Wenn Hardware-Implementierungen von Standardprotokollen Spezifikationen nicht entsprechen, kann der NIC-Teamvorgang Leistung beeinträchtigt werden. Darüber hinaus kann je nach Konfiguration, NIC-Teamvorgang Pakete die gleiche IP-Adresse mit mehreren MAC-Adressen, die am physischen Switch Sicherheitsfunktionen Speicherprobleme senden.

  
## <a name="hardware-that-doesnt-conform-to-specification"></a>Hardware, die Spezifikation entsprechen nicht  
  
Während des normalen Betriebs kann der NIC-Teamvorgang Pakete von derselben IP-Adresse, noch mit mehreren MAC-Adressen senden. Gemäß Protokollstandards müssen die IP-Adresse des Hosts oder der VM die Empfängern dieser Pakete an die MAC-Adresse aus dem empfangenden Paket reagieren, anstatt eine bestimmte MAC-Adresse aufgelöst werden.  Clients, die die Adresse-Auflösung-Protokolle (ARP und NDP) ordnungsgemäß implementieren senden Pakete mit die richtige Ziel-MAC-Adressen – d. h. die MAC-Adresse des virtuellen Computers oder Hosts, die die IP-Adresse besitzt. 
  
Eingebettete Hardware die Protokolle der Adresse-Auflösung nicht richtig implementiert, und auch behebt möglicherweise nicht explizit eine IP-Adresse zu einer MAC-Adresse, die über ARP oder NDP.  Beispielsweise kann ein Storage Area Network (SAN)-Controller auf diese Weise ausführen. Nicht konforme Geräte kopieren die Quell-MAC-Adresse aus eines empfangenen Pakets und verwenden sie dann als MAC-Zieladresse in die entsprechenden ausgehenden Paketen, wodurch Pakete, die zu einem falschen Ziel-MAC-Adresse gesendet werden. Aus diesem Grund werden die Pakete vom virtuellen Hyper-V-Switch gelöscht, da sie keine bekannten Ziel übereinstimmen.  
  
Wenn Sie haben Probleme beim Herstellen einer Verbindung mit SAN-Controllern oder anderen Hardware eingebettet, Sie paketerfassungen, um festzustellen, ob die Hardware ordnungsgemäß ARP- oder NDP implementiert werden soll, und wenden Sie sich für Unterstützung an Ihren Hardwarehersteller.  

  
## <a name="physical-switch-security-features"></a>Sicherheitsfunktionen für physischen switch  
Je nach der Konfiguration möglicherweise NIC-Teamvorgang Pakete die gleiche IP-Adresse mit mehrere Quell-MAC-Adressen, die am physischen Switch Sicherheitsfunktionen Speicherprobleme senden. Z. B. ist dynamische ARP-Überprüfung oder die IP-Quell-Wächter bietet insbesondere dann, wenn das physische switch nicht beachten Sie, dass die Ports Teil eines Teams, das auftritt, wenn Sie NIC-Teaming im Switchunabhängig Modus konfigurieren. Überprüfen Sie die Switch-Protokolle, um zu bestimmen, ob die Switch-Sicherheitsfunktionen Konnektivitätsprobleme verursacht werden. 
  
## <a name="disabling-and-enabling-network-adapters-by-using-windows-powershell"></a>Deaktivieren und Aktivieren von Netzwerkadapter mithilfe von Windows PowerShell  

Eine häufige Ursache für das Fehlschlagen eines NIC-Teams ist, dass die teamschnittstelle deaktiviert ist, und in vielen Fällen verhindern, wenn eine Sequenz von Befehlen ausgeführt.  Diese bestimmte Sequenz von Befehlen ermöglicht nicht aller der NetAdapters deaktiviert, da die NIC-Team-Schnittstelle deaktivieren alle zugrunde liegenden physischen Mitglieder von NICs entfernt werden. 

In diesem Fall die NIC-Team-Schnittstelle nicht mehr angezeigt wird, in der Get-NetAdapter und aus diesem Grund **aktivieren-NetAdapter \***  ermöglicht nicht das NIC-Team. Die **aktivieren-NetAdapter \***  Befehl der Fall ist, jedoch aktivieren, das Element Netzwerkkarten, die (nach kurzer Zeit) klicken Sie dann die teamschnittstelle erstellt. Die teamschnittstelle bleibt im Zustand "deaktiviert" erst wieder aktiviert, Netzwerk-Datenverkehr fließen beginnen. 

Die folgende Windows PowerShell Befehlsfolge kann die teamschnittstelle versehentlich deaktivieren:  
  
```PowerShell 
Disable-NetAdapter *  
Enable-NetAdapter *  
```  
  

  
## <a name="related-topics"></a>Verwandte Themen  
- [NIC-Teamvorgang](NIC-Teaming.md): In diesem Thema stellen wir Ihnen in Windows Server 2016 einen Überblick über die Windows-Verwaltungsinstrumentation (Network Interface Card, NIC)-Teamvorgang. NIC-Teamvorgang ermöglicht Ihnen, zwischen 1 und 32 gruppieren, physische Ethernet-Netzwerkadapter in ein oder mehrere softwarebasierte virtuelle Netzwerkadapter. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.   

- [NIC-Teamvorgang-MAC-Adresse und -Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md): Beim Konfigurieren eines NIC-Teams mit unabhängigen Modus wechseln und adresshash oder dynamische lastverteilung steuern das Team verwendet, die die MAC-Adresse (MAC) des primären Mitglieds-NIC-Team für ausgehenden Datenverkehr. Dem primären NIC-Team-Mitglied ist, einen Netzwerkadapter, die vom Betriebssystem aus den anfänglichen Satz von Team-Mitglieder ausgewählt wird.

- [Einstellungen für die NIC-Teamvorgang](nic-teaming-settings.md): In diesem Thema haben wir bieten Ihnen einen Überblick über den NIC-Team-Eigenschaften, z. B. Teamvorgang und Lastenausgleich Modi zu laden. Sie haben zudem Details über die Standby-adaptereinstellung und die Eigenschaft des primären Team-Schnittstelle. Wenn Sie in einem NIC-Team über mindestens zwei Netzwerkadapter verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz zu bestimmen.
  


