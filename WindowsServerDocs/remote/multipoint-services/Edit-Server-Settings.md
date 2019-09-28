---
title: Bearbeiten von Servereinstellungen
description: Weitere Informationen zu Multipoint Services-Einstellungen
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: afb64b94-9055-4703-b8ce-a8839b2718da
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: 5973bf6a23d0ce3f91620eaa3537f751ec19303c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389688"
---
# <a name="edit-server-settings"></a>Bearbeiten von Servereinstellungen
Während der Installation von MultiPoint Services haben Sie Einstellungen für das System konfiguriert, einschließlich Einstellungen für die Teilnahme an bestimmten Programmen. In diesem Thema werden die Einstellungen, die Sie für das MultiPoint Services-System festlegen können, und die Möglichkeiten zu ihrer Bearbeitung beschrieben.  
  
## <a name="about-multipoint-services-settings"></a>Informationen zu MultiPoint Services-Einstellungen  
In der folgenden Tabelle werden die verschiedenen Einstellungen für das MultiPoint Services-System beschrieben, die Sie ändern können.  
  
|MultiPoint Services-Einstellung|Beschreibung|  
|-----------------------------------------------------------------------------------------|---------------|  
|Zulassen mehrerer Sitzungen für ein Konto|Erlaubt einem einzelnen Benutzerkonto, gleichzeitig an mehreren Stationen angemeldet zu sein. Dies kann z.B. in Situationen wie Schulungen nützlich sein, in denen alle Teilnehmer gemeinsam ein einziges Konto verwenden. Mithilfe dieser Einstellung stehen alle Änderungen an den Kontoressourcen, wie Dokumentordner oder der Desktop, allen mit dem gleichen Konto angemeldeten Benutzern zur Verfügung.|  
|Eine Remoteverwaltung dieses Computers erlauben|Ermöglicht die Verwaltung des Computers, auf dem Multipoint Services ausgeführt wird, von anderen Multipoint-Systemen im Netzwerk. Wenn diese Option ausgewählt ist und sich der verwaltende Computer auf dem gleichen Subnetz befindet, erscheint dieser Computer in der Liste der verfügbaren zu verwaltenden Server. Wenn diese Option ausgewählt ist und sich der verwaltende Computer auf einem anderen Subnetz befindet, kann der verwaltende Computer diesen Computer trotzdem verwalten, Sie müssen jedoch die IP-Adresse des Computers angeben.|
|Überwachung der Desktops dieses Computers zulassen|Ermöglicht Ihnen, festzulegen, ob Desktops auf dem MultiPoint Services-System überwacht werden können. Wenn diese Einstellung deaktiviert (nicht ausgewählt) ist, werden Desktops von Stationen (sowohl lokal als auch Remote), die mit dem Computer verbunden sind, auf dem Multipoint Services ausgeführt wird, nicht auf der Registerkarte Start des Multipoint-Managers angezeigt (auch auf einem anderen Computer, wenn der Computer Remote verwaltet).|  
|Immer im Konsolenmodus starten|Aktiviert die RemoteFX-Technologie, die darauf ausgelegt ist, durch das Auslagern von Prozessen auf die CPU und die GPU schnellere und effizientere Remotedesktopsitzungen zu ermöglichen. Wenn Sie mithilfe eines remotefx-fähigen Clients eine Verbindung mit Multipoint Services herstellen, können Sie mit dieser Option möglicherweise eine bessere Leistung erzielen. Die Vorteile richten sich nach den Fähigkeiten Ihres Servers und Netzwerks. Ein Aspekt beispielsweise ist, ob für die zusätzliche Verarbeitung zum Komprimieren des Datenstroms weniger Zeit erforderlich ist, als durch das Übertragen einer kleineren Datenmenge eingespart wird.|  
|Datenschutzerklärung nicht bei der ersten Anmeldung des Benutzers anzeigen|Wenn ein Benutzer sich zum ersten Mal an einer MultiPoint-Station anmeldet, wird eine Benachrichtigung angezeigt, die den Benutzer darüber informiert, dass die auf der Station ausgeführten Aktivitäten möglicherweise überwacht werden.|  
|Zuweisen einer eindeutigen IP zu jeder Station|Weist jeder Station eine eindeutige IP-Station zu. Standardmäßig verfügt MultiPoint Services über eine IP-Adresse, die von allen auf dem System ausgeführten Sitzungen gemeinsam verwendet wird. Diese Konfiguration kann jedoch einige Probleme mit der Anwendungskompatibilität verursachen. Wenn eine Anwendung z.B. eine eindeutige IP-Adresse benötigt, wird die Anwendung in MultiPoint Services möglicherweise nicht ordnungsgemäß ausgeführt. Durch das Aktivieren dieser Option, auch als IP-Virtualisierung bezeichnet, kann dieses Problem behoben werden.<br /><br />Die IP-Virtualisierung ist auch für das Überwachen von aktiven Sitzungen in MultiPoint Services nützlich. Einige Überwachungstools melden Nutzungsinformationen anhand der IP-Adresse. Zum Aktivieren der Sitzungsüberwachung können Sie in diesen Fällen die IP-Virtualisierung verwenden, um jeder Sitzung eine eindeutige IP-Adresse zuzuweisen. Hinweis: Wenn Sie diese Option aktivieren, erhält jede neue Sitzung eine eindeutige IP-Adresse. Alle vorhandenen Sitzungen verwenden weiterhin die gemeinsam genutzte IP-Adresse, bis sie abgemeldet und erneut angemeldet werden.|  
|Chatunterhaltungen zwischen dem MultiPoint-Dashboard und einer Benutzersitzung auf diesem Computer zulassen|Ermöglicht Chats zwischen einem Benutzer im MultiPoint-Manager und einem Benutzer in einer Benutzersitzung auf diesem Computer. Weitere Informationen finden Sie unter [Kommunizieren mit Chat](Use-IM.md).|  
|Orchestrierung von Administrator- und MultiPoint-Dashboard-Benutzersitzungen zulassen|Ermöglicht bei Aktivierung Administratoren die Verwendung des MultiPoint-Dashboards für die Orchestrierung von Sitzungen. Diese Sitzungen werden als Miniaturansichten angezeigt.|  
|Stationen die Verwendung von GPU-Hardwarerendering ermöglichen|Steuert, ob Stationen die GPU des Systems verwenden können.|   
  
## <a name="editing-the-computer-settings"></a>Bearbeiten der Computereinstellungen  
  
1.  Öffnen Sie den Multipoint-Manager im [Stations Modus](Switch-Between-Modes.md), und klicken Sie dann auf die Registerkarte **Start** .  
  
2.  Klicken Sie in der Spalte **Computer** auf den Computernamen, und klicken Sie dann unter *Computername* **Tasks**auf **Computereinstellungen bearbeiten**.  
  
3.  Aktivieren oder löschen Sie die Elemente, die Sie ändern möchten, und klicken Sie dann auf **OK**.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Systemaufgaben mithilfe des MultiPoint-Managers](Manage-System-Tasks-Using-MultiPoint-Manager.md)  
  
