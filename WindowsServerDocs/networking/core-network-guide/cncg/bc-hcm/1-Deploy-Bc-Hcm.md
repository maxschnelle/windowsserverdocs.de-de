---
title: Bereitstellen des BranchCache-Modus „Gehosteter Cache“
description: Dieses Handbuch enthält Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" auf Computern unter Windows Server 2016 und Windows 10.
manager: brianlic
ms.topic: article
ms.assetid: 4235231c-4732-4ea9-9330-2a8c8a616d39
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8f82e6e42201a1c68c2b2c62bb933887f3d8de77
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87997111"
---
# <a name="deploy-branchcache-hosted-cache-mode"></a>Bereitstellen des BranchCache-Modus „Gehosteter Cache“

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Das Handbuch zum Windows Server 2016-Kern Netzwerk enthält Anweisungen zum Planen und Bereitstellen der Kernkomponenten, die für ein voll funktionsfähiges Netzwerk und eine neue Active Directory &reg; Domäne in einer neuen Gesamtstruktur erforderlich sind.

In diesem Handbuch wird erläutert, wie Sie das zentrale Netzwerk erstellen, indem Sie Anweisungen zum Bereitstellen von BranchCache im Modus "gehosteter Cache" in einer oder mehreren Zweigstellen mit einem schreibgeschützten \- Domänen Controller bereitstellen, auf dem auf Client Computern Windows &reg; 10, Windows 8.1 oder Windows 8 ausgeführt wird und die der Domäne hinzugefügt werden.

>[!IMPORTANT]
>Verwenden Sie diese Anleitung nicht, wenn Sie einen BranchCache-gehosteten Cache Server, auf dem Windows Server 2008 R2 ausgeführt wird, bereitstellen oder bereits bereitgestellt haben. Dieses Handbuch enthält Anweisungen zum Bereitstellen des Modus "gehosteter Cache" mit einem gehosteten Cache Server, auf dem Windows Server &reg; 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.

Dieses Handbuch enthält die folgenden Abschnitte:

- [Voraussetzung für die Verwendung dieses Handbuchs](#bkmk_pre)

- [Informationen zur Anleitung](#bkmk_about)

- [Nicht in diesem Handbuch enthaltene Informationen](#bkmk_not)

- [Technologie Übersichten](#bkmk_tech)

- [BranchCache-Bereitstellung im gehosteten Cache Modus](2-Bc-Hcm-Deploy-Overview.md)

- [BranchCache-Bereitstellungs Planung im gehosteten Cache Modus](3-Bc-Hcm-Plan.md)

- [BranchCache-Bereitstellung im gehosteten Cache Modus](4-Bc-Hcm-Deployment.md)

- [Weitere Ressourcen](11-Bc-Hcm-additional-resources.md)

## <a name="prerequisites-for-using-this-guide"></a><a name="bkmk_pre"></a>Voraussetzung für die Verwendung dieses Handbuchs

Dies ist ein Begleit Handbuch zum Windows Server 2016-Kern Netzwerk Handbuch. Zum Bereitstellen von BranchCache im Modus "Gehosteter Cache" mit diesem Handbuch müssen Sie die folgenden Schritte ausführen.

- Stellen Sie mithilfe des Kernnetzwerkhandbuchs ein Kernnetzwerk in Ihrem Hauptbüro bereit, sofern nicht bereits die im Kernnetzwerkhandbuch beschriebenen Technologien in Ihrem Netzwerk installiert sind und ordnungsgemäß funktionieren. Zu diesen Technologien gehören TCP \/ IP V4, DHCP, Active Directory Domain Services \( AD DS \) und DNS.

    > [!NOTE]
    > Das Windows Server 2016- [Kern Netzwerk Handbuch](../../core-network-guide.md) ist in der technischen Bibliothek für Windows Server 2016 verfügbar.

- Stellen Sie BranchCache-Inhalts Server, auf denen Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird, in ihrer Zentrale oder in einem cloudrechenzentrum bereit. Informationen zum Bereitstellen von BranchCache-Inhalts Servern finden Sie unter [zusätzliche Ressourcen](11-Bc-Hcm-additional-resources.md).

- Richten Sie \( \) mithilfe eines \( VPN- \) , DirectAccess-oder einer anderen Verbindungsmethode für ein virtuelles privates Netzwerk WAN-Verbindungen zwischen Ihrer Zweigstelle, ihrer Zentrale und ggf. ihren cloudressourcen ein.

- Stellen Sie Client Computer in der Zweigstelle bereit, auf denen eines der folgenden Betriebssysteme ausgeführt wird, die BranchCache mit Unterstützung für Bits (Bits), hypertexttransfer-Protokoll (http) und Server Message Block (SMB) bereitstellen.
    - Windows 10 Enterprise
    - Windows 10 Education
    - Windows 8.1 Enterprise
    - Windows 8 Enterprise

> [!NOTE]
> In den folgenden Betriebssystemen unterstützt BranchCache keine HTTP-und SMB-Funktionalität, unterstützt jedoch die BranchCache-Bits-Funktionalität.
>     - Windows 10 pro, nur Bits-Unterstützung
>     - Windows 8.1 pro, nur Bits-Unterstützung
>     - Windows 8 pro, nur Bits-Unterstützung

## <a name="about-this-guide"></a><a name="bkmk_about"></a>Über diesen Leitfaden

Dieses Handbuch richtet sich an Netzwerk-und Systemadministratoren, die die Anweisungen im Windows Server 2016-Kern Netzwerk Handbuch oder im Windows Server 2012-Kern Netzwerk Handbuch zum Bereitstellen eines Kern Netzwerks befolgt haben, oder für diejenigen, die zuvor die im Handbuch zum Hauptnetzwerk enthaltenen Technologien bereitgestellt haben, einschließlich Active Directory Domain Services \( AD DS \) , Domain Name Service \( DNS \) , \( DHCP \) und TCP \/ -IP V4.

Sie sollten die Entwurfs- und Bereitstellungshandbücher für jede der Technologien einsehen, die in diesem Bereitstellungsszenario verwendet werden. Diese Handbücher können Ihnen helfen, zu bestimmen, ob dieses Bereitstellungsszenario die Dienste und Konfigurationen bietet, die Sie zur Organisation des Netzwerks benötigen.

## <a name="what-this-guide-does-not-provide"></a><a name="bkmk_not"></a>Nicht in diesem Handbuch enthaltene Informationen

Dieses Handbuch bietet keine grundlegende Informationen zu BranchCache, Informationen zu Modi und Funktionen von BranchCache inbegriffen.

Dieses Handbuch bietet keine Informationen über die Bereitstellung von WAN-Verbindungen oder anderen Technologien in der Zweigstelle, wie z. B. von DHCP, einem RODC oder VPN-Server.

Darüber hinaus erfahren Sie in diesem Handbuch nicht, welche Hardware Sie zum Bereitstellen von gehosteten Cacheservers verwenden sollten. Sie können zwar andere Dienste und Anwendungen auf dem gehosteten Cacheserver ausführen, jedoch müssen Sie auf der Basis von Arbeitsauslastung, Hardwarefunktionen und Zweigstellengröße bestimmen, ob der gehostete Cacheserver für BranchCache auf einem bestimmten Computer installiert werden soll, und wie viel Speicherplatz für den Cache zugewiesen werden soll.
Dieses Handbuch enthält keine Anweisungen zum Konfigurieren von Computern, auf denen Windows 7 ausgeführt wird. Wenn Sie über Client Computer verfügen, auf denen Windows 7 in ihren Zweigstellen ausgeführt wird, müssen Sie diese mithilfe von Verfahren konfigurieren, die sich von den in diesem Handbuch für Client Computer unter Windows 10, Windows 8.1 und Windows 8 bereitgestellten Verfahren unterscheiden.

Wenn Sie über Computer verfügen, auf denen Windows 7 ausgeführt wird, müssen Sie außerdem den gehosteten Cache Server mit einem Serverzertifikat konfigurieren, das von einer Zertifizierungsstelle ausgestellt wird, der Client Computer vertrauen. \(Wenn auf allen Client Computern Windows 10, Windows 8.1 oder Windows 8 ausgeführt wird, müssen Sie den gehosteten Cache Server nicht mit einem Serverzertifikat konfigurieren.\)
> [!IMPORTANT]
> Wenn auf ihren gehosteten Cache Servern Windows Server 2008 R2 ausgeführt wird, verwenden Sie das Windows Server 2008 R2 [BranchCache-Bereitstellungs Handbuch](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649232(v=ws.10)) anstelle dieser Anleitung, um BranchCache im Modus "gehosteter Cache" bereitzustellen. Wenden Sie die in diesem Handbuch beschriebenen Gruppenrichtlinie Einstellungen auf alle BranchCache-Clients an, auf denen Versionen von Windows von Windows 7 auf Windows 10 ausgeführt werden. Computer, auf denen Windows Server 2008 R2 ausgeführt wird, können mithilfe der in diesem Handbuch beschriebenen Schritte nicht konfiguriert werden.

## <a name="technology-overviews"></a><a name="bkmk_tech"></a>Technologie Übersichten

Bei diesem Begleithandbuch ist BranchCache die einzige Technologie, die Sie installieren und konfigurieren müssen. Sie müssen Windows PowerShell-BranchCache-Befehle auf Ihren Inhaltsservern, z. B. Web- und Dateiservern, ausführen, jedoch müssen Sie die Inhaltsserver auf keine andere Weise ändern oder neu konfigurieren. Außerdem müssen Sie Client Computer mithilfe von Gruppenrichtlinie auf Ihren Domänen Controllern konfigurieren, auf denen AD DS auf Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.

### <a name="branchcache"></a>BranchCache

BranchCache ist eine Technologie zur Optimierung der Bandbreite in einem WAN (Wide Area Network), die in einigen Editionen der Windows Server 2016-und Windows 10-Betriebssysteme sowie in einigen Editionen von Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2 und Windows 7 enthalten ist.

Um die WAN-Bandbreite zu optimieren, wenn Benutzer auf Inhalte auf Remote Servern zugreifen, werden von BranchCache vom Client angeforderte Inhalte von Ihrem Hauptbüro oder von gehosteten cloudanwendungsserver heruntergeladen und in Zweigstellen zwischengespeichert, sodass andere Client Computer in Filialen lokal und nicht über das WAN auf denselben Inhalt zugreifen können.

Wenn Sie BranchCache im Modus "Gehosteter Cache" bereitstellen, müssen Sie die Clientcomputer in der Zweigstelle als Clients im Modus "Gehosteter Cache" konfigurieren, und dann müssen Sie einen gehosteten Cacheserver in der Zweigstelle bereitstellen. In dieser Anleitung wird veranschaulicht, wie Sie Ihren gehosteten Cache Server mit vorab Hash-und vorab geladenen Inhalten von Ihren Web-und Dateiserver \- basierten Inhalts Servern bereitstellen.

### <a name="group-policy"></a>Gruppenrichtlinie

Gruppenrichtlinie in Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ist eine Infrastruktur, mit der eine oder mehrere gewünschte Konfigurationen oder Richtlinien Einstellungen für eine Gruppe von Ziel Benutzern und Computern in einer Active Directory Umgebung bereitgestellt und angewendet werden.

Diese Infrastruktur besteht aus einer Gruppenrichtlinie-Engine und mehreren Client \- seitigen Erweiterungen \( \) , die für das Lesen von Richtlinien Einstellungen auf den Ziel Client Computern zuständig sind.

In diesem Szenario dient die Gruppenrichtlinie zum Konfigurieren von Domänenmitglieds-Clientcomputern mit BranchCache im Modus "Gehosteter Cache".

Informationen zum Fortsetzen dieses Handbuchs finden Sie unter [Übersicht über BranchCache-bereit Stellungen im gehosteten Cache Modus](2-Bc-Hcm-Deploy-Overview.md).