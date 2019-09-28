---
title: 'Ksetup: adressalm Flags'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 543fcb8105d21020cc9a4ab5e5e8c1eca14a358b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375170"
---
# <a name="ksetupaddrealmflags"></a>Ksetup: adressalm Flags



Fügt dem angegebenen Bereich weitere bereichflags hinzu. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /addrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|Bereichs Name|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|

## <a name="remarks"></a>Hinweise

Die bereichsflags geben zusätzliche Features eines Kerberos-Bereichs an, der nicht auf dem Windows Server-Betriebssystem basiert. Computer, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird, können einen Kerberos-Server verwenden, um die Authentifizierung zu verwalten, anstatt eine Domäne zu verwenden, in der ein Windows Server-Betriebssystem ausgeführt wird. diese Systeme nehmen an einem Der Kerberos-Bereich. Mit diesem Eintrag werden die Funktionen des Bereichs festgelegt. In der folgenden Tabelle werden die einzelnen beschrieben.

|Wert|Bereichsflag|Beschreibung|
|-----|----------|-----------|
|0xF|All|Alle bereichflags werden festgelegt.|
|0x00|Keine|Es wurden keine bereichflags festgelegt, und es sind keine weiteren Funktionen aktiviert.|
|0x01|Element sendaddress|Die IP-Adresse wird in den Tickets für Ticket Gewährung enthalten sein.|
|0x02|Tcpsupported|In diesem Bereich werden sowohl das Transmission Control Protocol (TCP) als auch das User Datagram-Protokoll (UDP) unterstützt.|
|0x04|Delegieren|Jeder in diesem Bereich ist für die Delegierung vertrauenswürdig.|
|0x08|Ncsupported|Dieser Bereich unterstützt die namens Kanonisierung, die DNS-und Bereichs Benennungs Standards ermöglicht.|
|0x80|RC4|Dieser Bereich unterstützt die RC4-Verschlüsselung, um eine bereichsübergreifende Vertrauensstellung zu ermöglichen, die die Verwendung von TLS ermöglicht.|

Bereichsflags werden in der Registrierung unter **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains @ no__t-1**<em>Realm-Name</em>gespeichert. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den Befehl " [Ksetup: adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

Sie können sehen, welche bereichflags verfügbar sind und festgelegt werden, indem Sie die Ausgabe von Ksetup oder Ksetup/dumpstate. anzeigen.

## <a name="BKMK_Examples"></a>Beispiele

Listet die verfügbaren bereichflags für den Bereich "" auf.
```
Ksetup /listrealmflags
```
Legen Sie zwei Flags auf den Bereich "sechanso" fest:
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
Fügen Sie ein Flag hinzu, das sich zurzeit nicht in der Gruppe befindet:
```
ksetup /addrealmflags CONTOSO SendAddress
```
Führen Sie den **Ksetup** -Befehl aus, um zu überprüfen, ob das bereichsflag festgelegt ist, indem Sie die Ausgabe anzeigen und nach **bereichsflags**

#### <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:setrealmflags](ksetup-setrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)