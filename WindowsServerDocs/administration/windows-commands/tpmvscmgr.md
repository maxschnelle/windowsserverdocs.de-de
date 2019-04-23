---
title: tpmvscmgr
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8b2c8ff4-5c5d-446d-99e7-4daa1b36a163
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f6cfc15b7c089c9b6ad4d9a267b951373e63a63a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59888591"
---
# <a name="tpmvscmgr"></a>tpmvscmgr



Das Befehlszeilentool von tpmvscmgr kann Benutzer mit administrativen Anmeldeinformationen erstellen und Löschen von virtuellen Smartcards TPM auf einem Computer. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Tpmvscmgr create [/name] [/AdminKey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```
```
Tpmvscmgr destroy [/instance <instance ID>] [/?]
```

### <a name="parameters-for-create-command"></a>Parameter für die Create-Befehl.

Create-Befehl richtet ein neues virtuelle Smartcards: auf dem System des Benutzers. Es gibt die Instanz-ID der neu erstellte Karte zur späteren Bezugnahme zurück, wenn löschen erforderlich ist. Die Instanz-ID im Format ist **ROOT\SMARTCARDREADER\000n** , in denen **n** bei 0 beginnt und jedes Mal, die Sie eine neue virtuelle Smartcard erstellen um 1 erhöht.

|Parameter|Beschreibung|
|---------|-----------|
|/ name|Erforderlich. Gibt den Namen der neuen virtuellen Smartcard.|
|/AdminKey|Gibt den gewünschten Administratorschlüssel, der zum Zurücksetzen der PIN der Karte, wenn der Benutzer die PIN vergisst verwendet werden kann.</br>**STANDARDMÄßIGE** gibt den Standardwert des 010203040506070801020304050607080102030405060708.</br>**EINGABEAUFFORDERUNG** fordert den Benutzer auf einen Wert für den Administratorschlüssel eingeben.</br>**ZUFÄLLIGE** führt zu einer zufälligen Einstellung für den Administratorschlüssel für eine Karte, die nicht für den Benutzer zurückgegeben wird. Dadurch wird eine Karte, die nicht verwaltet werden kann, mithilfe einer Smartcard-Verwaltungstools erstellt. Wenn mit zufällig generiert wird, muss der Administratorschlüssel als 48 hexadezimalen Zeichen eingegeben werden.|
|/PIN|Gibt die gewünschte Benutzer-PIN-Wert an.</br>**STANDARDMÄßIGE** gibt an, die Standard-PIN des 12345678.</br>**EINGABEAUFFORDERUNG** fordert den Benutzer zur Eingabe einer PIN in der Befehlszeile. Die PIN muss mindestens acht Zeichen sein und Zeichen, Zahlen und Sonderzeichen enthalten kann.|
|/PUK|Gibt den gewünschten Wert für die PIN entsperren Schlüssel (PUK) an. Der PUK-Wert muss mindestens acht Zeichen sein, und es kann Zahlen, Zeichen und Sonderzeichen enthalten. Wenn der Parameter ausgelassen wird, wird die Karte ohne eine PUK erstellt.</br>**STANDARDMÄßIGE** gibt die Standardvordergrundfarbe für PUK von 12345678.</br>**EINGABEAUFFORDERUNG** für den Benutzer werden aufgefordert, eine PUK in der Befehlszeile eingeben.|
|/generate|Generiert die Dateien im Speicher, die für die virtuelle Smartcard funktionieren erforderlich sind. Wenn die / generieren Parameter ausgelassen wird, dies ist äquivalent zum Erstellen einer Karte ohne dieses Dateisystem. Eine Karte ohne Dateisystem kann nur von einer Smartcard-Verwaltungssystems wie Microsoft Configuration Manager verwaltet werden.|
|/ machine|Können Sie den Namen eines Remotecomputers angeben, auf dem die virtuelle Smartcard erstellt werden können. Dies kann in einer domänenumgebung nur verwendet werden, und es beruht auf DCOM. Der Befehl erfolgreich ausgeführt werden, erstellen Sie eine virtuelle Smartcard auf einem anderen Computer muss der Benutzer das Ausführen dieses Befehls ein Element in der lokalen Administratorengruppe auf dem Remotecomputer sein.|
|/?|Zeigt die Hilfe für diesen Befehl.|

### <a name="parameters-for-destroy-command"></a>Parameter für Destroy-Befehle

Destroy-Befehle werden sicher eine virtuelle Smartcard gelöscht, von dem Computer des Benutzers.

> [!WARNING]
> Wenn eine virtuelle Smartcard gelöscht wird, kann nicht wiederhergestellt werden.

|Parameter|Beschreibung|
|---------|-----------|
|/ Instanz|Gibt die Instanz-ID der virtuellen Smartcard entfernt werden soll. Die Instanz-ID wurde als Ausgabe vom Tpmvscmgr.exe generiert, wenn die Karte erstellt wurde. Der Parameter/Instanz ist ein erforderliches Feld für den Befehl löschen.|
|/?|Zeigt die Hilfe für diesen Befehl.|

## <a name="remarks"></a>Hinweise

Mitgliedschaft in der **Administratoren** Gruppe (oder Äquivalent) auf dem Zielcomputer ist mindestens erforderlich, um alle Parameter mit diesem Befehl ausführen.

Bei alphanumerischen Eingaben ist die vollständige 127 ASCII-Zeichensatz zulässig.

## <a name="BKMK_Examples"></a>Beispiele für

Der folgende Befehl zeigt, wie Sie eine virtuelle Smartcard erstellen, die später durch eine Smartcard-Verwaltungstool, die von einem anderen Computer gestartet verwaltet werden können.
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey DEFAULT /PIN PROMPT
```
Anstatt einen Administrator Standardschlüssel verwenden, können Sie alternativ einen Administratorschlüssel in der Befehlszeile erstellen. Der folgende Befehl zeigt, wie Sie einen Administratorschlüssel zu erstellen.
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey PROMPT /PIN PROMPT
```
Der folgende Befehl wird die nicht verwaltete virtuelle Smartcard erstellen, die zum Registrieren von Zertifikaten verwendet werden kann.
```
tpmvscmgr.exe create /name "VirtualSmartCardForCorpAccess" /AdminKey RANDOM /PIN PROMPT /generate
```
Der folgende Befehl erstellt eine virtuelle Smartcard mit einem Administratorschlüssel nach dem Zufallsprinzip. Der Schlüssel wird nach der Cardis erstellt automatisch verworfen. Dies bedeutet, dass wenn der Benutzer die PIN vergisst oder die Änderung die PIN möchte, der Benutzer benötigt auf die Karte löschen und neu erstellt werden. Um die Karte zu löschen, kann der Benutzer den folgenden Befehl ausführen.
```
tpmvscmgr.exe destroy /instance <instance ID> 
```
wo \<Instanz-ID > ist der Wert ausgegeben auf dem Bildschirm, wenn der Benutzer die Karte erstellt. Insbesondere ist die Instanz-ID für die erste Karte erstellt wird, ROOT\SMARTCARDREADER\0000.

#### <a name="additional-references"></a>Weitere Verweise

-   [Befehlszeilensyntax](command-line-syntax-key.md)