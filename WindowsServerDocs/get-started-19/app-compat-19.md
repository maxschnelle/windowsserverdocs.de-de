---
title: Windows Server 2019 und Microsoft-Server-Anwendungskompatibilität
description: Tabelle zur Anwendungskompatibilität für Windows Server 2019 und Microsoft-serveranwendungen
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
ms.openlocfilehash: e8bb8cda003ca151216e3b86d5884dfd05e73e6d
ms.sourcegitcommit: 5d55c3ebd1ceee7229ea9a9989c69cf93757ed88
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/21/2019
ms.locfileid: "9256943"
---
# Windows Server 2019 und Microsoft-Server-Anwendungskompatibilität

>Gilt für: Windows Server2019

Diese Tabelle enthält die Microsoft-Server-Anwendungen, die auf Windows Server 2019 Installation und Funktionen zu unterstützen. Diese Informationen sind als Kurzreferenz vorgesehen und sollen nicht dazu dienen, die einzelnen Produktspezifikationen, Anforderungen, Ankündigungen oder allgemeinen Mitteilungen jeder einzelnen Serveranwendung zu ersetzen. In der offiziellen Dokumentation zu jedem Produkt können Sie sich genau über Kompatibilität und Optionen informieren.

Wenn Sie weitere Informationen zur Kompatibilität von Windows Server mit nicht von Microsoft stammenden Anwendungen suchen Software Anbieter-Partner sind, besuchen Sie die [Commercial App-Zertifizierung-Portal](https://commercialappcertification.microsoft.com/).
| **Produkt**                                                  | **Auf servercore unterstützt**             |   | **Auf Server mit Desktop Experience unterstützt** | **Veröffentlicht?** |   | **Produkt-Weblink**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange-Server 2019                                         | Ja                                      |   | Ja                                             | Ja           |   | [Exchange Server-Systemanforderungen](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integrationsserver 2016 CU3                            | Ja                                      |   | Ja                                             | Nein            |   | [Host Integration Server-Systemanforderungen](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | Yes\ *                                    |   | Ja                                             | Ja           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | Yes\ *                                    |   | Ja                                             | Ja           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | Yes\ *                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für die Installation von SQL Server 2014](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | Yes\ *                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für die Installation von SQLServer 2016](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | Yes\ *                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für die Installation von SQLServer 2017](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (Version 1806) | Ja als verwalteten Client nicht als Standortserver |   | Ja als verwalteten Client nicht als Standortserver        | Ja           |   | [Was ist neu in Version 1806 von System Center Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | Yes\ *                                    |   | Ja                                             | Ja           |   | [Systemanforderungen für System Center Operations Manager](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | Yes\ *                                    |   | Ja                                             | Ja           |   | [Systemanforderungen für System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | Nein                                       |   | Ja                                             | Ja           |   | [Vorbereiten der Umgebung für System Center Data Protection Manager](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint-Server 2016                                       | Nein                                       |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für SharePoint Server 2016](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | Nein                                       |   | Ja                                             | Ja           |   | [Hardware- und Software-Anforderungen für SharePoint Server 2019](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | Nein                                       |   | Ja                                             | Ja           |   | [Softwareanforderungen für Project Server 2016](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Projektserver 2019                                          | Nein                                       |   | Ja                                             | Ja           |   | [Softwareanforderungen für Project Server 2019](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| Skype für Unternehmen 2019                                      | Nein                                       |   | Ja                                             | Ja           |   | [Voraussetzungen für Skype for Business-Server installieren](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*May gelten Einschränkungen oder erfordern die [Server Core-App-Kompatibilität-Feature on Demand (FOD). ](install-fod-19.md)
Finden Sie in bestimmten Produkt oder FOD-Dokumentation.
