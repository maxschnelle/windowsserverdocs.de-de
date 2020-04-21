---
title: Richtlinien für die Problembehandlung von Aktivierungsproblemen im Zusammenhang mit DNS
ms.topic: article
ms.date: 09/10/2019
ms.technology: server-general
author: Teresa-Motiv
ms.author: v-tea
ms.localizationpriority: medium
ms.openlocfilehash: 76665d91cc1e2997a837721ffbc51b0513dd7c1a
ms.sourcegitcommit: af1cf89632d62a94943d3ad9f6b5234b88499278
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/16/2020
ms.locfileid: "81524935"
---
# <a name="guidelines-for-troubleshooting-dns-related-activation-issues"></a>Richtlinien für die Problembehandlung von Aktivierungsproblemen im Zusammenhang mit DNS

Möglicherweise müssen Sie einige dieser Methoden verwenden, wenn eine oder mehrere der folgenden Bedingungen zutreffen:

- Sie verwenden Medien mit Volumenlizenzierung und einen&nbsp;generischen Volumenlizenz-Product Key zum Installieren eines der folgenden Betriebssysteme:
   - Windows Server 2019
   - Windows Server 2016
   - Windows Server 2012 R2
   - Windows Server 2012
   - Windows Server 2008 R2
   - WindowsServer 2008
   - Windows 10
   - Windows 8.1
   - Windows 8
- Der Aktivierungs-Assistent kann keine Verbindung mit einem KMS-Hostcomputer herstellen.

Wenn Sie versuchen, ein Clientsystem zu aktivieren, verwendet der Aktivierungs-Assistent DNS, um nach einem entsprechenden Computer zu suchen, auf dem die KMS-Software ausgeführt wird. Wenn der Assistent DNS abfragt und den DNS-Eintrag für den KMS-Hostcomputer nicht findet, meldet der Assistent einen Fehler.   

<a id="list"></a>Suchen Sie in der folgenden Liste eine Vorgehensweise für Ihr Problem:

- Wenn Sie keinen KMS-Host installieren können oder die KMS-Aktivierung nicht verwenden können, [ändern Sie den Product Key in einen MAK](#change-the-product-key-to-an-mak).
- Wenn Sie einen KMS-Host installieren und konfigurieren müssen, [konfigurieren Sie einen KMS-Host für die Clients, für die die Aktivierung erfolgen soll](#configure-a-kms-host-for-the-clients-to-activate-against).
- Wenn der Client den vorhandenen KMS-Host nicht finden kann, gehen Sie wie folgt vor, um Probleme bei den Routingkonfigurationen zu beheben. Diese Liste der Verfahren ist nach zunehmender Komplexität sortiert.
  - [Überprüfen der grundlegenden IP-Konnektivität mit dem DNS-Server](#verify-basic-ip-connectivity-to-the-dns-server)
  - [Überprüfen der KMS-Hostkonfiguration](#verify-the-configuration-of-the-kms-host)  
  - [Bestimmen des Typs des Routingproblems](#determine-the-type-of-routing-issue)
  - [Überprüfen der DNS-Konfiguration](#verify-the-dns-configuration)
  - [Manuelles Erstellen eines KMS-SRV-Eintrags](#manually-create-a-kms-srv-record)
  - [Manuelles Zuweisen eines KMS-Hosts zu einem KMS-Client](#manually-assign-a-kms-host-to-a-kms-client)
  - [Konfigurieren des KMS-Hosts für die Veröffentlichung in mehreren DNS-Domänen](#configure-the-kms-host-to-publish-in-multiple-dns-domains)

## <a name="change-the-product-key-to-an-mak"></a>Ändern des Product Key in einen MAK

Wenn Sie keinen KMS-Host installieren können oder die KMS-Aktivierung aus einem anderen Grund nicht verwenden können, ändern Sie den Product Key in einen MAK. Wenn Sie Windows-Images vom Microsoft Developer Network (MSDN) oder von TechNet heruntergeladen haben, sind die unter den Medien aufgeführten Stock Keeping Units (SKUs) im Allgemeinen Medien mit Volumenlizenz, und der bereitgestellte Product Key ist ein MAK.

Um den Product Key in einen MAK zu ändern, führen Sie die folgenden Schritte aus:

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten. Drücken Sie hierzu WINDOWS-TASTE+X, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und wählen Sie dann **Als Administrator ausführen** aus. Wenn Sie aufgefordert werden, ein Administratorkennwort oder eine Bestätigung einzugeben, geben Sie das Kennwort ein, bzw. bestätigen Sie den Vorgang.
2. Führen Sie an der Eingabeaufforderung den folgenden Befehl aus:
   ```cmd
    slmgr -ipk xxxxx-xxxxx-xxxxx-xxxxx-xxxxx
   ```
   > [!NOTE]
   > Der Platzhalter **xxxxx-xxxxx-xxxxx-xxxxx-xxxxx** stellt den MAK-Product Key dar.  

[Zurück zur Liste der Verfahren](#list)

## <a name="configure-a-kms-host-for-the-clients-to-activate-against"></a>Konfigurieren eines KMS-Hosts für die Clients, für die die Aktivierung erfolgen soll

Die KMS-Aktivierung erfordert das Konfigurieren eines KMS-Hosts für die Clients, für die die Aktivierung erfolgen soll. Wenn in Ihrer Umgebung keine KMS-Hosts konfiguriert sind, installieren und aktivieren Sie einen KMS-Host, indem Sie einen geeigneten KMS-Hostschlüssel verwenden. Nachdem Sie einen Netzwerkcomputer zum Hosten der KMS-Software konfiguriert haben, veröffentlichen Sie die DNS-Einstellungen (Domain Name System).

Weitere Informationen zum Konfigurieren von KMS-Hosts finden Sie unter [Aktivieren mit dem Schlüsselverwaltungsdienst](https://docs.microsoft.com/windows/deployment/volume-activation/activate-using-key-management-service-vamt) und [Installieren und Konfigurieren des VAMT](https://docs.microsoft.com/windows/deployment/volume-activation/install-configure-vamt).

[Zurück zur Liste der Verfahren](#list)

## <a name="verify-basic-ip-connectivity-to-the-dns-server"></a>Überprüfen der grundlegenden IP-Konnektivität mit dem DNS-Server

Überprüfen Sie die grundlegende IP-Konnektivität mithilfe des Pingbefehls. Führen Sie hierzu auf dem KMS-Client, auf dem der Fehler aufgetreten ist, und auf dem KMS-Hostcomputer die folgenden Schritte aus:

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten.
1. Führen Sie an der Eingabeaufforderung den folgenden Befehl aus:
   ```cmd
   ping <DNS_Server_IP_address>
   ```
   > [!NOTE]
   > Wenn in der Ausgabe dieses Befehls nicht der Ausdruck „Antwort von“ enthalten ist, gibt es ein Netzwerkproblem oder ein DNS-Problem, das Sie beheben müssen, bevor Sie die anderen Verfahren in diesem Artikel verwenden können. Weitere Informationen zum Beheben von TCP/IP-Problemen, wenn der DNS-Server nicht gepingt werden kann, finden Sie unter [Erweiterte Problembehandlung für TCP/IP](https://docs.microsoft.com/windows/client-management/troubleshoot-tcpip).

[Zurück zur Liste der Verfahren](#list)

## <a name="verify-the-configuration-of-the-kms-host"></a>Überprüfen der KMS-Hostkonfiguration

Überprüfen Sie die Registrierung des KMS-Hostservers, um zu bestimmen, ob er eine DNS-Registrierung durchführt. Standardmäßig registriert ein KMS-Hostserver dynamisch alle 24 Stunden einen DNS-SRV-Eintrag. 
> [!IMPORTANT]
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/help/322756) für den Fall, dass Probleme auftreten.  

Gehen Sie wie folgt vor, um diese Einstellung zu überprüfen:
1. Starten Sie den Registrierungs-Editor. Klicken Sie hierzu mit der rechten Maustaste auf **Start**, wählen Sie **Ausführen** aus, geben Sie **regedit** ein, und drücken Sie die EINGABETASTE.
1. Suchen Sie den Unterschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SL**, und überprüfen Sie den Wert des Eintrags **DisableDnsPublishing**. Die möglichen Werte dieses Eintrags lauten:
   - **0** oder nicht definiert (Standard): Der KMS-Hostserver registriert alle 24 Stunden einen SRV-Eintrag.
   - **1**: Der KMS-Hostserver registriert SRV-Einträge nicht automatisch. Wenn Ihre Implementierung keine dynamischen Updates unterstützt, lesen Sie [Manuelles Erstellen eines KMS-SRV-Eintrags](#manually-create-a-kms-srv-record).  
1. Wenn der Eintrag **DisableDnsPublishing** fehlt, erstellen Sie ihn (der Typ lautet „DWORD“). Wenn die dynamische Registrierung akzeptabel ist, lassen Sie den Wert undefiniert, oder legen Sie ihn auf **0** fest.

[Zurück zur Liste der Verfahren](#list)

## <a name="determine-the-type-of-routing-issue"></a>Bestimmen des Typs des Routingproblems

Mit den folgenden Befehlen können Sie feststellen, ob es sich um ein Problem bei der Namensauflösung oder um ein Problem beim SRV-Eintrag handelt.  

1. Öffnen Sie auf einem KMS-Client ein Eingabeaufforderungsfenster mit erhöhten Rechten.  
1. Führen Sie an der Eingabeaufforderung die folgenden Befehle aus:
   ```cmd
   cscript \windows\system32\slmgr.vbs -skms <KMS_FQDN>:<port>
   cscript \windows\system32\slmgr.vbs -ato
   ```
   > [!NOTE]
   > In diesem Befehl stellt <KMS_FQDN> den vollqualifizierten Domänennamen (FQDN) des KMS-Hostcomputers und \<port\> den vom KMS verwendeten TCP-Port dar.  

   Wenn das Problem durch diese Befehle behoben wird, handelt es sich um ein Problem beim SRV-Eintrag. Sie können es mit einem der Befehle beheben, die unter [Manuelles Zuweisen eines KMS-Hosts zu einem KMS-Client](#manually-assign-a-kms-host-to-a-kms-client) dokumentiert sind.  

1. Wenn das Problem weiterhin besteht, führen Sie die folgenden Befehle aus:
   ```cmd
   cscript \windows\system32\slmgr.vbs -skms <IP Address>:<port>
   cscript \windows\system32\slmgr.vbs -ato
   ```
   > [!NOTE]
   > In diesem Befehl stellt \<IP Address\> die IP-Adresse des KMS-Hostcomputers und \<port\> den vom KMS verwendeten TCP-Port dar.  

   Wenn das Problem durch diese Befehle behoben wird, handelt es sich mit hoher Wahrscheinlichkeit um ein Problem bei der Namensauflösung. Weitere Informationen zur Problembehandlung finden Sie unter [Überprüfen der DNS-Konfiguration](#verify-the-dns-configuration).

1. Wenn das Problem durch keinen dieser Befehle behoben wird, überprüfen Sie die Firewallkonfiguration des Computers. Bei allen Aktivierungsnachrichten zwischen KMS-Clients und dem KMS-Host wird der TCP-Port 1688 verwendet. Die Firewalls auf dem KMS-Client und KMS-Host müssen die Kommunikation über Port 1688 zulassen.

[Zurück zur Liste der Verfahren](#list)

## <a name="verify-the-dns-configuration"></a>Überprüfen der DNS-Konfiguration

>[!NOTE]
> Sofern nicht anders angegeben, führen Sie die folgenden Schritte auf einem KMS-Client aus, bei dem der entsprechende Fehler aufgetreten ist.

1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten.
1. Führen Sie an der Eingabeaufforderung den folgenden Befehl aus:
   ```cmd
   IPCONFIG /all
   ```
1. Beachten Sie in den Befehlsergebnissen die folgenden Informationen:
   - Die zugewiesene IP-Adresse des KMS-Clientcomputers
   - Die IP-Adresse des primären DNS-Servers, der vom KMS-Clientcomputer verwendet wird
   - Die IP-Adresse des Standardgateways, das vom KMS-Clientcomputer verwendet wird
   - Die DNS-Suffixsuchliste, die der KMS-Clientcomputer verwendet
1. Vergewissern Sie sich, dass die SRV-Einträge des KMS-Hosts in DNS registriert sind. Gehen Sie hierzu folgendermaßen vor:  
   1. Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten.
   1. Führen Sie an der Eingabeaufforderung den folgenden Befehl aus:
      ```cmd
      nslookup -type=all _vlmcs._tcp>kms.txt
      ```
   1. Öffnen Sie die Datei „KMS.txt“, die durch den Befehl generiert wird. Diese Datei sollte mindestens einen Eintrag wie den folgenden enthalten:
       ```
       _vlmcs._tcp.contoso.com SRV service location:
       priority = 0
       weight = 0
       port = 1688 svr hostname = kms-server.contoso.com
       ```
       > [!NOTE]
       > In diesem Eintrag stellt „contoso.com“ die Domäne des KMS-Hosts dar.
      1. Überprüfen Sie die IP-Adresse, den Hostnamen, den Port und die Domäne des KMS-Hosts.
      1. Wenn diese **_vlmcs**-Einträge vorhanden sind und die erwarteten KMS-Hostnamen enthalten, fahren Sie mit [Manuelles Zuweisen eines KMS-Hosts zu einem KMS-Client](#manually-assign-a-kms-host-to-a-kms-client) fort.  
      > [!NOTE]
      > Wenn mit dem Befehl [**nslookup**](https://docs.microsoft.com/windows-server/administration/windows-commands/nslookup) der KMS-Host gefunden wird, bedeutet dies nicht, dass der DNS-Client den KMS-Host finden kann. Wenn mit dem Befehl **nslookup** der KMS-Host gefunden wird, die Aktivierung mit dem KMS-Host jedoch immer noch nicht möglich ist, überprüfen Sie die anderen DNS-Einstellungen, z. B. das primäre DNS-Suffix und die DNS-Suffixsuchliste.
1. Vergewissern Sie sich, dass die Suchliste des primären DNS-Suffix das DNS-Domänensuffix enthält, das dem KMS-Host zugeordnet ist. Wenn diese Information in der Suchliste nicht enthalten ist, fahren Sie mit [Konfigurieren des KMS-Hosts für die Veröffentlichung in mehreren DNS-Domänen](#configure-the-kms-host-to-publish-in-multiple-dns-domains) fort.

[Zurück zur Liste der Verfahren](#list)

## <a name="manually-create-a-kms-srv-record"></a>Manuelles Erstellen eines KMS-SRV-Eintrags

Führen Sie die folgenden Schritte aus, um manuell einen SRV-Eintrag für einen KMS-Host zu erstellen, der einen Microsoft-DNS-Server verwendet:

1. Öffnen Sie auf dem DNS-Server den DNS-Manager. Um den DNS-Manager zu öffnen, wählen Sie **Start**, **Verwaltung** und dann **DNS** aus.
1. Wählen Sie den DNS-Server aus, auf dem Sie den SRV-Ressourceneintrag erstellen müssen.
1. Erweitern Sie in der Konsolenstruktur **Forward-Lookupzonen**, klicken Sie mit der rechten Maustaste auf die Domäne, und wählen Sie dann **Weitere neue Einträge** aus.
1. Scrollen Sie in der Liste nach unten, wählen Sie **Dienstidentifizierung (SRV)** aus, und wählen Sie dann **Eintrag erstellen** aus.
1. Geben Sie die folgenden Informationen ein:
   - Dienst: **_VLMCS**
   - Protokoll: **_TCP**
   - Portnummer: **1688**
   - Host, der diesen Dienst anbietet: **&lt;*FQDN des KMS-Hosts*&gt;**
1. Wenn Sie fertig sind, klicken Sie auf **OK** und dann auf **Fertig**.

Um manuell einen SRV-Eintrag für einen KMS-Host zu erstellen, der einen mit BIND 9.x kompatiblen DNS-Server verwendet, befolgen Sie die Anweisungen für diesen DNS-Server, und geben Sie die folgenden Informationen für den SRV-Eintrag an:

- Name:&nbsp; **_vlmcs._TCP**
- Typ:&nbsp;**SRV**
- Priorität: **0**
- Gewichtung: **0**
- Port: **1688**
- Hostname: **&lt;*FQDN oder A-Eintrag des KMS-Hosts*&gt;**

> [!NOTE]
> Die Werte **Priorität** und **Gewichtung** werden im KMS nicht verwendet. Der Eintrag muss sie jedoch enthalten.

Um zur Unterstützung der automatischen KMS-Veröffentlichung einen mit BIND 9.x kompatiblen DNS-Server zu konfigurieren, aktivieren Sie in der DNS-Serverkonfiguration das Aktualisieren von Ressourceneinträgen von KMS-Hosts. Fügen Sie beispielweise der Zonendefinition in „Named.conf“ oder „Named.conf.local“ die folgende Zeile hinzu:

```cmd
allow-update { any; };
```
## <a name="manually-assign-a-kms-host-to-a-kms-client"></a>Manuelles Zuweisen eines KMS-Hosts zu einem KMS-Client

Standardmäßig wird von den KMS-Clients die automatische Ermittlung verwendet. Dabei fragt ein KMS-Client DNS nach einer Liste von Servern ab, die in der Mitgliedschaftszone des Clients _vlmcs-SRV-Einträge veröffentlicht haben. DNS gibt die Liste der KMS-Hosts in zufälliger Reihenfolge zurück. Der Client wählt einen KMS-Host aus und versucht, eine Sitzung auf ihm einzurichten. Wenn die Sitzung erfolgreich eingerichtet wird, zwischenspeichert der Client den Namen des KMS-Hosts und versucht, ihn bei der nächsten Verlängerung zu verwenden. Wenn das Einrichten der Sitzung fehlschlägt, wählt der Client nach dem Zufallsprinzip einen anderen KMS-Host aus. Es wird dringend empfohlen, die automatische Ermittlung zu verwenden.  

Sie können jedoch einen KMS-Host manuell einem bestimmten KMS-Client zuweisen. Führen Sie dazu folgende Schritte durch.

1. Öffnen Sie auf einem KMS-Client ein Eingabeaufforderungsfenster mit erhöhten Rechten.
1. Führen Sie je nach Implementierung einen der folgenden Schritte aus:
   - Führen Sie den folgenden Befehl aus, um einen KMS-Host mithilfe des FQDN des Hosts zuzuweisen:
     ```cmd
     cscript \windows\system32\slmgr.vbs -skms <KMS_FQDN>:<port>
     ```
   - Führen Sie den folgenden Befehl aus, um einen KMS-Host mithilfe der IPv4-Adresse des Hosts zuzuweisen:
     ```cmd
     cscript \windows\system32\slmgr.vbs -skms <IPv4Address>:<port>
     ```
    - Führen Sie den folgenden Befehl aus, um einen KMS-Host mithilfe der IPv6-Adresse des Hosts zuzuweisen:
      ```cmd
      cscript \windows\system32\slmgr.vbs -skms <IPv6Address>:<port>
      ```
    - Führen Sie den folgenden Befehl aus, um einen KMS-Host mithilfe des NetBIOS-Namens des Hosts zuzuweisen:
      ```cmd
      cscript \windows\system32\slmgr.vbs -skms <NETBIOSName>:<port>
      ```
   - Führen Sie den folgenden Befehl aus, um die automatische Ermittlung auf einem KMS-Client wiederherzustellen:
     ```cmd
     cscript \windows\system32\slmgr.vbs -ckms
     ```
     > [!NOTE]
     > In diesen Befehlen werden die folgenden Platzhalter verwendet:
     >- **<KMS_FQDN>** stellt den vollqualifizierten Domänennamen (FQDN) des KMS-Hostcomputers dar.
     >- **\<IPv4Address\>** stellt die IPv4-Adresse des KMS-Hostcomputers dar.
     >- **\<IPv6Address\>** stellt die IPv6-Adresse des KMS-Hostcomputers dar.
     >- **\<NETBIOSName\>** steht für den NetBIOS-Namen des KMS-Hostcomputers.
     >- **\<\>port** stellt den vom KMS verwendeten TCP-Port dar.  

## <a name="configure-the-kms-host-to-publish-in-multiple-dns-domains"></a>Konfigurieren des KMS-Hosts für die Veröffentlichung in mehreren DNS-Domänen

> [!IMPORTANT]
> Folgen Sie den Schritten in diesem Abschnitt sorgfältig. Wird die Registrierung falsch angepasst, können schwerwiegende Probleme auftreten. Bevor Sie sie ändern, [sichern Sie die Registrierung zwecks Wiederherstellung](https://support.microsoft.com/help/322756) für den Fall, dass Probleme auftreten.

Wie unter [Manuelles Zuweisen eines KMS-Hosts zu einem KMS-Client](#manually-assign-a-kms-host-to-a-kms-client) beschrieben, verwenden KMS-Clients in der Regel die automatische Ermittlung zur Identifizierung von KMS-Hosts. Hierfür müssen die _vlmcs-SRV-Einträge in der DNS-Zone des KMS-Clientcomputers verfügbar sein. Die DNS-Zone entspricht entweder dem primären DNS-Suffix des Computers oder einem der folgenden Elemente:
- Für Computer, die einer Domäne beigetreten sind, die von DNS zugewiesene Domäne des Computers, z. B. AD DS-DNS (Active Directory Domain Services).
- Für Arbeitsgruppencomputer die per DHCP (Dynamic Host Configuration Protocol) zugewiesene Domäne des Computers. Dieser Domänenname wird durch die Option mit dem Codewert 15 in RFC 2132 (Request for Comments) definiert.

Standardmäßig registriert ein KMS-Host seine SRV-Einträge in der DNS-Zone, die der Domäne des KMS-Hostcomputers entspricht. Angenommen, ein KMS-Host tritt der Domäne „contoso.com“ bei. In diesem Szenario registriert der KMS-Host den _vmlcs-SRV-Eintrag in der DNS-Zone „contoso.com“. Daher identifiziert der Eintrag den Dienst als „_VLMCS._TCP.CONTOSO.COM“.

Wenn der KMS-Host und die KMS-Clients unterschiedliche DNS-Zonen verwenden, müssen Sie den KMS-Host so konfigurieren, dass seine SRV-Einträge automatisch in mehreren DNS-Domänen veröffentlicht werden. Gehen Sie hierzu folgendermaßen vor:

1. Starten Sie auf dem KMS-Host den Registrierungs-Editor. 
1. Suchen Sie den Unterschlüssel **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\SL**, und wählen Sie ihn aus.
1. Klicken Sie im Bereich **Details** mit der rechten Maustaste auf einen leeren Bereich, wählen Sie **Neu** aus, und wählen Sie dann **Wert der mehrteiligen Zeichenfolge** aus.
1. Geben Sie als Namen des neuen Eintrags **DnsDomainPublishList** ein.
1. Klicken Sie mit der rechten Maustaste auf den neuen Eintrag **DnsDomainPublishList**, und wählen Sie dann **Ändern** aus.
1. Geben Sie im Dialogfeld **Mehrteilige Zeichenfolge bearbeiten** jedes vom KMS veröffentlichte DNS-Domänensuffix in einer eigenen Zeile ein, und klicken Sie dann auf **OK**.
   > [!NOTE]
   > Unter Windows Server 2008 R2 wird für **DnsDomainPublishList** ein anderes Format verwendet. Weitere Informationen finden Sie in „Technische Referenz zur Volumenaktivierung“.
1. Verwenden Sie das Verwaltungstool „Dienste“, um den Softwarelizenzierungsdienst neu zu starten. Mit diesem Vorgang werden die SRV-Einträge erstellt.
1. Überprüfen Sie mithilfe einer typischen Methode, ob der KMS-Client Kontakt mit dem von Ihnen konfigurierten KMS-Host aufnehmen kann. Überprüfen Sie, ob der KMS-Client den KMS-Host ordnungsgemäß anhand des Namens und der IP-Adresse identifiziert. Wenn eine dieser Überprüfungen fehlschlägt, untersuchen Sie dieses DNS-Clientresolverproblem.
1. Um ggf. zuvor zwischengespeicherte KMS-Hostnamen auf dem KMS-Client zu löschen, öffnen Sie auf dem KMS-Client ein Eingabeaufforderungsfenster mit erhöhten Rechten, und führen Sie dann den folgenden Befehl aus:
   ```cmd
   cscript C:\Windows\System32\slmgr.vbs -ckms
   ```
