---
title: Sc.exe Abfrage
description: Referenz Artikel für den sc.exe Query-Befehl, der Informationen über den angegebenen Dienst, Treiber, Diensttyp oder den Typ des Treibers abruft und anzeigt.
ms.topic: reference
ms.assetid: ac365f89-4b20-4de6-a582-b204c5e7d0eb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 7d5994c54914165cb79ba0f505f1a44b2d7f019a
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388213"
---
# <a name="scexe-query"></a>Sc.exe Abfrage

Ruft Informationen zum angegebenen Dienst, Treiber, Diensttyp oder Typ des Treibers ab und zeigt diese an.

## <a name="syntax"></a>Syntax

```
sc.exe [<servername>] query [<servicename>] [type= {driver | service | all}] [type= {own | share | interact | kernel | filesys | rec | adapt}] [state= {active | inactive | all}] [bufsize= <Buffersize>] [ri= <Resumeindex>] [group= <groupname>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| `<servername>` | Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ . MyServer) verwenden. Verwenden Sie diesen Parameter nicht, um SC.exe lokal auszuführen. |
| `<servicename>` | Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird. Dieser **Abfrage** Parameter wird nicht in Verbindung mit anderen **Abfrage** Parametern (mit Ausnahme von *Servername*) verwendet. |
| `type= {driver | service | all}` | Gibt an, was aufgezählt werden soll. Die Optionen lauten:<ul><li>**Driver** : gibt an, dass nur Treiber aufgelistet werden.</li><li>**Dienst** : gibt an, dass nur Dienste aufgelistet werden. Dies ist der Standardwert.</li><li>**all** : gibt an, dass sowohl Treiber als auch Dienste aufgelistet werden.</li></ul> |
| `type= {own | share | interact | kernel | filesys | rec | adapt}` | Gibt den Typ der Dienste oder des Typs der aufzuzählenden Treiber an. Die Optionen lauten:<ul><li>**own** : gibt einen Dienst an, der in einem eigenen Prozess ausgeführt wird. Eine ausführbare Datei wird nicht mit anderen Diensten gemeinsam genutzt. Dies ist der Standardwert.</li><li>**Freigabe** : gibt einen Dienst an, der als frei gegebener Prozess ausgeführt wird. Er gibt eine ausführbare Datei mit anderen Diensten frei.</li><li>**Kernel** : gibt einen Treiber an.</li><li>**filesys** : gibt einen Dateisystem Treiber an.</li><li>**rec** : Hiermit wird ein vom Dateisystem erkannter Treiber angegeben, mit dem die auf dem Computer verwendeten Dateisysteme identifiziert werden.</li><li>**Interaktion** : gibt einen Dienst an, der mit dem Desktop interagieren und Eingaben von Benutzern empfangen kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss in Verbindung mit **Type = own** oder **Type = Shared** verwendet werden (z. b. **Type = Interact** **Type = own**). Durch die Verwendung von **Type = Interact** allein wird ein Fehler generiert.</li></ul> |
| `state= {active | inactive | all}` | Gibt den gestarteten Zustand des aufzuzählenden Dienstanbieter an. Die Optionen lauten:<ul><li>**aktiv** : Hiermit werden alle aktiven Dienste angegeben. Dies ist der Standardwert.</li><li>**inaktiv** : Hiermit werden alle angehaltenen oder beendeten Dienste angegeben.</li><li>**all** : gibt alle-Dienste an.</li></ul> |
| `bufsize= <Buffersize>` | Gibt die Größe (in Bytes) des enumerationspuffers an. Die Standardpuffergröße beträgt 1.024 Bytes. Sie sollten die Größe des Puffers vergrößern, wenn die aus einer Abfrage resultierende Anzeige mehr als 1.024 Bytes übersteigt. |
| `ri= <Resumeindex>` | Gibt die Indexnummer an, bei der die Enumeration gestartet oder fortgesetzt werden soll. Der Standardwert ist 0 (null). Wenn mehr Informationen zurückgegeben werden, als der Standard Puffer anzeigen kann, verwenden Sie diesen Parameter mit dem- `bufsize=` Parameter. |
| `group= <Groupname>` | Gibt die aufzuzählende Dienstgruppe an. Standardmäßig werden alle Gruppen aufgelistet. Standardmäßig werden alle Gruppen aufgelistet (* * Group = * *). |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Jede Befehlszeilenoption (Parameter) muss das Gleichheitszeichen als Teil des Options namens enthalten.

- Zwischen einer Option und ihrem Wert (z. b. **Type = own**) ist ein Leerzeichen erforderlich. Wenn der Leerraum weggelassen wird, schlägt der Vorgang fehl.

- Der **Abfrage** Vorgang zeigt die folgenden Informationen zu einem Dienst an: SERVICE_NAME (Name des Registrierungs unter Schlüssels des dienstaners), Typ, Status (und nicht verfügbare Zustände), WIN32_EXIT_B, SERVICE_EXIT_B, Prüfpunkt und WAIT_HINT.

- Der **Type =** -Parameter kann in einigen Fällen zweimal verwendet werden. Die erste Darstellung des **Type =** -Parameters gibt an, ob Dienste, Treiber oder beides (**alle**) abgefragt werden sollen. Die zweite Darstellung des **Type =** -Parameters gibt einen Typ aus dem **Create** -Vorgang an, um den Bereich einer Abfrage weiter einzugrenzen.

- Wenn die Anzeigeergebnisse von einem **Abfrage** Befehl die Größe des enumerationspuffers überschreitet, wird eine Meldung ähnlich der folgenden angezeigt:

  ```
  Enum: more data, need 1822 bytes start resume at index 79

  To display the remaining **query** information, rerun **query**, setting **bufsize=** to be the number of bytes and setting **ri=** to the specified index. For example, the remaining output would be displayed by typing the following at the command prompt:

  sc.exe query bufsize= 1822 ri= 79
  ```

## <a name="examples"></a>Beispiele

Wenn Sie nur Informationen für aktive Dienste anzeigen möchten, geben Sie einen der folgenden Befehle ein:

```
sc.exe query
sc.exe query type= service
```

Um Informationen für aktive Dienste anzuzeigen und eine Puffergröße von 2.000 Bytes anzugeben, geben Sie Folgendes ein:

```
sc.exe query type= all bufsize= 2000
```

Geben Sie Folgendes ein, um Informationen für den *wuauserv* -Dienst anzuzeigen:

```
sc.exe query wuauserv
```

Geben Sie Folgendes ein, um Informationen für alle Dienste anzuzeigen (aktiv und inaktiv):

```
sc.exe query state= all
```

Zum Anzeigen von Informationen für alle Dienste (aktiv und inaktiv) geben Sie ab Zeile 56 Folgendes ein:

```
sc.exe query state= all ri= 56
```

Geben Sie Folgendes ein, um Informationen für interaktive Dienste anzuzeigen:

```
sc.exe query type= service type= interact
```

Geben Sie Folgendes ein, um nur Informationen für Treiber anzuzeigen:

```
sc.exe query type= driver
```

Geben Sie Folgendes ein, um Informationen für Treiber in der *Network Driver Interface Specification (NDIS)-Gruppe*anzuzeigen:

```
sc.exe query type= driver group= NDIS
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
