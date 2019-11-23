---
title: Netsh-Befehle für Hypertext Transfer Protocol (http)
description: Verwenden Sie netsh http zum Abfragen und Konfigurieren von http. sys-Einstellungen und-Parametern.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7b9032eb05128532c8bf90a0db2f685b4435e6eb
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401879"
---
# <a name="netsh-http-commands"></a>Netsh http-Befehle


Verwenden Sie **netsh http** zum Abfragen und Konfigurieren von http. sys-Einstellungen und-Parametern.  

>[!TIP]
>Wenn Sie Windows PowerShell auf einem Computer verwenden, auf dem Windows Server 2016 oder Windows 10 ausgeführt wird, geben Sie **netsh** ein, und drücken Sie die EINGABETASTE. Geben Sie an der netsh-Eingabeaufforderung **http** ein, und drücken Sie die EINGABETASTE, um die netsh http-Eingabeaufforderung
>
>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;netsh http\>

Die folgenden netsh http-Befehle sind verfügbar:

- [iplauschen hinzufügen](#add-iplisten)
- [Hinzufügen von sslcert](#add-sslcert)
- [Timeout hinzufügen](#add-timeout)
- [urlacl hinzufügen](#add-urlacl)
- [Cache löschen](#delete-cache)
- [Löschen von iplauschen](#delete-iplisten)
- [Löschen von sslcert](#delete-sslcert)
- [Timeout für Löschvorgang](#delete-timeout)
- [Löschen von urlacl](#delete-urlacl)
- [logbuffer leeren](#flush-logbuffer)
- [cachestate anzeigen](#show-cachestate)
- [iplauschen anzeigen](#show-iplisten)
- [SERVICESTATE ausgeführt wird anzeigen](#show-servicestate)
- [sslcert anzeigen](#show-sslcert)
- [Timeout anzeigen](#show-timeout)
- [urlacl anzeigen](#show-urlacl)

## <a name="add-iplisten"></a>iplauschen hinzufügen

Fügt der IP-Abhörliste eine neue IP-Adresse ohne die Portnummer hinzu.

**Syntax**

```powershell
add iplisten [ ipaddress= ] IPAddress
```

**Parameters**

|               |                                                                                                                                                                                                                          |          |
|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **IPAddress** | Die IPv4-oder IPv6-Adresse, die der IP-Abhörliste hinzugefügt werden soll. Die IP-Abhörliste wird verwendet, um den Bereich der Liste der Adressen festzustellen, an die der HTTP-Dienst gebunden ist. "0.0.0.0" bezeichnet eine beliebige IPv4-Adresse und "::" eine beliebige IPv6-Adresse. | Erforderlich |

---

**Beispiele**

Im folgenden sind vier Beispiele für den Befehl " **iplauschen hinzufügen** " aufgeführt.

-   IP-Adress Verwaltungs-IP-Adresse = FE80:: 1 hinzufügen
-   iplauschen IPAddress = 1.1.1.1 hinzufügen
-   iplauschen IPAddress = 0.0.0.0 hinzufügen
-   Fügen Sie iplauschen IPAddress =::

---

## <a name="add-sslcert"></a>Hinzufügen von sslcert

Fügt eine neue SSL-Serverzertifikat Bindung und entsprechende Client Zertifikat Richtlinien für eine IP-Adresse und einen Port hinzu.

**Syntax**

```powershell
add sslcert [ ipport= ] IPAddress:port [ certhash= ] CertHash [ appid= ] GUID [ [ certstorename= ] CertStoreName [ verifyclientcertrevocation= ] enable | disable [verifyrevocationwithcachedclientcertonly= ] enable | disable [ usagecheck= ] enable | disable [ revocationfreshnesstime= ] U-Int [ urlretrievaltimeout= ] U-Int [sslctlidentifier= ] SSLCTIdentifier [ sslctlstorename= ] SLCtStoreName [ dsmapperusage= ] enable | disable [ clientcertnegotiation= ] enable | disable ] ]
```

**Parameters**


|                                              |                                                                                                                                                                                          |          |
|----------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|                  **IPPort**                  |                       Gibt die IP-Adresse und den Port für die Bindung an. Ein Doppelpunkt (:) wird als Trennzeichen zwischen der IP-Adresse und der Portnummer verwendet.                        | Erforderlich |
|                 **CertHash**                 |                                     Gibt den SHA-Hash des Zertifikats an. Dieser Hash ist 20 Byte lang und wird als hexadezimale Zeichenfolge angegeben.                                      | Erforderlich |
|                  **appid**                   |                                                                  Gibt die GUID zum Identifizieren der besitzenden Anwendung an.                                                                  | Erforderlich |
|              **certstorename**               |                                  Gibt den Speicher Namen für das Zertifikat an. Der Standardwert ist My. Das Zertifikat muss im Kontext des lokalen Computers gespeichert werden.                                  | Optional |
|        **verifyclientcertrevocation**        |                                                      Gibt an, dass die Sperrung von Client Zertifikaten durch ein-und ausgeschaltet wird.                                                       | Optional |
| **verifyrevocationwithcachedclientcertonly** |                                      Gibt an, ob die Verwendung eines zwischengespeicherten Client Zertifikats für die Sperr Überprüfung aktiviert oder deaktiviert ist.                                       | Optional |
|                **usagecheck**                |                                                      Gibt an, ob die Verwendungs Überprüfung aktiviert oder deaktiviert ist. Der Standardwert ist aktiviert.                                                       | Optional |
|         **RevocationFreshnessTime**          | Gibt das Zeitintervall (in Sekunden) für die Überprüfung auf eine aktualisierte Zertifikat Sperr Liste (CRL) an. Wenn dieser Wert 0 (null) ist, wird die neue Zertifikat Sperr Liste nur aktualisiert, wenn die vorherige abgelaufen ist. | Optional |
|           **UrlRetrievalTimeout**            |                            Gibt das Timeout Intervall (in Millisekunden) nach dem Versuch an, die Zertifikat Sperr Liste für die Remote-URL abzurufen.                            | Optional |
|             **sslctlidentifier**             |                Gibt die Liste der Zertifikat Aussteller an, denen vertraut werden kann. Diese Liste kann eine Teilmenge der Zertifikat Aussteller sein, die vom Computer als vertrauenswürdig eingestuft werden.                 | Optional |
|             **SslCtlStoreName**              |                                                Gibt den Namen des Zertifikat Speicher unter LOCAL_MACHINE an, in dem sslctlidentifier gespeichert ist.                                                | Optional |
|              **dsmapperusage**               |                                                        Gibt an, ob DS-Mapper aktiviert oder deaktiviert sind. Der Standardwert ist deaktiviert.                                                         | Optional |
|          **clientcertaushandlung**           |                                              Gibt an, ob die Aushandlung des Zertifikats aktiviert oder deaktiviert ist. Der Standardwert ist deaktiviert.                                               | Optional |

---

**Beispiele**

Im folgenden finden Sie ein Beispiel für den Befehl " **sslcert hinzufügen** ".

Fügen Sie sslcert IPPort = 1.1.1.1:443 CertHash = 0102030405060708090a0b0c0d0e0f 1011121314 AppID = {00112233-4455-6677-8899-aabbccddeeff} hinzu.

---

## <a name="add-timeout"></a>Timeout hinzufügen

Fügt dem Dienst ein globales Timeout hinzu.

**Syntax** 

```powershell
add timeout [ timeouttype= ] IdleConnectionTimeout | HeaderWaitTimeout [ value=] U-Short
```

**Parameters**

|                 |                                                                                                     |
|-----------------|-----------------------------------------------------------------------------------------------------|
| **timeouttype** |                                    Der Typ des Timeouts für die Einstellung.                                     |
|    **value**    | Der Wert des Timeouts (in Sekunden). Wenn der Wert in Hexadezimal Schreibweise angegeben ist, fügen Sie das Präfix 0x hinzu. |

---

**Beispiele**

Im folgenden finden Sie zwei Beispiele für den Befehl **Timeout hinzufügen** .

-   Timeout timeouttype = idleconnectiontimeout Wert = 120 hinzufügen
-   Timeout timeouttype = HeaderWaitTimeout Wert = 0x40 hinzufügen

---

## <a name="add-urlacl"></a>urlacl hinzufügen

Fügt einen Uniform Resource Locator (URL)-Reservierungs Eintrag hinzu. Dieser Befehl reserviert die URL für Benutzer und Konten ohne Administratorrechte. Die DACL kann mithilfe eines NT-Konto namens mit den Abhör-und delegatparametern oder mithilfe einer SDDL-Zeichenfolge angegeben werden.

**Syntax**

```powershell
add urlacl [ url= ] URL [ [user=] User [ [ listen= ] yes | no [ delegate= ] yes | no ] | [ sddl= ] SDDL ]
```

**Parameters**

|              |                                                                                                                                                  |          |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|
|   **url**    |                                          Gibt den voll qualifizierten Uniform Resource Locator (URL) an.                                           | Erforderlich |
|   **user**   |                                                      Gibt den Namen des Benutzers oder der Benutzergruppe an.                                                       | Erforderlich |
|  **hin**  | Gibt einen der folgenden Werte an: Ja: erlauben Sie dem Benutzer das Registrieren von URLs. Dies ist der Standardwert. Nein: verweigert dem Benutzer das Registrieren von URLs. | Optional |
| **Führers** |  Gibt einen der folgenden Werte an: Ja: dem Benutzer gestatten, URLs zu delegieren Nein: verweigert dem Benutzer die Delegierung von URLs. Dies ist der Standardwert.  | Optional |
|   **SDDL**   |                                                Gibt eine SDDL-Zeichenfolge an, die die DACL beschreibt.                                                 | Optional |

---

**Beispiele**

Im folgenden sind vier Beispiele für den Befehl " **urlacl hinzufügen** " aufgeführt.

- add urlacl URL =https://+:80/MyUri User = Domäne\\Benutzer
- add urlacl URL =<https://www.contoso.com:80/MyUri> User = Domain\\User lauschen = Yes
- add urlacl URL =<https://www.contoso.com:80/MyUri> User = Domain\\User Delegat = No
- add urlacl URL =https://+:80/MyUri SDDL =...

---

## <a name="delete-cache"></a>Cache löschen

Löscht alle Einträge oder einen angegebenen Eintrag aus dem HTTP-Dienst-Kernel-URI-Cache.

**Syntax**

```powershell
delete cache [ [ url= ] URL [ [recursive= ] yes | no ]
```

**Parameters**

|               |                                                                                                                              |          |
|---------------|------------------------------------------------------------------------------------------------------------------------------|----------|
|    **url**    |                    Gibt den voll qualifizierten Uniform Resource Locator (URL) an, den Sie löschen möchten.                     | Optional |
| **rekursive** | Gibt an, ob alle Einträge im URL-Cache entfernt werden. **Ja**: alle Einträge entfernen **Nein**: alle Einträge nicht entfernen | Optional |

---

**Beispiele**

Im folgenden finden Sie zwei Beispiele für den Befehl **Cache löschen** .

- Cache-URL löschen =<https://www.contoso.com:80/myresource/> rekursiv = ja
- Cache löschen

---

## <a name="delete-iplisten"></a>Löschen von iplauschen

Löscht eine IP-Adresse aus der IP-Abhörliste. Die IP-Abhörliste wird verwendet, um den Bereich der Liste der Adressen festzustellen, an die der HTTP-Dienst gebunden ist.

**Syntax**

```powershell
delete iplisten [ ipaddress= ] IPAddress
```

**Parameters**

|               |                                                                                                                                                                                                                                                                     |          |
|---------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **IPAddress** | Die IPv4-oder IPv6-Adresse, die aus der IP-Abhörliste gelöscht werden soll. Die IP-Abhörliste wird verwendet, um den Bereich der Liste der Adressen festzustellen, an die der HTTP-Dienst gebunden ist. "0.0.0.0" bezeichnet eine beliebige IPv4-Adresse und "::" eine beliebige IPv6-Adresse. Dies schließt nicht die Portnummer ein. | Erforderlich |

---


**Beispiele**

Im folgenden sind vier Beispiele für den Befehl " **iplauschen löschen** " aufgeführt.

-   Löschen von iplistener IPAddress = FE80:: 1
-   Löschen von iplistener IPAddress = 1.1.1.1
-   Löschen von iplistener IPAddress = 0.0.0.0
-   Löschen Sie iplistener IPAddress =::

---

## <a name="delete-sslcert"></a>Löschen von sslcert


Löscht SSL-Serverzertifikat Bindungen und entsprechende Client Zertifikat Richtlinien für eine IP-Adresse und einen Port.

**Syntax**

```powershell
delete sslcert [ ipport= ] IPAddress:port
```

**Parameters**

|            |                                                                                                                                                                                          |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **IPPort** | Gibt die IPv4-oder IPv6-Adresse und den Port an, für die die SSL-Zertifikat Bindungen gelöscht werden. Ein Doppelpunkt (:) wird als Trennzeichen zwischen der IP-Adresse und der Portnummer verwendet. | Erforderlich |

---


**Beispiele**

Im folgenden sind drei Beispiele für den Befehl " **sslcert löschen** " aufgeführt.

- Löschen von sslcert IPPort = 1.1.1.1:443
- Löschen von sslcert IPPort = 0.0.0.0:443
- Löschen Sie sslcert IPPort = [::]: 443.

---

## <a name="delete-timeout"></a>Timeout für Löschvorgang

Löscht ein globales Timeout und macht den Dienst auf die Standardwerte zurück.

**Syntax**

```powershell
delete timeout [ timeouttype= ] idleconnectiontimeout | headerwaittimeout
```

**Parameters**

|                 |                                        |          |
|-----------------|----------------------------------------|----------|
| **timeouttype** | Gibt den Typ der Timeout Einstellung an. | Erforderlich |

---


**Beispiele**

Im folgenden sind zwei Beispiele des Befehls **Delete Timeout** aufgeführt.

-   Timeout timeouttype = idleconnectiontimeout für DELETE
-   Timeout für Timeout timeouttype = HeaderWaitTimeout

---

## <a name="delete-urlacl"></a>Löschen von urlacl

Löscht URL-Reservierungen.

**Syntax**

```powershell
delete urlacl [ url= ] URL
```

**Parameters**

|         |                                                                                       |          |
|---------|---------------------------------------------------------------------------------------|----------|
| **url** | Gibt den voll qualifizierten Uniform Resource Locator (URL) an, den Sie löschen möchten. | Erforderlich |

---


**Beispiele**

Im folgenden sind zwei Beispiele für den Befehl " **urlacl löschen** " aufgeführt.

- urlacl-URL löschen =https://+:80/MyUri
- urlacl-URL löschen =<https://www.contoso.com:80/MyUri>

---

## <a name="flush-logbuffer"></a>logbuffer leeren

Leert die internen Puffer für die Protokolldateien.

**Syntax**

```powershell
flush logbuffer
```

---

## <a name="show-cachestate"></a>cachestate anzeigen

Listet zwischengespeicherte URI-Ressourcen und die zugehörigen Eigenschaften auf. Mit diesem Befehl werden alle Ressourcen und die zugehörigen Eigenschaften aufgelistet, die im HTTP-Antwort Cache zwischengespeichert werden, oder es werden eine einzelne Ressource und die zugehörigen Eigenschaften angezeigt.

**Syntax**

```powershell
show cachestate [ [url= ] URL]
```

**Parameters**

|         |                                                                                                                                                    |          |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **url** | Gibt die voll qualifizierte URL an, die Sie anzeigen möchten. Wenn nichts angegeben ist, zeigen Sie alle URLs an. Die URL könnte auch ein Präfix für registrierte URLs sein. | Optional |

---


**Beispiele**

Im folgenden sind zwei Beispiele für den Befehl " **cachestate anzeigen** " aufgeführt:

- Cache Estate URL anzeigen =<https://www.contoso.com:80/myresource>
- cachestate anzeigen

---

## <a name="show-iplisten"></a>iplauschen anzeigen

Zeigt alle IP-Adressen in der IP-Abhörliste an. Die IP-Abhörliste wird verwendet, um den Bereich der Liste der Adressen festzustellen, an die der HTTP-Dienst gebunden ist. "0.0.0.0" bezeichnet eine beliebige IPv4-Adresse und "::" eine beliebige IPv6-Adresse.

**Syntax**

```powershell
show iplisten
```

---

## <a name="show-servicestate"></a>SERVICESTATE ausgeführt wird anzeigen

Zeigt eine Momentaufnahme des http-Dienes an.

**Syntax**
```powershell
show servicestate [ [ view= ] session | requestq ] [ [ verbose= ] yes | no ]
```

**Parameters**

|             |                                                                                                                      |          |
|-------------|----------------------------------------------------------------------------------------------------------------------|----------|
|  **Ansicht**   | Gibt an, ob eine Momentaufnahme des HTTP-Dienst Zustands basierend auf der Server Sitzung oder in den Anforderungs Warteschlangen angezeigt werden soll. | Optional |
| **Ausführliche** |                Gibt an, ob ausführliche Informationen angezeigt werden sollen, in denen auch Eigenschafts Informationen angezeigt werden.                | Optional |

---

**Beispiele**

Im folgenden finden Sie zwei Beispiele für den Befehl **Show SERVICESTATE ausgeführt wird** .

-   SERVICESTATE ausgeführt wird View = "Session" anzeigen
-   SERVICESTATE ausgeführt wird View = "requestq" anzeigen

---

## <a name="show-sslcert"></a>sslcert anzeigen

Zeigt Secure Sockets Layer (SSL)-Serverzertifikat Bindungen und entsprechende Client Zertifikat Richtlinien für eine IP-Adresse und einen Port an.

**Syntax**

```powershell
show sslcert [ ipport= ] IPAddress:port
```

**Parameters**

|            |                                                                                                                                                                                                                                                |          |
|------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|
| **IPPort** | Gibt die IPv4-oder IPv6-Adresse und den Port an, für die die SSL-Zertifikat Bindungen angezeigt werden. Ein Doppelpunkt (:) wird als Trennzeichen zwischen der IP-Adresse und der Portnummer verwendet. Wenn Sie IPPort nicht angeben, werden alle Bindungen angezeigt. | Erforderlich |

---


**Beispiele**

Im folgenden sind fünf Beispiele für den Befehl " **sslcert anzeigen** " aufgeführt.

-   sslcert IPPort = [fe80:: 1]: 443 anzeigen
-   sslcert IPPort = 1.1.1.1:443 anzeigen
-   sslcert IPPort = 0.0.0.0:443 anzeigen
-   sslcert IPPort = [::]: 443 anzeigen
-   sslcert anzeigen

---

## <a name="show-timeout"></a>Timeout anzeigen

Zeigt die Timeout Werte für den HTTP-Dienst in Sekunden an.

**Syntax**

```powershell
show timeout
```

---

## <a name="show-urlacl"></a>urlacl anzeigen

Zeigt freigegebene Zugriffs Steuerungs Listen (DACLs) für die angegebene reservierte URL oder alle reservierten URLs an.

**Syntax**

```powershell
show urlacl [ [url= ] URL]
```

**Parameters**

|         |                                                                                                |          |
|---------|------------------------------------------------------------------------------------------------|----------|
| **url** | Gibt die voll qualifizierte URL an, die Sie anzeigen möchten. Wenn keine Spezifikationen angezeigt werden, zeigen Sie alle URLs an. | Optional |

---


**Beispiele**

Im folgenden sind drei Beispiele für den Befehl **show urlacl** aufgeführt.

- urlacl-URL anzeigen =https://+:80/MyUri
- urlacl-URL anzeigen =<https://www.contoso.com:80/MyUri>
- urlacl anzeigen

---