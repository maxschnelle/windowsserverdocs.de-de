---
title: Aufheben der Registrierung eines NPS aus einer Active Directory-Domäne
description: Sie können in diesem Thema verwenden, um einen Server Network Policy Server in Windows Server 2016 in der NPS-Standarddomäne oder in einer anderen Domäne zu registrieren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 68a94616-3c29-45bd-bd33-e4c578f119e1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8fe4773efd89aeb413b3793f874ad6a1b030294a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864351"
---
# <a name="unregister-an-nps-from-an-active-directory-domain"></a>Aufheben der Registrierung eines NPS aus einer Active Directory-Domäne

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Bei der Verwaltung von der NPS-Bereitstellung, finden Sie es möglicherweise sinnvoll, ein NPS in einer anderen Domäne, ein NPS ersetzt oder so Koppeln Sie einen NPS zu verschieben. 

Wenn Sie verschoben oder außer Betrieb einen NPS nehmen, können Sie den NPS in den Active Directory-Domänen Registrierung aufheben, in dem der NPS über die Berechtigung zum Lesen der Eigenschaften von Benutzerkonten in Active Directory hat.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

## <a name="to-unregister-an-nps"></a>Beim Aufheben der Registrierung ein NPS

1. Klicken Sie auf dem Domänencontroller im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.

2. Klicken Sie auf **Benutzer**, und doppelklicken Sie dann auf **RAS- und IAS-Server**.

3. Klicken Sie auf die **Mitglieder** Registerkarte, und wählen Sie dann auf den NPS, die Sie aufheben möchten.

4. Klicken Sie auf **entfernen**, klicken Sie auf **Ja**, und klicken Sie dann auf **OK**.

