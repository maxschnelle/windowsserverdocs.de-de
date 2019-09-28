---
title: Bereitstellen des BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 49e74132dba2909b7e5b639c95ef50064cf23e8c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356379"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>Bereitstellen des BranchCache-Modus „Gehosteter Cache“

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Das Handbuch zum Windows Server 2016-Kern Netzwerk enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory @ no__t-0-Domäne in einer neuen Gesamtstruktur erforderlich sind.

In diesem Handbuch wird erläutert, wie Sie das Hauptnetzwerk erstellen, indem Sie Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" in einer oder mehreren Zweigstellen mit einem Domänen Controller mit Leseberechtigung @ no__t-0bereit stellen, auf dem auf Client Computern Windows @ no__t-1 10 ausgeführt Windows 8.1 wird , oder Windows 8 und sind mit der Domäne verknüpft.

>[!IMPORTANT]
>Verwenden Sie diese Anleitung nicht, wenn Sie einen BranchCache-gehosteten Cache Server, auf dem Windows Server 2008 R2 ausgeführt wird, bereitstellen oder bereits bereitgestellt haben. Dieses Handbuch enthält Anweisungen zum Bereitstellen des Modus "gehosteter Cache" mit einem gehosteten Cache Server, auf dem Windows Server @ no__t-0 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.

Dieses Handbuch enthält die folgenden Abschnitte:

- [Voraussetzungen für die Verwendung dieses Handbuchs](#bkmk_pre)

- [Informationen zur Anleitung](#bkmk_about)

- [Nicht in diesem Handbuch enthaltene Informationen](#bkmk_not)

- [Technologie Übersichten](#bkmk_tech)

- [BranchCache-Bereitstellung im gehosteten Cache Modus](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache-Bereitstellungs Planung im gehosteten Cache Modus](3-Bc-Hcm-Plan.md)

- [BranchCache-Bereitstellung im gehosteten Cache Modus](4-Bc-Hcm-Deployment.md)

- [Weitere Ressourcen](11-Bc-Hcm-additional-resources.md)

## <a name="bkmk_pre"></a>Voraussetzungen für die Verwendung dieses Handbuchs

Dies ist ein Begleit Handbuch zum Windows Server 2016-Kern Netzwerk Handbuch. Zum Bereitstellen von BranchCache im Modus "Gehosteter Cache" mit diesem Handbuch müssen Sie die folgenden Schritte ausführen.

- Stellen Sie mithilfe des Kernnetzwerkhandbuchs ein Kernnetzwerk in Ihrem Hauptbüro bereit, sofern nicht bereits die im Kernnetzwerkhandbuch beschriebenen Technologien in Ihrem Netzwerk installiert sind und ordnungsgemäß funktionieren. Zu diesen Technologien gehören TCP @ no__t-0ip V4, DHCP, Active Directory Domain Services \(AD DS @ no__t-2 und DNS.

    > [!NOTE]
    > Das Windows Server 2016- [Kern Netzwerk Handbuch](https://technet.microsoft.com/windows-server-docs/networking/core-network-guide/core-network-guide) ist in der technischen Bibliothek für Windows Server 2016 verfügbar.  

- Stellen Sie BranchCache-Inhalts Server, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, in ihrer Zentrale oder in einem cloudrechenzentrum bereit. Informationen zum Bereitstellen von BranchCache-Inhalts Servern finden Sie unter [zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md).

- Richten Sie \(wan @ no__t-1-Verbindungen zwischen Ihrer Zweigstelle, ihrer Zentrale und ggf. ihren cloudressourcen mithilfe eines virtuellen privaten Netzwerks \(vpn @ no__t-3, DirectAccess oder einer anderen Verbindungsmethode ein.

- Stellen Sie Client Computer in der Zweigstelle bereit, auf denen eines der folgenden Betriebssysteme ausgeführt wird, die BranchCache mit Unterstützung für Bits (Bits), hypertexttransfer-Protokoll (http) und Server Message Block (SMB) bereitstellen. .
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

> [!NOTE]
> In den folgenden Betriebssystemen unterstützt BranchCache keine HTTP-und SMB-Funktionalität, unterstützt jedoch die BranchCache-Bits-Funktionalität.
>     - Windows 10 pro, nur Bits-Unterstützung
>     - Windows 8.1 pro, nur Bits-Unterstützung
>     - Windows 8 pro, nur Bits-Unterstützung

## <a name="bkmk_about"></a>Informationen zu diesem Leitfaden

Dieses Handbuch richtet sich an Netzwerk-und Systemadministratoren, die die Anweisungen im Windows Server 2016-Kern Netzwerk Handbuch oder im Windows Server 2012-Kern Netzwerk Handbuch zum Bereitstellen eines Kern Netzwerks befolgt haben, oder für diejenigen, die zuvor das im Handbuch zum Hauptnetzwerk enthaltene Technologien, einschließlich Active Directory Domain Services \(ad DS @ no__t-1, Domain Name Service \(dns @ no__t-3, Dynamic Host Configuration-Protokoll \(dhcp @ no__t-5 und TCP @ no__t-6ip v4.

Sie sollten die Entwurfs- und Bereitstellungshandbücher für jede der Technologien einsehen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher können Ihnen helfen, zu bestimmen, ob dieses Bereitstellungsszenario die Dienste und Konfigurationen bietet, die Sie zur Organisation des Netzwerks benötigen.

## <a name="bkmk_not"></a>Was diese Anleitung nicht bietet

Dieses Handbuch bietet keine grundlegende Informationen zu BranchCache, Informationen zu Modi und Funktionen von BranchCache inbegriffen.  

Dieses Handbuch bietet keine Informationen über die Bereitstellung von WAN-Verbindungen oder anderen Technologien in der Zweigstelle, wie z. B. von DHCP, einem RODC oder VPN-Server.

Darüber hinaus erfahren Sie in diesem Handbuch nicht, welche Hardware Sie zum Bereitstellen von gehosteten Cacheservers verwenden sollten. Sie können zwar andere Dienste und Anwendungen auf dem gehosteten Cacheserver ausführen, jedoch müssen Sie auf der Basis von Arbeitsauslastung, Hardwarefunktionen und Zweigstellengröße bestimmen, ob der gehostete Cacheserver für BranchCache auf einem bestimmten Computer installiert werden soll, und wie viel Speicherplatz für den Cache zugewiesen werden soll.  
Dieses Handbuch enthält keine Anweisungen zum Konfigurieren von Computern, auf denen Windows 7 ausgeführt wird. Wenn Sie über Client Computer verfügen, auf denen Windows 7 in ihren Zweigstellen ausgeführt wird, müssen Sie diese mithilfe von Verfahren konfigurieren, die sich von den in diesem Handbuch für Client Computer unter Windows 10, Windows 8.1 und Windows 8 bereitgestellten Verfahren unterscheiden.
  
Wenn Sie über Computer verfügen, auf denen Windows 7 ausgeführt wird, müssen Sie außerdem den gehosteten Cache Server mit einem Serverzertifikat konfigurieren, das von einer Zertifizierungsstelle ausgestellt wird, der Client Computer vertrauen. \(wenn auf allen Client Computern Windows 10, Windows 8.1 oder Windows 8 ausgeführt wird, müssen Sie den gehosteten Cache Server nicht mit einem Serverzertifikat konfigurieren. \) 
> [!IMPORTANT]
> Wenn auf ihren gehosteten Cache Servern Windows Server 2008 R2 ausgeführt wird, verwenden Sie das Windows Server 2008 R2 [BranchCache-Bereitstellungs Handbuch](https://technet.microsoft.com/library/ee649232(v=ws.10).aspx) anstelle dieser Anleitung, um BranchCache im Modus "gehosteter Cache" bereitzustellen. Wenden Sie die in diesem Handbuch beschriebenen Gruppenrichtlinie Einstellungen auf alle BranchCache-Clients an, auf denen Versionen von Windows von Windows 7 auf Windows 10 ausgeführt werden. Computer, auf denen Windows Server 2008 R2 ausgeführt wird, können mithilfe der in diesem Handbuch beschriebenen Schritte nicht konfiguriert werden.

## <a name="bkmk_tech"></a>Technologie Übersichten

Bei diesem Begleithandbuch ist BranchCache die einzige Technologie, die Sie installieren und konfigurieren müssen. Sie müssen Windows PowerShell-BranchCache-Befehle auf Ihren Inhaltsservern, z. B. Web- und Dateiservern, ausführen, jedoch müssen Sie die Inhaltsserver auf keine andere Weise ändern oder neu konfigurieren. Außerdem müssen Sie Client Computer mithilfe von Gruppenrichtlinie auf Ihren Domänen Controllern konfigurieren, auf denen AD DS auf Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.

### <a name="branchcache"></a>BranchCache

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen der Windows Server 2016-und Windows 10-Betriebssysteme enthalten ist, sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8 , Windows Server 2008 R2 und Windows 7.

Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte auf Remote Servern zugreifen, werden von BranchCache vom Client angeforderte Inhalte von Ihrem Hauptbüro oder von gehosteten cloudanwendungsserver heruntergeladen und in Zweigstellen zwischengespeichert, sodass andere Client Computer unter Zweigstellen, um lokal und nicht über das WAN auf denselben Inhalt zuzugreifen.

Wenn Sie BranchCache im Modus "Gehosteter Cache" bereitstellen, müssen Sie die Clientcomputer in der Zweigstelle als Clients im Modus "Gehosteter Cache" konfigurieren, und dann müssen Sie einen gehosteten Cacheserver in der Zweigstelle bereitstellen. In dieser Anleitung wird veranschaulicht, wie Sie Ihren gehosteten Cache Server mit vorab Hash-und vorab geladenen Inhalten von Ihrem Web-und Dateiserver @ no__t-0based Content Servers bereitstellen.

### <a name="group-policy"></a>Gruppenrichtlinie

Gruppenrichtlinie in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ist eine Infrastruktur, mit der eine oder mehrere gewünschte Konfigurationen oder Richtlinien Einstellungen für eine Gruppe von Ziel Benutzern und Computern in einer Active Directory Umgebung bereitgestellt und angewendet werden. 

Diese Infrastruktur besteht aus einer Gruppenrichtlinie-Engine und mehreren Client-no__t-0-@no__t Erweiterungen, die für das Lesen von Richtlinien Einstellungen auf den Ziel Client Computern zuständig sind.

In diesem Szenario dient die Gruppenrichtlinie zum Konfigurieren von Domänenmitglieds-Clientcomputern mit BranchCache im Modus "Gehosteter Cache".

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Übersicht über BranchCache-bereit Stellungen im gehosteten Cache Modus](2-Bc-Hcm-Deploy-Overview.md).
