---
title: 'QoS: häufig gestellte Fragen'
description: Dieses Thema enthält Antworten auf Fragen zur Quality of Service (QoS)-Richtlinie in Windows Server2016.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 74c97a14-b957-4568-b48e-8963a674fdb3
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e63cd00a2016411e9f2c532c0e4c301dabdfd816
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="qos-policy-frequently-asked-questions"></a>QoS-Richtlinie-häufig gestellte Fragen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Folgende sind häufig Fragen und Antworten auf diese Fragen – für QoS-Richtlinie aufgefordert.
  
1.  **Muss Domänencontroller unter welchem Betriebssystem ausgeführt werden, um QoS-Richtlinie verwenden?**
  
     Windows Server 2016, Windows Server2012 R2, Windows Server 2012, Windows Server2008 R2 oder Windows Server 2008

2.  **Welche Betriebssysteme unterstützen die Anwendung von QoS-Richtlinie auf den Benutzer oder Computer?**

     Sie können die QoS-Richtlinien für Benutzer oder Computer mit Windows Server2016, Windows10, Windows Server2012 R2, Windows8.1, Windows Server2012, Windows8, Windows Server2008 R2, Windows Server2008 und Windows Vista anwenden.

3.  **Gelten QoS-Richtlinien für den Absender oder die Empfänger des Datenverkehrs?**

     QoS-Richtlinien müssen auf dem sendenden Computer beeinflusst den ausgehenden Datenverkehr angewendet werden. Um den bidirektionalen Datenverkehr von zwei Computern betreffen, müssen QoS-Richtlinien auf beiden Computern angewendet werden.

4.  **Was geschieht, wenn in Konflikt stehende QoS-Richtlinien auf demselben Computer bereitgestellt werden?**  
  
     Wenn mehrere Richtlinien anwenden, hat die spezifischere QoS-Richtlinie Vorrang vor. Z.B. eine Richtlinie, dass Zustände einen Host (192.168.4.12 Adresse) wird anstelle einer weniger spezifisch Netzwerk Adresse (192.168.0.0/16 angewendet). Wenn eine Richtlinie auf Computerebene und auf der gleichen Genauigkeit haben, wird die QoS-Richtlinie auf Benutzerebene anstelle der Computerebene QoS-Richtlinie angewendet. 

5.  **Werden QoS-Richtlinie ist standardmäßig aktiviert?**

     Nein, ist die QoS-Richtlinie nicht standardmäßig aktiviert. Sie müssen manuell zum Aktivieren von QoS-QoS-Richtlinien erstellen.  Weitere Informationen finden Sie unter [QoS-Richtlinie verwalten](qos-policy-manage.md).

Das erste Thema in diesem Handbuch finden Sie unter [Quality of Service (QoS)-Richtlinie](qos-policy-top.md).
