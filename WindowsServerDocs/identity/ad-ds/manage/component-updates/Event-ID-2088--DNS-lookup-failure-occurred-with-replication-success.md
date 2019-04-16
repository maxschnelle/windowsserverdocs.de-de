---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: Ereignis-ID 2088 - DNS-Lookup-Problem bei erfolgreicher Replikation aufgetreten
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 4f223f075775f942f83a1962da28a77e85e89aa0
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>Ereignis-ID 2088: DNS-Lookup-Problem bei erfolgreicher Replikation aufgetreten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

    
    <developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
      <introduction>
    <para>When a destination domain controller running Windows Server 2003 with Service Pack 1 (SP1) receives Event ID 2088 in the Directory Service event log, attempts to resolve the globally unique identifier (GUID) in the alias (CNAME) resource record to an IP address for the source domain controller failed. However, the destination domain controller tried other means to resolve the name and succeeded by using either the fully qualified domain name (FQDN) or the NetBIOS name of the source domain controller. Although replication was successful, the Domain Name System (DNS) problem should be diagnosed and resolved. </para>
    <para>The following is an example of the event text: </para>
    <code>Log Name: Directory Service

    Source: Microsoft-Windows-ActiveDirectory_DomainService
    Date: 3/15/2008  9:20:11 AM
    Event ID: 2088
    Task Category: DS RPC Client 
    Level: Warning
    Keywords: Classic
    User: ANONYMOUS LOGON
    Computer: DC3.contoso.com
    Description:
    Active Directory could not use DNS to resolve the IP address of the 
    source domain controller listed below. To maintain the consistency 
    of Security groups, group policy, users and computers and their passwords, 
    Active Directory Domain Services successfully replicated using the NetBIOS 
    or fully qualified computer name of the source domain controller. 

Ungültige DNS-Konfiguration kann andere wichtige Vorgänge auf Mitgliedscomputern, Domänencontrollern oder Anwendungsserver in Active Directory-Domänendienste-Gesamtstruktur, einschließlich Authentifizierung bei der Anmeldung oder Zugriff auf Netzwerkressourcen beeinträchtigen. 

Sie sollten diesen DNS-Konfigurationsfehler sofort beheben, sodass dieser Domänencontroller die IP-Adresse die Quell-Domänencontroller mit DNS auflösen kann. 

Alternativer Servername: DC1-Fehler bei DNS-Hostnamen: 4a8717eb-8e58-456-c-995a-C92e4add7e8e._msdcs. contoso.com 

Hinweis: Standardmäßig werden nur bis zu 10 DNS-Fehler für einen bestimmten 12-Stunden-Zeitraum angezeigt, auch wenn mehr als 10 Fehler auftreten.  Um sämtliche Fehlerereignisse zu protokollieren, legen Sie die folgenden Diagnose Registrierungswert auf 1 fest: 

Registrierungspfad: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS-RPC-Client 

Handlung des Benutzers: 

1) Ist der Quelldomänencontroller nicht mehr funktioniert oder dessen Betriebssystem neu installiert wurde, einen neuen Computernamen zuweisen oder NTDSDSA Objekt-GUID des Quelldomänencontrollers Metadaten mit ntdsutil.exe entfernen mithilfe der Schritteim Microsoft Knowledge Base-Artikel 216498. 

2) Stellen Sie sicher, dass der Quelldomänencontroller Active Directory ausgeführt wird und im Netzwerk verfügbar, indem Sie eingeben ist "net View \\&lt;Name des Quelldomänencontrollers&gt;" oder "Ping &lt;Name des Quelldomänencontrollers&gt;". 

3) Stellen Sie sicher, dass der Quelldomänencontroller einen gültigen DNS-Server verwendet wird, für DNS-Dienste, und notieren Sie den Quelldomänencontroller Hosteintrag und CNAME sind ordnungsgemäß registriert, mit der DNS-erweiterte Version der DCDIAG.EXE auf https://www.microsoft.com/dns 

Dcdiag//Test: DNS 

4) Stellen Sie sicher, dass der Zieldomänencontroller einen gültigen DNS-Server für DNS-Dienste mithilfe der DNS-erweiterte Version von DCDIAG.EXE Befehl auf der Konsole des dem Zieldomänencontroller wie folgt: 

Dcdiag//Test: DNS 

5) Zur weiteren Analyse der DNS-Fehler-Fehlern finden Sie unter KB 824449: https://support.microsoft.com/?kbid=824449 

Zusätzliche Daten Fehlerwert: 11004 der angeforderte Name ist gültig, jedoch keine Daten des angeforderten Typs gefunden</code>
  </introduction>
  <section>
    <title>Diagnose</title>
    <content>
      <para>der Name des Quelldomänencontrollers mithilfe der Aliasressourceneintrags (CNAME) in DNS aufgelöst kann aufgrund von DNS-Fehlkonfigurationen oder Verzögerungen bei der Verteilung von DNS-Daten.</para>
    </content>
  </section>
  <section>
    <title>Auflösung</title>
    <content>
      <para>fortsetzen DNS zu testen, wie unter "<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">Ereignis-ID 2087: DNS-Lookup-Problem verursacht Replikationsfehler</link>."</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


