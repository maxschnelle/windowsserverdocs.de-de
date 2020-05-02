---
title: repair-bde
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 534dca1a-05f7-4ea8-ac24-4fe5f14f988a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 501ab801e76980f7e94e88213dd3aa42ee04d4d7
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82722399"
---
# <a name="repair-bde"></a>repair-bde



Der Zugriff auf verschlüsselte Daten auf einer schwer beschädigten Festplatte, wenn das Laufwerk mithilfe von BitLocker verschlüsselt wurde. Mit Repair-bde können wichtige Laufwerksbereiche wiederhergestellt und wiederherstellbare Daten repariert werden, vorausgesetzt ein gültiges Wiederherstellungskennwort oder ein gültiger Wiederherstellungsschlüssel wird zum Entschlüsseln der Daten verwendet. Wenn die BitLocker-Metadaten auf dem Laufwerk beschädigt sind, muss neben einem Wiederherstellungskennwort oder Wiederherstellungsschlüssel ein Sicherungsschlüsselpaket angegeben werden. Dieses Schlüsselpaket wird in den Active Directory-Domänendiensten (AD DS) gesichert, wenn Sie die Standardeinstellung für die AD DS-Sicherung verwendet haben. Mit diesem Schlüsselpaket dem Wiederherstellungskennwort oder Wiederherstellungsschlüssel können Sie Teile eines mit BitLocker geschützten Laufwerks entschlüsseln, wenn die Festplatte beschädigt ist. Jeder Schlüsselpaket funktioniert nur für ein Laufwerk mit der entsprechenden Laufwerkskennung. Mit dem [BitLocker-Wiederherstellungs Kennwort-Viewer](https://technet.microsoft.com/library/dd875531(v=ws.10).aspx) können Sie Active Directory dieses Schlüssel Paket von AD DS abrufen.

> [!NOTE]
> Der BitLocker-Wiederherstellungs Kennwort-Viewer ist als eines der optionalen Verwaltungsfunktionen enthalten, die mithilfe von Server Verwaltung unter Windows Server 2012 installiert werden können.

Für das Befehlszeilen Tool Repair-bde gelten die folgenden Einschränkungen:
-   Repair-bde kann ein Laufwerk nicht reparieren, das während des Verschlüsselungs-oder Entschlüsselungs Prozesses fehlgeschlagen ist.
-   Repair-bde geht davon aus, dass das Laufwerk vollständig verschlüsselt ist, wenn das Laufwerk über eine Verschlüsselung verfügt.



## <a name="syntax"></a>Syntax

```
repair-bde <InputVolume> <OutputVolumeorImage> [-rk] [–rp] [-pw] [–kp] [–lf] [-f] [{-?|/?}]
```

#### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<Inputvolume->|Gibt den Laufwerk Buchstaben des zu reparierenden BitLocker-verschlüsselten Laufwerks an. Der Laufwerk Buchstabe muss einen Doppelpunkt enthalten. Beispiel: **C:**.|
|\<Outputvolumeorimage->|Gibt das Laufwerk an, auf dem der Inhalt des reparierten Laufwerks gespeichert werden soll. Alle Informationen auf dem Ausgabe Laufwerk werden überschrieben.|
|-RK|Gibt den Speicherort des Wiederherstellungs Schlüssels an, der zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch als **-Wiederherstellungsschlüssel**angegeben werden.|
|-RP|Identifiziert das numerische Wiederherstellungs Kennwort, das zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch als **-wiederherstellungkennwort**angegeben werden.|
|-PW|Gibt das Kennwort an, das zum Entsperren des Volumes verwendet werden soll. Dieser Befehl kann auch als **-Kennwort** angegeben werden.|
|-KP|Identifiziert das Wiederherstellungs Schlüssel Paket, das zum Entsperren des Volumes verwendet werden kann. Dieser Befehl kann auch als **-KeyPackage**angegeben werden.|
|-lf|Gibt den Pfad zu der Datei an, in der Fehler-, Warn-und Informationsmeldungen von Repair-bde gespeichert werden. Dieser Befehl kann auch als **-logfile**angegeben werden.|
|-f|Erzwingt das Aufheben der Bereitstellung eines Volumes, auch wenn es nicht gesperrt werden kann. Dieser Befehl kann auch als **-Force**angegeben werden.|
|-? oder /?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

Wenn der Pfad zu einem Schlüssel Paket nicht angegeben wird, durchsucht **Repair-bde** das Laufwerk nach einem Schlüssel Paket. Wenn die Festplatte jedoch beschädigt wurde, ist **Repair-bde** möglicherweise nicht in der Lage, das Paket zu finden, und Sie werden aufgefordert, den Pfad anzugeben.

## <a name="examples"></a>Beispiele

Zum Reparieren von Laufwerk c und zum Schreiben des Inhalts von Laufwerk c auf Laufwerk D mithilfe der Wiederherstellungs Schlüsseldatei (Wiederherstellungsschlüssel. Bek), die auf Laufwerk F gespeichert ist, und Schreiben der Ergebnisse dieses Versuchs in die Protokolldatei (Log. txt) auf Laufwerk Z.
```
repair-bde C: D: -rk F:\RecoveryKey.bek –lf Z:\log.txt
```
Zum Reparieren von Laufwerk c und zum Schreiben des Inhalts auf Laufwerk c in Laufwerk D unter Verwendung des angegebenen Wiederherstellungs Kennworts von 48. Das Wiederherstellungs Kennwort sollte in acht Blöcken mit sechs Ziffern eingegeben werden, wobei ein Bindestrich die einzelnen Blöcke trennt.
```
repair-bde C: D: -rp 111111-222222-333333-444444-555555-666666-777777-888888
```
Um das Aufheben der Bereitstellung von Laufwerk c zu erzwingen, versucht dann, Laufwerk c zu reparieren und den Inhalt auf Laufwerk c auf Laufwerk D zu schreiben, indem Sie das Wiederherstellungs Schlüssel Paket und die Wiederherstellungs Schlüsseldatei (Wiederherstellungs Schlüssel. Bek) verwenden, die auf Laufwerk F gespeichert ist.
```
repair-bde C: D: -kp F:\RecoveryKeyPackage -rk F:\RecoveryKey.bek -f
```
Wenn Sie versuchen, Laufwerk c zu reparieren und den Inhalt von Laufwerk c auf Laufwerk D zu schreiben, müssen Sie ein Kennwort zum Entsperren des Laufwerks c: eingeben, wenn Sie dazu aufgefordert werden:
```
repair-bde C: D: -pw
```

## <a name="additional-references"></a>Zusätzliche Referenzen

-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)