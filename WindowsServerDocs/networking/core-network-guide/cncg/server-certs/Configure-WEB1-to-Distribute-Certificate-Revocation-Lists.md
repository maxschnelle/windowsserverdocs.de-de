---
title: Konfigurieren von WEB1 zum Verteilen von Zertifikatsperrlisten (CRLs)
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: fa4a8c41-8c2a-425c-8511-736fe5d196ac
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 57fa45eff87a1f0cdaae8b780d7f605e54ff6871
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839191"
---
# <a name="configure-web1-to-distribute-certificate-revocation-lists-crls"></a>Konfigurieren von WEB1 zum Verteilen von Zertifikatsperrlisten (CRLs)

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, so konfigurieren Sie den Webserver WEB1 zur Verteilung von Zertifikatsperrlisten.  
  
In den Erweiterungen der Stamm-ZS, wurde angegeben, dass die Zertifikatsperrliste der Stammzertifizierungsstelle über verfügbar wäre https://pki.corp.contoso.com/pki. Derzeit besteht kein virtuelles PKI-Verzeichnis auf WEB1 sodass muss es erstellt werden.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied werden **Domänen-Admins**.  
  
> [!NOTE]  
> Ersetzen Sie im folgenden Verfahren den Benutzerkontonamen, den Namen des Webservers, Ordnernamen und Speicherorte und andere Werte durch die für Ihre Bereitstellung geeignet sind.  
  
#### <a name="to-configure-web1-to-distribute-certificates-and-crls"></a>So konfigurieren Sie WEB1 zum Verteilen von Zertifikaten und Zertifikatsperrlisten  
  
1.  Geben Sie auf WEB1, führen Sie Windows PowerShell als Administrator `explorer c:\`, und drücken Sie dann die EINGABETASTE. Windows-Explorer wird geöffnet, auf Laufwerk c:.   
  
2.  Erstellen Sie einen neuen Ordner mit dem Namen PKI, auf dem Laufwerk "c:". Zu diesem Zweck klicken Sie auf **Startseite**, und klicken Sie dann auf **neuer Ordner**. Ein neuer Ordner wird mit den temporären Namen hervorgehoben erstellt. Typ **Pki** und drücken Sie dann die EINGABETASTE.  
  
3.  Im Windows-Explorer mit der Maustaste des Ordners, die Sie gerade erstellt haben, zeigen Sie den Mauszeiger auf **freigeben**, und klicken Sie dann auf **bestimmte Personen**. Das Dialogfeld **Dateifreigabe** wird geöffnet.  
  
4.  In **Dateifreigabe**, Typ **Zertifikatherausgeber**, und klicken Sie dann auf **hinzufügen**. Die Gruppe "Zertifikatherausgeber" wird zur Liste hinzugefügt. In der Liste der in **Berechtigungsebene**, klicken Sie auf den Pfeil neben **Zertifikatherausgeber**, und klicken Sie dann auf **Lese-/Schreibzugriff**. Klicken Sie auf **Freigabe**, und klicken Sie dann auf **Fertig**.  
  
5.  Schließen Sie Windows Explorer.  
  
6.  Öffnen Sie die IIS-Konsole. Klicken Sie in Server-Manager auf **Extras**, klicken Sie auf Verwaltung, und klicken Sie dann auf **Internetinformationsdienste-Manager**.  
  
7.  Erweitern Sie in der Konsolenstruktur von Internetinformationsdienste (Internet Information Services, IIS) Manager **WEB1**. Wenn Sie gefragt werden, ob Sie mit Microsoft-Webplattform beginnen möchten, klicken Sie auf **Abbrechen**.  
  
8.  Erweitern Sie **Websites**, klicken Sie mit der rechten Maustaste auf **Standardwebsite**, und klicken Sie dann auf **Virtuelles Verzeichnis hinzufügen**.  
  
9. In **Alias**, Typ **Pki**. In **physischer Pfad** Typ **C:\pki**, klicken Sie dann auf **OK**.  
  
10. Aktivieren Sie den anonymen Zugriff auf auf das virtuelle Pki-Verzeichnis, sodass alle Clients die Gültigkeit der ZS-Zertifikate und Zertifikatsperrlisten überprüfen kann. Gehen Sie hierzu wie folgt vor:  
  
    1.  Stellen Sie im Bereich **Verbindungen** sicher, dass **pki** ausgewählt ist.  
  
    2.  Klicken Sie in **pki-Startseite** auf **Authentifizierung**.  
  
    3.  Klicken Sie im Bereich **Aktionen** auf **Berechtigungen bearbeiten**.  
  
    4.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Bearbeiten**.  
  
    5.  Klicken Sie im Dialogfeld **Berechtigungen für pki** auf **Hinzufügen**.  
  
    6.  In der **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen**, Typ **ANONYMOUS-Anmeldung; Jeder** , und klicken Sie dann auf **Namen überprüfen**. Klicken Sie auf **OK**.  
  
    7.  Klicken Sie auf **OK** auf die **Auswahl von Benutzern, Computern, Dienstkonten oder Gruppen** Dialogfeld.  
  
    8.  Klicken Sie auf **OK** auf die **Berechtigungen für Pki** Dialogfeld.  
  
11. Klicken Sie auf **OK** auf die **Pki Eigenschaften** Dialogfeld.  
  
12. Doppelklicken Sie im Bereich **pki-Startseite** auf **Anforderungsfilterung**.  
  
13. Im Bereich **Anforderungsfilterung** ist die Registerkarte **Dateinamenerweiterungen** standardmäßig ausgewählt. Klicken Sie im Bereich **Aktionen** auf **Featureeinstellungen bearbeiten**.  
  
14. Wählen Sie unter **Einstellungen für die Anforderungsfilterung bearbeiten**die Option **Doppelte Escapezeichen zulassen** aus, und klicken Sie dann auf **OK**.  
  
15. Klicken Sie in der MMC (Internet Information Services, IIS) Manager auf den Namen des Webservers. Z. B. wenn der Webserver WEB1 benannt wird, klicken Sie auf **WEB1**.  
  
16. In **Aktionen**, klicken Sie auf **Neustart**. Internet-Dienste werden beendet und neu gestartet.  
  

