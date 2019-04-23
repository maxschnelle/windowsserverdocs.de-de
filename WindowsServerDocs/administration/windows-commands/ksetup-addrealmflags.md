---
title: ksetup:addrealmflags
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 80ca1e16-8871-494b-b9be-6bc9d63de860
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bbc878bd0ee25ad92c640710ab6b46bbc0eaf62a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59827681"
---
# <a name="ksetupaddrealmflags"></a>ksetup:addrealmflags



Fügt zusätzliche Realm-Flags in den angegebenen Bereich hinzu. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Bereichsname|Der Bereichsname ist als Großbuchstaben DNS-Name, wie z. B. CORP. angegeben. "CONTOSO.COM".|

## <a name="remarks"></a>Hinweise

Die Bereichs-Flags Geben Sie zusätzliche Funktionen, die von einem Kerberos-Bereich, der nicht auf dem Windows Server-Betriebssystem basiert. Computer, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt werden können einen Kerberos-Server zum Verwalten der Authentifizierung statt einer Domäne, die ein Windows Server-Betriebssystem ausgeführt wird, und diese Systeme beteiligt ein Kerberos-Bereich. Dieser Eintrag stellt die Funktionen des Bereichs her. In der folgende Tabelle werden die einzelnen beschrieben.

|Wert|Realm-flag|Beschreibung|
|-----|----------|-----------|
|0xF|Alle|Alle Realm-Flags sind festgelegt.|
|0x00|Keine|Sind keine Flags Bereich festgelegt, und es sind keine zusätzlichen Features aktiviert.|
|0x01|SendAddress|Die IP-Adresse wird in den Ticket-granting Tickets enthalten sein.|
|0x02|TcpSupported|In diesem Bereich werden sowohl das Protokoll TCP (Transmission Control) und User Datagram-Protokoll (UDP) unterstützt.|
|0x04|Delegieren|Alle in diesem Bereich wird für Delegierungszwecke vertraut.|
|0x08|NcSupported|Dieser Bereich unterstützt Namen Kanonisierung, DNS und Bereich Benennungsstandards ermöglicht.|
|0x80|RC4|Dieser Bereich unterstützt bereichsübergreifende Vertrauensstellung, sodass für die Verwendung von TLS ermöglicht die RC4-Verschlüsselung.|

Bereich Flags werden gespeichert, in der Registrierung unter **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\*** Realm-Name *. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können die [Ksetup:addrealmflags](ksetup-addrealmflags.md) Befehl aus, um die Registrierung zu füllen.

Sehen Sie, welche Flags Bereich verfügbar und festgelegt sind, indem Sie die Ausgabe Ksetup oder Ksetup /dumpstate anzeigen.

## <a name="BKMK_Examples"></a>Beispiele für

Liste der verfügbaren Bereich-Flags für den CONTOSO-Bereich an:
```
Ksetup /listrealmflags
```
Legen Sie zwei Flags in der CONTOSO-Bereich ein:
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
Fügen Sie eine weitere Flag, das derzeit nicht im Satz enthalten ist:
```
ksetup /addrealmflags CONTOSO SendAddress
```
Führen Sie die **Ksetup** Befehl aus, um sicherzustellen, dass das Realm-Flag festgelegt ist, indem die Ausgabe anzeigen und nach **Bereich Flags =**.

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Befehlszeilensyntax](command-line-syntax-key.md)