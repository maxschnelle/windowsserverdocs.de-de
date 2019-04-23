---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'Replikationsfehler 1396: Anmeldefehler. Der Zielkontoname ist falsch'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ef3da06dd348b804f538d37cafbfabdd8bf45beb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844501"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>Replikationsfehler 1396: Anmeldefehler. Der Zielkontoname ist falsch

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>In diesem Artikel wird beschrieben, die Symptome, Ursachen und Behebung von Active Directory-Replikation mit dem Win32-Fehler 1396: "Fehler bei der Anmeldung: Der Zielkontoname ist falsch." </para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">Symptome</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">Bewirkt, dass</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">Lösungen</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>Symptome</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>DCDIAG-Berichte, die der Test für die Active Directory-Replikationen mit Fehler 1396 fehlgeschlagen ist: Fehler bei der Anmeldung: Der Zielkontoname ist falsch."</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN. EXE-Berichte, die dem letzten Replikationsversuch mit dem Status 1396 fehlgeschlagen ist.</para><para>REPADMIN-Befehle, die, die dies häufig an den 1396 Status enthalten, jedoch sind nicht darauf beschränkt:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN /REHOST</para></listItem><listItem><para>REPADMIN/SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>Beispielausgabe von "REPADMIN/SHOWREPS" zeigt die eingehenden Replikation vom CONTOSO-DC2 CONTOSO-DC1 mit der "Fehler bei der Anmeldung: Der Zielkontoname ist falsch." Fehler wird im folgenden dargestellt:</para><code>Default-First-Site-NameCONTOSO-DC1
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
</code></listItem><listItem><para>Die <ui>Jetzt replizieren</ui> gibt der Befehl in Active Directory-Standorte und-Dienste "Fehler bei der Anmeldung: Der Zielkontoname ist falsch."</para><para>Mit der rechten Maustaste auf das Verbindungsobjekt aus einem Quell-DC und Auswahl <ui>Jetzt replizieren</ui> schlägt fehl mit "Fehler bei der Anmeldung: Der Zielkontoname ist falsch." Die Fehlermeldung wird auf dem Bildschirm unten gezeigt:</para><para>Titel des dialogtexts:</para><para>Jetzt replizieren</para><para>Dialogfeld-Nachrichtentext: </para><para>Der folgende Fehler aufgetreten ist, bei dem Versuch, die namenskontextsynchronisierung &lt;Pfad der Systempartition DNS&gt; vom Domänencontroller &lt;Quell-DC&gt; Domänencontroller &lt;Ziel-DC&gt;: Fehler bei der Anmeldung: Der Zielkontoname ist falsch. Dieser Vorgang wird nicht fortgesetzt werden. </para></listItem><listItem><para>NTDS KCC, NTDS-Allgemein oder Microsoft-Windows-ActiveDirectory_DomainService Ereignisse mit dem Status 1396 werden in das Verzeichnisdienst-Ereignisprotokoll in der Ereignisanzeige protokolliert.</para><para>Active Directory-Ereignisse, die häufig den Status 1396 zitieren umfassen, aber es sind nicht darauf beschränkt:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Ereignis-ID</para></TD><TD><para>Ereignisquelle</para></TD><TD><para>Ereigniszeichenfolge</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Active Directory Domain Services Installations-Assistenten (Dcpromo) konnte nicht zum Herstellen der Verbindung mit dem folgenden Domänencontroller.</para></TD></tr><tr><TD><para>1645</para><para>Dieses Ereignis Listet den SPN dreiteiligen.</para></TD><TD><para>NTDS-Replikation</para></TD><TD><para>Active Directory hat den authentifizierten Remoteprozeduraufruf (RPC) zu einer anderen Domäne nicht ausgeführt, weil der gewünschte Dienstprinzipalname (SPN) für den Zieldomänencontroller im Schlüsselverteilungscenter (KDC)-Domänencontroller, der zum SPN gehört, nicht registriert ist.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services, die für die Kommunikation mit dem folgenden globalen Katalog hat versucht, und die Versuche nicht erfolgreich waren.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Konsistenzprüfung befindet sich eine replikationsverbindung für den Dienst für lokales Verzeichnis für nur-Lese und versucht, per Remotezugriff in der folgenden Directory-Service-Instanz zu aktualisieren. Der Vorgang ist fehlgeschlagen. Er wird wiederholt.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Fehler beim Herstellen ein Replikationslinks für die folgenden schreibbare Verzeichnispartition.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Der Versuch zum Herstellen eines Replikationslinks zu einer Verzeichnispartition nur-Lese mit den folgenden Parametern, die Fehler.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> Der Server kann nicht seinen Namen im DNS registrieren.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO schlägt fehl mit Fehler auf dem Bildschirm</para><para>Titel des Dialogtexts:</para><para>Fehler bei der Active Directory-Installation.</para><para>Dialogfeld-Nachrichtentext:</para><para>Fehler beim Ausführen des Vorgangs: Active Directory konnte das Serverobjekt für CN erstellen NTDS Settings, CN = ServerBeingPromoted, CN = Servers, CN = = Standort, CN = Sites, CN = Configuration, DC = Contoso, DC = com auf dem Server ReplicationSourceDC.contoso.com. </para><para>Vergewissern Sie sich die bereitgestellten Anmeldeinformationen für das Netzwerk über ausreichende Zugriffsrechte zum Hinzufügen eines Replikats haben. </para><para>
"Fehler bei der Anmeldung: Der Zielkontoname ist falsch. "</para><para>In diesem Fall werden die Ereignis-ID 1168, 1645 und 1125 auf dem Server, der heraufgestuft wird protokolliert.</para></listItem><listItem><para>Ordnen Sie ein Laufwerk mit <embeddedLabel>net verwenden</embeddedLabel>:</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>In diesem Fall die Protokollierung auch 333 der Ereignis-ID in das Systemereignisprotokoll kann der Server, und verwenden Sie einen hohen Betrag an virtuellem Arbeitsspeicher für eine Anwendung z. B. SQL Server.</para></listItem><listItem><para>Der Domänencontroller ist falsch.</para></listItem><listItem><para>Das KDC wird nicht auf einem RODC nach einer Wiederherstellung des Krbtgt-Kontos für den RODC, gestartet, die gelöscht wurde. Die wird nach einer Wiederherstellung, z. B. Fehler 1396 ein. </para><para>
Ereignis-ID 1645 wird auf dem RODC protokolliert. </para><para>
Dcdiag gibt auch eine entsprechende Fehlermeldung das Krbtgt-Konto des RODC nicht aktualisiert werden kann. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>Bewirkt, dass</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>Der SPN für den globalen Katalog vom KDC durchsucht wird, im Auftrag des Clients, es wird versucht, mithilfe von Kerberos authentifizieren ist nicht vorhanden.</para>
          <para>Im Kontext des Active Directory-Replikation der Kerberos-Client ist, dass das Ziel-DC, das Ausführen der SPN-Suche KDC wahrscheinlich der Ziel-DC selbst ist jedoch möglicherweise eine remote-DC.</para>
        </listItem>
        <listItem>
          <para>Der Benutzer oder das Dienstkonto, das enthalten Service principal Name, der gesucht wird, sollte ist auf den globalen Katalog vom KDC durchsucht wird, im Auftrag von Ziel-DC versuchen, zu replizieren nicht vorhanden.</para>
          <para>Im Kontext des Active Directory-Replikation ist die Quell-DC-Computerkonto für den globalen Katalog, die vom Domänencontroller gesucht, für die Durchführung eingehende Replikation von Ziel-DC nicht vorhanden.</para>
        </listItem>
        <listItem>
          <para>Das Ziel-DC verfügt nicht über die LSA-Schlüssel für die Quelldomäne-DCs.</para>
        </listItem>
        <listItem>
          <para>Der SPN, der gesucht werden, die auf einem anderen Computer-Konto als das Quell-DC vorhanden ist.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Lösungen</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>Überprüfen Sie das Verzeichnisdienst-Ereignisprotokoll auf der Ziel-DC für NTDS-Replikationsereignisses 1645, und beachten Sie Folgendes:</para>
          <para>Der Name des Ziel-DC</para>
          <para>Der SPN, der gesucht wird (E3514235-4B06-11D1-AB04-00C04FC2DCD2 /&lt;Objekt-Guid für die Quelle DCs NTDS-Einstellungsobjekt&gt;/&lt;Zieldomäne&gt;.&lt; TLD&gt;@&lt;Zieldomäne&gt;.&lt; TLD&gt;</para>
          <para>Das KDC, die von der Ziel-DC verwendet wird</para>
        </listItem>
        <listItem>
          <para>In der Konsole des in Schritt 1 identifizierten KDC Folgendes ein: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>Führen Sie den NLTEST-Locator-Test einen Replikationsversuch auf, der mit dem Fehler 1396 auf den Zieldomänencontroller nicht unmittelbar folgt. </para>
          <para>Dies sollten diesen globalen Katalogserver ermitteln, die das KDC SPN Suchvorgänge für ausführt. </para>
          <para>Der Garbage Collector vom KDC durchsucht wird möglicherweise auch in Microsoft-Windows-ActiveDirectory_DomainService Ereignis 1655 erfasst werden.</para>
        </listItem>
        <listItem>
          <para>Suchen Sie nach dem SPN, der in Schritt 1 für den globalen Katalog, die in Schritt 2 ermittelt wurden ermittelt.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:"(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)" /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>ODER</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter "(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)" -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>Stellen Sie sicher, dass das Hostobjekt für den SPN vorhanden ist.</para>
          <para>Überprüfen Sie den DN-Pfad für das Objekt des Hosts einschließlich, ob das Objekt CNF ist / Konflikt geändert oder befindet sich in den LostAndFound-Container aus.</para>
          <para>Stellen Sie sicher, dass die Quelle DCs Active Directory-Replikation SPN nur auf dem Quellcomputer Domänencontroller das Computerkonto registriert ist.</para>
          <para>Wenn der Replikations-SPN nicht vorhanden ist, bestimmen Sie, wenn der Quell-DC mit sich selbst der SPN registriert und, ob der SPN auf die GC das KDC aufgrund von einfachen Replikationswartezeit oder aufgrund eines Replikationsfehlers ein, die nicht vorhanden ist.</para>
        </listItem>
        <listItem>
          <para>Überprüfen Sie die Integrität des sicheren Kanals, und vertrauen Sie Integrität.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Problembehandlung bei Active Directory-Vorgänge, bei denen Fehler 1396: Fehler bei der Anmeldung: Der Zielkontoname ist falsch.</linkText>
      <linkUri>https://support.microsoft.com/kb/2183411/en-gb</linkUri>
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


