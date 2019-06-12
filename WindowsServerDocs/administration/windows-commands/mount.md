---
title: Bereitstellen
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
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
ms.openlocfilehash: 65083ce4b7d04129ff630a7f314c458d7ee378f4
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437247"
---
# <a name="mount"></a>Bereitstellen



Sie können **einbinden** Netzwerkfreigaben für Network File System (NFS) bereitstellen.

## <a name="syntax"></a>Syntax

```
mount [-o <Option>[...]] [-u:<UserName>] [-p:{<Password> | *}] {\\<ComputerName>\<ShareName> | <ComputerName>:/<ShareName>} {<DeviceName> | *}
```

## <a name="description"></a>Beschreibung

Die **einbinden** Befehlszeilen-Hilfsprogramm stellt das Dateisystem identifizierte *ShareName* vom identifizierte NFS-Server exportiert *ComputerName* und ordnet ihn der durch angegebene Laufwerkbuchstabe *DeviceName* oder, wenn ein Sternchen ( **&#42;** ) verwendet wird, nach dem ersten verfügbaren Treiber Buchstaben. Benutzer können dann die exportierte Dateisystem zugreifen, als wäre es ein Laufwerk auf dem lokalen Computer. Bei der Verwendung ohne Optionen oder Argumente **einbinden** zeigt Informationen zu allen bereitgestellten NFS-Dateisysteme.

Die **einbinden** Dienstprogramm ist nur verfügbar, wenn für NFS-Client installiert ist.

Die folgenden Optionen und Argumente können mit verwendet werden die **einbinden** Hilfsprogramm.


|          Begriff          |                                                                                                                                                                                                                                                Definition                                                                                                                                                                                                                                                |
|------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -o rsize=\<buffersize> |                                                                                                                                                                                            Legt die Größe in Kilobytes des Lesepuffers fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32. Der Standardwert ist 32 KB.                                                                                                                                                                                            |
| -o wsize=\<buffersize> |                                                                                                                                                                                           Legt die Größe in KB, der den Schreibpuffer fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32. Der Standardwert ist 32 KB.                                                                                                                                                                                            |
| -o timeout=\<seconds>  |                                                                                                                                                                       Setzt den Timeoutwert in Sekunden für einen Remoteprozeduraufruf (RPC) an. Zulässige Werte sind 0,8 0,9 und eine beliebige ganze Zahl im Bereich von 1 bis 60; Der Standardwert ist 0,8.                                                                                                                                                                       |
|   -o retry=\<number>   |                                                                                                                                                                                             Legt die Anzahl der Wiederholungen bei einer zeitweiligen Bereitstellung ausführt. Zulässige Werte sind ganze Zahlen im Bereich von 1 bis 10. Der Standardwert ist 1.                                                                                                                                                                                             |
|     -o mtype={soft     |                                                                                                                                                                                                                                                  feste}                                                                                                                                                                                                                                                   |
|        -o anon         |                                                                                                                                                                                                                                       Die Bereitstellung als anonymer Benutzer.                                                                                                                                                                                                                                       |
|       -o nolock        |                                                                                                                                                                                                                                Deaktiviert die Sperrung (der Standardwert ist **aktiviert**).                                                                                                                                                                                                                                |
|    -o casesensitive    |                                                                                                                                                                                                                         Erzwingt, dass die Datei Suchvorgänge auf dem Server, die Groß-/Kleinschreibung beachtet werden.                                                                                                                                                                                                                          |
| -o fileaccess=\<mode>  | Gibt den Standard-Berechtigungsmodus neuer Dateien, die auf die NFS-Freigabe erstellt. Geben Sie *Modus* als eine dreistellige Zahl in der Form *Ogw*, wobei *o*, *g*, und *w* sind jeweils eine Ziffer die Zugriff darstellt gewährt der Besitzer der Datei, Gruppe und der ganzen Welt bzw. Die Ziffern muss im Bereich 0-7 mit folgende Bedeutung:</br>-   0: Kein Zugriff</br>– 1: X (führen Sie den Zugriff)</br>– 2: w (Schreibzugriff)</br>-   3: wx</br>-4: R (Lesezugriff)</br>-5: Rx</br>– 6: RW-Medien</br>– 7: Rwx |
|    -o lang={euc-jp     |                                                                                                                                                                                                                                                  EUC-tw                                                                                                                                                                                                                                                  |
|     -u:\<Benutzername >     |                                                                                                                                                                             Gibt den Benutzernamen ein, verwenden Sie für das Einbinden der Freigabe an. Wenn *Benutzername* nicht durch einen umgekehrten Schrägstrich vorangestellt ist ( **\\** ), wird er als einen UNIX-Benutzernamen behandelt.                                                                                                                                                                             |
|     -p:\<Kennwort >     |                                                                                                                                                                                          Das Kennwort für das Einbinden der Freigabe. Wenn Sie ein Sternchen verwenden ( **&#42;** ), Sie werden aufgefordert, das Kennwort.                                                                                                                                                                                          |

> [!NOTE]
