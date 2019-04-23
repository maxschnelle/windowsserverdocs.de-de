---
title: prnmngr
description: Informationen Sie zum Hinzufügen, löschen und Auflisten von Druckern und Verbindungen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 39eee1a8-4b41-4c9f-941e-486495135eb8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 2c0aa44cc6f27e553bf8c1b57356b884bc0cd632
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887201"
---
# <a name="prnmngr"></a>prnmngr

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Fügt hinzu, löscht und Drucker oder druckerverbindungen, zusätzlich zum Festlegen und Anzeigen von den Standarddrucker aufgeführt.

## <a name="syntax"></a>Syntax
```
cscript Prnmngr {-a | -d | -x | -g | -t | -l | -?}[c] [-s <ServerName>] 
[-p <printerName>] [-m <printermodel>] [-r <PortName>] [-u <UserName>] 
[-w <Password>]
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-a|Fügt eine lokalen Drucker-Verbindung.|
|-d|Löscht eine Druckerverbindung an.|
|-x|Löscht alle Drucker auf dem Server angegeben wird, mit der **-s** Parameter. Wenn Sie keinen Server angeben, löscht Windows alle Drucker auf dem lokalen Computer.|
|-g|Zeigt den Standarddrucker.|
|-t|Legt den Standarddrucker an den Drucker, die gemäß der **-p** Parameter.|
|-l|Listet alle Drucker auf dem vom angegebenen Server installiert die **-s** Parameter. Wenn Sie keinen Server angeben, führt Windows die auf dem lokalen Computer installierten Drucker.|
|c|Gibt an, dass der Parameter für druckerverbindungen gilt. Kann verwendet werden, mit der **– ein** und **- X** Parameter.|
|-s <ServerName>|Gibt den Namen des Remotecomputers, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|
|-p \<Druckername >|Gibt den Namen des Druckers, den Sie verwalten möchten.|
|-m \<DrivermodelName >|Gibt an (nach Namen) der Treiber, die, den Sie installieren möchten. Treiber werden häufig für das Modell des Druckers mit dem Namen, die sie unterstützen. Finden Sie auf Drucker, Weitere Informationen.|
|-R \<PortName >|Gibt den Port, den Drucker verbunden ist. Ist dies einer parallelen oder seriellen Anschluss, verwenden Sie die ID des Ports (z. B. LPT1: oder COM1:). Ist dies ein TCP/IP-Port, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde.|
|-u \<UserName > -w \<Kennwort >|Gibt ein Konto mit Berechtigungen zum Verbinden mit dem Computer, der den Drucker hostet, den Sie verwalten möchten. Alle Mitglieder der lokalen Gruppe Administratoren des Zielcomputers über diese Berechtigungen verfügen, aber die Berechtigungen können auch für andere Benutzer erteilt werden. Wenn Sie ein Konto nicht angeben, müssen Sie über ein Konto mit Berechtigungen für der Befehl funktioniert angemeldet sein.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Prndrvr** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad zu der **Prnmngr** -Datei ein, oder wechseln Sie in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnmngr
    ```
-   Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).

## <a name="BKMK_examples"></a>Beispiele für
Geben Sie zum Hinzufügen eines Druckers mit dem Namen Farbdrucker_2, die LPT1 auf dem lokalen Computer verbunden ist, und erfordert einen Druckertreiber, der Farbe Drucker Driver1 genannt:
```
cscript prnmngr -a -p colorprinter_2 -m "color printer Driver1" -r lpt1:
```
Um den Drucker mit dem Namen Farbdrucker_2 des Remotecomputers, mit dem Namen HRServer zu löschen, geben Sie Folgendes ein:
```
cscript prnmngr -d -s HRServer -p colorprinter_2 
```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
