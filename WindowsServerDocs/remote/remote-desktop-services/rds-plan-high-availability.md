---
title: Remote Desktop Services – hohe Verfügbarkeit
description: Planen die Informationen zum Einrichten einer hoch verfügbaren RDS-Bereitstellung.
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: b5a2bd38c8831063d6fd2ba525b71a10403b8fc2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839261"
---
# <a name="remote-desktop-services---high-availability"></a>Remote Desktop Services – hohe Verfügbarkeit

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Fehler und Drosselung sind unvermeidlich großmaßstäbliche Systeme. Es ist einfach zum Einrichten von Remote Desktop-Infrastrukturrollen, Unterstützung für hochverfügbarkeit und Endbenutzern ermöglichen, verbinden Sie nahtlos, jedes Mal, wenn.

In Remote Desktop Services stellen die folgenden Elemente der Infrastrukturrollen von Remotedesktop mit ihren entsprechenden Anleitungen zum Herstellen von hochverfügbarkeit dar:
- [Remotedesktop-Verbindungsbroker](Deploy-a-Remote-Desktop-Connection-Broker-cluster.md)
- [Remotedesktopgateway](Deploy-a-RD-Web-Access-and-Gateway-farm.md)
- Remotedesktoplizenzierung
- [Web Access für Remotedesktop](Deploy-a-RD-Web-Access-and-Gateway-farm.md)

Hoher Verfügbarkeit wird hergestellt, indem die einzelnen Rollendienste auf einem zweiten Computer dupliziert wird. In Azure erhalten Sie eine garantierte Verfügbarkeit durch den Satz von zwei virtuellen Computer (in der gleichen Rolle gehostet) in einer verfügbarkeitsgruppe platzieren legt diese fest.

Zusammen mit Verfügbarkeitsgruppen können Sie jetzt die Leistungsfähigkeit von Azure SQL-Datenbank und der Azure-Backup-SLA, um sicherzustellen, dass Sie immer Informationen über die Verbindung und die können Benutzer auf ihre Desktops und Anwendungen nutzen.

Bewährte Methoden zum Erstellen der RDS-Umgebung finden Sie unter den [desktophosting-Architektur](desktop-hosting-reference-architecture.md).