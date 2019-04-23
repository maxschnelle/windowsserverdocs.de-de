---
title: printui.dll, rundll32 PrintUIEntry
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 12fb48b6-5dd8-4cc0-8808-e6a681aceb84 jpjofre
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/25/2018
ms.openlocfilehash: c90641820bfa01c19ae7bf587c5467d3f9c5a01c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836841"
---
# <a name="rundll32-printuidllprintuientry"></a>printui.dll, rundll32 PrintUIEntry

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Automatisiert viele Konfigurationsaufgaben für Drucker. printui.dll ist die ausführbare Datei, die von den Dialogfeldern der Drucker-Konfiguration verwendete Funktionen enthält. Diese Funktionen können auch in ein Skript oder eine Batchdatei für die Befehlszeile aus aufgerufen werden, oder sie können über die Eingabeaufforderung interaktiv ausgeführt werden. Beispiele wie dieser Befehl verwendet werden kann, finden Sie unter [Beispiele](#BKMK_Examples).  
## <a name="syntax"></a>Syntax  
```  
rundll32 printui.dll PrintUIEntry [BaseParameter] [ModificationParameter1] [ModificationParameter2] [ModificationParameterN]  
```  
Sie können auch die folgenden alternativen Syntaxen verwenden, obwohl in die Beispielen in diesem Thema auf die vorherige Syntax verwenden:  
```  
rundll32 printui.dll,PrintUIEntry [BaseParameter] [ModificationParameter1] [ModificationParameter2] [ModificationParameterN]  
```  
```  
rundll32 printui PrintUIEntry [BaseParameter] [ModificationParameter1] [ModificationParameter2] [ModificationParameterN]  
```  
```  
rundll32 printui,PrintUIEntry [BaseParameter] [ModificationParameter1] [ModificationParameter2] [ModificationParameterN]  
```  
## <a name="parameters"></a>Parameter  
Es gibt zwei Arten von Parametern: Basis-Parameter und Änderung. Basisparameter Geben Sie die Funktion, die der Befehl ausführen. Nur einer dieser Parameter kann in einer angegebenen Befehlszeile angezeigt werden. Anschließend können Sie die Basis-Parameter ändern, mit mindestens einer der Parameter geändert, wenn sie auf der Basis-Parameter anwendbar sind (nicht alle Änderungen-Parameter werden von allen basisparameter unterstützt).  
|Basis-Parameter|Beschreibung|  
|----------|--------|  
|/dl|Löscht den lokalen Drucker.|  
|/dn|Löscht eine Netzwerkverbindung für den Drucker.|  
|/dd|Löscht einen Druckertreiber.|  
|/ e|Zeigt die druckeinstellungen für einen bestimmten Drucker an.|  
|/ga|Fügt eine pro Computer Druckerverbindung (die Verbindung ist für alle Benutzer auf diesem Computer verfügbar, wenn sie sich anmelden).|  
|/ ge|Zeigt pro Computer druckerverbindungen auf einem Computer an.|  
|/gd|Löscht eine pro Computer Druckerverbindung (die Verbindung wird das nächste Mal ein Benutzer sich meldet gelöscht).|  
|/ia|Installiert einen Druckertreiber mit einer INF-Datei an.|  
|/id|Installiert einen Druckertreiber mithilfe des hinzufügen-Druckers Treiberimport-Assistenten.|  
|/if|Installiert einen Drucker mit einer INF-Datei.|  
|/ii|Installiert einen Drucker mit dem Druckerinstallations-Assistenten mit einer INF-Datei an.|  
|/il|Installiert einen Drucker mit dem Druckerinstallations-Assistenten.|  
|/in|Eine Verbindung mit einem Remotenetzwerk-Drucker.|  
|/ip|Installiert einen Drucker mit der Netzwerkdrucker-Installations-Assistenten (über die Benutzeroberfläche aus mit der Druckverwaltung verfügbar).|  
|/k|Gibt eine Testseite auf einem Drucker aus.|  
|/o|Zeigt die Warteschlange für einen Drucker an.|  
|/p|Zeigt die Eigenschaften eines Druckers. Wenn Sie diesen Parameter verwenden, müssen Sie auch angeben, auf einen Wert für den Parameter für die Änderung **/ [Name] n**.|  
|/s|Zeigt die Eigenschaften eines Druckservers. Wenn Sie den lokalen Druckerserver anzeigen möchten, müssen Sie keinen Parameter für die Änderung zu verwenden. Aber wenn Sie eine Remotedruckerserver anzeigen möchten, müssen Sie angeben der **/c [Name]** Änderung-Parameter.|  
|/Ss|Gibt an, welche Art von Informationen für einen Drucker gespeichert werden. Wenn keiner der Werte für **/ss** angegeben sind, wird das Standardverhalten ist, als ob alle von ihnen angegeben wurden. Verwenden Sie diese Basis-Parameter mit den folgenden Werten, die am Ende der Befehlszeile platziert:<br /><br />-   **2**: Verwenden Sie zum Speichern der Informationen in der Drucker s printER_INFO_2 Struktur enthalten. Diese Struktur enthält die grundlegende Informationen über den Drucker wie z. B. Name, Servername, Portnamen und Freigabenamen an.<br />-   **7**: Verwenden Sie zum Speichern der Directory-Dienst-Informationen in der Struktur printER_INFO_7 enthalten.<br />-   **c**: Verwenden Sie, um die Farbe Profilinformationen für einen Drucker zu speichern.<br />-   **d**: Verwenden Sie zum Speichern von Drucker bestimmte Daten wie z. B. die Drucker s Hardware-ID<br />-   **s**: Verwenden Sie, um die Sicherheitsbeschreibung für den Drucker s zu speichern.<br />-   **g**: Verwenden Sie zum Speichern der Informationen in der globalen Drucker s-DEVmode-Struktur.<br />-   **m**: Verwenden Sie die mindesteinstellungen für den Drucker zu speichern. Dies ist gleichbedeutend mit der Angabe **2** **d**, und **g**.<br />-   **u**: Verwenden Sie zum Speichern der Informationen im Drucker s pro Benutzer DEVmode-Struktur.|  
|/Sr|Gibt an, welche Informationen über einen Drucker wiederhergestellt wird und wie Konflikte bei Einstellungen behandelt werden. Verwenden Sie die folgenden Werte, die am Ende der Befehlszeile platziert:<br /><br />-   **2**: Verwenden Sie die Informationen in der Drucker s printER_INFO_2 Struktur wiederhergestellt. Diese Struktur enthält die grundlegende Informationen über den Drucker wie z. B. Name, Servername, Portnamen und Freigabenamen an.<br />-   **7**: Verwenden Sie zum Wiederherstellen der Service-Verzeichnisinformationen, die in der Struktur printER_INFO_7 enthalten.<br />-   **c**: Verwenden Sie zum Wiederherstellen der Color-Profilinformationen für einen Drucker.<br />-   **d**: Verwenden Sie zum Wiederherstellen von Drucker bestimmten Daten, z. B. die Drucker s Hardware-ID<br />-   **s**: Verwenden Sie, um die Sicherheitsbeschreibung für den Drucker s wiederherstellen.<br />-   **g**: Verwenden Sie zum Wiederherstellen der Informationen in der globalen Drucker s-DEVmode-Struktur.<br />-   **m**: Verwenden Sie zum Wiederherstellen der mindesteinstellungen für den Drucker. Dies ist gleichbedeutend mit der Angabe **2**, **d**, und **g**.<br />-   **u** verwenden, um die Informationen in der Print-s pro Benutzer DEVmode-Struktur wiederherzustellen.<br />-   **R**: den Namen des Druckers in der Datei gespeichert, den Namen des Druckers zum wiederhergestellt unterscheidet, verwenden Sie dann den Namen des aktuellen Druckers. Dies kann nicht angegeben werden, mit **f**. Wenn weder **r** noch **f** angegeben ist und die Namen stimmen nicht überein, schlägt fehl, die Wiederherstellung der Einstellungen.<br />-   **f**: ist der Druckername, der in der Datei gespeicherten sich vom Namen des Druckers wiederhergestellt wird, verwenden Sie den Namen des Druckers in der Datei. Dies kann nicht angegeben werden, mit **r**. Wenn weder **f** noch **r** angegeben ist und die Namen stimmen nicht überein, schlägt fehl, die Wiederherstellung der Einstellungen.<br />-   **p**: Wenn es sich bei der Portnamen, in der Datei, die wiederhergestellt wird, über den aktuellen Portname des Druckers wiederhergestellt wird, um nicht übereinstimmt, wird der aktuellen Drucker s-Port-Name verwendet.<br />-   **h**: Wenn der Drucker, die Sie wiederherstellen nicht mithilfe der Ressourcenname für die Freigabe in der gespeicherten Datei freigegeben werden kann, klicken Sie dann versuchen, den Drucker mit den aktuellen Freigabenamen oder einen neuen Freigabenamen der generierten freizugeben, wenn weder **H**noch **h** angegeben ist und wiederherzustellende wird, um Drucker kann nicht mit dem gespeicherten Freigabenamen freigegeben werden, schlägt die Wiederherstellung fehl.<br />-   **h**: Wenn der Drucker, die wiederhergestellt wird, um mit dem gespeicherten Freigabenamen gemeinsam genutzt werden kann, klicken Sie dann weisen nicht den Drucker. Wenn weder **H** noch **h** angegeben ist und wiederherzustellende wird, um Drucker kann nicht mit dem gespeicherten Freigabenamen freigegeben werden, schlägt die Wiederherstellung fehl.<br />-   **ich**: Wenn der Treiber in der gespeicherten Datei nicht des Treibers für den Drucker entspricht, die Sie wiederherstellen, und klicken Sie dann die Wiederherstellung ein Fehler auftritt.|  
|/Xg|Ruft die Einstellungen für einen Drucker ab.|  
|/Xs|Legt die Einstellungen für einen Drucker fest.|  
|/y|Legt fest, den Drucker als den Standarddrucker installiert wird.|  
|/?|Zeigt die Hilfe im Produkt für den Befehl und die dazugehörigen Parameter.|  
|@[file]|Gibt eine Befehlszeilenargument-Datei und fügt den Text direkt in der Datei, in der Befehlszeile aus.|  
|Änderung von Parameter|Beschreibung|  
|--------------|--------|  
|/ a [Datei]|Gibt den Namen der Binärdatei.|  
|/b[name]|Gibt den base Druckernamen an.|  
|/c[name]|Gibt den Namen des Computers, auf einem Remotecomputer ist die Aktion ausgeführt werden.|  
|/f[file]|Gibt den Pfad für die Universal Naming Convention (UNC) und der Name der INF-Dateiname oder der Name der Ausgabedatei, abhängig von der Aufgabe, die Sie ausführen. Verwendung **/f [Datei]** eine abhängige INF-Datei angeben.|  
|/ F [Datei]|Gibt den UNC-Pfad und den Namen der INF-Datei, die mit die INF-Datei angegeben **/f [Datei]** abhängig.|  
|/h[architecture]|Gibt an, die Treiberarchitektur dar. Verwenden Sie eine der folgenden: **X86**, **X64**, oder **Itanium**.|  
|/ j [Provider]|Gibt den Anbieternamen der print.|  
|/l[path]|Gibt den UNC-Pfad, in dem die Dateien für den Druckertreiber, die Sie verwenden befinden.|  
|/m[model]|Gibt den Namen des Treibers-Modell an. (Dieser Wert kann in der INF-Datei angegeben werden.)|  
|/ n [Name]|Gibt den Namen des Druckers an.|  
|/q|Führt den Befehl ohne Benachrichtigungen für den Benutzer an.|  
|/r[port]|Gibt den Namen des Anschlusses.|  
|/u|Gibt an, um den vorhandenen Druckertreiber zu verwenden, wenn es bereits installiert ist.|  
|/t[#]|Gibt den nullbasierten Indexseite starten Sie auf.|  
|/v[version]|Gibt die Version des Treibers. Wenn Sie einen Wert für nicht gleichzeitig angeben **/k**, müssen Sie einen der folgenden Werte angeben: **Typ 2 - Kernelmodus** oder **Typ 3 - Benutzermodus**.|  
|/w|fordert den Benutzer für einen Treiber der Treiber nicht in der INF-Datei gefunden wird, der angegebenen **/f**.|  
|/ Y|Gibt an, dass die Druckernamen nicht automatisch generiert werden soll.|  
|/z|Gibt an, die nicht automatisch freigeben des Druckers installiert wird.|  
|/K|Ändert die Bedeutung des Parameters **/h [Architektur]** akzeptieren **2** anstelle von **X86**, **3** anstelle von **X64**, oder **4** anstelle von **Itanium**. Wird auch den Wert des Parameters geändert **/v [Version]** akzeptieren **2** an die Stelle von **Typ 2 - Kernelmodus** und **3** anstelle **Typ 3 - Benutzermodus**.|  
|/Z|Gibt den Drucker, der installiert ist. Verwenden Sie nur für die **/if** Parameter.|  
|/Mw[message]|Zeigt eine Warnmeldung an, die dem Benutzer vor dem Commit der Änderungen, die in der Befehlszeile angegeben.|  
|/Mq[message]|Zeigt eine bestätigungsmeldung an, die dem Benutzer vor dem Commit der Änderungen, die in der Befehlszeile angegeben.|  
|/ W [Flags]|Gibt alle Parameter oder die Optionen für den Druckerinstallations-Assistenten den Drucker hinzufügen Treiberimport-Assistent und der Netzwerkdrucker-Installations-Assistenten.<br /><br />**r**: Können die Assistenten neu gestartet werden, von der letzten Seite.|  
|/ G [Flags]|Gibt an, globalen Parametern und Optionen, die Sie verwenden möchten.<br /><br />**w**: Unterdrückt die Setup-Treiber Warnungen für den Benutzer.|  
## <a name="remarks"></a>Hinweise  
-   Die **PrintUIEntry** Schlüsselwort ist Groß-/Kleinschreibung beachtet, und Sie müssen die Syntax für diesen Befehl eingeben, mit der gewünschten Großschreibung, die in den Beispielen in diesem Thema gezeigt.  
-   Finden Sie unter [Beispiele](#BKMK_Examples) in diesem Dokument für die Syntax für einige allgemeinen Aufgaben. Weitere Beispiele, die an einer Eingabeaufforderung Folgendes: **printui.dll, rundll32 PrintUIEntry /?**  
## <a name="BKMK_Examples"></a>Beispiele für  
Um einen neuen remote Drucker Drucker1, für einen Computer Client1 hinzufügen angezeigt wird für das Benutzerkonto an, in dem dieser Befehl ausgeführt wird, geben Sie Folgendes ein:  
```  
rundll32 printui.dll PrintUIEntry /in /n\\client1\printer1  
```  
Zum Hinzufügen eines Druckers, verwenden den Drucker hinzufügen befinden sich im Assistenten und mithilfe einer INF-Datei, InfFile.inf, auf Laufwerk c: auf Infpath, Typ:  
```  
rundll32 printui.dll PrintUIEntry /ii /f c:\Infpath\InfFile.inf  
```  
So löschen Sie einen vorhandenen Drucker, Drucker1, auf einem Computer (Client1)  
```  
rundll32 printui.dll PrintUIEntry /dn /n\\client1\printer1  
```  
Hinzufügen einer pro Computer Druckerverbindung, Drucker2, für alle Benutzer eines Computer Client2-Typs (die Verbindung angewendet werden, wenn ein Benutzer anmeldet):  
```  
rundll32 printui.dll PrintUIEntry /ga /n\\client2\printer2  
```  
So löschen Sie eine pro Computer Druckerverbindung, Drucker2, für alle Benutzer eines Computer Client2-Typs (die Verbindung werden gelöscht, wenn ein Benutzer anmeldet):  
```  
rundll32 printui.dll PrintUIEntry /gd /n\\client2\printer2  
```  
Zum Anzeigen der Eigenschaften des Druckerservers, dem Namen printServer1, geben Sie Folgendes ein:  
```  
rundll32 printui.dll PrintUIEntry /s /t1 /c\\printserver1  
```  
Zum Anzeigen der Eigenschaften eines Druckers, printer3, geben Sie Folgendes ein:  
```  
rundll32 printui.dll PrintUIEntry /p /n\\printer3  
```  
## <a name="additional-references"></a>Zusätzliche Referenzen  
  
-   [rundll32](rundll32.md)  
-   [Druckbefehlsreferenz](print-command-reference.md)  
