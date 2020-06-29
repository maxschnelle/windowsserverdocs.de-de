---
title: Hinzufügen von Branding zum Dashboard, Remote Webzugriff und launchpad
description: Hinzufügen von Branding-Materialien zu ihren Dashboards, Remote Webzugriff und Launchpad-Bildschirmen.
ms.date: 04/10/2014
ms.prod: windows-server
ms.topic: article
ms.assetid: 166262f8-b2a5-4b1c-a4a7-a141e1c54f10
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 056c7264fc90adbf115c3c6587081a449240a98a
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85471085"
---
# <a name="add-branding-to-the-dashboard-remote-web-access-and-launchpad"></a>Hinzufügen von Branding zum Dashboard, zu Remotewebzugriff und zum Launchpad

> Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Sie können Ihre Brandings um zahlreiche zusätzliche Brandings erweitern, indem Sie in der Registrierung entsprechende Einträge hinzufügen. Alle brandingeinträge in der Registrierung für das Betriebssystem befinden sich unter `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Server\OEM` .

Für das Co-Branding muss das Windows Server Essentials-Logo eine minimale Breite von **170 Pixeln**aufweisen, wobei das richtige Seitenverhältnis mit **96 dpi**beibehalten wird.

## <a name="to-add-branding-by-changing-the-registry"></a>So fügen Sie ein Branding durch Ändern der Registrierung hinzu

1. Bewegen Sie Ihre Maus auf dem Server in die obere rechte Ecke des Bildschirms, und klicken Sie auf **Suchen**.

2. Geben Sie im Suchfeld **regedit** ein, und klicken Sie dann auf die Anwendung **Regedit**.

3. Erweitern Sie im Navigationsbereich nacheinander **HKEY_LOCAL_MACHINE**, **SOFTWARE**, **Microsoft** und **Windows Server**. Wenn der **OEM** -Schlüssel nicht vorhanden ist, können Sie ihn erstellen:

    1. Klicken Sie mit der rechten Maustaste auf **Windows Server**, klicken Sie auf **Neu**, und klicken Sie dann auf **Schlüssel**.

    2. Geben Sie **OEM** als Namen des Schlüssels ein.

4. Optionale Wenn Sie einen Eintrag für ein Logo erstellen, können Sie verschiedene Schlüssel erstellen, um die Sprachversionen des Logos zu unterscheiden. Wenn Sie z. B. Logoversionen in Englisch und Deutsch haben, können Sie einen Schlüssel "en-us" und einen Schlüssel "de-de" erstellen. Da alle Logodateien im gleichen Ordner gespeichert sind, müssen Sie Instanzen der Datei mit dem Logobild mit einem eindeutigen Namen für jede Sprache bereitstellen. Sie würden beispielsweise eine Datei namens "DashboardLogo_en.png" und "DashboardLogo_de.png" erstellen.

5. Klicken Sie mit der rechten Maustaste auf **OEM** , oder klicken Sie mit der rechten Maustaste auf den entsprechenden Sprachschlüssel, klicken Sie auf **neu**und dann auf **Zeichen folgen Wert**

6. Geben Sie den Namen der Zeichenfolge ein, und drücken Sie die EINGABETASTE. Weitere Informationen zu den Zeichen folgen Namen und Datenwerten finden Sie im Abschnitt "Registrierungs Zeichenfolgen **und-Werte** " in diesem Artikel.

7. Geben Sie den Namen der Zeichenfolge ein, und drücken Sie die EINGABETASTE. Weitere Informationen zu den Zeichen folgen Namen und Datenwerten finden Sie im Abschnitt "Registrierungs Zeichenfolgen **und-Werte** " in diesem Artikel.

8. Klicken Sie mit der rechten Maustaste auf die neue Zeichenfolge, und klicken Sie dann auf **Ändern**.

9. Geben Sie den Wert aus der Tabelle ein, der dem Zeichenfolgennamen zugeordnet ist, und klicken Sie dann auf **OK**.

10. Wenn Sie einen Eintrag für ein Logo Bild oder angefügte Verknüpfungen erstellen, kopieren Sie die Datei in `%programFiles%\Windows Server\Bin\OEM` . Wenn das Verzeichnis "OEM" nicht vorhanden ist, erstellen Sie es.

11. Wenn Sie Änderungen an der Remote Webzugriff vornehmen, nachdem der Kunde den Server in den Besitz genommen hat, müssen Sie die Remote Webzugriff wie folgt aktivieren:

    1. Klicken Sie auf dem Dashboard auf **Einstellungen** und dann auf die Registerkarte **Zugriff überall**.

    2. Wenn **Zugriff überall** aktiviert ist, klicken Sie auf **Konfigurieren**, und deaktivieren Sie dann das Kontrollkästchen Remote Webzugriff auf der Seite **zu aktivierende Funktionen für "Zugriff überall" aktivieren** des Assistenten zum Einrichten von "Zugriff **überall** ".

    3. Klicken Sie auf **Konfigurieren**.

### <a name="registry-strings-and-values"></a>Registrierungszeichenfolgen und -werte

In der folgenden Tabelle finden Sie Informationen zu den verfügbaren Zeichen folgen Namen und Datenwerten.

| Brandingspeicherort | BESCHREIBUNG | Zeichenfolgenname | Datenwert |
|--|--|--|--|
| Dashboard-Logo | Fügt das Logobild dem Dashboard hinzu. Das Dashboard-Logo muss das PNG-Format aufweisen und darf nicht größer als 350 x 38 Pixel (Breite x Höhe) sein.<p>**Wichtig:** Um das Dashboard mit Ihrem Logo zu versehen, müssen Sie die Kachel "Grafik" Bearbeiten, die auf der OPK-DVD enthalten ist, und Ihr Firmenlogo an das Image anfügen, während Sie die entsprechenden Leerraum Anforderungen befolgen. | DashboardLogo | Geben Sie den Namen der Logobilddatei ein. |
| DashboardClientLogo | Fügt das Logobild dem Dashboard-Client Anmeldebildschirm hinzu. | DashboardClientLogo | Geben Sie den Namen der Logobilddatei ein. |
| Hintergrundbild der Website | Ändert das Hintergrundbild, das auf der Remote Webzugriff-Anmeldeseite angezeigt wird. Häufig verwendete Auflösungen werden wie folgt dargestellt:<ul><li>**1024 x 768 Pixel** : diese Auflösung füllt die Anmeldeseite genau aus.</li><li>**800 x 600 Pixel** : bei dieser Auflösung wird das Bild auf der Seite zentriert und mit einem schwarzen Rand angezeigt.</li><li>**1.280 x 720 Pixel** : diese Auflösung zentriert das Bild. Pixel, die den Wert 1024 x 720 überschreiten, werden nicht angezeigt. | LogonBackground | Geben Sie den Namen der Hintergrundbild Datei ein. |
| Titel der Website | Ersetzt den Titel der Remote Webzugriff Site aus Windows Server Essentials durch den angegebenen Titel. | WebsiteName | Geben Sie den neuen Remote Webzugriff-Website Titel ein. |
| Logo der Website | Ändert das Standardlogo auf der Website für Remotewebzugriff. Die geforderte Größe des Logos beträgt 32 x 32 Pixel. Wenn Ihr Logo kleiner oder größer als dieses ist, wird es gestreckt oder reduziert, um diese Dimensionen zu erfüllen. | WebsiteLogo | Geben Sie den Namen der Logobilddatei ein. |
| Angefügtes Logo der Website | Ihr Partner Logo wird direkt unterhalb des Microsoft-Logos angezeigt, das auf der Remote Webzugriff-Website angezeigt wird. Die geforderte Größe des Logos beträgt 200 x 50 Pixel (Höhe x Breite). Wenn Ihr Logo größer ist, wird es unter Beibehaltung des ursprünglichen Seitenverhältnisses verkleinert. Wenn Ihr Logo kleiner ist, wird es im Pixelbereich von 200 x 50 zentriert, und weder Größe noch Seitenverhältnis werden geändert. | OEMLogo | Geben Sie den Namen der Logobilddatei ein. |
| Links auf der Startseite der Website und der Anmeldeseite | Fügt Links zur Anmeldeseite und der Startseite der Remote Webzugriff-Website hinzu. Die XML-Datei, die die Link Informationen enthält, muss sich im `%programFiles%\Windows Server\Bin\OEM` Ordner befinden. | LinksXML | In der Tabelle LinksXML-Elemente finden Sie eine Liste der Elemente und Beschreibungen. |
| Logo des Launchpads | Fügt das Logobild dem Launchpad hinzu. Das Launchpad-Logo muss im Format PNG vorliegen und darf 64 Pixel nicht überschreiten. | LaunchpadLogo | Geben Sie den Namen der Logobilddatei ein. |

#### <a name="xml-linking-format"></a>XML-Verknüpfungs Format

Sie müssen die Links auf der **Start** Seite der Website und der Anmeldeseite wie folgt formatieren:

```xml
<OemLinks>
    <LogonLinks>
        <Link Name=LogonLinkName>
        <Text>LogonLinkDescription</Text>
        <Url>LogonLinkURL</Url>
        <Icon>LinkIcon</Icon>
        </Link>
    </LogonLinks>

    <HomepageLinks>
        <Link Name=HomepageLinkName>
        <Text>HomepageLinkDescription</Text>
        <Url>HomepageLinkURL</Url>
        <Icon>HomepageLinkIcon</Icon>
        </Link>
    </HomepageLinks>
</OemLinks>
```

### <a name="linksxml-elements"></a>LinksXML-Elemente

| LinksXML-Element | BESCHREIBUNG |
|--|--|
| LogonLinks | Der übergeordnete Eintrag für Anmelde Verknüpfungen. |
| Verknüpfungsname | Der Name des Anmelde Links. |
| Text | Der Text, der als Link zur Anmeldeseite angezeigt wird. |
| URL | Die URL, die in den Link zur Anmeldeseite aufgelöst wird. |
| Symbol | Der Name der Symbol Datei für den Anmeldelink. Diese Datei sollte sich im selben Ordner wie die XML-Datei befinden. Symbolbilder sollten 16x16 Pixel und im PNG-Format sein. Wenn Sie kein Symbol angeben, wird das standardmäßige Link Symbolbild verwendet. |
| HomepageLinks | Der übergeordnete Eintrag für die **Start** Seite. |
| Verknüpfungsname | Der Link Name der **Start** Seite. |
| Text | Der Text, der als Link der **Start** Seite angezeigt wird. |
| URL | Die URL, die in den Link der **Start** Seite aufgelöst wird. |
| Symbol | Der Name der Symbol Datei für den Link der **Start** Seite. Diese Datei sollte sich im selben Ordner wie die XML-Datei befinden. Symbolbilder sollten 16x16 Pixel und im PNG-Format sein. Wenn Sie kein Symbol angeben, wird das Standardbild für den **Start** Seiten Link Symbol verwendet. |

## <a name="additional-references"></a>Zusätzliche Verweise

- [Erstellen und Anpassen des Images](Creating-and-Customizing-the-Image.md)

- [Weitere Anpassungen](Additional-Customizations.md)

- [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md)

- [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)