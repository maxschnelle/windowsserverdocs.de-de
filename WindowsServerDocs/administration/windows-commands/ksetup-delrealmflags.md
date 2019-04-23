---
title: ksetup:delrealmflags
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 22053041-1eb4-47f5-bed9-3d5681bcde7d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9522d384c4f6996534b47e98dc8d8003bda504cd
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877141"
---
# <a name="ksetupdelrealmflags"></a>ksetup:delrealmflags



Entfernt aus dem angegebenen Bereich Realm-Flags.  Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /delrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<RealmName>|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "Contoso.com" als den Standardbereich aufgeführt ist, und wenn **Ksetup** ausgeführt wird.|

## <a name="remarks"></a>Hinweise

Die Bereichs-Flags Geben Sie zusätzliche Funktionen, die von einem Kerberos-Bereich, der nicht auf dem Windows Server-Betriebssystem basiert. Computer, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt werden können einen Kerberos-Server zum Verwalten der Authentifizierung statt einer Domäne, die ein Windows Server-Betriebssystem ausgeführt wird, und diese Systeme beteiligt ein Kerberos-Bereich. Dieser Eintrag stellt die Funktionen des Bereichs her. In der folgende Tabelle werden die einzelnen beschrieben.

|Wert|Realm-flag|Beschreibung|
|-----|----------|-----------|
|0xF|Alle|Alle Realm-Flags sind festgelegt.|
|0x00|Keine|Sind keine Flags Bereich festgelegt, und es sind keine zusätzlichen Features aktiviert.|
|0x01|SendAddress|Die IP-Adresse wird in den Ticket-granting-Tickets enthalten sein.|
|0x02|TcpSupported|In diesem Bereich werden sowohl das Protokoll TCP (Transmission Control) und User Datagram-Protokoll (UDP) unterstützt.|
|0x04|Delegieren|Alle in diesem Bereich wird für Delegierungszwecke vertraut.|
|0x08|NcSupported|Dieser Bereich unterstützt Namen Kanonisierung, DNS und Bereich Benennungsstandards ermöglicht.|
|0x80|RC4|Dieser Bereich unterstützt bereichsübergreifende Vertrauensstellung, sodass für die Verwendung von TLS ermöglicht die RC4-Verschlüsselung.|

Bereich Flags werden in der Registrierung gespeichert **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\*** RealmName *. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können die [Ksetup:addrealmflags](ksetup-addrealmflags.md) Befehl aus, um die Registrierung zu füllen.

Sie können sehen, welche Flags Bereich verfügbar sind und festgelegt werden, indem Sie die Ausgabe des **Ksetup** oder **Ksetup /dumpstate**.

## <a name="BKMK_Examples"></a>Beispiele für

Liste der verfügbaren Bereich-Flags für den CONTOSO-Bereich an:
```
Ksetup /listrealmflags
```
Entfernen von zwei Flags, die derzeit in der Gruppe enthalten sind:
```
ksetup /delrealmflags CONTOSO ncsupported delegate
```
Führen Sie die **Ksetup** Befehl aus, um sicherzustellen, dass das Realm-Flag festgelegt ist, indem die Ausgabe anzeigen und nach **Bereich Flags =**.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)