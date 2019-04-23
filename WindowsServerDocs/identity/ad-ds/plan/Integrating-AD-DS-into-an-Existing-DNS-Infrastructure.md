---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: Integrieren von AD DS in eine vorhandene DNS-Infrastruktur
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 62405ea9ee38bb3fa457b7731e26fbffb2594797
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891041"
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>Integrieren von AD DS in eine vorhandene DNS-Infrastruktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Verfügt Ihre Organisation bereits über einen vorhandenen Domain Name System (DNS) Serverdienst, muss das DNS für den Besitzer der Active Directory Domain Services (AD DS) mit dem Besitzer des DNS für Ihre Organisation AD DS in die vorhandene Infrastruktur integrieren arbeiten. Dies umfasst das Erstellen einer DNS-Server und DNS-Clientkonfiguration.  
  
## <a name="creating-a-dns-server-configuration"></a>Erstellen einer DNS-Server-Konfiguration  
Wenn Sie AD DS mit einer vorhandenen DNS-Namespace zu integrieren, empfehlen wir, dass Sie die folgenden Schritte ausführen:  
  
-   Installieren Sie den DNS-Serverdienst auf jedem Domänencontroller in der Gesamtstruktur. Dies bietet Fehlertoleranz, wenn eine DNS-Server nicht verfügbar ist. Auf diese Weise müssen Domänencontroller keine andere DNS-Server für die namensauflösung verwendet. Dies vereinfacht die Management-Umgebung auch auf, da alle Domänencontroller mit eine einheitliche Konfiguration verfügen.  
  
-   Konfigurieren Sie den Stammdomänencontroller der Active Directory-Gesamtstruktur zum Hosten der DNS-Zone für die Active Directory-Gesamtstruktur.  
  
-   Konfigurieren Sie die Domänencontroller für jede Regionaldomäne zum DNS-Zonen hosten, die ihren Active Directory-Domänen entsprechen.  
  
-   Konfigurieren Sie die Zone, die die Active Directory-Gesamtstruktur-Locatoreinträge enthält (d. h. die "_msdcs". *Gesamtstrukturname* Zone) an alle DNS-Server in der Gesamtstruktur repliziert werden, mit der Gesamtstruktur-DNS-Anwendungsverzeichnispartition.  
  
    > [!NOTE]  
    > Wenn der DNS-Serverdienst (Wir empfehlen diese Option aus), mit dem Assistenten zum Installieren von Active Directory-Domäne installiert ist, werden alle vorherigen Aufgaben automatisch ausgeführt. Weitere Informationen finden Sie unter [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne](https://technet.microsoft.com/library/cc731174.aspx).  
  
    > [!NOTE]  
    > AD DS verwendet eine gesamtstrukturweite Lokatordatensätze um Replikationspartner einander finden und ermöglichen Sie Clients von globalen Katalogserver finden zu aktivieren. AD DS speichert die Gesamtstruktur-Locator-Datensätze in die "_msdcs". *Gesamtstrukturname* Zone. Da die Informationen in der Zone allgemein verfügbar sein muss, wird dieser Zone über die Gesamtstruktur-DNS-Anwendungsverzeichnispartition an alle DNS-Server in der Gesamtstruktur repliziert.  
  
Die vorhandene DNS-Struktur bleibt unverändert. Sie müssen keine Server oder Zonen zu verschieben. Sie müssen lediglich eine Delegierung zu Ihren Active Directory-integrierte DNS-Zonen aus Ihrer vorhandenen DNS-Hierarchie zu erstellen.  
  
## <a name="creating-the-dns-client-configuration"></a>Erstellen die DNS-Client-Konfiguration  
Zum Konfigurieren von DNS auf den Clientcomputern muss das DNS für AD DS-Besitzer Geben Sie den Computer, die Benennung von Schema und wie die Clients die DNS-Server findet. Die folgende Tabelle enthält unsere empfohlenen Konfigurationen für diese Entwurfselemente werden.  
  
|Entwurfselement|Konfiguration|  
|------------------|-----------------|  
|Benennen Computer|Verwenden Sie die Standardnamen. Wenn ein Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 oder Windows Vista-basierten Computer einer Domäne hinzugefügt, der Computer weist selbst einen vollständig qualifizierten Domänennamen (FQDN), der den Hostnamen des Computers enthält und den Namen des aktiven Directory-Domäne.|  
|Client-Resolver-Konfiguration|Konfigurieren von Clientcomputern, um auf einen DNS-Server im Netzwerk zu verweisen.|  
  
> [!NOTE]  
> Active Directory-Clients und Domänencontrollern können dynamisch ihre DNS-Namen registrieren, selbst wenn diese nicht den DNS-Server verweisen, die für ihre Namen autoritativ ist.  
  
Ein Computer möglicherweise einen anderen vorhandenen DNS-Namen aus, wenn die Organisation bisher statisch den Computer in DNS oder registriert Wenn die Organisation zuvor eine integrierte Lösung zur Dynamic Host Configuration Protocol (DHCP) bereitgestellt. Wenn die Clientcomputer bei der Aktualisierung der Domäne, die mit der sie verknüpft sind auf Windows Server 2008 AD DS bereits einen DNS-Name registriert haben, müssen sie zwei verschiedene Namen:  
  
-   Der vorhandene DNS-name  
  
-   Die neuen vollständig qualifizierten Domänennamen (FQDN)  
  
Clients können immer noch von entweder mit dem Namen gesucht werden. Alle vorhandenen DNS, DHCP oder integrierte DNS/DHCP-Lösung bleibt intakt. Die neuen primären Namen werden automatisch erstellt und mithilfe von dynamischen Updates aktualisiert. Sie werden automatisch mithilfe der durch eine Bereinigung bereinigt.  
  
Wenn Sie beim Herstellen einer Verbindung von einem Server unter Windows 2000, Windows Server 2003 oder Windows Server 2008 mit der Kerberos-Authentifizierung nutzen möchten, müssen Sie sicherstellen, dass der Client mit dem Server verbindet, mit dem primären Namen.  
  


