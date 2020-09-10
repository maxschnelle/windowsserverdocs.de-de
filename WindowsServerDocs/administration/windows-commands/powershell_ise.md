---
title: PowerShell_ise
description: Referenz Artikel für den PowerShell_ise-Befehl, mit dem eine Windows PowerShell Integrated Scripting Environment (ISE)-Sitzung gestartet wird.
ms.topic: reference
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
ms.author: lizross
author: eross-msft
manager: mtillman
ms.date: 10/16/2017
ms.openlocfilehash: 44fb06ae7a072730f2c364ce3287996ad1af90e8
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89627251"
---
# <a name="powershell_ise"></a>PowerShell_ise

Windows PowerShell Integrated Scripting Environment (ISE) ist eine grafische Host Anwendung, die es Ihnen ermöglicht, Skripts und Module in einer Grafik gestützten Umgebung zu lesen, zu schreiben, auszuführen, zu Debuggen und zu testen. Wichtige Funktionen wie IntelliSense, Show-Command, Ausschnitte, Vervollständigung mit der Tab-Taste, Syntax Farben, visuelles Debuggen und kontextbezogene Hilfe ermöglichen eine umfangreiche Skripterstellung.

## <a name="using-powershellexe"></a>Verwenden von PowerShell.exe

Das **PowerShell_ISE.exe** Tool startet eine Windows PowerShell ISE Sitzung. Wenn Sie **PowerShell_ISE.exe**verwenden, können Sie die optionalen Parameter verwenden, um Dateien in Windows PowerShell ISE zu öffnen oder um eine Windows PowerShell ISE Sitzung ohne Profil oder mit einem Multithread-Apartment zu starten.

- Um eine Windows PowerShell ISE Sitzung in einem Eingabe Aufforderungs Fenster, in Windows PowerShell oder im **Startmenü** zu starten, geben Sie Folgendes ein:

  ```powershell
  PowerShell_Ise.exe
  ```

- Zum Öffnen eines Skripts (. ps1), eines Skript Moduls (. psm1), eines Modul Manifests (. psd1), einer XML-Datei oder einer anderen unterstützten Datei in Windows PowerShell ISE geben Sie Folgendes ein:

  ```powershell
  PowerShell_Ise.exe <filepath>
  ```

  In Windows PowerShell 3,0 können Sie den optionalen **File** -Parameter wie folgt verwenden:

  ```powershell
  PowerShell_Ise.exe -file <filepath>
  ```

- Verwenden Sie den **NoProfile** -Parameter, um eine Windows PowerShell ISE Sitzung ohne Ihre Windows PowerShell-Profile zu starten. (Der **NoProfile** -Parameter wurde in Windows PowerShell 3,0 eingeführt.) geben Sie Folgendes ein:

  ```powershell
  PowerShell_Ise.exe -NoProfile
  ```

- Wenn Sie die PowerShell_ISE.exe Hilfedatei anzeigen möchten, geben Sie Folgendes ein:

    ```powershell
    PowerShell_Ise.exe -help
    PowerShell_Ise.exe -?
    PowerShell_Ise.exe /?
    ```

### <a name="remarks"></a>Hinweise

- Eine umfassende Liste der **PowerShell_ISE.exe** Befehlszeilenparameter finden Sie unter [about_PowerShell_Ise.Exe](/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe).

- Informationen zu anderen Möglichkeiten zum Starten von Windows PowerShell finden Sie unter [Starten von Windows PowerShell](/powershell/scripting/windows-powershell/starting-windows-powershell).

- Windows PowerShell wird auf der Server Core-Installationsoption von Windows Server-Betriebssystemen ausgeführt. Da Windows PowerShell ISE jedoch eine grafische Benutzeroberfläche erfordert, kann es nicht auf Server Core-Installationen ausgeführt werden.

## <a name="additional-references"></a>Weitere Verweise

- [about_PowerShell_Ise.exe](/powershell/module/microsoft.powershell.core/about/about_powershell_exe)
