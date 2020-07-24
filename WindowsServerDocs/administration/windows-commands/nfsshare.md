---
title: nfsshare
description: Referenz Artikel für den nfsshare-Befehl, der NFS-Freigaben (Network File System) steuert.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 437a2615-335a-442f-9713-d50d5f3983a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9db04752ad7982f78dc72c02108fe706cdf2fa04
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86956762"
---
# <a name="nfsshare"></a>nfsshare

Steuert NFS-Freigaben (Network File System). Der Befehl wird ohne Parameter verwendet und zeigt alle NFS-Freigaben (Network File System) an, die vom Server für NFS exportiert wurden.

## <a name="syntax"></a>Syntax

```
nfsshare <sharename>=<drive:path> [-o <option=value>...]
nfsshare {<sharename> | <drive>:<path> | * } /delete
```

### <a name="parameters"></a>Parameter

| Parameter | Beschreibung |
| --------- | ----------- |
| -o anon =`{yes|no}` | Gibt an, ob anonyme (nicht zugeordnete) Benutzer auf das Freigabe Verzeichnis zugreifen können. |
| -o RW =`[<host>[:<host>]...]` | Bietet Lese-/Schreibzugriff auf das freigegebene Verzeichnis durch die Hosts oder Client Gruppen, die vom *Host*angegeben werden. Host-und Gruppennamen müssen mit einem Doppelpunkt (**:**) getrennt werden. Wenn der *Host* nicht angegeben wird, erhalten alle Hosts und Client Gruppen (außer den mit der Option **RO** angegebenen) Lese-/Schreibzugriff. Wenn weder die **RO** -noch die **RW** -Option festgelegt ist, haben alle Clients Lese-/Schreibzugriff auf das freigegebene Verzeichnis. |
| -o Ro =`[<host>[:<host>]...]` | Bietet schreibgeschützten Zugriff auf das freigegebene Verzeichnis durch die Hosts oder Client Gruppen, die vom *Host*angegeben werden. Host-und Gruppennamen müssen mit einem Doppelpunkt (**:**) getrennt werden. Wenn der *Host* nicht angegeben wird, erhalten alle Clients (außer den mit der Option **RW** angegebenen) schreibgeschützten Zugriff. Wenn die Option " **RO** " für mindestens einen Client festgelegt ist, die Option " **RW** " jedoch nicht festgelegt ist, haben nur die mit der Option " **RO** " angegebenen Clients Zugriff auf das freigegebene Verzeichnis. |
| -o Encoding =`{euc-jp|euc-tw|euc-kr|shift-jis|Big5|Ksc5601|Gb2312-80|Ansi)` | Gibt die sprach Codierung an, die auf einer NFS-Freigabe konfiguriert werden soll. Sie können nur eine Sprache auf der Freigabe verwenden. Dieser Wert kann einen der folgenden Werte enthalten:<ul><li>**EUC-JP:** Japanisch</li><li>**EUC-TW:** Chinesisch</li><li>**EUC-KR:** Koreanisch</li><li>**Shift-JIS:** Japanisch</li><li>**Big5:** Chinesisch</li><li>**Ksc5601:** Koreanisch</li><li>**GB2312-80:** Vereinfachtes Chinesisch</li><li>**ANSI:** ANSI-codiert</li></ul> |
| -o anongid =`<gid>` | Gibt an, dass anonyme (nicht zugeordnete) Benutzer auf das Freigabe Verzeichnis mithilfe von *gid* als Gruppen Bezeichner (GID) zugreifen. Der Standardwert ist **-2**. Die anonyme gid wird verwendet, wenn der Besitzer einer Datei, die im Besitz eines nicht zugeordneten Benutzers ist, gemeldet wird, auch wenn der anonyme Zugriff deaktiviert ist. |
| -o anonuid =`<uid>` | Gibt an, dass anonyme (nicht zugeordnete) Benutzer mithilfe von *UID* als Benutzer-ID (UID) auf das Freigabe Verzeichnis zugreifen. Der Standardwert ist **-2**. Die anonyme UID wird verwendet, wenn der Besitzer einer Datei, die im Besitz eines nicht zugeordneten Benutzers ist, gemeldet wird, auch wenn der anonyme Zugriff deaktiviert ist. |
| -o root =`[<host>[:<host>]...]` | Ermöglicht den Stamm Zugriff auf das freigegebene Verzeichnis durch die Hosts oder Client Gruppen, die durch den *Host*angegeben werden. Host-und Gruppennamen müssen mit einem Doppelpunkt (**:**) getrennt werden. Wenn der *Host* nicht angegeben wird, erhalten alle Clients Zugriff auf den Stamm. Wenn die **root** -Option nicht festgelegt ist, haben keine Clients Stamm Zugriff auf das freigegebene Verzeichnis. |
| /delete | Wenn *ShareName* oder `<drive>:<path>` angegeben wird, löscht dieser Parameter die angegebene Freigabe. Wenn ein Platzhalter (*) angegeben wird, löscht dieser Parameter alle NFS-Freigaben. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn *ShareName* als einziger Parameter angegeben ist, werden mit diesem Befehl die Eigenschaften der von *ShareName*identifizierten NFS-Freigabe aufgelistet.

- Wenn *ShareName* und `<drive>:<path>` verwendet werden, exportiert dieser Befehl den von identifizierten Ordner `<drive>:<path>` als *ShareName*. Wenn Sie die Option **/Delete** verwenden, ist der angegebene Ordner für NFS-Clients nicht mehr verfügbar.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Dienste für Network File System-Befehlsreferenz](services-for-network-file-system-command-reference.md)

- [Referenz zu NFS-Cmdlets](/powershell/module/nfs)
