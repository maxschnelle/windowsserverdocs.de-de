---
title: Migrieren von Rollen und Features
description: ''
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.date: 04/03/2017
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0f78ef4c-dd12-4b1b-8c6e-251dd803c5d1
author: jaimeo
ms.author: jaimeo
manager: dougkim
ms.localizationpriority: medium
ms.openlocfilehash: 7469171005164d9ff823dad7de230d877c874dc9
ms.sourcegitcommit: 07ac08dea2b8f2763c2614a999dc7967018aa0b4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "6121359"
---
# Migrieren von Rollen und Features in Windows Server

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diese Seite enthält Links zu Informationen und Tools für den Prozess zum Migrieren von Rollen und Features zu Windows Server2016, Windows Server2012 R2 und Windows Server2012. Viele Rollen und Features können mit den WindowsServer-Migrationstools migriert werden. Hierbei handelt es sich um eine Gruppe von fünf Windows PowerShell-Cmdlets, die in Windows Server 2008 R2 zum einfachen Migrieren von Rollen- und Featureelementen und -daten eingeführt wurde.

Die Migrationshandbücher unterstützen Migrationen von angegebenen Rollen und Features von einem Server auf einen anderen (keine direkten Upgrades). Sofern in den Anleitungen nicht anders angegeben, werden Migrationen zwischen physischen und virtuellen Computern und zwischen vollständigen Windows Server-Installationen und Servern unterstützt, auf denen die Server Core-Installation ausgeführt wird.  

## Vorbemerkungen

Stellen Sie vor Beginn der Migration von Rollen und Features sicher, dass sowohl auf Quell- als auch auf Zielservern die aktuellsten Service Packs ausgeführt werden, die für das jeweilige Betriebssystem verfügbar sind.
Es ist jetzt auch ein E-Book zu den Windows Server 2012 R2- und Windows Server 2012-Migrationshandbüchern verfügbar. Weitere Informationen und die Downloadinfos zum E-Book finden Sie im [Katalog mit den E-Books für Technologie von Microsoft](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#MigrateRoles). 

>[!NOTE]
>Bei jeder Migration und jedem Upgrade auf eine Version von Windows Server sollten Sie sich mit der [Microsoft Lifecycle-Richtlinie zum Support](https://support.microsoft.com/lifecycle) und dem Zeitrahmen für die jeweilige Version vertraut machen und entsprechend planen. Sie können [nach den Lebenszyklusinformationen](https://support.microsoft.com/lifecycle) für die jeweils gewünschte Windows Server-Version suchen.
 
## Windows Server 2016

### Migrationshandbücher
Derzeit werden aktualisierte Migrationshandbücher für Windows Server2016 entwickelt. Sie finden die aktualisierten Handbücher hier, wenn sie verfügbar sind. In vielen Fällen sind die Schritte in den Windows Server 2012 R2-Migrationshandbüchern auch für Windows Server 2016 noch relevant.

- [Remotedesktopdienste](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/migrate-rds-role-services)
- [Webserver (IIS)](https://www.iis.net/downloads/microsoft/web-deploy)
- [Windows Server Update Services](https://technet.microsoft.com/library/hh852339.aspx)
- [MultiPoint Services](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/multipoint-services/multipoint-services-migrate)
 
## Windows Server 2012 R2

### Migrationshandbücher
Führen Sie die Schritte in diesen Handbüchern aus, um Rollen und Features von Servern, auf denen Windows Server 2003, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 oder Windows Server 2012 R2 ausgeführt wird, zu Windows Server 2012 R2 zu migrieren. Windows Server-Migrationstools in Windows Server2012 R2 unterstützen subnetzübergreifende Migrationen.

- [Installieren, Verwenden und Entfernen von Windows Server-Migrationstools](https://technet.microsoft.com/library/jj134202.aspx)
- [Handbuch für die Migration von Active Directory-Zertifikatdiensten für Windows Server2012R2](https://technet.microsoft.com/library/dn486797.aspx)
- [Migrieren des Rollendiensts der Active Directory-Verbunddienste (AD FS) zu Windows Server2012R2](https://technet.microsoft.com/library/dn486815.aspx)
- [Active Directory Rights Management Services – Migrations- und Upgradehandbuch](https://technet.microsoft.com/library/cc754277.aspx)
- [Migrieren von Datei- und Speicherdiensten zu Windows Server 2012 R2](https://technet.microsoft.com/library/dn479292.aspx)
- [Migration von Hyper-V zu Windows Server2012R2 von Windows Server2012](https://technet.microsoft.com/library/dn486799.aspx)
- [Migrieren des Netzwerkrichtlinienservers zu Windows Server 2012](https://technet.microsoft.com/library/hh831652)
- [Migrieren der Remotedesktopdienste zu Windows Server 2012 R2](https://technet.microsoft.com/library/dn479239.aspx)
- [Migrieren von Windows Server Update Services zu Windows Server 2012 R2](https://technet.microsoft.com/library/hh852339.aspx)
- [Migrieren von Clusterrollen zu Windows Server2012R2](https://technet.microsoft.com/library/dn530779.aspx)
- [Migrieren eines DHCP-Servers zu Windows Server 2012 R2](https://technet.microsoft.com/library/dn495425.aspx)
 
## Windows Server 2012

### Migrationshandbücher
Führen Sie die Schritte in diesen Handbüchern aus, um Rollen und Features von Servern, auf denen Windows Server 2003, Windows Server 2008, Windows Server 2008 R2 oder Windows Server 2012 ausgeführt wird, zu Windows Server 2012 zu migrieren. Windows Server-Migrationstools in Windows Server2012 unterstützen subnetzübergreifende Migrationen.

- [Installieren, Verwenden und Entfernen von Windows Server-Migrationstools](https://technet.microsoft.com/library/jj134202)
- [Migrieren von Rollendiensten der Active Directory-Verbunddienste (AD FS) zu WindowsServer2012](https://technet.microsoft.com/library/jj647765)
- [Migrieren der Integritätsregistrierungsstelle zu Windows Server2012](https://technet.microsoft.com/library/hh831513)
- [Migrieren von Hyper-V zu Windows Server2012 von Windows Server2008 R2](https://technet.microsoft.com/library/jj574113)
- [Migrieren der IP-Konfiguration zu WindowsServer2012](https://technet.microsoft.com/library/jj574133)
- [Migrieren des Netzwerkrichtlinienservers zu Windows Server 2012](https://technet.microsoft.com/library/hh831652)
- [Migrieren von Druck- und Dokumentdiensten zu Windows Server2012](https://technet.microsoft.com/library/jj134150)
- [Migrieren des Remotezugriffs zu Windows Server2012](https://technet.microsoft.com/library/hh831423)
- [Migrieren von Windows Server Update Services zu Windows Server 2012](https://technet.microsoft.com/library/hh852339)
- [Aktualisieren von Active Directory-Domänencontrollern zu Windows Server 2012](https://technet.microsoft.com/library/hh994618.aspx)
- [Migrieren von Clusterdiensten und -anwendungen zu Windows Server 2012](https://technet.microsoft.com/library/dn486790.aspx)
 

Weitere Ressourcen zur Migration finden Sie unter [Migrieren von Rollen und Features zu Windows Server 2012](https://technet.microsoft.com/library/jj134039).

## Windows Server 2008 R2

### Migrationshandbücher
Führen Sie die Schritte in diesen Handbüchern aus, um Rollen und Features von Servern, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird, zu Windows Server 2008 R2 zu migrieren. Windows Server-Migrationstools in Windows Server2008 R2 unterstützen keine subnetzübergreifenden Migrationen.

- [Installieren und Deinstallieren der WindowsServer-Migrationstools und Zugriff auf die Tools](https://technet.microsoft.com/library/dd379545)
- [Active Directory Certificate Services-Migrationshandbuch](https://technet.microsoft.com/library/ee126170)
- [Handbuch für die Migration von Servern mit Active Directory Domain Services (AD DS) und DNS (Domain Name System)](https://technet.microsoft.com/library/dd379558)
- [BranchCache-Migrationshandbuch](https://technet.microsoft.com/library/dd548365)
- [Handbuch für die Migration von DHCP-Servern (Dynamic Host Configuration Protocol)](https://technet.microsoft.com/library/dd379535)
- [Handbuch für die Migration von Dateidiensten](https://technet.microsoft.com/library/dd379487)
- [HRA-Migrationshandbuch](https://technet.microsoft.com/library/ee791829)
- [Hyper-V-Migrationshandbuch](https://technet.microsoft.com/library/ee849855)
- [Handbuch für die Migration der IP-Konfiguration](https://technet.microsoft.com/library/dd379537)
- [Handbuch für die Migration lokaler Benutzer und Gruppen](https://technet.microsoft.com/library/dd379531)
- [NPS-Migrationshandbuch](https://technet.microsoft.com/library/ee791849)
- [Handbuch für die Migration von Druckdiensten](https://technet.microsoft.com/library/dd379488)
- [Handbuch zur Migration von Remotedesktopdiensten](https://technet.microsoft.com/library/ff849223)
- [RRAS-Migrationshandbuch](https://technet.microsoft.com/library/ee822825)
- [Informationen und allgemeine Aufgaben für die WindowsServer-Migration](https://technet.microsoft.com/library/ff400258)
- [Migrationshandbuch für Windows Server Update Services3.0SP2](https://technet.microsoft.com/library/ee822826)
 
Weitere Ressourcen zur Migration finden Sie unter [Migrate Roles and Features to Windows Server 2008 R2](https://technet.microsoft.com/library/dd365353) (Migrieren von Rollen und Features zu Windows Server 2008 R2).
