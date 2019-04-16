---
title: Erstellen Sie die Oobe.xml-Datei, das Logo und EULA
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="create-the-oobexml-file-including-logo-and-eula"></a>Erstellen Sie die Oobe.xml-Datei, das Logo und EULA

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Sie können Ihre eigenen Endbenutzer-Lizenzvertrag (EULA) Erstkonfiguration hinzufügen, mit der Oobe.xml-Datei. Die Oobe.xml handelt es sich um eine Datei verwendet, um Text und Bilder für die Erstkonfiguration, Windows-Willkommensseite und andere dem Endbenutzer angezeigten Seiten bereitzustellen. Sie können mehrere Oobe.xml-Dateien, um den Inhalt basierend auf der Sprache und Land/Ihrer Region Auswahl des Endbenutzers anzupassen hinzufügen. Weitere Informationen finden Sie in der [Windows Assessment and Deployment Kit für Windows8](https://go.microsoft.com/fwlink/?LinkId=248694) Dokumentation.  
  
 Die Endbenutzer-Lizenzvertrag für Ihr Unternehmen wird zusätzlich zu den Microsoft-EULA angezeigt. Die Microsoft-EULA wird die zuerst während der Erstkonfiguration für Endbenutzer angezeigt werden, und klicken Sie dann Ihre Endbenutzer-Lizenzvertrag wird angezeigt. Ihre Endbenutzer-Lizenzvertrag an einer beliebigen Stelle auf dem Server platziert werden kann, und geben Sie den Speicherort in der Oobe.xml-Datei.  
  
#### <a name="to-add-your-company-eula-and-logo"></a>Hinzufügen Ihres Unternehmens EULA und Logo  
  
1.  Öffnen Sie die Oobe.xml-Datei in einem Text-Editor wie Editor.  
  
2.  In den < Logopath\ >< / Logopath\ >-Tags den absoluten Pfad zur Logodatei eingeben. Diese Datei sollte eine 32-Bit-portable Network (.png) Grafikdatei enthalten, die 240 x 100 Pixel.  
  
3.  In den < Eulafilename\ >< / Eulafilename\ > Tags, geben Sie den absoluten Pfad zur EULA-Datei. Die EULA-Datei muss eine Datei im Rich-Text-Format (.rtf) sein.  
  
4.  In den < Tokentypen >< / Tokentypen >-Tags, geben Sie den Namen Ihres Unternehmens.  
  
     Das folgende Beispiel zeigt die Tags in einer Oobe.xml-Datei:  
  
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
  
6.  Platzieren Sie die Oobe.xml-Datei auf eine der folgenden Speicherorte:  
  
    |Oobe.xml-Speicherort|Bedingung zum Bestimmen der Position|  
    |-----------------------|----------------------------------------|  
    |%windir%\system32\oobe\info\|Der Server ist in einem Land/einer Region und eine einzelne Sprache ausliefern.|  
    |%windir%\system32\oobe\info\default\\ < Language\ >|Der Server wird in einem Land/einer Region und mehreren ausgeliefert.|  
    |%windir%\system32\oobe\info\\ < Land/Region > \ und %windir%\system32\oobe\info\\ < Land/Region > \\ < Language\ > \|Um mehr als ein Land/Region des Servers ausgeliefert wird, und die Einstellungen müssen auf Basis pro Land/Region, jeweils mit einer einzigen Sprache. Wobei < Land/Region > ist der Dezimalversion der ID geografischen Standort (GeoID) des Landes oder der Region, in dem der Server bereitgestellt wird, und < Language\ > ist der Dezimalversion der Gebietsschema-ID (LCID).|  
  
 Wenn Sie ein anderes Unternehmenslogo mit weißem Text verfügen, kann in wirkt dieses aufgrund der blauen Hintergrund besser angezeigt.  Sie können dieses Logo optional angeben, indem Sie einen Registrierungsschlüssel und einen Wert festlegen.  
  
#### <a name="to-specify-a-company-logo-by-setting-the-oem-registry-key"></a>So geben Sie ein Unternehmenslogo Festlegen des Registrierungsschlüssels OEM  
  
1.  Auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suche**.  
  
2.  Geben Sie in das Suchfeld **Regedit**, und klicken Sie dann auf die Anwendung "regedit".  
  
3.  Klicken Sie im Navigationsbereich, navigieren Sie zu **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**. Wenn der OEM-Schlüssel nicht vorhanden ist, erstellen Sie den Schlüssel wie folgt:  
  
    1.  Mit der rechten Maustaste **Windows Server**, klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Geben Sie als Schlüsselnamen **OEM**.  
  
4.  (Optional) Wenn Sie einen Eintrag für ein Logo erstellen, können Sie verschiedene Schlüssel, um die Sprachversionen des Logos zu unterscheiden erstellen. Wenn beispielsweise Sie ein Logo Englisch und Deutsch Versionen haben, können Sie erstellen En-us Schlüssel und ein de-de-Schlüssel. Da alle Logodateien im gleichen Ordner gespeichert sind, müssen Sie Instanzen der Datei mit dem Logobild mit einem eindeutigen Namen für jede Sprache bereitstellen. Beispielsweise können Sie eine Datei namens LogoWithWhiteText_en.png "und" LogoWithWhiteText_de.png erstellen.  
  
5.  Entweder mit der rechten Maustaste **OEM** oder mit der rechten Maustaste in des zugehörigen Sprachschlüssel, klicken Sie auf **neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  
6.  Geben Sie "logowithwhitetext" als Zeichenfolge ein, und drücken Sie dann die EINGABETASTE.  
  
7.  Maustaste auf die neue Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
8.  Geben Sie den Pfad, der das Logobild enthält, und klicken Sie dann auf OK.  
  
## <a name="see-also"></a>Siehe auch  
 [Erste Schritte mit Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)