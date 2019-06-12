---
title: ksetup:listrealmflags
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: aa96e4da-6b98-4c05-bccf-73cbf33258c2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7db6caf4e63ea59fa40892679d3de0cfaca661e9
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66438027"
---
# <a name="ksetuplistrealmflags"></a>ksetup:listrealmflags



Listet die verfügbaren Bereich-Flags, die von berichtet werden können **Ksetup**. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /listrealmflags
```

### <a name="parameters"></a>Parameter

Keine

## <a name="remarks"></a>Hinweise

Die Bereichs-Flags Geben Sie zusätzliche Funktionen, die von einem nicht-Windows-basierten Kerberos-Bereich. Computer, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt werden, können einen nicht-Windows-basierten Kerberos-Server verwenden, zum Verwalten der Authentifizierung statt einer Domäne, die ein Windows Server-Betriebssystem ausgeführt wird. Diese Systeme ist ein Kerberos-Bereich anstelle einer Windows-Domäne beteiligt. Dieser Eintrag stellt die Funktionen des Bereichs her. In der folgende Tabelle werden die einzelnen beschrieben.

|Wert|Realm-flag|Beschreibung|
|-----|----------|-----------|
|0xF|All|Alle Realm-Flags sind festgelegt.|
|0x00|Keine|Sind keine Flags Bereich festgelegt, und es sind keine zusätzlichen Features aktiviert.|
|0x01|SendAddress|Die IP-Adresse wird in den Ticket-granting Tickets enthalten sein.|
|0x02|TcpSupported|Das Protokoll TCP (Transmission Control) und User Datagram-Protokoll (UDP) werden in diesem Bereich unterstützt.|
|0x04|Delegieren|Alle in diesem Bereich wird für Delegierungszwecke vertraut.|
|0x08|NcSupported|Dieser Bereich unterstützt Namen Kanonisierung, DNS und Bereich Benennungsstandards ermöglicht.|
|0x80|RC4|Dieser Bereich unterstützt bereichsübergreifende Vertrauensstellung, sodass für die Verwendung von TLS ermöglicht die RC4-Verschlüsselung.|

Bereich Flags werden in der Registrierung gespeichert **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\\** <em>Bereichsname</em>. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können die [Ksetup:addrealmflags](ksetup-addrealmflags.md) Befehl aus, um die Registrierung zu füllen.

## <a name="BKMK_Examples"></a>Beispiele für

Liste der bekannten Realm-Flags auf diesem Computer:
```
ksetup /listrealmflags
```
Die verfügbaren Bereich Flags festlegen, die **Ksetup** weiß nicht, indem Sie einen der folgenden Befehle in der Befehlszeile eingeben:
```
ksetup /setrealmflags CORP.CONTOSO.COM sendaddress tcpsupported delete ncsupported
```
```
ksetup /setrealmflags CORP.CONTOSO.COM 0xF
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Ksetup](ksetup.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)