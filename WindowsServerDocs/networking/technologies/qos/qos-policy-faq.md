---
title: Häufig gestellte Fragen zu QoS
description: Dieses Thema enthält Antworten auf Fragen zu Quality of Service (QoS)-Richtlinie in Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: lizross
author: eross-msft
ms.openlocfilehash: a2b0990bd1416032cd519c60878c389f391e053d
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315537"
---
# <a name="qos-policy-frequently-asked-questions"></a>Häufig gestellte Fragen zu QoS-Richtlinien

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Im folgenden finden Sie häufig gestellte Fragen – und Antworten auf diese Fragen – für die QoS-Richtlinie.
  
1.  **Welches Betriebssystem muss auf meinem Domänen Controller ausgeführt werden, um die QoS-Richtlinie verwenden zu können?**
  
     Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 oder Windows Server 2008

2.  **Welche Betriebssysteme unterstützen die Anwendung der QoS-Richtlinie für den Benutzer oder Computer?**

     Sie können QoS-Richtlinien auf Benutzer oder Computer anwenden, auf denen Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista ausgeführt wird.

3.  **Gelten QoS-Richtlinien für den Absender oder Empfänger von Datenverkehr?**

     Auf dem sendenden Computer müssen QoS-Richtlinien angewendet werden, um den ausgehenden Datenverkehr zu beeinflussen. Um den bidirektionalen Datenverkehr von zwei Computern zu beeinflussen, müssen QoS-Richtlinien auf beide Computer angewendet werden.

4.  **Was passiert, wenn in Konflikt stehende QoS-Richtlinien auf demselben Computer bereitgestellt werden?**  
  
     Wenn mehrere Richtlinien zutreffen, hat die spezifischere QoS-Richtlinie Vorrang. Beispielsweise wird eine Richtlinie, die angibt, dass eine Host Adresse (192.168.4.12) anstelle einer weniger spezifischen Netzwerkadresse (192.168.0.0/16) angewendet wird. Wenn eine Richtlinie auf Computer-und Benutzerebene die gleiche Besonderheit hat, wird die QoS-Richtlinie auf Benutzerebene anstelle der QoS-Richtlinie auf Computer Ebene angewendet. 

5.  **Ist die QoS-Richtlinie standardmäßig aktiviert?**

     Nein, die QoS-Richtlinie ist standardmäßig nicht aktiviert. QoS-Richtlinien müssen manuell erstellt werden, um QoS zu aktivieren.  Weitere Informationen finden Sie unter [Verwalten der QoS-Richtlinie](qos-policy-manage.md).

Das erste Thema in dieser Anleitung finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
