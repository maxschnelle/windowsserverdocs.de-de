---
title: Datei Server Ressourcen-Manager Befehlszeilen Tools
description: In diesem Artikel werden die Befehlszeilen Tools von Windows Server 2016 beschrieben.
ms.date: 7/7/2017
ms.prod: windows-server
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: 793c9d705cc225de2372d65bf92ce924b498032a
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961542"
---
# <a name="file-server-resource-manager-command-line-tools"></a>Datei Server Ressourcen-Manager Befehlszeilen Tools

> Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2

Datei Server Ressourcen-Manager installiert die PowerShell-Cmdlets [fileserverresourcemanager](/powershell/module/fileserverresourcemanager/?view=win10-ps) und die folgenden Befehlszeilen Tools:

-   **Dirquota.exe**. Verwenden Sie zum Erstellen und Verwalten von Kontingenten, zum automatischen Anwenden von Kontingenten und Kontingent Vorlagen.
-   **Filescrn.exe**. Verwenden Sie, um Datei Bildschirme, Datei Bildschirm Vorlagen, Datei Bildschirm Ausnahmen und Dateigruppen zu erstellen und zu verwalten.
-   **Storrept.exe**. Verwenden Sie, um Berichts Parameter zu konfigurieren und Speicher Berichte bei Bedarf zu generieren. Verwenden Sie außerdem, um Berichts Tasks zu erstellen, die Sie mit **schtasks.exe**planen können.

Sie können diese Tools verwenden, um Speicherressourcen auf einem lokalen Computer oder einem Remote Computer zu verwalten. Weitere Informationen zu diesen Befehlszeilen Tools finden Sie in den folgenden Referenzen:

-   **Dirquota**:<https://go.microsoft.com/fwlink/?LinkId=92741>
-   **Filescrn**:<https://go.microsoft.com/fwlink/?LinkId=92742>
-   **Storrept**:<https://go.microsoft.com/fwlink/?LinkId=92743>


> [!Note]
> Führen Sie den Befehl mit dem <strong>/?-</strong> Befehl aus, um die Befehlssyntax und die verfügbaren Parameter für einen Befehl anzuzeigen. .


## <a name="remote-management-using-the-command-line-tools"></a>Remote Verwaltung mithilfe der Befehlszeilen Tools

Jedes Tool verfügt über mehrere Optionen zum Ausführen von Aktionen, die mit den im Datei Server Ressourcen-Manager MMC-Snap-in verfügbaren Aktionen vergleichbar sind. Wenn ein Befehl eine Aktion auf einem Remote Computer statt auf dem lokalen Computer ausführen soll, verwenden Sie den **/Remote**:*Computername* -Parameter.

**Dirquota.exe** enthält z. b. einen **Vorlagen Export** Parameter, um Kontingent Vorlagen Einstellungen in eine XML-Datei zu schreiben, und einen **Vorlagen Import** Parameter, um Vorlagen Einstellungen aus der XML-Datei zu importieren. Durch Hinzufügen des **/Remote**:*Computername* -Parameters zum Befehl " **Dirquota.exe Template Import** " werden die Vorlagen aus der XML-Datei auf dem lokalen Computer auf den Remote Computer importiert.

> [!Note]
> Wenn Sie die Befehlszeilen Tools mit dem **/Remote**:<em>Computername</em> -Parameter ausführen, um einen Vorlagen Export (oder-Import) auf einem Remote Computer auszuführen, werden die Vorlagen in eine XML-Datei auf den lokalen Computer geschrieben (bzw. aus dieser kopiert).

<br />

## <a name="additional-considerations"></a>Weitere Überlegungen

So verwalten Sie Remote Ressourcen mit den Befehlszeilen Tools

-   Sie müssen mit einem Domänen Konto angemeldet sein, das Mitglied der Gruppe " **Administratoren** " auf dem lokalen Computer und auf dem Remote Computer ist.
-   Sie müssen die Befehlszeilen Tools über ein Eingabe Aufforderungs Fenster mit erhöhten Rechten ausführen. Klicken Sie zum Öffnen eines Eingabeaufforderungsfensters mit erhöhten Rechten auf **Start**, zeigen Sie auf **Alle Programme**, klicken Sie auf **Zubehör**, klicken Sie mit der rechten Maustaste auf **Eingabeaufforderung**, und klicken Sie anschließend auf **Als Administrator ausführen**.
-   Auf dem Remote Computer muss Windows Server ausgeführt werden, und es muss ein Datei Server Ressourcen-Manager installiert sein.
-   Die Ausnahme für den **Remote Datei Server Ressourcen-Manager Verwaltung** auf dem Remote Computer muss aktiviert sein. Aktivieren Sie diese Ausnahme mithilfe der Windows-Firewall in der Systemsteuerung.


## <a name="additional-references"></a>Zusätzliche Referenzen

-   [Verwalten von Remotespeicherressourcen](managing-remote-storage-resources.md)
