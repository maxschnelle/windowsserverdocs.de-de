---
title: 'AD-Gesamtstruktur-Wiederherstellung: Ausführen einer vollständigen Wiederherstellungs'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adds
ms.openlocfilehash: 9cf89c9f4875f602abea89e366cadfba8d0599c3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443010"
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD-Gesamtstruktur-Wiederherstellung: Ausführen einer vollständigen Wiederherstellungs 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren zum Ausführen einer vollständigen Wiederherstellungs für Windows Server 2016, 2012 R2 oder 2012 aus. 

## <a name="active-directory-full-server-recovery"></a>Active Directory vollständigen Serverwiederherstellung

Eine vollständige Wiederherstellung des Servers ist erforderlich, wenn Sie unterschiedliche Hardware- oder einer anderen Instanz wiederherstellen. Beachten Sie folgende Punkte:

- Die Anzahl der Ziel-Server muss gleich der Anzahl in der Sicherung werden Laufwerke und müssen identisch sein, Größe oder höher.
- Der Zielserver muss über das Betriebssystem gestartet werden, um Zugriff auf die **Computer reparieren** Option. 
- Wenn das Ziel, die, das Domänencontroller auf einem virtuellen Computer auf Hyper-V und die Sicherung ausgeführt wird, an einem Netzwerkspeicherort gespeichert ist, müssen Sie eine ältere Netzwerkkarte installieren. 
- Nach dem Durchführen einer vollständigen Wiederherstellungs müssen separat führen Sie eine autorisierende Wiederherstellung von SYSVOL, siehe [AD-Gesamtstruktur-Wiederherstellung: Ausführen einer autoritativen Synchronisierung des DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).

Je nach Szenario verwenden Sie eine der folgenden Verfahren zum Ausführen einer vollständigen Wiederherstellung aus. 
  
## <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>Ausführen einer vollständigen Wiederherstellung mit einer lokalen Sicherung mit dem aktuellen image
  
1. Starten Sie Windows Setup, geben Sie die Sprache, Uhrzeit und Währungsformat und Tastaturoptionen aus, und klicken Sie auf **Weiter**. 
2. Klicken Sie auf **Computer reparieren**.
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3. Klicken Sie auf **Problembehandlung**.</br>
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4. Klicken Sie auf **Systemabbild-Wiederherstellung**.</br>
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5. Klicken Sie auf **WindowsServer 2016**. 
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6. Wenn Sie die aktuelle lokale Sicherung wiederherstellen möchten, klicken Sie auf **verwenden Sie die neueste verfügbare Systemabbild (empfohlen)** , und klicken Sie auf **Weiter**.
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7. Sie werden jetzt eine Option aus, um angegeben werden:
   -  Datenträger formatieren und neu partitionieren
   -  Installieren von Treibern
   -  Deaktivieren Sie das Kontrollkästchen der **erweitert** Funktionen automatisch neu zu starten und die Überprüfung auf Fehler auf den Datenträger. Diese sind standardmäßig aktiviert.
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. Klicken Sie auf **Weiter**.
9. Klicken Sie auf **Fertig stellen**. Sie werden aufgefordert werden, stellen Sie sicher, dass Sie den Vorgang fortsetzen möchten. Klicken Sie auf **Ja**. 
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. Sobald dies abgeschlossen ist, führen eine autorisierende Wiederherstellung von SYSVOL, siehe [AD-Gesamtstruktur-Wiederherstellung: Ausführen einer autoritativen Synchronisierung des DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).

## <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>Ausführen einer vollständigen Wiederherstellung durch jedes Bild lokal oder remote

1. Starten Sie Windows Setup, geben Sie die Sprache, Uhrzeit und Währungsformat und Tastaturoptionen aus, und klicken Sie auf **Weiter**. 
2. Klicken Sie auf **Computer reparieren**.</br>
3. Klicken Sie auf **Problembehandlung**, klicken Sie auf **Systemabbild-Wiederherstellung**, und klicken Sie auf **Windows Server 2016**. 
4. Wenn Sie die aktuelle lokale Sicherung wiederherstellen möchten, klicken Sie auf **Systemabbild auswählen** , und klicken Sie auf **Weiter**.
5. Jetzt können Sie den Speicherort der Sicherung auswählen, die Sie wiederherstellen möchten. Wenn das Bild lokal ist, können Sie es aus der Liste auswählen. 
6. Wenn das Bild auf einer Netzwerkfreigabe ist, wählen Sie **erweitert**. Sie können auch auswählen, **erweitert** einen Treiber installiert werden sollen.
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7. Wenn Sie über das Netzwerk nach dem Klicken auf Wiederherstellen **erweitert** wählen **Suche nach einem Systemabbild im Netzwerk**. Sie werden möglicherweise aufgefordert, die Netzwerkkonnektivität wiederherzustellen. Wählen Sie Ok. </br>
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. Geben Sie den UNC-Pfad zum Speicherort Sicherungsfreigabe (z. B. \\\server1\backups), und klicken Sie auf **OK**. Sie können auch die IP-Adresse des Zielservers, eingeben, z. B. \\\192.168.1.3\backups. 
   ![Wiederherstellung des Servers](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
9. Geben Sie Anmeldeinformationen zum Zugreifen auf die Freigabe, und klicken Sie auf OK. 
10. Jetzt **wählen Sie Datum und Uhrzeit der Systemabbild wiederherzustellenden** , und klicken Sie auf **Weiter**.
11. Sie werden jetzt eine Option aus, um angegeben werden:
    - Datenträger formatieren und neu partitionieren
    - Installieren von Treibern
    - Deaktivieren Sie das Kontrollkästchen der **erweitert** Funktionen automatisch neu zu starten und die Überprüfung auf Fehler auf den Datenträger. Diese sind standardmäßig aktiviert.
12. Klicken Sie auf **Weiter**.
13. Klicken Sie auf **Fertig stellen**. Sie werden aufgefordert werden, stellen Sie sicher, dass Sie den Vorgang fortsetzen möchten. Klicken Sie auf **Ja**.  
14. Sobald dies abgeschlossen ist, führen eine autorisierende Wiederherstellung von SYSVOL, siehe [AD-Gesamtstruktur-Wiederherstellung: Ausführen einer autoritativen Synchronisierung des DFSR-repliziertes SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md).

## <a name="enabling-the-network-adapter-for-a-network-backup"></a>Aktivieren den Netzwerkadapter für eine netzwerksicherung

Wenn Sie einen Netzwerkadapter an der Eingabeaufforderung zum Wiederherstellen von einer Netzwerkfreigabe aktivieren müssen, verwenden Sie die folgenden Schritte aus.

1. Starten Sie Windows Setup, geben Sie die Sprache, Uhrzeit und Währungsformat und Tastaturoptionen aus, und klicken Sie auf **Weiter**. 
2. Klicken Sie auf **Computer reparieren**. I
3. Klicken Sie auf **Problembehandlung**, klicken Sie auf **Eingabeaufforderung**. 
4. Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   ```  
   wpeinit  
   ```

5. Um den Namen des Netzwerkadapters zu bestätigen, geben Sie Folgendes ein:  

   ```  
   show interfaces  
   ```  

   Geben Sie die folgenden Befehle aus, und drücken Sie nach jedem Befehl die EINGABETASTE:  

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

   Typ `quit` um an einer Eingabeaufforderung zurückzugeben. Typ `ipconfig /all` um zu überprüfen, ob das Netzwerk Adapter verfügt über eine IP-Adresse und versuchen Sie es aus, um die IP-Adresse des Servers zu pingen, die die Sicherungsfreigabe, um die Konnektivität überprüfen hostet. Schließen Sie die Eingabeaufforderung aus, wenn Sie fertig sind. 

6. Nun, dass der Netzwerkadapter funktioniert, wählen Sie die Schritte oben zum Abschließen des Wiederherstellungsvorgangs.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
