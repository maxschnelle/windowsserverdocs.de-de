---
title: Automatisches Installieren von Add-Ins während des Setups
description: Beschreibt, wie Windows Server Essentials
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
ms.openlocfilehash: c2345726a17a074fc7022c8c4dc9b2443e9ad384
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66433644"
---
# <a name="automate-installation-of-add-ins-during-setup"></a>Automatisches Installieren von Add-Ins während des Setups

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

##  <a name="BKMK_AddIns"></a> Installieren von Add-Ins während des Setups zu automatisieren.  
 Verwenden Sie zum Installieren von Add-Ins während des Setups die Methode „PostIC.cmd“, die im Abschnitt [Create the PostIC.cmd File for Running Post Initial Configuration Tasks](Create-the-PostIC.cmd-File-for-Running-Post-Initial-Configuration-Tasks.md) dieses Dokuments beschrieben wird.  
  
 Fügen Sie der Datei "PostIC.cmd" den folgenden Eintrag hinzu:  
  
```  
C:\Program Files\Windows Server\bin\Installaddin.exe <full path to wssx file> -q  
```  
  
 Das Add-In unterstützt jetzt Schritte zur Vorinstallation und angepasste Schritte zur Deinstallation.  
  
 Der Schritt zur Vorinstallation wird ausgeführt, bevor sämtliche Dateien des Typs **.msi** ausgeführt werden, die in der Datei "addin.xml" angegeben werden. Bei Ausführung im interaktiven Modus wird das Statusdialogfeld angezeigt, allerdings ohne Änderungen des Status. Die Schaltfläche zum Abbrechen ist während der Vorinstallationsphase deaktiviert. Wenn Sie einen Schritt zur Vorinstallation implementieren möchten, fügen Sie der Datei "addin.xml" die folgenden Inhalte hinzu (direkt unterhalb von "Paket"):  
  
> [!NOTE]
>  Das XML-Schema muss genau dem folgenden Schema entsprechen:  
  
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
  
 **exefile** stellt die ausführbare Datei im Add-In-Paket für die Ausführung des Schritts zur Vorinstallation dar und muss angegeben werden. **NormalArgs** gibt Argumente an, die an exefile in der Befehlszeile zu übergeben sind, wenn der interaktive Modus verwendet wird. In diesem Modus können von exefile einige Dialogfelder für Benutzereingriffe eingeblendet werden. **SilentArgs** gibt Argumente an, die an exefile in der Befehlszeile zu übergeben sind, wenn der unbeaufsichtigte Modus verwendet wird (beim Aufrufen der Datei "installaddin.exe" wird "-q" angegeben). In diesem Modus sollten von exefile keine Fenster eingeblendet werden. Wenn für **IgnoreExitCode** der Wert "True" angegeben wird, wird der Schritt zur Vorinstallation immer als erfolgreich betrachtet. Andernfalls zeigt der Beendigungscode "0" die erfolgreiche Ausführung an, der Beendigungscode "1" zeigt einen Abbruch an, und weitere Werte zeigen einen Fehler an. Die Tags **NormalArgs**, **SilentArgs** und **IgnoreExitCode** sind optional.  
  
 Ein angepasster Schritt zur Deinstallation kann für die folgenden Zwecke verwendet werden:  
  
- Ersetzen des integrierten Bestätigungsdialogfeldes  
  
- Ausfüllen von angepassten Dialogfeldern vor der Deinstallation  
  
- Ausführen von bestimmten Aufgaben vor der Deinstallation  
  
  Wenn Sie einen Schritt zur Deinstallation implementieren möchten, fügen Sie der Datei "addin.xml" die folgenden Inhalte hinzu (direkt unterhalb von "Package"):  
  
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
  
 Dabei wird mit **full-path-to-exefile** die bereits auf dem System installierte exefile angegeben. **Arguments** ist optional. Damit werden die Befehlszeilenargumente für exefile angegeben. Der Aufruf von exefile erfolgt, bevor das integrierte Bestätigungsdialogfeld für die Deinstallation eingeblendet wird.  
  
 In dieser Phase können die folgenden Tasks durch exefile ausgeführt werden:  
  
- Einblenden bestimmter Dialogfelder für Benutzereingriffe  
  
- Ausführen bestimmter Hintergrundaufgaben  
  
  Durch den Beendigungscode dieser ausführbaren Datei wird der weitere Deinstallationsprozess festgelegt:  
  
- 0: Der Deinstallationsprozess wird ohne Ausfüllen des integrierten Bestätigungsdialogfeldes so fortgesetzt, als ob der Benutzer bereits bestätigt hätte. (Dieser Ansatz kann zum Ersetzen des integrierten Bestätigungsdialogfeldes verwendet werden.)  
  
- 1: Der Deinstallationsprozess wird abgebrochen, und dem Benutzer wird zum Abschluss eine Abbruchnachricht angezeigt. Es werden keine Änderungen durchgeführt.  
  
- Weitere: Der Deinstallationsprozess wird mit dem integrierten Bestätigungsdialogfeld so fortgesetzt, als ob der angepasste Schritt zur Deinstallation nicht vorhanden wäre.  
  
  Alle Fehler, bei denen die exefile aufgerufen wird, führen zu demselben Verhalten wie bei der Rückgabe eines anderen Codes als "0" oder "1" der exefile.  
  
## <a name="see-also"></a>Siehe auch  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Zusätzliche Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)