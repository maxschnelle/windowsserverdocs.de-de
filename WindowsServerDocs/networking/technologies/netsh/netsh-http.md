---
title: Netsh-Befehle für HTTP (Hypertext Transfer Protocol)
description: Verwende „netsh http“, um HTTP.sys-Einstellungen und -Parameter abzufragen und zu konfigurieren.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 2c1032812f52eb32d9ae12310c8f2cff03f70aa5
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80309379"
---
# <a name="netsh-http-commands"></a>Netsh http-Befehle


Verwende **netsh http**, um HTTP.sys-Einstellungen und -Parameter abzufragen und zu konfigurieren.  

>[!TIP]
>Wenn du Windows PowerShell auf einem Computer mit Windows Server 2016 oder Windows 10 verwendest, gib **netsh** ein und drücke die EINGABETASTE. Gib an der Netsh-Eingabeaufforderung **http** ein und drücke die EINGABETASTE, um die „netsh http“-Eingabeaufforderung zu erhalten.
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

Die verfügbaren netsh http-Befehle sind:

- [add iplisten](#add-iplisten)
- [add sslcert](#add-sslcert)
- [add timeout](#add-timeout)
- [add urlacl](#add-urlacl)
- [delete cache](#delete-cache)
- [delete iplisten](#delete-iplisten)
- [delete sslcert](#delete-sslcert)
- [delete timeout](#delete-timeout)
- [delete urlacl](#delete-urlacl)
- [flush logbuffer](#flush-logbuffer)
- [show cachestate](#show-cachestate)
- [show iplisten](#show-iplisten)
- [show servicestate](#show-servicestate)
- [show sslcert](#show-sslcert)
- [show timeout](#show-timeout)
- [show urlacl](#show-urlacl)

## <a name="add-iplisten"></a>add iplisten

Fügt der IP-Abhörliste eine neue IP-Adresse hinzu, wobei die Portnummer nicht berücksichtigt wird.

**Syntax**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**Parameters**

|               |                                                                                                                                                                                                                          |          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | Die IPv4- oder IPv6-Adresse, die der IP-Abhörliste hinzugefügt werden soll. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu erweitern, an die der HTTP-Dienst gebunden ist. „0.0.0.0“ bedeutet eine beliebige IPv4-Adresse und „::“ bedeutet eine beliebige IPv6-Adresse. | Erforderlich |

---

**Beispiele**

Es folgen vier Beispiele für den Befehl **add iplisten**.

-   add iplisten ipaddress=fe80::1
-   add iplisten ipaddress=1.1.1.1
-   add iplisten ipaddress=0.0.0.0
-   add iplisten ipaddress=::

---

## <a name="add-sslcert"></a>add sslcert

Fügt eine neue SSL-Serverzertifikatsbindung und entsprechende Clientzertifikatsrichtlinien für eine IP-Adresse und einen Port hinzu.

**Syntax**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**Parameters**


|                                              |                                                                                                                                                                                          |          |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|                  **ipport**                  |                       Gibt die IP-Adresse und den Port für die Bindung an. Ein Doppelpunkt (:) wird als Trennzeichen zwischen der IP-Adresse und der Portnummer verwendet.                        | Erforderlich |
|                 **certhash**                 |                                     Gibt den SHA-Hash des Zertifikats an. Dieser Hash ist 20 Byte lang und wird als hexadezimale Zeichenfolge angegeben.                                      | Erforderlich |
|                  **appid**                   |                                                                  Gibt die GUID zum Identifizieren der besitzenden Anwendung an.                                                                  | Erforderlich |
|              **certstorename**               |                                  Gibt den Speichernamen für das Zertifikat an. Die Standardeinstellung ist MY. Das Zertifikat muss im Kontext des lokalen Computers gespeichert werden.                                  | Optional |
|        **verifyclientcertrevocation**        |                                                      Gibt die Aktivierung/Deaktivierung der Überprüfung der Sperrung von Clientzertifikaten an.                                                       | Optional |
| **verifyrevocationwithcachedclientcertonly** |                                      Gibt an, ob die Verwendung eines zwischengespeicherten Clientzertifikats für die Überprüfung der Sperrung aktiviert oder deaktiviert ist.                                       | Optional |
|                **usagecheck**                |                                                      Gibt an, ob die Verwendungsprüfung aktiviert oder deaktiviert ist. Die Standardeinstellung ist „Aktiviert“.                                                       | Optional |
|         **revocationfreshnesstime**          | Gibt das Zeitintervall in Sekunden an, in dem nach einer aktualisierten Zertifikatssperrliste (CRL) gesucht werden soll. Wenn dieser Wert null ist, wird die neue Zertifikatssperrliste nur dann aktualisiert, wenn die vorherige abläuft. | Optional |
|           **urlretrievaltimeout**            |                            Gibt das Timeoutintervall (in Millisekunden) nach dem Versuch an, die Zertifikatssperrliste für die Remote-URL abzurufen.                            | Optional |
|             **sslctlidentifier**             |                Gibt die Liste der Zertifikataussteller an, die vertrauenswürdig sind. Diese Liste kann eine Teilmenge der Zertifikatsaussteller sein, denen der Computer vertraut.                 | Optional |
|             **sslctlstorename**              |                                                Gibt den Namen des Zertifikatspeichers unter LOCAL_MACHINE an, wo „SslCtlIdentifier“ gespeichert ist.                                                | Optional |
|              **dsmapperusage**               |                                                        Gibt an, ob DS-Mapper aktiviert oder deaktiviert sind. Die Standardeinstellung ist „Deaktiviert“.                                                         | Optional |
|          **clientcertnegotiation**           |                                              Gibt an, ob die Aushandlung des Zertifikats aktiviert oder deaktiviert ist. Die Standardeinstellung ist „Deaktiviert“.                                               | Optional |

---

**Beispiele**

Es folgt ein Beispiel für den Befehl **add sslcert**.

add sslcert ipport=1.1.1.1:443 certhash=0102030405060708090A0B0C0D0E0F1011121314 appid={00112233-4455-6677-8899- AABBCCDDEEFF}

---

## <a name="add-timeout"></a>add timeout

Fügt dem Dienst eine globale Zeitüberschreitung hinzu.

**Syntax** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**Parameters**

|                 |                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **timeouttype** |                                    Der Typ der Zeitüberschreitung für die Einstellung.                                     |
|    **value**    | Wert der Zeitüberschreitung (in Sekunden). Wenn der Wert in Hexadezimalnotation vorliegt, füge das Präfix 0x hinzu. |

---

**Beispiele**

Es folgen zwei Beispiele für den Befehl **add timeout**.

-   add timeout timeouttype=idleconnectiontimeout value=120
-   add timeout timeouttype=headerwaittimeout value=0x40

---

## <a name="add-urlacl"></a>add urlacl

Fügt einen URL-Reservierungseintrag (Uniform Resource Locator) hinzu. Dieser Befehl reserviert die URL für Nicht-Administratorbenutzer und -konten. Die DACL kann durch die Verwendung eines NT-Kontonamens mit den listen- und delegate-Parametern oder durch die Verwendung einer SDDL-Zeichenfolge angegeben werden.

**Syntax**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**Parameters**

|              |                                                                                                                                                  |          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|   **url**    |                                          Gibt die vollqualifizierte URL (Uniform Resource Locator) an.                                           | Erforderlich |
|   **user**   |                                                      Gibt den Namen des Benutzers oder der Benutzergruppe an.                                                       | Erforderlich |
|  **listen**  | Gibt einen der folgenden Werte an: yes: Ermöglicht dem Benutzer das Registrieren von URLs. Dies ist der Standardwert. no: Verweigert dem Benutzer das Registrieren von URLs. | Optional |
| **delegate** |  Gibt einen der folgenden Werte an: yes: Ermöglicht dem Benutzer das Delegieren von URLs. no: Verweigert dem Benutzer das Delegieren von URLs. Dies ist der Standardwert.  | Optional |
|   **sddl**   |                                                Gibt eine SDDL-Zeichenfolge an, die die DACL beschreibt.                                                 | Optional |

---

**Beispiele**

Es folgen vier Beispiele für den Befehl **add urlacl**.

- add urlacl url=https://+:80/MyUri user=DOMAIN\\ user
- add urlacl url=<https://www.contoso.com:80/MyUri> user=DOMAIN\\user listen=yes
- add urlacl url=<https://www.contoso.com:80/MyUri> user=DOMAIN\\user delegate=no
- add urlacl url=https://+:80/MyUri sddl=...

---

## <a name="delete-cache"></a>delete cache

Löscht alle Einträge oder einen angegebenen Eintrag aus dem Kernel-URI-Cache des HTTP-Diensts.

**Syntax**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**Parameters**

|               |                                                                                                                              |          |
|---------------|------------------------------------------------------------------------------------------------------------------------------|----------|
|    **url**    |                    Gibt die zu löschende vollqualifizierte URL (Uniform Resource Locator) an.                     | Optional |
| **recursive** | Gibt an, ob alle Einträge unter dem URL-Cache entfernt werden. **yes**: alle Einträge entfernen. **no**: nicht alle Einträge entfernen. | Optional |

---

**Beispiele**

Es folgen zwei Beispiele für den Befehl **delete cache**.

- delete cache url=<https://www.contoso.com:80/myresource/> recursive=yes
- delete cache

---

## <a name="delete-iplisten"></a>delete iplisten

Löscht eine IP-Adresse aus der IP-Abhörliste. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu erweitern, an die der HTTP-Dienst gebunden ist.

**Syntax**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**Parameters**

|               |                                                                                                                                                                                                                                                                     |          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipaddress** | Die IPv4- oder IPv6-Adresse, die aus der IP-Abhörliste entfernt werden soll. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu erweitern, an die der HTTP-Dienst gebunden ist. „0.0.0.0“ bedeutet eine beliebige IPv4-Adresse und „::“ bedeutet eine beliebige IPv6-Adresse. Dies schließt nicht die Portnummer ein. | Erforderlich |

---


**Beispiele**

Es folgen vier Beispiele für den Befehl **delete iplisten**.

-   delete iplisten ipaddress=fe80::1
-   delete iplisten ipaddress=1.1.1.1
-   delete iplisten ipaddress=0.0.0.0
-   delete iplisten ipaddress=::

---

## <a name="delete-sslcert"></a>delete sslcert


Löscht eine SSL-Serverzertifikatsbindung und entsprechende Clientzertifikatsrichtlinien für eine IP-Adresse und einen Port.

**Syntax**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**Parameters**

|            |                                                                                                                                                                                          |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | Gibt die IPv4-oder IPv6-Adresse und den Port an, für die die SSL-Zertifikatsbindungen gelöscht werden. Ein Doppelpunkt (:) wird als Trennzeichen zwischen der IP-Adresse und der Portnummer verwendet. | Erforderlich |

---


**Beispiele**

Es folgen drei Beispiele für den Befehl **delete sslcert**.

- delete sslcert ipport=1.1.1.1:443
- delete sslcert ipport=0.0.0.0:443
- delete sslcert ipport=[::]:443

---

## <a name="delete-timeout"></a>delete timeout

Löscht eine globale Zeitüberschreitung und lässt den Dienst auf die Standardwerte zurückkehren.

**Syntax**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**Parameters**

|                 |                                        |          |
|-----------------|----------------------------------------|----------|
| **timeouttype** | Gibt den Typ der Einstellung für die Zeitüberschreitung an. | Erforderlich |

---


**Beispiele**

Es folgen zwei Beispiele für den Befehl **delete timeout**.

-   delete timeout timeouttype=idleconnectiontimeout
-   delete timeout timeouttype=headerwaittimeout

---

## <a name="delete-urlacl"></a>delete urlacl

Löscht URL-Reservierungen.

**Syntax**

```powershell
delete urlacl [ url= ] URL
```

**Parameters**

|         |                                                                                       |          |
|---------|---------------------------------------------------------------------------------------|----------|
| **url** | Gibt die zu löschende vollqualifizierte URL (Uniform Resource Locator) an. | Erforderlich |

---


**Beispiele**

Es folgen zwei Beispiele für den Befehl **delete urlacl**.

- delete urlacl url=https://+:80/MyUri
- delete urlacl url=<https://www.contoso.com:80/MyUri>

---

## <a name="flush-logbuffer"></a>flush logbuffer

Leert die internen Puffer für die Protokolldateien.

**Syntax**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>show cachestate

Listet zwischengespeicherte URI-Ressourcen und die zugehörigen Eigenschaften auf. Dieser Befehl listet alle Ressourcen und ihre zugehörigen Eigenschaften auf, die im HTTP-Antwortcache zwischengespeichert sind, oder zeigt eine einzelne Ressource und ihre zugehörigen Eigenschaften an.

**Syntax**

```powershell
show cachestate [ [url= ] URL]
```

**Parameters**

|         |                                                                                                                                                    |          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **url** | Gibt die anzuzeigende vollqualifizierte URL an. Wenn nicht angegeben, werden alle URLs angezeigt. Die URL könnte auch ein Präfix für registrierte URLs sein. | Optional |

---


**Beispiele**

Es folgen zwei Beispiele für den Befehl **show cachestate**:

- show cachestate url=<https://www.contoso.com:80/myresource>
- show cachestate

---

## <a name="show-iplisten"></a>show iplisten

Zeigt alle IP-Adressen in der IP-Abhörliste an. Die IP-Abhörliste wird verwendet, um die Liste der Adressen zu erweitern, an die der HTTP-Dienst gebunden ist. „0.0.0.0“ bedeutet eine beliebige IPv4-Adresse und „::“ bedeutet eine beliebige IPv6-Adresse.

**Syntax**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>show servicestate

Zeigt eine Momentaufnahme des HTTP-Diensts an.

**Syntax**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**Parameters**

|             |                                                                                                                      |          |
|-------------|----------------------------------------------------------------------------------------------------------------------|----------|
|  **Ansicht**   | Gibt an, ob eine Momentaufnahme des HTTP-Dienstzustands basierend auf der Serversitzung oder auf den Anforderungswarteschlangen angezeigt werden soll. | Optional |
| **Verbose** |                Gibt an, ob ausführliche Informationen angezeigt werden sollen, in denen auch Eigenschaftsinformationen angezeigt werden.                | Optional |

---

**Beispiele**

Es folgen zwei Beispiele für den Befehl **show servicestate**.

-   show servicestate view="session"
-   show servicestate view="requestq"

---

## <a name="show-sslcert"></a>show sslcert

Zeigt SSL-Serverzertifikatsbindungen (Secure Sockets Layer) und entsprechende Clientzertifikatsrichtlinien für eine IP-Adresse und einen Port an.

**Syntax**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**Parameters**

|            |                                                                                                                                                                                                                                                |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **ipport** | Gibt die IPv4-oder IPv6-Adresse und den Port an, für die die SSL-Zertifikatsbindungen angezeigt werden. Ein Doppelpunkt (:) wird als Trennzeichen zwischen der IP-Adresse und der Portnummer verwendet. Wenn „ipport“ nicht angegeben wird, werden alle Bindungen angezeigt. | Erforderlich |

---


**Beispiele**

Es folgen fünf Beispiele für den Befehl **show sslcert**.

-   show sslcert ipport=[fe80::1]:443
-   show sslcert ipport=1.1.1.1:443
-   show sslcert ipport=0.0.0.0:443
-   show sslcert ipport=[::]:443
-   show sslcert

---

## <a name="show-timeout"></a>show timeout

Zeigt die Zeitüberschreitungswerte des HTTP-Diensts in Sekunden an.

**Syntax**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>show urlacl

Zeigt freigegebene Zugriffssteuerungslisten (DACLs) für die angegebene reservierte URL oder alle reservierten URLs an.

**Syntax**

```powershell
show urlacl [ [url= ] URL]
```

**Parameters**

|         |                                                                                                |          |
|---------|------------------------------------------------------------------------------------------------|----------|
| **url** | Gibt die anzuzeigende vollqualifizierte URL an. Wenn nicht angegeben, werden alle URLs angezeigt. | Optional |

---


**Beispiele**

Es folgen drei Beispiele für den Befehl **show urlacl**.

- show urlacl url=https://+:80/MyUri
- show urlacl url=<https://www.contoso.com:80/MyUri>
- show urlacl

---