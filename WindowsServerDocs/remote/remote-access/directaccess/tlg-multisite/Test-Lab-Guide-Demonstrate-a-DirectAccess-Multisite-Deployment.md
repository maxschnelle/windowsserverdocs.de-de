---
title: 'Testumgebungsanleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte'
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 47b6848789a7e61bdb3cc12e6339777ed1a4f1b3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59811981"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>Testumgebungsanleitung: Veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

RAS ist eine Serverrolle in den Betriebssystemen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, die Remotebenutzern den sicheren Zugriff auf interne Netzwerkressourcen über DirectAccess oder RRAS-VPN ermöglicht. Diese Anleitung enthält schrittweise Anweisungen zum Erweitern der [Test Lab Guide: Demonstrate DirectAccess Single Server-Setup mit gemischten IPv4 und IPv6-](https://go.microsoft.com/fwlink/p/?LinkId=237004) um Remotezugriff auf in einem Szenario mit mehreren Standorten zu veranschaulichen.  
  
Bereitstellen des Remotezugriffs in einem Szenario mit mehreren Standorten können Sie unterschiedliche geografische Orte RAS-Server konfigurieren. Zuvor mussten Remotebenutzer stets eine Verbindung mit dem Unternehmensnetzwerk über einem bestimmten DirectAccess-Server. Mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 und Windows 10 oder Windows 8 können Sie die Einstiegspunkte für jeden geografischen Standort in Ihrer Bereitstellung konfigurieren. Jeden Einstiegspunkt kann es sich um eine RAS-Servers oder einen Cluster mit RAS-Server sein. Remote-Benutzer haben die Möglichkeit, sich mit einem RAS-Einstiegspunkte der Organisation verbinden. Z. B. wenn ein Remotebenutzer in der Regel stellt eine Verbindung her, auf den RAS-Einstiegspunkt in Asien befindet, aber dann in "Europa" auf einer Geschäftsreise wechselt, verbindet sich der Clientcomputer automatisch auf den nächsten Einstiegspunkt für den Remotezugriff.  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch enthält Anweisungen zum Konfigurieren und veranschaulichen des Remotezugriffs mit neun Servern und drei Clientcomputern. Die abgeschlossene für mehrere Standorte RAS-testumgebung simuliert ein Intranet, im Internet und einem Heimnetzwerk und veranschaulicht die remotezugriffsfunktionalität in verschiedenen internetverbindungsszenarios.  
  
> [!IMPORTANT]  
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.  
  


