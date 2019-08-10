---
title: DNS-Server
description: In diesem Artikel wird beschrieben, wie Sie DNS-Probleme auf Serverseite beheben.
manager: willchen
ms.prod: ''
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: b0547436cfa0f07ba9cbc4e3dd1825f8d33bc093
ms.sourcegitcommit: 0e3c2473a54f915d35687d30d1b4b1ac2bae4068
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2019
ms.locfileid: "68917767"
---
# <a name="troubleshooting-dns-servers"></a>DNS-Server

In diesem Artikel wird erläutert, wie Sie Probleme auf DNS-Servern beheben.

## <a name="check-ip-configuration"></a>IP-Konfiguration überprüfen

1. Führen `ipconfig /all` Sie an einer Eingabeaufforderung aus, und überprüfen Sie die IP-Adresse, die Subnetzmaske und das Standard Gateway.

2. Überprüfen Sie, ob der DNS-Server für den Namen, der gesucht wird, autorisierend ist. Wenn dies der Fall ist, finden Sie unter [Überprüfen auf Probleme mit autorisierenden](#checking-for-problems-with-authoritative-data)

3. Führen Sie den folgenden Befehl aus:

   ```cmd
   nslookup <name> <IP address of the DNS server>
   ```
   Zum Beispiel: 
   ```cmd
   nslookup app1 10.0.0.1
   ```
   Wenn Sie einen Fehler oder eine Timeout Antwort erhalten, finden Sie weitere Informationen unter [Überprüfen auf Rekursions Probleme](#checking-for-recursion-problems).

4. Leeren Sie den Konflikt Löser-Cache. Führen Sie hierzu den folgenden Befehl in einem Administrator Eingabe Aufforderungs Fenster aus:

   ```cmd
   dnscmd /clearcache
   ```
   Oder führen Sie in einem administrativen PowerShell-Fenster das folgende Cmdlet aus:
   ```powershell
   Clear-DnsServerCache
   ```

5. Wiederholen Sie Schritt 3. 

## <a name="check-dns-server-problems"></a>DNS-Serverprobleme überprüfen

### <a name="event-log"></a>Ereignisprotokoll

Überprüfen Sie die folgenden Protokolle, um festzustellen, ob aufgezeichnete Fehler aufgetreten sind:

- Application

- System

- DNS-Server

### <a name="test-by-using-nslookup-query"></a>Testen mit nslookup-Abfrage

Führen Sie den folgenden Befehl aus, und überprüfen Sie, ob der DNS-Server über Client Computer erreichbar ist.

```cmd
nslookup <client name> <server IP address>
```

- Wenn der Konflikt Löser die IP-Adresse des Clients zurückgibt, treten keine Probleme auf dem Server auf.

- Wenn der Konflikt Löser die Antwort "Server Fehler" oder "Abfrage abgelehnt" zurückgibt, wird die Zone wahrscheinlich angehalten, oder der Server ist möglicherweise überlastet. Sie können herausfinden, ob es angehalten wurde, indem Sie die Registerkarte "Allgemein" der Zonen Eigenschaften in der DNS-Konsole überprüfen.

Wenn der Konflikt Löser die Antwort "Anforderung an Server Timeout" oder "keine Antwort von Server" zurückgibt, wird der DNS-Dienst wahrscheinlich nicht ausgeführt. Versuchen Sie, den DNS-Server Dienst neu zu starten, indem Sie den folgenden Befehl an einer Eingabeaufforderung auf dem Server eingeben:

```cmd
net start DNS
```

Wenn das Problem auftritt, wenn der Dienst ausgeführt wird, überwacht der Server möglicherweise nicht die IP-Adresse, die Sie in ihrer nslookup-Abfrage verwendet haben. Auf der Registerkarte **Schnittstellen** der Seite Server Eigenschaften in der DNS-Konsole können Administratoren einen DNS-Server so einschränken, dass er nur an ausgewählten Adressen lauscht. Wenn der DNS-Server so konfiguriert wurde, dass der Dienst auf eine bestimmte Liste der konfigurierten IP-Adressen beschränkt wird, ist es möglich, dass die IP-Adresse, die zum Kontaktieren des DNS-Servers verwendet wird, nicht in der Liste enthalten ist. Sie können eine andere IP-Adresse in der Liste ausprobieren oder die IP-Adresse der Liste hinzufügen.

In seltenen Fällen kann der DNS-Server über eine erweiterte Sicherheits-oder Firewallkonfiguration verfügen. Wenn sich der Server in einem anderen Netzwerk befindet, das nur über einen zwischen Host (z. b. einen Paketfilterungs-Router oder einen Proxy Server) erreichbar ist, verwendet der DNS-Server möglicherweise einen nicht standardmäßigen Port zum lauschen und empfangen von Client Anforderungen. Standardmäßig sendet nslookup Abfragen an DNS-Server über den UDP-Port 53. Daher schlagen nslookup-Abfragen fehl, wenn der DNS-Server einen anderen Port verwendet. Wenn Sie der Ansicht sind, dass dies möglicherweise das Problem ist, überprüfen Sie, ob ein zwischen Filter absichtlich zum Blockieren von Datenverkehr für bekannte DNS-Ports verwendet wird. Wenn dies nicht der Fall ist, versuchen Sie, die Paketfilter oder Port Regeln in der Firewall zu ändern, um Datenverkehr über UDP/TCP-Port 53 zuzulassen.

## <a name="checking-for-problems-with-authoritative-data"></a>Überprüfen auf Probleme mit autorisierenden Daten

Überprüfen Sie, ob der Server, der die falsche Antwort zurückgibt, ein primärer Server für die Zone ist (der Standard primäre Server für die Zone oder ein Server, der Active Directory Integration verwendet, um die Zone zu laden), oder ein Server, der eine sekundäre Kopie der Zone gehostet. 

### <a name="if-the-server-is-a-primary-server"></a>Wenn es sich bei dem Server um einen primären Server handelt

Das Problem kann durch einen Benutzerfehler verursacht werden, wenn Benutzerdaten in die Zone eingeben. Möglicherweise wird dies durch ein Problem verursacht, das sich auf Active Directory Replikation oder dynamisches Update auswirkt.

### <a name="if-the-server-is-hosting-a-secondary-copy-of-the-zone"></a>Wenn auf dem Server eine sekundäre Kopie der Zone gehostet wird.

1. Überprüfen Sie die Zone auf dem Master Server (der Server, von dem dieser Server Zonenübertragungen abruft).

   > [!NOTE]
   >Sie können ermitteln, welcher Server der Master Server ist, indem Sie die Eigenschaften der sekundären Zone in der DNS-Konsole überprüfen.

   Wenn der Name auf dem Master Server nicht richtig ist, fahren Sie mit Schritt 4 fort.

2. Wenn der Name auf dem Master Server richtig ist, überprüfen Sie, ob die Seriennummer auf dem Master Server kleiner oder gleich der Seriennummer auf dem sekundären Server ist. Wenn dies der Fall ist, ändern Sie entweder den Master Server oder den sekundären Server so, dass die Seriennummer auf dem Master Server größer ist als die Seriennummer auf dem sekundären Server. 
  
3. Erzwingen Sie auf dem sekundären Server eine Zonen Übertragung in der DNS-Konsole, oder führen Sie den folgenden Befehl aus:
  
   ```cmd
   dnscmd /zonerefresh <zone name>
   ```
  
   Wenn die Zone z. b. Corp.contoso.com lautet, geben `dnscmd /zonerefresh corp.contoso.com`Sie Folgendes ein:.
  
4. Überprüfen Sie den sekundären Server erneut, um festzustellen, ob die Zone korrekt übertragen wurde Wenn dies nicht der Fall ist, liegt wahrscheinlich ein Zonen Übertragungsproblem vor. Weitere Informationen finden Sie unter [Zonen Übertragungsprobleme](#zone-transfer-problems).

5. Wenn die Zone ordnungsgemäß übertragen wurde, überprüfen Sie, ob die Daten jetzt korrekt sind. Andernfalls sind die Daten in der primären Zone falsch. Das Problem kann durch einen Benutzerfehler verursacht werden, wenn Benutzerdaten in die Zone eingeben. Möglicherweise wird dies durch ein Problem verursacht, das sich auf Active Directory Replikation oder dynamisches Update auswirkt.

## <a name="checking-for-recursion-problems"></a>Überprüfen auf Rekursions Probleme

Damit die Rekursion erfolgreich funktioniert, müssen alle DNS-Server, die im Pfad einer rekursiven Abfrage verwendet werden, die richtigen Daten beantworten und weiterleiten können. Wenn dies nicht möglich ist, kann eine rekursive Abfrage aus folgenden Gründen fehlschlagen:

- Timeout für die Abfrage, bevor Sie abgeschlossen werden kann.

- Ein Server, der während der Abfrage verwendet wird, antwortet nicht.

- Ein Server, der während der Abfrage verwendet wird, stellt falsche Daten bereit.

Starten Sie die Problembehandlung auf dem Server, der in der ursprünglichen Abfrage verwendet wurde. Überprüfen Sie, ob dieser Server Abfragen an einen anderen Server weiterleitet, indem Sie die Registerkarte Weiterleitungen in den Server Eigenschaften der DNS-Konsole untersuchen. Wenn das Kontrollkästchen **Weiterleitungen aktivieren aktiviert** ist und mindestens ein Server aufgeführt ist, leitet dieser Server Abfragen weiter.

Wenn dieser Server Abfragen an einen anderen Server weiterleitet, überprüfen Sie auf Probleme, die den Server betreffen, an den dieser Server Abfragen weiterleitet. Informationen zu Problemen finden Sie unter [Überprüfen von DNS-Server Problemen](#check-dns-server-problems). Wenn Sie in diesem Abschnitt aufgefordert werden, eine Aufgabe auf dem Client auszuführen, führen Sie Sie stattdessen auf dem Server aus.

Wenn der Server fehlerfrei ist und Abfragen weiterleiten kann, wiederholen Sie diesen Schritt, und überprüfen Sie den Server, an den dieser Server Abfragen weiterleitet.

Wenn von diesem Server keine Abfragen an einen anderen Server weiterleiten werden, testen Sie, ob dieser Server einen Stamm Server Abfragen kann. Führen Sie hierzu den folgenden Befehl aus:

```cmd
nslookup
server <IP address of server being examined>
set q=NS
 ```

- Wenn die Auflösung die IP-Adresse eines Stamm Servers zurückgibt, haben Sie wahrscheinlich eine unterbrochene Delegierung zwischen dem Stamm Server und dem Namen oder der IP-Adresse, die Sie auflösen möchten. Befolgen Sie das Verfahren [Testen einer unterbrochenen Delegierung](#test-a-broken-delegation) , um zu bestimmen, wo Sie eine unterbrochene Delegierung haben.

- Wenn der Konflikt Löser die Antwort "Anforderung an Server Timeout" zurückgibt, überprüfen Sie, ob die Stamm Hinweise auf funktionierende Stamm Server verweisen. Verwenden Sie hierzu das, [um die aktuellen Stamm Hinweise anzuzeigen](#to-view-the-current-root-hints) . Wenn die Stamm Hinweise auf funktionierende Stamm Server verweisen, liegt möglicherweise ein Netzwerkproblem vor, oder der Server kann eine erweiterte Firewallkonfiguration verwenden, die verhindert, dass der Konflikt Löser den Server abfragt, wie im Abschnitt [Überprüfen von DNS-Serverproblemen](#check-dns-server-problems) beschrieben. Es ist auch möglich, dass die rekursive Timeout-Standardeinstellung zu kurz ist.

### <a name="test-a-broken-delegation"></a>Testen einer unterbrochenen Delegierung

Starten Sie die Tests im folgenden Verfahren, indem Sie einen gültigen Stamm Server Abfragen. Der Test führt Sie durch einen Prozess, bei dem alle DNS-Server von der Stamm-zu einem Server abgefragt werden, den Sie auf eine unterbrochene Delegierung testen.

1. Geben Sie an der Eingabeaufforderung auf dem Server, den Sie testen, Folgendes ein:

   ```cmd
   nslookup
   server <server IP address>
   set norecursion
   set querytype= <resource record type>
   <FQDN>
   ```
   > [!NOTE]
   >Der Ressourcen eingabentyp ist der Typ des Ressourceneinsatzes, den Sie in der ursprünglichen Abfrage abgefragt haben. der voll qualifizierte Name ist der voll qualifizierte Name des voll qualifizierten Datensatzes (durch einen Zeitraum beendet).
 
2. Wenn die Antwort eine Liste der "NS"-und "a"-Ressourcen Einträge für Delegierte Server enthält, wiederholen Sie Schritt 1 für jeden Server, und verwenden Sie die IP-Adresse aus den "a"-Ressourcen Einträgen als Server-IP-Adresse.

   - Wenn die Antwort keinen "NS"-Ressourcen Daten Satz enthält, ist die Delegierung beschädigt.
   
   - Wenn die Antwort "NS"-Ressourcen Einträge, aber keine "A"-Ressourcen Einträge enthält, geben Sie **Rekursion festlegen**ein, und führen Sie einzeln Abfragen für "A"-Ressourcen Einträge von Servern aus, die in den NS-Einträgen aufgeführt sind. Wenn Sie nicht mindestens eine gültige IP-Adresse eines "A"-Ressourceneinsatzes für jeden NS-Ressourcen Daten Satz in einer Zone finden, ist die Delegierung beschädigt.

3. Wenn Sie feststellen, dass die Delegierung beschädigt ist, korrigieren Sie Sie durch Hinzufügen oder Aktualisieren eines "a"-Ressourceneinsatzes in der übergeordneten Zone, indem Sie eine gültige IP-Adresse für einen korrekten DNS-Server für die delegierte Zone verwenden.

### <a name="to-view-the-current-root-hints"></a>So zeigen Sie die aktuellen Stamm Hinweise an

1. Starten Sie die DNS-Konsole.

2. Fügen Sie den DNS-Server, bei dem eine rekursive Abfrage fehlgeschlagen ist

3. Klicken Sie mit der rechten Maustaste auf den Server, und wählen Sie **Eigenschaften**.

4. Klicken Sie auf root-Hinweise.

Überprüfen Sie, ob grundlegende Konnektivität zu den Stamm Servern besteht.

- Wenn die Stamm Hinweise ordnungsgemäß konfiguriert sind, überprüfen Sie, ob der DNS-Server, der in einer fehlgeschlagenen Namensauflösung verwendet wird, die Stamm Server per IP-Adresse pingen kann.

- Wenn die Stamm Server nicht auf das Pingen nach IP-Adresse reagieren, haben sich möglicherweise die IP-Adressen für die Stamm Server geändert. Es ist jedoch ungewöhnlich, dass Sie eine Neukonfiguration der Stamm Server sehen.

## <a name="zone-transfer-problems"></a>Zonen Übertragungsprobleme

Führen Sie die folgenden Überprüfungen aus:

- Überprüfen Sie Ereignisanzeige für den primären und den sekundären DNS-Server.

- Überprüfen Sie auf dem Master Server, ob die Übertragung der Sicherheit verweigert wird. 

- Überprüfen Sie die Registerkarte **Zonenübertragungen** der Zonen Eigenschaften in der DNS-Konsole. Wenn der Server Zonenübertragungen zu einer Liste von Servern einschränkt, z. b. auf der Registerkarte **Namen Server** der Zonen Eigenschaften, stellen Sie sicher, dass der sekundäre Server in der Liste enthalten ist. Stellen Sie sicher, dass der Server für das Senden von Zonenübertragungen konfiguriert ist.

- Überprüfen Sie den Master Server auf Probleme, indem Sie die Schritte im Abschnitt [Überprüfen der DNS-Serverprobleme](#check-dns-server-problems) ausführen. Wenn Sie aufgefordert werden, eine Aufgabe auf dem Client auszuführen, führen Sie die Aufgabe stattdessen auf dem sekundären Server aus.

- Überprüfen Sie, ob auf dem sekundären Server eine andere DNS-Server Implementierung ausgeführt wird, beispielsweise BIND. Wenn dies der Fall ist, kann das Problem eine der folgenden Gründe haben:

  - Der Windows-Master Server ist möglicherweise für das Senden von schnellen Zonenübertragungen konfiguriert, aber der sekundäre Server von Drittanbietern unterstützt möglicherweise keine schnellen Zonenübertragungen. Wenn dies der Fall ist, deaktivieren Sie in der DNS-Konsole die Übertragung von schnellen Zonen auf dem Master Server, indem Sie auf der Registerkarte **erweitert** in den Eigenschaften des Servers das Kontrollkästchen sekundäre Datenbanken **aktivieren aktivieren** .

  - Wenn eine Forward-Lookupzone auf dem Windows-Server einen Daten Recordtyp (z. b. einen SRV-Datensatz) enthält, den der sekundäre Server nicht unterstützt, kann der sekundäre Serverprobleme beim Ziehen der Zone haben.

Überprüfen Sie, ob auf dem Master Server eine andere DNS-Server Implementierung ausgeführt wird, beispielsweise BIND. Wenn dies der Fall ist, ist es möglich, dass die Zone auf dem Master Server nicht kompatible Ressourcen Einträge enthält, die von Windows nicht erkannt werden.
 
Wenn auf dem Master-oder sekundären Server eine andere DNS-Server Implementierung ausgeführt wird, überprüfen Sie beide Server, um sicherzustellen, dass Sie dieselben Features unterstützen. Sie können den Windows-Server in der DNS-Konsole auf der Registerkarte **erweitert** der Seite Eigenschaften für den Server überprüfen. Zusätzlich zum Kontrollkästchen "Binden von sekundären Replikaten aktivieren" enthält diese Seite die Dropdown Liste " **namens Überprüfung** ". Auf diese Weise können Sie die Erzwingung der strikten RFC-Konformität für Zeichen in DNS-Namen auswählen.

