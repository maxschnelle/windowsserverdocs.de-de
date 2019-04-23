---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: 'Ereignis-ID 2088: DNS-Lookup-Fehler bei erfolgreicher Replikation aufgetreten'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: cc090fa749a601e53b4347cce43245f22badc8ae
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840711"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>Ereignis-ID 2088: Fehler bei der DNS-Lookups bei erfolgreicher Replikation aufgetreten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

    
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

Ungültiger DNS-Konfiguration kann andere wichtige Vorgänge auf Computern, die Mitglieder, Domänencontroller oder Anwendungsserver in dieser Active Directory-Domänendienste-Gesamtstruktur, z. B. Authentifizierung bei der Anmeldung oder den Zugriff auf Netzwerkressourcen beeinträchtigen. 

Sie sollten diese DNS-Konfiguration-Fehler sofort beheben, damit dieser Domänencontroller die IP-Adresse die Quell-Domänencontroller mit DNS auflösen kann. 

Name des alternativen Servers: DC1-Fehler bei DNS-Hostname: 4a8717eb-8e58-456c-995a-c92e4add7e8e._msdcs.contoso.com 

HINWEIS: Standardmäßig werden nur bis zu 10 DNS-Fehler für alle angegebenen 12-Stunden-Zeitraum angezeigt, auch wenn mehr als 10 Fehler auftreten.  Um alle Fehlerereignisse der einzelnen zu protokollieren, legen Sie die folgenden Diagnose Registrierungswert auf 1: 

Registrierungspfad: HKLM\System\CurrentControlSet\Services\NTDS\Diagnostics\22 DS RPC Client 

Benutzeraktion: 

1) Ist der Quelldomänencontroller nicht mehr ausgeführt werden oder das Betriebssystem neu installiert wurde mit einem anderen Computernamen oder NTDSDSA Objekt-GUID des Quelldomänencontrollers Metadaten mit ntdsutil.exe entfernen mithilfe der im Microsoft Knowledge Base-Artikel beschriebenen Schritte 216498. 

2) Vergewissern Sie sich, dass der Quelldomänencontroller Active Directory ausgeführt wird und im Netzwerk verfügbar, indem Sie eingeben ist "net View \\ &lt;Quell-DC-Namen&gt;" oder "Ping &lt;Quell-DC-Namen&gt;". 

3) Stellen Sie sicher, dass der Quelldomänencontroller auf einen gültigen DNS-Server verwendet wird, für die DNS-Dienste und Aufzeichnen der Quelldomänencontroller Hosteintrag und CNAME sind ordnungsgemäß registriert ist, die verbesserte DNS-Version von DCDIAG. EXE-Datei verfügbar https://www.microsoft.com/dns 

Dcdiag/Test: DNS 

4) Stellen Sie sicher, dass diese Zieldomänencontroller einen gültigen DNS-Server für DNS-Dienste verwendet, durch die verbesserte DNS-Version von DCDIAG ausführen. EXE-Befehl auf der Konsole des dem Zieldomänencontroller, wie folgt: 

Dcdiag/Test: DNS 

5) Zur weiteren Analyse von DNS-Fehler Fehlern finden Sie in der KB 824449: https://support.microsoft.com/?kbid=824449 

Zusätzliche Daten Fehlerwert: 11004 der angeforderte Name ist gültig, aber keine Daten vom angeforderten Typ gefunden</code> </introduction>
  <section>
    <title>Diagnose</title>
    <content>
      <para>Fehler bei der Name des Quelldomänencontrollers mithilfe der Aliasressourceneintrags (CNAME) im DNS auflösen kann aufgrund von DNS-Fehlkonfigurationen oder Verzögerungen bei der Weitergabe von DNS-Daten sein.</para>
    </content>
  </section>
  <section>
    <title>Auflösung</title>
    <content>
      <para>Mit dem DNS-testen, wie in beschrieben fortfahren "<link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">Ereignis-ID 2087: DNS-Lookup-Problem verursacht Replikationsfehler</link>. "</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


