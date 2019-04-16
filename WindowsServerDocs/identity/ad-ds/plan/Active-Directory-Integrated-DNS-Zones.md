---
ms.assetid: 39c0126d-af5e-4dcb-88c1-aa38f888e973
title: Active Directory-integrierte DNS-Zonen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 11940ddda320ea36bf8439afed91fcf6803f2fee
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="active-directory-integrated-dns-zones"></a>Active Directory-integrierte DNS-Zonen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Domain Name System (DNS)-Servern, die auf Domänencontrollern ausgeführt, können die Zonen in Active Directory-Domänendienste (AD DS) speichern. Auf diese Weise ist es nicht erforderlich, eine separate DNS-Replikationstopologie zu konfigurieren, die normale Übertragung der DNS-Zone verwendet werden, da alle Zonendaten automatisch mithilfe der Active Directory-Replikation repliziert. Dies vereinfacht den Prozess der Bereitstellung von DNS und bietet die folgenden Vorteile:  
  
-   DNS-Replikation werden mehrere Master erstellt. Daher kann einen beliebigen Domänencontroller in der Domäne mit der DNS-Serverdienst Updates an die Active Directory-integrierte DNS-Zonen für den Domänennamen schreiben, für die er autorisierend sind. Eine separate Übertragung Topologie für die DNS-Zone ist nicht erforderlich.  
  
-   Sichere dynamische Updates unterstützt werden. Sichere dynamische Updates können ein Administrator steuern, welche Computer welche Namen aktualisieren und zu verhindern, dass nicht autorisierte Computer Überschreiben der vorhandene Namen in DNS.  
  
Active Directory-integrierte DNS in Windows Server 2008 speichert Zonendaten in DNS-Anwendungsverzeichnispartitionen. (Es gibt keine verhaltensänderungen von Windows Server 2003-basierten DNS-Integration in Active Directory.) Die folgenden DNS-spezifische Anwendungsverzeichnispartitionen werden während der AD DS-Installation erstellt:  
  
-   Eine gesamtstrukturweite Anwendungsverzeichnispartition, mit dem Namen ForestDnsZones  
  
-   Domänenweite Anwendungsverzeichnispartitionen für jede Domäne in der Gesamtstruktur mit dem Namen DomainDnsZones  
  
Weitere Informationen, wie AD DS DNS-Informationen in Anwendungspartitionen speichert, finden Sie unter der [DNS – technische Referenz](https://go.microsoft.com/fwlink/?LinkId=106636).  
  
> [!NOTE]  
> Es wird empfohlen, dass Sie DNS installieren, wenn Sie den Assistenten für Active Directory Domain Services Installation (Dcpromo.exe) ausführen. Wenn Sie dies tun, erstellt der Assistent automatisch die DNS-zonendelegierung. Weitere Informationen finden Sie unter [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server2008](https://technet.microsoft.com/library/cc731174.aspx).  
  


