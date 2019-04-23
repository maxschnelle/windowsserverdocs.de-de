---
title: Remote Desktop Services – erstellen Sie eine beliebige Stelle
description: Informationen zur Planung können Sie bestimmen, wo Sie Ihre RDS-Bereitstellung zu hosten.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c803a383-0eea-4e11-bca5-d204ab758048
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: cbb8e73d753b1fe4f0293cf4427c634020a23a42
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869511"
---
# <a name="remote-desktop-services---build-anywhere"></a>Remote Desktop Services – erstellen Sie eine beliebige Stelle

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Stellen Sie lokal, in der Cloud oder in einer Hybriden der beiden bereit. Ändern Sie die Bereitstellung aus, wie Sie Ihre geschäftlichen Anforderungen ändern.

Unabhängig davon, wo Sie sind, die zugrunde liegende [Architektur](desktop-hosting-logical-architecture.md) von der Remote Desktop Services Umgebung bleibt unverändert:
- Sie benötigen immer noch einen Server mit Internetverbindung Nutzen von Web Access für Remotedesktop und RD-Gateway für externe Benutzer
- Dennoch benötigen Sie ein Active Directory und--für hoch verfügbare Umgebungen – einer SQL-Datenbank, House-Benutzer und dem Remotedesktop-Eigenschaften
- Sie benötigen immer noch Zugriff der Kommunikation zwischen der Infrastrukturrollen Remotedesktop (RD-Verbindungsbroker, RD-Gateway, RD-Lizenzierung und Web Access für Remotedesktop) und dem Ende RDSH oder RDVH-Hosts, um die Endbenutzer auf ihre Desktops oder Anwendungen eine Verbindung herstellen zu können.

Diese Flexibilität können Sie das beste aus beiden Welten zu erzielen:
- Die Einfachheit und mit nutzungsbasierter Bezahlung-Methoden, mit der Cloud und die online-Welt verknüpft ist.
- Die Kenntnisse und diejenige Methode nutzen Sie umfangreiche Ressourcen, die bereits vorhanden sind lokal.

Weitere Informationen finden Sie in der Vorgehensweise [erstellen und Bereitstellen Ihrer Remote Desktop Services-Bereitstellung](rds-build-and-deploy.md).