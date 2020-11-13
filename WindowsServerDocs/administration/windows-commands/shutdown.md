---
title: shutdown
description: Referenz Artikel für den Befehl "Herunterfahren", mit dem Sie lokale Computer oder Remote Computer einzeln Herunterfahren oder neu starten können.
ms.topic: reference
ms.assetid: c432f5cf-c5aa-4665-83af-0ec52c87112e
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e8bd887796dd69645a4238fbbe9316ab6aba8b9b
ms.sourcegitcommit: 6a245fefdf958bfc0aeb69f7a887d11a07bdcd23
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2020
ms.locfileid: "94570295"
---
# <a name="shutdown"></a>shutdown

Ermöglicht das Herunterfahren oder Neustarten von lokalen Computern oder Remote Computern nacheinander.

## <a name="syntax"></a>Syntax

```
shutdown [/i | /l | /s | /sg | /r | /g | /a | /p | /h | /e | /o] [/hybrid] [/fw] [/f] [/m \\computer][/t xxx][/d [p|u:]xx:yy [/c "comment"]]
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
|--|--|
| /i | Zeigt das Kontrollkästchen **Remote herunter** fahren an. Die **/i** -Option muss der erste Parameter sein, der dem Befehl folgt. Wenn **/i** angegeben wird, werden alle anderen Optionen ignoriert. |
| /l | Meldet den aktuellen Benutzer sofort und ohne Timeout Zeitraum ab. **/L** kann nicht mit **/m** oder **/t** verwendet werden. |
| /s | Fährt den Computer herunter. |
| /sg | Fährt den Computer herunter. Wenn beim nächsten Start die **automatische Neustart Anmeldung** aktiviert ist, meldet sich das Gerät automatisch an und sperrt sich basierend auf dem letzten interaktiven Benutzer. Nach der Anmeldung werden alle registrierten Anwendungen neu gestartet. |
| /r | Startet den Computer nach dem Herunterfahren neu. |
| /g | Fährt den Computer herunter. Wenn beim nächsten Neustart die **automatische Neustart Anmeldung** aktiviert ist, meldet sich das Gerät automatisch an und sperrt sich basierend auf dem letzten interaktiven Benutzer. Nach der Anmeldung werden alle registrierten Anwendungen neu gestartet. |
| /a | Bricht das Herunterfahren eines Systems ab. Nur während des Timeout Zeitraums gültig. Um **/a** zu verwenden, müssen Sie auch die **/m** -Option verwenden. |
| /p | Schaltet nur den lokalen Computer (nicht einen Remote Computer) ein – ohne Timeout Zeitraum oder Warnung. Sie können **/p** nur mit **/d** oder **/f** verwenden. Wenn Ihr Computer die ausschalten-Funktionalität nicht unterstützt, wird er bei Verwendung von **/p** heruntergefahren, aber die Leistungsfähigkeit des Computers bleibt erhalten. |
| /h | Versetzt den lokalen Computer in den Ruhezustand, wenn der Ruhezustand aktiviert ist. Sie können **/h** nur mit **/f** verwenden. |
| Hybrid | Das Gerät wird heruntergefahren und für den schnellen Start vorbereitet. Diese Option muss mit der **/s** -Option verwendet werden. |
| /fw | Wenn Sie diese Option mit der Option zum Herunterfahren kombinieren, wird der nächste Neustart zur Firmware-Benutzeroberfläche. |
| /e | Hiermit können Sie den Grund für das unerwartete Herunterfahren auf dem Bereitstellungs Zielcomputer dokumentieren. |
| /o | Wechselt zum Menü **Erweiterte Startoptionen** und startet das Gerät neu. Diese Option muss mit der **/r** -Option verwendet werden. |
| /f | Erzwingt das Schließen der Ausführung von Anwendungen ohne Warn Benutzer.<br>**Vorsicht:** Die Verwendung der **/f** -Option kann zu einem Verlust nicht gespeicherter Daten führen. |
| /m `\\<computername>` | Gibt den Zielcomputer an. Kann nicht mit der **/l** -Option verwendet werden. |
| /t `<xxx>` | Legt den Timeout Zeitraum vor dem Herunterfahren auf *xxx* Sekunden fest. Der gültige Bereich ist 0-315360000 (10 Jahre), der Standardwert ist 30. Wenn der Timeout Zeitraum größer als 0 ist, wird der **/f** -Parameter impliziert. |
| /d `[p | u:]<XX>:<YY>` | Listet den Grund für den Neustart oder das Herunterfahren des Systems auf. Folgende Parameterwerte werden unterstützt:<ul><li>**p** : gibt an, dass der Neustart oder das Herunterfahren geplant ist.</li><li>**u** : gibt an, dass der Grund Benutzer definiert ist.<p>**HINWEIS**<br>Wenn **p** oder **u** nicht angegeben wird, ist der Neustart oder das Herunterfahren nicht geplant.</li><li>*xx* : gibt die Hauptgrund Zahl an (eine positive ganze Zahl, die kleiner als 256 ist).</li><li>*j* Gibt die Nebenzahl an (eine positive ganze Zahl, die kleiner als 65536 ist).</li></ul> |
| /c `<comment>` | Hier können Sie detaillierte Kommentare zum Grund für das Herunterfahren eingeben. Sie müssen zuerst einen Grund angeben, indem Sie die Option **/d** verwenden, und Sie müssen Ihre Kommentare in Anführungszeichen einschließen. Sie können maximal 511 Zeichen verwenden. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an, einschließlich einer Liste der Haupt-und neben Gründe, die auf dem lokalen Computer definiert sind. |

#### <a name="remarks"></a>Hinweise

- Benutzern muss das **System** Benutzerrecht Herunterfahren zugewiesen werden, um einen lokalen oder remote verwalteten Computer zu beenden, der den Befehl **Shutdown** verwendet.

- Benutzer müssen Mitglied der Gruppe " **Administratoren** " sein, um ein unerwartetes Herunterfahren eines lokalen oder remote verwalteten Computers zu kommentieren. Wenn der Zielcomputer einer Domäne angehört, können Mitglieder der Gruppe " **Domänen-Admins** " dieses Verfahren möglicherweise ausführen. Weitere Informationen finden Sie unter

  - [Lokale Standardgruppen](/previous-versions/windows/it-pro/windows-server-2003/cc785098(v=ws.10))

  - [Standardgruppen](/previous-versions/windows/it-pro/windows-server-2003/cc756898(v=ws.10))

- Wenn Sie mehrere Computer gleichzeitig Herunterfahren möchten, können Sie das **herunter** fahren für jeden Computer mithilfe eines Skripts aufrufen, oder Sie können **Shutdown** **/i** verwenden, um das Kontrollkästchen **Remote herunter** fahren anzuzeigen.

- Wenn Sie Haupt-und Nebengrund Codes angeben, müssen Sie diese Ursachen Codes zunächst auf jedem Computer definieren, auf dem Sie die Gründe verwenden möchten. Wenn die Ursachen Codes nicht auf dem Zielcomputer definiert sind, kann das Herunterfahren der Ereignisprotokollierung den richtigen Grund Text nicht protokollieren.

- Denken Sie daran, dass ein Herunterfahren mit dem **p** -Parameter geplant ist. Wenn Sie nicht den **p** -Parameter verwenden, gibt das Herunterfahren nicht geplant.

  - Wenn Sie den **p** -Parameter verwenden, wird das Herunterfahren aufgrund des Ursachen Codes für ein ungeplantes Herunterfahren fehlschlagen.

  - Wenn der **p** -Parameter nicht verwendet wird und nur der Ursachen Code für ein geplantes Herunterfahren bereitgestellt wird, verursacht das Herunterfahren ebenfalls einen Fehler.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um zu erzwingen, dass apps geschlossen werden, und um den lokalen Computer nach einer Verzögerung von einer Minute neu zu starten, und geben Sie myapp.exe *Folgendes ein:*

```
shutdown /r /t 60 /c "Reconfiguring myapp.exe" /f /d p:4:1
```

Um den Remote Computer *myremoteserver* mit denselben Parametern wie im vorherigen Beispiel neu zu starten, geben Sie Folgendes ein:

```
shutdown /r /m \\myremoteserver /t 60 /c "Reconfiguring myapp.exe" /f /d p:4:1
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
