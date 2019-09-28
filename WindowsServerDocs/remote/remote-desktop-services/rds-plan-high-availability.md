---
title: Remotedesktopdienste – Hochverfügbarkeit
description: Planen der Informationen für die Einrichtung einer hoch verfügbaren RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ec630ea0-ab80-4dfe-a25f-f4f601651f72
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 3d3d216c528b0b83d9dfd5265fe153a388c7382a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387284"
---
# <a name="remote-desktop-services---high-availability"></a>Remotedesktopdienste – Hochverfügbarkeit

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Fehler und Drosselung sind in umfangreichen Systemen unvermeidlich. Es ist einfach, Remotedesktop-Infrastrukturrollen einzurichten, um Hochverfügbarkeit zu unterstützen und es Endbenutzern zu ermöglichen, jederzeit problemlos eine Verbindung herzustellen.

In den Remotedesktopdiensten (Remote Desktop Services, RDS) repräsentieren die folgenden Elemente die Remotedesktop-Infrastrukturrollen. In den einzelnen Artikeln findest du Anleitungen dazu, wie du Hochverfügbarkeit herstellst:
- [Remotedesktop-Verbindungsbroker](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)
- [Remotedesktopgateway](Deploy-a-RD-Web-Access-and-Gateway-farm.md)
- Remotedesktoplizenzierung
- [Remotedesktop-Webzugriff](Deploy-a-RD-Web-Access-and-Gateway-farm.md)

Hochverfügbarkeit wird durch Duplizierung jedes dieser Rollendienste auf sekundären Computern erzielt. In Azure kannst du für eine garantierte Betriebszeit sorgen, indem du die Gruppe mit den beiden virtuellen Computern (die die gleiche Rolle hosten) in einer Verfügbarkeitsgruppe platzierst.

Zusätzlich zu Verfügbarkeitsgruppen kannst du jetzt von Azure SQL-Datenbank und der zugehörigen von Azure gestützten SLA profitieren, um sicherzustellen, dass du jederzeit über Verbindungsinformationen verfügst und Benutzer zu ihren Desktops und Anwendungen umleiten kannst.

Bewährte Methoden zum Erstellen deiner RDS-Umgebung findest du in der [Referenzarchitektur für das Desktophosting](desktop-hosting-reference-architecture.md).