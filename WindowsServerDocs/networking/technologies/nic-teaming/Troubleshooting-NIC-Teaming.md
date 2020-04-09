---
title: Problembehandlung beim NIC-Teamvorgang
description: Dieses Thema enthält Informationen zur Problembehandlung des NIC-Team Vorgangs in Windows Server 2016.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-nict
ms.topic: article
ms.assetid: fdee02ec-3a7e-473e-9784-2889dc1b6dbb
ms.author: lizross
author: eross-msft
ms.date: 09/13/2018
ms.openlocfilehash: e8da45053562ebd834a6657d4c85b4c70da5ce55
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853723"
---
# <a name="troubleshooting-nic-teaming"></a>Problembehandlung beim NIC-Teamvorgang

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird erläutert, wie Sie Probleme mit dem NIC-Team Vorgang beheben, wie z. b. Hardware-und physische switchschnittstellen.  Wenn Hardware Implementierungen von Standardprotokollen den Spezifikationen nicht entsprechen, kann die Leistung des NIC-Team Vorgangs beeinträchtigt werden. Abhängig von der Konfiguration kann der NIC-Team Vorgang außerdem Pakete von derselben IP-Adresse mit mehreren Mac-Adressen senden, die die Sicherheitsfunktionen auf dem physischen Switch überspringen.

  
## <a name="hardware-that-doesnt-conform-to-specification"></a>Hardware, die nicht der Spezifikation entspricht  
  
Während des normalen Betriebs kann der NIC-Team Vorgang Pakete von derselben IP-Adresse, aber mit mehreren Mac-Adressen senden. Gemäß den Protokollstandards müssen die Empfänger dieser Pakete die IP-Adresse des Hosts oder der VM in eine bestimmte MAC-Adresse auflösen, anstatt auf die Mac-Adresse des empfangenden Pakets zu antworten.  Clients, die die Adress Auflösungs Protokolle (ARP und NDP) ordnungsgemäß implementieren, senden Pakete mit den richtigen Ziel-MAC-Adressen – d. h. die Mac-Adresse des virtuellen Computers oder Hosts, der diese IP-Adresse besitzt. 
  
Einige eingebettete Hardware implementiert die Adress Auflösungs Protokolle nicht ordnungsgemäß und löst eine IP-Adresse möglicherweise nicht explizit mithilfe von ARP oder NDP in eine Mac-Adresse auf.  Beispielsweise kann ein Storage Area Network (San)-Controller auf diese Weise durchgeführt werden. Nicht konforme Geräte kopieren die MAC-Quelladresse aus einem empfangenen Paket und verwenden Sie dann als Ziel-MAC-Adresse in den entsprechenden ausgehenden Paketen, was dazu führt, dass Pakete an die falsche MAC-Zieladresse gesendet werden. Aus diesem Grund werden die Pakete vom virtuellen Hyper-V-Switch gelöscht, da Sie nicht mit einem bekannten Ziel identisch sind.  
  
Wenn Sie Probleme beim Herstellen einer Verbindung mit San-Controllern oder einer anderen eingebetteten Hardware haben, sollten Sie Paket Erfassungen erstellen, um zu ermitteln, ob Ihre Hardware die ordnungsgemäße Implementierung von ARP oder NDP hat, und sich an Ihren Hardwarehersteller wenden.  

  
## <a name="physical-switch-security-features"></a>Sicherheitsfeatures für physische Switches  
Abhängig von der Konfiguration kann der NIC-Team Vorgang Pakete von derselben IP-Adresse mit mehreren Quell-MAC-Adressen senden, um die Sicherheitsfeatures auf dem physischen Switch zu überspringen. Beispielsweise die dynamische ARP-Überprüfung oder IP Source Guard, insbesondere dann, wenn der physische Switch nicht weiß, dass die Ports Teil eines Teams sind. Dies geschieht, wenn Sie den NIC-Team Vorgang im Schalter unabhängigen Modus konfigurieren. Überprüfen Sie die Schalter Protokolle, um zu bestimmen, ob switchsicherheitsfeatures Verbindungsprobleme verursachen. 
  
## <a name="disabling-and-enabling-network-adapters-by-using-windows-powershell"></a>Deaktivieren und Aktivieren von Netzwerkadaptern mithilfe von Windows PowerShell  

Ein Fehler tritt häufig auf, wenn ein NIC-Team fehlschlägt, weil die Team Schnittstelle deaktiviert ist, und in vielen Fällen, wenn eine Sequenz von Befehlen ausgeführt wird.  Mit dieser speziellen Sequenz von Befehlen werden nicht alle NetAdapters deaktiviert, da durch das Deaktivieren aller zugrunde liegenden physischen Member von NICs die NIC-Team Schnittstelle entfernt wird. 

In diesem Fall wird die NIC-Team Schnittstelle nicht mehr in Get-netadapter angezeigt, und aus diesem Grund aktiviert **enable-netadapter \\** * das NIC-Team nicht mehr. Der Befehl **enable-netadapter \\** * aktiviert jedoch die Member-NICs, die dann (nach kurzer Zeit) die Team Schnittstelle neu erstellen. Die Team Schnittstelle verbleibt im Status "deaktiviert", bis Sie erneut aktiviert wird, sodass der Netzwerk Datenverkehr gestartet werden kann. 

Mit der folgenden Windows PowerShell-Sequenz von Befehlen kann die Team Schnittstelle nach einem Unfall deaktiviert werden:  
  
```PowerShell 
Disable-NetAdapter *  
Enable-NetAdapter *  
```  
  

  
## <a name="related-topics"></a>Verwandte Themen  
- [NIC](NIC-Teaming.md)-Team Vorgang: in diesem Thema erhalten Sie einen Überblick über den NIC-Team Vorgang (Network Interface Card) in Windows Server 2016. Mit dem NIC-Team Vorgang können Sie zwischen einem und 32 physischen Ethernet-Netzwerkadaptern in einem oder mehreren softwarebasierten virtuellen Netzwerkadaptern gruppieren. Diese virtuellen Netzwerkadapter bieten schnelle Leistung und Fehlertoleranz bei Ausfall eines Netzwerkadapters.   

- [NIC-Team Vorgang MAC-Adress Verwendung und-Verwaltung](NIC-Teaming-MAC-Address-Use-and-Management.md): Wenn Sie ein NIC-Team mit dem Switch-unabhängigen Modus und entweder Address Hash oder Dynamic Load Distribution konfigurieren, verwendet das Team die Media Access Control (Mac)-Adresse des primären NIC-Teammitglieds für ausgehenden Datenverkehr. Das primäre NIC-Team Mitglied ist ein Netzwerkadapter, der vom Betriebssystem aus der anfänglichen Gruppe von Team Mitgliedern ausgewählt wird.

- [NIC](nic-teaming-settings.md)-Team Vorgangs Einstellungen: in diesem Thema erhalten Sie eine Übersicht über die NIC-Team Eigenschaften, z. b. Team-und Lasten ausgleichsmodi. Außerdem erhalten Sie Informationen über die standbyadaptereinstellung und die Eigenschaft "primäre Team Schnittstelle". Wenn Sie über mindestens zwei Netzwerkadapter in einem NIC-Team verfügen, müssen Sie keinen Standby-Adapter für die Fehlertoleranz festlegen.
  


