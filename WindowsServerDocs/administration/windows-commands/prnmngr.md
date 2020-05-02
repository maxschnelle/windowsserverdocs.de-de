---
title: prnmngr
description: Erfahren Sie, wie Sie Drucker und Verbindungen hinzufügen, löschen und auflisten.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 0851e5c24d743a80b7edc611306df4f65338d95d
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722825"
---
# <a name="prnmngr"></a>prnmngr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Drucker oder Drucker Verbindungen hinzu, löscht sie und listet diese neben dem festlegen und Anzeigen des Standard Druckers auf.

## <a name="syntax"></a>Syntax
```
cscript Prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <ServerName>] 
[-p <printerName>] [-m <printermodel>] [-r <PortName>] [-u <UserName>] 
[-w <Password>]
```

### <a name="parameters"></a>Parameter

|           Parameter           |                                                                                                                                                                                        BESCHREIBUNG                                                                                                                                                                                        |
|-------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -a               |                                                                                                                                                                             Fügt eine lokale Druckerverbindung hinzu.                                                                                                                                                                              |
|              -d               |                                                                                                                                                                               Löscht eine Druckerverbindung.                                                                                                                                                                               |
|              -X               |                                                                                                               Löscht alle Drucker von dem Server, der mit dem **-s-** Parameter angegeben wird. Wenn Sie keinen Server angeben, löscht Windows alle Drucker auf dem lokalen Computer.                                                                                                               |
|              -g               |                                                                                                                                                                               Zeigt den Standarddrucker an.                                                                                                                                                                               |
|              -t               |                                                                                                                                                        Legt den Standarddrucker auf den Drucker fest, der durch den **-p-** Parameter angegeben wird.                                                                                                                                                         |
|              -l               |                                                                                                         Listet alle Drucker auf, die auf dem durch den **-s-** Parameter angegebenen Server installiert sind. Wenn Sie keinen Server angeben, werden die auf dem lokalen Computer installierten Drucker von Windows aufgelistet.                                                                                                         |
|               c               |                                                                                                                                      Gibt an, dass der-Parameter für Drucker Verbindungen gilt. Kann mit den Parametern **-a** und **-x** verwendet werden.                                                                                                                                      |
|        -s<ServerName>        |                                                                                                                  Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.                                                                                                                  |
|       -p \<PrinterName>       |                                                                                                                                                                Gibt den Namen des Druckers an, den Sie verwalten möchten.                                                                                                                                                                 |
|     -m \<drivermodelname>     |                                                                                                          Gibt (nach Name) den Treiber an, den Sie installieren möchten. Treiber werden oft für das Drucker Modell benannt, das Sie unterstützen. Weitere Informationen finden Sie in der Druckerdokumentation.                                                                                                           |
|        -r \<Portname>         |                                                                         Gibt den Port an, mit dem der Drucker verbunden ist. Wenn es sich um einen parallelen oder seriellen Anschluss handelt, verwenden Sie die ID des Ports (z. b. LPT1: oder COM1:). Wenn dies ein TCP/IP-Port ist, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde.                                                                          |
| -u \<Benutzername>- \<w-Kennwort> | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
|              /?               |                                                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                            |

## <a name="remarks"></a>Bemerkungen
-   Der **prndrvr** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis "%windir%\SYSTEM32\ printing_Admin_Scripts\\ <language> " befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** gefolgt vom vollständigen Pfad zur Datei **Prnmngr** ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen `"computer Name"`(z. b.).

## <a name="examples"></a><a name="BKMK_examples"></a>Beispiele
Wenn Sie einen Drucker mit dem Namen colorprinter_2 hinzufügen möchten, der auf dem lokalen Computer mit LPT1 verbunden ist und einen Druckertreiber namens Color Printer Driver1 erfordert, geben Sie Folgendes ein:
```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```
Geben Sie Folgendes ein, um den Drucker mit dem Namen colorprinter_2 vom Remote Computer "hrserver" zu löschen:
```
cscript prnmngr -d -s HRServer -p colorprinter_2 
```

## <a name="additional-references"></a>Zusätzliche Referenzen
- [Befehlszeilen Syntax Schlüssel](command-line-syntax-key.md)
[Print-Befehlsreferenz](print-command-reference.md)
