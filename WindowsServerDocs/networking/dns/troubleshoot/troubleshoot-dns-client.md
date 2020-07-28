---
title: Problembehandlung bei DNS-Clients
description: In diesem Artikel wird beschrieben, wie Sie ein DNS-Problem auf Clientseite beheben.
manager: dcscontentpm
ms.technology: networking-dns
ms.topic: article
ms.author: delhan
ms.date: 8/8/2019
author: Deland-Han
ms.openlocfilehash: 2a9b44807ae6bc9f4c446d4af2150caf09955899
ms.sourcegitcommit: d99bc78524f1ca287b3e8fc06dba3c915a6e7a24
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2020
ms.locfileid: "87182336"
---
# <a name="troubleshooting-dns-clients"></a>Problembehandlung bei DNS-Clients

In diesem Artikel wird erläutert, wie Sie Probleme von DNS-Clients beheben.

## <a name="check-ip-configuration"></a>IP-Konfiguration überprüfen

1. Öffnen Sie ein Eingabe Aufforderungs Fenster als Administrator auf dem Client Computer.

2. Führen Sie den folgenden Befehl aus:

   ```cmd
   ipconfig /all
   ```

3. Stellen Sie sicher, dass der Client über eine gültige IP-Adresse, Subnetzmaske und ein Standard Gateway für das Netzwerk verfügt, an das es angefügt und verwendet wird.

4. Überprüfen Sie die DNS-Server, die in der Ausgabe aufgeführt sind, und überprüfen Sie, ob die aufgeführten IP-Adressen korrekt sind.

5. Überprüfen Sie das Verbindungs spezifische DNS-Suffix in der Ausgabe, und überprüfen Sie, ob es korrekt ist.

Wenn der Client keine gültige TCP/IP-Konfiguration hat, verwenden Sie eine der folgenden Methoden:

* Verwenden Sie für dynamisch konfigurierte Clients den `ipconfig /renew` Befehl, um die IP-Adress Konfiguration des Clients manuell mit dem DHCP-Server zu erneuern.

* Ändern Sie für statisch konfigurierte Clients die TCP/IP-Client Eigenschaften so, dass gültige Konfigurationseinstellungen verwendet werden, oder schließen Sie die DNS-Konfiguration für das Netzwerk ab.

## <a name="check-network-connection"></a>Netzwerkverbindung überprüfen

### <a name="ping-test"></a>Ping-Test

Stellen Sie sicher, dass der Client einen bevorzugten (oder Alternativen) DNS-Server kontaktieren kann, indem er den bevorzugten DNS-Server über seine IP-Adresse anhebt.

Wenn der Client z. b. einen bevorzugten DNS-Server von 10.0.0.1 verwendet, führen Sie diesen Befehl an einer Eingabeaufforderung aus:

```cmd
ping 10.0.0.1
```

Wenn kein konfigurierter DNS-Server auf das direkte Pingen seiner IP-Adresse antwortet, bedeutet dies, dass die Ursache des Problems wahrscheinlicher ist, dass die Netzwerk Konnektivität zwischen dem Client und den DNS-Servern besteht. Wenn dies der Fall ist, befolgen Sie die grundlegenden Schritte zur Behebung des TCP/IP-Netzwerks, um das Problem zu beheben. Beachten Sie, dass ICMP-Datenverkehr über die Firewall zugelassen werden muss, damit der Ping-Befehl funktioniert.

### <a name="dns-query-tests"></a>DNS-Abfrage Tests

Wenn der DNS-Client einen Ping an den DNS-Server Computer durchführen kann, verwenden Sie die folgenden `nslookup` Befehle, um zu testen, ob der Server auf DNS-Clients reagieren kann. Da nslookup nicht den DNS-Cache des Clients verwendet, wird bei der Namensauflösung der konfigurierte DNS-Server des Clients verwendet.

#### <a name="test-a-client"></a>Testen eines Clients

```cmd
nslookup <client>
```

Wenn der Client Computer z. b. den Namen **CLIENT1**hat, führen Sie den folgenden Befehl aus:

```cmd
nslookup client1
```

Wenn keine erfolgreiche Antwort zurückgegeben wird, versuchen Sie, den folgenden Befehl auszuführen:

```cmd
nslookup <fqdn of client>
```

Wenn der voll qualifizierte Name für den voll qualifizierten Namen " **CLIENT1.Corp.contoso.com**" lautet, führen Sie den folgenden Befehl aus:

```cmd
nslookup client1.corp.contoso.com.
```

> [!NOTE]
> Sie müssen den nachfolgenden Zeitraum angeben, wenn Sie diesen Test ausführen.

Wenn Windows den voll qualifizierten Namen gefunden hat, den Kurznamen jedoch nicht finden kann, überprüfen Sie die DNS-Suffixkonfiguration auf der Registerkarte DNS der erweiterten TCP/IP-Einstellungen der NIC. Weitere Informationen finden Sie unter [Konfigurieren der DNS-Auflösung](/previous-versions/tn-archive/dd163570(v=technet.10)#configuring-dns-resolution).

#### <a name="test-the-dns-server"></a>Testen des DNS-Servers

```cmd
nslookup <DNS Server>
```

Wenn der DNS-Server z. b. den Namen DC1 hat, führen Sie den folgenden Befehl aus:

```cmd
nslookup dc1
```
Wenn die vorherigen Tests erfolgreich waren, sollte dieser Test ebenfalls erfolgreich sein. Wenn der Test nicht erfolgreich ist, überprüfen Sie die Konnektivität zum DNS-Server.

#### <a name="test-the-failing-record"></a>Testen des fehlerhaften Datensatzes

```cmd
nslookup <failed internal record>
```

Wenn der fehlerhafte Datensatz z. b. **App1.Corp.contoso.com**lautet, führen Sie den folgenden Befehl aus:

```cmd
nslookup app1.corp.contoso.com
```

#### <a name="test-a-public-internet-address"></a>Testen einer öffentlichen Internet Adresse

```cmd
nslookup <external name>
```

Beispiel:
```cmd
nslookup bing.com
```

Wenn alle vier Tests erfolgreich waren, führen `ipconfig /displaydns` Sie aus, und überprüfen Sie die Ausgabe auf den Namen, der fehlgeschlagen ist. Wenn der Name "Name ist nicht vorhanden" angezeigt wird, wurde eine negative Antwort von einem DNS-Server zurückgegeben und auf dem Client zwischengespeichert.

Um das Problem zu beheben, löschen Sie den Cache, indem Sie Ausführen `ipconfig /flushdns` .

## <a name="next-step"></a>Nächster Schritt

Wenn die Namensauflösung weiterhin fehlschlägt, besuchen Sie den Abschnitt Problembehandlung bei [DNS-Servern](troubleshoot-dns-server.md) .
