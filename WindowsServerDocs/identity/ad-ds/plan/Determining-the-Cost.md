---
ms.assetid: e3ea1f67-60d4-4566-b24c-37faa95c3b2a
title: Bestimmen der Kosten
author: iainfoulds
ms.author: daveba
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 9da1c4f247a1acfe982a2d5444fc3385806ce039
ms.sourcegitcommit: b115e5edc545571b6ff4f42082cc3ed965815ea4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "93069202"
---
# <a name="determining-the-cost"></a>Bestimmen der Kosten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie weisen Standort Verknüpfungen Kostenwerte zu, um kostengünstige Verbindungen über teure Verbindungen zu bevorzugen. Bestimmte Anwendungen und Dienste, z. b. Domänen Controller-Locator (DCLOCATOR) und verteiltes Dateisystem Namespaces (DFSN), verwenden auch Kosteninformationen, um die nächstgelegenen Ressourcen zu finden. Die Kosten für die Standort Verknüpfung können verwendet werden, um zu bestimmen, welcher Domänen Controller von Clients an einem Standort kontaktiert wird, wenn der Domänen Controller für die angegebene Domäne an diesem Standort nicht vorhanden ist. Der Client kontaktiert den Domänen Controller über die Standort Verknüpfung, der die niedrigsten Kosten zugewiesen sind.

Es wird empfohlen, den Kosten Wert auf standortweite Basis zu definieren. Die Kosten basieren in der Regel nicht nur auf der Gesamtbandbreite der Verknüpfung, sondern auch auf der Verfügbarkeit, Latenz und den monetären Kosten der Verknüpfung.

Um die Kosten für Standort Verknüpfungen zu ermitteln, dokumentieren Sie die Verbindungsgeschwindigkeit für jede Standort Verknüpfung. Informationen über die von Ihnen identifizierte Verbindungsgeschwindigkeit finden [Sie im Arbeits](../../ad-ds/plan/Collecting-Network-Information.md) Blatt "geografische Standorte und Kommunikations Links" (DSSTOPO_1.doc).

In der folgenden Tabelle werden die Geschwindigkeiten für verschiedene Arten von Netzwerken aufgelistet.

|Netzwerktyp|Geschwindigkeit|
|----------------|---------|
|Sehr langsam|56 Kilobit pro Sekunden (KBit/s)|
|Langsam|64 Kbit/s|
|Integriertes Services Digital Network (ISDN)|64 Kbit/s 128 bzw|
|Frame Relay|Variablen Rate, häufig zwischen 56 Kbit/s und 1,5 meits pro Sekunde (Mbit/s)|
|T1|1,5 Mbit/s|
|T3|45 MBit/s|
|10BaseT|10 Mbit/s|
|Asynchroner Übertragungsmodus (ATM)|Variablenate, häufig zwischen 155 Mbit/s und 622 Mbit/s|
|100BaseT|100 MBit/s|
|Gigabit-Ethernet|1 Gigabit pro Sekunde (GBit/s)|

Verwenden Sie die folgende Tabelle, um die Kosten der einzelnen Standort Verknüpfungen basierend auf der WAN-Verbindungsgeschwindigkeit (Wide Area Network Speed) zu berechnen. Wenn die WAN-Verbindungsgeschwindigkeit in der Tabelle nicht aufgeführt ist, können Sie einen relativen Kostenfaktor berechnen, indem Sie 1.024 durch das Protokoll der verfügbaren Bandbreite, gemessen in Kbit/s, verteilen.

|Verfügbare Bandbreite (KB)|Kosten|
|--------------------------------|--------|
|9,6|1.042|
|19,2|798|
|38,4|644|
|56|586|
|64|567|
|128|486|
|256|425|
|512|378|
|1\.024|340|
|2\.048|309|
|4\.096|283|

Diese Kosten entsprechen nicht den Unterschieden bei der Zuverlässigkeit zwischen Netzwerkverbindungen. Legen Sie für alle fehleranfälligen Netzwerkverbindungen höhere Kosten fest, damit Sie sich nicht auf diese Verknüpfungen für die Replikation verlassen müssen. Durch Festlegen der Kosten für eine höhere Standort Verknüpfung können Sie das Replikations Failover steuern, wenn eine Standort Verknüpfung ausfällt.



