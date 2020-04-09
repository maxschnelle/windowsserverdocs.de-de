---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'Replikationsfehler 1396: Anmeldefehler. Der Zielkontoname ist falsch'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: b608066f3fd9d2f6c2bd86194e816f4c9665d6c1
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822073"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>Replikationsfehler 1396: Anmeldefehler. Der Zielkontoname ist falsch

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction>
    <para>In diesem Artikel werden die Symptome, Ursachen und die Behebung Active Directory Replikations Fehlers beschrieben, die mit Win32-Fehler 1396: &quot;Anmeldefehler: der Name des Ziel Kontos ist falsch ist.&quot; </para>
    <list class="bullet"> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">Symptome</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">Bewirkt</link>
        </para>
      </listItem> <listItem>
        <para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">Auflösungen</link>
        </para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>Symptome</title>
    <content>
      <para />
      <list class="ordered">
<listItem><para>Dcdiag meldet, dass der Test für die Active Directory Replikationen mit dem Fehler 1396 fehlgeschlagen ist: Anmeldefehler: der Name des Ziel Kontos ist falsch.&quot;</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN. EXE meldet, dass der letzte Replikations Versuch mit dem Status 1396 fehlgeschlagen ist.</para><para>Repadmin-Befehle, die häufig den 1396-Status angeben, enthalten u. a. die folgenden:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>repadmin/Add</para></listItem><listItem><para>repadmin/REPLSUM</para></listItem><listItem><para>repadmin/REHOST</para></listItem><listItem><para>repadmin/SHOWVECTOR/Latency</para></listItem></list></TD><TD><list class="bullet"><listItem><para>repadmin/SHOWREPS</para></listItem><listItem><para>repadmin/SHOWREPL</para></listItem><listItem><para>repadmin/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>Beispielausgabe von &quot;repadmin/SHOWREPS&quot; die &quot;die eingehende Replikation von "" von "" in "" in "Configuration Manager" darstellt. Im folgenden wird&quot; Fehler angezeigt:</para><code>Default-First-Site-NameCONTOSO-DC1
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
</code></listItem><listItem><para>Der Befehl " <ui>Jetzt replizieren</ui> " in Active Directory Websites und Dienste gibt &quot;Anmeldefehler zurück: der Name des Ziel Kontos ist falsch.&quot;</para><para>Wenn Sie von einem Quell Domänen Controller mit der rechten Maustaste auf das Verbindungs Objekt klicken und <ui>Jetzt replizieren</ui> auswählen, tritt bei &quot;Anmeldefehler ein Fehler auf: der Ziel Konto Name ist falsch&quot; die Bildschirm Fehlermeldung unten angezeigt wird:</para><para>Text des Dialog Titels:</para><para>Jetzt replizieren</para><para>Text der Dialog Meldung: </para><para>Fehler beim Versuch, den namens Kontext &lt;DNS-Partitions Pfad&gt; vom Domänen Controller &lt;Quell Domänen Controller&gt; an den Domänen Controller &lt;Ziel-DC zu synchronisieren&gt;: Anmeldefehler: der Name des Ziel Kontos ist falsch. Dieser Vorgang wird nicht fortgesetzt. </para></listItem><listItem><para>NTDS-KCC-, NTDS-allgemeine oder Microsoft-Windows-ActiveDirectory_DomainService-Ereignisse mit dem Status 1396 werden in der Verzeichnisdienst Anmeldung Ereignisanzeige protokolliert.</para><para>Active Directory Ereignisse, die den 1396-Status häufig erwähnen, sind u. a. die folgenden:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Ereignis-ID</para></TD><TD><para>Ereignisquelle</para></TD><TD><para>Ereignis Zeichenfolge</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Assistent zum Installieren von Active Directory Domain Services (Dcpromo) konnte keine Verbindung mit dem folgenden Domänen Controller herstellen.</para></TD></tr><tr><TD><para>1645</para><para>Dieses Ereignis listet den dreiteiligen SPN auf.</para></TD><TD><para>NTDS-Replikation</para></TD><TD><para>Active Directory hat den authentifizierten Remoteprozeduraufruf (RPC) zu einer anderen Domäne nicht ausgeführt, weil der gewünschte Dienstprinzipalname (SPN) für den Zieldomänencontroller im Schlüsselverteilungscenter (KDC)-Domänencontroller, der zum SPN gehört, nicht registriert ist.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services versuchte, mit dem folgenden globalen Katalog zu kommunizieren, und die Versuche waren nicht erfolgreich.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Konsistenzprüfung hat eine Replikations Verbindung für den lokalen schreibgeschützten Verzeichnisdienst gefunden und versucht, Sie Remote auf der folgenden Verzeichnisdienst Instanz zu aktualisieren. Der Vorgang ist fehlgeschlagen. Der Vorgang wird wiederholt.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS-KCC</para></TD><TD><para>Der Versuch, einen Replikations Link für die folgende beschreibbare Verzeichnis Partition einzurichten, ist fehlgeschlagen.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS-KCC</para></TD><TD><para>Der Versuch, einen Replikations Link mit einer schreibgeschützten Verzeichnis Partition mit den folgenden Parametern zu erstellen, ist fehlgeschlagen.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>Netlogon</para></TD><TD><para> Der Server kann seinen Namen nicht in DNS registrieren.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO schlägt mit einem Bildschirm Fehler fehl</para><para>Text des Dialog Titels:</para><para>Active Directory Installation fehlgeschlagen</para><para>Text der Dialog Meldung:</para><para>Fehler beim Vorgang: Fehler beim Erstellen des Server Objekts für CN = NTDS Settings, CN = serverbeingherauf gestuft, CN = Servers, CN = site, CN = Sites, CN = Configuration, DC = Configuration, DC = com auf Server ReplicationSourceDC.contoso.com. </para><para>Stellen Sie sicher, dass die bereitgestellten Netzwerk Anmelde Informationen über ausreichende Zugriffsrechte für das Hinzufügen eines </para><para>
&quot;Anmeldefehler: der Name des Ziel Kontos ist falsch. &quot;</para><para>In diesem Fall werden die Ereignis-ID 1645, 1168 und 1125 auf dem Server protokolliert, der höher gestuft wird.</para></listItem><listItem><para>Zuordnen eines Laufwerks mithilfe von " <embeddedLabel>net use</embeddedLabel>":</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>In diesem Fall kann der Server auch die Ereignis-ID 333 im System Ereignisprotokoll protokollieren und eine große Menge an virtuellem Arbeitsspeicher für eine Anwendung verwenden, wie z. b. SQL Server.</para></listItem><listItem><para>Die DC-Zeit ist falsch.</para></listItem><listItem><para>Der KDC startet nicht auf einem RODC, nachdem das krbtgt-Konto für den RODC wieder hergestellt wurde, das gelöscht wurde. Nach einer Wiederherstellung wird z. b. Fehler 1396 angezeigt. </para><para>
Die Ereignis-ID 1645 wird auf dem RODC protokolliert. </para><para>
Dcdiag meldet außerdem eine Fehlermeldung, dass das RODC-krbtgt-Konto nicht aktualisiert werden kann. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>Bewirkt</title>
    <content>
      <para />
      <list class="ordered">
        <listItem>
          <para>Der SPN ist nicht im globalen Katalog vorhanden, der vom KDC durchsucht wird, wenn der Client versucht, sich mithilfe von Kerberos zu authentifizieren.</para>
          <para>Im Zusammenhang mit Active Directory Replikation ist der Kerberos-Client der Ziel-DC. der KDC, der die SPN-Suche ausführt, ist wahrscheinlich der Ziel-DC selbst, kann jedoch ein Remote-DC sein.</para>
        </listItem>
        <listItem>
          <para>Das Benutzer-oder Dienst Konto, das den zu suchenden Dienst Prinzipal Namen enthalten soll, ist nicht im globalen Katalog vorhanden, der vom KDC im Auftrag des Zieldomänen Controllers, der die Replikation versucht, durchsucht wurde.</para>
          <para>Im Zusammenhang mit Active Directory Replikation ist das Computer Konto des Quell Domänen Controllers in dem globalen Katalog, der vom Domänen Controller für den Zieldomänen Controller nach der eingehenden Replikation durchsucht wird, nicht vorhanden</para>
        </listItem>
        <listItem>
          <para>Auf dem Ziel-DC fehlt ein LSA-Geheimnis für die Domäne der Quell Domänen Controller.</para>
        </listItem>
        <listItem>
          <para>Der SPN, der gesucht wird, ist auf einem anderen Computer Konto als der Quell Domänen Controller vorhanden.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>Auflösungen</title>
    <content>
      <list class="ordered">
        <listItem>
          <para>Überprüfen Sie das Verzeichnisdienst-Ereignisprotokoll auf dem Ziel-DC für das NTDS-Replikations Ereignis 1645. Beachten Sie Folgendes:</para>
          <para>Der Name des Ziel-DC.</para>
          <para>Der SPN, der gesucht wird (E3514235-4B06-11d1-AB04-00C04FC2DCD2/&lt;Objekt-GUID für Quell Domänen-NTDS-Einstellungs Objekt&gt;/&lt;Zieldomäne&amp;amp; gt;.&amp;amp; lt; TLD&amp;amp; gt; @&lt;Zieldomäne&gt;.&lt;TLD&gt;</para>
          <para>Der vom Ziel-DC verwendete KDC</para>
        </listItem>
        <listItem>
          <para>Geben Sie in der Konsole des KDC, der in Schritt 1 identifiziert wurde, Folgendes ein: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>Führen Sie den NLTEST-Serverlocatorpunkt-Test direkt nach einem Replikations Versuch aus, der mit dem Fehler 1396 auf dem Ziel-DC fehlschlägt. </para>
          <para>Dadurch sollte der GC identifiziert werden, mit dem der KDC SPN-suchen ausführt. </para>
          <para>Der GC, der vom KDC durchsucht wird, kann auch in Microsoft-Windows-ActiveDirectory_DomainService-Ereignis 1655 aufgezeichnet werden.</para>
        </listItem>
        <listItem>
          <para>Suchen Sie nach dem in Schritt 1 ermittelten Dienst Prinzipal Namen im globalen Katalog, der in Schritt 2 erkannt wurde.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:&quot;(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)&quot; /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>OR</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter &quot;(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)&quot; -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>Vergewissern Sie sich, dass das Host Objekt für den SPN vorhanden ist.</para>
          <para>Überprüfen Sie den DN-Pfad für das Host Objekt, z. b., ob das Objekt cnf/Konflikt hat oder sich im verlorenen und gefundenen Container befindet.</para>
          <para>Vergewissern Sie sich, dass die Quell Domänen Controller Active Directory Replikations-SPN nur auf dem Computer Konto der Quell Domänen Controller</para>
          <para>Wenn der Replikations-SPN fehlt, stellen Sie fest, ob der Quell Domänen Controller seinen SPN bei sich selbst registriert hat und ob der SPN auf der vom KDC verwendeten GC aufgrund einer einfachen Replikations Latenz oder eines Replikations Fehlers fehlt.</para>
        </listItem>
        <listItem>
          <para>Überprüfen Sie die Integrität des sicheren Kanals und den Vertrauens Zustand.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics>
    <externalLink> 
      <linkText>Problembehandlung bei Active Directory fehlgeschlagener Vorgänge mit Fehler 1396: Anmeldefehler: der Name des Ziel Kontos ist falsch.</linkText> 
      <linkUri><a href="https://support.microsoft.com/kb/2183411/en-gb" data-raw-source="https://support.microsoft.com/kb/2183411/en-gb">https://support.microsoft.com/kb/2183411/en-gb</a></linkUri> 
    </externalLink>
  </relatedTopics>
</developerConceptualDocument>


