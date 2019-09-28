---
title: Netsh-Befehle für Schnittstelle Portproxy
description: Verwenden Sie die Portproxy-Befehle von Netsh Interface als Proxys zwischen IPv4-und IPv6-Netzwerken und-Anwendungen.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 6244213ea689f07230ce53288e52959972112037
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405502"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh Interface Portproxy-Befehle

Verwenden Sie die Portproxy-Befehle von **Netsh Interface als Proxys** zwischen IPv4-und IPv6-Netzwerken und-Anwendungen. Sie können diese Befehle verwenden, um den Proxy Dienst auf folgende Weise einzurichten:

-   Von IPv4 konfigurierte Computer-und Anwendungs Nachrichten, die an andere mit IPv4 konfigurierte Computer und Anwendungen gesendet werden.

-   Von IPv4 konfigurierte Computer-und Anwendungs Nachrichten, die an IPv6-konfigurierte Computer und Anwendungen gesendet werden.

-   Von IPv6 konfigurierte Computer-und Anwendungs Nachrichten, die an von IPv4 konfigurierte Computer und Anwendungen gesendet werden.

-   Von IPv6 konfigurierte Computer-und Anwendungs Nachrichten, die an andere von IPv6 konfigurierte Computer und Anwendungen gesendet werden.

Beim Schreiben von Batch Dateien oder Skripts mit diesen Befehlen muss jeder Befehl mit **Netsh Interface Portproxy**beginnen. Wenn Sie z. b. den Befehl **delete v4tov6** verwenden, um anzugeben, dass der Portproxy-Server einen IPv4-Port und eine Adresse aus der Liste der IPv4-Adressen löscht, für die der Server lauscht, muss die Batchdatei bzw. das Skript die folgende Syntax verwenden:

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

Die folgenden Netsh Interface-portproxybefehle sind verfügbar:

-   [v4tov4 hinzufügen](#add-v4tov4)

-   [v4tov6 hinzufügen](#add-v4tov6)

-   [v6tov4 hinzufügen](#add-v6tov4)

-   [v6tov6 hinzufügen](#add-v6tov6)

-   [v4tov4 löschen](#delete-v4tov4)

-   [v4tov6 löschen](#delete-v4tov6)

-   [v6tov6 löschen](#delete-v6tov6)

-   [Festlegen](#reset)

-   [v4tov4 festlegen](#set-v4tov4)

-   [v4tov6 festlegen](#set-v4tov6)

-   [setv6tov4](#set-v6tov4)

-   [v6tov6 festlegen](#set-v6tov6)

-   [Alle anzeigen](#show-all)

-   [v4tov4 anzeigen](#show-v4tov4)

-   [v4tov6 anzeigen](#show-v4tov6)

-   [v6tov4 anzeigen](#show-v6tov4)

-   [v6tov6 anzeigen](#show-v6tov6)


## <a name="add-v4tov4"></a>v4tov4 hinzufügen

Der Port Proxy Server lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv4-Adresse gesendet werden, und ordnet einen Port und eine IPv4-Adresse zu, um die Nachrichten zu senden, die nach dem Einrichten

### <a name="syntax"></a>Syntax

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv4-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv4-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="add-v4tov6"></a>v4tov6 hinzufügen

Der Portproxy-Server lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv4-Adresse gesendet werden, und ordnet einen Port und eine IPv6-Adresse zu, um die Nachrichten zu senden, die nach dem Einrichten

### <a name="syntax"></a>Syntax

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv4-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv6-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv4-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer.  |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="add-v6tov4"></a>v6tov4 hinzufügen

Der Port Proxy Server lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv6-Adresse gesendet werden, und ordnet einen Port und eine IPv4-Adresse zu, an die nach dem Einrichten einer separaten TCP-Verbindung empfangene Nachrichten gesendet

### <a name="syntax"></a>Syntax

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv6-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv6-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer.  |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="add-v6tov6"></a>v6tov6 hinzufügen

Der Port Proxy Server lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv6-Adresse gesendet werden, und ordnet einen Port und eine IPv6-Adresse zu, an die nach dem Einrichten einer separaten TCP-Verbindung empfangene Nachrichten gesendet

### <a name="syntax"></a>Syntax

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv6-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv6-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv6-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer.  |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="delete-v4tov4"></a>v4tov4 löschen

Der Portproxy-Server löscht eine IPv4-Adresse aus der Liste der IPv4-Ports und-Adressen, die der Server überwacht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **ListenPort**   |                                    Gibt den zu löschenden IPv4-Port an.                                    |
| **ListenAddress** | Gibt die zu löschende IPv4-Adresse an. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|   **spezifische**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="delete-v4tov6"></a>v4tov6 löschen

Der Port Proxy Server löscht einen IPv4-Port und eine IPv4-Adresse aus der Liste der IPv4-Adressen, die der Server überwacht.

### <a name="syntax"></a>Syntax

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **ListenPort**   |                                    Gibt den zu löschenden IPv4-Port an.                                    |
| **ListenAddress** | Gibt die zu löschende IPv4-Adresse an. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|   **spezifische**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="delete-v6tov4"></a>v6tov4 löschen

Der Port Proxy Server löscht einen IPv6-Port und eine IPv6-Adresse aus der Liste der IPv6-Adressen, die der Server überwacht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **ListenPort**   |                                    Gibt den zu löschenden IPv6-Port an.                                    |
| **ListenAddress** | Gibt die zu löschende IPv6-Adresse an. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|   **spezifische**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="delete-v6tov6"></a>v6tov6 löschen

Der Portproxy-Server löscht eine IPv6-Adresse aus der Liste der IPv6-Adressen, die der Server überwacht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **ListenPort**   |                                    Gibt den zu löschenden IPv6-Port an.                                    |
| **ListenAddress** | Gibt die zu löschende IPv6-Adresse an. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|   **spezifische**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="reset"></a>Festlegen

Setzt den IPv6-Konfigurations Status zurück.

### <a name="syntax"></a>Syntax

`reset`

## <a name="set-v4tov4"></a>v4tov4 festlegen

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxy-Server, der mit dem Befehl **add v4tov4** erstellt wurde, oder fügt der Liste einen neuen Eintrag hinzu, der Port-/Adress-Paare zuordnet.

### <a name="syntax"></a>Syntax

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv4-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv4-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="set-v4tov6"></a>v4tov6 festlegen

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxy-Server, der mit dem Befehl **Add v4tov6** erstellt wurde, oder fügt der Liste einen neuen Eintrag hinzu, der Port-/Adress-Paare zuordnet.

### <a name="syntax"></a>Syntax

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv4-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv6-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv4-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer.  |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="set-v6tov4"></a>v6tov4 festlegen

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxy-Server, der mit dem Befehl **add v6tov4** erstellt wurde, oder fügt der Liste einen neuen Eintrag hinzu, der Port-/Adress-Paare zuordnet.

### <a name="syntax"></a>Syntax

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                           Gibt den IPv6-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv6-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer.  |
|    **spezifische**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="set-v6tov6"></a>v6tov6 festlegen

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxy-Server, der mit dem Befehl **add v6tov6** erstellt wurde, oder fügt der Liste einen neuen Eintrag hinzu, der Port-/Adress-Paare zuordnet.

### <a name="syntax"></a>Syntax

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **ListenPort**   |                                                            Gibt den IPv6-Port, nach Portnummer oder Dienst Name an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der Standardwert der lokale Computer.  |
|  **connectport**   |        Gibt den IPv6-Port, die Portnummer oder den Dienstnamen an, mit der eine Verbindung hergestellt werden soll. Wenn **connectport** nicht angegeben ist, wird standardmäßig der Wert **ListenPort** auf dem lokalen Computer verwendet.        |
| **ListenAddress**  | Gibt die IPv6-Adresse an, die überwacht werden soll. Zulässige Werte sind IP-Adresse, NetBIOS-Name des Computers oder DNS-Name des Computers. Wenn Sie keine Adresse angeben, ist der Standardwert der lokale Computer. |
|    **spezifische**    |                                                                                   Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="show-all"></a>Anzeigen aller Wiederherstellungspunkte

Zeigt alle Portproxy-Parameter an, einschließlich Port/Adress Paare für v4tov4, v4tov6, v6tov4 und v6tov6.

### <a name="syntax"></a>Syntax

`show all`


## <a name="show-v4tov4"></a>v4tov4 anzeigen

Zeigt v4tov4 Portproxy-Parameter an.

### <a name="syntax"></a>Syntax

`show v4tov4`

## <a name="show-v4tov6"></a>v4tov6 anzeigen

Zeigt v4tov6 Portproxy-Parameter an.

### <a name="syntax"></a>Syntax

`show v4tov6`

## <a name="show-v6tov4"></a>v6tov4 anzeigen

Zeigt v6tov4 Portproxy-Parameter an.

### <a name="syntax"></a>Syntax

`show v6tov4`


## <a name="show-v6tov6"></a>v6tov6 anzeigen

Zeigt v6tov6 Portproxy-Parameter an.

### <a name="syntax"></a>Syntax

`show v6tov6`

---
