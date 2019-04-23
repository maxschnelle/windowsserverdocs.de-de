---
title: Schritt 3 Überprüfen der Bereitstellung
description: Dieses Thema ist Teil des Leitfadens verwalten DirectAccess-Clients Remote in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 89b9e53b7321ebeddda50a448829ad73395eeed0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835611"
---
# <a name="step-3-verify-the-deployment"></a>Schritt 3 Überprüfen der Bereitstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt, wie Sie sicher, dass Sie die Bereitstellung für die Remoteverwaltung von DirectAccess-Clients ordnungsgemäß konfiguriert haben.  
  
### <a name="to-verify-proper-deployment"></a>So überprüfen ordnungsgemäße Bereitstellung.  
  
1.  Einen DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk herstellen, und das Gruppenrichtlinienobjekt zu erhalten.  
  
2.  Klicken Sie auf dem Clientcomputer auf die **Netzwerkverbindungen** Symbol im Infobereich der Taskleiste auf dem DirectAccess-Medienverwaltung zuzugreifen.  
  
3.  Klicken Sie auf **DirectAccess-Verbindung**, und Sie sehen, dass der Status **lokal verbundenen**.  
  
4.  Entfernen Sie den Computer aus dem Unternehmensnetzwerk, und verbinden Sie es mit einem öffentlichen Netzwerk.  
  
5.  Geben Sie an einer Eingabeaufforderung den Befehl **Nltest/dsgetdc: [vollständig qualifizierter Domänenname]**. Dieser Befehl prüft, ob im Unternehmensnetzwerk an den Client verfügbar ist. Ist der Domänencontroller nicht zugegriffen werden kann, wird die folgende Fehlermeldung angezeigt, Berichten, die die Domäne nicht vorhanden ist: ERROR_NO_SUCH_DOMAIN.  
  


