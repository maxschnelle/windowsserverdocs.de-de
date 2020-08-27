---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: In Active Directory integrierte DNS-Zonen
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: 4f313b09954697f4b54c31a1721311ea0a017dd5
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941270"
---
# <a name="active-directory-integrated-dns-zones"></a>In Active Directory integrierte DNS-Zonen

> Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Domain Name System (DNS)-Server, die auf Domänen Controllern ausgeführt werden, können Ihre Zonen in Active Directory Domain Services (AD DS) speichern. Auf diese Weise ist es nicht erforderlich, eine separate DNS-Replikations Topologie zu konfigurieren, die normale DNS-Zonenübertragungen verwendet, da alle Zonendaten automatisch mithilfe Active Directory Replikation repliziert werden. Dies vereinfacht den Prozess der Bereitstellung von DNS und bietet die folgenden Vorteile:

- Für die DNS-Replikation werden mehrere Master erstellt. Daher können alle Domänen Controller in der Domäne, auf der der DNS-Server Dienst ausgeführt wird, Updates für die Active Directory integrierten DNS-Zonen für den Domänen Namen schreiben, für den Sie autorisierend sind. Eine separate DNS-Zonen Übertragungs Topologie ist nicht erforderlich.

- Sichere dynamische Updates werden unterstützt. Sichere dynamische Updates ermöglichen es einem Administrator zu steuern, welche Computer die Namen aktualisieren und verhindern, dass nicht autorisierte Computer vorhandene Namen in DNS überschreiben.

Active Directory integrierte DNS in Windows Server 2008 speichert Zonendaten in Anwendungsverzeichnis Partitionen. (Es gibt keine Verhaltensänderungen von der Windows Server 2003-basierten DNS-Integration mit Active Directory.) Die folgenden DNS-spezifischen Anwendungsverzeichnis Partitionen werden während AD DS Installation erstellt:

- Eine Gesamtstruktur weite Anwendungsverzeichnis Partition namens ForestDnsZones

- Domänen weite Anwendungsverzeichnis Partitionen für jede Domäne in der Gesamtstruktur namens DomainDnsZones

Weitere Informationen dazu, wie AD DS DNS-Informationen in Anwendungs Partitionen speichert, finden Sie in der [technischen Referenz zu DNS](/previous-versions/windows/it-pro/windows-server-2003/cc779926(v=ws.10)).

> [!NOTE]
> Es wird empfohlen, DNS zu installieren, wenn Sie die Assistent zum Installieren von Active Directory Domain Services ausführen (Dcpromo.exe). Wenn Sie dies tun, erstellt der Assistent automatisch die DNS-Zonen Delegierung. Weitere Informationen finden Sie unter Bereitstellen [einer Windows Server 2008](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc731174(v=ws.10))-Gesamtstruktur-Stamm Domäne.
