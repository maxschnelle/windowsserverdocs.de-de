---
title: 'Ksetup: setrealmflags'
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: bcb2824e-fba7-4ebe-be62-e62b4fae5b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 29ef5de8130fa9b10ce6d999e16765b0aa2697a4
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80841283"
---
# <a name="ksetupsetrealmflags"></a>Ksetup: setrealmflags



Legt bereichflags für den angegebenen Bereich fest. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
ksetup /setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

#### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Realmname >|Der Bereichs Name wird als Großbuchstabe (DNS-Name) angegeben, z. b. Corp. CONTOSO.com.|
|Bereichsflag|Gibt eines der folgenden Flags an:</br>-Sendaddress</br>-Tcpsupported</br>-Delegat</br>-Ncsupported</br>-RC4|

## <a name="remarks"></a>Hinweise

Die bereichsflags geben zusätzliche Features eines Kerberos-Bereichs an, der nicht auf dem Windows Server-Betriebssystem basiert. Computer, auf denen Windows Server 2003, Windows Server 2008 oder Windows Server 2008 R2 ausgeführt wird, können einen Kerberos-Server verwenden, um die Authentifizierung zu verwalten, anstatt eine Domäne zu verwenden, in der ein Windows Server-Betriebssystem ausgeführt wird, und diese Systeme an einem Kerberos-Bereich teilnehmen. Mit diesem Eintrag werden die Funktionen des Bereichs festgelegt. In der folgenden Tabelle werden die einzelnen beschrieben.

|Wert|Bereichsflag|Beschreibung|
|-----|----------|-----------|
|0xF|Alle|Alle bereichflags werden festgelegt.|
|0x00|Keine|Es wurden keine bereichflags festgelegt, und es sind keine weiteren Funktionen aktiviert.|
|0x01|Element sendaddress|Die IP-Adresse wird in den Tickets für Ticket Gewährung enthalten sein.|
|0x02|Tcpsupported|In diesem Bereich werden sowohl das Transmission Control Protocol (TCP) als auch das User Datagram-Protokoll (UDP) unterstützt.|
|0x04|Delegat|Jeder in diesem Bereich ist für die Delegierung vertrauenswürdig.|
|0x08|Ncsupported|Dieser Bereich unterstützt die namens Kanonisierung, die DNS-und Bereichs Benennungs Standards ermöglicht.|
|0x80|RC4|Dieser Bereich unterstützt die RC4-Verschlüsselung, um eine bereichsübergreifende Vertrauensstellung zu ermöglichen, die die Verwendung von TLS ermöglicht.|

Bereichsflags werden in der Registrierung unter **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\lsa\kerberos\domains\\** <em>Realmname</em>gespeichert. Dieser Eintrag ist nicht standardmäßig in der Registrierung vorhanden. Sie können den Befehl " [Ksetup: adressalmflags](ksetup-addrealmflags.md) " verwenden, um die Registrierung aufzufüllen.

Sie können sehen, welche bereichflags verfügbar sind und wie Sie festgelegt werden, indem Sie die Ausgabe von **Ksetup**anzeigen.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

Listet die verfügbaren und Set-bereichflags für den Bereich "" auf.
```
ksetup
```
Legen Sie zwei Flags fest, die derzeit nicht festgelegt sind:
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
Führen Sie den **Ksetup** -Befehl aus, um zu überprüfen, ob das bereichsflag festgelegt ist, indem Sie die Ausgabe anzeigen und nach **bereichsflags**

## <a name="additional-references"></a>Weitere Verweise

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)