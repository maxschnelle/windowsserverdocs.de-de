---
title: SC-Abfrage
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac365f89-4b20-4de6-a582-b204c5e7d0eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 60b6e945c4b2944f97d40cbc27694acc2915c615
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441621"
---
# <a name="sc-query"></a>SC-Abfrage



Ruft ab und zeigt Informationen zu den angegebenen Dienst, Treiber, Diensttyp oder Typ des Treibers.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] query [<ServiceName>] [type= {driver | service | all}] [type= {own | share | interact | kernel | filesys | rec | adapt}] [state= {active | inactive | all}] [bufsize= <BufferSize>] [ri= <ResumeIndex>] [group= <GroupName>]
```

## <a name="parameters"></a>Parameter

|       Parameter        |                                                                                                                          Beschreibung                                                                                                                          |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     \<ServerName>      |                       Gibt den Namen des Remoteservers auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format verwenden (z. B. \\ \\"myserver"). Um SC.exe lokal ausführen zu können, müssen lassen Sie diesen Parameter Weg.                        |
|     \<ServiceName>     |                                      Gibt den Dienstnamen, die zurückgegeben werden, indem die **Getkeyname** Vorgang. Dies **Abfrage** Parameter wird nicht verwendet, im Zusammenhang mit anderen **Abfrage** Parameter (außer *ServerName*).                                      |
|     Typ = {-Treiber      |                                                                                                                            Dienst                                                                                                                            |
|       Typ = {besitzen       |                                                                                                                             Freigeben                                                                                                                             |
|     Status = {Aktiv     |                                                                                                                           inaktiv                                                                                                                            |
| bufsize= \<BufferSize> |                     Gibt die Größe (in Byte) des Puffers Enumeration. Die Standardpuffergröße ist 1.024 Bytes. Sie sollten die Größe des Puffers Enumeration erhöhen, wenn die Anzeige, die aus einer Abfrage resultierenden 1.024 Bytes überschreitet.                      |
|   ri= \<ResumeIndex>   | Gibt die Indexnummer, die bei der Enumeration ist, um zu beginnen oder fortsetzen. Der Standardwert ist **0** (null). Verwenden Sie diesen Parameter in Verbindung mit der **Bufsize =** Parameter an, wenn Informationen von einer Abfrage zurückgegeben wird, als der Standardpuffer angezeigt werden kann. |
|  group= \<GroupName>   |                                                                             Gibt die Dienstgruppe aufgelistet werden sollen. Standardmäßig werden alle Gruppen aufgelistet (**Group = ""** ).                                                                              |
|           /?           |                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                              |

## <a name="remarks"></a>Hinweise

- Ohne Leerzeichen zwischen einem Parameter und dessen Wert (d. h. **Typ = eigenen**, nicht **Typ = eigenen**), der Vorgang schlägt fehl.
- Die **Abfrage** Prozess zeigt die folgende Informationen zu einem Dienst: SERVICE_NAME (des Diensts Registrierung Unterschlüsselnamen), TYPE, STATE (sowie die Zustände, die nicht verfügbar sind), WIN32_EXIT_B, SERVICE_EXIT_B, CHECKPOINT und WAIT_HINT.
- Die **Typ =** Parameter kann in einigen Fällen zweimal verwendet werden. Die erste Darstellung der **Typ =** Parameter gibt an, ob Dienste, Treiber oder beide Abfragen (**alle**). Die zweite Darstellung der **Typ =** Parameter gibt an, einen Typ aus der **erstellen** Vorgang, um den Umfang einer Abfrage einzugrenzen.
- Wenn die Anzeige, die aus einem **Abfrage** Befehl überschreitet die Größe des Puffers Enumeration ist, wird eine Meldung ähnlich der folgenden angezeigt:  
  ```
  Enum: more data, need 1822 bytes start resume at index 79
  ```  
  Zum Anzeigen der verbleibenden **Abfrage** Informationen erneut ausführen **Abfrage**, wobei **Bufsize =** gleich der Anzahl der Bytes und die Einstellung **ri =** auf der angegebene Index. Beispielsweise würde die verbleibende Ausgabe angezeigt werden, indem Sie Folgendes an der Eingabeaufforderung eingeben:  
  ```
  sc query bufsize= 1822 ri= 79
  ```

## <a name="BKMK_examples"></a>Beispiele für

Geben Sie zum Anzeigen von Informationen für die aktiven Dienste nur einen der folgenden Befehle aus:
```
sc query
sc query type= service
```
Informationen für den aktiven Dienste an, und geben Sie eine Puffergröße von 2.000 Bytes, geben Sie ein:
```
sc query type= all bufsize= 2000
```
Um Informationen für den Dienst WUAUSERV anzuzeigen, geben Sie Folgendes ein:
```
sc query wuauserv
```
Anzeigen von Informationen für alle Dienste (aktive und inaktive) Geben Sie Folgendes ein:
```
sc query state= all
```
Um Informationen für alle Dienste ("aktiv" und "inaktiv"), beginnend bei Zeile 56 anzuzeigen, geben Sie Folgendes ein:
```
sc query state= all ri= 56
```
Um Informationen für die interaktive Dienste anzuzeigen, geben Sie Folgendes ein:
```
sc query type= service type= interact
```
Um Informationen für Treiber nur anzuzeigen, geben Sie Folgendes ein:
```
sc query type= driver
```
Um Informationen für den Treiber in der Gruppe der Network Driver Interface Specification (NDIS) anzuzeigen, geben Sie Folgendes ein:
```
sc query type= driver group= ndis
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)