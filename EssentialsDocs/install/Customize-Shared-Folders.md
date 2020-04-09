---
title: Anpassen freigegebener Ordner
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: 47bc4986-14eb-4a29-9930-83a25704a3a0
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 861107035408fc39d0dc5e4d94a4d82d8dfba74e
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80818073"
---
# <a name="customize-shared-folders"></a>Anpassen freigegebener Ordner

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Standardmäßig werden Serverordner auf der größten Datenpartition auf Datenträger 0 erstellt. Partner können mit den folgenden Schritten den Ort anpassen und weitere Serverordner erstellen:  
  
1. Erstellen Sie mit einer benutzerdefinierten Partitionskonfiguration das Originalabbild, und erstellen Sie dann einen neuen Registrierungsschlüssel "Storage", bevor Sie sysprep verwenden. Während der Erstkonfiguration wird bei der Speichererstkonfiguration dieser Registrierungsschlüssel überprüft. Ist er vorhanden, werden die standardmäßigen Serverordner im Verzeichnis "C:\ServerFolders" erstellt.  
  
   #### <a name="to-create-a-new-storage-registry-key"></a>So erstellen Sie einen neuen Registrierungsschlüssel "Storage"  
  
   1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
   2.  Geben Sie im Suchfeld **regedit** ein, und klicken Sie dann auf die Anwendung **Regedit**.  
  
   3.  Erweitern Sie im Navigationsbereich **HKEY_LOCAL_MACHINE**, **SOFTWARE** und dann **Microsoft**.  
  
   4.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, klicken Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
   5.  Nennen Sie den Schlüssel **Storage**.  
  
   6.  Klicken Sie im Navigationsbereich mit der rechten Maustaste auf den neuen Registrierungsschlüssel "Storage", klicken Sie auf **Neu**, und klicken Sie dann auf **DWORD-Wert (32-Bit)** .  
  
   7.  Geben Sie als Namen der Zeichenfolge **CreateFoldersOnSystem** ein.  
  
   8.  Klicken Sie mit der rechten Maustaste auf **CreateFoldersOnSystem**, und klicken Sie dann auf **Ändern**. Das Dialogfeld **Zeichenfolge bearbeiten** wird angezeigt.  
  
   9. Legen Sie den Wert dieses neuen Schlüssels auf **1** fest, und klicken Sie dann auf **OK**.  
  
2. Verwenden Sie das Skript "PostIC.cmd", um die Ordner an einen anderen Ort zu verschieben oder um weitere Ordner zu erstellen. Siehe das folgende Beispiel: [Beispiel 1: Erstellen eines benutzerdefinierten Ordners und Verschieben der Standardordner von "PostIC.cmd" an einen neuen Ort mithilfe von Windows PowerShell](Customize-Shared-Folders.md#BKMK_Example1).  
  
3. Verwenden Sie das SDK für Windows Server-Lösungen, um die Ordner an einen anderen Ort zu verschieben oder um weitere Ordner zu erstellen. Siehe das folgende Beispiel: [Beispiel 2: Erstellen eines benutzerdefinierten Ordners und Verschieben eines vorhandenen Ordners mit dem SDK für Windows Server-Lösungen](Customize-Shared-Folders.md#BKMK_Example2).  
  
   Optional können Partner die Datenordner auf dem Laufwerk "C" belassen. So kann der Endbenutzer oder der Handelspartner das Layout der Datenordner auf den Datenlaufwerken bestimmen.  
  
###  <a name="example-1-create-a-custom-folder-and-move-the-default-folders-to-a-new-location-from-posticcmd-by-using-windows-powershell"></a><a name="BKMK_Example1"></a>Beispiel 1: Erstellen eines benutzerdefinierten Ordners und Verschieben der Standardordner von "postic. cmd" an einen neuen Speicherort mithilfe von Windows PowerShell  
  
1.  Erstellen Sie die Datei "PostIC.cmd" zum Ausführen von Aufgaben nach der Erstkonfiguration, wie im Abschnitt [Erstellen der Datei "PostIC.cmd" zum Ausführen von Aufgaben nach der Erstkonfiguration](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) erläutert.  
  
2.  Erstellen Sie im Ordner "c:\windows\setup\scripts" im Ordner "c:\windows\setup\scripts" eine Datei mit dem Namen " **customizefolders. ps1** ", und fügen Sie die folgenden Windows PowerShell-&reg; Befehle in die Datei ein.  
  
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
  
3.  Fügen Sie der Datei "PostIC.cmd" die folgende Zeile hinzu, um dieses Skript auszuführen.  
  
    ```  
    REM Lower the execution policy  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy RemoteSigned"  
  
    REM Execute the folder customization script  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" -NoProfile -Noninteractive -command ". %windir%\setup\scripts\customizefolders.ps1;exit $LASTEXITCODE"  
    Set error_level=%ERRORLEVEL%  
  
    REM Restore the execution policy to default  
    "%programfiles%\Windows Server\bin\WssPowershell.exe" "Set-ExecutionPolicy Restricted"  
    Set ERRORLEVEL=%error_level%  
    ```  
  
###  <a name="example-2-create-a-custom-folder-and-move-an-existing-folder-by-using-the-windows-server-solutions-sdk"></a><a name="BKMK_Example2"></a>Beispiel 2: Erstellen eines benutzerdefinierten Ordners und Verschieben eines vorhandenen Ordners mit dem SDK für Windows Server-Lösungen  
 Der von Ihnen erstellte Code kann als ausführbare Datei kompiliert werden und dann von der Datei "PostIC.cmd" oder direkt von einem installierten Add-In aufgerufen werden.  
  
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
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)
