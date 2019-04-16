---
title: Domain Name System (DNS)
description: Dieses Thema enthält eine Übersicht über DNS in Windows Server2016
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 23851d2d8015fc6ae9e0653e8a0843f8c4295162
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="domain-name-system-dns"></a>Domain Name System (DNS)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Domain Name System (DNS) ist eine von der branchenüblichen Suiten von Protokollen, die TCP/IP umfassen, und der DNS-Client und DNS-Server bereit to-IP Name - Computer zusammen Adresse Zuordnung Namensauflösungsdienste für Computer und Benutzer.  
  
> [!NOTE]  
> Zusätzlich zu diesem Thema wird der folgende DNS-Inhalt zur Verfügung.  
>   
> -   [Neues in DNS-Client](What-s-New-in-DNS-Client.md)  
> -   [Neues in DNS-Server](What-s-New-in-DNS-Server.md)  
> -   [DNS-Gruppenrichtlinienszenarien](deploy/DNS-Policy-Scenario-Guide.md)  
> -   Video: [Windows Server 2016: DNS-Verwaltung in IPAM](https://channel9.msdn.com/Blogs/windowsserver/Windows-Server-2016-DNS-management-in-IPAM)  
  
In Windows Server2016 ist DNS eine Serverrolle, die Sie mithilfe von Server-Manager oder Windows PowerShell-Befehle installieren können. Wenn Sie eine neue Active Directory-Gesamtstruktur und Domäne installieren, wird DNS automatisch mit Active Directory als globalen Katalog Server für die Gesamtstruktur und Domäne installiert.  
  
Active Directory-Domänendienste (AD DS) verwendet DNS als Domain Controller Speicherort Mechanismus. Wenn eines der wichtigsten Active Directory-Operationen ausgeführt haben, z.B. Authentifizierung, verwenden aktualisieren oder die Suche nach Computern DNS, um Active Directory-Domänencontroller zu suchen. Darüber hinaus verwenden Domänencontroller DNS gegenseitig erkennen.  
  
Der DNS-Clientdienst ist in allen Client- und Serverversionen von Windows-Betriebssystems enthalten und wird standardmäßig bei der Installation des Betriebssystems ausgeführt wird. Wenn Sie eine TCP/IP-Verbindung mit der IP-Adresse eines DNS-Servers konfigurieren, fragt der DNS-Client den DNS-Server, Domänencontroller und zum Auflösen von Computernamen in IP-Adressen. Beispielsweise fragt, wenn ein Netzwerkbenutzer mit einem Active Directory-Benutzerkonto zu einer Active Directory-Domäne anmeldet, der DNS-Clientdienst den DNS-Server um einen Domänencontroller für Active Directory-Domäne zu suchen. Wenn der DNS-Server auf die Abfrage antwortet und die IP-Adresse des Domänencontrollers an dem Client, der Client kontaktiert den Domänencontroller und der Authentifizierung beginnen können.  
  
Die Windows Server2016-DNS-Server und DNS-Client verwenden des DNS-Protokolls, die in der TCP/IP-Protokollsuite enthalten ist. DNS ist Teil der Anwendungsschicht des TCP/IP-Referenzmodells, wie in der folgenden Abbildungdargestellt.  
  
![DNS in TCP/IP](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

