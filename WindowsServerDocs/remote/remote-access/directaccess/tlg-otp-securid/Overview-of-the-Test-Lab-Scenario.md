---
title: Übersicht über das Testumgebungsszenario
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ce584811-b209-48fe-ab2b-4c399bd0bd79
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ebf19d75928e2a19732f2c6c4acaebbf8b34f25f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59871161"
---
# <a name="overview-of-the-test-lab-scenario"></a>Übersicht über das Testumgebungsszenario

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

RAS ist eine Serverrolle in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012-Betriebssysteme, die es ermöglicht Remotebenutzern den sicheren internen Zugriff auf Netzwerkressourcen über DirectAccess oder virtuelle Private Netzwerke (VPNs) mit der Routing und RAS-Dienst (RRAS). Diese Anleitung enthält schrittweise Anweisungen zum Erweitern der [Test Lab Guide: Demonstrate DirectAccess Single Server-Setup mit gemischten IPv4 und IPv6-](https://go.microsoft.com/fwlink/p/?LinkId=237004) veranschaulicht eine Konfiguration des Remotezugriffs Einmalkennwort (OTP).  
  
> [!WARNING]  
> Das Design der vorliegenden testumgebungsanleitung enthält Infrastrukturserver, z. B. einen Domänencontroller und einer Zertifizierungsstelle (CA), die entweder Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden. Mit der vorliegenden testumgebungsanleitung Infrastrukturserver zu konfigurieren, auf denen andere Betriebssysteme ausgeführt werden nicht getestet wurde, und Anweisungen zum Konfigurieren von anderen Betriebssystemen sind in dieser Anleitung nicht enthalten.  
  
## <a name="about-this-guide"></a>Informationen zur Anleitung  
Remote Access in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 fügt Unterstützung für die Clientauthentifizierung mit OTP hinzu. Für die Zwecke dieser testumgebung wird nur RSA SecurID zur Veranschaulichung der OTP-Funktionalität mit dem Remotezugriff verwendet. Andere RADIUS-basierten OTP-Lösungen werden ebenfalls unterstützt, aber nicht Bestandteil dieser testumgebung sind. Diese Anleitung enthält Anweisungen zum Konfigurieren und Veranschaulichen des Remotezugriffs mit sechs Servern und zwei Clientcomputern. Der abgeschlossenen Remotezugriff mit OTP-testumgebung simuliert ein Intranet, im Internet und einem Heimnetzwerk und veranschaulicht die remotezugriffsfunktionalität in verschiedenen internetverbindungsszenarios.  
  
> [!IMPORTANT]  
> Diese Testumgebung ist eine Machbarkeitsstudie mit der minimalen Anzahl an Computern. Die in dieser Anleitung beschriebene Konfiguration ist nur für Testzwecke geeignet und sollte nicht in einer Produktionsumgebung verwendet werden.  
  


