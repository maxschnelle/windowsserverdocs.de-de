---
title: Datei Prüfungsverwaltung
description: Dieser Artikel beschreibt das Erstellen von Datei Bildschirmen, das Generieren von Benachrichtigungen, das Definieren von Datei Überprüfungs Vorlagen und das Erstellen von Datei Überprüfungs Ausnahmen.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: c189386ac340e9362c8774340732f8689f17effe
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87957437"
---
# <a name="file-screening-management"></a>Datei Prüfungsverwaltung

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Im Knoten **Datei Überprüfungs Verwaltung** des-Dateiservers Ressourcen-Manager MMC-Snap-in können Sie die folgenden Aufgaben ausführen:

-   Erstellen Sie Datei Bildschirme, um die Dateitypen zu steuern, die Benutzer speichern können, und generieren Sie Benachrichtigungen, wenn Benutzer versuchen, nicht autorisierte Dateien zu speichern.
-   Definieren Sie Datei Überprüfungs Vorlagen, die auf neue Volumes oder Ordner angewendet werden können und die in einer Organisation verwendet werden können.
-   Erstellen Sie Datei Überprüfungs Ausnahmen, die die Flexibilität der Datei Überprüfungs Regeln erweitern.

Sie haben unter anderem folgende Möglichkeiten:

-   Stellen Sie sicher, dass keine Musikdateien in persönlichen Ordnern auf einem Server gespeichert werden. Sie können jedoch die Speicherung bestimmter Arten von Mediendateien zulassen, die die Rechteverwaltung unterstützen oder die Unternehmensrichtlinien einhalten. Im gleichen Szenario empfiehlt es sich, einem Vizepräsidenten in den Unternehmen spezielle Berechtigungen zum Speichern beliebiger Dateitypen in seinem persönlichen Ordner zu geben.
-   Implementieren Sie einen Überprüfungsprozess, um Sie per e-Mail zu benachrichtigen, wenn eine ausführbare Datei in einem freigegebenen Ordner gespeichert wird, einschließlich Informationen über den Benutzer, der die Datei und den genauen Speicherort der Datei gespeichert hat, sodass Sie die entsprechenden Vorsichtsmaßnahmen ergreifen können.

Dieser Abschnitt schließt folgende Themen ein:

-   [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)
-   [Erstellen einer Dateiprüfung](create-file-screen.md)
-   [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)
-   [Bearbeiten der Eigenschaften der Dateiprüfungsvorlage](edit-file-screen-template-properties.md)

> [!Note]
> Um e-Mail-Benachrichtigungen und bestimmte Berichterstattungs Funktionen festzulegen, müssen Sie zunächst die allgemeinen Optionen für den Datei Server Ressourcen-Manager konfigurieren.

## <a name="additional-references"></a>Weitere Verweise

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


