---
title: Schritt 8 Konfigurieren von INET1
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
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: 707591604a1d030b3abba9395081d2c2e4b7fb1c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838811"
---
# <a name="step-8-configure-inet1"></a>SCHRITT 8: Konfigurieren von INET1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Um-Clientcomputern über das Internet eine Verbindung zum RAS-Server zu aktivieren, müssen Sie einen DNS-Eintrag für die 2-EDGE1 auf INET1 konfigurieren.  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>Den 2-EDGE1 DNS-Eintrag erstellen  
  
1.  Auf der **starten** geben**dnsmgmt.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie in der Konsolenstruktur **Forward-Lookupzonen**, klicken Sie auf **"contoso.com"**, klicken Sie dann mit der rechten Maustaste **"contoso.com"**, und klicken Sie dann auf **neuer Host (A oder AAAA)**.  
  
3.  In **Namen**, Typ **2-EDGE1**. In **IP-Adresse**, Typ **131.107.0.20**. Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.  
  


