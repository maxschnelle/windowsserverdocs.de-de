---
title: Grundlegendes zu Funktionen
description: Dieses Thema definiert das Konzept der Funktionen im System Einblicke und führt die Standardfunktionen in Windows Server-2019 verfügbar.
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
ms.date: 6/05/2018
ms.openlocfilehash: 21932a3e45d7fc6711400eb30c63c3412bbc116e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830971"
---
# <a name="understanding-capabilities"></a>Grundlegendes zu Funktionen

>Gilt für: Windows Server 2019

Dieses Thema definiert das Konzept der Funktionen im System Einblicke und führt die Standardfunktionen in Windows Server-2019 verfügbar. 

Dieses Thema beschreibt auch die Datenquellen, Vorhersage Zeitachsen und Vorhersage-Status für die Standardfunktionen verwendet. 

## <a name="capability-overview"></a>Funktionsübersicht
Eine System-Insights-Funktion befindet sich ein Machine Learning oder statistikmodell, das Systemdaten ermöglichen Ihnen den analysiert erhöht, einen Einblick in die Funktionsweise der Bereitstellung. System Insights stellt einen anfänglichen Satz von Standardfunktionen und können Sie neue Funktionen dynamisch hinzuzufügen, ohne das Betriebssystem aktualisieren. 

>[!NOTE]
>Ausführliche Dokumentation erläutern, wie für das Erstellen, hinzufügen und Aktualisierungsfunktionen steht [hier](adding-and-developing-capabilities.md), und [das Verwalten von Funktionen Dokument](managing-capabilities.md) bietet eine grobe Übersicht dazu die Funktionalität.

Darüber hinaus jede Funktion wird lokal auf einem Windows Server-Instanz ausgeführt, und jede Funktion einzeln verwaltet werden kann.

### <a name="capability-outputs"></a>Ausgaben der Funktion
Wenn eine Funktion aufgerufen wird, wird eine Ausgabe, um das Ergebnis der Analyse oder Vorhersage zu erklären. Jede Ausgabe darf eine **Status** und ein **Statusbeschreibung** zur Beschreibung der Vorhersage, und jedes Ergebnis können optional Funktion-spezifische Daten enthalten mit der Vorhersage verknüpft ist. Die **Statusbeschreibung** hilft bietet eine kontextbezogene Erläuterung für die **Status**, und die Funktion gibt entweder eine **OK**, **Warnung**, oder **kritisch** Status. Darüber hinaus kann eine Funktion mithilfe einer **Fehler** oder **keine** Status, wenn keine Vorhersage getroffen wurde. Hier befinden die Statusangaben für die Funktion und ihrer grundlegenden Bedeutung: 

- **OK** – alles sieht gut aus.
- **Warnung** – keine sofortigen Maßnahmen erforderlich, aber Sie sollten sehen. 
- **Kritische** – Sie sollten sehen Sie in Kürze. 
- **Fehler** -ein unbekanntes Problem verursacht hat, die Funktion fehlschlägt. 
- **Keine** -keine Vorhersage getroffen wurde. Dies kann aufgrund fehlender Daten oder einem anderen Funktion-spezifische Grund für die nicht Treffen einer Vorhersage sein. 

Darüber hinaus werden im Resultset enthaltenen Funktion-spezifische Daten platziert werden, in ein Benutzer zugreifen kann JSON-Datei, und den Dateipfad [finden Sie mithilfe von PowerShell](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results). 

## <a name="default-capabilities"></a>Standardfunktionen
In Windows Server-2019 werden System Insights vier Standardfunktionen, die mit dem Schwerpunkt Kapazitätsprognosen eingeführt:

- **CPU-kapazitätsprognose** -Prognosen CPU-Auslastung. 
- **Netzwerk Kapazitätsprognosen** -Prognosen Netzwerkverwendung für jeden Netzwerkadapter. 
- **Gesamtspeicher Verbrauch Prognose** -Prognosen insgesamt belegter Speicher auf allen lokalen Laufwerken. 
- **Volume Verbrauch Prognose** -Speicherverbrauch für jedes Volume Vorhersagen.

Jede Funktion analysiert das Verlaufsdaten zur Vorhersage von zukünftigen Stromverbrauch, und **alle forecasting Funktionen dienen, langfristige Trends und nicht als kurzfristige Verhalten zu prognostizieren**, was den Administratoren ordnungsgemäß Bereitstellen von Hardware, und Optimieren Sie ihre Workloads, um zukünftige Ressourcenkonflikte zu vermeiden. Da diese Funktionen auf langfristiger Nutzung zu konzentrieren, analysieren diese Funktionen datenkontingent von täglich aus. 

### <a name="forecasting-model"></a>Forecasting-Modells
Die Standardfunktionen verwenden ein forecasting-Modell zur Vorhersage von zukünftigen Stromverbrauch, und für jede Vorhersage, das Modell wird trainiert lokal auf Ihrer VM Daten. Dieses Modell wurde entwickelt, um mehr Begriff Trends zu erkennen und zum erneuten trainieren auf jeder Windows Server-Instanz ermöglicht die Möglichkeit zur Anpassung an das bestimmte Verhalten und die Details in Bezug auf jeden Computer die Nutzung.

>[!NOTE]
>Bestimmen, welche Art von Modell, das erforderlich sind, viele Modelle, die unter Verwendung eines Datasets mit Zehntausenden von Computern zu testen. Nach dem Analysieren und diese Modelle optimieren, haben wir beschlossen verwenden ein autoregressive zeitreihenmethode forecasting-Modells, wie es äußerst präzise und visuell intuitive Vorhersagen erstellt, nicht erforderlich ist zu viel Zeit zum Trainieren. Dieses Modell, erfordert jedoch drei Wochen von Trainingsdaten, daher wird jede Funktion einen einfachen linearen Trend verwendet, bis drei Wochen von Daten zur Verfügung stehen.

### <a name="forecasting-timelines"></a>Vorhersagen von Zeitachsen
Die Standardfunktionen prognostizieren eine bestimmte Anzahl von Tagen, in die Zukunft basierend auf der Anzahl von Tagen, die für die Daten erfasst wurden. Die folgende Tabelle zeigt die Zeitachsen für die Vorhersage dieser Funktionen:

| Größe der Eingabedaten | Länge prognostizieren |
| --------------- | --------------- |
| 0 bis 5 Tagen | Es ist keine Vorhersage getroffen. |
| 6 – 180 Tage | 1/3 * Größe der Eingabedaten |
| 180-365 Tage | 60 Tage | 

### <a name="forecasting-data"></a>Prognosedaten
Jede Funktion analysiert die tägliche Daten, um zukünftige Nutzung zu prognostizieren. CPU, Netzwerk, und sogar speichernutzung, kann jedoch im Laufe des Tages, häufig ändern dynamisch anpassen, um die arbeitsauslastungen auf dem Computer. Da Nutzung im Laufe des Tages Konstanten nicht ist, ist es wichtig, um Daten zur täglichen Nutzung in einen einzelnen Datenpunkt ordnungsgemäß darzustellen. In der folgenden Tabelle werden die bestimmten Datenpunkten und wie die Daten verarbeitet werden:


| Funktionsname | Datenquelle(n) | Filterlogik |
| --------------- | -------------- | ---------------- |
 Volume Verbrauch Vorhersagen          | Volumegröße                    | Maximale tägliche Nutzung              
 Gesamtspeicher Verbrauch Vorhersagen   | Summe der Volumegrößen, Summe der Größe von Datenträgern              | Maximale tägliche Nutzung             
 CPU-kapazitätsprognose                | % Processor Time  | Maximal 2 Stunden Durchschnitt pro Tag   
 Netzwerk kapazitätsprognose         | Gesamtanzahl Bytes/Sek.         | Maximal 2 Stunden Durchschnitt pro Tag  

Beim Auswerten der Filterlogik oben, es zu beachten, dass jede Funktion sucht, um Administratoren zu informieren beim weiteren Nutzung die verfügbare Kapazität – Klassenmemberfunktionen überschreiten, obwohl die CPU vorübergehend Auslastung von 100 % erreicht, kann CPU-Auslastung nicht haben. verursacht, sinnvolle Leistung Leistungsabfällen oder Ressource Konflikte. Für CPU und das Netzwerk dann dürfte anhaltend hohe Auslastung anstelle von vorübergehenden Spitzen. Durchschnitt CPU und Netzwerk-Verwendung überall in den ganzen Tag, würden jedoch wichtige Informationen, verlieren, wie ein paar Stunden hoher CPU- oder Netzwerk Nutzung Klassenmemberfunktionen kritische Workloads die Leistung auswirken können. Der maximal 2 Stunden Durchschnitt während jedes Tages vermeidet diesen extremen und weiterhin erzeugt aussagekräftige Daten für die einzelnen Funktionen zu analysieren.

Volume und die gesamte speicherauslastung kann nicht jedoch die speicherauslastung die verfügbare Kapazität, sogar sofort überschreiten, sodass die maximale Daten zur tägliche Nutzung für diese Funktionen verwendet wird. 

### <a name="forecasting-statuses"></a>Prognose des Status
Alle System-Insights-Funktionen müssen einen Status in Verbindung mit der einzelnen Vorhersagen ausgegeben werden. Jede Standardfunktion verwendet die folgende Logik zum Status der einzelnen Vorhersage zu definieren:
- **OK**: Die Vorhersage ist die verfügbare Kapazität nicht überschreiten.
- **Warnung**: Die Vorhersage überschreitet die verfügbare Kapazität in den nächsten 30 Tagen. 
- **Kritisch**: Die Vorhersage überschreitet die verfügbare Kapazität in den nächsten 7 Tagen. 
- **Fehler**: Die Funktion ist ein unerwarteter Fehler aufgetreten. 
- **Keine**: Es ist nicht genügend Daten für eine Vorhersage zu treffen. Dies ist möglicherweise aufgrund fehlender Daten, oder weil vor kurzem keine Daten gemeldet wurde.

>[!NOTE]
>Wenn eine Funktion Vorhersagen auf mehreren Instanzen – z. B. mehrere Volumes oder Netzwerkadapter – gibt den Status der schwerwiegendsten Status für alle Instanzen wieder. Einzelne Status für jedes Volume oder Netzwerkadapter werden angezeigt, in Windows Admin Center oder die Daten in die Ausgabe der einzelnen Funktionen. Anweisungen dazu, wie die JSON-Ausgabe die Standardfunktionen analysiert, finden Sie unter [diesen Blog](https://aka.ms/systeminsights-mitigationscripts). 


## <a name="see-also"></a>Siehe auch
Weitere Informationen zum System Insights können Sie die folgenden Ressourcen:

- [System-Insights-Übersicht](overview.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und die Entwicklung von Funktionen](adding-and-developing-capabilities.md)
- [System Insights – häufig gestellte Fragen](faq.md)
