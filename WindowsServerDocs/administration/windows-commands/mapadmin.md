---
title: mapadmin
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3ad9f55ba130014227326f4abe8540c78755f6c5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437375"
---
# <a name="mapadmin"></a>mapadmin



Sie können **Mapadmin** User Name Mapping für Microsoft Services for Network File System zu verwalten.

## <a name="syntax"></a>Syntax
```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <WindowsUser> -uu <UNIXUser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <WindowsGroup> -ug <UNIXGroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <WindowsUser> [-uu <UNIXUser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <WindowsGroup> [-ug <UNIXGroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename> 
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <WindowsDomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <WindowsDomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

## <a name="description"></a>Beschreibung
Die **Mapadmin** Befehlszeilen-Hilfsprogramm verwaltet User Name Mapping, auf dem lokalen oder remote-Computer, die mit Microsoft Services for Network File System. Wenn Sie mit einem Konto, die nicht über administrative Anmeldeinformationen verfügen angemeldet sind, können Sie angeben, einen Benutzernamen und das Kennwort für ein Konto mit diesen.

Zusätzlich zu den spezifischen Befehlszeilenargumenten **Mapadmin** akzeptiert die folgenden Argumente und Optionen:

&lt;Computer&gt; gibt an, dem Remotecomputer mit den User Name Mapping-Dienst, den Sie verwalten möchten. Sie können den Computer mithilfe der Name einer Windows Internet Name Service (WINS) oder ein Domain Name System (DNS) angeben oder von IP (Internet Protocol) zu beheben.

-u &lt;Benutzer&gt; gibt den Benutzernamen des Benutzers, dessen Anmeldeinformationen sind, verwendet werden soll. Es kann erforderlich sein, den Domänennamen hinzufügen, um den Benutzernamen im Format <em>Domäne</em> **\\** <em>Benutzernamen</em>.

-p &lt;Kennwort&gt; gibt das Kennwort des Benutzers. Bei Angabe der **-u** option jedoch weglassen der **-p** -Option verwenden, werden Sie aufgefordert, für das Kennwort des Benutzers.
Die jeweilige Aktion, die **Mapadmin** ausführt, hängt das Befehlsargument, die Sie angeben:

## <a name="parameters"></a>Parameter
### <a name="start"></a>start
Startet den Dienst User Name Mapping.

### <a name="stop"></a>stop
Beendet den Dienst User Name Mapping.

### <a name="config"></a>config
Gibt allgemeine Einstellungen für die User Name Mapping. Die folgenden Optionen sind verfügbar, mit diesem Befehlsargument: **- R &lt;Dddd&gt;:&lt;Hh&gt;:&lt;mm&gt;**  – gibt an, das Aktualisierungsintervall für aus den Windows und NIS-Datenbanken wird in Tagen, Stunden und Minuten aktualisiert. Das kürzeste Intervall ist 5 Minuten.
**-i {yes | keine}** – aktiviert die einfache Zuordnung (**Ja**) oder deaktiviert (**keine**). Standardmäßig ist die einfache Zuordnung auf.
**Hinzufügen** -erstellt eine neue Zuordnung für einen Benutzer oder Gruppe. Die folgenden Optionen sind verfügbar, mit diesem Befehlsargument:

|Option|Definition|
|-----|-------|
|-Wu &lt;Name&gt;|Gibt den Namen des Windows-Benutzers, für die eine neue Zuordnung erstellt wird.|
|-Uu &lt;Name&gt;|Gibt den Namen von den UNIX-Benutzer, die für den eine neue Zuordnung erstellt wird.|
|-Wg &lt;Gruppe&gt;|Gibt den Namen der Windows-Gruppe, die für die eine neue Zuordnung erstellt wird.|
|Ug - &lt;Gruppe&gt;|Gibt den Namen der UNIX-Gruppe, die für die eine neue Zuordnung erstellt wird.|
|-setprimary|Gibt an, dass die neue Zuordnung die primären Zuordnung.|

**Setprimary** – gibt an, die eine Zuordnung der primären Zuordnung für einen UNIX-Benutzer oder eine Gruppe mit mehreren Zuordnungen. Die folgenden Optionen sind verfügbar, mit diesem Befehlsargument:

|Option|Definition|
|-----|-------|
|-Wu &lt;Name&gt;|Gibt den Windows-Benutzer der primäre Zuordnung. Wenn mehr als eine Zuordnung für den Benutzer vorhanden ist, verwenden Sie die **- Uu** Option aus, um die primäre Zuordnung angeben.|
|-Uu &lt;Name&gt;|Gibt den UNIX-Benutzer der primäre Zuordnung.|
|-Wg &lt;Gruppe&gt;|Gibt die Windows-Gruppe der primären Zuordnung. Wenn mehr als eine Zuordnung für die Gruppe vorhanden ist, verwenden Sie die **Ug -** Option aus, um die primäre Zuordnung angeben.|
|Ug - &lt;Gruppe&gt;|Gibt die UNIX-Gruppe der primären Zuordnung.|

**Löschen Sie** – entfernt die Zuordnung für einen Benutzer oder Gruppe. Die folgenden Optionen sind für dieses Befehlsargument verfügbar:

|Option|Definition|
|-----|-------|
|-wu &lt;user&gt;|Der Windows-Benutzer, die für die die Zuordnung gelöscht werden, angegeben als &lt; *WindowsDomain&gt;\\&lt;Benutzernamen&gt;* . Geben Sie die **- Wu** oder **- Uu** Option oder beides. Wenn Sie beide Optionen angeben, werden diese spezielle Zuordnung, die durch die beiden Optionen identifiziert wird gelöscht. Wenn Sie nur angeben, die **- Wu** -Option verwenden, alle Zuordnungen für der angegebene Benutzer werden gelöscht.|
|-Wg &lt;Gruppe&gt;|Die Windows-Gruppe, die für die die Zuordnung gelöscht werden, angegeben als &lt;WindowsDomain&gt;\\&lt;Groupname&gt;. Geben Sie die **- Wg** oder **Ug -** Option oder beides. Wenn Sie beide Optionen angeben, werden diese spezielle Zuordnung, die durch die beiden Optionen identifiziert wird gelöscht. Wenn Sie nur angeben, die **- Wg** -Option verwenden, alle Zuordnungen für die angegebene Gruppe gelöscht werden.|
|-Uu &lt;Benutzer&gt;|Der UNIX-Benutzer, die für den die Zuordnung gelöscht werden, angegeben als &lt;Benutzernamen&gt;. Geben Sie die **- Wu** oder **- Uu** Option oder beides. Wenn Sie beide Optionen angeben, werden diese spezielle Zuordnung, die durch die beiden Optionen identifiziert wird gelöscht. Wenn Sie nur angeben, die **- Uu** -Option verwenden, alle Zuordnungen für der angegebene Benutzer werden gelöscht.|
|Ug - &lt;Gruppe&gt;|Der UNIX-Gruppe, die für die die Zuordnung gelöscht werden, angegeben als &lt;Groupname&gt;. Geben Sie die **- Wg** oder **Ug -** Option oder beides. Wenn Sie beide Optionen angeben, werden diese spezielle Zuordnung, die durch die beiden Optionen identifiziert wird gelöscht. Wenn Sie nur angeben, die **Ug -** -Option verwenden, alle Zuordnungen für die angegebene Gruppe gelöscht werden.|

**Liste** -zeigt Informationen zu Benutzer- und Zuordnungen. Die folgenden Optionen sind verfügbar, mit diesem Befehlsargument:

|Option|Definition|
|-----|-------|
|– alle|sind Sie sowohl einfache als auch erweiterte Zuordnungen für Benutzer und Gruppen aufgelistet.|
|-einfache|Listet alle einfachen zugeordnete Benutzer und Gruppen.|
|-Erweiterte|Listet alle erweiterten zugeordnete Benutzer und Gruppen. Zuordnungen werden in der Reihenfolge aufgeführt, in denen sie ausgewertet werden. Primäre Karten, die mit einem Sternchen (*) gekennzeichnet werden zuerst aufgeführt, gefolgt von der sekundären-Zuordnungen, die mit einem Caretzeichen (^) gekennzeichnet sind.|
|-Wu &lt;Name&gt;|Listet die Zuordnung für einen angegebenen Windows-Benutzer.|
|-Wg &lt;Gruppe&gt;|Listet die Zuordnung für eine Windows-Gruppe.|
|-Uu &lt;Name&gt;|Listet die Zuordnung für UNIX-Benutzer.|
|Ug - &lt;Gruppe&gt;|Listet die Zuordnung für eine UNIX-Gruppe.|

**Backup** – speichert Benutzernamen Zuordnen von Konfiguration und Zuordnen von Daten in die Datei, die anhand des &lt;Filename&gt;.
**Wiederherstellen** -Konfigurations-und Zuordnung mit Daten aus der Datei ersetzt (gemäß &lt;Filename&gt;), erstellt wurde, mithilfe der **backup** Befehlsargument.
**Adddomainmap** -Fügt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne oder Kennwort- und Gruppendateien hinzu. Die folgenden Optionen sind für dieses Befehlsargument verfügbar:

|Option|Definition|
|-----|-------|
|-d &lt;WindowsDomain&gt;|Gibt die Windows-Domäne zugeordnet werden soll.|
|-y &lt;NISdomain&gt;|Gibt die NIS-Domäne zugeordnet werden soll. &lt;Br /&gt;&lt;Br /&gt; **- n** &lt;NisServer&gt; gibt an, die NIS-Server für NIS-Domäne angegeben, mit der **- y**Option.|
|-f &lt;Pfad&gt;|Gibt den vollqualifizierten Pfad des Verzeichnisses mit den Dateien von Kennwörtern und Gruppen zugeordnet werden soll. Die Dateien müssen auf dem zu verwaltenden Computer befinden, und können keine **Mapadmin** zum Verwalten von eines Remotecomputer befindet, um Zuordnungen auf Grundlage von Kennwort- und Gruppendateien einzurichten.|

**Removedomainmap** – eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne entfernt. Die folgenden Optionen und Argument stehen für dieses Befehlsargument:

|Option|Definition|
|-----|-------|
|-d &lt;WindowsDomain&gt;|Gibt die Windows-Domäne der Zuordnung entfernt werden soll.|
|-y &lt;NISdomain&gt;|Gibt die NIS-Domäne der Zuordnung entfernt werden soll.|
|– alle|Gibt an, dass alle einfache Zuordnungen zwischen Windows und NIS-Domänen entfernt werden soll. Dies entfernt auch einfache Zuordnung zwischen einer Windows-Domäne und Kennwort und die Gruppe von Dateien.|

**Listdomainmaps** -Listet die Windows-Domänen, die NIS-Domänen oder Kennwort- und Gruppendateien zugeordnet sind.

## <a name="notes"></a>Hinweise
-   Wenn Sie kein Befehlsargument angeben **Mapadmin** zeigt die aktuellen Einstellungen für die User Name Mapping.
-   für alle Optionen, die eine Benutzer- oder Gruppennamen angeben, können die folgenden Formate verwendet werden:
-   Verwenden Sie für Windows-Benutzer das Formular &lt;Domäne&gt;\\&lt;Benutzernamen&gt;, \\ \\ &lt;Computer&gt;\\&lt;Benutzer Namen&gt;, \\ &lt;Computer&gt;\\&lt;Benutzernamen&gt;, oder &lt;Computer&gt;\\&lt;Benutzer Name&gt;
-   Verwenden Sie für Windows-Gruppen, die das Formular &lt;Domäne&gt;\\&lt;&lt;Groupname&gt;&gt;, \\ \\ &lt;Computer&gt; \\ &lt; &lt;Groupname&gt;&gt;, \\ &lt;Computer&gt;\\&lt;&lt;Groupname&gt; &gt;, oder &lt;Computer&gt;\\&lt;&lt;Groupname&gt;&gt;
-   Verwenden Sie für UNIX-Benutzer das Formular &lt;NamenRegistrierungNISDomain&gt;\\&lt;Benutzernamen&gt;, &lt;Benutzernamen&gt;@&lt;NamenRegistrierungNISDomain&gt;, Benutzer &lt;Namen&gt;@PCNFS, oder PCNFS\\&lt;Benutzername&gt;
-   für UNIX-Gruppen, verwenden Sie das Formular &lt;NamenRegistrierungNISDomain&gt;\\&lt;Groupname&gt;, &lt;Groupname&gt;@&lt;NamenRegistrierungNISDomain&gt;, &lt;Groupname&gt;@PCNFS, oder PCNFS\\&lt;Groupname&gt;

## <a name="additional-references"></a>Zusätzliche Referenzen
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
