<properties title="" pageTitle="Die Namen und Speicherorte für die technische Artikel zu Windows Server 2016" description="Erläutert die Dateistruktur für den Artikel und die Benennungskonventionen, die Sie befolgen sollten, wenn Sie einen neuen Artikel erstellen." metaKeywords="" services="" solutions="" documentationCenter="" authors="Kathy-Davies" videoId="" scriptId="" manager="required" />

<tags ms.service="contributor-guide" ms.devlang="" ms.topic="article" ms.tgt_pltfrm="" ms.workload="" ms.date="03/14/2016" ms.author="jimpark; tysonn" />

# <a name="file-names-and-locations-for-windows-server-technical-articles"></a>Die Namen und Speicherorte für Windows Server – Technische Artikel

Zu wissen, und gemäß den Regeln können Sie die Ihren Pull Request akzeptiert schneller abrufen.

+ [Regeln]
+ [Muster]
+ [Genehmigung für Datei-name]

## <a name="rules"></a>Regeln

- Alle Dateien müssen in Markdown und die Dateierweiterung .md verwenden.
- Halten Sie den Dateinamen nach Möglichkeit auf 3 bis 5 Wörter – 10 Wörter ist zu lang für die Lesbarkeit und SEO.
- Verwenden Sie Kleinbuchstaben und nur Buchstaben, Zahlen und Bindestriche enthalten.
- Keine leer- oder Interpunktionszeichen. Verwenden Sie zum Trennen von Wörtern und Zahlen im Dateinamen einen Bindestrich.
- Verwenden Sie nicht die Kurzform von Verben, die "-Ing" Formular: `deploy-nano-server` nicht `Deploying-Nano-Server`
- Lassen Sie Wörter, z. B. ein, und, die in oder.
- Rechtschreibung von Wörtern, Vermeiden Sie nicht genehmigte oder nicht benötigten Akronyme in Dateinamen
- Dateinamen muss eindeutige - anstelle von `overview.md` verwenden `storage-spaces-overview.md`

Akronyme und Abkürzungen, die in Dateinamen - spezifische Richtlinien:

- Führen Sie die vorhandene Microsoft-Sicherheitsleitfaden für zulässigen Namen Abkürzungen
- Industriestandard Abkürzungen werden nach Bedarf in Dateinamen akzeptiert.

## <a name="pattern"></a>Muster

Überprüfen Sie die Liste der Artikel im Repository um eine Vorstellung der vorhandenen Namen erhalten. Hier ist das allgemeine Muster ein:

 **component-topic-title.md**
 
beispielsweise `storage-spaces-direct-overview.md`

## <a name="file-name-approval"></a>Genehmigung für Datei-name

Wenn Sie eine neue Datei übermitteln, werden Pull Request-Prüfer prüfen Sie den Namen und Bereitstellen von Feedback über den Pull Request kommentarstream tippt, wenn Änderungen erforderlich sind. Der Dateiname muss korrigiert werden, bevor der Pull Request akzeptiert wird. Mitwirkende können ganz einfach das Update zu den ausstehenden Pull Request übertragen.

## <a name="folders-in-the-repo"></a>Ordner im Repository

Verwenden Sie die Ordnerstruktur. Erstellen Sie keine Ordner ohne Genehmigung aus einer Repository-Administrator. Wenden Sie sich an sie, wenn Sie glauben, benötigen Sie einen neuen Ordner.

Das GitHub-Repository verfügen über eine einfache und relativ flache Ordnerstruktur – sollten \<Bereich >\\\<Technologie > – für die Beispiel-Storage\data-Deduplizierung. Auf diese Weise bietet folgende Vorteile:
 - Es ist sehr einfach.
 - Es ist näher an der Funktionsweise der Azure.com
 - Es erleichtert es Autoren/PMs schnell finden ihre Themen – nicht erforderlich, um zu untersuchen, mit anderen Ordnern gesucht, in denen eine bestimmte Technologie geschachtelt ist.
 - Er hält die URL, short, handelt es sich gut für SEO und benutzererfahrung, Kunden gelegentlich betrachten Sie die URL für Hinweise.

## <a name="changing-case-in-file-names"></a>Groß-/Kleinschreibung in Dateinamen ändern

Windows-Betriebssystemen wird die Groß-/Kleinschreibung. Wenn Sie einen Dateinamen zur Groß-und Kleinschreibung beheben ändern müssen, ist es besser, eine Änderung an den Inhalt der Datei vornehmen, außer Sie sind auf einem Linux- oder Mac. Zum Beispiel:

  biztalk-administration-and-Development-Task-List-in-BizTalk-Services --> biztalk-services-administration-and-development-task-list

Verwenden der `git mv` Befehl aus, um eine Datei umzubenennen:
```
  git mv <WindowsServerDocs/tech-area/subarea/current-file-name.md> <WindowsServerDocs/tech-area/subarea/new-file-name.md>
```

### <a name="contributors-guide-links"></a>Links im Leitfaden Mitwirkende

- [Index der Artikel mit Hinweisen](./contributor-guide-index.md)


<!--Anchors-->
[Regeln]: #rules
[Muster]: #pattern
[Genehmigung für Datei-name]: #file-name-approval
