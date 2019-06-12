---
title: RDS - erstellen und bereitstellen
description: Schritte zum Erstellen einer Bereitstellung von Remotedesktop
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/18/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: 309ea068488d005eabfe22f8ea055f85dd098452
ms.sourcegitcommit: 48bb3e5c179dc520fa879b16c9afe09e07c87629
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66453073"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>Erstellen Sie und Bereitstellen Sie Ihrer Remote Desktop Services-Bereitstellung

Eine Remote Desktop Services-Bereitstellung ist die Infrastruktur verwendet, um apps und Ressourcen für Ihre Benutzer freigeben. Je nach der Erfahrung, die Sie bereitstellen möchten, können Sie es beliebig klein oder komplexe vornehmen, wie Sie benötigen. Remotedesktopbereitstellungen auf einfache Weise skaliert werden. Sie können zu erhöhen und Reduzieren von Web Access für Remotedesktop, werden Gateway "," Connection Broker "und" Session Host-Servern an. Sie können Remote Desktop Connection Broker verwenden, um arbeitsauslastungen zu verteilen. Active Directory-basierte Authentifizierung bietet eine äußerst sichere Umgebung. 

[Remotedesktopclients](clients/remote-desktop-clients.md) Aktivieren des Zugriffs von jedem Windows, Apple und Android-Computer, Tablet oder Telefon.

Finden Sie unter [Remote Desktop Services-Architektur](desktop-hosting-logical-architecture.md) für ausführliche Informationen zu den unterschiedlichen Komponenten, die zusammenarbeiten, um die Remotedesktopdienste-Bereitstellung zu erstellen.

Haben Sie eine vorhandene basierende auf einer früheren Version von Windows Server Remote Desktop-Bereitstellung? Sehen Sie sich die Optionen zum Wechsel zu WIndows Server 2016, wenn Sie neue und bessere Funktionen bezüglich Leistung und Skalierung nutzen können:

- [Migrieren Sie Ihre RDS-Bereitstellung auf Windows Server 2016](migrate-rds-role-services.md)
- [Aktualisieren Sie Ihre RDS-Bereitstellung auf Windows Server 2016](upgrade-to-rds-2016.md)

Möchten Sie zum Erstellen einer neuen Remotedesktop-Bereitstellung? Verwenden Sie zum Bereitstellen von Remotedesktop in Windows Server 2016 die folgende Informationen ein:

- [Bereitstellen der Infrastruktur Remote Desktop Services](rds-deploy-infrastructure.md)
- [Erstellen einer sitzungssammlung zum Speichern von den apps und Ressourcen, die Sie freigeben möchten.](rds-create-collection.md)
- [Lizenzieren Sie Ihre RDS-Bereitstellung](rds-client-access-license.md)
- Haben Sie Ihre Benutzer bei der Installation einer [Remotedesktopclient](clients/remote-desktop-clients.md) damit sie die apps und Ressourcen zugreifen können. 
- Aktivieren Sie hohen Verfügbarkeit durch Hinzufügen von zusätzlichen Verbindungsbroker und -Sitzungshosts:
   - [Horizontales Skalieren einer vorhandenen RDS-Sammlung mit einer RD-Sitzungshostfarm](rds-scale-rdsh-farm.md)
   - [Hinzufügen von hoher Verfügbarkeit zur RD Connection Broker-Infrastruktur](rds-connection-broker-cluster.md)
   - [Hinzufügen von hoher Verfügbarkeit zur RD Web- und RD Gateway-Webfront](rds-rdweb-gateway-ha.md)
   - [Bereitstellen eines auf zwei Knoten und „Direkte Speicherplätze“ basierenden Dateisystems für die UPD-Speicherung](rds-storage-spaces-direct-deployment.md)


Wenn Sie einem Hostingpartner interessiert, die über Remote Desktop-apps und Ressourcen bereitstellen, Kunden oder einen Kunden, die für eine Person zum Hosten Ihrer apps suchen möchten, sehen Sie sich [Remote Desktop Services Hosten von Partnern](rds-hosting-partners.md) Informationen zu einer Bewertung können Sie nutzen, zur Verwendung von RDS in Azure als hostumgebung sowie eine Liste der Partner, die sie übergeben haben.
