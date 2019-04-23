---
title: Architektur der Remotedesktopdienste
description: Architekturdiagramme für Remotedesktopdienste
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 02/10/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7f73bb0a-ce98-48a4-9d9f-cf7438936ca1
author: lizap
manager: dongill
ms.openlocfilehash: ba597318cdaf1d4659a72905eeb4e252c9020e49
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887871"
---
# <a name="remote-desktop-services-architecture"></a>Architektur der Remotedesktopdienste

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Im folgenden finden Sie verschiedene Konfigurationen für die Bereitstellung von Remote Desktop Services Hosten von Windows-apps und Desktops für Endbenutzer.

>[!NOTE]
> Die folgenden Architekturdiagramme zeigen die Verwendung von RDS in Azure. Sie können jedoch Remote Desktop Services lokal bereitstellen und in anderen Clouds. Diese Diagramme werden in erster Linie veranschaulichen, wie die RDS-Rollen zusammengestellt werden, und andere Dienste verwenden.

## <a name="standard-rds-deployment-architectures"></a>Standardarchitekturen für RDS-Bereitstellung

Remote Desktop Services verfügt über zwei standard-Architekturen:
-   Einfache Bereitstellung – enthält die minimale Anzahl von Servern zum Erstellen einer vollständig wirksam RDS-Umgebung
-   Bereitstellung mit hoher Verfügbarkeit – enthält alle erforderlichen Komponenten für die höchste garantierte Betriebszeit für Ihre RDS-Umgebung

### <a name="basic-deployment"></a>Einfache Bereitstellung

![Grundlegenden RDS-Bereitstellung](./media/basic-rds.png)

### <a name="highly-available-deployment"></a>Bereitstellung mit hoher Verfügbarkeit

![Hoch verfügbaren RDS-Bereitstellung](./media/ha-rds.png)

## <a name="rds-architectures-with-unique-azure-paas-roles"></a>RDS-Architekturen mit eindeutigen Azure-PaaS-Rollen

Auch wenn die RDS-Bereitstellung und Standardarchitekturen den meisten Fällen entspricht, Azure engagiert sich auch weiterhin Erstanbieter-PaaS-Lösungen, Kundenwert Laufwerk. Im folgenden finden Sie einige Architekturen zeigt, wie sie mit RDS integrieren

### <a name="rds-deployment-with-azure-ad-domain-services"></a>RDS-Bereitstellung mit Azure AD Domain Services

Die beiden oben stehenden Standardarchitektur Diagrammen basieren auf einer herkömmlichen Active Directory (AD), die auf einem Windows Server-VM bereitgestellt. Jedoch wenn Sie nicht über eine herkömmliche AD verfügen und nur über Azure AD-Mandanten verfügen, über Dienste wie Office 365 – aber weiterhin RDS nutzen möchten, können Sie [Azure AD Domain Services](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview) zum Erstellen einer vollständig verwalteten Domäne in Ihrem Azure-IaaS Umgebung, die die Benutzern verwendet, die in Azure AD-Mandanten vorhanden sein. Dadurch wird die Komplexität der manuellen Synchronisierung von Benutzern und Verwalten von mehr virtuelle Computer entfernt. Azure Active Directory-Domänendienste in keiner der Bereitstellungen ausgeführt werden kann: grundlegende oder hoch verfügbar.

![Azure AD und RDS-Bereitstellung](./media/aadds-rds.png)

### <a name="rds-deployment-with-azure-ad-application-proxy"></a>RDS-Bereitstellung mit Azure AD-Anwendungsproxy

Die beiden oben stehenden Standardarchitektur Diagrammen verwenden Sie die Web-/Remotedesktopgateway-Server als Einstiegspunkt in das System RDS Internetzugriff. In einigen Umgebungen bevorzugen Administratoren ihre eigenen Server aus dem Umkreis entfernen und stattdessen Technologien, die auch zusätzliche Sicherheit durch Technologien für reverse-Proxy bereitstellen. Die [Azure AD-Anwendungsproxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-get-started) PaaS-Rolle passt hervorragend zu diesem Szenario.

Unterstützte Konfigurationen und wie Sie dieses Setup erstellen, finden Sie unter Vorgehensweise [Veröffentlichen des Remotedesktops mit Azure AD-Anwendungsproxy](/azure/active-directory/application-proxy-publish-remote-desktop).

![RDS mit Azure AD-Anwendungsproxy](./media/aadappproxy-rds.png)
