---
title: "Hinzufügen von Branding zum Dashboard, Remotewebzugriff und Launchpad"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 04/10/2014
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 02088b169e44cdcf87385425e1949232ffa408a6
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>Hinzufügen von Branding zum Dashboard, Remotewebzugriff und Launchpad

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_Branding"></a>Hinzufügen von Branding zum Dashboard, Remotewebzugriff und Launchpad  
 Sie können zahlreiche zusätzliche Brandings erweitern, indem Sie Einträge in der Registrierung. Alle brandingeinträge in der Registrierung für das Betriebssystem befinden sich unter HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM.  
  
 Co-Branding muss die folgenden logoanforderungen erfüllen:  
  
-   Das Windows Server Essentials-Logo muss eine Mindestbreite von haben **170 Pixel**, halten das richtige Seitenverhältnis mit **96 DPI**.  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>Zum Hinzufügen von Branding durch Ändern der Registrierung  
  
1.  Auf dem Server, bewegen Sie den Mauszeiger in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suche**.  
  
2.  Geben Sie in das Suchfeld **Regedit**, und klicken Sie dann auf die **Regedit** Anwendung.  
  
3.  Erweitern Sie im Navigationsbereich **HKEY_LOCAL_MACHINE**, erweitern Sie **SOFTWARE**, erweitern Sie **Microsoft**, erweitern Sie **Windows Server**. Wenn die **OEM** Schlüssel nicht vorhanden ist, führen Sie die folgenden Schritteaus, um ihn zu erstellen:  
  
    1.  Mit der rechten Maustaste **Windows Server**, klicken Sie auf **neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Typ **OEM** für den Namen des Schlüssels.  
  
4.  (Optional) Wenn Sie einen Eintrag für ein Logo erstellen, können Sie verschiedene Schlüssel, um die Sprachversionen des Logos zu unterscheiden erstellen. Wenn beispielsweise Sie ein Logo Englisch und Deutsch Versionen haben, können Sie erstellen En-us Schlüssel und ein de-de-Schlüssel. Da alle Logodateien im gleichen Ordner gespeichert sind, müssen Sie Instanzen der Datei mit dem Logobild mit einem eindeutigen Namen für jede Sprache bereitstellen. Beispielsweise würden Sie eine Datei namens DashboardLogo_en.png "und" DashboardLogo_de.png erstellen.  
  
5.  Entweder mit der rechten Maustaste **OEM** oder mit der rechten Maustaste in des zugehörigen Sprachschlüssel, klicken Sie auf **neu**, und klicken Sie dann auf **Zeichenfolgenwert**.  
  

6.  Geben Sie den Namen der Zeichenfolge ein, und drücken Sie dann die EINGABETASTE. Weitere Informationen finden Sie in der [Registrierungszeichenfolgen und -Werte](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings) Tabelle für die Zeichenfolgenwerte Namen und Daten.  

6.  Geben Sie den Namen der Zeichenfolge ein, und drücken Sie dann die EINGABETASTE. Weitere Informationen finden Sie in der [Registrierungszeichenfolgen und -Werte](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings) Tabelle für die Zeichenfolgenwerte Namen und Daten.  

  
7.  Maustaste auf die neue Zeichenfolge, und klicken Sie dann auf **ändern**.  
  
8.  Geben Sie den Wert aus der Tabelle, die dem Zeichenfolgennamen zugeordnet ist, und klicken Sie dann auf **OK**.  
  
9. Wenn Sie einen Eintrag für ein Logobild oder für angefügte Links erstellen, kopieren Sie die Datei in %programFiles%\Windows Server\Bin\OEM. Wenn das Verzeichnis "OEM" nicht vorhanden ist, erstellen Sie ihn.  
  
10. Wenn Sie Änderungen, die Remotewebzugriff auswirken, nachdem der Kunde den Server ist, müssen sie Remote Web Access aktivieren. Teilen Sie dem Kunden die folgenden Schritteausführen:  
  
    1.  Klicken Sie auf dem Dashboard auf **Einstellungen**, und klicken Sie dann auf die **"Zugriff überall"** Registerkarte.  
  
    2.  Wenn "Zugriff überall" aktiviert ist, klicken Sie auf **konfigurieren**, und deaktivieren Sie das Kontrollkästchen Remote Web Access auf dem **Funktionen für Zugriff überall aktivieren** Seite des Assistenten zum "Zugriff überall" einrichten.  
  
    3.  Klicken Sie auf **konfigurieren**.  
  
###  <a name="BKMK_RegStrings"></a>Die folgende Tabelle enthält den Speicherort, in der Registrierung Branding beeinflussen, den Namen und den Wert.  
  
### <a name="registry-strings-and-values"></a>Registrierungszeichenfolgen und -Werte  
  
|Speicherort der Branding|Beschreibung|Zeichenfolgenname|Datenwert|  
|--------------------------|-----------------|-----------------|----------------|  
|Dashboard-Logo|Fügt das Logobild dem Dashboard hinzu. Das Dashboard-Logo muss im PNG-Format aufweisen und darf nicht größer als 350 Pixel breit und 38 Pixel hoch sein.<br /><br /> **Wichtig:** um das Dashboard mit Ihrem Logo Grafikvorlage, müssen Sie die grafikkachel, das Anfügen von Logo Ihres Unternehmens auf das Bild beim Durchführen der erforderlichen Leerzeichen Anforderungen finden Sie auf der OPK-DVD bearbeiten. Weitere Informationen finden Sie unter der Beispielkachel, die bereitgestellt wird.|DashboardLogo|Name der Datei mit dem Logobild|  
|DashboardClientLogo|Fügt das Logobild zum Dashboard Client-Anmeldebildschirm hinzu.|DashboardClientLogo|Name der Datei mit dem Logobild|  
|Hintergrundbild der Website|Ändert das Hintergrundbild, das auf der Anmeldeseite für Remotewebzugriff angezeigt wird. Häufig verwendete Auflösungen werden wie folgt angezeigt:<br /><br /> -1024 X 768 pixelauflösung wird genau die Anmeldeseite ganz ausgefüllt.<br /><br /> -800 x 600 pixelauflösung wird auf der Seite zentriert und mit einem schwarzen Rahmen angezeigt<br /><br /> -1280 X 720 pixelauflösung wird das Bild zentriert und die, die 1024 x 768 gelegenen Pixel werden nicht angezeigt.|LogonBackground|Name der Datei für das Hintergrundbild|  
|Titel der Website|Ersetzt den Titel der Website für Remotewebzugriff von Windows Server Essentials auf einem, den von Ihnen ausgewählten Titel.|WebsiteName|Neue Titel der Website für Remotewebzugriff|  
|Website-Logo|Ändert das Standardlogo auf der Remotewebzugriff-Website. Die geforderte Größe des Logos beträgt 32 x 32 Pixel. Wenn Ihr Logo viel kleiner oder größer ist, werden es gestreckt oder verkleinert, damit Sie diesen Abmessungen entspricht.|WebsiteLogo|Name der Datei mit dem Logobild|  
|Angefügtes Logo der Website|Ihr Partnerlogo wird genau unter dem Microsoft-Logo angezeigt, die auf der Website für Remotewebzugriff angezeigt wird. Die geforderte Größe des Logos beträgt 200 Pixel x 50 Pixel breit. Wenn Ihr Logo größer ist, werden sie kleinere gestellt Beibehaltung des ursprünglichen Seitenverhältnisses verkleinert. Wenn Ihr Logo kleiner ist, es innerhalb des 200 x 50 Pixel zentriert wird und weder Größe noch Seitenverhältnis werden geändert.|OEMLogo|Name der Datei mit dem Logobild|  

| Links auf der Homepage der Website und der Anmeldeseite | Fügen Sie Links auf der Anmeldeseite und Startseite der Remotewebzugriff-Website. Die XML-Datei, die den Linkinformationen muss in %programFiles%\Windows Server\Bin\OEM befinden. Das folgende Beispiel zeigt das Format der XML-Datei:<br /><br /> < OemLinks\ ><br /> < LogonLinks\ ><br /> < link Tokentypen LogonLinkName = ><br /> < skriptregisterkarten > LogonLinkDescription < / skriptregisterkarten ><br /> < Url\ > LogonLinkURL < / Url\ ><br /> < Icon\ > Standardbild für Links < / Icon\ ><br /> < / Link\ ><br /> < / LogonLinks\ ><br /> < HomepageLinks\ ><br /> < link Tokentypen HomepageLinkName = ><br /> < skriptregisterkarten > HomepageLinkDescription < / skriptregisterkarten ><br /> < Url\ > HomepageLinkURL < / Url\ ><br /> < / Link\ ><br /> < / HomepageLinks\ ><br /> < / OemLinks\ > | LinksXML | Weitere Informationen finden Sie in der [LinksXML-Elemente](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) Tabelle enthält eine Liste der Elemente und Beschreibungen. |  

| Links auf der Homepage der Website und der Anmeldeseite | Fügen Sie Links auf der Anmeldeseite und Startseite der Remotewebzugriff-Website. Die XML-Datei, die den Linkinformationen muss in %programFiles%\Windows Server\Bin\OEM befinden. Das folgende Beispiel zeigt das Format der XML-Datei:<br /><br /> < OemLinks\ ><br /> < LogonLinks\ ><br /> < link Tokentypen LogonLinkName = ><br /> < skriptregisterkarten > LogonLinkDescription < / skriptregisterkarten ><br /> < Url\ > LogonLinkURL < / Url\ ><br /> < Icon\ > Standardbild für Links < / Icon\ ><br /> < / Link\ ><br /> < / LogonLinks\ ><br /> < HomepageLinks\ ><br /> < link Tokentypen HomepageLinkName = ><br /> < skriptregisterkarten > HomepageLinkDescription < / skriptregisterkarten ><br /> < Url\ > HomepageLinkURL < / Url\ ><br /> < / Link\ ><br /> < / HomepageLinks\ ><br /> < / OemLinks\ > | LinksXML | Weitere Informationen finden Sie in der [LinksXML-Elemente](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) Tabelle enthält eine Liste der Elemente und Beschreibungen. |  

| Launchpad-Logo | Fügt das Logobild dem LaunchPad hinzu. Das Launchpad-Logo muss im PNG-Format aufweisen und darf nicht größer als 64 Pixel sein. | LaunchpadLogo | Name der Datei mit dem Logobild |  
  
###  <a name="BKMK_Links"></a>In der folgende Tabelle aufgelistet und beschrieben von den LinksXML-Zeichenfolge Name-Elemente.  
  
### <a name="linksxml-elements"></a>LinksXML-Elemente  
  
|LinksXML-Element|Beschreibung|  
|----------------------|-----------------|  
|**LogonLinks**|  
|LogonLinkName|Der Anmeldename für die Verknüpfung.|  
|LogonLinkDescription|Der Text, der als Link zur Anmeldeseite angezeigt wird.|  
|LogonLinkURL|Die Url, die auf den Link zur Anmeldeseite aufgelöst wird.|  
|Standardbild für Links|Der Name der Datei mit dem Symbol für den Link für die Anmeldung. Diese Datei sollte sich im gleichen Ordner wie die XML-Datei. Symbolbilder für Links sollten 16 x 16 Pixel und PNG-Format aufweisen. Wenn Sie keinen Standardbild für Links angeben, wird das Standardbild für Links Symbol verwendet.|  
|**HomepageLinks**|  
|HomepageLinkName|Der Name zur Startseite.|  
|HomepageLinkDescription|Text, der den Link zur Startseite angezeigt wird.|  
|HomepageLinkURL|Die URL, die auf den Link zur Startseite aufgelöst wird.|  
|HomepageLinkIcon|Der Name der Datei mit dem Symbol für den Link zur Startseite. Diese Datei sollte sich im gleichen Ordner wie die XML-Datei. HomepageLinkIcon Bilder sollten 16 x 16 Pixel und PNG-Format aufweisen. Wenn Sie eine HomepageLinkIcon nicht angeben, wird die standardmäßige Startseite Link das Symbolbild verwendet.|  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

