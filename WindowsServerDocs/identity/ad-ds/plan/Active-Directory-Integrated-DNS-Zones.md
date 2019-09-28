---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: In Active Directory integrierte DNS-Zonen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 858dbc539d48dc3d024ceb871fa9f2d1f80cce0d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402670"
---
# <a name="active-directory-integrated-dns-zones"></a>In Active Directory integrierte DNS-Zonen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Domain Name System (DNS)-Server, die auf Domänen Controllern ausgeführt werden, können Ihre Zonen in Active Directory Domain Services (AD DS) speichern. Auf diese Weise ist es nicht erforderlich, eine separate DNS-Replikations Topologie zu konfigurieren, die normale DNS-Zonenübertragungen verwendet, da alle Zonendaten automatisch mithilfe Active Directory Replikation repliziert werden. Dies vereinfacht den Prozess der Bereitstellung von DNS und bietet die folgenden Vorteile:  
  
-   Für die DNS-Replikation werden mehrere Master erstellt. Daher können alle Domänen Controller in der Domäne, auf der der DNS-Server Dienst ausgeführt wird, Updates für die Active Directory integrierten DNS-Zonen für den Domänen Namen schreiben, für den Sie autorisierend sind. Eine separate DNS-Zonen Übertragungs Topologie ist nicht erforderlich.  
  
-   Sichere dynamische Updates werden unterstützt. Sichere dynamische Updates ermöglichen es einem Administrator zu steuern, welche Computer die Namen aktualisieren und verhindern, dass nicht autorisierte Computer vorhandene Namen in DNS überschreiben.  
  
Active Directory integrierte DNS in Windows Server 2008 speichert Zonendaten in Anwendungsverzeichnis Partitionen. (Es gibt keine Verhaltensänderungen von der Windows Server 2003-basierten DNS-Integration mit Active Directory.) Die folgenden DNS-spezifischen Anwendungsverzeichnis Partitionen werden während AD DS Installation erstellt:  
  
-   Eine Gesamtstruktur weite Anwendungsverzeichnis Partition namens ForestDnsZones  
  
-   Domänen weite Anwendungsverzeichnis Partitionen für jede Domäne in der Gesamtstruktur namens DomainDnsZones  
  
Weitere Informationen dazu, wie AD DS DNS-Informationen in Anwendungs Partitionen speichert, finden Sie in der [technischen Referenz zu DNS](https://go.microsoft.com/fwlink/?LinkId=106636).  
  
> [!NOTE]  
> Es wird empfohlen, DNS zu installieren, wenn Sie die Assistent zum Installieren von Active Directory Domain Services (Dcpromo. exe) ausführen. Wenn Sie dies tun, erstellt der Assistent automatisch die DNS-Zonen Delegierung. Weitere Informationen finden Sie unter Bereitstellen [einer Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx)-Gesamtstruktur-Stamm Domäne.  
  


