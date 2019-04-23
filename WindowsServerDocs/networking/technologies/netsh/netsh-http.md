---
title: Netsh-Befehle für Hypertext Transfer-Protokoll (HTTP)
description: Verwenden Sie Netsh http, Abfragen und Konfigurieren von HTTP.sys-Einstellungen und Parameter.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: daecc6a385d7aa2c02d1bea02eb0a585a9b33185
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59881791"
---
# <a name="netsh-http-commands"></a>Netsh http-Befehle


Verwendung **Netsh http** Abfragen und Konfigurieren von HTTP.sys-Einstellungen und Parameter.  

>[!TIP]
>Wenn Sie Windows PowerShell auf einem Computer unter Windows Server 2016 oder Windows 10 verwenden, geben Sie **Netsh** und drücken Sie EINGABETASTE. Geben Sie an der Eingabeaufforderung Netsh **http** , und drücken Sie EINGABETASTE, um die Netsh-http-Aufforderung erhalten.
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Netsh http\>

Die verfügbaren Netsh http-Befehle sind:

- [Hinzufügen von iplisten](#add-iplisten)
- [add sslcert](#add-sslcert)
- [Hinzufügen von Timeouts](#add-timeout)
- [Hinzufügen von urlacl](#add-urlacl)
- [Cache löschen](#delete-cache)
- [Delete iplisten](#delete-iplisten)
- [Sslcert löschen](#delete-sslcert)
- [Timeout löschen](#delete-timeout)
- [Delete urlacl](#delete-urlacl)
- [leeren logbuffer](#flush-logbuffer)
- [Cachestate anzeigen](#show-cachestate)
- [Iplisten anzeigen](#show-iplisten)
- [Servicestate anzeigen](#show-servicestate)
- [Sslcert anzeigen](#show-sslcert)
- [Anzeigen von Timeouts](#show-timeout)
- [Urlacl anzeigen](#show-urlacl)

## <a name="add-iplisten"></a>Hinzufügen von iplisten

Fügt eine neue IP-Adresse, die IP-Abhörliste, ausgenommen die Nummer des Ports an.

**Syntax**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**Parameter**
| | | |
|---|---|---|
| **ipaddress** | Abhörliste für die IPv4- oder IPv6-Adresse die IP-Adresse hinzugefügt werden. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu begrenzen, an den der HTTP-Dienst gebunden. "0.0.0.0" bedeutet, dass jede IPv4-Adresse und "::" bedeutet, dass IPv6-Adresse. | Erforderlich |
---

**Beispiele für**

Es folgen vier Beispiele für die **hinzufügen Iplisten** Befehl.

-   Hinzufügen von Iplisten IP-Adresse FE80:: 1 =
-   Fügen Sie die IP-Adresse Iplisten 1.1.1.1 =
-   Hinzufügen von Iplisten IP-Adresse "0.0.0.0" =
-   Fügen Sie die IP-Adresse Iplisten =::

---

## <a name="add-sslcert"></a>Hinzufügen von sslcert

Fügt ein neues SSL-Serverzertifikat, Bindung und das entsprechende Zertifikat Clientrichtlinien für eine IP-Adresse und Port hinzu.

**Syntax**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**Parameter**

| | | |
|---|---|---|
| **ipport**                                   | Gibt die IP-Adresse und Port für die Bindung. Einen Doppelpunkt (:) Dient als Trennzeichen zwischen der IP-Adresse und die Portnummer an.                                              | Erforderlich |
| **certhash**                                 | Gibt den SHA-Hash des Zertifikats an. Dieser Hash 20 Byte lang ist und als hexadezimale Zeichenfolge angegeben ist.                                                                          | Erforderlich |
| **appid**                                    | Gibt die GUID, um die besitzende Anwendung zu identifizieren.                                                                                                                                   | Erforderlich |
| **certstorename**                            | Gibt den Speichernamen für das Zertifikat an. Der Standardwert ist MY. Zertifikat muss im Kontext lokalen Computers gespeichert werden.                                                                   | Optional |
| **verifyclientcertrevocation**               | Gibt an, die aktiviert bzw. deaktiviert die Überprüfung der Zertifikatsperrlisten von Clientzertifikaten.                                                                                                            | Optional |
| **verifyrevocationwithcachedclientcertonly** | Gibt an, ob die Verwendung von nur zwischengespeicherte Clientzertifikat für die Überprüfung der Zertifikatsperrlisten aktiviert oder deaktiviert ist.                                                                            | Optional |
| **usagecheck**                               | Gibt an, ob die Prüfung der Datennutzung aktiviert oder deaktiviert ist. Standardmäßig ist aktiviert.                                                                                                            | Optional |
| **revocationfreshnesstime**                  | Gibt das Zeitintervall in Sekunden, um für eine aktualisierte Zertifikatssperrliste (CRL) zu überprüfen. Wenn dieser Wert 0 (null) ist, klicken Sie dann die neue Zertifikatsperrliste nur aktualisiert, wenn dem Ablauf. | Optional |
| **urlretrievaltimeout**                      | Gibt das Timeout-Intervall (in Millisekunden) nach dem Versuch zum Abrufen der Sperrliste für die remote-URL an.                                                       | Optional |
| **sslctlidentifier**                         | Gibt die Liste der Zertifikataussteller, die vertrauenswürdig sind. Diese Liste kann es sich um eine Teilmenge der Zertifikataussteller sein, die vom Computer als vertrauenswürdig eingestuft werden.                                | Optional |
| **sslctlstorename**                          | Gibt den Namen des Zertifikatspeichers unter LOCAL_MACHINE, wo SslCtlIdentifier gespeichert werden.                                                                                               | Optional |
| **dsmapperusage**                            | Gibt an, ob der DS-Zuordnungen aktiviert oder deaktiviert ist. Standardmäßig ist deaktiviert.                                                                                                                | Optional |
| **clientcertnegotiation**                    | Gibt an, ob die Aushandlung des Zertifikats aktiviert oder deaktiviert ist. Standardmäßig ist deaktiviert.                                                                                            | Optional |
---

**Beispiele für**

Es folgt ein Beispiel für die **hinzufügen Sslcert** Befehl.

add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899- AABBCCDDEEFF}

---

## <a name="add-timeout"></a>Hinzufügen von Timeouts

Fügt ein globales Zeitlimit an den Dienst an.

**Syntax** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**Parameter**
| | |
|---|---|
| **timeouttype** | Der Typ des Timeout für die Einstellung.                                                                        |
| **value**       | Wert für das Timeout (in Sekunden). Wenn der Wert in der Hexadezimalnotation, klicken Sie dann, fügen Sie das Präfix 0 X. |
---

**Beispiele für**

Es folgen zwei Beispiele für die **hinzufügen Timeout** Befehl.

-   add timeout timeouttype=idleconnectiontimeout value=120
-   add timeout timeouttype=headerwaittimeout value=0x40

---

## <a name="add-urlacl"></a>Hinzufügen von urlacl

Fügt eine Reservierung Uniform Resource Locator (URL) hinzu. Mit diesem Befehl reserviert die URL für Konten und Benutzer ohne Administratorrechte. Die DACL kann einen NT-Kontonamen mit den Parametern Lauschen und Delegaten verwenden oder mithilfe einer SDDL-Zeichenfolge angegeben werden.

**Syntax**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**Parameter**
| | | |
|---|---|---|
| **url**       | Gibt an, die den vollqualifizierten Uniform Resource Locator (URL).                                                                                    | Erforderlich |
| **user**      | Gibt den Namen für Benutzer oder eine Benutzergruppe                                                                                                            | Erforderlich |
| **listen**    | Gibt einen der folgenden Werte: Ja: Ermöglicht dem Benutzer um URLs zu registrieren. Dies ist der Standardwert. Nein: Den Benutzer beim Registrieren von URLs zu verweigern. | Optional |
| **delegate**  | Gibt einen der folgenden Werte: Ja: Erlauben Sie dem Benutzer nicht Delegieren von URLs ein: Verweigern Sie den Benutzer aus URLs zu delegieren. Dies ist der Standardwert.   | Optional |
| **sddl**      | Gibt eine SDDL-Zeichenfolge, die beschreibt, die DACL an.                                                                                                | Optional |
---

**Beispiele für**

Es folgen vier Beispiele für die **hinzufügen Urlacl** Befehl.

-   Hinzufügen von Urlacl Url =https://+:80/MyUri Benutzer = DOMAIN\\Benutzer
-   Hinzufügen von Urlacl Url =https://www.contoso.com:80/MyUri Benutzer = DOMAIN\\Benutzer warten = Ja
-   Hinzufügen von Urlacl Url =https://www.contoso.com:80/MyUri Benutzer = DOMAIN\\Benutzerdelegaten = Nein
-   Hinzufügen von Urlacl Url =https://+:80/MyUri Sddl =...

---

## <a name="delete-cache"></a>Cache löschen

Löscht alle Einträge oder eines angegebenen Eintrags, aus dem HTTP-Dienst-Kernel URI-Cache an.

**Syntax**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**Parameter**
| | | |
|---|---|---|
| **url**       | Gibt an, die den vollqualifizierten Locator URL (Uniform Resource), die Sie löschen möchten.                                        | Optional |
| **recursive** | Gibt an, ob alle Einträge unter der Url-Cache entfernt werden. **Ja**: Entfernen Sie alle Einträge **keine**: nicht alle Einträge entfernt | Optional |
---

**Beispiele für**

Es folgen zwei Beispiele für die **Cache löschen** Befehl.

-   Löschen des Cache-Url =https://www.contoso.com:80/myresource/ rekursive = Ja
-   Cache löschen

---

## <a name="delete-iplisten"></a>Delete iplisten

Löscht eine IP-Adresse aus der IP-lauschliste an. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu begrenzen, an den der HTTP-Dienst gebunden.

**Syntax**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**Parameter**
| | | |
|---|---|---|
| **ipaddress** | Abhörliste für die IPv4- oder IPv6-Adresse aus der IP-Adresse gelöscht werden. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu begrenzen, an den der HTTP-Dienst gebunden. "0.0.0.0" bedeutet, dass jede IPv4-Adresse und "::" bedeutet, dass IPv6-Adresse. Dies schließt nicht die Nummer des Ports. | Erforderlich |
---


**Beispiele für**

Es folgen vier Beispiele für die **delete Iplisten** Befehl.

-   Delete Iplisten IP-Adresse FE80:: 1 =
-   Delete Iplisten Ipaddress = 1.1.1.1
-   Delete Iplisten IP-Adresse "0.0.0.0" =
-   Delete Iplisten Ipaddress =::

---

## <a name="delete-sslcert"></a>Sslcert löschen


Werden SSL-zertifikatbindungen für Server und die entsprechende Zertifikat für Clientrichtlinien für eine IP-Adresse und Port gelöscht.

**Syntax**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**Parameter**
| | | |
|---|---|---|
| **ipport** | Gibt die IPv4- oder IPv6-Adresse und Port für die SSL-zertifikatbindungen gelöscht werden. Einen Doppelpunkt (:) Dient als Trennzeichen zwischen der IP-Adresse und die Portnummer an. | Erforderlich |
---


**Beispiele für**

Drei Beispiele für die **löschen Sslcert** Befehl.

- Löschen von Sslcert Ipport = 1.1.1.1:443
- delete sslcert ipport=0.0.0.0:443
- Löschen von Sslcert Ipport = [:]: 443

---

## <a name="delete-timeout"></a>Timeout löschen

Löscht ein globales Zeitlimit und macht den Dienst, der auf die Standardwerte zurückgesetzt.

**Syntax**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**Parameter**
| | | |
|---|---|---|
| **timeouttype** | Gibt den Typ der Timeouteinstellung festgelegt. | Erforderlich |
---


**Beispiele für**

Es folgen zwei Beispiele für die **Timeout löschen** Befehl.

-   Löschen von Timeout Timeouttype Idleconnectiontimeout =
-   delete timeout timeouttype=headerwaittimeout

---

## <a name="delete-urlacl"></a>Delete urlacl

Löscht die URL-Reservierungen.

**Syntax**

```powershell
delete urlacl [ url= ] URL
```

**Parameter**
| | | |
|---|---|---|
| **url** | Gibt an, die den vollqualifizierten Locator URL (Uniform Resource), die Sie löschen möchten. | Erforderlich |
---


**Beispiele für**

Es folgen zwei Beispiele für die **delete Urlacl** Befehl.

-   Delete Urlacl Url =https://+:80/MyUri
-   Delete Urlacl Url =https://www.contoso.com:80/MyUri

---

## <a name="flush-logbuffer"></a>leeren logbuffer

Leert die internen Puffer für die "LogFiles".

**Syntax**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>Cachestate anzeigen

Listen zwischengespeichert URI-Ressourcen und die zugehörigen Eigenschaften. Dieser Befehl listet alle Ressourcen und die zugehörigen Eigenschaften, die im HTTP-Antwort-Cache zwischengespeichert werden, oder zeigt eine einzelne Ressource und die zugehörigen Eigenschaften.

**Syntax**

```powershell
show cachestate [ [url= ] URL]
```

**Parameter**
| | | |
|---|---|---|
| **url** | Gibt die vollqualifizierte URL, die Sie anzeigen möchten. Wenn nicht angegeben ist, zeigen Sie alle URLs. Die URL kann auch ein Präfix für die registrierten URLs sein. | Optional |
---


**Beispiele für**

Es folgen zwei Beispiele für die **anzeigen Cachestate** Befehl:

-   Anzeigen von Cachestate Url =https://www.contoso.com:80/myresource
-   Cachestate anzeigen

---

## <a name="show-iplisten"></a>Iplisten anzeigen

Zeigt alle IP-Adressen in der IP-lauschliste an. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu begrenzen, an den der HTTP-Dienst gebunden. "0.0.0.0" bedeutet, dass jede IPv4-Adresse und "::" bedeutet, dass IPv6-Adresse.

**Syntax**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>Servicestate anzeigen

Zeigt eine Momentaufnahme der HTTP-Dienst.

**Syntax**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**Parameter**
| | | |
|---|---|---|
| **Ansicht**    | Gibt an, ob eine Momentaufnahme des Status des HTTP-Dienstes basierend auf den Server-Sitzung oder die Anforderungswarteschlangen anzuzeigen. | Optional |
| **Verbose** | Gibt an, ob ausführliche Informationen anzuzeigen, die auch die Eigenschafteninformationen zeigt.                               | Optional |
---

**Beispiele für**

Es folgen zwei Beispiele für die **anzeigen Servicestate** Befehl.

-   show servicestate view="session"
-   show servicestate view="requestq"

---

## <a name="show-sslcert"></a>Sslcert anzeigen

Zeigt zertifikatbindungen für Secure Sockets Layer (SSL)-Server und die entsprechenden Zertifikat für Clientrichtlinien für eine IP-Adresse und Port.

**Syntax**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**Parameter**
| | | |
|---|---|---|
| **ipport** | Gibt die IPv4- oder IPv6-Adresse und Port für den das SSL-Zertifikat Bindungen anzeigen. Einen Doppelpunkt (:) Dient als Trennzeichen zwischen der IP-Adresse und die Portnummer an. Wenn Sie Ipport keinen angeben, werden alle Bindungen angezeigt. | Erforderlich |
---


**Beispiele für**

Fünf Beispiele für die **anzeigen Sslcert** Befehl.

-   Anzeigen von Sslcert Ipport = [FE80:: 1]: 443
-   Anzeigen von Sslcert Ipport = 1.1.1.1:443
-   show sslcert ipport=0.0.0.0:443
-   Anzeigen von Sslcert Ipport = [:]: 443
-   Sslcert anzeigen

---

## <a name="show-timeout"></a>Anzeigen von Timeouts

Zeigt an, in Sekunden an, die Timeoutwerte, der den HTTP-Dienst.

**Syntax**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>Urlacl anzeigen

Zeigt Zugriffssteuerungslisten besitzerverwaltete (DACLs) für die angegebene reservierte URL oder alle reservierte URLs.

**Syntax**

```powershell
show urlacl [ [url= ] URL]
```

**Parameter**
| | | |
|---|---|---|
| **url** | Gibt die vollqualifizierte URL, die Sie anzeigen möchten. Wenn wurde nicht angegeben, zeigen Sie alle URLs. | Optional |
---


**Beispiele für**

Drei Beispiele für die **anzeigen Urlacl** Befehl.

-   Anzeigen von Urlacl Url =https://+:80/MyUri
-   Anzeigen von Urlacl Url =https://www.contoso.com:80/MyUri
-   Urlacl anzeigen

---