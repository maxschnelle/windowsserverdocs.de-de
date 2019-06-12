---
title: Erstellen eines Nutzungsberichts für Remoteclients mithilfe von Verlaufsdaten
description: Dieses Thema ist Teil des Leitfadens für die Überwachung des Remotezugriffs und Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0305467b-ce39-4532-a05a-2cc5ff946f55
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fa82ba8e2fc3fe19b9e73f602605d3ef76f4b9a5
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446901"
---
# <a name="generate-a-usage-report-for-remote-clients-using-historical-data"></a>Erstellen eines Nutzungsberichts für Remoteclients mithilfe von Verlaufsdaten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

**Hinweis**: Durch Windows Server 2013 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Die-Verwaltungskonsole auf dem RAS-Server kann verwendet werden, um einen Bericht für die Remoteclients zu generieren, die auf den Server zugreifen. Um eines Nutzungsberichts für Remoteclients zu generieren, können Sie zuerst Kontoführung auf dem RAS-Server. Nachdem Sie den Bericht generiert haben, können Sie das überwachungsdashboard verwenden, das in der Verwaltungskonsole auf dem RAS-Server an die Load-Statistiken auf dem Server verfügbar ist.  
  
> [!NOTE]  
> Sie müssen als Mitglied der Gruppe "Domänen-Admins" oder ein Mitglied der Gruppe "Administratoren" auf jedem Computer angemeldet sein, die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht abschließen können, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Administratoren" ist, versuchen Sie es die Aufgabe auszuführen, während Sie sich mit einem Konto angemeldet sind, die Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-enable-accounting-on-the-remote-access-server"></a>Kontoführung auf dem RAS-Server aktivieren  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **REPORTING** , zu dem navigiert **Remoteberichte Zugriff** in die **Remotezugriffs-Verwaltungskonsole**.  
  
3.  Klicken Sie auf **Kontoführung konfigurieren** in die **Remoteberichte Zugriff** Aufgabenbereich.  
  
4.  Wählen Sie die **verwenden posteingangskontoführung** um Kontoführung auf dem RAS-Server zu aktivieren.  
  
5.  Klicken Sie auf **übernehmen** die Buchhaltung-Konfiguration auf dem Server zu aktivieren, und klicken Sie auf **schließen** , nachdem der Server die Konfiguration erfolgreich angewendet wurde.  
  
#### <a name="to-generate-the-usage-report"></a>Den Nutzungsbericht generieren  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **REPORTING** , zu dem navigiert **Remoteberichte Zugriff** in die **Remotezugriffs-Verwaltungskonsole**.  
  
3.  Klicken Sie im mittleren Bereich auf Datumsangaben im Kalender auswählen die Berichtsdauer **Startdatum:** und **Enddatum:** , und klicken Sie dann auf **Bericht generieren**.  
  
4.  Sie sehen die Liste der Benutzer, die in den ausgewählten Zeitraum und detaillierte Statistiken zu diesen an den RAS-Server verbunden haben. Klicken Sie auf der ersten Zeile in der Liste. Wenn Sie eine Zeile auswählen, wird die Remotebenutzer-Aktivität im Vorschaufenster angezeigt. Wählen Sie jetzt die **Serverstatistiken laden** Registerkarte im Vorschaubereich auf das Laden historischer Daten auf dem Server finden Sie unter.  
  
    Klicken Sie auf die **Serverstatistiken laden** Registerkarte im Vorschaubereich auf das Laden historischer Daten auf dem Server finden Sie unter.  
  
> [!NOTE]  
> **Grundlegendes zu Sitzungen**  
>   
> Remote Access Buchhaltung basiert auf dem Konzept von **Sitzungen**. Im Gegensatz zu einem **Verbindung**, **Sitzung** wird durch eine Kombination von remote-Client-IP-Adresse und ein beispielbenutzername eindeutig identifiziert. Z. B. wenn ein computertunnel vom Remoteclient, mit dem Namen Client1, formatiert ist wird eine Sitzung erstellt und gespeichert werden in der Datenbank berücksichtigt. Beim Übergeben von eines Benutzers benannten "user1" von diesem Client nach einiger Zeit eine Verbindung herstellt (aber der computertunnel noch aktiv ist), wird die Sitzung einer separaten Sitzung aufgezeichnet. Die Unterscheidung von Sitzungen ist den Unterschied zwischen computertunnel und Benutzer Tunnel beibehalten werden sollen.  
  
![Windows PowerShell](../../../media/Generate-a-usage-report-for-remote-clients-using-historical-data/PowerShellLogoSmall.gif)***<em>gleichwertige Windows PowerShell-Befehle</em>***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
Das folgende Skript, ändern Sie den Datumsbereich für die Sie einen Bericht, in möchten der **"StartDateTime" -** und **- EndDateTime** Parameter.  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
Shows server load statistics.  
PS> Get-RemoteAccessUserActivity -HostIPAddress 10.0.0.1 -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
```  
  


