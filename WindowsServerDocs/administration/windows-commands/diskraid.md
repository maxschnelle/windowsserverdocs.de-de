---
title: diskraid
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 20aef1e5-7641-47cf-b4eb-cda117f65b6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: a565a1d5fa1bc3ff57d1578fb54cfa4553e3bb26
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818871"
---
# <a name="diskraid"></a>diskraid



DiskRAID ist ein Befehlszeilentool, mit der Sie zum Konfigurieren und verwalten redundante Array von Speichersubsystemen unabhängigen (bzw. kostengünstige) Datenträger (RAID).

RAID ist eine Methode, die zum standardisieren und fehlertolerante Datenträgersysteme kategorisieren. RAID-Stufen bieten verschiedene Kombinationen von Kosten, Zuverlässigkeit und Leistung. RAID wird normalerweise auf Servern verwendet. Einige Server stellen die drei von der RAID-Stufen zur Verfügung: Ebene 0 (Stripeset), 1 (Spiegelung) und der Ebene 5 (Striping mit Parität).

Eine Hardware-RAID-Subsystem unterscheidet physisch adressierbaren Speichereinheiten von den anderen, mit der Nummer einer logischen Einheit (LUN). Ein LUN-Objekt muss mindestens ein plexer verfügen, und kann eine beliebige Anzahl von zusätzlichen zu haben. Jede plexer enthält eine Kopie der Daten auf das LUN-Objekt. Zu können hinzugefügt und entfernt aus einem LUN-Objekt werden.

Die meisten DiskRAID-Befehle werden für einen bestimmten Host Bus Hostbusadapter (HBA)-Port, Initiatoradapter, Initiatorportal, Anbieter, Subsystem, Controller, Port, Laufwerk, LUN, Zielportal, Ziel oder Zielgruppe für Portals. Sie verwenden den SELECT-Befehl, um ein Objekt auszuwählen. Das ausgewählte Objekt wird als den Fokus besitzen. Fokus vereinfacht die häufigsten Konfigurationsaufgaben wie das Erstellen von mehreren LUNs innerhalb des gleichen Subsystems.

> [!NOTE]
> Das Befehlszeilentool DiskRAID funktioniert nur mit Speichersubsystemen, die Verwaltung digitaler Rechte (Virtual Disk Service, VDS) zu unterstützen.

## <a name="diskraid-commands"></a>DiskRAID-Befehle

Klicken Sie auf einen Befehl, um die Befehlssyntax anzuzeigen:
-   [add](#BKMK_1)
-   [associate](#BKMK_2)
-   [automagic](#BKMK_3)
-   [break](#BKMK_4)
-   [chap](#BKMK_5)
-   [create](#BKMK_6)
-   [delete](#BKMK_7)
-   [detail](#BKMK_8)
-   [dissociate](#BKMK_9)
-   [exit](#BKMK_10)
-   [extend](#BKMK_11)
-   [flushcache](#BKMK_12)
-   [help](#BKMK_13)
-   [importtarget](#BKMK_14)
-   [initiator](#BKMK_15)
-   [invalidatecache](#BKMK_16)
-   [lbpolicy](#BKMK_18)
-   [list](#BKMK_19)
-   [login](#BKMK_20)
-   [logout](#BKMK_21)
-   [maintenance](#BKMK_22)
-   [name](#BKMK_23)
-   [offline](#BKMK_24)
-   [online](#BKMK_25)
-   [recover](#BKMK_26)
-   [reenumerate](#BKMK_27)
-   [refresh](#BKMK_28)
-   [rem](#BKMK_29)
-   [remove](#BKMK_30)
-   [replace](#BKMK_31)
-   [reset](#BKMK_32)
-   [select](#BKMK_33)
-   [setflag](#BKMK_34)
-   [shrink](#BKMK_shrink)
-   [standby](#BKMK_35)
-   [unmask](#BKMK_36)

### <a name="BKMK_1"></a>add

Fügt eine vorhandene LUN, die derzeit ausgewählte LUN oder die Zielgruppe für ausgewählte iSCSI-Portal ein iSCSI-Zielportals hinzugefügt.

#### <a name="syntax"></a>Syntax

```
add plex lun=n [noerr]
add tpgroup tportal=n [noerr]
```

#### <a name="parameters"></a>Parameter

**plexer Lun**=*n*

Gibt an, die LUN-Nummer, der derzeit ausgewählten LUN als eine plexer hinzufügen.

> [!CAUTION]
> Alle Daten auf die LUN, die als eine plexer hinzugefügt wird, werden gelöscht werden.

**TPGROUP Tportal = *** n*

Gibt die iSCSI-Ziel Portal an, der aktuell ausgewählten iSCSI-Ziel-Portal-Gruppe hinzufügen.

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs werden ignoriert. Dies ist hilfreich, im Skriptmodus.

### <a name="BKMK_2"></a>Zuordnen

Legt die angegebene Liste der Controller Ports als aktiv für die aktuell ausgewählten LUN (andere Controller Ports werden inaktive vorgenommen), fügt die angegebenen Controller-Ports zur Liste der vorhandenen aktiven Controller-Ports für die aktuell ausgewählten LUN oder ordnet die angegebene iSCSI-Ziel für die aktuell ausgewählten LUN.

#### <a name="syntax"></a>Syntax

```
associate controllers [add] <n>[,<n> [,…]]
associate ports [add] <n-m>[,<n-m>[,…]]
associate targets [add] <n>[,<n> [,…]]
```

#### <a name="parameters"></a>Parameter

**Controller**

Für die Verwendung mit nur Hardwareanbieter für VDS 1.0-Anbieter. Fügt hinzu oder ersetzt die Liste der Domänencontroller, auf denen der derzeit ausgewählten LUN zugeordnet sind.

**ports**

Für die Verwendung mit nur VDS 1.1-Anbieter. Fügt hinzu oder ersetzt die Liste der Controllerports, die derzeit ausgewählten LUN zugeordnet sind.

**targets**

Für die Verwendung mit nur VDS 1.1-Anbieter. Fügt hinzu oder ersetzt die Liste der iSCSI-Ziele, die derzeit ausgewählten LUN zugeordnet sind.

**add**

Die angegebenen Controller hinzugefügt für VDS 1.0-Anbieter aus der vorhandenen Liste der Controller die LUN zugeordnet. Wenn dieser Parameter nicht angegeben ist, ersetzt die Liste der Controller die vorhandene Liste der Controller, die dieser LUN zugeordnet.

Die angegebenen Controller-Ports hinzugefügt für VDS 1.1-Anbieter aus der vorhandenen Liste der Controllerports, die die LUN zugeordnet. Wenn dieser Parameter nicht angegeben ist, ersetzt die Liste der Controllerports die vorhandene Liste der Controllerports, die dieser LUN zugeordnet.
```
<n>[,<n> [, ...]]
```
Für die Verwendung mit der **Controller** oder **Ziele** Parameter. Gibt die Anzahl von Controllern oder iSCSI-Ziele, die auf active oder zuordnen festgelegt.
```
<n-m>[,<n-m>[,…]]
```
Für die Verwendung mit der **Ports** Parameter. Gibt an, die Controllerports mit einer Reihe Controller aktiv festgelegt (*n*) und Port-Nummer (*m*) Paar.

#### <a name="example"></a>Beispiel

Das folgende Beispiel zeigt, wie Sie zuweisen und Hinzufügen von Ports zur eine LUN, die einen VDS 1.1-Anbieter verwendet wird:
```
DISKRAID> SEL LUN 5
LUN 5 is now the selected LUN.

DISKRAID> ASSOCIATE PORTS 0-0,0-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1)

DISKRAID> ASSOCIATE PORTS ADD 1-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1, Ctlr 1 Port 1)
```

### <a name="BKMK_3"></a>automagic

Legt fest oder löscht Flags, die Hinweise auf Anbietern, die zum Konfigurieren einer LUNs zu gewähren. Ohne Parameter verwendet den **Automagic** Prozess zeigt eine Liste von Flags.

#### <a name="syntax"></a>Syntax

```
automagic {set | clear | apply} all <flag=value> [<flag=value> [...]]
```

#### <a name="parameters"></a>Parameter

**set**

Legt die angegebenen Flags auf die angegebenen Werte fest.

**clear**

Löscht die angegebenen Flags. Die **alle** Schlüsselwort löscht alle automagischen Flags.

**apply**

Wendet die aktuellen Optionen zur ausgewählten LUN.

\<flag>

Flags werden mit drei Buchstaben bestehenden Akronyme identifiziert.

|Flag|Beschreibung|
|----|-----------|
|FCR|Schnelle Systemabsturz erforderlich|
|FTL|Fehlertoleranz|
|MSR|Überwiegend Lesevorgänge|
|MXD|Maximale Laufwerke|
|MXS|Maximale Größe, die erwartet|
|ORA|Ausrichtung für eine optimale lesen|
|OR|Optimale Lesecaches|
|OSR|Für sequenzielle Lesevorgänge zu optimieren|
|OSW|Bei sequenziellen Schreibvorgängen optimieren|
|OWA|Optimale Write-Ausrichtung|
|OWS|Optimale Schreibgröße|
|RBP|Erstellen Sie Priorität neu.|
|RBV|Lesen wieder überprüfen aktiviert|
|RMP|Neuzuordnung aktiviert|
|STS|Stripegröße|
|WTC|Write-Through-Caching aktiviert|
|YNK|Wechseldatenträger|

### <a name="BKMK_4"></a>break

Entfernt die plexer aus den derzeit ausgewählten LUN. Die plexer und die enthaltenen Daten werden nicht beibehalten, und die Laufwerk-Blöcke können freigegeben werden.

#### <a name="syntax"></a>Syntax

```
break plex=<plex_number> [noerr]
```

#### <a name="parameters"></a>Parameter

**plex**

Gibt die Anzahl von der plexer entfernen. Die plexer und die enthaltenen Daten nicht beibehalten, und die von diesem plexer verwendeten Ressourcen freigegeben. Die Daten in die LUN ist nicht garantiert konsistent. Wenn Sie diese plexer beibehalten möchten, verwenden Sie den Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS).

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs werden ignoriert. Dies ist hilfreich, im Skriptmodus.

#### <a name="remarks"></a>Hinweise

> [!NOTE]
> Sie müssen zuerst eine gespiegelte LUN auswählen, vor der Verwendung der **Break** Befehl.

> [!CAUTION]
> Alle Daten auf den plexer gelöscht werden.

> [!CAUTION]
> Alle Daten auf die ursprüngliche LUN ist nicht garantiert konsistent.

### <a name="BKMK_5"></a>chap

Der freigegebene Challenge Handshake Authentication Protocol (CHAP) festgelegt geheimen so, dass iSCSI-Initiatoren und iSCSI-Ziele miteinander kommunizieren können.

#### <a name="syntax"></a>Syntax

```
chap initiator set secret=[<secret>] [target=<target>]
chap initiator remember secret=[<secret>] target=<target>
chap target set secret=[<secret>] [initiator=<initiatorname>]
chap target remember secret=[<secret>] initiator=<initiatorname>
```

#### <a name="parameters"></a>Parameter

**Initiator-Satz**

Legt den gemeinsamen geheimen Schlüssel in der lokalen iSCSI-Initiator-Dienst für die wechselseitige CHAP-Authentifizierung verwendet wird, wenn der Initiator das Ziel authentifiziert fest.

**Initiator speichern**

Den CHAP-Schlüssel von einem iSCSI-Ziel auf dem lokalen iSCSI-Initiator-Dienst kommuniziert, so, dass der Initiator-Dienst den geheimen Schlüssel verwenden kann, um sich an das Ziel während der CHAP-Authentifizierung zu authentifizieren.

**Zielsatz**

Legt den gemeinsamen geheimen Schlüssel in der aktuell ausgewählten iSCSI-Ziel für die CHAP-Authentifizierung verwendet wird, wenn das Ziel den Initiator authentifiziert.

**Ziel speichern**

Den CHAP-Schlüssel, der einen iSCSI-Initiator auf das aktuelle Fokus des iSCSI-Ziel kommuniziert, damit das Ziel den geheime Schlüssel verwenden kann, um sich an den Initiator während der wechselseitige CHAP-Authentifizierung zu authentifizieren.

**secret**

Gibt an, den geheimen Schlüssel verwenden. Falls leer, wird der geheime Schlüssel gelöscht.

**target**

Gibt ein Ziel im aktuell ausgewählten Subsystem, das Geheimnis zugeordnet werden soll. Dies ist optional, wenn die Einstellung für eines geheimen Schlüssels für den Initiator, und es auslassen gibt an, dass der geheime Schlüssel für alle Ziele verwendet werden, die noch nicht über einen zugeordneten geheimen Schlüssel verfügen.

**initiatorname**

Gibt ein iSCSI-Initiatorname, den geheimen Schlüssel zugeordnet werden soll. Dies ist optional, wenn Sie einen geheimen Schlüssel auf einem Ziel festlegen, und es auslassen gibt an, dass der geheime Schlüssel für alle Initiatoren verwendet werden, die noch nicht über einen zugeordneten geheimen Schlüssel verfügen.

### <a name="BKMK_6"></a>Erstellen

Erstellt eine neue LUN oder iSCSI-Ziel auf dem aktuell ausgewählten Subsystem oder erstellt eine Zielgruppe für Portals für das aktuell ausgewählte Ziel. Sie können anzeigen, die tatsächliche Bindung mithilfe der **DiskRAID Liste** Befehl.

#### <a name="syntax"></a>Syntax

```
create lun simple [size=<n>] [drives=<n>] [noerr]
create lun stripe [size=<n>] [drives=<n, n> [,...]]  [stripesize=<n>] [noerr]
create lun raid [size=<n>] [drives=<n, n> [,...]] [stripesize=<n>] [noerr]
create lun mirror [size=<n>] [drives=<n, n> [,...]] [stripesize=<n>] [noerr]
create lun automagic size=<n> [noerr]
create target name=<name> [iscsiname=<iscsiname>] [noerr]
create tpgroup [noerr]
```

#### <a name="parameter"></a>Parameter

**simple**

Erstellt eine einfache LUN.

**stripe**

Erstellt eine Stripesetvolumes LUN.

**RAID**

Erstellt eine Stripesetvolumes LUN mit Parität.

**mirror**

Erstellt eine gespiegelte LUN.

**automagic**

Erstellt eine LUN mit der *Automagic* Hinweise momentan. Finden Sie unter den **Automagic** untergeordneten Befehl Weitere Informationen.

**size**=

Gibt die gesamte LUN-Größe in Megabyte an. Wenn die **Größe =** Parameter nicht angegeben wird, die LUN erstellt haben, werden die maximal zulässige Größe der Laufwerke zulässig.

Ein Anbieter in der Regel erstellt eine LUN über mindestens so groß sein wie die angeforderte Größe, aber der Anbieter möglicherweise Rundet auf die nächste maximale Größe in einigen Fällen. Wenn Size angegeben ist, wie.99 GB und der Anbieter nur GB datenträgerwertebereichen zugewiesen werden können, würde z. B. die resultierenden LUN 1 GB betragen.

Um die Größe, die mit anderen Einheiten anzugeben, verwenden Sie eine der folgenden Suffixe erkannten unmittelbar auf die Größe aus:
-   **B** für Byte.
-   **KB** für KB.
-   **MB** für Megabyte.
-   **GB** für Gigabyte.
-   **TB** für Terabyte.
-   **PB** Petabyte.

**Laufwerke**=

Gibt an, die *Drive_number* für die Laufwerke mit eine LUN zu erstellen. Wenn die **Größe =** Parameter nicht angegeben wird, die LUN, die erstellt wird, die maximal zulässige Größe der Laufwerke zulässig. Wenn die **Größe =** -Parameter angegeben wird, wählt Anbieter die Laufwerke aus der Liste angegebenen Laufwerk, auf die LUN zu erstellen. Anbieter versucht, verwenden Sie die Laufwerke in der Reihenfolge angegeben werden, wenn möglich.

**stripesize**=

Gibt die Größe in MB für eine *Stripe* oder *RAID* LUN. Die Stripesize kann nicht geändert werden, nachdem die LUN erstellt wurde.

Um die Größe, die mit anderen Einheiten anzugeben, verwenden Sie eine der folgenden Suffixe erkannten unmittelbar auf die Größe aus:
-   **B** für Byte.
-   **KB** für KB.
-   **MB** für Megabyte.
-   **GB** für Gigabyte.
-   **TB** für Terabyte.
-   **PB** Petabyte.

**target**

Erstellt ein neue iSCSI-Ziel auf dem aktuell ausgewählten Subsystem an.

**name**

Gibt den Anzeigenamen für das Ziel an.

**iscsiname**

Stellt der iSCSI-Namen für das Ziel und den Anbieter kann ausgelassen werden, generieren Sie einen Namen.

**tpgroup**

Erstellt eine neue iSCSI-Portal Zielgruppe für das aktuell ausgewählte Ziel.

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs werden ignoriert. Dies ist hilfreich, im Skriptmodus.

#### <a name="remarks"></a>Hinweise

-   Entweder die **Größe**= oder **Laufwerke**= Parameter muss angegeben werden. Sie können auch zusammen verwendet werden.
-   Die Stripegröße für LUNs kann nicht nach der Erstellung nicht geändert werden.

### <a name="BKMK_7"></a>delete

Löscht die aktuell ausgewählten LUN-, iSCSI-Ziel (sofern es sind keine LUNs, die mit dem iSCSI-Ziel verknüpft ist) oder iSCSI-Portal Zielgruppe.

#### <a name="syntax"></a>Syntax

```
delete lun [uninstall] [noerr]
delete target [noerr]
delete tpgroup [noerr]
```

#### <a name="parameters"></a>Parameter

**lun**

Löscht die aktuell ausgewählten LUN und alle Daten darauf.

**uninstall**

Gibt an, dass der Datenträger auf dem lokalen System, das die LUN zugeordnet bereinigt wird, bevor die LUN gelöscht wird.

**target**

Löscht das aktuell ausgewählte iSCSI-Ziel an, wenn keine LUNs mit dem Ziel verknüpft sind.

**tpgroup**

Löscht die aktuell ausgewählten iSCSI-Ziel-Portal-Gruppe.

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs werden ignoriert. Dies ist hilfreich, im Skriptmodus.

### <a name="BKMK_8"></a>detail

Zeigt detaillierte Informationen über das aktuell ausgewählte Objekt des angegebenen Typs.

#### <a name="syntax"></a>Syntax

```
Detail {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup} [verbose]
```

#### <a name="parameters"></a>Parameter

**hbaport**

Listet Informationen über den derzeit ausgewählten Host Bus Hostbusadapter (HBA) Port an.

**iadapter**

Listet Informationen über den derzeit ausgewählten iSCSI-Initiator-Adapter an.

**iportal**

Listet Informationen über das aktuell ausgewählte iSCSI-Initiator-Portal an.

**provider**

Listet Informationen über den derzeit ausgewählten Anbieter an.

**subsystem**

Listet Informationen über das aktuell ausgewählte-Subsystem an.

**controller**

Listet Informationen über den aktuell ausgewählten Controller an.

**port**

Listet Informationen über den derzeit ausgewählten Controller-Port an.

**drive**

Listet Informationen über das ausgewählte Laufwerk, einschließlich der occupying LUNs an.

**lun**

Gibt ausführliche Informationen zu den aktuell ausgewählten LUN, einschließlich der beitragen steuert. Die Ausgabe unterscheidet sich geringfügig, je nachdem, ob die LUN Teil einer Fibre Channel- oder iSCSI-Subsystem. Wenn die Liste Aufheben der Maskierung Hosts nur ein Sternchen enthält, bedeutet dies, dass die LUN für alle Hosts nicht maskiert ist.

**tportal**

Listet Informationen über das aktuell ausgewählte iSCSI-Zielportal an.

**target**

Listet Informationen über das aktuell ausgewählte iSCSI-Ziel an.

**tpgroup**

Listet Informationen über die Zielgruppe für ausgewählte iSCSI-Portal an.

**verbose**

Für die Verwendung nur mit dem LUN-Parameter. Gibt zusätzliche Informationen, einschließlich der zu.

### <a name="BKMK_9"></a>Aufheben der Zuordnung

Legt angegebene Liste der Controllerports als inaktiv für die aktuell ausgewählten LUN (andere Controller Ports nicht betroffen sind.), oder hebt die Zuordnung der angegebenen Liste von iSCSI-Zielen für die aktuell ausgewählten LUN.

#### <a name="syntax"></a>Syntax

```
dissociate controllers <n> [,<n> [,...]]
dissociate ports <n-m>[,<n-m>[,…]]
dissociate targets <n> [,<n> [,…]]
```

#### <a name="parameter"></a>Parameter

**Controller**

Für die Verwendung mit nur Hardwareanbieter für VDS 1.0-Anbieter. Entfernt Controller aus der Liste der Domänencontroller, auf denen der derzeit ausgewählten LUN zugeordnet sind.

**ports**

Für die Verwendung mit nur VDS 1.1-Anbieter. Entfernt Controllerports in der Liste der Controllerports, die derzeit ausgewählten LUN zugeordnet sind.

**targets**

Für die Verwendung mit nur VDS 1.1-Anbieter. Entfernt Ziele aus der Liste der iSCSI-Ziele, die derzeit ausgewählten LUN zugeordnet sind.
```
<n> [,<n> [,…]]
```
Für die Verwendung mit der **Controller** oder **Ziele** Parameter. Gibt die Anzahl von Controllern oder iSCSI-Ziele, die als inaktiv festlegen oder Aufheben der Zuordnung an.
```
<n-m>[,<n-m>[,…]]
```
Für die Verwendung mit der **Ports** Parameter. Gibt an, die Controllerports als inaktiv festlegen, indem Sie über eine Reihe von Controller (*n*) und Port-Nummer (*m*) Paar.

#### <a name="example"></a>Beispiel

```
DISKRAID> SEL LUN 5
LUN 5 is now the selected LUN.

DISKRAID> ASSOCIATE PORTS 0-0,0-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1)

DISKRAID> ASSOCIATE PORTS ADD 1-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 0, Ctlr 0 Port 1, Ctlr 1 Port 1)

DISKRAID> DISSOCIATE PORTS 0-0,1-1
Controller port associations changed.
(Controller ports active after this command: Ctlr 0 Port 1)
```

### <a name="BKMK_10"></a>Beenden

Beendet DiskRAID.

#### <a name="syntax"></a>Syntax

```
exit
```

### <a name="BKMK_11"></a>Erweitern

Erweitert den aktuell ausgewählte LUN durch Hinzufügen von Sektoren am Ende der LUN. Nicht alle Anbieter unterstützen LUNs erweitern. Alle Volumes oder Dateisysteme, die sich auf die LUN befinden wird nicht erweitert werden. Nachdem Sie die LUN erweitert haben, sollten Sie die zugehörigen auf dem Datenträger von Strukturen mit Erweitern der **DiskPart erweitern** Befehl.

#### <a name="syntax"></a>Syntax

```
extend lun [size=<LUN_size>] [drives=<drive_number>, [<drive_number>, ...]] [noerr]
```

#### <a name="parameters"></a>Parameter

**size=**

Gibt die Größe in Megabyte, um die LUN zu erweitern. Wenn die **Größe =** Parameter nicht angegeben wird, die LUN wird durch die von der Laufwerke zugelassene maximale Größe erweitert. Wenn die **Größe =** -Parameter angegeben wird, auswählen von Anbietern Laufwerke aus der Liste, die gemäß der **Laufwerke =** Parameter, um die LUN zu erstellen.

Um die Größe, die mit anderen Einheiten anzugeben, verwenden Sie eine der folgenden Suffixe erkannten unmittelbar auf die Größe aus:
-   **B** für Byte.
-   **KB** für KB.
-   **MB** für Megabyte.
-   **GB** für Gigabyte.
-   **TB** für Terabyte
-   **PB** Petabyte

**drives=**

Gibt an, die \<Drive_number > für die Laufwerke verwenden, wenn Sie eine LUN zu erstellen. Wenn die **Größe =** Parameter nicht angegeben wird, die LUN, die erstellt wird, die maximal zulässige Größe der Laufwerke zulässig. Anbieter verwenden die Laufwerke in der Reihenfolge angegeben werden, wenn möglich.

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs ignoriert werden sollen. Dies ist hilfreich, im Skriptmodus.

#### <a name="remarks"></a>Hinweise

Entweder die *Größe* oder \<Laufwerk >-Parameter muss angegeben werden. Sie können auch zusammen verwendet werden.

### <a name="BKMK_12"></a>flushcache

Löscht den Cache auf dem aktuell ausgewählten Controller.

#### <a name="syntax"></a>Syntax

```
flushcache controller
```

### <a name="BKMK_13"></a>Hilfe

Zeigt eine Liste aller DiskRAID-Befehle.

#### <a name="syntax"></a>Syntax

```
help
```

### <a name="BKMK_14"></a>importtarget

Ruft ab, oder legt diese fest im aktuellen Ziels des Typs Volumeschattenkopie-Dienst (Volume Shadow Copy Service, VSS) importieren, die für das aktuell ausgewählte Subsystem festgelegt ist.

#### <a name="syntax"></a>Syntax

```
importtarget subsystem [set target]
```

#### <a name="parameter"></a>Parameter

**Set-Ziel**

Wenn angegeben, wird das aktuell ausgewählte Ziel für das Ziel des VSS-Import für das aktuell ausgewählte Subsystem. Wenn nicht angegeben, ruft der Befehl im aktuelle VSS-Import-Ziel, die für das aktuell ausgewählte Subsystem festgelegt ist.

### <a name="BKMK_15"></a>initiator

Ruft Informationen über den lokalen iSCSI-Initiator ab.

#### <a name="syntax"></a>Syntax

```
initiator
```

### <a name="BKMK_16"></a>invalidatecache

Erklärt den Cache auf dem derzeit ausgewählten Controller.

#### <a name="syntax"></a>Syntax

```
invalidatecache controller
```

### <a name="BKMK_18"></a>lbpolicy

Legt die Lastenausgleichsrichtlinie für den derzeit ausgewählten LUN fest.

#### <a name="syntax"></a>Syntax

```
lbpolicy set lun type=<type> [paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]]
lbpolicy set lun paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]
```

#### <a name="parameters"></a>Parameter

**type**

Gibt die Lastenausgleichsrichtlinie an. Wenn der Typ nicht angegeben ist, und klicken Sie dann die **Pfad** Parameter muss angegeben werden. Typ kann eine der folgenden sein:

**FAILOVER**: Wird ein primären Pfad mit anderen Pfaden Sicherungspfade wird verwendet.

**ROUNDROBIN**: Alle Pfade verwendet im roundrobinverfahren, die jeweils nacheinander versucht.

**SUBSETROUNDROBIN**: Verwendet von allen primären Pfaden in Roundrobin-Verfahren; Sicherungspfade werden nur verwendet, wenn allen primäre Pfaden Fehler auftreten.

**DYNLQD**: Verwendet den Pfad mit der geringsten Anzahl von aktiven Anforderungen.

**GEWICHTETER**: Verwendet den Pfad mit der geringsten Gewichtung (jeder Pfad muss eine Gewichtung zugewiesen werden).

**LEASTBLOCKS**: Verwendet den Pfad mit der geringsten blockiert.

**VENDORSPECIFIC**: Eine anbieterspezifische-Richtlinie verwendet.

**paths**

Gibt an, ob ein Pfad ist **primären** oder verfügt über einen bestimmten \<Gewichtung >. Alle nicht angegebenen Pfade werden implizit als Sicherung festgelegt. Alle aufgelisteten Pfade muss einer der Pfade für den aktuell ausgewählten LUN.

### <a name="BKMK_19"></a>list

Zeigt eine Liste von Objekten des angegebenen Typs.

#### <a name="syntax"></a>Syntax

```
List {hbaports | iadapters | iportals | providers | subsystems | controllers | ports | drives | LUNs | tportals | targets | tpgroups}
```

#### <a name="parameters"></a>Parameter

**hbaports**

Listet die Zusammenfassungsinformationen zu allen bekannt, dass VDS HBA-Ports. Der aktuell ausgewählte HBA-Port wird durch ein Sternchen (*) gekennzeichnet.

**iadapters**

Listet die Zusammenfassungsinformationen über alle iSCSI-Initiator-Adapter mit VDS bezeichnet. Der Adapter derzeit ausgewählten Initiator wird durch ein Sternchen (*) gekennzeichnet.

**iportals**

Enthält zusammenfassende Informationen über alle iSCSI-Initiator-Portale im aktuell ausgewählten Initiatoradapter. Das aktuell ausgewählte Initiatorportal wird durch ein Sternchen (*) gekennzeichnet.

**providers**

Enthält zusammenfassende Informationen zu jeder bekannt, dass der VDS-Anbieter. Der aktuell ausgewählte Anbieter wird durch ein Sternchen (*) gekennzeichnet.

**subsystems**

Listet die Zusammenfassungsinformationen zu jedem Subsystem im System. Das derzeit ausgewählte Subsystem wird durch ein Sternchen (*) gekennzeichnet.

**Controller**

Listet die Zusammenfassungsinformationen zu jedem Controller im aktuell ausgewählten Subsystem. Der aktuell ausgewählte Controller wird durch ein Sternchen (*) gekennzeichnet.

**ports**

Enthält zusammenfassende Informationen zu jeder Controllerport in der aktuell ausgewählten Controller. Der ausgewählte Port wird durch ein Sternchen (*) gekennzeichnet.

**drives**

Listet die Zusammenfassungsinformationen zu jedem Laufwerk im aktuell ausgewählten Subsystem. Das ausgewählte Laufwerk ist durch ein Sternchen (*) gekennzeichnet.

**luns**

Enthält zusammenfassende Informationen über jede LUN im aktuell ausgewählten Subsystem. Die derzeit ausgewählte LUN wird durch ein Sternchen (*) gekennzeichnet.

**tportals**

Enthält zusammenfassende Informationen über alle iSCSI-Ziel-Portale im aktuell ausgewählten Subsystem. Das Portal für die aktuell ausgewählte Ziel wird durch ein Sternchen (*) gekennzeichnet.

**targets**

Enthält zusammenfassende Informationen über alle iSCSI-Ziele im aktuell ausgewählten Subsystem. Das aktuell ausgewählte Ziel wird durch ein Sternchen (*) gekennzeichnet.

**tpgroups**

Listet die Zusammenfassungsinformationen zu allen iSCSI-Ziel Portal Gruppen in das aktuell ausgewählte Ziel. Die aktuell ausgewählte Portal Gruppe wird durch ein Sternchen (*) gekennzeichnet.

### <a name="BKMK_20"></a>login

Protokolliert den angegebenen iSCSI-Initiator-Adapter in dem aktuell ausgewählten iSCSI-Ziel an.

#### <a name="syntax"></a>Syntax

```
login target iadapter=<iadapter> [type={manual | persistent | boot}] [chap={none | oneway | mutual}] [iportal=<iportal>] [tportal=<tportal>] [<flag> [<flag> […]]]
```

#### <a name="parameters"></a>Parameter

**type**

Gibt den Typ des Anmeldenamens ausführen: **manuelle**, **persistente**, oder **Boot**. Falls nicht angegeben, wird eine manuelle Anmeldung ausgeführt.

**Manuelle** -Anmeldung manuell.

**persistente** : automatisch die gleiche Anmeldung verwenden, wenn der Computer neu gestartet wird.

**Start** -(diese Option ist für die künftige Entwicklung und wird derzeit nicht verwendet *.*)

**chap**

Gibt den Typ der zu verwendenden CHAP-Authentifizierung: **keine**, **Oneway** CHAP ist oder **gegenseitige** CHAP; Wenn nicht anders angegeben, wird keine Authentifizierung verwendet werden.

**tportal**

Gibt ein optionales Ziel-Portal im aktuell ausgewählten Subsystem, die für die Anmeldung verwendet.

**iportal**

Gibt eine optionale Initiatorportal in der angegebenen Initiator-Adapter, die für die Anmeldung verwendet.

\<flag>

Durch die drei Buchstaben bestehende Akronyme identifiziert.

**IPS**: Erfordern von IPsec

**EMP**: Multipfad aktivieren

**EHD**: Headerdigest aktivieren

**EDD**: Datendigest aktivieren

### <a name="BKMK_21"></a>logout

Protokolliert den angegebenen iSCSI-Initiator-Adapter aus dem aktuell ausgewählten iSCSI-Ziel an.

#### <a name="syntax"></a>Syntax

```
logout target iadapter= <iadapter>
```

#### <a name="parameters"></a>Parameter

**iadapter**

Gibt an, die Initiatoradapter mit eine anmeldesitzung Abmelden aus.

### <a name="BKMK_22"></a>Wartung

Führt Wartungsvorgänge für das aktuell ausgewählte Objekt des angegebenen Typs.

#### <a name="syntax"></a>Syntax

```
maintenance <object operation> [count=<iteration>]
```

#### <a name="parameters"></a>Parameter

\<object>

Gibt den Typ des Objekts, um den Vorgang auszuführen. Die *Objekt* kann sein, eine **Subsystem**, **Controller**, **portieren, Laufwerk** oder **LUN**.

\<operation>

Gibt den auszuführenden Wartungsvorgang an. Die *Vorgang* kann sein, **Spinup**, **Spindown**, **blinkt**, **Signalton** oder **Ping** . Ein *Vorgang* muss angegeben werden.

**count=**

Gibt die Anzahl der Wiederholungen der *Vorgang*. Dies wird normalerweise verwendet, mit **blinkt**, **Signalton**, oder **Ping**.

### <a name="BKMK_23"></a>Name

Legt den Anzeigenamen des aktuell ausgewählten Subsystem, LUN oder iSCSI-Ziels auf dem angegebenen Namen fest.

#### <a name="syntax"></a>Syntax

```
name {subsystem | lun | target} [<name>]
```

#### <a name="parameter"></a>Parameter

\<name>

Gibt einen Namen für das Subsystem, LUN oder Ziel. Der Name muss weniger als 64 Zeichen lang sein. Wenn kein Name angegeben wird, wird der vorhandene Namen, ggf. gelöscht.

### <a name="BKMK_24"></a>offline

Legt den Status des angegebenen Typs, das aktuell ausgewählte Objekt **offline**.

#### <a name="syntax"></a>Syntax

```
offline <object>
```

#### <a name="parameter"></a>Parameter

\<object>

Gibt den Typ des Objekts, um diesen Vorgang auszuführen. Die \<Objekt >

kann sein, **Subsystem**, **Controller**, **Laufwerk**, **LUN**, oder **Tportal**.

### <a name="BKMK_25"></a>Online

Legt den Zustand des ausgewählten Objekts des angegebenen Typs zum **online**. Wenn Objekt **Hbaport**, ändert sich der Status der Pfade zu den aktuell ausgewählten HBA-Port **online**.

#### <a name="syntax"></a>Syntax

```
online <object> 
```

#### <a name="parameter"></a>Parameter

\<object>

Gibt den Typ des Objekts, um diesen Vorgang auszuführen. Die \<Objekt >

kann sein, **Hbaport**, **Subsystem**, **Controller**, **Laufwerk**, **LUN**, oder  **TPORTAL**.

### <a name="BKMK_26"></a>recover

Führt Vorgänge erforderlich, z. B. bei der erneuten Synchronisierung oder "Hot" Ersatz, die derzeit ausgewählte fehlertolerante LUN zu reparieren. Z. B. möglicherweise wiederherstellen ein Hotspares zu bindenden ein RAID-Satz, der ein ausgefallener Datenträger oder andere Datenträger Block neuzuordnung verfügt.

#### <a name="syntax"></a>Syntax

```
recover <lun>
```

### <a name="BKMK_27"></a>REENUMERATE

Neu aufgelistet, so Objekte des angegebenen Typs. Wenn Sie das Erweitern LUN-Befehl verwenden, müssen Sie den Refresh-Befehl verwenden, um die Größe des Datenträgers zu aktualisieren, bevor Sie mit dem Befehl Reenumerate.

#### <a name="syntax"></a>Syntax

```
reenumerate {subsystems | drives}
```

#### <a name="parameters"></a>Parameter

**subsystems**

Fragt den Anbieter aus, um neue Subsysteme zu ermitteln, die in den derzeit ausgewählten Anbieter hinzugefügt wurden.

**drives**

Fragt die internen e/a-Busse, um neue Laufwerke erkennen, die im aktuell ausgewählten Subsystem hinzugefügt wurden.

### <a name="BKMK_28"></a>refresh

Aktualisiert interne Daten für den aktuell ausgewählten Anbieter an.

#### <a name="syntax"></a>Syntax

```
refresh provider
```

### <a name="BKMK_29"></a>rem

Kommentar-Skripts verwendet.

#### <a name="syntax"></a>Syntax

```
Rem <comment>
```

### <a name="BKMK_30"></a>remove

Entfernt das angegebene iSCSI-Zielportal aus der aktuell ausgewählten Portal Zielgruppe.

#### <a name="syntax"></a>Syntax

```
remove tpgroup tportal=<tportal> [noerr]
```

#### <a name="parameter"></a>Parameter

**TPGROUP Tportal =** \<Tportal >

Gibt an, das iSCSI-Zielportal entfernen.

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs ignoriert werden sollen. Dies ist hilfreich, im Skriptmodus.

### <a name="BKMK_31"></a>Ersetzen Sie

Ersetzt das angegebene Laufwerk mit dem ausgewählten Laufwerk.

#### <a name="syntax"></a>Syntax

```
replace drive=<drive_number>
```

#### <a name="parameter"></a>Parameter

**drive=**

Gibt an, die \<Drive_number > für das Laufwerk ersetzt werden.

#### <a name="remarks"></a>Hinweise

-   Das angegebene Laufwerk darf nicht mit dem derzeit ausgewählten Laufwerk sein.

### <a name="BKMK_32"></a>reset

Setzt den derzeit ausgewählten Controller oder den Port an.

#### <a name="syntax"></a>Syntax

```
Reset {controller | port}
```

#### <a name="parameters"></a>Parameter

**controller**

Setzt den Controller zurück.

**port**

Setzt den Port an.

### <a name="BKMK_33"></a>select

Zeigt an, oder das aktuell ausgewählte Objekt ändert.

#### <a name="syntax"></a>Syntax

```
Select {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup } [<n>]
```

#### <a name="parameters"></a>Parameter

**object**

Gibt den Typ des Objekts auf. Die \<Objekt > kann sein, **Anbieter**, **Subsystem**, **Controller**, **Laufwerk**, oder **LUN**.

**hbaport** [\<n>]

Legt den Fokus auf den angegebenen lokalen HBA-Port fest. Wenn keine HBA-Port angegeben ist, zeigt der Befehl den aktuell ausgewählten HBA-Port (sofern vorhanden). Keine HBA-Port im Fokus führt einen ungültigen Index der HBA-Port angeben. Auswählen eines HBA-Ports deaktiviert alle ausgewählten Initiator-Adapter und der Initiatorportalen.

**IADAPTER** [\<n >]

Legt den Fokus an den angegebenen lokalen iSCSI-Initiator-Adapter fest. Wenn kein Initiatoradapter angegeben wird, zeigt der Befehl den aktuell ausgewählten Initiatoradapter an, (sofern vorhanden). Ungültige Initiator Adapter Index angeben führt kein Initiatoradapter im Fokus. Auswählen einer Initiator-Adapters hebt die Auswahl alle ausgewählten HBA-Ports und der Initiatorportalen.

**IPORTAL** [\<n >]

Legt den Fokus auf dem angegebenen lokalen iSCSI-Initiator-Portal im ausgewählten iSCSI-Initiator-Adapter fest. Wenn keine Initiatorportal angegeben ist, zeigt der Befehl das aktuell ausgewählte Initiatorportal an, (sofern vorhanden). Ungültige Initiator Portal Index angeben, führt keine ausgewählten Initiator-Portal.

**Anbieter** [\<n >]

Legt den Fokus auf den angegebenen Anbieter fest. Wenn kein Anbieter angegeben wird, zeigt der Befehl den derzeit ausgewählten Anbieter (sofern vorhanden). Einen Ungültiger Anbieter Index angeben, führt kein Anbieter in den Fokus hat.

**Subsystem** [\<n >]

Legt den Fokus auf das angegebene Subsystem fest. Wenn kein Subsystem angegeben wird, zeigt der Befehl das Subsystem mit Fokus (sofern vorhanden). Angeben eines Indexes wurde ein ungültiges Subsystem führt kein Subsystem im Fokus. Ein Subsystem implizit auswählen, wird der entsprechende Anbieter ausgewählt.

**Controller** [\<n >]

Legt den Fokus auf den angegebenen Controller innerhalb des aktuell ausgewählten Subsystems fest. Wenn kein Controller angegeben wird, zeigt der Befehl den aktuell ausgewählten Controller (sofern vorhanden). Einen Ungültiger Controller Index angeben, führt kein Controller in den Fokus hat. Auswählen eines Controllers hebt die Auswahl alle Ports der ausgewählten Controller, Laufwerke, LUNs, Zielportale, Ziele und Zielgruppen für Portals.

**Port** [\<n >]

Legt den Fokus auf den angegebenen Controller-Port in der aktuell ausgewählten Controller fest. Wenn kein Port angegeben ist, zeigt der Befehl den aktuell ausgewählten Port an, (sofern vorhanden). Einen Ungültiger Port Index angeben, führt keine ausgewählten Port.

**drive** [\<n>]

Legt den Fokus auf das angegebene Laufwerk oder physischen Datenträgern, die innerhalb des aktuell ausgewählten Subsystems fest. Wenn kein Laufwerk angegeben wird, zeigt der Befehl das ausgewählte Laufwerk (sofern vorhanden). Einen Ungültiges Laufwerk Index angeben, führt kein Laufwerk in den Fokus hat. Wählen ein Laufwerk hebt die Auswahl alle ausgewählten Controller, Controllerports, LUNs, Zielportale, Ziele und Zielgruppen für Portals.

**lun** [\<n>]

Legt den Fokus auf dem angegebenen LUN innerhalb des aktuell ausgewählten Subsystems fest. Wenn keine LUN angegeben wird, zeigt der Befehl die derzeit ausgewählte LUN (sofern vorhanden). Keine ausgewählten LUN führt einen ungültigen Index für die LUN angeben. Wählen eine LUN hebt die Auswahl alle ausgewählten Controller, Controllerports, Laufwerke, Zielportale, Ziele und Zielgruppen für Portals.

**TPORTAL** [\<n >]

Legt den Fokus auf das angegebene iSCSI-Zielportal innerhalb des aktuell ausgewählten Subsystems fest. Wenn kein Zielportal angegeben wird, zeigt der Befehl das aktuell ausgewählte Ziel-Portal (sofern vorhanden). Einen ungültiges Ziel Portal Index angeben, führt keine ausgewählte Ziel-Portal. Auswählen eines Zielportals hebt die Auswahl alle Controller, Controllerports, Laufwerke, LUNs, Ziele und Zielgruppen für Portals.

**target** [\<n>]

Legt den Fokus auf das angegebene iSCSI-Ziel innerhalb des aktuell ausgewählten Subsystems fest. Wenn kein Ziel angegeben wird, zeigt der Befehl das aktuell ausgewählte Ziel (sofern vorhanden). Einen ungültiges Ziel-Index angeben, führt keine ausgewählte Ziel. Auswählen eines Ziels hebt die Auswahl alle Controller, Controllerports, Laufwerke, LUNs, Zielportale und Zielgruppen für Portals.

**TPGROUP** [\<n >]

Legt den Fokus auf die angegebenen iSCSI-Portal Zielgruppe innerhalb des aktuell ausgewählten iSCSI-Ziels fest. Wenn keine Zielgruppe für Portals angegeben wird, zeigt der Befehl die aktuell ausgewählten Portal Zielgruppe (sofern vorhanden). Einen ungültiges Ziel Portalgruppe Index angeben, führt keine Portal bildschärfenmodus Zielgruppe.

[\<n>]

Gibt an, die \<-Objekt Anzahl > auswählen. Wenn die <object number> angegeben ist nicht gültig ist, wird die vorhandene Auswahl für Objekte des angegebenen Typs werden gelöscht. Wenn kein <object number> angegeben ist, wird das aktuelle Objekt wird angezeigt.

### <a name="BKMK_34"></a>setflag

Das ausgewählte Laufwerk wird als Hotspare festgelegt.

#### <a name="syntax"></a>Syntax

```
setflag drive hotspare={true | false}
```

#### <a name="parameters"></a>Parameter

**true**

Das ausgewählte Laufwerk wird als Hotspare ausgewählt.

**false**

Hebt die Auswahl der aktuell ausgewählten Laufwerks als Hotspare.

#### <a name="remarks"></a>Hinweise

Hotspares können nicht für normale LUN-Vorgängen verwendet werden. Sie sind für die Fehlerbehandlung nur reserviert. Das Laufwerk muss nicht auf alle vorhandenen LUN derzeit gebunden werden.

### <a name="BKMK_shrink"></a>shrink

Reduziert die Größe der ausgewählten LUN.

#### <a name="syntax"></a>Syntax

```
shrink lun size=<n> [noerr]
```

#### <a name="parameters"></a>Parameter

**size=**

Gibt die gewünschte Menge des Speicherplatzes in Megabyte (MB), um die Größe der LUN zu reduzieren. Um die Größe, die mit anderen Einheiten anzugeben, verwenden Sie eine der die bekannte Suffixe (B, KB, MB, GB, TB und PB) unmittelbar auf die Größe aus.

**noerr**

Gibt an, dass Fehler auftreten, die beim Ausführen dieses Vorgangs werden ignoriert. Dies ist hilfreich, im Skriptmodus.

### <a name="BKMK_35"></a>standby

Ändert den Status der Pfade für den aktuell ausgewählten Host Bus Hostbusadapter (HBA)-Port zur STANDBY.

#### <a name="syntax"></a>Syntax

```
standby hbaport
```

#### <a name="parameters"></a>Parameter

**hbaport**

Ändert den Status der Pfade für den aktuell ausgewählten Host Bus Hostbusadapter (HBA)-Port zur STANDBY.

### <a name="BKMK_36"></a>unmask

Wandelt einen der aktuell ausgewählten LUNs in den angegebenen Hosts zugegriffen werden kann.

#### <a name="syntax"></a>Syntax

```
unmask LUN {all | none | [add] wwn=<hexadecimal_number> [;<hexadecimal_number> [;…]] | [add] initiator=<initiator>[;<initiator>[;…]]} [uninstall]
```

#### <a name="parameters"></a>Parameter

**all**

Gibt an, dass die LUN von allen Hosts zugänglich gemacht werden sollen. Allerdings können nicht Sie die LUN für alle Ziele in einem iSCSI-Subsystem durch Aufheben der Maskierung.

> [!IMPORTANT]
> Sie müssen die Abmeldung von das Ziel vor dem Ausführen des Befehls alle Aufheben der MASKIERUNG.

**Keine**

Gibt an, dass die LUN nicht auf einem beliebigen Host zugegriffen werden soll.

> [!IMPORTANT]
> Sie müssen die Abmeldung von das Ziel vor dem Ausführen des Befehls durch Aufheben der MASKIERUNG LUN NONE.

**add**

Gibt an, dass die angegebenen Hosts die vorhandene Liste der Hosts hinzugefügt werden müssen, die dieser LUN aus zugänglich ist. Wenn dieser Parameter nicht angegeben ist, ersetzt die Liste der Hosts, die bereitgestellte die vorhandene Liste der Hosts, denen dieser LUN aus zugänglich ist.

**WWN=**

Gibt eine Liste von hexadezimalen Zahlen, die World Wide-Namen, die von denen der LUN oder Hosts zugänglich sein dürfen darstellt. Um die Maske/auf einen bestimmten Satz von Hosts in einem Fibre Channel-Subsystem Aufheben der Maskierung, können Sie eine durch Semikolons getrennte Liste von WWN für die Ports auf den Hostcomputern von Interesse eingeben.

**initiator=**

Gibt eine Liste von iSCSI-Initiatoren, die derzeit ausgewählte LUN verfügbar gemacht werden sollen. Um die Maske/auf einen bestimmten Satz von Hosts in einem iSCSI-Subsystem Aufheben der Maskierung, können Sie eine durch Semikolons getrennte Liste von iSCSI-Initiator-Namen für die Initiatoren auf den Hostcomputern von Interesse eingeben.

**uninstall**

Wenn angegeben, wird den Datenträger, auf die LUN, auf dem lokalen System zugeordnet ist, bevor Sie die LUN maskiert wird deinstalliert.

## <a name="scripting-diskraid"></a>Scripting DiskRAID

DiskRAID kann ein Skript auf jedem Computer unter Windows Server 2008 oder Windows Server 2003 mit einem zugeordneten VDS-Hardwareanbieter erstellt werden. Ein DiskRAID-Skript, an der Eingabeaufforderung Folgendes aufrufen:
```
diskraid /s <script.txt>
```
Standardmäßig werden DiskRAID beendet die Verarbeitung von Befehlen und gibt einen Fehlercode zurück, wenn ein Problem, in das Skript vorliegt. Zum Fortsetzen der Ausführung des Skripts Fehler ignorieren, und fügen Sie den DiskPart-Parameter auf den Befehl. Dies ermöglicht eine solche nützlichsten Methoden wie die Verwendung eines einzelnen Skripts So löschen Sie alle LUNs in einem Subsystem, unabhängig von der Gesamtanzahl von LUNs. Nicht alle Befehle unterstützen den DiskPart-Parameter. Fehler werden immer zurückgegeben, auf den Befehl-Syntaxfehler, unabhängig davon, ob Sie den DiskPart-Parameter enthalten,

### <a name="diskraid-error-codes"></a>DiskRAID-Fehlercodes

|Fehlercode|Fehlerbeschreibung|
|----------|-----------------|
|0|Kein Fehler aufgetreten ist. Das gesamte Skript wurde ohne Fehler ausgeführt.|
|1|Eine schwerwiegende Ausnahme aufgetreten ist.|
|2|Die in einer Befehlszeile DiskRAID angegebenen Argumente sind falsch.|
|3|DiskRAID konnte die angegebene Skript oder die Ausgabedatei zu öffnen.|
|4|Einer der Dienste verwendeten DiskRAID zurückgegeben einen Fehler.|
|5|Ein Befehlssyntaxfehler ist aufgetreten. Das Skript ist fehlgeschlagen, da ein Objekt nicht ordnungsgemäß ausgewählt wurde, oder war ungültig. für die Verwendung mit diesem Befehl.|

## <a name="example-interactively-view-status-of-subsystem"></a>Beispiel: Interaktives Anzeigen von Status des Subsystems

Wenn Sie den Status des Subsystems 0 auf Ihrem Computer anzeigen möchten, geben Sie Folgendes an der Befehlszeile eingeben:
```
diskraid
```
Drücken Sie die EINGABETASTE. Im folgenden wird angezeigt:
```
Microsoft Diskraid version 5.2.xxxx
Copyright (©) 2003 Microsoft Corporation
On computer: COMPUTER_NAME
```
Um das Subsystem 0 auswählen, geben Sie Folgendes an der Eingabeaufforderung DiskRAID aus:
```
select subsystem 0
```
Drücken Sie die EINGABETASTE. Es wird eine Ausgabe ähnlich der folgenden angezeigt:
```
Subsystem 0 is now the selected subsystem.

DISKRAID> list drives

  Drive ###  Status      Health          Size      Free    Bus  Slot  Flags
  ---------  ----------  ------------  --------  --------  ---  ----  -----
  Drive 0    Online      Healthy         107 GB    107 GB    0     1
  Drive 1    Offline     Healthy          29 GB     29 GB    1     0
  Drive 2    Online      Healthy         107 GB    107 GB    0     2
  Drive 3    Not Ready   Healthy          19 GB     19 GB    1     1
```
Um DiskRAID zu beenden, geben Sie Folgendes an der Eingabeaufforderung DiskRAID aus:
```
exit
```