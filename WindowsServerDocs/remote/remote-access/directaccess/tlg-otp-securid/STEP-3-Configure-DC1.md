---
title: Schritt 3 Konfigurieren von DC1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 338e214ac10796d3f9864aef74190f2d27f173b7
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281355"
---
# <a name="step-3-configure-dc1"></a>Schritt 3 Konfigurieren von DC1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

DC1 fungiert als Domänencontroller, DNS-Server und DHCP-Server für die Domäne "corp.contoso.com". Konfigurieren Sie DC1 wie folgt:  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Stellen Sie sicher, dass "user1" ein Benutzerprinzipalname auf DC1 definiert ist  
  
1.  Klicken Sie auf DC1 öffnen Sie Server-Manager, und klicken Sie auf **AD DS** im linken Bereich. Mit der rechten Maustaste **DC1** , und wählen Sie **Active Directory-Benutzer und-Computer**. Erweitern Sie im linken Bereich **corp.contoso.com\Users**, und doppelklicken Sie auf "user1".  
  
2.  Auf der **Konto** Registerkarte überprüfen Sie, ob **Benutzeranmeldename** auf "user1" festgelegt ist. Wenn dies nicht der Fall, geben Sie **"user1"** in die **Benutzeranmeldename** Feld.  
  
3.  Klicken Sie auf **OK**. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer** .  
  


