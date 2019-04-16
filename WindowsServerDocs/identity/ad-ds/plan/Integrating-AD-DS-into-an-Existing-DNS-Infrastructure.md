---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: Integrieren von AD DS in eine vorhandene DNS-Infrastruktur
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ab8d92a237a6d1fb623d9f4bb7dcc88561edf742
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>Integrieren von AD DS in eine vorhandene DNS-Infrastruktur

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Verfügt Ihre Organisation bereits über einen vorhandenen Domain Name System (DNS) Serverdienst, muss das DNS für Active Directory-Domänendienste (AD DS) Besitzer mit dem Besitzer des DNS für Ihre Organisation AD DS in die vorhandene Infrastruktur integrieren funktionieren. Dies beinhaltet das Erstellen eines DNS-Server und DNS-Clientkonfiguration.  
  
## <a name="creating-a-dns-server-configuration"></a>Erstellen einer DNS-Server-Konfiguration  
Wenn Sie AD DS mit einer vorhandenen DNS-Namespace zu integrieren, empfehlen wir, dass Sie die folgenden Schritte aus:  
  
-   Installieren Sie den DNS-Serverdienst auf jedem Domänencontroller in der Gesamtstruktur. Dies bietet Fehlertoleranz, wenn die DNS-Server nicht verfügbar ist. Auf diese Weise müssen Domänencontroller nicht auf andere DNS-Server für die namensauflösung verwendet. Dies vereinfacht auch die Management-Umgebung, da alle Domänencontroller eine einheitliche Konfiguration haben.  
  
-   Konfigurieren Sie Active Directory-Gesamtstruktur Stammdomänencontroller der zum Hosten der DNS-Zone für die Active Directory-Gesamtstruktur.  
  
-   Konfigurieren Sie die Domänencontroller für jede regionale Domäne für die DNS-Zonen, die ihre Active Directory-Domänen entsprechen.  
  
-   Konfigurieren Sie die Zone, die Active Directory-Gesamtstruktur-Locatoreinträge enthält (d. h. die "_msdcs".* Gesamtstrukturname* Zone) auf jedem DNS-Server in der Gesamtstruktur repliziert werden, mithilfe der Gesamtstruktur-DNS-Anwendungsverzeichnispartition.  
  
    > [!NOTE]  
    > Wenn der DNS-Serverdienst (Wir empfehlen diese Option) mit dem Assistenten zum Installieren von Active Directory-Domäne installiert ist, werden alle vorherigen Aufgaben automatisch ausgeführt. Weitere Informationen finden Sie unter [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server2008](https://technet.microsoft.com/library/cc731174.aspx).  
  
    > [!NOTE]  
    > AD DS verwendet gesamtstrukturweiten Locatoreinträge Replikationspartner finden und zum Aktivieren von Clients zum globalen Katalogserver gefunden. AD DS speichert die gesamtstrukturweite Locatoreinträge in die "_msdcs". *Gesamtstrukturname* Zone. Da die Informationen in der Zone allgemein verfügbar sein muss, wird dieser Zone über die Gesamtstruktur-DNS-Anwendungsverzeichnispartition alle DNS-Server in der Gesamtstruktur repliziert.  
  
Die vorhandene DNS-Struktur bleibt erhalten. Sie müssen keine Server oder Zonen zu verschieben. Sie müssen lediglich eine Delegierung von vorhandenen DNS-Hierarchie zu Active Directory-integrierte DNS-Zonen erstellen.  
  
## <a name="creating-the-dns-client-configuration"></a>Erstellen der DNS-Client-Konfiguration  
Zum Konfigurieren von DNS auf Clientcomputern muss das DNS für AD DS-Besitzer Geben Sie den Computer benennen Schema und wie die Clients DNS-Server gesucht werden. Die folgende Tabelle enthält unserer empfohlenen Konfigurationen für diese Elemente.  
  
|Designelement|Konfiguration|  
|------------------|-----------------|  
|Benennung von Computern|Verwenden Sie die Standardnamen. Beim Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 oder Windows Vista-basierten Computer einer Domäne hinzugefügt werden, der Computer weist sich selbst einen vollständig qualifizierten Domänennamen (FQDN), der den Hostnamen des Computers umfasst und den Namen der Active Directory-Domäne.|  
|Client-Weiterleitungskonfiguration|Konfigurieren von Clientcomputern auf einen DNS-Server im Netzwerk.|  
  
> [!NOTE]  
> Active Directory-Clients und Domänencontrollern können dynamisch von DNS-Namen registrieren, auch wenn sie nicht den DNS-Server zeigen, die für ihre Namen autorisierend ist.  
  
Ein Computer möglicherweise einen anderen vorhandenen DNS-Namen, wenn die Organisation zuvor statisch die Computer in DNS oder registriert Wenn die Organisation zuvor eine integrierte Lösung mit Dynamic Host Configuration-Protokoll (DHCP) bereitgestellt. Wenn die Clientcomputer bei der Aktualisierung der Domäne, die sie hinzugefügt wurden, auf Windows Server 2008 AD DS bereits einen registrierten DNS-Namen haben, können sie zwei unterschiedliche Namen verwendet werden:  
  
-   Der vorhandene DNS-name  
  
-   Die neuen vollständig qualifizierten Domänennamen (FQDN)  
  
Clients können entweder mit dem Namen weiterhin befinden. Alle vorhandenen DNS, DHCP oder integrierte DNS und DHCP-Lösung bleibt intakt. Die neuen primären Namen werden automatisch erstellt und über das dynamische Update aktualisiert. Sie werden automatisch über Aufräumen bereinigt.  
  
Wenn Sie Kerberos-Authentifizierung beim Verbinden mit einem Server unter Windows 2000, Windows Server 2003 oder Windows Server 2008 nutzen möchten, müssen Sie sicherstellen, dass der Client mit dem Server verbindet, mit dem primären Namen.  
  


