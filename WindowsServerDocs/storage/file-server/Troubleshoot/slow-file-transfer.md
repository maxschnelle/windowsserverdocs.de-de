---
title: Langsame Übertragungsgeschwindigkeit bei SMB-Dateien
description: Erläutert die Behandlung von Problemen bei der Übertragung von SMB-Dateien.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: af05daa164b5b2c5eca73eff51d97d4c25ba1ca3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80815393"
---
# <a name="slow-smb-files-transfer-speed"></a>Langsame Übertragungsgeschwindigkeit bei SMB-Dateien

Dieser Artikel enthält empfohlene Vorgehensweisen zur Problembehandlung bei langsamen Übertragungsgeschwindigkeiten durch SMB.

## <a name="large-file-transfer-is-slow"></a>Große Dateiübertragungen ist langsam

Wenn Sie langsame Übertragungen großer Dateien bemerken, sollten Sie die folgenden Schritte ausführen:

- Verwenden Sie den Befehl zum Kopieren von Dateien für nicht gepufferte e/a (**xcopy/J** oder **Robocopy/J**).

- Testen Sie die Speichergeschwindigkeit. Dies liegt daran, dass die Geschwindigkeit der Datei Kopien durch die Speichergeschwindigkeit eingeschränkt ist.

- Datei Kopien werden manchmal schnell gestartet und dann verlangsamt. Befolgen Sie diese Richtlinien, um diese Situation zu überprüfen
    
  - Dies tritt normalerweise auf, wenn die anfängliche Kopie zwischengespeichert oder gepuffert wird (entweder im Arbeitsspeicher oder im Arbeitsspeicher Cache des RAID-Controllers) und der Cache abläuft. Dadurch wird erzwungen, dass Daten direkt auf den Datenträger geschrieben werden (durch Schreiben). Dies ist ein langsamer Vorgang.
    
  - Verwenden Sie die Speicher Leistungsindikatoren, um zu bestimmen, ob die Speicherleistung im Zeitverlauf beeinträchtigt wird. Weitere Informationen finden Sie unter [Leistungsoptimierung für SMB-Dateiserver](https://docs.microsoft.com/windows-server/administration/performance-tuning/role/file-server/smb-file-server).

- Verwenden Sie rammap (Sysinternals), um zu bestimmen, ob die Nutzung von "zugeordneten Dateien" im Arbeitsspeicher aufgrund der freien Speicherauslastung nicht mehr zunimmt.

- Suchen Sie nach Paketverlust in der Ablauf Verfolgung. Dies kann eine Drosselung durch den TCP-Überlastungs Anbieter zur Ursache haben.

- Stellen Sie für SMBv3 und spätere Versionen sicher, dass SMB Multichannel aktiviert ist und funktioniert.

- Aktivieren Sie auf dem SMB-Client große MTU in SMB, und deaktivieren Sie die Bandbreitendrosselung. Führen Sie hierzu den folgenden Befehl aus:  
  
  ```PowerShell
  Set-SmbClientConfiguration -EnableBandwidthThrottling 0 -EnableLargeMtu 1
  ```

## <a name="small-file-transfer-is-slow"></a>Kleine Dateiübertragung ist langsam

Eine langsame Übertragung von kleinen Dateien über SMB erfolgt am häufigsten, wenn viele Dateien vorhanden sind. Dies ist ein erwartetes Verhalten.

Während der Dateiübertragung verursacht die Dateierstellung sowohl einen hohen Protokoll Aufwand als auch einen hohen Aufwand für das Dateisystem. Bei großen Dateiübertragungen treten diese Kosten nur einmal auf. Wenn eine große Anzahl von kleinen Dateien übertragen wird, werden die Kosten wiederholt und verursachen langsame Übertragungen.

Im folgenden finden Sie technische Details zu diesem Problem:

- SMB Ruft einen Create-Befehl auf, um anzufordern, dass die Datei erstellt werden soll. In einem Code wird überprüft, ob die Datei vorhanden ist, und dann wird die Datei erstellt. Oder eine Variation des create-Befehls erstellt die eigentliche Datei.

- Jeder Create-Befehl generiert Aktivitäten im Dateisystem.

- Nachdem die Daten geschrieben wurden, wird die Datei geschlossen.

- Seit einiger Zeit hat der Prozess von der Netzwerk Latenz und der SMB-Server Latenz eine gewisse Zeit. Dies liegt daran, dass die SMB-Anforderung zuerst in einen Dateisystem Befehl und dann in die tatsächliche Dateisystem Latenz übersetzt wird, um den Vorgang abzuschließen.

- Wenn ein Antivirenprogramm ausgeführt wird, wird die Übertragung noch weiter verlangsamt. Dies liegt daran, dass die Daten in der Regel einmal durch die Paket Ermittlung und ein zweites Mal gescannt werden, wenn Sie auf den Datenträger geschrieben wird. In einigen Szenarien werden diese Aktionen tausend Mal wiederholt. Möglicherweise beobachten Sie die Geschwindigkeit von weniger als 1 MB/s.

## <a name="opening-office-documents-is-slow"></a>Das Öffnen von Office-Dokumenten ist langsam

Dieses Problem tritt im Allgemeinen bei einer WAN-Verbindung auf. Dies ist häufig der Fall, der in der Regel durch die Art und Weise verursacht wird, in der Office-Apps (insbesondere Microsoft Excel) auf Daten zugreifen und diese lesen.

Es wird empfohlen, dass Sie sicherstellen, dass die Office-und SMB-Binärdateien auf dem neuesten Stand sind, und dann testen, ob das Leasing auf dem SMB-Server deaktiviert ist. Gehen Sie hierzu folgendermaßen vor:
   
1. Führen Sie den folgenden PowerShell-Befehl in Windows 8 und Windows Server 2012 oder höheren Versionen von Windows aus:
      
   ```PowerShell
   Set-SmbServerConfiguration -EnableLeasing $false  
   ```
      
   Oder führen Sie den folgenden Befehl in einem Eingabe Aufforderungs Fenster mit erhöhten Rechten aus:  

   ```cmd
   REG ADD HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\lanmanserver\parameters /v DisableLeasing /t REG\_DWORD /d 1 /f  
   ```
      
   > [!NOTE]
   > Nachdem Sie diesen Registrierungsschlüssel festgelegt haben, werden SMB2 Leases nicht mehr gewährt, aber es sind noch keine oplocks verfügbar. Diese Einstellung wird in erster Linie für die Problembehandlung verwendet.
    
2. Starten Sie den Dateiserver neu, oder starten Sie den **Server** Dienst neu. Um den Dienst neu zu starten, führen Sie die folgenden Befehle aus:

   ```cmd  
   NET STOP SERVER 
   NET START SERVER
   ```

Um dieses Problem zu vermeiden, können Sie die Datei auch auf einen lokalen Dateiserver replizieren. Weitere Informationen finden Sie unter [Überprüfen von Office-Dokumenten auf einem Netzwerkserver ist langsam bei der Verwendung von EFS](https://docs.microsoft.com/office/troubleshoot/office/saving-file-to-network-server-slow).
