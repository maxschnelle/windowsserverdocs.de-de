---
title: Schritte zum Konfigurieren der Testumgebung für DirectAccess-Cluster-NLB
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: Vorführen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3a243debf79d2c9d12de511153b74f23c5a44cce
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59880741"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>Schritte zum Konfigurieren der Testumgebung für DirectAccess-Cluster-NLB

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Schritte beschreiben das Konfigurieren der remotezugriffinfrastruktur, die RAS-Server und Clients zu konfigurieren und Testen der DirectAccess-Konnektivität über das Internet und Homenet-Subnetz.  
  
In diesem Test aktiviert testumgebungsanleitung für die Sie erstellen einen Network Load Balancing (NLB) Testumgebungsbereitstellung eines remotezugriffsclusters, indem Sie die folgenden Schritte ausführen:  
  
-   [Schritt 1 vervollständigen die DirectAccess-Konfiguration](STEP-1-Complete-the-DirectAccess-Configuration.md). Führen Sie alle Schritte in der [Test Lab Guide: Veranschaulichen von DirectAccess Single Server-Setup mit gemischten IPv4 und IPv6-](https://go.microsoft.com/fwlink/p/?LinkId=237004).  
  
-   [SCHRITT 2: Konfigurieren von EDGE1](STEP-2-Configure-EDGE1.md). Konfigurieren Sie die remotezugriffsrolle auf EDGE1 für den Lastenausgleich.  
  
-   [SCHRITT 3: Installieren und Konfigurieren von EDGE2](STEP-3-Install-and-Configure-EDGE2.md). EDGE2 fungiert als die zweite RAS-Server in einem Cluster den Remotezugriff.  
  
-   [SCHRITT 4: Erstellen Sie den Cluster Network Load Balancing RAS](STEP-4-Create-the-Network-Load-Balanced-Remote-Access-Cluster.md)-EDGE1 als der erste Server in einem Cluster den Remotezugriff konfiguriert ist. EDGE2 mit dem Cluster verknüpft ist, und NLB für den Cluster konfiguriert ist.  
  
-   [SCHRITT 5: Testen der DirectAccess-Konnektivität aus dem Internet und durch den Cluster](STEP-5-Test-DirectAccess-Connectivity-from-the-Internet-and-Through-the-Cluster.md). Nach Abschluss der Konfiguration von NLB und Cluster können Sie DirectAccess-Client-Konnektivität über den Load-Cluster mit Lastenausgleich testen.  
  
-   [SCHRITT 6: Testen der DirectAccess-Clientkonnektivität hinter einem NAT-Gerät](STEP-6-Test-DirectAccess-Client-Connectivity-from-Behind-a-NAT-Device.md). Verschieben Sie die Clientcomputer hinter einem NAT-Gerät zum Testen der DirectAccess-Clientkonnektivität hinter einem Router home zu simulieren.  
  
-   [SCHRITT 7: Testen der Konnektivität bei der Rückkehr zum Unternehmensnetzwerk](STEP-7-Test-Connectivity-When-Returning-to-the-Corpnet.md). Stellen Sie sicher, dass der Clientcomputer immer noch auf Unternehmensressourcen zugreifen kann, bei der Rückkehr zum Unternehmensnetzwerk.  
  
-   [SCHRITT 8: Eine Momentaufnahme der Konfiguration](da-cluster-nlb-s8-snapshot.md). Nach Abschluss der testumgebung können eine Momentaufnahme der arbeiten Remote Access-NLB-Cluster, damit Sie zurückkehren können, um diese später, um zusätzliche Szenarien zu testen.  
  


