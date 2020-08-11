---
title: 'Remotedesktopdienste: Erstellen überall'
description: Planungsinformationen zur Unterstützung Ihrer Entscheidung, wo Ihre RDS-Bereitstellung gehostet werden soll.
ms.topic: article
ms.assetid: c803a383-0eea-4e11-bca5-d204ab758048
author: lizap
ms.author: elizapo
ms.date: 09/07/2016
manager: dongill
ms.openlocfilehash: 0956fec88fc0bc07fb964d0eb4c2ff0b976628bf
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87946373"
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