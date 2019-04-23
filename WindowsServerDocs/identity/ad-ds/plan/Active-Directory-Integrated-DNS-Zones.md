---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: In Active Directory integrierte DNS-Zonen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 5e0830944ec5d91dace52db337e89211ee362b98
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59873251"
---
# <a name="active-directory-integrated-dns-zones"></a>In Active Directory integrierte DNS-Zonen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Domain Name System (DNS)-Servern, die auf Domänencontrollern ausgeführt, können die Zonen in Active Directory Domain Services (AD DS) speichern. Auf diese Weise ist es nicht erforderlich, um eine separate DNS-Replikationstopologie zu konfigurieren, die normale DNS-zonenübertragungen verwendet werden, da alle Daten der Zone automatisch mittels Active Directory-Replikation repliziert. Dies vereinfacht das Bereitstellen von DNS und bietet die folgenden Vorteile:  
  
-   Für DNS-Replikation werden mehrere Master erstellt. Aus diesem Grund kann einen beliebigen Domänencontroller in der Domäne, die mit dem DNS-Server-Dienst Updates auf die Active Directory-integrierte DNS-Zonen für den Domänennamen schreiben, für die sie autorisierend sind. Eine separate DNS-Zone Übertragung Topologie ist nicht erforderlich.  
  
-   Sichere dynamische Updates werden unterstützt. Sichere dynamische Updates können es sich um ein Administrator steuern, welche Computer welche Namen aktualisieren und zu verhindern, dass nicht autorisierte Computer vorhandene DNS-Namen zu überschreiben.  
  
Active Directory-integrierte DNS in Windows Server 2008 speichert Zonendaten in Anwendungsverzeichnispartitionen. (Es sind keine Änderungen am Verhalten von Windows Server 2003-basierten DNS-Integration in Active Directory.) Die folgenden DNS-spezifische Anwendungsverzeichnispartitionen werden während der AD DS-Installation erstellt:  
  
-   Eine Gesamtstruktur Anwendungsverzeichnispartition, ForestDnsZones aufgerufen  
  
-   Domänenweite Anwendungsverzeichnispartitionen für jede Domäne in der Gesamtstruktur, mit dem Namen DomainDnsZones  
  
Weitere Informationen dazu, wie AD DS die DNS-Informationen in Anwendungspartitionen speichert, finden Sie unter den [DNS – technische Referenz](https://go.microsoft.com/fwlink/?LinkId=106636).  
  
> [!NOTE]  
> Es wird empfohlen, dass Sie DNS installieren, wenn Sie die Active Directory Domain Services Installations-Assistenten (Dcpromo.exe) ausführen. Wenn Sie so vorgehen, erstellt der Assistent automatisch den DNS-zonendelegierung. Weitere Informationen finden Sie unter [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne](https://technet.microsoft.com/library/cc731174.aspx).  
  


