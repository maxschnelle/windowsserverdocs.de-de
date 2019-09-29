---
title: Schritt 8 Konfigurieren von INET1
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen einer DirectAccess-Bereitstellung für mehrere Standorte für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 693acb5c-dffc-4484-8286-163bb67724c9
ms.author: coreyp
author: coreyp-at-msft
ms.openlocfilehash: 54674adc33f45a58f2515d07fed4c8a070ded5a1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404710"
---
# <a name="step-8-configure-inet1"></a>SCHRITT 8: Konfigurieren von INET1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Damit Client Computer eine Verbindung mit RAS-Servern über das Internet herstellen können, müssen Sie einen DNS-Eintrag für 2-Edge1 auf INET1 konfigurieren.  
  
### <a name="to-create-the-2-edge1-dns-entry"></a>So erstellen Sie den 2 Edge1-DNS-Eintrag  
  
1.  Geben Sie auf der **Start** Seite**dnsmgmt. msc**ein, und drücken Sie dann die EINGABETASTE.  
  
2.  Öffnen Sie in der Konsolen Struktur **Forward-Lookupzonen**, klicken Sie auf **contoso.com**, klicken Sie mit der rechten Maustaste auf **contoso.com**, und klicken Sie dann auf **neuer Host (A oder AAAA)** .  
  
3.  Geben Sie unter **Name den Namen** **2-Edge1**ein. Geben Sie unter **IP-Adresse**den Namen **131.107.0.20**ein. Klicken Sie auf **Host hinzufügen**, klicken Sie auf **OK**, und klicken Sie dann auf **Fertig**.  
  


