---
title: Wechseln zwischen Modi
description: Erfahren Sie, wie Sie in Multipoint Services zwischen dem Stations-und Konsolenmodus wechseln.
ms.custom: na
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5f1b2324-c1b0-4b61-ab51-39af15e7792a
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 08/04/2016
ms.openlocfilehash: 181324bff3227f7b071b8ae32f756d365b059a74
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71389242"
---
# <a name="switch-between-modes"></a>Wechseln zwischen Modi
Der Multipoint-Manager umfasst die folgenden Modi, die Ihnen bei der Ausführung verschiedener Typen der Multipoint Services-Systemverwaltung helfen:  
  
-   *Stations Modus*: Standardmäßig wird das Multipoint Services-System im Stations Modus gestartet. Im Stationsmodus weisen die MultiPoint Server-Stationen folgendes Verhalten auf: Jede Station wird als separater Computer mit Windows ausgeführt, und das System kann von mehreren Benutzern gleichzeitig verwendet werden. Sie und Ihre Benutzer können Dateien freigeben und die erforderlichen Aufgaben erledigen.  
  
-   *Konsolenmodus*: Wenn sich das Multipoint Services-System im Konsolenmodus befindet, können Sie Software und Treiber installieren und aktualisieren oder andere Wartungs Tasks ausführen. Im Konsolenmodus sind keine anderen *Stationen* zur Verwendung durch andere Computerbenutzer verfügbar. Solche Stationen werden nicht im Multipoint-Manager angezeigt. Alle Monitore, die direkt mit dem Server verbunden sind, werden als Anzeige dieses Computer Systems behandelt.   
  
> [!NOTE]
> Um den Start des Systems im Konsolenmodus zu erzwingen, ändern Sie die Standardeinstellung in den Einstellungen für den Server.  
> ## <a name="to-switch-from-station-mode-to-console-mode"></a>So wechseln Sie aus dem Stationsmodus in den Konsolenmodus  
  
1.  Öffnen Sie den Multipoint-Manager im Stations Modus, und klicken Sie dann auf die Registerkarte **Start** .  
  
2.  Klicken Sie in der Spalte **Computer** auf den Computer, für den Sie den Modus ändern möchten.  
  
3.  Klicken Sie unter *Computernamen* **Tasks** **auf zum Konsolenmodus wechseln**. Der Computer wird neu gestartet, und keine Station ist mehr verfügbar.  
  
## <a name="to-switch-from-console-mode-to-station-mode"></a>So wechseln Sie aus dem Konsolenmodus in den Stationsmodus  
  
1.  Öffnen Sie den Multipoint-Manager im Konsolenmodus, und klicken Sie dann auf die Registerkarte **Start** .  
  
2.  Klicken Sie in der Spalte **Computer** auf den Computer, für den Sie den Modus ändern möchten.  
  
3.  Klicken Sie unter *Computernamen* **Tasks** **auf in den Stations Modus wechseln**. Der Computer wird neu gestartet, und alle Stationen sind verfügbar.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Systemaufgaben mithilfe des MultiPoint-Managers](Manage-System-Tasks-Using-MultiPoint-Manager.md)