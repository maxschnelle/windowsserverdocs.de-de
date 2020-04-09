---
title: 'Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung mit mehreren Standorten'
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 3c98106c-67cc-406a-810e-f2e09f7e2c5e
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c915cf9ad5059e0069f68caa6bc7605d6c3fcfab
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80861503"
---
# <a name="test-lab-guide-demonstrate-a-directaccess-multisite-deployment"></a>Testumgebungsanleitung: Vorführung einer DirectAccess-Bereitstellung für mehrere Standorte

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Der Remote Zugriff ist eine Server Rolle in den Betriebssystemen Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012, die Remote Benutzern den sicheren Zugriff auf interne Netzwerkressourcen über DirectAccess oder RRAS-VPN ermöglicht. Diese Anleitung enthält Schritt-für-Schritt-Anweisungen zum Erweitern der [Test Umgebungs Anleitung: veranschaulichen der Einrichtung von DirectAccess Single Server mit gemischtem IPv4 und IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004) , um den Remote Zugriff in einem Szenario mit mehreren Standorten zu veranschaulichen.  
  
Beim Bereitstellen des Remote Zugriffs in einem Szenario mit mehreren Standorten können Sie RAS-Server an geografisch unterschiedlichen Standorten konfigurieren. Früher mussten Remote Benutzer stets eine Verbindung mit dem Unternehmensnetzwerk über einen bestimmten DirectAccess-Server herstellen. Mit Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 und Windows 10 oder Windows 8 können Sie Einstiegspunkte für jeden geografischen Standort in Ihrer Bereitstellung konfigurieren. Jeder Einstiegspunkt kann ein einzelner RAS-Server oder ein Cluster von Remote Zugriffs Servern sein. Remote Benutzer haben die Möglichkeit, eine Verbindung mit einem der RAS-Einstiegspunkte der Organisation herzustellen. Wenn ein Remote Benutzer z. b. in der Regel eine Verbindung mit dem RAS-Einstiegspunkt in Asien herstellt, aber dann einen geschäftlichen Trip zu Europa durchführt, stellt der Client Computer automatisch eine Verbindung mit dem nächstgelegenen RAS-Einstiegspunkt her.  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Dieses Handbuch enthält Anweisungen zum Konfigurieren und veranschaulichen des Remote Zugriffs mithilfe von neun Servern und drei Client Computern. Die abgeschlossene Remote Zugriffs-Testumgebung für mehrere Standorte simuliert ein Intranet, das Internet und ein Heimnetzwerk und veranschaulicht die Remote Zugriffs Funktionalität in verschiedenen Internetverbindungs Szenarien.  
  
> [!IMPORTANT]  
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.  
  


