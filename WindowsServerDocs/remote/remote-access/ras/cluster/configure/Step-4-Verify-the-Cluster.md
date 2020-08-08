---
title: Schritt 4 Überprüfen des Clusters
description: Dieses Thema ist Teil des Handbuchs Bereitstellen des Remote Zugriffs in einem Cluster unter Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: f22dcf10-b453-4664-a9ef-e40e95c72f63
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 4fa053519116ddadbe1469223001a33384aebe91
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87963896"
---
# <a name="step-4-verify-the-cluster"></a>Schritt 4 Überprüfen des Clusters

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen, ob Sie die DirectAccess-Cluster Bereitstellung richtig konfiguriert haben.

### <a name="to-verify-access-to-internal-resources-through-the-cluster"></a>So überprüfen Sie den Zugriff auf interne Ressourcen über den Cluster

1.  Einen DirectAccess-Client-Computer mit dem Unternehmensnetzwerk herstellen und die Gruppenrichtlinie zu erhalten.

2.  Verbinden Sie des Clientcomputers mit dem externen Netzwerk ein, und versuchen Sie den Zugriff auf interne Ressourcen.

    Sie sollten auf alle Unternehmensressourcen zugreifen können.

3.  Testen Sie die Konnektivität über jeden Server im Cluster, indem Sie die Verbindung mit dem externen Netzwerk ausschalten oder trennen, bis auf einen der Cluster Server. Versuchen Sie auf dem Client Computer, auf Unternehmensressourcen zuzugreifen. Wiederholen Sie den Test auf einem anderen Cluster Server.

    Sie sollten in der Lage sein, über jeden Cluster Server auf alle Unternehmensressourcen zuzugreifen.



