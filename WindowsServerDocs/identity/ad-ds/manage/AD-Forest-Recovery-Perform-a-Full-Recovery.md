---
title: 'AD-Gesamtstruktur Wiederherstellung: Ausführen einer vollständigen Server Wiederherstellung'
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 1a1182a6-4462-4a13-806e-0e642a0d5db2
ms.technology: identity-adds
ms.openlocfilehash: bf321ae769aa6f0da1cebce7700ea429161a0956
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80824013"
---
# <a name="ad-forest-recovery---performing-a-full-server-recovery"></a>AD-Gesamtstruktur Wiederherstellung: Ausführen einer vollständigen Server Wiederherstellung 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um eine vollständige Server Wiederherstellung für Windows Server 2016, 2012 R2 oder 2012 auszuführen. 

## <a name="active-directory-full-server-recovery"></a>Active Directory vollständige Server Wiederherstellung

Eine vollständige Server Wiederherstellung ist erforderlich, wenn Sie auf einer anderen Hardware oder einer anderen Betriebssystem Instanz wiederherstellen. Beachten Sie folgende Punkte:

- Die Anzahl der Laufwerke auf dem Zielserver muss gleich der Anzahl in der Sicherung sein, und Sie müssen dieselbe Größe oder höher aufweisen.
- Der Zielserver muss über die DVD des Betriebssystems gestartet werden, um auf die Option **Computer reparieren** zugreifen zu können. 
- Wenn der Zieldomänen Controller auf einem virtuellen Computer unter Hyper-V ausgeführt wird und die Sicherung an einem Netzwerk Speicherort gespeichert ist, müssen Sie einen älteren Netzwerkadapter installieren. 
- Nachdem Sie eine vollständige Server Wiederherstellung durchgeführt haben, müssen Sie eine autoritative Wiederherstellung von SYSVOL ausführen, wie unter Active Directory-Gesamtstruktur [Wiederherstellung: Durchführen einer autorisierenden Synchronisierung von DFSR-replizierter SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)beschrieben.

Verwenden Sie je nach Szenario eines der folgenden Verfahren, um eine vollständige Wiederherstellung auszuführen. 
  
## <a name="perform-a-full-server-restore-with-a-local-backup-with-the-latest-image"></a>Ausführen einer vollständigen Server Wiederherstellung mit einer lokalen Sicherung mit dem neuesten Image
  
1. Starten Sie Windows Setup, geben Sie die Sprache, das Zeit-und Währungs Format und die Tastatur Optionen an, und klicken Sie auf **weiter**. 
2. Klicken Sie auf **Computer reparieren**.
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore1.png)
3. Klicken Sie auf **Problembehandlung**.</br>
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore2.png)
4. Klicken Sie auf **System Image Recovery**.</br>
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore3.png)
5. Klicken Sie auf **Windows Server 2016**. 
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore4.png)
6. Wenn Sie die letzte lokale Sicherung wiederherstellen, klicken Sie auf **das neueste verfügbare System Abbild verwenden (empfohlen)** , und klicken Sie auf **weiter**.
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore5.png)
7. Sie erhalten nun eine Option für Folgendes:
   -  Datenträger formatieren und neu partitionieren
   -  Treiber installieren
   -  Deaktivieren Sie die **erweiterten** Features der automatischen Neustarts und der Überprüfung auf Datenträger Fehler. Diese sind standardmäßig aktiviert.
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore6.png)
8. Klicken Sie auf **Weiter**.
9. Klicken Sie auf **Fertig stellen**. Sie werden gefragt, ob Sie den Vorgang fortsetzen möchten. Klicken Sie auf **Ja**. 
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore11.png) 
10. Nachdem dies abgeschlossen ist, führen Sie eine autoritative Wiederherstellung von SYSVOL aus, wie unter [AD Forest Recovery-durchführen einer autorisierenden Synchronisierung von DFSR-replizierten SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)beschrieben.

## <a name="perform-a-full-server-restore-with-any-image-local-or-remote"></a>Ausführen einer vollständigen Server Wiederherstellung mit einem beliebigen Image (lokal oder Remote)

1. Starten Sie Windows Setup, geben Sie die Sprache, das Zeit-und Währungs Format und die Tastatur Optionen an, und klicken Sie auf **weiter**. 
2. Klicken Sie auf **Computer reparieren**.</br>
3. Klicken Sie auf Problem **Behandlung, auf** **System Abbild-Wiederherstellung**und dann auf **Windows Server 2016**. 
4. Wenn Sie die letzte lokale Sicherung wiederherstellen, klicken Sie auf **System Abbild auswählen** , und klicken Sie auf **weiter**.
5. Nun können Sie den Speicherort der Sicherung auswählen, die Sie wiederherstellen möchten. Wenn das Bild lokal ist, können Sie es in der Liste auswählen. 
6. Wenn sich das Abbild auf einer Netzwerkfreigabe befindet, wählen Sie **erweitert**aus. Sie können auch **erweitert** auswählen, wenn Sie einen Treiber installieren müssen.
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore7.png)
7. Wenn Sie nach dem Klicken auf **erweitert** über das Netzwerk wiederherstellen, wählen Sie **im Netzwerk nach einem System Abbild suchen**aus. Möglicherweise werden Sie aufgefordert, die Netzwerk Konnektivität wiederherzustellen. Wählen Sie OK aus. </br>
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore8.png)
8. Geben Sie den UNC-Pfad zum Speicherort der Sicherungs Freigabe ein (z. b. \\\server1\backups), und klicken Sie auf **OK**. Sie können auch die IP-Adresse des Zielservers eingeben, z. b. \\\192.168.1.3\backups. 
   ![Server Wiederherstellung](media/AD-Forest-Recovery-Perform-a-Full-Recovery/restore9.png)
9. Geben Sie die Anmelde Informationen ein, die für den Zugriff auf die Freigabe erforderlich sind 
10. **Wählen Sie jetzt das Datum und die Uhrzeit für die Wiederherstellung des System Images aus,** und klicken Sie auf **weiter**
11. Sie erhalten nun eine Option für Folgendes:
    - Datenträger formatieren und neu partitionieren
    - Treiber installieren
    - Deaktivieren Sie die **erweiterten** Features der automatischen Neustarts und der Überprüfung auf Datenträger Fehler. Diese sind standardmäßig aktiviert.
12. Klicken Sie auf **Weiter**.
13. Klicken Sie auf **Fertig stellen**. Sie werden gefragt, ob Sie den Vorgang fortsetzen möchten. Klicken Sie auf **Ja**.  
14. Nachdem dies abgeschlossen ist, führen Sie eine autoritative Wiederherstellung von SYSVOL aus, wie unter [AD Forest Recovery-durchführen einer autorisierenden Synchronisierung von DFSR-replizierten SYSVOL](AD-Forest-Recovery-Authoritative-Recovery-SYSVOL.md)beschrieben.

## <a name="enabling-the-network-adapter-for-a-network-backup"></a>Aktivieren des Netzwerkadapters für eine Netzwerk Sicherung

Wenn Sie einen Netzwerkadapter von der Eingabeaufforderung aus für die Wiederherstellung über eine Netzwerkfreigabe aktivieren müssen, führen Sie die folgenden Schritte aus.

1. Starten Sie Windows Setup, geben Sie die Sprache, das Zeit-und Währungs Format und die Tastatur Optionen an, und klicken Sie auf **weiter**. 
2. Klicken Sie auf **Computer reparieren**. I
3. Klicken Sie auf Problem **Behandlung und dann auf** **Eingabeaufforderung**. 
4. Geben Sie den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  

   ```  
   wpeinit  
   ```

5. Geben Sie Folgendes ein, um den Namen des Netzwerkadapters zu bestätigen:  

   ```  
   show interfaces  
   ```  

   Geben Sie folgende Befehle ein, und drücken Sie nach jedem Befehl die EINGABETASTE:  

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

   Beispiel:  
  
   ```  
   set address "Local Area Connection" static 192.168.1.2 255.0.0.0 192.168.1.1 1  
   ```  

   Geben Sie `quit` ein, um zu einer Eingabeaufforderung zurückzukehren. Geben Sie `ipconfig /all` ein, um zu überprüfen, ob der Netzwerkadapter über eine IP-Adresse verfügt, und versuchen Sie, die IP-Adresse des Servers, der die Sicherungs Freigabe hostet, zu Schließen Sie die Eingabeaufforderung, wenn Sie den Vorgang abgeschlossen haben. 

6. Nachdem der Netzwerkadapter ordnungsgemäß funktioniert, wählen Sie die obigen Schritte aus, um die Wiederherstellung abzuschließen.

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
