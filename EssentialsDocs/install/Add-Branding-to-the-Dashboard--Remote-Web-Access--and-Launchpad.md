---
title: Hinzufügen von Branding zum Dashboard, zu Remotewebzugriff und zum Launchpad
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823501"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>Hinzufügen von Branding zum Dashboard, zu Remotewebzugriff und zum Launchpad

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_Branding"></a> Hinzufügen von Branding zum Dashboard, Remotewebzugriff und Launchpad  
 Sie können Ihre Brandings um zahlreiche zusätzliche Brandings erweitern, indem Sie in der Registrierung entsprechende Einträge hinzufügen. Alle Brandingeinträge in der Registrierung für das Betriebssystem befinden sich unter "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM".  
  
 Das Cobranding muss die folgenden Logoanforderungen erfüllen:  
  
-   Das Windows Server Essentials-Logo muss eine Mindestbreite von haben **170 Pixeln**, da das richtige Seitenverhältnis **96 DPI**.  
  
#### <a name="to-add-branding-by-changing-the-registry"></a>So fügen Sie ein Branding durch Ändern der Registrierung hinzu  
  
1.  Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.  
  
2.  Geben Sie im Suchfeld **regedit**ein, und klicken Sie dann auf die Anwendung **Regedit** .  
  
3.  Erweitern Sie im Navigationsbereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft** und **Windows Server**. Wenn der Schlüssel **OEM** nicht vorhanden ist, führen Sie die folgenden Schritte aus, um ihn zu erstellen:  
  
    1.  Klicken Sie mit der rechten Maustaste auf **Windows Server**, klicken Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.  
  
    2.  Geben Sie **OEM** als Namen des Schlüssels ein.  
  
4.  (Optional) Wenn Sie einen Eintrag für ein Logo erstellen, können Sie verschiedene Schlüssel erstellen, um zwischen den Sprachversionen des Logos zu unterscheiden. Wenn Sie z. B. Logoversionen in Englisch und Deutsch haben, können Sie einen Schlüssel "en-us" und einen Schlüssel "de-de" erstellen. Da alle Logodateien im gleichen Ordner gespeichert sind, müssen Sie Instanzen der Datei mit dem Logobild mit einem eindeutigen Namen für jede Sprache bereitstellen. Sie würden beispielsweise eine Datei namens "DashboardLogo_en.png" und "DashboardLogo_de.png" erstellen.  
  
5.  Klicken Sie mit der rechten Maustaste auf **OEM**, oder klicken Sie mit der rechten Maustaste auf den zugehörigen Sprachschlüssel, klicken Sie auf **Neu**, und klicken Sie dann auf **Zeichenfolge**.  
  

6.  Geben Sie den Namen der Zeichenfolge ein, und drücken Sie die EINGABETASTE. Die Zeichenfolgennamen und Datenwerte finden Sie in der Tabelle [Registrierungszeichenfolgen und -werte](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings).  

6.  Geben Sie den Namen der Zeichenfolge ein, und drücken Sie die EINGABETASTE. Die Zeichenfolgennamen und Datenwerte finden Sie in der Tabelle [Registrierungszeichenfolgen und -werte](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_RegStrings).  

  
7.  Klicken Sie mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie dann auf **Ändern**.  
  
8.  Geben Sie den Wert aus der Tabelle ein, der dem Zeichenfolgennamen zugeordnet ist, und klicken Sie dann auf **OK**.  
  
9. Wenn Sie einen Eintrag für ein Logobild oder für angefügte Links erstellen, kopieren Sie die Datei in den Pfad "%programFiles%\Windows Server\Bin\OEM". Wenn das Verzeichnis "OEM" nicht vorhanden ist, erstellen Sie es.  
  
10. Wenn Sie Änderungen, die sich auf Remotewebzugriff auswirken, vornehmen, nachdem der Server vom Kunden übernommen wurde, muss Remotewebzugriff aktiviert werden. Stellen Sie dem Kunden folgende Anweisungen zur Verfügung:  
  
    1.  Klicken Sie auf dem Dashboard auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.  
  
    2.  Wenn Zugriff überall aktiviert ist, klicken Sie auf **Konfigurieren**, und deaktivieren Sie dann im Assistenten zum Einrichten von Zugriff überall auf der Seite **Folgende Funktionen für Zugriff überall aktivieren** das Kontrollkästchen "Remotewebzugriff".  
  
    3.  Klicken Sie auf **Konfigurieren**.  
  
###  <a name="BKMK_RegStrings"></a> Die folgende Tabelle enthält den Speicherort, wo registrierungsänderungen branding auswirken, den Namen und den Datenwert.  
  
### <a name="registry-strings-and-values"></a>Registrierungszeichenfolgen und -werte  
  
|Branding|Beschreibung|Zeichenfolgenname|Datenwert|  
|--------------------------|-----------------|-----------------|----------------|  
|Dashboard-Logo|Fügt das Logobild dem Dashboard hinzu. Das Dashboard-Logo muss das PNG-Format aufweisen und darf nicht größer als 350 x 38 Pixel (Breite x Höhe) sein.<br /><br /> **Wichtig:** Wenn Sie das Dashboard mit einem Cobranding versehen möchten, müssen Sie die Grafikvorlage auf der OPK-DVD bearbeiten und das Logo Ihres Unternehmens unter Beachtung der erforderlichen Leerzeichen an das Bild anhängen. Weitere Informationen finden Sie im bereitgestellten Beispiel.|DashboardLogo|Name der Datei mit dem Logobild|  
|DashboardClientLogo|Fügt das Logobild zum Dashboard Client-Anmeldebildschirm hinzu.|DashboardClientLogo|Name der Datei mit dem Logobild|  
|Hintergrundbild der Website|Ändert das Hintergrundbild, das auf der Anmeldeseite für Remotewebzugriff angezeigt wird. Häufig verwendete Auflösungen werden wie folgt dargestellt:<br /><br /> -1024 X 768 Pixel-Auflösung wird genau die Anmeldeseite ausgefüllt.<br /><br /> -800 x 600 Pixel-Auflösung wird auf der Seite zentriert und mit einem schwarzen Rahmen angezeigt werden<br /><br /> -1280 X 720 Pixel-Auflösung wird das Bild zentriert, und die, die von 1024 x 768 gelegenen Pixel werden nicht angezeigt.|LogonBackground|Name der Datei für das Hintergrundbild|  
|Titel der Website|Ersetzt den Titel der Remotewebzugriff-Website von Windows Server Essentials in einer, den von Ihnen ausgewählten Titel.|WebsiteName|Neuer Titel der Website für Remotewebzugriff|  
|Logo der Website|Ändert das Standardlogo auf der Website für Remotewebzugriff. Die geforderte Größe des Logos beträgt 32 x 32 Pixel. Wenn das Logo kleiner oder größer ist, wird es gestreckt oder verkleinert, damit es diesen Abmessungen entspricht.|WebsiteLogo|Name der Datei mit dem Logobild|  
|Angefügtes Logo der Website|Ihr Partnerlogo wird genau unter dem Microsoft-Logo angezeigt, das auf der Website für Remotewebzugriff angezeigt wird. Die geforderte Größe des Logos beträgt 200 x 50 Pixel (Höhe x Breite). Wenn Ihr Logo größer ist, wird es unter Beibehaltung des ursprünglichen Seitenverhältnisses verkleinert. Wenn Ihr Logo kleiner ist, wird es im Pixelbereich von 200 x 50 zentriert, und weder Größe noch Seitenverhältnis werden geändert.|OEMLogo|Name der Datei mit dem Logobild|  

| Links auf der Homepage der Website und der Anmeldeseite | Fügen Sie Links auf die Anmeldeseite und Startseite der Remotewebzugriff-Website. Die XML-Datei mit den Linkinformationen muss sich unter "%programFiles%\Windows Server\Bin\OEM" befinden. Im folgenden Beispiel wird das Format der XML-Datei veranschaulicht:<br /><br /> <OemLinks\><br /> <LogonLinks\><br /> < Namen verknüpfen\=LogonLinkName ><br /> <Text\>LogonLinkDescription</Text\><br /> <Url\>LogonLinkURL</Url\><br /> <Icon\>LinkIcon</Icon\><br /> </Link\><br /> </LogonLinks\><br /> <HomepageLinks\><br /> < Namen verknüpfen\=HomepageLinkName ><br /> <Text\>HomepageLinkDescription</Text\><br /> <Url\>HomepageLinkURL</Url\><br /> </Link\><br /> </HomepageLinks\><br /> < / OemLinks\>| LinksXML | Finden Sie in der [LinksXML-Elemente](Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) Tabelle enthält eine Liste der Elemente und Beschreibungen. |  

| Links auf der Homepage der Website und der Anmeldeseite | Fügen Sie Links auf die Anmeldeseite und Startseite der Remotewebzugriff-Website. Die XML-Datei mit den Linkinformationen muss sich unter "%programFiles%\Windows Server\Bin\OEM" befinden. Im folgenden Beispiel wird das Format der XML-Datei veranschaulicht:<br /><br /> <OemLinks\><br /> <LogonLinks\><br /> < Namen verknüpfen\=LogonLinkName ><br /> <Text\>LogonLinkDescription</Text\><br /> <Url\>LogonLinkURL</Url\><br /> <Icon\>LinkIcon</Icon\><br /> </Link\><br /> </LogonLinks\><br /> <HomepageLinks\><br /> < Namen verknüpfen\=HomepageLinkName ><br /> <Text\>HomepageLinkDescription</Text\><br /> <Url\>HomepageLinkURL</Url\><br /> </Link\><br /> </HomepageLinks\><br /> < / OemLinks\>| LinksXML | Finden Sie in der [LinksXML-Elemente](../install/Add-Branding-to-the-Dashboard--Remote-Web-Access--and-Launchpad.md#BKMK_Links) Tabelle enthält eine Liste der Elemente und Beschreibungen. |  

| Logo des LaunchPads | Fügt das Logobild dem LaunchPad hinzu. Das Launchpad-Logo muss im PNG-Format aufweisen und darf nicht größer als 64 Pixel sein. | LaunchpadLogo | Name der Datei mit dem Logobild |  
  
###  <a name="BKMK_Links"></a> In der folgende Tabelle aufgelistet und beschrieben von LinksXML-Elemente für die Zeichenfolge benennen.  
  
### <a name="linksxml-elements"></a>LinksXML-Elemente  
  
|LinksXML-Element|Beschreibung|  
|----------------------|-----------------|  
|**LogonLinks**|  
|LogonLinkName|Name des Links zur Anmeldeseite.|  
|LogonLinkDescription|Text, der als Link zur Anmeldeseite angezeigt wird.|  
|LogonLinkURL|URL, die in den Link zur Anmeldeseite aufgelöst wird.|  
|LinkIcon|Name der Datei mit dem Symbol für den Link zur Anmeldeseite. Diese Datei sollte sich im selben Ordner wie die XML-Datei befinden. Symbolbilder für Links sollten 16 x 16 Pixel groß sein und das PNG-Format aufweisen. Wenn Sie kein Symbol für den Link angeben, wird das Standardbild für Links verwendet.|  
|**HomepageLinks**|  
|HomepageLinkName|Name des Links zur Startseite.|  
|HomepageLinkDescription|Text, der als Link zur Startseite angezeigt wird.|  
|HomepageLinkURL|URL, die in den Link zur Startseite aufgelöst wird.|  
|HomepageLinkIcon|Name der Datei mit dem Symbol für den Link zur Startseite. Diese Datei sollte sich im selben Ordner wie die XML-Datei befinden. Bilder für das Symbol für den Link zur Startseite sollten 16 x 16 Pixel groß sein und das PNG-Format aufweisen. Wenn Sie kein Symbol für den Link zur Startseite angeben, wird das Standardbild für Links zur Startseite verwendet.|  
  
## <a name="see-also"></a>Siehe auch  

 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Erstellen und Anpassen des Abbilds](../install/Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

