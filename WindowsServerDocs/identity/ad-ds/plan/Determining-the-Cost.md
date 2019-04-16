---
ms.assetid: e3ea1f67-60d4-4566-b24c-37faa95c3b2a
title: Bestimmen der Kosten
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b32d1930fcef944fbd719338797f0f29b70fa29d
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="determining-the-cost"></a>Bestimmen der Kosten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie weisen Kosten standortverknüpfungen, kostengünstige Verbindungen über teure Verbindungen zu bevorzugen. Bestimmte Anwendungen und Dienste, z.B. Domänencontrollerlocator (Domänencontrollerlocator) und verteilt Datei System Namespaces (DFSN), verwenden auch Informationen, die am nächsten gelegenen Ressourcen gesucht werden soll. Standortverknüpfungskosten kann verwendet werden, um zu bestimmen, welche Domänencontroller von Clients an einem Standort kontaktiert wird, wenn der Domänencontroller für die angegebene Domäne an diesem Standort nicht vorhanden ist. Der Client kontaktiert den Domänencontroller mit der standortverknüpfung, das den geringsten Kosten zugewiesen wurde.  
  
Es wird empfohlen, dass der Wert der Kosten pro standortweite definiert werden. Kosten basiert in der Regel nicht nur auf die gesamte Bandbreite der Verbindung, sondern auch auf die Verfügbarkeit, Latenz und zu den Kosten des Links.  
  
Um festzustellen, die Kosten für standortverknüpfungen zu platzieren, dokumentieren Sie die Geschwindigkeit der Verbindung Link für jede Site. Weitere Informationen finden Sie in das Arbeitsblatt "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc) in [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) Informationen über die verbindungsgeschwindigkeit, die Sie identifiziert.  
  
Die folgende Tabelle enthält die Geschwindigkeit für unterschiedliche Arten von Netzwerken.  
  
|"Netzwerk"|Geschwindigkeit|  
|----------------|---------|  
|Sehr langsam|56 Kilobit pro Sekunde (KBit/s)|  
|Langsam|64 KBit/s|  
|Integrierte Dienste Digital Network (ISDN)|64 KBit/s oder 128 KBit/s|  
|Frame Relay|Variable Rate, meistens zwischen 56 KBit/s und 1,5 Megabit pro Sekunde (MBit/s)|  
|T1|1,5 MBit/s|  
|T3|45 MBit/s|  
|10BaseT|10 MBit/s|  
|Asynchroner Übertragungsmodus (ATM)|Variable Rate, meistens zwischen 155 MBit/s und 622 MBit/s|  
|100BaseT|100 MBit/s|  
|Gigabit-Ethernet|1-Gigabit pro Sekunde (Gbit/s)|  
  
Verwenden Sie in der folgende Tabelle, um die Kosten für jeden Standort-Verbindung basierend auf der verbindungsgeschwindigkeit von wide Area Network Geschwindigkeit (WAN) zu berechnen. Für WAN-verbindungsgeschwindigkeit, die in der Tabelle nicht aufgeführt ist, können Sie einen relativen Kostenfaktor berechnen, 1.024 durch das Protokoll der verfügbaren Bandbreite, gemessen in KBit/s geteilt.  
  
|Verfügbare Bandbreite (KBit/s)|Kosten|  
|--------------------------------|--------|  
|9.6|1,042|  
|19.2|798|  
|38.4|644|  
|56|586|  
|64|567|  
|128|486|  
|256|425|  
|512|378|  
|1,024|340|  
|2,048|309|  
|4,096|283|  
  
Diese Kosten entsprechen nicht Unterschiede zwischen der Netzwerkverbindungen in Zuverlässigkeit. Höhere Kosten für Netzwerklinks fehleranfällige festgelegt, so, dass Sie nicht auf die Links für die Replikation verlassen verfügen. Durch Einstellung höhere Standortverknüpfungskosten können Sie Replikations-Failovers steuern, wenn eine standortverknüpfung fehlschlägt.  
  


