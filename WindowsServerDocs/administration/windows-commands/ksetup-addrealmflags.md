---
title: ksetup addrealmflags
description: Referenz Artikel für den Ksetup-Befehl "adressalmflags", mit dem dem angegebenen Bereich weitere bereichsflags hinzugefügt werden.
ms.topic: reference
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 34f9067e95a0632fd1f22de604545fe2a5417727
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89037958"
---
# <a name="ksetup-addrealmflags"></a>ksetup addrealmflags

Fügt dem angegebenen Bereich weitere bereichflags hinzu.

## <a name="syntax"></a>Syntax

```
ksetup /addrealmflags <realmname> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| `<realmname>` | Gibt den Großbuchstaben-DNS-Namen an, z. b. Corp. CONTOSO.com. |

#### <a name="remarks"></a>Bemerkungen

- Die bereichsflags geben zusätzliche Features eines Kerberos-Bereichs an, die nicht auf dem Windows Server-Betriebssystem basieren. Computer, auf denen Windows Server ausgeführt wird, können einen Kerberos-Server verwenden, um die Authentifizierung im Kerberos-Bereich zu verwalten, anstatt eine Domäne zu verwenden, die ein Windows Server-Betriebssystem ausgeführt wird. Mit diesem Eintrag werden die Funktionen des Bereichs festgelegt, und es gibt folgende Möglichkeiten:

| Wert | Bereichsflag | Beschreibung |
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

Geben Sie Folgendes ein, um die verfügbaren bereichflags für den Bereich "" zu erhalten:

```
ksetup /listrealmflags
```

Geben Sie Folgendes ein, um zwei Flags auf den Bereich "" von "" von ""

```
ksetup /setrealmflags CONTOSO ncsupported delegate
```

Wenn Sie ein Flag hinzufügen möchten, das sich derzeit nicht in der Gruppe befindet, geben Sie Folgendes ein:

```
ksetup /addrealmflags CONTOSO SendAddress
```

Wenn Sie überprüfen möchten, ob das bereichsflag festgelegt ist, geben Sie ein, `ksetup` und **Realm flags =** zeigen Sie dann die Ausgabe an, und suchen Sie nach dem Text Wenn der Text nicht angezeigt wird, bedeutet dies, dass das Flag nicht festgelegt wurde.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup listrealmflags-Befehl](ksetup-listrealmflags.md)

- [ksetup setrealmflags-Befehl](ksetup-setrealmflags.md)

- [Ksetup-Befehl "Delta-Flags"](ksetup-delrealmflags.md)

- [Ksetup (dumpstate-Befehl)](ksetup-dumpstate.md)
