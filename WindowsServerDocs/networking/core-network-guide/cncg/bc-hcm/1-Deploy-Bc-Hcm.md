---
title: Bereitstellen des BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus für gehostete Caches auf Computern unter Windows Server 2016 und Windows 10
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 54991b343623b934118bb62af1bd91871a726996
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446482"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>Bereitstellen des BranchCache-Modus „Gehosteter Cache“

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Windows Server 2016 Core Network Guide enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten erforderlich, die für eine voll funktionsfähige Netzwerks und einer neuen Active Directory sind&reg; Domäne in einer neuen Gesamtstruktur.

Dieses Handbuch wird erläutert, wie das Hauptnetzwerk zu erstellen, indem Sie die Anleitungen zum Bereitstellen von BranchCache im Modus für gehostete Caches in eine oder mehrere Zweigstellen mit einer Lese-\-Only Domain Controller, auf dem Clientcomputer Windows ausgeführt werden&reg; 10, Windows 8.1 oder Windows 8 und in die Domäne eingebunden sind.

>[!IMPORTANT]
>Verwenden Sie dieses Handbuch nicht, wenn Sie planen, bereitstellen oder einen gehosteten BranchCache-Cacheserver, auf der Windows Server 2008 R2 ausgeführt wird bereits bereitgestellt haben. Dieses Handbuch enthält Anweisungen für die Bereitstellung mit einem gehosteten Cacheserver, auf denen Windows Server ausgeführt wird, der Modus für gehostete Caches&reg; 2016, Windows Server 2012 R2 und Windows Server 2012.

Dieses Handbuch enthält die folgenden Abschnitte:

- [Voraussetzungen für die Verwendung dieses Handbuchs](#bkmk_pre)

- [Informationen zur Anleitung](#bkmk_about)

- [Nicht in diesem Handbuch enthaltene Informationen](#bkmk_not)

- [Technologieübersicht](#bkmk_tech)

- [BranchCache Hosted Cache Mode-Bereitstellungsübersicht](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache Modus für gehostete Caches Planung der Bereitstellung](3-Bc-Hcm-Plan.md)

- [BranchCache-gehosteten Cache-Modus-Bereitstellung](4-Bc-Hcm-Deployment.md)

- [Weitere Ressourcen](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>Voraussetzungen für die Verwendung dieses Handbuchs

Dies ist ein Begleithandbuch zum Windows Server 2016 Core Network Guide. Zum Bereitstellen von BranchCache im Modus "Gehosteter Cache" mit diesem Handbuch müssen Sie die folgenden Schritte ausführen.

- Stellen Sie mithilfe des Kernnetzwerkhandbuchs ein Kernnetzwerk in Ihrem Hauptbüro bereit, sofern nicht bereits die im Kernnetzwerkhandbuch beschriebenen Technologien in Ihrem Netzwerk installiert sind und ordnungsgemäß funktionieren. Zu diesen Technologien zählen TCP\/IP-v4, DHCP, Active Directory Domain Services \(AD DS\), und DNS.

    > [!NOTE]
    > Windows Server 2016 [Core Network Guide](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) ist in der technischen Bibliothek zu Windows Server 2016 verfügbar.  

- Bereitstellen von BranchCache-Inhaltsserver, die Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 in Ihrem Hauptbüro oder in einem Cloud-Rechenzentrum ausgeführt werden. Informationen dazu, wie Sie BranchCache-Inhaltsserver bereitstellen, finden Sie unter [Zusatzressourcen](11-Bc-Hcm-additional-resources.md).

- WAN herzustellen \(WAN\) Verbindungen zwischen Ihrer Zweigstelle, Ihrem Hauptbüro und, falls zutreffend, Ihre Cloud-Ressourcen, mit einem virtuellen privaten Netzwerk \(VPN\), DirectAccess oder andere die Verbindungsmethode.

- Bereitstellen Sie Clientcomputer, die eine der folgenden Betriebssysteme ausgeführt werden, die BranchCache-Unterstützung für Intelligent Service (BITS) Hyper Text Transfer-Protokoll (HTTP) und Server Message Block (SMB) bereitstellen, in der Zweigstelle .
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

> [!NOTE]
> In den folgenden Betriebssystemen BranchCache ist HTTP und SMB-Funktionalität nicht unterstützt, aber BITS des BranchCache-Funktionalität unterstützt.
>     - Windows 10 Pro, unterstützen BITS nur
>     - Windows 8.1 Pro unterstützen BITS nur
>     - Windows 8 Pro, unterstützen BITS nur

## <a name="bkmk_about"></a>Über diesen Leitfaden

Dieses Handbuch richtet sich für die Netzwerk- und Systemadministratoren, die die Anweisungen in der Windows Server 2016 Core Network Guide oder Windows Server 2012 Core Network Guide zum Bereitstellen eines Hauptnetzwerks befolgt haben, oder für Benutzer, die zuvor bereitgestellt haben die Technologien in das Handbuch zum Hauptnetzwerk, einschließlich Active Directory Domain Services \(AD DS\), Domain Name Service \(DNS\), Dynamic Host Configuration Protocol \(DHCP\), und TCP-\/IP-v4.

Sie sollten die Entwurfs- und Bereitstellungshandbücher für jede der Technologien einsehen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher können Ihnen helfen, zu bestimmen, ob dieses Bereitstellungsszenario die Dienste und Konfigurationen bietet, die Sie zur Organisation des Netzwerks benötigen.

## <a name="bkmk_not"></a>Was dieses Handbuch bietet keine

Dieses Handbuch bietet keine grundlegende Informationen zu BranchCache, Informationen zu Modi und Funktionen von BranchCache inbegriffen.  

Dieses Handbuch bietet keine Informationen über die Bereitstellung von WAN-Verbindungen oder anderen Technologien in der Zweigstelle, wie z. B. von DHCP, einem RODC oder VPN-Server.

Darüber hinaus erfahren Sie in diesem Handbuch nicht, welche Hardware Sie zum Bereitstellen von gehosteten Cacheservers verwenden sollten. Sie können zwar andere Dienste und Anwendungen auf dem gehosteten Cacheserver ausführen, jedoch müssen Sie auf der Basis von Arbeitsauslastung, Hardwarefunktionen und Zweigstellengröße bestimmen, ob der gehostete Cacheserver für BranchCache auf einem bestimmten Computer installiert werden soll, und wie viel Speicherplatz für den Cache zugewiesen werden soll.  
Dieses Handbuch bietet keine Anweisungen zum Konfigurieren von Computern, auf denen Windows 7 ausgeführt werden. Wenn Sie über Clientcomputer, auf denen Windows 7 in Zweigstellen ausgeführt werden verfügen, müssen Sie sie konfigurieren mithilfe von Prozeduren, die anders als die in diesem Handbuch für Clientcomputer, auf denen Windows 10, Windows 8.1 und Windows 8 ausgeführt werden.
  
Darüber hinaus, wenn Sie auf Computern unter Windows 7 haben, müssen Sie den gehosteten Cacheserver mit einem Serverzertifikat konfigurieren, die von einer Zertifizierungsstelle ausgestellt wird, der den Clientcomputern zu vertrauen. \(Wenn alle von den Clientcomputern Windows 10, Windows 8.1 oder Windows 8 ausgeführt werden, müssen Sie nicht den gehosteten Cacheserver mit einem Serverzertifikat konfigurieren.\) 
> [!IMPORTANT]
> Wenn die gehosteten Cacheserver mit Windows Server 2008 R2 ausgeführt werden, verwenden Sie die Windows Server 2008 R2 [BranchCache-Bereitstellungshandbuch](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx) anstelle dieses Handbuch zum Bereitstellen von BranchCache im Modus "gehosteter Cache". Wenden Sie die gruppenrichtlinieneinstellungen, die in dieser Anleitung für alle BranchCache-Clients beschrieben werden, die Windows-Versionen von Windows 7 auf Windows 10 ausgeführt werden. Computer, auf denen Windows Server 2008 R2 ausgeführt werden können nicht konfiguriert werden, mithilfe der Schritte in diesem Handbuch.

## <a name="bkmk_tech"></a>Technologieübersicht

Bei diesem Begleithandbuch ist BranchCache die einzige Technologie, die Sie installieren und konfigurieren müssen. Sie müssen Windows PowerShell-BranchCache-Befehle auf Ihren Inhaltsservern, z. B. Web- und Dateiservern, ausführen, jedoch müssen Sie die Inhaltsserver auf keine andere Weise ändern oder neu konfigurieren. Darüber hinaus müssen Sie den Clientcomputern konfigurieren, mithilfe der Gruppenrichtlinie auf den Domänencontrollern, die AD DS in Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt werden.

### <a name="branchcache"></a>BranchCache

BranchCache ist eine Technologie wide Area Network (WAN)-Bandbreite Optimierung, die in einigen Editionen der Windows Server 2016 und Windows 10-Betriebssysteme sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8 ist , Windows Server 2008 R2 und Windows 7.

Um die WAN-Bandbreite optimieren, wenn Benutzer auf Inhalte auf Remoteservern zugreifen, BranchCache downloads von Clients angeforderte Inhalt aus Ihrem Hauptbüro oder gehosteten inhaltsservern, und speichert Sie zwischen an filialstandorten, sodass andere Clientcomputer an Filialen lokal anstatt über das WAN auf den gleichen Inhalt zugreifen.

Wenn Sie BranchCache im Modus "Gehosteter Cache" bereitstellen, müssen Sie die Clientcomputer in der Zweigstelle als Clients im Modus "Gehosteter Cache" konfigurieren, und dann müssen Sie einen gehosteten Cacheserver in der Zweigstelle bereitstellen. Diese Anleitung veranschaulicht, wie Sie Ihre gehosteten cacheservers mit vorab gehashten und geladenen Inhalten von Ihren Web- und -Server bereitstellen\-basierte Inhaltsserver dieses Typs.

### <a name="group-policy"></a>Gruppenrichtlinie

Der Gruppenrichtlinie in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 handelt es sich um eine Infrastruktur zum Bereitstellen und wenden eine oder mehrere gewünschte Konfigurationen oder Richtlinieneinstellungen auf eine Gruppe von Benutzern oder Computern in einer Active Directory-Umgebung. 

Diese Infrastruktur besteht aus einem Gruppenrichtlinienmodul und mehreren Client\-clientseitige Erweiterungen \(CSEs\) verantwortlich für das Lesen von Richtlinieneinstellungen auf entsprechenden Clientcomputern.

In diesem Szenario dient die Gruppenrichtlinie zum Konfigurieren von Domänenmitglieds-Clientcomputern mit BranchCache im Modus "Gehosteter Cache".

Mit diesem Handbuch finden Sie [BranchCache Hosted Cache Mode Übersicht über die Bereitstellung](2-Bc-Hcm-Deploy-Overview.md).
