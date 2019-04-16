---
title: Deaktivieren der Weiterleitung von NAS-Benachrichtigung auf dem Netzwerkrichtlinienserver
description: Dieses Thema enthält Anweisungen zum Konfigurieren des Netzwerkrichtlinienservers gleichzeitiger Authentifizierungen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: c25f3b5a94624a35099e84ede3296f7ab860da7c
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>Deaktivieren der Weiterleitung von NAS-Benachrichtigung auf dem Netzwerkrichtlinienserver

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahren können Sie die Weiterleitung von Start deaktivieren und verhindern, dass Nachrichten Netzwerkzugriffsservern (NAS) für Mitglieder einer RADIUS-Remoteservergruppe in NPS konfiguriert.

Wenn Sie RADIUS-Remoteservergruppen konfiguriert haben und auf dem Netzwerkrichtlinienserver **Verbindungsanforderungsrichtlinien**, deaktivieren Sie die **kontoführungsanforderungen an diesem RADIUS-Remoteservergruppe weiterleiten** das Kontrollkästchen Diese Gruppen werden weiterhin NAS gesendet starten und Beenden von Benachrichtigungen. 

Dadurch entsteht unnötigen Netzwerkverkehr. Um diesen Datenverkehr zu vermeiden, deaktivieren Sie NAS-Benachrichtigung für einzelne Server an jeden RADIUS-Remoteservergruppe weiterleiten.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Administratoren** Gruppe.

### <a name="to-disable-nas-notification-forwarding"></a>So deaktivieren Sie die Weiterleitung von NAS-Benachrichtigung

1. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und Servern**, klicken Sie auf **RADIUS-Remoteservergruppen**, und doppelklicken Sie dann auf die RADIUS-Remoteservergruppe, die Sie konfigurieren möchten. Die RADIUS-Remoteservergruppe **Eigenschaften** Dialogfeld wird geöffnet.

3. Doppelklicken Sie auf das Mitglied der Gruppe, die Sie konfigurieren möchten, und klicken Sie dann auf die **Authentifizierung/Kontoführung** Registerkarte.

4. In **Accounting**Kontrollkästchen die **weiterleiten Network Access Server starten und Beenden von Benachrichtigungen an diesen Server** , und klicken Sie dann auf **OK**.

5. Wiederholen Sie die Schritte 3 und 4 für alle Mitglieder der Gruppe, die Sie konfigurieren möchten.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Netzwerkrichtlinienserver verwalten](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
