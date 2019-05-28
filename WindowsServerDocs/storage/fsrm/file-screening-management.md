---
title: Dateiprüfungsverwaltung
description: Dieser Artikel beschreibt, wie Dateiprüfungen erstellt, Benachrichtigungen generiert, Dateiprüfungsvorlagen festgelegt und Dateiprüfungsausnahmen erstellt werden
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 05fcaf402347d16bf8c28528d402664ae5f99165
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/09/2019
ms.locfileid: "65476045"
---
# <a name="file-screening-management"></a>Dateiprüfungsverwaltung

> Gilt für: WindowsServer 2019, WindowsServer 2016, WindowsServer (Halbjährlicher Kanal), Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Sie können auf dem Knoten **Dateiprüfungsverwaltung** des Ressourcen-Manager für Dateiserver-MMC-Snap-Ins folgende Aufgaben ausführen:

-   Erstellen Sie Dateiprüfungen, um die Dateitypen zu steuern, die Benutzer speichern können und um Benachrichtigungen zu generieren, wenn Benutzer versuchen, nicht autorisierte Dateien zu speichern.
-   Legen Sie Dateiprüfungsvorlagen fest, die auf neue Volumes oder Ordner angewendet werden und die in der gesamten Organisation verwendet werden können.
-   Erstellen Sie Dateiprüfungsausnahmen, die die Flexibilität der Dateiprüfungsregeln erweitern.

Sie haben u. a. folgende Möglichkeiten:

-   Stellen Sie sicher, dass keine Musikdateien in persönlichen Ordnern auf einem Server gespeichert sind. Sie können allerdings das Speichern bestimmter Arten von Mediendateien erlauben, die die Verwaltung gesetzlicher Rechte unterstützt oder die Unternehmensrichtlinien einhält. Das gleiche Szenario empfiehlt sich unter Umständen, wenn Sie einem Vice President des Unternehmens besondere Rechte zum Speichern von allen Dateitypen in seinem persönlichen Ordner gewähren.
-   Implementieren Sie einen Prüfungsprozess, der Sie per E-Mail benachrichtigt, wenn eine ausführbare Datei in einem freigegebenen Ordner gespeichert wird, einschließlich Informationen über den Benutzer, der die Datei gespeichert hat und den genauen Speicherort der Datei, damit Sie entsprechende vorbeugende Maßnahmen ergreifen können.

In diesem Abschnitt werden folgende Themen behandelt:

-   [Definieren von Dateigruppen für die Prüfung](define-file-groups-for-screening.md)
-   [Erstellen Sie einen Datei-Bildschirm](create-file-screen.md)
-   [Erstellen einer Dateiprüfungsausnahme](create-file-screen-exception.md)
-   [Erstellen einer Dateiprüfungsvorlage](create-file-screen-template.md)
-   [Bearbeiten der Eigenschaften der Dateiprüfungsvorlage](edit-file-screen-template-properties.md)

> [!Note]
> Zum Festlegen von E-Mail-Benachrichtigungen und bestimmten Berichtsfunktionen müssen Sie zuerst die Optionen des Ressourcen-Manager für Dateiserverkonfigurieren konfigurieren.

## <a name="see-also"></a>Siehe auch

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


