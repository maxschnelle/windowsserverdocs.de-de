---
title: gpfixup
description: Windows-Befehle Thema ****-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 2b145410-fc75-4526-932d-f16b7ee3aaef
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e0f1ce2e050a3d741f9b2f7a5cce9d2988716106
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80842553"
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

#### <a name="parameters"></a>Parameter

|       Parameter       |                                                                                                                                                                                                                               Beschreibung                                                                                                                                                                                                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          /v           |                                                                                                                                                      Zeigt detaillierte Statusmeldungen an.</br>Wenn dieser Parameter nicht verwendet wird, werden nur Fehlermeldungen oder eine Zusammenfassungs Statusmeldung mit **Erfolg** oder **Fehler angezeigt.**                                                                                                                                                       |
| /olddns:\<olddnsname > |                                                                                                           Gibt den alten DNS-Namen der umbenannten Domäne als *\<olddnsname >* an, wenn der Domänen Umbenennungs Vorgang den DNS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie auch den **/newdns** -Parameter verwenden, um einen neuen DNS-Domänen Namen anzugeben.                                                                                                            |
| /newdns:\<newdnsname > |                                                                                                          Gibt den neuen DNS-Namen der umbenannten Domäne als *\<newdnsname >* an, wenn der Domänen Umbenennungs Vorgang den DNS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie auch den **/olddns** -Parameter verwenden, um den alten DNS-Domänen Namen anzugeben.                                                                                                           |
| /oldnb:\<oldflatname > |                                                                                                        Gibt den alten NetBIOS-Namen der umbenannten Domäne als *\<oldflatname >* an, wenn der Domänen Umbenennungs Vorgang den NetBIOS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie den **/newnb** -Parameter verwenden, um einen neuen NetBIOS-Domänen Namen anzugeben.                                                                                                        |
| /newnb:\<newflatname > |                                                                                                       Gibt den neuen NetBIOS-Namen der umbenannten Domäne als *\<newflatname >* an, wenn der Domänen Umbenennungs Vorgang den NetBIOS-Namen einer Domäne ändert. Sie können diesen Parameter nur verwenden, wenn Sie den **/oldnb** -Parameter verwenden, um den alten NetBIOS-Domänen Namen anzugeben.                                                                                                       |
|     "/DC:\<DCNAME >     | Stellen Sie eine Verbindung mit dem Domänen Controller namens *\<DCNAME >* (DNS-Name oder NetBIOS-Name) her. *\<DCNAME->* muss ein beschreibbares Replikat der Domänen Verzeichnis Partition hosten, wie in einem der folgenden aufgeführt:</br>: Der DNS-Name *\<newdnsname >* mithilfe von **/newdns**</br>: Der NetBIOS-Name *\<newflatname >* mithilfe von **/newnb**</br>Wenn dieser Parameter nicht verwendet wird, stellen Sie eine Verbindung mit einem beliebigen Domänen Controller in der umbenannten Domäne her, der durch *\<newdnsname >* oder *\<newflatname >* angegeben wird. |
|        /sionly        |                                                                                                                           Führt nur die Gruppenrichtlinie Korrektur durch, die sich auf die verwaltete Software Installation bezieht (die Software Installations Erweiterung für Gruppenrichtlinie). Überspringen Sie die Aktionen, mit denen Gruppenrichtlinie Verknüpfungen und die SYSVOL-Pfade in GPOs korrigiert werden.                                                                                                                           |
|   /User:\<Benutzername >   |                                                                                                                                   Führt diesen Befehl im Sicherheitskontext des Benutzers *\<username >* aus, wobei *\<username >* im Format Domäne \ Benutzer vorliegt.</br>Wenn dieser Parameter nicht verwendet wird, wird dieser Befehl von als angemeldeter Benutzer ausgeführt.                                                                                                                                    |
|   /PWD: {\<Password >   |                                                                                                                                                                                                                                   \*}                                                                                                                                                                                                                                   |
|          /?           |                                                                                                                                                                                                                  Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                   |

## <a name="remarks"></a>Hinweise

-   Der **Gpfixup** -Befehl ist in Windows Server 2008 R2 und Windows Server 2008 mit Ausnahme von Server Core-Installationen verfügbar.
-   Obwohl die Gruppenrichtlinien-Verwaltungskonsole (GPMC) mit Windows Server 2008 R2 und Windows Server 2008 verteilt ist, müssen Sie Gruppenrichtlinie Management als Feature über Server-Manager installieren.

## <a name="examples"></a><a name=BKMK_Examples></a>Beispiele

In diesem Beispiel wird davon ausgegangen, dass Sie bereits einen Domänen Umbenennungs Vorgang durchgeführt haben, in dem Sie den DNS-Namen von **myolddnsname** in **mynewdnsname**und den NetBIOS-Namen von **myoldnetbiosname** in **mynewnetbiosname**geändert haben. In diesem Beispiel verwenden Sie den **Gpfixup** -Befehl, um eine Verbindung mit dem Domänen Controller namens **mydcdnsname** herzustellen und GPOs und Gruppenrichtlinie Verknüpfungen zu reparieren, indem Sie den alten Domänen Namen aktualisieren, der in die GPOs und Verknüpfungen eingebettet ist. Die Status-und Fehlerausgabe wird in einer Datei mit dem Namen " **Gpfixup. log**" gespeichert.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
Dieses Beispiel ist mit dem vorherigen identisch, mit dem Unterschied, dass der NetBIOS-Name der Domäne während des Domänen Umbenennungs Vorgangs nicht geändert wurde.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

## <a name="additional-references"></a>Weitere Verweise

-   [Verwalten Active Directory-Domäne umbenennen](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [Gruppenrichtlinie-TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   - [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)