---
title: Network Shell (Netsh)
description: Dieses Thema enthält eine Übersicht über das Network Shell (Netsh)-Befehlszeilen Dienstprogramm in Windows Server 2016.
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
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405546"
---
# <a name="network-shell-netsh"></a>Netzwerkshell \(Netsh\)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Network Shell (Netsh) ist ein Befehlszeilenprogramm, mit dem Sie den Status verschiedener Server Rollen und Komponenten für die Netzwerkkommunikation konfigurieren und anzeigen können, nachdem Sie auf Computern mit Windows Server 2016 installiert wurden.

Einige Client Technologien, wie z. b. das Dynamic Host Configuration-Protokoll \(DHCP-\) Client und BranchCache, stellen auch Netsh-Befehle bereit, mit denen Sie Client Computer konfigurieren können, auf denen Windows 10 ausgeführt wird.

In den meisten Fällen bieten Netsh-Befehle die gleiche Funktionalität, die verfügbar ist, wenn Sie die Microsoft Management Console \(MMC\) Snap\-in für jede Netzwerkserver Rolle oder Netzwerkfunktion verwenden. Beispielsweise können Sie den Netzwerk Richtlinien Server \(NPS-\) konfigurieren, indem Sie entweder das NPS-MMC-Snap-in oder die Netsh-Befehle im **netsh NPS** -Kontext verwenden.

Außerdem gibt es Netsh-Befehle für Netzwerktechnologien, wie z. b. für IPv6, Network Bridge und Remote Prozedur Aufruf \(RPC-\), die in Windows Server nicht als MMC-Snap-in verfügbar sind.

>[!IMPORTANT]
>Es wird empfohlen, dass Sie Windows PowerShell zum Verwalten von Netzwerktechnologien in [Windows Server 2016 und Windows 10](https://technet.microsoft.com/library/mt156917.aspx) anstelle der Netzwerkshell verwenden. Die Netzwerkshell ist jedoch für die Kompatibilität mit Ihren Skripts enthalten, und die Verwendung wird unterstützt.

## <a name="network-shell-netsh-technical-reference"></a>Technische Referenz für Network Shell (Netsh)

Die technische Referenz zu Netsh bietet eine umfassende netsh-Befehlsreferenz, einschließlich Syntax, Parametern und Beispielen für Netsh-Befehle. Sie können die technische Referenz zu Netsh verwenden, um Skripts und Batch Dateien mithilfe von Netsh-Befehlen für die lokale oder Remote Verwaltung von Netzwerktechnologien auf Computern mit Windows Server 2016 und Windows 10 zu erstellen.  
  
### <a name="content-availability"></a>Verfügbarkeit  
  
Die technische Referenz für die Netzwerk Shell kann in der Windows-Hilfe \(*. chm\) Format aus der TechNet Gallery heruntergeladen werden: [Netsh Technical Reference](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
