---
title: Bereitstellung von Serverzertifikaten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 751c5c5958b3d06ae0f4b701e4d6e10a7fef19dc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59858491"
---
# <a name="server-certificate-deployment"></a>Bereitstellung von Serverzertifikaten

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Führen Sie die folgenden Schritte aus, um eine Unternehmens-Stammzertifizierungsstelle (CA) installieren und Bereitstellen von Serverzertifikaten für die Verwendung mit PEAP und EAP.  
  
> [!IMPORTANT]  
> Vor der Installation von Active Directory Certificate Services müssen Sie den Computer benennen, konfigurieren Sie den Computer mit einer statischen IP-Adresse und fügen Sie den Computer der Domäne. Nach der Installation von AD CS können nicht Sie den Namen des Computers oder der Domänenmitgliedschaft des Computers ändern, aber Sie die IP-Adresse ändern können, bei Bedarf. Weitere Informationen zum Umsetzen dieser Aufgaben finden Sie unter Windows Server&reg; 2016 [Core Network Guide](../../Core-Network-Guide.md).  

  
-   [Installieren Sie die Web-Server-WEB1](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [Erstellen Sie ein Aliaseintrag (CNAME) in DNS für WEB1](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [Konfigurieren von WEB1 zum Verteilen von Zertifikatsperrlisten (CRLs)](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [Vorbereiten der CAPolicy inf-Datei](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [Installieren der Zertifizierungsstelle](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [Konfigurieren Sie die CDP- und AIA-Erweiterungen für CA1](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [Kopieren Sie der ZS-Zertifikat und die Zertifikatsperrliste auf das virtuelle Verzeichnis](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [Konfigurieren der Zertifikatvorlage](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [Konfigurieren der automatischen Registrierung von Serverzertifikaten](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [Aktualisierung der Gruppenrichtlinie](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [Überprüfen der Registrierung der Server ein Serverzertifikat](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für Fälle, in denen das Dialogfeld **Benutzerkontensteuerung** geöffnet wird, um die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter**, wenn das Dialogfeld während der Ausführung der Verfahren in dieser Anleitung geöffnet wird und als Folge der ausgeführten Aktionen geöffnet wurde.  
  


