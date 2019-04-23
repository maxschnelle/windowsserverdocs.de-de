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
ms.openlocfilehash: f9d13f5eddef80d99c11fe59c6bd5e589fa67546
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858371"
---
# <a name="mount"></a>Bereitstellen



Sie können **einbinden** Netzwerkfreigaben für Network File System (NFS) bereitstellen.

## <a name="syntax"></a>Syntax

```
mount [-o <Option>[...]] [-u:<UserName>] [-p:{<Password> | *}] {\\<ComputerName>\<ShareName> | <ComputerName>:/<ShareName>} {<DeviceName> | *}
```

## <a name="description"></a>Beschreibung

Die **einbinden** Befehlszeilen-Hilfsprogramm stellt das Dateisystem identifizierte *ShareName* vom identifizierte NFS-Server exportiert *ComputerName* und ordnet ihn der durch angegebene Laufwerkbuchstabe *DeviceName* oder, wenn ein Sternchen (**&#42;**) verwendet wird, nach dem ersten verfügbaren Treiber Buchstaben. Benutzer können dann die exportierte Dateisystem zugreifen, als wäre es ein Laufwerk auf dem lokalen Computer. Bei der Verwendung ohne Optionen oder Argumente **einbinden** zeigt Informationen zu allen bereitgestellten NFS-Dateisysteme.

Die **einbinden** Dienstprogramm ist nur verfügbar, wenn für NFS-Client installiert ist.

Die folgenden Optionen und Argumente können mit verwendet werden die **einbinden** Hilfsprogramm.

|Begriff|Definition|
|----|----------|
|-o rsize=\<buffersize>|Legt die Größe in Kilobytes des Lesepuffers fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32. Der Standardwert ist 32 KB.|
|-o wsize=\<buffersize>|Legt die Größe in KB, der den Schreibpuffer fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32. Der Standardwert ist 32 KB.|
|-o timeout=\<seconds>|Setzt den Timeoutwert in Sekunden für einen Remoteprozeduraufruf (RPC) an. Zulässige Werte sind 0,8 0,9 und eine beliebige ganze Zahl im Bereich von 1 bis 60; Der Standardwert ist 0,8.|
|-o retry=\<number>|Legt die Anzahl der Wiederholungen bei einer zeitweiligen Bereitstellung ausführt. Zulässige Werte sind ganze Zahlen im Bereich von 1 bis 10. Der Standardwert ist 1.|
|-o mtype={soft | feste}|Bestimmt den Mount-Typ (der Standardwert ist **vorläufig**). Unabhängig vom Bereitstellungstyp **einbinden** zurück, wenn sie sofort die Freigabe Bereitstellung ist nicht möglich. Sobald die Freigabe erfolgreich, jedoch bereitgestellt wurde, wenn der Bereitstellungstyp ist **schwer**, Client für NFS wird weiterhin versucht, auf die Freigabe zugreifen, bis dies erfolgreich ist. Daher ist der NFS-Server nicht verfügbar, alle Windows-Programme, die versuchen, Zugriff auf die Dateifreigabe erscheint reagiert werden soll, oder "abstürzt", wenn der Bereitstellungstyp ist **schwer**.|
|-o anon|Die Bereitstellung als anonymer Benutzer.|
|-o nolock|Deaktiviert die Sperrung (der Standardwert ist **aktiviert**).|
|-o casesensitive|Erzwingt, dass die Datei Suchvorgänge auf dem Server, die Groß-/Kleinschreibung beachtet werden.|
|-o fileaccess=\<mode>|Gibt den Standard-Berechtigungsmodus neuer Dateien, die auf die NFS-Freigabe erstellt. Geben Sie *Modus* als eine dreistellige Zahl in der Form *Ogw*, wobei *o*, *g*, und *w* sind jeweils eine Ziffer die Zugriff darstellt gewährt der Besitzer der Datei, Gruppe und der ganzen Welt bzw. Die Ziffern muss im Bereich 0-7 mit folgende Bedeutung:</br>-   0: Kein Zugriff</br>– 1: X (führen Sie den Zugriff)</br>– 2: w (Schreibzugriff)</br>-   3: wx</br>-4: R (Lesezugriff)</br>-5: Rx</br>– 6: RW-Medien</br>– 7: Rwx|
|-o lang={euc-jp|EUC-tw|EUC-kr|shift-jis|Big5|ksc5601|gb2312-80|ANSI}|Die standardcodierung für Datei- und Verzeichnisnamen verwendet und angegeben, wenn verwendet, muss auf eine der folgenden festgelegt werden:</br>-   **ansi**</br>-   **Big5** (Chinesisch)</br>-   **EUC-jp** (Japanisch)</br>-   **EUC-Kr** (Koreanisch)</br>-   **EUC-Tw** (Chinesisch)</br>-   **GB2312-80** (Chinesisch (vereinfacht))</br>-   **ksc5601** (Korean)</br>-   **Shift-Jis** (Japanisch)</br>Wenn diese Option, um festgelegt ist **Ansi** auf Systemen, die für nicht englische Gebietsschemas konfiguriert werden, das Codierungsschema, das Standard-Codierungsschema für das Gebietsschema festgelegt ist. Im folgenden finden die Codierung des Standardschemas für die angegebenen Gebietsschemas:</br>– Japanisch: SHIFT-JIS</br>– Koreanisch: KS_C_5601-1987</br>-Chinesisch vereinfacht, Chinesisch: GB2312-80</br>– Traditionelles Chinesisch: BIG5|
|-u:\<Benutzername >|Gibt den Benutzernamen ein, verwenden Sie für das Einbinden der Freigabe an. Wenn *Benutzername* nicht durch einen umgekehrten Schrägstrich vorangestellt ist (**\**), wird er als einen UNIX-Benutzernamen behandelt.|
|-p:\<Kennwort >|Das Kennwort für das Einbinden der Freigabe. Wenn Sie ein Sternchen verwenden (**&#42;**), Sie werden aufgefordert, das Kennwort.|

> [!NOTE]
