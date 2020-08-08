---
title: Management von Sollvorgaben
description: In diesem Artikel wird das Erstellen und Verwalten von Kontingenten beschrieben.
ms.date: 7/7/2017
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: b1d2d37d73a3d7837fd5390b9f5860f7cb41ee85
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87961374"
---
# <a name="quota-management"></a>Management von Sollvorgaben

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Im Knoten **Kontingent Verwaltung** des-Dateiservers Ressourcen-Manager Microsoft<sup>®</sup> Management Console (MMC)-Snap-in können Sie die folgenden Aufgaben ausführen:

-   Erstellen Sie Kontingente, um den für ein Volume oder einen Ordner zulässigen Speicherplatz einzuschränken, und generieren Sie Benachrichtigungen, wenn die Kontingent Grenzen erreicht oder überschritten werden.
-   Generieren von automatischen Apply-Kontingenten, die für alle vorhandenen Unterordner in einem Volume oder Ordner und für alle Unterordner gelten, die in der Zukunft erstellt werden.
-   Definieren Sie Kontingent Vorlagen, die auf einfache Weise auf neue Volumes oder Ordner angewendet und dann in einer Organisation verwendet werden können.

Sie haben unter anderem folgende Möglichkeiten:

-   Legen Sie eine Beschränkung von 200 Megabyte (MB) für die persönlichen Server Ordner der Benutzer fest, und senden Sie eine e-Mail-Benachrichtigung an Sie und den Benutzer, wenn 180 MB Speicher überschritten wurden.
-   Legen Sie für den freigegebenen Ordner einer Gruppe ein flexibles Kontingent von 500 MB fest. Wenn diese Speichergrenze erreicht ist, werden alle Benutzer in der Gruppe per e-Mail benachrichtigt, dass das Speicher Kontingent vorübergehend auf 520 MB erweitert wurde, sodass Sie unnötige Dateien löschen und die vordefinierte 500 MB-Kontingent Richtlinie einhalten können.
-   Sie erhalten eine Benachrichtigung, wenn ein temporärer Ordner eine Nutzung von 2 Gigabyte (GB) erreicht, aber nicht das Kontingent dieses Ordners einschränkt, da es für einen Dienst, der auf dem Server ausgeführt wird, erforderlich ist.

Dieser Abschnitt schließt folgende Themen ein:

-   [Erstellen eines Kontingents](create-quota.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)
-   [Erstellen einer Kontingent Vorlage](create-quota-template.md)
-   [Bearbeiten von Kontingentvorlageneigenschaften](edit-quota-template-properties.md)
-   [Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents](edit-auto-apply-quota-properties.md)

> [!Note]
> Zum Festlegen von e-Mail-Benachrichtigungen und Bericht Erstellungs Funktionen müssen Sie zunächst die allgemeinen Optionen für den Datei Server Ressourcen-Manager konfigurieren.

## <a name="additional-references"></a>Weitere Verweise

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


