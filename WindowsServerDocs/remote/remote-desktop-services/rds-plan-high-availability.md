---
title: Remotedesktopdienste – Hochverfügbarkeit
description: Planen der Informationen für die Einrichtung einer hoch verfügbaren RDS-Bereitstellung.
ms.topic: article
ms.assetid: ec630ea0-ab80-4dfe-a25f-f4f601651f72
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: c50c66bee8f9f387497ef2f5971dbee5e1b402c6
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87955007"
---
# <a name="remote-desktop-services---high-availability"></a>Remotedesktopdienste – Hochverfügbarkeit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Fehler und Drosselung sind in umfangreichen Systemen unvermeidlich. Es ist einfach, Remotedesktop-Infrastrukturrollen einzurichten, um Hochverfügbarkeit zu unterstützen und es Endbenutzern zu ermöglichen, jederzeit problemlos eine Verbindung herzustellen.

In den Remotedesktopdiensten (Remote Desktop Services, RDS) repräsentieren die folgenden Elemente die Remotedesktop-Infrastrukturrollen. In den einzelnen Artikeln findest du Anleitungen dazu, wie du Hochverfügbarkeit herstellst:
- [Remotedesktop-Verbindungsbroker](./rds-connection-broker-cluster.md)
- [Remotedesktopgateway](./rds-rdweb-gateway-ha.md)
- Remotedesktoplizenzierung
- [Remotedesktop-Webzugriff](./rds-rdweb-gateway-ha.md)

Hochverfügbarkeit wird durch Duplizierung jedes dieser Rollendienste auf sekundären Computern erzielt. In Azure kannst du für eine garantierte Betriebszeit sorgen, indem du die Gruppe mit den beiden virtuellen Computern (die die gleiche Rolle hosten) in einer Verfügbarkeitsgruppe platzierst.

Zusätzlich zu Verfügbarkeitsgruppen kannst du jetzt von Azure SQL-Datenbank und der zugehörigen von Azure gestützten SLA profitieren, um sicherzustellen, dass du jederzeit über Verbindungsinformationen verfügst und Benutzer zu ihren Desktops und Anwendungen umleiten kannst.

Bewährte Methoden zum Erstellen deiner RDS-Umgebung findest du in der [Referenzarchitektur für das Desktophosting](desktop-hosting-reference-architecture.md).
