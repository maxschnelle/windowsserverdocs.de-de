---
title: Ksetup listrealmflags
description: Referenz Thema für den Ksetup listrealmflags-Befehl, der die verfügbaren bereichsflags auflistet, die von Ksetup gemeldet werden können.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5c5ebbee7f937733286e0354eca1cf5524459e86
ms.sourcegitcommit: 4f407b82435afe3111c215510b0ef797863f9cb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2020
ms.locfileid: "83817720"
---
# <a name="ksetup-listrealmflags"></a>Ksetup listrealmflags

Listet die verfügbaren bereichflags auf, die von **Ksetup**gemeldet werden können.

## <a name="syntax"></a>Syntax

```
ksetup /listrealmflags
```

### <a name="remarks"></a>Hinweise

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

- Bereichflags werden in der Registrierung unter gespeichert `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\<realmname>` . Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den [Befehl "Ksetup adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die bekannten bereichflags auf diesem Computer aufzulisten:

```
ksetup /listrealmflags
```

Geben Sie Folgendes ein, um die verfügbaren bereichflags festzulegen, die **Ksetup** nicht kennt:

```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```

**Noch**

```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Ksetup-Befehl](ksetup.md)

- [Ksetup-Befehl "adressalmflags"](ksetup-addrealmflags.md)

- [ksetup setrealmflags-Befehl](ksetup-setrealmflags.md)

- [Ksetup-Befehl "Delta-Flags"](ksetup-delrealmflags.md)
