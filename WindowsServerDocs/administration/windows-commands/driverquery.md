---
title: driverquery
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 993c05a930a7702880af23fcfa7c19a43aa8b22b
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82720833"
---
# <a name="driverquery"></a>driverquery



Ermöglicht es einem Administrator, eine Liste der installierten Gerätetreiber und deren Eigenschaften anzuzeigen. Bei Verwendung ohne Parameter wird die Ausführung von **driverquery** auf dem lokalen Computer ausgeführt.



## <a name="syntax"></a>Syntax

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

### <a name="parameters"></a>Parameter

|         Parameter         |                                                                                                                                         BESCHREIBUNG                                                                                                                                          |
|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s \<System>        |                                                                                      Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der lokale Computer.                                                                                       |
| /u [\<Domänen>\]<Username> | Führt den Befehl mit den Anmelde Informationen des Benutzerkontos entsprechend der Angabe durch den *Benutzer* oder den *Domänen*\*Benutzer aus<em>. \* \*Standardmäßig verwendet/s</em> \* die Anmelde Informationen des Benutzers, der zurzeit auf dem Computer angemeldet ist, von dem der Befehl ausgegeben wird. **/u** kann nur verwendet werden, wenn **/s** angegeben wird. |
|      /p \<Password>       |                                                                           Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. **/p** kann nur verwendet werden, wenn **/u** angegeben wird.                                                                            |
|        /FO {Table         |                                                                                                                                             list                                                                                                                                             |
|            /nh            |                                                                                      Lässt die Kopfzeile der angezeigten Treiber Informationen aus. Ungültig, wenn der **/FO** -Parameter auf **List**festgelegt ist.                                                                                      |
|            /v             |                                                                                                               Zeigt die ausführliche Ausgabe an. **/v** ist für signierte Treiber nicht gültig.                                                                                                               |
|            /Si            |                                                                                                                          Enthält Informationen zu signierten Treibern.                                                                                                                          |
|            /?             |                                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                             |

## <a name="examples"></a>Beispiele

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

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)