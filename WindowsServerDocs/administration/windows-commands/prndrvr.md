---
title: prndrvr
description: Referenz Artikel zum prndrvr-Befehl, der Druckertreiber hinzufügt, löscht und auflistet.
ms.topic: article
ms.assetid: 82b09e3e-bd38-4df1-9953-b0e9ee2565a3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 2be35ef44b7c54a5b8390120cef65054c06008d2
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87884757"
---
# <a name="prndrvr"></a>prndrvr

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Fügt Druckertreiber hinzu, löscht sie und listet Sie auf. Dieser Befehl ist ein Visual Basic Skript, das sich im `%WINdir%\System32\printing_Admin_Scripts\<language>` Verzeichnis befindet. Wenn Sie diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben Sie **cscript** gefolgt vom vollständigen Pfad der prndrvr-Datei ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Beispiel: `cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prndrvr`.

Wenn Sie ohne Parameter verwendet wird, zeigt **prndrvr** die Befehlszeilen Hilfe an.

## <a name="syntax"></a>Syntax

```
cscript prndrvr {-a | -d | -l | -x | -?} [-m <model>] [-v {0|1|2|3}] [-e <environment>] [-s <Servername>] [-u <Username>] [-w <password>] [-h <path>] [-i <inf file>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| -a | Installiert einen Treiber. |
| -d | Löscht einen Treiber. |
| -l | Listet alle Druckertreiber auf, die auf dem durch den **-s-** Parameter angegebenen Server installiert sind. Wenn Sie keinen Server angeben, werden die auf dem lokalen Computer installierten Druckertreiber von Windows aufgelistet. |
| -X | Löscht alle Druckertreiber und zusätzlichen Druckertreiber, die nicht von einem logischen Drucker auf dem Server verwendet werden, der durch den **-s-** Parameter angegeben wird. Wenn Sie keinen Server angeben, der aus der Liste entfernt werden soll, löscht Windows alle nicht verwendeten Druckertreiber auf dem lokalen Computer. |
| -m `<model_name>` | Gibt (nach Name) den Treiber an, den Sie installieren möchten. Treiber werden oft für das Drucker Modell benannt, das Sie unterstützen. Weitere Informationen finden Sie in der Druckerdokumentation. |
| `-v {0|1|2|3}` | Gibt die Version des Treibers an, den Sie installieren möchten. Informationen dazu, welche Versionen für welche Umgebung verfügbar sind, finden Sie in der Beschreibung des **-e-** Parameters. Wenn Sie keine Version angeben, wird die Version des Treibers für die Version von Windows, die auf dem Computer ausgeführt wird, auf dem Sie den Treiber installieren, installiert. |
| -e `<environment>` | Gibt die Umgebung für den Treiber an, den Sie installieren möchten. Wenn Sie keine Umgebung angeben, wird die Umgebung des Computers verwendet, auf dem Sie den Treiber installieren. Folgende Umgebungsparameter werden unterstützt: **Windows NT x86**, **Windows x64** oder **Windows ia64**. |
| -s `<Servername>` | Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet. |
| -u `<Username>` -w`<password>` | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
| -h`<path>` | Gibt den Pfad zur Treiberdatei an. Wenn Sie keinen Pfad angeben, wird der Pfad zu dem Speicherort verwendet, an dem Windows installiert wurde. |
| -i`<filename.inf>` | Gibt den kompletten Pfad und den Dateinamen für den Treiber an, den Sie installieren möchten. Wenn Sie keinen Dateinamen angeben, verwendet das Skript eine der INF-Posteingangs Dateien im INF-Unterverzeichnis des Windows-Verzeichnisses.<p>Wenn der Treiber Pfad nicht angegeben ist, sucht das Skript in der driver.cab-Datei nach Treiberdateien. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Bemerkungen

- Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. "Computer Name").

- Der **-x-** Parameter löscht alle zusätzlichen Druckertreiber (Treiber, die für die Verwendung auf Clients installiert sind, auf denen alternative Versionen von Windows ausgeführt werden), auch wenn der primäre Treiber verwendet wird. Wenn die Faxkomponente installiert ist, werden mit dieser Option auch Faxtreiber gelöscht. Der primäre Faxtreiber wird gelöscht, wenn er nicht verwendet wird (d. h., wenn keine Warteschlange verwendet wird). Wenn der primäre Faxtreiber gelöscht wird, besteht die einzige Möglichkeit zum erneuten Aktivieren von Fax darin, die Faxkomponente erneut zu installieren.

### <a name="examples"></a>Beispiele

Um alle Treiber auf dem lokalen printServer1-Server aufzulisten, geben Sie Folgendes ein \\ :

```
cscript prndrvr -l -s
```

Geben Sie Folgendes ein, um einen Windows x64-Druckertreiber der Version 3 für das Modell "Laser Drucker Modell 1" mithilfe der c:\temp\laserprinter1.inf-Treiber Informationsdatei für einen im Ordner "c:\temp" gespeicherten Treiber hinzuzufügen:

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64 -i c:\temp\Laserprinter1.inf -h c:\temp
```

Zum Löschen eines Windows x64-Druckertreibers der Version 3 für das Laser Drucker Modell 1 geben Sie Folgendes ein:

```
cscript prndrvr -a -m Laser printer model 1 -v 3 -e Windows x64
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)

- [Druckbefehlsreferenz](print-command-reference.md)
