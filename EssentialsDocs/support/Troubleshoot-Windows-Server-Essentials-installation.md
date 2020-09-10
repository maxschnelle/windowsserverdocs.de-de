---
title: Problembehandlung bei der Windows Server Essentials-Installation
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.topic: article
ms.assetid: ecf19216-7aac-4aca-839a-342ac28f5329
author: nnamuhcs
ms.author: geschuma
manager: mtillman
ms.openlocfilehash: d46e760fd168d44cb8f036d6b1b28180db2ffce2
ms.sourcegitcommit: db2d46842c68813d043738d6523f13d8454fc972
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2020
ms.locfileid: "89625113"
---
# <a name="troubleshoot-windows-server-essentials-installation"></a>Problembehandlung bei der Windows Server Essentials-Installation

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Dieses Thema enthält Informationen zur Problembehandlung bei Problemen, die bei der Installation von Windows Server Essentials auftreten. Anleitungen werden für die folgenden Bereiche bereitgestellt:


-   [Allgemeine Schritte zur Problembehandlung](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)

-   [Behandeln von Treiberproblemen](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)

-   [Allgemeine Schritte zur Problembehandlung](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_GeneralTroubleshootingSteps)

-   [Behandeln von Treiberproblemen](Troubleshoot-Windows-Server-Essentials-installation.md#BKMK_TroubleshootDrivers)


> [!NOTE]
>  Die aktuellsten Informationen zur Problembehandlung aus der Windows Server Essentials-Community finden Sie im [Windows Server Essentials-Forum](/answers/topics/windows-server-essentials.html/threads). Das Windows Server Essentials-Forum eignet sich optimal, um nach Hilfe zu suchen oder um Fragen zu stellen.

##  <a name="general-troubleshooting-steps"></a><a name="BKMK_GeneralTroubleshootingSteps"></a> Allgemeine Schritte zur Problembehandlung
 Wenn die Installation von Windows Server Essentials fehlschlägt, führen Sie diese Schritte aus, um das Problem zu identifizieren, das den Fehler verursacht hat.

> [!IMPORTANT]
>  Es ist wichtig, dass Sie den Server bei der Installation von Windows Server Essentials nicht manuell neu starten. Der Server wird während der Installation und Erstkonfiguration automatisch mehrere Male neu gestartet. Wenn Sie den Server manuell neu gestartet haben, bevor Sie die Meldung **Serverinstallation erfolgreich** angezeigt wird, kann dies möglicherweise die Unterbrechung und das Misslingen der Installation verursacht haben.

#### <a name="to-identify-issues-in-a-failed-installation-of-windows-server-essentials"></a>So identifizieren Sie Probleme in einer fehlgeschlagenen Installation von Windows Server Essentials

1.  Stellen Sie sicher, dass Ihre Serverhardware die Mindestanforderungen erfüllt. Informationen zu Hardwareanforderungen finden Sie unter [System Anforderungen für Windows Server Essentials](../get-started/system-requirements.md).

2.  Wenn Sie die Windows Server Essentials-Installations-DVD von MSDN erhalten haben, stellen Sie sicher, dass die DVD gültig ist, indem Sie die SHA1-Summe prüfen. Weitere Informationen finden Sie unter [Verfügbarkeit und Beschreibung des File Checksum Integrity Verifier Utility](https://go.microsoft.com/fwlink/?LinkId=220495) ( https://go.microsoft.com/fwlink/?LinkId=220495) .

3.  Stellen Sie sicher, dass der Netzwerkadapter auf dem Server über ein Netzwerkkabel mit einem Router verbunden ist.

4.  Wenn der Server über mehrere Netzwerkadapter verfügt, stellen Sie sicher, dass nur ein Netzwerkadapter aktiviert ist.

    > [!IMPORTANT]
    >  Trennen Sie das Netzwerkkabel nicht, oder starten Sie den Router bei der Installation von Windows Server Essentials nicht neu.

5.  Lesen Sie "Server Installation und-Bereitstellung" in der [releasedokumentation für Windows Server Essentials](../get-started/release-notes.md) .

6.  Wenn Sie die Fehlermeldung erhalten, dass beim Einrichten des Servers während der Installation ein Fehler aufgetreten ist, verwenden Sie die serverwiederherstellungs-DVD und die Anweisungen des Herstellers der Hardware, um den Server auf die Werkseinstellungen wiederherzustellen.

##  <a name="troubleshoot-driver-issues"></a><a name="BKMK_TroubleshootDrivers"></a> Beheben von Treiber Problemen
 Das häufigste Problem bei der Installation von Windows Server Essentials sind Speichercontroller, für die Treiber manuell installiert werden müssen. Windows bietet Treiber für viele Speichercontroller, jedoch möglicherweise keine Treiber für Ihre bestimmte Hardware.

 Sie müssen möglicherweise auch Netzwerkkartentreiber für Ihre bestimmte Hardware manuell installieren.

###  <a name="adding-drivers-for-storage-controllers"></a><a name="BKMK_StorageDrivers"></a> Hinzufügen von Treibern für Speichercontroller
 Wenn Ihre Hardware Speicher Treiber erfordert, die nicht in Windows Server Essentials enthalten sind, verwenden Sie die folgenden Informationen, um das Setup abzuschließen.

 Wenn während der Installation die folgende Meldung angezeigt wird, müssen Sie für Ihren Speichercontroller manuell Treiber hinzufügen:

 **Fehler beim Setup von Windows Server**

 Das Festplattenlaufwerk, auf dem Windows Server Essentials gehostet werden konnte, wurde nicht gefunden. Möchten Sie zusätzliche Speichertreiber laden?

 Gehen Sie wie folgt vor, um einen Treiber für den Speichercontroller zu installieren.

##### <a name="to-manually-install-a-storage-controller-driver"></a>So installieren Sie einen Treiber für den Speichercontroller manuell

1. Besorgen Sie sich die Treiber für Ihren Speichercontroller. Diese werden vom Hardwarehersteller bereitgestellt und können auch auf der Website des Herstellers verfügbar sein.

2. Erstellen Sie einen Ordner namens TREIBER auf einer Diskette oder einem USB-Stick, und kopieren Sie die Treiber in den Ordner.

3. Schließen Sie das Diskettenlaufwerk bzw. den USB-Stick mit dem Treiber an den Computer an.

4. Starten Sie den Computer von der Windows Server Essentials-DVD.

    Wenn Speichercontroller Treiber fehlen, wird das Dialogfeld Windows Server Essentials-Setup Fehler angezeigt.

5. Klicken Sie im Dialogfeld Fehler des Windows Server Essentials-Setups auf **Ja** , um die zusätzlichen Speicher Treiber zu laden.

6. Bei der Aufforderung **Wählen Sie die INF-Datei des Treibers aus** navigieren Sie zur INF-Datei im Ordner TREIBER auf der Diskette oder dem USB-Stick, wählen die Datei aus, klicken mit der rechten Maustaste auf den Dateinamen und klicken dann auf **Öffnen**. Dadurch wird der Treiber geladen.

   > [!NOTE]
   >  Bevor Sie versuchen, die Datei zu laden, vergewissern Sie sich, dass Sie die Dateinamenweiterung (.inf) aus Kleinbuchstaben besteht. Bei diesem Vorgang wird Groß-/Kleinschreibung beachtet, sodass die Treiberdatei nicht geladen wird, wenn die Dateinamenweiterung Großbuchstaben enthält.

7. Klicken Sie an der Eingabeaufforderung auf **Ja**, um den Treiber während der Textmodusphase des Setups zur Verfügung zu stellen.

   Das Setup sollte nun normal fortgesetzt werden.

###  <a name="adding-drivers-for-network-adapters"></a><a name="BKMK_AddingNICdrivers"></a> Hinzufügen von Treibern für Netzwerkadapter
 Wenn ein Netzwerkadapter auf dem Computer nicht von Windows Server Essentials unterstützt wird, hat der Server nach Abschluss des Setups keine Netzwerkverbindung, und Sie können keine Computer mit dem Server verbinden.

 Am Ende der Windows Server Essentials-Installation werden Sie informiert, wenn ein Netzwerkadapter Treiber nicht automatisch installiert wurde. Sie können auch **Netzwerkverbindungen** in der Systemsteuerung auf einen fehlenden Netzwerkadaptertreiber überprüfen. Wenn dem Netzwerkadapter auf dem Server keine Netzwerkverbindung zugeordnet ist, müssen Sie einen Treiber installieren.

 Wenn dem Computer für einen Netzwerkadapter ein unterstützter Treiber fehlt, müssen Sie den richtigen Netzwerkadaptertreiber manuell installieren und den Server anschließend neu starten. Verwenden Sie das folgende Verfahren.

##### <a name="to-install-a-network-adapter-driver"></a>So installieren Sie einen Netzwerkadaptertreiber

1.  Beziehen Sie den fehlenden Treiber vom Hersteller des Netzwerkadapters.

2.  Befolgen Sie die Anweisungen des Herstellers zur Installation des Treibers.

3.  Starten Sie den Computer neu.

    > [!IMPORTANT]
    >  Wenn Sie den Server nach der Installation des fehlenden Netzwerkadapter Treibers nicht neu starten, kann die Installation der Windows Server Essentials-Connector-Software auf Ihren Client Computern fehlschlagen.