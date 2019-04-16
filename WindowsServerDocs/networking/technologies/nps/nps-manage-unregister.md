---
title: Heben Sie die Registrierung eines NPS-Servers aus Active Directory-Domäne
description: In diesem Thema können Sie um einen Server mit der Netzwerkrichtlinienserver in Windows Server2016 in der Standarddomäne des NPS-Server oder in einer anderen Domäne registrieren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 55c3b00146706831351ce63d1e5b74f45d7b9be1
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="unregister-an-nps-server-from-an-active-directory-domain"></a>Heben Sie die Registrierung eines NPS-Servers aus Active Directory-Domäne

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Verwalten von der Bereitstellung des NPS-Server, könnten Sie finden es nützlich, verschieben Sie einen NPS-Server zu einer anderen Domäne, ersetzen Sie einen NPS-Server oder einen NPS-Server abkoppeln. 

Beim Verschieben oder einen NPS-Server außer Betrieb setzen, können Sie den NPS-Server in Active Directory-Domänen Registrierung aufheben, in dem der NPS-Server über die Berechtigung zum Lesen der Eigenschaften von Benutzerkonten in Active Directory verfügt.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

## <a name="to-unregister-an-nps-server"></a>Aufheben der Registrierung ein NPS-Servers

1. Klicken Sie auf dem Domänencontroller im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.

2. Klicken Sie auf **Benutzer**, und doppelklicken Sie dann auf **RAS- und IAS-Server**.

3. Klicken Sie auf die **Mitglieder** Registerkarte, und wählen Sie den NPS-Server, die Sie aufheben möchten.

4. Klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie dann auf **OK**.

