---
title: prnmngr
description: Referenz Artikel zum prnmngr-Befehl, der Drucker oder Drucker Verbindungen hinzufügt, löscht und auflistet, zusätzlich zum Festlegen und Anzeigen des Standard Druckers.
ms.topic: reference
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 07/11/2018
ms.openlocfilehash: cfbba48747dfca7230f0ef397201cea610fdc3dd
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89628057"
---
# <a name="prnmngr"></a>prnmngr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Drucker oder Drucker Verbindungen hinzu, löscht sie und listet diese neben dem festlegen und Anzeigen des Standard Druckers auf. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad zur Datei prnmngr ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr`.

## <a name="syntax"></a>Syntax

```
cscript prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <Servername>] [-p <Printername>] [-m <printermodel>] [-r <portname>] [-u <Username>]
[-w <password>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -a | Fügt eine lokale Druckerverbindung hinzu. |
| -d | Löscht eine Druckerverbindung. |
| -X | Löscht alle Drucker von dem Server, der durch den **-s-** Parameter angegeben wird. Wenn Sie keinen Server angeben, löscht Windows alle Drucker auf dem lokalen Computer. |
| -g | Zeigt den Standarddrucker an. |
| -t | Legt den Standarddrucker auf den Drucker fest, der durch den **-p-** Parameter angegeben wird. |
| -l | Listet alle Drucker auf, die auf dem durch den **-s-** Parameter angegebenen Server installiert sind. Wenn Sie keinen Server angeben, werden die auf dem lokalen Computer installierten Drucker von Windows aufgelistet. |
| c | Gibt an, dass der-Parameter für Drucker Verbindungen gilt. Kann mit den Parametern **-a** und **-x** verwendet werden. |
| -s `<Servername>` | Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| -p `<Printername>` | Gibt den Namen des Druckers an, den Sie verwalten möchten. |
| -m `<Modelname>` | Gibt (nach Name) den Treiber an, den Sie installieren möchten. Treiber werden oft für das Drucker Modell benannt, das Sie unterstützen. Weitere Informationen finden Sie in der Druckerdokumentation. |
| -r `<portname>` | Gibt den Port an, mit dem der Drucker verbunden ist. Wenn es sich um einen parallelen oder seriellen Anschluss handelt, verwenden Sie die ID des Ports (z. b. LPT1: oder COM1:). Wenn dies ein TCP/IP-Port ist, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde. |
| -u `<Username>` -w `<password>` | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

### <a name="examples"></a>Beispiele

Wenn Sie einen Drucker mit dem Namen colorprinter_2 hinzufügen möchten, der auf dem lokalen Computer mit LPT1 verbunden ist und einen Druckertreiber namens Color Printer Driver1 erfordert, geben Sie Folgendes ein:

```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```

Geben Sie Folgendes ein, um den Drucker mit dem Namen colorprinter_2 vom Remote Computer "hrserver" zu löschen:

```
cscript prnmngr -d -s HRServer -p colorprinter_2
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
