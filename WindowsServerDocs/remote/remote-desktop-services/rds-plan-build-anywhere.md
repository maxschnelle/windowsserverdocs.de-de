---
title: 'Remotedesktopdienste: Erstellen überall'
description: Planungsinformationen zur Unterstützung Ihrer Entscheidung, wo Ihre RDS-Bereitstellung gehostet werden soll.
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
ms.openlocfilehash: 4563108d2efa9cd864fbe75fa82349d21659a941
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "63712332"
---
# <a name="remote-desktop-services---build-anywhere"></a>Remotedesktopdienste: Erstellen überall

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016

Sie können lokal, in der Cloud oder in einer aus beiden Optionen bestehenden Hybridumgebung bereitstellen. Ändern Sie Ihre Bereitstellung, wenn sich Ihre geschäftlichen Anforderungen ändern.

Unabhängig davon, wo Sie sich befinden, die zugrunde liegende [Architektur](desktop-hosting-logical-architecture.md) der Remotedesktopdienste-Umgebung bleibt die gleiche:
- Sie benötigen in jedem Fall einen Server mit Internetverbindung, um RD Web Access und RD Gateway für externe Benutzer verwenden zu können
- Sie benötigen in jedem Fall Active Directory und – für Umgebungen mit Hochverfügbarkeit – eine SQL-Datenbank zum Speichern der Eigenschaften von Benutzern und Remotedesktops
- Sie benötigen in jedem Fall Verbindungszugriff zwischen den RD-Infrastrukturrollen (RD-Verbindungsbroker, RD-Gateway, RD-Lizenzierung und RD Web Access) und die RDSH- oder RDVH-Endhosts, um Endbenutzer mit ihren Desktops oder Anwendungen verbinden zu können.

Mithilfe dieser Flexibilität sichern Sie sich das beste aus beiden Welten:
- Die Einfachheit und nutzungsbasierten Zahlungsverfahren aus der Cloud und der Onlinewelt.
- Die Vertrautheit und Problemlosigkeit bei der Nutzung der lokal bereits vorhandenen umfangreichen Ressourcen.

Weitere Informationen finden Sie in der Vorgehensweise zum [Erstellen und Bereitstellen Ihrer Remotedesktopdienste-Bereitstellung](rds-build-and-deploy.md).