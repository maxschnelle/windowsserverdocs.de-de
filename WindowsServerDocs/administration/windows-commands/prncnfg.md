---
title: prncnfg
description: Erfahren Sie, wie Sie einen Drucker mit dem Befehl Prncfg konfigurieren.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 6426b053a5c56918768f82cbd7631631abcf0a6f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59859151"
---
# <a name="prncnfg"></a>prncnfg

>Gilt für: WindowsServer (Halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Konfiguriert, oder Zeigt Konfigurationsinformationen zu einem Drucker aus.

## <a name="syntax"></a>Syntax
```
cscript Prncnfg {-g | -t | -x | -?} [-S <ServerName>] [-P <printerName>] [-z <NewprinterName>] [-u <UserName>] [-w <Password>] [-r <PortName>] [-l <Location>] [-h <Sharename>] [-m <Comment>] [-f <SeparatorFileName>] [-y <Datatype>] [-st <starttime>] [-ut <Untiltime>] [-i <DefaultPriority>] [-o <Priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-g|Zeigt die Konfigurationsinformationen zu einem Drucker.|
|-t|Konfiguriert einen Drucker an.|
|-x|Benennt einen Drucker an.|
|-S \<ServerName\>|Gibt den Namen des Remotecomputers, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie einen Computer nicht angeben, wird der lokale Computer verwendet.|
|-P \<Druckername\>|Gibt den Namen des Druckers, den Sie verwalten möchten. Erforderlich.|
|-z \<NewprinterName\>|Gibt den neuen Druckernamen an. Erfordert die **- X** und **-P** Parameter.|
|-u \<Benutzername\> -w \<Kennwort\>|Gibt ein Konto mit Berechtigungen zum Verbinden mit dem Computer, der den Drucker hostet, den Sie verwalten möchten. Alle Mitglieder der lokalen Gruppe Administratoren des Zielcomputers über diese Berechtigungen verfügen, aber die Berechtigungen können auch für andere Benutzer erteilt werden. Wenn Sie ein Konto nicht angeben, müssen Sie über ein Konto mit Berechtigungen für der Befehl funktioniert angemeldet sein.|
|-R \<PortName\>|Gibt den Port, den Drucker verbunden ist. Ist dies einer parallelen oder seriellen Anschluss, klicken Sie dann verwenden Sie die ID des Ports (z. B. "LPT1" oder "COM1"). Ist dies ein TCP/IP-Port, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde.|
|-l \<Speicherort\>|Gibt den Drucker an, wie z. B. "Kopieren Platz."|
|-h \<Freigabename\>|Gibt den Namen des Druckers Freigabe an.|
|-m \<Kommentar\>|Gibt die Kommentarzeichenfolge des Druckers an.|
|-f \<SeparatorFileName\>|Gibt eine Datei mit dem Text, der auf der Seite "Trennzeichen" angezeigt wird.|
|/ y \<Datatype\>|Gibt an, die Datentypen, die der Drucker akzeptieren kann.|
|St - \<"StartTime"\>|Konfiguriert den Drucker, für die eingeschränkte Verfügbarkeit. Gibt die Zeit des Tages, die der Drucker verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument (gespoolten) aufbewahrt, bis der Drucker verfügbar ist. Sie müssen die Zeit als 24-Stunden-Format angeben. Um 23:00 Uhr anzugeben, geben Sie z. B. **2300**.|
|-Ut \<"EndTime"\>|Konfiguriert den Drucker, für die eingeschränkte Verfügbarkeit. Gibt die Zeit des Tages, die der Drucker nicht mehr verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument (gespoolten) aufbewahrt, bis der Drucker verfügbar ist. Sie müssen die Zeit als 24-Stunden-Format angeben. Um 23:00 Uhr anzugeben, geben Sie z. B. **2300**.|
|-o \<Priorität\>|Gibt eine Priorität, die der Spooler zum Weiterleiten von Druckaufträgen in der Warteschlange verwendet. Eine Druckwarteschlange, die mit einer höheren Priorität erhält alle ihre Aufträge vor alle Warteschlangen mit niedrigerer Priorität.|
|-i \<DefaultPriority\>|Gibt die Standardpriorität für jeden Druckauftrag zugewiesen.|
|{+&#124;-}shared|Gibt an, ob der Drucker im Netzwerk freigegeben ist.|
|{+&#124;-}direct|Gibt an, ob das Dokument direkt an den Drucker gesendet werden soll, ohne in die Warteschlange gestellt wird.|
|{+&#124;-}published|Gibt an, ob der Drucker im active Directory veröffentlicht werden sollen. Wenn Sie den Drucker veröffentlichen, können andere Benutzer für sie basierend auf den Speicherort und Funktionen (z. B. Farbe, Drucken und Heften) suchen.|
|{+&#124;-}hidden|Reservierte-Funktion.|
|{+&#124;-}rawonly|Gibt an, ob nur die Druckaufträge Rohdaten in dieser Warteschlange gespoolt werden können.|
|{+ &#124; -}queued|Gibt an, dass der Drucker nicht begonnen werden soll, um bis zu drucken, nach die letzte Seite des Dokuments beginnen. Die Druck-Anwendung ist nicht verfügbar, bis das Dokument gedruckt wurde. Mithilfe dieses Parameters wird jedoch sichergestellt, dass das gesamte Dokument an den Drucker verfügbar ist.|
|{+ &#124; -}keepprintedjobs|Gibt an, ob die Druckwarteschlange Dokumente beibehalten werden sollen, nachdem sie gedruckt werden. Aktivieren diese Option ermöglicht einem Benutzer, aus der Druckwarteschlange statt aus dem Programm drucken ein Dokuments an den Drucker erneut zu übermitteln.|
|{+ &#124; -}workoffline|Gibt an, ob ein Benutzer Druckaufträge auf die Druckwarteschlange senden, wenn der Computer nicht mit dem Netzwerk verbunden ist.|
|{+ &#124; -}enabledevq|Gibt an, ob die Druckaufträge, die nicht die Druckereinrichtung (z. B. Dateien, die auf nicht-PostScript-Drucker gespoolten PostScript) entsprechen, die in der Warteschlange gespeichert werden soll statt gedruckt wird.|
|{+ &#124; -}docompletefirst|Gibt an, ob die Druckwarteschlange Druckaufträge mit einer niedrigeren Priorität senden soll, die abgeschlossen sind, Spoolen vor dem Senden von Druckaufträgen mit einer höheren Priorität, die nicht die Aufträge abgeschlossen wurden. Wenn diese Option aktiviert ist, und keine Dokumente Aufträge abgeschlossen wurden, sendet der Spooler großer Dokumente vor kleineren. Sie sollten diese Option aktivieren, wenn zur Maximierung der Effizienz der Drucker Auftragspriorität werden sollen. Wenn diese Option deaktiviert ist, sendet der Spooler immer Aufträge mit höherer Priorität an ihre jeweiligen Warteschlangen zuerst.|
|{+ &#124; -}enablebidi|Gibt an, ob der Drucker Statusinformationen an den Spooler sendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Die **Prncnfg** Befehl ist eine Visual Basic-Skript befindet sich in der %WINdir%\System32\printing_Admin_Scripts\\ <language> Verzeichnis. Um diesen Befehl an einer Eingabeaufforderung verwenden möchten, geben **Cscript** gefolgt von den vollständigen Pfad und die Prncnfg-Datei, oder wechseln in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg
    ```
-   Wenn die Informationen, die Sie angeben, die Leerzeichen enthält, verwenden Sie den Text in Anführungszeichen (z. B. `"computer Name"`).

## <a name="BKMK_examples"></a>Beispiele für
Zum Anzeigen von Konfigurationsinformationen für den Drucker mit dem Namen "Farbdrucker_2", und eine Druckwarteschlange, die von dem remote-Computer mit dem Namen HRServer gehostet wird, geben Sie Folgendes ein:
```
cscript prncnfg -g -S HRServer -P colorprinter_2 
```

Geben Sie zum Konfigurieren eines Druckers mit dem Namen Farbdrucker_2, so, dass der Spooler auf dem Remotecomputer mit dem Namen HRServer Druckaufträge speichert, nachdem sie ausgegeben wurden:
```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs 
```

So ändern Sie den Namen eines Druckers auf dem Remotecomputer mit dem Namen HRServer aus Farbdrucker_2 zu Colorprinter 3, Typ:
```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3" 
```

#### <a name="additional-references"></a>Zusätzliche Referenzen
[Befehlszeilen-Syntaxschlüssel](command-line-syntax-key.md)
[druckbefehlsreferenz](print-command-reference.md)
