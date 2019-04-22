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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59820421"
---
# <a name="publishing-extensions"></a>Veröffentlichen von Erweiterungen

>Gilt für: Windows Admin Center, Windows Admin Center Preview

Nachdem Sie die Erweiterung entwickelt haben, sollten Sie es veröffentlichen und andere Benutzer testen oder verwenden Sie zur Verfügung zu stellen. Je nach Ihrer Zielgruppe und der Zweck der Veröffentlichung stehen einige Optionen, die wir unten zusammen mit die Schritte und Anforderungen für die Veröffentlichung einführen, sollten Sie zur Verfügung.

## <a name="publishing-options"></a>Veröffentlichungsoptionen

Es gibt drei primäre Optionen für die konfigurierbare Paketquellen, die Windows Admin Center unterstützt:
* Microsofts öffentliche Windows Admin Center-NuGet-feed
* Eigener privater NuGet-feed
* Lokale oder Dateifreigabe im Netzwerk

### <a name="publishing-to-the-windows-admin-center-extension-feed"></a>Der feed Windows Admin Center-Erweiterung veröffentlichen

Standardmäßig Windows Admin Center verbunden ist, um ein NuGet Feeds, die vom Produktteam bei Microsoft Windows Admin Center verwaltet. Frühe Preview-Versionen von neuen Erweiterungen, die von Microsoft entwickelte können für diesen Feed veröffentlichte als auch für Windows Admin Center Benutzer verfügbar sein. Externe Entwickler, die planen, erstellen und öffentlich Freigeben von Erweiterungen können auch [eine Anfrage](#publishing-your-extension-to-the-windows-admin-center-feed) für diesen Feed zu veröffentlichen.

### <a name="publishing-to-a-different-nuget-feed"></a>Veröffentlichen in einer anderen NuGet-feed

Sie können auch Erstellen Ihres eigenen NuGet-feed, um Ihre Erweiterungen zu veröffentlichen, auf die Verwendung einer der zahlreichen [verschiedene Optionen für das Einrichten einer privaten Quelle oder das Verwenden von NuGet Hostingdienst](https://docs.microsoft.com/nuget/hosting-packages/overview). Der NuGet-Feed muss es sich um die NuGet v2-API unterstützen. Da Windows Admin Center feed Authentifizierung derzeit nicht unterstützt wird, muss der Feed konfiguriert werden, um Lesezugriff auf alle Benutzer zu ermöglichen.

### <a name="publishing-to-a-file-share"></a>Veröffentlichen in einer Dateifreigabe

Um Zugriff auf Ihre Erweiterung in Ihrer Organisation oder auf eine eingeschränkte Gruppe von Personen zu beschränken, können Sie SMB-Dateifreigabe als feed-Erweiterung. In diesem Fall werden die Freigabe- und Dateiberechtigungen angewendet werden, zum Gewähren des Zugriffs auf den Feed.

## <a name="preparing-your-extension-for-release"></a>Vorbereiten der Erweiterungs für die Veröffentlichung

Stellen Sie sicher, dass Sie lesen und erwägen Sie die folgenden Entwicklungsthemen:

- [Steuern des Tools Sichtbarkeit](guides/dynamic-tool-display.md)
- [Zeichenfolgen und Lokalisierung](guides/strings-localization.md)

### <a name="consider-releasing-as-a-preview-release"></a>Betrachten Sie als Vorschauversion veröffentlichen

Wenn Sie eine Preview-Version der Erweiterung für Evaluierungszwecke freigeben, sollten Sie:

- Fügen Sie am Ende des Titels für Ihre Erweiterung in der NuSpec-Datei "(Preview)"
- Erläutert die Einschränkungen in Ihre Erweiterung in der Beschreibung in der NuSpec-Datei

## <a name="creating-an-extension-package"></a>Erstellen ein Erweiterungspaket

Windows Admin Center verwendet die NuGet-Pakete und -Feeds für die Verteilung und das Herunterladen von Erweiterungen.  Damit für Ihr Paket gesendet werden können müssen Sie ein NuGet-Paket, das mit Ihrer-Plug-Ins und Erweiterungen zu generieren.  Ein einzelnes Paket kann sowohl eine Benutzeroberflächenerweiterung als auch eine Gateway-Plug-in enthalten, und der folgende Abschnitt führt Sie durch den Prozess.

### <a name="1-build-your-extension"></a>1. Erstellen Sie Ihre Erweiterung

Sobald Sie zum Starten die Erweiterung verpacken, erstellen ein neues Verzeichnis im Dateisystem bereit sind, öffnen Sie die CD und eine Konsole hinein.  Dies wird im Stammverzeichnis sein, das wir verwenden alle Verzeichnisse für die NuSpec-Datei und den Inhalt enthalten, aus denen unser Paket besteht.  Wir werden diesen Ordner als "NuGet-Paket" für die Dauer dieses Dokuments verweisen.

#### <a name="ui-extensions"></a>UI-Erweiterungen

Führen Sie die "gulp Build" auf das Tool, und stellen Sie sicher, dass der Build erfolgreich ist, zunächst den Prozess zum Erfassen von alle Inhalte, die für eine Benutzeroberflächenerweiterung erforderlich sind.  Dieser Prozesspakete, die alle Komponenten in einen Ordner namens "bündeln" im Stammverzeichnis Ihrer Erweiterung (auf derselben Ebene der das SCR-Verzeichnis) befinden.  Kopieren Sie dieses Verzeichnis und alle es handelt sich um Inhalte in den Ordner "NuGet-Paket".

#### <a name="gateway-plugins"></a>Gateway-Plug-Ins

Verwenden Ihre Build-Infrastruktur (Dies kann so einfach wie das Visual Studio öffnen, und klicken Sie auf die Schaltfläche "Build" sein), kompilieren Sie und erstellen Sie Ihr Plug-in.  Öffnen Sie Ihre Buildausgabeverzeichnis, und kopieren Sie die DLLs, die Ihr Plug-in darstellen, und platzieren Sie sie in einen neuen Ordner im Verzeichnis "NuGet-Paket" als "Paket" bezeichnet.  Sie müssen nicht die FeatureInterface-Dll, nur die DLLs zu kopieren, die Ihren Code darstellen.

### <a name="2-create-the-nuspec-file"></a>2. Erstellen der NuSpec-Datei

Um das NuGet-Paket zu erstellen, müssen Sie zuerst eine NuSpec-Datei zu erstellen. Eine NuSpec-Datei ist eine XML-Manifestdatei, die NuGet-Paketmetadaten enthält. Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Consumer verwendet.  Platzieren Sie diese Datei im Stammverzeichnis des Ordners "NuGet-Paket".

Hier ist ein Beispiel für NuSpec-Datei und die Liste der Eigenschaften, die erforderliche oder empfohlene. Das vollständige Schema finden Sie unter den [NuSpec-Referenz](https://docs.microsoft.com/nuget/reference/nuspec). Die NuSpec-Datei zum Stammordner des Projekts, mit einem Dateinamen Ihrer Wahl zu speichern.

> [!IMPORTANT]
> Die ```<id>``` Wert in der NuSpec-Datei entsprechen muss die ```"name"``` Wert Ihres Projekts ```manifest.json``` Datei ansonsten wird Ihre veröffentlichte Erweiterung nicht erfolgreich in Windows Admin Center geladen.

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

#### <a name="required-or-recommended-properties"></a>Erforderliche oder empfohlene Eigenschaften

| Eigenschaftenname | Erforderlich / empfohlen | Beschreibung |
| ---- | ---- | ---- |
| packageType | Erforderlich | Verwenden Sie "WindowsAdminCenterExtension" der NuGet-Paket für Windows Admin Center-Erweiterungen definiert ist. |
| id | Erforderlich | Eindeutiger Bezeichner "Paket" innerhalb des Feeds. Dieser Wert muss mit dem Wert "Name" in der manifest.json-Datei des Projekts übereinstimmen.  Informationen finden Sie unter [Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number). |
| title | Erforderlich für die Veröffentlichung in der Windows Admin Center-feed | Der Anzeigename für das Paket, das im Windows Admin Center Erweiterungs-Manager angezeigt wird. |
| version | Erforderlich | Version der Erweiterung. Mithilfe von [semantische Versionskontrolle (SemVer-Konvention)](http://semver.org/spec/v1.0.0.html) wird empfohlen, jedoch nicht erforderlich. |
| authors | Erforderlich | Wenn für Ihr Unternehmen zu veröffentlichen, verwenden Sie den Namen Ihres Unternehmens. |
| description | Erforderlich | Geben Sie eine Beschreibung der Funktionen von der Erweiterung. |
| iconUrl | Empfohlen, bei der Veröffentlichung in der Windows Admin Center-feed | URL für das Symbol in der Erweiterungs-Manager angezeigt. |
| projectUrl | Erforderlich für die Veröffentlichung in der Windows Admin Center-feed | Die Erweiterung des Website-URL. Wenn Sie nicht über eine separate Website verfügen, verwenden Sie die URL für die Webseite Paket auf NuGet-feed. |
| licenseUrl | Erforderlich für die Veröffentlichung in der Windows Admin Center-feed | URL, die Erweiterung des Endbenutzer-Lizenzvertrag. |
| files | Erforderlich | Diese beiden Einstellungen richten Sie die Ordnerstruktur, die Windows Admin Center für UI-Erweiterungen und Gateway-Plug-Ins erwartet. |

### <a name="3-build-the-extension-nuget-package"></a>3. Erstellen Sie die Erweiterung NuGet-Paket

Verwenden der NuSpec-Datei, die, der Sie soeben erstellt haben, nun erstellen die NUPKG-Datei von NuGet-Paket Sie die NuGet-feed veröffentlichen und hochladen kann.

1. Laden Sie das nuget.exe-CLI-Tool aus dem [NuGet Client Tools-Website](https://docs.microsoft.com/nuget/install-nuget-client-tools).
2. Führen Sie "nuget.exe Pack [.nuspec File Name]", um die NUPKG-Datei zu erstellen.

### <a name="4-signing-your-extension-nuget-package"></a>4. Signieren Ihre Erweiterung NuGet-Paket

Alle DLL-Dateien enthalten, die in der Erweiterung müssen mit einem Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle (CA) signiert werden. Standardmäßig werden ohne Vorzeichen DLL-Dateien blockiert ausgeführt werden, wenn Windows Admin Center im Produktionsmodus ausgeführt wird.

Es wird auch stark empfohlen, dass Sie die Erweiterung NuGet-Paket, um sicherzustellen, dass die Integrität der Paket signieren, aber dies kein erforderlicher Schritt ist.

### <a name="5-test-your-extension-nuget-package"></a>5. Testen Sie Ihrer Erweiterung NuGet-Paket

Ihres Erweiterungspakets ist jetzt bereit zum Testen! Hochladen der NUPKG-Datei in ein NuGet-Feed ein, oder kopieren Sie ihn an eine Dateifreigabe. Zum Anzeigen und Herunterladen von Paketen von einem anderen Feed oder die Dateifreigabe, müssen Sie [ändern Sie die Konfiguration der feed](../configure/using-extensions.md#installing-extensions-from-a-different-feed) zeigen Sie auf Ihrem NuGet-Feed oder die Dateifreigabe. Beim Testen, stellen Sie sicher, dass die Eigenschaften werden ordnungsgemäß im Erweiterungs-Manager angezeigt, und Sie können erfolgreich installieren und deinstallieren die Erweiterung an.

## <a name="publishing-your-extension-to-the-windows-admin-center-feed"></a>Veröffentlichen Ihre Erweiterung in der Windows Admin Center-feed

Durch die Veröffentlichung der Windows Admin Center-feed, können Sie die Erweiterung für alle Benutzer Windows Admin Center zur Verfügung. Da das Windows Admin Center-SDK noch in der Vorschauphase ist, müssen wir möchten, die eng mit der Sie beheben Sie Probleme bei der Entwicklung, und stellen Sie sicher, dass Sie können zum Übermitteln eines Qualitätsprodukts und Ihren Benutzern auftreten.

Vor dem Freigeben der ersten Version der Erweiterung, empfehlen wir, eine Erweiterung Review-Anforderung an Microsoft mindestens 2 und 3 Wochen vor der Freigabe übermitteln, um sicherzustellen, dass wir genügend Zeit, um zu überprüfen und Sie Ihre Erweiterung bei Bedarf ändern. Sobald die Erweiterung veröffentlicht werden kann, müssen Sie es zur Überprüfung an uns senden, und bei einer Genehmigung werden wir sie veröffentlichen, auf den Feed für Sie.

Wenn Sie ein Update für Ihre Erweiterung freigeben möchten, müssen Sie anschließend eine weitere Anforderung zur Überprüfung übermitteln. Abhängig von der Umfang der Änderungen, sollte die Verarbeitungszeit für die Update-Überprüfung in der Regel kürzer sein.

### <a name="submit-an-extension-review-request-to-microsoft"></a>Eine Erweiterung Review-Anforderung an Microsoft senden

Um eine Anforderung für domänennamenerweiterung Review zu übermitteln, geben Sie die folgende Informationen ein, und als e-Mail zu senden [ wacextensionrequest@microsoft.com ](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request). Wir werden innerhalb einer Woche an Ihre e-Mail Antworten.

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### <a name="submit-your-extension-package-for-review-and-publishing"></a>Übermitteln Sie Ihres Erweiterungspakets für die Überprüfung und Veröffentlichung

Stellen Sie sicher, folgen Sie den Anweisungen oben für [erstellen ein Erweiterungspaket](#creating-an-extension-package) und die NuSpec-Datei ordnungsgemäß definiert ist, und Dateien werden signiert. Außerdem wird empfohlen, dass Sie eine Projektwebsite, einschließlich der folgenden haben:

- Detaillierte Beschreibung Ihrer Erweiterung, einschließlich Screenshots oder Videos
- E-Mail-Adresse oder Website-Funktion zum Empfangen von Feedback oder Fragen

Wenn Sie Ihre Erweiterung veröffentlichen möchten, senden Sie eine e-Mail an [ wacextensionrequest@microsoft.com ](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) und Anweisungen zum Senden Ihres Erweiterungspakets bereitgestellt wird. Wenn wir das Paket erhalten haben, wir prüfen und bei Genehmigung werden die Windows Admin Center-feed veröffentlichen.