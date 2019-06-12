---
title: Installieren und Verwalten von Erweiterungen
description: Installieren und Verwalten von Erweiterungen in Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 9038fd480ed105aed3949b0c48dffc7eab94f970
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66445897"
---
# <a name="install-and-manage-extensions"></a>Installieren und Verwalten von Erweiterungen

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Windows Admin Center wird als eine erweiterbare Plattform erstellt, in dem einzelnen Verbindungstyp und Tools eine Erweiterung ist, die Sie installieren, deinstallieren und einzeln aktualisieren können. Suchen Sie nach neuen Erweiterungen veröffentlicht von Microsoft und andere Entwickler, und installieren, und diese einzeln aktualisieren, ohne die gesamte Windows Admin Center-Installation aktualisieren zu müssen. Sie können auch konfigurieren einen separaten NuGet-Feed oder -Dateifreigabe und Erweiterungen intern in Ihrer Organisation verwenden.

## <a name="installing-an-extension"></a>Installieren einer Erweiterung

Windows Admin Center-werden Erweiterungen zur Verfügung stehen aus der angegebenen NuGet-feed angezeigt werden. Standardmäßig zeigt Windows Admin Center auf Microsoft offiziellen NuGet-feed hostet Erweiterungen, die von Microsoft und anderen Entwicklern veröffentlicht.

1. Klicken Sie auf die **Einstellungen** -Schaltfläche in der oberen rechten Ecke > Klicken Sie im linken Bereich auf **Erweiterungen**. 
2. Die **verfügbaren Erweiterungen** Registerkarte listet die Erweiterungen auf dem Feed, die für die Installation verfügbar sind.
3. Klicken Sie auf eine Erweiterung an die erweiterungsbeschreibung, Version, Publisher und andere Informationen in den **Details** Bereich.
4. Klicken Sie auf **installieren** eine Erweiterung installieren. Wenn das Gateway im erweiterten Modus für diese Änderung ausführen muss, wird ein UAC-Eingabeaufforderung für erhöhte Rechte angezeigt werden. Nach Abschluss der Installation Ihr Browser wird automatisch aktualisiert werden, und Windows Admin Center wird erneut geladen werden, mit der neuen Erweiterung installiert. Wenn die Erweiterung versuchen Sie zu installieren ist ein Update für einen zuvor installierten Erweiterung, können Sie auf die **Aktualisierung auf neueste** Schaltfläche, um das Update zu installieren. Sie können auch zum Wechseln der **installierte Erweiterungen** Registerkarte Erweiterungen anzeigen, die installiert und sehen Sie sich, wenn ein Update in verfügbar ist die **Status** Spalte.

## <a name="installing-extensions-from-a-different-feed"></a>Installieren von Extensions von einem anderen feed

Windows Admin Center unterstützt mehrere Feeds, und können Sie anzeigen und Verwalten von Paketen aus mehr als ein Feed zu einem Zeitpunkt. Alle NuGet-feed, unterstützt die NuGet V2-APIs oder eine Dateifreigabe kann Windows Admin Center für die Installation von Erweiterungen hinzugefügt werden.

1. Klicken Sie auf die **Einstellungen** -Schaltfläche in der oberen rechten Ecke > Klicken Sie im linken Bereich auf **Erweiterungen**.
2. Klicken Sie im rechten Bereich auf die **Feeds** Registerkarte.
3. Klicken Sie auf die **hinzufügen** , um einem anderen Feed hinzuzufügen. Geben Sie für ein NuGet-Feed der NuGet V2-feed-URL ein. Anbieter für die NuGet-feed oder Administrator muss die URL-Informationen bereitstellen. Geben Sie für eine Dateifreigabe, die Sie des vollständigen Pfads der Datei Freigabe in der die Erweiterungsdateien-Paket (NUPKG-Datei) gespeichert werden.
4. Klicken Sie auf **Hinzufügen**. Wenn das Gateway im erweiterten Modus für diese Änderung ausführen muss, wird ein UAC-Eingabeaufforderung für erhöhte Rechte angezeigt werden.

Die **verfügbaren Erweiterungen** Liste werden die Erweiterungen von allen registrierten Feeds angezeigt. Sie können überprüfen, welche Feed jede Erweiterung von der Verwendung wird der **Paket Feed** Spalte.

## <a name="uninstalling-an-extension"></a>Deinstallieren einer Erweiterung

Sie können alle Erweiterungen, die Sie zuvor installiert haben auch deinstallieren oder von Tools, die bereits als Teil der Windows Admin Center-Installation installiert wurden.

1. Klicken Sie auf die **Einstellungen** -Schaltfläche in der oberen rechten Ecke > Klicken Sie im linken Bereich auf **Erweiterungen**. 
2. Klicken Sie auf die **installierte Erweiterungen** Registerkarte, um alle installierten Erweiterungen anzuzeigen.
3. Wählen Sie eine Erweiterung zu deinstallieren, und klicken Sie dann **Deinstallieren**.

Nach der Deinstallation ist abgeschlossen, Ihren Browser automatisch aktualisiert werden, und Windows Admin Center wird mit der Erweiterung neu geladen werden. Wenn Sie ein Tool, die bereits als Teil des Windows Admin Center installiert wurde deinstalliert, das Tool stehen für die Neuinstallation in die **verfügbaren Erweiterungen** Registerkarte.

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>Installieren von Erweiterungen auf einem Computer ohne Internetverbindung

Wenn Windows Admin Center auf einem Computer, die nicht mit dem Internet verbunden ist oder hinter einem Proxy installiert ist, sind sie möglicherweise nicht in der zugreifen und die Erweiterungen aus der Windows Admin Center-feed installieren können. Sie können Erweiterungspakete herunterladen, manuell oder mit einem PowerShell-Skript, und Sie können Windows Admin Center zum Abrufen von Paketen aus einer Dateifreigabe oder ein lokales Laufwerk konfigurieren.

### <a name="manually-downloading-extension-packages"></a>Erweiterungspakete manuell herunterzuladen

1. Klicken Sie auf einem anderen Computer, die dem Internet verbunden ist, öffnen Sie einen Webbrowser, und navigieren Sie zu folgender URL: [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

   * Sie müssen ein Konto auf Msft-sme.myget.org und melden Sie sich an die Erweiterungspakete erstellen.

2. Klicken Sie auf den Namen des Pakets, die Sie installieren, um die Detailseite des Pakets anzeigen möchten.
3. Klicken Sie auf die **herunterladen** verknüpfen Sie im rechten Bereich der Detailseite des Pakets und Laden Sie die NUPKG-Datei für die Erweiterung.
4. Wiederholen Sie die Schritte 2 und 3 für alle Pakete, die Sie herunterladen möchten.
5. Kopieren Sie die Paketdateien an eine Dateifreigabe, die auf dem Computer zugegriffen werden kann, die, denen auf Windows Admin Center installiert ist, oder auf der lokalen Festplatte des Computers.
6. [Führen Sie die Anweisungen zum Installieren von Erweiterungen aus einem anderen Feed](#installing-extensions-from-a-different-feed).

### <a name="downloading-packages-with-a-powershell-script"></a>Herunterladen von Paketen mit einem Powershellskript

Es gibt viele Skripts im Internet zum Herunterladen des NuGet-Pakete aus einem NuGet-feed verfügbar. Wir verwenden die [von Jon Galloway bereitgestellte Skript](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), Senior Program Manager bei Microsoft.

1. Siehe die [Blogbeitrag](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), installieren Sie das Skript als NuGet-Paket, oder kopieren und fügen Sie das Skript in PowerShell ISE.
2. Bearbeiten, die die erste Zeile des Skripts in Ihr NuGet-feed ist v2-URL. Wenn Sie Pakete aus dem offiziellen Windows Admin Center Feeds heruntergeladen haben, verwenden Sie die unten aufgeführte URL.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. Das Skript auszuführen, und es werden alle NuGet-Pakete aus dem Feed in den folgenden lokalen Ordner heruntergeladen: %USERPROFILE%\Documents\NuGetLocal
4. [Führen Sie die Anweisungen zum Installieren von Erweiterungen aus einem anderen Feed](#installing-extensions-from-a-different-feed).

## <a name="manage-extensions-with-powershell"></a>Verwalten von Erweiterungen mit PowerShell

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Windows Admin Center Preview umfasst ein PowerShell-Modul, um Ihre Gateway-Erweiterungen zu verwalten.

```powershell
# Add the module to the current session
Import-Module "$env:ProgramFiles\windows admin center\PowerShell\Modules\ExtensionTools"
# Available cmdlets: Get-Feed, Add-Feed, Remove-Feed, Get-Extension, Install-Extension, Uninstall-Extension, Update-Extension

# List feeds
Get-Feed "https://wac.contoso.com"

# Add a new extension feed
Add-Feed -GatewayEndpoint "https://wac.contoso.com" -Feed "\\WAC\our-private-extensions"

# Remove an extension feed
Remove-Feed -GatewayEndpoint "https://wac.contoso.com" -Feed "\\WAC\our-private-extensions"

# List all extensions
Get-Extension "https://wac.contoso.com"

# Install an extension (locate the latest version from all feeds and install it)
Install-Extension -GatewayEndpoint "https://wac.contoso.com" "msft.sme.containers"

# Install an extension (latest version from a specific feed, if the feed is not present, it will be added)
Install-Extension -GatewayEndpoint "https://wac.contoso.com" "msft.sme.containers" -Feed "https://aka.ms/sme-extension-feed"

# Install an extension (install a specific version)
Install-Extension "https://wac.contoso.com" "msft.sme.certificate-manager" "0.133.0"

# Uninstall-Extension
Uninstall-Extension "https://wac.contoso.com" "msft.sme.containers"

# Update-Extension
Update-Extension "https://wac.contoso.com" "msft.sme.containers"
```

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Weitere Informationen zum Erstellen einer Erweiterung mit dem Windows Admin Center-SDK](../extend/extensibility-overview.md).