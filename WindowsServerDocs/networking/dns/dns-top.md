---
title: Domain Name System (DNS)
description: Dieses Thema enthält eine Übersicht über DNS in Windows Server 2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 3d4ec63e904dd899a3ddc53a59274ad607136edd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59870821"
---
# <a name="domain-name-system-dns"></a>Domain Name System (DNS)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Domain Name System (DNS) ist eines der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen, und zusammen mit den DNS-Client und der DNS-Server bieten die entsprechenden Computer-IP-Adresse Zuordnung Namensauflösungsdienste für Computer und Benutzer.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema wird Folgendes DNS-verfügbar.  
>   
> -   [Neues in DNS-Client](What-s-New-in-DNS-Client.md)  
> -   [Neues in DNS-Server](What-s-New-in-DNS-Server.md)  
> -   [DNS-Gruppenrichtlinienszenarien](deploy/DNS-Policy-Scenario-Guide.md)  
> -   Video: [Windows Server 2016: DNS-Verwaltung in IPAM](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)  
  
In Windows Server 2016 ist DNS für eine Serverrolle, die Sie installieren können, mithilfe von Server-Manager oder Windows PowerShell-Befehlen. Wenn Sie eine neue Active Directory-Gesamtstruktur und Domäne installieren, wird DNS automatisch in Active Directory als globalen Katalog Server für die Gesamtstruktur und Domäne installiert.  
  
Active Directory-Domänendienste (AD DS) verwendet DNS als Suchmechanismus seine Domäne-Controller. Wenn die Dienstprinzipalnamen Active Directory-Vorgänge ausgeführt wird, wie z. B. Authentifizierung, verwenden aktualisieren, oder suchen Sie, Computer DNS, um Active Directory-Domänencontroller zu suchen. Darüber hinaus verwenden Domänencontroller DNS finden, an.  
  
Der DNS-Clientdienst ist in allen Client- und Server-Versionen des Windows-Betriebssystems enthalten, und standardmäßig nach der Installation des Betriebssystems ausgeführt wird. Wenn Sie eine TCP/IP-Netzwerkverbindung mit der IP-Adresse eines DNS-Servers konfigurieren, fragt der DNS-Client den DNS-Server aus, um den Domänencontroller zu ermitteln und Auflösen von Computernamen in IP-Adressen an. Wenn ein Netzwerkbenutzer mit einem Active Directory-Benutzerkonto zu einer Active Directory-Domäne anmeldet, fragt der DNS-Clientdienst z. B. den DNS-Server um einen Domänencontroller für Active Directory-Domäne zu suchen. Wenn der DNS-Server auf die Abfrage antwortet und die IP-Adresse des Domänencontrollers an dem Client stellt, kann der Client kontaktiert den Domänencontroller und des Authentifizierungsvorgangs zu.  
  
Die Windows Server 2016-DNS-Server und DNS-Client-Dienste verwenden Sie das DNS-Protokoll, das in der TCP/IP-Protokollsuite enthalten ist. DNS ist Teil der Anwendungsschicht des TCP/IP-Verweis dar, wie in der folgenden Abbildung dargestellt.  
  
![DNS in TCP/IP](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

