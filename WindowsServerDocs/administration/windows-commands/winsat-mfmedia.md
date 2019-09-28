---
title: WinSAT-MF-Medien
description: Windows-Befehle
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 09a3b3dd-f746-4e6e-b684-76a9bde0c78d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 3684d4b23ba6d34febe226f54b8b2ab2204f610c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361899"
---
# <a name="winsat-mfmedia"></a>WinSAT-MF-Medien



Misst die Leistung der Video Decodierung (Wiedergabe) mithilfe des Media Foundation Frameworks.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
winsat mfmedia <parameters>
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|----------|-----------|
|-Eingabe \<dateiname >|Erforderlich: Geben Sie die Datei an, die den zu Wiedergabe enden oder zu codierenden Videoclip enthält. Die Datei kann in einem beliebigen Format vorliegen, das von Media Foundation gerendert werden kann.|
|-dumpgraph|Geben Sie an, dass das Filter Diagramm in einer mit GraphEdit kompatiblen Datei gespeichert werden soll, bevor die Bewertung beginnt.|
|-NS|Geben Sie an, dass das Filter Diagramm mit der normalen Wiedergabegeschwindigkeit der Eingabedatei ausgeführt werden soll. Standardmäßig wird das Filter Diagramm so schnell wie möglich ausgeführt, wobei Präsentations Zeiten ignoriert werden.|
|-Play|Führen Sie die Bewertung im Decodierungs Modus aus, und geben Sie alle bereitgestellten Audioinhalte in der in **-Input** angegebenen Datei mit dem DirectSound-Standardgerät wieder. Standardmäßig ist die Audiowiedergabe deaktiviert.|
|-nopmp|Verwenden Sie während der Bewertung nicht den mfpmp-Prozess (Media Foundation Protected Media Pipeline).|
|-PMP|Verwenden Sie immer den mfpmp-Prozess während der Bewertung.</br>Hinweis: Wenn **-PMP** oder **-nopmp** nicht angegeben ist, wird mfpmp nur bei Bedarf verwendet.|
|-v|Senden Sie eine ausführliche Ausgabe an stdout, einschließlich Status-und Fortschrittsinformationen. Alle Fehler werden auch in das Befehlsfenster geschrieben.|
|-XML \<-Dateiname >|Speichert die Ausgabe der Bewertung als die angegebene XML-Datei. Wenn die angegebene Datei vorhanden ist, wird sie überschrieben.|
|-idiskinfo|Speichern Sie Informationen zu physischen Volumes und logischen Datenträgern als Teil des  **\<SystemConfig->** Abschnitts in der XML-Ausgabe.|
|-iguid|Erstellen Sie eine Globally Unique Identifier (GUID) in der XML-Ausgabedatei.|
|-Hinweis "Hinweis Text"|Fügen Sie den Hinweis Text  **\<dem Abschnitt Notiz >** in der XML-Ausgabedatei hinzu.|
|-ICN|Fügen Sie den Namen des lokalen Computers in die XML-Ausgabedatei ein.|
|-EEF|Listet zusätzliche Systeminformationen in der XML-Ausgabedatei auf.|

## <a name="BKMK_examples"></a>Beispiele

- Im folgenden Beispiel wird die Bewertung mit der Eingabedatei ausgeführt, die während einer **formalen WinSAT** -Bewertung verwendet wird, ohne dass die Media Foundation Protected Media Pipeline (mfpmp) auf einem Computer verwendet wird, auf dem "c:\Windows" der Speicherort des Windows-Ordners ist.  
  ```
  winsat mfmedia -input c:\windows\performance\winsat\winsat.wmv -nopmp
  ```

## <a name="remarks"></a>Hinweise

-   Sie müssen mindestens Mitglied der lokalen Gruppe Administratoren oder einer entsprechenden Gruppe sein, um **WinSAT**verwenden zu können. Der Befehl muss von einem Eingabe Aufforderungs Fenster mit erhöhten Rechten ausgeführt werden.
-   Klicken Sie zum Öffnen einer Eingabeaufforderung mit erhöhten Rechten auf **Start**und auf **Zubehör**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie dann auf **als Administrator ausführen**.

#### <a name="additional-references"></a>Weitere Verweise

