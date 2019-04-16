---
title: Veröffentlichen von Erweiterungen für Windows Admin Center
description: Veröffentlichen von Erweiterungen für Windows Admin Center (Projekt Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.openlocfilehash: 762bd4613fa8ad6cdfb5b44745a7ce78b331499d
ms.sourcegitcommit: 3883eebbba70bfea0221e510863ee1a724a5f926
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/29/2018
ms.locfileid: "5783752"
---
# Erweiterungen veröffentlichen

>Betrifft: Windows Admin Center, Windows Admin Center – Vorschau

Nachdem Sie die Erweiterung entwickelt haben, sollten Sie es veröffentlichen und an andere Benutzer zu testen, oder verwenden Sie zur Verfügung stellen. Je nach Ihrer Zielgruppe und den Zweck der Veröffentlichung gibt es einige Optionen, die unten zusammen mit dem Schritte und Anforderungen für die Veröffentlichung führen wir sehen.

## Optionen für die Veröffentlichung

Es gibt drei primäre Optionen für die konfigurierbare Paketquellen, die von Windows Admin Center unterstützt:
* Microsofts öffentlichen Windows Admin Center NuGet feed
* Eine eigene private NuGet-feed
* Lokale oder Dateifreigabe im Netzwerk

### Die Windows Admin Center-Erweiterung feed veröffentlichen

Standardmäßig ist Windows Admin Center mit einer NuGet verbunden Feed von im Windows Admin Center Produkt-Team von Microsoft verwaltet. Early Vorschauversion der neue Erweiterungen, die von Microsoft entwickelte möglicherweise Feed veröffentlicht und für Windows Admin Center-Benutzer verfügbar. Externe Entwickler zum Erstellen und freigeben Erweiterungen öffentlich Planung haben auch die Möglichkeit, [Fordern Sie ein](#publishing-your-extension-to-the-windows-admin-center-feed) Feed veröffentlichen möchten.

### Die Veröffentlichung auf einem anderen NuGet feed

Sie können auch Ihre eigenen NuGet feed, um Ihre Erweiterungen veröffentlichen Sie mithilfe einer der vielen [verschiedene Optionen für das Einrichten einer privaten Quelle oder über eine NuGet auf dem Dienst](https://docs.microsoft.com/nuget/hosting-packages/overview)erstellen. Der NuGet-Feed muss die NuGet-v2-API unterstützen. Da Windows Admin Center feed Authentifizierung derzeit nicht unterstützt, muss der Feed Lesezugriff auf alle Benutzer konfiguriert werden.

### Sie eine Dateifreigabe veröffentlichen.

Zum Einschränken des Zugriffs der Erweiterung für Ihre Organisation oder auf einer begrenzten Gruppe von Benutzern können Sie eine SMB-Dateifreigabe als Erweiterung feed verwenden. In diesem Fall werden die Dateiberechtigungen Freigabe- und zum Gewähren des Zugriffs auf den Feed angewendet werden.

## Vorbereiten der Erweiterungs für Version

Stellen Sie sicher, lesen und betrachten Sie die folgenden Themen zur Entwicklung:

- [Steuern der Sichtbarkeit des Tools](guides/dynamic-tool-display.md)
- [Zeichenfolgen und Lokalisierung](guides/strings-localization.md)

### Erwägen Sie als eine Vorschauversion freigeben

Wenn Sie eine Vorschauversion der Erweiterung für Testzwecke freigeben, empfehlen wir, die Sie:

- Fügen Sie am Ende der Erweiterung Titel in der Datei .nuspec "(Vorschau)"
- Erläutern Sie die Einschränkungen in der Erweiterung Beschreibung in der Datei .nuspec

## Erstellen ein Erweiterungspaket

Windows Admin Center nutzt NuGet-Pakete und Feeds für die Verteilung und das Herunterladen von Erweiterungen.  Damit für Ihr Paket ausgeliefert werden können müssen Sie Ihre-Plug-Ins und Erweiterungen mit NuGet-Paket zu generieren.  Ein einzelnes Paket kann sowohl eine UI-Erweiterung als auch ein Gateway-Plug-in enthalten, und im folgende Abschnitt führt Sie durch den Prozess.

### 1. erstellen Sie Ihre Erweiterung

Sobald Sie starten Ihre Erweiterung verpacken, erstellen Sie ein neues Verzeichnis auf Ihrem System bereit sind, öffnen Sie eine Konsolen- und CD hinein.  Dies ist das Stammverzeichnis, mit denen wir alle Nuspec und Inhalte Verzeichnisse enthalten, die unsere Paket bilden werden.  Wir werden diese Ordner für die Dauer der in diesem Dokument als "NuGet-Paket" verweisen.

#### UI-Erweiterungen

Um den Vorgang für alle erforderlichen für eine UI-Erweiterung Inhalte sammeln auszuführen, führen Sie "gulp Build" auf Ihr Tool, und stellen Sie sicher, dass der Build erfolgreich ist.  Dieser Prozesspakete, die alle Komponenten, die zusammen in einem Ordner namens "bundle" im Stammverzeichnis der Erweiterung (auf der gleichen Ebene des Verzeichnisses Src) befindet.  Kopieren Sie dieses Verzeichnis und alle es handelt sich um Inhalt in den Ordner "NuGet-Paket".

#### Gateway-Plug-Ins

Verwenden die Build-Infrastruktur (Dies kann so einfach wie das Visual Studio öffnen, und klicken Sie auf die Schaltfläche "Build" sein), kompilieren und Ihre Plug-in erstellen.  Öffnen Sie Ihre Buildausgabeverzeichnis und kopieren Sie die DLLs, die Ihr Plugin darstellen, und platzieren Sie sie in einem neuen Ordner im Verzeichnis "NuGet-Paket" als "Paket" bezeichnet.  Sie müssen nicht die FeatureInterface Dll, nur die DLLs kopieren, die Ihr Code darstellen.

### 2. erstellen Sie die Datei .nuspec

Um das NuGet-Paket zu erstellen, müssen Sie zunächst eine .nuspec-Datei erstellen. Eine .nuspec-Datei ist eine XML-Manifest, das NuGet-Paketmetadaten enthält. Dieses Manifest wird verwendet, um die Erstellung des Pakets und Informationen für Verbraucher bereit.  Platzieren Sie diese Datei im Stammverzeichnis des Ordners "NuGet-Paket".

Hier ist ein Beispiel .nuspec Datei- und die Liste der erforderliche oder empfohlene Eigenschaften. Das vollständige Schema finden Sie unter der [.nuspec Referenz](https://docs.microsoft.com/nuget/reference/nuspec). Speichern Sie die .nuspec-Datei in Ihrem Projekt Stammordner mit einem Dateinamen Ihrer Wahl.

> [!IMPORTANT]
> Die ```<id>``` Wert in der Datei .nuspec entsprechen muss die ```"name"``` Wert in Ihrem Projekts ```manifest.json``` Datei, da ansonsten der veröffentlichten Erweiterung nicht erfolgreich in Windows Admin Center geladen.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
    <packageTypes>
      <packageType name="WindowsAdminCenterExtension" />
    </packageTypes>  
    <id>contoso.project.extension</id>
    <version>1.0.0</version>
    <title>Contoso Hello Extension</title>
    <authors>Contoso</authors>
    <owners>Contoso</owners>
    <requireLicenseAcceptance>false</requireLicenseAcceptance>
    <projectUrl>https://msft-sme.myget.org/feed/windows-admin-center-feed/package/nuget/contoso.sme.hello-extension</projectUrl>
    <licenseUrl>http://YourLicenseLink</licenseUrl>
    <iconUrl>http://YourLogoLink</iconUrl>
    <description>Hello World extension by Contoso</description>
    <copyright>(c) Contoso. All rights reserved.</copyright> 
    <tags></tags>
  </metadata>
  <files>
    <file src="bundle\**\*.*" target="ux" />
    <file src="package\**\*.*" target="gateway" />
  </files>
</package>
```

#### Erforderlichen oder empfohlenen Eigenschaften

| Eigenschaftennamen | Erforderliche / empfohlen | Beschreibung |
| ---- | ---- | ---- |
| packageType | Erforderlich | Verwenden Sie "WindowsAdminCenterExtension" der NuGet-Paket für Windows Admin Center-Erweiterungen definiert ist. |
| id | Erforderlich | Eindeutiger Bezeichner Paket innerhalb des Feeds. Dieser Wert muss mit den Wert "Name" in Ihrer Projektdatei manifest.json übereinstimmen.  Anleitung finden Sie in der [Auswahl eines Paket eindeutige Bezeichner](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number) . |
| title | Erforderlich für die Veröffentlichung im Windows Admin Center-feed | Anzeigename für das Paket, das im Windows Admin Center-Erweiterung-Manager angezeigt wird. |
| version | Erforderlich | Erweiterungsversion. Hilfe der [Semantische Versionskontrolle (SemVer Konvention)](http://semver.org/spec/v1.0.0.html) wird empfohlen, jedoch nicht erforderlich. |
| Autoren | Erforderlich | Wenn im Auftrag Ihres Unternehmens zu veröffentlichen, verwenden Sie den Namen Ihres Unternehmens. |
| description | Erforderlich | Geben Sie eine Beschreibung der Erweiterung Funktionen. |
| "iconUrl" | Bei der Veröffentlichung von Windows Admin Center feed empfohlen | URL für das Symbol, das in der Erweiterung-Manager angezeigt. |
| "projectUrl" | Erforderlich für die Veröffentlichung im Windows Admin Center-feed | Die URL mit der Erweiterung Website. Wenn Sie nicht mit eine separate Website verfügen, verwenden Sie die URL der Webseite Paket auf das NuGet-feed. |
| "licenseUrl" | Erforderlich für die Veröffentlichung im Windows Admin Center-feed | URL, die Erweiterung Endbenutzer-Lizenzvertrag. |
| Dateien | Erforderlich | Dieser beiden Einstellungen richten Sie die Ordnerstruktur, die Windows Admin Center für UI-Erweiterungen und Gateway-Plug-Ins erwartet. |

### 3. Erstellen des Erweiterung NuGet-Pakets

Mithilfe der .nuspec-Datei, die, der Sie soeben erstellt haben, werden Sie jetzt die NuGet-Paket NUPKG-Datei erstellen die Sie hochladen und den feed NuGet veröffentlichen können.

1. Herunterladen des nuget.exe CLI-Tools aus dem [NuGet-Client-Toolswebsite](https://docs.microsoft.com/nuget/install-nuget-client-tools).
2. Führen Sie "nuget.exe Pack [.nuspec Dateiname]", um die NUPKG-Datei zu erstellen.

### 4. Signieren Ihre Erweiterung NuGet-Paket

Alle DLL-Dateien enthalten in der Erweiterung sind erforderlich, um mit einem Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle (CA) signiert werden. Standardmäßig werden ohne Vorzeichen DLL-Dateien blockiert, ausgeführt wird, wenn Windows Admin Center in den Produktionsmodus ausgeführt wird.

Es wird außerdem dringend empfohlen, dass Sie das Erweiterung NuGet-Paket, um sicherzustellen, dass die Integrität des Pakets signieren, aber dies kein erforderlicher Schritt ist.

### 5. testen Sie Ihre Erweiterung NuGet-Paket

Ihre Erweiterungspaket ist jetzt bereit zum Testen! Hochladen der NUPKG-Datei in ein NuGet-Feed oder in eine Dateifreigabe kopieren. Zum Anzeigen und Herunterladen von Paketen aus einer anderen Feed oder Dateifreigabe, müssen Sie [Ihre feed-Konfiguration ändern](../configure/using-extensions.md#installing-extensions-from-a-different-feed) , auf dem NuGet-feed oder der Datei verweisen freigeben müssen. Achten Sie beim Testen sicher, dass die Eigenschaften werden ordnungsgemäß in Extension Manager angezeigt und können Sie erfolgreich installieren und deinstallieren die Erweiterung.

## Veröffentlichen Ihre Erweiterung für das Windows Admin Center feed

Durch Veröffentlichung im Windows Admin Center feed, können Sie Ihre Erweiterung für jeden Benutzer Windows Admin Center zur Verfügung. Da Windows Admin Center SDK noch in der Vorschau ist, möchten wir eng mit Ihnen, Entwicklungsprobleme zu beheben, und stellen Sie sicher, dass Sie ein Produkt Qualität liefern können und Ihren Benutzern auftreten.

Vor der Freigabe der anfänglichen Version der Erweiterung, empfehlen wir, dass Sie eine Erweiterung Rezension Anforderung an Microsoft übermitteln, an mindestens 2 bis 3 Wochen vor der Freigabe, um sicherzustellen, dass wir genügend Zeit zum Überprüfen haben und Sie keine Änderungen an der Erweiterung ggf. vornehmen. Sobald die Erweiterung zur Veröffentlichung bereit ist, müssen Sie es zur Überprüfung an uns senden, und wenn genehmigt, werden wir Sie veröffentlichen, um den Feed für Sie.

Wenn Sie ein Update zur Erweiterung freigeben möchten, müssen Sie danach eine andere Anforderung zur Überprüfung übermitteln. Je nach den Umfang der Änderung, sollte die Bearbeitungszeit für Update Rezensionen in der Regel kürzer sein.

### Übermitteln Sie eine Erweiterung Rezension Anforderung an Microsoft

Um eine Anforderung zur Erweiterung Rezension zu übermitteln, geben Sie die folgende Informationen und als eine e-Mail an [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request)senden. Wir werden innerhalb einer Woche auf Ihre e-Mail-Adresse antworten.

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### Übermitteln Sie Ihre Erweiterungspaket zur Überprüfung und Veröffentlichung

Stellen Sie sicher, dass Sie folgen Sie den Anweisungen über [ein Erweiterungspaket erstellen](#creating-an-extension-package) und die Datei .nuspec ordnungsgemäß definiert und Dateien signiert sind. Außerdem wird empfohlen, dass Sie eine Projekt-Website, einschließlich der folgenden haben:

- Ausführliche Beschreibung der Erweiterung einschließlich Screenshots oder video
- E-Mail-Adresse oder Website Feature Feedback und Fragen zu erhalten

Wenn Sie für die Veröffentlichung der Erweiterungs bereit sind, Senden einer e-Mail an [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) und bieten wir Anweisungen zum Senden Sie uns Ihre Erweiterungspaket. Sobald wir Ihr Paket erhalten, wir überprüfen und wenn genehmigt, zum Windows Admin Center feed veröffentlichen.