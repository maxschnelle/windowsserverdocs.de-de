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
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2ea4658df75b7e290d66751a1373181f60f05f4e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80310734"
---
# <a name="steps-for-configuring-the-directaccess-cluster-nlb-test-lab"></a>Schritte zum Konfigurieren der Testumgebung für DirectAccess-Cluster-NLB

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In den folgenden Schritten wird beschrieben, wie Sie die Remote Zugriffs Infrastruktur konfigurieren, die RAS-Server und-Clients konfigurieren und die DirectAccess-Konnektivität aus den Subnetzen Internet und homenet testen.  
  
In dieser Test Umgebungs Anleitung erstellen Sie einen NLB-aktivierten Remote Zugriffs Cluster, indem Sie die folgenden Schritte ausführen:  
  
-   [Schritt 1: vervollständigen Sie die DirectAccess-Konfiguration](STEP-1-Complete-the-DirectAccess-Configuration.md). Führen Sie alle Schritte in der [Test Umgebungs Anleitung zum Veranschaulichen der Einrichtung von DirectAccess Single Server mit gemischtem IPv4 und IPv6](https://go.microsoft.com/fwlink/p/?LinkId=237004)aus.  
  
-   [Schritt 2: Konfigurieren von Edge1](STEP-2-Configure-EDGE1.md). Konfigurieren Sie die Remote Zugriffs Rolle auf Edge1 für den Lastenausgleich.  
  
-   [Schritt 3: Installieren und Konfigurieren von EDGE2](STEP-3-Install-and-Configure-EDGE2.md). EDGE2 fungiert als zweiter RAS-Server in einem Remote Zugriffs Cluster.  
  
-   [Schritt 4: Erstellen des Remote Zugriffs Clusters mit Netzwerk Lastenausgleich](STEP-4-Create-the-Network-Load-Balanced-Remote-Access-Cluster.md)Edge1 wird als erster Server in einem Remote Zugriffs Cluster konfiguriert. EDGE2 wird dem Cluster hinzugefügt, und NLB ist für den Cluster konfiguriert.  
  
-   [Schritt 5: Testen der DirectAccess-Konnektivität über das Internet und über den Cluster](STEP-5-Test-DirectAccess-Connectivity-from-the-Internet-and-Through-the-Cluster.md). Nach Abschluss der NLB-und Cluster Konfiguration können Sie die DirectAccess-Client Konnektivität über den Cluster mit Lastenausgleich testen.  
  
-   [Schritt 6: Testen der DirectAccess-Client Konnektivität hinter einem NAT-Gerät](STEP-6-Test-DirectAccess-Client-Connectivity-from-Behind-a-NAT-Device.md). Verschieben Sie den Client Computer hinter ein NAT-Gerät, um das Testen der DirectAccess-Client Konnektivität hinter einem Heim Router zu simulieren.  
  
-   [Schritt 7: Testen der Konnektivität bei der Rückkehr zum Unternehmensnetzwerk](STEP-7-Test-Connectivity-When-Returning-to-the-Corpnet.md). Stellen Sie sicher, dass der Client Computer bei der Rückkehr zu Corpnet weiterhin auf Unternehmensressourcen zugreifen kann.  
  
-   [Schritt 8: Erstellen einer Momentaufnahme der Konfiguration](da-cluster-nlb-s8-snapshot.md) Nachdem Sie die Testumgebung abgeschlossen haben, erstellen Sie eine Momentaufnahme des funktionierenden NLB-Clusters für den Remote Zugriff, damit Sie später wieder zurückkehren können, um weitere Szenarios zu testen.  
  


