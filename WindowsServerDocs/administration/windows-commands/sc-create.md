---
title: Sc.exe erstellen
description: Erfahren Sie, wie Sie mithilfe des Hilfsprogramms "sc.exe neue Dienste bei Windows Service Manager registrieren.
ms.topic: article
ms.assetid: 59416460-0661-4fef-85cc-73e9d8f4beb4
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: eba3939418a40d987ced4bcf3ed19f729409bf91
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87883281"
---
# <a name="scexe-create"></a>Sc.exe erstellen

Erstellt einen Unterschlüssel und Einträge für einen Dienst in der Registrierung und in der Dienststeuerungs-Manager-Datenbank.

## <a name="syntax"></a>Syntax

```
sc.exe [<ServerName>] create [<ServiceName>] [type= {own | share | kernel | filesys | rec | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto }] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<ServerName>|Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ \\ . MyServer) verwenden. Wenn Sie SC.exe lokal ausführen möchten, lassen Sie diesen Parameter Weg.|
|\<ServiceName>|Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird.|
|Type = {eigener \| Freigabe \| -Kernel \| filesys \| rec \| Interaktion Type = {eigener \| Freigabe}}|Gibt den Diensttyp an. Die Standardeinstellung ist **Type = own**.</br>**own** : gibt an, dass der Dienst in einem eigenen Prozess ausgeführt wird. Eine ausführbare Datei wird nicht mit anderen Diensten gemeinsam genutzt. Dies ist die Standardeinstellung.</br>**Freigabe** : gibt an, dass der Dienst als frei gegebener Prozess ausgeführt wird. Er gibt eine ausführbare Datei mit anderen Diensten frei.</br>**Kernel** : gibt einen Treiber an.</br>**filesys** : gibt einen Dateisystem Treiber an.</br>**rec** : gibt einen von einem Dateisystem erkannten Treiber an (identifiziert Dateisysteme, die auf dem Computer verwendet werden).</br>**Interact** : gibt an, dass der Dienst mit dem Desktop interagieren und Eingaben von Benutzern empfangen kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss in Verbindung mit **Type = own** oder **Type = Shared**verwendet werden. Durch die Verwendung von **Type = Interact** allein wird ein Fehler wegen eines ungültigen Parameters generiert.|
|Start = { \| automatische Start \| System \| Nachfrage \| deaktiviert \| -automatisch}|Gibt den Starttyp für den Dienst an. Die Standardeinstellung ist **Start = Demand**.</br>**Boot** : gibt einen Gerätetreiber an, der vom Start Lade Modul geladen wird.</br>**System** : gibt einen Gerätetreiber an, der während der Kernel Initialisierung gestartet wird.</br>gibt **automatisch einen** Dienst an, der automatisch gestartet wird, wenn der Computer neu gestartet wird. Beachten Sie, dass der Dienst auch dann ausgeführt wird, wenn sich niemand am Computer anmeldet.</br>**Demand** : gibt einen Dienst an, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **Start =** nicht angegeben ist.</br>**deaktiviert** : gibt einen Dienst an, der nicht gestartet werden kann. Ändern Sie den Starttyp in einen anderen Wert, um einen deaktivierten Dienst zu starten.</br>**verzögert:** gibt automatisch einen Dienst an, der nach dem Start anderer automatischer Dienste automatisch gestartet wird.|
|Fehler = {normaler \| schwerwiegender schwerwiegender Fehler \| \| }|Gibt den Schweregrad des Fehlers an, wenn der Dienst beim Starten des Computers fehlschlägt. Die Standardeinstellung ist **Error = normal**.</br>**Normal** : gibt an, dass der Fehler protokolliert wird. Ein Meldungs Feld wird angezeigt, das den Benutzer darüber informiert, dass ein Dienst nicht gestartet werden konnte. Der Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</br>**schwerwiegend** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Dies könnte dazu führen, dass der Computer neu gestartet werden kann, der Dienst jedoch möglicherweise trotzdem nicht ausgeführt werden kann.</br>**kritisch** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Wenn bei der letzten als funktionierend bekannten Konfiguration ein Fehler auftritt, schlägt der Startvorgang fehl, und der Startvorgang wird mit einem Fehler beendet.</br>**Ignore** : gibt an, dass der Fehler protokolliert und der Startvorgang fortgesetzt wird. Es wird keine Benachrichtigung an den Benutzer über die Aufzeichnung des Fehlers im Ereignisprotokoll ausgegeben.|
|BinPath =\<BinaryPathName>|Gibt einen Pfad zur Dienst Binärdatei an. Es gibt keinen Standardwert für " **BinPath =**", und diese Zeichenfolge muss angegeben werden.|
|Gruppe =\<LoadOrderGroup>|Gibt den Namen der Gruppe an, deren Mitglied dieser Dienst ist. Die Liste der Gruppen wird in der Registrierung im Unterschlüssel **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** gespeichert. Der Standardwert ist "null".|
|Tag = {Yes \| No}|Gibt an, ob eine TagID aus dem Befehl "{ateservice" abgerufen werden soll. Tags werden nur für Start-und Systemstart-Treiber verwendet.|
|abhängig =\<dependencies>|Gibt die Namen der Dienste oder Gruppen an, die vor dem Start dieses Diensts gestartet werden müssen. Die Namen werden durch Schrägstriche (/) getrennt.|
|obj = { \<AccountName> \| \<ObjectName> }|Gibt den Namen eines Kontos an, in dem ein Dienst ausgeführt wird, oder gibt einen Namen für das Windows-Treiber Objekt an, in dem der Treiber ausgeführt wird.|
|Display Name =\<DisplayName>|Gibt einen anzeigen Amen an, der von Benutzeroberflächen Programmen verwendet werden kann, um den Dienst zu identifizieren.|
|Kennwort =\<Password>|Gibt ein Kennwort an. Dies ist erforderlich, wenn ein anderes Konto als "LocalSystem" verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Bemerkungen

-   Für jede Befehlszeilenoption ist das Gleichheitszeichen Teil des Options namens.
-   Zwischen einer Option und ihrem Wert (z. b. **Type = own**) ist ein Leerzeichen erforderlich. Wenn der Speicherplatz weggelassen wird, schlägt der Vorgang fehl.

## <a name="examples"></a>Beispiele

In den folgenden Beispielen wird gezeigt, wie Sie den Befehl **sc.exe Create** verwenden können:
```
sc.exe \\myserver create NewService binpath= c:\windows\system32\NewServ.exe
sc.exe create NewService binpath= c:\windows\system32\NewServ.exe type= share start= auto depend= +TDI NetBIOS
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
