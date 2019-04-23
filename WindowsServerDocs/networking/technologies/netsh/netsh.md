---
title: Network Shell (Netsh)
description: Dieses Thema enthält eine Übersicht über die Network Shell (Netsh)-Befehlszeilen-Hilfsprogramm in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: aedef092-8445-4e53-b9d4-525ecd98b02d
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/13/2018
ms.openlocfilehash: 038b21783ef1d27619657ec3f9a472cf3caba68e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849361"
---
# <a name="network-shell-netsh"></a>Netzwerk-Shell \(Netsh\)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Netzwerkshell (Netsh) ist ein Befehlszeilen-Hilfsprogramm, mit dem Sie zum Konfigurieren und den Status der verschiedenen Network Communications Server-Rollen und Komponenten angezeigt, nachdem sie auf Computern unter Windows Server 2016 installiert sind.

Einige Client-Technologien, wie Dynamic Host Configuration Protocol \(DHCP\) Client- und BranchCache, bieten Sie auch Netsh-Befehle, mit denen Sie zum Konfigurieren von Clientcomputern, auf denen Windows 10 ausgeführt werden.

In den meisten Fällen bieten Netsh-Befehle die gleichen Funktionen, die verfügbar ist, wenn Sie die Microsoft Management Console verwenden \(MMC\) ausrichten\-in für alle Netzwerke Server-Rolle oder Netzwerk-Funktionen. Sie können z. B. Konfigurieren des Netzwerkrichtlinienservers \(NPS\) mithilfe der NPS-MMC-Snap-in oder die Netsh-Befehle in der **Netsh Nps** Kontext.

Darüber hinaus stehen Netsh-Befehle für die Netzwerk-Technologien, wie z. B. für die IPv6-Netzwerkbrücke und Remote Procedure Call \(RPC\), nicht im Windows-Server als ein MMC-Snap-in verfügbar sind.

>[!IMPORTANT]
>Es wird empfohlen, dass Sie Windows PowerShell, zum Verwalten von netzwerktechnologien in verwenden [Windows Server 2016 und Windows 10](https://technet.microsoft.com/library/mt156917.aspx) statt Network Shell. Netzwerkshell wird aus Gründen der Kompatibilität mit Ihren Skripts jedoch und ihre Verwendung wird unterstützt.

## <a name="network-shell-netsh-technical-reference"></a>Technische Referenz für Network Shell (Netsh)

Die technische Referenz zu Netsh bietet eine umfassende Netsh-Befehlsreferenz, einschließlich Syntax, Parameter und Beispielen für die Netsh-Befehle. Sie können die technische Referenz zu Netsh verwenden, Skripts und Batchdateien zu erstellen, indem Sie mithilfe von Netsh-Befehle für die lokal oder remote-Verwaltung von Netzwerk-Technologien auf Computern unter Windows Server 2016 und Windows 10.  
  
### <a name="content-availability"></a>Verfügbarkeit  
  
Technische Referenz für die Network Shell steht zum Download in der Windows-Hilfe \(.chm\) TechNet Gallery-Format: [Netsh – technische Referenz](https://gallery.technet.microsoft.com/Netsh-Technical-Reference-c46523dc)  
  
---
