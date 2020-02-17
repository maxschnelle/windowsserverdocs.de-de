---
title: Network Shell (Netsh)
description: Dieses Thema bietet eine Übersicht über das Befehlszeilenprogramm Network Shell (Netsh) in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: ac440c8187424733c0636cf2013342458f08d2f4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405546"
---
# <a name="network-shell-netsh"></a>Network Shell \(Netsh\)

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Network Shell (Netsh) ist ein Befehlszeilenprogramm, mit dem der Status unterschiedlicher Serverrollen und Komponenten für die Netzwerkkommunikation konfiguriert und angezeigt werden kann, nachdem sie auf Computern unter Windows Server 2016 installiert wurden.

Einige Clienttechnologien wie der DHCP-Client \(Dynamic Host Configuration Protocol\) und BranchCache bieten ebenfalls Netsh-Befehle, mit denen Clientcomputer unter Windows 10 konfiguriert werden können.

In den meisten Fällen bieten die Netsh-Befehle dieselbe Funktionalität, die verfügbar ist, wenn du das MMC-Snap\-In \(Microsoft Management Console\) für die einzelnen Netzwerkserverrollen oder Netzwerkfunktionen verwendest. Du kannst z. B. den Netzwerkrichtlinienserver \(NPS\) konfigurieren, indem du entweder das NPS-MMC-Snap-In oder die Netsh-Befehle im **netsh nps**-Kontext verwendest.

Darüber hinaus gibt es Netsh-Befehle für Netzwerktechnologien wie für IPv6, Netzwerkbrücke und Remoteprozeduraufruf \(RPC\), die in Windows Server nicht als MMC-Snap-In verfügbar sind.

>[!IMPORTANT]
>Es wird empfohlen, Windows PowerShell zur Verwaltung von Netzwerktechnologien in [Windows Server 2016 und Windows 10](https://technet.microsoft.com/library/mt156917.aspx) statt Network Shell zu verwenden. Network Shell wird jedoch aus Gründen der Kompatibilität mit deinen Skripts einbezogen und seine Verwendung wird unterstützt.

## <a name="network-shell-netsh-technical-reference"></a>Technische Referenz für Network Shell (Netsh)

Die technische Referenz zu Netsh bietet eine umfassende Referenz für Netsh-Befehle, einschließlich Syntax, Parameter und Beispielen. Du kannst die technische Referenz von Netsh verwenden, um Skripts und Batchdateien mithilfe von Netsh-Befehlen für die lokale oder Remoteverwaltung von Netzwerktechnologien auf Computern mit Windows Server 2016 und Windows 10 zu erstellen.  
  
### <a name="content-availability"></a>Verfügbarkeit  
  
Die technische Referenz für Network Shell kann im Windows-Hilfeformat \(*.chm\) aus der TechNet Gallery heruntergeladen werden: [Technische Referenz zu Netsh](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
