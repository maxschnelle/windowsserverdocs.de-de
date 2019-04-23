---
title: 'Befehlszeilentools für den Ressourcen-Manager für Dateiserver:'
description: Dieser Artikel beschreibt die Befehlszeilentools von Windows Server 2016
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 9b31c133b0ee4382b5b9aeded9b3852c7230d2d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858441"
---
# <a name="file-server-resource-manager-command-line-tools"></a>Befehlszeilentools für den Ressourcen-Manager für Dateiserver:

> Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016, Windows Server 2012 R2, WindowsServer 2012, Windows Server 2008 R2

Der Ressourcen-Manager für Dateiserver installiert die [FileServerResourceManager](https://technet.microsoft.com/itpro/powershell/windows/fileserverresourcemanager/fileserverresourcemanager) PowerShell-Cmdlets sowie die folgenden Befehlszeilentools:

-   **Dirquota.exe**. Verwenden Sie den Befehl, um Kontingente, automatisch zugewiesene Kontingente und Kontingentvorlagen zu erstellen und zu verwalten.
-   **Filescrn.exe**. Verwenden Sie den Befehl, um Dateiprüfungen, Dateiprüfungsvorlagen, Dateiprüfungsausnahmen und Dateigruppen zu erstellen und zu verwalten.
-   **Storrept.exe**. Verwenden Sie den Befehl zum Konfigurieren von Berichtsparametern und um Speicherberichte nach Bedarf zu generieren. Verwenden Sie den Befehl ebenfalls, um Berichtsaufgaben zu erstellen, die Sie mithilfe von **schtasks.exe** planen können.

Sie können diese Tools zum Verwalten von Speicherressourcen auf einem lokalen Computer oder einem Remotecomputer verwenden. Weitere Informationen zur Verwendung dieser Befehlszeilentools finden Sie in den folgenden Referenzen:

-   **Dirquota**: <https://go.microsoft.com/fwlink/?LinkId=92741>
-   **Filescrn**: <https://go.microsoft.com/fwlink/?LinkId=92742>
-   **Storrept**: <https://go.microsoft.com/fwlink/?LinkId=92743>


> [!Note]
> Um die Syntax des Befehls und die verfügbaren Parameter für einen Befehl anzuzeigen, führen Sie den Befehl <strong>/?</strong> aus übergeben.


## <a name="remote-management-using-the-command-line-tools"></a>Remoteverwaltung mithilfe der Befehlszeilentools

Jedes Tool verfügt über verschiedene Optionen zum Ausführen von Aktionen, die den verfügbaren Aktionen im Ressourcen-Manager für Dateiserver-MMC-Snap-Ins ähnlich sind. Damit ein Befehl eine Aktion auf einem Remotecomputer anstatt auf dem lokalen Computer ausführt, verwenden Sie den Parameter **/remote**:*ComputerName*.

**Dirquota.exe** enthält beispielsweise einen Parameter **Vorlage exportieren**, um die Einstellungen der Kontingentvorlage in eine XML-Datei zu schreiben, und einen Parameter **Vorlage importieren**, um die Einstellungen einer Vorlagen aus der XML-Datei zu importieren. Das Hinzufügen des Parameters **/remote**:*ComputerName* zu dem Befehl **Dirquota.exe Vorlage importieren** importiert die Vorlagen aus der XML-Datei vom lokalen Computer auf den Remotecomputer.

> [!Note]
> Beim Ausführen der Befehlszeilentools mit dem Parameter **/remote**:<em>ComputerName</em>, um eine Vorlage auf einem Remotecomputer zu exportieren (oder zu importieren), werden die Vorlagen auf eine XML-Datei auf den lokalen Computer geschrieben (oder kopiert) .

<br />

## <a name="additional-considerations"></a>Weitere Aspekte 

So verwalten Sie Remoteressourcen mit den Befehlszeilentools:

-   Sie müssen auf dem lokalen Computer und dem Remotecomputer mit einem Domänenkonto, das Mitglied einer lokalen **Administratoren**gruppe ist, angemeldet sein.
-   Die Befehlszeilentools müssen über eine Eingabeaufforderung mit erhöhten Rechten ausgeführt werden. Klicken Sie zum Öffnen eines Eingabeaufforderungsfensters mit erhöhten Rechten auf **Start**, zeigen Sie auf **Alle Programme**, klicken Sie auf **Zubehör**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie anschließend auf **Als Administrator ausführen**.
-   Auf dem Remotecomputer muss Windows Server ausgeführt werden und der Ressourcen-Manager für Dateiserver muss installiert sein.
-   Die **Remotedateiserver Ressourcen-Manager für Dateiserver**-Ausnahme muss auf dem Remotecomputer aktiviert sein. Aktivieren Sie diese Ausnahme mithilfe von Windows-Firewall in der Systemsteuerung.


## <a name="see-also"></a>Siehe auch

-   [Verwalten von Remote-Speicherressourcen](managing-remote-storage-resources.md)