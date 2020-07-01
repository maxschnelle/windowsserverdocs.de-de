---
title: Erweiterungen für das Windows Admin Center werden veröffentlicht.
description: Veröffentlichen von Erweiterungen für Windows Admin Center (Project Honolulu)
ms.technology: manage
ms.topic: article
author: daniellee-msft
ms.author: jol
ms.date: 09/18/2018
ms.localizationpriority: medium
ms.prod: windows-server
ms.openlocfilehash: 357c37ec395e5c51f3c3f946414f38ea5f95e9e4
ms.sourcegitcommit: eaf3fb57517b9110082edad356b12daf3345bb2c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593991"
---
# <a name="publishing-extensions"></a>Erweiterungen werden veröffentlicht.

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Nachdem Sie Ihre Erweiterung entwickelt haben, möchten Sie Sie veröffentlichen und anderen Benutzern zur Verfügung stellen, um Sie zu testen oder zu verwenden. Abhängig von Ihrer Zielgruppe und dem Zweck der Veröffentlichung stehen Ihnen einige Optionen zur Verfügung, die wir unten zusammen mit den Schritten und Anforderungen für die Veröffentlichung vorstellen werden.

## <a name="publishing-options"></a>Veröffentlichungsoptionen

Es gibt drei primäre Optionen für konfigurierbare Paketquellen, die von Windows Admin Center unterstützt werden:
* Der öffentliche Windows Admin Center-nuget-Feed von Microsoft
* Ihren eigenen privaten nuget-Feed
* Lokale Datei oder Netzwerkdatei Freigabe

### <a name="publishing-to-the-windows-admin-center-extension-feed"></a>Veröffentlichen im Windows Admin Center-Erweiterungs Feed

Standardmäßig ist das Windows Admin Center mit einem nuget-Feed verbunden, der vom Windows Admin Center-Produktteam bei Microsoft verwaltet wird. Frühe Vorschau Versionen von neuen Erweiterungen, die von Microsoft entwickelt wurden, können in diesem Feed veröffentlicht und für Benutzer von Windows Admin Center verfügbar sein. Externe Entwickler, die die Erstellung und Freigabe von Erweiterungen öffentlich planen, übermitteln möglicherweise auch [eine Anforderung](#publishing-your-extension-to-the-windows-admin-center-feed) zur Veröffentlichung in diesem Feed.

### <a name="publishing-to-a-different-nuget-feed"></a>Veröffentlichen in einem anderen nuget-Feed

Sie können auch einen eigenen nuget-Feed erstellen, um Ihre Erweiterungen unter Verwendung einer der vielen [unterschiedlichen Optionen zum Einrichten einer privaten Quelle oder mithilfe eines nuget-Hostingdiensts](https://docs.microsoft.com/nuget/hosting-packages/overview)zu veröffentlichen. Der nuget-Feed muss die nuget v2-API unterstützen. Da Windows Admin Center derzeit keine Feed-Authentifizierung unterstützt, muss der Feed so konfiguriert werden, dass jeder beliebige den Lesezugriff zulässt.

### <a name="publishing-to-a-file-share"></a>Veröffentlichen in einer Dateifreigabe

Sie können eine SMB-Dateifreigabe als Erweiterungs Feed verwenden, um den Zugriff ihrer Erweiterung auf Ihre Organisation oder auf eine begrenzte Gruppe von Personen einzuschränken. In diesem Fall werden die Berechtigungen für die Dateifreigabe und den Ordner angewendet, um den Zugriff auf den Feed zuzulassen.

## <a name="preparing-your-extension-for-release"></a>Vorbereiten der Extension für Release

Stellen Sie sicher, dass Sie die folgenden Entwicklungsthemen lesen und beachten:

- [Steuern der Sichtbarkeit des Tools](guides/dynamic-tool-display.md)
- [Zeichenfolgen und Lokalisierung](guides/strings-localization.md)

### <a name="consider-releasing-as-a-preview-release"></a>Als Vorschauversion veröffentlichen

Wenn Sie eine Vorschauversion ihrer Erweiterung zu Evaluierungs Zwecken veröffentlichen, empfehlen wir Folgendes:

- Fügen Sie am Ende des Erweiterungs Titels in der nuspec-Datei "(Vorschau)" an.
- Erläutern der Einschränkungen in der Beschreibung ihrer Erweiterung in der nuspec-Datei

## <a name="creating-an-extension-package"></a>Erstellen eines Erweiterungspakets

Windows Admin Center verwendet nuget-Pakete und Feeds zum Verteilen und Herunterladen von Erweiterungen.  Damit Ihr Paket ausgeliefert werden kann, müssen Sie ein nuget-Paket mit den Plug-ins und Erweiterungen generieren.  Ein einzelnes Paket kann sowohl eine Benutzeroberflächen Erweiterung als auch ein Gateway-Plug-in enthalten. im folgenden Abschnitt werden Sie durch den Prozess geführt.

### <a name="1-build-your-extension"></a>1. Erstellen Sie die Erweiterung.

Sobald Sie bereit sind, mit dem Packen Ihrer Erweiterung zu beginnen, erstellen Sie ein neues Verzeichnis auf Ihrem Dateisystem, öffnen Sie eine Konsole, und führen Sie eine CD ein.  Dabei handelt es sich um das Stammverzeichnis, in dem alle nuspec-und Inhaltsverzeichnisse enthalten sein werden, aus denen das Paket besteht.  Dieser Ordner wird für die Dauer dieses Dokuments als "nuget-Paket" referenziert.

#### <a name="ui-extensions"></a>Erweiterungen der Benutzeroberfläche

Führen Sie "Gulp Build" in Ihrem Tool aus, und stellen Sie sicher, dass der Build erfolgreich ist.  Bei diesem Prozess werden alle Komponenten in einem Ordner namens "Bundle" zusammengefasst, der sich im Stammverzeichnis Ihrer Erweiterung befindet (auf derselben Ebene des src-Verzeichnisses).  Kopieren Sie dieses Verzeichnis und den gesamten Inhalt in den Ordner "nuget-Paket".

#### <a name="gateway-plugins"></a>Plug-ins

Verwenden Sie Ihre buildinfrastruktur (Dies könnte so einfach sein wie das Öffnen von Visual Studio und das Klicken auf die Schaltfläche "Build"), kompilieren und erstellen Sie das  Öffnen Sie das Buildausgabeverzeichnis, und kopieren Sie die dll (s), die das Plug-in darstellen, und fügen Sie Sie in einem neuen Ordner im Verzeichnis "nuget-Paket" mit dem Namen "Package" ein.  Sie müssen die featureinterface-dll nicht kopieren, sondern nur die dll (s), die Ihren Code darstellen.

### <a name="2-create-the-nuspec-file"></a>2. Erstellen Sie die nuspec-Datei.

Um das nuget-Paket zu erstellen, müssen Sie zunächst eine nuspec-Datei erstellen. Bei einer nuspec-Datei handelt es sich um ein XML-Manifest, das nuget-Paket Metadaten enthält. Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Benutzer verwendet.  Legen Sie diese Datei im Stammverzeichnis des Ordners "nuget-Paket" ab.

Im folgenden finden Sie ein Beispiel für eine nuspec-Datei und die Liste der erforderlichen oder empfohlenen Eigenschaften. Das vollständige Schema finden Sie in der [. nuspec-Referenz](https://docs.microsoft.com/nuget/reference/nuspec). Speichern Sie die nuspec-Datei im Stamm Ordner Ihres Projekts mit einem Dateinamen Ihrer Wahl.

> [!IMPORTANT]
> Der ```<id>``` Wert in der nuspec-Datei muss mit dem ```"name"``` Wert in der Projektdatei identisch sein ```manifest.json``` , oder Ihre veröffentlichte Erweiterung wird nicht erfolgreich in das Windows Admin Center geladen.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="https://schemas.microsoft.com/packaging/2011/08/nuspec.xsd">
  <metadata>
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

| Eigenschaftenname | Erforderlich/empfohlen | Beschreibung |
| ---- | ---- | ---- |
| packageType | Erforderlich | Verwenden Sie "windowsadmincenterextension", bei dem es sich um den nuget-Pakettyp handelt, der für Erweiterungen des Windows Admin Centers |
| id | Erforderlich | Eindeutiger Paket Bezeichner innerhalb des Feeds. Dieser Wert muss mit dem Wert "Name" in der manifest.jsDatei Ihres Projekts identisch sein.  Informationen finden Sie unter [Choosing a unique package identifier (Auswählen eines eindeutigen Paketbezeichners)](https://docs.microsoft.com/nuget/create-packages/creating-a-package#choosing-a-unique-package-identifier-and-setting-the-version-number). |
| title | Zum Veröffentlichen im Windows Admin Center-Feed erforderlich | Anzeige Name für das Paket, das im Windows Admin Center Extension Manager angezeigt wird. |
| version | Erforderlich | Erweiterungs Version. Die Verwendung der [semantischen Versionsverwaltung (semver-Konvention)](http://semver.org/spec/v1.0.0.html) wird empfohlen, ist jedoch nicht erforderlich. |
| authors | Erforderlich | Wenn Sie im Auftrag Ihres Unternehmens veröffentlichen, verwenden Sie den Namen Ihres Unternehmens. |
| description | Erforderlich | Geben Sie eine Beschreibung der Funktionalität der Erweiterung an. |
| iconUrl | Empfohlen beim Veröffentlichen im Windows Admin Center-Feed | Die URL für das Symbol, das im Erweiterungs-Manager angezeigt werden soll. |
| projectUrl | Zum Veröffentlichen im Windows Admin Center-Feed erforderlich | URL zur Website ihrer Erweiterung. Wenn Sie nicht über eine separate Website verfügen, verwenden Sie die URL für die Paket Webseite im nuget-Feed. |
| licenseUrl | Zum Veröffentlichen im Windows Admin Center-Feed erforderlich | URL zum Endbenutzer-Lizenzvertrag ihrer Erweiterung. |
| files | Erforderlich | Mit diesen beiden Einstellungen wird die Ordnerstruktur eingerichtet, die das Windows Admin Center für UI-Erweiterungen und Gateway-Plug-ins erwartet. |

### <a name="3-build-the-extension-nuget-package"></a>3. Erstellen Sie das nuget-Paket für Erweiterungen.

Mithilfe der zuvor erstellten nuspec-Datei erstellen Sie jetzt die nupkg-Datei "nuget Package", die Sie hochladen und in den nuget-Feed veröffentlichen können.

1. Laden Sie das nuget.exe CLI-Tool von der Website für die [nuget-Client Tools](https://docs.microsoft.com/nuget/install-nuget-client-tools)herunter.
2. Führen Sie "nuget.exe Pack [. nuspec File Name]" aus, um die nupkg-Datei zu erstellen.

### <a name="4-signing-your-extension-nuget-package"></a>4. Signieren eines nuget-Pakets für die Erweiterung

Alle dll-Dateien, die in ihrer Erweiterung enthalten sind, müssen mit einem Zertifikat von einer vertrauenswürdigen Zertifizierungsstelle (Certificate Authority, ca) signiert werden. Standardmäßig wird die Ausführung von nicht signierten dll-Dateien blockiert, wenn das Windows Admin Center im Produktionsmodus ausgeführt wird.

Außerdem wird dringend empfohlen, dass Sie das nuget-Paket für die Erweiterung signieren, um die Integrität des Pakets sicherzustellen. Dies ist jedoch kein erforderlicher Schritt.

### <a name="5-test-your-extension-nuget-package"></a>5. Testen Sie das nuget-Paket der Erweiterung.

Das Erweiterungspaket ist jetzt zum Testen bereit! Laden Sie die nupkg-Datei in einen nuget-Feed hoch, oder kopieren Sie Sie in eine Dateifreigabe. Um Pakete aus einem anderen Feed oder einer anderen Dateifreigabe anzuzeigen und herunterzuladen, müssen Sie [die Feed-Konfiguration so ändern](../configure/using-extensions.md#installing-extensions-from-a-different-feed) , dass Sie auf den nuget-Feed oder die Dateifreigabe verweist. Stellen Sie beim Testen sicher, dass die Eigenschaften im Erweiterungs-Manager richtig angezeigt werden und Sie die Erweiterung erfolgreich installieren und deinstallieren können.

## <a name="publishing-your-extension-to-the-windows-admin-center-feed"></a>Veröffentlichen der Erweiterung im Windows Admin Center-Feed

Wenn Sie im Windows Admin Center-Feed veröffentlichen, können Sie die Erweiterung für jeden Windows Admin Center-Benutzer verfügbar machen. Da sich das SDK für Windows Admin Center noch in der Vorschau Phase befindet, möchten wir Ihnen eng mit Ihnen zusammenarbeiten, um Entwicklungsprobleme zu beheben, und sicherstellen, dass Sie für Ihre Benutzer ein qualitativ hochwertiges Produkt und eine Qualität bereitstellen können.

Bevor Sie die erste Version ihrer Erweiterung freigeben, empfiehlt es sich, eine Anforderung zur Erweiterungs Überprüfung mindestens 2-3 Wochen vor der Freigabe an Microsoft zu senden, um sicherzustellen, dass ausreichend Zeit für die Überprüfung vorhanden ist, und dass Sie ggf. Änderungen an ihrer Erweiterung vornehmen können. Sobald Ihre Extension bereit für die Veröffentlichung ist, müssen Sie Sie zur Überprüfung an uns senden. Wenn Sie genehmigt ist, veröffentlichen wir Sie für Sie im Feed.

Wenn Sie anschließend ein Update für Ihre Erweiterung freigeben möchten, müssen Sie eine weitere Überprüfungs Anforderung einreichen. Abhängig vom Umfang der Änderung sollte die Zeit für die Überprüfung der Aktualisierung im allgemeinen kürzer sein.

### <a name="submit-an-extension-review-request-to-microsoft"></a>Übermitteln einer Anforderung zur Erweiterungs Überprüfung an Microsoft

Geben Sie die folgenden Informationen ein, und senden Sie als e-Mail an, um eine Anforderung zur Erweiterungs Überprüfung zu übermitteln [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Review%20Request) . Wir werden innerhalb einer Woche auf Ihre e-Mail Antworten.

```
Windows Admin Center Extension Review Request
1. Name and email address of extension owner/developer (up to 3 users). If you will be releasing an extension on behalf of your company, provide your company email address.
2. Company name (Only required if you are releasing an extension on behalf of your company):
3. Extension name:
4. Release target date (estimate):
5. For new extension submission - Extension description (early design wire frames, screen mockups or product screenshots are highly recommended):
6. For extension update review – Description of changes (include product screenshots if UI has been significantly changed):
```

### <a name="submit-your-extension-package-for-review-and-publishing"></a>Übermitteln Sie Ihr Erweiterungspaket zum Überprüfen und veröffentlichen.

Stellen Sie sicher, dass Sie die oben aufgeführten Anweisungen zum [Erstellen eines Erweiterungspakets](#creating-an-extension-package) befolgen und die nuspec-Datei ordnungsgemäß definiert ist und Dateien signiert sind. Außerdem wird empfohlen, dass Sie über eine Projektwebsite verfügen, die Folgendes umfasst:

- Ausführliche Beschreibung ihrer Erweiterung einschließlich Screenshots oder Videos
- E-Mail-Adresse oder Website Funktion zum Empfangen von Feedback oder Fragen

Wenn Sie bereit sind, ihre Erweiterung zu veröffentlichen, senden Sie eine e-Mail an, [wacextensionrequest@microsoft.com](mailto:wacextensionrequest@microsoft.com?subject=Windows%20Admin%20Center%20Extension%20Package%20Review) und wir geben Ihnen Anweisungen, wie Sie uns Ihr Erweiterungspaket senden. Sobald wir Ihr Paket erhalten haben, überprüfen wir, ob Sie im Windows Admin Center-Feed veröffentlicht werden.
