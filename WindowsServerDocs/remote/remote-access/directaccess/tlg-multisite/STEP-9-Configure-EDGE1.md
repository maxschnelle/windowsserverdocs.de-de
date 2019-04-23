---
title: Schritt 9 Konfigurieren von EDGE1
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
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f5d216934f0d09cdef97ce4405161862b112d632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864871"
---
# <a name="step-9-configure-edge1"></a>Schritt 9 Konfigurieren von EDGE1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die folgenden Verfahren werden auf dem Server EDGE1 ausgeführt:  
  
1. Konfigurieren Sie die DNS-Server, auf EDGE1. Es ist erforderlich, den DNS-Server aus der Domäne corp2.corp.contoso.com auf EDGE1 zu konfigurieren.  
  
2. Konfigurieren des Routings zwischen Subnetzen. Konfigurieren von routing auf EDGE1 zum Aktivieren der Kommunikation zwischen den Subnetzen "Corpnet" und "2-Corpnet".  
  
## <a name="IPv6"></a>Konfigurieren Sie die DNS-Server auf EDGE1  
  
1.  Klicken Sie in der Server-Manager-Konsole auf **lokalen Server**, und klicken Sie dann in der **Eigenschaften** Bereich, der neben **"Corpnet"**, klicken Sie auf den Link.  
  
2.  Im Fenster Netzwerkverbindungen mit der Maustaste **"Corpnet"**, und klicken Sie dann auf **Eigenschaften**.  
  
3.  Klicken Sie auf **Internetprotokoll Version 4 (TCP/IPv4)**, und klicken Sie dann auf **Eigenschaften**.  
  
4.  In **alternativer DNS-Server**, Typ **10.2.0.1**. ein, und klicken Sie dann auf **OK**.  
  
5.  Klicken Sie auf **Internetprotokoll Version 6 (TCP/IPv6)**, und klicken Sie dann auf **Eigenschaften**.  
  
6.  In **alternativer DNS-Server**, Typ **2001:db8:2::1** , und klicken Sie dann auf **OK**.  
  
7.  Auf der **Corpnet Eigenschaften** Dialogfeld klicken Sie auf **schließen**.  
  
8.  Schließen Sie das Fenster **Netzwerkverbindungen**.  
  
## <a name="ConfigRouting"></a>Konfigurieren des Routings zwischen Subnetzen  
  
1.  Auf der **starten** geben**cmd.exe**, mit der rechten Maustaste **Cmd**, klicken Sie auf **erweitert**, und klicken Sie dann auf **Ausführen als Administrator**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
2.  Geben Sie im Eingabeaufforderungsfenster Befehl die folgenden Befehle aus. Drücken Sie nach der Eingabe jedes Befehls die EINGABETASTE.  
  
    ```  
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254  
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe  
    ```  
  
3.  Schließen Sie das Eingabeaufforderungsfenster.  
  


