---
title: PowerShell
description: Erfahren Sie, wie Sie die PowerShell-Konsole über eine Eingabeaufforderung öffnen.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: b733a187017293e8a33ff307b485380ef8f9b472
ms.sourcegitcommit: bf887504703337f8ad685d778124f65fe8c3dc13
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/16/2020
ms.locfileid: "83436565"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell ist eine aufgabenbasierte Befehlszeilenshell und Skriptsprache, die speziell für die Systemverwaltung entwickelt wurde. Windows PowerShell basiert auf .NET Framework und unterstützt IT-Experten und erfahrene Benutzer beim Steuern und Automatisieren der Verwaltung von Windows-Betriebssystemen sowie von Anwendungen, die unter Windows ausgeführt werden.

Mit dem Befehlszeilen Tool " **PowerShell. exe** " wird in einem Eingabe Aufforderungs Fenster eine Windows PowerShell-Sitzung gestartet. Wenn Sie " **PowerShell. exe**" verwenden, können Sie die entsprechenden optionalen Parameter verwenden, um die Sitzung anzupassen. Beispielsweise können Sie eine Sitzung starten, die eine bestimmte Ausführungs Richtlinie verwendet, oder eine Sitzung, von der ein Windows PowerShell-Profil ausgeschlossen wird. Andernfalls ist die Sitzung mit jeder Sitzung identisch, die in der Windows PowerShell-Konsole gestartet wird.

## <a name="using-powershellexe"></a>Verwenden von "PowerShell. exe"

Sie können das Befehlszeilen Tool " **PowerShell. exe** " verwenden, um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu starten.

- Um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu starten, geben Sie ein `PowerShell` . Der Eingabeaufforderung wird ein **PS** -Präfix hinzugefügt, um anzugeben, dass Sie sich in einer Windows PowerShell-Sitzung befinden.

- Verwenden Sie zum Starten einer Sitzung mit einer bestimmten Ausführungs Richtlinie den **ExecutionPolicy** -Parameter.

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Verwenden Sie den **NoProfile** -Parameter, um eine Windows PowerShell-Sitzung ohne Ihre Windows PowerShell-Profile zu starten.

    ```
    PowerShell.exe -NoProfile
    ```

- Verwenden Sie den **ExecutionPolicy** -Parameter, um eine Sitzung zu starten.

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Verwenden Sie das folgende Befehls Format, um die Hilfedatei von "PowerShell. exe" anzuzeigen.

    ```
    PowerShell.exe -help, -?, /?
    ```

- Um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu beenden, geben Sie ein `exit` . Die typische Eingabeaufforderung gibt zurück.

Eine komplette Liste der Befehlszeilenparameter von " **PowerShell. exe** " finden Sie unter [about_PowerShell. exe](https://go.microsoft.com/fwlink/?LinkID=113439).

## <a name="other-ways-to-start-windows-powershell"></a>Weitere Möglichkeiten zum Starten von Windows PowerShell

Informationen zu anderen Möglichkeiten zum Starten von Windows PowerShell finden Sie unter [Starten von Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=135259).

## <a name="remarks"></a>Hinweise

Windows PowerShell wird auf der Server Core-Installationsoption von Windows Server-Betriebssystemen ausgeführt. Features, die eine grafische Benutzeroberfläche erfordern, wie z. b. die [Windows PowerShell Integrated Scripting Environment (ISE)](https://technet.microsoft.com/library/hh849182)und die Cmdlets " [out-GridView](https://go.microsoft.com/fwlink/?LinkID=113364) " und " [Show-Command](https://go.microsoft.com/fwlink/?LinkID=217448) ", können jedoch nicht auf Server Core-Installationen ausgeführt werden.

## <a name="additional-references"></a>Zusätzliche Referenzen

[about_PowerShell. exe](https://go.microsoft.com/fwlink/?LinkID=113439) 
 [about_PowerShell_Ise. exe](https://go.microsoft.com/fwlink/?LinkId=256512) 
 [Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116) 
 [Skripterstellung mit Windows PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) Siehe auch