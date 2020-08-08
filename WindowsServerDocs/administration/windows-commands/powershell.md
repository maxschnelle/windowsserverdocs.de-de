---
title: PowerShell
description: Referenz Artikel für den PowerShell-Befehl, mit dem die PowerShell-Konsole über eine Eingabeaufforderung geöffnet wird.
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 29751bdb6f17c167ffa17170be24c302fda557fd
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87991154"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell ist eine aufgabenbasierte Befehlszeilenshell und Skriptsprache, die speziell für die Systemverwaltung entwickelt wurde. Windows PowerShell basiert auf .NET Framework und unterstützt IT-Experten und erfahrene Benutzer beim Steuern und Automatisieren der Verwaltung von Windows-Betriebssystemen sowie von Anwendungen, die unter Windows ausgeführt werden.

## <a name="using-powershellexe"></a>Verwenden von PowerShell.exe

Mit dem Befehlszeilen Tool **PowerShell.exe** wird eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster gestartet. Wenn Sie **PowerShell.exe**verwenden, können Sie die zugehörigen optionalen Parameter verwenden, um die Sitzung anzupassen. Beispielsweise können Sie eine Sitzung starten, die eine bestimmte Ausführungs Richtlinie verwendet, oder eine Sitzung, von der ein Windows PowerShell-Profil ausgeschlossen wird. Andernfalls ist die Sitzung mit jeder Sitzung identisch, die in der Windows PowerShell-Konsole gestartet wird.

- Um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu starten, geben Sie ein `PowerShell` . Der Eingabeaufforderung wird ein **PS** -Präfix hinzugefügt, um anzugeben, dass Sie sich in einer Windows PowerShell-Sitzung befinden.

- Verwenden Sie zum Starten einer Sitzung mit einer bestimmten Ausführungs Richtlinie den **ExecutionPolicy** -Parameter, und geben Sie Folgendes ein:

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Verwenden Sie zum Starten einer Windows PowerShell-Sitzung ohne Ihre Windows PowerShell-Profile den **NoProfile** -Parameter, und geben Sie Folgendes ein:

    ```powershell
    PowerShell.exe -NoProfile
    ```

- Um eine Sitzung zu starten, verwenden Sie den **ExecutionPolicy** -Parameter, und geben Sie Folgendes ein:

    ```powershell
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Wenn Sie die PowerShell.exe Hilfedatei anzeigen möchten, geben Sie Folgendes ein:

    ```powershell
    PowerShell.exe -help
    PowerShell.exe -?
    PowerShell.exe /?
    ```

- Um eine Windows PowerShell-Sitzung in einem Eingabe Aufforderungs Fenster zu beenden, geben Sie ein `exit` . Die typische Eingabeaufforderung gibt zurück.

### <a name="remarks"></a>Hinweise

- Eine umfassende Liste der **PowerShell.exe** Befehlszeilenparameter finden Sie unter [about_PowerShell.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe).

- Informationen zu anderen Möglichkeiten zum Starten von Windows PowerShell finden Sie unter [Starten von Windows PowerShell](/powershell/scripting/windows-powershell/starting-windows-powershell).

- Windows PowerShell wird auf der Server Core-Installationsoption von Windows Server-Betriebssystemen ausgeführt. Features, die eine grafische Benutzeroberfläche erfordern, wie z. b. die [Windows PowerShell Integrated Scripting Environment (ISE)](/previous-versions/hh849182(v=technet.10))und die Cmdlets " [out-GridView](/powershell/module/microsoft.powershell.utility/out-gridview) " und " [Show-Command](/powershell/module/microsoft.powershell.utility/show-command) ", werden jedoch nicht auf Server Core-Installationen ausgeführt.

## <a name="additional-references"></a>Weitere Verweise

- [about_PowerShell.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe)

- [about_PowerShell_Ise.exe](/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe)

- [Windows PowerShell](/powershell/)
