---
title:
- TITEL DES ARTIKELS
description: ''
author:
- GITHUB USERNAME
ms.author:
- MICROSOFT ALIAS
ms.date:
- DATE
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: ''
ms.localizationpriority:
- high/medium/low
ms.openlocfilehash: 4f885680426c0bfa55d5f73a7ef0c2143a8dd5a9
ms.sourcegitcommit: e0479b0114eac7f232e8b1e45eeede96ccd72b26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/22/2018
ms.locfileid: "2082157"
---
# <a name="metadata-and-markdown-template"></a>Metadaten und Abzugsverteilung(en)-Vorlage

Diese Vorlage VORGÄNGEN enthält Beispiele der Abzugsverteilung(en) Syntax sowie Anleitungen zum Festlegen der Metadaten. Wenn der Großteil erhalten möchten, müssen Sie sowohl die [Rohdaten Abzugsverteilung(en)](https://raw.githubusercontent.com/Microsoft/WindowsServerDocs-pr/master/Contributor-guide/ws-template.md?token=AG1vEhARRHNLtPgKXP35BGjNZGajKOArks5YLNIwwA%3D%3D) und die [Ansicht gerendert](https://github.com/Microsoft/WindowsServerDocs-pr/blob/master/Contributor-guide/ws-template.md)anzeigen. (Die Rohdaten Abzugsverteilung(en) zeigt den Metadaten-Block, während die gerenderte Ansicht nicht der Fall ist.)

Beim Erstellen einer Abzugsverteilung(en)-Datei sollten Sie diese Vorlage in eine neue Datei kopieren, füllen Sie die Metadaten als unten angegebenen Satz die H1-Überschrift an den Titel des Artikels und löschen Sie den Inhalt. Alles in Großbuchstaben in eckige Klammern benötigt Ihre Aufmerksamkeit.


## <a name="metadata"></a>Metadaten 

Der vollständige Metadaten-Block ist oben. Einige wichtige Hinweise:

- Sie **müssen** haben ein Leerzeichen zwischen dem Doppelpunkt (:)) und den Wert für ein Metadata-Element.
- Doppelpunkte in einen Wert (beispielsweise einen Titel) unterbrechen den Parser Metadaten. Verwenden Sie die HTML-Codierung für ein Doppelpunkt des an ihrer Stelle `&#58;` (z. B. `"title: Azure Rights Management&#58; the basics | Azure RMS"`).
- **Titel**: Dieser Titel wird in Suchergebnissen angezeigt. 
- **Autor**: das Autorenfeld sollte die **GitHub Benutzername** des Autors, nicht ihre Alias enthalten.
- **ms.Prod**, **ms.technology**: Verwenden von "Windows-Server-Schwellenwert" für ms.prod (oder w10, wenn Sie diese Vorlage zum Erstellen von Inhalten für Windows 10 verwenden). Wenden Sie sich an Ihren CX-Kontakt, den ms.technology-Eigenschaftswert abzurufen.

## <a name="basic-markdown-gfm-and-special-characters"></a>Grundlegende Abzugsverteilung(en), GFM und Sonderzeichen

Alle grundlegenden und GitHub flavored Abzugsverteilung(en) wird unterstützt. Weitere Informationen dazu finden Sie unter:

- [Geplante Abzugsverteilung(en) syntax](https://daringfireball.net/projects/markdown/syntax)
- [Dokumentation zu GitHub flavored Abzugsverteilung(en) (GFM)](https://guides.github.com/features/mastering-markdown)

Abzugsverteilung(en) verwendet Sonderzeichen wie \ *, \', und \ # für die Formatierung. Wenn Sie eines der folgenden Zeichen in Ihrer Inhalte aufnehmen möchten, müssen Sie einen der folgenden Schritte ausführen:

- Platzieren Sie einen umgekehrten Schrägstrich vor das Sonderzeichen "sie" Escapezeichen (beispielsweise \\\ * für eine \ *)
- Verwenden Sie die [HTML-Entität Code](http://www.ascii.cl/htmlcodes.htm) für das Zeichen (beispielsweise \ & \#42\; für eine & #42;).

## <a name="headings"></a>Überschriften

Überschriften sollte erfolgen 1-6 Hash-Zeichen (#) am Anfang der Zeile an, dass eine Überschrift, entsprechend der HTML-Überschriften Ebenen H1 bis H6 Atx-Formatvorlage verwenden, d. h., verwenden. Beispiele der ersten und zweiten Ebene Kopfzeilen werden oben verwendet. 

Es **muss nur eine Überschrift der ersten Ebene (H1) in Ihrer Thema, das als Titel auf der Seite angezeigt wird** .  

Überschriften der zweiten Ebene generiert das Inhaltsverzeichnis auf der Seite, die im Abschnitt "In diesem Artikel" unterhalb des Titels auf der Seite angezeigt wird.

### <a name="third-level-heading"></a>Überschrift der dritten Ebene
#### <a name="fourth-level-heading"></a>Überschrift der vierten Ebene
##### <a name="fifth-level-heading"></a>Fünften Ebene Überschrift
###### <a name="sixth-level-heading"></a>Überschrift der sechsten-Ebene

## <a name="text-styling"></a>Text formatieren

*Kursiv* 

**Fett** 

~~Durchgestrichen~~

## <a name="links"></a>Links

### <a name="internal-links"></a>Interne Hyperlinks

Um eine Kopfzeile in der gleichen Abzugsverteilung(en) Datei verknüpfen, die Quelle des veröffentlichten Artikels, suchen Sie die ID der Head (z. B. `id="blockquote"`), und Verknüpfen mit # + -Id (z. B. `#blockquote`).

- Beispiel: [Blockquotes](#blockquote)

Verwenden Sie zum Verknüpfen mit einer Abzugsverteilung(en)-Datei in der gleichen Repo [relative Hyperlinks](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2), einschließlich ".md" am Ende des Dateinamens.

- Beispiel: [Tipps und Punkte](tips-gotchas.md)
- Beispiel: [Tools und Setup für Teilnehmer](../readme.md)

Verwenden Sie zum Verknüpfen mit einer Kopfzeile in einer Abzugsverteilung(en)-Datei in der gleichen Repo relative verknüpfen + Hashtag verknüpfen.

- Beispiel: [Löschen von Dateien](tips-gotchas.md#deleting-files)

### <a name="external-links"></a>Externe Links

Um in einer externen Datei zu verknüpfen, verwenden Sie die vollständige URL als den Link.

- Beispiel: [GitHub](http://www.github.com)

Wenn eine URL in einer Datei Abzugsverteilung(en) angezeigt wird, wird es in einem Link umgewandelt.

- Beispiel: http://www.github.com

## <a name="lists"></a>Listen

### <a name="ordered-lists"></a>Sortierte Listen

1. Dies  
1. Ist
1. Ein
1. Bestellt
1. Liste  


#### <a name="ordered-list-with-an-embedded-list"></a>Sortierte Liste mit einer eingebetteten Liste

1. Hier
1. stammen
1. ein
1. eingebettete
    1. Verpassen leicht
    1. Pflaume Dozenten
1. bestellt
1. list


### <a name="unordered-lists"></a>Nicht sortierte Listen

- Dies 
-  auf 
- a
- Aufzählung
- list


##### <a name="unordered-list-with-an-embedded-list"></a>Ungeordnete Liste mit einer eingebetteten Liste

- Dies  
- Aufzählung 
- list
    - Frau Peacock
    - John Green
- enthält  
- Andere
    1. Colonel Senf
    1. Frau weiß
- Listen


## <a name="horizontal-rule"></a>Horizontale Linie

---

## <a name="tables"></a>Tabellen

Verwenden Sie in fast jeder Instanz MD-Formatierung für Tabellen. Während der HTML-Tabellen mehr Flexibilität bieten Verwendung wir nicht deren in unseren Content. Wenn Sie eine HTML-Tabelle in Ihrer Artikel haben, werden wir diese Artikel nicht zusammengeführt.

| Tabellen        | Sind           | Leuchtstoff  |
| ------------- |:-------------:| -----:|
| Spalte 3 ist      | rechts ausgerichtet | $1600 |
| Spalte 2 ist      | Zentriert      |   12 USD |
| SP 1 ist Standard | Linksbündig     |    $1 |


## <a name="code"></a>Code

### <a name="generic-codeblock"></a>Generische codeblock

Leerzeichen Sie Code vier für die Codierung von generischen Codeblock.

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }


### <a name="codeblocks-with-language-identifier"></a>Codeblocks mit Sprach-ID

Verwenden Sie drei Backticks (& 96 #; #96; & #96;) + eine Sprach-ID anzuwendende Farbe sprachspezifische-Codierung auf einen Codeblock.  Hier wird die gesamte Liste der [Sprachen-IDs GitHub Flavored Abzugsverteilung(en) (GFM)](https://github.com/jmm/gfm-lang-ids/wiki/GitHub-Flavored-Markdown-(GFM)-language-IDs).

##### <a name="c9839"></a>C & #9839;

```c#
using System;
namespace HelloWorld
{
    class Hello 
    {
        static void Main() 
        {
            Console.WriteLine("Hello World!");

            // Keep the console window open in debug mode.
            Console.WriteLine("Press any key to exit.");
            Console.ReadKey();
        }
    }
}
```
#### <a name="python"></a>Python

```python
friends = ['john', 'pat', 'gary', 'michael']
for i, name in enumerate(friends):
    print "iteration {iteration} is {name}".format(iteration=i, name=name)
```
#### <a name="powershell"></a>PowerShell

```powershell
Clear-Host
$Directory = "C:\Windows\"
$Files = Get-Childitem $Directory -recurse -Include *.log `
-ErrorAction SilentlyContinue
```

### <a name="inline-code"></a>Inlinecode

Verwenden Sie Backticks (& #96;) für `inline code`.

## <a name="blockquotes"></a>Blockquotes

> Der Dürre jetzt zehn Millionen Jahren dauerte hatte, und die von der schlechte Lizards Kaiserherrschaft hatte lange inzwischen beendet. Hier auf die Äquator, in dem Kontinent, die einen Tag als Afrika bezeichnet werden würde der Wettbewerb um Vorhandensein hatte erreicht eine neue Climax der Kämpfe, und die Victor wurde noch nicht im Blick. In diesem Land barren und verdorrt ist konnte nur kleine oder die Swift die harten Schnörkel oder sogar hoffe überstehen.

## <a name="images"></a>Images

### <a name="static-image"></a>Statisches Bild

![Dies ist die Alt-text](../windowsserverdocs/get-started/media/wsbanner.png)

### <a name="linked-image"></a>Verknüpftes Bild

[![aLt Text für verknüpfte Bild](../windowsserverdocs/get-started/nano.png)](../windowsserverdocs/get-started/getting-started-with-nano-server.md) 

## <a name="alerts"></a>Warnungen

### <a name="note"></a>Hinweis:

> [!NOTE]
> Hierbei handelt es sich um Hinweis

### <a name="warning"></a>Warnung

> [!WARNING]
> Dies ist eine Warnung

### <a name="tip"></a>Tipp

> [!TIP]
> Hierbei handelt es sich um Tipp

### <a name="important"></a>Wichtig

> [!IMPORTANT]
> Das ist wichtig

