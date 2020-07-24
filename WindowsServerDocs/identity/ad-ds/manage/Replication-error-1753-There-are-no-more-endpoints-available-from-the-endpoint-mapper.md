---
ms.assetid: 0f21951c-b1bf-43bb-a329-bbb40c58c876
title: 'Replikationsfehler 1753: Die Endpunktzuordnung hat keine weiteren Endpunkte verfügbar'
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ca7ab368c9e15de15f733070a5bcb06584956500
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961132"
---
# <a name="replication-error-1753-there-are-no-more-endpoints-available-from-the-endpoint-mapper"></a>Replikationsfehler 1753: Die Endpunktzuordnung hat keine weiteren Endpunkte verfügbar

>Gilt für: Windows Server

In diesem Artikel werden Symptome, Ursachen und Lösungsschritte für Active Directory Vorgänge beschrieben, die mit dem Win32-Fehler 1753 fehlschlagen: "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar."

Dcdiag meldet, dass der Konnektivitätstest, Active Directory Replikationen oder der KnowsOfRoleHolders-Test fehlgeschlagen ist. Fehler 1753: "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar."

```
Testing server: <site><DC Name>
Starting test: Connectivity
* Active Directory LDAP Services Check
* Active Directory RPC Services Check
[<DC Name>] DsBindWithSpnEx() failed with error 1753,
There are no more endpoints available from the endpoint mapper..
Printing RPC Extended Error Info:
Error Record 1, ProcessID is <process ID> (DcDiag)
System Time is: <date> <time>
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper. Detection location is 500
NumberOfParameters is 4
Unicode string: ncacn_ip_tcp
Unicode string: <source DC object GUID>._msdcs.contoso.com
Long val: -481213899
Long val: 65537
Error Record 2, ProcessID is 700 (DcDiag)
System Time is: <date> <time>
Generating component is 2 (RPC runtime)
Status is 1753: There are no more endpoints available from the endpoint mapper.
NumberOfParameters is 1
Unicode string: 1025
[Replications Check,<DC Name>] A recent replication attempt failed:
From <source DC> to <destination DC>
Naming Context: <DN path of directory partition>
The replication generated an error (1753):
There are no more endpoints available from the endpoint mapper.
The failure occurred at <date> <time>.
The last success occurred at <date> <time>.
3 failures have occurred since the last success.
The directory on <DC name> is in the process.
of starting up or shutting down, and is not available.
Verify machine is not hung during boot.
```

REPADMIN.EXE meldet, dass der Replikations Versuch mit Status 1753 fehlgeschlagen ist.
Repadmin-Befehle, die häufig den 1753-Status angeben, enthalten u. a. die folgenden:

* repadmin/REPLSUM
* repadmin/SHOWREPL
* repadmin/SHOWREPS
* repadmin/SYNCALL

Die Beispielausgabe von "repadmin/SHOWREPS", die die eingehende Replikation von "Configuration Manager" zu "" darstellt, wird nachstehend angezeigt:

```
Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ <date> <time> failed, result 1753 (0x6d9):
There are no more endpoints available from the endpoint mapper.
<#> consecutive failure(s).
Last success @ <date> <time>.
```

Der Befehl **Replikations Topologie überprüfen** in Active Directory Sites und Dienste gibt an, dass keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar sind.

Wenn Sie von einem Quell Domänen Controller mit der rechten Maustaste auf das Verbindungs Objekt klicken und **Replikations Topologie überprüfen** auswählen, tritt ein Fehler auf, weil keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar sind. Die Bildschirm Fehlermeldung wird unten angezeigt:

Dialogfeld Titeltext: Dialogfeld Meldungs Text der Replikations Topologie überprüfen: beim Versuch, eine Verbindung mit dem Domänen Controller aufzunehmen, ist folgender Fehler aufgetreten: Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar.

Der Befehl " **Jetzt replizieren** " in Active Directory Sites und Dienste gibt "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar".
Wenn Sie von einem Quell Domänen Controller mit der rechten Maustaste auf das Verbindungs Objekt klicken und **Jetzt replizieren** auswählen, tritt ein Fehler mit der Option "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar".
Die Bildschirm Fehlermeldung wird unten angezeigt:

Dialogfeld Titel Text: Dialog Meldungs Text replizieren: der folgende Fehler ist beim Versuch aufgetreten, den namens Kontext \<%directory partition name%> vom Domänen Controller \<Source DC> mit dem Domänen Controller zu synchronisieren \<Destination DC> :

Es sind keine Endpunkte mehr von der Endpunktzuordnung verfügbar.
Der Vorgang wird nicht fortgesetzt.

NTDS-KCC-, NTDS-allgemeine oder Microsoft-Windows-ActiveDirectory_DomainService-Ereignisse mit dem Status-2146893022 werden in der Verzeichnisdienst Anmeldung Ereignisanzeige protokolliert.

Active Directory Ereignisse, die den Status "-2146893022" häufig erwähnen, sind u. a. die folgenden:

| Ereignis-ID | Ereignisquelle | Ereignis Zeichenfolge|
| --- | --- | --- |
| 1655 | NTDS allgemein | Active Directory versuchte, mit dem folgenden globalen Katalog zu kommunizieren, und die Versuche waren nicht erfolgreich. |
| 1925 | NTDS-KCC | Der Versuch, einen Replikations Link für die folgende beschreibbare Verzeichnis Partition einzurichten, ist fehlgeschlagen. |
| 1265 | NTDS-KCC | Ein Versuch der Konsistenzprüfung (KCC) zum Hinzufügen eines Replikations Vertrags für die folgende Verzeichnis Partition und den Quell Domänen Controller ist fehlgeschlagen. |

## <a name="cause"></a>Ursache

Die folgenden Schritte zeigen den RPC-Workflow, beginnend mit der Registrierung der Serveranwendung bei der RPC Endpoint Mapper (EPM) in Schritt 1 zum Übergeben von Daten vom RPC-Client an die Client Anwendung in Schritt 7.

### <a name="adds-rpc-workflow"></a>Fügt den RPC-Workflow

1. Die Server-App registriert Ihre Endpunkte beim RPC-Endpunkt Mapper (EPM).
1. Der Client sendet einen RPC-Aufruf (im Auftrag eines Benutzer-, Betriebssystem-oder Anwendungs initiierten Vorgangs).
1. Client seitiges RPC kontaktiert die Zielcomputer (EPM) und fordert den Endpunkt auf, den Client Aufruf abzuschließen.
1. Das EPM des Server Computers antwortet mit einem Endpunkt.
1. Client seitiges RPC kontaktiert die Server-App
1. Die Server-App führt den Aufruf aus und gibt das Ergebnis an den Client-RPC zurück.
1. Client seitiges RPC übergibt das Ergebnis an die Client-App zurück.

Der Fehler 1753 wird durch einen Fehler zwischen den Schritten #3 und #4 generiert. Insbesondere bedeutet der Fehler 1753, dass der RPC-Client (Ziel-DC) den RPC-Server (Quell Domänen Controller) über Port 135 kontaktieren konnte, aber der EPM auf dem RPC-Server (Quell Domänen Controller) die gewünschte RPC-Anwendung nicht finden konnte und den Server seitigen Fehler 1753 zurückgegeben hat. Das vorhanden sein des Fehlers 1753 zeigt an, dass der RPC-Client (Ziel-DC) die serverseitige Fehler Antwort vom RPC-Server (AD Replication Source DC) über das Netzwerk erhalten hat.

Zu den spezifischen Ursachen für den 1753-Fehler zählen folgende:

* Die Server-App wurde nie gestartet (d. h. Schritt #1 im obigen Diagramm "Weitere Informationen" wurde nie versucht).
* Die Server-App wurde gestartet, aber während der Initialisierung ist ein Fehler aufgetreten, der die Registrierung beim RPC-Endpunkt-Mapper verhindert hat (d. h., der Schritt #1 im obigen Diagramm "Weitere Informationen" wurde versucht, aber nicht ausgeführt).
* Die Server-App wurde gestartet, wurde aber anschließend beendet. (Dies bedeutet, dass Schritt #1 im obigen Diagramm "Weitere Informationen" erfolgreich abgeschlossen wurde, aber später rückgängig gemacht wurde, weil der Server ausgefallen ist.)
* Die Server-APP hat die Registrierung Ihrer Endpunkte (ähnlich wie 3, beabsichtigt) manuell aufgehoben. Nicht wahrscheinlich, aber aus Gründen der Vollständigkeit eingeschlossen.)
* Der RPC-Client (Ziel-DC) hat eine Verbindung mit einem anderen RPC-Server als beabsichtigt hergestellt, weil in der DNS-, WINS-oder Host/LMHOSTS-Datei der Name der IP-Zuordnung aufgetreten ist.

Der Fehler 1753 wird nicht durch Folgendes verursacht:

* Fehlende Netzwerk Konnektivität zwischen dem RPC-Client (Ziel-DC) und dem RPC-Server (Quell Domänen Controller) über Port 135
* Fehlende Netzwerk Konnektivität zwischen dem RPC-Server (Quell Domänen Controller) mit Port 135 und dem RPC-Client (Ziel-DC) über den kurzlebigen Port.
* Ein Kennwort stimmt nicht überein, oder der Quell Domänen Controller konnte ein Kerberos-verschlüsseltes Paket nicht entschlüsseln.

## <a name="resolutions"></a>Lösungen

Überprüfen Sie, ob der Dienst, der seinen Dienst bei der Endpunkt Zuordnung registriert, gestartet wurde.

* Für Windows 2000 und Windows Server 2003 DCS: Stellen Sie sicher, dass der Quell-DC im normalen Modus gestartet wird.
* Für Windows Server 2008 oder Windows Server 2008 R2: Starten Sie in der-Konsole des Quell Domänen Controllers den Dienst-Manager (Services. msc), und überprüfen Sie, ob der Active Directory Domain Services-Dienst ausgeführt wird.

Überprüfen, ob der RPC-Client (Ziel-DC) mit dem gewünschten RPC-Server (Quell Domänen Controller)

Alle DCS in einer allgemeinen Active Directory Gesamtstruktur registrieren einen Domänen Controller-CNAME-Datensatz im _msdcs. \<forest root domain>DNS-Zone unabhängig davon, in welcher Domäne Sie sich innerhalb der Gesamtstruktur befinden. Der DC CNAME-Datensatz wird vom objectGUID-Attribut des NTDS-Einstellungs Objekts für jeden Domänen Controller abgeleitet.

Beim Ausführen von Replikations basierten Vorgängen fragt ein Ziel-DC DNS nach dem CNAME-Datensatz des Quell-DCS ab. Der CNAME-Datensatz enthält den voll qualifizierten Domänen Namen des Quell Domänen Controllers, der verwendet wird, um die IP-Adresse des Quell Domänen Controllers über DNS-Client Cache Suche, Host/Lmhost-Dateisuche, Host A/AAAA-Datensatz in DNS oder WINS zu ableiten.

Veraltete NTDS-Einstellungs Objekte und ungültige namens-zu-IP-Zuordnungen in DNS-, WINS-, Host-und Lmhost-Dateien können bewirken, dass der RPC-Client (Ziel-DC) eine Verbindung mit dem falschen RPC-Server (Quell-DC) herstellt Darüber hinaus kann die Zuordnung von "fehlerhafter Name zu IP" dazu führen, dass der RPC-Client (Ziel-DC) eine Verbindung mit einem Computer herstellt, auf dem nicht einmal die von Interesse ist (in diesem Fall die Active Directory Rolle). (Beispiel: ein veralteter Host Daten Satz für DC2 enthält die IP-Adresse von DC3 oder eines Mitglieds Computers).

Vergewissern Sie sich, dass die objectGUID für den Quell Domänen Controller, der in der Ziel-DCS-Kopie von Active Directory vorhanden ist, der Quell-DC-objectGUID entspricht, die in der Quell-DCS-Active Directory Kopie Wenn eine Abweichung vorliegt, verwenden Sie Repadmin/showobjmeta für das NTDS-Einstellungs Objekt, um festzustellen, welcher Wert der letzten herauf Stufung des Quell Domänen Controllers entspricht (Hinweis: Vergleichen von Datumsstempeln für das NTDS-Einstellungs Objekt Create Date from/showobjmeta mit dem Datum der letzten herauf Stufung in der Quelldatei DCS Dcpromo. log. Möglicherweise müssen Sie das Datum der letzten Änderung/Erstellung der Dcpromo-Datei verwenden. Protokolldatei selbst). Wenn die Objekt-GUIDs nicht identisch sind, verfügt der Ziel-DC wahrscheinlich über ein veraltetes NTDS-Einstellungs Objekt für den Quell Domänen Controller, dessen CNAME-Datensatz auf einen Host Daten Satz mit einem ungültigen Namen für die IP-Zuordnung verweist.

Führen Sie auf dem Ziel-DC ipconfig/all aus, um zu ermitteln, welche DNS-Server der Ziel-DC für die Namensauflösung verwendet:

```
c:>ipconfig /all
```

Führen Sie auf dem Ziel-DC nslookup für den voll qualifizierten Domänen Controller-CNAME-Datensatz für den Quellcode aus:

```
c:>nslookup -type=cname <fully qualified cname of source DC> <destination DCs primary DNS Server IP >
c:>nslookup -type=cname <fully qualified cname of source DC> <destination DCs secondary DNS Server IP>
```

Vergewissern Sie sich, dass die von nslookup zurückgegebene IP-Adresse den Hostnamen bzw. die Sicherheitsidentität des Quell Domänen Controllers "besitzt":

```
C:>NBTSTAT -A <IP address returned by NSLOOKUP in the step above>
```

Melden Sie sich bei der Konsole des Quell Domänen Controllers an, führen Sie "ipconfig" an der Eingabeaufforderung aus, und überprüfen Sie, ob der Quell Domänen Controller die IP-Adresse besitzt, die vom Befehl "nslookup

Überprüfen Sie, ob Host-zu-IP-Zuordnungen in DNS vorhanden sind

```
NSLOOKUP -type=hostname <single label hostname of source DC> <primary DNS Server IP on destination DC>
NSLOOKUP -type=hostname <single label hostname of source DC> <secondary DNS Server IP on destination DC>

NSLOOKUP -type=hostname <fully qualified computer name of source DC> <primary DNS Server IP on destination DC>
NSLOOKUP -type=hostname <fully qualified computer name of source DC> <secondary DNS Server IP on dest. DC>
```

Wenn in Host Einträgen ungültige IP-Adressen vorhanden sind, überprüfen Sie, ob das DNS-Bereinigung aktiviert und ordnungsgemäß konfiguriert ist

Wenn die Tests oben oder eine Netzwerk Ablauf Verfolgung keine Namensabfrage anzeigt, die eine ungültige IP-Adresse zurückgibt, sollten Sie veraltete Einträge in Host Dateien, LMHOSTS-Dateien und WINS-Servern in Erwägung gezogen. Beachten Sie, dass DNS-Server auch für die Ausführung der WINS-Fall Back Namen Auflösung konfiguriert werden können.

* Überprüfen Sie, ob die Serveranwendung (Active Directory et al) bei der Endpunkt Zuordnung auf dem RPC-Server (Quell-DC) registriert ist.
* Active Directory verwendet eine Kombination aus bekannten und dynamisch registrierten Ports. In dieser Tabelle werden bekannte Ports und Protokolle aufgelistet, die von Active Directory Domänen Controllern verwendet werden.

| RPC-Server Anwendung | Port | TCP | UDP |
| --- | --- | --- | --- |
| DNS-Server | 53 | X | X |
| Kerberos | 88 | X | X |
| LDAP-Server | 389 | X | X |
| Microsoft-DS | 445 | X | X |
| LDAP SSL | 636 | X | X |
| Globaler Katalogserver | 3268 | X |   |
| Globaler Katalogserver | 3269 | X |   |

Bekannte Ports sind nicht bei der Endpunkt Zuordnung registriert.

Active Directory und andere Anwendungen registrieren auch Dienste, die dynamisch zugewiesene Ports im kurzlebigen RPC-Port Bereich empfangen. Diese RPC-Server Anwendungen werden dynamisch TCP-Ports zwischen 1024 und 5000 auf Windows 2000-und Windows Server 2003-Computern und Ports zwischen dem 49152-und 65535-Bereich auf Windows Server 2008-und Windows Server 2008 R2-Computern zugewiesen. Der von der Replikation verwendete RPC-Port kann in der Registrierung hart codiert werden, indem Sie die im [KB-Artikel 224196](https://support.microsoft.com/kb/224196)beschriebenen Schritte ausführen. Active Directory wird weiterhin beim EPM registriert, wenn es für die Verwendung eines hart codierten Ports konfiguriert ist.

Stellen Sie sicher, dass sich die zu berücksichtigende RPC-Serveranwendung bei der RPC-Endpunkt Zuordnung auf dem RPC-Server (dem Quell Domänen Controller bei der AD-Replikation) registriert hat.

Es gibt eine Reihe von Möglichkeiten, diese Aufgabe zu erledigen, aber eine ist die Installation und Ausführung von Portqry über eine Eingabeaufforderung für Administratorrechte in der Konsole des Quell Domänen Controllers mit der folgenden Syntax:

```
portquery -n <source DC> -e 135 > file.txt
```

Beachten Sie in der PortQry-Ausgabe die Portnummern, die von der "MS NT Directory DRS Interface" (UUID = 351...) für das ncacn_ip_tcp Protokoll dynamisch registriert werden. Der folgende Code Ausschnitt zeigt eine Beispiel-PortQuery-Ausgabe eines Windows Server 2008 R2-DC:

```
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\pipe\lsass] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_np:CONTOSO-DC01[\PIPE\protected_storage] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_ip_tcp:CONTOSO-DC01[49156] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[49157] 
UUID: e3514235-4b06-11d1-ab04-00c04fc2dcd2 MS NT Directory DRS Interface
ncacn_http:CONTOSO-DC01[6004]
```

Weitere Möglichkeiten, diesen Fehler zu beheben:

* Vergewissern Sie sich, dass der Quell Domänen Controller im normalen Modus gestartet wurde und dass das Betriebssystem und die DC-Rolle auf dem Quell Domänen Controller vollständig gestartet wurden
* Überprüfen Sie, ob der Active Directory-Domäne-Dienst ausgeführt wird. Wenn der Dienst derzeit beendet oder nicht mit Standard Startwerten konfiguriert wurde, setzen Sie die Standard Startwerte zurück, starten Sie den geänderten Domänen Controller neu, und wiederholen Sie dann den Vorgang.
* Überprüfen Sie, ob der Starttyp und der Dienststatus für den RPC-Dienst und den RPC-Locator für die Betriebssystemversion des RPC-Clients (Ziel-DC) und des RPC-Servers (Quell Domänen Wenn der Dienst derzeit beendet oder nicht mit Standard Startwerten konfiguriert wurde, setzen Sie die Standard Startwerte zurück, starten Sie den geänderten Domänen Controller neu, und wiederholen Sie dann den Vorgang.
   * Stellen Sie außerdem sicher, dass der Dienst Kontext mit den in der folgenden Tabelle aufgeführten Standardeinstellungen übereinstimmt.

      | Dienst | Standardstatus (Starttyp) in Windows Server 2003 und höher | Standardstatus (Starttyp) in Windows Server 2000 |
      | --- | --- | --- |
      | Remoteprozeduraufruf | Gestartet (automatisch) | Gestartet (automatisch) |
      | Locator für Remote Prozedur Aufrufe | NULL oder beendet (manuell) | Gestartet (automatisch) |

* Vergewissern Sie sich, dass die Größe des dynamischen Port Bereichs nicht eingeschränkt wurde. Die Syntax von Windows Server 2008 und Windows Server 2008 R2 netsh zum Auflisten des RPC-Port Bereichs ist unten dargestellt:

   ```
   netsh int ipv4 show dynamicport tcp
   netsh int ipv4 show dynamicport udp
   netsh int ipv6 show dynamicport tcp
   netsh int ipv6 show dynamicport udp
   ```

* Vergewissern Sie sich, dass in KB 224196 definierte hart codierte Port Definitionen innerhalb des dynamischen Port Bereichs für die Quell-DCS-Betriebssystemversion liegen. Lesen Sie [KB-Artikel 224196](https://support.microsoft.com/kb/224196) , und stellen Sie sicher, dass der hart codierte Port innerhalb des kurzlebigen Port Bereichs für die Betriebssystemversion des Quell Domänen Controllers liegt.

* Vergewissern Sie sich, dass der Client Protokolls-Schlüssel unter "hklm\software\microsoft\rpc" vorhanden ist und die folgenden fünf Standardwerte enthält:

   ```
   ncacn_http REG_SZ rpcrt4.dll
   ncacn_ip_tcp REG_SZ rpcrt4.dll
   ncacn_nb_tcp REG_SZ rpcrt4.dll
   ncacn_np REG_SZ rpcrt4.dll
   ncacn_ip_udp REG_SZ rpcrt4.dll
   ```

## <a name="more-information"></a>Weitere Informationen

Beispiel für einen ungültigen Namen für die IP-Zuordnung, der RPC-Fehler 1753 und-2146893022 verursacht: der Ziel Prinzipal Name ist falsch.

Die contoso.com-Domäne besteht aus DC1 und DC2 mit den IP-Adressen x. x. 1.1 und x. x. 1.2. Die Host "A"/"AAAA"-Einträge für DC2 sind auf allen für DC1 konfigurierten DNS-Servern ordnungsgemäß registriert. Außerdem enthält die Hostdatei auf DC1 eine Eintrags Zuordnung DC2s voll qualifizierten Hostnamen zur IP-Adresse x. x. 1.2. Später wird die DC2's-IP-Adresse von x. x. 1.2 in X. x. 1.3 geändert, und ein neuer Mitglieds Computer wird mit der IP-Adresse X. x. 1.2 der Domäne hinzugefügt. AD-Replikations Versuche, die vom Befehl " **Jetzt replizieren** " in Active Directory Standorte und Dienste-Snap-in ausgelöst werden, schlagen mit Fehler 1753 wie in der folgenden Ablauf Verfolgung dargestellt

```
F# SRC    DEST    Operation
1 x.x.1.1 x.x.1.2 ARP:Request, x.x.1.1 asks for x.x.1.2
2 x.x.1.2 x.x.1.1 ARP:Response, x.x.1.2 at 00-13-72-28-C8-5E
3 x.x.1.1 x.x.1.2 TCP:Flags=......S., SrcPort=50206, DstPort=DCE endpoint resolution(135)
4 x.x.1.2 x.x.1.1 ARP:Request, x.x.1.2 asks for x.x.1.1
5 x.x.1.1 x.x.1.2 ARP:Response, x.x.1.1 at 00-15-5D-42-2E-00
6 x.x.1.2 x.x.1.1 TCP:Flags=...A..S., SrcPort=DCE endpoint resolution(135)
7 x.x.1.1 x.x.1.2 TCP:Flags=...A...., SrcPort=50206, DstPort=DCE endpoint resolution(135)
8 x.x.1.1 x.x.1.2 MSRPC:c/o Bind: UUID{E1AF8308-5D1F-11C9-91A4-08002B14A0FA} EPT(EPMP)
9 x.x.1.2 x.x.1.1 MSRPC:c/o Bind Ack: Call=0x2 Assoc Grp=0x5E68 Xmit=0x16D0 Recv=0x16D0
10 x.x.1.1 x.x.1.2 EPM:Request: ept_map: NDR, DRSR(DRSR) {E3514235-4B06-11D1-AB04-00C04FC2DCD2} [DCE endpoint resolution(135)]
11 x.x.1.2 x.x.1.1 EPM:Response: ept_map: 0x16C9A0D6 - EP_S_NOT_REGISTERED
```

Bei Frame **10**fragt der Ziel-DC die Quell-DCS-Endpunkt Zuordnung über Port 135 für die Active Directory Replikations Dienstklasse UUID E351...

In Frame **11**ist der Quell Domänen Controller, in diesem Fall ein Mitglieds Computer, der die DC-Rolle noch nicht hostet und daher die E351 nicht registriert hat... Die UUID für den Replikations Dienst mit dem lokalen EPM antwortet mit einem symbolischen Fehler EP_S_NOT_REGISTERED der dem dezimalen Fehler 1753, Hex-Fehler 0x6d9 und dem anzeigen Amen "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar" zugeordnet ist.

Später wird der Mitglieds Computer mit der IP-Adresse x. x. 1.2 als Replikat "mayberrydc" in der contoso.com-Domäne herauf gestuft. Der Befehl " **Jetzt replizieren** " wird verwendet, um die Replikation zu initiieren. dieses Mal schlägt jedoch mit dem Bildschirm Fehler "der Ziel Prinzipal Name ist falsch" fehl. Der Computer, dessen Netzwerkadapter der IP-Adresse x. x. 1.2 zugewiesen ist, ist ein Domänen Controller, wird zurzeit im normalen Modus gestartet und hat den E351 registriert... die UUID des Replikations Diensts mit dem lokalen EPM ist aber nicht der Besitzer des Namens oder der Sicherheitsidentität von DC2 und kann die Kerberos-Anforderung nicht von DC1 entschlüsseln, sodass die Anforderung jetzt mit dem Fehler "der Ziel Prinzipal Name ist falsch" fehlschlägt. Der Fehler wird dem dezimalen Fehler-2146893022/Hex-Fehler 0x80090322 zugeordnet.

Solche ungültigen Host-zu-IP-Zuordnungen können durch veraltete Einträge in Host-/LM-Host-Dateien, Host A/AAAA-Registrierungen in DNS oder WINS verursacht werden.

Zusammenfassung: Dieses Beispiel ist fehlgeschlagen, weil eine ungültige Host-zu-IP-Zuordnung (in diesem Fall in der Hostdatei) bewirkt hat, dass der Domänen Controller zu einem "Quell Domänen Controller" aufgelöst 1753 wurde, auf dem der Active Directory Domain Services-Dienst nicht ausgeführt wird (bzw Im zweiten Fall hat eine ungültige Host-zu-IP-Zuordnung (wieder in der Hostdatei) bewirkt, dass der Domänen Controller eine Verbindung mit einem Domänen Controller herstellt, der die E351 registriert hat... der Replikations-SPN, aber diese Quelle besaß einen anderen Hostnamen und eine andere Sicherheitsidentität als der beabsichtigte Quell Domänen Controller, sodass bei den versuchen Fehler-2146893022: der Ziel Prinzipal Name falsch ist.

## <a name="related-topics"></a>Verwandte Themen

* [Problembehandlung bei Active Directory Vorgängen mit Fehler 1753: Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar.](https://support.microsoft.com/kb/2089874)
* [KB-Artikel 839880 Beheben von Fehlern bei der RPC-Endpunkt Zuordnung mithilfe der Windows Server 2003-Support Tools von der Produkt-CD](https://support.microsoft.com/kb/839880)
* [KB-Artikel 832017 Dienst Übersicht und Netzwerk Port Anforderungen für das Windows Server-System](https://support.microsoft.com/kb/832017/)
* [KB-Artikel 224196 einschränken Active Directory Replikations Datenverkehrs und RPC-Client Datenverkehr zu einem bestimmten Port](https://support.microsoft.com/kb/224196/)
* [KB-Artikel 154596 Konfigurieren der dynamischen RPC-Port Zuweisung zum Arbeiten mit Firewalls](https://support.microsoft.com/kb/154596)
* [Funktionsweise von RPC](/windows/win32/rpc/how-rpc-works)
* [Wie der Server eine Verbindung vorbereitet](/windows/win32/rpc/how-the-server-prepares-for-a-connection)
* [Einrichten einer Verbindung durch den Client](/windows/win32/rpc/how-the-client-establishes-a-connection)
* [Registrieren der-Schnittstelle](/windows/win32/rpc/registering-the-interface)
* [Verfügbar machung des Servers im Netzwerk](/windows/win32/rpc/making-the-server-available-on-the-network)
* [Registrieren von Endpunkten](/windows/win32/rpc/registering-endpoints)
* [Lauschen auf Client Anrufe](/windows/win32/rpc/listening-for-client-calls)
* [Einrichten einer Verbindung durch den Client](/windows/win32/rpc/how-the-client-establishes-a-connection)
* [Einschränken Active Directory Replikations Datenverkehrs und Client-RPC-Datenverkehr an einen bestimmten Port](https://support.microsoft.com/kb/224196)
* [SPN für einen Ziel-DC in AD DS](/openspecs/windows_protocols/ms-drsr/41efc56e-0007-4e88-bafe-d7af61efd91f)
