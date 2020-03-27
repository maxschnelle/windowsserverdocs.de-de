---
title: Vorbereiten des Abbilds für die Bereitstellung
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 681c6cad-7fde-494f-86a5-f4c7c15d23f9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: aac776253c094c4a77269720bcc5762d6c41d720
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80311550"
---
# <a name="preparing-the-image-for-deployment"></a>Vorbereiten des Abbilds für die Bereitstellung

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

"Sysprep.exe" stellt ein typisches Tool zur Vorbereitung eines Abbilds dar. Mit diesem Tool wird das Abbild generalisiert und der Server heruntergefahren, sodass die Erstkonfiguration ausgeführt wird, wenn der Server, auf dem das Abbild enthalten ist, neu gestartet wird. Vor der Ausführung von "Sysprep.exe" müssen alle Änderungen am Abbild abgeschlossen sein.  
  
> [!NOTE]
>  Sie können die Windows-Produktaktivierung höchstens dreimal mit "Sysprep.exe" zurücksetzen.  
  
#### <a name="to-prepare-the-image"></a>So bereiten Sie das Abbild vor  
  
1.  Löschen Sie die von Ihnen hinzugefügte Datei "SkipIC.txt".  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten. Klicken Sie auf **Start**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und wählen Sie dann **Als Administrator ausführen** aus.  
  
3.  Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel zurückzusetzen, sodass dem Benutzer die vollständige Karenzzeit zur Verfügung steht, bevor die Richtlinienkonformität des Servers erlischt.  
  
    ```  
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f  
    ```  
  
4.  Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel der Schlüsselanzeige, Sprachseite, Gebietsschemaseite und der Seite des Endbenutzer-Lizenzvertrags hinzuzufügen. Standardmäßig werden diese Seiten bei der Erstkonfiguration nicht angezeigt. Daher müssen Sie diesen Registrierungsschlüssel hinzufügen, wenn Sie eine vorinstallierte Box freigeben. Wenn Sie jedoch eine DVD freigeben, sollten Sie diesen Schlüssel nicht hinzufügen, da diese Seiten bei der Konfiguration von WinPE und der Erstkonfiguration angezeigt werden.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
5.  Deaktivieren Sie die Schlüsselseite der Erstkonfiguration, wenn die Box bereits einen Schlüssel enthält. Die Schlüsselseite wird nur angezeigt, wenn "ShowPreinstallPages = true" und "KeyPreInstalled != true" festgelegt sind.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f  
    ```  
  
6.  Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel hinzuzufügen, wenn Sie die Überprüfungen der Hardwareanforderungen deaktivieren möchten. Dies gilt nur für die vorinstallierte Box, die die Hardwareanforderungen nicht erfüllt. Wenn Sie eine DVD freigeben, oder Ihre Box die Hardwareanforderungen erfüllt, wird empfohlen, dass Sie diesen Schlüssel nicht hinzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
7.  (Optional) Entfernen Sie die Protokolle unter **%programdata%\Microsoft\Windows Server\Logs**.  
  
8.  Bereiten Sie die XML-Datei für den unbeaufsichtigten Modus für Sysprep vor, wie in der folgenden Vorlage dargestellt.  
  
    ```  
    <unattend xmlns="urn:schemas-microsoft-com:unattend" xmlns:ms="urn:schemas-microsoft-com:asm.v3">  
  
      <settings pass="oobeSystem">  
        <component name="Microsoft-Windows-Shell-Setup" processorArchitecture="amd64" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" xmlns:wcm="https://schemas.microsoft.com/WMIConfig/2002/State" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
  
          <!-- Must have -->  
          <OOBE>  
             <HideEULAPage>true</HideEULAPage>  
          </OOBE>  
          <!-- Must have -->  
          <AutoLogon>   
            <Enabled>true</Enabled>   
            <Username>Administrator</Username>   
            <Domain>.</Domain>   
            <Password>   
              <!--You can set any password you like, but keep it consistent with password settings -->       
              <Value>Admin@123</Value>   
              <PlainText>true</PlainText>   
            </Password>   
          </AutoLogon>   
          <UserAccounts>   
           <AdministratorPassword>   
             <!--You can set any password you like, but keep it consistent with auto logon settings -->       
             <Value>Admin@123</Value>   
             <PlainText>true</PlainText>   
           </AdministratorPassword>   
          </UserAccounts>  
  
          <!-- Optional -->  
          <OEMInformation>  
             <HelpCustomized>true</HelpCustomized>  
             <Manufacturer>OEM name</Manufacturer>  
             <Model>model name</Model>  
             <SupportHours>hours</SupportHours>  
             <SupportPhone>123-456-7890</SupportPhone>  
             <SupportURL>http://www.contoso.com</SupportURL>  
          </OEMInformation>  
  
        </component>  
  
      </settings>  
  
      <settings pass="specialize">  
        <component name="Microsoft-Windows-Shell-Setup" publicKeyToken="31bf3856ad364e35" language="neutral" versionScope="nonSxS" processorArchitecture="amd64">  
          <!-- Must have -->  
          <ComputerName>Server</ComputerName>          
          <!-- Optional -->  
          <ProductKey>XXXXX-XXXXX-XXXXX-XXXXX-XXXXX</ProductKey>  
        </component>  
      </settings>  
    </unattend>  
    ```  
  
9. Führen Sie den folgenden Befehl für Sysprep aus.  
  
    ```  
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit  
    ```  
  
    > [!IMPORTANT]
    >  Anstelle eines Parameters von Sysprep können Sie auch die Datei "unattend.xml" unter "%systemdrive%" hinzufügen. Wenn sich die Datei unter "c:\" befindet Sie wird durch die Benutzereinstellungen abgedeckt, aber wenn Sie als Parameter von syunp verwendet wird, wird Sie nicht durch die Benutzereinstellungen abgedeckt. Die Datei "unattend.xml" unter "%systemdrive%" wird bei jedem Neustart des Servers gelöscht. Stellen Sie daher nach dem Erstellen von "unattend.xml" unter "%systemdrive%" sicher, dass der Server nicht neu gestartet wird.  
  
10. Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel zum Überspringen der Windows OOBE-Schlüsselseite hinzuzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f  
    ```  
  
11. Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel zum Überspringen der Windows-Sprachauswahlseite hinzuzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f  
    ```  
  
    > [!IMPORTANT]
    >  Sie müssen die letzten beiden Schritte ausführen, andernfalls wird die Seite für Windows OOBE angezeigt, die mit der Erstkonfigurationsseite angezeigt wird und die das remote verwaltete Serverszenario abbricht.  
  
12. Fahren Sie die Box nach der Ausführung von Sysprep herunter. Sie können ein Abbild erfassen oder den Server neu starten, um die Erstkonfiguration von einem Clientcomputer aus fortzusetzen.  
  
> [!IMPORTANT]
>  Partner, die Serverwiederherstellungsmedien erstellen möchten, müssen das Abbild aufzeichnen und die Wiederherstellungsmedien erstellen, bevor sie mit dem nächsten Schritt fortfahren.