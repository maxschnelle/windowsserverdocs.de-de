---
title: setx
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef37482f-f8a8-4765-951a-2518faac3f44
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5a650fae246d71d8c1f9822dfa9ff8e96d855b4b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886571"
---
# <a name="setx"></a>setx



Erstellt oder ändert Umgebungsvariablen in der Benutzer oder einer systemumgebung, ohne Programmierung oder Skripts. Die **Setx** Befehl auch Ruft die Werte von Registrierungsschlüsseln ab und schreibt sie in Textdateien.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] <Variable> <Value> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] [<Variable>] /k <Path> [/m]
setx [/s <Computer> [/u [<Domain>\]<User name> [/p [<Password>]]]] /f <FileName> {[<Variable>] {/a <X>,<Y> | /r <X>,<Y> "<String>"} [/m] | /x} [/d <Delimiters>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/ s \<Computer >|Gibt den Namen oder die IP-Adresse eines Remotecomputers. Verwenden Sie keine umgekehrte Schrägstriche. Der Standardwert ist der Name des lokalen Computers.|
|/u [\<Domain>\]<User name>|Führt das Skript mit den Anmeldeinformationen des angegebenen Benutzerkontos. Der Standardwert ist die Systemberechtigungen.|
|/ p [\<Kennwort >]|Gibt das Kennwort des Benutzerkontos ein, die im angegebenen die **/u** Parameter.|
|\<Variable>|Gibt den Namen der Umgebungsvariablen, die Sie festlegen möchten.|
|\<Wert >|Gibt den Wert, den um die Umgebungsvariable festgelegt werden soll.|
|/ k \<Pfad >|Gibt an, dass die Variable basierend auf Informationen aus einem Registrierungsschlüssel festgelegt ist. Das p*fehlerprotokollpf* verwendet die folgende Syntax:</br>`\\<HIVE>\<KEY>\...\<Value>`</br>Beispielsweise können Sie den folgenden Pfad angeben:</br>`HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName`|
|/ f \<Dateiname >|Gibt die Datei, die Sie verwenden möchten.|
|/ a \<X >,<Y>|Gibt an, absolute Koordinaten und Offset als Suchparameter.|
|/ r \<X >,<Y> "<String>"|Gibt an, relative Koordinaten und den Offset vom **Zeichenfolge** als Suchparameter.|
|/m|Gibt an, um die Variable in der Umgebung. Die Standardeinstellung ist der lokalen Umgebung.|
|/x|Zeigt Datei vorliegen, wird ignoriert, die **/a**, **/r**, und **/d** Befehlszeilenoptionen.|
|/d \<Delimiters>|Gibt an, Trennzeichen wie z. B. "**,**" oder "**\**", zusätzlich zu den vier integrierte Trennzeichen verwendet werden soll – Speicherplatz, Registerkarte, Zeilenvorschub und EINGABETASTE. Gültige Trennzeichen enthalten jedes ASCII-Zeichen. Die maximale Anzahl von Trennzeichen ist, 15, einschließlich integrierten Trennzeichen.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

-   Die **Setx** Befehl ähnelt dem UNIX-Dienstprogramm SETENV.
-   **SETX** die nur Befehlszeile oder eine programmgesteuerte Möglichkeit zum System direkt und dauerhaft Umgebungswerte festgelegt. Umgebungsvariablen des Systems sind über manuell konfigurierbare **Systemsteuerung** oder über einen Registrierungs-Editor. Die **festgelegt** Befehl, der an den Befehlsinterpreter (Cmd.exe) intern verwendet wird, werden Umgebungsvariablen Benutzer für das aktuelle Konsolenfenster nur.
-   Sie können die **Setx** Befehl aus, um Werte für Benutzer- und Umgebungsvariablen aus einem der drei Quellen (Modus) festgelegt: Befehlszeilenmodus, Modus der Registrierung oder Datei-Modus.
-   **SETX** Variablen in der master-Umgebung in der Registrierung geschrieben. Legen Sie Variablen mit **Setx** Variablen sind nicht verfügbar in zukünftigen nur im aktuellen Befehlsfenster.
-   **HKEY_CURRENT_USER** und **HKEY_LOCAL_MACHINE** sind die einzigen unterstützten Strukturen. REG_DWORD-Wert "," REG_EXPAND_SZ "," REG_SZ "und" REG_MULTI_SZ gelten die **RegKey** -Datentypen.
-   Wenn erhalten Sie Zugang zu **REG_MULTI_SZ** Werte in der Registrierung, nur das erste Element extrahiert und verwendet wird.
-   Sie können keine der **Setx** Befehl aus, um Werte zu entfernen, die auf dem lokalen System oder Umgebungen hinzugefügt wurden. Sie können **festgelegt** mit einem Variablennamen und keinen Wert einen entsprechenden Wert aus der lokalen Umgebung zu entfernen.
-   REG_DWORD-Registrierungswerte werden extrahiert und im Hexadezimalmodus verwendet.
-   Datei-Modus unterstützt das Analysieren der Carriage return, Wagenrücklauf und Zeilenvorschub (CR), Textdateien nur.

## <a name="BKMK_examples"></a>Beispiele für

Um die Computer-Umgebungsvariable in der lokalen Umgebung auf den Wert Brand1 festzulegen, geben Sie Folgendes ein:
```
setx MACHINE Brand1
```
Um die Computer-Umgebungsvariable in der Umgebung auf den Wert Brand1 Computer festzulegen, geben Sie Folgendes ein:
```
setx MACHINE "Brand1 Computer" /m
```
Um die Umgebungsvariable "myPath" in der lokalen Umgebung verwenden Sie den Suchpfad, der definiert, in der PATH-Umgebungsvariablen festzulegen, geben Sie Folgendes ein:
```
setx MYPATH %PATH%
```
Festlegen der Umgebungsvariablen "myPath" in der lokalen Umgebung verwenden Sie den Suchpfad, die in der PATH-Umgebungsvariable definiert ist, nach dem Ersetzen **~** mit **%**, Typ:
```
setx MYPATH ~PATH~ 
```
Um die Computer-Umgebungsvariable in der lokalen Umgebung zu Brand1 auf einem Remotecomputer mit dem Namen Computer1 festzulegen, geben Sie Folgendes ein:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MACHINE Brand1
```
Um die Umgebungsvariable "myPath" in der lokalen Umgebung verwenden Sie den Suchpfad, der definiert, in der PATH-Umgebungsvariablen auf einem Remotecomputer mit dem Namen Computer1 festzulegen, geben Sie Folgendes ein:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 MYPATH %PATH%
```
Zum Festlegen der TZONE-Umgebungsvariablen in der lokalen Umgebung auf die im Wert der **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName angegebenen** Registrierung, Schlüsseltyp:
```
setx TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
Zum Festlegen der TZONE-Umgebungsvariablen in der lokalen Umgebung von einem Remotecomputer mit dem Namen Computer1 auf den Wert finden Sie in der **HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName angegebenen** Registrierung Schlüsseltyp:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 TZONE /k HKEY_LOCAL_MACHINE\System\CurrentControlSet\Control\TimeZoneInformation\StandardName 
```
Der BUILD-Umgebungsvariablen in der Umgebung auf die im Wert festlegen die **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** Registrierung, Schlüsseltyp:
```
setx BUILD /k "HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber" /m
```
Der BUILD-Umgebungsvariablen in der Umgebung von einem Remotecomputer mit dem Namen Computer1 auf die im Wert festlegen die **HKEY_LOCAL_MACHINE\Software\Microsoft\WindowsNT\CurrentVersion\CurrentBuildNumber** Registrierungsschlüssel , Typ:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23  BUILD /k "HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\CurrentBuildNumber" /m
```
Zum Anzeigen des Inhalts einer Datei mit dem Namen Ipconfig.out, zusammen mit den entsprechenden Koordinaten für den Inhalt, geben Sie Folgendes ein:
```
setx /f ipconfig.out /x
```
Um die IPADDR-Umgebungsvariable in der lokalen Umgebung auf den Wert an die Koordinate 5,11 finden Sie in der Datei Ipconfig.out festzulegen, geben Sie Folgendes ein:
```
setx IPADDR /f ipconfig.out /a 5,11
```
Festlegen der Umgebungsvariablen OCTET1 in der lokalen Umgebung auf den Wert an die Koordinate 5,3 finden Sie in der Datei Ipconfig.out Trennzeichen **"#$\*."** , Typ:
```
setx OCTET1 /f ipconfig.out /a 5,3 /d "#$*." 
```
Um die IP-Gateway-Umgebungsvariable in der lokalen Umgebung auf den Wert an die Koordinate 0,7 in Bezug auf die Koordinate des "Gateway" finden Sie in der Datei Ipconfig.out festzulegen, geben Sie Folgendes ein:
```
setx IPGATEWAY /f ipconfig.out /r 0,7 Gateway 
```
Anzeigen der Inhalte einer Datei mit dem Namen Ipconfig.out – zusammen mit den entsprechenden Koordinaten für den Inhalt, geben Sie auf einem Computer mit dem Namen Computer1:
```
setx /s computer1 /u maindom\hiropln /p p@ssW23 /f ipconfig.out /x 
```

#### <a name="additional-references"></a>Weitere Verweise

[Befehlszeilensyntax](command-line-syntax-key.md)