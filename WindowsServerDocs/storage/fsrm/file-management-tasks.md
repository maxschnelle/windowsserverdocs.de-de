---
title: Dateiverwaltungsaufgaben
description: In diesem Artikel wird der Prozess der Automatisierung von Datei Verwaltungsaufgaben beschrieben.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 402af4bd7c00bedfc3d01d43071af4fcd374d428
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85473997"
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

## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


