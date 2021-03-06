---
title: ksetup setrealmflags
description: Referenz Artikel für den Ksetup-Befehl setrealmflags, mit dem bereichsflags für den angegebenen Bereich festgelegt werden.
ms.topic: reference
ms.assetid: bcb2824e-fba7-4ebe-be62-e62b4fae5b17
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 08cb63da37f72cf0fd0e26f90ce7a9c2ec7839ac
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89634305"
---
# <a name="ksetup-setrealmflags"></a>ksetup setrealmflags

Legt bereichflags für den angegebenen Bereich fest.

## <a name="syntax"></a>Syntax

```
ksetup /setrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com. |

#### <a name="remarks"></a>Hinweise

- Die bereichsflags geben zusätzliche Features eines Kerberos-Bereichs an, die nicht auf dem Windows Server-Betriebssystem basieren. Computer, auf denen Windows Server ausgeführt wird, können einen Kerberos-Server verwenden, um die Authentifizierung im Kerberos-Bereich zu verwalten, anstatt eine Domäne zu verwenden, die ein Windows Server-Betriebssystem ausgeführt wird. Mit diesem Eintrag werden die Funktionen des Bereichs festgelegt, und es gibt folgende Möglichkeiten:

| Wert | Bereichsflag | BESCHREIBUNG |
| ----- | ---------- | ----------- |
| 0xF | All | Alle bereichflags werden festgelegt. |
| 0x00 | Keine | Es wurden keine bereichflags festgelegt, und es sind keine weiteren Funktionen aktiviert. |
| 0x01 | Element sendaddress | Die IP-Adresse wird in den Tickets für Ticket Gewährung enthalten sein. |
| 0x02 | tcpsupported | In diesem Bereich werden sowohl das Transmission Control Protocol (TCP) als auch das User Datagram-Protokoll (UDP) unterstützt. |
| 0x04 | delegate | Jeder in diesem Bereich ist für die Delegierung vertrauenswürdig. |
| 0x08 | ncsupported | Dieser Bereich unterstützt die namens Kanonisierung, die DNS-und Bereichs Benennungs Standards ermöglicht. |
| 0x80 | RC4 | Dieser Bereich unterstützt die RC4-Verschlüsselung, um eine bereichsübergreifende Vertrauensstellung zu ermöglichen, die die Verwendung von TLS ermöglicht. |

- Bereichflags werden in der Registrierung unter gespeichert `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` . Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den Befehl " [Ksetup adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

- Sie können die verfügbaren bereichflags und festlegen, indem Sie die Ausgabe von **Ksetup** oder anzeigen `ksetup /dumpstate` .

### <a name="examples"></a>Beispiele

Zum Auflisten der verfügbaren und zum Festlegen von bereichflags für den Bereich "", geben Sie Folgendes ein:

```
ksetup
```

Um zwei Flags festzulegen, die zurzeit nicht festgelegt sind, geben Sie

```
ksetup /setrealmflags CONTOSO ncsupported delegate
```

Wenn Sie überprüfen möchten, ob das bereichsflag festgelegt ist, geben Sie ein, `ksetup` und **Realm flags =** zeigen Sie dann die Ausgabe an, und suchen Sie nach dem Text Wenn der Text nicht angezeigt wird, bedeutet dies, dass das Flag nicht festgelegt wurde.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup listrealmflags-Befehl](ksetup-listrealmflags.md)

- [Ksetup-Befehl "adressalmflags"](ksetup-addrealmflags.md)

- [Ksetup-Befehl "Delta-Flags"](ksetup-delrealmflags.md)

- [Ksetup (dumpstate-Befehl)](ksetup-dumpstate.md)
