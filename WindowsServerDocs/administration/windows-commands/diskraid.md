---
title: diskraid
description: 'Windows-Befehle Thema ****- '
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
ms.openlocfilehash: f2dfda058a7ca266adedbacf8860137c5d1782c7
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70867080"
---
# <a name="diskraid"></a>diskraid



Diskraid ist ein Befehlszeilen Tool, mit dem Sie redundante Arrays unabhängiger (oder kostengünstiger) Speicher Subsysteme (oder kostengünstiger) konfigurieren und verwalten können.

RAID ist eine Methode, mit der fehlertolerante Datenträger Systeme standardisiert und kategorisiert werden. RAID-Stufen bieten verschiedene Mischung aus Leistung, Zuverlässigkeit und Kosten. RAID wird in der Regel auf Servern verwendet. Einige Server stellen drei der RAID-Stufen bereit: Ebene 0 (Striping), Ebene 1 (Spiegelung) und Ebene 5 (Striping mit Parität).

Ein Hardware-RAID-Subsystem unterscheidet physisch adressierbare Speichereinheiten mithilfe einer logischen Gerätenummer (Logical Unit Number, LUN) voneinander. Ein LUN-Objekt muss mindestens einen Plex aufweisen und kann über eine beliebige Anzahl zusätzlicher plexes verfügen. Jeder Plex enthält eine Kopie der Daten auf dem LUN-Objekt. Plexes können einem LUN-Objekt hinzugefügt und daraus entfernt werden.

Die meisten Diskraid-Befehle arbeiten an einem bestimmten HBA-Port (Hostbus Adapter), einem Initiatoradapter, einem Initiator-Portal, einem Anbieter, einem Subsystem, einem Controller, einem Port, einem Laufwerk, einer LUN, einem Zielportal, einer Zielgruppe oder Zielportal Verwenden Sie den SELECT-Befehl, um ein Objekt auszuwählen. Das ausgewählte Objekt hat den Fokus. Der Fokus vereinfacht allgemeine Konfigurationsaufgaben, z. b. das Erstellen mehrerer LUNs innerhalb desselben Subsystems.

> [!NOTE]
> Das Diskraid-Befehlszeilen Tool funktioniert nur mit Speicher Subsystemen, die den Dienst für virtuelle Datenträger (Virtual Disk Service, VDS) unterstützen.

## <a name="diskraid-commands"></a>Diskraid-Befehle

Um die Befehlssyntax anzuzeigen, klicken Sie auf einen der folgenden Befehle:
-   [add](#BKMK_1)
-   [ierter](#BKMK_2)
-   [automagisch](#BKMK_3)
-   [break](#BKMK_4)
-   [CHAP](#BKMK_5)
-   [create](#BKMK_6)
-   [Lösch](#BKMK_7)
-   [einzelnen](#BKMK_8)
-   [Trennen](#BKMK_9)
-   [exit](#BKMK_10)
-   [extend](#BKMK_11)
-   [flushcache](#BKMK_12)
-   [help](#BKMK_13)
-   [IMPORTTARGET](#BKMK_14)
-   [initiator](#BKMK_15)
-   [INVALIDATECACHE](#BKMK_16)
-   [lbpolicy](#BKMK_18)
-   [List](#BKMK_19)
-   [login](#BKMK_20)
-   [logout](#BKMK_21)
-   [Unterhalt](#BKMK_22)
-   [name](#BKMK_23)
-   [aufzu](#BKMK_24)
-   [Internet](#BKMK_25)
-   [recover](#BKMK_26)
-   [erneut auflisten](#BKMK_27)
-   [erneuten](#BKMK_28)
-   [rem](#BKMK_29)
-   [aufgeh](#BKMK_30)
-   [replace](#BKMK_31)
-   [Festlegen](#BKMK_32)
-   [Auswahl](#BKMK_33)
-   [setflag](#BKMK_34)
-   [shrink](#BKMK_shrink)
-   [Standby](#BKMK_35)
-   [Maskierung](#BKMK_36)

### <a name="BKMK_1"></a>eren

Fügt der aktuell ausgewählten LUN eine vorhandene LUN hinzu oder fügt der aktuell ausgewählten iSCSI-Zielportal Gruppe ein iSCSI-Zielportal hinzu.

#### <a name="syntax"></a>Syntax

```
add plex lun=n [noerr]
add tpgroup tportal=n [noerr]
```

#### <a name="parameters"></a>Parameter

**Plex-LUN**=*n*

Gibt die LUN-Nummer an, die der aktuell ausgewählten LUN als Plex hinzugefügt werden soll.

> [!CAUTION]
> Alle Daten auf der LUN, die als Plex hinzugefügt werden, werden gelöscht.

**TPGROUP TPORTAL =** <em>n</em>

Gibt die iSCSI-Zielportal-Nummer an, die der aktuell ausgewählten iSCSI-Zielportal Gruppe hinzugefügt werden soll.

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden. Dies ist im Skript Modus nützlich.

### <a name="BKMK_2"></a>ierter

Legt die angegebene Liste von Controller Anschlüssen als aktiv für die aktuell ausgewählte LUN (andere Controller Anschlüsse werden inaktiv) oder fügt die angegebenen Controller Anschlüsse der Liste der vorhandenen aktiven Controller Anschlüsse für die aktuell ausgewählte LUN hinzu oder ordnet die das angegebene iSCSI-Ziel für die aktuell ausgewählte LUN.

#### <a name="syntax"></a>Syntax

```
associate controllers [add] <n>[,<n> [,…]]
associate ports [add] <n-m>[,<n-m>[,…]]
associate targets [add] <n>[,<n> [,…]]
```

#### <a name="parameters"></a>Parameter

**kontrolliert**

Nur für die Verwendung mit VDS 1,0-Anbietern. Fügt der Liste der Controller, die der aktuell ausgewählten LUN zugeordnet sind, hinzu oder ersetzt Sie.

**Landungen**

Nur für die Verwendung mit VDS 1,1-Anbietern. Fügt die Liste der Controllerports hinzu, die der aktuell ausgewählten LUN zugeordnet sind, oder ersetzt Sie.

**Lern**

Nur für die Verwendung mit VDS 1,1-Anbietern. Fügt die Liste der iSCSI-Ziele, die der aktuell ausgewählten LUN zugeordnet sind, hinzu oder ersetzt Sie.

**add**

Fügt bei VDS 1,0-Anbietern die angegebenen Controller der vorhandenen Liste der der LUN zugeordneten Controller hinzu. Wenn dieser Parameter nicht angegeben wird, ersetzt die Liste der Controller die vorhandene Liste von Controllern, die dieser LUN zugeordnet sind.

Fügt bei VDS 1,1-Anbietern die angegebenen Controller Anschlüsse der vorhandenen Liste der der LUN zugeordneten Controllerports hinzu. Wenn dieser Parameter nicht angegeben wird, ersetzt die Liste der Controllerports die vorhandene Liste der Controllerports, die dieser LUN zugeordnet sind.
```
<n>[,<n> [, ...]]
```
Zur Verwendung mit dem **Controller** oder dem **Targets** -Parameter. Gibt die Anzahl der Controller oder iSCSI-Ziele an, die auf "aktiv" oder "zuordnen" festgelegt werden
```
<n-m>[,<n-m>[,…]]
```
Zur Verwendung mit dem **Ports** -Parameter. Gibt die Controllerports an, die mithilfe einer Controller Nummer (*n*) und eines Portnummern Paars (*m*) aktiv festgelegt werden sollen.

#### <a name="example"></a>Beispiel

Im folgenden Beispiel wird gezeigt, wie Sie Ports einer LUN zuordnen und hinzufügen, die einen VDS 1,1-Anbieter verwendet:
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

### <a name="BKMK_3"></a>automagisch

Legt Flags fest, die den Anbietern Hinweise zum Konfigurieren einer LUN zur Verfügung stellt, oder löscht sie. Der **automagingvorgang** wird ohne Parameter verwendet und zeigt eine Liste von Flags an.

#### <a name="syntax"></a>Syntax

```
automagic {set | clear | apply} all <flag=value> [<flag=value> [...]]
```

#### <a name="parameters"></a>Parameter

**set**

Legt die angegebenen Flags auf die angegebenen Werte fest.

**Klartext**

Löscht die angegebenen Flags. Mit dem **all** -Schlüsselwort werden alle automagflags gelöscht.

**Apply**

Wendet die aktuellen Flags auf die ausgewählte LUN an.

\<Flag >

Flags werden durch aus drei Buchstaben bestehende Akronyme identifiziert.

|Flag|Beschreibung|
|----|-----------|
|F|Schnelle Wiederherstellung von Abstürzen erforderlich|
|FTL|Fehler tolerant|
|MSR|Meistens Lesevorgänge|
|MXD|Maximale Laufwerke|
|MXS|Maximale Größe erwartet|
|AS|Optimale Lese Ausrichtung|
|KANZLER|Optimale Lese Größe|
|OSR|Bei sequenziellen Lesevorgängen optimieren|
|OSW|Bei sequenziellen Schreibvorgängen optimieren|
|OWA|Optimale Schreib Ausrichtung|
|WINDEN|Optimale Schreibgröße|
|RBP|Priorität neu erstellen|
|RBV|Read-Back-Überprüfung aktiviert|
|RMP|Neuzuordnung aktiviert|
|WESTE|Stripe-Größe|
|WTC|Write-Through-Caching aktiviert|
|YNK|Ab|

### <a name="BKMK_4"></a>Umbruch

Entfernt den Plex aus der aktuell ausgewählten LUN. Der Plex und die darin enthaltenen Daten werden nicht beibehalten, und die Laufwerks Blöcke können freigegeben werden.

#### <a name="syntax"></a>Syntax

```
break plex=<plex_number> [noerr]
```

#### <a name="parameters"></a>Parameter

**Plex**

Gibt die Nummer des zu entfernenden Plex an. Der Plex und die darin enthaltenen Daten werden nicht beibehalten, und die von diesem Plex verwendeten Ressourcen werden freigegeben. Es ist nicht garantiert, dass die in der LUN enthaltenen Daten konsistent sind. Wenn Sie diesen Plex beibehalten möchten, verwenden Sie den Volumeschattenkopie-Dienst (VSS).

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden. Dies ist im Skript Modus nützlich.

#### <a name="remarks"></a>Hinweise

> [!NOTE]
> Sie müssen zuerst eine gespiegelte LUN auswählen, bevor Sie den **break** -Befehl verwenden.

> [!CAUTION]
> Alle Daten auf dem Plex werden gelöscht.

> [!CAUTION]
> Es ist nicht sichergestellt, dass alle Daten, die in der ursprünglichen LUN enthalten sind, einheitlich sind.

### <a name="BKMK_5"></a>CHAP

Legt den gemeinsamen geheimen Schlüssel des Challenge Handshake Authentication-Protokolls (CHAP) so fest, dass iSCSI-Initiatoren und iSCSI-Ziele miteinander kommunizieren können.

#### <a name="syntax"></a>Syntax

```
chap initiator set secret=[<secret>] [target=<target>]
chap initiator remember secret=[<secret>] target=<target>
chap target set secret=[<secret>] [initiator=<initiatorname>]
chap target remember secret=[<secret>] initiator=<initiatorname>
```

#### <a name="parameters"></a>Parameter

**initiatorsatz**

Legt den gemeinsamen geheimen Schlüssel im lokalen iSCSI-Initiatordienst für die gegenseitige CHAP-Authentifizierung fest, wenn der Initiator das Ziel authentifiziert.

**Erinnerung an Initiator**

Kommuniziert das CHAP-Geheimnis eines iSCSI-Ziels mit dem lokalen iSCSI-Initiatordienst, sodass der Initiatordienst das Geheimnis verwenden kann, um sich bei der CHAP-Authentifizierung beim Ziel zu authentifizieren.

**Zielsatz**

Legt den gemeinsamen geheimen Schlüssel im aktuell ausgewählten iSCSI-Ziel für die CHAP-Authentifizierung fest, wenn der Initiator vom Ziel authentifiziert wird.

**Ziel speichern**

Kommuniziert das CHAP-Geheimnis eines iSCSI-Initiators mit dem aktuellen iSCSI-Ziel im Fokus, sodass das Ziel das Geheimnis verwenden kann, um sich bei der wechselseitigen CHAP-Authentifizierung beim Initiator zu authentifizieren.

**geheimen**

Gibt den zu verwendenden geheimen Schlüssel an. Wenn der Eintrag leer ist, wird der geheime Schlüssel gelöscht.

**target**

Gibt ein Ziel im aktuell ausgewählten Subsystem an, das dem geheimen Schlüssel zugeordnet werden soll. Dies ist optional, wenn Sie einen geheimen Schlüssel für den Initiator festlegen und ihn verlassen, gibt an, dass der geheime Schlüssel für alle Ziele verwendet wird, die noch nicht über ein zugeordnetes Geheimnis verfügen.

**Initiatorname**

Gibt einen iSCSI-Initiatornamen an, der dem geheimen Schlüssel zugeordnet werden soll. Dies ist optional, wenn ein Geheimnis für ein Ziel festgelegt wird und das Geheimnis nicht angezeigt wird, dass das Geheimnis für alle Initiatoren verwendet wird, die noch nicht über einen zugehörigen geheimen Schlüssel verfügen.

### <a name="BKMK_6"></a>Stelle

Erstellt eine neue LUN oder ein iSCSI-Ziel für das aktuell ausgewählte Subsystem oder erstellt eine Zielportal Gruppe für das aktuell ausgewählte Ziel. Die tatsächliche Bindung können Sie mit dem Befehl **Diskraid List** anzeigen.

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

**einfache**

Erstellt eine einfache LUN.

**Reifen**

Erstellt eine stripesetlun.

**RAZZIEN**

Erstellt eine stripesetlun mit Parität.

**OL**

Erstellt eine gespiegelte LUN.

**automagisch**

Erstellt eine LUN mithilfe der zurzeit gültigen *automagandeutungen* . Weitere Informationen finden Sie unter dem Unterbefehl **AUTOMAGIC** .

**Größe**=

Gibt die Gesamtgröße der LUN in Megabyte an. Wenn der **size =** -Parameter nicht angegeben wird, ist die LUN, die für alle angegebenen Laufwerke zulässig ist, die größtmögliche Größe.

Ein Anbieter erstellt in der Regel eine LUN, die mindestens so groß wie die angeforderte Größe ist, aber der Anbieter muss in einigen Fällen möglicherweise auf die nächst größere Größe aufrunden. Wenn z. b. Size als. 99 GB angegeben wird und der Anbieter nur GB Datenträger Blöcke zuordnen kann, beträgt die resultierende LUN 1 GB.

Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:
-   **B** für Byte.
-   **KB** für Kilobyte.
-   **MB** für Megabyte.
-   **GB** für Gigabyte.
-   **TB** für Terabyte.
-   **PB** für "Peer".

**Master**=

Gibt den *drive_number* für die Laufwerke an, die zum Erstellen einer LUN verwendet werden sollen. Wenn der **size =** -Parameter nicht angegeben wird, ist die LUN, die für alle angegebenen Laufwerke zulässig ist, die größtmögliche Größe. Wenn der **size =** -Parameter angegeben wird, wählen die Anbieter Laufwerke aus der angegebenen Laufwerks Liste aus, um die LUN zu erstellen. Anbieter versuchen, die Laufwerke nach Möglichkeit in der angegebenen Reihenfolge zu verwenden.

**stripesize**=

Gibt die Größe für eine *Stripe* -oder *RAID* -LUN in Megabyte an. Die stripesize kann nicht geändert werden, nachdem die LUN erstellt wurde.

Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:
-   **B** für Byte.
-   **KB** für Kilobyte.
-   **MB** für Megabyte.
-   **GB** für Gigabyte.
-   **TB** für Terabyte.
-   **PB** für "Peer".

**target**

Erstellt ein neues iSCSI-Ziel für das derzeit ausgewählte Subsystem.

**name**

Gibt den anzeigen Amen für das Ziel an.

**iscsiname**

Gibt den iSCSI-Namen für das Ziel an und kann weggelassen werden, damit der Anbieter einen Namen generiert.

**TPGROUP**

Erstellt eine neue iSCSI-Zielportal Gruppe für das aktuell ausgewählte Ziel.

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden. Dies ist im Skript Modus nützlich.

#### <a name="remarks"></a>Hinweise

-   Entweder der **size**=-Parameter oder der **Drives**=-Parameter muss angegeben werden. Sie können auch gleichzeitig verwendet werden.
-   Die Stripesetgröße für eine LUN kann nach der Erstellung nicht mehr geändert werden.

### <a name="BKMK_7"></a>Lösch

Löscht die derzeit ausgewählte LUN, das iSCSI-Ziel (sofern keine LUNs mit dem iSCSI-Ziel verknüpft sind) oder die iSCSI-Zielportal Gruppe.

#### <a name="syntax"></a>Syntax

```
delete lun [uninstall] [noerr]
delete target [noerr]
delete tpgroup [noerr]
```

#### <a name="parameters"></a>Parameter

**LUN**

Löscht die derzeit ausgewählte LUN und alle darin ausgewählten Daten.

**stalli**

Gibt an, dass der Datenträger auf dem lokalen System, der der LUN zugeordnet ist, bereinigt wird, bevor die LUN gelöscht wird.

**target**

Löscht das aktuell ausgewählte iSCSI-Ziel, wenn dem Ziel keine LUNs zugeordnet sind.

**TPGROUP**

Löscht die derzeit ausgewählte iSCSI-Zielportal Gruppe.

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden. Dies ist im Skript Modus nützlich.

### <a name="BKMK_8"></a>einzelnen

Zeigt ausführliche Informationen über das aktuell ausgewählte Objekt des angegebenen Typs an.

#### <a name="syntax"></a>Syntax

```
Detail {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup} [verbose]
```

#### <a name="parameters"></a>Parameter

**HBAPORT**

Listet ausführliche Informationen zum aktuell ausgewählten HBA-Port (Hostbus Adapter) auf.

**IADAPTER**

Listet ausführliche Informationen zum aktuell ausgewählten iSCSI-Initiator-Adapter auf.

**IPORTAL**

Listet ausführliche Informationen über das aktuell ausgewählte iSCSI-Initiator-Portal auf.

**ab**

Listet ausführliche Informationen über den aktuell ausgewählten Anbieter auf.

**subsystem**

Listet ausführliche Informationen über das aktuell ausgewählte Subsystem auf.

**ern**

Listet ausführliche Informationen über den aktuell ausgewählten Controller auf.

**Port**

Listet ausführliche Informationen zum aktuell ausgewählten Controllerport auf.

**Antrie**

Listet ausführliche Informationen über das aktuell ausgewählte Laufwerk, einschließlich der ersetzenden LUNs, auf.

**LUN**

Listet ausführliche Informationen über die derzeit ausgewählte LUN, einschließlich der Mitwirkenden Laufwerke. Die Ausgabe unterscheidet sich geringfügig, je nachdem, ob die LUN Teil eines Fibre Channel-oder iSCSI-Subsystems ist. Wenn die Liste der nicht maskierten Hosts nur ein Sternchen enthält, bedeutet dies, dass die LUN für alle Hosts unmaskiert ist.

**Portal – Entitäten**

Listet ausführliche Informationen über das aktuell ausgewählte iSCSI-Zielportal auf.

**target**

Listet ausführliche Informationen über das aktuell ausgewählte iSCSI-Ziel auf.

**TPGROUP**

Listet ausführliche Informationen zur aktuell ausgewählten iSCSI-Zielportal Gruppe auf.

**Ausführliche**

Nur für die Verwendung mit dem LUN-Parameter. Listet zusätzliche Informationen, einschließlich der zugehörigen plexes, auf.

### <a name="BKMK_9"></a>Trennen

Legt die angegebene Liste von Controllerports für die aktuell ausgewählte LUN als inaktiv fest (andere Controller Anschlüsse sind nicht betroffen) oder trennt die angegebene Liste von iSCSI-Zielen für die aktuell ausgewählte LUN.

#### <a name="syntax"></a>Syntax

```
dissociate controllers <n> [,<n> [,...]]
dissociate ports <n-m>[,<n-m>[,…]]
dissociate targets <n> [,<n> [,…]]
```

#### <a name="parameter"></a>Parameter

**kontrolliert**

Nur für die Verwendung mit VDS 1,0-Anbietern. Entfernt Controller aus der Liste der Controller, die der aktuell ausgewählten LUN zugeordnet sind.

**Landungen**

Nur für die Verwendung mit VDS 1,1-Anbietern. Entfernt Controller Anschlüsse aus der Liste der Controllerports, die der aktuell ausgewählten LUN zugeordnet sind.

**Lern**

Nur für die Verwendung mit VDS 1,1-Anbietern. Entfernt Ziele aus der Liste der iSCSI-Ziele, die der aktuell ausgewählten LUN zugeordnet sind.
```
<n> [,<n> [,…]]
```
Zur Verwendung mit dem **Controller** oder dem **Targets** -Parameter. Gibt die Anzahl der Controller oder iSCSI-Ziele an, die als inaktiv festgelegt oder getrennt werden sollen.
```
<n-m>[,<n-m>[,…]]
```
Zur Verwendung mit dem **Ports** -Parameter. Gibt die Controller Anschlüsse an, die als inaktiv festgelegt werden sollen, indem eine Controller Nummer (*n*) und ein Portnummern Paar (*m*) verwendet werden.

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

### <a name="BKMK_10"></a>Abstiegs

Beendet Diskraid.

#### <a name="syntax"></a>Syntax

```
exit
```

### <a name="BKMK_11"></a>gewähren

Erweitert die aktuell ausgewählte LUN, indem Sektoren am Ende der LUN hinzugefügt werden. Nicht alle Anbieter unterstützen das Erweitern von LUNs. Erweitert keine Volumes oder Dateisysteme, die auf der LUN enthalten sind. Nachdem Sie die LUN erweitert haben, sollten Sie die zugeordneten Strukturen auf dem Datenträger mithilfe des Befehls **DiskPart Extend** erweitern.

#### <a name="syntax"></a>Syntax

```
extend lun [size=<LUN_size>] [drives=<drive_number>, [<drive_number>, ...]] [noerr]
```

#### <a name="parameters"></a>Parameter

**Größe =**

Gibt die Größe in Megabyte an, um die LUN zu erweitern. Wenn der **size =** -Parameter nicht angegeben wird, wird die LUN um die größtmögliche Größe erweitert, die von allen angegebenen Laufwerken zugelassen wird. Wenn der **size =** -Parameter angegeben wird, wählen Anbieter Laufwerke aus der Liste aus, die durch den **Laufwerke =** -Parameter angegeben wird, um die LUN zu erstellen.

Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:
-   **B** für Byte.
-   **KB** für Kilobyte.
-   **MB** für Megabyte.
-   **GB** für Gigabyte.
-   **TB** für Terabyte
-   **PB** für "Peer Tabellen"

**Laufwerke =**

Gibt den \<drive_number-> für die Laufwerke an, die beim Erstellen einer LUN verwendet werden sollen. Wenn der **size =** -Parameter nicht angegeben wird, ist die LUN, die für alle angegebenen Laufwerke zulässig ist, die größtmögliche Größe. Anbieter verwenden die Laufwerke in der angegebenen Reihenfolge, wenn möglich.

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden sollen. Dies ist im Skript Modus nützlich.

#### <a name="remarks"></a>Hinweise

Es muss entweder die Größe \<oder das Laufwerk >-Parameters angegeben werden. Sie können auch gleichzeitig verwendet werden.

### <a name="BKMK_12"></a>flushcache

Löscht den Cache auf dem aktuell ausgewählten Controller.

#### <a name="syntax"></a>Syntax

```
flushcache controller
```

### <a name="BKMK_13"></a>Hilfe

Zeigt eine Liste aller Diskraid-Befehle an.

#### <a name="syntax"></a>Syntax

```
help
```

### <a name="BKMK_14"></a>IMPORTTARGET

Ruft das VSS-Import Ziel (Current Volumeschattenkopie-Dienst) ab, das für das aktuell ausgewählte Subsystem festgelegt ist, oder legt dieses fest.

#### <a name="syntax"></a>Syntax

```
importtarget subsystem [set target]
```

#### <a name="parameter"></a>Parameter

**Ziel festlegen**

Bei Angabe dieser Option wird das aktuell ausgewählte Ziel auf das VSS-Import Ziel für das aktuell ausgewählte Subsystem festgelegt. Wenn nicht angegeben, ruft der Befehl das aktuelle VSS-Import Ziel ab, das für das aktuell ausgewählte Subsystem festgelegt ist.

### <a name="BKMK_15"></a>Photo

Ruft Informationen zum lokalen iSCSI-Initiator ab.

#### <a name="syntax"></a>Syntax

```
initiator
```

### <a name="BKMK_16"></a>INVALIDATECACHE

Erklärt den Cache auf dem aktuell ausgewählten Controller für ungültig.

#### <a name="syntax"></a>Syntax

```
invalidatecache controller
```

### <a name="BKMK_18"></a>lbpolicy

Legt die Richtlinie für den Lastenausgleich für die aktuell ausgewählte LUN fest.

#### <a name="syntax"></a>Syntax

```
lbpolicy set lun type=<type> [paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]]
lbpolicy set lun paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]
```

#### <a name="parameters"></a>Parameter

**type**

Gibt die Richtlinie für den Lastenausgleich an. Wenn der Typ nicht angegeben wird, muss der **path** -Parameter angegeben werden. Der Typ kann eines der folgenden sein:

**FAILOVER**: Verwendet einen primären Pfad mit anderen Pfaden, die Sicherungs Pfade sind.

**ROUNDROBIN**: Verwendet alle Pfade im Roundrobin-Verfahren, wobei jeder Pfad nacheinander ausprobiert wird.

**SUBNETZTROUNDROBIN**: Verwendet alle primären Pfade im Roundrobin-Verfahren. Sicherungs Pfade werden nur verwendet, wenn alle primären Pfade fehlschlagen.

**DYNLQD**: Verwendet den Pfad mit der geringsten Anzahl aktiver Anforderungen.

**GEWICHTET**: Verwendet den Pfad mit dem geringsten Gewicht (jedem Pfad muss eine Gewichtung zugewiesen werden).

**LEASTBLOCKS**: Verwendet den Pfad mit den geringsten Blöcken.

**VENDORSPECIFIC**: Verwendet eine herstellerspezifische Richtlinie.

**Tramp**

Gibt an, ob ein Pfad **primär** ist oder über \<ein bestimmtes Gewichtungs > verfügt. Alle Pfade, die nicht angegeben sind, werden implizit als Sicherung festgelegt. Alle aufgelisteten Pfade müssen einer der aktuell ausgewählten Pfade der LUN sein.

### <a name="BKMK_19"></a>List

Zeigt eine Liste von Objekten des angegebenen Typs an.

#### <a name="syntax"></a>Syntax

```
List {hbaports | iadapters | iportals | providers | subsystems | controllers | ports | drives | LUNs | tportals | targets | tpgroups}
```

#### <a name="parameters"></a>Parameter

**hbapbrüche**

Listet zusammenfassende Informationen zu allen HBA-Ports auf, die VDS bekannt sind. Der aktuell ausgewählte HBA-Port wird durch ein Sternchen (*) markiert.

**IADAPTERS**

Listet Zusammenfassungs Informationen zu allen iSCSI-Initiator-Adaptern, die VDS bekannt sind. Der aktuell ausgewählte Initiatoradapter wird durch ein Sternchen (*) markiert.

**iportale**

Listet zusammenfassende Informationen zu allen iSCSI-Initiator-Portalen im aktuell ausgewählten Initiator-Adapter auf. Das aktuell ausgewählte Initiatorportal wird durch ein Sternchen (*) markiert.

**Anbieter**

Listet zusammenfassende Informationen zu den einzelnen Anbietern von VDS auf. Der aktuell ausgewählte Anbieter wird durch ein Sternchen (*) markiert.

**Subsysteme**

Listet zusammenfassende Informationen zu den einzelnen Subsystemen im System auf. Das aktuell ausgewählte Subsystem wird durch ein Sternchen (*) markiert.

**kontrolliert**

Listet Zusammenfassungs Informationen zu jedem Controller im aktuell ausgewählten Subsystem auf. Der aktuell ausgewählte Controller wird durch ein Sternchen (*) markiert.

**Landungen**

Listet Zusammenfassungs Informationen zu jedem Controller Anschluss im aktuell ausgewählten Controller auf. Der aktuell ausgewählte Port wird durch ein Sternchen (*) markiert.

**Master**

Listet Zusammenfassungs Informationen zu jedem Laufwerk im aktuell ausgewählten Subsystem auf. Das aktuell ausgewählte Laufwerk wird durch ein Sternchen (*) markiert.

**LUNs**

Listet zusammenfassende Informationen zu den einzelnen LUN im aktuell ausgewählten Subsystem auf. Die aktuell ausgewählte LUN wird durch ein Sternchen (*) markiert.

**tportale**

Listet zusammenfassende Informationen zu allen iSCSI-Ziel Portalen im aktuell ausgewählten Subsystem auf. Das aktuell ausgewählte Zielportal wird durch ein Sternchen (*) markiert.

**Lern**

Listet zusammenfassende Informationen zu allen iSCSI-Zielen im aktuell ausgewählten Subsystem auf. Das aktuell ausgewählte Ziel ist durch ein Sternchen (*) markiert.

**TPGROUPS**

Listet Zusammenfassungs Informationen zu allen iSCSI-Zielportal Gruppen im aktuell ausgewählten Ziel auf. Die aktuell ausgewählte Portal Gruppe wird durch ein Sternchen (*) markiert.

### <a name="BKMK_20"></a>Anmel

Protokolliert den angegebenen iSCSI-Initiator-Adapter im aktuell ausgewählten iSCSI-Ziel.

#### <a name="syntax"></a>Syntax

```
login target iadapter=<iadapter> [type={manual | persistent | boot}] [chap={none | oneway | mutual}] [iportal=<iportal>] [tportal=<tportal>] [<flag> [<flag> […]]]
```

#### <a name="parameters"></a>Parameter

**type**

Gibt den Typ des auszuführenden Anmelde namens an: **manuell**, **beständig**oder **gestartet**. Wenn keine Angabe erfolgt, wird ein manueller Anmelde Name ausgeführt.

**Manuelles** anmelden manuell.

**permanent** : verwendet automatisch denselben Anmelde Namen, wenn der Computer neu gestartet wird.

**Start** : (diese Option ist für die zukünftige Entwicklung vorgesehen und wird zurzeit nicht verwendet<em>.</em>)

**CHAP**

Gibt den Typ der zu verwendenden CHAP-Authentifizierung an: **None**, **OneWay** CHAP oder **gegenseitiges** CHAP. Wenn keine Angabe erfolgt, wird keine Authentifizierung verwendet.

**Portal – Entitäten**

Gibt ein optionales Zielportal im aktuell ausgewählten Subsystem an, das für die Anmeldung verwendet werden soll.

**IPORTAL**

Gibt ein optionales Initiatorportal im angegebenen Initiator-Adapter an, das für die Anmeldung verwendet werden soll.

\<Flag >

Identifiziert durch drei Buchstaben von Akronymen:

**IP**-ADRESSEN: IPSec erforderlich

**EMP**: Multipfad aktivieren

**EHD**: Header Digest aktivieren

**EDD**: Daten Digest aktivieren

### <a name="BKMK_21"></a>Abmelde

Protokolliert den angegebenen iSCSI-Initiator-Adapter aus dem aktuell ausgewählten iSCSI-Ziel.

#### <a name="syntax"></a>Syntax

```
logout target iadapter= <iadapter>
```

#### <a name="parameters"></a>Parameter

**IADAPTER**

Gibt den Initiator-Adapter mit einer Anmelde Sitzung an, von der abgemeldet werden soll.

### <a name="BKMK_22"></a>Unterhalt

Führt Wartungsvorgänge für das aktuell ausgewählte Objekt des angegebenen Typs aus.

#### <a name="syntax"></a>Syntax

```
maintenance <object operation> [count=<iteration>]
```

#### <a name="parameters"></a>Parameter

\<Objekt >

Gibt den Objekttyp an, für den der Vorgang durchgeführt werden soll. Der *Objekttyp* kann ein **Subsystem**, ein **Controller**, ein **Port, ein Laufwerk** oder eine **LUN**sein.

\<Vorgangs >

Gibt den auszuführenden Wartungs Vorgang an. Der Vorgangstyp kann **SpinUp**, **Spindown**, **Blink**, **Signal Tons** oder **Ping**sein. Es muss ein *Vorgang* angegeben werden.

**Anzahl =**

Gibt an, wie oft der *Vorgang*wiederholt werden soll. Dies wird in der Regel mit **Blink**, **Signal Tons**oder **Ping**verwendet.

### <a name="BKMK_23"></a>Benennen

Legt den anzeigen amen des derzeit ausgewählten Subsystems, LUN oder iSCSI-Ziels auf den angegebenen Namen fest.

#### <a name="syntax"></a>Syntax

```
name {subsystem | lun | target} [<name>]
```

#### <a name="parameter"></a>Parameter

\<Name >

Gibt einen Namen für das Subsystem, die LUN oder das Ziel an. Der Name muss eine Länge von weniger als 64 Zeichen aufweisen. Wenn kein Name angegeben wird, wird der vorhandene Name (sofern vorhanden) gelöscht.

### <a name="BKMK_24"></a>aufzu

Legt den Zustand des aktuell ausgewählten Objekts des angegebenen Typs auf **Offline**fest.

#### <a name="syntax"></a>Syntax

```
offline <object>
```

#### <a name="parameter"></a>Parameter

\<Objekt >

Gibt den Objekttyp an, für den dieser Vorgang durchgeführt werden soll. Das \<Objekt >

Type kann **Subsystem**, **Controller**, **Laufwerk**, **LUN**oder **Portal – Entitäten**sein.

### <a name="BKMK_25"></a>Internet

Legt den Status des ausgewählten Objekts des angegebenen Typs auf **Online**fest. Wenn das Objekt " **HBAPORT**" ist, wird der Status der Pfade auf den aktuell ausgewählten HBA **-** Port in "Online" geändert.

#### <a name="syntax"></a>Syntax

```
online <object> 
```

#### <a name="parameter"></a>Parameter

\<Objekt >

Gibt den Objekttyp an, für den dieser Vorgang durchgeführt werden soll. Das \<Objekt >

Typ kann **HBAPORT**, **Subsystem**, **Controller**, **Laufwerk**, **LUN**oder **Portal – Entitäten**sein.

### <a name="BKMK_26"></a>Wiederherstellen

Führt Vorgänge aus, wie z. b. eine erneute Synchronisierung oder Hot sparsam, um die aktuell ausgewählte fehlertolerante LUN zu reparieren. Eine Wiederherstellung kann beispielsweise dazu führen, dass ein Hotspare an einen RAID-Satz gebunden ist, der einen fehlerhaften Datenträger oder eine andere erneute Zuordnung von Datenträgern aufweist.

#### <a name="syntax"></a>Syntax

```
recover <lun>
```

### <a name="BKMK_27"></a>erneut auflisten

Listet die Objekte des angegebenen Typs erneut auf. Wenn Sie den LUN-Erweiterungs Befehl verwenden, müssen Sie den Refresh-Befehl verwenden, um die Datenträger Größe zu aktualisieren, bevor Sie den Befehl "REENUMERATE" verwenden.

#### <a name="syntax"></a>Syntax

```
reenumerate {subsystems | drives}
```

#### <a name="parameters"></a>Parameter

**Subsysteme**

Fragt den Anbieter ab, um alle neuen Subsysteme zu ermitteln, die dem aktuell ausgewählten Anbieter hinzugefügt wurden.

**Master**

Fragt die internen e/a-Busse ab, um neue Laufwerke zu ermitteln, die im derzeit ausgewählten Subsystem hinzugefügt wurden.

### <a name="BKMK_28"></a>erneuten

Aktualisiert die internen Daten für den aktuell ausgewählten Anbieter.

#### <a name="syntax"></a>Syntax

```
refresh provider
```

### <a name="BKMK_29"></a>REM

Wird zum Kommentieren von Skripts verwendet.

#### <a name="syntax"></a>Syntax

```
Rem <comment>
```

### <a name="BKMK_30"></a>aufgeh

Entfernt das angegebene iSCSI-Zielportal aus der aktuell ausgewählten Zielportal Gruppe.

#### <a name="syntax"></a>Syntax

```
remove tpgroup tportal=<tportal> [noerr]
```

#### <a name="parameter"></a>Parameter

**TPGROUP TPORTAL =** \<TPORTAL->

Gibt das zu entfernende iSCSI-Zielportal an.

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden sollen. Dies ist im Skript Modus nützlich.

### <a name="BKMK_31"></a>Stelle

Ersetzt das angegebene Laufwerk durch das aktuell ausgewählte Laufwerk.

#### <a name="syntax"></a>Syntax

```
replace drive=<drive_number>
```

#### <a name="parameter"></a>Parameter

**Laufwerk =**

Gibt den \<drive_number-> für das zu ersetzende Laufwerk an.

#### <a name="remarks"></a>Hinweise

-   Das angegebene Laufwerk ist möglicherweise nicht das aktuell ausgewählte Laufwerk.

### <a name="BKMK_32"></a>Festlegen

Setzt den aktuell ausgewählten Controller oder Port zurück.

#### <a name="syntax"></a>Syntax

```
Reset {controller | port}
```

#### <a name="parameters"></a>Parameter

**ern**

Setzt den Controller zurück.

**Port**

Setzt den Port zurück.

### <a name="BKMK_33"></a>Auswahl

Zeigt das aktuell ausgewählte Objekt an oder ändert es.

#### <a name="syntax"></a>Syntax

```
Select {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup } [<n>]
```

#### <a name="parameters"></a>Parameter

**object**

Gibt den Typ des ausgewählten Objekts an. Beim \<Objekt > Typ kann es sich um **Anbieter**, **Subsystem**, **Controller**, **Laufwerk**oder **LUN**handeln.

**HBAPORT** [\<n >]

Legt den Fokus auf den angegebenen lokalen HBA-Port fest. Wenn kein HBA-Port angegeben wird, zeigt der Befehl den aktuell ausgewählten HBA-Port an (sofern vorhanden). Das Angeben eines ungültigen HBA-Port Indexes führt zu keinem in-Focus-HBA-Port. Wenn Sie einen HBA-Port auswählen, werden alle ausgewählten Initiatoradapter und Initiator-Portale deaktiviert.

**IADAPTER** [\<n >]

Legt den Fokus auf den angegebenen lokalen iSCSI-Initiator-Adapter fest. Wenn kein Initiator-Adapter angegeben ist, zeigt der Befehl den aktuell ausgewählten Initiatoradapter (sofern vorhanden) an. Das Angeben eines ungültigen initiatoradapteradapters führt zu keinem in-Focus-Initiator-Adapter. Wenn Sie einen Initiatoradapter auswählen, werden alle ausgewählten HBA-Ports und Initiator-Portale deaktiviert.

**IPORTAL** [\<n >]

Legt den Fokus auf das angegebene lokale iSCSI-Initiatorportal innerhalb des ausgewählten iSCSI-Initiator-Adapters fest. Wenn kein Initiator-Portal angegeben ist, zeigt der Befehl das aktuell ausgewählte Initiatorportal (sofern vorhanden) an. Wenn Sie einen ungültigen Initiator-Portal Index angeben, wird kein Initiatorportal ausgewählt.

**Anbieter** [\<n >]

Legt den Fokus auf den angegebenen Anbieter fest. Wenn kein Anbieter angegeben ist, zeigt der Befehl den aktuell ausgewählten Anbieter (sofern vorhanden) an. Das Angeben eines ungültigen Anbieter Indexes führt zu keinem in-Focus-Anbieter.

**Subsystem** [\<n >]

Legt den Fokus auf das angegebene Subsystem fest. Wenn kein Subsystem angegeben ist, zeigt der Befehl das Subsystem mit dem Fokus an (sofern vorhanden). Das Angeben eines ungültigen subsystemindexes führt zu keinem in-Focus-Subsystem. Bei Auswahl eines Subsystems wird der zugehörige Anbieter implizit ausgewählt.

**Controller** [\<n >]

Legt den Fokus auf den angegebenen Controller innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Controller angegeben ist, zeigt der Befehl den aktuell ausgewählten Controller an (sofern vorhanden). Das Angeben eines ungültigen Controller Indexes führt nicht zu einem Fokus Controller. Bei Auswahl eines Controllers werden alle ausgewählten Controller Anschlüsse, Laufwerke, LUNs, Ziel Portale, Ziele und Zielportal Gruppen deaktiviert.

**Port** [\<n >]

Legt den Fokus auf den angegebenen Controller Anschluss innerhalb des aktuell ausgewählten Controllers fest. Wenn kein Port angegeben ist, zeigt der Befehl den aktuell ausgewählten Port (sofern vorhanden) an. Das Angeben eines ungültigen Port Indexes führt zu keinem ausgewählten Port.

**Laufwerk** [\<n >]

Legt den Fokus auf das angegebene Laufwerk bzw. die physische Spindel innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Laufwerk angegeben wird, zeigt der Befehl das aktuell ausgewählte Laufwerk an (sofern vorhanden). Das Angeben eines ungültigen Laufwerks Indexes führt zu keinem Fokus Laufwerk. Wenn Sie ein Laufwerk auswählen, werden ausgewählte Controller, Controller Anschlüsse, LUNs, Ziel Portale, Ziele und Zielportal Gruppen deaktiviert.

**LUN** [\<n >]

Legt den Fokus auf die angegebene LUN innerhalb des derzeit ausgewählten Subsystems fest. Wenn keine LUN angegeben ist, zeigt der Befehl die aktuell ausgewählte LUN (sofern vorhanden) an. Wenn Sie einen ungültigen LUN-Index angeben, wird keine LUN ausgewählt. Wenn Sie eine LUN auswählen, werden ausgewählte Controller, Controller Anschlüsse, Laufwerke, Ziel Portale, Ziele und Zielportal Gruppen deaktiviert.

**Portal – Entitäten** [\<n >]

Legt den Fokus auf das angegebene iSCSI-Zielportal innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Zielportal angegeben ist, zeigt der Befehl das aktuell ausgewählte Zielportal (sofern vorhanden) an. Wenn ein ungültiger Zielportal Index angegeben wird, wird kein Zielportal ausgewählt. Wenn Sie ein Zielportal auswählen, werden alle Controller, Controller Anschlüsse, Laufwerke, LUNs, Ziele und Zielportal Gruppen deaktiviert.

**Ziel** [\<n >]

Legt den Fokus auf das angegebene iSCSI-Ziel innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Ziel angegeben ist, zeigt der Befehl das aktuell ausgewählte Ziel an (sofern vorhanden). Wenn ein Ungültiger Zielindex angegeben wird, wird kein Ziel ausgewählt. Wenn Sie ein Ziel auswählen, werden alle Controller, Controller Anschlüsse, Laufwerke, LUNs, Ziel Portale und Zielportal Gruppen deaktiviert.

**TPGROUP** [\<n >]

Legt den Fokus auf die angegebene iSCSI-Zielportal Gruppe innerhalb des aktuell ausgewählten iSCSI-Ziels fest. Wenn keine Zielportal Gruppe angegeben ist, zeigt der Befehl die aktuell ausgewählte Zielportal Gruppe (sofern vorhanden) an. Das Angeben eines ungültigen Zielportal-Gruppen Indexes führt zu keiner Zielportal Gruppe im Fokus.

[\<n >]

Gibt die \<Objekt Nummer an, die > ausgewählt werden soll. Wenn das <object number> angegebene nicht gültig ist, werden alle vorhandenen Auswahlen für Objekte des angegebenen Typs gelöscht. Wenn kein <object number> angegeben wird, wird das aktuelle-Objekt angezeigt.

### <a name="BKMK_34"></a>setflag

Legt das aktuell ausgewählte Laufwerk als Hotspare fest.

#### <a name="syntax"></a>Syntax

```
setflag drive hotspare={true | false}
```

#### <a name="parameters"></a>Parameter

**true**

Wählt das aktuell ausgewählte Laufwerk als Hotspare aus.

**false**

Hebt die Auswahl des aktuell ausgewählten Laufwerks als Hotspare auf.

#### <a name="remarks"></a>Hinweise

Hot Spares können nicht für gewöhnliche LUN-Bindungs Vorgänge verwendet werden. Sie sind nur für die Fehlerbehandlung reserviert. Das Laufwerk darf zurzeit nicht an eine vorhandene LUN gebunden sein.

### <a name="BKMK_shrink"></a>Verkleinern

Verringert die Größe der ausgewählten LUN.

#### <a name="syntax"></a>Syntax

```
shrink lun size=<n> [noerr]
```

#### <a name="parameters"></a>Parameter

**Größe =**

Gibt die gewünschte Menge an Speicherplatz in Megabyte (MB) an, um die Größe der LUN um zu verringern. Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eine der erkannten Suffixe (B, KB, MB, GB, TB und PB) direkt nach der Größe.

**Noerr**

Gibt an, dass alle Fehler, die während der Ausführung dieses Vorgangs auftreten, ignoriert werden. Dies ist im Skript Modus nützlich.

### <a name="BKMK_35"></a>Standby

Ändert den Status der Pfade zum aktuell ausgewählten Port des Hostbus Adapters (HBA) in den Standbymodus.

#### <a name="syntax"></a>Syntax

```
standby hbaport
```

#### <a name="parameters"></a>Parameter

**HBAPORT**

Ändert den Status der Pfade zum aktuell ausgewählten Port des Hostbus Adapters (HBA) in den Standbymodus.

### <a name="BKMK_36"></a>Maskierung

Macht die aktuell ausgewählten LUNs von den angegebenen Hosts aus verfügbar.

#### <a name="syntax"></a>Syntax

```
unmask LUN {all | none | [add] wwn=<hexadecimal_number> [;<hexadecimal_number> [;…]] | [add] initiator=<initiator>[;<initiator>[;…]]} [uninstall]
```

#### <a name="parameters"></a>Parameter

**allen**

Gibt an, dass die LUN von allen Hosts zugänglich gemacht werden soll. Allerdings können Sie die LUN nicht für alle Ziele in einem iSCSI-Subsystem aufheben.

> [!IMPORTANT]
> Sie müssen sich vom Ziel abmelden, bevor Sie den Befehl unmask all ausführen.

**gar**

Gibt an, dass der Zugriff auf die LUN für jeden Host nicht möglich sein soll.

> [!IMPORTANT]
> Sie müssen sich vom Ziel abmelden, bevor Sie den Befehl unmask LUN none ausführen.

**add**

Gibt an, dass die angegebenen Hosts der vorhandenen Liste von Hosts hinzugefügt werden müssen, von denen diese LUN zugänglich ist. Wenn dieser Parameter nicht angegeben wird, ersetzt die Liste der bereitgestellten Hosts die vorhandene Liste der Hosts, von denen diese LUN zugänglich ist.

**WWN =**

Gibt eine Liste von hexadezimalen Zahlen an, die World Wide Names darstellen, von denen aus die LUN oder Hosts zugänglich gemacht werden sollen. Um eine bestimmte Gruppe von Hosts in einem Fibre Channel Subsystem zu maskieren bzw. die Maskierung aufzuheben, können Sie eine durch Semikolons getrennte Liste von WWN für die Ports auf den gewünschten Host Computern eingeben.

**Initiator =**

Gibt eine Liste von iSCSI-Initiatoren an, auf die die aktuell ausgewählte LUN zugegriffen werden soll. Um eine bestimmte Gruppe von Hosts in einem iSCSI-Subsystem zu maskieren bzw. die Maskierung aufzuheben, können Sie eine durch Semikolons getrennte Liste von iSCSI-Initiator-Namen für die Initiatoren auf den gewünschten Host Computern eingeben.

**stalli**

Wenn angegeben, wird der Datenträger, der der LUN auf dem lokalen System zugeordnet ist, deinstalliert, bevor die LUN maskiert wird.

## <a name="scripting-diskraid"></a>Skripterstellung für Diskraid

Auf allen Computern, auf denen Windows Server 2008 oder Windows Server 2003 mit einem zugeordneten VDS-Hardware Anbieter ausgeführt wird, kann ein Skript erstellt werden. Zum Aufrufen eines Diskraid-Skripts geben Sie an der Eingabeaufforderung Folgendes ein:
```
diskraid /s <script.txt>
```
Standardmäßig beendet Diskraid die Verarbeitung von Befehlen und gibt einen Fehlercode zurück, wenn ein Problem im Skript vorliegt. Um die Ausführung des Skripts fortzusetzen und Fehler zu ignorieren, fügen Sie den Noerr-Parameter in den Befehl ein. Dies ermöglicht die Verwendung eines einzelnen Skripts, um alle LUNs in einem Subsystem unabhängig von der Gesamtanzahl der LUNs zu löschen. Nicht alle Befehle unterstützen den Noerr-Parameter. Fehler werden immer bei Befehlssyntax Fehlern zurückgegeben, unabhängig davon, ob Sie den Noerr-Parameter eingefügt haben.

### <a name="diskraid-error-codes"></a>Diskraid-Fehlercodes

|Fehlercode|Fehlerbeschreibung|
|----------|-----------------|
|0|Es ist kein Fehler aufgetreten. Das gesamte Skript wurde ohne Fehler ausgeführt.|
|1|Es ist eine schwerwiegende Ausnahme aufgetreten.|
|2|Die in einer Diskraid-Befehlszeile angegebenen Argumente waren falsch.|
|3|Das angegebene Skript oder die angegebene Ausgabedatei konnte von Diskraid nicht geöffnet werden.|
|4|Einer der Dienste von Diskraid hat einen Fehler zurückgegeben.|
|5|Befehlssyntax Fehler. Fehler beim Skript, weil ein Objekt nicht ordnungsgemäß ausgewählt wurde oder für die Verwendung mit diesem Befehl ungültig war.|

## <a name="example-interactively-view-status-of-subsystem"></a>Beispiel: Interaktiv Status des Subsystems anzeigen

Wenn Sie den Status von Subsystem 0 auf dem Computer anzeigen möchten, geben Sie Folgendes in der Befehlszeile ein:
```
diskraid
```
Drücken Sie die EINGABETASTE. Folgendes wird angezeigt:
```
Microsoft Diskraid version 5.2.xxxx
Copyright (©) 2003 Microsoft Corporation
On computer: COMPUTER_NAME
```
Geben Sie Folgendes an der Diskraid-Eingabeaufforderung ein, um Subsystem 0 auszuwählen:
```
select subsystem 0
```
Drücken Sie die EINGABETASTE. Eine Ausgabe ähnlich der folgenden wird angezeigt:
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
Geben Sie zum Beenden von Diskraid Folgendes an der Diskraid-Eingabeaufforderung ein:
```
exit
```