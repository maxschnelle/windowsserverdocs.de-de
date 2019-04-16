---
title: Network Shell (Netsh)
description: Dieses Thema enthält eine Übersicht über das Befehlszeilenprogramm Network Shell (Netsh) in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0a23d60bc3f181fee62ade105e546bbb7161c133
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="network-shell-netsh"></a>Network Shell \(Netsh\)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Network Shell (Netsh) ist ein Befehlszeilenprogramm, mit dem Sie konfigurieren und den Status der verschiedenen Netzwerk Kommunikation Serverrollen und Komponenten anzeigen, nachdem sie auf Computern mit Windows Server 2016 installiert sind.

>[!NOTE]
>Zusätzlich zu diesem Thema wird die folgende Network Shell-Inhalte zur Verfügung.
>
> - [Netsh-Befehl Syntax Kontexte und formatieren](netsh-contexts.md)
> - [Network Shell (Netsh) Beispielbatchdatei](netsh-wins.md)
> - [Netsh Technical Reference](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc) 

Einige Clienttechnologien, wie z. B. das Dynamic Host Configuration-Protokoll \(DHCP\) Client und BranchCache, bieten auch Netsh-Befehle, mit denen Sie zum Konfigurieren von Clientcomputern, auf denen Windows 10 ausgeführt werden.

In den meisten Fällen Netsh-Befehle bieten die gleiche Funktionalität, die verfügbar ist, bei der Verwendung der Microsoft Management Console \(MMC\) snap\-in für jedes Netzwerk Server-Rolle oder einen Netzwerk-Feature. Sie können z. B. Netzwerkrichtlinienserver \(NPS\) konfigurieren, mit der NPS-MMC-Snap-in oder die Netsh-Befehle in der **Netsh Nps** Kontext.

Es gibt darüber hinaus Netsh-Befehle für die netzwerktechnologien, wie z. B. für IPv6-Netzwerk-Bridge und \(RPC\) Remote Procedure Call, die nicht in Windows Server als ein MMC-Snap-in verfügbar sind.

>[!IMPORTANT]
>Es wird empfohlen, die Verwendung von Windows PowerShell zum Verwalten von netzwerktechnologien in [Windows Server 2016 und Windows 10](https://technet.microsoft.com/library/mt156917.aspx) anstatt Network Shell. Network Shell ist für die Kompatibilität mit Skripts, enthalten jedoch und ihre Verwendung wird unterstützt.

## <a name="network-shell-netsh-technical-reference"></a>Technische Referenz zu Network Shell (Netsh)

Die technische Referenz zu Netsh bietet eine umfassende Netsh-Befehlsreferenz, einschließlich Syntax, Parameter und Beispiele für die Netsh-Befehle. Die technische Referenz zu Netsh können Sie Skripts und Batchdateien mithilfe von Netsh-Befehle für die lokale oder remote-Verwaltung von netzwerktechnologien auf Computern unter Windows Server 2016 und Windows 10 erstellen.  
  
### <a name="content-availability"></a>Verfügbarkeit der Inhalte  
  
Der technischen Referenz zu Network Shell steht zum Download im Windows-Hilfe \(*.chm\) Format aus dem TechNet-Galerie: [technische Referenz zu Netsh](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  

