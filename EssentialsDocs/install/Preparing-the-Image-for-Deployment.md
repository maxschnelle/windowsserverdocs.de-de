---
title: "Vorbereiten des Abbilds für die Bereitstellung"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 681c6cad-7fde-494f-86a5-f4c7c15d23f9
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 16411ab073e9417c52592aa9a6b13707dd461537
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="preparing-the-image-for-deployment"></a>Vorbereiten des Abbilds für die Bereitstellung

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Ein typisches Tool zur Vorbereitung eines Abbilds ist sysprep.exe. Mit diesem Tool generalisiert das Image und der Server heruntergefahren werden, damit die Erstkonfiguration ausgeführt wird, wenn der Server mit dem Bild neu gestartet wird. Alle Änderungen auf das Image müssen abgeschlossen sein, bevor Sie sysprep.exe ausführen.  
  
> [!NOTE]
>  Sie können die Windows-produktaktivierung höchstens dreimal mit sysprep.exe zurücksetzen.  
  
#### <a name="to-prepare-the-image"></a>Um das Image vorzubereiten  
  
1.  Löschen Sie SkipIC.txt, die Sie hinzugefügt haben?  
  
2.  Öffnen Sie ein Eingabeaufforderungsfenster mit erhöhten Rechten. Klicken Sie auf **starten**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und wählen Sie dann **als Administrator ausführen**.  
  
3.  Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel zurückzusetzen, sodass der Benutzer die vollständige Karenzzeit hat, bevor der Server nicht kompatibel ist.  
  
    ```  
    %systemroot%\system32\reg.exe add HKLM\Software\Microsoft\ServerInfrastructureLicensing /v Rearm /t REG_DWORD /d 1 /f  
    ```  
  
4.  Führen Sie den folgenden Befehl zum Hinzufügen des Registrierungsschlüssels zum Schlüssel, Sprache, Gebietsschema Seite und Endbenutzer-Lizenzvertrag Seite anzeigen. Standardmäßig werden diese Seiten während der Erstkonfiguration nicht angezeigt. Wenn Sie eine vorinstallierte Box freigeben, müssen Sie daher diesen Registrierungsschlüssel hinzuzufügen. Aber wenn Sie eine DVD freigeben, sollten Sie nicht diesen Schlüssel hinzufügen wie diese Seiten bei der Windows PE und Erstkonfiguration angezeigt werden.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
5.  Deaktivieren Sie die schlüsselseite der Erstkonfiguration, wenn die Box bereits mit Schlüssel ist. Die schlüsselseite wird nur angezeigt, wenn ShowPreinstallPages = True und KeyPreInstalled! = True.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v KeyPreInstalled /t REG_SZ /d true /f  
    ```  
  
6.  Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel hinzuzufügen, wenn Sie die Überprüfungen der Hardwareanforderungen deaktivieren möchten. Dies ist nur für die vorinstallierte Box, die die Hardwareanforderungen nicht erfüllt. Wenn Sie eine DVD freigeben, oder Ihre Box die Hardwareanforderungen erfüllt, wird empfohlen, diesen Schlüssel nicht hinzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v HWRequirementChecks /t REG_DWORD /d 0 /f  
    ```  
  
7.  (Optional) Entfernen Sie die Protokolle unter **%programdata%\Microsoft\Windows Server\Logs**.  
  
8.  Vorbereiten der unbeaufsichtigten XML-Datei für Sysprep wie in der folgenden Vorlage dargestellt.  
  
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
  
9. Führen Sie den folgenden Befehl für Sysprep.  
  
    ```  
    %systemroot%\system32\sysprep\sysprep.exe /generalize /OOBE /unattend:xxx.xml /Quit  
    ```  
  
    > [!IMPORTANT]
    >  Sie können auch die "unattend.xml" unter "% SystemDrive%" anstelle von als Parameter von Sysprep hinzufügen. Befindet sich die Datei unter c:\, es wird, fallen s-Einstellungen des Benutzers, aber wenn als Parameter von Sysprep verwendet wird, nicht behandelt wird durch Benutzer s Einstellungen. Die "unattend.xml" unter "% SystemDrive%" wird jedes Mal gelöscht, der Server neu gestartet wird. Stellen Sie daher sicher, dass nach der Erstellung unattend.xml unter "% SystemDrive%" der Server nicht neu gestartet wird.  
  
10. Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel zum Überspringen der Windows OOBE-schlüsselseite hinzuzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedProductKey /t REG_DWORD /d 1 /f  
    ```  
  
11. Führen Sie den folgenden Befehl aus, um den Registrierungsschlüssel zum Überspringen der Windows-Sprachauswahlseite hinzuzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\Windows\CurrentVersion\Setup\OOBE" /v SetupDisplayedLanguageSelection /t REG_DWORD /d 1 /f  
    ```  
  
    > [!IMPORTANT]
    >  Sie müssen die letzten 2 Schritteausführen, da andernfalls die Windows-Willkommensseite wird angezeigt mit der Erstkonfiguration und Remote verwalteten Server-Szenario ist.  
  
12. Fahren das Feld, nach Sysprep, können Sie Aufzeichnen eines Images oder starten Sie den Server aus, um die Erstkonfiguration von einem Clientcomputer aus fortzusetzen.  
  
> [!IMPORTANT]
>  Partner, die zum Erstellen von Wiederherstellungsmedien Server müssen das Image aufzeichnen und das Wiederherstellungsmedium vor dem Fortfahren mit dem nächsten Schritterstellen.