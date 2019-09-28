---
title: Willkommen bei den Remotedesktopdiensten in Windows Server 2016
description: Bietet eine Übersicht der Remotedesktopdienste
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: chrimo
ms.date: 02/22/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 52b9e09f-39e0-41a9-9d3b-4d5f4eacf3e0
author: christianmontoya
manager: scottman
ms.localizationpriority: medium
ms.openlocfilehash: 46a04905d5247ae940ca900297171d1112cf936b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404204"
---
# <a name="welcome-to-remote-desktop-services"></a>Willkommen bei den Remotedesktopdiensten 

Remotedesktopdienste (RDS) sind die Plattform der Wahl zum Erstellen von Virtualisierungslösungen für jede Anforderung von Endbenutzern, einschließlich der Bereitstellung individueller virtualisierter Anwendungen, sicherem mobilem und Remote-Desktopzugriff und der Möglichkeit für Endbenutzer, ihre Anwendungen und Desktops in der Cloud auszuführen.

![Remotedesktopdienste – Übersicht](./media/rds-overview.png)

RDS bietet flexible Bereitstellung, Kosteneffizienz und Erweiterbarkeit: alles realisiert mithilfe einer Vielzahl von Bereitstellungsoptionen, einschließlich Windows Server 2016 für lokale Bereitstellungen, Microsoft Azure für Cloudbereitstellungen und eines robusten Spektrums an Partnerlösungen.

Abhängig von Ihrer Umgebung und Ihren Wünschen können Sie die RDS-Lösung für sitzungsbasierte Virtualisierung, als virtuelle Desktopinfrastruktur (VDI) oder als Kombination daraus einrichten:

- **Sitzungsbasierte Virtualisierung**: Nutze die Rechenleistung von Windows Server, um eine kostengünstige Multisessionumgebung für die täglichen Workloads deiner Benutzer bereitzustellen.
- **VDI**: Nutzen Sie den Windows-Client, um die hohe Leistung, App-Kompatibilität und Vertrautheit zu bieten, die Ihre Benutzer von ihrer Windows-Desktopdarstellung gewohnt sind.

Innerhalb dieser Virtualisierungsumgebungen besitzen Sie zusätzliche Flexibilität in dem, was Sie für Ihre Benutzer veröffentlichen:

- **Desktops**: Bieten Sie Ihren Benutzern eine vollständige Desktoperfahrung mit einer Vielzahl von Anwendungen, die Sie installieren und verwalten. Ideal für Benutzer, die diese Computer als primäre Arbeitsstationen nutzen oder von Thin Clients umsteigen, wie etwa von MultiPoint-Diensten.
- **RemoteApps**: Geben Sie einzelne Anwendungen an, die auf dem virtuellen Computer gehostet/ausgeführt werden, sich aber verhalten, als würden sie wie lokale Anwendungen auf dem Desktop des Benutzers ausgeführt. Die Apps haben einen eigenen Eintrag in der Taskleiste, ihre Größe lässt sich verändern, und sie können zwischen Monitoren verschoben werden. Ideal zum Bereitstellen und Verwalten von wichtigen Anwendungen in der sicheren Remoteumgebung, trotzdem können Benutzer an ihren eigenen Desktops arbeiten und sie anpassen.

Für Umgebungen, in denen Kosteneffizienz kritisch ist und Sie die Vorzüge der Bereitstellung von vollständigen Desktops in einer sitzungsbasierten Virtualisierungsumgebung ausweiten möchten, können Sie [MultiPoint-Dienste](../multipoint-services/multipoint-services.md) verwenden, um den besten Wert zu realisieren. 

Dank dieser Optionen und Konfiguration haben Sie die Flexibilität, die von Ihren Benutzern benötigten Desktops und Anwendungen remote, sicher und kostengünstig bereitzustellen.

## <a name="next-steps"></a>Nächste Schritte

Hier sind einige weiterführende Schritte, die Ihnen helfen sollen, ein besseres Verständnis von RDS zu entwickeln und sogar mit der Bereitstellung Ihrer eigenen Umgebung zu beginnen:
-   Verstehen der [unterstützten Konfigurationen](rds-supported-config.md) für RDS mit den verschiedenen Versionen von Windows und Windows Server
-   [Planen und Entwerfen](rds-plan-and-design.md) einer RDS-Umgebung, die verschiedenen Anforderungen Rechnung trägt, beispielsweise Hochverfügbarkeit und mehrstufige Authentifizierung.
-   Überprüfen der [Remotedesktopdienste-Architekturmodelle](desktop-hosting-logical-architecture.md), die sich optimal für Ihre gewünschte Umgebung eignen.
-   Beginnen der [Bereitstellung Ihrer RDS-Umgebung mit ARM und Azure Marketplace](rds-in-azure.md).
