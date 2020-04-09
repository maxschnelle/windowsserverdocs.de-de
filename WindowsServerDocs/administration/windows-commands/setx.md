---
title: setx
description: Windows-Befehls Thema für SETX, das Umgebungsvariablen in der Benutzer-oder Systemumgebung erstellt oder ändert, ohne dass Programmieren oder Skripts erforderlich sind.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: ef37482f-f8a8-4765-951a-2518faac3f44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 19f6625ffaaf745ae2af26e52986e97382f42702
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80834343"
---
# <a name="setx"></a>setx

Erstellt oder ändert Umgebungsvariablen in der Benutzer-oder Systemumgebung, ohne dass Programmieren oder Skripts erforderlich sind. Der **setx** -Befehl ruft auch die Werte von Registrierungs Schlüsseln ab und schreibt Sie in Textdateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] <Variable> <Value> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] [<Variable>] /k <Path> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <FileName> {[<Variable>] {/a <X>,<Y> | /r <X>,<Y> <String>} [/m] | /x} [/d <Delimiters>]
```

### <a name="parameters"></a>Parameter

|         Parameter          |                                                                                                                                              Beschreibung                                                                                                                                              |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|       /s \<Computer >       |                                                                                  Gibt den Namen oder die IP-Adresse eines Remote Computers an. Verwenden Sie keine umgekehrten Schrägstriche. Der Standardwert ist der Name des lokalen Computers.                                                                                  |
| /u [\<Domänen >\]<User name> |                                                                                           Führt das Skript mit den Anmelde Informationen des angegebenen Benutzerkontos aus. Der Standardwert ist die System Berechtigungen.                                                                                            |
|      /p [\<Password >]      |                                                                                                         Gibt das Kennwort des Benutzerkontos an, das im **/u** -Parameter angegeben ist.                                                                                                         |
|        \<Variable >         |                                                                                                                 Gibt den Namen der Umgebungsvariablen an, die Sie festlegen möchten.                                                                                                                  |
|          \<Wert >          |                                                                                                                Gibt den Wert an, auf den die Umgebungsvariable festgelegt werden soll.                                                                                                                 |
|         /k \<Pfad >         | Gibt an, dass die Variable auf der Grundlage von Informationen aus einem Registrierungsschlüssel festgelegt wird. Der p-*ATH* verwendet die folgende Syntax:</br>`\\<HIVE>\<KEY>\...\<Value>`</br>Sie können z. b. den folgenden Pfad angeben:</br>`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName` |
|      /f \<Dateiname >       |                                                                                                                               Gibt die Datei an, die Sie verwenden möchten.                                                                                                                                |
|        /a \<X >,<Y>         |                                                                                                                    Gibt absolute Koordinaten und einen Offset als Suchparameter an.                                                                                                                    |
|   /r \<X >,<Y> <String>   |                                                                                                            Gibt relative Koordinaten und einen Offset von der **Zeichenfolge** als Suchparameter an.                                                                                                            |
|             /m             |                                                                                                Gibt an, dass die Variable in der Systemumgebung festgelegt wird. Die Standardeinstellung ist die lokale Umgebung.                                                                                                 |
|             /x             |                                                                                                       Zeigt Datei Koordinaten an, wobei die Befehlszeilenoptionen **/a**, **/r**und **/d** ignoriert werden.                                                                                                        |
|      /d \<Trennzeichen >      |                    Gibt Trennzeichen wie oder **\\** **an, die** zusätzlich zu den vier integrierten Trennzeichen verwendet werden können – Leerzeichen, Tabstopps, Eingabe und Zeilenvorschub. Gültige Trennzeichen sind beliebige ASCII-Zeichen. Die maximale Anzahl von Trennzeichen beträgt 15, einschließlich integrierter Trennzeichen.                    |
|             /?             |                                                                                                                                 Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                  |

## <a name="remarks"></a>Hinweise

-   Der **setx** -Befehl ähnelt dem UNIX-Hilfsprogramm setenv.
-   **Setx** stellt die einzige Befehlszeile oder programmgesteuerte Möglichkeit bereit, um System Umgebungs Werte direkt und dauerhaft festzulegen. System Umgebungsvariablen können manuell über die System **Steuerung** oder über einen Registrierungs-Editor konfiguriert werden. Mit dem SET-Befehl, der für den Befehls Interpreter (cmd. exe) intern ist, werden Benutzer Umgebungsvariablen nur für das aktuelle Konsolenfenster **fest** gelegt.
-   Mit dem Befehl **setx** können Sie Werte für Benutzer-und System Umgebungsvariablen aus einer der drei Quellen (Modi) festlegen: Befehlszeilen Modus, Registrierungs Modus oder Dateimodus.
-   **Setx** schreibt Variablen in die Master Umgebung in der Registrierung. Mit **setx** -Variablen festgelegte Variablen sind nur in zukünftigen Befehls Fenstern, nicht im aktuellen Befehlsfenster verfügbar.
-   **HKEY_CURRENT_USER** und **HKEY_LOCAL_MACHINE** sind die einzigen unterstützten Strukturen. REG_DWORD, REG_EXPAND_SZ, REG_SZ und REG_MULTI_SZ sind die gültigen **RegKey** -Datentypen.
-   Wenn Sie Zugriff auf **REG_MULTI_SZ** Werte in der Registrierung erhalten, wird nur das erste Element extrahiert und verwendet.
-   Sie können den Befehl **setx** nicht verwenden, um Werte zu entfernen, die der lokalen Umgebung oder der Systemumgebung hinzugefügt wurden. Sie können **Set** mit einem Variablennamen und ohne Wert verwenden, um einen entsprechenden Wert aus der lokalen Umgebung zu entfernen.
-   REG_DWORD Registrierungs Werte werden extrahiert und im Hexadezimal Modus verwendet.
-   Im Dateimodus wird nur das Übertragen von Textdateien in Wagen Rücklauf-und Zeilenvorschub (CRLF) unterstützt.

## <a name="examples"></a><a name=BKMK_examples></a>Beispiele

Geben Sie Folgendes ein, um die Computer Umgebungsvariable in der lokalen Umgebung auf den Wert Brand1 festzulegen:
```
setx MACHINE Brand1
```
Geben Sie Folgendes ein, um die Computer Umgebungsvariable in der Systemumgebung auf den Wert Brand1 Computer festzulegen:
```
setx MACHINE Brand1 Computer /m
```
Geben Sie Folgendes ein, um die Umgebungsvariable myPath in der lokalen Umgebung so festzulegen, dass Sie den in der PATH-Umgebungsvariablen definierten Suchpfad verwendet:
```
setx MYPATH %PATH%
```
Geben Sie Folgendes ein, um die Umgebungsvariable myPath in der lokalen Umgebung so festzulegen, dass Sie den Suchpfad verwendet, der in der PATH-Umgebungsvariablen definiert ist, nachdem **~** durch **%**
```
setx MYPATH ~PATH~ 
```
Geben Sie Folgendes ein, um die Computer Umgebungsvariable in der lokalen Umgebung auf Brand1 auf einem Remote Computer mit dem Namen Computer1 festzulegen:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MACHINE Brand1
```
Geben Sie Folgendes ein, um die Umgebungsvariable myPath in der lokalen Umgebung auf den Suchpfad festzulegen, der in der PATH-Umgebungsvariablen auf einem Remote Computer mit dem Namen Computer1 definiert ist:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MYPATH %PATH%
```
Geben Sie Folgendes ein, um die TZONE-Umgebungsvariable in der lokalen Umgebung auf den Wert im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\timezoneinformation\standardname** festzulegen:
```
setx TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
Geben Sie Folgendes ein, um die TZONE-Umgebungsvariable in der lokalen Umgebung eines Remote Computers mit dem Namen Computer1 auf den Wert festzulegen, der im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \system\currentcontrolset\control\timezoneinformation\standardname** gefunden wurde:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
Geben Sie Folgendes ein, um die Buildumgebungs Variable in der Systemumgebung auf den Wert im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \software\microsoft\windowsnt\currentversion\currentbuildnumber** festzulegen:
```
setx BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber /m
```
Geben Sie Folgendes ein, um die Buildumgebungs Variable in der Systemumgebung eines Remote Computers mit dem Namen Computer1 auf den Wert festzulegen, der im Registrierungsschlüssel **HKEY_LOCAL_MACHINE \software\microsoft\windowsnt\currentversion\currentbuildnumber** gefunden wurde.
```
setx /s computer1 /u maindom\hiropln /p p@ssW23  BUILD /k HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\CurrentBuildNumber /m
```
Um den Inhalt einer Datei mit dem Namen "ipconfig. out" zusammen mit den entsprechenden Koordinaten des Inhalts anzuzeigen, geben Sie Folgendes ein:
```
setx /f ipconfig.out /x
```
Geben Sie Folgendes ein, um die Umgebungsvariable ipaddr in der lokalen Umgebung auf den Wert festzulegen, der in der-Koordinate 5, 11 in der Datei "ipconfig. out" gefunden wird:
```
setx IPADDR /f ipconfig.out /a 5,11
```
Zum Festlegen der OCTET1-Umgebungsvariablen in der lokalen Umgebung auf den Wert in der-Koordinate 5, 3 in der Datei ipconfig. out mit Trennzeichen **#$\*.** geben Sie Folgendes ein:
```
setx OCTET1 /f ipconfig.out /a 5,3 /d #$*. 
```
Geben Sie Folgendes ein, um die IPGateway-Umgebungsvariable in der lokalen Umgebung auf den Wert festzulegen, der in der Koordinate 0, 7 in Bezug auf die Koordinaten des Gateways in der Datei "ipconfig. out" gefunden wird:
```
setx IPGATEWAY /f ipconfig.out /r 0,7 Gateway 
```
Geben Sie Folgendes ein, um den Inhalt einer Datei mit dem Namen ipconfig. out – zusammen mit den entsprechenden Koordinaten des Inhalts – auf einem Computer mit dem Namen Computer1 anzuzeigen:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 /f ipconfig.out /x 
```

## <a name="additional-references"></a>Weitere Verweise

- [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)