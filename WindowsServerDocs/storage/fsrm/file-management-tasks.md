---
title: Dateiverwaltungsaufgaben
description: In diesem Artikel wird der Prozess der Automatisierung von Datei Verwaltungsaufgaben beschrieben.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 4e10aeec47498d6af72e767f519b11ebb4e72932
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961384"
---
# <a name="file-management-tasks"></a>Dateiverwaltungsaufgaben

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Datei Verwaltungsaufgaben automatisieren das Auffinden von Teilmengen von Dateien auf einem Server und das Anwenden einfacher Befehle. Diese Aufgaben können in regelmäßigen Abständen ausgeführt werden, um sich wiederholende Kosten zu reduzieren. Dateien, die von einer Datei Verwaltungsaufgabe verarbeitet werden, können durch eine der folgenden Eigenschaften definiert werden:

-   Standort
-   Klassifizierungs Eigenschaften
-   Erstellungszeit
-   Änderungszeit
-   Zeitpunkt des letzten Zugriffs

Datei Verwaltungsaufgaben können auch so konfiguriert werden, dass Dateibesitzer von allen bevorstehenden Richtlinien benachrichtigt werden, die auf Ihre Dateien angewendet werden.

> [!Note]
> Einzelne Datei Verwaltungsaufgaben werden in unabhängigen Zeitplänen ausgeführt.

<br />
Dieser Abschnitt schließt folgende Themen ein:

-   [Erstellen einer Dateiablaufaufgabe](create-file-expiration-task.md)
-   [Erstellen einer benutzerdefinierten Dateiverwaltungsaufgabe](create-custom-file-management-task.md)

> [!Note]
> Um e-Mail-Benachrichtigungen und bestimmte Berichterstattungs Funktionen festzulegen, müssen Sie zunächst die allgemeinen Optionen für den Datei Server Ressourcen-Manager konfigurieren.

## <a name="additional-references"></a>Weitere Verweise

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


