---
title: Pktmon-Unterstützung für Microsoft-Netzwerkmonitor (NetMon)
description: Verwenden Sie diese Seite, um die vom Paket Monitor generierten ETL-Dateien in NetMon zu analysieren.
ms.topic: how-to
author: khdownie
ms.author: v-kedow
ms.date: 11/12/2020
ms.openlocfilehash: 7c6e3a40558ea27a273464d157fa4fbdbacd7134
ms.sourcegitcommit: 8808f871c8cf131f819ef5540286218bd425da96
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/14/2020
ms.locfileid: "94632512"
---
# <a name="pktmon-support-for-microsoft-network-monitor-netmon"></a>Pktmon-Unterstützung für Microsoft-Netzwerkmonitor (NetMon)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows 10, Azure Stack HCI, Azure Stack Hub, Azure

Der Paket Monitor (pktmon) generiert Protokolle im ETL-Format. Diese Protokolle können mithilfe von Microsoft-Netzwerkmonitor (NetMon) mithilfe spezieller Parser analysiert werden. In diesem Thema wird erläutert, wie die vom Paket Monitor generierten ETL-Dateien in Netmon analysiert werden.

## <a name="network-monitor-setup-and-configuration"></a>Netzwerkmonitor Setup und Konfiguration

Führen Sie die folgenden Schritte zum Installieren und Konfigurieren von Netmon aus, um die von Paketen generierten ETL-Dateien zu analysieren:

   1. [Installieren Sie Netzwerkmonitor 3,4](/download/4865).
   1. Starten Sie Netzwerkmonitor erweitert, und legen Sie Windows als aktives parserprofil auf fest (Extras > Optionen > Parser Profile)
   1. Kopieren Sie etl_Microsoft-Windows-pktmon-Events. NPL von [hier](https://github.com/microsoft/NetMon_Parsers_for_PacketMon/blob/main/etl_Microsoft-Windows-PktMon-Events.npl)   nach "%ProgramData%\microsoft\network Monitor 3 \ npl\networkmonitor parameters\windows"
   1. Kopieren Sie stub_etl_Microsoft-Windows-pktmon-Events. NPL von [hier](https://github.com/microsoft/NetMon_Parsers_for_PacketMon/blob/main/stub_etl_Microsoft-Windows-PktMon-Events.npl) nach "%ProgramData%\microsoft\network Monitor 3 \ npl\networkmonitor parameters\windows\stub"
   1. Benennen Sie stub_etl_Microsoft-Windows-pktmon-Events. NPL in etl_Microsoft-Windows-pktmon-Events. NPL um.
   1. Schließen Sie etl_Microsoft-Windows-pktmon-Events. NPL in NetworkMonitor_Parsers_sparser. NPL unter "%ProgramData%\microsoft\network Monitor 3 \ npl\networkmonitor Parser" ein.
   1. Neustart Netzwerkmonitor zum erneuten Erstellen der Parser erhöht.

