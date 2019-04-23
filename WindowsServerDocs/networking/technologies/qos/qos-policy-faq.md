---
title: QoS-häufig gestellte Fragen
description: Dieses Thema enthält Antworten auf Fragen zu Quality of Service (QoS)-Richtlinie in Windows Server 2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f9fb54cc3bda9a259188ae02fb2ef2836dd8718d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833751"
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS-Richtlinie – häufig gestellte Fragen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Im folgenden werden häufig gestellte für Fragen – und Antworten auf diese Fragen – für QoS-Richtlinie.
  
1.  **Welches Betriebssystem muss mein Domänencontroller ausgeführt werden, um QoS-Richtlinie verwenden?**
  
     WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2 oder WindowsServer 2008

2.  **Welche Betriebssysteme unterstützen die Anwendung von QoS-Richtlinie für den Benutzer oder Computer?**

     Sie können die QoS-Richtlinien auf Benutzer oder Computer unter Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows Server 2008 und Windows Vista anwenden.

3.  **Werden QoS-Richtlinien werden zum Absender oder Empfänger des Datenverkehrs angewendet?**

     QoS-Richtlinien müssen angewendet werden, auf dem sendenden Computer an, um den ausgehenden Datenverkehr zu beeinflussen. Um den bidirektionalen Datenverkehr von zwei Computern auswirken können, müssen QoS-Richtlinien auf beiden Computern angewendet werden.

4.  **Was geschieht, wenn in Konflikt stehende QoS-Richtlinien auf demselben Computer bereitgestellt werden?**  
  
     Wenn mehrere Richtlinien anwenden, hat die spezifischere QoS-Richtlinie Vorrang vor. Beispielsweise wird eine Richtlinie eine Hostadresse (192.168.4.12) anstelle einer weniger spezifischen Netzwerkadresse (192.168.0.0/16) angewendet. Wenn eine Richtlinie auf Computerebene und Benutzerebene der gleichen detailgenauigkeit haben, wird die QoS-Richtlinie auf Benutzerebene anstelle der Computerebene QoS-Richtlinie angewendet. 

5.  **Werden QoS-Richtlinie ist standardmäßig aktiviert?**

     Nein, ist die QoS-Richtlinie nicht standardmäßig aktiviert. Sie müssen manuell zum Aktivieren von QoS-QoS-Richtlinien erstellen.  Weitere Informationen finden Sie unter [QoS-Richtlinie verwalten](qos-policy-manage.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
