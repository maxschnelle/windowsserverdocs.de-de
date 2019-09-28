---
title: 'Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung mit mehreren Standorten'
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bb4d69f914331e8fa7a06c6dd77ea342d5eefc6a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388223"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>Testumgebungsanleitung: Veranschaulichen einer DirectAccess-Bereitstellung mit mehreren Standorten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Der Remote Zugriff ist eine Server Rolle in den Betriebssystemen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, die Remote Benutzern den sicheren Zugriff auf interne Netzwerkressourcen über DirectAccess oder RRAS-VPN ermöglicht. Diese Anleitung enthält Schritt-für-Schritt-Anweisungen zum Erweitern der Test Umgebungs Anleitung für [: Veranschaulichen der DirectAccess-Einzel Server Einrichtung mit gemischtem IPv4 und IPv6 @ no__t-0, um den Remote Zugriff in einem Szenario mit mehreren Standorten zu veranschaulichen.  
  
Beim Bereitstellen des Remote Zugriffs in einem Szenario mit mehreren Standorten können Sie RAS-Server an geografisch unterschiedlichen Standorten konfigurieren. Früher mussten Remote Benutzer stets eine Verbindung mit dem Unternehmensnetzwerk über einen bestimmten DirectAccess-Server herstellen. Mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 und Windows 10 oder Windows 8 können Sie Einstiegspunkte für jeden geografischen Standort in Ihrer Bereitstellung konfigurieren. Jeder Einstiegspunkt kann ein einzelner RAS-Server oder ein Cluster von Remote Zugriffs Servern sein. Remote Benutzer haben die Möglichkeit, eine Verbindung mit einem der RAS-Einstiegspunkte der Organisation herzustellen. Wenn ein Remote Benutzer z. b. in der Regel eine Verbindung mit dem RAS-Einstiegspunkt in Asien herstellt, aber dann einen geschäftlichen Trip zu Europa durchführt, stellt der Client Computer automatisch eine Verbindung mit dem nächstgelegenen RAS-Einstiegspunkt her.  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch enthält Anweisungen zum Konfigurieren und veranschaulichen des Remote Zugriffs mithilfe von neun Servern und drei Client Computern. Die abgeschlossene Remote Zugriffs-Testumgebung für mehrere Standorte simuliert ein Intranet, das Internet und ein Heimnetzwerk und veranschaulicht die Remote Zugriffs Funktionalität in verschiedenen Internetverbindungs Szenarien.  
  
> [!IMPORTANT]  
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.  
  


