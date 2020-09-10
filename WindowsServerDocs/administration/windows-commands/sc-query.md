---
title: Sc.exe Abfrage
description: Erfahren Sie, wie Sie mithilfe des Hilfsprogramms "sc.exe" Informationen zu Diensten, Treibern, Dienst Typen oder Typen von Treibern abrufen.
ms.topic: reference
ms.assetid: ac365f89-4b20-4de6-a582-b204c5e7d0eb
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: e961badf867237c0725441e138bf4f0ea948155f
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637043"
---
# <a name="scexe-query"></a>Sc.exe Abfrage

Ruft Informationen zum angegebenen Dienst, Treiber, Diensttyp oder Typ des Treibers ab und zeigt diese an.

## <a name="syntax"></a>Syntax

```
sc.exe [<ServerName>] query [<ServiceName>] [type= {driver | service | all}] [type= {own | share | interact | kernel | filesys | rec | adapt}] [state= {active | inactive | all}] [bufsize= <BufferSize>] [ri= <ResumeIndex>] [group= <GroupName>]
```

### <a name="parameters"></a>Parameter

|       Parameter        |                                                                                                                          BESCHREIBUNG                                                                                                                          |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     \<ServerName>      |                       Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ \\ . MyServer) verwenden. Wenn Sie SC.exe lokal ausführen möchten, lassen Sie diesen Parameter Weg.                        |
|     \<ServiceName>     |                                      Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird. Dieser **Abfrage** Parameter wird nicht in Verbindung mit anderen **Abfrage** Parametern (mit Ausnahme von *Servername*) verwendet.                                      |
|     Type = {Driver      |                                                                                                                            Dienst                                                                                                                            |
|       Type = {Own       |                                                                                                                             Freigeben                                                                                                                             |
|     State = {Active     |                                                                                                                           inactive                                                                                                                            |
| buf size = \<BufferSize> |                     Gibt die Größe (in Bytes) des enumerationspuffers an. Die Standardpuffergröße beträgt 1.024 Bytes. Sie sollten die Größe des enumerationspuffers erhöhen, wenn die aus einer Abfrage resultierende Anzeige 1.024 Bytes überschreitet.                      |
|   RI = \<ResumeIndex>   | Gibt die Indexnummer an, bei der die Enumeration gestartet oder fortgesetzt werden soll. Der Standardwert ist **0** (null). Verwenden Sie diesen Parameter in Verbindung mit dem Parameter " **bussize =** ", wenn mehr Informationen von einer Abfrage zurückgegeben werden, als der Standard Puffer anzeigen kann. |
|  Gruppe = \<GroupName>   |                                                                             Gibt die aufzuzählende Dienstgruppe an. Standardmäßig werden alle Gruppen aufgelistet (* * Group = * *).                                                                              |
|           /?           |                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                              |

## <a name="remarks"></a>Hinweise

- Ohne Leerzeichen zwischen einem Parameter und dessen Wert (d. h. **Type = own**, nicht **Type = own**) schlägt der Vorgang fehl.
- Der **Abfrage** Vorgang zeigt die folgenden Informationen zu einem Dienst an: SERVICE_NAME (Name des Registrierungs unter Schlüssels des dienstaners), Typ, Status (und nicht verfügbare Zustände), WIN32_EXIT_B, SERVICE_EXIT_B, Prüfpunkt und WAIT_HINT.
- Der **Type =** -Parameter kann in einigen Fällen zweimal verwendet werden. Die erste Darstellung des **Type =** -Parameters gibt an, ob Dienste, Treiber oder beides (**alle**) abgefragt werden sollen. Die zweite Darstellung des **Type =** -Parameters gibt einen Typ aus dem **Create** -Vorgang an, um den Bereich einer Abfrage weiter einzugrenzen.
- Wenn die von einem **Abfrage** Befehl resultierende Anzeige die Größe des enumerationspuffers überschreitet, wird eine Meldung ähnlich der folgenden angezeigt:
  ```
  Enum: more data, need 1822 bytes start resume at index 79
  ```
  Um die restlichen **Abfrage** Informationen anzuzeigen, führen Sie die **Abfrage**erneut aus, und legen Sie für " **bufsize =** " die Anzahl von Bytes und für " **RI =** " den angegebenen Index fest. Beispielsweise würde die verbleibende Ausgabe angezeigt werden, indem Sie an der Eingabeaufforderung Folgendes eingeben:
  ```
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
Geben Sie Folgendes ein, um Informationen für den wuauserv-Dienst anzuzeigen:
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
Geben Sie Folgendes ein, um Informationen für Treiber in der Network Driver Interface Specification (NDIS)-Gruppe anzuzeigen:
```
sc.exe query type= driver group= ndis
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
