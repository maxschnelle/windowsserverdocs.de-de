---
title: sc.exe erstellen
description: Referenz Artikel für den sc.exe Create-Befehl, mit dem ein Unterschlüssel und Einträge für einen Dienst in der Registrierung und in der Dienststeuerungs-Manager-Datenbank erstellt werden.
ms.topic: reference
ms.assetid: 59416460-0661-4fef-85cc-73e9d8f4beb4
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 2be59f0d91abdf91984985c536e45abb3cdc0d3f
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388509"
---
# <a name="scexe-create"></a>sc.exe erstellen

Erstellt einen Unterschlüssel und Einträge für einen Dienst in der Registrierung und in der Dienststeuerungs-Manager-Datenbank.

## <a name="syntax"></a>Syntax

```
sc.exe [<servername>] create [<servicename>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto}] [error= {normal | severe | critical | ignore}] [binpath= <binarypathname>] [group= <loadordergroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<accountname> | <objectname>}] [displayname= <displayname>] [password= <password>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
| `<servername>` | Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ . MyServer) verwenden. Verwenden Sie diesen Parameter nicht, um SC.exe lokal auszuführen. |
| `<servicename>` | Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird. |
| `type= {own | share | kernel | filesys | rec | interact type= {own | share}}` | Gibt den Diensttyp an. Die Optionen lauten:<ul><li>**own** : gibt einen Dienst an, der in einem eigenen Prozess ausgeführt wird. Eine ausführbare Datei wird nicht mit anderen Diensten gemeinsam genutzt. Dies ist der Standardwert.</li><li>**Freigabe** : gibt einen Dienst an, der als frei gegebener Prozess ausgeführt wird. Er gibt eine ausführbare Datei mit anderen Diensten frei.</li><li>**Kernel** : gibt einen Treiber an.</li><li>**filesys** : gibt einen Dateisystem Treiber an.</li><li>**rec** : Hiermit wird ein vom Dateisystem erkannter Treiber angegeben, mit dem die auf dem Computer verwendeten Dateisysteme identifiziert werden.</li><li>**Interaktion** : gibt einen Dienst an, der mit dem Desktop interagieren und Eingaben von Benutzern empfangen kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss in Verbindung mit **Type = own** oder **Type = Shared** verwendet werden (z. b. **Type = Interact** **Type = own**). Durch die Verwendung von **Type = Interact** allein wird ein Fehler generiert.</li></ul> |
| `start= {boot | system | auto | demand | disabled | delayed-auto}` | Gibt den Starttyp für den Dienst an. Die Optionen lauten:<ul><li>**Boot** : gibt einen Gerätetreiber an, der vom Start Lade Modul geladen wird.</li><li>**System** : gibt einen Gerätetreiber an, der während der Kernel Initialisierung gestartet wird.</li><li>gibt **automatisch einen** Dienst an, der automatisch gestartet wird, sobald der Computer neu gestartet wird. er wird auch dann ausgeführt, wenn sich niemand am Computer anmeldet.</li><li>**Demand** : gibt einen Dienst an, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **Start =** nicht angegeben ist.</li><li>**deaktiviert** : gibt einen Dienst an, der nicht gestartet werden kann. Ändern Sie den Starttyp in einen anderen Wert, um einen deaktivierten Dienst zu starten.</li><li>**verzögert:** gibt automatisch einen Dienst an, der nach dem Start anderer automatischer Dienste automatisch gestartet wird.</li></ul> |
| `error= {normal | severe | critical | ignore}` | Gibt den Schweregrad des Fehlers an, wenn der Dienst nicht gestartet werden kann, wenn der Computer gestartet wird. Die Optionen lauten:<ul><li>**Normal** : gibt an, dass der Fehler protokolliert und ein Meldungs Feld angezeigt wird, um den Benutzer darüber zu informieren, dass ein Dienst nicht gestartet werden konnte. Der Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</li><li>**schwerwiegend** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Dies könnte dazu führen, dass der Computer neu gestartet werden kann, der Dienst jedoch möglicherweise trotzdem nicht ausgeführt werden kann.</li><li>**kritisch** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Wenn bei der letzten als funktionierend bekannten Konfiguration ein Fehler auftritt, schlägt der Startvorgang fehl, und der Startvorgang wird mit einem Fehler beendet.</li><li>**Ignore** : gibt an, dass der Fehler protokolliert und der Startvorgang fortgesetzt wird. Es wird keine Benachrichtigung an den Benutzer über die Aufzeichnung des Fehlers im Ereignisprotokoll ausgegeben.</li></ul> |
| `binpath= <binarypathname>` | Gibt einen Pfad zur Dienst Binärdatei an. Es gibt keinen Standardwert für " **BinPath =**", und diese Zeichenfolge muss angegeben werden. |
| `group= <loadordergroup>` | Gibt den Namen der Gruppe an, deren Mitglied dieser Dienst ist. Die Liste der Gruppen wird in der Registrierung im Unterschlüssel **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** gespeichert. Der Standardwert ist "null". |
| `tag= {yes | no}` | Gibt an, ob eine TagID aus dem Befehl "| ateservice" abgerufen werden soll. Tags werden nur für Start-und Systemstart-Treiber verwendet. |
| `depend= <dependencies>` | Gibt die Namen der Dienste oder Gruppen an, die vor diesem Dienst gestartet werden müssen. Die Namen werden durch Schrägstriche (/) getrennt. |
| `obj= {<accountname> | <objectname>}` | Gibt den Namen eines Kontos an, in dem ein Dienst ausgeführt wird, oder gibt einen Namen für das Windows-Treiber Objekt an, in dem der Treiber ausgeführt wird. Die Standardeinstellung ist " **LocalSystem**". |
| `displayname= <displayname>` | Gibt einen anzeigen Amen zum Identifizieren des Dienstanbieter in Benutzeroberflächen Programmen an. Beispielsweise ist der Unterschlüssel Name eines bestimmten **dienstaners wuauserv**, der einen freundlicheren anzeigen Amen automatische Updates hat. |
| `password= <password>` | Gibt ein Kennwort an. Dies ist erforderlich, wenn ein anderes Konto als das Konto "LocalSystem" verwendet wird. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Jede Befehlszeilenoption (Parameter) muss das Gleichheitszeichen als Teil des Options namens enthalten.

- Zwischen einer Option und ihrem Wert (z. b. **Type = own**) ist ein Leerzeichen erforderlich. Wenn der Leerraum weggelassen wird, schlägt der Vorgang fehl.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen neuen binären Pfad für den *newservice* -Dienst zu erstellen und zu registrieren:

```
sc.exe \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
```

```
sc.exe create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= +TDI NetBIOS
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
