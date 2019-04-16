---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'Replikationsfehler 1396: Anmeldefehler. der Zielkontoname ist falsch'
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 84799de26e1260f914d9b959357d5eed6fef62f6
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>Replikationsfehler 1396: Anmeldefehler. der Zielkontoname ist falsch

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Dieser Artikel beschreibt die Symptome Ursache und zum Beheben von Active Directory-Replikationsfehler mit Win32-Fehler 1396: "-Anmeldefehler: der Zielkontoname ist falsch." </para><list class="bullet"><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">Symptome</link></para></listItem><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">bewirkt, dass</link></para></listItem><listItem><para><link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">Auflösungen</link></para></listItem></list>
  </introduction>
  <section address="BKMK_Symptoms">
              
    <title>Symptoms</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>DCDIAG reports that the Active Directory Replications test has failed with error 1396: Logon failure: The target account name is incorrect."</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN.EXE reports that the last replication attempt has failed with status 1396.</para><para>REPADMIN commands that commonly cite the 1396 status include but are not limited to:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/Add</para></listItem><listItem><para>REPADMIN/replsum</para></listItem><listItem><para>REPADMIN /REHOST</para></listItem><listItem><para>REPADMIN /SHOWVECTOR /Latency</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/showrepl</para></listItem><listItem><para>repadmin / syncall</para></listItem></list></TD></tr></tbody></table><para>Sample output from "REPADMIN /SHOWREPS" depicting inbound replication from CONTOSO-DC2 to CONTOSO-DC1 failing with the "Logon Failure: The target account name is incorrect." error is shown below::</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1396 (0x574):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.
</code></listItem><listItem><para>The <ui>Replicate now</ui> command in Active Directory Sites and Services returns "Logon Failure: The target account name is incorrect."</para><para>Right-clicking on the connection object from a source DC and choosing <ui>Replicate now</ui> fails with "Logon Failure: The target account name is incorrect." The on-screen error message is shown below:</para><para>Dialog title text:</para><para>Replicate Now</para><para>Dialog message text: </para><para>The following error occurred during the attempt to synchronize naming context &lt;partition DNS path&gt; from domain controller &lt;source DC&gt; to domain controller &lt;destination DC&gt;: Logon Failure: The target account name is incorrect. This operation will not continue. </para></listItem><listItem><para>NTDS KCC, NTDS General or Microsoft-Windows-ActiveDirectory_DomainService events with the 1396 status are logged in the Directory Services log in Event Viewer.</para><para>Active Directory events that commonly cite the 1396 status include but are not limited to:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Ereignis-ID</para></TD><TD><para>Ereignisquelle</para></TD><TD><para>Ereignis Zeichenfolge</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Der Active Directory-Domäne Installation-Assistent (Dcpromo) konnte keine Verbindung mit dem folgenden Domänencontroller herstellen.</para></TD></tr><tr><TD><para>1645</para><para>dieses Ereignis enthält den dreiteilige Dienstprinzipalnamen.</para></TD><TD><para>NTDS-Replikation</para></TD><TD><para>Active Directory hat einen authentifizierten Remoteprozeduraufruf (RPC) an einen anderen Domänencontroller nicht ausgeführt, weil der gewünschte Dienstprinzipalname (SPN) für den Zieldomänencontroller nicht auf dem Schlüsselverteilungscenter (Key Distribution Center, KDC)-Domänencontroller registriert ist, das den SPN auflöst.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services, die zur Kommunikation mit den folgenden globalen Katalog hat versucht, und die Versuche nicht erfolgreich waren.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Konsistenzprüfung befindet sich eine replikationsverbindung für lokalen Verzeichnisdienst schreibgeschützt und hat versucht, es auf die folgenden Verzeichnis Dienstinstanz Remoteaktualisierung. Der Vorgang ist fehlgeschlagen. Es wird wiederholt.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS-KONSISTENZPRÜFUNG (KCC)</para></TD><TD><para>Fehler beim Herstellen ein Replikationslinks für die folgenden schreibbare Verzeichnispartition.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS-KONSISTENZPRÜFUNG (KCC)</para></TD><TD><para>Der Versuch, einen Replikationslink zu einer schreibgeschützten Verzeichnispartition mit den folgenden Parametern konnte nicht hergestellt.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>ANMELDEDIENST</para></TD><TD><para> Der Server kann nicht den Namen in DNS registrieren.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO fails with an onscreen error</para><para>Dialog Title Text:</para><para>Active Directory Installation Failed</para><para>Dialog Message text:</para><para>The operation failed because: The Directory Service failed to create the server object for CN=NTDS Settings,CN=ServerBeingPromoted,CN=Servers,CN=Site,CN=Sites,CN=Configuration,DC=contoso,DC=com on server ReplicationSourceDC.contoso.com. </para><para>Please ensure the network credentials provided have sufficient access to add a replica. </para><para> "Logon Failure: The target account name is incorrect. "</para><para>In this case, Event ID 1645, 1168, and 1125 are logged on the server that is being promoted.</para></listItem><listItem><para>Map a drive using <embeddedLabel>net use</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>In this case, the server can also logging Event ID 333 in the system event log and use a high amount of virtual memory for an application such as SQL Server.</para></listItem><listItem><para>The DC time is incorrect.</para></listItem><listItem><para>The KDC will not start on an RODC after a restore of the krbtgt account for the RODC, which had been deleted. For example, after a restore, error 1396 appears. </para><para> Event ID 1645 is logged on the RODC. </para><para> Dcdiag also reports an error that it cannot update the RODC krbtgt account. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>bewirkt, dass</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>der SPN ist nicht vorhanden, auf den globalen Katalog durchsucht, durch das KDC im Auftrag der Client versucht, mit Kerberos authentifiziert werden.</para>
          <para>In Zusammenhang mit der Active Directory-Replikation, der Kerberos-Client ist der Zieldomänencontroller, das KDC die SPN-Lookup durchgeführt ist wahrscheinlich der Zieldomänencontroller selbst wurde jedoch eine Remote-DC.</para>
        </listItem>
        <listItem>
          <para>der Benutzer oder Dienst Konto, das den Dienst enthalten soll principal Name nachgeschlagen ist nicht vorhanden, auf den globalen Katalog vom KDC im Auftrag der Zieldomänencontroller Replikationsversuch durchsucht.</para>
          <para>In Zusammenhang mit der Active Directory-Replikation, die Quell-DC-Computerkonto existiert nicht auf den globalen Katalog, die vom Domänencontroller für die Durchführung eingehende Replikation von Zieldomänencontroller durchsucht.</para>
        </listItem>
        <listItem>
          <para>der Zieldomänencontroller verfügt nicht über die LSA-Schlüssel für die Domänencontroller-Quelldomäne.</para>
        </listItem>
        <listItem>
          <para>der SPN nachgeschlagen wird auf einem anderen Computerkonto als dem Quelldomänencontroller vorhanden ist.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Auflösungen</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>im Verzeichnisdienst-Ereignisprotokoll auf dem Zieldomänencontroller für NTDS-Replikation Ereignis 1645 und beachten Sie Folgendes:</para>
          <para>den Namen des Ziel-DC</para>
          <para>nachgeschlagen wird der SPN (E3514235-4B06-11D1-AB04-00C04FC2DCD2 /&lt;Objekt-GUID für die Quelle DCs NTDS-Einstellungsobjekt&gt;/&lt;Zieldomäne&gt;.&lt; TLD&gt;@&lt;Zieldomäne&gt;. &lt;Tld&gt;</para>
          <para>das KDC verwendet wird, indem Sie den Zieldomänencontroller</para>
        </listItem>
        <listItem>
          <para>Geben Sie an der Konsole des Schlüsselverteilungscenters identifiziert, die in Schritt1: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>führen Sie den NLTEST Locator-Test unmittelbar nach einen Replikationsversuch, die mit dem Fehler 1396 auf dem Zieldomänencontroller ein Fehler auftritt. </para>
          <para>Identifizieren dieses diesen globalen Katalogserver, die das KDC SPN Suchen in ausführt. </para>
          <para>Das GC vom KDC durchsucht wird auch im Microsoft-Windows-ActiveDirectory_DomainService Ereignis 1655 erfasst werden. </para>
        </listItem>
        <listItem>
          <para>Suchen Sie nach den SPN in Schritt1 für den globalen Katalog in Schritt2 ermittelt ermittelt. </para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:"(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)" /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>Oder</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter "(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)" -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>überprüfen, die das Hostobjekt für den SPN vorhanden sind. </para>
          <para>Überprüfen Sie den DN-Pfad für den Host Objekt z.B., ob das Objekt CNF / Konflikt unvollständig oder befindet sich in den LostAndFound-Container. </para>
          <para>Stellen Sie sicher, dass die Quelle Domänencontroller Active Directory-Replikation SPN nur auf dem Quell-Domänencontroller-Computerkonto registriert ist. </para>
          <para>Fehlt der Replikations-SPN zu bestimmen, ob der Quelldomänencontroller ihren SPN selbst registriert hat, und, ob der SPN auf dem globalen Katalogserver vom KDC aufgrund von einfachen Replikationswartezeit oder einen Replikationsfehler verwendet fehlt. </para>
        </listItem>
        <listItem>
          <para>Überprüfen der Integrität des sicheren Kanals und Integrität zu vertrauen.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Problembehandlung für Active Directory-Vorgänge, die nicht mit dem Fehler 1396: Anmeldefehler: der Zielkontoname ist falsch.</linkText>
      <linkUri>https://support.microsoft.com/kb/2183411/en-gb</linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


