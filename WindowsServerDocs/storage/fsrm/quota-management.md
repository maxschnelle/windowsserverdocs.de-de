---
title: Kontingentverwaltung
description: Dieser Artikel beschreibt, wie Sie Kontingente erstellen und verwalten
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 5a655e28020d08bb1c10fa862c007f914a8cf566
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403072"
---
# <a name="quota-management"></a>Kontingentverwaltung

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server (halbjährlicher Kanal), Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Sie können auf dem Knoten **Kontingentverwaltung** des Ressourcen-Manager für Dateiserver Microsoft<sup>®</sup> Management Console (MMC)-Snap-Ins folgende Aufgaben ausführen:

-   Mithilfe von Kontingenten können Sie den für ein Volume oder einen Ordner zulässigen Platz beschränken und Benachrichtigungen generieren, wenn die Kontingentgrenzen erreicht oder überschritten werden.
-   Generieren von automatisch zugewiesenen Kontingenten, die für alle vorhandenen Unterordner in einem Volume oder Ordner und allen Unterordnen gelten, die in Zukunft erstellt werden.
-   Legen Sie Kontingente fest, die ganz einfach auf neue Volumes oder Ordner angewendet werden und dann die in der gesamten Organisation verwendet werden können.

Sie haben u. a. folgende Möglichkeiten:

-   Legen Sie eine Beschränkung von 200 Megabyte (MB) für die persönlichen Server Ordner der Benutzer fest, und senden Sie eine e-Mail-Benachrichtigung an Sie und den Benutzer, wenn 180 MB Speicher überschritten wurden.
-   Legen Sie für den freigegebenen Ordner einer Gruppe ein flexibles Kontingent von 500 MB fest. Wenn diese Speichergrenze erreicht ist, werden alle Benutzer in der Gruppe per e-Mail benachrichtigt, dass das Speicher Kontingent vorübergehend auf 520 MB erweitert wurde, sodass Sie unnötige Dateien löschen und die vordefinierte 500 MB-Kontingent Richtlinie einhalten können.
-   Empfangen Sie eine Benachrichtigung, wenn ein temporärer Ordner 2 Gigabyte (GB) der Verwendung erreicht, der Kontingent dieses Ordners allerdings nicht eingeschränkt wird, da er für einen Dienst auf dem Server erforderlich ist.

In diesem Abschnitt werden folgende Themen behandelt:

-   [Erstellen eines Kontingents](create-quota.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)
-   [Erstellen einer Kontingent Vorlage](create-quota-template.md)
-   [Bearbeiten von Kontingentvorlageneigenschaften](edit-quota-template-properties.md)
-   [Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents](edit-auto-apply-quota-properties.md)

> [!Note]
> Zum Festlegen von E-Mail-Benachrichtigungen und Berichtsfunktionen müssen Sie zuerst die Optionen des Ressourcen-Manager für Dateiserverkonfigurieren konfigurieren.

## <a name="see-also"></a>Siehe auch

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


