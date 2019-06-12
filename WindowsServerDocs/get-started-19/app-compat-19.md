---
title: 2019 für Windows Server und Microsoft Server-Anwendungskompatibilität
description: Tabelle für die Kompatibilität für Windows Server-2019 und Microsoft-serveranwendungen
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2afe7c32-1fda-4441-989b-4115dabdcd34
author: coreyp
ms.author: coreyp-at-msft
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 8dcaff6ab8a296790158f59035bd4a5c1a093cbd
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442370"
---
# <a name="windows-server-2019-and-microsoft-server-application-compatibility"></a>2019 für Windows Server und Microsoft Server-Anwendungskompatibilität

>Gilt für: Windows Server 2019

Diese Tabelle enthält die Microsoft-serveranwendungen, die Installation und Funktionalität 2019 für Fenster-Server zu unterstützen. Diese Informationen sind als Kurzreferenz vorgesehen und sollen nicht dazu dienen, die einzelnen Produktspezifikationen, Anforderungen, Ankündigungen oder allgemeinen Mitteilungen jeder einzelnen Serveranwendung zu ersetzen. In der offiziellen Dokumentation zu jedem Produkt können Sie sich genau über Kompatibilität und Optionen informieren.

Wenn Sie weitere Informationen zur Kompatibilität von Windows Server mit Microsoft-fremden Anwendungen suchen Software Vendor-Partner sind, finden Sie auf die [professionellen App-Zertifizierung Portal](https://commercialappcertification.microsoft.com/).

| **Product**                                                  | **Auf Server Core unterstützt**             |   | **Für Server mit Desktopdarstellung unterstützt** | **Veröffentlicht?** |   | **Weblink Produkt**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | Ja                                      |   | Ja                                             | Ja           |   | [Systemanforderungen für Exchange Server](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integrationsserver 2016 CU3                            | Ja                                      |   | Ja                                             | Ja            |   | [Systemanforderungen für Host Integration Server](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen zum Installieren von SQLServer 2014](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen zum Installieren von SQLServer 2016](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen zum Installieren von SQLServer 2017](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (Version 1806) | Ja, die als verwalteter Client, nicht wie der Standortserver |   | Ja, die als verwalteter Client, nicht wie der Standortserver        | Ja           |   | [Was ist neu in Version 1806 von System Center Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Systemanforderungen für System Center Operations Manager](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager-2019         | "Ja"\*                                    |   | Ja                                             | Ja           |   | [Systemanforderungen für System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | Nein                                       |   | Ja                                             | Ja           |   | [Vorbereiten der Umgebung für System Center Data Protection Manager](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint-Server 2016                                       | Nein                                       |   | Ja                                             | Ja           |   | [Hardware- und softwareanforderungen für SharePoint Server 2016](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | Nein                                       |   | Ja                                             | Ja           |   | [Hardware- und softwareanforderungen für SharePoint Server 2019](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | Nein                                       |   | Ja                                             | Ja           |   | [Softwareanforderungen für Project Server 2016](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Projektserver 2019                                          | Nein                                       |   | Ja                                             | Ja           |   | [Softwareanforderungen für Project Server 2019](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| Skype for Business 2019                                      | Nein                                       |   | Ja                                             | Ja           |   | [Installieren von erforderlichen Komponenten für Skype for Business Server](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*Möglicherweise Einschränkungen oder fordert den [Server Core-App-Kompatibilitätsfeature auf Nachfrage (Feature-On)](install-fod-19.md).
Finden Sie in bestimmten Produkt oder Feature-On-Dokumentation.
