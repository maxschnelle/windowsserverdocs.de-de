---
title: Konfigurieren von WEB1 zum Verteilen von Zertifikatsperrlisten (CRLs)
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: fa4a8c41-8c2a-425c-8511-736fe5d196ac
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: b96fad769638de9835c52137e5165fa32a6b9bd4
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="configure-web1-to-distribute-certificate-revocation-lists-crls"></a>Konfigurieren von WEB1 zum Verteilen von Zertifikatsperrlisten (CRLs)

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie den Webserver WEB1 zum Verteilen von Zertifikatssperrlisten konfigurieren.  
  
In den Stamm-CA-Erweiterungen wurde angegeben, dass die Zertifikatsperrliste der Stammzertifizierungsstelle über wäre http://pki.corp.contoso.com/pki. Derzeit ist kein virtuelles PKI-Verzeichnis auf WEB1 so muss es erstellt werden.  
  
Zum Ausführen dieses Verfahrens müssen Sie Mitglied der sein **Domänen-Admins**.  
  
> [!NOTE]  
> Ersetzen Sie in den folgenden Schritten den Namen des Benutzerkontos, der Name des Webservers, Ordnernamen und Speicherorte und andere Werte durch die für Ihre Bereitstellung geeignet sind.  
  
#### <a name="to-configure-web1-to-distribute-certificates-and-crls"></a>So konfigurieren Sie WEB1 zum Verteilen von Zertifikaten und Zertifikatsperrlisten  
  
1.  Geben Sie auf WEB1, führen Sie Windows PowerShell als Administrator, `explorer c:\`, und drücken Sie dann die EINGABETASTE. Windows Explorer geöffnet wird, auf Laufwerk c:.   
  
2.  Erstellen Sie einen neuen Ordner mit dem Namen PKI auf dem Laufwerk "c:". Klicken Sie hierzu auf **Home**, und klicken Sie dann auf **neuen Ordner**. Mit dem temporären Namen hervorgehoben ist ein neuer Ordner erstellt. Typ **Pki** und drücken Sie dann die EINGABETASTE.  
  
3.  In Windows-Explorer Maustaste auf den Ordner, die Sie gerade erstellt haben, und bewegen Sie den Mauszeiger über **freigeben**, und klicken Sie dann auf **bestimmte Personen**. Die **Dateifreigabe** Dialogfeld wird geöffnet.  
  
4.  In **Dateifreigabe**, Typ **Zertifikatherausgeber**, und klicken Sie dann auf **hinzufügen**. Die Gruppe "Zertifikatherausgeber" wird der Liste hinzugefügt. In der Liste in **Berechtigungsstufe**, klicken Sie auf den Pfeil neben **Zertifikatherausgeber**, und klicken Sie dann auf **Lese-/Schreibzugriff**. Klicken Sie auf **Freigabe**, und klicken Sie dann auf **Fertig**.  
  
5.  Schließen Sie Windows_explorer.  
  
6.  Öffnen Sie die IIS-Konsole. Klicken Sie im Server-Manager auf **Tools**, und klicken Sie dann auf **(Internet Information Services, IIS) Manager**.  
  
7.  Erweitern Sie in der Konsolenstruktur von Internetinformationsdienste (Internet Information Services, IIS) Manager **WEB1**. Wenn Sie gefragt werden, die mit Microsoft-Webplattform beginnen, klicken Sie auf **Abbrechen**.  
  
8.  Erweitern Sie **Sites** klicken Sie dann mit der rechten Maustaste die **Default Web Site** , und klicken Sie dann auf **virtuelles Verzeichnis hinzufügen**.  
  
9. In **Alias**, Typ **Pki**. In **physischen Pfad** Typ **C:\pki**, klicken Sie dann auf **OK**.  
  
10. Aktivieren Sie den anonymen Zugriff auf das virtuelle Pki-Verzeichnis, sodass alle Clients die Gültigkeit der ZS-Zertifikate und Zertifikatsperrlisten überprüfen kann. Dazu:  
  
    1.  In der **Verbindungen** Bereich sicher, dass **Pki** ausgewählt ist.  
  
    2.  Auf **Pki-Startseite** klicken Sie auf **Authentifizierung**.  
  
    3.  In der **Aktionen** Bereich, klicken Sie auf **Berechtigungen zum Bearbeiten von**.  
  
    4.  Auf der **Security** auf **bearbeiten**  
  
    5.  Auf der **Berechtigungen für Pki** Dialogfeld, klicken Sie auf **hinzufügen**.  
  
    6.  In der **Benutzer, Computer, Dienstkonten oder Gruppen**, Typ **ANONYMOUS-Anmeldung; Jeder** , und klicken Sie dann auf **Namen überprüfen**. Klicken Sie auf **OK**.  
  
    7.  Klicken Sie auf **OK** auf die **Benutzer, Computer, Dienstkonten oder Gruppen auswählen** Dialogfeld.  
  
    8.  Klicken Sie auf **OK** auf die **Berechtigungen für Pki** Dialogfeld.  
  
11. Klicken Sie auf **OK** auf die **Pki Eigenschaften** Dialogfeld.  
  
12. In der **Pki-Startseite** Bereich, doppelklicken Sie auf **Anforderungsfilterung**.  
  
13. Die **Dateinamenerweiterungen** Registerkarte ist standardmäßig ausgewählt, in der **Anforderungsfilterung** Bereich. In der **Aktionen** Bereich, klicken Sie auf **Featureeinstellungen bearbeiten**.  
  
14. In **bearbeiten Einstellungen für die Anforderungsfilterung**Option **doppelte Escapezeichen zulassen** , und klicken Sie dann auf **OK**.  
  
15. Klicken Sie in der MMC-Manager (Internet Information Services, IIS) auf den Namen des Webservers. Z. B. wenn Webservers WEB1 lautet, klicken Sie auf **WEB1**.  
  
16. In **Aktionen**, klicken Sie auf **neu starten**. Internet-Dienste beendet und neu gestartet.  
  

