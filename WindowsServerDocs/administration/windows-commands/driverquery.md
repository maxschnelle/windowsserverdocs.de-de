---
title: driverquery
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d44a1be300b7178bc2271187344c2fc4ab8815e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71377654"
---
# <a name="driverquery"></a>driverquery



Ermöglicht es einem Administrator, eine Liste der installierten Gerätetreiber und deren Eigenschaften anzuzeigen. Bei Verwendung ohne Parameter wird die Ausführung von **driverquery** auf dem lokalen Computer ausgeführt.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

## <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                         Beschreibung                                                                                                                                          |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s \<System >        |                                                                                      Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der lokale Computer.                                                                                       |
| /u [\<Domänen >\]<Username> | Führt den Befehl mit den Anmelde Informationen des Benutzerkontos aus, die von *Benutzer* -oder *Domänen*\*Benutzer angegeben wurden<em>. Standardmäßig verwendet \*\*/s</em> -\* die Anmelde Informationen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird. **/u** kann nur verwendet werden, wenn **/s** angegeben wird. |
|      /p \<Kennwort >       |                                                                           Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. **/p** kann nur verwendet werden, wenn **/u** angegeben wird.                                                                            |
|        /FO {Table         |                                                                                                                                             list                                                                                                                                             |
|            /nh            |                                                                                      Lässt die Kopfzeile der angezeigten Treiber Informationen aus. Ungültig, wenn der **/FO** -Parameter auf **List**festgelegt ist.                                                                                      |
|            /v             |                                                                                                               Zeigt die ausführliche Ausgabe an. **/v** ist für signierte Treiber nicht gültig.                                                                                                               |
|            /Si            |                                                                                                                          Enthält Informationen zu signierten Treibern.                                                                                                                          |
|            /?             |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um eine Liste der installierten Gerätetreiber auf dem lokalen Computer anzuzeigen:
```
driverquery 
```
Geben Sie Folgendes ein, um die Ausgabe in einem CSV-Format (Comma-Separated Values) anzuzeigen:
```
driverquery /fo csv 
```
Um die Kopfzeile in der Ausgabe auszublenden, geben Sie Folgendes ein:
```
driverquery /nh 
```
Geben Sie Folgendes ein, um den Befehl " **driverquery** " auf einem Remote Server mit dem Namen **Server1** mit ihren aktuellen Anmelde Informationen auf dem lokalen Computer zu verwenden:
```
driverquery /s server1
```
Wenn Sie den Befehl " **driverquery** " auf einem Remote Server mit dem Namen **Server1** mithilfe der Anmelde Informationen für **User1** im Domänen- **Maindom**verwenden möchten, geben Sie
```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)