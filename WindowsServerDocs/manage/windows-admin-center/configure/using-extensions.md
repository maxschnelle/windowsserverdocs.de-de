---
title: Installieren und Verwalten von Erweiterungen
description: Installieren Sie und Verwalten von Erweiterungen in Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: c775dd5a3011115bbb031c0b9e4e24a8911d378e
ms.sourcegitcommit: f1edfc6525e09dd116b106293f9260123a94de0c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/12/2019
ms.locfileid: "9296702"
---
# Installieren und Verwalten von Erweiterungen

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Windows Admin Center wird als eine erweiterbare Plattform erstellt, in denen jede Verbindungstyp und jedes Tool eine Erweiterung ist, die Sie installieren, deinstallieren und einzeln aktualisieren können. Sie können neue Erweiterungen, die von Microsoft und anderen Entwicklern veröffentlicht suchen und installieren und einzeln aktualisieren, ohne die gesamte Windows Admin Center-Installation zu aktualisieren. Sie können auch konfigurieren einen separaten NuGet-Feed oder Dateifreigabe und Erweiterungen für die interne Verwendung in Ihrer Organisation verteilen.

## Installieren einer Erweiterung

Windows Admin Center wird von der angegebenen NuGet feed Erweiterungen verfügbar angezeigt. Standardmäßig zeigt Windows Admin Center auf der offiziellen Microsoft-NuGet feed der Erweiterungen, die von Microsoft und anderen Entwicklern veröffentlicht hostet.

1. Klicken Sie auf die Schaltfläche " **Einstellungen** " in der oberen rechten > im linken Bereich, klicken Sie auf **Erweiterungen**. 
2. Die Registerkarte " **Verfügbare Erweiterungen** " wird die Erweiterungen auf den Feed aufgeführt, die für die Installation verfügbar sind.
3. Klicken Sie auf eine Erweiterung, um die Erweiterung Beschreibung, Version, Herausgeber und andere Informationen im **Detailbereich** anzuzeigen.
4. Klicken Sie auf **Installieren** , um eine Erweiterung zu installieren. Wenn das Gateway im Modus mit erhöhten Rechten für diese Änderung ausführen muss, wird ein UAC-Aufforderung angezeigt werden. Nach Abschluss der Installation Ihren Browser automatisch aktualisiert werden, und Windows Admin Center wird mit der neuen Erweiterung installiert neu geladen werden. Wenn die Erweiterung, die Sie installieren möchten ein Update zu einer zuvor installierten-Erweiterung ist, können Sie die Schaltfläche **auf dem neuesten Update** zum Installieren des Updates klicken. Sie gelangen Sie auf der Registerkarte " **Installierte Erweiterungen** " zum Anzeigen von installierter Erweiterungen und festzustellen, ob ein Update in **der Statusspalte** verfügbar ist.

## Installieren von Erweiterungen aus einem anderen feed

Windows Admin Center unterstützt mehrere Feeds und können Sie anzeigen und Verwalten von Paketen aus mehr als ein Feed zu einem Zeitpunkt. Alle NuGet-feed, unterstützt die NuGet-V2-APIs oder eine Dateifreigabe bei Windows Admin Center hinzugefügt werden kann, für die Installation von Erweiterungen.

1. Klicken Sie auf die Schaltfläche " **Einstellungen** " in der oberen rechten > im linken Bereich, klicken Sie auf **Erweiterungen**.
2. Klicken Sie im rechten Bereich auf der Registerkarte " **Feeds** ".
3. Klicken Sie auf die Schaltfläche **Hinzufügen** , um einen anderen Feed hinzuzufügen. Geben Sie für ein NuGet-Feed das NuGet-V2 feed-URL ein. Das NuGet-feed Anbieter oder Administrator sollten in der Lage, die URL-Informationen bereitzustellen. Geben Sie den vollständigen Pfad der Datei für eine Dateifreigabe Teilen, in denen die Erweiterung-Paketdateien (NUPKG) gespeichert sind.
4. Klicken Sie auf **Hinzufügen**. Wenn das Gateway im Modus mit erhöhten Rechten für diese Änderung ausführen muss, wird ein UAC-Aufforderung angezeigt werden.

Die Liste der **Verfügbaren Erweiterungen** werden Erweiterungen von allen registrierten Feeds angezeigt. Sie können überprüfen, welche Feed jede Erweiterung aus mithilfe der Spalte " **Paket Feed** " ist.

## Deinstallieren einer Erweiterung

Deinstallieren Sie alle Erweiterungen, die Sie zuvor installiert haben können alle Tools, die als Teil der Windows Admin Center-Installation vorab installiert wurden, oder sogar deinstalliert werden.

1. Klicken Sie auf die Schaltfläche " **Einstellungen** " in der oberen rechten > im linken Bereich, klicken Sie auf **Erweiterungen**. 
2. Klicken Sie auf der Registerkarte " **Installierte Erweiterungen** ", um alle installierte Erweiterungen anzuzeigen.
3. Wählen Sie eine Erweiterung von deinstallieren, und klicken Sie auf **Deinstallieren**.

Nach der Deinstallation ist abgeschlossen, Ihren Browser automatisch aktualisiert werden, und Windows Admin Center wird neu geladen werden, mit der Erweiterung entfernt. Wenn Sie ein Tool, die als Teil des Windows Admin Center vorinstalliert wurde deinstalliert, wird das Tool für die Neuinstallation in der Registerkarte " **Verfügbare Erweiterungen** " verfügbar sein.

## Installieren von Erweiterungen auf einem Computer ohne Internetzugang

Wenn Windows Admin Center auf einem Computer, die nicht mit dem Internet verbunden ist oder hinter einem Proxy befindet installiert ist, sind sie möglicherweise nicht in der auf zugreifen und die Erweiterungen aus dem Windows Admin Center-feed installieren. Sie können Erweiterung Pakete manuell oder mit einem Powershellskript herunterladen, und konfigurieren Windows Admin Center, um Pakete aus einer Dateifreigabe oder lokalen Laufwerk abzurufen.

### Erweiterung Pakete manuell herunterladen

1. Klicken Sie auf einem anderen Computer, die über Internetkonnektivität verfügt, öffnen Sie einen Webbrowser, und navigieren Sie mit folgender URL:[https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) 

  * Sie müssen möglicherweise ein Konto auf Msft-sme.myget.org und melden Sie sich die Erweiterung Pakete anzeigen zu erstellen.

2. Klicken Sie auf den Namen des Pakets, die Sie installieren, um die Paket-Details-Seite anzeigen möchten.
3. Klicken Sie auf den Link **herunterladen** im rechten Bereich der Seite Details Paket und Laden Sie die Datei NUPKG für die Erweiterung.
4. Wiederholen Sie die Schritte 2 und 3 für alle Pakete, die Sie herunterladen möchten.
5. Kopieren Sie die Paketdateien, auf eine Dateifreigabe, die auf dem Computer zugegriffen werden kann, denen Windows Admin Center installiert ist, oder auf der lokalen Festplatte des Computers.
6. [Folgen Sie den Anweisungen Erweiterungen aus einem anderen Feed installieren](#installing-extensions-from-a-different-feed).

### Herunterladen von Paketen mit einem Powershellskript

Es gibt viele Skripts im Internet für das Herunterladen von NuGet-Pakete aus einem feed NuGet verfügbar. Wir verwenden das [Skript von Jon Galloway bereitgestellt](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), Senior Program Manager bei Microsoft.

1. Gemäß der [Blogbeitrag](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), installieren Sie das Skript als NuGet-Paket oder kopieren, und fügen Sie das Skript in der PowerShell ISE.
2. Bearbeiten, die die erste Zeile des Skripts auf Ihre NuGet feed's v2-URL. Wenn Sie Pakete aus dem Windows Admin Center offiziellen feed herunterladen, verwenden Sie die folgenden URL.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. Führen Sie das Skript, und es werden alle NuGet-Pakete aus dem Feed herunterladen, in den folgenden lokalen Ordner: %USERPROFILE%\Documents\NuGetLocal
4. [Folgen Sie den Anweisungen Erweiterungen aus einem anderen Feed installieren](#installing-extensions-from-a-different-feed).

## Verwalten von Erweiterungen mit PowerShell

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Windows Admin Center – Vorschau enthält ein PowerShell-Modul, um Ihre Gateway-Erweiterungen zu verwalten.

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

### [Erfahren Sie mehr über das Erstellen einer Erweiterung mit dem Windows Admin Center SDK](../extend/extensibility-overview.md).