---
title: Schritt 4 Konfigurieren von APP1
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
ms.assetid: 7000e80f-31b1-43c5-b51e-1469d26909e5
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ccfac583f64d40012881a2d3f6a0897beb16c02a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867221"
---
# <a name="step-4-configure-app1"></a>Schritt 4 Konfigurieren von APP1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Konfigurieren Sie statische IPv6-Adressierung und Gateway-Einstellungen zum Aktivieren des APP1-Zugriffs auf das 2-Corpnet-Subnetz.  
  
- Das Standardgateway und DNS-Server zu konfigurieren. Die Konfiguration für mehrere Standorte verwendet der ROUTER1-Computer als Standard-Gateway. Konfigurieren Sie die Standard-Gateway auf dem Computer APP1 an.  
  
## <a name="to-configure-the-default-gateway-and-dns-server"></a>So konfigurieren Sie das Standardgateway und DNS-server  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **verkabelte Ethernetverbindung**, klicken Sie auf den Link.  
  
2.  In der **Netzwerkverbindungen** Fenster mit der rechten Maustaste **verkabelte Ethernetverbindung**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Auf der **Verbindungseigenschaften von Ethernetkabelverbindung** Dialogfeld klicken Sie auf **Internet Protocol Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  In **Standardgateway**, Typ **10.0.0.254**, und klicken Sie in **alternativer DNS-Server**, Typ **10.2.0.1**, und klicken Sie dann auf **OK** .  
  
5.  Auf der **Verbindungseigenschaften von Ethernetkabelverbindung** Dialogfeld klicken Sie auf **Internet Protocol Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
6.  In **Standardgateway**, Typ **2001:db8:1::fe**. In **alternativer DNS-Server**, Typ **2001:db8:2::1**, und klicken Sie dann auf **OK**.  
  
7.  Auf der **Verbindungseigenschaften von Ethernetkabelverbindung** Dialogfeld klicken Sie auf **schließen**, und schließen Sie dann die **Netzwerkverbindungen** Fenster.  
  


