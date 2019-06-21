---
title: Schritte zum Konfigurieren der Testumgebung
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: a3d01dd8002e28fb127ac6b1b4cea25c58953521
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281395"
---
# <a name="steps-for-configuring-the-test-lab"></a>Schritte zum Konfigurieren der Testumgebung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Schritte beschreiben das Konfigurieren der remotezugriffinfrastruktur, die RAS-Server und Clients zu konfigurieren und Testen der DirectAccess-Konnektivität über das Internet und Homenet-Subnetz.  
  
In dieser testumgebungsanleitung werden Sie eine remotezugriffsbereitstellung für mehrere Standorte erstellen, durch die folgenden Schritte ausführen:  
  
-   [SCHRITT 1: Erstellen der Basiskonfiguration](assetId:///9eb4a9ba-9118-4ea3-8963-e643ec81c3ed). Führen Sie alle Schritte in der [Test Lab Guide: Veranschaulichen von DirectAccess Single Server-Setup mit gemischten IPv4 und IPv6-](https://go.microsoft.com/fwlink/p/?LinkId=237004).  
  
-   [SCHRITT 2: Installieren und Konfigurieren von ROUTER1](assetId:///e4b1a298-d5b0-410e-970b-c5358a9378f9). ROUTER1 bietet und Weiterleitung Funktionen zwischen den Subnetzen "Corpnet" und "2-Corpnet".  
  
-   [SCHRITT 3: Installieren und Konfigurieren von CLIENT2](assetId:///6cbee1b5-f6f6-443f-8fa9-31cc5c05a0ee). CLIENT2 ist ein Windows 7-Clientcomputer, die verwendet wird, um zu veranschaulichen die Abwärtskompatibilität Kompatibilität einer Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012-RAS-Bereitstellung.  
  
-   [SCHRITT 4: Konfigurieren von APP1](assetId:///a0ee655e-c01e-4bf3-a7b3-064e9614f810). Konfigurieren von APP1 mit ROUTER1 als Standardgateway und 2-DC1 als alternativen DNS-Server.  
  
-   [SCHRITT 5: Konfigurieren von DC1](assetId:///205ca795-93ce-4e53-aa6b-b44c87f0e14a). Konfigurieren von DC1 mit zusätzlichen Active Directory-Standort und weitere Sicherheitsgruppen für Windows 7-Clientcomputer.  
  
-   [SCHRITT 6: Installieren und Konfigurieren von 2-DC1](assetId:///16752f61-edbf-4ff4-9d7a-e2077b66a127). Bei einer Bereitstellung mit mehreren Standorten müssen Sie zwei oder mehrere Domänen und Standorte an. 2-DC1 bietet Domänencontroller und DNS-Dienste für die Domäne corp2.corp.contoso.com.  
  
-   [SCHRITT 7: Installieren und Konfigurieren von 2-APP1](assetId:///7d04b54e-590a-4d33-9766-415789859f29). 2-APP1 ist ein Web- und Server im Netzwerk 2 – "Corpnet".  
  
-   [SCHRITT 8: Konfigurieren von INET1](assetId:///8ecc0b63-8626-4939-8d26-3d51d051d231). INET1 simuliert, das Internet in der vorliegenden testumgebungsanleitung wird. Sie müssen einen DNS-Eintrag konfigurieren, der in die öffentliche IP-Adresse 2-EDGE1 aufgelöst wird.  
  
-   [SCHRITT 9: Konfigurieren von EDGE1](assetId:///562744dc-30f6-42fa-bd5f-60a013b2179e). Konfigurieren der 2-Unternehmensnetzwerks-DNS-Server und routing auf EDGE1.  
  
-   [SCHRITT 10: Installieren und Konfigurieren von 2-EDGE1](assetId:///1938c4f3-ca96-475d-9f2e-6bea3b7a4130). In einer Bereitstellung für mehrere Standorte sind zwei RAS-Server erforderlich. 2-EDGE1 bietet RAS-Dienste für die zweite Domäne.  
  
-   [SCHRITT 11: Konfigurieren der Bereitstellung für mehrere Standorte](assetId:///537e4b68-043f-49c9-94d8-15ce8c4b18e2). Nachdem beide RAS-Server konfiguriert haben, können Sie Ihre Bereitstellung für mehrere Standorte konfigurieren.  
  
-   [SCHRITT 12: Testen der DirectAccess-Konnektivität](assetId:///aa293b5d-4b6f-4004-95f3-0ab54804b15c). Testen der DirectAccess-Konnektivität auf beiden Clientcomputern aus dem Internet-Subnetz über EDGE1 und 2-EDGE1.  
  
-   [SCHRITT 13: Testen der DirectAccess-Clientkonnektivität hinter einem NAT-Gerät](assetId:///41f8195b-00a1-4991-9db8-3703514dbe0c). DirectAccess-Clientkonnektivität hinter einem NAT-Gerät zu testen.  
  
-   [SCHRITT 14: Eine Momentaufnahme der Konfiguration](assetId:///7b56d5c9-c334-463e-9e29-d652ca110d84). Nach Abschluss der testumgebung können eine Momentaufnahme der arbeiten remotezugriffsbereitstellung für mehrere Standorte, damit Sie zurückkehren können, um diese später, um zusätzliche Szenarien zu testen.  
  


