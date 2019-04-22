---
title: Schritt 4 Überprüfen des Clusters
description: Dieses Thema ist Teil des Leitfadens Bereitstellen des Remotezugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f22dcf10-b453-4664-a9ef-e40e95c72f63
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b449197265befb7caf7d8d3a5b56accf5c52aef9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821841"
---
# <a name="step-4-verify-the-cluster"></a>Schritt 4 Überprüfen des Clusters

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt, wie Sie sicher, dass Sie die DirectAccess-Clusterbereitstellung ordnungsgemäß konfiguriert haben.  
  
### <a name="to-verify-access-to-internal-resources-through-the-cluster"></a>Um den Zugriff auf interne Ressourcen über den Cluster überprüfen  
  
1.  Stellen Sie eine Verbindung von einem DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk her, und rufen Sie die Gruppenrichtlinie ab.  
  
2.  Verbinden Sie den Clientcomputer mit dem externen Netzwerk, und versuchen Sie, auf interne Ressourcen zuzugreifen.  
  
    Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  
3.  Testen der Konnektivität über jeden Server im Cluster durch das Deaktivieren oder Trennen der Verbindung aus dem externen Netzwerk, alle bis auf eines der Clusterserver. Versuchen Sie auf dem Clientcomputer auf Unternehmensressourcen zugreifen. Wiederholen Sie den Test auf einem anderen Cluster-Server aus.  
  
    Sie sollten alle Unternehmensressourcen über auf jedem Clusterserver zugreifen können.  
  


