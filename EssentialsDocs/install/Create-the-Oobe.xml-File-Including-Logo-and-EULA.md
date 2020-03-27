---
title: Erstellen der Datei "Oobe.xml" mit Logo und EULA
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8a7b3cc1-21bb-4344-8110-f5d5959b370d
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 58d98aa84b8851e3226ebc76c86cffd574400c42
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80312056"
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>Erstellen der Datei "Oobe.xml" mit Logo und EULA

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Mithilfe der Datei "Oobe.xml" können Sie der Erstkonfiguration Ihre eigenen Endbenutzer-Lizenzbestimmungen (End User License Agreement, EULA) hinzufügen. Die Datei "Oobe.xml" wird verwendet, um Text und Bilder für die Erstkonfiguration, die Windows-Willkommensseite und andere dem Endbenutzer angezeigten Seiten bereitzustellen. Sie können mehrere Dateien vom Typ "Oobe.xml" hinzufügen, um den Inhalt basierend auf der Auswahl der Sprache und des Landes bzw. der Region des Endbenutzers anzupassen. Weitere Informationen finden Sie in der Dokumentation zum [Windows Assessment and Deployment Kit für Windows 8](https://go.microsoft.com/fwlink/?LinkId=248694) .  
  
 Die Endbenutzer-Lizenzbestimmungen für Ihr Unternehmen werden zusätzlich zu den Endbenutzer-Lizenzbestimmungen von Microsoft angezeigt. Die Endbenutzer-Lizenzbestimmungen von Microsoft werden dem Endbenutzer während der Erstkonfiguration zuerst angezeigt, danach folgen Ihre Endbenutzer-Lizenzbestimmungen. Ihre Endbenutzer-Lizenzbestimmungen können an einem beliebigen Ort auf dem Server platziert werden. Sie geben lediglich den Ort in der Datei "Oobe.xml" an.  
  
#### <a name="to-add-your-company-eula-and-logo"></a>So fügen Sie die Endbenutzer-Lizenzbestimmungen und das Logo Ihres Unternehmens hinzu  
  
1. Öffnen Sie die Datei "Oobe.xml" in einem Text-Editor, z. B. in Editor.  
  
2. Geben Sie im < Logopath\></Logopath\> Tags den absoluten Pfad zur Logodatei ein. Die Datei sollte eine 32-Bit-PNG-Datei (Portable Network Graphics) mit 240 x 100 Pixeln enthalten.  
  
3. Geben Sie im < eulafilename\></eulafilename\> Tags den absoluten Pfad zur EULA-Datei ein. Bei der EULA-Datei muss es sich um eine RTF-Datei handeln.  
  
4. Geben Sie im < Namen\></Name\> Tags den Namen Ihres Unternehmens ein.  
  
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
  
5. Speichern Sie die Datei.  
  
6. Legen Sie die Datei "Oobe.xml" unter einem der folgenden Pfade ab:  
  
   |Pfad zur Datei "Oobe.xml"|Bedingung zum Festlegen des Pfads|  
   |-----------------------|----------------------------------------|  
   |%WINDIR%\System32\Oobe\Info\|der Server wird in einem Land/einer Region und einem einzelnen Sprachsystem ausgeliefert.|  
   |%windir%\system32\oobe\info\default\\< Language\>|Der Server wurde für den Vertrieb in einem Land/einer Region und mehreren Sprachsystemen konzipiert.|  
   |%WINDIR%\System32\Oobe\Info\\< Country/Region > \ und%WINDIR%\System32\Oobe\Info\\< Land/Region >\\< Sprache\>\|der Server in mehr als einem Land bzw. in einer Region ausgeliefert wird und die Einstellungen pro Land/Region angepasst werden müssen, jeweils mit einer einzigen Sprache. Dabei ist < Land/Region > die Dezimal Version des geografischen Standort Bezeichners (Geoid) des Landes oder der Region, in der der Server bereitgestellt wird, und < Language\> die Dezimal Version der Gebiets Schema-ID (Locale Identifier, LCID) ist.|  
  
   Wenn Sie über ein anderes Unternehmenslogo mit weißem Text verfügen, wirkt dieses aufgrund des dunklen Hintergrunds im Setupablauf möglicherweise besser.  Sie können dieses Logo optional angeben, indem Sie einen Registrierungsschlüssel mit zugehörigem Wert angeben.  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>So geben Sie ein Unternehmenslogo durch Festlegen des Registrierungsschlüssels "OEM" an  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **regedit** ein, und klicken Sie dann auf die Anwendung "Regedit".  
  
3.  Navigieren Sie im Navigationsbereich zu **HKEY_LOCAL_MACHINE**, und erweitern Sie nacheinander **SOFTWARE**, **Microsoft** und **Windows Server**. Wenn der Schlüssel "OEM" nicht vorhanden ist, gehen Sie wie folgt vor, um ihn zu erstellen:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, klicken Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Geben Sie als Schlüsselnamen **OEM** ein.  
  
4.  (Optional) Wenn Sie einen Eintrag für ein Logo erstellen, können Sie verschiedene Schlüssel erstellen, um zwischen den Sprachversionen des Logos zu unterscheiden. Wenn Sie z. B. Logoversionen in Englisch und Deutsch haben, können Sie einen Schlüssel "en-us" und einen Schlüssel "de-de" erstellen. Da alle Logodateien im gleichen Ordner gespeichert sind, müssen Sie Instanzen der Datei mit dem Logobild mit einem eindeutigen Namen für jede Sprache bereitstellen. Sie können beispielsweise eine Datei namens "LogoWithWhiteText_en.png" und "LogoWithWhiteText_de.png" erstellen.  
  
5.  Klicken Sie mit der rechten Maustaste auf **OEM**, oder klicken Sie mit der rechten Maustaste auf den zugehörigen Sprachschlüssel, klicken Sie auf **Neu**, und klicken Sie dann auf **Zeichenfolge**.  
  
6.  Geben Sie "LogoWithWhiteText" als Zeichenfolge ein, und drücken Sie dann die EINGABETASTE.  
  
7.  Klicken Sie mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie dann auf **Ändern**.  
  
8.  Geben Sie den Pfad zum Logobild ein, und klicken Sie dann auf "OK".  
  
## <a name="see-also"></a>Weitere Informationen  
 [Die ersten Schritte mit dem Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md) -   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)