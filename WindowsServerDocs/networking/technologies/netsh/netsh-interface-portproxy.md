---
title: Netsh-Befehle für Schnittstellen-portproxy
description: Verwenden Sie die Befehle von Netsh Interface Portproxy, fungiert als Proxy zwischen IPv4 und IPv6-Netzwerken und Anwendungen.
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: ''
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 08/30/2018
ms.openlocfilehash: 194a418fe6b33e312a3f2529e82d50d76cd15f4c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59842481"
---
# <a name="netsh-interface-portproxy-commands"></a>Netsh Interface Portproxy-Befehle

Verwenden der **Netsh Interface Portproxy** Befehle aus, um als Proxy zwischen IPv4 und IPv6-Netzwerken und Anwendungen fungieren. Sie können diese Befehle verwenden, zum Einrichten der Proxydienst gibt folgenden Möglichkeiten:

-   IPv4-konfigurierter Computer, und die Anwendung an andere IPv4-konfigurierte Computer und Anwendungen gesendete Nachrichten.

-   IPv4-konfigurierter Computer, und die Anwendung Nachrichten gesendete IPv6-Konfiguration von Computern und Anwendungen.

-   IPv6-konfigurierter Computer, und die Anwendung Nachrichten gesendeten IPv4-Konfiguration von Computern und Anwendungen.

-   IPv6-konfigurierter Computer, und die Anwendung an andere IPv6-konfigurierte Computer und Anwendungen gesendete Nachrichten.

Beim Schreiben von Batchdateien oder Skripts, die mit diesen Befehlen muss jeden Befehl mit beginnen **Netsh Interface Portproxy**. Beispielsweise wird bei Verwendung der **v4tov6 löschen** Befehl aus, um anzugeben, dass die Portproxyserver Löscht einen IPv4-Port und Adresse aus der Liste der IPv4-Adressen, die für die der Server lauscht, die Batch-Datei oder das Skript muss die folgende Syntax verwenden:

```PowerShell
netsh interface portproxy delete v4tov6listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address| HostName}] [[protocol=]tcp]
```

Die verfügbaren Netsh Interface Portproxy-Befehle sind:

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

-   [Alle anzeigen](#show-all)

-   [show v4tov4](#show-v4tov4)

-   [show v4tov6](#show-v4tov6)

-   [show v6tov4](#show-v6tov4)

-   [show v6tov6](#show-v6tov6)


## <a name="add-v4tov4"></a>Hinzufügen von v4tov4

Die Portproxyserver Lauscht auf Nachrichten, die einen Port und die IPv4-Adresse in die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindungs gesendet, um einen bestimmten Port und die IPv4-Adresse und die Zuordnungen.

### <a name="syntax"></a>Syntax

```PowerShell
add v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName}] [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName}] [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter


| | |
|-----|--------|----------|
| **listenport**     | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.                                                                                                                      | Erforderlich |
| **connectaddress** | Gibt die IPv4-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv4-Adresse für das Lauschen an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                    |          |

## <a name="add-v4tov6"></a>Hinzufügen von v4tov6

Die Portproxyserver Lauscht auf Nachrichten, die einen Port und die IPv6-Adresse in die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindungs gesendet, um einen bestimmten Port und IPv4-Adresse und Zuordnungen.

### <a name="syntax"></a>Syntax

```PowerShell
add v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|-----------|-------------|----------|
| **listenport**     | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.       | Erforderlich |
| **connectaddress** | Gibt die IPv6-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv4-Adresse auf den gelauscht. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer.  |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                    |          |

## <a name="add-v6tov4"></a>add v6tov4

Die Portproxyserver Lauscht auf Nachrichten, die an einem bestimmten Port und IPv6-Adresse und Zuordnungen, der die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindungs einen Port und die IPv4-Adresse, gesendet.

### <a name="syntax"></a>Syntax

```PowerShell
add v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|------------|-------------|----------|
| **listenport**     | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.              | Erforderlich |
| **connectaddress** | Gibt die IPv4-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv6-Adresse auf den gelauscht. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer.  |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.      |          |

## <a name="add-v6tov6"></a>Hinzufügen von v6tov6

Die Portproxyserver Lauscht auf Nachrichten, die an einem bestimmten Port und IPv6-Adresse und Zuordnungen, der die empfangenen Nachrichten nach dem Einrichten einer separaten TCP-Verbindungs einen Port und die IPv6-Adresse, gesendet.

### <a name="syntax"></a>Syntax

```PowerShell
add v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|-------------|------------------|----------|
| **listenport**     | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.       | Erforderlich |
| **connectaddress** | Gibt die IPv6-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv6-Adresse auf den gelauscht. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer.  |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                    |          |

## <a name="delete-v4tov4"></a>v4tov4 löschen

Die Portproxyserver Löscht eine IPv4-Adresse aus der Liste der IPv4-Ports und Adressen, die für die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v4tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | Gibt den IPv4-Port zu löschen.                                                                       | Erforderlich |
| **listenaddress** | Gibt die IPv4-Adresse zu löschen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **protocol**      | Gibt das zu verwendende Protokoll an.                                                                           |          |

## <a name="delete-v4tov6"></a>v4tov6 löschen

Die Portproxyserver Löscht einen IPv4-Port und Adresse aus der Liste der IPv4-Adressen, die für die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell 
delete v4tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | Gibt den IPv4-Port zu löschen.                                                                       | Erforderlich |
| **listenaddress** | Gibt die IPv4-Adresse zu löschen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **protocol**      | Gibt das zu verwendende Protokoll an.                                                                           |          |

## <a name="delete-v6tov4"></a>v6tov4 löschen

Die Portproxyserver Löscht eine IPv6-Port und Adresse aus der Liste der IPv6-Adressen, die für die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v6tov4 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | Gibt den IPv6-Port zu löschen.                                                                       | Erforderlich |
| **listenaddress** | Gibt an, die IPv6-Adresse zu löschen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **protocol**      | Gibt das zu verwendende Protokoll an.                                                                           |          |

## <a name="delete-v6tov6"></a>v6tov6 löschen

Die Portproxyserver Löscht eine IPv6-Adresse aus der Liste der IPv6-Adressen, die für die der Server lauscht.

### <a name="syntax"></a>Syntax

```PowerShell
delete v6tov6 listenport= {Integer | ServiceName} [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|-------------------|----------------------------------------------------------------------------------------------------------|----------|
| **listenport**    | Gibt den IPv6-Port zu löschen.                                                                       | Erforderlich |
| **listenaddress** | Gibt an, die IPv6-Adresse zu löschen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **protocol**      | Gibt das zu verwendende Protokoll an.                                                                           |          |

## <a name="reset"></a>Zurücksetzen

Setzt den Zustand der IPv6-Konfiguration zurück.

### <a name="syntax"></a>Syntax

`reset`

## <a name="set-v4tov4"></a>Set-v4tov4

Ändert die Werte der Parameter eines vorhandenen Eintrags auf dem Portproxyserver mit der **hinzufügen v4tov4** Befehl oder fügt einen neuen Eintrag der Liste aus, dass Zuordnungen/Paare Portadresse.

### <a name="syntax"></a>Syntax

```PowerShell
set v4tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|--------------------|---------------------------|----------|
| **listenport**     | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.     | Erforderlich |
| **connectaddress** | Gibt die IPv4-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv4-Adresse für das Lauschen an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                    |          |

## <a name="set-v4tov6"></a>Set-v4tov6

Ändert die Werte der Parameter eines vorhandenen Eintrags auf dem Portproxyserver mit der **hinzufügen v4tov6** Befehl oder fügt einen neuen Eintrag der Liste aus, dass Zuordnungen/Paare Portadresse.

### <a name="syntax"></a>Syntax

```PowerShell
set v4tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv4Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|--------------------|---------------------|----------|
| **listenport**     | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.     | Erforderlich |
| **connectaddress** | Gibt die IPv6-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv4-Adresse auf den gelauscht. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer.  |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                    |          |

## <a name="set-v6tov4"></a>Set-v6tov4

Ändert die Werte der Parameter eines vorhandenen Eintrags auf dem Portproxyserver mit der **hinzufügen v6tov4** Befehl oder fügt einen neuen Eintrag der Liste aus, dass Zuordnungen/Paare Portadresse.

### <a name="syntax"></a>Syntax

```PowerShell
set v6tov4 listenport= {Integer | ServiceName} [[connectaddress=] {IPv4Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|--------------------|----------------------|----------|
| **listenport**     | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.      | Erforderlich |
| **connectaddress** | Gibt die IPv4-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer. |          |
| **connectport**    | Gibt an, der IPv4-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.              |          |
| **listenaddress**  | Gibt die IPv6-Adresse auf den gelauscht. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer.  |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                    |          |

## <a name="set-v6tov6"></a>Set-v6tov6

Ändert die Werte der Parameter eines vorhandenen Eintrags auf dem Portproxyserver mit der **hinzufügen v6tov6** Befehl oder fügt einen neuen Eintrag der Liste aus, dass Zuordnungen/Paare Portadresse.

### <a name="syntax"></a>Syntax

```PowerShell 
set v6tov6 listenport= {Integer | ServiceName} [[connectaddress=] {IPv6Address | HostName} [[connectport=] {Integer | ServiceName}] [[listenaddress=] {IPv6Address | HostName} [[protocol=]tcp]
```

### <a name="parameters"></a>Parameter

|   |   |
|--------------------|-------------------------|----------|
| **listenport**     | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, auf den gelauscht.   | Erforderlich |
| **connectaddress** | Gibt die IPv6-Adresse für die Verbindung an. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn eine Adresse nicht angegeben wird, ist der Standardwert der lokale Computer.  |          |
| **connectport**    | Gibt an, der IPv6-Port, Portnummer oder den Dienst anzugeben, für die Verbindung. Wenn **Connectport** nicht angegeben ist, wird der Standardwert ist der Wert des **Listenport** auf dem lokalen Computer.               |          |
| **listenaddress**  | Gibt die IPv6-Adresse auf den gelauscht. Zulässige Werte sind die IP-Adresse, NetBIOS-Computernamen oder DNS-Computernamen. Wenn Sie keine Adresse angeben, ist der Standardwert der lokale Computer. |          |
| **protocol**       | Gibt das zu verwendende Protokoll an.                                                                                                                                                                     |          |

## <a name="show-all"></a>Anzeigen aller Wiederherstellungspunkte

Zeigt alle Portproxyparameter, einschließlich Portadresse /-Paare für v4tov4, v4tov6, v6tov4 und v6tov6 an.

### <a name="syntax"></a>Syntax

`show all`


## <a name="show-v4tov4"></a>v4tov4 anzeigen

Zeigt v4tov4 Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v4tov4`

## <a name="show-v4tov6"></a>v4tov6 anzeigen

Zeigt v4tov6 Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v4tov6`

## <a name="show-v6tov4"></a>v6tov4 anzeigen

Zeigt v6tov4 Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v6tov4`


## <a name="show-v6tov6"></a>v6tov6 anzeigen

Zeigt v6tov6 Portproxyparameter an.

### <a name="syntax"></a>Syntax

`show v6tov6`

---
