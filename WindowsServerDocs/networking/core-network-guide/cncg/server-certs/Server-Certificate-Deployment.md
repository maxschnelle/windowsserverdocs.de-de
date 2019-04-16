---
title: Bereitstellung von Serverzertifikaten
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4a10a9bafa6a8c9fddecac799ec8e837bf339d0e
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment"></a>Bereitstellung von Serverzertifikaten

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Gehen Sie so installieren Sie eine Unternehmens-Stammzertifizierungsstelle (CA) und Serverzertifikate für die Verwendung mit PEAP und EAP bereitgestellt.  
  
> [!IMPORTANT]  
> Vor der Installation von Active Directory Certificate Services müssen Sie Namen für den Computer, konfigurieren Sie den Computer mit einer statischen IP-Adresse und der Computer der Domäne hinzufügen. Nach der Installation von AD CS können nicht Sie den Computernamen oder die Domänenmitgliedschaft des Computers ändern, jedoch Sie die IP-Adresse ändern können, bei Bedarf. Weitere Informationen dazu, wie zum Ausführen dieser Aufgaben finden Sie unter Windows Server&reg; 2016 [Kernnetzwerkhandbuch](../../Core-Network-Guide.md).  

  
-   [Installieren des Webservers WEB1](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [Erstellen Sie ein Aliaseintrag (CNAME) in DNS für WEB1](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [Konfigurieren von WEB1 zum Verteilen von Zertifikatsperrlisten (CRLs)](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [Vorbereiten der CAPolicy inf-Datei](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [Installieren der Zertifizierungsstelle](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [Kopieren Sie das Zertifizierungsstellenzertifikat und die Zertifikatsperrliste auf das virtuelle Verzeichnis](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [Konfigurieren der Serverzertifikatvorlage](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [Konfigurieren von Serverzertifikaten](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [Aktualisieren von Gruppenrichtlinien](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [Überprüfen der Serverregistrierung eines Serverzertifikats](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für Fälle in der die **User Account Control** Dialogfeld geöffnet wird, um Ihre Zustimmung zum Fortfahren abzufragen. Wenn dieses Dialogfeld wird geöffnet, während Sie die Verfahren in diesem Handbuch durchgeführt werden, und wenn das Dialogfeld, als Antwort auf Ihre Aktionen geöffnet wurde auf **Weiter**.  
  


