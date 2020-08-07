---
title: Patchen von Server Core
description: Erfahren Sie, wie Sie eine Server Core-Installation von Windows Server aktualisieren.
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: eb444dd05359f033bec8b45aa9ed53a6ed5096c6
ms.sourcegitcommit: 53d526bfeddb89d28af44210a23ba417f6ce0ecf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/06/2020
ms.locfileid: "87895854"
---
# <a name="patch-a-server-core-installation"></a>Patchen einer Server Core-Installation

> Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Sie können einen Server, auf dem die Server Core-Installation ausgeführt wird, wie folgt Patchen:

- **Automatisches Verwenden von Windows Update oder mit Windows Server Update Services (WSUS)**. Wenn Sie Windows Update entweder automatisch oder mit Befehlszeilen Tools oder Windows Server Update Services (WSUS) verwenden, können Sie Server verwenden, auf denen eine Server Core-Installation ausgeführt wird.

- **Manuell**. Auch in Organisationen, in denen Windows Update oder WSUS nicht verwendet wird, können Sie Updates manuell anwenden.

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Anzeigen der auf dem Server-Core-Server installierten Updates
Bevor Sie ein neues Update zu Server Core hinzufügen, empfiehlt es sich, zu sehen, welche Updates bereits installiert wurden.

Wenn Sie Updates mithilfe von Windows PowerShell anzeigen möchten, führen **Sie Get-Hotfix**aus.

Führen Sie **systeminfo.exe**aus, um Updates durch Ausführen eines Befehls anzuzeigen. Möglicherweise kommt es zu einer kurzen Verzögerung, während das Tool das System prüft.

Sie können auch die **WMIC-QFE-Liste** über die Befehlszeile ausführen.

## <a name="patch-server-core-automatically-with-windows-update"></a>Automatisches Patchen von Server Core mit Windows Update

Führen Sie die folgenden Schritte aus, um den Server automatisch mit Windows Update zu patchen:

1. Überprüfen Sie die aktuelle Windows Update Einstellung:
   ```
   %systemroot%\system32\Cscript %systemroot%\system32\scregedit.wsf /AU /v
   ```

2. So aktivieren Sie automatische Updates:

   ```
   Net stop wuauserv
   %systemroot%\system32\Cscript %systemroot%\system32\scregedit.wsf /AU 4
   Net start wuauserv
   ```

3. Führen Sie Folgendes aus, um automatische Updates zu deaktivieren:

   ```
   Net stop wuauserv
   %systemroot%\system32\Cscript %systemroot%\system32\scregedit.wsf /AU 1
   Net start wuauserv
   ```

Wenn der Server Mitglied einer Domäne ist, können Sie Windows Update auch mithilfe einer Gruppenrichtlinie konfigurieren. Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=192470. Wenn Sie diese Methode verwenden, ist jedoch nur Option 4 ("Automatisches herunterladen und Planen der Installation") für Server Core-Installationen relevant, weil keine grafische Oberfläche verfügbar ist. Um besser steuern zu können, welche Updates zu welchem Zeitpunkt installiert werden, können Sie ein Skript verwenden. Das Skript stellt ein Befehlszeilenäquivalent der meisten Optionen der grafischen Windows Update-Benutzeroberfläche dar. Weitere Informationen zum Skript finden Sie unter https://go.microsoft.com/fwlink/?LinkId=192471 .

Führen Sie den folgenden Befehl aus, um zu erzwingen, dass Windows Update alle verfügbaren Updates sofort erkennt und installiert:

```
Wuauclt /detectnow
```

Je nach den installierten Updates kann es sein, dass Sie den Computer neu starten müssen, auch wenn vom System keine entsprechende Meldung angezeigt wird. Um zu ermitteln, ob der Installationsvorgang abgeschlossen ist, verwenden Sie den Task-Manager, um zu überprüfen, ob die Prozesse **wuauclt** oder **vertrauenswürdiger Installer** nicht aktiv ausgeführt werden. Sie können auch die Methoden in [Anzeigen der auf dem Server-Core-Server installierten Updates](#view-the-updates-installed-on-your-server-core-server) verwenden, um die Liste der installierten Updates zu überprüfen.

## <a name="patch-the-server-with-wsus"></a>Patchen des Servers mit WSUS

Wenn der Server Core-Server Mitglied einer Domäne ist, können Sie diesen mithilfe einer Gruppenrichtlinie für die Verwendung eines WSUS-Servers konfigurieren. Weitere Informationen finden Sie unter [Gruppenrichtlinie Referenzinformationen](https://www.microsoft.com/download/details.aspx?id=25250). Weitere Informationen finden Sie auch unter [Konfigurieren von Gruppenrichtlinie Einstellungen für automatische Updates](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md)

## <a name="patch-the-server-manually"></a>Manuelles Patchen des Servers

Laden Sie das Update herunter, und stellen Sie es für die Server Core-Installation zur Verfügung.
Führen Sie an der Eingabeaufforderung folgenden Befehl aus:

```
Wusa <update>.msu /quiet
```

Je nach den installierten Updates kann es sein, dass Sie den Computer neu starten müssen, auch wenn vom System keine entsprechende Meldung angezeigt wird.

Um ein Update manuell zu deinstallieren, führen Sie den folgenden Befehl aus:

```
Wusa /uninstall <update>.msu /quiet
```

