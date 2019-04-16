---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: "Replikationsfehler 1753 es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0e7412f5edc6c206888551fdc250883b5c0ced3e
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>Replikationsfehler 1753 es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>In diesem Thema wird erläutert, Symptome, Ursachen und zum Beheben von Active Directory-Replikation Fehler 8524 der DSA-Vorgang nicht aufgrund einer DNS-Lookup-Problem fortgesetzt wird.</para>
    <list class="bullet">
      <listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Symptoms">Symptome</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Cause">Ursache</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_Resolutions">Auflösungen</link></para></listItem><listItem><para><link xlink:href="f7022f0d-0099-410c-8178-c654e624bc42#BKMK_MoreInfo">Informationen</link></para></listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>Symptome</title>
    <content>
      <para>dieser Artikel beschreibt Symptome, Ursache und Lösungsschritte für Active Directory-Vorgänge, die nicht mit Win32-Fehler 1753: "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung." </para>
      <list class="ordered">
        <listItem>
          <para>DCDIAG-Berichte, die den Test der Netzwerkverbindung, Active Directory-Replikation oder KnowsOfRoleHolders Test mit Fehler 1753 fehlgeschlagen ist: "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung." </para>
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
<listItem><para>REPADMIN. EXE meldet, dass die Replikation mit dem Status 1753 ist fehlgeschlagen ist. </para><para>REPADMIN-Befehle, die den Status 1753 häufig mit enthalten sind aber nicht beschränkt auf:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/replsum</para></listItem><listItem><para>REPADMIN/showrepl</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>repadmin / syncall</para></listItem></list></TD></tr></tbody></table><para>Beispiel für die Ausgabe von "REPADMIN/SHOWREPS" darstellen, wird die eingehender Replikation von CONTOSO-DC2 auf CONTOSO-DC1 fehlerhaften mit dem Fehler "der Replikationszugriff wurde verweigert" unten gezeigt:</para><code>Default-First-Site-NameCONTOSO-DC1
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

</code></listItem><listItem><para>der <ui>Überprüfen der Replikationstopologie</ui> Befehl in Active Directory-Standorte und -Dienste gibt "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung." </para><para>Mit der rechten Maustaste auf das Verbindungsobjekt von einem Quelldomänencontroller aus, und wählen Sie <ui>Überprüfen der Replikationstopologie</ui> schlägt fehl mit "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung." Die auf dem Bildschirm gezeigte Fehlermeldung:</para><para>Dialogfeld Titeltext: Überprüfen der Replikationstopologie</para><para>Dialogfeld Meldungstext: </para><para>Fehler beim Verbinden mit dem Domänencontroller herstellen: sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung. </para></listItem><listItem><para>Der <ui>Jetzt replizieren</ui> Befehl in Active Directory-Standorte und -Dienste gibt "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung." </para><para>Mit der rechten Maustaste auf das Verbindungsobjekt von einem Quelldomänencontroller und auswählen <ui>Jetzt replizieren</ui> schlägt fehl mit "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung." Die auf dem Bildschirm gezeigte Fehlermeldung:</para><para>Dialogfeld Titeltext: Jetzt replizieren</para><para>Dialogfeld Meldungstext: Fehler beim Versuch der namenskontextsynchronisierung &lt;Directory Partition Namen %&gt; vom Domänencontroller &lt;Quelldomänencontroller&gt; Domänencontroller &lt;Ziel DC&gt;:</para><para>

Es sind keine weiteren Endpunkte die endpunktzuordnung verfügbar. </para><para>Der Vorgang wird nicht fortgesetzt</para></listItem><listItem><para>NTDS KCC "," Allgemein "NTDS" bzw. "Microsoft-Windows-ActiveDirectory_DomainService Ereignisse mit dem Status-2146893022 werden in das Verzeichnisdienst-Ereignisprotokoll in der Ereignisanzeige protokolliert. </para><para>Active Directory-Ereignisse, die den Status-2146893022 häufig mit enthalten sind aber nicht beschränkt auf:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Ereignis-ID</para></TD><TD><para>Ereignisquelle</para></TD><TD><para>Ereignis Zeichenfolge</para></TD></tr></thead><tbody><tr><TD><para>1655</para></TD><TD><para>NTDS Allgemein</para></TD><TD><para>Active Directory versucht, die Kommunikation mit den folgenden globalen Katalog, und die Versuche nicht erfolgreich waren.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS-KONSISTENZPRÜFUNG (KCC)</para></TD><TD><para>Fehler beim Herstellen ein Replikationslinks für die folgenden schreibbare Verzeichnispartition.</para></TD></tr><tr><TD><para>1265</para></TD><TD><para>NTDS-KONSISTENZPRÜFUNG (KCC)</para></TD><TD><para>Durch die Konsistenzprüfung (KCC) hinzufügen ein Replikationsvertrags für den folgenden Verzeichnis Partition und die Quelle Domänencontroller ist fehlgeschlagen.</para></TD></tr></tbody></table></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Cause">
    <title>Ursache</title>
    <content>
      <para>das folgende Diagramm zeigt den RPC-Workflow beginnend mit der Registrierung von Server-Anwendung mit RPC Endpoint Mapper (EPM) in Schritt1, das Übergeben von Daten aus der RPC-Client an die Clientanwendung in Schritt7. </para>
      <para>&lt;ADDS_RPCWorkflow&gt;</para>
      <para>Schritte1 bis 7 Karte, um die folgenden Vorgänge:</para>
      <list class="ordered">
        <listItem>
          <para>Server-App registriert die Endpunkte mit RPC Endpoint Mapper (EPM) </para>
        </listItem>
        <listItem>
          <para>Client stellt einen RPC-Aufruf (im Auftrag eines Benutzers Betriebssystem oder eine Anwendung initiiert Vorgang) </para>
        </listItem>
        <listItem>
          <para>Client side RPC-Kontakten den Zielcomputern EPM und fordern Sie den Endpunkt auf den Clientaufruf abgeschlossen </para>
        </listItem>
        <listItem>
          <para>des Servercomputers EPM antwortet mit einem Endpunkt </para>
        </listItem>
        <listItem>
          <para>clientseitig RPC eine Verbindung mit die Server-App </para>
        </listItem>
        <listItem>
          <para>Server-App führt der Aufruf, gibt das Ergebnis an den Client RPC </para>
        </listItem>
        <listItem>
          <para>clientseitig RPC übergibt das Ergebnis an die Client-App</para>
        </listItem>
      </list>
      <para>Fehler 1753 wird durch einen Fehler zwischen den Schritten 3 und 4 # generiert. Konkret bedeutet Fehler 1753, dass der RPC-Client (Ziel-DC) den RPC-Server (Quell-DC) über Port 135 herzustellen konnte, aber die EPM auf dem RPC-Server (Quell-DC) konnte den RPC-Anwendung von Interesse finden und serverseitiger Fehler 1753 zurückgegeben. Das Vorhandensein der 1753 Fehler weist darauf hin, dass der RPC-Client (Ziel-DC) die Antwort des Servers auf Fehler von der RPC-Server (Active Directory-Replikation Quelldomänencontroller) über das Netzwerk empfangen. </para>
      <para>Bestimmten Ursachen für den Fehler 1753 gehören: </para>
      <list class="ordered">
        <listItem>
          <para>der Server-App, die noch nie gestartet (d.h. Schritt1 im Diagramm "Weitere Informationen" oberhalb wurde nie versucht). </para>
        </listItem>
        <listItem>
          <para>Die Server-App gestartet, aber ein Fehler aufgetreten, während der Initialisierung, die verhindert, dass Sie mit der RPC-Endpunktzuordnung (d.h. Schritt1 im obigen Diagramm "Weitere Informationen" war nicht möglich) registrieren. </para>
        </listItem>
        <listItem>
          <para>Der Server-App gestartet, aber nachfolgend wurde unerwartet beendet. (d.h. Schritt1 im obigen Diagramm "Weitere Informationen" wurde erfolgreich abgeschlossen, aber rückgängig gemacht wurde später, da der Server wurde unerwartet beendet). </para>
        </listItem>
        <listItem>
          <para>Die Server-App manuell aufgehoben Endpunkte (vergleichbar mit 3 jedoch beabsichtigt. Nicht wahrscheinlich jedoch Vollständigkeit halber.) </para>
        </listItem>
        <listItem>
          <para>Der RPC-Client (Ziel-DC) kontaktiert, einen anderen RPC-Server als dem vorgesehenen aufgrund einen Namen zu IP-Zuordnungsfehler in DNS, WINS oder Host/Lmhosts-Datei. </para>
        </listItem>
      </list>
      <para>Fehler 1753 beruht nicht: </para>
      <list class="bullet">
        <listItem>
          <para>eine fehlende Netzwerkkonnektivität zwischen dem RPC-Client (Ziel-DC) und RPC-Server (Quell-DC) über Port 135</para>
        </listItem>
        <listItem>
          <para>eine fehlende Netzwerkkonnektivität zwischen dem RPC-Server (Quell-DC) mithilfe von Port 135 und der RPC-Client (Ziel-DC) über die ein kurzlebiger Port. </para>
        </listItem>
        <listItem>
          <para>Kennwörter stimmen nicht oder nicht von der Quell-DC ein Kerberos-verschlüsselte Paket entschlüsseln</para>
        </listItem>
      </list>
      <para></para>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Auflösungen</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>
            <embeddedLabel>überprüfen, die dem Start des Diensts, registrieren den Dienst mit der endpunktzuordnung</embeddedLabel>
          </para>
          <para>für Windows2000 und Windows Server2003-Domänencontrollern: Stellen Sie sicher, dass der Quelldomänencontroller im normalen Modus gestartet wird. </para>
          <para>Für Windows Server2008 oder Windows Server2008 R2: über die Konsole des Quelldomänencontrollers Dienste-Manager (Services.msc) starten, und überprüfen, ob die <embeddedLabel>Active Directory Domain Services</embeddedLabel> -Dienst wird ausgeführt. </para>
        </listItem>
        <listItem>
          <para>
            <embeddedLabel>Überprüfen Sie die RPC-Client (Ziel-DC) mit dem vorgesehenen RPC-Server (Quell-DC) verbunden</embeddedLabel>
          </para>
          <para>alle Domänencontroller in einem allgemeinen Active Directory-Gesamtstruktur Register-ein Domänencontrollers CNAME in die "_msdcs" aufzeichnen. &lt;Gesamtstruktur-Stammdomäne&gt; DNS-Zone, unabhängig davon, welche Domäne sie befinden sich im innerhalb der Gesamtstruktur. Der DC-CNAME-Eintrag stammt aus der <embeddedLabel>"objectGUID"</embeddedLabel> -Attribut des NTDS-Einstellungsobjekts für jeden Domänencontroller. </para>
          <para>Replikation-basierte Vorgängen, fragt ein Zieldomänencontroller DNS für die Quelle DCs CNAME-Eintrag. Der CNAME-Eintrag enthält den Quelldomänencontroller vollqualifizierten Computernamen wird verwendet, um die Quell-Domänencontroller IP-Adresse ableiten über DNS-Client-Cache-Suche, Host / LMHost Datei nachschlagen, Host A / AAAA in DNS oder WINS aufzeichnen. </para>
          <para>Veraltete NTDS-Einstellungsobjekten und ungültige Namen - to-IP Zuordnungen in DNS, WINS, Host und LMHOST Dateien können dazu führen, dass den RPC-Client (Ziel-DC) zur Verbindung mit dem falschen RPC-Server (Quell-DC). Darüber hinaus kann die ungültige Namen - to-IP-Zuordnung dazu führen, dass den RPC-Client (Ziel-DC) eine Verbindung zu einem Computer, die nicht auch der RPC-Server-Anwendung von Interesse sind (in diesem Fall ist dies der Active Directory-Rolle) installiert. (Beispiel: ein veraltete Hosteintrag für DC2 enthält die IP-Adresse DC3 oder ein Mitgliedscomputer). </para>
          <para>Überprüfen, die die Objekt-GUID für den Quelldomänencontroller, die am Zielort DCs Kopie der Active Directory vorhanden ist, die Quell-DC "objectGUID" in der Quelle DCs Kopie von Active Directory gespeichert entspricht. Wenn Widersprüche, mithilfe von Repadmin /showobjmeta auf der Ntds-Einstellungsobjekt, um festzustellen, welches letzten Förderung der Quelldomänencontroller entspricht (Hinweis: Datumsstempel vergleichen, für das NTDS-Einstellungsobjekt erstellen Datum aus /showobjmeta gegen das Datum der letzten Aktion in der Quelldatei für Domänencontroller dcpromo.log. Sie müssen möglicherweise verwenden das Letzte ändern / Datum der DCPROMO.LOG selbst). Wenn die Objekt-GUIDs nicht identisch sind, hat der Zieldomänencontroller wahrscheinlich eine veraltete NTDS-Einstellungsobjekt für den Quelldomänencontroller, deren CNAME-Eintrag auf einen Hosteintrag mit einem ungültigen Namen für die IP-Zuordnung bezieht sich. </para>
          <para>Führen Sie auf dem Zieldomänencontroller IPCONFIG//ALL, um zu ermitteln, welcher DNS-Server der Zieldomänencontroller ist für die Auflösung name:</para>
          <code>c:&gt;ipconfig /all</code>
          <para>führen Sie auf dem Zieldomänencontroller NSLOOKUP für die Quelle DCs vollqualifizierten DC-CNAME-Eintrag:</para>
          <code>c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs primary DNS Server IP &gt;
c:&gt;nslookup -type=cname &lt;fully qualified cname of source DC&gt; &lt;destination DCs secondary DNS Server IP&gt;</code>
          <para>stellen Sie sicher, dass die IP-Adresse zurückgegeben wird, indem NSLOOKUP den Hostnamen "besitzt" / Sicherheits-ID des Quelldomänencontrollers:</para>

          <code>C:&gt;NBTSTAT -A &lt;IP address returned by NSLOOKUP in the step above&gt;</code>
          <para>oder</para>
          <para>melden Sie sich an der Konsole des Quelldomänencontrollers, führen Sie "IPCONFIG" über die CMD-Eingabeaufforderung, und stellen Sie sicher, dass der Quelldomänencontroller die oben genannten Befehl NSLOOKUP zurückgegebene IP-Adresse besitzt</para>
          <para>prüfen, ob veraltete / doppelte IP-Zuordnungen im DNS-Host</para>
          <code>NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;single label hostname of source DC&gt; &lt;secondary DNS Server IP on destination DC&gt;

NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;primary DNS Server IP on destination DC&gt;
NSLOOKUP -type=hostname &lt;fully qualified computer name of source DC&gt; &lt;secondary DNS Server IP on dest. DC&gt;</code>
<para>ungültige IP-Adressen im Hosteinträge vorhanden, überprüfen Sie, ob DNS-Aufräumvorgänge aktiviert und richtig konfiguriert ist. </para><para>Wenn die oben genannten Tests oder eine netzwerkablaufverfolgung eine Namensabfrage Rückgabe eine ungültige IP-Adresse angezeigt wird, sollten Sie veraltete Einträge im HOST-Dateien, LMHOSTS-Dateien und WINS-Server. Beachten Sie, dass DNS-Server auch konfiguriert werden können, um alternative WINS-Auflösung auszuführen. </para>
</listItem>
        <listItem>
          <para>
            <embeddedLabel>Überprüfen, die die Server-Anwendung (Active Directory Befehlsshell und mehr) mit der endpunktzuordnung auf dem RPC-Server (Quell-DC) registriert hat</embeddedLabel>
          </para>
          <para>Active Directory verwendet eine Kombination aus bekannten und dynamisch registrierten Ports. Diese Tabelle enthält die bekannten Ports und Protokolle, die von Active Directory-Domänencontroller verwendet.</para>
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
                  <para>LDAP-Server</para>
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
                  <para>Globale Katalogserver</para>
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
                  <para>Globale Katalogserver</para>
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
          <para>Bekannte Ports sind nicht mit der endpunktzuordnung registriert. </para>
          <para>Active Directory und andere Anwendungen auch Dienste, die dynamisch zugewiesenen Ports in der temporäre Portbereich RPC empfangen registrieren. Diese RPC-Server-Anwendungen werden TCP-Ports zwischen 1024 und 5000 auf Windows2000 und Windows Server2003-Computern und Ports zwischen 49152 und 65535 Reichweite auf Windows Server2008 und Windows Server2008 R2-Computern dynamisch zugewiesen. Von der Replikation verwendet der RPC-Port kann in der Registrierung mithilfe der dokumentierten Schrittewerden hartcodierte <externalLink><linkText>KB-Artikel 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink>. Active Directory wird weiterhin mit der EPM konfiguriert einen hartcodierten Anschluss registrieren. </para>
          <para>Stellen Sie sicher, dass die RPC-Server-Anwendung von Interesse sind mit der RPC-endpunktzuordnung auf dem RPC-Server (der Quelldomänencontroller im Fall von Active Directory-Replikation) registriert hat. </para>
          <para>Es gibt eine Reihe von Methoden, um diese Aufgabe jedoch eine ist zum Installieren und Ausführen von PORTQRY aus einer privilegierten Admin CMD-Eingabeaufforderung auf der Konsole des Quelldomänencontrollers mithilfe der Syntax: </para>
          <code>c:\&gt;portquery -n &lt;source DC&gt; -e 135 &gt;file.txt</code>
          <para>In der Ausgabe Portqry Beachten Sie die Portnummern dynamisch registriert, indem die "MS NT Directory DRS Interface" (UUID = 351...) für die <embeddedLabel>Ncacn_ip_tcp Protokoll</embeddedLabel>. Der folgende Codeausschnitt zeigt eine Beispielausgabe für Portquery aus einem Windows Server2008 R2-Domänencontroller und der UUID / Protokoll-Paar speziell von Active Directory verwendet hervorgehoben <embeddedLabel>fett</embeddedLabel>: </para>
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
          <para>andere Methoden für diesen Fehler zu beheben:</para>
          <list class="ordered">
            <listItem>
              <para>stellen Sie sicher, dass der Quelldomänencontroller im normalen Modus gestartet wird und die Betriebssystem- und DC-Rolle auf dem Quelldomänencontroller vollständig gestartet haben. </para>
            </listItem>
            <listItem>
              <para>Überprüfen, die Active Directory-Domänendienste ausgeführt wird. Wenn der Dienst beendet wurde oder nicht mit standardmäßigen Systemstart Werten konfiguriert wurde, die Start-Standardwerte zurückgesetzt, starten Sie den geänderten Domänencontroller neu, und wiederholen Sie den Vorgang. </para>
            </listItem>
            <listItem>
              <para>Überprüfen Sie der Startstatus Wert und -Diensts für RPC-Dienst und RPC-Locator für die Betriebssystemversion des RPC-Clients (Ziel-DC) und der RPC-Server (Quell-DC). Wenn der Dienst beendet wurde oder nicht mit standardmäßigen Systemstart Werten konfiguriert wurde, die Start-Standardwerte zurückgesetzt, starten Sie den geänderten Domänencontroller neu, und wiederholen Sie den Vorgang. </para>
              <para>Darüber hinaus stellen Sie sicher, dass die Dienstkontext in der folgenden Tabelle aufgeführte Standardeinstellungen übereinstimmt.</para>
              <table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11">
                <thead>
                  <tr>
                    <TD>
                      <para>Dienst</para>
                    </TD>
                    <TD>
                      <para>Standardstatus (Starttyp) in Windows Server2003 und höher </para>
                    </TD>
                    <TD>
                      <para>Standardstatus (Starttyp) in Windows Server2000</para>
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
                      <para>Remote Procedure Call Locator</para>
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
              <para>Stellen Sie sicher, dass die Größe der dynamischen Portbereich nicht eingeschränkt. Windows Server2008 und Windows Server2008 R2 NETSH Syntax zum Auflisten des RPC-Portbereich wird unten gezeigt:</para>
              <code>&gt;netsh int ipv4 show dynamicport tcp
&gt;netsh int ipv4 show dynamicport udp
&gt;netsh int ipv6 show dynamicport tcp
&gt;netsh int ipv6 show dynamicport udp</code>
            </listItem>
            <listItem>
              <para>überprüfen, ob die dynamischen Portbereich für Quelle DCs Betriebssystemversion hartcodierte Port Definitionen in KB 224196 definierten fallen. </para>
              <para>Überprüfung <externalLink><linkText>KB-Artikel 224196</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink> und stellen Sie sicher, dass die hartcodierte Port in der temporäre Portbereich für die Betriebssystemversion der Quelldomänencontroller fällt. </para>
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
        <embeddedLabel>Beispiel für einen ungültigen Namen zu IP-Zuordnung verursacht RPC-Fehlers 1753 im Vergleich zu-2146893022: der Zielprinzipalname ist falsch</embeddedLabel>
      </para>
      <para>besteht aus die Domäne contoso.com DC1 und DC2 mit IP-Adressen x.x.1.1 und x.x.1.2. Der Host "A" / "AAAA"-Einträge für DC2 korrekt auf allen für DC1 konfigurierten DNS-Servern registriert sind. Darüber hinaus enthält die Hostdatei auf DC1 einen Eintrag, der IP-Adresse x.x.1.2 DC2s vollqualifizierter Hostname zuordnen. Später wird DC2s IP-Adresse ändert sich von X.X.1.2 X.X.1.3 und einen neuen Computer als Mitglied der Domäne mit IP-Adresse x.x.1.2 verbunden. Active Directory-Replikation versucht ausgelöst wird, indem Sie die <ui>Jetzt replizieren</ui> Befehl im Active Directory-Standorte und -Dienste-Snap-In tritt der Fehler 1753 wie in der Ablaufverfolgung unten dargestellt:</para>
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
      <para>Frame <embeddedLabel>10</embeddedLabel>, der Zieldomänencontroller fragt die Quelle DCs endpunktzuordnung über Port 135 für die Active Directory-Replikation-Dienstklasse UUID E351... </para>
      <para>Im Frame <embeddedLabel>11</embeddedLabel>, der Quelldomänencontroller, in diesem Fall einen Mitgliedscomputer, der die Domänencontrollerrolle ist noch kein Host und der E351 wurde nicht registriert... UUID für den Replikationsdienst seine lokale EPM antwortet mit symbolischen Fehler EP_S_NOT_REGISTERED zuordnet Dezimal Fehler 1753, hex Fehler 0x6d9 wird angezeigt und angezeigte Fehler "Es sind keine weiteren Endpunkte verfügbar, die endpunktzuordnung". </para>
      <para>Später die Mitgliedscomputer mit IP-Adresse x.x.1.2 als Replikat "MayberryDC" in der Domäne contoso.com heraufgestuft wird. In diesem Fall die <ui>Jetzt replizieren</ui> Befehl dient zum Auslösen der Replikation, aber dieses Mal ein Fehler auftritt, mit der auf dem Bildschirm Fehler "der Zielprinzipalname ist falsch." Des Computers, dessen Netzwerkadapter zugewiesen ist die IP-Adresse x.x.1.2 <placeholder>ist</placeholder> ein Domänencontroller wird derzeit im normalen Modus gestartet und die E351... registriert wurde Replikationsdienst UUID mit den lokalen EPM, aber es ist nicht im Besitz der Name oder die Sicherheits-Identität von DC2 und die Kerberos-Anfrage von DC1 nicht entschlüsselt werden, damit die Anforderung schlägt mit Fehler "der Zielprinzipalname ist falsch." Der Fehler ist dezimal Fehler-2146893022 / hex-Fehler 0x80090322. </para>
      <para>Konnte eine solche ungültige Host - to-IP Zuordnungen veraltete Einträge im Host zurückzuführen sein / Lmhost-Dateien, Host A / AAAA-Registrierungen in DNS oder WINS. </para>
      <para>Zusammenfassung: in diesem Beispiel wird eine ungültige Host - to-IP-Zuordnung (in der HOST-Datei in diesem Fall) verursacht den Zieldomänencontroller beheben eine "Quelle"-Domänencontroller, der nicht über die Active Directory-Domänendienste verfügt-Dienst wird ausgeführt (oder sogar darum installiert) daher die Replikation SPN wurde noch nicht registriert und der Quelldomänencontroller Fehler 1753 fehlgeschlagen. Im zweiten Fall verursacht eine ungültige Host - to-IP-Zuordnung (erneut in die HOST-Datei) der Zieldomänencontroller, eine Verbindung mit einem Domänencontroller, die die E351 registriert hatten... Replikations-SPN, aber dieser Quelle eine andere Identität Hostname und Sicherheit als der vorgesehenen Quelldomänencontroller hatten, damit der fehlgeschlagenen mit Fehler-2146893022: der Zielprinzipalname ist falsch.</para>
    </content>
  </section>
  <relatedTopics>
    <externalLink>
      <linkText>Problembehandlung bei Active Directory-Vorgänge, die nicht mit dem Fehler 1753: Es gibt keine weiteren Endpunkte verfügbar, die endpunktzuordnung. </linkText>
      <linkUri>https://support.microsoft.com/kb/2089874</linkUri>
    </externalLink>
<externalLink><linkText>KB-Artikel 839880 Problembehandlung bei RPC-Endpunktzuordnung Fehler bei der Verwendung der Windows Server2003-Supporttools von der Produkt-CD</linkText><linkUri>https://support.microsoft.com/kb/839880</linkUri></externalLink>
<externalLink><linkText>KB-Artikel 832017 (Übersicht) und Netzwerk portanforderungen für das Windows Server-System</linkText><linkUri>https://support.microsoft.com/kb/832017/</linkUri></externalLink>
<externalLink><linkText>KB-Artikel 224196 Einschränken des Active Directory-Replikations-Datenverkehr und Client-RPC-Datenverkehr an einen bestimmten Port</linkText><linkUri>https://support.microsoft.com/kb/224196/</linkUri></externalLink>
<externalLink><linkText>KB-Artikel 154596 Vorgehensweise beim Konfigurieren der dynamischen RPC-portzuweisung funktionieren mit Firewalls</linkText><linkUri>https://support.microsoft.com/kb/154596</linkUri></externalLink><externalLink><linkText>Funktionsweise von RPC-</linkText><linkUri>https://msdn.microsoft.com/library/aa373935(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Wie der Server vorbereitet für eine Verbindung</linkText><linkUri>https://msdn.microsoft.com/library/aa373938(VS.85).aspx</linkUri></externalLink>
<externalLink><linkText>wie der Client eine Verbindung herstellt</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Registrieren der Schnittstelle</linkText><linkUri>https://msdn.microsoft.com/library/aa375357(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Verfügbarmachen der Server im Netzwerk</linkText><linkUri>https://msdn.microsoft.com/library/aa373974(VS.85).aspx</linkUri></externalLink><externalLink><linkText>registrieren Endpunkte</linkText><linkUri>https://msdn.microsoft.com/library/aa375255(VS.85).aspx</linkUri></externalLink><externalLink><linkText>Clientaufrufe Lauschen</linkText><linkUri>https://msdn.microsoft.com/library/aa373966(VS.85).aspx</linkUri></externalLink><externalLink><linkText>wie der Client eine Verbindung herstellt</linkText><linkUri>https://msdn.microsoft.com/library/aa373937(VS.85).aspx</linkUri></externalLink><externalLink><linkText> Einschränken von Active Directory Replikationsdatenverkehr und RPC-Client Datenverkehr an einen bestimmten Port</linkText><linkUri>https://support.microsoft.com/kb/224196</linkUri></externalLink><externalLink><linkText>SPN für eine Ziel-DC in AD DS</linkText><linkUri>https://msdn.microsoft.com/library/dd207688(PROT.13).aspx</linkUri></externalLink></relatedTopics>
</developerConceptualDocument>


