---
title: mount
description: Referenz Thema für * * * *-
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2e7ef55f5e5b66a0501c62767968a4192880040f
ms.sourcegitcommit: ab64dc83fca28039416c26226815502d0193500c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/01/2020
ms.locfileid: "82723930"
---
# <a name="mount"></a>mount



Zum Einbinden von Network File System (NFS)-Netzwerkfreigaben können Sie **einbinden** verwenden.

## <a name="syntax"></a>Syntax

```
mount [-o <Option>[...]] [-u:<UserName>] [-p:{<Password> | *}] {\\<ComputerName>\<ShareName> | <ComputerName>:/<ShareName>} {<DeviceName> | *}
```

## <a name="description"></a>BESCHREIBUNG

Das Bereitstellungs Befehlszeilen-Hilfsprogramm **bindet das durch** *ShareName* identifizierte Dateisystem ein, das von dem durch den *Computernamen* identifizierten NFS-Server exportiert wurde, und ordnet *das durch den* ersten verfügbaren Treiber Buchstaben **&#42;** angegebene Laufwerk Buchstaben zu. Benutzer können dann auf das exportierte Dateisystem zugreifen, als handele es sich um ein Laufwerk auf dem lokalen Computer. Bei Verwendung ohne Optionen oder Argumente zeigt **Mount** Informationen zu allen bereitgestellten NFS-Dateisystemen an.

Das Hilfsprogramm " **Mount** " ist nur verfügbar, wenn der Client für NFS installiert ist.

Die folgenden Optionen und Argumente können mit dem Hilfsprogramm " **Mount** " verwendet werden.


|          Begriff          |                                                                                                                                                                                                                                                Definition                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -o rsize =\<bufferSize> |                                                                                                                                                                                            Legt die Größe des Lese Puffers in Kilobyte fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32; der Standardwert ist 32 KB.                                                                                                                                                                                            |
| -o wsize =\<bufferSize> |                                                                                                                                                                                           Legt die Größe des Schreib Puffers in Kilobyte fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32; der Standardwert ist 32 KB.                                                                                                                                                                                            |
| -o Timeout =\<Sekunden>  |                                                                                                                                                                       Legt den Timeout Wert für einen Remote Prozedur Aufruf (RPC) in Sekunden fest. Zulässige Werte sind 0,8, 0,9 und jede beliebige ganze Zahl im Bereich 1-60; der Standardwert ist 0,8.                                                                                                                                                                       |
|   -o Retry =\<Anzahl>   |                                                                                                                                                                                             Legt die Anzahl der Wiederholungs Versuche für eine weiche Bereitstellung fest. Zulässige Werte sind ganze Zahlen im Bereich 1-10; der Standardwert ist 1.                                                                                                                                                                                             |
|     -o mtype = {Soft     |                                                                                                                                                                                                                                                  stark                                                                                                                                                                                                                                                   |
|        -o anon         |                                                                                                                                                                                                                                       Wird als anonymer Benutzer bereitgestellt.                                                                                                                                                                                                                                       |
|       -o NOLOCK        |                                                                                                                                                                                                                                Deaktiviert das Sperren (standardmäßig **aktiviert**).                                                                                                                                                                                                                                |
|    -o CaseSensitive    |                                                                                                                                                                                                                         Erzwingt bei Datei Suchvorgängen auf dem Server die Groß-/Kleinschreibung.                                                                                                                                                                                                                          |
| -o FileAccess =\<Mode>  | Gibt den Standard Berechtigungs Modus von neuen Dateien an, die auf der NFS-Freigabe erstellt werden. Geben Sie den *Modus* als dreistellige Zahl in der Form *OGW*an, wobei *o*, *g*und *w* jede Ziffer sind, die den Zugriff auf den Besitzer, die Gruppe und die Welt der Datei darstellt. Die Ziffern müssen zwischen 0-7 und der folgenden Bedeutung liegen:</br>-0: kein Zugriff</br>-1: x (Zugriff ausführen)</br>-2: w (Schreibzugriff)</br>-3: WX</br>-4: r (Lesezugriff)</br>-5: RX</br>-6: RW</br>-7: rwx |
|    -o lang = {EUC-JP     |                                                                                                                                                                                                                                                  EUC-TW                                                                                                                                                                                                                                                  |
|     -u:\<username>     |                                                                                                                                                                             Gibt den Benutzernamen an, der zum Einbinden der Freigabe verwendet werden soll. Wenn einem *Benutzer* Namen kein umgekehrter Schrägstrich (**\\**) vorangestellt ist, wird er als Unix-Benutzername behandelt.                                                                                                                                                                             |
|     -p:\<Kennwort>     |                                                                                                                                                                                          Das Kennwort, das zum Einbinden der Freigabe verwendet werden soll. Wenn Sie ein Sternchen (**&#42;**) verwenden, werden Sie zur Eingabe des Kennworts aufgefordert.                                                                                                                                                                                          |

> [!NOTE]
