---
title: Sc config
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ad4d68a6-efe5-452b-8501-7f1f1c552a4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: 361a8407aae3b5e823b58cd71b97b043159146e6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837221"
---
# <a name="sc-config"></a>Sc config



Ändert den Wert eines Diensts Einträge in der Registrierung und in der Dienststeuerungs-Manager-Datenbank.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] config [<ServiceName>] [type= {own | share | kernel | filesys | rec | adapt | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ServerName>|Gibt den Namen des Remoteservers auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format verwenden (z. B. \\ \\"myserver"). Um SC.exe lokal ausführen zu können, müssen lassen Sie diesen Parameter Weg.|
|\<ServiceName>|Gibt den Dienstnamen, die zurückgegeben werden, indem die **Getkeyname** Vorgang.|
|Typ = {eigenen\| freigeben \| Kernel \| Filesys \| Rec \| anpassen \| interagieren, Typ = {eigenen \| freigeben}} | Gibt den Diensttyp an.</br>**eigene** -gibt einen Dienst, der in einem eigenen Prozess ausgeführt wird. Es gibt eine ausführbare Datei nicht mit anderen Diensten frei. Dies ist der Standardwert.</br>**Freigeben von** – gibt an, ein Dienst, der als einen gemeinsam genutzten Prozess ausgeführt wird. Es gibt eine ausführbare Datei für andere Dienste frei.</br>**Kernel** – gibt an, einen Treiber.</br>**Filesys** – gibt an, einem Dateisystemtreiber.</br>**REC** – gibt an, ein System erkannt-Treiber, die Dateisysteme, die auf dem Computer verwendeten identifiziert.</br>**Passen Sie** : Gibt an, einen Adaptertreiber, die Hardwaregeräte wie z. B. Tastaturen, Mäuse, identifiziert und Festplattenlaufwerke.</br>**Interaktion** -gibt einen Dienst, der Interaktion mit dem Desktop, Eingaben von Benutzern empfangen. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss verwendet werden, zusammen mit **Typ = eigenen** oder **Typ = freigegebene** (z. B. **Typ = interagieren** **Typ = eigenen**). Mithilfe von **Typ = interagieren** , wird einen Fehler generiert.|
|Start = {Boot \| System \| automatisch \| Bedarf \| deaktiviert \| -automatische}|Gibt den Starttyp für den Dienst an.</br>**Start** – gibt an, einen Gerätetreiber, die durch Bootloader geladen wird.</br>**System** – gibt an, einen Gerätetreiber, die während der Kernelinitialisierung gestartet wird.</br>**automatische** : Gibt an, ein Dienst, der automatisch startet jedes Computers Zeit wird neu gestartet und ausgeführt wird, auch wenn niemand am Computer anmeldet.</br>**bei Bedarf** – gibt an, ein Dienst, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **starten =** nicht angegeben ist.</br>**deaktiviert** – gibt an, ein Dienst, der nicht gestartet werden kann. Um eines deaktivierten Dienstes zu starten, ändern Sie den Starttyp auf einen anderen Wert ein.</br>**-automatische** -gibt einen Dienst, der eine kurze Zeit automatisch gestartet, nachdem andere Dienste automatisch gestartet werden.|
|Fehler = {normal \| schwerwiegende \| kritische \| ignorieren}|Gibt den Schweregrad des Fehlers an, wenn der Dienst nicht beim Booten hochfährt.</br>**normale** – gibt an, dass der Fehler protokolliert wird und ein Meldungsfeld angezeigt wird, informiert den Benutzer, der ein Dienst nicht gestartet werden konnte. Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</br>**schwerwiegende** – gibt an, dass der Fehler (sofern möglich) protokolliert wird. Der Computer versucht, mit der letzten bekannten guten Konfiguration neu zu starten. Könnte dies auf dem Computer gestartet werden kann, aber der Dienst ist möglicherweise immer noch in der kann nicht ausgeführt werden.</br>**kritische** – gibt an, dass der Fehler (sofern möglich) protokolliert wird. Der Computer versucht, mit der letzten bekannten guten Konfiguration neu zu starten. Wenn die letzten bekannten gute Konfiguration ein Fehler auftritt, starten auch ein Fehler auftritt und des Startvorgangs wird mit einem Abbruchfehler angehalten.</br>**ignorieren Sie** – gibt an, dass der Fehler protokolliert wird und der Startvorgang wird fortgesetzt. Keine Benachrichtigung erhält der Benutzer über den Fehler im Ereignisprotokoll aufgezeichnet.|
|binpath= \<BinaryPathName>|Gibt einen Pfad zur Binärdatei Diensts an.|
|group= \<LoadOrderGroup>|Gibt den Namen der Gruppe, der diesen Dienst Mitglied ist. Die Liste der Gruppen befindet sich in der Registrierung in der **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** Unterschlüssel. Der Standardwert ist null.|
|Tag = {Ja \| keine}|Gibt an, ob eine TagID aus dem CreateService-Aufruf abrufen. Tags werden nur für Bootstart- und Systemstart-Treiber verwendet.|
|depend= \<dependencies>|Gibt die Namen der Dienste oder Gruppen, die vor diesem Dienst starten zu müssen. Die Namen werden durch Schrägstriche (/) getrennt.|
|obj= {\<AccountName> \| \<ObjectName>}|Gibt einen Namen für ein Konto, in dem ein Dienst wird ausgeführt, oder gibt einen Namen für das Windows-Treiber-Objekt in dem der Treiber ausgeführt wird. Die Standardeinstellung ist **"LocalSystem"**.|
|displayname= \<DisplayName>|Gibt einen beschreibenden Namen für die Identifizierung des Diensts in Programmen für Benutzer-Schnittstelle an. Ist Sie beispielsweise den Namen des Unterschlüssels eines bestimmten Diensts **Wuauserv**, die über eine benutzerfreundlichere Anzeigenamen von Automatische Updates verfügt.|
|Kennwort = \<Kennwort >|Gibt ein Kennwort. Dies ist erforderlich, wenn ein anderes Konto als das Konto "LocalSystem" verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Für jede Befehlszeilenoption (Parameter) ist das Gleichheitszeichen Teil des Optionsnamens.
-   Ein Leerzeichen zwischen einer Option und den Wert erforderlich ist (z. B. **Typ = eigenen**. Wenn der Speicherplatz fehlt, schlägt der Vorgang fehl.

## <a name="BKMK_examples"></a>Beispiele für

Um eine binäre Pfad für den Dienst NEWSERVICE anzugeben, geben Sie Folgendes ein:
```
sc config NewService binpath= "ntsd -d c:\windows\system32\NewServ.exe"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)