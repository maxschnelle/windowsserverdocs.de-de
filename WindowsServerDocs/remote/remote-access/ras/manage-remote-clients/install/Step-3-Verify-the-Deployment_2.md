---
title: Schritt 3 Überprüfen der Bereitstellung
description: Dieses Thema ist Teil des Handbuchs zur Remote Verwaltung von DirectAccess-Clients in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6a78a078-d2e7-4cbd-b8d5-20cfb6d1524b
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 81ac8bf7321df915330d8d706fa5ba3912b8f54c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367295"
---
# <a name="step-3-verify-the-deployment"></a>Schritt 3 Überprüfen der Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen, ob die Bereitstellung für die Remote Verwaltung von DirectAccess-Clients ordnungsgemäß konfiguriert wurde.  
  
### <a name="to-verify-proper-deployment"></a>So überprüfen  
  
1.  Verbinden eines DirectAccess-Client Computers mit dem Unternehmensnetzwerk und Abrufen des Gruppenrichtlinie Objekts.  
  
2.  Klicken Sie auf dem Client Computer im Benachrichtigungsbereich auf das Symbol **Netzwerkverbindungen** , um auf den DirectAccess-Medien-Manager zuzugreifen.  
  
3.  Klicken Sie auf **DirectAccess-Verbindung**, und Sie werden feststellen, dass der Status **Lokal verbunden**ist.  
  
4.  Entfernen Sie den Computer aus dem Unternehmensnetzwerk, und verbinden Sie ihn mit einem öffentlichen Netzwerk.  
  
5.  Geben Sie an einer Eingabeaufforderung **nltest/dsgetdc: [voll qualifizierter Domänen Name]** ein. Mit diesem Befehl wird überprüft, ob der Client über das Unternehmensnetzwerk erreichbar ist. Wenn auf den Domänen Controller nicht zugegriffen werden kann, wird in der folgenden Fehlermeldung angezeigt, dass die Domäne nicht vorhanden ist: ERROR_NO_SUCH_DOMAIN.  
  


