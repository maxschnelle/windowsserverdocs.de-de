---
title: Migrieren von Rollen und Features
description: Informationen zum Migrieren von Rollen und Features zu einer neueren Version von Windows Server.
ms.prod: windows-server
ms.date: 08/28/2019
ms.technology: server-general
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jasongerend
ms.author: jgerend
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 99a684cc90d47e1e80dc84ef9c3705a2ed79728b
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182026"
---
# <a name="migrating-roles-and-features-in-windows-server"></a>Migrieren von Rollen und Features in Windows Server

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diese Seite enthält Links zu Informationen und Tools, die dich durch den Migrationsvorgang für Rollen und Features zu einer neuen Version von Windows Server führen können. Du kannst Dateiserver und Speicher mit dem [Speichermigrationsdienst](../storage/storage-migration-service/overview.md) migrieren, während viele andere Rollen und Features mithilfe der Windows Server-Migrationstools migriert werden können, einer Reihe von PowerShell-Cmdlets, die in Windows Server 2008 R2 zum Migrieren von Rollen und Features eingeführt wurden.

Die Migrationshandbücher unterstützen Migrationen von angegebenen Rollen und Features zwischen Servern (keine direkten Upgrades). Sofern in den Anleitungen nicht anders angegeben, werden Migrationen zwischen physischen und virtuellen Computern sowie zwischen vollständigen Windows Server-Installationen und Servern mit Server Core-Installation unterstützt.

## <a name="before-you-begin"></a>Vorbereitung

Vergewissere dich vor Beginn der Migration von Rollen und Features, dass Quell- und Zielserver über die neuesten Service Packs verfügen, die für das jeweilige Betriebssystem verfügbar sind.

> [!NOTE]
> Bei jeder Migration und jedem Upgrade auf eine Version von Windows Server solltest du dich mit der [Microsoft Lifecycle-Richtlinie für den Support](https://support.microsoft.com/lifecycle) und dem Zeitrahmen für die jeweilige Version vertraut machen und entsprechend planen. Du kannst [nach den Lebenszyklusinformationen für die jeweils gewünschte Windows Server-Version suchen](https://support.microsoft.com/lifecycle).

## <a name="windows-server-2019"></a>Windows Server 2019

Wir empfehlen die Verwendung des [Speichermigrationsdiensts](../storage/storage-migration-service/overview.md) zum Migrieren von Dateiservern und Speicher zu Windows Server 2019 oder Windows Server 2016. Informationen zum Migrieren anderer Rollen findest du in der Anleitung für Windows Server 2016 und Windows Server 2012 R2.

## <a name="windows-server-2016"></a>Windows Server 2016

Hier findest du die Migrationshandbücher zu Windows Server 2016. Beachte, dass du in vielen Fällen auch die Migrationshandbücher für Windows Server 2012 R2 verwenden kannst.

- [Remotedesktopdienste](../remote/remote-desktop-services/migrate-rds-role-services.md)
- [Webserver (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11))
- [MultiPoint Services](../remote/multipoint-services/multipoint-services-migrate.md)

Wir empfehlen die Verwendung des [Speichermigrationsdiensts](../storage/storage-migration-service/overview.md) zum Migrieren von Dateiservern zu Windows Server 2019 oder Windows Server 2016.

## <a name="windows-server-2012-r2"></a>Windows Server 2012 R2

Führe die Schritte in diesen Handbüchern aus, um Rollen und Features von Servern unter Windows Server 2003, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 oder Windows Server 2012 R2 zu Windows Server 2012 R2 zu migrieren. Windows Server-Migrationstools in Windows Server 2012 R2 unterstützen subnetzübergreifende Migrationen.

- [Install, Use, and Remove Windows Server Migration Tools](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134202(v=ws.11)) (Installieren, Verwenden und Entfernen von Windows Server-Migrationstools)
- [Active Directory Certificate Services Migration Guide for Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486797(v=ws.11)) (Handbuch für die Migration von Active Directory-Zertifikatdiensten für Windows Server 2012 R2)
- [Migrating Active Directory Federation Services Role Service to Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486815(v=ws.11)) (Migrieren des Rollendiensts der Active Directory-Verbunddienste (AD FS) zu Windows Server 2012 R2)
- [Active Directory Rights Management Services Migration and Upgrade Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc754277(v=ws.10)) (Active Directory Rights Management Services – Migrations- und Upgradehandbuch)
- [Migrate File and Storage Services to Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn479292(v=ws.11)) (Migrieren von Datei- und Speicherdiensten zu Windows Server 2012 R2)
- [Migration von Hyper-V zu Windows Server 2012 R2 von Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486799(v=ws.11))
- [Migrate Network Policy Server to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831652(v=ws.11)) (Migrieren des Netzwerkrichtlinienservers zu Windows Server 2012)
- [Migrate Remote Desktop Services to Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn479239(v=ws.11)) (Migrieren der Remotedesktopdienste zu Windows Server 2012 R2)
- [Migrate Windows Server Update Services to Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11)) (Migrieren von Windows Server Update Services zu Windows Server 2012 R2)
- [Migrate Cluster Roles to Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn530779(v=ws.11)) (Migrieren von Clusterrollen zu Windows Server 2012 R2)
- [Migrate DHCP Server to Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn495425(v=ws.11)) (Migrieren eines DHCP-Servers zu Windows Server 2012 R2)

Es ist jetzt auch ein E-Book mit den Windows Server 2012 R2- und Windows Server 2012-Migrationshandbüchern verfügbar. Weitere Informationen findest du im [Katalog mit den E-Books für Technologie von Microsoft](https://download.microsoft.com/download/8/D/3/8D33661A-7E21-4FEE-9AAA-C17C3004B5AA/Windows-Migration-and-Upgrade-Guide.pdf). Hier kannst du auch das E-Book herunterladen.

## <a name="windows-server-2012"></a>Windows Server 2012

Führe die Schritte in diesen Handbüchern aus, um Rollen und Features von Servern unter Windows Server 2003, Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 zu Windows Server 2012 zu migrieren. Die Windows Server-Migrationstools in Windows Server 2012 unterstützen subnetzübergreifende Migrationen.

- [Install, Use, and Remove Windows Server Migration Tools](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134202(v=ws.11)) (Installieren, Verwenden und Entfernen von Windows Server-Migrationstools)
- [Migrieren von Rollendiensten der Active Directory-Verbunddienste (AD FS) zu Windows Server 2012](../identity/ad-fs/deployment/migrate-ad-fs-role-services-to-windows-server-2012.md)
- [Migrate Health Registration Authority to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831513(v=ws.11)) (Migrieren der Integritätsregistrierungsstelle zu Windows Server 2012)
- [Migrate Hyper-V to Windows Server 2012 from Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574113(v=ws.11)) (Migrieren von Hyper-V zu Windows Server 2012 von Windows Server 2008 R2)
- [Migrate IP Configuration to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj574133(v=ws.11)) (Migrieren der IP-Konfiguration zu Windows Server 2012)
- [Migrate Network Policy Server to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831652(v=ws.11)) (Migrieren des Netzwerkrichtlinienservers zu Windows Server 2012)
- [Migrate Print and Document Services to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134150(v=ws.11)) (Migrieren von Druck- und Dokumentdiensten zu Windows Server 2012)
- [Migrate Remote Access to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831423(v=ws.11)) (Migrieren des Remotezugriffs zu Windows Server 2012)
- [Migrate Windows Server Update Services to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh852339(v=ws.11)) (Migrieren von Windows Server Update Services zu Windows Server 2012)
- [Upgrade Active Directory Domain Controllers to Windows Server 2012](../identity/ad-ds/deploy/upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012.md) (Upgraden von Active Directory-Domänencontrollern auf Windows Server 2012)
- [Migrating Clustered Services and Applications to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn486790(v=ws.11)) (Migrieren von Clusterdiensten und -anwendungen zu Windows Server 2012)


Weitere Ressourcen zur Migration findest du unter [Migrate Roles and Features to Windows Server 2012](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj134039(v=ws.11)) (Migrieren von Rollen und Features zu Windows Server 2012).

## <a name="windows-server-2008-r2"></a>Windows Server 2008 R2

Führe die Schritte in diesen Handbüchern aus, um Rollen und Features von Servern unter Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 zu Windows Server 2008 R2 zu migrieren. Die Windows Server-Migrationstools in Windows Server 2008 R2 unterstützen keine subnetzübergreifenden Migrationen.

- [Windows Server Migration Tools Installation, Access, and Removal](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379545(v=ws.10)) (Windows Server-Migrationstools: Installation, Zugriff und Entfernung)
- [Active Directory Certificate Services Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee126170(v=ws.10)) (Migrationshandbuch für die Active Directory-Zertifikatdienste)
- [Active Directory Domain Services and Domain Name System (DNS) Server Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379558(v=ws.10)) (Handbuch für die Migration von Servern mit Active Directory Domain Services und Domain Name System (DNS))
- [BranchCache Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd548365(v=ws.10)) (BranchCache-Migrationsanleitung)
- [Dynamic Host Configuration Protocol (DHCP) Server Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379535(v=ws.10)) (Handbuch für die Migration von DHCP-Servern (Dynamic Host Configuration Protocol))
- [File Services Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379487(v=ws.10)) (Handbuch für die Migration von Dateidiensten)
- [HRA Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee791829(v=ws.10)) (HRA-Migrationshandbuch)
- [Hyper-V Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee849855(v=ws.10)) (Hyper-V-Migrationshandbuch)
- [IP Configuration Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379537(v=ws.10)) (Handbuch für die Migration der IP-Konfiguration)
- [Local User and Group Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379531(v=ws.10)) (Handbuch für die Migration lokaler Benutzer und Gruppen)
- [NPS Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee791849(v=ws.10)) (NPS-Migrationshandbuch)
- [Print Services Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379488(v=ws.10)) (Handbuch für die Migration von Druckdiensten)
- [Remote Desktop Services Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff849223(v=ws.10)) (Handbuch zur Migration von Remotedesktopdiensten)
- [RRAS Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee822825(v=ws.10)) (RRAS-Migrationshandbuch)
- [Windows Server Migration Common Tasks and Information](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ff400258(v=ws.10)) (Windows Server-Migration: allgemeine Aufgaben und Informationen)
- [Windows Server Update Services 3.0 SP2 Migration Guide](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee822826(v=ws.10)) (Migrationshandbuch für Windows Server Update Services 3.0 SP2)

Weitere Ressourcen zur Migration findest du unter [Migrate Server Roles to Windows Server 2008 R2](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd365353(v=ws.10)) (Migrieren von Serverrollen zu Windows Server 2008 R2).
