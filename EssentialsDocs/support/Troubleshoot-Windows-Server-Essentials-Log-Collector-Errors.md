---
title: Problembehandlung für Fehler mit dem Windows Server Essentials-Protokollsammler
description: Beschreibt, wie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: e92236c8e5d956b50f657ebcbe1a942b5841fded
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836661"
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Problembehandlung für Fehler mit dem Windows Server Essentials-Protokollsammler

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Bei der Ausführung des Log Collectors kann einer der folgenden Fehler auftreten. Um ein Problem zu beheben, befolgen Sie die Anleitungen für den jeweiligen Fehler.  
  
> [!NOTE]
>  In diesem Dokument werden die Computer in Ihrem Netzwerk, anders als Ihr Server, Netzwerkcomputer aufgerufen.?  
  
###  <a name="BKMK_TheDestinationFolderIsNotValid"></a> Der Zielordner ist ungültig  
 **Ursache:** Der Ordner, in den Sie die Protokolldateien kopieren möchten, ist möglicherweise nicht vorhanden oder hat möglicherweise nicht genügend Speicherplatz für die Dateien.  
  
 **Lösung:** Überprüfen Sie, ob der ausgewählte Ordner vorhanden ist und ob auf dem Laufwerk für die Dateien ausreichend freier Speicherplatz verfügbar ist. Sie sollten auch sicherstellen, dass ausreichend freier Speicherplatz im temporären Ordner auf dem Laufwerk vorhanden ist.  
  
###  <a name="BKMK_ANetworkErrorHasOccurred"></a> Ein Netzwerkfehler ist aufgetreten.  
 **Ursache:** Möglicherweise gibt es ein Netzwerkproblem auf dem Netzwerk-Computer oder dem Server.  
  
 **Lösung:** Stellen Sie sicher, dass alle Computer und Netzwerkgeräte eingeschaltet sind und dass sie mit dem Netzwerk verbunden sind. Wenn Sie das Problem nicht beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.  
  
###  <a name="BKMK_CannotCollectLogFiles"></a> Protokolldateien für den Computer kann nicht erfasst werden.  
 **Ursache:** Der Log Collector ist möglicherweise nicht auf dem Computer installiert, da der Computer sich nicht erfolgreich mit dem Server mit Hilfe des Assistenten "Computer mit dem Server verbinden" verbunden hat.  
  
 **Lösung:** Weitere Informationen zur Behebung von Problemen in Bezug auf Verbindungen mit Ihrem Server finden Sie unter [Problembehandlung beim Verbinden von Computern an den Server](https://go.microsoft.com/fwlink/p/?LinkID=241492)? (https://go.microsoft.com/fwlink/p/?LinkID=241492) auf der Microsoft-Website.  
  
 Wenn Sie den Computer immer noch nicht mit dem Server verbinden können, können Sie die Protokolldateien manuell auf ein USB-Flashlaufwerk wie folgt kopieren:  
  
-   Für Clientcomputer, auf denen Windows 7, Windows 8 oder Windows Multipoint Server ausgeführt wird, kopieren Sie den Ordner **Protokolle** , der sich unter **%sysdir%\programdata\Microsoft\Windows Server**befindet.  
  
###  <a name="BKMK_YouDoNotHavePermission"></a> Sie haben keine Berechtigung zum Speichern der Log-Dateien in den ausgewählten Ordner  
 **Ursache:** Sie haben möglicherweise für den Ordner, den Sie für die Speicherung von Protokolldateien ausgewählt haben, keine Schreibberechtigung.  
  
 **Lösung:** Wenn Sie den Standardpfad zum Speichern von Protokolldateien verwenden, stellen Sie sicher, dass Sie über Schreibberechtigungen für den freigegebenen Ordner verfügen  **\\ \\< ServerName\>\Logs**. Wenn Sie Protokolle auf einem Computer im Netzwerk speichern, stellen Sie sicher, dass Sie eine Schreibberechtigung für den für die Speicherung von Protokolldateien ausgewählten Ordner haben  
  
###  <a name="BKMK_TheComputerIsNotConfiguredProperly"></a> Der Computer ist nicht ordnungsgemäß konfiguriert die Log-Dateien sammeln  
 **Ursache:** FDer Computer nicht ordnungsgemäß für den Log Collector konfiguriert.  
  
 **Lösung:** Neuinstallation des Log Collectors Weitere Informationen unter [Reinstalling the Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall).  
  
###  <a name="BKMK_AnUnknownErrorOccurred"></a> Unbekannter Fehler.  
 **Ursache:** Unbekannt  
  
 **Lösung 1:** Erneutes Ausführen des Log Collectors Wenn der Fehler erneut auftritt, stellen Sie sicher, dass es sich nicht um Probleme mit der Netzwerkkonnektivität handelt. Sie können auch versuchen, den Log Collector erneut zu installieren. Weitere Informationen unter [Reinstalling the Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Wenn Sie das Problem nicht beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.  
  
 **Lösung 2:** Versuchen Sie zunächst, den Ordner zu öffnen, in dem die Protokolldateien gespeichert werden. Wenn die Zip-Datei mit dem Computernamen bereits erstellt wurde, ignorieren Sie diesen Fehler und verwenden Sie stattdessen die Protokolldateien. Sind keine Protokolldateien generiert, führen Sie den Log Collector erneut aus. Wenn der Fehler erneut auftritt, stellen Sie sicher, dass es sich nicht um Probleme mit der Netzwerkkonnektivität handelt. Sie können auch versuchen, den Log Collector erneut zu installieren. Weitere Informationen unter [Reinstalling the Log Collector](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Wenn Sie das Problem nicht beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.