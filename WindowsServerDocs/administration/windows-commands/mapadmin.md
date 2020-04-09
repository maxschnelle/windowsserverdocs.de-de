---
title: mapadmin
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5ea60f4d9753ed90c0d13ee48289b011aeafe6b0
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80839673"
---
# <a name="mapadmin"></a>mapadmin



Sie können " **mapadmin** " verwenden, um Benutzernamenzuordnung für Microsoft-Dienste für das Netzwerkdatei System zu verwalten.

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
Mit dem Befehlszeilen-Hilfsprogramm " **mapadmin** " werden Benutzernamenzuordnung auf dem lokalen Computer oder dem Remote Computer verwaltet, auf dem Microsoft Services for Network File System ausgeführt wird Wenn Sie mit einem Konto angemeldet sind, das nicht über Administratorrechte verfügt, können Sie einen Benutzernamen und ein Kennwort für ein Konto angeben.

Zusätzlich zu bestimmten Befehls Argumenten akzeptiert **mapadmin** die folgenden Argumente und Optionen:

&lt;Computer&gt; gibt den Remote Computer an, auf dem der Benutzernamenzuordnung Dienst ausgeführt wird, den Sie verwalten möchten. Sie können den Computer mithilfe eines WINS-Namens (Windows Internet Name Service) oder eines Domain Name System (DNS) oder über eine IP-Adresse (Internet Protocol) angeben.

-u &lt;Benutzer&gt; der den Benutzernamen des Benutzers angibt, dessen Anmelde Informationen verwendet werden sollen. Möglicherweise ist es erforderlich, den Domänen Namen dem Benutzernamen in der Form <em>Domäne</em> **\\** <em>Benutzername</em>hinzuzufügen.

-p &lt;Kennwort&gt; gibt das Kennwort des Benutzers an. Wenn Sie die Option "- **u** " angeben, aber die Option " **-p** " weglassen, werden Sie zur Eingabe des Benutzer Kennworts aufgefordert.
Die spezifische Aktion, die von **mapadmin** ausgeführt wird, hängt vom angegebenen Befehls Argument ab:

### <a name="parameters"></a>Parameter
### <a name="start"></a>Start
startet den Benutzernamenzuordnung-Dienst.

### <a name="stop"></a>stop
Beendet den Benutzernamenzuordnung-Dienst.

### <a name="config"></a>config
Gibt allgemeine Einstellungen für Benutzernamenzuordnung an. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar: **-r &lt;dddd&gt;:&lt;HH&gt;:&lt;mm&gt;** : gibt das Aktualisierungs Intervall für die Aktualisierung aus den Windows-und NIS-Datenbanken in Tagen, Stunden und Minuten an. Das Mindestintervall beträgt 5 Minuten.
**-i {Yes | No}** -schaltet die einfache Zuordnung ein (**Ja**) oder aus (**Nein**). Standardmäßig ist die einfache Zuordnung aktiviert.
**Add** -erstellt eine neue Zuordnung für einen Benutzer oder eine Gruppe. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Wu &lt;Name&gt;|Gibt den Namen des Windows-Benutzers an, für den eine neue Zuordnung erstellt wird.|
|-UU &lt;Name&gt;|Gibt den Namen des UNIX-Benutzers an, für den eine neue Zuordnung erstellt wird.|
|-WG &lt;Gruppe&gt;|Gibt den Namen der Windows-Gruppe an, für die eine neue Zuordnung erstellt wird.|
|-UG &lt;Gruppe&gt;|Gibt den Namen der UNIX-Gruppe an, für die eine neue Zuordnung erstellt wird.|
|-setprimary|Gibt an, dass die neue Zuordnung die primäre Zuordnung ist.|

**setprimary** : gibt an, welche Zuordnung die primäre Zuordnung für einen UNIX-Benutzer oder eine UNIX-Gruppe mit mehreren Zuordnungen ist. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Wu &lt;Name&gt;|Gibt den Windows-Benutzer der primären Zuordnung an. Wenn mehr als eine Zuordnung für den Benutzer vorhanden ist, verwenden Sie die Option **-UU** , um die primäre Zuordnung anzugeben.|
|-UU &lt;Name&gt;|Gibt den UNIX-Benutzer der primären Zuordnung an.|
|-WG &lt;Gruppe&gt;|Gibt die Windows-Gruppe der primären Zuordnung an. Wenn mehr als eine Zuordnung für die Gruppe vorhanden ist, verwenden Sie die Option **-UG** , um die primäre Zuordnung anzugeben.|
|-UG &lt;Gruppe&gt;|Gibt die UNIX-Gruppe der primären Zuordnung an.|

**Löschen** : entfernt die Zuordnung für einen Benutzer oder eine Gruppe. Die folgenden Optionen sind für dieses Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Wu &lt;Benutzer&gt;|Der Windows-Benutzer, für den die Zuordnung gelöscht wird, angegeben als &lt;*WindowsDomain&gt;\\&lt;Benutzer Name&gt;* . Sie müssen entweder die **-Wu-** oder die **-UU-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-Wu** ' angeben, werden alle Zuordnungen für den angegebenen Benutzer gelöscht.|
|-WG &lt;Gruppe&gt;|Die Windows-Gruppe, für die die Zuordnung gelöscht wird, angegeben als &lt;WindowsDomain&gt;\\&lt;GroupName&gt;. Sie müssen entweder die **-WG-** Option oder die **-UG-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-WG** ' angeben, werden alle Zuordnungen für die angegebene Gruppe gelöscht.|
|-UU &lt;Benutzer&gt;|Der UNIX-Benutzer, für den die Zuordnung gelöscht wird, angegeben als &lt;Benutzer Name&gt;. Sie müssen entweder die **-Wu-** oder die **-UU-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option **-UU** angeben, werden alle Zuordnungen für den angegebenen Benutzer gelöscht.|
|-UG &lt;Gruppe&gt;|Die UNIX-Gruppe, für die die Zuordnung gelöscht wird, angegeben als &lt;GroupName&gt;. Sie müssen entweder die **-WG-** Option oder die **-UG-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-UG** ' angeben, werden alle Zuordnungen für die angegebene Gruppe gelöscht.|

**List** -zeigt Informationen zu Benutzer-und Gruppen Zuordnungen an. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Alle|listet sowohl einfache als auch erweiterte Zuordnungen für Benutzer und Gruppen auf.|
|-einfach|Listet alle einfachen zugeordneten Benutzer und Gruppen auf.|
|-erweitert|Listet alle erweiterten zugeordneten Benutzer und Gruppen auf. Zuordnungen werden in der Reihenfolge aufgelistet, in der Sie ausgewertet werden. Primäre Zuordnungen, die mit einem Sternchen (*) gekennzeichnet sind, werden zuerst aufgelistet, gefolgt von sekundären Zuordnungen, die mit einem "Karat" (^) gekennzeichnet sind.|
|-Wu &lt;Name&gt;|Listet die Zuordnung für einen angegebenen Windows-Benutzer auf.|
|-WG &lt;Gruppe&gt;|Listet die Zuordnung für eine Windows-Gruppe auf.|
|-UU &lt;Name&gt;|Listet die Zuordnung für einen UNIX-Benutzer auf.|
|-UG &lt;Gruppe&gt;|Listet die Zuordnung für eine UNIX-Gruppe auf.|

**Backup** : speichert Benutzernamenzuordnung Konfiguration und die Zuordnung von Daten in der durch &lt;Dateinamen&gt;angegebenen Datei.
**Restore** -ersetzt Konfigurations-und Zuordnungsdaten durch Daten aus der Datei (angegeben durch &lt;filename&gt;), die mit dem **Backup** -Befehls Argument erstellt wurde.
**adddomainmap** : Fügt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne bzw. einem Kennwort und Gruppen Dateien hinzu. Die folgenden Optionen sind für dieses Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-d &lt;WindowsDomain&gt;|Gibt die Windows-Domäne an, die zugeordnet werden soll.|
|-y &lt;nisdomain&gt;|Gibt die NIS-Domäne an, die zugeordnet werden soll.&lt;BR/&gt;&lt;BR/&gt; **-n** &lt;nisServer&gt; gibt den NIS-Server für die NIS-Domäne an, die mit der Option **-y** angegeben wurde.|
|-f &lt;Pfad&gt;|Gibt den voll qualifizierten Pfad des Verzeichnisses mit den Kennwort-und Gruppen Dateien an, die zugeordnet werden sollen. Die Dateien müssen sich auf dem verwalteten Computer befinden, und Sie können nicht mithilfe von " **mapadmin** " einen Remote Computer zum Einrichten von Zuordnungen auf der Grundlage von Kennwort-und Gruppen Dateien verwalten.|

**removedomainmap** : entfernt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne. Die folgenden Optionen und Argumente sind für dieses Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-d &lt;WindowsDomain&gt;|Gibt die Windows-Domäne der zu entfernenden Karte an.|
|-y &lt;nisdomain&gt;|Gibt die NIS-Domäne der zu entfernenden Karte an.|
|-Alle|Gibt an, dass alle einfachen Zuordnungen zwischen Windows-und NIS-Domänen entfernt werden sollen. Dadurch werden auch alle einfachen Zuordnungen zwischen einer Windows-Domäne und den Kennwort-und Gruppen Dateien entfernt.|

**listdomainmaps** : Listet die Windows-Domänen auf, die NIS-Domänen oder Kennwort-und Gruppen Dateien zugeordnet sind.

## <a name="notes"></a>Hinweise
-   Wenn Sie kein Befehls Argument angeben, zeigt **mapadmin** die aktuellen Einstellungen für Benutzernamenzuordnung an.
-   für alle Optionen, die einen Benutzer-oder Gruppennamen angeben, können die folgenden Formate verwendet werden:
-   Verwenden Sie für Windows-Benutzer das Formular &lt;Domänen&gt;\\&lt;Benutzernamen&gt;, \\\\&lt;&gt;Computer \\&lt;&gt;Benutzername \\, &lt;&gt;\\&lt;&gt;&lt;Benutzername&gt;\\&lt;&gt; Computer
-   Verwenden Sie für Windows-Gruppen das Formular &lt;Domänen&gt;\\&lt;&lt;GroupName&gt;&gt;, \\\\&lt;&gt;\\&lt;&lt;&gt;GroupName &gt;\\&lt;&gt;\\Computer &lt;&lt;&gt;&gt;GroupName &lt;&gt;oder \\Computer &lt;&lt;&gt;&gt; GroupName
-   Verwenden Sie für UNIX-Benutzer das Formular &lt;zdomain&gt;\\&lt;Benutzernamen&gt;, &lt;Benutzernamen&gt;@&lt;zdomain&gt;, Benutzer &lt;Name&gt;@PCNFSoder PCNFS\\&lt;Benutzername&gt;
-   Verwenden Sie für UNIX-Gruppen das Formular &lt;zdomain&gt;\\&lt;GroupName&gt;, &lt;GroupName&gt;@&lt;zdomain&gt;, &lt;GroupName&gt;@PCNFSoder PCNFS\\&lt;GroupName&gt;

## <a name="additional-references"></a>Weitere Verweise
- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
