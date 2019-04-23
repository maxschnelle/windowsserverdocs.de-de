---
title: SC erstellen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 59416460-0661-4fef-85cc-73e9d8f4beb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7931ddc91b91d5fce01335f4b090d0305790f65c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826501"
---
# <a name="sc-create"></a>SC erstellen



In der Registrierung und in der Dienststeuerungs-Manager-Datenbank einen Unterschlüssel und Einträge für einen Dienst erstellt werden soll.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] create [<ServiceName>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<ServerName>|Gibt den Namen des Remoteservers auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format verwenden (z. B. \\ \\"myserver"). Um SC.exe lokal ausführen zu können, müssen lassen Sie diesen Parameter Weg.|
|\<ServiceName>|Gibt den Dienstnamen, die zurückgegeben werden, indem die **Getkeyname** Vorgang.|
|Typ = {eigenen \| freigeben \| Kernel \| Filesys \| Rec \| interagieren, Typ = {eigenen \| freigeben}}|Gibt den Diensttyp an. Die Standardeinstellung ist **Typ = eigenen**.</br>**eigene** – gibt an, dass der Dienst in einem eigenen Prozess ausgeführt wird. Es gibt eine ausführbare Datei nicht mit anderen Diensten frei. Dies ist die Standardeinstellung.</br>**Freigeben von** – gibt an, dass der Dienst einen gemeinsam genutzten Prozess ausgeführt wird. Es gibt eine ausführbare Datei für andere Dienste frei.</br>**Kernel** – gibt an, einen Treiber.</br>**Filesys** – gibt an, einem Dateisystemtreiber.</br>**REC** -gibt ein erkannt Dateisystemtreiber (identifiziert Dateisysteme, die auf dem Computer verwendet).</br>**Interaktion** – gibt an, dass der Dienst mit dem Desktop empfängt Eingaben von Benutzern interagieren kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss verwendet werden, zusammen mit **Typ = eigenen** oder **Typ = freigegebene**. Mithilfe von **Typ = interagieren** , wird einen Fehler "Ungültiger Parameter" generiert.|
|Start = {Boot \| System \| automatisch \| Bedarf \| deaktiviert}|Gibt den Starttyp für den Dienst an. Die Standardeinstellung ist **start = Demand**.</br>**Start** – gibt an, einen Gerätetreiber, die durch Bootloader geladen wird.</br>**System** – gibt an, einen Gerätetreiber, die während der Kernelinitialisierung gestartet wird.</br>**automatische** -gibt einen Dienst, der automatisch jedes Mal startet der Computer neu gestartet wird. Beachten Sie, dass der Dienst ausgeführt wird, auch wenn niemand am Computer anmeldet.</br>**bei Bedarf** – gibt an, ein Dienst, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **starten =** nicht angegeben ist.</br>**deaktiviert** – gibt an, ein Dienst, der nicht gestartet werden kann. Um eines deaktivierten Dienstes zu starten, ändern Sie den Starttyp auf einen anderen Wert ein.|
|Fehler = {normal \| schwerwiegende \| kritische \| ignorieren}|Gibt den Schweregrad des Fehlers an, wenn der Dienst nicht, wenn der Computer gestartet wird. Die Standardeinstellung ist **Fehler = normal**.</br>**normale** – gibt an, dass der Fehler protokolliert wird. Ein Meldungsfeld wird angezeigt, informiert den Benutzer, den ein Dienst nicht gestartet werden konnte. Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</br>**schwerwiegende** – gibt an, dass der Fehler (sofern möglich) protokolliert wird. Der Computer versucht, mit der letzten bekannten guten Konfiguration neu zu starten. Könnte dies auf dem Computer gestartet werden kann, aber der Dienst ist möglicherweise immer noch in der kann nicht ausgeführt werden.</br>**kritische** – gibt an, dass der Fehler (sofern möglich) protokolliert wird. Der Computer versucht, mit der letzten bekannten guten Konfiguration neu zu starten. Wenn die letzten bekannten gute Konfiguration ein Fehler auftritt, starten auch ein Fehler auftritt und des Startvorgangs wird mit einem Abbruchfehler angehalten.</br>**ignorieren Sie** – gibt an, dass der Fehler protokolliert wird und der Startvorgang wird fortgesetzt. Keine Benachrichtigung erhält der Benutzer über den Fehler im Ereignisprotokoll aufgezeichnet.|
|binpath= \<BinaryPathName>|Gibt einen Pfad zur Binärdatei Diensts an. Es gibt keinen Standardwert für **Anwendungsbasis =**, und diese Zeichenfolge muss angegeben werden.|
|group= \<LoadOrderGroup>|Gibt den Namen der Gruppe, der diesen Dienst Mitglied ist. Die Liste der Gruppen befindet sich in der Registrierung in der **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** Unterschlüssel. Der Standardwert ist null.|
|Tag = {Ja \| keine}|Gibt an, ob eine TagID wird von der CreateService-Aufruf abgerufen. Tags werden nur für Bootstart- und Systemstart-Treiber verwendet.|
|depend= \<dependencies>|Gibt die Namen der Dienste oder Gruppen, die vor dem Start dieses Diensts beginnen müssen. Die Namen werden durch Schrägstriche (/) getrennt.|
|obj= {\<AccountName> \| \<ObjectName>}|Gibt den Namen eines Kontos, in dem ein Dienst wird ausgeführt, oder gibt einen Namen für das Windows-Treiber-Objekt in dem der Treiber ausgeführt wird.|
|displayname= \<DisplayName>|Gibt einen Anzeigenamen ein, der von Programmen für Benutzer-Schnittstelle zum Identifizieren des Diensts verwendet werden kann.|
|Kennwort = \<Kennwort >|Gibt ein Kennwort. Dies ist erforderlich, wenn ein anderes Konto als "LocalSystem" verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Für jede Befehlszeilenoption ist das Gleichheitszeichen Teil des Optionsnamens.
-   Ein Leerzeichen zwischen einer Option und den Wert erforderlich ist (z. B. **Typ = eigenen**. Wenn der Speicherplatz nicht angegeben, wird der Vorgang schlägt fehl.

## <a name="BKMK_examples"></a>Beispiele für

Die folgenden Beispiele zeigen Informationen zur Verwendung der **sc erstellen** Befehl:
```
sc \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
sc create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= "+TDI NetBIOS"
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)
