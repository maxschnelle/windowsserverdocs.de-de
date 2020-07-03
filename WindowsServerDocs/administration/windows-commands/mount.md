---
title: mount
description: Referenz Artikel für den Mount-Befehl, der NFS (Network File System)-Netzwerkfreigaben bereitstellt.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: dd9d7ecb-ef00-4aaa-bcd0-423fa636e34a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 505094251ab6b0053cc3d46801ba5f6170201ecd
ms.sourcegitcommit: 2afed2461574a3f53f84fc9ec28d86df3b335685
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/02/2020
ms.locfileid: "85935722"
---
# <a name="mount"></a>mount

Ein Befehlszeilen-Hilfsprogramm, das NFS-Netzwerkfreigaben (Network File System) bereitstellt. Bei Verwendung ohne Optionen oder Argumente zeigt **Mount** Informationen zu allen bereitgestellten NFS-Dateisystemen an.

> [!NOTE]
> Dieses Hilfsprogramm ist nur verfügbar, wenn der **Client für NFS** installiert ist.

## <a name="syntax"></a>Syntax

```
mount [-o <option>[...]] [-u:<username>] [-p:{<password> | *}] {\\<computername>\<sharename> | <computername>:/<sharename>} {<devicename> | *}
```

### <a name="parameters"></a>Parameter

| Parameter  | Beschreibung |
| ---------- | ----------- |
| -o rsize =`<buffersize>` | Legt die Größe des Lese Puffers in Kilobyte fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32; der Standardwert ist 32 KB. |
| -o wsize =`<buffersize>` | Legt die Größe des Schreib Puffers in Kilobyte fest. Zulässige Werte sind 1, 2, 4, 8, 16 und 32; der Standardwert ist 32 KB. |
| -o Timeout =`<seconds>` | Legt den Timeout Wert für einen Remote Prozedur Aufruf (RPC) in Sekunden fest. Zulässige Werte sind 0,8, 0,9 und jede beliebige ganze Zahl im Bereich 1-60; der Standardwert ist 0,8. |
| -o Retry =`<number>` | Legt die Anzahl der Wiederholungs Versuche für eine weiche Bereitstellung fest. Zulässige Werte sind ganze Zahlen im Bereich 1-10; der Standardwert ist 1. |
| -o mtype =`{soft|hard}` | Legt den Einstellungstyp für die NFS-Freigabe fest. Standardmäßig wird von Windows eine weiche einreihe verwendet. Bei Verbindungsproblemen ist das Timeout bei der Soft-Bereitstellung leichter. um die e/a-Unterbrechung bei NFS-Serverneustarts zu reduzieren, empfiehlt es sich jedoch, eine harte Bereitstellung zu verwenden.|
| -o anon | Wird als anonymer Benutzer bereitgestellt. |
| -o NOLOCK | Deaktiviert das Sperren (standardmäßig **aktiviert**). |
| -o CaseSensitive | Erzwingt bei Datei Suchvorgängen auf dem Server die Groß-/Kleinschreibung. |
| -o FileAccess =`<mode>` | Gibt den Standard Berechtigungs Modus von neuen Dateien an, die auf der NFS-Freigabe erstellt werden. Geben Sie den *Modus* als dreistellige Zahl in der Form *OGW*an, wobei *o*, *g*und *w* jede Ziffer sind, die den Zugriff auf den Besitzer, die Gruppe und die Welt der Datei darstellt. Die Ziffern müssen im Bereich 0-7 liegen, einschließlich:<ul><li>**0:** Kein Zugriff</li><li>**1:** x (Zugriff ausführen)</li><li>**2:** w (Schreibzugriff)</li><li>**3:** WX (Schreib-und Ausführungs Zugriff)</li><li>**4:** r (Lesezugriff)</li><li>**5:** RX (Lese-und Ausführungs Zugriff)</li><li>**6:** RW (Lese-und Schreibzugriff)</li><li>**7:** rwx (Lese-, Schreib-und Ausführungs Zugriff)</li></ul> |
| -o lang =`{euc-jp|euc-tw|euc-kr|shift-jis|Big5|Ksc5601|Gb2312-80|Ansi)` | Gibt die sprach Codierung an, die auf einer NFS-Freigabe konfiguriert werden soll. Sie können nur eine Sprache auf der Freigabe verwenden. Dieser Wert kann einen der folgenden Werte enthalten:<ul><li>**EUC-JP:** Japanisch</li><li>**EUC-TW:** Chinesisch</li><li>**EUC-KR:** Koreanisch</li><li>**Shift-JIS:** Japanisch</li><li>**Big5:** Chinesisch</li><li>**Ksc5601:** Koreanisch</li><li>**GB2312-80:** Vereinfachtes Chinesisch</li><li>**ANSI:** ANSI-codiert</li></ul> |
| u`<username>` | Gibt den Benutzernamen an, der zum Einbinden der Freigabe verwendet werden soll. Wenn einem *Benutzer* Namen kein umgekehrter Schrägstrich (* *\** ) vorangestellt ist, wird er als Unix-Benutzername behandelt. |
| -p:`<password>` | Das Kennwort, das zum Einbinden der Freigabe verwendet werden soll. Wenn Sie ein Sternchen (**&#42;**) verwenden, werden Sie zur Eingabe des Kennworts aufgefordert. |
| `<computername>` | Gibt den Namen des NFS-Servers an. |
| `<sharename>` | Gibt den Namen des Dateisystems an. |
| `<devicename>` | Gibt den Laufwerk Buchstaben und den Namen des Geräts an. Wenn Sie ein Sternchen (**&#42;**) verwenden, stellt dieser Wert den ersten verfügbaren Treiber Buchstaben dar. |

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
