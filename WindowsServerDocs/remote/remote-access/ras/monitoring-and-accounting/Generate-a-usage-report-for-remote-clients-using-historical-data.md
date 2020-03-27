---
title: Erstellen eines Nutzungsberichts für Remoteclients mithilfe von Verlaufsdaten
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0305467b-ce39-4532-a05a-2cc5ff946f55
ms.author: lizross
author: eross-msft
ms.openlocfilehash: ce5219feca1d55191352d95f2aac017709a5a449
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80314293"
---
# <a name="generate-a-usage-report-for-remote-clients-using-historical-data"></a>Erstellen eines Nutzungsberichts für Remoteclients mithilfe von Verlaufsdaten

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

**Hinweis:** Durch Windows Server 2012 werden DirectAccess und RRAS (Routing and Remote Access Service, Routing- und RAS-Dienst) zu einer einzigen Remotezugriffsrolle zusammengefasst.  
  
Mithilfe der-Verwaltungskonsole auf dem Remote Zugriffs Server kann ein Verwendungs Bericht für die Remote Clients generiert werden, die auf den Server zugreifen. Um einen Verwendungs Bericht für Remote Clients zu generieren, aktivieren Sie zunächst die Kontoführung auf dem RAS-Server. Nachdem Sie den Bericht generiert haben, können Sie das Überwachungs Dashboard verwenden, das in der-Verwaltungskonsole auf dem RAS-Server verfügbar ist, um die Auslastungs Statistiken auf dem Server anzuzeigen.  
  
> [!NOTE]  
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-enable-accounting-on-the-remote-access-server"></a>So aktivieren Sie die Kontoführung auf dem Remote Zugriffs Server  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **Berichterstattung** , um in der **Remote Zugriffs-Verwaltungskonsole**zur **Remote Zugriffs Berichterstattung** zu navigieren.  
  
3.  Klicken Sie im Aufgabenbereich **Remote Zugriffs Berichterstattung** auf Konto **Führung konfigurieren** .  
  
4.  Aktivieren Sie das Kontrollkästchen **Posteingangs Erfassung verwenden** , um die Kontoführung auf dem Remote Zugriffs Server zu aktivieren.  
  
5.  Klicken **Sie auf übernehmen, um die** Buchhaltungs Konfiguration auf dem Server zu aktivieren, und klicken Sie dann auf **Schließen** , nachdem der Server die Konfiguration erfolgreich angewendet hat.  
  
#### <a name="to-generate-the-usage-report"></a>So generieren Sie den Verwendungs Bericht  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **Berichterstattung** , um in der **Remote Zugriffs-Verwaltungskonsole**zur **Remote Zugriffs Berichterstattung** zu navigieren.  
  
3.  Klicken Sie im mittleren Bereich auf Datumsangaben im Kalender, um das **Start Datum** für die Berichts Dauer (und das **Enddatum:** ) auszuwählen, und klicken Sie dann auf **Bericht generieren**.  
  
4.  Es wird eine Liste der Benutzer angezeigt, die innerhalb des ausgewählten Zeitraums eine Verbindung mit dem RAS-Server hergestellt haben, und detaillierte Statistiken dazu. Klicken Sie auf die erste Zeile in der Liste. Wenn Sie eine Zeile auswählen, wird die Remote Benutzeraktivität im Vorschaubereich angezeigt. Wählen Sie nun im Vorschaubereich die Registerkarte **Server Lade Statistik** aus, um die Verlaufs Auslastung auf dem Server anzuzeigen.  
  
    Klicken Sie im Vorschaufenster auf die Registerkarte Statistiken für den **Server Lade** Vorgang, um die Verlaufs Auslastung auf dem Server anzuzeigen.  
  
> [!NOTE]  
> **Grundlegendes zu Sitzungen**  
>   
> Die Kontoführung für den Remote Zugriff basiert auf dem Konzept der **Sitzungen**. Im Gegensatz zu einer **Verbindung**wird eine **Sitzung** durch eine Kombination aus Remote Client-IP-Adresse und Benutzername eindeutig identifiziert. Wenn z. b. ein Computer Tunnel vom Remote Client mit dem Namen CLIENT1 gebildet wird, wird eine Sitzung erstellt und in der Buchhaltungs Datenbank gespeichert. Wenn ein Benutzer mit dem Namen user1 nach einiger Zeit eine Verbindung mit diesem Client herstellt (der Computer Tunnel ist jedoch noch aktiv), wird die Sitzung als separate Sitzung aufgezeichnet. Der Unterschied zwischen den verschiedenen Sitzungen besteht darin, den Unterschied zwischen Computer Tunnel und Benutzer Tunnel beizubehalten.  
  
![der entsprechenden Windows PowerShell-](../../../media/Generate-a-usage-report-for-remote-clients-using-historical-data/PowerShellLogoSmall.gif)***<em>Befehle in Windows PowerShell</em>***  
  
Die folgenden Windows PowerShell-Cmdlets führen dieselbe Funktion wie das vorherige Verfahren aus. Jedes Cmdlet sollte in einer eigenen Zeile eingegeben werden, obwohl sie hier aufgrund von Formateinschränkungen auf mehrere Zeilen umbrochen sein können.  
  
Ändern Sie im folgenden Skript den Datumsbereich, für den Sie einen Bericht erstellen möchten, in den Parametern **-StartDateTime** und **-EndDateTime** .  
  
```  
PS> Get-RemoteAccessConnectionStatisticsSummary -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
Shows server load statistics.  
PS> Get-RemoteAccessUserActivity -HostIPAddress 10.0.0.1 -StartDateTime "1 October 2010 00:00:00" -EndDateTime "14 October 2010 00:00:00"  
```  
  


