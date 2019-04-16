---
title: Problembehandlung bei Windows Server Essentials Log Collector-Fehler
description: Beschreibt, wie Sie Windows Server Essentials
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Problembehandlung bei Windows Server Essentials Log Collector-Fehler

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Wenn Sie den Log Collector ausführen, können Sie eine der folgenden Fehlermeldungen auftreten. Um das Problem zu beheben, führen Sie in der Anleitung für den jeweiligen Fehler.  
  
> [!NOTE]
>  In diesem Dokument werden die Computer in Ihrem Netzwerk, anders als Ihr Server Computern im Netzwerk bezeichnet.?  
  
###  <a name="BKMK_TheDestinationFolderIsNotValid"></a>Der Zielordner ist ungültig  
 **Ursache:** der Ordner, in dem Sie versuchen, die Protokolldateien kopieren, ist möglicherweise nicht vorhanden oder möglicherweise nicht genügend Speicherplatz für die Dateien.  
  
 **Lösung:** überprüfen, ob der ausgewählte Ordner vorhanden ist und auf dem Laufwerk für die Dateien ausreichend freier Speicherplatz verfügbar ist. Sie sollten außerdem sicherstellen, dass ausreichend freier Speicherplatz in den temporären Ordner auf dem Laufwerk vorhanden ist.  
  
###  <a name="BKMK_ANetworkErrorHasOccurred"></a>Ein Fehler ist aufgetreten.  
 **Ursache:** möglicherweise liegt ein Netzwerkproblem auf dem Netzwerkcomputer oder Server.  
  
 **Lösung:** stellen Sie sicher, die alle Computer und Netzwerkgeräte eingeschaltet sind, und sie mit dem Netzwerk verbunden sind. Wenn Sie das Problem beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.  
  
###  <a name="BKMK_CannotCollectLogFiles"></a>Protokolldateien für den Computer kann nicht erfasst werden.  
 **Ursache:** des Log Collectors kann nicht auf dem Computer installiert werden, da der Computer nicht erfolgreich mit dem Server den Assistenten zum Verbinden eines Computers mit hergestellt hat.  
  
 **Lösung:** Informationen zum Beheben von Problemen mit Verbindungen mit dem Server, finden Sie unter [Problembehandlung beim Verbinden von Computern mit dem Server](https://go.microsoft.com/fwlink/p/?LinkID=241492)? (https://go.microsoft.com/fwlink/p/?LinkID=241492) auf der Microsoft-Website.  
  
 Wenn Sie noch nicht auf den Computer mit dem Server verbinden können, können Sie die Protokolldateien manuell auf einem USB-Flashlaufwerk wie folgt kopieren:  
  
-   Für Clientcomputer, auf denen Windows7, Windows8 oder Windows Multipoint Server ausgeführt werden, kopieren Sie die **Protokolle** Ordner befindet sich am **%sysdir%\programdata\Microsoft\Windows Server**.  
  
###  <a name="BKMK_YouDoNotHavePermission"></a>Sie haben keine Berechtigung, um die Protokolldateien im ausgewählten Ordner zu speichern  
 **Ursache:** Sie möglicherweise nicht über eine Schreibberechtigung verfügen in den Ordner, die Sie für die Speicherung von Protokolldateien ausgewählt haben.  
  
 **Lösung:** Wenn Sie den Standardpfad verwenden, um Protokolldateien zu speichern, stellen Sie sicher, dass Sie über Schreibberechtigung für den freigegebenen Ordner verfügen **\\\ < ServerName\ > \Logs**. Wenn Sie Protokolle auf einem Computer im Netzwerk speichern, stellen Sie sicher, dass Sie über Schreibberechtigung für den Ordner, die Sie verfügen für die Speicherung von Protokolldateien ausgewählt haben.  
  
###  <a name="BKMK_TheComputerIsNotConfiguredProperly"></a>Der Computer ist nicht ordnungsgemäß konfiguriert die Protokolldateien erfassen  
 **Ursache:** der Computer wurde nicht ordnungsgemäß für den Log Collector konfiguriert wurde.  
  
 **Lösung:** den Log Collector erneut zu installieren. Weitere Informationen finden Sie unter [Neuinstallation des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall).  
  
###  <a name="BKMK_AnUnknownErrorOccurred"></a>Ein Unbekannter Fehler aufgetreten ist.  
 **Ursache:** unbekannt.  
  
 **Lösung 1:** führen Sie den Log Collector erneut aus. Wenn der Fehler erneut auftritt, stellen Sie sicher, dass keine Konnektivitätsprobleme vorliegen. Sie können auch versuchen, den Log Collector neu zu installieren. Weitere Informationen finden Sie unter [Neuinstallation des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Wenn Sie das Problem beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.  
  
 **Lösung 2:** versuchen Sie zunächst, den Ordner zu öffnen, in dem die Protokolldateien gespeichert werden. Wenn die ZIP-Datei mit dem Computernamen bereits erstellt wurde, ignorieren Sie diesen Fehler, und verwenden Sie stattdessen die Protokolldateien. Wenn es keine Protokolldateien generiert sind, führen Sie den Log Collector erneut aus. Wenn der Fehler erneut auftritt, stellen Sie sicher, dass keine Konnektivitätsprobleme vorliegen. Sie können auch versuchen, den Log Collector neu zu installieren. Weitere Informationen finden Sie unter [Neuinstallation des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Wenn Sie das Problem beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.