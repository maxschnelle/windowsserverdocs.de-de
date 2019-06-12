---
title: PowerShell
description: Erfahren Sie, wie die PowerShell-Konsole über eine Eingabeaufforderung zu öffnen.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 694fc970-0b6c-4046-b1b5-7eb1a0d26609
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 1e2ccf6187e4480f94b30632b6f8f9f092052541
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/07/2019
ms.locfileid: "66811074"
---
# <a name="powershell"></a>PowerShell

Windows PowerShell ist eine aufgabenbasierte Befehlszeilenshell und Skriptsprache, die speziell für die systemverwaltung entwickelt wurde. Windows PowerShell basiert auf .NET Framework und unterstützt IT-Experten und erfahrene Benutzer beim Steuern und Automatisieren der Verwaltung von Windows-Betriebssystemen sowie von Anwendungen, die unter Windows ausgeführt werden.

Die **PowerShell.exe** Befehlszeilentool startet eine Windows PowerShell-Sitzung in einem Eingabeaufforderungsfenster. Bei Verwendung von **PowerShell.exe**, Sie können ihrer optionalen Parameter verwenden, um die Sitzung anzupassen. Beispielsweise können Sie eine Sitzung starten, die einer bestimmten Ausführungsrichtlinie oder eine, die ein Windows PowerShell-Profil schließt verwendet. Andernfalls ist mit die Sitzung identisch mit einer beliebigen Sitzung, die in der Windows PowerShell-Konsole gestartet wird.

## <a name="using-powershellexe"></a>Verwenden von PowerShell.exe

Sie können die **PowerShell.exe** Befehlszeilentool, mit eine Windows PowerShell-Sitzung in einem Eingabeaufforderungsfenster starten.

- Geben Sie zum Starten einer Windows PowerShell-Sitzungs in einem Eingabeaufforderungsfenster `PowerShell`. Ein **PS** Präfix wird an der Eingabeaufforderung aus, um anzugeben, dass Sie in einer Windows PowerShell-Sitzung hinzugefügt.

- Verwenden Sie zum Starten einer Sitzungs mit einer bestimmten Ausführung der **ExecutionPolicy** Parameter.

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```

- Verwenden Sie zum Starten einer Windows PowerShell-Sitzungs, ohne Ihre Windows PowerShell-Profile die **NoProfile** Parameter.

    ```
    PowerShell.exe -NoProfile
    ```
  
- Verwenden Sie zum Starten einer Sitzungs die **ExecutionPolicy** Parameter.

    ```
    PowerShell.exe -ExecutionPolicy Restricted
    ```
  
- Um die Hilfedatei PowerShell.exe anzuzeigen, verwenden Sie das folgende Befehlsformat.  
    
    ```
    PowerShell.exe -help, -?, /?
    ```

- Geben Sie zum Beenden einer Windows PowerShell-Sitzungs in einem Eingabeaufforderungsfenster `exit`. Die typische Eingabeaufforderung kehrt zurück.

Eine vollständige Liste der **PowerShell.exe** Befehlszeilenparameter, finden Sie unter [about_PowerShell.Exe](https://go.microsoft.com/fwlink/?LinkID=113439).

## <a name="other-ways-to-start-windows-powershell"></a>Weitere Informationen zum Starten von Windows PowerShell

Weitere Informationen über andere Möglichkeiten zum Starten von Windows PowerShell finden Sie unter [Starten von Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=135259).

## <a name="remarks"></a>Hinweise

Windows PowerShell wird auf die Server Core-Installationsoption von Windows Server-Betriebssysteme ausgeführt werden. Jedoch Features, die einen grafischen Benutzer erfordern Schnittstelle, z. B. die [Windows PowerShell Integrated Scripting Environment (ISE)](https://technet.microsoft.com/library/hh849182), und die [Out-GridView](https://go.microsoft.com/fwlink/?LinkID=113364) und [Show-Command](https://go.microsoft.com/fwlink/?LinkID=217448)-Cmdlets auf Server Core-Installationen nicht ausführen.

## <a name="additional-references"></a>Weitere Verweise

[about_PowerShell.exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Skripterstellung mit Windows PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) Siehe auch