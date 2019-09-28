---
title: Bereitstellen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9a225c847055198a9a48962a3b40969556f10ec1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71373593"
---
# <a name="mount"></a>Bereitstellen



Zum Einbinden von Network File System (NFS)-Netzwerkfreigaben können Sie **einbinden** verwenden.

## <a name="syntax"></a>Syntax

```
mount [-o <Option>[...]] [-u:<UserName>] [-p:{<Password> | *}] {\\<ComputerName>\<ShareName> | <ComputerName>:/<ShareName>} {<DeviceName> | *}
```

## <a name="description"></a>Beschreibung

Mit dem Befehlszeilen-Hilfsprogramm **Mount** wird das durch *ShareName* identifizierte Dateisystem bereitgestellt, das von dem durch den *Computername* identifizierten NFS-Server exportiert wurde, und dem Laufwerk Buchstaben, der von *DeviceName* angegeben wird, oder, wenn ein Sternchen ( **&#42;** ) verwendet wird, wird der erste verfügbare Treiber Buchstabe verwendet. Benutzer können dann auf das exportierte Dateisystem zugreifen, als handele es sich um ein Laufwerk auf dem lokalen Computer. Bei Verwendung ohne Optionen oder Argumente zeigt **Mount** Informationen zu allen bereitgestellten NFS-Dateisystemen an.

Das Hilfsprogramm " **Mount** " ist nur verfügbar, wenn der Client für NFS installiert ist.

Die folgenden Optionen und Argumente können mit dem Hilfsprogramm " **Mount** " verwendet werden.


|          Begriff          |                                                                                                                                                                                                                                                Definition                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -o rsize = \<buffersize > |                                                                                                                                                                                            Legt die Größe des Lese Puffers in Kilobyte fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32; der Standardwert ist 32 KB.                                                                                                                                                                                            |
| -o wsize = \<buffersize > |                                                                                                                                                                                           Legt die Größe des Schreib Puffers in Kilobyte fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32; der Standardwert ist 32 KB.                                                                                                                                                                                            |
| -o Timeout = \<seconds >  |                                                                                                                                                                       Legt den Timeout Wert für einen Remote Prozedur Aufruf (RPC) in Sekunden fest. Zulässige Werte sind 0,8, 0,9 und jede beliebige ganze Zahl im Bereich 1-60; der Standardwert ist 0,8.                                                                                                                                                                       |
|   -o Retry = \<number >   |                                                                                                                                                                                             Legt die Anzahl der Wiederholungs Versuche für eine weiche Bereitstellung fest. Zulässige Werte sind ganze Zahlen im Bereich 1-10; der Standardwert ist 1.                                                                                                                                                                                             |
|     -o mtype = {Soft     |                                                                                                                                                                                                                                                  stark                                                                                                                                                                                                                                                   |
|        -o anon         |                                                                                                                                                                                                                                       Wird als anonymer Benutzer bereitgestellt.                                                                                                                                                                                                                                       |
|       -o NOLOCK        |                                                                                                                                                                                                                                Deaktiviert das Sperren (standardmäßig **aktiviert**).                                                                                                                                                                                                                                |
|    -o CaseSensitive    |                                                                                                                                                                                                                         Erzwingt bei Datei Suchvorgängen auf dem Server die Groß-/Kleinschreibung.                                                                                                                                                                                                                          |
| -o FileAccess = \<mode >  | Gibt den Standard Berechtigungs Modus von neuen Dateien an, die auf der NFS-Freigabe erstellt werden. Geben Sie den *Modus* als dreistellige Zahl in der Form *OGW*an, wobei *o*, *g*und *w* jede Ziffer sind, die den Zugriff auf den Besitzer, die Gruppe und die Welt der Datei darstellt. Die Ziffern müssen zwischen 0-7 und der folgenden Bedeutung liegen:</br>1,0 Kein Zugriff</br>-1: x (Zugriff ausführen)</br>-2: w (Schreibzugriff)</br>-3: WX</br>-4: r (Lesezugriff)</br>-5: RX</br>-6: RW</br>-7: rwx |
|    -o lang = {EUC-JP     |                                                                                                                                                                                                                                                  EUC-TW                                                                                                                                                                                                                                                  |
|     -u: \<username >     |                                                                                                                                                                             Gibt den Benutzernamen an, der zum Einbinden der Freigabe verwendet werden soll. Wenn einem *Benutzer* Namen kein umgekehrter Schrägstrich ( **\\** ) vorangestellt ist, wird er als Unix-Benutzername behandelt.                                                                                                                                                                             |
|     -p: \<password >     |                                                                                                                                                                                          Das Kennwort, das zum Einbinden der Freigabe verwendet werden soll. Wenn Sie ein Sternchen ( **&#42;** ) verwenden, werden Sie zur Eingabe des Kennworts aufgefordert.                                                                                                                                                                                          |

> [!NOTE]
