---
title: gpfixup
description: Referenz Artikel für den Gpfixup-Befehl, mit dem Domänen Namen Abhängigkeiten in Gruppenrichtlinie Objekten und Gruppenrichtlinie links nach einem Domänen Umbenennungs Vorgang korrigiert werden.
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9379efe545544028980cf570de30bc6d3d816c81
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87888565"
---
# <a name="gpfixup"></a>gpfixup

Korrigiert Domänen Namen Abhängigkeiten in Gruppenrichtlinie Objekten und Gruppenrichtlinie links nach einem Domänen Umbenennungs Vorgang. Um diesen Befehl verwenden zu können, müssen Sie Gruppenrichtlinie Management als Feature über Server-Manager installieren.

## <a name="syntax"></a>Syntax

```
gpfixup [/v]
[/olddns:<olddnsname> /newdns:<newdnsname>]
[/oldnb:<oldflatname> /newnb:<newflatname>]
[/dc:<dcname>] [/sionly]
[/user:<username> [/pwd:{<password>|*}]] [/?]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
| --------- |------------ |
| /v | Zeigt detaillierte Statusmeldungen an. Wenn dieser Parameter nicht verwendet wird, werden nur Fehlermeldungen oder eine Zusammenfassungs Statusmeldung mit der Angabe, **Erfolg** oder **Fehler** angezeigt. |
| /olddns:`<olddnsname>` | Gibt den alten DNS-Namen der umbenannten Domäne so an, dass der `<olddnsname>` DNS-Name einer Domäne durch den Domänen Umbenennungs Vorgang geändert wird. Sie können diesen Parameter nur verwenden, wenn Sie auch den **/newdns** -Parameter verwenden, um einen neuen DNS-Domänen Namen anzugeben. |
| /newdns:`<newdnsname>` | Gibt den neuen DNS-Namen der umbenannten Domäne an, als `<newdnsname>` Wenn der Domänen Umbenennungs Vorgang den DNS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie auch den **/olddns** -Parameter verwenden, um den alten DNS-Domänen Namen anzugeben. |
| /oldnb:`<oldflatname>` | Gibt den alten NetBIOS-Namen der umbenannten Domäne so an, dass der `<oldflatname>` NetBIOS-Name einer Domäne durch den Domänen Umbenennungs Vorgang geändert wird. Sie können diesen Parameter nur verwenden, wenn Sie den **/newnb** -Parameter verwenden, um einen neuen NetBIOS-Domänen Namen anzugeben. |
| /newnb:`<newflatname>` | Gibt den neuen NetBIOS-Namen der umbenannten Domäne so an, dass der `<newflatname>` NetBIOS-Name einer Domäne durch den Domänen Umbenennungs Vorgang geändert wird. Sie können diesen Parameter nur verwenden, wenn Sie den **/oldnb** -Parameter verwenden, um den alten NetBIOS-Domänen Namen anzugeben. |
| "/DC`<dcname>` | Stellen Sie eine Verbindung mit dem Domänen Controller namens her `<dcname>` (DNS-Name oder NetBIOS-Name). `<dcname>`muss ein beschreibbares Replikat der Domänen Verzeichnis Partition hosten, wie in einem der folgenden aufgeführt:<ul><li>Der DNS-Name `<newdnsname>` mithilfe von **/newdns**</li><li>Der NetBIOS-Name `<newflatname>` mithilfe von **/newnb**</br>Wenn dieser Parameter nicht verwendet wird, können Sie eine Verbindung mit einem beliebigen Domänen Controller in der umbenannten Domäne herstellen, die von oder angegeben wird `<newdnsname>` `<newflatname>`</li></ul> |
| /sionly | Führt nur die Gruppenrichtlinie Korrektur durch, die sich auf die verwaltete Software Installation bezieht (die Software Installations Erweiterung für Gruppenrichtlinie). Überspringen Sie die Aktionen, mit denen Gruppenrichtlinie Verknüpfungen und die SYSVOL-Pfade in GPOs korrigiert werden. |
| /User`<username>` |Führt diesen Befehl im Sicherheitskontext des Benutzers aus `<username>` , wobei `<username>` im Format Domäne \ Benutzer angegeben ist. Wenn dieser Parameter nicht verwendet wird, wird dieser Befehl als angemeldeter Benutzer ausgeführt. |
| /PWD`{<password> | *}` | Gibt das Kennwort für den Benutzer an. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

### <a name="examples"></a>Beispiele

In diesem Beispiel wird davon ausgegangen, dass Sie bereits einen Domänen Umbenennungs Vorgang durchgeführt haben, in dem Sie den DNS-Namen von **myolddnsname** in **mynewdnsname**und den NetBIOS-Namen von **myoldnetbiosname** in **mynewnetbiosname**geändert haben.

In diesem Beispiel verwenden Sie den **Gpfixup** -Befehl, um eine Verbindung mit dem Domänen Controller namens **mydcdnsname** herzustellen und GPOs und Gruppenrichtlinie Verknüpfungen zu reparieren, indem Sie den alten Domänen Namen aktualisieren, der in die GPOs und Verknüpfungen eingebettet ist. Die Status-und Fehlerausgabe wird in einer Datei mit dem Namen " **Gpfixup. log**" gespeichert.

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

Dieses Beispiel ist mit dem vorherigen identisch, mit dem Unterschied, dass der NetBIOS-Name der Domäne während des Domänen Umbenennungs Vorgangs nicht geändert wurde.

```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Verwalten Active Directory-Domäne umbenennen](/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794869(v=ws.10))
