---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: 'Ereignis-ID 2088: DNS-Suche-Fehler bei erfolgreicher Replikation'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: d51cbcc93a8decbcb72a1e91854a09345507511d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71368909"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>Ereignis-ID 2088: DNS-Suche-Fehler beim Erfolg der Replikation.

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

    
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

Eine ungültige DNS-Konfiguration wirkt sich möglicherweise auf andere wichtige Vorgänge auf Mitglieds Computern, Domänen Controllern oder Anwendungsservern in dieser Active Directory Domain Services Gesamtstruktur aus, einschließlich der Anmelde Authentifizierung oder des Zugriffs auf Netzwerkressourcen. 

Sie sollten diesen DNS-Konfigurationsfehler sofort beheben, damit dieser Domänen Controller die IP-Adresse des Quell Domänen Controllers mithilfe von DNS auflösen kann. 

Alternativer Servername: DC1 fehlerhafter DNS-Hostname: 4a8717eb-8e58-456c-995a-c92e4add7e8e. _msdcs. 

HINWEIS: Standardmäßig werden nur bis zu 10 DNS-Fehler für einen Zeitraum von 12 Stunden angezeigt, auch wenn mehr als 10 Fehler auftreten.  Legen Sie den folgenden Wert für die Diagnose Registrierung auf 1 fest, um alle einzelnen Fehlerereignisse zu protokollieren: 

Registrierungs Pfad: Hklm\system\currentcontrolset\services\ntds\diagnostics\22 DS RPC Client 

Benutzeraktion: 

1) Wenn der Quell Domänen Controller nicht mehr funktionsfähig ist oder das Betriebssystem mit einem anderen Computernamen oder einer NTDSDSA-Objekt-GUID neu installiert wurde, entfernen Sie die Metadaten des Quell Domänen Controllers mit "Ntdsutil. exe", indem Sie die im MSKB-Artikel beschriebenen Schritte ausführen. 216498. 

2) Vergewissern Sie sich, dass auf dem Quell Domänen Controller Active Directory ausgeführt wird und dass im Netzwerk darauf zugegriffen werden kann, indem Sie "net View \\ @ no__t-1source DC Name @ no__t-2" oder "Ping &lt;source DC Name @ no__t-4" eingeben. 

3) Stellen Sie sicher, dass der Quell Domänen Controller einen gültigen DNS-Server für DNS-Dienste verwendet und dass der Host Daten Satz und der CNAME-Datensatz des Quell Domänen Controllers ordnungsgemäß registriert sind. verwenden Sie dazu die erweiterte DNS-Version von Dcdiag. EXE verfügbar auf <https://www.microsoft.com/dns> 

Dcdiag/Test: DNS 

4) Vergewissern Sie sich, dass dieser Zieldomänen Controller einen gültigen DNS-Server für DNS-Dienste verwendet, indem Sie die erweiterte DNS-Version von Dcdiag ausführen. Befehl "exe" in der Konsole des Zieldomänen Controllers wie folgt: 

Dcdiag/Test: DNS 

5) Informationen zur weiteren Analyse von DNS-Fehler Fehlern finden Sie unter KB 824449: <https://support.microsoft.com/?kbid=824449> 

Zusätzliche Daten Fehlerwert: 11004 der angeforderte Name ist gültig, aber es wurden keine Daten vom angeforderten Typ gefunden @ no__t-0 </introduction>.
  <section>
    <title>diagnose @ no__t-1 @ no__t-2 @ no__t-3<para>Wenn Sie den Namen des Quell Domänen Controllers nicht mithilfe des Alias Ressourceneinsatzes (CNAME) in DNS auflösen, kann dies auf DNS-Fehlkonfigurationen oder Verzögerungen bei der DNS-Datenweitergabe zurückzuführen sein.</para>
    </content>
  </section>
  <section>
    <title>resolution @ no__t-1 @ no__t-2 @ no__t-3<para>Fahren Sie mit den DNS-Tests fort, wie in &quot; @ no__t-1event ID 2087: Fehler beim DNS-Suche-Fehler beim Replikations Fehler @ no__t-0. &quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>


