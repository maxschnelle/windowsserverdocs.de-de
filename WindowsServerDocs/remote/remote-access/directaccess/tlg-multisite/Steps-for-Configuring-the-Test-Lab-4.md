---
title: Schritte zum Konfigurieren der Testumgebung
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7205b4-a822-4038-ab67-ec0a870737f2
ms.author: pashort
author: shortpatti
ms.openlocfilehash: dd8b8864dff98e51bf55aad9307523df4a0c30bf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404693"
---
# <a name="steps-for-configuring-the-test-lab"></a>Schritte zum Konfigurieren der Testumgebung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In den folgenden Schritten wird beschrieben, wie Sie die Remote Zugriffs Infrastruktur konfigurieren, die RAS-Server und-Clients konfigurieren und die DirectAccess-Konnektivität aus den Subnetzen Internet und homenet testen.  
  
In dieser Test Umgebungs Anleitung erstellen Sie eine Remote Zugriffs Bereitstellung für mehrere Standorte, indem Sie die folgenden Schritte ausführen:  
  
-   [SCHRITT 1: Vervollständigen Sie die Basiskonfiguration @ no__t-0. Führen Sie alle Schritte in der Test Umgebungs Anleitung für [aus: Veranschaulichen der Einrichtung eines einzelnen Servers für DirectAccess mit gemischtem IPv4 und IPv6 @ no__t-0.  
  
-   [SCHRITT 2: Installieren und konfigurieren Sie ROUTER1 @ no__t-0. ROUTER1 bietet Routing-und Weiterleitungs Funktionen zwischen den Subnetzen Corpnet und 2-Corpnet.  
  
-   [SCHRITT 3: Installieren und konfigurieren Sie CLIENT2 @ no__t-0. CLIENT2 ist ein Windows 7-Client Computer, der verwendet wird, um die Abwärtskompatibilität einer Windows Server 2016-, Windows Server 2012 R2-oder Windows Server 2012-Remote Zugriffs Bereitstellung zu veranschaulichen.  
  
-   [SCHRITT 4: Konfigurieren Sie App1 @ no__t-0. Konfigurieren Sie App1 mit ROUTER1 als Standard Gateway und 2 DC1 als alternativen DNS-Server.  
  
-   [SCHRITT 5: Konfigurieren Sie DC1 @ no__t-0. Konfigurieren Sie DC1 mit einer zusätzlichen Active Directory Site und zusätzlichen Sicherheitsgruppen für Windows 7-Client Computer.  
  
-   [SCHRITT 6: Installieren und Konfigurieren von 2-DC1 @ no__t-0. Bei einer Bereitstellung mit mehreren Standorten verfügen Sie über zwei oder mehr Domänen und Standorte. 2 DC1 stellt Domänen Controller und DNS-Dienste für die corp2.Corp.contoso.com-Domäne bereit.  
  
-   [SCHRITT 7: Installieren und Konfigurieren von 2-App1 @ no__t-0. 2 App1 ein Web-und Dateiserver im Netzwerk "2-Corpnet".  
  
-   [SCHRITT 8: Konfigurieren Sie INET1 @ no__t-0. INET1 simuliert das Internet in dieser Test Umgebungs Anleitung. Sie müssen einen DNS-Eintrag konfigurieren, der in die öffentliche IP-Adresse von 2-Edge1 aufgelöst wird.  
  
-   [SCHRITT 9: Konfigurieren Sie Edge1 @ no__t-0. Konfigurieren Sie den DNS-Server 2-Corpnet und das Routing auf Edge1.  
  
-   [SCHRITT 10: Installieren und Konfigurieren von 2-Edge1 @ no__t-0. Bei einer Bereitstellung mit mehreren Standorten sind zwei Remote Zugriffs Server erforderlich. 2 Edge1 bietet Remote Zugriffs Dienste für die zweite Domäne.  
  
-   [SCHRITT 11: Konfigurieren Sie die Bereitstellung für mehrere Standorte @ no__t-0. Nach dem Konfigurieren von Remote Zugriffs Servern können Sie die Bereitstellung für mehrere Standorte konfigurieren.  
  
-   [SCHRITT 12: Testen Sie die DirectAccess-Konnektivität @ no__t-0. Testen Sie die DirectAccess-Konnektivität von beiden Client Computern aus dem Subnetz Internet über Edge1 und 2-Edge1.  
  
-   [SCHRITT 13: Testen Sie die DirectAccess-Konnektivität hinter einem NAT-Gerät @ no__t-0. Testen Sie die DirectAccess-Konnektivität hinter einem NAT-Gerät.  
  
-   [SCHRITT 14: Momentaufnahme der Konfiguration @ no__t-0. Nachdem Sie die Testumgebung abgeschlossen haben, erstellen Sie eine Momentaufnahme der funktionierenden Remote Zugriffs Bereitstellung für mehrere Standorte, damit Sie Sie später wieder aufrufen können, um weitere Szenarios zu testen.  
  


