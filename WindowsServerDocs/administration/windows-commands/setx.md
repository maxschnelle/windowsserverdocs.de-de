---
title: setx
description: Referenz Artikel für den Befehl SETX, mit dem Umgebungsvariablen in der Benutzer-oder Systemumgebung erstellt oder geändert werden, ohne dass Programmieren oder Skripts erforderlich sind.
ms.topic: reference
ms.assetid: ef37482f-f8a8-4765-951a-2518faac3f44
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 82ec683f0ed4723e7905daea759965690b8adcd5
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388304"
---
# <a name="setx"></a>setx

Erstellt oder ändert Umgebungsvariablen in der Benutzer-oder Systemumgebung, ohne dass Programmieren oder Skripts erforderlich sind. Der **setx** -Befehl ruft auch die Werte von Registrierungs Schlüsseln ab und schreibt Sie in Textdateien.

> [!NOTE]
> Dieser Befehl stellt die einzige Befehlszeile oder programmgesteuerte Möglichkeit bereit, um System Umgebungs Werte direkt und dauerhaft festzulegen. System Umgebungsvariablen können manuell über die System **Steuerung** oder über einen Registrierungs-Editor konfiguriert werden. Mit dem SET-Befehl, der für den Befehls Interpreter (Cmd.exe) intern ist, werden Benutzer Umgebungsvariablen nur für das aktuelle Konsolenfenster **fest** gelegt.

## <a name="syntax"></a>Syntax

```
setx [/s <computer> [/u [<domain>\]<user name> [/p [<password>]]]] <variable> <value> [/m]
setx [/s <computer> [/u [<domain>\]<user name> [/p [<password>]]]] <variable>] /k <path> [/m]
setx [/s <computer> [/u [<domain>\]<user name> [/p [<password>]]]] /f <filename> {[<variable>] {/a <X>,<Y> | /r <X>,<Y> <String>} [/m] | /x} [/d <delimiters>]
```

### <a name="parameters"></a>Parameter

| Parameter | BESCHREIBUNG |
|--|--|
| /s `<computer>` | Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der Name des lokalen Computers. |
| /u `[<domain>\]<user name>` | Führt das Skript mit den Anmelde Informationen des angegebenen Benutzerkontos aus. Der Standardwert ist die System Berechtigungen. |
| /p [ `<password>` ]| Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist. |
| `<variable>` | Gibt den Namen der Umgebungsvariablen an, die Sie festlegen möchten. |
| `<value>` | Gibt den Wert an, auf den die Umgebungsvariable festgelegt werden soll. |
| /k `<path>` | Gibt an, dass die Variable auf der Grundlage von Informationen aus einem Registrierungsschlüssel festgelegt wird. Der *Pfad* verwendet die folgende Syntax: `\\<HIVE>\<KEY>\...\<Value>` . Sie können z. b. den folgenden Pfad angeben: `HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName` |
| /f `<filename>` | Gibt die Datei an, die Sie verwenden möchten. |
| /a `<X>,<Y>` | Gibt absolute Koordinaten und einen Offset als Suchparameter an. |
| /r `<X>,<Y> <String>` | Gibt relative Koordinaten und einen Offset von der **Zeichenfolge** als Suchparameter an. |
| /m | Gibt an, dass die Variable in der Systemumgebung festgelegt wird. Die Standardeinstellung ist die lokale Umgebung. |
| /x | Zeigt Datei Koordinaten an, wobei die Befehlszeilenoptionen **/a**, **/r**und **/d** ignoriert werden. |
| /d `<delimiters>` | Gibt Trennzeichen wie oder an **,** **\\** die zusätzlich zu den vier integrierten Trennzeichen verwendet werden können – Leerzeichen, Tabstopps, EINGABETASTE und Zeilenvorschub. Gültige Trennzeichen sind beliebige ASCII-Zeichen. Die maximale Anzahl von Trennzeichen beträgt 15, einschließlich integrierter Trennzeichen. |
| /? | Zeigt die Hilfe an der Eingabeaufforderung an. |

#### <a name="remarks"></a>Hinweise

- Dieser Befehl ähnelt dem UNIX-Hilfsprogramm "\tenv".

- Mit diesem Befehl können Sie Werte für Benutzer-und System Umgebungsvariablen aus einer der drei Quellen (Modi) festlegen: Befehlszeilen Modus, Registrierungs Modus oder Dateimodus.

- Dieser Befehl schreibt Variablen in die Master Umgebung in der Registrierung. Mit **setx** -Variablen festgelegte Variablen sind nur in zukünftigen Befehls Fenstern, nicht im aktuellen Befehlsfenster verfügbar.

- **HKEY_CURRENT_USER** und **HKEY_LOCAL_MACHINE** sind die einzigen unterstützten Strukturen. REG_DWORD, REG_EXPAND_SZ, REG_SZ und REG_MULTI_SZ sind die gültigen **RegKey** -Datentypen.

- Wenn Sie Zugriff auf **REG_MULTI_SZ** Werte in der Registrierung erhalten, wird nur das erste Element extrahiert und verwendet.

- Sie können diesen Befehl nicht verwenden, um Werte zu entfernen, die der lokalen Umgebung oder der Systemumgebung hinzugefügt werden Sie können diesen Befehl mit einem Variablennamen und ohne Wert verwenden, um einen entsprechenden Wert aus der lokalen Umgebung zu entfernen.

- REG_DWORD Registrierungs Werte werden extrahiert und im Hexadezimal Modus verwendet.

- Im Dateimodus wird nur das Übertragen von Textdateien in Wagen Rücklauf-und Zeilenvorschub (CRLF) unterstützt.

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die *Computer* Umgebungsvariable in der lokalen Umgebung auf den Wert *Brand1*festzulegen:

```
setx MACHINE Brand1
```

Geben Sie Folgendes ein, um die Computer *Umgebungsvariable in der System* Umgebung auf den Wert *Brand1 Computer*festzulegen:

```
setx MACHINE Brand1 Computer /m
```

Geben Sie Folgendes ein, um die Umgebungsvariable *myPath* in der lokalen Umgebung so festzulegen, dass Sie den in der *path* -Umgebungsvariablen definierten Suchpfad verwendet:

```
setx MYPATH %PATH%
```

Um die *myPath* -Umgebungsvariable in der lokalen Umgebung so festzulegen, dass Sie den Suchpfad verwendet, der in der *path* -Umgebungsvariablen nach dem ersetzen **~** von definiert **%** ist, geben Sie

```
setx MYPATH ~PATH~
```

Geben Sie Folgendes ein, um die *Computer* Umgebungsvariable in der lokalen Umgebung auf *Brand1* auf einem Remote Computer mit dem Namen *Computer1*festzulegen:

```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MACHINE Brand1
```

Geben Sie Folgendes ein, um die Umgebungsvariable *myPath* in der lokalen Umgebung auf den Suchpfad festzulegen, der in der *path* -Umgebungsvariablen auf einem Remote Computer mit dem Namen *Computer1*definiert ist:

```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MYPATH %PATH%
```

Geben Sie Folgendes ein, um die *Tzone* -Umgebungsvariable in der lokalen Umgebung auf den Wert im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\timezoneinformation\standardname** festzulegen:

```
setx TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName
```

Geben Sie Folgendes ein, um die *Tzone* -Umgebungsvariable in der lokalen Umgebung eines Remote Computers mit dem Namen *Computer1* auf den Wert festzulegen, der im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\timezoneinformation\standardname** gefunden wurde:

```
setx /s computer1 /u maindom\hiropln /p p@ssW23 TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName
```

Geben Sie Folgendes *BUILD* ein, um die Buildumgebungs Variable in der Systemumgebung auf den Wert im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \software\microsoft\windowsnt\currentversion\currentbuildnumber** festzulegen:

```
setx BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber /m
```

Geben Sie Folgendes ein, um die Buildumgebungs Variable in der Systemumgebung eines Remote Computers mit dem Namen Computer1 auf den Wert festzulegen, der im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \software\microsoft\windowsnt\currentversion\currentbuildnumber** gefunden wurde.

```
setx /s computer1 /u maindom\hiropln /p p@ssW23  BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\CurrentBuildNumber /m
```

Um den Inhalt einer Datei mit dem Namen " *ipconfig. out*" zusammen mit den entsprechenden Koordinaten des Inhalts anzuzeigen, geben Sie Folgendes ein:

```
setx /f ipconfig.out /x
```

Geben Sie Folgendes ein, um die Umgebungsvariable *ipaddr* in der lokalen Umgebung auf den Wert festzulegen, der in der Datei " *ipconfig. out* " in der Koordinate *5, 11* gefunden wurde:

```
setx IPADDR /f ipconfig.out /a 5,11
```

Geben Sie Folgendes ein, um die *OCTET1* -Umgebungsvariable in der lokalen Umgebung auf den Wert festzulegen, der in der Datei "ipconfig. out *" in der* Datei " *ipconfig. out* " mit Trennzeichen **# $ *.** gefunden wurde.

```
setx OCTET1 /f ipconfig.out /a 5,3 /d #$*.
```

Geben Sie Folgendes ein, um die *IPGateway* -Umgebungsvariable in der lokalen Umgebung auf den Wert festzulegen, der sich in Bezug auf die Koordinaten des *Gateways* in der Datei " *ipconfig. out* " auf den Wert in der Koordinate *0* befindet.

```
setx IPGATEWAY /f ipconfig.out /r 0,7 Gateway
```

Um den Inhalt der Datei " *ipconfig. out* " zusammen mit den entsprechenden Koordinaten des Inhalts auf einem Computer mit dem Namen " *Computer1*" anzuzeigen, geben Sie Folgendes ein:

```
setx /s computer1 /u maindom\hiropln /p p@ssW23 /f ipconfig.out /x
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
