---
title: Schritt 3 DC1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 07167f2bc68ab8c465a96ce00552339d04dbb198
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80856073"
---
# <a name="step-3-configure-dc1"></a>Schritt 3 DC1 konfigurieren

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

DC1 fungiert als Domänen Controller, DNS-Server und DHCP-Server für die Corp.contoso.com-Domäne. Konfigurieren Sie DC1 wie folgt:  
  
## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Überprüfen, ob user1 einen Benutzer Prinzipal Namen auf DC1 definiert ist  
  
1.  Öffnen Sie auf DC1 Server-Manager, und klicken Sie im linken Bereich auf **AD DS** . Klicken Sie mit der rechten Maustaste auf **DC1** , und wählen Sie **Active Directory Benutzer und Computer** Erweitern Sie im linken Bereich **Corp. Configuration. com\users**, und doppelklicken Sie auf user1.  
  
2.  Überprüfen Sie auf der Registerkarte **Konto** , ob der **Benutzer Anmelde Name** auf user1 festgelegt ist. Wenn dies nicht der Wert ist, geben Sie **User1** in das Feld **Benutzer Anmelde Name** ein.  
  
3.  Klicken Sie auf **OK**. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer**.  
  


