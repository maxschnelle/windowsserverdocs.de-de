---
title: "Wiederherstellung des AD-Gesamtstruktur - Ausführen einer vollständigen Wiederherstellungs"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/07/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adfs
ms.openlocfilehash: 5de71cc005e9ec4c1425f9fa805b3c043ab4ea36
ms.sourcegitcommit: 84a2bdcb92ba6af45781fab9727617e50fa5e911
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/07/2017
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>Wiederherstellung des AD-Gesamtstruktur - Ausführen einer vollständigen Wiederherstellungs 

>Gilt für: Windows Server2016, Windows Server2012 und 2012 R2, Windows Server2008 und 2008 R2
 
Verwenden Sie das folgende Verfahren zum Ausführen einer vollständigen Wiederherstellungs für Windows Server2016, 2012 R2 oder 2012. 

## <a name="active-directory-full-server-recovery"></a>Active Directory vollständige Wiederherstellung des Servers
Eine vollständige Wiederherstellung des Servers ist erforderlich, wenn Sie auf anderer Hardware oder ein anderes Betriebssystem-Instanz wiederherstellen. Beachten Sie Folgendes:

- Die Anzahl Laufwerke auf dem Server muss gleich der Anzahl in der Sicherung werden und müssen identisch sein, Größe oder höher.
- Der Zielserver muss von der Betriebssystem-DVD gestartet werden, für den Zugriff auf die **Computer reparieren** Option. 
- Wenn das Ziel, das Domänencontroller auf einem virtuellen Computer auf Hyper-V und die Sicherung ausgeführt wird, an einem Netzwerkspeicherort gespeichert ist, müssen Sie eine ältere Netzwerkkarte installieren.  
- Nach der Durchführung einer vollständigen Wiederherstellungs müssen separat führen Sie eine autorisierende Wiederherstellung von SYSVOL, wie unter [AD-Gesamtstruktur-Wiederherstellung – führt eine autorisierende Synchronisation der DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).


In Abhängigkeit vom Szenario verwenden Sie eine der folgenden Verfahren zum Durchführen einer vollständigen Wiederherstellung.  
  
### <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>Führen Sie eine vollständige Server-Wiederherstellung mit einer lokalen Sicherung mit dem aktuellen Bild
  
1.  Starten Sie Windows Setup, geben Sie die Sprache, Uhrzeit und Währungsformat und Tastaturoptionen und klicken Sie auf **Weiter**.  
2.  Klicken Sie auf **Computer reparieren**.</br>
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3.  Klicken Sie auf **Problembehandlung**.</br>
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4.  Klicken Sie auf **Systemabbild-Wiederherstellung**.</br>
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5.  Klicken Sie auf **unter Windows Server 2016**.  
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6.  Wenn Sie die aktuelle lokale Sicherung wiederherstellen möchten, klicken Sie auf **verwenden Sie die neueste verfügbare Systemabbild (empfohlen)**, und klicken Sie auf **Weiter**.
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7.  Sie jetzt die Möglichkeit haben:
    -  Datenträger formatieren und neu partitionieren
    -  Installieren von Treibern
    -  Deaktivieren der **erweitert** Features von automatisch neu gestartet und das Überprüfen auf Festplattenfehler.  Diese sind standardmäßig aktiviert.
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. Klicken Sie auf **Weiter**.
9. Klicken Sie auf **Fertig stellen**.  Sie werden gefragt, ob Sie sind sicher, dass Sie den Vorgang fortsetzen aufgefordert werden.  Klicken Sie auf **Ja**.  
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. Nachdem dies abgeschlossen ist, führen eine autorisierende Wiederherstellung von SYSVOL, wie unter [AD-Gesamtstruktur-Wiederherstellung – führt eine autorisierende Synchronisation der DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).
 

### <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>Führen Sie eine vollständige Server-Wiederherstellung mit jedem Bild lokal oder remote
1.  Starten Sie Windows Setup, geben Sie die Sprache, Uhrzeit und Währungsformat und Tastaturoptionen und klicken Sie auf **Weiter**.  
2.  Klicken Sie auf **Computer reparieren**.</br>
3.  Klicken Sie auf **Problembehandlung**, klicken Sie auf **Systemabbild-Wiederherstellung**, und klicken Sie auf **Windows Server2016**.  
4.  Wenn Sie die aktuelle lokale Sicherung wiederherstellen möchten, klicken Sie auf **wählen Sie ein Systemabbild**, und klicken Sie auf **Weiter**.

5.  Jetzt können Sie den Speicherort für die Sicherung auswählen, die Sie wiederherstellen möchten.  Wenn das Bild lokalen ist, können Sie es aus der Liste auswählen.  
6.  Wenn das Bild auf einer Netzwerkfreigabe ist, wählen Sie **erweitert**.  Sie können auch auswählen, **erweitert** Wenn Sie einen Treiber installieren möchten.
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7.  Wenn Sie über das Netzwerk nach dem Klicken auf Wiederherstellen **erweitert** wählen **suchen Sie nach einem Systemabbild im Netzwerk**.  Sie möglicherweise aufgefordert, um die Netzwerkkonnektivität wiederherzustellen.  Wählen Sie Ok. </br>
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. Geben Sie den UNC-Pfad auf den Speicherort der Sicherung Freigabe (z.B. \\\server1\backups), und klicken Sie auf **OK**.  Sie können auch die IP-Adresse des Zielservers, z.B. \\\192.168.1.3\backups eingeben.  
![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
10. Geben Sie Anmeldeinformationen erforderlich, um Zugriff auf die Freigabe, und klicken Sie auf OK.  
11. Jetzt **wählen Sie Datum und Uhrzeit der Systemabbild wiederherstellen**, und klicken Sie auf **Weiter**.
12. Sie jetzt die Möglichkeit haben:
    1.   Datenträger formatieren und neu partitionieren
    2.   Installieren von Treibern
    3.   Deaktivieren der **erweitert** Features von automatisch neu gestartet und das Überprüfen auf Festplattenfehler.  Diese sind standardmäßig aktiviert.
13. Klicken Sie auf **Weiter**.
14. Klicken Sie auf **Fertig stellen**.  Sie werden gefragt, ob Sie sind sicher, dass Sie den Vorgang fortsetzen aufgefordert werden.  Klicken Sie auf **Ja**.   
15. Nachdem dies abgeschlossen ist, führen eine autorisierende Wiederherstellung von SYSVOL, wie unter [AD-Gesamtstruktur-Wiederherstellung – führt eine autorisierende Synchronisation der DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).


### <a name="enabling-the-network-adapter-for-a-network-backup"></a>Aktivieren den Netzwerkadapter für eine netzwerksicherung
Wenn Sie einen Netzwerkadapter über die Befehlszeile zum Wiederherstellen von einer Netzwerkfreigabe aktivieren möchten, verwenden Sie die folgenden Schritteaus.

1.  Starten Sie Windows Setup, geben Sie die Sprache, Uhrzeit und Währungsformat und Tastaturoptionen und klicken Sie auf **Weiter**.  
2.  Klicken Sie auf **Computer reparieren**. Ich
3.  Klicken Sie auf **Problembehandlung**, klicken Sie auf **Eingabeaufforderung**.  
4.  Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
  
    ```  
    wpeinit  
    ```   
5.  Um den Namen des Netzwerkadapters zu bestätigen, geben Sie Folgendes ein:  
  
    ```  
    show interfaces  
    ```  
  
     Geben Sie die folgenden Befehle ein, und drücken Sie nach jedem Befehl die EINGABETASTE:  
  
    ```  
    netsh  
    ```  
  
    ```  
    interface  
    ```  
  
    ```  
    tcp  
    ```  
  
    ```  
    ipv4  
    ```  
  
    ```  
    set address "Name of Network Adapter" static IPv4 Address SubnetMask IPv4 Gateway Address 1  
    ```  
  
     Zum Beispiel:  
  
    ```  
    set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
    ```  
  
     Typ `quit`in einem Eingabeaufforderungsfenster zurückgegeben. Typ `ipconfig /all`Adapter So überprüfen Sie das Netzwerk verfügt, eine IP-Adresse und versuchen Sie, ein Pingsignal an die IP-Adresse des Servers senden, die die Sicherung Freigabe, um Konnektivität zu bestätigen. Schließen Sie die Befehlszeile, wenn Sie fertig sind.  
  
6.  Nun, dass der Netzwerkadapter funktioniert, wählen Sie die oben beschriebenen Schrittezum Abschluss der Wiederherstellung.

## <a name="next-steps"></a>Nächste Schritte

- [AD-Gesamtstruktur für die Wiederherstellung](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der Active Directory-Gesamtstruktur - Verfahren](AD-Forest-Recovery-Procedures.md)
