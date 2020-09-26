---
title: rundll32 printui.dll, PrintUIEntry
description: Referenz Artikel zum rundll32-printui.dll, PrintUIEntry-Befehl, mit dem viele Drucker Konfigurationsaufgaben automatisiert werden.
ms.topic: reference
ms.assetid: 12fb48b6-5dd8-4cc0-8808-e6a681aceb84
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 05/25/2018
ms.openlocfilehash: 8ad0b9b3cfdca8d9ed82cc980d29df7c885bac46
ms.sourcegitcommit: e164aeffc01069b8f1f3248bf106fcdb7f64f894
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/26/2020
ms.locfileid: "91388451"
---
# <a name="rundll32-printuidllprintuientry"></a>rundll32 printui.dll, PrintUIEntry

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Automatisiert viele Drucker Konfigurationsaufgaben. printui.dll ist die ausführbare Datei, die die Funktionen enthält, die von den Dialogfeldern für die Druckerkonfiguration verwendet werden. Diese Funktionen können auch innerhalb eines Skripts oder einer Befehlszeilen-Batchdatei aufgerufen werden, oder Sie können interaktiv von der Eingabeaufforderung aus ausgeführt werden.

## <a name="syntax"></a>Syntax

```
rundll32 printui.dll PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [modificationparameterN]
```

Sie können auch die folgenden alternativen Syntaxen verwenden, obwohl in den Beispielen in diesem Thema die vorherige Syntax verwendet wird:

```
rundll32 printui.dll,PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [ModificationParameterN]
```

```
rundll32 printui PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [modificationparameterN]
```

```
rundll32 printui,PrintUIEntry [baseparameter] [modificationparameter1] [modificationparameter2] [modificationparameterN]
```

### <a name="parameters"></a>Parameter

Es gibt zwei Arten von Parametern: Basisparameter und Änderungs Parameter. Basisparameter geben die Funktion an, die der Befehl ausführen soll. Nur einer dieser Parameter kann in einer bestimmten Befehlszeile angezeigt werden. Anschließend können Sie den Basisparameter ändern, indem Sie einen oder mehrere der Änderungs Parameter verwenden, wenn Sie auf den Basisparameter anwendbar sind (nicht alle Änderungs Parameter werden von allen Basis Parametern unterstützt).

| Basisparameter | BESCHREIBUNG |
|--|--|
| /dl | Löscht den lokalen Drucker. |
| /dn | Löscht eine Netzwerkdrucker Verbindung. |
| /dd | Löscht einen Druckertreiber. |
| /e | Zeigt die Druckeinstellungen für einen bestimmten Drucker an. |
| /GA | Fügt eine Druckerverbindung pro Computer hinzu (die Verbindung ist für alle Benutzer auf diesem Computer verfügbar, wenn Sie sich anmelden). |
| /ge | Zeigt Drucker Verbindungen pro Computer auf einem Computer an. |
| /GD | Löscht eine pro-Computer-Druckerverbindung (die Verbindung wird bei der nächsten Anmeldung des Benutzers gelöscht). |
| /IA | Installiert einen Druckertreiber mithilfe einer INF-Datei. |
| /id | Installiert einen Druckertreiber mithilfe des Assistenten zum Hinzufügen von Druckertreibern. |
| /if | Installiert einen Drucker mithilfe einer INF-Datei. |
| /ii | Installiert einen Drucker mithilfe des Assistenten zum Hinzufügen von Druckern mit einer INF-Datei. |
| /il | Mit dem Assistenten zum Hinzufügen von Druckern wird ein Drucker installiert. |
| /in | Stellt eine Verbindung mit einem Remote Netzwerkdrucker her. |
| /IP | Installiert einen Drucker mithilfe des Assistenten zum Installieren von Netzwerkdruckern (verfügbar über die Benutzeroberfläche der Druck Verwaltung). |
| /k | druckt eine Testseite auf einem Drucker. |
| /o | Zeigt die Warteschlange für einen Drucker an. |
| /p | Zeigt die Eigenschaften eines Druckers an. Wenn Sie diesen Parameter verwenden, müssen Sie auch einen Wert für den Modifikations Parameter **/n [Name]** angeben. |
| /s | Zeigt die Eigenschaften eines Druck Servers an. Wenn Sie den lokalen Drucker Server anzeigen möchten, müssen Sie keinen Änderungs Parameter verwenden. Wenn Sie jedoch einen Remote Druckserver anzeigen möchten, müssen Sie den Parameter " **/c [Name]** " ändern. |
| /SS | Gibt an, welche Art von Informationen für einen Drucker gespeichert werden. Wenn keiner der Werte für **/SS** angegeben wird, ist das Standardverhalten so, als ob alle Werte angegeben wurden. Verwenden Sie diesen Basisparameter mit den folgenden Werten am Ende der Befehlszeile:<ul><li>**2**: speichert die Informationen, die in der printER_INFO_2 Struktur der Drucker s enthalten sind. Diese Struktur enthält die grundlegenden Informationen über den Drucker, z. b. den Namen, den Servernamen, den Portnamen und den Freigabe Namen.</li><li>**7**: wird zum Speichern der Verzeichnisdienst Informationen verwendet, die in der printER_INFO_7 Struktur enthalten sind.</li><li>**c**: speichert die Farbprofil Informationen für einen Drucker.</li><li>**d**: speichert Drucker spezifische Daten, z. b. die Hardware-ID des Druckers.</li><li>**s**: speichert die Sicherheits Beschreibung des Druckers.</li><li>**g**: speichert die Informationen in der globalen DEVMODE-Struktur des Druckers.</li><li>**m**: speichert die minimalen Einstellungen für den Drucker. Dies entspricht der Angabe von **2** **d**und **g**.</li><li>**u**: speichert die Informationen in der DEVMODE-Struktur des Druckers pro Benutzer.</li></ul> |
| /Sr | Gibt an, welche Informationen zu einem Drucker wieder hergestellt werden und wie Konflikte in den Einstellungen behandelt werden. Verwenden Sie, wenn die folgenden Werte am Ende der Befehlszeile abgelegt werden:<ul><li>**2**: stellt die Informationen wieder her, die in der printER_INFO_2 Struktur der Drucker s enthalten sind. Diese Struktur enthält die grundlegenden Informationen über den Drucker, z. b. den Namen, den Servernamen, den Portnamen und den Freigabe Namen.</li><li>**7**: stellt die Verzeichnisdienst Informationen wieder her, die in der printER_INFO_7 Struktur enthalten sind.</li><li>**c**: stellt die Farbprofil Informationen für einen Drucker wieder her.</li><li>**d**: stellt Drucker spezifische Daten wieder her, z. b. die Hardware-ID des Druckers.</li><li>**s**: stellt die Sicherheits Beschreibung des Druckers wieder her.</li><li>**g**: stellt die Informationen in der globalen DEVMODE-Struktur des Druckers wieder her.</li><li>**m**: stellt die minimalen Einstellungen für den Drucker wieder her. Dies entspricht der Angabe von **2**, **d**und **g**.</li><li>**u** stellt die Informationen in der DEVMODE-Struktur "Printe s pro Benutzer" wieder her.</li><li>**r**: Wenn der in der Datei gespeicherte Druckername nicht mit dem Namen des Druckers identisch ist, in dem die Datei wieder hergestellt wird, verwenden Sie den aktuellen Drucker Namen. Dies kann nicht mit **f**angegeben werden. Wenn weder **r** noch **f** angegeben ist und die Namen nicht identisch sind, tritt bei der Wiederherstellung der Einstellungen ein Fehler auf.</li><li>**f**: Wenn sich der in der Datei gespeicherte Druckername von dem Namen des Druckers unterscheidet, in dem die Datei wieder hergestellt wird, verwenden Sie den Drucker Namen in der Datei. Dies kann nicht mit **r**angegeben werden. Wenn weder **f** noch **r** angegeben ist und die Namen nicht identisch sind, tritt bei der Wiederherstellung der Einstellungen ein Fehler auf.</li><li>**p**: Wenn der Portname in der Datei, die wieder hergestellt wird, nicht mit dem aktuellen Portnamen des Druckers identisch ist, der wieder hergestellt wird, wird der aktuelle Portname des Druckers verwendet.</li><li>**h**: Wenn der Drucker, auf dem wieder hergestellt wird, nicht mithilfe des Ressourcen Freigabe namens in der gespeicherten Einstellungsdatei freigegeben werden konnte, versuchen Sie, den Drucker entweder mit dem aktuellen Freigabe Namen oder einem neuen generierten Freigabe Namen freizugeben, wenn weder **h** noch **h** angegeben ist und der Drucker, auf dem wieder hergestellt wird, nicht mit dem gespeicherten Freigabe Namen gemeinsam genutzt werden kann.</li><li>**h**: Wenn der Drucker, der wieder hergestellt wird, nicht mit dem gespeicherten Freigabe Namen gemeinsam genutzt werden kann, sollten Sie den Drucker nicht freigeben. Wenn weder **h** noch **h** angegeben ist und der Drucker, der wieder hergestellt wird, nicht mit dem gespeicherten Freigabe Namen gemeinsam genutzt werden kann, schlägt die Wiederherstellung fehl.</li><li>**i**: Wenn der Treiber in der Datei mit den gespeicherten Einstellungen nicht mit dem Treiber für den Drucker identisch ist, der wieder hergestellt wird, tritt bei der Wiederherstellung ein Fehler auf. |
| /Xg | Ruft die Einstellungen für einen Drucker ab. |
| /Xs | Legt die Einstellungen für einen Drucker fest. |
| /y | Legt den zu installierenden Drucker als Standarddrucker fest. |
| /? | Zeigt die Produkt Hilfe für den Befehl und die zugehörigen Parameter an. |
| @ [Datei] | Gibt eine Befehlszeilenargument-Datei an und fügt den Text direkt in diese Datei in die Befehlszeile ein. |

| Modifikations Parameter | BESCHREIBUNG |
|--|--|
| /a [Datei] | Gibt den Binär Dateinamen an. |
| /b [Name] | Gibt den Namen des Basis Druckers an. |
| /c [Name] | Gibt den Namen des Computers an, wenn die auszuführende Aktion auf einem Remote Computer ausgeführt wird. |
| /f [Datei] | Gibt den Universal Naming Convention (UNC)-Pfad und den Namen des INF-Datei namens oder den Namen der Ausgabedatei an, abhängig von der Aufgabe, die Sie ausführen. Verwenden Sie **/F [File]** , um eine abhängige INF-Datei anzugeben. |
| /F [Datei] | Gibt den UNC-Pfad und-Namen einer INF-Datei an, von der die mit **/f [File]** angegebene INF-Datei abhängig ist. |
| /h [Architektur] | Gibt die Treiberarchitektur an. Verwenden Sie eine der folgenden Aktionen: **x86**, **x64**oder **Itanium**. |
| /j [Anbieter] | Gibt den Namen des Druck Anbieters an. |
| /l [Pfad] | Gibt den UNC-Pfad an, in dem sich die von Ihnen verwendeten Druckertreiber Dateien befinden. |
| /m [Model] | Gibt den Namen des Treiber Modells an. (Dieser Wert kann in der INF-Datei angegeben werden.) |
| /n [Name] | Gibt den Drucker Namen an. |
| /q | Führt den Befehl ohne Benachrichtigungen für den Benutzer aus. |
| /r [Port] | Gibt den Portnamen an. |
| /U | Gibt an, dass der vorhandene Druckertreiber verwendet werden soll, wenn er bereits installiert ist. |
| /t [#] | Gibt die null basierte Indexseite an, auf der begonnen werden soll. |
| /v [Version] | Gibt die Treiber Version an. Wenn Sie für **/K**nicht auch einen Wert angeben, müssen Sie einen der folgenden Werte angeben: **Typ 2-Kernel Modus** oder **Typ 3-Benutzermodus**. |
| /w | fordert den Benutzer zur Eingabe eines Treibers auf, wenn der Treiber in der INF-Datei, die durch **/f**angegeben ist, nicht gefunden wurde. |
| /Y | Gibt an, dass Drucker Namen nicht automatisch generiert werden sollen. |
| /z | Gibt an, dass der installierte Drucker nicht automatisch freigegeben wird. |
| /K | ändert die Bedeutung des Parameters **/h [Architecture]** in accept **2** anstelle von **x86**, **3** anstelle von **x64**oder **4** anstelle von **Itanium**. Außerdem wird der Wert des Parameters **/v [Version]** auf accept **2** an der Stelle des **Typs 2-Kernel Modus** und **3** anstelle des **Typs 3-Benutzermodus**geändert. |
| /Z | Gibt den installierten Drucker frei. Verwenden Sie nur mit dem **/if** -Parameter. |
| /MW [Meldung] | Zeigt dem Benutzer eine Warnmeldung an, bevor ein Commit für die in der Befehlszeile angegebenen Änderungen ausgeführt wird. |
| /MQ [Meldung] | Zeigt dem Benutzer eine Bestätigungsmeldung an, bevor ein Commit für die in der Befehlszeile angegebenen Änderungen ausgeführt wird. |
| /W [Flags] | Gibt alle Parameter oder Optionen für den Assistenten zum Hinzufügen von Druckern, den Assistenten zum Hinzufügen von Druckertreibern und den Installations-Assistenten für den Netzwerkdrucker an.<p>**r**: ermöglicht das Neustarten der Assistenten auf der letzten Seite. |
| /G [Flags] | Gibt globale Parameter und Optionen an, die Sie verwenden möchten.<p>**w**: Unterdrückt Warnungen des Setup Treibers für den Benutzer. |

#### <a name="remarks"></a>Hinweise

- Beim **PrintUIEntry** -Schlüsselwort wird die Groß-/Kleinschreibung beachtet, und Sie müssen die Syntax für diesen Befehl mit der exakten groß Schreibung eingeben, die in den Beispielen in diesem Thema gezeigt wird

- Weitere Beispiele erhalten Sie, wenn Sie an einer Eingabeaufforderung Folgendes eingeben: **rundll32 printui.dll, PrintUIEntry/?**

## <a name="examples"></a>Beispiele

Zum Hinzufügen eines neuen Remote Druckers, printer1, für einen Computer CLIENT1, der für das Benutzerkonto sichtbar ist, in dem dieser Befehl ausgeführt wird, geben Sie Folgendes ein:

```
rundll32 printui.dll PrintUIEntry /in /n\\client1\printer1
```

Wenn Sie mit dem Assistenten zum Hinzufügen von Druckern und der INF-Datei einen Drucker hinzufügen möchten, geben Sie in das Verzeichnis "Laufwerk c:" unter "INFPath" Folgendes ein:

```
rundll32 printui.dll PrintUIEntry /ii /f c:\Infpath\InfFile.inf
```

Um einen vorhandenen Drucker, printer1, auf einem Computer Client1 zu löschen, geben Sie Folgendes ein:

```
rundll32 printui.dll PrintUIEntry /dn /n\\client1\printer1
```

Zum Hinzufügen einer pro-Computer-Druckerverbindung (printer2) für alle Benutzer eines Computers CLIENT2 geben Sie ein (die Verbindung wird angewendet, wenn sich ein Benutzer anmeldet):

```
rundll32 printui.dll PrintUIEntry /ga /n\\client2\printer2
```

Zum Löschen einer Druckerverbindung pro Computer printer2 geben Sie für alle Benutzer eines Computers CLIENT2 den Namen (die Verbindung wird bei der Anmeldung eines Benutzers gelöscht) ein:

```
rundll32 printui.dll PrintUIEntry /gd /n\\client2\printer2
```

Geben Sie Folgendes ein, um die Eigenschaften des Druck Servers printServer1 anzuzeigen:

```
rundll32 printui.dll PrintUIEntry /s /t1 /c\\printserver1
```

Zum Anzeigen der Eigenschaften eines Druckers, printer3, geben Sie Folgendes ein:
```
rundll32 printui.dll PrintUIEntry /p /n\\printer3
```

## <a name="additional-references"></a>Zusätzliche Referenzen

- [rundll32](rundll32.md)

- [Befehls Verweis drucken](print-command-reference.md)
