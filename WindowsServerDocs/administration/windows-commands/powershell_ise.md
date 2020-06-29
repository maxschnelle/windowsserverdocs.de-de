---
title: PowerShell_ise
description: Referenz Thema für den PowerShell_ise-Befehl, mit dem eine Windows PowerShell Integrated Scripting Environment (ISE)-Sitzung gestartet wird.
ms.prod: windows-server
ms.technology: manage-windows-commands
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4c1b525c0178b08e34851b800be8ce4791f38913
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85472335"
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

- Eine umfassende Liste der **PowerShell_ISE.exe** Befehlszeilenparameter finden Sie unter [about_PowerShell_Ise.Exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe).

- Informationen zu anderen Möglichkeiten zum Starten von Windows PowerShell finden Sie unter [Starten von Windows PowerShell](https://docs.microsoft.com/powershell/scripting/windows-powershell/starting-windows-powershell).

- Windows PowerShell wird auf der Server Core-Installationsoption von Windows Server-Betriebssystemen ausgeführt. Da Windows PowerShell ISE jedoch eine grafische Benutzeroberfläche erfordert, kann es nicht auf Server Core-Installationen ausgeführt werden.

## <a name="additional-references"></a>Zusätzliche Referenzen

- [about_PowerShell_Ise.exe] (https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_ise_exe

- [about_PowerShell.Exe](https://docs.microsoft.com/powershell/module/microsoft.powershell.core/about/about_powershell_exe)

- [Windows PowerShell](https://docs.microsoft.com/powershell/)
