---
title: gpfixup
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: fdbe9873cc15866037c4688aaac89095e4a85dec
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59889421"
---
# <a name="gpfixup"></a>gpfixup



Beheben Sie Namen domänenabhängigkeiten in Group Policy Objects und Gruppenrichtlinien verknüpft, nach dem Umbenennungsvorgang für einer Domäne. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).

## <a name="syntax"></a>Syntax

```
Gpfixup [/v] 
[/olddns:<OLDDNSNAME> /newdns:<NEWDNSNAME>] 
[/oldnb:<OLDFLATNAME> /newnb:<NEWFLATNAME>] 
[/dc:<DCNAME>] [/sionly] 
[/user:<USERNAME> [/pwd:{<PASSWORD>|*}]] [/?]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/v|Zeigt detaillierte statusmeldungen an.</br>Wenn dieser Parameter nicht verwendet wird, nur Fehlermeldungen oder eine Statusübersicht Nachricht **Erfolg** oder **Fehler** angezeigt wird.|
|/olddns:\<OLDDNSNAME>|Gibt an, der alte DNS-Name der Domäne umbenannt als  *\<OLDDNSNAME >* die domänenumbenennung Änderungen bei der DNS-Name einer Domäne. Sie können diesen Parameter nur, wenn Sie auch verwenden, verwenden die **/newdns** Parameter, um einen neuen DNS-Domänennamen anzugeben.|
|/newdns:\<NEWDNSNAME>|Gibt den neuen DNS-Namen der Domäne umbenannt als  *\<NEWDNSNAME >* die domänenumbenennung Änderungen bei der DNS-Name einer Domäne. Sie können diesen Parameter nur, wenn Sie auch verwenden, verwenden die **/olddns** Parameter, um den alten DNS-Domänennamen anzugeben.|
|/oldnb:\<OLDFLATNAME>|Gibt den alten NetBIOS-Namen der Domäne umbenannt als  *\<OLDFLATNAME >* Wenn sich die domänenumbenennung ändert den NetBIOS-Namen einer Domäne. Verwenden Sie diesen Parameter nur, wenn Sie verwenden die **/newnb** Parameter, um einen neuen NetBIOS-Domänennamen anzugeben.|
|/newnb:\<NEWFLATNAME>|Gibt den neuen NetBIOS-Namen der Domäne umbenannt als  *\<NEWFLATNAME >* Wenn sich die domänenumbenennung ändert den NetBIOS-Namen einer Domäne. Verwenden Sie diesen Parameter nur, wenn Sie verwenden die **/oldnb** Parameter, um den alten NetBIOS-Domänennamen anzugeben.|
|/dc:\<DCNAME>|Herstellen einer Verbindung mit dem Namen der Domänencontroller mit  *\<DCNAME >* (einen DNS-Namen oder einen NetBIOS-Namen). *\<DCNAME >* muss ein beschreibbares Replikat der Domänenverzeichnispartition hosten, wie durch eine der folgenden angezeigt:</br>– Der DNS-Name  *\<NEWDNSNAME >* mit **/newdns**</br>– Der NetBIOS-Namen  *\<NEWFLATNAME >* mit **/newnb**</br>Wenn dieser Parameter nicht verwendet wird, Herstellen einer Verbindung mit einem beliebigen Domänencontroller in der umbenannten Domäne erkennbar  *\<NEWDNSNAME >* oder  *\<NEWFLATNAME >*.|
|/sionly|Führt nur die Gruppenrichtlinien-Lösung, die mit verwalteter Softwareinstallation (Installation der Clientsoftware Erweiterung der Gruppenrichtlinie) verknüpft. Überspringen Sie die Aktionen, die Gruppenrichtlinien-Verknüpfungen und der SYSVOL-Pfade in Gruppenrichtlinienobjekten beheben.|
|/ User:\<Benutzername >|Führt diesen Befehl im Sicherheitskontext des Benutzers  *\<Benutzername >*, wobei  *\<Benutzername >* befindet sich in dem Format "Domäne\Benutzer".</br>Wenn dieser Parameter nicht verwendet wird, wird dieser Befehl wie dem angemeldeten Benutzer ausgeführt.|
|/pwd:{\<PASSWORD>|*}|Gibt das Kennwort für den anderen Sicherheitskontext angegeben werden, mithilfe von **/User**. Wenn **&#42;** angegeben anstelle eines Kennworts, werden Sie aufgefordert, ein Kennwort.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **Gpfixup** Befehl ist verfügbar in Windows Server 2008 R2 und Windows Server 2008, außer auf Server Core-Installationen.
-   Auch wenn die Gruppe Gruppenrichtlinien-Verwaltungskonsole (GPMC) mit Windows Server 2008 R2 und Windows Server 2008 verteilt wird, müssen Sie die Gruppenrichtlinien-Verwaltungskonsole als Feature über Server-Manager installieren.

## <a name="BKMK_Examples"></a>Beispiele für

In diesem Beispiel wird davon ausgegangen, dass Sie bereits ein Umbenennungsvorgang für die Domäne ausgeführt haben, in dem Sie den DNS-Namen von geändert **MyOldDnsName** zu **MyNewDnsName**, und den NetBIOS-Namen aus  **MyOldNetBIOSName** zu **MyNewNetBIOSName**. In diesem Beispiel verwenden Sie die **Gpfixup** -Befehl zum Verbinden mit dem Domänencontroller, die mit dem Namen **MyDcDnsName** und reparieren Sie Gruppenrichtlinienobjekte und Gruppenrichtlinieneinstellungen Links, indem Sie den alten Domänennamen aktualisieren, die in den GPOs und Links eingebettet. Status und die Fehlerausgabe wird gespeichert, in eine Datei mit dem Namen **gpfixup.log**.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /oldnb:MyOldNetBIOSName /newnb:MyNewNetBIOSName /dc:MyDcDnsName 2>&1 >gpfixup.log
```
In diesem Beispiel ist identisch mit dem vorherigen Beispiel, mit dem Unterschied, dass es wird davon ausgegangen, dass die NetBIOS-Namen der Domäne nicht geändert wurde, während der Domäne Umbenennungsvorgang.
```
gpfixup /olddns: MyOldDnsName /newdns:MyNewDnsName /dc:MyDcDnsName 2>&1 >gpfixup.log
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Umbenennen der Verwaltung von Active Directory-Domänen](https://go.microsoft.com/fwlink/?LinkId=198385)
-   [Gruppenrichtlinien-TechCenter](https://go.microsoft.com/fwlink/?LinkID=145531)
-   [Befehlszeilensyntax](command-line-syntax-key.md)