---
title: Konfigurieren von WEB1 zum Verteilen von Zertifikat Sperr Listen (CRLs)
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: fa4a8c41-8c2a-425c-8511-736fe5d196ac
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 3319715e70c1e68739a10a4c67a9fa404d5ad80e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318417"
---
# <a name="configure-web1-to-distribute-certificate-revocation-lists-crls"></a>Konfigurieren von WEB1 zum Verteilen von Zertifikat Sperr Listen (CRLs)

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mithilfe dieses Verfahrens können Sie den Webserver WEB1 für die Verteilung von CRLs konfigurieren.  
  
In den Erweiterungen der Stamm Zertifizierungsstelle wurde festgestellt, dass die CRL der Stamm Zertifizierungsstelle über https://pki.corp.contoso.com/pkiverfügbar wäre. Zurzeit ist kein virtuelles PKI-Verzeichnis auf WEB1 vorhanden, daher muss eine erstellt werden.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe " **Domänen-Admins**" sein.  
  
> [!NOTE]  
> Ersetzen Sie im folgenden Verfahren den Benutzerkonto Namen, den Webserver Namen, die Ordnernamen und-Speicherorte sowie andere Werte durch die Werte, die für Ihre Bereitstellung geeignet sind.  
  
#### <a name="to-configure-web1-to-distribute-certificates-and-crls"></a>So konfigurieren Sie WEB1 für die Verteilung von Zertifikaten und CRLs  
  
1.  Führen Sie auf WEB1 Windows PowerShell als Administrator aus, geben Sie `explorer c:\`ein, und drücken Sie dann die EINGABETASTE. Windows-Explorer wird mit Laufwerk C geöffnet.   
  
2.  Erstellen Sie auf Laufwerk C: einen neuen Ordner mit dem Namen PKI. Klicken Sie hierzu auf **Startseite**, und klicken Sie dann auf **neuer Ordner**. Es wird ein neuer Ordner erstellt, in dem der temporäre Name hervorgehoben ist. Geben Sie **PKI** ein, und drücken Sie die EINGABETASTE  
  
3.  Klicken Sie in Windows Explorer mit der rechten Maustaste auf den soeben erstellten Ordner, zeigen Sie mit dem Mauszeiger auf die **Freigabe**, und klicken Sie dann auf **bestimmte Personen**. Das Dialogfeld **Dateifreigabe** wird geöffnet.  
  
4.  Geben Sie in **Dateifreigabe** **Zertifikat**Herausgeber ein, und klicken Sie dann auf **Hinzufügen**. Die Gruppe Zertifikat Herausgeber wird der Liste hinzugefügt. Klicken Sie in der Liste unter **Berechtigungsstufe**auf den Pfeil neben **Zertifikat**Herausgeber, und klicken Sie dann auf **Lesen/Schreiben**. Klicken Sie auf **Freigeben**und dann auf **done**.  
  
5.  Schließen Sie Windows-Explorer.  
  
6.  Öffnen Sie die IIS-Konsole. Klicken Sie im Server-Manager auf **Extras** und anschließend auf **Internetinformationsdienste-Manager**.  
  
7.  Erweitern Sie in der Konsolen Struktur Internetinformationsdienste (IIS)-Manager den Eintrag **WEB1**. Wenn Sie gefragt werden, ob Sie mit Microsoft-Webplattform beginnen möchten, klicken Sie auf **Abbrechen**.  
  
8.  Erweitern Sie **Websites**, klicken Sie mit der rechten Maustaste auf **Default Web Site**, und klicken Sie dann auf **Virtuelles Verzeichnis hinzufügen**.  
  
9. Geben **Alias**Sie als Alias **PKI**ein. Geben Sie unter **physischer Pfad** **c:\pki**ein, und klicken Sie dann auf **OK**.  
  
10. Aktivieren Sie den anonymen Zugriff auf das virtuelle PKI-Verzeichnis, sodass jeder Client die Gültigkeit der Zertifizierungsstellen Zertifikate und CRLs überprüfen kann. Gehen Sie hierzu wie folgt vor:  
  
    1.  Stellen Sie im Bereich **Verbindungen** sicher, dass **pki** ausgewählt ist.  
  
    2.  Klicken Sie in **pki-Startseite** auf **Authentifizierung**.  
  
    3.  Klicken Sie im Bereich **Aktionen** auf **Berechtigungen bearbeiten**.  
  
    4.  Klicken Sie auf der Registerkarte **Sicherheit** auf **Bearbeiten**.  
  
    5.  Klicken Sie im Dialogfeld **Berechtigungen für pki** auf **Hinzufügen**.  
  
    6.  Geben **Sie unter Benutzer, Computer, Dienst Konten oder Gruppen auswählen** **Anonyme Anmeldung ein. Und klicken** Sie dann auf **Namen überprüfen**. Klicken Sie auf **OK**.  
  
    7.  Klicken Sie im Dialogfeld **Benutzer, Computer, Dienst Konten oder Gruppen auswählen** auf **OK** .  
  
    8.  Klicken Sie im Dialogfeld **Berechtigungen für PKI** auf **OK** .  
  
11. Klicken Sie im Dialogfeld **PKI-Eigenschaften** auf **OK** .  
  
12. Doppelklicken Sie im Bereich **pki-Startseite** auf **Anforderungsfilterung**.  
  
13. Im Bereich **Anforderungsfilterung** ist die Registerkarte **Dateinamenerweiterungen** standardmäßig ausgewählt. Klicken Sie im Bereich **Aktionen** auf **Featureeinstellungen bearbeiten**.  
  
14. Wählen Sie unter **Einstellungen für die Anforderungsfilterung bearbeiten** die Option **Doppelte Escapezeichen zulassen** aus, und klicken Sie dann auf **OK**.  
  
15. Klicken Sie im Internetinformationsdienste (IIS)-Manager-MMC auf den Namen Ihres Webservers. Wenn der Webserver z. b. den Namen WEB1 hat, klicken Sie auf **WEB1**.  
  
16. Klicken Sie unter **Aktionen**auf **neu starten**. Internet Dienste werden beendet und dann neu gestartet.  
  

