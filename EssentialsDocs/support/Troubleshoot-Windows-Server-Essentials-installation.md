---
title: Problembehandlung bei der Windows Server Essentials-Installation
description: Beschreibt, wie Windows Server Essentials
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59862021"
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Problembehandlung bei der Windows Server Essentials-Installation

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema enthält die Behandlung von Problemen, die auftreten, wenn Sie Windows Server Essentials installieren. Anleitungen werden für die folgenden Bereiche bereitgestellt:  
  

-   [Allgemeine Schritte zur Problembehandlung](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [Behandeln von Treiberproblemen](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

-   [Allgemeine Schritte zur Problembehandlung](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)  
  
-   [Behandeln von Treiberproblemen](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)  

  
> [!NOTE]
>  Die aktuellsten Informationen zur Problembehandlung aus der Windows Server Essentials-Community wird empfohlen, Sie besuchen die [Windows Server Essentials-Forum](https://social.technet.microsoft.com/Forums/winserveressentials/threads). Das Windows Server Essentials-Forum eignet sich optimal, um nach Hilfe zu suchen oder um Fragen zu stellen.  
  
##  <a name="BKMK_GeneralTroubleshootingSteps"></a> Allgemeine Schritte zur Problembehandlung  
 Wenn die Installation von Windows Server Essentials ein Fehler auftritt, werden Sie diese Maßnahmen durchführen, um das Problem zu identifizieren, das den Fehler verursacht hat.  
  
> [!IMPORTANT]
>  Es ist wichtig, dass Sie nicht manuell Ihren Server neu gestartet werden während der Installation von Windows Server Essentials. Der Server wird während der Installation und Erstkonfiguration automatisch mehrere Male neu gestartet. Wenn Sie den Server manuell neu gestartet haben, bevor Sie die Meldung **Serverinstallation erfolgreich** angezeigt wird, kann dies möglicherweise die Unterbrechung und das Misslingen der Installation verursacht haben.  
  
#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>Zum Identifizieren von Problemen bei einer fehlerhaften Installation von Windows Server Essentials  
  
1.  Stellen Sie sicher, dass Ihre Serverhardware die Mindestanforderungen erfüllt. Weitere Informationen zu den hardwareanforderungen finden Sie unter [System Requirements for Windows Server Essentials](../get-started/system-requirements.md).  
  
2.  Wenn Sie die Windows Server Essentials-Installations-DVD von MSDN erhalten haben, stellen Sie sicher, dass die DVD gültig ist, indem Sie die SHA1-Summe überprüfen. Weitere Informationen finden Sie unter [Verfügbarkeit und Beschreibung des Hilfsprogramms File Checksum Integrity Verifier](https://go.microsoft.com/fwlink/?LinkId=220495) (https://go.microsoft.com/fwlink/?LinkId=220495).  
  
3.  Stellen Sie sicher, dass der Netzwerkadapter auf dem Server über ein Netzwerkkabel mit einem Router verbunden ist.  
  
4.  Wenn der Server über mehrere Netzwerkadapter verfügt, stellen Sie sicher, dass nur ein Netzwerkadapter aktiviert ist.  
  
    > [!IMPORTANT]
    >  Das Netzwerkkabel nicht, und starten Sie den Router neu, während der Installation von Windows Server Essentials.  
  
5.  Überprüfen Sie "Server-Installation und Bereitstellung" in [Release Documentation for Windows Server Essentials](../get-started/release-notes.md)  
  
6.  Wenn Sie die Fehlermeldung ist ein Fehler aufgetreten, während der Einrichtung des Servers während der Installation verwenden die Serverwiederherstellungs-DVD und den Anweisungen des Herstellers der Hardware, um den Server auf die werkseitigen Standardeinstellungen zurückzusetzen.  
  
##  <a name="BKMK_TroubleshootDrivers"></a> Behandeln von Treiberproblemen  
 Das häufigste Problem bei der Installation von Windows Server Essentials ist Speichercontroller, die Treiber manuell installiert wurden. Windows bietet Treiber für viele Speichercontroller, jedoch möglicherweise keine Treiber für Ihre bestimmte Hardware.  
  
 Sie müssen möglicherweise auch Netzwerkkartentreiber für Ihre bestimmte Hardware manuell installieren.  
  
###  <a name="BKMK_StorageDrivers"></a> Hinzufügen von Treibern für Speichercontroller  
 Wenn Ihre Hardware Speichertreiber, die nicht in Windows Server Essentials enthalten sind benötigt, verwenden Sie die folgende Informationen, um das Setup abzuschließen.  
  
 Wenn während der Installation die folgende Meldung angezeigt wird, müssen Sie für Ihren Speichercontroller manuell Treiber hinzufügen:  
  
 **Windows Server-Setup-Fehler**  
  
 Hosten von Windows Server Essentials können Festplattenlaufwerk wurde nicht gefunden. Möchten Sie zusätzliche Speichertreiber laden?  
  
 Gehen Sie wie folgt vor, um einen Treiber für den Speichercontroller zu installieren.  
  
##### <a name="to-manually-install-a-storage-controller-driver"></a>So installieren Sie einen Treiber für den Speichercontroller manuell  
  
1.  Besorgen Sie sich die Treiber für Ihren Speichercontroller. Diese werden vom Hardwarehersteller bereitgestellt und können auch auf der Website des Herstellers verfügbar sein.  
  
2.  Erstellen Sie einen Ordner namens TREIBER auf einer Diskette oder einem USB-Stick, und kopieren Sie die Treiber in den Ordner.  
  
3.  Schließen Sie das Diskettenlaufwerk bzw. den USB-Stick mit dem Treiber an den Computer an.  
  
4.  Starten Sie den Computer auf der DVD für Windows Server Essentials.  
  
     Wenn Speichercontrollertreiber fehlen, wird das Dialogfeld "Windows Server Essentials-Setup-Fehler" angezeigt.  
  
5.  Klicken Sie in das Dialogfeld Windows Server Essentials-Setup-Fehler auf **Ja** um zusätzliche Speichertreiber zu laden.  
  
6.  Bei der Aufforderung **Wählen Sie die INF-Datei des Treibers aus** navigieren Sie zur INF-Datei im Ordner TREIBER auf der Diskette oder dem USB-Stick, wählen die Datei aus, klicken mit der rechten Maustaste auf den Dateinamen und klicken dann auf **Öffnen**. Dadurch wird der Treiber geladen.  
  
    > [!NOTE]
    >  Bevor Sie versuchen, die Datei zu laden, vergewissern Sie sich, dass Sie die Dateinamenweiterung (.inf) aus Kleinbuchstaben besteht. Bei diesem Vorgang wird Groß-/Kleinschreibung beachtet, sodass die Treiberdatei nicht geladen wird, wenn die Dateinamenweiterung Großbuchstaben enthält.  
  
7.  Klicken Sie an der Eingabeaufforderung auf **Ja**, um den Treiber während der Textmodusphase des Setups zur Verfügung zu stellen.  
  
 Das Setup sollte nun normal fortgesetzt werden.  
  
###  <a name="BKMK_AddingNICdrivers"></a> Hinzufügen von Treibern für Netzwerkadapter  
 Wenn ein Netzwerkadapter auf dem Computer nicht von Windows Server Essentials unterstützt wird, wird Ihr Server keine Netzwerkverbindung nachdem Setup abgeschlossen ist, und Sie werden nicht in der Computer mit Ihrem Server herstellen können.  
  
 Am Ende der Installation von Windows Server Essentials werden Sie darüber informiert, wenn ein Netzwerkadaptertreiber nicht automatisch installiert wurde. Sie können auch **Netzwerkverbindungen** in der Systemsteuerung auf einen fehlenden Netzwerkadaptertreiber überprüfen. Wenn dem Netzwerkadapter auf dem Server keine Netzwerkverbindung zugeordnet ist, müssen Sie einen Treiber installieren.  
  
 Wenn dem Computer für einen Netzwerkadapter ein unterstützter Treiber fehlt, müssen Sie den richtigen Netzwerkadaptertreiber manuell installieren und den Server anschließend neu starten. Führen Sie dazu die nachfolgend aufgeführten Schritte aus.  
  
##### <a name="to-install-a-network-adapter-driver"></a>So installieren Sie einen Netzwerkadaptertreiber  
  
1.  Beziehen Sie den fehlenden Treiber vom Hersteller des Netzwerkadapters.  
  
2.  Befolgen Sie die Anweisungen des Herstellers zur Installation des Treibers.  
  
3.  Starten Sie den Computer neu.  
  
    > [!IMPORTANT]
    >  Wenn Sie den Server nach der Installation der fehlenden Netzwerkadaptertreiber nicht neu starten, kann die Installation der Windows Server Essentials Connector-Software auf Ihren Clientcomputern fehlschlagen.
