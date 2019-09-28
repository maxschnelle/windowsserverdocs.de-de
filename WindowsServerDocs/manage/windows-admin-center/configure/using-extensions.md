---
title: Installieren und Verwalten von Erweiterungen
description: Installieren und Verwalten von Erweiterungen im Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: d49e25591c705afa217b2332ee48eb42c5c2f7ab
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357241"
---
# <a name="install-and-manage-extensions"></a>Installieren und Verwalten von Erweiterungen

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Windows Admin Center wird als erweiterbare Plattform erstellt, wobei jeder Verbindungstyp und jedes Tool eine Erweiterung ist, die Sie einzeln installieren, deinstallieren und aktualisieren können. Sie können nach neuen, von Microsoft und anderen Entwicklern veröffentlichten Erweiterungen suchen und diese einzeln installieren und aktualisieren, ohne die gesamte Installation des Windows Admin Centers aktualisieren zu müssen. Sie können auch einen separaten nuget-Feed oder eine separate Dateifreigabe konfigurieren und Erweiterungen zur internen Verwendung innerhalb Ihrer Organisation verteilen.

## <a name="installing-an-extension"></a>Installieren einer Erweiterung

Windows Admin Center zeigt Erweiterungen an, die im angegebenen nuget-Feed verfügbar sind. Standardmäßig verweist das Windows Admin Center auf den offiziellen nuget-Feed von Microsoft, der von Microsoft und anderen Entwicklern veröffentlichte Erweiterungen hostet.

1. Klicken Sie oben rechts auf die Schaltfläche mit den **Einstellungen** > Klicken Sie im linken Bereich auf **Erweiterungen**. 
2. Auf der Registerkarte **Verfügbare Erweiterungen** werden die Erweiterungen des Feeds aufgelistet, die für die Installation verfügbar sind.
3. Klicken Sie auf eine Erweiterung, um die Erweiterungs Beschreibung, die Version, den Herausgeber und weitere Informationen im **Detail** Bereich anzuzeigen.
4. Klicken Sie auf **Installieren** , um eine Erweiterung zu installieren. Wenn das Gateway im erweiterten Modus ausgeführt werden muss, um diese Änderung vorzunehmen, wird eine UAC-Eingabeaufforderung für erhöhte Rechte angezeigt. Nach Abschluss der Installation wird der Browser automatisch aktualisiert, und das Windows Admin Center wird erneut geladen, wenn die neue Erweiterung installiert ist. Wenn die Erweiterung, die Sie installieren möchten, ein Update für eine zuvor installierte Erweiterung ist, können Sie auf die Schaltfläche **Update to Latest** klicken, um das Update zu installieren. Sie können auch auf der Registerkarte **installierte Erweiterungen** die installierten Erweiterungen anzeigen und überprüfen, ob in der Spalte **Status** ein Update verfügbar ist.

## <a name="installing-extensions-from-a-different-feed"></a>Installieren von Erweiterungen aus einem anderen Feed

Das Windows Admin Center unterstützt mehrere Feeds, und Sie können Pakete von mehreren Feeds gleichzeitig anzeigen und verwalten. Jedem nuget-Feed, der die nuget v2-APIs oder eine Dateifreigabe unterstützt, kann Windows Admin Center zum Installieren von Erweiterungen aus hinzugefügt werden.

1. Klicken Sie oben rechts auf die Schaltfläche mit den **Einstellungen** > Klicken Sie im linken Bereich auf **Erweiterungen**.
2. Klicken Sie im rechten Bereich auf die Registerkarte **Feeds** .
3. Klicken Sie auf **Hinzufügen** , um einen weiteren Feed hinzuzufügen. Geben Sie für einen nuget-Feed die URL für den nuget-v2-Feed ein. Der nuget-Feed-Anbieter oder-Administrator sollte die URL-Informationen bereitstellen können. Geben Sie für eine Dateifreigabe den vollständigen Pfad der Dateifreigabe ein, in der die Erweiterungspaket Dateien (nupkg-Dateien) gespeichert sind.
4. Klicken Sie auf **Hinzufügen**. Wenn das Gateway im erweiterten Modus ausgeführt werden muss, um diese Änderung vorzunehmen, wird eine UAC-Eingabeaufforderung für erhöhte Rechte angezeigt.

In der Liste **Verfügbare Erweiterungen** werden Erweiterungen aller registrierten Feeds angezeigt. Mithilfe der **paketfeed** -Spalte können Sie überprüfen, in welchem Feed jede Erweiterung sich befindet.

## <a name="uninstalling-an-extension"></a>Deinstallieren einer Erweiterung

Sie können alle Erweiterungen deinstallieren, die Sie zuvor installiert haben, oder sogar alle Tools deinstallieren, die im Rahmen der Installation des Windows Admin Centers vorinstalliert wurden.

1. Klicken Sie oben rechts auf die Schaltfläche mit den **Einstellungen** > Klicken Sie im linken Bereich auf **Erweiterungen**. 
2. Klicken Sie auf die Registerkarte **installierte Erweiterungen** , um alle installierten Erweiterungen anzuzeigen.
3. Wählen Sie eine zu deinstallierende Erweiterung aus, **und klicken Sie**dann auf

Nach Abschluss der Deinstallation wird der Browser automatisch aktualisiert, und das Windows Admin Center wird erneut geladen, wenn die Erweiterung entfernt wurde. Wenn Sie ein Tool deinstalliert haben, das als Teil des Windows Admin Centers vorinstalliert war, steht das Tool für die erneute Installation auf der Registerkarte **Verfügbare Erweiterungen** zur Verfügung.

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>Installieren von Erweiterungen auf einem Computer ohne Internetverbindung

Wenn das Windows Admin Center auf einem Computer installiert ist, der nicht mit dem Internet verbunden ist oder sich hinter einem Proxy befindet, ist er möglicherweise nicht in der Lage, auf die Erweiterungen aus dem Windows Admin Center-Feed zuzugreifen und diese zu installieren. Sie können Erweiterungs Pakete manuell oder mit einem PowerShell-Skript herunterladen und Windows Admin Center so konfigurieren, dass Pakete von einer Dateifreigabe oder einem lokalen Laufwerk abgerufen werden.

### <a name="manually-downloading-extension-packages"></a>Manuelles Herunterladen von Erweiterungs Paketen

1. Öffnen Sie auf einem anderen Computer, der über eine Internetverbindung verfügt, einen Webbrowser, und navigieren Sie zur folgenden URL: [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed) . 

   * Möglicherweise müssen Sie ein Konto auf MSFT-SME.myget.org erstellen und sich anmelden, um die Erweiterungs Pakete anzuzeigen.

2. Klicken Sie auf den Namen des Pakets, das Sie installieren möchten, um die Seite Paket Details anzuzeigen.
3. Klicken Sie im rechten Bereich der Seite Paket Details auf den Link **herunterladen** , und laden Sie die nupkg-Datei für die Erweiterung herunter.
4. Wiederholen Sie die Schritte 2 und 3 für alle Pakete, die Sie herunterladen möchten.
5. Kopieren Sie die Paketdateien in eine Dateifreigabe, auf die von dem Computer, auf dem Windows Admin Center installiert ist, oder auf dem lokalen Datenträger des Computers zugegriffen werden kann.
6. [Befolgen Sie die Anweisungen zum Installieren von Erweiterungen aus einem anderen Feed](#installing-extensions-from-a-different-feed).

### <a name="downloading-packages-with-a-powershell-script"></a>Herunterladen von Paketen mit einem PowerShell-Skript

Es sind viele Skripts im Internet verfügbar, um nuget-Pakete von einem nuget-Feed herunterzuladen. Wir verwenden das Skript, das [von Jon Galloway](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), Senior Program Manager bei Microsoft, bereitgestellt wird.

1. Wie im [Blogbeitrag](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell)beschrieben, installieren Sie das Skript als nuget-Paket, oder kopieren Sie das Skript, und fügen Sie es in die PowerShell ISE ein.
2. Bearbeiten Sie die erste Zeile des Skripts mit der V2-URL Ihres nuget-Feeds. Wenn Sie Pakete aus dem offiziellen Windows Admin Center-Feed herunterladen, verwenden Sie die unten angegebene URL.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. Führen Sie das Skript aus, und es werden alle nuget-Pakete aus dem Feed in den folgenden lokalen Ordner heruntergeladen:%USERPROFILE%\documents\nugetlocal
4. [Befolgen Sie die Anweisungen zum Installieren von Erweiterungen aus einem anderen Feed](#installing-extensions-from-a-different-feed).

## <a name="manage-extensions-with-powershell"></a>Verwalten von Erweiterungen mit PowerShell

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Die Vorschau des Windows Admin Centers umfasst ein PowerShell-Modul zum Verwalten Ihrer gatewayerweiterungen.

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

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Erfahren Sie mehr über das Entwickeln einer Erweiterung mit dem Windows Admin Center SDK](../extend/extensibility-overview.md).