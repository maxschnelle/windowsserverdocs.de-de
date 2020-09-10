---
title: mapadmin
description: Referenz Artikel zum mapadmin-Befehl, der Benutzernamenzuordnung für Microsoft-Dienste für das Netzwerkdatei System verwaltet.
ms.topic: reference
ms.assetid: b17332c7-8622-4223-9c43-2fb9cf4d992d
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 561215bbffc12c725e82a066824206131f4859da
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89636538"
---
# <a name="mapadmin"></a>mapadmin

Mit dem Befehlszeilen-Hilfsprogramm " **mapadmin** " werden Benutzernamenzuordnung auf dem lokalen Computer oder dem Remote Computer verwaltet, auf dem Microsoft Services for Network File System ausgeführt wird Wenn Sie mit einem Konto angemeldet sind, das nicht über Administratorrechte verfügt, können Sie einen Benutzernamen und ein Kennwort für ein Konto angeben.

## <a name="syntax"></a>Syntax

```
mapadmin [<computer>] [-u <user> [-p <password>]]
mapadmin [<computer>] [-u <user> [-p <password>]] {start | stop}
mapadmin [<computer>] [-u <user> [-p <password>]] config <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] add -wu <windowsuser> -uu <UNIXuser> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] add -wg <windowsgroup> -ug <UNIXgroup> [-setprimary]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wu <Windowsuser> [-uu <UNIXuser>]
mapadmin [<computer>] [-u <user> [-p <password>]] setprimary -wg <Windowsgroup> [-ug <UNIXgroup>]
mapadmin [<computer>] [-u <user> [-p <password>]] delete <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] list <option[...]>
mapadmin [<computer>] [-u <user> [-p <password>]] backup <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] restore <filename>
mapadmin [<computer>] [-u <user> [-p <password>]] adddomainmap -d <Windowsdomain> {-y <<NISdomain>> | -f <path>}
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -d <Windowsdomain> -y <<NISdomain>>
mapadmin [<computer>] [-u <user> [-p <password>]] removedomainmap -all
mapadmin [<computer>] [-u <user> [-p <password>]] listdomainmaps
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- | ----------- |
| `<computer>` | Gibt den Remote Computer an, auf dem der Benutzernamenzuordnung-Dienst ausgeführt wird, den Sie verwalten möchten. Sie können den Computer mithilfe eines WINS-Namens (Windows Internet Name Service) oder eines Domain Name System (DNS) oder über eine IP-Adresse (Internet Protocol) angeben. |
| -u `<user>` | Gibt den Benutzernamen des Benutzers an, dessen Anmelde Informationen verwendet werden sollen. Möglicherweise ist es erforderlich, den Domänen Namen dem Benutzernamen im Format "Domäne *\ Benutzer*Name" hinzuzufügen. |
| -p `<password>` | Gibt das Kennwort des Benutzers an. Wenn Sie die Option "- **u** " angeben, aber die Option " **-p** " weglassen, werden Sie zur Eingabe des Benutzer Kennworts aufgefordert. |
| `start | stop` | Startet oder beendet den Benutzernamenzuordnung-Dienst. |
| config | Gibt allgemeine Einstellungen für Benutzernamenzuordnung an. Die folgenden Optionen sind für diesen Parameter verfügbar:<ul><li>**-r `<dddd>:<hh>:<mm>` :** Hiermit wird das Aktualisierungs Intervall für die Aktualisierung aus den Windows-und NIS-Datenbanken in Tagen, Stunden und Minuten angegeben. Das Mindestintervall beträgt 5 Minuten.</li><li>**-i `{yes | no}` :** schaltet die einfache Zuordnung ein (**Ja**) oder aus (**Nein**). Standardmäßig ist die Zuordnung aktiviert.</li></ul> |
| add | Erstellt eine neue Zuordnung für einen Benutzer oder eine Gruppe. Die folgenden Optionen sind für diesen Parameter verfügbar:<ul><li>**-Wu `<name>` :** gibt den Namen des Windows-Benutzers an, für den eine neue Zuordnung erstellt wird.</li><li>**-UU `<name>` :** gibt den Namen des UNIX-Benutzers an, für den eine neue Zuordnung erstellt wird.</li><li>**-WG `<group>` :** gibt den Namen der Windows-Gruppe an, für die eine neue Zuordnung erstellt wird.</li><li>**-UG `<group>` :** gibt den Namen der UNIX-Gruppe an, für die eine neue Zuordnung erstellt wird.</li><li>**-setprimary:** Gibt an, dass die neue Zuordnung die primäre Zuordnung ist.</li></ul> |
| setprimary | Gibt an, welche Zuordnung die primäre Zuordnung für einen UNIX-Benutzer oder eine UNIX-Gruppe mit mehreren Zuordnungen ist. Die folgenden Optionen sind für diesen Parameter verfügbar:<ul><li>**-Wu `<name>` :** gibt den Windows-Benutzer der primären Zuordnung an. Wenn mehr als eine Zuordnung für den Benutzer vorhanden ist, verwenden Sie die Option **-UU** , um die primäre Zuordnung anzugeben.</li><li>**-UU `<name>` :** gibt den UNIX-Benutzer der primären Zuordnung an.</li><li>**-WG `<group>` :** gibt die Windows-Gruppe der primären Zuordnung an. Wenn mehr als eine Zuordnung für die Gruppe vorhanden ist, verwenden Sie die Option **-UG** , um die primäre Zuordnung anzugeben.</li><li>**-UG `<group>` :** gibt die UNIX-Gruppe der primären Zuordnung an.</li></ul> |
| delete | Entfernt die Zuordnung für einen Benutzer oder eine Gruppe. Die folgenden Optionen sind für diesen Parameter verfügbar:<ul><li>**-Wu `<user>` :** gibt den Windows-Benutzer an, für den die Zuordnung gelöscht wird, angegeben als `<windowsdomain>\<username>` .<p>Sie müssen entweder die **-Wu-** oder die **-UU-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-Wu** ' angeben, werden alle Zuordnungen für den angegebenen Benutzer gelöscht.</li><li>**-UU `<user>` :** gibt den UNIX-Benutzer an, für den die Zuordnung gelöscht wird, angegeben als `<username>` .<p>Sie müssen entweder die **-Wu-** oder die **-UU-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option **-UU** angeben, werden alle Zuordnungen für den angegebenen Benutzer gelöscht.</li><li>**-WG `<group>` :** gibt die Windows-Gruppe an, für die die Zuordnung gelöscht wird, angegeben als `<windowsdomain>\<username>` .<p>Sie müssen entweder die **-WG-** Option oder die **-UG-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-WG** ' angeben, werden alle Zuordnungen für die angegebene Gruppe gelöscht.</li><li>**-UG `<group>` :** gibt die UNIX-Gruppe an, für die die Zuordnung gelöscht wird, angegeben als `<groupname>` .<p>Sie müssen entweder die **-WG-** Option oder die **-UG-** Option oder beides angeben. Wenn Sie beide Optionen angeben, wird die von den beiden Optionen identifizierte Zuordnung gelöscht. Wenn Sie nur die Option ' **-UG** ' angeben, werden alle Zuordnungen für die angegebene Gruppe gelöscht.</li></ul> |
| list | Zeigt Informationen zu Benutzer-und Gruppen Zuordnungen an. Die folgenden Optionen sind für diesen Parameter verfügbar:<ul><li>**-alle:** Listet sowohl einfache als auch erweiterte Zuordnungen für Benutzer und Gruppen auf.</li><li>**-einfach:** Listet alle einfachen zugeordneten Benutzer und Gruppen auf.</li><li>**-erweitert:** Listet alle erweiterten zugeordneten Benutzer und Gruppen auf. Zuordnungen werden in der Reihenfolge aufgelistet, in der Sie ausgewertet werden. Primäre Zuordnungen, die mit einem Sternchen () gekennzeichnet sind,*werden zuerst aufgelistet, gefolgt von sekundären Zuordnungen, die mit einem "Karat" gekennzeichnet sind `(^)` . </li> <li> * *-Wu `<name>` :** listet die Zuordnung für einen angegebenen Windows-Benutzer auf.</li><li>**-WG `<group>` :** listet die Zuordnung für eine Windows-Gruppe auf.</li><li>**-UU `<name>` :** listet die Zuordnung für einen UNIX-Benutzer auf.</li><li>**-UG `<group>` :** listet die Zuordnung für eine UNIX-Gruppe auf.</li></ul> |
| Sicherung | Speichert Benutzernamenzuordnung Konfiguration und die Zuordnung von Daten in der durch angegebenen Datei `<filename>` . |
| Wiederherstellen | Ersetzt Konfigurations-und Mapping-Daten durch Daten aus der Datei (angegeben durch `<filename>` ), die mit dem **Backup** -Parameter erstellt wurde. |
| adddomainmap | Fügt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne bzw. einem Kennwort und Gruppen Dateien hinzu. Die folgenden Optionen sind für diesen Parameter verfügbar:<ul><li>**-d `<windowsdomain>` :** gibt die Windows-Domäne an, die zugeordnet werden soll.</li><li>**-y `<NISdomain>` :** gibt die NIS-Domäne an, die zugeordnet werden soll. Sie müssen den **-n `<NISserver>` -** Parameter verwenden, um den NIS-Server für die NIS-Domäne anzugeben, die durch die **-y-** Option angegeben wird.</li><li>**-f `<path>` :** gibt den voll qualifizierten Pfad des Verzeichnisses mit den Kennwort-und Gruppen Dateien an, die zugeordnet werden sollen. Die Dateien müssen sich auf dem verwalteten Computer befinden, und Sie können nicht mithilfe von " **mapadmin** " einen Remote Computer zum Einrichten von Zuordnungen auf der Grundlage von Kennwort-und Gruppen Dateien verwalten.</li></ul> |
| removedomainmap | Entfernt eine einfache Zuordnung zwischen einer Windows-Domäne und einer NIS-Domäne. Die folgenden Optionen und Argumente sind für diesen Parameter verfügbar:<ul><li>**-d `<windowsdomain>` :** gibt die Windows-Domäne der zu entfernenden Karte an.</li><li>**-y `<NISdomain>` :** gibt die NIS-Domäne der zu entfernenden Karte an.</li><li>**-alle:** Gibt an, dass alle einfachen Zuordnungen zwischen Windows-und NIS-Domänen entfernt werden sollen. Dadurch werden auch alle einfachen Zuordnungen zwischen einer Windows-Domäne und den Kennwort-und Gruppen Dateien entfernt.</li></ul> |
| listdomainmaps | Listet die Windows-Domänen auf, die NIS-Domänen oder Kennwort-und Gruppen Dateien zugeordnet sind. |

#### <a name="remarks"></a>Hinweise

- Wenn Sie keine Parameter angeben, zeigt der Befehl **mapadmin** die aktuellen Einstellungen für Benutzernamenzuordnung an.

- Für alle Optionen, die einen Benutzer-oder Gruppennamen angeben, können die folgenden Formate verwendet werden:

    - Verwenden Sie für Windows-Benutzer die folgenden Formate: `<domain>\<username>` , `\\<computer>\<username>` , `\<computer>\<username>` oder `<computer>\<username>`

    - Verwenden Sie für Windows-Gruppen die folgenden Formate: `<domain>\<groupname>` , `\\<computer>\<groupname>` , `\<computer>\<groupname>` oder `<computer>\<groupname>`

    - Verwenden Sie für UNIX-Benutzer die folgenden Formate: `<NISdomain>\<username>` , `<username>@<NISdomain>` , `<username>@PCNFS` oder `PCNFS\<username>`

    - Verwenden Sie für UNIX-Gruppen die folgenden Formate: `<NISdomain>\<groupname>` , `<groupname>@<NISdomain>` , `<groupname>@PCNFS` oder `PCNFS\<groupname>`

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
