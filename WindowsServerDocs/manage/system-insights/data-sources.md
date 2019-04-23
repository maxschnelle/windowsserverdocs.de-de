---
title: Systemdatenquellen für Insights
description: Wenn eine neue Funktion im System Insights zu schreiben, können Sie vorhandene oder neue Datenquellen, um lokal zu erfassen und Analysieren von angeben. Dieses Thema beschreibt die Datenquellen, die Sie auswählen können, wenn Sie eine neue Funktion zu registrieren.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 9b46db90787d24a173ffa472ec1ecb8eaffe054b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59845411"
---
# <a name="system-insights-data-sources"></a>Systemdatenquellen für Insights

>Gilt für: Windows Server 2019

System Insights stellt erweiterbare Funktionalität für die modelldatensammlung. Wenn Sie eine neue Funktion zu schreiben, können Sie vorhandene oder neue Datenquellen, um lokal zu erfassen und Analysieren von angeben. Dieses Thema beschreibt die Datenquellen, die Sie auswählen können, wenn Sie eine neue Funktion zu registrieren.

## <a name="data-sources"></a>Datenquellen
Wenn Sie eine neue Funktion zu schreiben, müssen Sie die bestimmte Datenquellen zum Sammeln von für die einzelnen Funktionen identifizieren. Datenquellen, die Sie angeben, erfasst und direkt auf Ihrem Computer gespeichert werden, und Sie können aus drei Arten von Datenquellen auswählen:

- **Leistungsindikatoren**: 
    - Geben Sie den Zählerpfad, Name und Instanzen, und System-Insights erfasst die relevanten Daten, die von dieser Leistungsindikatoren gemeldet. 

- **Systemereignisse**:
    - Geben Sie den Kanal und die Ereignis-ID, und Insights von System wird aufgezeichnet, wie oft dieses Ereignis ist aufgetreten.

- **Well-Known-Serie**
    - System Insights erfasst einige grundlegende Informationen, auf dem Computer für einige, klar definierte Ressourcen. Diese Reihe wird für die Standardfunktionen verwendet, aber sie können auch durch eine benutzerdefinierte Funktion verwendet werden. Diese sammeln Sie die folgende Informationen:

        - **Datenträger**: 
            - *Eigenschaften*: Guid
            - *Daten*: Größe
        - **Volume**:
            - *Eigenschaften*: UniqueId, DriveLetter, FileSystemLabel, Size
            - *Daten*: Verwendete Größe
        - **Netzwerkadapter**:
            - *Eigenschaften*: InterfaceGuid, InterfaceDescription, Speed
            - *Daten*: Bytes empfangen/s, gesendete Protokollbytes/Sek, Gesamtanzahl Bytes/Sek.
        - **CPU**: 
            - *Eigenschaften*:-
            - *Daten*: Prozessorzeit (%)

    - Geben Sie eine bekannte Reihe und Insights von System wird von dieser Serie gesammelten Daten zurück. 


## <a name="retention-timelines-and-collection-intervals"></a>Aufbewahrungsintervalle Zeitachsen und Sammlung
Die oben aufgeführten Datenquellen haben unterschiedliche aufbewahrungsintervalle Zeitachsen und der Auflistung. Die folgende Tabelle zeigt, wie lang und wie oft jede Datenquelle gesammelt werden:

| Datenquelle | Zeitachse der Aufbewahrung | Sammlungsintervall |
| --------------- | --------------- | ----------- |
| Leistungsindikatoren | 3 Monate | 15 Minuten |
| Systemereignisse | 3 Monate | 15 Minuten |
| Well-Known-Serie | 1 Jahr | 1 Stunden |


### <a name="aggregation-types"></a>Aggregationstypen
Da jede Reihe nur einen Datenpunkt für jedes Sammlungsintervall aufzeichnen jeder Reihe ist eine Aggregation Typ zugeordnetes es. In der folgenden Tabelle werden die Datenquelle und den entsprechenden Aggregationstyp beschrieben:

>[!NOTE]
>Für Leistungsindikatoren können Sie über ein paar unterschiedliche Aggregationstypen auswählen.

| Datenquelle | Aggregationstypen |
| --------------- | --------------- |
| Leistungsindikatoren | SUM, Average, max, min |
| Systemereignisse | Anzahl |
| Bekannte Disk-Serie | Letzte (neueste Wert in das Intervall der Datensammlung) |
| Bekannte Reihe von Volume | Letzte (neueste Wert in das Intervall der Datensammlung) |
| Bekannte CPU-Serie | Durchschnitt |
| Bekannte Network-Serie | Durchschnitt |

## <a name="data-footprint"></a>Speicherbedarf

System Insights erfasst alle Daten, die lokal auf dem Laufwerk "C:" ("c:") vorhanden sind. Im Allgemeinen ist, den Platzbedarf der System-Insights-Daten. Es abhängt, direkt auf den Typ und Anzahl der Datenquellen, die jede Funktion gibt an, und in der folgenden Tabelle werden die speichernutzung für jeden Datentyp:

| Datenquelle | Maximale Speicherbedarf |
| --------------- | --------------- |
| Leistungsindikatoren | 240 KB |
| Systemereignisse | 200 KB |
| Bekannte Disk-Serie | 200 KB pro Datenträger |
| Bekannte Reihe von Volume | 300 KB pro volume |
| Bekannte CPU-Serie | 100 KB |
| Bekannte Network-Serie | 300 KB pro Netzwerkadapter |

>[!NOTE]
>**Für den standardmäßigen Prognosefunktionen sollte der maximale Speicherbedarf weniger als 10 MB für die meisten eigenständigen Computer.** 

## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [System-Insights-Übersicht](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und die Entwicklung von Funktionen](adding-and-developing-capabilities.md)
- [System Insights – häufig gestellte Fragen](faq.md)
