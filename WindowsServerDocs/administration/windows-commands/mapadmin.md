---
title: mapadmin
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: fc4b76c1989298ea83c480b9c838ce0fc18fef5f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373757"
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

&lt;computer @ no__t-1 gibt den Remote Computer an, auf dem der Benutzernamenzuordnung Dienst ausgeführt wird, den Sie verwalten möchten. Sie können den Computer mithilfe eines WINS-Namens (Windows Internet Name Service) oder eines Domain Name System (DNS) oder über eine IP-Adresse (Internet Protocol) angeben.

-u &lt;User @ no__t-1 gibt den Benutzernamen des Benutzers an, dessen Anmelde Informationen verwendet werden sollen. Möglicherweise ist es erforderlich, den Domänen Namen dem Benutzernamen in der Form <em>Domäne</em> **\\** <em>Benutzername</em>hinzuzufügen.

-p &lt;password @ no__t-1 gibt das Kennwort des Benutzers an. Wenn Sie die Option "- **u** " angeben, aber die Option " **-p** " weglassen, werden Sie zur Eingabe des Benutzer Kennworts aufgefordert.
Die spezifische Aktion, die von **mapadmin** ausgeführt wird, hängt vom angegebenen Befehls Argument ab:

## <a name="parameters"></a>Parameter
### <a name="start"></a>start
startet den Benutzernamenzuordnung-Dienst.

### <a name="stop"></a>stop
Beendet den Benutzernamenzuordnung-Dienst.

### <a name="config"></a>Einstellungen
Gibt allgemeine Einstellungen für Benutzernamenzuordnung an. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar: **-r &lt;dddd @ no__t-2: &lt;hh @ no__t-4: &lt;mm @ no__t-6** -gibt das Aktualisierungs Intervall für die Aktualisierung aus den Windows-und NIS-Datenbanken in Tagen, Stunden und Minuten an. Das Mindestintervall beträgt 5 Minuten.
**-i {Yes | No}** -schaltet die einfache Zuordnung ein (**Ja**) oder aus (**Nein**). Standardmäßig ist die einfache Zuordnung aktiviert.
**Add** -erstellt eine neue Zuordnung für einen Benutzer oder eine Gruppe. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Wu &lt;name @ no__t-1|Gibt den Namen des Windows-Benutzers an, für den eine neue Zuordnung erstellt wird.|
|-UU &lt;name @ no__t-1|Gibt den Namen des UNIX-Benutzers an, für den eine neue Zuordnung erstellt wird.|
|-WG &lt;group @ no__t-1|Gibt den Namen der Windows-Gruppe an, für die eine neue Zuordnung erstellt wird.|
|-UG &lt;group @ no__t-1|Gibt den Namen der UNIX-Gruppe an, für die eine neue Zuordnung erstellt wird.|
|-setprimary|Gibt an, dass die neue Zuordnung die primäre Zuordnung ist.|

**setprimary** : gibt an, welche Zuordnung die primäre Zuordnung für einen UNIX-Benutzer oder eine UNIX-Gruppe mit mehreren Zuordnungen ist. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Wu &lt;name @ no__t-1|Gibt den Windows-Benutzer der primären Zuordnung an. Wenn mehr als eine Zuordnung für den Benutzer vorhanden ist, verwenden Sie die Option **-UU** , um die primäre Zuordnung anzugeben.|
|-UU &lt;name @ no__t-1|Gibt den UNIX-Benutzer der primären Zuordnung an.|
|-WG &lt;group @ no__t-1|Gibt die Windows-Gruppe der primären Zuordnung an. Wenn mehr als eine Zuordnung für die Gruppe vorhanden ist, verwenden Sie die Option **-UG** , um die primäre Zuordnung anzugeben.|
|-UG &lt;group @ no__t-1|Gibt die UNIX-Gruppe der primären Zuordnung an.|

**Löschen** : entfernt die Zuordnung für einen Benutzer oder eine Gruppe. Die folgenden Optionen sind für dieses Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Wu &lt;User @ no__t-1|Der Windows-Benutzer, für den die Zuordnung gelöscht wird, angegeben als &lt;*WindowsDomain @ no__t-2 @ no__t-3 @ no__t-4user Name @ no__t-5*. Sie müssen entweder die **-Wu-** oder die **-UU-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-Wu** ' angeben, werden alle Zuordnungen für den angegebenen Benutzer gelöscht.|
|-WG &lt;group @ no__t-1|Die Windows-Gruppe, für die die Zuordnung gelöscht wird, angegeben als &lt;windowsdomain @ no__t-1 @ no__t-2 @ no__t-3groupname @ no__t-4. Sie müssen entweder die **-WG-** Option oder die **-UG-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-WG** ' angeben, werden alle Zuordnungen für die angegebene Gruppe gelöscht.|
|-UU &lt;User @ no__t-1|Der UNIX-Benutzer, für den die Zuordnung gelöscht wird, angegeben als &lt;User Name @ no__t-1. Sie müssen entweder die **-Wu-** oder die **-UU-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option **-UU** angeben, werden alle Zuordnungen für den angegebenen Benutzer gelöscht.|
|-UG &lt;group @ no__t-1|Die UNIX-Gruppe, für die die Zuordnung gelöscht wird, angegeben als &lt;groupname @ no__t-1. Sie müssen entweder die **-WG-** Option oder die **-UG-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-UG** ' angeben, werden alle Zuordnungen für die angegebene Gruppe gelöscht.|

**List** -zeigt Informationen zu Benutzer-und Gruppen Zuordnungen an. Die folgenden Optionen sind mit diesem Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-Alle|listet sowohl einfache als auch erweiterte Zuordnungen für Benutzer und Gruppen auf.|
|-einfach|Listet alle einfachen zugeordneten Benutzer und Gruppen auf.|
|-erweitert|Listet alle erweiterten zugeordneten Benutzer und Gruppen auf. Zuordnungen werden in der Reihenfolge aufgelistet, in der Sie ausgewertet werden. Primäre Zuordnungen, die mit einem Sternchen (*) gekennzeichnet sind, werden zuerst aufgelistet, gefolgt von sekundären Zuordnungen, die mit einem "Karat" (^) gekennzeichnet sind.|
|-Wu &lt;name @ no__t-1|Listet die Zuordnung für einen angegebenen Windows-Benutzer auf.|
|-WG &lt;group @ no__t-1|Listet die Zuordnung für eine Windows-Gruppe auf.|
|-UU &lt;name @ no__t-1|Listet die Zuordnung für einen UNIX-Benutzer auf.|
|-UG &lt;group @ no__t-1|Listet die Zuordnung für eine UNIX-Gruppe auf.|

**Backup** : speichert Benutzernamenzuordnung Konfiguration und die Zuordnung von Daten in der durch &lt;filename @ no__t-2 angegebenen Datei.
**Restore** -ersetzt Konfigurations-und Zuordnungsdaten durch Daten aus der Datei (angegeben durch &lt;filename @ no__t-2), die mit dem **Backup** -Befehls Argument erstellt wurde.
**adddomainmap** : Fügt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne bzw. einem Kennwort und Gruppen Dateien hinzu. Die folgenden Optionen sind für dieses Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-d &lt;windowsdomain @ no__t-1|Gibt die Windows-Domäne an, die zugeordnet werden soll.|
|-y &lt;nisdomain @ no__t-1|Gibt die NIS-Domäne an, die zugeordnet werden soll. &lt;BR/&gt; @ no__t-2BR/&gt; **-n** &lt;nisserver @ no__t-6 gibt den NIS-Server für die NIS-Domäne an, die mit der Option **-y** angegeben wurde.|
|-f &lt;path @ no__t-1|Gibt den voll qualifizierten Pfad des Verzeichnisses mit den Kennwort-und Gruppen Dateien an, die zugeordnet werden sollen. Die Dateien müssen sich auf dem verwalteten Computer befinden, und Sie können nicht mithilfe von " **mapadmin** " einen Remote Computer zum Einrichten von Zuordnungen auf der Grundlage von Kennwort-und Gruppen Dateien verwalten.|

**removedomainmap** : entfernt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne. Die folgenden Optionen und Argumente sind für dieses Befehls Argument verfügbar:

|Option|Definition|
|-----|-------|
|-d &lt;windowsdomain @ no__t-1|Gibt die Windows-Domäne der zu entfernenden Karte an.|
|-y &lt;nisdomain @ no__t-1|Gibt die NIS-Domäne der zu entfernenden Karte an.|
|-Alle|Gibt an, dass alle einfachen Zuordnungen zwischen Windows-und NIS-Domänen entfernt werden sollen. Dadurch werden auch alle einfachen Zuordnungen zwischen einer Windows-Domäne und den Kennwort-und Gruppen Dateien entfernt.|

**listdomainmaps** : Listet die Windows-Domänen auf, die NIS-Domänen oder Kennwort-und Gruppen Dateien zugeordnet sind.

## <a name="notes"></a>Hinweise
-   Wenn Sie kein Befehls Argument angeben, zeigt **mapadmin** die aktuellen Einstellungen für Benutzernamenzuordnung an.
-   für alle Optionen, die einen Benutzer-oder Gruppennamen angeben, können die folgenden Formate verwendet werden:
-   Verwenden Sie für Windows-Benutzer das Formular &lt;domäne @ no__t-1 @ no__t-2 @ no__t-3user Name @ no__t-4, \\ @ no__t-6 @ no__t-7computer @ no__t-8 @ no__t-9 @ no__t-10User Name @ no__t-11, &gt;2 @ no__t-13computer @ no__t-14 @ no__t-15 @ no__t-16benutzername @ no__ t-17 oder 8computer @ no__t-19 @ no__t-20 @ no__t-21user Name @ no__t-22
-   Verwenden Sie für Windows-Gruppen das Formular &lt;domäne @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4groupname @ no__t-5 @ no__t-6, \\ @ no__t-8 @ no__t-9computer @ no__t-10 @ no__t-11 @ no__t-12 @ no__t-13groupname @ no__t-14 @ no__t-15, &gt;6 @ no__t-17computer @ no_ _T-18 @ no__t-19 @ no__t-20 @ no__t-21groupname @ no__t-22 @ no__t-23 oder \\4computer @ no__t-25 @ no__t-26 @ no__t-27 @ no__t-28groupname @ no__t-29 @ no__t-30
-   Verwenden Sie für UNIX-Benutzer das Formular &lt;nisdomain @ no__t-1 @ no__t-2 @ no__t-3user Name @ no__t-4, &lt;benutzer Name @ no__t-6 @ no__t-7 @ no__t-8nisdomain @ no__t-9, User &gt;0name @ no__t-11 @ no__t-12 oder PCNFS @ no__t-13 @ no__t-14User Name @ no__t-15
-   Verwenden Sie für UNIX-Gruppen das Formular &lt;nisdomain @ no__t-1 @ no__t-2 @ no__t-3groupname @ no__t-4, &lt;groupname @ no__t-6 @ no__t-7 @ no__t-8nisdomain @ no__t-9, &gt;0groupname @ no__t-11 @ no__t-12 oder PCNFS @ no__t-13 @ no__t-14groupname @ no__t-15

## <a name="additional-references"></a>Weitere Verweise
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
