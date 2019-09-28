---
title: gpfixup
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e32427369f1664476c81a81353ae8869ec0c2ff3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71375668"
---
# <a name="gpfixup"></a>gpfixup



Beheben von Domänen Namen Abhängigkeiten in Gruppenrichtlinie Objekten und Gruppenrichtlinie links nach einem Domänen Umbenennungs Vorgang. Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLATNAME> /newnb:<NEWFLATNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWORD>|*}]] [/?]
```

### <a name="parameters"></a>Parameter

|       Parameter       |                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /v           |                                                                                                                                                      Zeigt detaillierte Statusmeldungen an.</br>Wenn dieser Parameter nicht verwendet wird, werden nur Fehlermeldungen oder eine Zusammenfassungs Statusmeldung mit **Erfolg** oder **Fehler angezeigt.**                                                                                                                                                       |
| /olddns: \<olddnsname > |                                                                                                           Gibt den alten DNS-Namen der umbenannten Domäne als *\<olddnsname >* an, wenn der Domänen Umbenennungs Vorgang den DNS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie auch den **/newdns** -Parameter verwenden, um einen neuen DNS-Domänen Namen anzugeben.                                                                                                            |
| /newdns: \<newdnsname > |                                                                                                          Gibt den neuen DNS-Namen der umbenannten Domäne als *\<newdnsname >* an, wenn der Domänen Umbenennungs Vorgang den DNS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie auch den **/olddns** -Parameter verwenden, um den alten DNS-Domänen Namen anzugeben.                                                                                                           |
| /oldnb: \<oldflatname > |                                                                                                        Gibt den alten NetBIOS-Namen der umbenannten Domäne als *\<oldflatname >* an, wenn der Domänen Umbenennungs Vorgang den NetBIOS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie den **/newnb** -Parameter verwenden, um einen neuen NetBIOS-Domänen Namen anzugeben.                                                                                                        |
| /newnb: \<newflatname > |                                                                                                       Gibt den neuen NetBIOS-Namen der umbenannten Domäne als *\<newflatname >* an, wenn der Domänen Umbenennungs Vorgang den NetBIOS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie den **/oldnb** -Parameter verwenden, um den alten NetBIOS-Domänen Namen anzugeben.                                                                                                       |
|     "/DC: \<dcname >     | Stellen Sie eine Verbindung mit dem Domänen Controller mit dem Namen *\<dcname >* (DNS-Name oder NetBIOS-Name) her. *\<dcname >* muss ein beschreibbares Replikat der Domänen Verzeichnis Partition hosten, wie in einem der folgenden aufgeführt:</br>: Der DNS *-Name \<newdnsname >* mithilfe von **/newdns**</br>: Der NetBIOS-Name *\<newflatname >* mithilfe von **/newnb**</br>Wenn dieser Parameter nicht verwendet wird, stellen Sie eine Verbindung mit einem beliebigen Domänen Controller in der umbenannten Domäne her, der durch *\<newdnsname >* oder *\<newflatname >* angegeben wird. |
|        /sionly        |                                                                                                                           Führt nur die Gruppenrichtlinie Korrektur durch, die sich auf die verwaltete Software Installation bezieht (die Software Installations Erweiterung für Gruppenrichtlinie). Überspringen Sie die Aktionen, mit denen Gruppenrichtlinie Verknüpfungen und die SYSVOL-Pfade in GPOs korrigiert werden.                                                                                                                           |
|   /User: \<username >   |                                                                                                                                   Führt diesen Befehl im Sicherheitskontext des Benutzers *\<username >* aus, wobei *\<username >* im Format Domäne \ Benutzer vorliegt.</br>Wenn dieser Parameter nicht verwendet wird, wird dieser Befehl von als angemeldeter Benutzer ausgeführt.                                                                                                                                    |
|   /PWD: {\<password >   |                                                                                                                                                                                                                                   \*}                                                                                                                                                                                                                                   |
|          /?           |                                                                                                                                                                                                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                   |

## <a name="remarks"></a>Hinweise

-   Der **Gpfixup** -Befehl ist in Windows Server 2008 R2 und Windows Server 2008 mit Ausnahme von Server Core-Installationen verfügbar.
-   Obwohl die Gruppenrichtlinien-Verwaltungskonsole (GPMC) mit Windows Server 2008 R2 und Windows Server 2008 verteilt ist, müssen Sie Gruppenrichtlinie Management als Feature über Server-Manager installieren.

## <a name="BKMK_Examples"></a>Beispiele

In diesem Beispiel wird davon ausgegangen, dass Sie bereits einen Domänen Umbenennungs Vorgang durchgeführt haben, in dem Sie den DNS-Namen von **myolddnsname** in **mynewdnsname**und den NetBIOS-Namen von **myoldnetbiosname** in **mynewnetbiosname**geändert haben. In diesem Beispiel verwenden Sie den **Gpfixup** -Befehl, um eine Verbindung mit dem Domänen Controller namens **mydcdnsname** herzustellen und GPOs und Gruppenrichtlinie Verknüpfungen zu reparieren, indem Sie den alten Domänen Namen aktualisieren, der in die GPOs und Verknüpfungen eingebettet ist. Die Status-und Fehlerausgabe wird in einer Datei mit dem Namen " **Gpfixup. log**" gespeichert.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
Dieses Beispiel ist mit dem vorherigen identisch, mit dem Unterschied, dass der NetBIOS-Name der Domäne während des Domänen Umbenennungs Vorgangs nicht geändert wurde.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Verwalten Active Directory-Domäne umbenennen](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [Gruppenrichtlinie-TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)