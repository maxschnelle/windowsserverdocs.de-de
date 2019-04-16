---
title: Passen freigegebener Ordner an
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 47bc4986-14eb-4a29-9930-83a25704a3a0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: bcdd43183512bb225dd4afa916f2782c6eb79d7e
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="customize-shared-folders"></a>Passen freigegebener Ordner an

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Standardmäßig werden Serverordner auf der größten Datenpartition auf Datenträger 0 erstellt. Partner können den Ort anpassen und zusätzliche Serverordner anzugeben, indem Sie die folgenden Schritteaus:  
  
1.  Erstellen Sie mithilfe einer benutzerdefinierten Partitionskonfiguration das werkseitige Image, und klicken Sie dann erstellen Sie einen neuen Registrierungsschlüssel für den Speicher, bevor Sie Sysprep verwenden. Während der ersten Konfiguration (IC) überprüft der speichererstkonfiguration dieser Registrierungsschlüssel. Wenn sie vorhanden ist, werden die standardmäßigen Serverordner im Verzeichnis C:\ServerFolders erstellt.  
  
    #### <a name="to-create-a-new-storage-registry-key"></a>Erstellen Sie einen neuen Speicher-Registrierungsschlüssel  
  
    1.  Auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suche**.  
  
    2.  Geben Sie in das Suchfeld **Regedit**, und klicken Sie dann auf die **Regedit** Anwendung.  
  
    3.  Erweitern Sie im Navigationsbereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, und erweitern Sie dann **Microsoft**.  
  
    4.  Mit der rechten Maustaste **Windows Server**, klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
    5.  Benennen Sie den Schlüssel **Speicher**.  
  
    6.  Klicken Sie im Navigationsbereich mit der Maustaste der neue Speicher-Registrierung, klicken Sie auf **neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)**.  
  
    7.  Namen der Zeichenfolge **CreateFoldersOnSystem**.  
  
    8.  Mit der rechten Maustaste **CreateFoldersOnSystem**, und klicken Sie dann auf **ändern**. Die **Zeichenfolge bearbeiten** Dialogfeld wird angezeigt.  
  
    9. Legen Sie den Wert dieses neuen Schlüssels auf **1**, und klicken Sie dann auf **OK**.  
  
2.  Verwenden Sie das PostIC.cmd-Skript, um die Ordner an einen anderen Speicherort verschieben oder weitere Ordner zu erstellen. Im folgenden Beispiel dargestellt: [Beispiel 1: Erstellen eines benutzerdefinierten Ordners und Verschieben der Standardordner von PostIC.cmd an einen neuen Speicherort mithilfe von Windows PowerShell](Customize-Shared-Folders.md#BKMK_Example1).  
  
3.  Verwenden Sie Windows Server Solutions SDK, um die Ordner an einen anderen Speicherort zu verschieben oder um weitere Ordner zu erstellen. Im folgenden Beispiel dargestellt: [Beispiel 2: Erstellen eines benutzerdefinierten Ordners und Verschieben eines vorhandenen Ordners mithilfe von Windows Server Solutions SDK](Customize-Shared-Folders.md#BKMK_Example2).  
  
 Optional können Partner die Datenordner auf Laufwerk c: lassen Dadurch können die Endbenutzer oder Wiederverkäufer das Layout der Datenordner auf den Datenlaufwerken bestimmen.  
  
###  <a name="BKMK_Example1"></a>Beispiel 1: Erstellen eines benutzerdefinierten Ordners und Verschieben der Standardordner von PostIC.cmd an einen neuen Ort mithilfe von Windows PowerShell  
  
1.  Erstellen Sie eine Datei "PostIC.cmd" zum Ausführen von Aufgaben zur Erstkonfiguration beschriebenen nach der [erstellen die PostIC.cmd-Datei für die Ausführung Posten Aufgaben zur Erstkonfiguration](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) Abschnitt.  
  
2.  Mit dem Editor, erstellen Sie eine Datei namens **customizefolders. ps1** im C:\Windows\Setup\Scripts Ordner, und fügen Sie dann die folgenden Windows PowerShell® Befehle in die Datei (Markierung entsprechende Zeilen abhängig vom gewünschten Verhalten).  
  
    ```  
    # Move the Documents folder to D:\ServerFolders  
    #Get-WssFolder -name Documents| Move-WssFolder - NewDrive D:\ -Force  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    # Move all folders to D:\ServerFolders  
    #foreach( $folder in Get-WssFolder )  
    #{  
    #    Move-WssFolder $folder -NewDrive D:\ -Force  
    #}  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    # Create a custom folder named Custom Folder  
    #Add-WssFolder -Name CustomFolder -Path D:\ServerFolders\CustomFolder -Description "Custom Folder"  
  
    # Check for last error. If last error is not null, exit with return code 1  
    #If ($error[0] -ne $null) { exit 1}   
  
    exit 0  
    ```  
  
3.  Fügen Sie die folgende Zeile in die Datei "PostIC.cmd" zum Ausführen des Skripts.  
  
    ```  
    REM Lower the execution policy  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"  
  
    REM Execute the folder customization script  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"  
    Set error_level=%ERRORLEVEL%  
  
    REM Restore the execution policy to deafult  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"  
    Set ERRORLEVEL=%error_level%  
    ```  
  
###  <a name="BKMK_Example2"></a>Beispiel 2: Erstellen eines benutzerdefinierten Ordners und Verschieben eines vorhandenen Ordners mithilfe von Windows Server Solutions SDK  
 Die, den von Ihnen erstellte Code kann erfüllt als ausführbare Datei, und klicken Sie dann aus der PostIC.cmd-Datei aufgerufen oder direkt aus einem installierten Add-In aufgerufen werden.  
  
```  
static void Main(string[] args)  
{  
 StorageManager storageManager = new StorageManager();  
 //Connect to the StorageManager  
 storageManager.Connect();  
  
 //Move the Documents folder to D:\ServerFolders  
 Folder targetFolder = storageManager.Folders.First(folder => folder.Name == "Documents");  
  
 MoveFolderRequest moveRequest = targetFolder.GetMoveRequest(@"D:\");  
 moveRequest.MoveFolder();  
  
 //Verify operation was successful, if so print result  
 if (moveRequest.Status == OperationStatus.Succeeded)  
 {  
  Console.WriteLine("Folder {0} now located at {1}", targetFolder.Name, targetFolder.Path);  
 }  
  
 string newFolderName = "New Custom Folder";  
 string newFolderLocation = @"C:\ServerFolders\New Custom Folder";  
  
 //Create add request based with specific name and location  
 CreateFolderRequest request = storageManager.GetCreateFolderRequest(newFolderName, newFolderLocation);  
  
 //Give Guest user read only permission to folder  
 request.PermissionsByName.Add(new NamePermission("Guest", Permission.ReadOnly));  
  
 //Create the new folders  
 request.CreateFolder();  
  
 //Verify operation was successful, if so print result  
 if( request.Status == OperationStatus.Succeeded)  
 {  
  Folder newFolder = storageManager.Folders.First(folder => folder.Path == newFolderLocation);  
  
  Console.WriteLine("Folder {0} created at {1}", newFolder.Name, newFolder.Path);  
 }  
}  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)