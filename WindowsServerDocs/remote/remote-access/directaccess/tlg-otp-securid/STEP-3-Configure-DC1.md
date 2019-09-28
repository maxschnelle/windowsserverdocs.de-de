---
title: Schritt 3 DC1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7655208fb537e78839f2b459c8df0e24c0573aa7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367549"
---
# <a name="step-3-configure-dc1"></a>Schritt 3 DC1 konfigurieren

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

DC1 fungiert als Domänen Controller, DNS-Server und DHCP-Server für die Corp.contoso.com-Domäne. Konfigurieren Sie DC1 wie folgt:  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Überprüfen, ob user1 einen Benutzer Prinzipal Namen auf DC1 definiert ist  
  
1.  Öffnen Sie auf DC1 Server-Manager, und klicken Sie im linken Bereich auf **AD DS** . Klicken Sie mit der rechten Maustaste auf **DC1** , und wählen Sie **Active Directory Benutzer und Computer** Erweitern Sie im linken Bereich **Corp. Configuration. com\users**, und doppelklicken Sie auf user1.  
  
2.  Überprüfen Sie auf der Registerkarte **Konto** , ob der **Benutzer Anmelde Name** auf user1 festgelegt ist. Wenn dies nicht der Wert ist, geben Sie **User1** in das Feld **Benutzer Anmelde Name** ein.  
  
3.  Klicken Sie auf **OK**. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer** .  
  


