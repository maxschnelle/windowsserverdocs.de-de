---
title: Patchen von Server Core
description: Hier erfahren Sie, wie Sie Server Core-Installationsoption von Windows Server aktualisieren
ms.prod: windows-server-threshold
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 10/17/2017
ms.openlocfilehash: f51ffae5ed8f91cca386eb209e7a1d8cc664ceeb
ms.sourcegitcommit: 1533d994a6ddea54ac189ceb316b7d3c074307db
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/01/2018
ms.locfileid: "1448056"
---
# <a name="patch-a-server-core-installation"></a>Patch einer Server Core-installation

> Betrifft: WindowsServer (Semikolons jährlichen Channel) und WindowsServer 2016

Sie können einen Server mit der Server Core-Installation auf folgende Weise patch:

- **Mithilfe von Windows Update automatisch oder mit Windows Server Update Services (WSUS)**. Mithilfe von Windows Update, können Sie entweder automatisch oder mit Befehlszeilentools oder Windows Server Update Services (WSUS)-Servern mit einer Server Core-Installation service.

- **Manuell**. Auch in Organisationen, die Windows Update oder WSUS nicht verwenden, können Sie Updates manuell anwenden.

## <a name="view-the-updates-installed-on-your-server-core-server"></a>Zeigen Sie die Updates installiert sind, auf dem Server Core-Server an
Bevor Sie ein neues Update Server Core hinzufügen, ist es ratsam, finden Sie unter welche Updates bereits installiert wurden.

Wenn Updates mithilfe von Windows PowerShell anzeigen möchten, führen Sie **Get-Hotfix**aus.

Führen Sie zum Anzeigen von Updates durch Ausführen eines Befehls, **systeminfo.exe**. Es könnten eine kurze Verzögerung, während das Tool auf Ihrem System untersucht.

Sie können auch **Wmic Qfe Liste** über die Befehlszeile ausführen. 

## <a name="patch-server-core-automatically-with-windows-update"></a>Patch Server Core automatisch mit Windows Update

Verwenden Sie die folgenden Schritte auf den Server mit Windows Update automatisch patch:

1. Überprüfen Sie die aktuelle Einstellung der Windows-Updates:
   ```
   %systemroot%\system32\Cscript scregedit.wsf /AU /v 
   ```

2. So aktivieren Sie automatische Updates:

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 4 
   Net start wuauserv
   ```  

3. Um automatische Updates zu deaktivieren, führen Sie Folgendes aus:

   ```
   Net stop wuauserv 
   %systemroot%\system32\Cscript scregedit.wsf /AU 1 
   Net start wuauserv 
   ```

Wenn der Server Mitglied einer Domäne ist, können Sie auch Windows Update mithilfe von Gruppenrichtlinien konfigurieren. Weitere Informationen finden Sie unter https://go.microsoft.com/fwlink/?LinkId=192470. Wenn Sie diese Methode verwenden, ist jedoch nur die Option 4 ("Automatische Download und Zeitplan für die Installation") für Server Core-Installationen von Bedeutung Mangels einer Benutzeroberfläche. Für größere Kontrolle über die Updates installiert sind, und wenn Sie ein Skript, das ein Command-Line-Äquivalent für die meisten der Benutzeroberfläche Windows Update bietet verwenden können. Informationen über das Skript finden Sie unter https://go.microsoft.com/fwlink/?LinkId=192471.

Wenn Sie um Windows Update sofort erkennen und installieren alle verfügbaren Updates zu erzwingen, führen Sie den folgenden Befehl ein:

```
Wuauclt /detectnow 
```

Abhängig von den Updates, die installiert sind, müssen Sie einen Neustart des Computers, obwohl das System nicht dieses benachrichtigt wird. Verwenden Sie Task-Manager, um festzustellen, ob der Installationsvorgang abgeschlossen ist, um sicherzustellen, dass die Prozesse **Wuauclt** oder **Trusted Installer** nicht aktiv ausgeführt werden. Sie können auch die Methoden in der [Ansicht, die die Updates auf dem Server Core-Server installiert](#view-the-updates-installed-on-your-Server-Core-server) verwenden, um die Liste der installierten Updates zu überprüfen.

## <a name="patch-the-server-with-wsus"></a>Patchen Sie den Server mit WSUS 

Wenn der Server Core-Server ein Mitglied einer Domäne ist, können Sie die Verwendung der WSUS-Server mithilfe von Gruppenrichtlinien konfigurieren. Weitere Informationen Laden Sie die [Gruppenrichtlinien-Referenzinformationen](https://www.microsoft.com/download/details.aspx?id=25250). Sie können auch [Konfigurieren von Gruppenrichtlinieneinstellungen für automatische Updates](../windows-server-update-services/deploy/4-configure-group-policy-settings-for-automatic-updates.md) überprüfen.

## <a name="patch-the-server-manually"></a>Patchen Sie den Server manuell

Laden Sie das Update, und stellen Sie die Server Core-Installation zur Verfügung zu.
Führen Sie an einer Eingabeaufforderung den folgenden Befehl ein:

```
Wusa <update>.msu /quiet 
```

Abhängig von den Updates, die installiert sind, müssen Sie einen Neustart des Computers, obwohl das System nicht dieses benachrichtigt wird.

Um ein Update manuell zu deinstallieren, führen Sie den folgenden Befehl aus:

```
Wusa /uninstall <update>.msu /quiet 
```

