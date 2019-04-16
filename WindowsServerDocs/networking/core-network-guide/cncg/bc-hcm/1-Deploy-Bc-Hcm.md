---
title: Bereitstellen von BranchCache-Modus für gehostete Caches
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 326a1f1edfe6cb763a33ebfc8fd5abdd5b6aab3a
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>Bereitstellen von BranchCache-Modus für gehostete Caches

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server2016, Windows Server2012 R2, Windows Server 2012

Windows Server 2016 Core Network Guide enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten, die für eine einwandfreie Verwendung des Netzwerks und eine neue Active Directory erforderlichen&reg; Domäne in einer neuen Gesamtstruktur.

Dieses Handbuch wird erläutert, wie das Hauptnetzwerk erstellen, durch die Bereitstellung von Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches in einem oder mehreren Zweigstellen mit einem Read\-Only Domänencontroller, auf dem Clientcomputer Windows ausführen&reg; 10, Windows 8.1 oder Windows 8 und der Domäne hinzugefügt werden.

>[!IMPORTANT]
>Verwenden Sie dieses Handbuch nicht, wenn Sie planen, bereitstellen oder einen BranchCache-gehosteten Cacheserver, auf der Windows Server 2008 R2 ausgeführt wird bereits bereitgestellt haben. Dieses Handbuch enthält Anweisungen zum Bereitstellen von gehosteten Cachemodus mit einem gehosteten Cacheserver, die unter Windows Server&reg; 2016, Windows Server 2012 R2 oder Windows Server 2012.

Dieses Handbuch enthält die folgenden Abschnitte.

- [Voraussetzungen für die Verwendung dieses Handbuchs](#bkmk_pre)

- [Informationen zum Handbuch](#bkmk_about)

- [Was dieses Handbuch bietet keine](#bkmk_not)

- [Technologieübersichten](#bkmk_tech)

- [BranchCache-gehosteten Cache Bereitstellung – Übersicht](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache-gehosteten Cachemodus Planung der Bereitstellung](3-Bc-Hcm-Plan.md)

- [BranchCache-gehosteten Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md)

- [Zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>Voraussetzungen für die Verwendung dieses Handbuchs

Dies ist ein Begleithandbuch zum Windows Server 2016 Core Network Guide. Zum Bereitstellen von BranchCache im Modus für gehostete Caches in diesem Handbuch müssen Sie die folgenden Schritte ausführen.

- Bereitstellen von mithilfe des Kernnetzwerkhandbuchs ein Kernnetzwerk in Ihrem Hauptbüro oder bereits haben die Technologien bereitgestellt, in das Handbuch zum Hauptnetzwerk installiert und ordnungsgemäß in Ihrem Netzwerk. Zu diesen Technologien zählen TCP/IP v4, DHCP, Active Directory Domain Services \(AD DS\) und DNS.

    > [!NOTE]
    > Die Windows Server 2016 [Kernnetzwerkhandbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) ist in der technischen Bibliothek zu Windows Server 2016 verfügbar.  

- Bereitstellen von BranchCache-Inhaltsserver, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in Ihrem Hauptbüro oder in einem Rechenzentrum des Cloud ausgeführt werden. Informationen dazu, wie Sie BranchCache-Inhaltsserver bereitstellen, finden Sie unter [zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md).

- Herstellen von Verbindungen von wide Area Network \(WAN\) zwischen Ihrer Zweigstelle, Ihrem Hauptbüro und ggf. Ihren Cloudressourcen mit einem virtuellen privaten Netzwerk \(VPN\), DirectAccess oder anderen Verbindungsmethoden.

- Bereitstellen von Clientcomputern in der Zweigstelle, die eine der folgenden Betriebssysteme ausgeführt werden die BranchCache-Unterstützung für intelligente Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS), Hyper Text Transfer-Protokoll (HTTP) und Server Message Block (SMB) zur Verfügung stellen.
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

>[!NOTE]
>In den folgenden Betriebssystemen BranchCache ist HTTP und SMB-Funktionalität nicht unterstützt, aber BITS BranchCache-Funktionalität unterstützt.
>     - Windows 10 Pro, unterstützen BITS nur
>     - Windows 8.1 Pro BITS wird nur unterstützt
>     - Windows 8 Pro unterstützt BITS nur

## <a name="bkmk_about"></a>Informationen zum Handbuch

Dieses Handbuch richtet sich für Netzwerk- und Systemadministratoren, die die Anweisungen in der Windows Server 2016 Core Network Guide oder Windows Server 2012-Core Network Guide zum Bereitstellen eines Hauptnetzwerks befolgt haben, oder für Benutzer, die zuvor die im Hauptnetzwerkhandbuch, einschließlich Active Directory-Domänendienste \(AD DS\), Domain Name System \(DNS\), Dynamic Host Configuration-Protokoll \(DHCP\) enthaltenen Technologien bereitgestellt haben , und TCP/IP v4.

Es wird empfohlen, dass Sie die Entwurfs- und Bereitstellungshandbücher für jede der Technologien überprüfen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher hilft Ihnen festzustellen, ob dieses Bereitstellungsszenario bereitstellt, die Dienste und Konfigurationen, die Sie für das Netzwerk Ihrer Organisation benötigen.

## <a name="bkmk_not"></a>Was dieses Handbuch bietet keine

Dieses Handbuch bietet keine grundlegende Informationen zu BranchCache, einschließlich Informationen zu BranchCache-Modi und Funktionen.  

Dieses Handbuch bietet keine Informationen über das WAN-Verbindungen oder anderen Technologien in Ihrer Zweigstelle, wie z. B. DHCP, einem RODC oder VPN-Server bereitstellen.

Darüber hinaus bietet dieses Handbuch Anweisungen auf der Hardware keine, die Sie verwenden sollten, wenn Sie einen gehosteten Cacheserver bereitstellen. Es ist möglich, führen Sie andere Dienste und Anwendungen auf den gehosteten Cacheserver, jedoch die Entscheidung auf Grundlage der arbeitsauslastung, Hardwarefunktionen und Branch Office Größe treffen, ob Sie BranchCache-gehosteten Cacheserver auf einem bestimmten Computer zu installieren und wie viel Speicherplatz für den Cache ab.  
Dieses Handbuch bietet keine Anweisungen zum Konfigurieren von Computern, auf denen Windows 7 ausgeführt werden. Wenn Sie über Clientcomputer, auf denen Windows 7 in Zweigstellen ausgeführt werden verfügen, müssen Sie sie konfigurieren mithilfe von Prozeduren, die anders als die in diesem Handbuch für Clientcomputer, auf denen Windows 10, Windows 8.1 und Windows 8 ausgeführt werden.
  
Darüber hinaus, wenn Sie Computer mit Windows 7 haben, müssen Sie den gehosteten Cacheserver mit einem Serverzertifikat konfigurieren, die von einer Zertifizierungsstelle ausgestellt wird, die Clientcomputer als vertrauenswürdig eingestuft. \ (Wenn auf allen Clientcomputern Windows 10, Windows 8.1 oder Windows 8 ausgeführt wird, müssen Sie nicht den gehosteten Cacheserver mit einem Serverzertifikat konfigurieren. \) 
> [!IMPORTANT]
> Wenn die gehosteten Cacheserver Windows Server 2008 R2 ausgeführt werden, verwenden Sie die Windows Server 2008 R2 [BranchCache-Bereitstellungshandbuchs](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx) anstelle dieses Handbuch zum Bereitstellen von BranchCache im Modus für gehostete Caches. Wenden Sie die gruppenrichtlinieneinstellungen, die in dieser Anleitung für alle BranchCache-Clients beschrieben werden, die Windows-Versionen von Windows 7 auf Windows 10 ausgeführt werden. Computer, auf denen Windows Server 2008 R2 ausgeführt werden, können mithilfe der Schritte in dieser Anleitung konfiguriert werden.

## <a name="bkmk_tech"></a>Technologieübersichten

Bei diesem Begleithandbuch ist BranchCache die einzige Technologie, die Sie installieren und konfigurieren müssen. Sie müssen, führen Sie Windows PowerShell-BranchCache-Befehle auf dem Inhaltsserver, z. B. Web- und Dateiservern, aber Sie müssen nicht ändern oder neu konfigurieren, die Inhaltsserver auf andere Weise. Darüber hinaus müssen Sie Clientcomputer mithilfe von Gruppenrichtlinien auf den Domänencontrollern, auf denen AD DS unter Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 konfigurieren.

### <a name="branchcache"></a>BranchCache

BranchCache ist eine Technologie wide Area Network (WAN)-Bandbreite Optimierung, die in einigen Editionen der Betriebssysteme Windows Server 2016 und Windows 10 sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 und Windows 7 verfügbar ist.

Um die WAN-Bandbreite zu optimieren, wenn Benutzer Inhalte von Remoteservern zugreifen, BranchCache Client angeforderte Inhalt aus der zentrale heruntergeladen oder gehosteten Cloud-Inhaltsserver, und speichert Sie zwischen in Filialen, sodass andere Clientcomputer in Filialen lokal statt über das WAN auf den gleichen Inhalt zugreifen.

Wenn Sie BranchCache im Modus für gehostete Caches bereitstellen, müssen Sie Clientcomputer in der Filiale als gehostete Cachemodusclients konfigurieren und dann müssen Sie einen gehosteten Cacheserver in der Zweigstelle bereitstellen. Dieses Handbuch wird das Bereitstellen Ihrer gehosteten cacheservers mit vorab gehashten und geladenen Inhalten von Web- und Dateiservern im Server\ basierende veranschaulicht.

### <a name="group-policy"></a>Gruppenrichtlinie

Gruppenrichtlinien in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 handelt es sich um eine Infrastruktur übermittelt, und wenden eine oder mehrere gewünschte Konfigurationen oder Richtlinieneinstellungen auf eine Gruppe von entsprechenden Benutzern und Computern in einer Active Directory-Umgebung verwendet. 

Diese Infrastruktur besteht aus einem Gruppenrichtlinienmodul und mehreren Client-Side Extensions \(CSEs\), die für das Lesen von Richtlinieneinstellungen auf entsprechenden Clientcomputern verantwortlich sind.

Gruppenrichtlinien ist in diesem Szenario zum Konfigurieren von Domänenmitglieds-Clientcomputern mit BranchCache-gehosteten Cachemodus verwendet.

Wenn Sie mit dieser Anleitung fortfahren, finden Sie unter [BranchCache Hosted Cache Mode Übersicht über die Bereitstellung](2-Bc-Hcm-Deploy-Overview.md).
