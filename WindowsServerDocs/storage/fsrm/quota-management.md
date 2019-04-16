---
title: Kontingentverwaltung
description: Dieser Artikel beschreibt, wie Sie Kontingente erstellen und verwalten
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 60436f12e07b8a3f16312829d53a2885c98f30ed
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2017
---
# <a name="quota-management"></a>Kontingentverwaltung

> Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Sie können auf dem Knoten **Kontingentverwaltung** des Ressourcen-Manager für Dateiserver Microsoft<sup>®</sup> Management Console (MMC)-Snap-Ins folgende Aufgaben ausführen:

-   Mithilfe von Kontingenten können Sie den für ein Volume oder einen Ordner zulässigen Platz beschränken und Benachrichtigungen generieren, wenn die Kontingentgrenzen erreicht oder überschritten werden.
-   Generieren von automatisch zugewiesenen Kontingenten, die für alle vorhandenen Unterordner in einem Volume oder Ordner und allen Unterordnen gelten, die in Zukunft erstellt werden.
-   Legen Sie Kontingente fest, die ganz einfach auf neue Volumes oder Ordner angewendet werden und dann die in der gesamten Organisation verwendet werden können.

Sie haben u. a. folgende Möglichkeiten:

-   Legen Sie eine Beschränkung von 200Megabyte (MB) für die persönlichen Serverordner von Benutzern mit einer E-Mail-Benachrichtigung fest, die an Sie und den Benutzer gesendet wird, wenn 180MB Speicherplatz überschritten wurde.
-   Legen Sie ein flexibles Kontingent von 500MB für den freigegebenen Ordner einer Gruppe fest. Wird diese Speicherbeschränkung erreicht, werden alle Benutzer in der Gruppe per E-Mail benachrichtigt, dass das Speicherkontingent vorübergehend auf 520MB erweitert wurde. Daraufhin können die Benutzer nicht benötigte Dateien löschen, um die vordefinierten Kontingentrichtlinie von 500MB einzuhalten.
-   Empfangen Sie eine Benachrichtigung, wenn ein temporärer Ordner 2Gigabyte (GB) der Verwendung erreicht, der Kontingent dieses Ordners allerdings nicht eingeschränkt wird, da er für einen Dienst auf dem Server erforderlich ist.

In diesem Abschnitt werden folgende Themen behandelt:

-   [Erstellen eines Kontingents](create-quota.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)
-   [Erstellen einer Kontingentvorlage](create-quota-template.md)
-   [Bearbeiten von Kontingentvorlageneigenschaften](edit-quota-template-properties.md)
-   [Bearbeiten der Eigenschaften des automatisch zugewiesenen Kontingents](edit-auto-apply-quota-properties.md)

> [!Note]
> Zum Festlegen von E-Mail-Benachrichtigungen und Berichtsfunktionen müssen Sie zuerst die Optionen des Ressourcen-Manager für Dateiserverkonfigurieren konfigurieren.

## <a name="see-also"></a>Weitere Informationen:

-   [Festlegen der Optionen des Ressourcen-Managers für Dateiserver](setting-file-server-resource-manager-options.md)


