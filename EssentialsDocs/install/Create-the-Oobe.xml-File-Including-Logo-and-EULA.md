---
title: Erstellen der Datei "Oobe.xml" mit Logo und EULA
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a7b3cc1-21bb-4344-8110-f5d5959b370d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: f8f99a2051e114b3c890f1cdac23aebf58689980
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884651"
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>Erstellen der Datei "Oobe.xml" mit Logo und EULA

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Mithilfe der Datei "Oobe.xml" können Sie der Erstkonfiguration Ihre eigenen Endbenutzer-Lizenzbestimmungen (End User License Agreement, EULA) hinzufügen. Die Datei "Oobe.xml" wird verwendet, um Text und Bilder für die Erstkonfiguration, die Windows-Willkommensseite und andere dem Endbenutzer angezeigten Seiten bereitzustellen. Sie können mehrere Dateien vom Typ "Oobe.xml" hinzufügen, um den Inhalt basierend auf der Auswahl der Sprache und des Landes bzw. der Region des Endbenutzers anzupassen. Weitere Informationen finden Sie in der Dokumentation zum [Windows Assessment and Deployment Kit für Windows 8](https://go.microsoft.com/fwlink/?LinkId=248694) .  
  
 Die Endbenutzer-Lizenzbestimmungen für Ihr Unternehmen werden zusätzlich zu den Endbenutzer-Lizenzbestimmungen von Microsoft angezeigt. Die Endbenutzer-Lizenzbestimmungen von Microsoft werden dem Endbenutzer während der Erstkonfiguration zuerst angezeigt, danach folgen Ihre Endbenutzer-Lizenzbestimmungen. Ihre Endbenutzer-Lizenzbestimmungen können an einem beliebigen Ort auf dem Server platziert werden. Sie geben lediglich den Ort in der Datei "Oobe.xml" an.  
  
#### <a name="to-add-your-company-eula-and-logo"></a>So fügen Sie die Endbenutzer-Lizenzbestimmungen und das Logo Ihres Unternehmens hinzu  
  
1.  Öffnen Sie die Datei "Oobe.xml" in einem Text-Editor, z. B. in Editor.  
  
2.  In den < Logopath\>< / Logopath\> Tags, geben Sie den absoluten Pfad zur Logodatei. Die Datei sollte eine 32-Bit-PNG-Datei (Portable Network Graphics) mit 240 x 100 Pixeln enthalten.  
  
3.  In den < Eulafilename\>< / Eulafilename\> Tags, geben Sie den absoluten Pfad zur EULA-Datei. Bei der EULA-Datei muss es sich um eine RTF-Datei handeln.  
  
4.  In den < Name\>< / name\> Tags, geben Sie den Namen Ihres Unternehmens.  
  
     Im folgenden Beispiel werden die Tags in einer Datei vom Typ "Oobe.xml" veranschaulicht:  
  
    ```  
  
    <FirstExperience>  
       <oobe>  
          <oem>  
             <name>Fabrikam</name>  
             <logopath>c:\fabrikam\fabrikam.png</logopath>  
             <eulafilename>c:\fabrikam\fabrikam_eula.rtf</eulafilename>  
          </oem>  
       </oobe>  
    </FirstExperience>  
  
    ```  
  
5.  Speichern Sie die Datei.  
  
6.  Legen Sie die Datei "Oobe.xml" unter einem der folgenden Pfade ab:  
  
    |Pfad zur Datei "Oobe.xml"|Bedingung zum Festlegen des Pfads|  
    |-----------------------|----------------------------------------|  
    |%WINDIR%\System32\Oobe\Info\|der Server in einem Land/einer Region und einem ausgeliefert wird.|  
    |%windir%\system32\oobe\info\default\\< Sprache\>|Der Server wurde für den Vertrieb in einem Land/einer Region und mehreren Sprachsystemen konzipiert.|  
    |%WINDIR%\System32\Oobe\Info\\< Land/Region > \ und %windir%\system32\oobe\info\\< Land/Region >\\< Sprache\>\|Server ausgeliefert wird, um mehr als einem Land / müssen Anpassungen auf einer pro Land/Region jeweils in einer einzigen Sprache, Region und die Einstellungen. < Land/Region > ist die Dezimalversion der geografische Standort-Bezeichner (GeoID) des Landes oder der Region, in dem der Server bereitgestellt wird, und < Sprache\> ist die Dezimalversion der Gebietsschema-ID (LCID).|  
  
 Wenn Sie über ein anderes Unternehmenslogo mit weißem Text verfügen, wirkt dieses aufgrund des dunklen Hintergrunds im Setupablauf möglicherweise besser.  Sie können dieses Logo optional angeben, indem Sie einen Registrierungsschlüssel mit zugehörigem Wert angeben.  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>So geben Sie ein Unternehmenslogo durch Festlegen des Registrierungsschlüssels "OEM" an  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **regedit** ein, und klicken Sie dann auf die Anwendung "Regedit".  
  
3.  Navigieren Sie im Navigationsbereich zu  **HKEY_LOCAL_MACHINE**, und erweitern Sie nacheinander **SOFTWARE**, **Microsoft**und **Windows Server**. Wenn der Schlüssel "OEM" nicht vorhanden ist, gehen Sie wie folgt vor, um ihn zu erstellen:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, klicken Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Geben Sie als Schlüsselnamen **OEM**ein.  
  
4.  (Optional) Wenn Sie einen Eintrag für ein Logo erstellen, können Sie verschiedene Schlüssel erstellen, um zwischen den Sprachversionen des Logos zu unterscheiden. Wenn Sie z. B. Logoversionen in Englisch und Deutsch haben, können Sie einen Schlüssel "en-us" und einen Schlüssel "de-de" erstellen. Da alle Logodateien im gleichen Ordner gespeichert sind, müssen Sie Instanzen der Datei mit dem Logobild mit einem eindeutigen Namen für jede Sprache bereitstellen. Sie können beispielsweise eine Datei namens "LogoWithWhiteText_en.png" und "LogoWithWhiteText_de.png" erstellen.  
  
5.  Klicken Sie mit der rechten Maustaste auf **OEM**, oder klicken Sie mit der rechten Maustaste auf den zugehörigen Sprachschlüssel, klicken Sie auf **Neu**, und klicken Sie dann auf **Zeichenfolge**.  
  
6.  Geben Sie "LogoWithWhiteText" als Zeichenfolge ein, und drücken Sie dann die EINGABETASTE.  
  
7.  Klicken Sie mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie dann auf **Ändern**.  
  
8.  Geben Sie den Pfad zum Logobild ein, und klicken Sie dann auf "OK".  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)