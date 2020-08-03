---
ms.assetid: 0fd7b6aa-3e50-45a3-a3a6-56982844363e
title: 'Ereignis-ID 2088: DNS-Suche-Fehler bei erfolgreicher Replikation'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a54b13121933d2780ada9e68a9a7656709947c22
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87518858"
---
# <a name="event-id-2088-dns-lookup-failure-occurred-with-replication-success"></a>Ereignis-ID 2088: DNS-Lookup-Problem bei erfolgreicher Replikation aufgetreten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn ein Zieldomänen Controller, auf dem Windows Server 2003 mit Service Pack 1 (SP1) ausgeführt wird, die Ereignis-ID 2088 im Verzeichnisdienst-Ereignisprotokoll empfängt, ist der Versuch, den Globally Unique Identifier (GUID) im Alias Ressourcen Daten Satz (CNAME) in eine IP-Adresse für den Quell Domänen Controller aufzulösen, fehlgeschlagen. Der Zieldomänen Controller hat jedoch andere Mittel ausprobiert, um den Namen aufzulösen und erfolgreich zu sein, indem entweder der voll qualifizierte Domänen Name (FQDN) oder der NetBIOS-Name des Quell Domänen Controllers verwendet wird. Obwohl die Replikation erfolgreich war, sollte das Domain Name System-Problem (DNS) diagnostiziert und behoben werden.

Im Folgenden finden Sie ein Beispiel für den Ereignistext:

```
Log Name: Directory Service
Source: Microsoft-Windows-ActiveDirectory_DomainService
Date: 3/15/2008  9:20:11 AM
Event ID: 2088
Task Category: DS RPC Client
Level: Warning
Keywords: Classic
User: ANONYMOUS LOGON
Computer: DC3.contoso.com
Description:
Active Directory could not use DNS to resolve the IP address of the source domain controller listed below. To maintain the consistency of Security groups, group policy, users and computers and their passwords, Active Directory Domain Services successfully replicated using the NetBIOS or fully qualified computer name of the source domain controller.
```

Eine ungültige DNS-Konfiguration wirkt sich möglicherweise auf andere wichtige Vorgänge auf Mitglieds Computern, Domänen Controllern oder Anwendungsservern in dieser Active Directory Domain Services Gesamtstruktur aus, einschließlich der Anmelde Authentifizierung oder des Zugriffs auf Netzwerkressourcen.

Sie sollten diesen DNS-Konfigurationsfehler sofort beheben, damit dieser Domänen Controller die IP-Adresse des Quell Domänen Controllers mithilfe von DNS auflösen kann.

Alternativer Servername: DC1 fehlerhafter DNS-Hostname: 4a8717eb-8e58-456c-995a-c92e4add7e8e. _msdcs....

Hinweis: Standardmäßig werden nur bis zu 10 DNS-Fehler für einen Zeitraum von 12 Stunden angezeigt, auch wenn mehr als 10 Fehler auftreten.  Legen Sie den folgenden Wert für die Diagnose Registrierung auf 1 fest, um alle einzelnen Fehlerereignisse zu protokollieren:

Registrierungs Pfad: hklm\system\currentcontrolset\services\ntds\diagnostics\22 DS RPC Client

Benutzeraktion:

1) Wenn der Quell Domänen Controller nicht mehr funktionsfähig ist oder das Betriebssystem mit einem anderen Computernamen oder einer NTDSDSA-Objekt-GUID neu installiert wurde, entfernen Sie die Metadaten des Quell Domänen Controllers mit ntdsutil.exe, indem Sie die im MSKB-Artikel 216498 beschriebenen Schritte ausführen.

2) Vergewissern Sie sich, dass auf dem Quell Domänen Controller Active Directory ausgeführt wird und der Zugriff auf das Netzwerk möglich ist, indem Sie "net View \\ <source DC name> " oder "ping <source DC name> " eingeben.

3) Vergewissern Sie sich, dass der Quell Domänen Controller einen gültigen DNS-Server für DNS-Dienste verwendet und dass der Host Datensatz und der CNAME-Datensatz des Quell Domänen Controllers ordnungsgemäß registriert sind. verwenden Sie dazu die erweiterte DNS-Version von DCDIAG.EXE verfügbar auf<https://www.microsoft.com/dns>

Dcdiag/Test: DNS

4) Vergewissern Sie sich, dass dieser Zieldomänen Controller einen gültigen DNS-Server für DNS-Dienste verwendet, indem Sie die erweiterte DNS-Version DCDIAG.EXE Befehl in der Konsole des Zieldomänen Controllers wie folgt ausführen:

Dcdiag/Test: DNS

5) Informationen zur weiteren Analyse von DNS-Fehler Fehlern finden Sie in KB 824449:<https://support.microsoft.com/?kbid=824449>

Zusätzlicher Datenfehler Wert: 11004 der angeforderte Name ist gültig, aber es wurden keine Daten vom angeforderten Typ gefunden </code> .</introduction>
  <section>
    <title>Diagnosis</title>
    <content>
      <para>Wenn Sie den Namen des Quell Domänen Controllers nicht mithilfe des Alias Ressourceneinsatzes (CNAME) in DNS auflösen, kann dies auf DNS-Fehlkonfigurationen oder Verzögerungen bei der DNS-Datenweitergabe zurückzuführen sein.</para>
    </content>
  </section>
  <section>
    <title>Lösung</title>
    <content>
      <para>Fahren Sie mit den DNS-Tests fort, wie unter &quot; <link xlink:href="85b1d179-f53e-4f95-b0b8-5b1c096a8076">Ereignis-ID 2087: Fehler bei DNS-Suche-Fehler bei der Replikation</link>&quot;</para>
    </content>
  </section>
  <relatedTopics />
</developerConceptualDocument>
