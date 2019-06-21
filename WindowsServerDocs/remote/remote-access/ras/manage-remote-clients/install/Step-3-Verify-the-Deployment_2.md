---
title: Schritt 3 Überprüfen der Bereitstellung
description: Dieses Thema ist Teil des Leitfadens verwalten DirectAccess-Clients Remote in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8d2b0b27d4b1d33971564672954667b49a87a4e0
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67282767"
---
# <a name="step-3-verify-the-deployment"></a>Schritt 3 Überprüfen der Bereitstellung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt, wie Sie sicher, dass Sie die Bereitstellung für die Remoteverwaltung von DirectAccess-Clients ordnungsgemäß konfiguriert haben.  
  
### <a name="to-verify-proper-deployment"></a>So überprüfen ordnungsgemäße Bereitstellung.  
  
1.  Einen DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk herstellen, und das Gruppenrichtlinienobjekt zu erhalten.  
  
2.  Klicken Sie auf dem Clientcomputer auf die **Netzwerkverbindungen** Symbol im Infobereich der Taskleiste auf dem DirectAccess-Medienverwaltung zuzugreifen.  
  
3.  Klicken Sie auf **DirectAccess-Verbindung**, und Sie sehen, dass der Status **lokal verbundenen**.  
  
4.  Entfernen Sie den Computer aus dem Unternehmensnetzwerk, und verbinden Sie es mit einem öffentlichen Netzwerk.  
  
5.  Geben Sie an einer Eingabeaufforderung den Befehl **Nltest/dsgetdc: [vollständig qualifizierter Domänenname]** . Dieser Befehl prüft, ob im Unternehmensnetzwerk an den Client verfügbar ist. Ist der Domänencontroller nicht zugegriffen werden kann, wird die folgende Fehlermeldung angezeigt, Berichten, die die Domäne nicht vorhanden ist: ERROR_NO_SUCH_DOMAIN.  
  


