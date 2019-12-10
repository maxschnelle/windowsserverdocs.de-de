---
title: Installieren und Verwalten von Erweiterungen
description: Installieren und Verwalten von Erweiterungen im Windows Admin Center (Projekt „Honolulu“)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 7c1a70e36dfac9b23ded8f920ffcc8cccbfff023
ms.sourcegitcommit: 7c7fc443ecd0a81bff6ed6dbeeaf4f24582ba339
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/07/2019
ms.locfileid: "74903946"
---
# <a name="install-and-manage-extensions"></a>Installieren und Verwalten von Erweiterungen

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Windows Admin Center ist als erweiterbare Plattform ausgelegt, bei der jeder Verbindungstyp und jedes Tool eine Erweiterung darstellt, die du einzeln installieren, deinstallieren und aktualisieren kannst. Du kannst nach neuen, von Microsoft und anderen Entwicklern veröffentlichten Erweiterungen suchen und diese einzeln installieren und aktualisieren, ohne die gesamte Windows Admin Centers-Installation aktualisieren zu müssen. Du kannst außerdem einen separaten NuGet-Feed oder eine gesonderte Dateifreigabe konfigurieren und Erweiterungen zur internen Verwendung innerhalb deiner Organisation verteilen.

## <a name="installing-an-extension"></a>Installieren einer Erweiterung

Windows Admin Center zeigt die im angegebenen NuGet-Feed verfügbaren Erweiterungen an. Das Windows Admin Center verweist standardmäßig auf den offiziellen NuGet-Feed von Microsoft, der von Microsoft und anderen Entwicklern veröffentlichte Erweiterungen hostet.

1. Klicke oben rechts auf die Schaltfläche **Einstellungen**, und klicke im linken Bereich auf **Erweiterungen**. 
2. Auf der Registerkarte **Verfügbare Erweiterungen** werden die Erweiterungen des Feeds aufgelistet, die zur Installation verfügbar sind.
3. Klicke auf eine Erweiterung, um die Erweiterungsbeschreibung, die Version, den Herausgeber und weitere Informationen im Bereich **Details** anzuzeigen.
4. Klicke auf **Installieren**, um eine Erweiterung zu installieren. Wenn das Gateway im Modus mit erhöhten Rechten ausgeführt werden muss, um diese Änderung vorzunehmen, wird dir eine Eingabeaufforderung der Benutzerkontensteuerung (UAC) für erhöhte Rechte angezeigt. Nach Abschluss der Installation wird dein Browser automatisch aktualisiert, und das Windows Admin Center wird mit der installierten neuen Erweiterung erneut geladen. Wenn die Erweiterung, die du installieren möchtest, ein Update einer zuvor installierten Erweiterung ist, kannst du auf die Schaltfläche **Auf neueste Version aktualisieren** klicken, um das Update zu installieren. Du kannst auch zur Registerkarte **Installierte Erweiterungen** wechseln, um installierte Erweiterungen anzuzeigen und in der Spalte **Status** zu überprüfen, ob ein Update verfügbar ist.

## <a name="installing-extensions-from-a-different-feed"></a>Installieren von Erweiterungen aus einem anderen Feed

Das Windows Admin Center unterstützt mehrere Feeds, und du kannst Pakete aus mehr als einem Feed gleichzeitig anzeigen und verwalten. Jeder NuGet-Feed, der die NuGet V2-APIs unterstützt, oder eine Dateifreigabe, kann dem Windows Admin Center hinzugefügt werden, um daraus Erweiterungen zu installieren.

1. Klicke oben rechts auf die Schaltfläche **Einstellungen**, und klicke im linken Bereich auf **Erweiterungen**.
2. Klicke im rechten Bereich auf die Registerkarte **Feeds**.
3. Klicke auf die Schaltfläche **Hinzufügen**, um einen anderen Feed hinzuzufügen. Gib für einen NuGet-Feed die URL des NuGet V2-Feeds ein. Der NuGet-Feedanbieter oder -administrator sollte dir die URL-Informationen bereitstellen können. Gib für eine Dateifreigabe den vollständigen Pfad der Dateifreigabe ein, auf der die Erweiterungspaketdateien (NUPKG) gespeichert sind.
4. Klicken Sie auf **Hinzufügen**. Wenn das Gateway im Modus mit erhöhten Rechten ausgeführt werden muss, um diese Änderung vorzunehmen, wird dir eine Eingabeaufforderung der Benutzerkontensteuerung (UAC) für erhöhte Rechte angezeigt.

In der Liste **Verfügbare Erweiterungen** werden Erweiterungen aus allen registrierten Feeds angezeigt. Du kannst anhand der Spalte **Paketfeed** überprüfen, aus welchem Feed die jeweilige Erweiterung stammt.

## <a name="uninstalling-an-extension"></a>Deinstallieren einer Erweiterung

Du kannst alle Erweiterungen deinstallieren, die du zuvor installiert hast, oder sogar alle Tools deinstallieren, die im Rahmen der Installation des Windows Admin Centers vorinstalliert wurden.

1. Klicke oben rechts auf die Schaltfläche **Einstellungen**, und klicke im linken Bereich auf **Erweiterungen**. 
2. Klicke auf die Registerkarte **Installierte Erweiterungen**, um alle installierten Erweiterungen anzuzeigen.
3. Wähle eine zu deinstallierende Erweiterung aus, und klicke auf **Deinstallieren**.

Nach Abschluss der Deinstallation wird dein Browser automatisch aktualisiert, und das Windows Admin Center wird ohne die entfernte Erweiterung erneut geladen. Wenn du ein Tool deinstalliert hast, das als Teil des Windows Admin Centers vorinstalliert war, steht das Tool zur erneuten Installation auf der Registerkarte **Verfügbare Erweiterungen** zur Verfügung.

## <a name="installing-extensions-on-a-computer-without-internet-connectivity"></a>Installieren von Erweiterungen auf einem Computer ohne Internetverbindung

Wenn das Windows Admin Center auf einem Computer installiert ist, der nicht mit dem Internet verbunden ist oder sich hinter einem Proxy befindet, kann es möglicherweise nicht auf die Erweiterungen aus dem Windows Admin Center-Feed zugreifen und diese installieren. Du kannst Erweiterungspakete manuell oder mit einem PowerShell-Skript herunterladen und Windows Admin Center so konfigurieren, dass es Pakete von einer Dateifreigabe oder einem lokalen Laufwerk abruft.

### <a name="manually-downloading-extension-packages"></a>Manuelles Herunterladen von Erweiterungspaketen

1. Öffne auf einem anderen Computer mit Internetverbindung einen Webbrowser, und navigiere zur folgenden URL: [https://msft-sme.myget.org/gallery/windows-admin-center-feed](https://msft-sme.myget.org/gallery/windows-admin-center-feed). 

   * Möglicherweise musst du ein Konto auf „msft-sme.myget.org“ erstellen und dich anmelden, um die Erweiterungspakete anzeigen zu können.

2. Klicke auf den Namen des Pakets, das du installieren möchtest, um die Seite mit den Paketdetails anzuzeigen.
3. Klicke im rechten Bereich der Seite „Paketdetails“ auf den Link **Herunterladen**, und lade die NUPKG-Datei für die Erweiterung herunter.
4. Wiederhole die Schritte 2 und 3 für alle Pakete, die du herunterladen möchtest.
5. Kopiere die Paketdateien auf eine Dateifreigabe, auf die von dem Computer aus, auf dem Windows Admin Center installiert ist, zugegriffen werden kann, oder auf den lokalen Datenträger des Computers.
6. [Befolge die Anweisungen zum Installieren von Erweiterungen aus einem anderen Feed](#installing-extensions-from-a-different-feed).

### <a name="downloading-packages-with-a-powershell-script"></a>Herunterladen von Paketen mit einem PowerShell-Skript

Es sind viele Skripts im Internet verfügbar, um NuGet-Pakete aus einem NuGet-Feed herunterzuladen. Wir verwenden das [Skript, das von Jon Galloway](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell), Senior Program Manager bei Microsoft, bereitgestellt wird.

1. Wie im [Blogbeitrag](https://weblogs.asp.net/jongalloway/downloading-a-local-nuget-repository-with-powershell) beschrieben, installiere das Skript als NuGet-Paket, oder kopiere das Skript, und füge es in die PowerShell ISE ein.
2. Ändere die erste Zeile des Skripts in die v2-URL deines NuGet-Feeds. Wenn du Pakete aus dem offiziellen Windows Admin Center-Feed herunterlädst, verwende die unten angegebene URL.

```powershell
$feedUrlBase = "https://aka.ms/sme-extension-feed"
```

3. Führe das Skript aus, und es lädt alle NuGet-Pakete aus dem Feed in den folgenden lokalen Ordner herunter: „%USERPROFILE%\Dokumente\NuGetLocal“.
4. [Befolge die Anweisungen zum Installieren von Erweiterungen aus einem anderen Feed](#installing-extensions-from-a-different-feed).

## <a name="manage-extensions-with-powershell"></a>Verwalten von Erweiterungen mit PowerShell

Windows Admin Center Preview umfasst ein PowerShell-Modul zum Verwalten deiner Gatewayerweiterungen.

[!INCLUDE [ps-extensions](../includes/ps-extensions.md)]

### <a name="learn-more-about-building-an-extension-with-the-windows-admin-center-sdkextendextensibility-overviewmd"></a>[Weitere Informationen zum Erstellen einer Erweiterung mit dem Windows Admin Center SDK](../extend/extensibility-overview.md).