---
title: Deaktivieren der NAS-Notification-Weiterleitung auf dem Netzwerkrichtlinienserver
description: Dieses Thema enthält Anweisungen zum Konfigurieren des Netzwerkrichtlinienservers gleichzeitiger Authentifizierungen in Windows Server 2016.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: a09bfb03-95fc-4534-bf3c-97078ef6b07e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bc4c6afdcb02eb2bbab1f0373a5b3a28236269bf
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59882261"
---
# <a name="disable-nas-notification-forwarding-in-nps"></a>Deaktivieren der NAS-Notification-Weiterleitung auf dem Netzwerkrichtlinienserver

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, deaktivieren die Weiterleitung von starten und Beenden von Nachrichten von Netzwerkzugriffsservern (NAS) für Mitglieder einer remote-RADIUS-Servergruppe auf dem Netzwerkrichtlinienserver so konfiguriert.

Wenn Sie RADIUS-Remoteservergruppen konfiguriert haben und auf dem Netzwerkrichtlinienserver **Verbindungsanforderungsrichtlinien**, Sie deaktivieren die **kontoführungsanforderungen an diese remote-RADIUS-Servergruppe weiterleiten** Kontrollkästchen, um diese Gruppen sind weiterhin gesendeten NAS starten und Beenden von benachrichtigungsmeldungen. 

Dadurch wird die unnötigen Netzwerkdatenverkehr erstellt. Um diesen Datenverkehr zu vermeiden, deaktivieren Sie NAS-Benachrichtigung, die für einzelne Server an jeden RADIUS-Remoteservergruppe weiterleiten.

Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.

### <a name="to-disable-nas-notification-forwarding"></a>So deaktivieren Sie die Weiterleitung von NAS-Benachrichtigung

1. Klicken Sie im Server-Manager **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die NPS-Konsole wird geöffnet.

2. Doppelklicken Sie in der NPS-Konsole auf **RADIUS-Clients und Servern**, klicken Sie auf **RADIUS-Remoteservergruppen**, und doppelklicken Sie dann auf die remote-RADIUS-Servergruppe, die Sie konfigurieren möchten. Der RADIUS-Remoteservergruppe **Eigenschaften** Dialogfeld wird geöffnet.

3. Doppelklicken Sie auf das Mitglied der Gruppe, die Sie konfigurieren möchten, und klicken Sie dann auf die **Authentifizierung/Kontoführung** Registerkarte.

4. In **Accounting**Deaktivieren der **weiterleiten Network Access Server starten und Beenden von Benachrichtigungen an diesen Server** , und klicken Sie dann auf **OK**.

5. Wiederholen Sie die Schritte 3 und 4 für alle Mitglieder der Gruppe, die Sie konfigurieren möchten.

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerkrichtlinienservers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
