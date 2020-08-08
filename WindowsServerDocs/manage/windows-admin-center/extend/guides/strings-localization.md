---
title: Zeichen folgen und Lokalisierung im Windows Admin Center
description: Erfahren Sie, wie Sie Ihre Zeichen folgen im Windows Admin Center SDK (Project Honolulu) für die Lokalisierung vorbereiten.
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.date: 06/18/2018
ms.localizationpriority: medium
ms.openlocfilehash: 565e4da69466549538c380457269304c7f1cdd5a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87944920"
---
# <a name="strings-and-localization-in-windows-admin-center"></a>Zeichen folgen und Lokalisierung im Windows Admin Center #

>Gilt für: Windows Admin Center, Windows Admin Center-Vorschau

Im folgenden finden Sie weitere Informationen zum Windows Admin Center Extensions SDK und sprechen über Zeichen folgen und Lokalisierung.

Um die Lokalisierung aller Zeichen folgen zu aktivieren, die auf der Darstellungs Schicht gerendert werden, nutzen Sie die Datei Strings. resjson unter/src/Resources/Strings, die bereits eingerichtet ist. Wenn Sie der Erweiterung eine neue Zeichenfolge hinzufügen müssen, fügen Sie diese dieser resjson-Datei als neuen Eintrag hinzu. Die vorhandene Struktur folgt dem folgenden Format:

``` ts
"<YourExtensionName>_<Component>_<Accessor>": "Your string value goes here.",
```

Sie können ein beliebiges Format für die Zeichen folgen verwenden, aber beachten Sie, dass der Generierungsprozess (der Prozess, der den resjson-Code annimmt und die verwendbare typescript-Klasse ausgibt) Unterstrich (_) in Punkte (.) konvertiert.

Dieser Eintrag lautet z. b.:
``` ts
"HelloWorld_cim_title": "CIM Component",
```
Generiert die folgende accessorstruktur:
``` ts
MsftSme.resourcesStrings<Strings>().HelloWorld.cim.title;
```

## <a name="add-other-languages-for-localization"></a>Hinzufügen weiterer Sprachen für die Lokalisierung ##

Für die Lokalisierung in andere Sprachen muss für jede Sprache eine Strings. resjson-Datei erstellt werden. Diese Dateien müssen stellen in sein ```\loc\output\{!ExtensionName}\{!LanguageFolder}\strings.resjson``` . Die verfügbaren Sprachen mit den entsprechenden Ordnern lauten:

| Sprache      | Ordner      |
| ------------- |-------------|
| Čeština | cs-CZ |
| Deutsch | de-DE |
| Englisch | de-DE |
| Español | es-ES |
| Français | fr-FR |
| Magyar | hu-HU |
| Italiano | it-IT |
| 日本語 | ja-JP |
| 한국어 | ko-KR |
| Nederlands | nl-NL |
| Polski | pl-PL |
| Português (Brasil) | pt-BR |
| Português (Portugal) | pt-PT |
| Русский | ru-RU |
| Svenska | sv-SE |
| Türkçe    | tr-TR |
| 中文(简体) | zh-CN |
| 中文(繁體) | zh-TW |
> [!NOTE]
> Wenn sich die Dateistruktur Anforderungen innerhalb von Loc/Output unterscheiden, müssen Sie localeoffset für den Gulp-Task ' Generate-resjson-JSON-lokalisiert ' anpassen, der sich im gulpfile.js befindet. Dieser Offset ist die Tiefe im Loc-Ordner, in der nach Strings. resjson-Dateien gesucht werden soll.

Jede Strings. resjson-Datei wird auf die gleiche Weise formatiert, wie oben in diesem Handbuch bereits erwähnt.

Wenn Sie z. b. eine Lokalisierung für Español einschließen möchten, schließen Sie diesen Eintrag in ein ```\loc\output\HelloWorld\es-ES\strings.resjson``` :
```json
"HelloWorld_cim_title": "CIM Componente",
```
Wenn Sie lokalisierte Zeichen folgen hinzugefügt haben, muss Gulp Generate erneut ausgeführt werden, damit Sie angezeigt werden. Führen Sie folgenden Befehl aus:
``` cmd
gulp generate
```

Navigieren Sie zu, um zu bestätigen, dass die Zeichen folgen generiert wurden ```\src\app\assets\strings\{!LanguageFolder}\strings.resjson``` . Der neu hinzugefügte Eintrag wird in dieser Datei angezeigt.
Wenn Sie jetzt die Option "language" im Windows Admin Center wechseln, können Sie die lokalisierten Zeichen folgen in ihrer Erweiterung sehen.
