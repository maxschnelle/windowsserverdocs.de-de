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
ms.openlocfilehash: febcd6ab0744a7fddd024e1f0afdb93711e8939a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829541"
---
# <a name="quota-management"></a>Kontingentverwaltung

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2019, Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Sie können auf dem Knoten **Kontingentverwaltung** des Ressourcen-Manager für Dateiserver Microsoft<sup>®</sup> Management Console (MMC)-Snap-Ins folgende Aufgaben ausführen:

-   Mithilfe von Kontingenten können Sie den für ein Volume oder einen Ordner zulässigen Platz beschränken und Benachrichtigungen generieren, wenn die Kontingentgrenzen erreicht oder überschritten werden.
-   Generieren von automatisch zugewiesenen Kontingenten, die für alle vorhandenen Unterordner in einem Volume oder Ordner und allen Unterordnen gelten, die in Zukunft erstellt werden.
-   Legen Sie Kontingente fest, die ganz einfach auf neue Volumes oder Ordner angewendet werden und dann die in der gesamten Organisation verwendet werden können.

Sie haben u. a. folgende Möglichkeiten:

-   Platzieren Sie einen Grenzwert von 200 Megabyte (MB) für Benutzer Persönliche Serverordner, mit einer e-Mail-Benachrichtigung an Sie und der Benutzer gesendet, wenn es sich bei 180 MB Speicher überschritten wurde.
-   Legen Sie ein flexibles Kontingent von 500 MB für eine Gruppe der freigegebenen Ordner. Wenn diese speicherbeschränkung erreicht wird, werden alle Benutzer in der Gruppe per E-mail benachrichtigt, die das Speicherkontingent vorübergehend auf 520 MB erweitert wurde, damit sie nicht benötigte Dateien löschen können, und die vordefinierten Kontingentrichtlinie von 500 MB einzuhalten.
-   Empfangen Sie eine Benachrichtigung, wenn ein temporärer Ordner 2 Gigabyte (GB) der Verwendung erreicht, der Kontingent dieses Ordners allerdings nicht eingeschränkt wird, da er für einen Dienst auf dem Server erforderlich ist.

In diesem Abschnitt werden folgende Themen behandelt:

-   [Erstellen Sie ein Kontingent](create-quota.md)
-   [Erstellen eines automatisch zugewiesenen Kontingents](create-auto-apply-quota.md)
-   [Erstellen Sie eine Kontingentvorlage](create-quota-template.md)
-   [Kontingentvorlageneigenschaften bearbeiten](edit-quota-template-properties.md)
-   [Bearbeiten Sie die automatische Anwenden von Kontingenteigenschaften](edit-auto-apply-quota-properties.md)

> [!Note]
> Zum Festlegen von E-Mail-Benachrichtigungen und Berichtsfunktionen müssen Sie zuerst die Optionen des Ressourcen-Manager für Dateiserverkonfigurieren konfigurieren.

## <a name="see-also"></a>Siehe auch

-   [Einstellung File Server Resource Manager-Optionen](setting-file-server-resource-manager-options.md)


