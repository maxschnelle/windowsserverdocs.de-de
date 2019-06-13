---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: 'Replikationsfehler 1753: Die Endpunktzuordnung hat keine weiteren Endpunkte verfügbar'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e7d2b47c9c14af22cdcf29fb388779e7639e38cb
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442775"
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>Replikationsfehler 1753: Die Endpunktzuordnung hat keine weiteren Endpunkte verfügbar

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>In diesem Thema wird erläutert, Symptome, Ursachen und Behebung von Active Directory-Replikation Fehler 8524 der DSA-Vorgang kann nicht aufgrund eines DNS-Lookup-Fehlers fortgesetzt wird.</para>
    <list class="bullet">
      <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Symptoms">Symptome</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Cause">Ursache</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Resolutions">Lösungen</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_MoreInfo">Weitere Informationen</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>Symptome</title>
    <content>
      <para>Dieser Artikel beschreibt die Symptome, die Ursache und Lösung die Schritte für Active Directory-Vorgänge, bei denen mit Win32-Fehler 1753: &quot;Es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.&quot;</para>
      <list class="ordered">
        <listItem>
          <para>DCDIAG-Berichte, die den Test der Netzwerkverbindung, Active Directory-Replikationen oder KnowsOfRoleHolders Test Fehler 1753 fehlgeschlagen ist: &quot;Es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.&quot;</para>
          <code>Testing server: &lt;site&gt;&lt;DC Name&gt;
Starting test: Connectivity
* Active Directory LDAP Services Check
* Active Directory RPC Services Check
[&lt;DC Name&gt;] <codeFeaturedElement>DsBindWithSpnEx() failed with error 1753,
There are no more endpoints available from the endpoint mapper..</codeFeaturedElement>
Printing RPC Extended Error Info:
Error Record 1, ProcessID is &lt;process ID&gt; (DcDiag) 
System Time is: &lt;date&gt; &lt;time&gt;
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper. Detection location is 500
NumberOfParameters is 4
Unicode string: ncacn_ip_tcp
Unicode string: &lt;source DC object GUID&gt;._msdcs.contoso.com
Long val: -481213899
Long val: 65537
Error Record 2, ProcessID is 700 (DcDiag) 
System Time is: &lt;date&gt; &lt;time&gt;
Generating component is 2 (RPC runtime)
<codeFeaturedElement>Status is 1753: There are no more endpoints available from the endpoint mapper.</codeFeaturedElement>
NumberOfParameters is 1
Unicode string: 1025
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: &lt;DN path of directory partition&gt;
The replication generated an error <codeFeaturedElement>(1753):
There are no more endpoints available from the endpoint mapper.</codeFeaturedElement> 
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
3 failures have occurred since the last success.
The directory on &lt;DC name&gt; is in the process.
of starting up or shutting down, and is not available.
Verify machine is not hung during boot.
</code>
        </listItem>
<listItem><para>REPADMIN. EXE-Datei meldet, dass diese Replikationsversuch mit dem Status 1753 fehlgeschlagen ist.</para><para>REPADMIN-Befehle, die, die dies häufig an den 1753 Status enthalten, jedoch sind nicht darauf beschränkt:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>Beispiel einer Ausgabe &quot;REPADMIN/SHOWREPS&quot; mit eingehende Replikation vom CONTOSO-DC2 CONTOSO-DC1 mit der &quot;Replikationszugriff wurde verweigert&quot; Fehler wird im folgenden dargestellt:</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1753 (0x6d9):
There are no more endpoints available from the endpoint mapper.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.

</code></listItem><listItem><para>Die <ui>überprüfen Sie die Replikationstopologie</ui> gibt der Befehl in Active Directory-Standorte und-Dienste &quot;es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.&quot;</para><para>Mit der rechten Maustaste auf das Verbindungsobjekt aus einem Quell-DC und Auswahl <ui>überprüfen Sie die Replikationstopologie</ui> schlägt mit &quot;es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.&quot; Die Fehlermeldung wird auf dem Bildschirm unten gezeigt:</para><para>Titel des dialogtexts: Überprüfen Sie die Replikationstopologie</para><para>Dialogfeld-Nachrichtentext: </para><para>Fehler beim Versuch, den Domänencontroller zu kontaktieren: Es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.</para></listItem><listItem><para>Die <ui>Jetzt replizieren</ui> gibt der Befehl in Active Directory-Standorte und-Dienste &quot;es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.&quot;</para><para>Mit der rechten Maustaste auf das Verbindungsobjekt aus einem Quell-DC und Auswahl <ui>Jetzt replizieren</ui> schlägt mit &quot;es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.&quot; Die Fehlermeldung wird auf dem Bildschirm unten gezeigt:</para><para>Titel des dialogtexts: Jetzt replizieren</para><para>Dialogfeld-Nachrichtentext: Der folgende Fehler aufgetreten ist, bei dem Versuch, die namenskontextsynchronisierung &lt;Directory Partition Namen %&gt; vom Domänencontroller &lt;Quelldomänencontroller&gt; auf Domänencontroller &lt;Zieldomänencontroller&gt;:</para><para>

Es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar.</para><para>Der Vorgang wird nicht fortgesetzt werden.</para></listItem><listItem><para>NTDS KCC, NTDS-Allgemein oder Microsoft-Windows-ActiveDirectory_DomainService Ereignisse mit dem Status-2146893022 werden in das Verzeichnisdienst-Ereignisprotokoll in der Ereignisanzeige protokolliert.</para><para>Active Directory-Ereignisse, die häufig den Status-2146893022 zitieren umfassen, aber es sind nicht darauf beschränkt:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Ereignis-ID</para></TD><TD><para>Ereignisquelle</para></TD><TD><para>Ereigniszeichenfolge</para></TD></tr></thead><tbody><tr><TD><para>1655</para></TD><TD><para>NTDS Allgemein</para></TD><TD><para>Active Directory versucht, für die Kommunikation mit dem folgenden globalen Katalog und die Versuche nicht erfolgreich waren.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Fehler beim Herstellen ein Replikationslinks für die folgenden schreibbare Verzeichnispartition.</para></TD></tr><tr><TD><para>1265</para></TD><TD><para>NTDS KCC</para></TD><TD><para>Fehler beim durch die Konsistenzprüfung (KCC) ein Replikationsvertrags für den folgenden Directory Partition und Quelle Domänencontroller hinzufügen.</para></TD></tr></tbody></table></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Cause">
    <title>Ursache</title>
    <content>
      <para>Das folgende Diagramm zeigt die RPC-Workflow mit der Registrierung der Server-Anwendung mit dem RPC Endpoint Mapper (EPM) in Schritt 1, das Übergeben von Daten aus der RPC-Client an die Clientanwendung, die in Schritt 7 ab. </para>
      <para>&lt;ADDS_RPCWorkflow&gt;</para>
      <para>Schritte 1 bis 7 Zuordnung auf die folgenden Vorgänge:</para>
      <list class="ordered">
        <listItem>
          <para>Server-app registriert seine Endpunkte mit RPC Endpoint Mapper (EPM) </para>
        </listItem>
        <listItem>
          <para>Client sendet einen RPC-Aufruf (im Auftrag eines Benutzers, Betriebssystem bzw. der Anwendung initiierte Vorgang) </para>
        </listItem>
        <listItem>
          <para>Clientseite RPC-kontaktiert die Zielcomputern EPM und fordern Sie den Endpunkt der Clientaufruf abgeschlossen werden </para>
        </listItem>
        <listItem>
          <para>Server-Computer&#39;s EPM mit einem Endpunkt antwortet </para>
        </listItem>
        <listItem>
          <para>Clientseite RPC kontaktiert die Server-app </para>
        </listItem>
        <listItem>
          <para>Server-app führt der Aufruf, gibt das Ergebnis zurück, an den Client-RPC </para>
        </listItem>
        <listItem>
          <para>Clientseite RPC übergibt das Ergebnis an die Client-app</para>
        </listItem>
      </list>
      <para>Fehler bei 1753 wird durch einen Fehler zwischen den Schritten 3 mit # und #4 generiert. Insbesondere bedeutet Fehler 1753 an, dass der RPC-Client (Ziel-DC) den RPC-Server (Quell-DC) über Port 135 zu kontaktieren konnte, aber der EPM für den RPC-Server (Quell-DC) konnte den RPC-Anwendung von Interesse zu finden und serverseitiger Fehler 1753 zurückgegeben. Das Vorhandensein der 1753 Fehler gibt an, dass der RPC-Client (Ziel-DC) die Antwort des Servers Seite Fehler von der RPC-Server (Active Directory-Replikation Quell-DC) über das Netzwerk empfangen. </para>
      <para>Bestimmte Ursachen für den Fehler 1753: </para>
      <list class="ordered">
        <listItem>
          <para>Der Server-app, die nie gestartet (z. B. Schritt Nr. 1 in der &quot;Informationen&quot; Diagramm befindet sich oben wurde noch nie versucht).</para>
        </listItem>
        <listItem>
          <para>Die Server-app gestartet, aber ein Fehler aufgetreten, während der Initialisierung, die Registrierung bei der RPC-Endpunktzuordnung verhindert (d. h. Schritt 1 im der &quot;Informationen&quot; im obigen Diagramm war nicht möglich).</para>
        </listItem>
        <listItem>
          <para>Die Server-app gestartet, aber anschließend wurde unerwartet beendet. (d. h. Schritt Nr. 1 in der &quot;Informationen&quot; Diagramm oben wurde erfolgreich abgeschlossen, aber wurde rückgängig gemacht werden später noch Mal, da der Server wurde unerwartet beendet).</para>
        </listItem>
        <listItem>
          <para>Die Server-app nicht manuell registriert seine Endpunkte (ähnlich wie 3 jedoch beabsichtigt. Nicht wahrscheinlich jedoch enthalten aus Gründen der Vollständigkeit.)</para>
        </listItem>
        <listItem>
          <para>Der RPC-Client (Ziel-DC) kontaktiert anderen RPC-Server als das vorgesehene aufgrund einen Namen zu IP-Zuordnungsfehler in DNS, WINS oder Host/Lmhosts-Datei.</para>
        </listItem>
      </list>
      <para>Fehler 1753 wird nicht durch verursacht: </para>
      <list class="bullet">
        <listItem>
          <para>Eine fehlende Netzwerkkonnektivität zwischen dem RPC-Client (Ziel-DC) und RPC-Server (Quell-DC) über Port 135</para>
        </listItem>
        <listItem>
          <para>Eine fehlende Netzwerkkonnektivität zwischen dem RPC-Server (Quell-DC) über Port 135 und der RPC-Client (Ziel-DC) über den kurzlebigen Port. </para>
        </listItem>
        <listItem>
          <para>Einem kennwortkonflikt oder keine von der Quell-DC zum Entschlüsseln eines verschlüsselten Kerberos-Pakets </para>
        </listItem>
      </list>
      <para> </para>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Lösungen</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>
            <embeddedLabel>Stellen Sie sicher, dass der Dienst den Dienst registrieren, mit der endpunktzuordnung gestartet wurde</embeddedLabel>
          </para>
          <para>Für Windows 2000 und Windows Server 2003-DCs: Stellen Sie sicher, dass der Quell-DC im normalen Modus gestartet wird. </para>
          <para>
Für Windows Server 2008 oder Windows Server 2008 R2: Klicken Sie in der Konsole von der Quell-DC-Managers (services.msc) starten, und überprüfen, ob die <embeddedLabel>Active Directory Domain Services</embeddedLabel> -Dienst wird ausgeführt. </para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Stellen Sie sicher, RPC-Clients (Zielendpunkte DC) an, die mit dem gewünschten RPC-Server (Quell-DC) verbunden sind</embeddedLabel>
          </para>
          <para>Alle Domänencontroller in einer allgemeinen Active Directory-Gesamtstruktur registrieren Sie einen Domänencontroller CNAME-Eintrag in die "_msdcs". &lt;Gesamtstruktur-Stammdomäne&gt; DNS-Zone, unabhängig davon, welche sie befinden sich im innerhalb der Gesamtstruktur, Domäne. Der DC-CNAME-Eintrag ergibt sich aus der <embeddedLabel>"objectGUID"</embeddedLabel> -Attribut des NTDS-Einstellungsobjekts für jeden Domänencontroller. </para>
          <para>Bei der Replikation-basierte Vorgänge durchführen, fragt einen Ziel-DC DNS für die Quell-Domänencontroller-CNAME-Eintrag. Der CNAME-Eintrag enthält den vollqualifizierten Quell-DC-Computernamen, mit der die Quell-Domänencontroller-IP-Adresse abgeleitet werden, über DNS-Client-Cache-Lookup, Host / LMHost file, Suche, Host A / AAAA aufzeichnen in DNS oder WINS. </para>
          <para>NTDS-Einstellungsobjekten veraltete und ungültige Namen zu IP-Zuordnungen in DNS, WINS, Host und LMHOST Dateien können dazu führen, dass des RPC-Clients (Ziel-DC) zur Verbindung mit dem falschen RPC-Server (Quell-DC). Darüber hinaus kann die ungültige Namen zu IP-Zuordnung veranlasst, dass die RPC-(Ziel-DC) zur Verbindung mit eines Computers, die nicht auch der RPC-Server-Anwendung von Interesse sind (in diesem Fall die Active Directory-Rolle) installiert. (Beispiel: ein veraltete Hosteintrag für DC2 enthält die IP-Adresse von DC3 oder einen Computer als Mitglied). </para>
          <para>Stellen Sie sicher, dass die "objectGUID" für die Quell-DC, die im Ziel-DCs Kopie von Active Directory vorhanden ist. die Quell-DC "objectGUID" gespeichert, in der Quelle DCs Kopie von Active Directory übereinstimmt. Ist eine Abweichung, können Sie Repadmin/showobjmeta für Ntds-Einstellungsobjekt verwenden, um anzuzeigen, die letzte heraufstufung des Quelldomänencontrollers entspricht (Hinweis: Vergleichen von Datumsangaben für das NTDS-Einstellungsobjekt Erstellungsdatum aus/showobjmeta für das Datum der letzten heraufstufung in die DCs dcpromo.log-Quelldatei. Möglicherweise verwenden Sie das letzte "ändern", oder erstellen das DCPROMO-Dienstprogramm Datum. Protokolldatei selbst). Wenn die Objekt-GUIDs nicht identisch sind, hat das Ziel-DC wahrscheinlich ein veralteter NTDS-Einstellungsobjekt für den Quell-DC, dessen CNAME-Datensatz auf einen Hosteintrag mit einem ungültigen Namen für die IP-Zuordnung bezieht sich, auf. </para>
          <para>Führen Sie auf der Ziel-DC IPCONFIG/all ausgeführt um zu bestimmen, welche DNS-Server das Ziel, die, das Domänencontroller für die namensauflösung verwendet wird:</para>
          <code>c:&gt;ipconfig /all</code>
          <para>Führen Sie auf der Ziel-DC NSLOOKUP, für die Quelle DCs vollqualifizierten DC-CNAME-Eintrag:</para>
          <code>c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs primary DNS Server IP &gt;
c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs secondary DNS Server IP&gt;</code>
          <para>Stellen Sie sicher, dass die IP-Adresse von NSLOOKUP zurückgegeben &quot;besitzt&quot; den Hostnamen / Sicherheits-ID von der Quell-DC:</para>
          <code>C:&gt;NBTSTAT -A &lt;IP address returned by NSLOOKUP in the step above&gt;</code>
          <para>oder</para>
          <para>Melden Sie sich auf der Konsole von der Quell-DC, führen Sie &quot;IPCONFIG&quot; fordert über den Befehl aus, und stellen Sie sicher, dass der Quell-DC die IP-Adresse, die vom oben genannten Befehls "NSLOOKUP" besitzt</para>
          <para>Überprüfen Sie für veraltete / doppelte Host-IP-Zuordnungen im DNS</para>
          <code>NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;secondary DNS Server IP on destination DC&gt;

NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;secondary DNS Server IP on dest. DC&gt;</code>
<para>Wenn eine ungültige IP-Adresse im Hostdatensätze vorhanden sind, prüfen Sie, ob DNS-Aufräumvorgänge aktiviert und ordnungsgemäß konfiguriert ist. </para><para>Wenn die oben angegebenen Tests oder in einem Netzwerk Ablaufverfolgung&#39;Anzeigen einer benannten Abfrage zurückgeben eine ungültige IP-Adresse, sollten Sie veraltete Einträge im HOST-Dateien, die LMHOSTS-Dateien und WINS-Server. Beachten Sie, dass DNS-Server auch für die WINS-fallback namensauflösung konfiguriert werden können.</para>
</listItem>
        <listItem>
          <para>
            <embeddedLabel>Stellen Sie sicher, dass die Server-Anwendung (Active Directory Et al.), mit der endpunktzuordnung auf dem RPC-Server (Quell-DC registriert hat)</embeddedLabel>
          </para>
          <para>Active Directory verwendet eine Kombination aus bekannten und dynamisch registrierten Ports. Diese Tabelle enthält die bekannten Ports und Protokolle, die von Active Directory-Domänencontrollern verwendet.</para>
          <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
            <thead>
              <tr>
                <TD>
                  <para>RPC-Server-Anwendung</para>
                </TD>
                <TD>
                  <para>Port</para>
                </TD>
                <TD>
                  <para>TCP</para>
                </TD>
                <TD>
                  <para>UDP</para>
                </TD>
              </tr>
            </thead>
            <tbody>
              <tr>
                <TD>
                  <para>DNS-Server</para>
                </TD>
                <TD>
                  <para>53</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Kerberos</para>
                </TD>
                <TD>
                  <para>88</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LDAP-server</para>
                </TD>
                <TD>
                  <para>389</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Microsoft-DS</para>
                </TD>
                <TD>
                  <para>445</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>LDAP-SSL</para>
                </TD>
                <TD>
                  <para>636</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Globaler Katalogserver</para>
                </TD>
                <TD>
                  <para>3268</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
              <tr>
                <TD>
                  <para>Globaler Katalogserver</para>
                </TD>
                <TD>
                  <para>3269</para>
                </TD>
                <TD>
                  <para>X</para>
                </TD>
                <TD>
                  <para />
                </TD>
              </tr>
            </tbody>
          </table>
          <para>Well-Known-Ports sind nicht mit der endpunktzuordnung registriert. </para>
          <para>Active Directory und anderen Anwendungen registrieren außerdem Dienste, die dynamisch zugewiesene Ports im kurzlebigen RPC-Portbereich zu erhalten. Solche RPC-Server-Anwendungen werden dynamisch TCP-Ports zwischen 1024 und 5000 auf Windows 2000 und Windows Server 2003-Computern und Ports zwischen 49152 und 65535 Bereichs auf Windows Server 2008 und Windows Server 2008 R2-Computern zugewiesen werden. Der RPC-Port, der von der Replikation kann hartcodiert werden, in der Registrierung verwenden die Schritte im <externalLink> <linkText>KB-Artikel 224196</linkText> <linkUri> <a href="https://support.microsoft.com/kb/224196" data-raw-source="https://support.microsoft.com/kb/224196"> https://support.microsoft.com/kb/224196 </a> </linkUri> </externalLink>. Active Directory wird weiterhin mit der EPM konfiguriert verwendet einen hartcodierten Port zu registrieren. </para>
          <para>Stellen Sie sicher, dass die RPC-Server-Anwendung von Interesse sind mit der RPC-endpunktzuordnung auf dem RPC-Server (der Quell-DC im Fall von Active Directory-Replikation) registriert hat. </para>
          <para>Es gibt zahlreiche Möglichkeiten zum Ausführen dieser Aufgabe, aber eine besteht darin, installieren und Ausführen von PORTQRY von einem Administrator, privilegierter CMD-Eingabeaufforderung in der Konsole des Quelldomänencontrollers mithilfe der Syntax: </para>
          <code>c:&amp;gt;portquery -n &lt;source DC&gt; -e 135 &gt;file.txt</code>
          <para>Beachten Sie in der Ausgabe Portqry die Portnummern, die vom dynamisch registriert die &quot;MS NT Directory DRS Interface&quot; (UUID = 351...) für die <embeddedLabel>Ncacn_ip_tcp Protokoll</embeddedLabel>. Der folgende Codeausschnitt zeigt die Ausgabe des Beispiels Portquery aus einem Windows Server 2008 R2-DC und die UUID / Protokoll-Paar, insbesondere von Active Directory verwendet hervorgehoben <embeddedLabel>fett</embeddedLabel>: </para>
          <code>UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\pipe\lsass] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\PIPE\protected_storage] 
<codeFeaturedElement>UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_ip_tcp:CONTOSO-DC01[49156]</codeFeaturedElement> 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[49157] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[6004]</code>
          <para />
        </listItem>
        <listItem>
          <para>Andere Möglichkeiten zum Beheben dieses Fehlers:</para>
          <list class="ordered">
            <listItem>
              <para>Stellen Sie sicher, dass der Quell-DC im normalen Modus gestartet wird und die Betriebssystem und DC-Rolle auf der Quell-DC vollständig gestartet haben.</para>
            </listItem>
            <listItem>
              <para>Stellen Sie sicher, dass die Active Directory Domain Services ausgeführt wird. Wenn der Dienst beendet wurde oder nicht mit den Standardwerten für die beim Start konfiguriert wurde, die Start-Standardwerte zurückzusetzen, starten Sie die geänderten DC neu, dann den Vorgang wiederholen.</para>
            </listItem>
            <listItem>
              <para>Stellen Sie sicher, dass der Startstatus-Dienst und dem Wert für RPC-Dienst und RPC-Locator für die Betriebssystemversion des RPC-Clients (Ziel-DC) und RPC-Server (Quell-DC) korrekt ist. Wenn der Dienst beendet wurde oder nicht mit den Standardwerten für die beim Start konfiguriert wurde, die Start-Standardwerte zurückzusetzen, starten Sie die geänderten DC neu, dann den Vorgang wiederholen.</para>
              <para>Darüber hinaus stellen Sie sicher, dass der Dienstkontext Standardeinstellungen, die in der folgenden Tabelle aufgeführten übereinstimmt.</para>
              <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>Service</para>
                    </TD>
                    <TD>
                      <para>Standardstatus (Starttyp) in Windows Server 2003 und höher </para>
                    </TD>
                    <TD>
                      <para>Standardstatus (Starttyp) in Windows Server 2000</para>
                    </TD>
                  </tr>
                </thead>
                <tbody>
                  <tr>
                    <TD>
                      <para>Remoteprozeduraufruf</para>
                    </TD>
                    <TD>
                      <para>Gestartet (automatisch)</para>
                    </TD>
                    <TD>
                      <para>Gestartet (automatisch)</para>
                    </TD>
                  </tr>
                  <tr>
                    <TD>
                      <para>Remoteprozeduraufruf-Aufruf-Locators</para>
                    </TD>
                    <TD>
                      <para>NULL oder mehr (manuell)</para>
                    </TD>
                    <TD>
                      <para>Gestartet (automatisch)</para>
                    </TD>
                  </tr>
                </tbody>
              </table>
            </listItem>
            <listItem>
              <para>Stellen Sie sicher, dass die Größe des dynamischen Portbereich nicht eingeschränkt wurde. Die Syntax für Windows Server 2008 und Windows Server 2008 R2 NETSH zum Aufzählen des RPC-Portbereich ist unten dargestellt:</para>
              <code>&gt;netsh int ipv4 show dynamicport tcp
&gt;netsh int ipv4 show dynamicport udp
&gt;netsh int ipv6 show dynamicport tcp
&gt;netsh int ipv6 show dynamicport udp</code>
            </listItem>
            <listItem>
              <para>Sicherstellen Sie, dass die dynamischen Portbereich für DCs OS Quellversion hartcodierten Port-Definitionen, die in KB 224196 definierten fallen.</para>
              <para>Überprüfen Sie <externalLink> <linkText>KB-Artikel 224196</linkText> <linkUri> <a href="https://support.microsoft.com/kb/224196" data-raw-source="https://support.microsoft.com/kb/224196"> https://support.microsoft.com/kb/224196 </a> </linkUri> </externalLink> und stellen Sie sicher, dass die hartcodierte Port innerhalb der temporäre Portbereich für liegt der Quell-DC&#39;s Betriebssystemversion.</para>
            </listItem>
            <listItem>
              <para>Stellen Sie sicher, dass der Schlüssel ClientProtocols unter HKLM\Software\Microsoft\Rpc vorhanden und die folgenden 5 Standardwerte enthält:</para>
              <code>ncacn_http REG_SZ rpcrt4.dll
ncacn_ip_tcp REG_SZ rpcrt4.dll
<codeFeaturedElement>ncacn_nb_tcp REG_SZ rpcrt4.dll</codeFeaturedElement>
ncacn_np REG_SZ rpcrt4.dll
ncacn_ip_udp REG_SZ rpcrt4.dll</code>
            </listItem>
          </list>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_MoreInfo">
    <title>Weitere Informationen</title>
    <content>
      <para>
        <embeddedLabel>Beispiel für einen ungültigen Namen auf IP-Adresse zuordnen zu RPC-Fehlers 1753 im Vergleich zu-2146893022: der Zielprinzipalname ist falsch</embeddedLabel>
      </para>
      <para>Die Domäne "contoso.com" besteht aus DC1 und DC2 mit IP-Adressen x.x.1.1 und x.x.1.2. Der Host &quot;ein&quot; / &quot;AAAA&quot; Datensätze für DC2 sind auf allen für DC1 konfigurierten DNS-Server ordnungsgemäß registriert. Darüber hinaus enthält die Hostdatei auf DC1 einen Eintrag DC2s vollqualifizierter Hostname, IP-Adresse x.x.1.2 zuordnen. Später DC2&#39;IP-Adresse ändert sich von X.X.1.2 in X.X.1.3 und ein neuen Computer als Mitglied der Domäne mit IP-Adresse x.x.1.2 verknüpft ist. Active Directory-Replikation Versuch ausgelöst wird, durch die <ui>Jetzt replizieren</ui> Befehl im Active Directory-Standorte und -Dienste-Snap-in tritt der Fehler 1753 wie in der Ablaufverfolgung unten gezeigt:</para>
      <code>F# SRC    DEST    Operation 
1 x.x.1.1 x.x.1.2 ARP:Request, x.x.1.1 asks for x.x.1.2
2 x.x.1.2 x.x.1.1 ARP:Response, x.x.1.2 at 00-13-72-28-C8-5E
3 x.x.1.1 x.x.1.2 TCP:Flags=......S., SrcPort=50206, DstPort=DCE endpoint resolution(135)
4 x.x.1.2 x.x.1.1 ARP:Request, x.x.1.2 asks for x.x.1.1
5 x.x.1.1 x.x.1.2 ARP:Response, x.x.1.1 at 00-15-5D-42-2E-00
6 x.x.1.2 x.x.1.1 TCP:Flags=...A..S., SrcPort=DCE endpoint resolution(135)
7 x.x.1.1 x.x.1.2 TCP:Flags=...A...., SrcPort=50206, DstPort=DCE endpoint resolution(135)
8 x.x.1.1 x.x.1.2 MSRPC:c/o Bind: UUID{E1AF8308-5D1F-11C9-91A4-08002B14A0FA} EPT(EPMP) 
9 x.x.1.2 x.x.1.1 MSRPC:c/o Bind Ack: Call=0x2 Assoc Grp=0x5E68 Xmit=0x16D0 Recv=0x16D0 
<codeFeaturedElement>10</codeFeaturedElement> x.x.1.1 x.x.1.2 EPM:Request: ept_map: NDR, DRSR(DRSR) {E3514235-4B06-11D1-AB04-00C04FC2DCD2} [DCE endpoint resolution(135)]
<codeFeaturedElement>11</codeFeaturedElement> x.x.1.2 x.x.1.1 EPM:Response: ept_map: 0x16C9A0D6 - EP_S_NOT_REGISTERED
</code>
      <para>Am Frame <embeddedLabel>10</embeddedLabel>, das Ziel-DC-Mapper Datenquelle DCs Endpunkt über Port 135 für die Active Directory-Replikation-Dienstklasse UUID E351 Abfragen... </para>
      <para>Im Frame <embeddedLabel>11</embeddedLabel>, der Quell-DC, in diesem Fall einen Mitgliedscomputer, der die DC-Rolle ist noch kein host und die E351 wurde nicht registriert... UUID für der Replikationsdienst, mit der lokalen EPM mit symbolischen Fehler EP_S_NOT_REGISTERED reagiert der decimal-Fehler 1753 zuordnet hex-Fehler 0x6d9 und Fehlermeldung &quot;stehen keine Endpunkte mehr von der endpunktzuordnung&quot; .</para>
      <para>Später, die Member-Computer mit IP-Adresse x.x.1.2 höher gestuft als Replikat &quot;MayberryDC&quot; in der Domäne "contoso.com". In diesem Fall die <ui>Jetzt replizieren</ui> Befehl wird für die Replikation ausgelöst, aber dieses Mal schlägt fehl, mit der auf dem Bildschirm Fehler &quot;der Zielprinzipalname ist falsch.&quot; Der Computer, dessen Netzwerkadapter ist die IP-Adresse zugewiesen, Adresse x.x.1.2 <placeholder>ist</placeholder> ein Domänencontroller wird derzeit im normalen Modus gestartet und wurde die E351 registriert... Replikationsdienst UUID, mit der lokalen EPM jedoch besitzt nicht die Identität oder einer Sicherheitsgruppe von DC2 und die Kerberos-Anforderung von DC1 kann nicht entschlüsselt werden, damit die Anforderung jetzt führt zu einem Fehler &quot;der Zielprinzipalname ist falsch.&quot; Der Fehler ist decimal Fehler-2146893022 / Fehler 0x80090322 hex. </para>
      <para>Können eine solche ungültige Host-IP-Zuordnungen veraltete Einträge im Host zurückzuführen sein / Lmhost-Dateien, host A / AAAA-Registrierungen in DNS oder WINS. </para>
      <para>Zusammenfassung In diesem Beispiel ist fehlgeschlagen, da eine ungültige Host-IP-Zuordnung (in der Hosts-Datei in diesem Fall) verursacht, das Ziel-DC in aufgelöst wurde eine &quot;Quelle&quot; DC, der keine der Active Directory Domain Services-Dienst wird ausgeführt (oder sogar für installiert eigentlich), damit die Replikation SPN wurde noch nicht registriert und der Quell-DC Fehler 1753 zurückgegeben. Im zweiten Fall verursacht eine ungültige Host-IP-Zuordnung (wieder in die HOST-Datei) das Ziel-DC die Verbindung mit einem DC, der die E351 registriert haben... Replikations-SPN, aber diese Quelle mussten eine andere Identität für Hostname und die Sicherheit als den vorgesehenen Quelldomänencontroller, daher versucht die-2146893022 fehlgeschlagen: Der Zielprinzipalname ist falsch.</para>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Problembehandlung bei Active Directory-Vorgänge, bei denen Fehler 1753: Es sind keine weiteren Endpunkte von der endpunktzuordnung verfügbar. </linkText> 
      <linkUri> <a href="https://support.microsoft.com/kb/2089874" data-raw-source="https://support.microsoft.com/kb/2089874"> https://support.microsoft.com/kb/2089874 </a> </linkUri> 
    </externalLink> 
<externalLink> <linkText>KB-Artikel 839880 Problembehandlung bei RPC-Endpunktzuordnung Fehler bei der Verwendung der Unterstützung von Windows Server 2003 Tools von der Produkt-CD</linkText><linkUri><a href="https://support.microsoft.com/kb/839880" data-raw-source="https://support.microsoft.com/kb/839880">https://support.microsoft.com/kb/839880</a></linkUri></externalLink>
<externalLink><linkText>KB-Artikel 832017 dienstübersicht und Dienstport Anforderungen für das Windows Server System</linkText><linkUri><a href="https://support.microsoft.com/kb/832017/" data-raw-source="https://support.microsoft.com/kb/832017/">https://support.microsoft.com/kb/832017/</a></linkUri></externalLink>
<externalLink><linkText>KB-Artikel 224196 einschränken Active Directory-Replikations-Datenverkehr als auch Client-RPC-Datenverkehr zu einem bestimmten Port</linkText><linkUri><a href="https://support.microsoft.com/kb/224196/" data-raw-source="https://support.microsoft.com/kb/224196/">https://support.microsoft.com/kb/224196/</a></linkUri></externalLink>
<externalLink><linkText>KB-Artikel 154596 Vorgehensweise: Konfigurieren der dynamischen RPC-portzuweisung portzuweisung</linkText><linkUri><a href="https://support.microsoft.com/kb/154596" data-raw-source="https://support.microsoft.com/kb/154596">https://support.microsoft.com/kb/154596</a></linkUri></externalLink><externalLink><linkText>wie RPC Works</linkText><linkUri><a href="https://msdn.microsoft.com/library/aa373935(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373935(VS.85).aspx">https://msdn.microsoft.com/library/aa373935(VS.85).aspx</a></linkUri></externalLink><externalLink><linkText>wie der Server für die eine Verbindung vorbereitet</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373938(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373938(VS.85).aspx"> https://msdn.microsoft.com/library/aa373938(VS.85).aspx </a> </linkUri> </externalLink> 
<externalLink> <linkText>Wie der Client eine Verbindung herstellt</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373937(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373937(VS.85).aspx"> https://msdn.microsoft.com/library/aa373937(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>Registrieren der Schnittstelle</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa375357(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa375357(VS.85).aspx"> https://msdn.microsoft.com/library/aa375357(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>Und der Server im Netzwerk verfügbaren</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373974(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373974(VS.85).aspx"> https://msdn.microsoft.com/library/aa373974(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>Registrieren von Endpunkten</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa375255(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa375255(VS.85).aspx"> https://msdn.microsoft.com/library/aa375255(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>Lauschen auf Clientaufrufe</linkText> <linkUri> <a href="https://msdn.microsoft.com/library/aa373966(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373966(VS.85).aspx"> https://msdn.microsoft.com/library/aa373966(VS.85).aspx </a> </linkUri> </externalLink> <externalLink> <linkText>Wie der Client eine Verbindung herstellt</linkText><linkUri><a href="https://msdn.microsoft.com/library/aa373937(VS.85).aspx" data-raw-source="https://msdn.microsoft.com/library/aa373937(VS.85).aspx">https://msdn.microsoft.com/library/aa373937(VS.85).aspx</a></linkUri></externalLink><span class=" class=""></span class="></linkText><linkUri><a href="https://msdn.microsoft.com/library/dd207688(PROT.13).aspx" data-raw-source="https://msdn.microsoft.com/library/dd207688(PROT.13).aspx">https://msdn.microsoft.com/library/dd207688(PROT.13).aspx</a></linkUri></externalLink></relatedTopics>
</developerConceptualDocument>


