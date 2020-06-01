---
title: Neuerungen in Windows Server, Version 2004
description: Neue Features in Windows Server, Version 2004
ms.prod: windows-server
ms.technology: server-general
ms.topic: article
author: Heidilohr
ms.author: helohr
ms.date: 05/27/2020
ms.localizationpriority: high
ms.openlocfilehash: e0136dad7180e41f15ae6226008aa7580ec53283
ms.sourcegitcommit: c63672805c93d5bf2a9eb71b3e2de2df00194529
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/28/2020
ms.locfileid: "84124898"
---
# <a name="whats-new-in-windows-server-version-2004"></a>Neuerungen in Windows Server, Version 2004

>Gilt für: Windows Server (Halbjährlicher Kanal)

Weitere Informationen zu den neuesten Features in Windows finden Sie unter [Neuerungen in Windows Server](whats-new-in-windows-server.md). In diesem Thema werden einige der neuen Features in Windows Server, Version 2004, beschrieben.

## <a name="server-core-container-improvements"></a>Server Core-Containerverbesserungen

Wir haben die Gesamtgröße der Server Core-Containerimages reduziert, um Downloadgeschwindigkeiten und -leistung zu verbessern. Folgende Verbesserungen wurden vorgenommen:

- Die meisten NGEN-Images wurden aus dem Server Core-Containerimage entfernt, um die Größe des Images zu verkleinern.
- .NET Framework-Laufzeitimages, die auf Server Core-Containerimages basieren, sind jetzt für ASP.NET-Apps und Windows PowerShell-Skriptleistung optimiert.
- Das .NET-Team hat auch dafür gesorgt, dass es nur eine Kopie jedes NGEN-Bildes gibt, was zu einer geringeren Größe bei den .NET-Framework-Images führt.

Um Ihnen eine bessere Vorstellung von der Größe dieser Container zu geben, vergleicht die folgende Tabelle die aktuelle Version des Containers aus dem [monatlichen Sicherheitsupdate vom Mai 2020](https://support.microsoft.com/help/4561769/windows-server-containers-for-may-2020) (auch als „5B“-Update bezeichnet) mit früheren Versionen.

| Containerversion | Downloadgröße | Größe auf dem Datenträger |
|---|---|---|
| Windows Server, Version 1903 | 2,311 GB | 5,1 GB |
| Windows Server, Version 1909 | 2,257 GB | 4,97 GB |
| Windows Server, Version 2004 | 1,830 GB | 3,98 GB |

Weitere Informationen zum Update von Windows Server, Version 2004, finden Sie in [unserem Blogbeitrag](https://techcommunity.microsoft.com/t5/containers/windows-server-version-2004-now-available/ba-p/1419194). Weitere Informationen zu Windows-Containerupdates im Allgemeinen finden Sie unter [Aktualisieren von Windows Server-Containern](/virtualization/windowscontainers/deploy-containers/update-containers/).
