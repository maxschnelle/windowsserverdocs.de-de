---
title: tpmvscmgr
description: Referenz Artikel für tpmvscmgr, ein Befehlszeilen Tool, mit dem Benutzer mit Administrator Anmelde Informationen virtuelle TPM-Smartcards auf einem Computer erstellen und löschen können.
ms.topic: reference
ms.assetid: 8b2c8ff4-5c5d-446d-99e7-4daa1b36a163
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: d5957ff63d7adca1c3800f806b838686cd8aa38f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89640404"
---
# <a name="tpmvscmgr"></a>tpmvscmgr

Mit dem Befehlszeilen Tool "tpmvscmgr" können Benutzer mit administrativen Anmelde Informationen virtuelle TPM-Smartcards auf einem Computer erstellen und löschen.

## <a name="syntax"></a>Syntax

```
Tpmvscmgr create [/name] [/AdminKey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```
```
Tpmvscmgr destroy [/instance <instance ID>] [/?]
```

#### <a name="parameters-for-create-command"></a>Parameter für CREATE-Befehl

Mit dem Create-Befehl werden neue virtuelle Smartcards auf dem System des Benutzers festgelegt. Wenn ein Löschvorgang erforderlich ist, wird die Instanz-ID der neu erstellten Karte für den späteren Verweis zurückgegeben. Die Instanz-ID hat das Format **root\smartcardreader\000n** , wobei **n** bei 0 beginnt und bei jeder Erstellung einer neuen virtuellen Smartcard um 1 zunimmt.

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/Name|Erforderlich. Gibt den Namen der neuen virtuellen Smartcard an.|
|/AdminKey|Gibt den gewünschten Administrator Schlüssel an, der zum Zurücksetzen der PIN der Karte verwendet werden kann, wenn der Benutzer die PIN vergisst.</br>**Standard** Gibt den Standardwert von 010203040506070801020304050607080102030405060708 an.</br>**Eingabeaufforderung** Fordert den Benutzer auf, einen Wert für den Administrator Schlüssel einzugeben.</br>**Zufällig** Führt zu einer zufälligen Einstellung für den Administrator Schlüssel für eine Karte, die nicht an den Benutzer zurückgegeben wird. Dadurch wird eine Karte erstellt, die ggf. nicht mithilfe von Smartcard-Verwaltungs Tools verwaltet werden kann. Beim Generieren mit Random muss der Administrator Schlüssel als 48-hexadezimal Zeichen eingegeben werden.|
|/PIN|Gibt den gewünschten Benutzer-PIN-Wert an.</br>**Standard** Gibt die Standard-PIN von 12345678 an.</br>**Eingabeaufforderung** Fordert den Benutzer zur Eingabe einer PIN in der Befehlszeile auf. Die PIN muss mindestens acht Zeichen lang sein und Ziffern, Zeichen und Sonderzeichen enthalten.|
|/PUK|Gibt den gewünschten PUK-Wert (PIN Unlock Key) an. Der PUK-Wert muss mindestens acht Zeichen lang sein und Ziffern, Zeichen und Sonderzeichen enthalten. Wenn der-Parameter ausgelassen wird, wird die Karte ohne PUK erstellt.</br>**Standard** Gibt das Standard-PUK von 12345678 an.</br>**Eingabeaufforderung** Fordert den Benutzer auf, ein PUK in der Befehlszeile einzugeben.|
|/generate|Generiert die Dateien im Speicher, die erforderlich sind, damit die virtuelle Smartcard funktioniert. Wenn der/Generate-Parameter weggelassen wird, entspricht er dem Erstellen einer Karte ohne dieses Dateisystem. Eine Karte ohne Dateisystem kann nur von einem Smartcard-Verwaltungssystem, z. b. Microsoft Configuration Manager, verwaltet werden.|
|/machine|Hiermit können Sie den Namen eines Remote Computers angeben, auf dem die virtuelle Smartcard erstellt werden kann. Dies kann nur in einer Domänen Umgebung verwendet werden und basiert auf DCOM. Damit der Befehl erfolgreich eine virtuelle Smartcard auf einem anderen Computer erstellen kann, muss der Benutzer, der diesen Befehl ausführen muss, Mitglied der lokalen Administratoren Gruppe auf dem Remote Computer sein.|
|/?|Zeigt die Hilfe für diesen Befehl an.|

#### <a name="parameters-for-destroy-command"></a>Parameter für den Befehl "zerstören"

Mit dem Befehl zerstören wird eine virtuelle Smartcard auf sichere Weise auf dem Computer des Benutzers gelöscht.

> [!WARNING]
> Wenn eine virtuelle Smartcard gelöscht wird, kann Sie nicht wieder hergestellt werden.

|Parameter|BESCHREIBUNG|
|---------|-----------|
|/instance|Gibt die Instanz-ID der virtuellen Smartcard an, die entfernt werden soll. Die InstanceId wurde bei der Erstellung der Karte als Ausgabe Tpmvscmgr.exe generiert. Der/instance-Parameter ist ein erforderliches Feld für den Befehl zerstören.|
|/?|Zeigt die Hilfe für diesen Befehl an.|

## <a name="remarks"></a>Hinweise

Sie müssen mindestens Mitglied der Gruppe " **Administratoren** " (oder einer entsprechenden Gruppe) auf dem Zielcomputer sein, um alle Parameter dieses Befehls ausführen zu können.

Bei alphanumerischen Eingaben ist der vollständige 127-Zeichen-ASCII-Satz zulässig.

## <a name="examples"></a>Beispiele

Der folgende Befehl zeigt, wie Sie eine virtuelle Smartcard erstellen, die später von einem von einem anderen Computer gestarteten Smartcard-Verwaltungs Tool verwaltet werden kann.
```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey DEFAULT /PIN PROMPT
```
Anstatt einen Standard Administrator Schlüssel zu verwenden, können Sie alternativ einen Administrator Schlüssel in der Befehlszeile erstellen. Der folgende Befehl zeigt, wie ein Administrator Schlüssel erstellt wird.
```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey PROMPT /PIN PROMPT
```
Mit dem folgenden Befehl wird die nicht verwaltete virtuelle Smartcard erstellt, die zum Registrieren von Zertifikaten verwendet werden kann.
```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey RANDOM /PIN PROMPT /generate
```
Mit dem folgenden Befehl wird eine virtuelle Smartcard mit einem zufälligen Administrator Schlüssel erstellt. Der Schlüssel wird nach dem Erstellen der Cardis automatisch verworfen. Dies bedeutet Folgendes: Wenn der Benutzer die PIN vergisst oder die PIN ändern möchte, muss der Benutzer die Karte löschen und erneut erstellen. Der Benutzer kann den folgenden Befehl ausführen, um die Karte zu löschen.
```
tpmvscmgr.exe destroy /instance <instance ID>
```
dabei \<instance ID> ist der auf dem Bildschirm gedruckte Wert, wenn der Benutzer die Karte erstellt hat. Insbesondere bei der ersten erstellten Karte ist die Instanz-ID root\smartcardreader\0000.

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)