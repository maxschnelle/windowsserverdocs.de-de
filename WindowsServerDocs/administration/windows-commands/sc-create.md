---
title: SC erstellen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 8ea8f1c33472b7ac95ec0282a50d902a9d7cf84d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384374"
---
# <a name="sc-create"></a>SC erstellen



Erstellt einen Unterschlüssel und Einträge für einen Dienst in der Registrierung und in der Dienststeuerungs-Manager-Datenbank.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] create [<ServiceName>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Servername >|Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention Format (UNC) verwenden (z. b. \\\\MyServer). Wenn Sie "SC. exe" lokal ausführen möchten, lassen Sie diesen Parameter Weg.|
|\<ServiceName >|Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird.|
|Type = {own \| Share \| Kernel \| filesys \| REC \| Interact Type = {own \| Share}}|Gibt den Diensttyp an. Die Standardeinstellung ist **Type = own**.</br>**own** : gibt an, dass der Dienst in einem eigenen Prozess ausgeführt wird. Eine ausführbare Datei wird nicht mit anderen Diensten gemeinsam genutzt. Dies ist die Standardeinstellung.</br>**Freigabe** : gibt an, dass der Dienst als frei gegebener Prozess ausgeführt wird. Er gibt eine ausführbare Datei mit anderen Diensten frei.</br>**Kernel** : gibt einen Treiber an.</br>**filesys** : gibt einen Dateisystem Treiber an.</br>**rec** : gibt einen von einem Dateisystem erkannten Treiber an (identifiziert Dateisysteme, die auf dem Computer verwendet werden).</br>**Interact** : gibt an, dass der Dienst mit dem Desktop interagieren und Eingaben von Benutzern empfangen kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss in Verbindung mit **Type = own** oder **Type = Shared**verwendet werden. Durch die Verwendung von **Type = Interact** allein wird der Fehler "Ungültiger Parameter" generiert.|
|Start = {Boot \| System \| Auto \| Demand \| deaktiviert}|Gibt den Starttyp für den Dienst an. Die Standardeinstellung ist **Start = Demand**.</br>**Boot** : gibt einen Gerätetreiber an, der vom Start Lade Modul geladen wird.</br>**System** : gibt einen Gerätetreiber an, der während der Kernel Initialisierung gestartet wird.</br>gibt **automatisch einen** Dienst an, der automatisch gestartet wird, wenn der Computer neu gestartet wird. Beachten Sie, dass der Dienst auch dann ausgeführt wird, wenn sich niemand am Computer anmeldet.</br>**Demand** : gibt einen Dienst an, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **Start =** nicht angegeben ist.</br>**deaktiviert** : gibt einen Dienst an, der nicht gestartet werden kann. Ändern Sie den Starttyp in einen anderen Wert, um einen deaktivierten Dienst zu starten.|
|Fehler = {normal \| schwerer \| kritisch \| ignorieren}|Gibt den Schweregrad des Fehlers an, wenn der Dienst beim Starten des Computers fehlschlägt. Die Standardeinstellung ist **Error = normal**.</br>**Normal** : gibt an, dass der Fehler protokolliert wird. Ein Meldungs Feld wird angezeigt, das den Benutzer darüber informiert, dass ein Dienst nicht gestartet werden konnte. Der Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</br>**schwerwiegend** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Dies könnte dazu führen, dass der Computer neu gestartet werden kann, der Dienst jedoch möglicherweise trotzdem nicht ausgeführt werden kann.</br>**kritisch** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Wenn bei der letzten als funktionierend bekannten Konfiguration ein Fehler auftritt, schlägt der Startvorgang fehl, und der Startvorgang wird mit einem Fehler beendet.</br>**Ignore** : gibt an, dass der Fehler protokolliert und der Startvorgang fortgesetzt wird. Es wird keine Benachrichtigung an den Benutzer über die Aufzeichnung des Fehlers im Ereignisprotokoll ausgegeben.|
|BinPath = \<binarypathname >|Gibt einen Pfad zur Dienst Binärdatei an. Es gibt keinen Standardwert für " **BinPath =** ", und diese Zeichenfolge muss angegeben werden.|
|Group = \<LoadOrderGroup >|Gibt den Namen der Gruppe an, deren Mitglied dieser Dienst ist. Die Liste der Gruppen wird in der Registrierung im Unterschlüssel **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** gespeichert. Der Standardwert ist NULL.|
|Tag = {Yes \| No}|Gibt an, ob eine TagID aus dem Befehl "{ateservice" abgerufen werden soll. Tags werden nur für Start-und Systemstart-Treiber verwendet.|
|abhängig = \<Abhängigkeiten >|Gibt die Namen der Dienste oder Gruppen an, die vor dem Start dieses Diensts gestartet werden müssen. Die Namen werden durch Schrägstriche (/) getrennt.|
|obj = {\<Accountname > \| \<ObjectName >}|Gibt den Namen eines Kontos an, in dem ein Dienst ausgeführt wird, oder gibt einen Namen für das Windows-Treiber Objekt an, in dem der Treiber ausgeführt wird.|
|Display Name = \<Display Name >|Gibt einen anzeigen Amen an, der von Benutzeroberflächen Programmen verwendet werden kann, um den Dienst zu identifizieren.|
|Password = \<Kennwort >|Gibt ein Kennwort an. Dies ist erforderlich, wenn ein anderes Konto als "LocalSystem" verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Für jede Befehlszeilenoption ist das Gleichheitszeichen Teil des Options namens.
-   Zwischen einer Option und ihrem Wert (z. b. **Type = own**) ist ein Leerzeichen erforderlich. Wenn der Speicherplatz weggelassen wird, schlägt der Vorgang fehl.

## <a name="BKMK_examples"></a>Beispiele

In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **SC Create** verwenden können:
```
sc \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
sc create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= "+TDI NetBIOS"
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
