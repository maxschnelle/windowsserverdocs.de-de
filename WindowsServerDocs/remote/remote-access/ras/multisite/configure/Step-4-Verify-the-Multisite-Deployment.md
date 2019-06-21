---
title: Schritt 4 Überprüfen der Bereitstellung für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 345b676a-a397-4d51-9973-8b25bc05fa55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f186084e9d2dbeabbc560ce7631e7d63ff1b99b8
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67281033"
---
# <a name="step-4-verify-the-multisite-deployment"></a>Schritt 4 Überprüfen der Bereitstellung für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema beschreibt, wie Sie sicher, dass Sie Ihre Bereitstellung des Remotezugriffs für mehrere Standorte ordnungsgemäß konfiguriert haben.  
  
### <a name="to-verify-access-to-internal-resources-through-the-multisite-deployment"></a>Zum Überprüfen des Zugriffs auf interne Ressourcen über die Bereitstellung für mehrere Standorte  
  
1.  Stellen Sie eine Verbindung von einem DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk her, und rufen Sie die Gruppenrichtlinie ab.  
  
2.  Verbinden Sie den Clientcomputer mit dem externen Netzwerk, und versuchen Sie, auf interne Ressourcen zuzugreifen.  
  
    Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  
3.  Testen der Konnektivität über jeden Server in der Bereitstellung für mehrere Standorte durch das Deaktivieren oder aus dem externen Netzwerk, alle bis auf einen der RAS-Server trennen. Versuchen Sie auf dem Clientcomputer auf Unternehmensressourcen zugreifen. Wiederholen Sie den Test auf einem anderen Server für mit mehreren Standorten aus. Es dauert bis zu 10 Minuten für den Clientcomputer zur Verbindung mit des neuen Einstiegspunkts. Dies ist da Tests 10 Minuten als Einstiegspunkt ausgeschaltet ist, nachdem es ist nicht erreichbar, angesehen wird, um die Bandbreite und die Akkulaufzeit zu optimieren. Alternativ können Sie zwischen den verschiedenen Einstiegspunkten manuell, indem Sie eine gewünschte Einstiegspunkt-im Kombinationsfeld angezeigt wird, wenn die Ausführung wechseln **daprop.exe**.  
  
    Sie sollten auf alle Unternehmensressourcen über jeden Server für mehrere Standorte zugreifen können.  
  
4.  Verbinden Sie eine Windows 7&reg; Clientcomputer an das Unternehmen Netzwerk und die Gruppenrichtlinie zu erhalten.  
  
5.  Verbinden Sie den Windows 7-Clientcomputer mit dem externen Netzwerk, und versuchen Sie den Zugriff auf interne Ressourcen.  
  
    Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  
6.  Testen der Konnektivität für Windows 7-Clients über jeden Server in der Bereitstellung für mehrere Standorte durch den Zugriff auf die Konsole Active Directory-Benutzer und-Computer und verschieben die Clientcomputer der Sicherheitsgruppe, die jeden Server entspricht. Nachdem die Änderungen in der gesamten Domäne repliziert wurden, für starten Sie den Clientcomputer, die während der Verbindung mit dem Unternehmensnetzwerk, um die neue Gruppenrichtlinie erhalten neu. Es wurde versucht, den Zugriff auf Unternehmensressourcen. Wiederholen Sie den Test auf einem anderen Server für mit mehreren Standorten aus.  
  
    Sie sollten auf alle Unternehmensressourcen über jeden Server für mehrere Standorte zugreifen können.  
  
    In einer produktionsumgebung kann diese Methode nicht aufgrund der Menge der Zeitaufwand für die Änderungen in der gesamten Domäne repliziert durchführbar. Sie sollten nach Möglichkeit die Replikation erzwingen. Tests kann auch aus mehreren verschiedenen Windows 7-Clientcomputern ausgeführt werden, die bereits Mitglied der verschiedenen Windows 7-Sicherheitsgruppen in der Bereitstellung für mehrere Standorte sind.  
  


