---
title: Problembehandlung bei Windows Server Essentials-Installation
description: Beschreibt, wie Sie Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecf19216-7aac-4aca-839a-342ac28f5329
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 293b392203269a65efffcefb3744bedc659f71c9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Problembehandlung bei Windows Server Essentials-Installation

>Gilt für: Windows Server2016 Essentials, Windows Server2012 R2 Essentials, Windows Server2012 Essentials

Dieses Thema enthält Informationen zur Problembehandlung von Problemen, die bei der Installation von Windows Server Essentials auftreten. Anleitungen finden Sie in den folgenden Bereichen:  
  

-   [Allgemeine Schrittezur Problembehandlung](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [Behandeln von Treiberproblemen](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

-   [Allgemeine Schrittezur Problembehandlung](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [Behandeln von Treiberproblemen](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

  
> [!NOTE]
>  Aktuelle Informationen zur Problembehandlung aus der Windows Server Essentials-Community, empfehlen wir, Sie besuchen die [Windows Server Essentials-Forum](https://social.technet.microsoft.com/Forums/winserveressentials/threads). Die Windows Server Essentials-Forum ist ein idealer Ausgangspunkt, um nach Hilfe suchen oder eine Frage stellen.  
  
##  <a name="BKMK_GeneralTroubleshootingSteps"></a>Allgemeine Schrittezur Problembehandlung  
 Wenn die Installation von Windows Server Essentials fehlschlägt, nehmen Sie diese Schritte, um das Problem zu identifizieren, das den Fehler verursacht hat.  
  
> [!IMPORTANT]
>  Es ist wichtig, dass Sie nicht manuell den Server neu starten während der Installation von Windows Server Essentials. Der Server wird automatisch neu gestartet mehrmals während der Installation und Erstkonfiguration. Wenn Sie manuell vor dem Neustart des Servers wurde die **Serverinstallation erfolgreich** Nachricht, die die Installation unterbrochen und verursacht haben.  
  
#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Identifizieren von Problemen in einer nicht erfolgreichen Installation von Windows Server Essentials  
  
1.  Stellen Sie sicher, dass Ihre Serverhardware die Mindestanforderungen erfüllt. Informationen zu den Hardwareanforderungen finden Sie unter [System Requirements for Windows Server Essentials](../get-started/system-requirements.md).  
  
2.  Wenn Sie die Windows Server Essentials-Installations-DVD von MSDN erhalten haben, stellen Sie sicher, dass die DVD gültig ist, indem Sie die SHA1-Summe überprüfen. Weitere Informationen finden Sie unter [Verfügbarkeit und Beschreibung des Dienstprogramms File Checksum Integrity Verifier](https://go.microsoft.com/fwlink/?LinkId=220495) (https://go.microsoft.com/fwlink/?LinkId=220495).  
  
3.  Stellen Sie sicher, dass der Netzwerkadapter auf dem Server über ein Netzwerkkabel mit einem Router verbunden ist.  
  
4.  Wenn der Server über mehrere Netzwerkadapter verfügt, stellen Sie sicher, dass nur ein Netzwerkadapter aktiviert ist.  
  
    > [!IMPORTANT]
    >  Trennen Sie das Netzwerkkabel nicht, und starten Sie den Router während der Installation von Windows Server Essentials.  
  
5.  Überprüfen von "Server-Installation und Bereitstellung" in [Release Documentation for Windows Server Essentials](../get-started/release-notes.md)  
  
6.  Wenn Sie die Fehlermeldung ist ein Fehler aufgetreten, während der Einrichtung des Servers während der Installation verwenden Sie die Serverwiederherstellungs-DVD und den Anweisungen des Herstellers der Hardware zum Wiederherstellen des Servers auf die werkseitigen Standardeinstellungen.  
  
##  <a name="BKMK_TroubleshootDrivers"></a>Behandeln von Treiberproblemen  
 Das häufigste Problem bei der Installation von Windows Server Essentials ist Speichercontroller, um den Treiber manuell installiert wurden. Windows bietet Treiber für viele Speichercontroller, jedoch möglicherweise keine Treiber für Ihre bestimmte Hardware.  
  
 Sie müssen möglicherweise auch Netzwerkkartentreiber für Ihre bestimmte Hardware manuell installieren.  
  
###  <a name="BKMK_StorageDrivers"></a>Hinzufügen von Treibern für Speichercontroller  
 Wenn Ihre Hardware Speichertreiber, die nicht in Windows Server Essentials enthalten sind benötigt, verwenden Sie die folgende Informationen zum Abschließen der Installation.  
  
 Wenn Sie während der Installation die folgende Meldung angezeigt wird, müssen Sie die Treiber für Ihren Speichercontroller manuell hinzufügen:  
  
 **Fehler beim Setup von Windows Server**  
  
 Festplatte kann Windows Server Essentials gehostet wurde nicht gefunden. Möchten Sie zusätzliche Speichertreiber laden?  
  
 Verwenden Sie das folgende Verfahren, um einen Treiber für den Speichercontroller zu installieren.  
  
##### <a name="to-manually-install-a-storage-controller-driver"></a>So installieren Sie einen Treiber für den Speichercontroller manuell  
  
1.  Suchen Sie die Treiber für Ihren Speichercontroller. Diese werden vom Hardwarehersteller bereitgestellt, und sie können möglicherweise auch auf der Website des Herstellers verfügbar.  
  
2.  Erstellen Sie einen Ordner namens Treiber auf einer Diskette oder einem USB Flash-Laufwerk, und kopieren Sie die Treiber in den Ordner.  
  
3.  Schließen Sie das Diskettenlaufwerk bzw. USB-Flashlaufwerk mit dem Treiber an den Computer  
  
4.  Starten Sie den Computer von der Windows Server Essentials-DVD.  
  
     Wenn Speichercontrollertreiber fehlen, wird das Dialogfeld "Windows Server Essentials-Setup-Fehler" angezeigt.  
  
5.  Klicken Sie im Dialogfeld "Fehler beim Setup von Windows Server Essentials" **Ja** zusätzliche Speichertreiber laden.  
  
6.  Bei der **wählen Sie die inf-Datei des Treibers** auffordern, navigieren Sie zu der INF-Datei im Ordner "Treiber" auf der Diskette oder USB-Laufwerk, wählen Sie die Datei, mit der rechten Maustaste in des Dateinamens und klicken Sie dann auf **öffnen**. Dadurch wird den Treiber geladen.  
  
    > [!NOTE]
    >  Bevor Sie versuchen, die Datei zu laden, stellen Sie sicher, dass die Datei Namen Erweiterung (.inf) aus Kleinbuchstaben besteht. Dieser Vorgang wird Groß-/Kleinschreibung beachtet, und eine Treiberdatei wird nicht geladen werden, wenn die Dateinamenerweiterung Großbuchstaben enthält.  
  
7.  Klicken Sie dazu aufgefordert werden, auf **Ja** den Treiber während der Textmodusphase des Setups zur Verfügung stellen.  
  
 Setup sollte nun normal fortgesetzt.  
  
###  <a name="BKMK_AddingNICdrivers"></a>Hinzufügen von Treibern für Netzwerkadapter  
 Wenn ein Netzwerkadapter auf dem Computer von Windows Server Essentials nicht unterstützt wird, müssen der Server nicht Netzwerkkonnektivität, nachdem Setup abgeschlossen ist, und Sie ist nicht in der Lage, Computer mit dem Server herstellen.  
  
 Am Ende der Windows Server Essentials-Installation werden Sie darüber informiert, wenn ein Netzwerkadaptertreiber nicht automatisch installiert wurde. Sie können auch **Netzwerkverbindungen** in der Systemsteuerung für einen fehlenden Netzwerkadaptertreiber überprüfen. Wenn Sie eine Netzwerkverbindung mit dem Netzwerkadapter auf dem Server zugeordnete nicht angezeigt werden, müssen Sie einen Treiber installieren.  
  
 Wenn der Computer für einen Netzwerkadapter einen unterstützten Treiber fehlt, müssen Sie den richtigen Netzwerkadaptertreiber manuell installieren und starten Sie den Server neu. Mithilfe des folgenden Verfahrens.  
  
##### <a name="to-install-a-network-adapter-driver"></a>So installieren Sie einen Netzwerkadaptertreiber  
  
1.  Rufen Sie die fehlenden Treiber vom Hersteller des Netzwerkadapters.  
  
2.  Führen Sie die Installation des Herstellers zur Installation des Treibers.  
  
3.  Starten Sie den Computer neu.  
  
    > [!IMPORTANT]
    >  Wenn Sie den Server nach der Installation des fehlenden Netzwerkadaptertreibers nicht neu starten, kann die Installation der Windows Server Essentials Connector-Software auf den Clientcomputern fehlschlagen.
