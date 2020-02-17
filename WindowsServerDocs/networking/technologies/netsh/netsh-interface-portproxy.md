---
title: Netsh-Befehle für Interface-Portproxy
description: Verwende die Netsh-Befehle für Interface-Portproxy, um als Proxy zwischen IPv4- und IPv6-Netzwerken und -Anwendungen zu fungieren.
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
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405502"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh Interface-Portproxybefehle

Verwende die **Netsh-Befehle für Interface-Portproxy**, um als Proxy zwischen IPv4- und IPv6-Netzwerken und -Anwendungen zu fungieren. Mit diesen Befehlen kannst du einen Proxydienst auf folgende Weise einrichten:

-   IPv4-konfigurierte Computer- und Anwendungsnachrichten, die an andere IPv4-konfigurierte Computer und Anwendungen gesendet werden.

-   IPv4-konfigurierte Computer- und Anwendungsnachrichten, die an IPv6-konfigurierte Computer und Anwendungen gesendet werden.

-   IPv6-konfigurierte Computer- und Anwendungsnachrichten, die an IPv4-konfigurierte Computer und Anwendungen gesendet werden.

-   IPv6-konfigurierte Computer- und Anwendungsnachrichten, die an andere IPv6-konfigurierte Computer und Anwendungen gesendet werden.

Beim Schreiben von Batchdateien oder Skripts mit diesen Befehlen muss jeder Befehl mit **netsh interface portproxy** beginnen. Wenn du z. B. mit dem Befehl **delete v4tov6** angibst, dass der Portproxyserver einen IPv4-Port und eine Adresse aus der Liste der IPv4-Adressen, auf die der Server lauscht, löscht, muss die Batchdatei oder das Skript die folgende Syntax verwenden:

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

Die verfügbaren Netsh Interface-Portproxybefehle sind:

-   [add v4tov4](#add-v4tov4)

-   [add v4tov6](#add-v4tov6)

-   [add v6tov4](#add-v6tov4)

-   [add v6tov6](#add-v6tov6)

-   [delete v4tov4](#delete-v4tov4)

-   [delete v4tov6](#delete-v4tov6)

-   [delete v6tov6](#delete-v6tov6)

-   [reset](#reset)

-   [set v4tov4](#set-v4tov4)

-   [set v4tov6](#set-v4tov6)

-   [setv6tov4](#set-v6tov4)

-   [set v6tov6](#set-v6tov6)

-   [show all](#show-all)

-   [show v4tov4](#show-v4tov4)

-   [show v4tov6](#show-v4tov6)

-   [show v6tov4](#show-v6tov4)

-   [show v6tov6](#show-v6tov6)


## <a name="add-v4tov4"></a>add v4tov4

Der Portproxyserver lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv4-Adresse gesendet werden, und ordnet einen Port und eine IPv4-Adresse zu, um die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindung zu senden.

### <a name="syntax"></a>Syntax

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter


|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv4-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv4-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="add-v4tov6"></a>add v4tov6

Der Portproxyserver lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv4-Adresse gesendet werden, und ordnet einen Port und eine IPv6-Adresse zu, um die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindung zu senden.

### <a name="syntax"></a>Syntax

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv4-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv6-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv4-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer.  |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="add-v6tov4"></a>add v6tov4

Der Portproxyserver lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv6-Adresse gesendet werden, und ordnet einen Port und eine IPv4-Adresse zu, um die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindung zu senden.

### <a name="syntax"></a>Syntax

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv6-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv6-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer.  |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="add-v6tov6"></a>add v6tov6

Der Portproxyserver lauscht auf Nachrichten, die an einen bestimmten Port und eine IPv6-Adresse gesendet werden, und ordnet einen Port und eine IPv6-Adresse zu, um die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindung zu senden.

### <a name="syntax"></a>Syntax

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv6-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv6-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv6-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer.  |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="delete-v4tov4"></a>delete v4tov4

Der Portproxyserver löscht eine IPv4-Adresse aus der Liste der IPv4-Ports und -Adressen, auf die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Gibt den zu löschenden IPv4-Port an.                                    |
| **listenaddress** | Gibt die zu löschende IPv4-Adresse an. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|   **protocol**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="delete-v4tov6"></a>delete v4tov6

Der Portproxyserver löscht einen IPv4-Port und eine IPv4-Adresse aus der Liste der IPv4-Adressen, auf die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Gibt den zu löschenden IPv4-Port an.                                    |
| **listenaddress** | Gibt die zu löschende IPv4-Adresse an. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|   **protocol**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="delete-v6tov4"></a>delete v6tov4

Der Portproxyserver löscht einen IPv6-Port und eine IPv6-Adresse aus der Liste der IPv6-Adressen, auf die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Gibt den zu löschenden IPv6-Port an.                                    |
| **listenaddress** | Gibt die zu löschende IPv6-Adresse an. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|   **protocol**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="delete-v6tov6"></a>delete v6tov6

Der Portproxyserver löscht eineIPv6-Adresse aus der Liste der IPv6-Adressen, auf die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                   |                                                                                                          |
|-------------------|----------------------------------------------------------------------------------------------------------|
|  **listenport**   |                                    Gibt den zu löschenden IPv6-Port an.                                    |
| **listenaddress** | Gibt die zu löschende IPv6-Adresse an. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|   **protocol**    |                                      Gibt das zu verwendende Protokoll an.                                      |

## <a name="reset"></a>reset

Setzt den IPv6-Konfigurationszustand zurück.

### <a name="syntax"></a>Syntax

`reset`

## <a name="set-v4tov4"></a>set v4tov4

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxyserver, der mit dem Befehl **add v4tov4** erstellt wurde, oder fügt der Liste, die Port-/Adressenpaare zuordnet, einen neuen Eintrag hinzu.

### <a name="syntax"></a>Syntax

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv4-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv4-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="set-v4tov6"></a>set v4tov6

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxyserver, der mit dem Befehl **add v4tov6** erstellt wurde, oder fügt der Liste, die Port-/Adressenpaare zuordnet, einen neuen Eintrag hinzu.

### <a name="syntax"></a>Syntax

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv4-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv6-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv4-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer.  |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="set-v6tov4"></a>set v6tov4

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxyserver, der mit dem Befehl **add v6tov4** erstellt wurde, oder fügt der Liste, die Port-/Adressenpaare zuordnet, einen neuen Eintrag hinzu.

### <a name="syntax"></a>Syntax

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                   |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                           Gibt den IPv6-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv4-Adresse an, mit der eine Verbindung hergestellt wird. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer. |
|  **connectport**   |       Gibt den IPv4-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv6-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer.  |
|    **protocol**    |                                                                                  Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="set-v6tov6"></a>set v6tov6

Ändert die Parameterwerte eines vorhandenen Eintrags auf dem Portproxyserver, der mit dem Befehl **add v6tov6** erstellt wurde, oder fügt der Liste, die Port-/Adressenpaare zuordnet, einen neuen Eintrag hinzu.

### <a name="syntax"></a>Syntax

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|                    |                                                                                                                                                                                                    |
|--------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   **listenport**   |                                                            Gibt den IPv6-Port nach Portnummer oder Dienstname an, auf dem gelauscht werden soll.                                                            |
| **connectaddress** | Gibt die IPv6-Adresse an, mit der eine Verbindung hergestellt werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben ist, ist der Standardwert der lokale Computer.  |
|  **connectport**   |        Gibt den IPv6-Port nach Portnummer oder Dienstname an, mit dem eine Verbindung hergestellt wird. Wenn **connectport** nicht angegeben ist, ist der Standardwert der Wert von **listenport** auf dem lokalen Computer.        |
| **listenaddress**  | Gibt die IPv6-Adresse an, auf die gelauscht werden soll. Zulässige Werte sind die IP-Adresse, der NetBIOS-Name des Computers oder der DNS-Name des Computers. Wenn keine Adresse angegeben wird, ist der lokale Computer der Standardwert. |
|    **protocol**    |                                                                                   Gibt das zu verwendende Protokoll an.                                                                                   |

## <a name="show-all"></a>Anzeigen aller Wiederherstellungspunkte

Zeigt alle Portproxyparameter an, einschließlich Port-/Adresspaare für v4tov4, v4tov6, v6tov4 und v6tov6.

### <a name="syntax"></a>Syntax

`show all`


## <a name="show-v4tov4"></a>show v4tov4

Zeigt v4tov4-Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v4tov4`

## <a name="show-v4tov6"></a>show v4tov6

Zeigt v4tov6-Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v4tov6`

## <a name="show-v6tov4"></a>show v6tov4

Zeigt v6tov4-Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v6tov4`


## <a name="show-v6tov6"></a>show v6tov6

Zeigt v6tov6-Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v6tov6`

---
