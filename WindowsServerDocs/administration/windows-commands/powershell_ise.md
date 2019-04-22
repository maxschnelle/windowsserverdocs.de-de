---
title: PowerShell_ise
description: 'Windows-Befehle Thema ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 32c41b5b-a210-47d9-bd8c-91eb9830b4f0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 03c765b276a2e61247661e132dd49434b444530c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817281"
---
# <a name="powershellise"></a>PowerShell_ise



Windows PowerShell Integrated Scripting Environment (ISE) ist ein grafischer Host-Anwendung, die ermöglicht es Ihnen, lesen, schreiben, ausführen, Debuggen und Testen von Skripts und Module in einer Grafik-assisted-Umgebung. Wichtige Funktionen wie IntelliSense, Show-Command, Codeausschnitte, Tab-Vervollständigung, farbliche syntaxkennzeichnung, visuelle Debuggen und kontextbezogene Hilfe, die eine komfortable Skripterstellung.

Die **PowerShell_ISE.exe** Tool startet eine Windows PowerShell ISE-Sitzung. Bei Verwendung von **PowerShell_ISE.exe**, können Sie zum Öffnen von Dateien in der Windows PowerShell ISE oder eine Windows PowerShell ISE-Sitzung ohne Profil oder mit einem Multithread-Apartment Starten ihrer optionalen Parameter verwenden.

**PowerShell_ISE.exe** in Windows PowerShell 2.0 eingeführt wurde, und in Windows PowerShell 3.0 bedeutend erweitert.

## <a name="using-powershelliseexe"></a>Verwenden von PowerShell_ISE.exe

Sie können **PowerShell_ISE.exe** zum Starten und beenden eine Windows PowerShell-Sitzung wie folgt:
-   Geben Sie Folgendes ein, um eine Windows PowerShell ISE-Sitzung, in ein Eingabeaufforderungsfenster geöffnet, in Windows PowerShell oder im Menü Start zu starten:  
    ```
    PowerShell_Ise
    ```  
-   Verwenden zum Öffnen eines Skripts (ps1) das Skriptmodul (psm1), das modulmanifest (psd1), XML-Datei oder eine beliebige andere unterstützte Datei in Windows PowerShell ISE das folgende Befehlsformat:  
    ```
    PowerShell_Ise <FilePath>
    ```  
    In Windows PowerShell 3.0 können Sie mithilfe des optionalen **Datei** Parameter wie folgt:  
    ```
    PowerShell_Ise -File <FilePath>
    ```  
-   Verwenden Sie zum Starten einer Windows PowerShell ISE-Sitzungs, ohne Ihre Windows PowerShell-Profile die **NoProfile** Parameter. (Die **NoProfile** Parameter wird in Windows PowerShell 3.0 eingeführt.)  
    ```
    PowerShell_Ise -NoProfile
    ```  
-   Anzeigen der **PowerShell_ISE.exe** helfen bei der Datei in ein Eingabeaufforderungsfenster, verwenden Sie das folgende Befehlsformat:  
    ```
    PowerShell_Ise -help, -?, /?
    ```  
Eine vollständige Liste der **PowerShell_ISE.exe** Befehlszeilenparameter, finden Sie unter [about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512).

## <a name="start-windows-powershell-ise-in-other-ways"></a>Starten Sie Windows PowerShell ISE auf andere Weise

Weitere Informationen über andere Möglichkeiten zum Starten von Windows PowerShell ISE finden Sie unter [Starten von Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=135259).

## <a name="remarks"></a>Hinweise

Windows PowerShell wird auf die Server Core-Installationsoption von Windows Server-Betriebssysteme ausgeführt werden. Aber da Windows PowerShell ISE eine grafische Benutzeroberfläche erfordert, wird es nicht auf Server Core-Installationen ausgeführt.

## <a name="additional-references"></a>Weitere Verweise

[about_PowerShell_Ise.exe](https://go.microsoft.com/fwlink/?LinkId=256512)
[about_PowerShell.exe](https://go.microsoft.com/fwlink/?LinkID=113439)
[Windows PowerShell](https://go.microsoft.com/fwlink/?LinkID=107116)
[Skripterstellung mit Windows PowerShell](https://technet.microsoft.com/scriptcenter/dd742419) Siehe auch