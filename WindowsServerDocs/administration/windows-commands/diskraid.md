---
title: Diskraid
description: Referenz Artikel für das Befehlszeilen Tool Diskraid, mit dem Sie redundante Arrays unabhängiger (oder kostengünstiger) Speicher Subsysteme (oder kostengünstiger) konfigurieren und verwalten können.
ms.topic: article
ms.assetid: 20aef1e5-7641-47cf-b4eb-cda117f65b6e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d13b8f6a8ffb4f78312a804dd277839021dbd9e1
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87890814"
---
# <a name="diskraid"></a>Diskraid

**Diskraid** ist ein Befehlszeilen Tool, mit dem Sie redundante Arrays unabhängiger (oder kostengünstiger) Speicher Subsysteme (oder kostengünstiger) konfigurieren und verwalten können.

RAID wird in der Regel auf Servern verwendet, um fehlertolerante Festplattensysteme zu standardisieren und zu kategorisieren. RAID-Stufen bieten verschiedene Mischung aus Leistung, Zuverlässigkeit und Kosten. Einige Server stellen drei RAID-Stufen bereit: Ebene 0 (Striping), Ebene 1 (Spiegelung) und Ebene 5 (Striping mit Parität).

Ein Hardware-RAID-Subsystem unterscheidet physisch adressierbare Speichereinheiten mithilfe einer logischen Gerätenummer (Logical Unit Number, LUN) voneinander. Ein LUN-Objekt muss mindestens einen Plex aufweisen und kann über eine beliebige Anzahl zusätzlicher plexes verfügen. Jeder Plex enthält eine Kopie der Daten auf dem LUN-Objekt. Plexes können einem LUN-Objekt hinzugefügt und daraus entfernt werden.

Die meisten Diskraid-Befehle arbeiten an einem bestimmten HBA-Port (Hostbus Adapter), einem Initiatoradapter, einem Initiator-Portal, einem Anbieter, einem Subsystem, einem Controller, einem Port, einem Laufwerk, einer LUN, einem Zielportal, einer Zielgruppe oder Zielportal Verwenden Sie den **Select** -Befehl, um ein Objekt auszuwählen. Das ausgewählte Objekt hat den Fokus. Der Fokus vereinfacht allgemeine Konfigurationsaufgaben, z. b. das Erstellen mehrerer LUNs innerhalb desselben Subsystems.

> [!NOTE]
> Das Diskraid-Befehlszeilen Tool funktioniert nur mit Speicher Subsystemen, die den Dienst für virtuelle Datenträger (Virtual Disk Service, VDS) unterstützen.

## <a name="diskraid-commands"></a>Diskraid-Befehle

Die folgenden Befehle sind innerhalb des Diskraid-Tools verfügbar.

### <a name="add"></a>add

Fügt der aktuell ausgewählten LUN eine vorhandene LUN hinzu oder fügt der aktuell ausgewählten iSCSI-Zielportal Gruppe ein iSCSI-Zielportal hinzu.

#### <a name="syntax"></a>Syntax

```
add plex lun=n [noerr]
add tpgroup tportal=n [noerr]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Plex-LUN =`<n>` | Gibt die LUN-Nummer an, die der aktuell ausgewählten LUN als Plex hinzugefügt werden soll. Vorsicht: alle Daten auf der LUN, die als Plex hinzugefügt werden, werden gelöscht. |
| TPGROUP TPORTAL =`<n>` | Gibt die iSCSI-Zielportal-Nummer an, die der aktuell ausgewählten iSCSI-Zielportal Gruppe hinzugefügt werden soll. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="associate"></a>ierter

Legt die angegebene Liste von Controllerports als aktiv für die aktuell ausgewählte LUN (andere Controller Anschlüsse werden inaktiv) oder fügt die angegebenen Controller Anschlüsse der Liste der vorhandenen aktiven Controller Anschlüsse für die aktuell ausgewählte LUN hinzu oder verknüpft das angegebene iSCSI-Ziel für die aktuell ausgewählte LUN.

#### <a name="syntax"></a>Syntax

```
associate controllers [add] <n>[,<n> [,…]]
associate ports [add] <n-m>[,<n-m>[,…]]
associate targets [add] <n>[,<n> [,…]]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Controller | Fügt der Liste der Controller, die der aktuell ausgewählten LUN zugeordnet sind, hinzu oder ersetzt Sie. Nur mit VDS 1,0-Anbietern verwenden. |
| ports | Fügt die Liste der Controllerports hinzu, die der aktuell ausgewählten LUN zugeordnet sind, oder ersetzt Sie. Nur mit VDS 1,1-Anbietern verwenden. |
| Ziele | Fügt die Liste der iSCSI-Ziele, die der aktuell ausgewählten LUN zugeordnet sind, hinzu oder ersetzt Sie. Nur mit VDS 1,1-Anbietern verwenden. |
| add | **Bei Verwendung von VDS 1,0-Anbietern:** Fügt der vorhandenen Liste von Controllern, die der LUN zugeordnet sind, die angegebenen Controller hinzu. Wenn dieser Parameter nicht angegeben wird, ersetzt die Liste der Controller die vorhandene Liste von Controllern, die dieser LUN zugeordnet sind.<p>**Bei Verwendung von VDS 1,1-Anbietern:** Fügt die angegebenen Controller Anschlüsse der vorhandenen Liste von Controllerports hinzu, die mit der LUN verknüpft sind. Wenn dieser Parameter nicht angegeben wird, ersetzt die Liste der Controllerports die vorhandene Liste der Controllerports, die dieser LUN zugeordnet sind. |
| `<n>[,<n> [, ...]]` | Verwenden Sie mit dem- **Controller** oder dem **Targets** -Parameter. Gibt die Anzahl der Controller oder iSCSI-Ziele an, die auf "aktiv" oder "zuordnen" festgelegt werden |
| `<n-m>[,<n-m>[,…]]` | Verwenden Sie mit dem **Ports** -Parameter. Gibt die Controllerports an, die mithilfe einer Controller Nummer (*n*) und eines Portnummern Paars (*m*) aktiv festgelegt werden sollen. |

#### <a name="example"></a>Beispiel

So ordnen Sie Ports zu und fügen Sie einer LUN hinzu, die einen VDS 1,1-Anbieter verwendet:

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

### <a name="automagic"></a>automagisch

Legt Flags fest, die den Anbietern Hinweise zum Konfigurieren einer LUN zur Verfügung stellt, oder löscht sie. Der **automagingvorgang** wird ohne Parameter verwendet und zeigt eine Liste von Flags an.

#### <a name="syntax"></a>Syntax

```
automagic {set | clear | apply} all <flag=value> [<flag=value> [...]]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| set | Legt die angegebenen Flags auf die angegebenen Werte fest. |
| clear | Löscht die angegebenen Flags. Mit dem **all** -Schlüsselwort werden alle automagflags gelöscht. |
| apply | Wendet die aktuellen Flags auf die ausgewählte LUN an. |
| `<flag>` | Flags werden aus drei Buchstaben bestehenden Akronymen identifiziert, einschließlich:<ul><li>**F** : schnelle Wiederherstellung von Abstürzen erforderlich</li><li>**FTL** -fehlertolerante</li><li>**MSR** -überwiegend Lesevorgänge</li><li>**MXD** -maximale Anzahl von Laufwerken</li><li>**MXS** -maximale Größe erwartet</li><li>**Ora** -optimale Lese Ausrichtung</li><li>**ORS** -optimale Lese Größe</li><li>**OSR** -für sequenzielle Lesevorgänge optimieren</li><li>**OSW** -Optimierung für sequenzielle Schreibvorgänge</li><li> **OWA** -optimale Schreib Ausrichtung</li><li>**OWS** -optimale Schreibgröße</li><li>**RBP** -Priorität neu erstellen</li><li>**RBV** -Read-Back-Überprüfung aktiviert</li><li>**RMP** -remap aktiviert</li><li>**STS** -Strip-Größe</li><li>Zwischenspeichern von **WTC** -Schreibzugriff aktiviert</li><li>**Ynk** -Wechsel</li></ul> |

### <a name="break"></a>break

Entfernt den Plex aus der aktuell ausgewählten LUN. Der Plex und die darin enthaltenen Daten werden nicht beibehalten, und die Laufwerks Blöcke können freigegeben werden.

> [!CAUTION]
> Sie müssen zuerst eine gespiegelte LUN auswählen, bevor Sie diesen Befehl verwenden. Alle Daten auf dem Plex werden gelöscht. Es ist nicht sichergestellt, dass alle Daten, die in der ursprünglichen LUN enthalten sind, einheitlich sind.

#### <a name="syntax"></a>Syntax

```
break plex=<plex_number> [noerr]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Plex | Gibt die Nummer des zu entfernenden Plex an. Der Plex und die darin enthaltenen Daten werden nicht beibehalten, und die von diesem Plex verwendeten Ressourcen werden freigegeben. Es ist nicht garantiert, dass die in der LUN enthaltenen Daten konsistent sind. Wenn Sie diesen Plex beibehalten möchten, verwenden Sie den Volumeschattenkopie-Dienst (VSS). |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="chap"></a>CHAP

Legt den gemeinsamen geheimen Schlüssel des Challenge Handshake Authentication-Protokolls (CHAP) so fest, dass iSCSI-Initiatoren und iSCSI-Ziele miteinander kommunizieren können.

#### <a name="syntax"></a>Syntax

```
chap initiator set secret=[<secret>] [target=<target>]
chap initiator remember secret=[<secret>] target=<target>
chap target set secret=[<secret>] [initiator=<initiatorname>]
chap target remember secret=[<secret>] initiator=<initiatorname>
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| initiatorsatz | Legt den gemeinsamen geheimen Schlüssel im lokalen iSCSI-Initiatordienst für die gegenseitige CHAP-Authentifizierung fest, wenn der Initiator das Ziel authentifiziert. |
| Erinnerung an Initiator | Kommuniziert das CHAP-Geheimnis eines iSCSI-Ziels mit dem lokalen iSCSI-Initiatordienst, sodass der Initiatordienst das Geheimnis verwenden kann, um sich bei der CHAP-Authentifizierung beim Ziel zu authentifizieren. |
| Zielsatz | Legt den gemeinsamen geheimen Schlüssel im aktuell ausgewählten iSCSI-Ziel für die CHAP-Authentifizierung fest, wenn der Initiator vom Ziel authentifiziert wird. |
| Ziel speichern | Kommuniziert das CHAP-Geheimnis eines iSCSI-Initiators mit dem aktuellen iSCSI-Ziel im Fokus, sodass das Ziel das Geheimnis verwenden kann, um sich bei der wechselseitigen CHAP-Authentifizierung beim Initiator zu authentifizieren. |
| secret | Gibt den zu verwendenden geheimen Schlüssel an. Wenn der Eintrag leer ist, wird der geheime Schlüssel gelöscht. |
| target | Gibt ein Ziel im aktuell ausgewählten Subsystem an, das dem geheimen Schlüssel zugeordnet werden soll. Dies ist optional, wenn Sie einen geheimen Schlüssel für den Initiator festlegen und ihn verlassen, gibt an, dass der geheime Schlüssel für alle Ziele verwendet wird, die noch nicht über ein zugeordnetes Geheimnis verfügen. |
| Initiatorname | Gibt einen iSCSI-Initiatornamen an, der dem geheimen Schlüssel zugeordnet werden soll. Dies ist optional, wenn ein Geheimnis für ein Ziel festgelegt wird und das Geheimnis nicht angezeigt wird, dass das Geheimnis für alle Initiatoren verwendet wird, die noch nicht über einen zugehörigen geheimen Schlüssel verfügen. |

### <a name="create"></a>create

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

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Einfach | Erstellt eine einfache LUN. |
| Bereichsstreifen | Erstellt eine stripesetlun. |
| Razzien | Erstellt eine stripesetlun mit Parität. |
| mirror | Erstellt eine gespiegelte LUN. |
| automagisch | Erstellt eine LUN mithilfe der zurzeit gültigen *automagandeutungen* . Weitere Informationen finden Sie unter dem Unterbefehl **AUTOMAGIC** in diesem Artikel. |
| Größe = | Gibt die Gesamtgröße der LUN in Megabyte an. Entweder der **size**=-Parameter oder der **Drives**=-Parameter muss angegeben werden. Sie können auch gleichzeitig verwendet werden. Wenn der **size =** -Parameter nicht angegeben wird, ist die LUN, die für alle angegebenen Laufwerke zulässig ist, die größtmögliche Größe.<p>Ein Anbieter erstellt in der Regel eine LUN, die mindestens so groß wie die angeforderte Größe ist, aber der Anbieter muss in einigen Fällen möglicherweise auf die nächst größere Größe aufrunden. Wenn z. b. Size als. 99 GB angegeben wird und der Anbieter nur GB Datenträger Blöcke zuordnen kann, beträgt die resultierende LUN 1 GB. Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:<ul><li>**B** -Byte</li><li>**KB** -KB</li><li>**MB** -Megabyte</li><li>**GB** -Gigabyte</li><li>**TB** -Terabyte</li><li>**PB** -Peer tabyte.</li></ul> |
| Laufwerke = | Gibt die *drive_number* für die Laufwerke an, die zum Erstellen einer LUN verwendet werden sollen. Entweder der **size**=-Parameter oder der **Drives**=-Parameter muss angegeben werden. Sie können auch gleichzeitig verwendet werden. Wenn der **size =** -Parameter nicht angegeben wird, ist die LUN, die für alle angegebenen Laufwerke zulässig ist, die größtmögliche Größe. Wenn der **size =** -Parameter angegeben wird, wählen die Anbieter Laufwerke aus der angegebenen Laufwerks Liste aus, um die LUN zu erstellen. Anbieter versuchen, die Laufwerke nach Möglichkeit in der angegebenen Reihenfolge zu verwenden. |
| stripesize = | Gibt die Größe für eine *Stripe* -oder *RAID* -LUN in Megabyte an. Die stripesize kann nicht geändert werden, nachdem die LUN erstellt wurde. Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:<ul><li>**B** -Byte</li><li>**KB** -KB</li><li>**MB** -Megabyte</li><li>**GB** -Gigabyte</li><li>**TB** -Terabyte</li><li>**PB** -Peer tabyte.</li></ul> |
| target | Erstellt ein neues iSCSI-Ziel für das derzeit ausgewählte Subsystem. |
| name | Gibt den anzeigen Amen für das Ziel an. |
| iscsiname | Gibt den iSCSI-Namen für das Ziel an und kann weggelassen werden, damit der Anbieter einen Namen generiert. |
| TPGROUP | Erstellt eine neue iSCSI-Zielportal Gruppe für das aktuell ausgewählte Ziel. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="delete"></a>delete

Löscht die derzeit ausgewählte LUN, das iSCSI-Ziel (sofern keine LUNs mit dem iSCSI-Ziel verknüpft sind) oder die iSCSI-Zielportal Gruppe.

#### <a name="syntax"></a>Syntax

```
delete lun [uninstall] [noerr]
delete target [noerr]
delete tpgroup [noerr]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| lun | Löscht die derzeit ausgewählte LUN und alle darin ausgewählten Daten. |
| uninstall | Gibt an, dass der Datenträger auf dem lokalen System, der der LUN zugeordnet ist, bereinigt wird, bevor die LUN gelöscht wird. |
| target | Löscht das aktuell ausgewählte iSCSI-Ziel, wenn dem Ziel keine LUNs zugeordnet sind. |
| TPGROUP | Löscht die derzeit ausgewählte iSCSI-Zielportal Gruppe. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="detail"></a>Detail

Zeigt ausführliche Informationen über das aktuell ausgewählte Objekt des angegebenen Typs an.

#### <a name="syntax"></a>Syntax

```
detail {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup} [verbose]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| HBAPORT | Listet ausführliche Informationen zum aktuell ausgewählten HBA-Port (Hostbus Adapter) auf. |
| IADAPTER | Listet ausführliche Informationen zum aktuell ausgewählten iSCSI-Initiator-Adapter auf. |
| IPORTAL | Listet ausführliche Informationen über das aktuell ausgewählte iSCSI-Initiator-Portal auf. |
| Provider | Listet ausführliche Informationen über den aktuell ausgewählten Anbieter auf. |
| subsystem | Listet ausführliche Informationen über das aktuell ausgewählte Subsystem auf. |
| Controller | Listet ausführliche Informationen über den aktuell ausgewählten Controller auf. |
| port | Listet ausführliche Informationen zum aktuell ausgewählten Controllerport auf. |
| Laufwerk | Listet ausführliche Informationen über das aktuell ausgewählte Laufwerk, einschließlich der ersetzenden LUNs, auf. |
| lun | Listet ausführliche Informationen über die derzeit ausgewählte LUN, einschließlich der Mitwirkenden Laufwerke. Die Ausgabe unterscheidet sich geringfügig, je nachdem, ob die LUN Teil eines Fibre Channel-oder iSCSI-Subsystems ist. Wenn die Liste der nicht maskierten Hosts nur ein Sternchen enthält, bedeutet dies, dass die LUN für alle Hosts unmaskiert ist. |
| Portal – Entitäten | Listet ausführliche Informationen über das aktuell ausgewählte iSCSI-Zielportal auf. |
| target | Listet ausführliche Informationen über das aktuell ausgewählte iSCSI-Ziel auf. |
| TPGROUP | Listet ausführliche Informationen zur aktuell ausgewählten iSCSI-Zielportal Gruppe auf. |
| Ausführlich | Nur für die Verwendung mit dem LUN-Parameter. Listet zusätzliche Informationen, einschließlich der zugehörigen plexes, auf. |

### <a name="dissociate"></a>Trennen

Legt die angegebene Liste von Controllerports für die aktuell ausgewählte LUN als inaktiv fest (andere Controller Anschlüsse sind nicht betroffen) oder trennt die angegebene Liste von iSCSI-Zielen für die aktuell ausgewählte LUN.

#### <a name="syntax"></a>Syntax

```
dissociate controllers <n> [,<n> [,...]]
dissociate ports <n-m>[,<n-m>[,…]]
dissociate targets <n> [,<n> [,…]]
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Controller | Entfernt Controller aus der Liste der Controller, die der aktuell ausgewählten LUN zugeordnet sind. Nur mit VDS 1,0-Anbietern verwenden. |
| ports | Entfernt Controller Anschlüsse aus der Liste der Controllerports, die der aktuell ausgewählten LUN zugeordnet sind. Nur mit VDS 1,1-Anbietern verwenden. |
| Ziele | Entfernt Ziele aus der Liste der iSCSI-Ziele, die der aktuell ausgewählten LUN zugeordnet sind. Nur mit VDS 1,1-Anbietern verwenden. |
| `<n> [,<n> [,…]]` | Zur Verwendung mit dem **Controller** oder dem **Targets** -Parameter. Gibt die Anzahl der Controller oder iSCSI-Ziele an, die als inaktiv festgelegt oder getrennt werden sollen. |
| `<n-m>[,<n-m>[,…]]` | Zur Verwendung mit dem **Ports** -Parameter. Gibt die Controller Anschlüsse an, die als inaktiv festgelegt werden sollen, indem eine Controller Nummer (*n*) und ein Portnummern Paar (*m*) verwendet werden. |

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

### <a name="exit"></a>exit

Beendet Diskraid.

#### <a name="syntax"></a>Syntax

```
exit
```

### <a name="extend"></a>extend

Erweitert die aktuell ausgewählte LUN, indem Sektoren am Ende der LUN hinzugefügt werden. Nicht alle Anbieter unterstützen das Erweitern von LUNs. Erweitert keine Volumes oder Dateisysteme, die auf der LUN enthalten sind. Nachdem Sie die LUN erweitert haben, sollten Sie die zugeordneten Strukturen auf dem Datenträger mithilfe des Befehls **DiskPart Extend** erweitern.

#### <a name="syntax"></a>Syntax

```
extend lun [size=<LUN_size>] [drives=<drive_number>, [<drive_number>, ...]] [noerr]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| size | Gibt die Größe in Megabyte an, um die LUN zu erweitern. Es muss entweder die *Größe* oder der- `<drive>` Parameter angegeben werden. Sie können auch gleichzeitig verwendet werden. Wenn der **size =** -Parameter nicht angegeben wird, wird die LUN um die größtmögliche Größe erweitert, die von allen angegebenen Laufwerken zugelassen wird. Wenn der **size =** -Parameter angegeben wird, wählen Anbieter Laufwerke aus der Liste aus, die durch den **Laufwerke =** -Parameter angegeben wird, um die LUN zu erstellen. Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:<ul><li>**B** -Byte</li><li>**KB** -KB</li><li>**MB** -Megabyte</li><li>**GB** -Gigabyte</li><li>**TB** -Terabyte</li><li>**PB** -Peer tabyte.</li></ul> |
| Laufwerke = | Gibt den `<drive_number>` für die Laufwerke an, die beim Erstellen einer LUN verwendet werden sollen. Es muss entweder die *Größe* oder der- `<drive>` Parameter angegeben werden. Sie können auch gleichzeitig verwendet werden. Wenn der **size =** -Parameter nicht angegeben wird, ist die LUN, die für alle angegebenen Laufwerke zulässig ist, die größtmögliche Größe. Anbieter verwenden die Laufwerke in der angegebenen Reihenfolge, wenn möglich. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="flushcache"></a>flushcache

Löscht den Cache auf dem aktuell ausgewählten Controller.

#### <a name="syntax"></a>Syntax

```
flushcache controller
```

### <a name="help"></a>help

Zeigt eine Liste aller Diskraid-Befehle an.

#### <a name="syntax"></a>Syntax

```
help
```

### <a name="importtarget"></a>IMPORTTARGET

Ruft das VSS-Import Ziel (Current Volumeschattenkopie-Dienst) ab, das für das aktuell ausgewählte Subsystem festgelegt ist, oder legt dieses fest.

#### <a name="syntax"></a>Syntax

```
importtarget subsystem [set target]
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Ziel festlegen | Bei Angabe dieser Option wird das aktuell ausgewählte Ziel auf das VSS-Import Ziel für das aktuell ausgewählte Subsystem festgelegt. Wenn nicht angegeben, ruft der Befehl das aktuelle VSS-Import Ziel ab, das für das aktuell ausgewählte Subsystem festgelegt ist. |

### <a name="initiator"></a>initiator

Ruft Informationen zum lokalen iSCSI-Initiator ab.

#### <a name="syntax"></a>Syntax

```
initiator
```

### <a name="invalidatecache"></a>INVALIDATECACHE

Erklärt den Cache auf dem aktuell ausgewählten Controller für ungültig.

#### <a name="syntax"></a>Syntax

```
invalidatecache controller
```

### <a name="lbpolicy"></a>lbpolicy

Legt die Richtlinie für den Lastenausgleich für die aktuell ausgewählte LUN fest.

#### <a name="syntax"></a>Syntax

```
lbpolicy set lun type=<type> [paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]]
lbpolicy set lun paths=<path>-{primary | <weight>}[,<path>-{primary | <weight>}[,…]]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| type | Gibt die Richtlinie für den Lastenausgleich an. Wenn der Typ nicht angegeben wird, muss der **path** -Parameter angegeben werden. Als Type kann eines der folgenden Elemente verwendet werden:<ul><li>**Failover** : verwendet einen primären Pfad mit anderen Pfaden, die Sicherungs Pfade sind.</li><li>**Roundrobin** : verwendet alle Pfade im Roundrobin-Verfahren, wobei jeder Pfad nacheinander ausprobiert wird.</li><li>**Subnetztroundrobin** : verwendet alle primären Pfade im Roundrobin-Verfahren. Sicherungs Pfade werden nur verwendet, wenn alle primären Pfade fehlschlagen.</li><li>**Dynlqd** : verwendet den Pfad mit der geringsten Anzahl aktiver Anforderungen.<li><li>**Gewichtet** : verwendet den Pfad mit dem geringsten Gewicht (jedem Pfad muss eine Gewichtung zugewiesen werden).</li><li>**Leastblocks** : verwendet den Pfad mit den geringsten Blöcken.</li><li>**Vendorspecific** : verwendet eine herstellerspezifische Richtlinie.</li></ul> |
| path | Gibt an, ob ein Pfad **primär** ist oder über einen bestimmten verfügt `<weight>` . Alle Pfade, die nicht angegeben sind, werden implizit als Sicherung festgelegt. Alle aufgelisteten Pfade müssen einer der aktuell ausgewählten Pfade der LUN sein. |

### <a name="list"></a>list

Zeigt eine Liste von Objekten des angegebenen Typs an.

#### <a name="syntax"></a>Syntax

```
list {hbaports | iadapters | iportals | providers | subsystems | controllers | ports | drives | LUNs | tportals | targets | tpgroups}
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| hbapbrüche | Listet zusammenfassende Informationen zu allen HBA-Ports auf, die VDS bekannt sind. Der aktuell ausgewählte HBA-Port wird durch ein Sternchen (*) markiert. |
| IADAPTERS | Listet Zusammenfassungs Informationen zu allen iSCSI-Initiator-Adaptern, die VDS bekannt sind. Der aktuell ausgewählte Initiatoradapter wird durch ein Sternchen (*) markiert. |
| iportale | Listet zusammenfassende Informationen zu allen iSCSI-Initiator-Portalen im aktuell ausgewählten Initiator-Adapter auf. Das aktuell ausgewählte Initiatorportal wird durch ein Sternchen (*) markiert. |
| providers | Listet zusammenfassende Informationen zu den einzelnen Anbietern von VDS auf. Der aktuell ausgewählte Anbieter wird durch ein Sternchen (*) markiert. |
| Subsysteme | Listet zusammenfassende Informationen zu den einzelnen Subsystemen im System auf. Das aktuell ausgewählte Subsystem wird durch ein Sternchen (*) markiert. |
| Controller | Listet Zusammenfassungs Informationen zu jedem Controller im aktuell ausgewählten Subsystem auf. Der aktuell ausgewählte Controller wird durch ein Sternchen (*) markiert. |
| ports | Listet Zusammenfassungs Informationen zu jedem Controller Anschluss im aktuell ausgewählten Controller auf. Der aktuell ausgewählte Port wird durch ein Sternchen (*) markiert. |
| Laufwerke | Listet Zusammenfassungs Informationen zu jedem Laufwerk im aktuell ausgewählten Subsystem auf. Das aktuell ausgewählte Laufwerk wird durch ein Sternchen (*) markiert. |
| LUNs | Listet zusammenfassende Informationen zu den einzelnen LUN im aktuell ausgewählten Subsystem auf. Die aktuell ausgewählte LUN wird durch ein Sternchen (*) markiert. |
| tportale | Listet zusammenfassende Informationen zu allen iSCSI-Ziel Portalen im aktuell ausgewählten Subsystem auf. Das aktuell ausgewählte Zielportal wird durch ein Sternchen (*) markiert. |
| Ziele | Listet zusammenfassende Informationen zu allen iSCSI-Zielen im aktuell ausgewählten Subsystem auf. Das aktuell ausgewählte Ziel ist durch ein Sternchen (*) markiert. |
| TPGROUPS | Listet Zusammenfassungs Informationen zu allen iSCSI-Zielportal Gruppen im aktuell ausgewählten Ziel auf. Die aktuell ausgewählte Portal Gruppe wird durch ein Sternchen (*) markiert. |

### <a name="login"></a>login

Protokolliert den angegebenen iSCSI-Initiator-Adapter im aktuell ausgewählten iSCSI-Ziel.

#### <a name="syntax"></a>Syntax

```
login target iadapter=<iadapter> [type={manual | persistent | boot}] [chap={none | oneway | mutual}] [iportal=<iportal>] [tportal=<tportal>] [<flag> [<flag> […]]]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| type | Gibt den Typ des auszuführenden Anmelde namens an: **manuell** oder **persistent**. Wenn keine Angabe erfolgt, wird ein manueller Anmelde Name ausgeführt. |
| manual | Manuelles anmelden. Es gibt auch eine **Start** Option, die für die zukünftige Entwicklung vorgesehen ist und derzeit nicht verwendet wird. |
| hartnäck | Verwenden Sie beim Neustart des Computers automatisch denselben Anmelde Namen. |
| CHAP | Gibt den Typ der zu verwendenden CHAP-Authentifizierung an: **None**, **OneWay** CHAP oder **gegenseitiges** CHAP. Wenn keine Angabe erfolgt, wird keine Authentifizierung verwendet. |
| Portal – Entitäten | Gibt ein optionales Zielportal im aktuell ausgewählten Subsystem an, das für die Anmeldung verwendet werden soll. |
| IPORTAL | Gibt ein optionales Initiatorportal im angegebenen Initiator-Adapter an, das für die Anmeldung verwendet werden soll. |
| `<flag>` | Identifiziert durch aus drei Buchstaben bestehende Akronyme:<ul><li>**IPS** : IPSec erforderlich</li><li>**EMP** -Multipfad aktivieren</li><li>**EHD** -Header Digest aktivieren</li><li>**EDD** -Daten Digest aktivieren</li></ul> |

### <a name="logout"></a>logout

Protokolliert den angegebenen iSCSI-Initiator-Adapter aus dem aktuell ausgewählten iSCSI-Ziel.

#### <a name="syntax"></a>Syntax

```
logout target iadapter= <iadapter>
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| IADAPTER | Gibt den Initiator-Adapter mit einer Anmelde Sitzung an, von der abgemeldet werden soll. |

### <a name="maintenance"></a>Wartung

Führt Wartungsvorgänge für das aktuell ausgewählte Objekt des angegebenen Typs aus.

#### <a name="syntax"></a>Syntax

```
maintenance <object operation> [count=<iteration>]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<object>` | Gibt den Objekttyp an, für den der Vorgang durchgeführt werden soll. Der *Objekttyp* kann ein **Subsystem**, ein **Controller**, ein **Port, ein Laufwerk** oder eine **LUN**sein. |
| `<operation>` | Gibt den auszuführenden Wartungs Vorgang an. Der *operation* Vorgangstyp kann **SpinUp**, **Spindown**, **Blink**, **Signal Tons** oder **Ping**sein. Es muss ein *Vorgang* angegeben werden. |
| Anzahl = | Gibt an, wie oft der *Vorgang*wiederholt werden soll. Dies wird in der Regel mit **Blink**, **Signal Tons**oder **Ping**verwendet. |

### <a name="name"></a>name

Legt den anzeigen amen des derzeit ausgewählten Subsystems, LUN oder iSCSI-Ziels auf den angegebenen Namen fest.

#### <a name="syntax"></a>Syntax

```
name {subsystem | lun | target} [<name>]
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<name>` | Gibt einen Namen für das Subsystem, die LUN oder das Ziel an. Der Name muss eine Länge von weniger als 64 Zeichen aufweisen. Wenn kein Name angegeben wird, wird der vorhandene Name (sofern vorhanden) gelöscht. |

### <a name="offline"></a>Offline

Legt den Zustand des aktuell ausgewählten Objekts des angegebenen Typs auf **Offline**fest.

#### <a name="syntax"></a>Syntax

```
offline <object>
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<object>` | Gibt den Objekttyp an, für den dieser Vorgang durchgeführt werden soll. Der Typ kann sein: **Subsystem**, **Controller**, **Laufwerk**, **LUN**oder **Portal – Entitäten**. |

### <a name="online"></a>online

Legt den Status des ausgewählten Objekts des angegebenen Typs auf **Online**fest. Wenn das Objekt " **HBAPORT**" ist, wird der Status der Pfade auf den aktuell ausgewählten HBA **-** Port in "Online" geändert.

#### <a name="syntax"></a>Syntax

```
online <object>
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<object>` | Gibt den Objekttyp an, für den dieser Vorgang durchgeführt werden soll. Der Typ kann lauten: **HBAPORT**, **Subsystem**, **Controller**, **Laufwerk**, **LUN**oder **Portal – Entitäten**. |

### <a name="recover"></a>recover

Führt Vorgänge aus, wie z. b. eine erneute Synchronisierung oder Hot sparsam, um die aktuell ausgewählte fehlertolerante LUN zu reparieren. Eine Wiederherstellung kann beispielsweise dazu führen, dass ein Hotspare an einen RAID-Satz gebunden ist, der einen fehlerhaften Datenträger oder eine andere erneute Zuordnung von Datenträgern aufweist.

#### <a name="syntax"></a>Syntax

```
recover <lun>
```

### <a name="reenumerate"></a>erneut auflisten

Listet die Objekte des angegebenen Typs erneut auf. Wenn Sie den LUN-Erweiterungs Befehl verwenden, müssen Sie den Refresh-Befehl verwenden, um die Datenträger Größe zu aktualisieren, bevor Sie den Befehl "REENUMERATE" verwenden.

#### <a name="syntax"></a>Syntax

```
reenumerate {subsystems | drives}
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Subsysteme | Fragt den Anbieter ab, um alle neuen Subsysteme zu ermitteln, die dem aktuell ausgewählten Anbieter hinzugefügt wurden. |
| Laufwerke | Fragt die internen e/a-Busse ab, um neue Laufwerke zu ermitteln, die im derzeit ausgewählten Subsystem hinzugefügt wurden. |

### <a name="refresh"></a>Aktualisieren

Aktualisiert die internen Daten für den aktuell ausgewählten Anbieter.

#### <a name="syntax"></a>Syntax

```
refresh provider
```

### <a name="rem"></a>rem

Wird zum Kommentieren von Skripts verwendet.

#### <a name="syntax"></a>Syntax

```
Rem <comment>
```

### <a name="remove"></a>remove

Entfernt das angegebene iSCSI-Zielportal aus der aktuell ausgewählten Zielportal Gruppe.

#### <a name="syntax"></a>Syntax

```
remove tpgroup tportal=<tportal> [noerr]
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| TPGROUP TPORTAL =`<tportal>` | Gibt das zu entfernende iSCSI-Zielportal an. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="replace"></a>replace

Ersetzt das angegebene Laufwerk durch das aktuell ausgewählte Laufwerk. Das angegebene Laufwerk ist möglicherweise nicht das aktuell ausgewählte Laufwerk.

#### <a name="syntax"></a>Syntax

```
replace drive=<drive_number>
```

##### <a name="parameter"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Laufwerk = | Gibt den `<drive_number>` für das zu ersetzende Laufwerk an. |

### <a name="reset"></a>reset

Setzt den aktuell ausgewählten Controller oder Port zurück.

#### <a name="syntax"></a>Syntax

```
reset {controller | port}
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Controller | Setzt den Controller zurück. |
| port | Setzt den Port zurück. |

### <a name="select"></a>select

Zeigt das aktuell ausgewählte Objekt an oder ändert es.

#### <a name="syntax"></a>Syntax

```
select {hbaport | iadapter | iportal | provider | subsystem | controller | port | drive | lun | tportal | target | tpgroup } [<n>]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| Objekt (object) | Gibt den Typ des ausgewählten Objekts an, einschließlich **Anbieter**, **Subsystem**, **Controller**, **Laufwerk**oder **LUN**. |
| HBAPORT`[<n>]` | Legt den Fokus auf den angegebenen lokalen HBA-Port fest. Wenn kein HBA-Port angegeben wird, zeigt der Befehl den aktuell ausgewählten HBA-Port an (sofern vorhanden). Das Angeben eines ungültigen HBA-Port Indexes führt zu keinem in-Focus-HBA-Port. Wenn Sie einen HBA-Port auswählen, werden alle ausgewählten Initiatoradapter und Initiator-Portale deaktiviert. |
| IADAPTER`[<n>]` | Legt den Fokus auf den angegebenen lokalen iSCSI-Initiator-Adapter fest. Wenn kein Initiator-Adapter angegeben ist, zeigt der Befehl den aktuell ausgewählten Initiatoradapter (sofern vorhanden) an. Das Angeben eines ungültigen initiatoradapteradapters führt zu keinem in-Focus-Initiator-Adapter. Wenn Sie einen Initiatoradapter auswählen, werden alle ausgewählten HBA-Ports und Initiator-Portale deaktiviert. |
| IPORTAL`[<n>]` | Legt den Fokus auf das angegebene lokale iSCSI-Initiatorportal innerhalb des ausgewählten iSCSI-Initiator-Adapters fest. Wenn kein Initiator-Portal angegeben ist, zeigt der Befehl das aktuell ausgewählte Initiatorportal (sofern vorhanden) an. Wenn Sie einen ungültigen Initiator-Portal Index angeben, wird kein Initiatorportal ausgewählt. |
| ab`[<n>]` | Legt den Fokus auf den angegebenen Anbieter fest. Wenn kein Anbieter angegeben ist, zeigt der Befehl den aktuell ausgewählten Anbieter (sofern vorhanden) an. Das Angeben eines ungültigen Anbieter Indexes führt zu keinem in-Focus-Anbieter. |
| System`[<n>]` | Legt den Fokus auf das angegebene Subsystem fest. Wenn kein Subsystem angegeben ist, zeigt der Befehl das Subsystem mit dem Fokus an (sofern vorhanden). Das Angeben eines ungültigen subsystemindexes führt zu keinem in-Focus-Subsystem. Bei Auswahl eines Subsystems wird der zugehörige Anbieter implizit ausgewählt. |
| ern`[<n>]` | Legt den Fokus auf den angegebenen Controller innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Controller angegeben ist, zeigt der Befehl den aktuell ausgewählten Controller an (sofern vorhanden). Das Angeben eines ungültigen Controller Indexes führt nicht zu einem Fokus Controller. Bei Auswahl eines Controllers werden alle ausgewählten Controller Anschlüsse, Laufwerke, LUNs, Ziel Portale, Ziele und Zielportal Gruppen deaktiviert. |
| Port`[<n>]` | Legt den Fokus auf den angegebenen Controller Anschluss innerhalb des aktuell ausgewählten Controllers fest. Wenn kein Port angegeben ist, zeigt der Befehl den aktuell ausgewählten Port (sofern vorhanden) an. Das Angeben eines ungültigen Port Indexes führt zu keinem ausgewählten Port. |
| Antrie`[<n>]` | Legt den Fokus auf das angegebene Laufwerk bzw. die physische Spindel innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Laufwerk angegeben wird, zeigt der Befehl das aktuell ausgewählte Laufwerk an (sofern vorhanden). Das Angeben eines ungültigen Laufwerks Indexes führt zu keinem Fokus Laufwerk. Wenn Sie ein Laufwerk auswählen, werden ausgewählte Controller, Controller Anschlüsse, LUNs, Ziel Portale, Ziele und Zielportal Gruppen deaktiviert. |
| LUN`[<n>]` | Legt den Fokus auf die angegebene LUN innerhalb des derzeit ausgewählten Subsystems fest. Wenn keine LUN angegeben ist, zeigt der Befehl die aktuell ausgewählte LUN (sofern vorhanden) an. Wenn Sie einen ungültigen LUN-Index angeben, wird keine LUN ausgewählt. Wenn Sie eine LUN auswählen, werden ausgewählte Controller, Controller Anschlüsse, Laufwerke, Ziel Portale, Ziele und Zielportal Gruppen deaktiviert. |
| Portal – Entitäten`[<n>]` | Legt den Fokus auf das angegebene iSCSI-Zielportal innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Zielportal angegeben ist, zeigt der Befehl das aktuell ausgewählte Zielportal (sofern vorhanden) an. Wenn ein ungültiger Zielportal Index angegeben wird, wird kein Zielportal ausgewählt. Wenn Sie ein Zielportal auswählen, werden alle Controller, Controller Anschlüsse, Laufwerke, LUNs, Ziele und Zielportal Gruppen deaktiviert. |
| Spar`[<n>]` | Legt den Fokus auf das angegebene iSCSI-Ziel innerhalb des derzeit ausgewählten Subsystems fest. Wenn kein Ziel angegeben ist, zeigt der Befehl das aktuell ausgewählte Ziel an (sofern vorhanden). Wenn ein Ungültiger Zielindex angegeben wird, wird kein Ziel ausgewählt. Wenn Sie ein Ziel auswählen, werden alle Controller, Controller Anschlüsse, Laufwerke, LUNs, Ziel Portale und Zielportal Gruppen deaktiviert. |
| TPGROUP`[<n>]` | Legt den Fokus auf die angegebene iSCSI-Zielportal Gruppe innerhalb des aktuell ausgewählten iSCSI-Ziels fest. Wenn keine Zielportal Gruppe angegeben ist, zeigt der Befehl die aktuell ausgewählte Zielportal Gruppe (sofern vorhanden) an. Das Angeben eines ungültigen Zielportal-Gruppen Indexes führt zu keiner Zielportal Gruppe im Fokus. |
|`[<n>]` | Gibt den `<object number>` auszuwählen. Wenn das `<object number>` angegebene nicht gültig ist, werden alle vorhandenen Auswahlen für Objekte des angegebenen Typs gelöscht. Wenn kein `<object number>` angegeben wird, wird das aktuelle-Objekt angezeigt.

### <a name="setflag"></a>setflag

Legt das aktuell ausgewählte Laufwerk als Hotspare fest. Hot Spares können nicht für normale LUN-Bindungs Vorgänge verwendet werden. Sie sind nur für die Fehlerbehandlung reserviert. Das Laufwerk darf zurzeit nicht an eine vorhandene LUN gebunden sein.

#### <a name="syntax"></a>Syntax

```
setflag drive hotspare={true | false}
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| true | Wählt das aktuell ausgewählte Laufwerk als Hotspare aus. |
| false | Hebt die Auswahl des aktuell ausgewählten Laufwerks als Hotspare auf. |

### <a name="shrink"></a>shrink

Verringert die Größe der ausgewählten LUN.

#### <a name="syntax"></a>Syntax

```
shrink lun size=<n> [noerr]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| size | Gibt die gewünschte Menge an Speicherplatz in Megabyte (MB) an, um die Größe der LUN um zu verringern. Um die Größe mit anderen Einheiten anzugeben, verwenden Sie eines der folgenden erkannten Suffixe direkt nach der Größe:<ul><li>**B** -Byte</li><li>**KB** -KB</li><li>**MB** -Megabyte</li><li>**GB** -Gigabyte</li><li>**TB** -Terabyte</li><li>**PB** -Peer tabyte. |
| Noerr | Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet Diskraid weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. |

### <a name="standby"></a>Standby

Ändert den Status der Pfade zum aktuell ausgewählten Port des Hostbus Adapters (HBA) in den Standbymodus.

#### <a name="syntax"></a>Syntax

```
standby hbaport
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| HBAPORT | Ändert den Status der Pfade zum aktuell ausgewählten Port des Hostbus Adapters (HBA) in den Standbymodus. |

### <a name="unmask"></a>Maskierung

Macht die aktuell ausgewählten LUNs von den angegebenen Hosts aus verfügbar.

#### <a name="syntax"></a>Syntax

```
unmask lun {all | none | [add] wwn=<hexadecimal_number> [;<hexadecimal_number> [;…]] | [add] initiator=<initiator>[;<initiator>[;…]]} [uninstall]
```

##### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| alle | Gibt an, dass die LUN von allen Hosts zugänglich gemacht werden soll. Allerdings können Sie die LUN nicht für alle Ziele in einem iSCSI-Subsystem aufheben.<P>Bevor Sie den Befehl ausführen, müssen Sie sich vom Ziel abmelden `unmask lun all` . |
| none | Gibt an, dass der Zugriff auf die LUN für jeden Host nicht möglich sein soll.<P>Bevor Sie den Befehl ausführen, müssen Sie sich vom Ziel abmelden `unmask lun none` . |
| add | Gibt an, dass die angegebenen Hosts der vorhandenen Liste von Hosts hinzugefügt werden müssen, von denen diese LUN zugänglich ist. Wenn dieser Parameter nicht angegeben wird, ersetzt die Liste der bereitgestellten Hosts die vorhandene Liste der Hosts, von denen diese LUN zugänglich ist. |
| WWN = | Gibt eine Liste von hexadezimalen Zahlen an, die World Wide Names darstellen, von denen aus die LUN oder Hosts zugänglich gemacht werden sollen. Um eine bestimmte Gruppe von Hosts in einem Fibre Channel Subsystem zu maskieren bzw. die Maskierung aufzuheben, können Sie eine durch Semikolons getrennte Liste von WWN für die Ports auf den gewünschten Host Computern eingeben. |
| Initiator = | Gibt eine Liste von iSCSI-Initiatoren an, auf die die aktuell ausgewählte LUN zugegriffen werden soll. Um eine bestimmte Gruppe von Hosts in einem iSCSI-Subsystem zu maskieren bzw. die Maskierung aufzuheben, können Sie eine durch Semikolons getrennte Liste von iSCSI-Initiator-Namen für die Initiatoren auf den gewünschten Host Computern eingeben. |
| uninstall | Wenn angegeben, wird der Datenträger, der der LUN auf dem lokalen System zugeordnet ist, deinstalliert, bevor die LUN maskiert wird. |

## <a name="scripting-diskraid"></a>Skripterstellung für Diskraid

Auf jedem Computer, auf dem eine unterstützte Version von Windows Server ausgeführt wird, mit einem zugeordneten VDS-Hardware Anbieter kann ein Skript erstellt werden. Zum Aufrufen eines Diskraid-Skripts geben Sie an der Eingabeaufforderung Folgendes ein:

```
diskraid /s <script.txt>
```

Standardmäßig beendet Diskraid die Verarbeitung von Befehlen und gibt einen Fehlercode zurück, wenn ein Problem im Skript vorliegt. Um die Ausführung des Skripts fortzusetzen und Fehler zu ignorieren, fügen Sie den **Noerr** -Parameter in den Befehl ein. Dies ermöglicht die Verwendung eines einzelnen Skripts, um alle LUNs in einem Subsystem unabhängig von der Gesamtanzahl der LUNs zu löschen. Nicht alle Befehle unterstützen den **Noerr** -Parameter. Fehler werden immer bei Befehlssyntax Fehlern zurückgegeben, unabhängig davon, ob Sie den **Noerr** -Parameter eingefügt haben.

## <a name="diskraid-error-codes"></a>Diskraid-Fehlercodes

| Fehlercode | Fehlerbeschreibung |
| ---------- | ----------------- |
| 0 | Kein Fehler ist aufgetreten. Das gesamte Skript wurde ohne Fehler ausgeführt. |
| 1 | Es ist eine schwerwiegende Ausnahme aufgetreten. |
| 2 | Die in einer Diskraid-Befehlszeile angegebenen Argumente waren falsch. |
| 3 | Das angegebene Skript oder die angegebene Ausgabedatei konnte von Diskraid nicht geöffnet werden. |
| 4 | Einer der Dienste von Diskraid hat einen Fehler zurückgegeben. |
| 5 | Befehlssyntax Fehler. Fehler beim Skript, weil ein Objekt nicht ordnungsgemäß ausgewählt wurde oder für die Verwendung mit diesem Befehl ungültig war. |

## <a name="example"></a>Beispiel

Geben Sie Folgendes ein, um den Status von Subsystem 0 auf dem Computer anzuzeigen:

```
diskraid
```

Drücken Sie die EINGABETASTE und die Ausgabe ähnlich der folgenden wird angezeigt:

```
Microsoft Diskraid version 5.2.xxxx
Copyright (©) 2003 Microsoft Corporation
On computer: COMPUTER_NAME
```

Geben Sie Folgendes an der Diskraid-Eingabeaufforderung ein, um Subsystem 0 auszuwählen:

```
select subsystem 0
```

Drücken Sie die EINGABETASTE und die Ausgabe ähnlich der folgenden wird angezeigt:

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

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)