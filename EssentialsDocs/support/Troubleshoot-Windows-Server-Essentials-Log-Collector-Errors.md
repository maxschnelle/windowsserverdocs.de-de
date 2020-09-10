---
title: Problembehandlung für Fehler mit dem Windows Server Essentials-Protokollsammler
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: fa2e1685-31c0-4d4f-a10a-6c8885dfc493
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: 6f8318b6a6b711c6041a9227cd2d207470233dab
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625137"
---
# <a name="troubleshoot-windows-server-essentials-log-collector-errors"></a>Problembehandlung für Fehler mit dem Windows Server Essentials-Protokollsammler

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Bei der Ausführung des Log Collectors kann einer der folgenden Fehler auftreten. Um ein Problem zu beheben, befolgen Sie die Anleitungen für den jeweiligen Fehler.

> [!NOTE]
> In diesem Dokument werden die Computer in Ihrem Netzwerk, von denen es sich nicht um den Server handelt, als "Netzwerk Computer" bezeichnet.

###  <a name="the-destination-folder-is-not-valid"></a><a name="BKMK_TheDestinationFolderIsNotValid"></a> Der Zielordner ist ungültig.
 **Ursache:** Der Ordner, in den Sie die Protokolldateien kopieren möchten, ist möglicherweise nicht vorhanden oder bietet vielleicht nicht genügend Speicherplatz für die Dateien.

 **Lösung:** Überprüfen Sie, ob der ausgewählte Ordner vorhanden ist und ob auf dem Laufwerk für die Dateien ausreichend freier Speicherplatz verfügbar ist. Sie sollten auch sicherstellen, dass ausreichend freier Speicherplatz im temporären Ordner auf dem Laufwerk vorhanden ist.

###  <a name="a-network-error-has-occurred"></a><a name="BKMK_ANetworkErrorHasOccurred"></a> Netzwerkfehler
 **Ursache:** Möglicherweise gibt es ein Netzwerkproblem auf dem Netzwerkcomputer oder -server.

 **Lösung:** Stellen Sie sicher, dass alle Computer und Netzwerkgeräte eingeschaltet sind und dass sie mit dem Netzwerk verbunden sind. Wenn Sie das Problem nicht beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.

###  <a name="cannot-collect-log-files-for-the-computer"></a><a name="BKMK_CannotCollectLogFiles"></a> Protokolldateien für den Computer können nicht erfasst werden.
 **Ursache:** Der Log Collector ist möglicherweise nicht auf dem Computer installiert, da der Computer über den Assistenten zum Verbinden des Computers mit dem Server keine erfolgreiche Verbindung mit dem Server hergestellt hat.

 **Lösung:** Informationen zum Beheben von Problemen bei Verbindungen mit dem Server finden Sie unter Problembehandlung [beim Verbinden von Computern mit dem Server](https://go.microsoft.com/fwlink/p/?LinkID=241492).

 Wenn Sie den Computer immer noch nicht mit dem Server verbinden können, können Sie die Protokolldateien manuell auf ein USB-Flashlaufwerk wie folgt kopieren:

-   Für Clientcomputer, auf denen Windows 7, Windows 8 oder Windows Multipoint Server ausgeführt wird, kopieren Sie den Ordner **Protokolle** , der sich unter **%sysdir%\programdata\Microsoft\Windows Server**befindet.

###  <a name="you-do-not-have-permission-to-save-the-log-files-to-the-selected-folder"></a><a name="BKMK_YouDoNotHavePermission"></a> Sie verfügen nicht über die Berechtigung, die Protokolldateien im ausgewählten Ordner zu speichern.
 **Ursache:** Sie haben möglicherweise für den Ordner, den Sie für die Speicherung von Protokolldateien ausgewählt haben, keine Schreibberechtigung.

 **Lösung:** Wenn Sie den Standardpfad zum Speichern von Protokolldateien verwenden, stellen Sie sicher, dass Sie über Schreibberechtigungen für den freigegebenen Ordner ** \\ \\<Servername \> \Logs**verfügen. Wenn Sie Protokolle auf einem Computer im Netzwerk speichern, stellen Sie sicher, dass Sie eine Schreibberechtigung für den für die Speicherung von Protokolldateien ausgewählten Ordner haben

###  <a name="the-computer-is-not-configured-properly-to-collect-the-log-files"></a><a name="BKMK_TheComputerIsNotConfiguredProperly"></a> Der Computer ist nicht ordnungsgemäß konfiguriert, um die Protokolldateien zu erfassen.
 **Ursache:** Der Computer wurde nicht ordnungsgemäß für den Log Collector konfiguriert.

 **Lösung:** Installieren Sie den Log Collector neu. Siehe [Neuinstallation des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall).

###  <a name="an-unknown-error-occurred"></a><a name="BKMK_AnUnknownErrorOccurred"></a> Ein unbekannter Fehler ist aufgetreten.
 **Ursache:** unbekannt.

 **Lösung 1:** Führen Sie den Log Collector erneut aus. Wenn der Fehler erneut auftritt, stellen Sie sicher, dass es sich nicht um Probleme mit der Netzwerkkonnektivität handelt. Sie können auch versuchen, den Log Collector erneut zu installieren. Siehe [Neuinstallation des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Wenn Sie das Problem nicht beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.

 **Lösung 2:** Versuchen Sie zunächst, den Ordner zu öffnen, in dem die Protokolldateien gespeichert werden. Wenn die Zip-Datei mit dem Computernamen bereits erstellt wurde, ignorieren Sie diesen Fehler und verwenden Sie stattdessen die Protokolldateien. Sind keine Protokolldateien generiert, führen Sie den Log Collector erneut aus. Wenn der Fehler erneut auftritt, stellen Sie sicher, dass es sich nicht um Probleme mit der Netzwerkkonnektivität handelt. Sie können auch versuchen, den Log Collector erneut zu installieren. Siehe [Neuinstallation des Log Collectors](Install-the-Windows-Server-Essentials-Log-Collector.md#BKMK_Reinstall). Wenn Sie das Problem nicht beheben können, wenden Sie sich an die Person, die Ihr Netzwerk wartet.