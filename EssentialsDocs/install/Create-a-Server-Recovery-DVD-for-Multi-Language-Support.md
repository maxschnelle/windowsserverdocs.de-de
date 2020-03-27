---
title: Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: c7da0f6c-9732-4784-9c28-7dad72c4071d
author: daveba
ms.author: daveba
ms.openlocfilehash: b71fc748f7cc8d82420b7a62fe502135036db727
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312117"
---
# <a name="create-a-server-recovery-dvd-for-multi-language-support"></a>Erstellen einer Serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="create-a-server-setup-and-server-recovery-dvd-for-multiple-language-support-on-locally-administered-servers"></a><a name="BKMK_MLHeadedRecovery"></a>Erstellen einer Server Setup-und serverwiederherstellungs-DVD für die Unterstützung mehrerer Sprachen auf lokal verwalteten Servern  
  
> [!NOTE]
>  Sie müssen zuerst ein mehrsprachiges Windows-Abbild erstellen, wie unter Exemplarische Vorgehensweise: Erstellen von [Windows-Images](https://technet.microsoft.com/library/jj126995) in mehreren Sprachen beschrieben, bevor Sie "install. wim" das Windows Server Essentials sprach Pack hinzufügen  
  
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
  
### <a name="prerequisites"></a>Erforderliche Komponenten  
 Sie benötigen Folgendes, um Windows Setup mehrsprachige Unterstützung hinzuzufügen:  
  

-   Einen Referenzcomputer mit allen Tools und Quelldateien, die zum Erstellen eines angepassten WinPE-Abbilds erforderlich sind. Weitere Informationen finden Sie unter [Vorbereiten des Referenzcomputers](Prepare-the-Technician-Computer.md).  

-   Einen Referenzcomputer mit allen Tools und Quelldateien, die zum Erstellen eines angepassten WinPE-Abbilds erforderlich sind. Weitere Informationen finden Sie unter [Vorbereiten des Referenzcomputers](../install/Prepare-the-Technician-Computer.md).  

  
-   Eine Windows Server Essentials-DVD.  
  
-   Eine Windows Server Essentials-Sprachpaket-DVD.  
  
###  <a name="adding-multiple-language-support"></a><a name="BKMK_Steps"></a>Hinzufügen mehrerer Sprachunterstützung  
 Wenn Sie Windows Setup Unterstützung für mehrere Sprachen hinzufügen möchten, aktualisieren Sie die Datei "install. wim", indem Sie die Windows Server 2012-und Windows Server Essentials-Sprachpakete hinzufügen.  
  
#### <a name="update-installwim"></a>Aktualisieren von "Install.wim"  
 In diesem Schritt fügen Sie "install. wim" Windows Server 2012-und Windows Server Essentials Language Packs hinzu.  
  
> [!NOTE]
>  Vergewissern Sie sich, dass Sie Sprachpakete für Windows Server 2012 installieren. Dadurch wird das richtige Branding sichergestellt. Die Sprachpakete für die mehrsprachige Benutzeroberfläche von Windows Server 2012 sind auf [Microsoft.com](https://www.microsoft.com/OEM/en/installation/downloads/Pages/technical-downloads.aspx)verfügbar. Befolgen Sie die Anweisungen unter Exemplarische Vorgehensweise [: Erstellen von Windows-Images](https://technet.microsoft.com/library/jj126995.aspx) in mehreren Sprachen zum Erstellen eines mehrsprachigen Windows-Abbilds, bevor Sie "install. wim" das Windows Server Essentials-Sprachpaket hinzufügen.  
>   
>  Windows Server Essentials Language Packs sind auf dem Sprachpaket Medium unter \language Packs\\< cultureName\>verfügbar.  
  
> [!NOTE]
>  Vor der Veröffentlichung von Windows Server 2012 sind nicht alle Sprachpakete möglicherweise nicht verfügbar.  
  
###### <a name="to-add-language-packs-to-installwim"></a>So fügen Sie "Install.wim" Sprachpakete hinzu  
  
1.  Gehen Sie wie folgt vor, um "Install.wim" Betriebssystem- und Produktsprachpakete hinzuzufügen (in diesem Beispiel wird Französisch verwendet):  
  
    ```  
    Dism /Mount-Wim /WimFile:C:\my_distribution\sources\install.wim /index:1 /MountDir:C:\InstallMount  
    Mkdir c:\temp_Scratch  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<path_to_OS_language_packs>\fr-fr\lp.cab  
    Dism /Image:C:\InstallMount /ScratchDir:C:\temp_Scratch /Add-Package /PackagePath:<OCD\Language Packs\FR-FR\lp.cab  
  
    ```  
  

2.  Fügen Sie sprachspezifische Dateien hinzu, um die Erstellung des USB-Speich erschlaufwerks für die Client Sicherungs Wiederherstellung zu unterstützen. verwenden Sie hierzu das unter [Erstellen von Multilanguage](Build-Multi-Language-Client-Restore-Media.md)  

2.  Fügen Sie sprachspezifische Dateien hinzu, um die Erstellung des USB-Speich erschlaufwerks für die Client Sicherungs Wiederherstellung zu unterstützen. verwenden Sie hierzu das unter [Erstellen von Multilanguage](../install/Build-Multi-Language-Client-Restore-Media.md)  

  
3.  Erstellen Sie mit dem Befehl `DISM /Gen-LangINI` die Datei "Lang.ini" auf dem beweglichen Medium neu, sodass sie die zusätzliche Sprachunterstützung widerspiegelt. Beispiel:  
  
    ```  
    Dism /image:C:\InstallMount /Gen-LangINI /distribution:C:\my_distribution  
  
    ```  
  
4.  Speichern Sie die Änderungen mit dem Befehl `DISM /unmount /commit` im Abbild. Beispiel:  
  
    ```  
    Dism /Unmount-Wim /MountDir:C:\InstallMount /Commit  
    ```  
  
## <a name="see-also"></a>Weitere Informationen  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

