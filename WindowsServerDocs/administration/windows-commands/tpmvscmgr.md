---
title: tpmvscmgr
description: Referenz Artikel für tpmvscmgr, ein Befehlszeilen Tool, mit dem Benutzer mit Administrator Anmelde Informationen virtuelle TPM-Smartcards auf einem Computer erstellen und löschen können.
ms.topic: reference
ms.assetid: 8b2c8ff4-5c5d-446d-99e7-4daa1b36a163
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 1dfa4a51c0ea75092e3abf885476e77d3c35435a
ms.sourcegitcommit: f45640cf4fda621b71593c63517cfdb983d1dc6a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/17/2020
ms.locfileid: "92156428"
---
# <a name="tpmvscmgr"></a>tpmvscmgr

Mit dem Befehlszeilen Tool "tpmvscmgr" können Benutzer mit administrativen Anmelde Informationen virtuelle TPM-Smartcards auf einem Computer erstellen und löschen.

## <a name="syntax"></a>Syntax

```
tpmvscmgr create [/name] [/adminkey DEFAULT | PROMPT | RANDOM] [/PIN DEFAULT | PROMPT] [/PUK DEFAULT | PROMPT] [/generate] [/machine] [/?]
```

```
tpmvscmgr destroy [/instance <instanceID>] [/?]
```

### <a name="create-parameters"></a>Erstellen von Parametern

Mit dem **Create** -Befehl werden neue virtuelle Smartcards auf dem System des Benutzers festgelegt. Außerdem wird die Instanz-ID der neu erstellten Karte für den späteren Verweis zurückgegeben, wenn ein Löschvorgang erforderlich ist. Die Instanz-ID hat das Format **root\smartcardreader\000n** , wobei **n** bei 0 beginnt und bei jeder Erstellung einer neuen virtuellen Smartcard um 1 zunimmt.

| Parameter | BESCHREIBUNG |
|--|--|
| /Name | Erforderlich. Gibt den Namen der neuen virtuellen Smartcard an. |
| /adminkey | Gibt den gewünschten Administrator Schlüssel an, der zum Zurücksetzen der PIN der Karte verwendet werden kann, wenn der Benutzer die PIN vergisst. Dies kann Folgendes umfassen:<ul><li>**Default** : gibt den Standardwert von *010203040506070801020304050607080102030405060708*an.</li><li>**Eingabeaufforderung** : fordert den Benutzer auf, einen Wert für den Administrator Schlüssel einzugeben.</li><li>**Random** : führt zu einer zufälligen Einstellung für den Administrator Schlüssel für eine Karte, die nicht an den Benutzer zurückgegeben wird. Dadurch wird eine Karte erstellt, die ggf. nicht mithilfe von Smartcard-Verwaltungs Tools verwaltet werden kann. Bei Verwendung der Option Random muss der Administrator Schlüssel als 48-hexadezimal Zeichen eingegeben werden.</li></ul> |
| /PIN | Gibt den gewünschten Benutzer-PIN-Wert an.<ul><li>**Default** : gibt die Standard-PIN von 12345678 an.</li><li>**Eingabeaufforderung** : fordert den Benutzer zur Eingabe einer PIN in der Befehlszeile auf. Die PIN muss mindestens acht Zeichen lang sein und Ziffern, Zeichen und Sonderzeichen enthalten.</li></ul> |
| /PUK | Gibt den gewünschten PUK-Wert (PIN Unlock Key) an. Der PUK-Wert muss mindestens acht Zeichen lang sein und Ziffern, Zeichen und Sonderzeichen enthalten. Wenn der-Parameter ausgelassen wird, wird die Karte ohne PUK erstellt. Die Optionen lauten:<ul><li>**Default** : gibt das Standard-PUK von *12345678*an.</li><li>**Eingabeaufforderung** : fordert den Benutzer auf, ein PUK in der Befehlszeile einzugeben.</li></ul> |
| /generate | Generiert die Dateien im Speicher, die erforderlich sind, damit die virtuelle Smartcard funktioniert. Wenn Sie den **/Generate** -Parameter nicht verwenden, ist es so, als ob Sie die Karte ohne das zugrunde liegende Dateisystem erstellt haben. Eine Karte ohne Dateisystem kann nur von einem Smartcard-Verwaltungssystem, z. b. Microsoft Configuration Manager, verwaltet werden. |
| /machine | Hiermit können Sie den Namen eines Remote Computers angeben, auf dem die virtuelle Smartcard erstellt werden kann. Dies kann nur in einer Domänen Umgebung verwendet werden und basiert auf DCOM. Damit der Befehl erfolgreich eine virtuelle Smartcard auf einem anderen Computer erstellen kann, muss der Benutzer, der diesen Befehl ausführen muss, Mitglied der lokalen Administratoren Gruppe auf dem Remote Computer sein. |
| /? | Zeigt die Hilfe für diesen Befehl an. |

### <a name="destroy-parameters"></a>Parameter zerstören

Mit dem Befehl **zerstören** wird eine virtuelle Smartcard auf sichere Weise auf dem Computer des Benutzers gelöscht.

> [!WARNING]
> Wenn eine virtuelle Smartcard gelöscht wird, kann Sie nicht wieder hergestellt werden.

| Parameter | BESCHREIBUNG |
|--|--|
| /instance | Gibt die Instanz-ID der virtuellen Smartcard an, die entfernt werden soll. Die InstanceId wurde bei der Erstellung der Karte als Ausgabe tpmvscmgr.exe generiert. Der **/instance** -Parameter ist ein erforderliches Feld für den Befehl **zerstören** . |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Bei alphanumerischen Eingaben ist der vollständige 127-Zeichen-ASCII-Satz zulässig.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um eine virtuelle Smartcard zu erstellen, die später von einem von einem anderen Computer gestarteten Smartcard-Verwaltungs Tool verwaltet werden kann:

```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey DEFAULT /PIN PROMPT
```

Anstatt einen Standard Administrator Schlüssel zu verwenden, können Sie alternativ einen Administrator Schlüssel in der Befehlszeile erstellen. Der folgende Befehl zeigt, wie ein Administrator Schlüssel erstellt wird.

```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey PROMPT /PIN PROMPT
```

Geben Sie Folgendes ein, um eine nicht verwaltete virtuelle Smartcard zu erstellen, die zum Registrieren von Zertifikaten verwendet werden kann:

```
tpmvscmgr.exe create /name VirtualSmartCardForCorpAccess /AdminKey RANDOM /PIN PROMPT /generate
```

Eine virtuelle Smartcard wird mit einem zufälligen Administrator Schlüssel erstellt. Der Schlüssel wird nach dem Erstellen der Karte automatisch verworfen. Dies bedeutet Folgendes: Wenn der Benutzer die PIN vergisst oder die PIN ändern möchte, muss der Benutzer die Karte löschen und erneut erstellen.

Geben Sie Folgendes ein, um die Karte zu löschen:

```
tpmvscmgr.exe destroy /instance <instance ID>
```

Dabei `<instanceID>` ist der auf dem Bildschirm gedruckte Wert, wenn der Benutzer die Karte erstellt hat. Insbesondere bei der ersten erstellten Karte ist die Instanz-ID *root\smartcardreader\0000*.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
