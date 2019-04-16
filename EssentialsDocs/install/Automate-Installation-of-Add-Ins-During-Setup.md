---
title: "Automatisches Installieren von Add-Ins während des Setups"
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 2e6ff6e4-8d68-4d49-9e38-8088bc8bf95e
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: d4c547c2fec8e2b11e5c1d9bde46e55e91c9d6fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="automate-installation-of-add-ins-during-setup"></a>Automatisches Installieren von Add-Ins während des Setups

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

##  <a name="BKMK_AddIns"></a>Installieren von Add-Ins während des Setups zu automatisieren.  
 Verwenden Sie zum Installieren von Add-Ins während des Setups die Methode "postic.cmd" beschrieben, die der [Erstellen der Datei "postic.cmd" Running Post Initial Configuration Tasks](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) Abschnitt dieses Dokuments.  
  
 Fügen Sie die folgenden Eintrag in der Datei "postic.cmd":  
  
```  
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q  
```  
  
 Das Add-in unterstützt jetzt Schritte der Vorinstallation und angepasste deinstallieren.  
  
 Der Schritt ausgeführt wird, bevor sämtliche **MSI** AddIn.xml angegebenen Dateien. Wenn im interaktiven Modus ausführen, wird das Statusdialogfeld angezeigt, allerdings ohne Änderungen des Status sein. Die Schaltfläche zum Abbrechen ist während der Vorinstallationsphase deaktiviert. Um einen Vorinstallationsschritt zu implementieren, fügen Sie die folgenden Inhalte AddIn.XML (direkt unterhalb von Paket):  
  
> [!NOTE]
>  Das XML-Schema muss genau ein:  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>  
<Executable>exefile</Executable>  
<NormalArgs>args-for-interactive-mode</NormalArgs>  
<SilentArgs>args-for-silent-mode</SilentArgs>  
<IgnoreExitCode>true</IgnoreExitCode>  
  </Preinstall>  
  <UninstallConfirm>...</UninstallConfirm>      
</Package>  
<¦>  
<¦>  
```  
  
 Dabei wird **Exefile** ist die ausführbare Datei im Add-in-Paket, die vor der Installation Schritt auszuführen, und muss angegeben werden. **NormalArgs** gibt Argumente an, die an Exefile in der Befehlszeile, wenn der interaktive Modus übergeben werden verwendet wird. In diesem Modus können von Exefile einige Dialogfelder für Benutzereingriffe. **SilentArgs** gibt Argumente an, die an Exefile in der Befehlszeile, wenn der unbeaufsichtigte Modus übergeben werden verwendet wird (-Q wird beim Aufrufen von installaddin.exe angegeben). Sollten von Exefile keine Fenster in diesem Modus. Wenn **IgnoreExitCode** der Schritt wird immer als erfolgreich betrachtet, andernfalls Exitcode 0 gibt Erfolg, 1 zeigt einen Abbruch und andere Werte zeigen einen Fehler mit "Wahr" zurückgegeben, angegeben ist. Tags **NormalArgs**, **SilentArgs**, und **IgnoreExitCode** sind optional.  
  
 Ein angepasste Schritt zur Deinstallation kann für Folgendes verwendet werden:  
  
-   Ersetzen des integrierten bestätigungsdialogfeldes.  
  
-   Ausfüllen von angepassten Dialogfeldern vor der Deinstallation.  
  
-   Aufgaben Sie bestimmte vor der Deinstallation.  
  
 Um einen Schritt zur Deinstallation implementieren möchten, fügen Sie die folgenden Inhalte AddIn.XML (direkt unterhalb von Paket):  
  
```  
<Package xmlns="https://schemas.microsoft.com/WindowsServerSolutions/2010/03/Addins" xmlns:i="http://www.w3.org/2001/XMLSchema-instance">  
  <Id>...</Id>  
  <Version>...</Version>  
  <Name>...</Name>  
  <Allow32BitOn64BitClients>...</Allow32BitOn64BitClients>  
  <ServerBinary>...</ServerBinary>  
  <ClientBinary32>...</ClientBinary32>  
  <ClientBinary64>...</ClientBinary64>  
  <SupportedSkus>...</SupportUrl>    
  <SupportUrl>...</SupportUrl>  
  <Location>...</Location>    
  <PrivacyStatement>...</PrivacyStatement>  
  <OtherBinaries>...</OtherBinaries>   
  <Preinstall>¦</Preinstall>  
<UninstallConfirm>  
<Executable>full-path-to-exefile</Executable>  
<Arguments>command-line-arguments</Arguments>  
</UninstallConfirm>  
</Package>  
```  
  
 Dabei wird **Full-Path-to-Exefile** bereits auf dem System installierte Exefile angegeben. **Argumente** ist optional und gibt die Befehlszeilenargumente für Exefile. Exefile aufgerufen wird, bevor das integrierte deinstallieren Bestätigung Dialogfeld angezeigt wird.  
  
 Exefile kann folgende Aufgaben in dieser Phase durchführen:  
  
-   Einige Dialogfelder für Benutzereingriffe wird angezeigt.  
  
-   Führen Sie bestimmter Hintergrundaufgaben aus.  
  
 Der Exitcode des diese Exe-Datei wird bestimmt, wie die Deinstallation nach vorne verschoben wird:  
  
-   0: der Deinstallationsprozess wird ohne Ausfüllen des integrierten bestätigungsdialogfeldes, fortgesetzt, wie Benutzer bereits bestätigt hat. (dieser Ansatz kann verwendet werden, zum Ersetzen des integrierten bestätigungsdialogfeldes).  
  
-   1: der Deinstallationsprozess wird abgebrochen, und schließlich eine abbruchnachricht für Benutzer angezeigt werden. Durchgeführt.  
  
-   Sonstiges: der Deinstallationsprozess fort integrierte Bestätigungsdialogfeld, wie der angepasste Schritt zur Deinstallation nicht vorhanden ist.  
  
 Jeder Fehler, auf denen die EXEFile aufgerufen führt zu demselben Verhalten wie die EXE-Datei ein anderen Codes als 0 oder 1 zurückgibt.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)