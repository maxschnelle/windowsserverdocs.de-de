---
title: Schritt 8 Konfigurieren von INET1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess Multisite-Bereitstellung für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: d6967b975b3a950c90de465872832d623755a494
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281416"
---
# <a name="step-8-configure-inet1"></a>SCHRITT 8: Konfigurieren von INET1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Um-Clientcomputern über das Internet eine Verbindung zum RAS-Server zu aktivieren, müssen Sie einen DNS-Eintrag für die 2-EDGE1 auf INET1 konfigurieren.  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>Den 2-EDGE1 DNS-Eintrag erstellen  
  
1.  Auf der **starten** geben**dnsmgmt.msc**, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie in der Konsolenstruktur **Forward-Lookupzonen**, klicken Sie auf **"contoso.com"** , klicken Sie dann mit der rechten Maustaste **"contoso.com"** , und klicken Sie dann auf **neuer Host (A oder AAAA)** .  
  
3.  In **Namen**, Typ **2-EDGE1**. In **IP-Adresse**, Typ **131.107.0.20**. Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.  
  


