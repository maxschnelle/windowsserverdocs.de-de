---
ms.assetid: e3ea1f67-60d4-4566-b24c-37faa95c3b2a
title: Bestimmen der Kosten
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0b34f1672311768d644c467fda10dc2fc643282d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59847081"
---
# <a name="determining-the-cost"></a>Bestimmen der Kosten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie weisen "Cost"-Werten standortverknüpfungen, teure Verbindungen kostengünstige Verbindungen vorzuziehen. Bestimmte Anwendungen und Dienste wie Domänencontrollerlocator (des DC-Locators) und Distributed Datei System-Namespaces (DFSN) –, verwenden auch Informationen zu den Kosten, die nächsten Ressourcen gesucht werden soll. Kosten für die Verbindung kann verwendet werden, um zu bestimmen, welcher Domänencontroller von den Clients an einem Standort kontaktiert wird, wenn der Domänencontroller für die angegebene Domäne nicht an diesem Standort vorhanden ist. Der Client kontaktiert den Domänencontroller mithilfe der standortverknüpfung, die den geringsten Kosten zugewiesen wurde.  
  
Es wird empfohlen, dass der Kostenwert pro Website-Ebene definiert werden. Die Kosten basieren in der Regel nicht nur auf die gesamte Bandbreite der Verbindung, sondern auch auf die Verfügbarkeit, Latenz und Kosten des Links.  
  
Um zu bestimmen, die Kosten für standortverknüpfungen zu platzieren, dokumentieren Sie die verbindungsgeschwindigkeit lautet für jede standortverknüpfung. Finden Sie in das Arbeitsblatt "Geografische Standorte und Kommunikationsverbindungen" (DSSTOPO_1.doc) in [Sammeln von Netzwerkinformationen](../../ad-ds/plan/Collecting-Network-Information.md) Informationen von der Geschwindigkeit der Verbindung, die Sie identifiziert.  
  
Die folgende Tabelle enthält die Geschwindigkeiten für verschiedene Typen von Netzwerken.  
  
|Netzwerktyp|Geschwindigkeit|  
|----------------|---------|  
|Sehr langsam.|56 Kilobit pro Sekunde (Kbit/s)|  
|Verzögerte Anzeige|64 Kbit/s|  
|Integrated Services Digital Network (ISDN)|64 Kbit/s oder 128 Kbit/s|  
|Frame relay|Variabler Rate, meistens zwischen 56 Kbit/s und 1,5 Megabit pro Sekunde (Mbit/s)|  
|T1|1,5 Mbit/s|  
|T3|45 Mbit/s|  
|10BaseT|10 Mbit/s|  
|Asynchroner Übertragungsmodus (ATM)|Variable Rate, häufig zwischen 155 Mbit/s und 622 Mbit/s|  
|100BaseT|100 Mbit/s|  
|Gigabit-Ethernet|1 Gigabit pro Sekunde (Gbit/s)|  
  
Verwenden Sie in der folgende Tabelle, um die Kosten für jede standortverknüpfung basierend auf wide Area Network (WAN)-Geschwindigkeit verbindungsgeschwindigkeit zu berechnen. Für die WAN-verbindungsgeschwindigkeit, die in der Tabelle nicht aufgeführt ist, können Sie die relative Kostenfaktor durch Division von 1.024 durch das Protokoll der verfügbaren Bandbreite, gemessen in Kbit/s berechnen.  
  
|Verfügbare Bandbreite (Kbit/s)|Kosten|  
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
  
Diese Kosten spiegeln sich nicht auf Unterschiede bei der Zuverlässigkeit Netzwerkverbindungen aus. Legen Sie höhere Kosten auf alle fehleranfälliger Netzwerkverbindungen, sodass Sie nicht auf diese Links für die Replikation verlassen verfügen. Durch Einstellung höher Standortverknüpfungskosten können Sie Failover der Replikation steuern, wenn eine standortverknüpfung ein Fehler auftritt.  
  


