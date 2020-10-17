---
title: tsecimp
description: Referenz Artikel für den Befehl "tscimp", mit dem Zuweisungs Informationen aus einer Extensible Markup Language-Datei (XML) in die TAPI-Server Sicherheits Datei (Tsec.ini) importiert werden.
ms.topic: reference
ms.assetid: d7488ec6-0eff-45ff-89ee-9cbe752416bf
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 0db7c7c191b4ca4cdd1d266892b68aa717c142da
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156667"
---
# <a name="tsecimp"></a>tsecimp

Importiert Zuweisungs Informationen aus einer Extensible Markup Language-Datei (XML) in die Sicherheits Datei des TAPI-Servers (Tsec.ini). Sie können diesen Befehl auch verwenden, um die Liste der TAPI-Anbieter und der zugehörigen Geräte anzuzeigen, die Struktur der XML-Datei zu überprüfen, ohne den Inhalt zu importieren, und die Domänen Mitgliedschaft zu überprüfen.

## <a name="syntax"></a>Syntax

```
tsecimp /f <filename> [{/v | /u}]
tsecimp /d
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /f `<filename>` | Erforderlich. Gibt den Namen der XML-Datei an, die die Zuweisungs Informationen enthält, die Sie importieren möchten. |
| /v | Überprüft die Struktur der XML-Datei, ohne die Informationen in die Tsec.ini Datei zu importieren. |
| /U | Überprüft, ob jeder Benutzer ein Mitglied der Domäne ist, die in der XML-Datei angegeben ist. Der Computer, auf dem Sie diesen Parameter verwenden, muss mit dem Netzwerk verbunden sein. Dieser Parameter kann die Leistung erheblich verlangsamen, wenn Sie eine große Menge an Benutzer Zuweisungs Informationen verarbeiten. |
| /d | Zeigt eine Liste installierter Telefonieanbieter an. Für jeden Telefonieanbieter werden die zugeordneten liniengeräte sowie die den einzelnen Zeilen Geräten zugeordneten Adressen und Benutzer aufgelistet. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

Die XML-Datei, aus der Sie Zuweisungs Informationen importieren möchten, muss der unten beschriebenen Struktur folgen:

```xml
<UserList>
  <User>
    <LineList>
      <Line>
```

- `<Userlist element>` : Das oberste Element der XML-Datei.

- `<User element>` -Enthält Informationen zu einem Benutzer, der Mitglied einer Domäne ist. Jedem Benutzer wird möglicherweise ein oder mehrere Linien Geräte zugewiesen. Darüber hinaus kann jedes **User** -Element ein Attribut mit dem Namen " **nomerge**" aufweisen. Wenn dieses Attribut angegeben wird, werden alle Geräte Zuweisungen der aktuellen Zeile für den Benutzer entfernt, bevor neue erstellt werden. Sie können dieses Attribut verwenden, um unerwünschte Benutzer Zuweisungen auf einfache Weise zu entfernen. Standardmäßig ist dieses Attribut nicht festgelegt. Das **User** -Element muss ein einzelnes **Domainusername** -Element enthalten, das die Domäne und den Benutzernamen des Benutzers angibt. Das **User** -Element kann auch ein **FriendlyName** -Element enthalten, das einen benutzerfreundlichen Namen für den Benutzer angibt. Das **User** -Element kann ein **LineList** -Element enthalten. Wenn ein **LineList** -Element nicht vorhanden ist, werden alle Zeilen Geräte für diesen Benutzer entfernt.

- `<LineList element>` -Enthält Informationen zu den einzelnen Zeilen oder Geräten, die dem Benutzer zugewiesen werden können. Jedes **LineList** -Element kann mehr als ein **Line** -Element enthalten.

- `<Line element>` : Gibt ein liniengerät an. Sie müssen jedes Zeilen Gerät identifizieren, indem Sie ein **Adress** Element oder ein **PermanentID-** Element unter dem **Line** -Element hinzufügen. Für jedes **Line** -Element können Sie das **Remove** -Attribut festlegen. Wenn Sie dieses Attribut festlegen, wird der Benutzer nicht mehr diesem Geräte Gerät zugewiesen. Wenn dieses Attribut nicht festgelegt ist, erhält der Benutzer Zugriff auf dieses liniengerät. Wenn das liniengerät für den Benutzer nicht verfügbar ist, wird kein Fehler ausgegeben.

##### <a name="sample-output-for-d-parameter"></a>Beispielausgabe für den/d-Parameter

Diese Beispielausgabe wird nach dem Ausführen des **/d** -Parameters angezeigt, um die aktuelle TAPI-Konfiguration anzuzeigen. Für jeden Telefonieanbieter werden die zugeordneten liniengeräte sowie die den einzelnen Zeilen Geräten zugeordneten Adressen und Benutzer aufgelistet.

```
NDIS Proxy TAPI Service Provider
  Line: WAN Miniport (L2TP)
    Permanent ID: 12345678910

NDIS Proxy TAPI Service Provider
  Line: LPT1DOMAIN1\User1
    Permanent ID: 12345678910

Microsoft H.323 Telephony Service Provider
  Line: H323 Line
    Permanent ID: 123456
    Addresses:
      BLDG1-TAPI32
```

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle der *User1*zugewiesenen Zeilen Geräte zu entfernen:

```xml
<UserList>
  <User NoMerge=1>
    <DomainUser>domain1\user1</DomainUser>
  </User>
</UserList>
```

Geben Sie Folgendes ein, um alle der *User1*zugewiesenen Zeilen Geräte zu entfernen, bevor Sie eine Zeile mit der Adresse *99999*zuweisen:

```xml
<UserList>
  <User NoMerge=1>
  <DomainUser>domain1\user1</DomainUser>
  <FriendlyName>User1</FriendlyName>
  <LineList>
    <Line>
      <Address>99999</Address>
    </Line>
  </LineList>
  </User>
</UserList>
```

In diesem Beispiel sind in *User1* keine anderen Linien Geräte zugewiesen, unabhängig davon, ob zuvor Zeilen Geräte zugewiesen wurden.

Wenn Sie ein Geräte Gerät für *User1*hinzufügen möchten, ohne zuvor zugewiesene Linien Geräte zu löschen, geben Sie Folgendes ein:

```xml
<UserList>
  <User>
  <DomainUser>domain1\user1</DomainUser>
  <FriendlyName>User1</FriendlyName>
  <LineList>
    <Line>
      <Address>99999</Address>
    </Line>
  </LineList>
  </User>
</UserList>
```

Zum Hinzufügen der Zeilen Adresse *99999* und zum Entfernen der Zeilen Adresse *88888* aus *User1's* Access geben Sie Folgendes ein:

```xml
<UserList>
  <User>
  <DomainUser>domain1\user1</DomainUser>
  <FriendlyName>User1</FriendlyName>
  <LineList>
    <Line>
      <Address>99999</Address>
    </Line>
    <Line Remove=1>
      <Address>88888</Address>
    </Line>
  </LineList>
  </User>
</UserList>
```

Wenn Sie permanentes Gerät *1000* hinzufügen und Zeile *88888* aus *User1's* Access entfernen möchten, geben Sie Folgendes ein:

```xml
<UserList>
  <User>
  <DomainUser>domain1\user1</DomainUser>
  <FriendlyName>User1</FriendlyName>
  <LineList>
    <Line>
    <PermanentID>1000</PermanentID>
    </Line>
    <Line Remove=1>
    <Address>88888</Address>
    </Line>
  </LineList>
  </User>
</UserList>
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Übersicht über Befehlsshell](/previous-versions/windows/it-pro/windows-server-2003/cc737438(v=ws.10))
