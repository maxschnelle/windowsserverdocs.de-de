---
title: winsat mfmedia
description: Verweis für WinSAT-MF-Medien, mit dem die Leistung der Video Decodierung (Wiedergabe) mithilfe des Media Foundation Frameworks gemessen wird.
ms.topic: reference
ms.assetid: 09a3b3dd-f746-4e6e-b684-76a9bde0c78d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 889ef018e5803f9905100b5ae0b65f1bc0c4093e
ms.sourcegitcommit: 96d46c702e7a9c3a321bbbb5284f73911c7baa3c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2020
ms.locfileid: "89038098"
---
# <a name="winsat-mfmedia"></a>winsat mfmedia



Misst die Leistung der Video Decodierung (Wiedergabe) mithilfe des Media Foundation Frameworks.



## <a name="syntax"></a>Syntax

```
winsat mfmedia <parameters>
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|----------|-----------|
|-Eingabe \<file name>|Erforderlich: Geben Sie die Datei an, die den Video Clip enthält, der abgespielt oder codiert werden soll. Die Datei kann in einem beliebigen Format vorliegen, das von Media Foundation gerendert werden kann.|
|-dumpgraph|Geben Sie an, dass das Filter Diagramm in einer mit GraphEdit kompatiblen Datei gespeichert werden soll, bevor die Bewertung beginnt.|
|-NS|Geben Sie an, dass das Filter Diagramm mit der normalen Wiedergabegeschwindigkeit der Eingabedatei ausgeführt werden soll. Standardmäßig wird das Filter Diagramm so schnell wie möglich ausgeführt, wobei Präsentations Zeiten ignoriert werden.|
|-Play|Führen Sie die Bewertung im Decodierungs Modus aus, und geben Sie alle bereitgestellten Audioinhalte in der in **-Input** angegebenen Datei mit dem DirectSound-Standardgerät wieder. Standardmäßig ist die Audiowiedergabe deaktiviert.|
|-nopmp|Verwenden Sie während der Bewertung nicht den mfpmp-Prozess (Media Foundation Protected Media Pipeline).|
|-PMP|Verwenden Sie immer den mfpmp-Prozess während der Bewertung.</br>Hinweis: Wenn **-PMP** oder **-nopmp** nicht angegeben ist, wird mfpmp nur bei Bedarf verwendet.|
|-v|Senden Sie eine ausführliche Ausgabe an stdout, einschließlich Status-und Fortschrittsinformationen. Alle Fehler werden auch in das Befehlsfenster geschrieben.|
|-XML \<file name>|Speichert die Ausgabe der Bewertung als die angegebene XML-Datei. Wenn die angegebene Datei vorhanden ist, wird sie überschrieben.|
|-idiskinfo|Speichern Sie Informationen zu physischen Volumes und logischen Datenträgern als Teil des **\<SystemConfig>** Abschnitts in der XML-Ausgabe.|
|-iguid|Erstellen Sie eine Globally Unique Identifier (GUID) in der XML-Ausgabedatei.|
|-Hinweis Text|Fügen Sie den Hinweis Text zum **\<note>** Abschnitt in der XML-Ausgabedatei hinzu.|
|-ICN|Fügen Sie den Namen des lokalen Computers in die XML-Ausgabedatei ein.|
|-EEF|Listet zusätzliche Systeminformationen in der XML-Ausgabedatei auf.|

## <a name="examples"></a>Beispiele

- Zum Ausführen der Bewertung mit der Eingabedatei, die bei einer **formalen WinSAT** -Bewertung verwendet wird, ohne die Media Foundation geschützte Medien Pipeline (mfpmp) auf einem Computer zu verwenden, auf dem "c:\Windows" der Speicherort des Windows-Ordners ist.
  ```
  winsat mfmedia -input c:\windows\performance\winsat\winsat.wmv -nopmp
  ```

## <a name="remarks"></a>Bemerkungen

-   Sie müssen mindestens Mitglied der lokalen Gruppe Administratoren oder einer entsprechenden Gruppe sein, um **WinSAT**verwenden zu können. Der Befehl muss von einem Eingabe Aufforderungs Fenster mit erhöhten Rechten ausgeführt werden.
-   Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**und auf **Zubehör**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

## <a name="additional-references"></a>Weitere Verweise

