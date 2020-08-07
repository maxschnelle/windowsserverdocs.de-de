---
title: Schritt 3 DC1 konfigurieren
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: 836a2a08-3d22-48d2-873e-80d7e57ebbd6
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 254789f18ca1adeebed227081c8177dc3c706e3d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971687"
---
# <a name="step-3-configure-dc1"></a>Schritt 3 DC1 konfigurieren

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

DC1 fungiert als Domänen Controller, DNS-Server und DHCP-Server für die Corp.contoso.com-Domäne. Konfigurieren Sie DC1 wie folgt:

## <a name="verify-user1-has-a-user-principal-name-defined-on-dc1"></a>Überprüfen, ob user1 einen Benutzer Prinzipal Namen auf DC1 definiert ist

1.  Öffnen Sie auf DC1 Server-Manager, und klicken Sie im linken Bereich auf **AD DS** . Klicken Sie mit der rechten Maustaste auf **DC1** , und wählen Sie **Active Directory Benutzer und Computer** Erweitern Sie im linken Bereich **Corp. Configuration. com\users**, und doppelklicken Sie auf user1.

2.  Überprüfen Sie auf der Registerkarte **Konto** , ob der **Benutzer Anmelde Name** auf user1 festgelegt ist. Wenn dies nicht der Wert ist, geben Sie **User1** in das Feld **Benutzer Anmelde Name** ein.

3.  Klicken Sie auf **OK**. Schließen Sie die Konsole **Active Directory-Benutzer und -Computer**.



