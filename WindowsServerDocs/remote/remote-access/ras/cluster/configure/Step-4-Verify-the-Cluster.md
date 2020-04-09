---
title: Schritt 4 Überprüfen des Clusters
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: f22dcf10-b453-4664-a9ef-e40e95c72f63
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c31db158856eb3c3881a36c29e40d1227116201f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855263"
---
# <a name="step-4-verify-the-cluster"></a>Schritt 4 Überprüfen des Clusters

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen, ob Sie die DirectAccess-Cluster Bereitstellung richtig konfiguriert haben.  
  
### <a name="to-verify-access-to-internal-resources-through-the-cluster"></a>So überprüfen Sie den Zugriff auf interne Ressourcen über den Cluster  
  
1.  Stellen Sie eine Verbindung von einem DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk her, und rufen Sie die Gruppenrichtlinie ab.  
  
2.  Verbinden Sie den Clientcomputer mit dem externen Netzwerk, und versuchen Sie, auf interne Ressourcen zuzugreifen.  
  
    Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  
3.  Testen Sie die Konnektivität über jeden Server im Cluster, indem Sie die Verbindung mit dem externen Netzwerk ausschalten oder trennen, bis auf einen der Cluster Server. Versuchen Sie auf dem Client Computer, auf Unternehmensressourcen zuzugreifen. Wiederholen Sie den Test auf einem anderen Cluster Server.  
  
    Sie sollten in der Lage sein, über jeden Cluster Server auf alle Unternehmensressourcen zuzugreifen.  
  


