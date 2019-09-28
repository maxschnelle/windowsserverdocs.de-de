---
title: Schritte zum Konfigurieren der Testumgebung für DirectAccess-Cluster-NLB
description: Dieses Thema ist Teil der Test Umgebungs Anleitung zum Veranschaulichen von DirectAccess in einem Cluster mit Windows NLB für Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e508d3ee-ffa6-463f-a3dd-9e35e745c005
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 108c63298ad3382f5ece790258f2d278bb03b78b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388403"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>Schritte zum Konfigurieren der Testumgebung für DirectAccess-Cluster-NLB

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In den folgenden Schritten wird beschrieben, wie Sie die Remote Zugriffs Infrastruktur konfigurieren, die RAS-Server und-Clients konfigurieren und die DirectAccess-Konnektivität aus den Subnetzen Internet und homenet testen.  
  
In dieser Test Umgebungs Anleitung erstellen Sie einen NLB-aktivierten Remote Zugriffs Cluster, indem Sie die folgenden Schritte ausführen:  
  
-   [Schritt 1: vervollständigen Sie die DirectAccess-Konfiguration](STEP-1-Complete-the-DirectAccess-Configuration.md). Führen Sie alle Schritte in der Test Umgebungs Anleitung für [aus: Veranschaulichen der Einrichtung eines einzelnen Servers für DirectAccess mit gemischtem IPv4 und IPv6 @ no__t-0.  
  
-   [SCHRITT 2: Konfigurieren Sie Edge1 @ no__t-0. Konfigurieren Sie die Remote Zugriffs Rolle auf Edge1 für den Lastenausgleich.  
  
-   [SCHRITT 3: Installieren und konfigurieren Sie EDGE2 @ no__t-0. EDGE2 fungiert als zweiter RAS-Server in einem Remote Zugriffs Cluster.  
  
-   [SCHRITT 4: Erstellen des Remote Zugriffs Clusters mit Netzwerk Lastenausgleich @ no__t-0-Edge1 wird als erster Server in einem Remote Zugriffs Cluster konfiguriert. EDGE2 wird dem Cluster hinzugefügt, und NLB ist für den Cluster konfiguriert.  
  
-   [SCHRITT 5: Testen Sie die DirectAccess-Konnektivität über das Internet und über den Cluster @ no__t-0. Nach Abschluss der NLB-und Cluster Konfiguration können Sie die DirectAccess-Client Konnektivität über den Cluster mit Lastenausgleich testen.  
  
-   [SCHRITT 6: Testen Sie die DirectAccess-Client Konnektivität hinter einem NAT-Gerät @ no__t-0. Verschieben Sie den Client Computer hinter ein NAT-Gerät, um das Testen der DirectAccess-Client Konnektivität hinter einem Heim Router zu simulieren.  
  
-   [SCHRITT 7: Testen Sie die Konnektivität bei der Rückkehr zum Corpnet @ no__t-0. Stellen Sie sicher, dass der Client Computer bei der Rückkehr zu Corpnet weiterhin auf Unternehmensressourcen zugreifen kann.  
  
-   [SCHRITT 8: Momentaufnahme der Konfiguration @ no__t-0. Nachdem Sie die Testumgebung abgeschlossen haben, erstellen Sie eine Momentaufnahme des funktionierenden NLB-Clusters für den Remote Zugriff, damit Sie später wieder zurückkehren können, um weitere Szenarios zu testen.  
  


