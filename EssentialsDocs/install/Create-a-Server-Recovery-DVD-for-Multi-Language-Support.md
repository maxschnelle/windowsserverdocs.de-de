---
title: Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: e2bbc7bf7af71c671153bf7ba3356ddc08dcc38b
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433630"
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_MLHeadedRecovery"></a> Erstellen einer Serversetup- und serverwiederherstellungs-DVD für die Unterstützung für mehrere Sprachen auf lokal verwalteten Servern  
  
> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Abbild erstellen, wie beschrieben in der [Exemplarische Vorgehensweise: Mehrsprachiges Windows-Abbilderstellung](https://technet.microsoft.com/library/jj126995) bevor Sie die Windows Server Essentials--Sprachpaket in install.wim hinzufügen.  
  
 Es gibt zwei Konfigurationsphasen: die Konfiguration von Windows Preinstallation Environment (Windows PE) und die Erstkonfiguration. Standardmäßig wird bei der Erstkonfiguration die Sprachauswahlseite nicht angezeigt.  
  
- Bei einem remote verwalteten OEM-Installations- oder einem OEM-Vorinstallationsszenario müssen Sie mithilfe des folgenden Befehls einen Registrierungsschlüssel hinzufügen, um die Sprachauswahlseite bei der Erstkonfiguration anzuzeigen.  
  
  ```  
  %systemroot%\system32\reg.exe add "HKLM\Software\microsoft\windows server\setup" /v ShowPreinstallPages /t REG_SZ /d true /f  
  ```  
  
  > [!IMPORTANT]
  >  Wenn OEMs im Labor ein Abbild erstellen, müssen sie während der Windows PE-Phase des Setups als Sprache **Englisch** auswählen.  
  
- In einem ROK-Szenario (Reseller Option Kit) erhält der Kunde eine DVD und ggf. Hardware. Der Kunde sollte die Sprache bei der Konfiguration von Windows PE auswählen können, und die Sprachauswahlseite wird bei der Erstkonfiguration nicht mehr angezeigt.  
  
  Sie können eine doppelschichtige DVD ausliefern, die mehrere Sprachen enthält.  
  
  In diesem Abschnitt wird beschrieben, wie Sie Windows Setup Sprachunterstützung hinzufügen. Das wichtigste Tool für die Anpassung von Windows PE 3.0 ist die Abbildverwaltung für die Bereitstellung (Deployment Image Servicing and Management, DISM), ein Befehlszeilentool. Diese Lösung ermöglicht die folgenden Szenarien:  
  
1.  Erstellen mehrsprachiger Installationen  
  
2.  Erstellen verteilbarer Medien  
  
### <a name="prerequisites"></a>Vorraussetzungen  
 Sie benötigen Folgendes, um Windows Setup mehrsprachige Unterstützung hinzuzufügen:  
  

-   Einen Referenzcomputer mit allen Tools und Quelldateien, die zum Erstellen eines angepassten WinPE-Abbilds erforderlich sind. Weitere Informationen finden Sie unter [Prepare the Technician Computer](Prepare-the-Technician-Computer.md).  

-   Einen Referenzcomputer mit allen Tools und Quelldateien, die zum Erstellen eines angepassten WinPE-Abbilds erforderlich sind. Weitere Informationen finden Sie unter [Prepare the Technician Computer](../install/Prepare-the-Technician-Computer.md).  

  
-   A  Windows Server Essentials DVD.  
  
-   Ein Windows Server Essentials Sprachpaket-DVD.  
  
###  <a name="BKMK_Steps"></a> Hinzufügen von Unterstützung für mehrere Sprachen  
 Um Windows Setup Unterstützung mehrerer Sprachen hinzufügen, aktualisieren Sie Install.wim durch Hinzufügen von Windows Server 2012 und die Windows Server Essentials-Language packs für sie.  
  
#### <a name="update-installwim"></a>Aktualisieren von "Install.wim"  
 In diesem Schritt fügen Sie Windows Server 2012 und Windows Server Essentials-Sprachpakete in "Install.wim" hinzu.  
  
> [!NOTE]
>  Stellen Sie sicher, dass Sie Language Packs für Windows Server 2012 installieren. Dadurch wird das richtige Branding sichergestellt. Die Windows Server 2012 Multilingual User Interface Language Packs stehen auf ["Microsoft.com"](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx). Befolgen Sie die Anweisungen aus, unter dem [Exemplarische Vorgehensweise: Mehrsprachiges Windows-Abbilderstellung Sprachen](https://technet.microsoft.com/library/jj126995.aspx) auf Mehrsprachiges Windows-Abbild erstellen, bevor Sie das Sprachpaket für Windows Server Essentials in install.wim hinzufügen.  
>   
>  Windows Server Essentials-Sprachpakete sind verfügbar, in der Language Pack-Medium auf \Language Packs\\< CultureName\>.  
  
> [!NOTE]
>  Nicht alle Sprachpakete möglicherweise nicht vor der Veröffentlichung von Windows Server 2012 verfügbar.  
  
###### <a name="to-add-language-packs-to-installwim"></a>So fügen Sie "Install.wim" Sprachpakete hinzu  
  
1.  Gehen Sie wie folgt vor, um "Install.wim" Betriebssystem- und Produktsprachpakete hinzuzufügen (in diesem Beispiel wird Französisch verwendet):  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  Fügen Sie sprachspezifische Dateien unterstützen, erstellen die Client-Sicherung wiederherstellen-USB-Flashlaufwerk, mit dem Verfahren in [erstellen mehrsprachigen Mediums zur Clientwiederherstellung](Build-Multi-Language-Client-Restore-Media.md).  

2.  Fügen Sie sprachspezifische Dateien unterstützen, erstellen die Client-Sicherung wiederherstellen-USB-Flashlaufwerk, mit dem Verfahren in [erstellen mehrsprachigen Mediums zur Clientwiederherstellung](../install/Build-Multi-Language-Client-Restore-Media.md).  

  
3.  Erstellen Sie mit dem Befehl `DISM /Gen-LangINI` die Datei "Lang.ini" auf dem beweglichen Medium neu, sodass sie die zusätzliche Sprachunterstützung widerspiegelt. Beispiel:  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  Speichern Sie die Änderungen mit dem Befehl `DISM /unmount /commit` im Abbild. Beispiel:  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
    ```  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

