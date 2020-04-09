---
title: System Insights-Datenquellen
description: Wenn Sie eine neue Funktion in System Insights schreiben, können Sie vorhandene oder neue Datenquellen angeben, die lokal erfasst und analysiert werden sollen. In diesem Thema werden die Datenquellen beschrieben, die Sie auswählen können, wenn Sie eine neue Funktion registrieren.
ms.prod: windows-server
ms.technology: system-insights
ms.topic: article
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 7/31/2018
ms.openlocfilehash: 920c5fa5919fd2c35edb99cc4e724745715091c7
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858423"
---
# <a name="system-insights-data-sources"></a>System Insights-Datenquellen

>Gilt für: Windows Server 2019

Mit System Insights werden erweiterbare Funktionen für die Datensammlung eingeführt. Wenn Sie eine neue Funktion schreiben, können Sie vorhandene oder neue Datenquellen angeben, die lokal erfasst und analysiert werden sollen. In diesem Thema werden die Datenquellen beschrieben, die Sie auswählen können, wenn Sie eine neue Funktion registrieren.

## <a name="data-sources"></a>Datenquellen
Wenn Sie eine neue Funktion schreiben, müssen Sie die spezifischen Datenquellen identifizieren, die für jede Funktion erfasst werden sollen. Die von Ihnen angegebenen Datenquellen werden gesammelt und direkt auf Ihrem Computer gespeichert, und Sie können drei Arten von Datenquellen auswählen:

- **Leistungsindikatoren**: 
    - Geben Sie den Indikator Pfad, den Namen und die Instanzen an, und System Insights sammelt die relevanten Daten, die von diesen Leistungsindikatoren gemeldet werden. 

- **System Ereignisse**:
    - Geben Sie den Channelnamen und die Ereignis-ID an, und mit System Insights wird aufgezeichnet, wie oft das Ereignis aufgetreten ist.

- **Bekannte Reihe**
    - System Insights sammelt einige grundlegende Informationen auf Ihrem Computer für einige klar definierte Ressourcen. Diese Reihen werden für die Standardfunktionen verwendet, Sie können aber auch von jeder benutzerdefinierten Funktion verwendet werden. Folgende Informationen werden gesammelt:

        - Daten **Träger:** 
            - *Eigenschaften*: GUID
            - *Daten*: Größe
        - **Volume**:
            - *Eigenschaften*: UniqueId, DriveLetter, filesystemlabel, size
            - *Daten*: verwendete Größe
        - **Netzwerk Adapter**:
            - *Eigenschaften*: interfaceguid, interfacedescription, Speed
            - *Daten*: empfangene Bytes/Sek., gesendete Bytes/Sek., Bytes gesamt/Sek.
        - **CPU**: 
            - *Eigenschaften*:-
            - *Daten*: Prozessorzeit (%)

    - Geben Sie eine bekannte Reihe an, und System Insights gibt die Daten zurück, die von dieser Reihe gesammelt werden. 


## <a name="retention-timelines-and-collection-intervals"></a>Beibehaltungs Zeitachsen und Sammlungs Intervalle
Die oben aufgeführten Datenquellen haben unterschiedliche Beibehaltungs Zeiträume und Sammlungs Intervalle. Die folgende Tabelle zeigt, wie lange und wie oft die einzelnen Datenquellen gesammelt werden:

| Datenquelle | Aufbewahrungs Zeitachse | Sammlungs Intervall |
| --------------- | --------------- | ----------- |
| Leistungsindikatoren | 3 Monate | 15 Minuten |
| System Ereignisse | 3 Monate | 15 Minuten |
| Bekannte Reihe | 1 Jahr | 1 Stunde |


### <a name="aggregation-types"></a>Aggregations Typen
Da jede Reihe nur einen Datenpunkt für jedes Sammlungs Intervall aufzeichnen, verfügt jede Reihe über einen Aggregationstyp. In der folgenden Tabelle werden die Datenquelle und der zugehörige Aggregationstyp beschrieben:

>[!NOTE]
>Für Leistungsindikatoren können Sie aus einigen unterschiedlichen Aggregations Typen auswählen.

| Datenquelle | Aggregations Typen |
| --------------- | --------------- |
| Leistungsindikatoren | Sum, Average, Max, min |
| System Ereignisse | Anzahl |
| Bekannte Reihe zu Datenträgern | Last (aktueller Wert im Sammlungs Intervall) |
| Well-Known-Reihe von Volumes | Last (aktueller Wert im Sammlungs Intervall) |
| Well-Known-Serie (CPU) | Durchschnitt |
| Bekannte Serie zu Netzwerken | Durchschnitt |

## <a name="data-footprint"></a>Daten Bedarf

System Insights sammelt alle Daten lokal auf Ihrem Laufwerk c (c:). Im Allgemeinen ist der Daten Speicherbedarf der System Insights gering. Dies hängt direkt vom Typ und der Anzahl der Datenquellen ab, die jede Funktion angibt, und in der folgenden Tabelle wird die Speicherauslastung für die einzelnen Datentypen ausführlich erläutert:

| Datenquelle | Maximaler Speicherbedarf |
| --------------- | --------------- |
| Leistungsindikatoren | 240 KB |
| System Ereignisse | 200 KB |
| Bekannte Reihe zu Datenträgern | 200 KB pro Datenträger |
| Well-Known-Reihe von Volumes | 300 KB pro Volume |
| Well-Known-Serie (CPU) | 100 KB |
| Bekannte Serie zu Netzwerken | 300 KB pro Netzwerkadapter |

>[!NOTE]
>**Bei den standardmäßigen Vorhersagefunktionen muss der maximale Speicherplatz für die meisten eigenständigen Computer weniger als 10 MB betragen.** 

## <a name="see-also"></a>Siehe auch
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Übersicht über System Einblicke](overview.md)
- [Grundlegendes zu Funktionen](understanding-capabilities.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und Entwickeln von Funktionen](adding-and-developing-capabilities.md)
- [FAQ zu System Insights](faq.md)
