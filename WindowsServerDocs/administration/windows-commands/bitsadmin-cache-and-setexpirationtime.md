---
Title: Bitsadmin Cache und Setexpirationtime Beschreibung: "Windows-Befehle Thema **Bitsadmin Cache und Setexpirationtime** -legt die Ablaufzeit für den Cache."
ms.custom: na ms.prod: windows-server-threshold ms.reviewer: na ms.suite: na ms.technology: manage-windows-commands ms.tgt_pltfrm: na ms.topic: article ms.assetid: 00ea6e4e-b707-4b31-88dd-b61a78565c8d author: coreyp-at-msft ms.author: coreyp manager: dongill ms.date: 10/16/2017 --

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

# <a name="bitsadmin-cache-and-setexpirationtime"></a>Bitsadmin-Cache und setexpirationtime
Legt die Ablaufzeit für den Cache fest.
## <a name="syntax"></a>Syntax
```
bitsadmin /Cache /SetExpirationtime secs
```
## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|Sekunden|Die Anzahl der Sekunden, bis der Cache abläuft.|
## <a name="BKMK_examples"></a>Beispiele für
Im folgende Beispiel läuft den Cache in 60 Sekunden.
```
C:\>bitsadmin /Cache / SetExpirationtime 60
```
## <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilensyntax](command-line-syntax-key.md)
