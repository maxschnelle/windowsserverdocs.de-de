---
title: Sc.exe config
description: Erfahren Sie, wie Sie Dienst Konfigurationen mithilfe des sc.exe Hilfsprogramms ändern.
ms.topic: reference
ms.assetid: ad4d68a6-efe5-452b-8501-7f1f1c552a4a
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 06/05/2018
ms.openlocfilehash: 55432910455896434a1857d17016519bedb51caf
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89637136"
---
# <a name="scexe-config"></a>Sc.exe config

Ändert den Wert der Einträge eines dienstantrags in der Registrierung und in der Dienststeuerungs-Manager-Datenbank.

## <a name="syntax"></a>Syntax

```
sc.exe [<ServerName>] config [<ServiceName>] [type= {own | share | kernel | filesys | rec | adapt | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

### <a name="parameters"></a>Parameter

|Parameter|BESCHREIBUNG|
|---------|-----------|
|\<ServerName>|Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention (UNC)-Format (z. b \\ \\ . MyServer) verwenden. Wenn Sie SC.exe lokal ausführen möchten, lassen Sie diesen Parameter Weg.|
|\<ServiceName>|Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird.|
|Type = {eigener \| Freigabe \| Kernel \| filesys \| rec \| Anpassung \| Interaktion Typ = {eigene \| Freigabe}} | Gibt den Diensttyp an.</br>**own** : gibt einen Dienst an, der in einem eigenen Prozess ausgeführt wird. Eine ausführbare Datei wird nicht mit anderen Diensten gemeinsam genutzt. Dies ist der Standardwert.</br>**Freigabe** : gibt einen Dienst an, der als frei gegebener Prozess ausgeführt wird. Er gibt eine ausführbare Datei mit anderen Diensten frei.</br>**Kernel** : gibt einen Treiber an.</br>**filesys** : gibt einen Dateisystem Treiber an.</br>**rec** : Hiermit wird ein vom Dateisystem erkannter Treiber angegeben, mit dem die auf dem Computer verwendeten Dateisysteme identifiziert werden.</br>**Anpassen** : gibt einen Adapter Treiber an, mit dem Hardware Geräte wie Tastaturen, Mäuse und Laufwerke identifiziert werden.</br>**Interaktion** : gibt einen Dienst an, der mit dem Desktop interagieren und Eingaben von Benutzern empfangen kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss in Verbindung mit **Type = own** oder **Type = Shared** verwendet werden (z. b. **Type = Interact** **Type = own**). Durch die Verwendung von **Type = Interact** allein wird ein Fehler generiert.|
|Start = { \| automatische Start \| System \| Nachfrage \| deaktiviert \| -automatisch}|Gibt den Starttyp für den Dienst an.</br>**Boot** : gibt einen Gerätetreiber an, der vom Start Lade Modul geladen wird.</br>**System** : gibt einen Gerätetreiber an, der während der Kernel Initialisierung gestartet wird.</br>gibt **automatisch einen** Dienst an, der automatisch gestartet wird, sobald der Computer neu gestartet wird. er wird auch dann ausgeführt, wenn sich niemand am Computer anmeldet.</br>**Demand** : gibt einen Dienst an, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **Start =** nicht angegeben ist.</br>**deaktiviert** : gibt einen Dienst an, der nicht gestartet werden kann. Ändern Sie den Starttyp in einen anderen Wert, um einen deaktivierten Dienst zu starten.</br>**verzögert:** gibt automatisch einen Dienst an, der nach dem Start anderer automatischer Dienste automatisch gestartet wird.|
|Fehler = {normaler \| schwerwiegender schwerwiegender Fehler \| \| }|Gibt den Schweregrad des Fehlers an, wenn der Dienst beim Starten nicht gestartet werden kann.</br>**Normal** : gibt an, dass der Fehler protokolliert und ein Meldungs Feld angezeigt wird, um den Benutzer darüber zu informieren, dass ein Dienst nicht gestartet werden konnte. Der Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</br>**schwerwiegend** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Dies könnte dazu führen, dass der Computer neu gestartet werden kann, der Dienst jedoch möglicherweise trotzdem nicht ausgeführt werden kann.</br>**kritisch** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Wenn bei der letzten als funktionierend bekannten Konfiguration ein Fehler auftritt, schlägt der Startvorgang fehl, und der Startvorgang wird mit einem Fehler beendet.</br>**Ignore** : gibt an, dass der Fehler protokolliert und der Startvorgang fortgesetzt wird. Es wird keine Benachrichtigung an den Benutzer über die Aufzeichnung des Fehlers im Ereignisprotokoll ausgegeben.|
|BinPath = \<BinaryPathName>|Gibt einen Pfad zur Dienst Binärdatei an.|
|Gruppe = \<LoadOrderGroup>|Gibt den Namen der Gruppe an, deren Mitglied dieser Dienst ist. Die Liste der Gruppen wird in der Registrierung im Unterschlüssel **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** gespeichert. Der Standardwert ist "null".|
|Tag = {Yes \| No}|Gibt an, ob eine TagID aus dem Befehl "| ateservice" abgerufen werden soll. Tags werden nur für Start-und Systemstart-Treiber verwendet.|
|abhängig = \<dependencies>|Gibt die Namen der Dienste oder Gruppen an, die vor diesem Dienst gestartet werden müssen. Die Namen werden durch Schrägstriche (/) getrennt.|
|obj = { \<AccountName> \| \<ObjectName> }|Gibt den Namen eines Kontos an, in dem ein Dienst ausgeführt wird, oder gibt einen Namen für das Windows-Treiber Objekt an, in dem der Treiber ausgeführt wird. Die Standardeinstellung ist " **LocalSystem**".|
|Display Name = \<DisplayName>|Gibt einen beschreibenden Namen für die Identifizierung des Dienstanbieter in Benutzeroberflächen Programmen an. Beispielsweise ist der Unterschlüssel Name eines bestimmten **dienstaners wuauserv**, der einen freundlicheren anzeigen Amen automatische Updates hat.|
|Kennwort = \<Password>|Gibt ein Kennwort an. Dies ist erforderlich, wenn ein anderes Konto als das Konto "LocalSystem" verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Für jede Befehlszeilenoption (Parameter) ist das Gleichheitszeichen Teil des Options namens.
-   Zwischen einer Option und ihrem Wert (z. b. **Type = own**) ist ein Leerzeichen erforderlich. Wenn der Leerraum weggelassen wird, schlägt der Vorgang fehl.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um einen binären Pfad für den newservice-Dienst anzugeben:
```
sc.exe config NewService binpath= ntsd -d c:\windows\system32\NewServ.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
