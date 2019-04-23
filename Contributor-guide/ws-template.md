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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59879561"
---
# <a name="metadata-and-markdown-template"></a>Metadaten- und Markdownvorlage

Diese OPS-Vorlage enthält Beispiele für markdownsyntax sowie Anleitungen zum Festlegen der Metadaten. Um die meisten davon zu erhalten, müssen Sie beide anzeigen die [unformatierte Markdown](https://raw.githubusercontent.com/Microsoft/WindowsServerDocs-pr/master/Contributor-guide/ws-template.md?token=AG1vEhARRHNLtPgKXP35BGjNZGajKOArks5YLNIwwA%3D%3D) und [Ansicht gerendert](https://github.com/Microsoft/WindowsServerDocs-pr/blob/master/Contributor-guide/ws-template.md). (Das unformatierte Markdown zeigt die Metadaten-Block, die gerenderte Ansicht jedoch nicht.)

Beim Erstellen einer markdowndatei sollten Sie diese Vorlage in eine neue Datei kopieren, füllen Sie die Metadaten wie unten festgelegten die H1-Überschrift oben auf den Titel des Artikels und löschen Sie den Inhalt. Alle Elemente in die OBERGRENZEN in eckigen Klammern erfordert Ihre Aufmerksamkeit.


## <a name="metadata"></a>Metadaten 

Der vollständige metadatenblock ist oben. Wichtige Hinweise:

- Sie **müssen** ein Leerzeichen zwischen dem Doppelpunkt (:)) und der Wert für ein Metadatenelement einfügen.
- Doppelpunkte in einem Wert (z.B. einem Titel) unterbrechen den metadatenparser. Verwenden Sie an ihre Stelle die HTML-Codierung für einen Doppelpunkt von `&#58;` (z. B. `"title: Azure Rights Management&#58; the basics | Azure RMS"`).
- **title**: Dieser Titel wird in suchmaschinenergebnissen angezeigt. 
- **author**: Das Feld "Autor" muss enthalten der **GitHub-Benutzernamen** des Autors, nicht seinen Alias.
- **ms.prod**, **ms.technology**: Verwenden Sie "Windows-Server-Threshold" ms.prod (oder w10, wenn Sie diese Vorlage zum Erstellen von Inhalt für Windows 10 verwenden). Wenden Sie sich an Ihre CX wenden Sie sich an den ms.technology-Wert abgerufen werden soll.

## <a name="basic-markdown-gfm-and-special-characters"></a>Grundlegendes Markdown, GFM und Sonderzeichen

Alle basic "und" GitHub-flavored Markdown wird unterstützt. Weitere Informationen dazu finden Sie unter:

- [Grundlegende markdownsyntax](https://daringfireball.net/projects/markdown/syntax)
- [Dokumentation zu GitHub-flavored Markdown (GFM)](https://guides.github.com/features/mastering-markdown)

Markdown verwendet Sonderzeichen wie z. B. \*, \`, und \# für die Formatierung. Wenn Sie eines dieser Zeichen in Ihren Inhalt einschließen möchten, müssen Sie einen der folgenden Schritte ausführen:

- Fügen einen umgekehrten Schrägstrich vor das Sonderzeichen "es" Escapezeichen (z. B. \\ \* für eine \*)
- Verwenden der [HTML-Entitätscode](http://www.ascii.cl/htmlcodes.htm) nach dem Zeichen (z. B. \& \#42\; für eine &#42;).

## <a name="headings"></a>Spaltenüberschriften

Überschriften sollten erfolgen Atx-Stils, d. h. verwenden 1-6 Hash-Zeichen (#) am Anfang der Zeile um eine Überschrift, die für HTML-Überschriftenebenen H1 bis H6 anzugeben. Beispiele für die Header der ersten und zweiten Ebene werden oben verwendet. 

Es **müssen** werden nur eine Überschrift der ersten Ebene (H1) in Ihrem Thema, die als Titel auf der Seite angezeigt wird.  

Überschriften der zweiten Ebene generiert das Inhaltsverzeichnis auf der Seite, die im Abschnitt "In diesem Artikel" unterhalb des Titels auf der Seite angezeigt wird.

### <a name="third-level-heading"></a>Überschrift der dritten Ebene
#### <a name="fourth-level-heading"></a>Überschrift der vierten Ebene
##### <a name="fifth-level-heading"></a>Überschrift der fünften Ebene
###### <a name="sixth-level-heading"></a>Überschrift der sechsten Ebene

## <a name="text-styling"></a>Textformat

*Kursiv* 

**Fett** 

~~Strikethrough~~

## <a name="links"></a>Links

### <a name="internal-links"></a>Interne Links

Um auf einen Header in der gleichen markdowndatei zu verlinken, zeigen Sie die Quelle des veröffentlichten Artikels, suchen Sie die ID des Anfangswerts (z. B. `id="blockquote"`), und Verknüpfen mit # + Id (z. B. `#blockquote`).

- Beispiel: [Blockquotes](#blockquote)

Verwenden Sie zum Verknüpfen mit einer markdowndatei im gleichen Repository [relative Links](https://www.w3.org/TR/WD-html40-970917/htmlweb.html#h-5.1.2), einschließlich ".md" am Ende des Dateinamens.

- Beispiel: [Tipps und Probleme](tips-gotchas.md)
- Beispiel: [Tools und Setup für Mitwirkende](../readme.md)

Um auf einen Header in einer markdowndatei im gleichen Repository zu verlinken, verwenden Sie relative Verknüpfung + hashtagverknüpfung.

- Beispiel: [Löschen von Dateien](tips-gotchas.md#deleting-files)

### <a name="external-links"></a>Externe Links

Verwenden Sie zum Verknüpfen mit einer externen Datei die vollständige URL als Link.

- Beispiel: [GitHub](http://www.github.com)

Wenn eine URL in einer markdowndatei angezeigt wird, wird sie in einen klickbaren Link umgewandelt werden.

- Beispiel: http://www.github.com

## <a name="lists"></a>Listen

### <a name="ordered-lists"></a>Sortierte Listen

1. Diese 
1. Is
1. Eine
1. Sortiert
1. List  


#### <a name="ordered-list-with-an-embedded-list"></a>Sortierte Liste mit einer eingebetteten Liste

1. Hier
1. stammt
1. Ein
1. Eingebettete
    1. Fehler leicht
    1. Professor Plum
1. Sortiert
1. list


### <a name="unordered-lists"></a>Unsortierte Listen

- Diese
- auf
- a
- Liste mit Aufzählungszeichen
- list


##### <a name="unordered-list-with-an-embedded-list"></a>Unsortierte Liste mit einer eingebetteten Liste

- Diese 
- Liste mit Aufzählungszeichen 
- list
    - Mrs Peacock
    - Mr. grün
- Enthält  
- andere
    1. Colonel Senf
    1. Mrs-Whitepaper
- Listen


## <a name="horizontal-rule"></a>Horizontale Trennlinie

---

## <a name="tables"></a>Tabellen

Verwenden Sie in fast jeder Instanz MD, die Formatierung für Tabellen. Während die HTML-Tabellen für mehr Flexibilität sorgen verwenden wir nicht sie in unserer Inhalte. Wenn Sie eine HTML-Tabelle in Ihrem Artikel verfügen, werden wir diesen Artikel nicht zusammen.

| Tabellen        | sind           | Cool  |
| ------------- |:-------------:| -----:|
| SP 3 ist      | Rechtsbündig | $1600 |
| SP 2 ist      | Zentriert      |   12 USD |
| SP 1 ist standardmäßig | Linksbündig     |    $1 |


## <a name="code"></a>Code

### <a name="generic-codeblock"></a>Generischer codeblock

Einrücken von Code vier Leerzeichen für die Codierung generischer Codeblock.

    function fancyAlert(arg) {
      if(arg) {
        $.docs({div:'#foo'})
      }
    }


### <a name="codeblocks-with-language-identifier"></a>Codeblocks mit Sprachen-ID

Verwenden Sie drei Graviszeichen (&#96;&#96;&#96;) + eine Sprachen-ID, um sprachenspezifische gelten für einen Codeblock zu codieren.  Hier ist die gesamte Liste der [GitHub Flavored Markdown (GFM) Sprachen-IDs](https://github.com/jmm/gfm-lang-ids/wiki/GitHub-Flavored-Markdown-(GFM)-language-IDs).

##### <a name="c9839"></a>C&#9839;

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

Verwenden Sie Graviszeichen (&#96;) für `inline code`.

## <a name="blockquotes"></a>Blockquotes

> Die Trockenheit hatte nun zehn Millionen Jahre, und die Herrschaft der schrecklichen echsen hatte längst geendet. Hier am Äquator, in dem Kontinent, der eines Tages Afrika, existenzkampf Miete Vorhandensein hatte einen neuen Gipfel der grausamkeit, und der Sieger war noch nicht im Blick. In diesem trostlosen und verdorrten Land konnte nur geringe oder der schnelle oder der wilde Gedeihen oder sogar zu Überleben hoffen.

## <a name="images"></a>Abbilder

### <a name="static-image"></a>Statisches Bild

![Dies ist der alternative Text.](../windowsserverdocs/get-started/media/wsbanner.png)

### <a name="linked-image"></a>Verknüpftes Bild

[![Alternativer Text für verknüpftes Bild](../windowsserverdocs/get-started/nano.png)](../windowsserverdocs/get-started/getting-started-with-nano-server.md) 

## <a name="alerts"></a>Benachrichtigungen

### <a name="note"></a>Hinweis

> [!NOTE]
> Dies ist ein Hinweis

### <a name="warning"></a>Warnung

> [!WARNING]
> Dies ist eine Warnung

### <a name="tip"></a>Tipp

> [!TIP]
> Dies ist ein Tipp

### <a name="important"></a>Wichtig

> [!IMPORTANT]
> Das ist wichtig

