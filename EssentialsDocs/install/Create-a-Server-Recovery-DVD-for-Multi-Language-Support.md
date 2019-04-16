---
title: "Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c7da0f6c-9732-4784-9c28-7dad72c4071d
4author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ac547f97b48e4cd0ebf87e0935cadc2c539b4d0b
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_MLHeadedRecovery"></a>Erstellen einer Serversetup- und serverwiederherstellungs-DVD für die Unterstützung für mehrere Sprachen auf lokal verwalteten Servern  
  
> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Image erstellen, wie beschrieben in die [Exemplarische Vorgehensweise: mehrsprachige Windows-Imageerstellung](https://technet.microsoft.com/library/jj126995) , bevor Sie die Windows Server Essentials--Sprachpaket in install.wim hinzufügen.  
  
 Es gibt zwei Konfigurationsphasen: die Windows Preinstallation Environment (Windows PE) und die Erstkonfiguration. Standardmäßig wird die Sprachauswahlseite bei der Erstkonfiguration nicht angezeigt werden.  
  
-   Für einen Remote verwalteten OEM-Installation oder einer OEM-vorinstallationsszenario müssen Sie eine Registrierung mithilfe des folgenden Befehls die Sprachauswahlseite bei der Erstkonfiguration anzeigen hinzufügen.  
  
    ```  
    %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
    ```  
  
    > [!IMPORTANT]
    >  Wenn OEMs im Labor ein Abbild erstellen, wählen sie **Englisch** während der Windows PE-Phase des Setups als Sprache.  
  
-   In einem Szenario (Reseller Option Kit, ROK) erhält der Kunde eine DVD und ggf. Hardware. Der Kunde sollte während der Installation von Windows PE die Sprache aus, und die Sprachauswahlseite wird während der Erstkonfiguration nicht mehr angezeigt.  
  
 Sie können eine einzelne Dual-Layer-DVD ausliefern, die mehrere Sprachen enthält.  
  
 In diesem Abschnittwird beschrieben, wie Sie Windows Setup sprachunterstützung hinzufügen. Das wichtigste Tool für die Anpassung von Windows PE 3.0 ist Deployment Image Servicing and Management (DISM), ein Befehlszeilentool. Diese Lösung ermöglicht die folgenden Szenarien:  
  
1.  Erstellen mehrsprachiger Installationen  
  
2.  Erstellen verteilbarer Medien  
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
 Zum Hinzufügen der Unterstützung mehrerer Sprachen zu Windows Setup benötigen Sie Folgendes:  
  

-   Einen Referenzcomputer, der alle Tools und Quelldateien, die zum Erstellen eines benutzerdefinierten Windows PE-Abbilds bereitstellt. Weitere Informationen finden Sie unter [Vorbereiten des Referenzcomputers ](Prepare-the-Technician-Computer.md).  

-   Einen Referenzcomputer, der alle Tools und Quelldateien, die zum Erstellen eines benutzerdefinierten Windows PE-Abbilds bereitstellt. Weitere Informationen finden Sie unter [Vorbereiten des Referenzcomputers ](../install/Prepare-the-Technician-Computer.md).  

  
-   Eine Windows Server Essentials-DVD.  
  
-   Ein Windows Server Essentials Sprachpaket-DVD.  
  
###  <a name="BKMK_Steps"></a>Hinzufügen der Unterstützung mehrerer Sprachen  
 Zum Hinzufügen der Unterstützung mehrerer Sprachen zu Windows Setup, aktualisieren Sie Install.wim durch Hinzufügen von Windows Server2012, und die Windows Server Essentials Sprachpakete.  
  
#### <a name="update-installwim"></a>Aktualisieren Sie Install.wim  
 In diesem Schrittfügen Sie Windows Server2012 und Windows Server Essentials-Sprachpakete in Install.wim hinzu.  
  
> [!NOTE]
>  Stellen Sie sicher, dass Sie Sprachpakete für Windows Server2012 installieren. Dadurch wird sichergestellt, dass Sie das richtige Branding sichergestellt. Die Windows Server2012 Multilingual User Interface Language Packs stehen auf [Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx). Befolgen Sie die Anweisungen, wie beschrieben in die [exemplarische Vorgehensweise: mehrsprachige Windows-Imageerstellung zum Erstellen von mehreren Sprachen](https://technet.microsoft.com/library/jj126995.aspx) auf ein mehrsprachiges Windows-Image erstellen, bevor Sie das Windows Server Essentials-Sprachpaket in hinzufügen Install.wim.  
>   
>  Windows Server Essentials-Sprachpakete sind in der Language Pack-Medium am \Language Packs\\ < CultureName\ > verfügbar.  
  
> [!NOTE]
>  Nicht alle Sprachpakete unter Umständen nicht vor der Veröffentlichung von Windows Server2012 verfügbar.  
  
###### <a name="to-add-language-packs-to-installwim"></a>Install.wim Sprachpakete hinzu  
  
1.  Hinzufügen von Betriebssystem und produktsprachpakete in Install.wim wie folgt (in diesem Beispiel wird Französisch verwendet):  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  Fügen Sie sprachspezifische Dateien unterstützt, erstellen die Client-Sicherung wiederherstellen USB-Speicherstick, mithilfe des Verfahrens [erstellen mehrsprachigen Mediums zur Clientwiederherstellung ](Build-Multi-Language-Client-Restore-Media.md).  

2.  Fügen Sie sprachspezifische Dateien unterstützt, erstellen die Client-Sicherung wiederherstellen USB-Speicherstick, mithilfe des Verfahrens [erstellen mehrsprachigen Mediums zur Clientwiederherstellung ](../install/Build-Multi-Language-Client-Restore-Media.md).  

  
3.  Erstellen Sie die Datei Lang.ini im beweglichen Medium, die zusätzliche sprachunterstützung widerspiegelt neu der `DISM /Gen-LangINI`Befehl, beispielsweise:  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  Speichern Sie die Änderungen im Abbild mithilfe der `DISM /unmount /commit`Befehl, beispielsweise:  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
    ```  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

