---
title: Schritt 4 Überprüfen der Bereitstellung für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: 345b676a-a397-4d51-9973-8b25bc05fa55
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 1f17f85104b59052de2e1accc20adb2579ac79f4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858353"
---
# <a name="step-4-verify-the-multisite-deployment"></a>Schritt 4 Überprüfen der Bereitstellung für mehrere Standorte

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Thema wird beschrieben, wie Sie überprüfen, ob Sie die Bereitstellung für den Remote Zugriff auf mehrere Standorte ordnungsgemäß  
  
### <a name="to-verify-access-to-internal-resources-through-the-multisite-deployment"></a>So überprüfen Sie den Zugriff auf interne Ressourcen über die Bereitstellung für mehrere Standorte  
  
1.  Stellen Sie eine Verbindung von einem DirectAccess-Clientcomputer mit dem Unternehmensnetzwerk her, und rufen Sie die Gruppenrichtlinie ab.  
  
2.  Verbinden Sie den Clientcomputer mit dem externen Netzwerk, und versuchen Sie, auf interne Ressourcen zuzugreifen.  
  
    Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  
3.  Testen Sie die Konnektivität über jeden Server in der Bereitstellung für mehrere Standorte, indem Sie alle außer einem der RAS-Server ausschalten oder die Verbindung mit dem externen Netzwerk trennen. Versuchen Sie auf dem Client Computer, auf Unternehmensressourcen zuzugreifen. Wiederholen Sie den Test auf einem anderen Server mit mehreren Standorten. Es kann bis zu 10 Minuten dauern, bis der Client Computer eine Verbindung mit dem neuen Einstiegspunkt herstellt. Dies liegt daran, dass die Überprüfung 10 Minuten für einen Einstiegspunkt deaktiviert wird, nachdem er als nicht erreichbar eingestuft wurde, um die Bandbreite und die Akku Lebensdauer zu optimieren. Alternativ dazu können Sie manuell zwischen den verschiedenen Einstiegspunkten wechseln, indem Sie den gewünschten Einstiegspunkt aus dem Kombinations Feld auswählen, das beim Ausführen von **daprop. exe**angezeigt wird.  
  
    Sie sollten in der Lage sein, über jeden Server mit mehreren Standorten auf alle Unternehmensressourcen zuzugreifen.  
  
4.  Verbinden Sie einen Windows 7-&reg; Client Computer mit dem Unternehmensnetzwerk, und rufen Sie die Gruppenrichtlinie ab.  
  
5.  Verbinden Sie den Windows 7-Client Computer mit dem externen Netzwerk, und versuchen Sie, auf interne Ressourcen zuzugreifen.  
  
    Sie sollten auf alle Unternehmensressourcen zugreifen können.  
  
6.  Testen Sie die Konnektivität für Windows 7-Clients über jeden Server in der Bereitstellung für mehrere Standorte, indem Sie auf die Konsole Active Directory Benutzer und Computer zugreifen und den Client Computer in die Sicherheitsgruppe verschieben, die den einzelnen Servern entspricht. Nachdem die Änderungen in der gesamten Domäne repliziert wurden, starten Sie den Client Computer neu, während Sie mit dem Unternehmensnetzwerk verbunden sind, um die neue Gruppenrichtlinie zu erhalten. Versuchen Sie, auf Unternehmensressourcen zuzugreifen. Wiederholen Sie den Test auf einem anderen Server mit mehreren Standorten.  
  
    Sie sollten in der Lage sein, über jeden Server mit mehreren Standorten auf alle Unternehmensressourcen zuzugreifen.  
  
    In einer Produktionsumgebung ist diese Methode möglicherweise aufgrund der Zeitspanne, die für die Replikation von Änderungen in der gesamten Domäne erforderlich ist, nicht möglich. Möglicherweise möchten Sie die Replikation nach Möglichkeit erzwingen. Tests können auch von mehreren unterschiedlichen Windows 7-Client Computern durchgeführt werden, die bereits Mitglieder der verschiedenen Windows 7-Sicherheitsgruppen in der Bereitstellung für mehrere Standorte sind.  
  


