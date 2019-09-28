---
title: Windows Server 2019 und Kompatibilität von Microsoft-Serveranwendungen
description: Kompatibilitätstabelle für Windows Server 2019 und Microsoft-Serveranwendungen
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 40c90b179321062949af5eea6d92f6238fb9b460
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71391999"
---
# <a name="windows-server-2019-and-microsoft-server-application-compatibility"></a>Windows Server 2019 und Kompatibilität von Microsoft-Serveranwendungen

>Gilt für: Windows Server 2019

Diese Tabelle enthält die Microsoft-Serveranwendungen, die unter Windows Server 2019 installiert und verwendet werden können. Diese Informationen sind als Kurzreferenz vorgesehen und sollen nicht dazu dienen, die einzelnen Produktspezifikationen, Anforderungen, Ankündigungen oder allgemeinen Mitteilungen jeder einzelnen Serveranwendung zu ersetzen. In der offiziellen Dokumentation zu jedem Produkt können Sie sich genau über Kompatibilität und Optionen informieren.

Wenn du als Softwarehersteller weitere Informationen zur Kompatibilität von Windows Server mit nicht von Microsoft stammenden Anwendungen suchst, sieh dir das [Commercial App Certification-Portal](https://commercialappcertification.microsoft.com/) an.

| **Produkt**                                                  | **Unterstützt in Server Core**             |   | **Unterstützt auf Servern mit Desktopdarstellung** | **Veröffentlicht?** |   | **Weblink zum Produkt**                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
|--------------------------------------------------------------|------------------------------------------|---|-------------------------------------------------|---------------|---|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Exchange Server 2019                                         | Ja                                      |   | Ja                                             | Ja           |   | [Systemanforderungen für Exchange Server](https://docs.microsoft.com/Exchange/plan-and-deploy/system-requirements?view=exchserver-2019)                                                                        |
| Host Integration Server 2016, CU3                            | Ja                                      |   | Ja                                             | Ja            |   | [Systemanforderungen für Host Integration Server](https://docs.microsoft.com/host-integration-server/install-and-config-guides/system-requirements)                                                            |
| Visual Studio Team Foundation Server 2017                    | Ja\*                                    |   | Ja                                             | Ja           |   | [Team Foundation Server 2017](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                |
| Visual Studio Team Foundation Server 2018                    | Ja\*                                    |   | Ja                                             | Ja           |   | [Team Foundation Server 2018](https://docs.microsoft.com/tfs/server/requirements?view=vsts)                                                                                                                  |
| Microsoft SQL Server 2014                                    | Ja\*                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für die Installation von SQL Server 2014](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2014)   |
| Microsoft SQL Server 2016                                    | Ja\*                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für die Installation von SQL Server 2016](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2016)   |
| Microsoft SQL Server 2017                                    | Ja\*                                    |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für die Installation von SQL Server 2017](https://docs.microsoft.com/sql/sql-server/install/hardware-and-software-requirements-for-installing-sql-server?view=sql-server-2017) |
| Microsoft System Center Configuration Manager (Version 1806) | Als verwalteter Client ja, als Standortserver nein |   | Als verwalteter Client ja, als Standortserver nein        | Ja           |   | [Neues in Version 1806 von System Center Configuration Manager](https://docs.microsoft.com/sccm/core/plan-design/changes/whats-new-in-version-1806)                                                    |
| Microsoft System Center Operations Manager 2019              | Ja\*                                    |   | Ja                                             | Ja           |   | [Systemanforderungen für System Center Operations Manager](https://docs.microsoft.com/system-center/scom/plan-system-requirements)                                                                                                      |
| Microsoft System Center Virtual Machine Manager 2019         | Ja\*                                    |   | Ja                                             | Ja           |   | [Systemanforderungen für System Center Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm/system-requirements)                                                                                                      |
| Microsoft System Center Data Protection Manager 2019         | Nein                                       |   | Ja                                             | Ja           |   | [Vorbereiten der Umgebung für System Center Data Protection Manager](https://docs.microsoft.com/system-center/dpm/prepare-environment-for-dpm?view=sc-dpm-2019)                                                                                                      |
| SharePoint-Server 2016                                       | Nein                                       |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für SharePoint Server 2016](https://docs.microsoft.com/SharePoint/install/hardware-and-software-requirements)                                                                |
| SharePoint Server 2019                                       | Nein                                       |   | Ja                                             | Ja           |   | [Hardware- und Softwareanforderungen für SharePoint Server 2019](https://docs.microsoft.com/sharepoint/install/hardware-and-software-requirements-2019)                                                       |
| Project Server 2016                                          | Nein                                       |   | Ja                                             | Ja           |   | [Softwareanforderungen für Project Server 2016](https://docs.microsoft.com/project/software-requirements-for-project-server-2016)                                                                                |
| Project Server 2019                                          | Nein                                       |   | Ja                                             | Ja           |   | [Softwareanforderungen für Project Server 2019](https://docs.microsoft.com/project/software-requirements-for-project-server-2019)                                                                          |
| Skype for Business 2019                                      | Nein                                       |   | Ja                                             | Ja           |   | [Installationsanforderungen für Skype for Business Server](https://docs.microsoft.com/skypeforbusiness/deploy/install/install-prerequisites)                                                                          |

\*Möglicherweise bestehen Einschränkungen, oder das [Server Core-Feature on Demand (FOD) für die App-Kompatibilität](install-fod-19.md) ist erforderlich.
Lies die Informationen zum jeweiligen Produkt bzw. die FOD-Dokumentation.
