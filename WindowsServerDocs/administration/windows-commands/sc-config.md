---
title: SC-Konfiguration
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ad4d68a6-efe5-452b-8501-7f1f1c552a4a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 06/05/2018
ms.openlocfilehash: fc864afe98823fa609cbe82398a486bf6e29defd
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80835313"
---
# <a name="sc-config"></a>SC-Konfiguration



Ändert den Wert der Einträge eines dienstantrags in der Registrierung und in der Dienststeuerungs-Manager-Datenbank.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] config [<ServiceName>] [type= {own | share | kernel | filesys | rec | adapt | interact type= {own | share}}] [start= {boot | system | auto | demand | disabled | delayed-auto}] [error= {normal | severe | critical | ignore}] [binpath= <BinaryPathName>] [group= <LoadOrderGroup>] [tag= {yes | no}] [depend= <dependencies>] [obj= {<AccountName> | <ObjectName>}] [displayname= <DisplayName>] [password= <Password>]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<Servername >|Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention Format (UNC) verwenden (z. b. \\\\MyServer). Wenn Sie "SC. exe" lokal ausführen möchten, lassen Sie diesen Parameter Weg.|
|\<ServiceName >|Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird.|
|Type = {own\| Share \| Kernel \| filesys \| REC \| anpassen \| Interact Type = {own \| Share}} | Gibt den Diensttyp an.</br>**own** : gibt einen Dienst an, der in einem eigenen Prozess ausgeführt wird. Eine ausführbare Datei wird nicht mit anderen Diensten gemeinsam genutzt. Dies ist der Standardwert.</br>**Freigabe** : gibt einen Dienst an, der als frei gegebener Prozess ausgeführt wird. Er gibt eine ausführbare Datei mit anderen Diensten frei.</br>**Kernel** : gibt einen Treiber an.</br>**filesys** : gibt einen Dateisystem Treiber an.</br>**rec** : Hiermit wird ein vom Dateisystem erkannter Treiber angegeben, mit dem die auf dem Computer verwendeten Dateisysteme identifiziert werden.</br>**Anpassen** : gibt einen Adapter Treiber an, mit dem Hardware Geräte wie Tastaturen, Mäuse und Laufwerke identifiziert werden.</br>**Interaktion** : gibt einen Dienst an, der mit dem Desktop interagieren und Eingaben von Benutzern empfangen kann. Interaktive Dienste müssen unter dem Konto "LocalSystem" ausgeführt werden. Dieser Typ muss in Verbindung mit **Type = own** oder **Type = Shared** verwendet werden (z. b. **Type = Interact** **Type = own**). Durch die Verwendung von **Type = Interact** allein wird ein Fehler generiert.|
|Start = {Boot \| System \| automatische \| Nachfrage \| deaktiviert \| verzögert-automatisch}|Gibt den Starttyp für den Dienst an.</br>**Boot** : gibt einen Gerätetreiber an, der vom Start Lade Modul geladen wird.</br>**System** : gibt einen Gerätetreiber an, der während der Kernel Initialisierung gestartet wird.</br>gibt **automatisch einen** Dienst an, der automatisch gestartet wird, sobald der Computer neu gestartet wird. er wird auch dann ausgeführt, wenn sich niemand am Computer anmeldet.</br>**Demand** : gibt einen Dienst an, der manuell gestartet werden muss. Dies ist der Standardwert, wenn **Start =** nicht angegeben ist.</br>**deaktiviert** : gibt einen Dienst an, der nicht gestartet werden kann. Ändern Sie den Starttyp in einen anderen Wert, um einen deaktivierten Dienst zu starten.</br>**verzögert:** gibt automatisch einen Dienst an, der nach dem Start anderer automatischer Dienste automatisch gestartet wird.|
|Fehler = {normal \| schwerer \| kritisch \| ignorieren}|Gibt den Schweregrad des Fehlers an, wenn der Dienst beim Starten nicht gestartet werden kann.</br>**Normal** : gibt an, dass der Fehler protokolliert und ein Meldungs Feld angezeigt wird, um den Benutzer darüber zu informieren, dass ein Dienst nicht gestartet werden konnte. Der Startvorgang wird fortgesetzt. Dies ist die Standardeinstellung.</br>**schwerwiegend** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Dies könnte dazu führen, dass der Computer neu gestartet werden kann, der Dienst jedoch möglicherweise trotzdem nicht ausgeführt werden kann.</br>**kritisch** : gibt an, dass der Fehler protokolliert wird (sofern möglich). Der Computer versucht, mit der letzten als funktionierend bekannten Konfiguration neu zu starten. Wenn bei der letzten als funktionierend bekannten Konfiguration ein Fehler auftritt, schlägt der Startvorgang fehl, und der Startvorgang wird mit einem Fehler beendet.</br>**Ignore** : gibt an, dass der Fehler protokolliert und der Startvorgang fortgesetzt wird. Es wird keine Benachrichtigung an den Benutzer über die Aufzeichnung des Fehlers im Ereignisprotokoll ausgegeben.|
|BinPath = \<binarypathname >|Gibt einen Pfad zur Dienst Binärdatei an.|
|Group = \<LoadOrderGroup >|Gibt den Namen der Gruppe an, deren Mitglied dieser Dienst ist. Die Liste der Gruppen wird in der Registrierung im Unterschlüssel **HKLM\System\CurrentControlSet\Control\ServiceGroupOrder** gespeichert. Der Standardwert ist NULL.|
|Tag = {Yes \| No}|Gibt an, ob eine TagID aus dem Befehl ateservice" abgerufen werden soll. Tags werden nur für Start-und Systemstart-Treiber verwendet.|
|abhängig = \<Abhängigkeiten >|Gibt die Namen der Dienste oder Gruppen an, die vor diesem Dienst gestartet werden müssen. Die Namen werden durch Schrägstriche (/) getrennt.|
|obj = {\<Accountname > \| \<ObjectName >}|Gibt den Namen eines Kontos an, in dem ein Dienst ausgeführt wird, oder gibt einen Namen für das Windows-Treiber Objekt an, in dem der Treiber ausgeführt wird. Die Standardeinstellung ist " **LocalSystem**".|
|Display Name = \<Display Name >|Gibt einen beschreibenden Namen für die Identifizierung des Dienstanbieter in Benutzeroberflächen Programmen an. Beispielsweise ist der Unterschlüssel Name eines bestimmten **dienstaners wuauserv**, der einen freundlicheren anzeigen Amen automatische Updates hat.|
|Password = \<Kennwort >|Gibt ein Kennwort an. Dies ist erforderlich, wenn ein anderes Konto als das Konto "LocalSystem" verwendet wird.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Für jede Befehlszeilenoption (Parameter) ist das Gleichheitszeichen Teil des Options namens.
-   Zwischen einer Option und ihrem Wert (z. b. **Type = own**) ist ein Leerzeichen erforderlich. Wenn der Leerraum weggelassen wird, schlägt der Vorgang fehl.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um einen binären Pfad für den newservice-Dienst anzugeben:
```
sc config NewService binpath= ntsd -d c:\windows\system32\NewServ.exe
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)