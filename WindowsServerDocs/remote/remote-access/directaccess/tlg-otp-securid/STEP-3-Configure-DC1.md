---
title: Schritt 3 Konfigurieren von DC1
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b1762fe6e5a98529956208c4c807dfeb39c439cd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59875741"
---
# <a name="step-3-configure-dc1"></a>Schritt 3 Konfigurieren von DC1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

DC1 fungiert als Domänencontroller, DNS-Server und DHCP-Server für die Domäne "corp.contoso.com". Konfigurieren Sie DC1 wie folgt:  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Stellen Sie sicher, dass "user1" ein Benutzerprinzipalname auf DC1 definiert ist  
  
1.  Klicken Sie auf DC1 öffnen Sie Server-Manager, und klicken Sie auf **AD DS** im linken Bereich. Mit der rechten Maustaste **DC1** , und wählen Sie **Active Directory-Benutzer und-Computer**. Erweitern Sie im linken Bereich **corp.contoso.com\Users**, und doppelklicken Sie auf "user1".  
  
2.  Auf der **Konto** Registerkarte überprüfen Sie, ob **Benutzeranmeldename** auf "user1" festgelegt ist. Wenn dies nicht der Fall, geben Sie **"user1"** in die **Benutzeranmeldename** Feld.  
  
3.  Klicken Sie auf **OK**. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer** .  
  


