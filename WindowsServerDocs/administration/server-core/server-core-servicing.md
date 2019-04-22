---
title: Patchen von Server Core
description: Informationen Sie zum Aktualisieren von einer Server Core-Installations von Windows Server
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: f51ffae5ed8f91cca386eb209e7a1d8cc664ceeb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59817351"
---
# <a name="patch-a-server-core-installation"></a>Patch für eine Server Core-installation

> Gilt für: WindowsServer (Halbjährlicher Kanal) und WindowsServer 2016

Sie können einen Server unter Server Core-Installation gibt folgende Möglichkeiten Patchen:

- **Verwenden von Windows Update, automatisch oder mit Windows Server Update Services (WSUS)**. Mithilfe von Windows Update, können entweder automatisch oder mit Befehlszeilentools und Windows Server Update Services (WSUS), Sie Server mit einer Server Core-Installation warten.

- **Manuell**. Auch in Organisationen, die nicht Windows Update oder WSUS verwenden, können Sie Updates manuell anwenden.

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Zeigen Sie die auf Ihrem Server Core-Server installierte Updates an
Bevor Sie ein neues Update von Server Core hinzufügen, ist es eine gute Idee, um festzustellen, welche Updates bereits installiert wurden.

Führen Sie zum Anzeigen Updates mithilfe von Windows PowerShell **Get-Hotfix**.

Um Updates anzuzeigen, indem Sie einen Befehl ausführen, führen Sie **systeminfo.exe**. Es gibt möglicherweise eine kurze Verzögerung während des Tools auf Ihrem System überprüft.

Sie können auch ausführen **Wmic-Qfe-Liste** über die Befehlszeile. 

## <a name="patch-server-core-automatically-with-windows-update"></a>Patch für Server Core automatisch mit Windows Update

Verwenden Sie die folgenden Schritte aus, um den patch für des Servers mit Windows Update automatisch:

1. Überprüfen Sie die aktuelle Einstellung für die Windows Update aus:
   ```
   %systemroot%\system32\Cscript scregedit.wsf /AU /v 
   ```

2. So aktivieren Sie automatische Updates:

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 4 
   Net start wuauserv
   ```  

3. Führen Sie zum Deaktivieren von automatischen Updates:

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 1 
   Net start wuauserv 
   ```

Wenn der Server Mitglied einer Domäne ist, können Sie Windows Update auch mithilfe einer Gruppenrichtlinie konfigurieren. Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=192470. Wenn Sie diese Methode verwenden, ist jedoch nur Option 4 ("Autom. herunterladen und laut Zeitplan installieren") für Server Core-Installationen relevant aufgrund des Mangels an eine grafische Benutzeroberfläche. Um besser steuern zu können, welche Updates zu welchem Zeitpunkt installiert werden, können Sie ein Skript verwenden. Das Skript stellt ein Befehlszeilenäquivalent der meisten Optionen der grafischen Windows Update-Benutzeroberfläche dar. Informationen zum Skript finden Sie unter https://go.microsoft.com/fwlink/?LinkId=192471.

Führen Sie den folgenden Befehl aus, um zu erzwingen, dass Windows Update alle verfügbaren Updates sofort erkennt und installiert:

```
Wuauclt /detectnow 
```

Je nach den installierten Updates kann es sein, dass Sie den Computer neu starten müssen, auch wenn vom System keine entsprechende Meldung angezeigt wird. Um zu bestimmen, ob der Installationsvorgang abgeschlossen ist, verwenden Sie Task-Manager zu überprüfen, ob die **Wuauclt** oder **vertrauenswürdiger Installer** -Prozess nicht aktiv ausgeführt wird. Sie können auch die Methoden in [die auf Ihrem Server Core-Server installierte Updates anzeigen](#view-the-updates-installed-on-your-Server-Core-server) um die Liste der installierten Updates zu überprüfen.

## <a name="patch-the-server-with-wsus"></a>Patch für den Server mit WSUS 

Wenn der Server Core-Server Mitglied einer Domäne ist, können Sie diesen mithilfe einer Gruppenrichtlinie für die Verwendung eines WSUS-Servers konfigurieren. Weitere Informationen, die [Referenzinformationen für die Gruppenrichtlinie](https://www.microsoft.com/download/details.aspx?id=25250). Sie können auch überprüfen [Gruppenrichtlinieneinstellungen für automatische Updates konfigurieren](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md)

## <a name="patch-the-server-manually"></a>Patch für den Server manuell

Das Update herunterladen und macht sie für die Server Core-Installation verfügbar.
Führen Sie an einer Eingabeaufforderung den folgenden Befehl ein:

```
Wusa <update>.msu /quiet 
```

Je nach den installierten Updates kann es sein, dass Sie den Computer neu starten müssen, auch wenn vom System keine entsprechende Meldung angezeigt wird.

Um ein Update manuell zu deinstallieren, führen Sie den folgenden Befehl aus:

```
Wusa /uninstall <update>.msu /quiet 
```

