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
ms.openlocfilehash: 327ac844bec0e4c89ee1443c193aa628de038dea
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80837403"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell ist eine aufgabenbasierte Befehlszeilenshell und Skriptsprache, die speziell für die Systemverwaltung entwickelt wurde. Windows PowerShell basiert auf .NET Framework und unterstützt IT-Experten und erfahrene Benutzer beim Steuern und Automatisieren der Verwaltung von Windows-Betriebssystemen sowie von Anwendungen, die unter Windows ausgeführt werden.

Mit dem Befehlszeilen Tool " **PowerShell. exe** " wird in einem Eingabe Aufforderungs Fenster eine Windows PowerShell-Sitzung gestartet. Wenn Sie " **PowerShell. exe**" verwenden, können Sie die entsprechenden optionalen Parameter verwenden, um die Sitzung anzupassen. Beispielsweise können Sie eine Sitzung starten, die eine bestimmte Ausführungs Richtlinie verwendet, oder eine Sitzung, von der ein Windows PowerShell-Profil ausgeschlossen wird. Andernfalls ist die Sitzung mit jeder Sitzung identisch, die in der Windows PowerShell-Konsole gestartet wird.

## <a name="using-powershellexe"></a>Verwenden von "PowerShell. exe"

Sie können das Befehlszeilen Tool " **PowerShell. exe** " verwenden, um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu starten.

- Geben Sie `PowerShell`ein, um in einem Eingabe Aufforderungs Fenster eine Windows PowerShell-Sitzung zu starten. Der Eingabeaufforderung wird ein **PS** -Präfix hinzugefügt, um anzugeben, dass Sie sich in einer Windows PowerShell-Sitzung befinden.

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

- Um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu beenden, geben Sie `exit`ein. Die typische Eingabeaufforderung gibt zurück.

Eine komplette Liste der Befehlszeilenparameter von " **PowerShell. exe** " finden Sie unter [about_PowerShell. exe](https://go.microsoft.com/fwlink/?LinkID=113439).

## <a name="other-ways-to-start-windows-powershell"></a>Weitere Möglichkeiten zum Starten von Windows PowerShell

Informationen zu anderen Möglichkeiten zum Starten von Windows PowerShell finden Sie unter [Starten von Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=135259).

## <a name="remarks"></a>Hinweise

Windows PowerShell wird auf der Server Core-Installationsoption von Windows Server-Betriebssystemen ausgeführt. Features, die eine grafische Benutzeroberfläche erfordern, wie z. b. die [Windows PowerShell Integrated Scripting Environment (ISE)](https://technet.microsoft.com/library/hh849182)und die Cmdlets " [out-GridView](https://go.microsoft.com/fwlink/?LinkID=113364) " und " [Show-Command](https://go.microsoft.com/fwlink/?LinkID=217448) ", können jedoch nicht auf Server Core-Installationen ausgeführt werden.

## <a name="additional-references"></a>Weitere Verweise

[about_PowerShell. exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[about_PowerShell_Ise. exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Skripterstellung mit Windows PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) siehe auch