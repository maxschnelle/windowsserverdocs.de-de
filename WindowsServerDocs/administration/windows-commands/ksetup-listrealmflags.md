---
title: 'Ksetup: listrealmflags'
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8f103875dc10dfbf7b0c604a8e2060fe58ee7a92
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71374969"
---
# <a name="ksetuplistrealmflags"></a>Ksetup: listrealmflags



Listet die verfügbaren bereichflags auf, die von **Ksetup**gemeldet werden können. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /listrealmflags
```

### <a name="parameters"></a>Parameter

Keine

## <a name="remarks"></a>Hinweise

Die bereichsflags geben zusätzliche Funktionen eines nicht Windows-basierten Kerberos-Bereichs an. Computer, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird, können einen nicht-Windows-basierten Kerberos-Server verwenden, um die Authentifizierung zu verwalten, anstatt eine Domäne zu verwenden, die ein Windows Server-Betriebssystem ausgeführt wird. Diese Systeme nehmen an einem Kerberos-Bereich statt in einer Windows-Domäne Teil. Mit diesem Eintrag werden die Funktionen des Bereichs festgelegt. In der folgenden Tabelle werden die einzelnen beschrieben.

|Wert|Bereichsflag|Beschreibung|
|-----|----------|-----------|
|0xF|Alle|Alle bereichflags werden festgelegt.|
|0x00|Keine|Es wurden keine bereichflags festgelegt, und es sind keine weiteren Funktionen aktiviert.|
|0x01|Element sendaddress|Die IP-Adresse wird in den Tickets für Ticket Gewährung enthalten sein.|
|0x02|Tcpsupported|Das Transmission Control-Protokoll (TCP) und das User Datagram-Protokoll (UDP) werden in diesem Bereich unterstützt.|
|0x04|Delegieren|Jeder in diesem Bereich ist für die Delegierung vertrauenswürdig.|
|0x08|Ncsupported|Dieser Bereich unterstützt die namens Kanonisierung, die DNS-und Bereichs Benennungs Standards ermöglicht.|
|0x80|RC4|Dieser Bereich unterstützt die RC4-Verschlüsselung, um eine bereichsübergreifende Vertrauensstellung zu ermöglichen, die die Verwendung von TLS ermöglicht.|

Bereichsflags werden in der Registrierung in **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\** <em>Bereichs Name</em>gespeichert. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den Befehl " [Ksetup: adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

## <a name="BKMK_Examples"></a>Beispiele

Listet die bekannten bereichflags auf diesem Computer auf:
```
ksetup /listrealmflags
```
Legen Sie die verfügbaren bereichsflags fest, die **Ksetup** nicht kennt, indem Sie einen der folgenden Befehle in der Befehlszeile eingeben:
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