---
title: Aktualisieren deines Remotedesktop-Sitzungshosts auf Windows Server 2016
description: In diesem Artikel wird beschrieben, wie Sie Ihre vorhandenen Bereitstellungen der Remotedesktopdienste auf Windows Server 2016 aktualisieren.
ms.author: spatnaik
ms.date: 08/01/2016
ms.topic: article
ms.assetid: 5c9b98b8-4eca-4a39-b10b-2bac729f7f44
author: spatnaik
manager: scottman
ms.openlocfilehash: b825c79ac698f2a61c81628180f1d7cc14b826e8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87948843"
---
# <a name="upgrading-your-remote-desktop-session-host-to-windows-server-2016"></a>Aktualisieren deines Remotedesktop-Sitzungshosts auf Windows Server 2016

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

> [!IMPORTANT]
> Alle Anwendungen müssen vor dem Upgrade deinstalliert und nach dem Upgrade neu installiert werden, um App-Kompatibilitätsprobleme zu vermeiden, die infolge des Upgrades auftreten können.

## <a name="supported-os-upgrades-with-rds-role-installed"></a>Unterstützte Betriebssystemupgrades mit installierter RDS-Rolle
Upgrades auf Windows Server 2016 werden nur von Windows Server 2012 R2 und Windows Server 2016 TP5 unterstützt.

## <a name="upgrading-a-rds-session-based-collection"></a>Upgrade einer auf einer RDS-Sitzung basierenden Sammlung
Um die Ausfallzeit möglichst gering zu halten, solltest du beim Aktualisieren einer auf einer RDS-Sitzung basierenden Sammlung die folgenden Schritte ausführen:

1. Ermittle die Server, für die das Upgrade ausgeführt werden soll (beispielsweise die Hälfte der Server in der Sammlung).
2. Verhindere neue Verbindungen mit diesen Servern, indem du **Neue Verbindungen zulassen** auf „false“ festlegst.
3. Melde alle Sitzungen auf diesen Servern ab.
4. Entferne diese Server aus der Sammlung.
5. Aktualisiere die Server auf Windows Server 2016.
6. Lege für die übrigen Server in der Sammlung die Option **Neue Verbindungen zulassen** auf „false“ fest.
7. Füge die aktualisierten Server wieder ihren entsprechenden Sammlungen hinzu.
8. Entferne die verbleibenden Server, für die ein Upgrade ausgeführt werden soll, aus der Sammlung.
9. Lege für die aktualisierten Server in der Sammlung die Option **Neue Verbindungen zulassen** auf „true“ fest.
10. Führe jetzt die oben angegebenen Schritte 3 bis 9 aus, um die verbleibenden Server in der Bereitstellung zu aktualisieren.

## <a name="upgrading-a-standalone-rd-session-host-server"></a>Aktualisieren eines eigenständigen RD-Sitzungshostservers
Ein eigenständiger RD-Sitzungshostserver kann jederzeit aktualisiert werden.