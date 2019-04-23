---
title: Kopieren Sie der ZS-Zertifikat und die Zertifikatsperrliste auf das virtuelle Verzeichnis
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: dougkim
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.date: 07/19/2018
ms.openlocfilehash: 15cc807db805e1be0349ea51119663e515c7e551
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874031"
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>Kopieren Sie der ZS-Zertifikat und die Zertifikatsperrliste auf das virtuelle Verzeichnis

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren verwenden, um Certificate Revocation List, und Unternehmen das Zertifikat der Stammzertifizierungsstelle aus Ihrer Zertifizierungsstelle in ein virtuelles Verzeichnis auf Ihrem Webserver zu kopieren, und um sicherzustellen, dass AD CS ordnungsgemäß konfiguriert ist. Bevor Sie die folgenden Befehle ausführen, stellen Sie sicher, dass Sie die Verzeichnis-und Server durch die ersetzen, die für Ihre Bereitstellung geeignet sind.  
  
Zum Ausführen dieses Verfahrens müssen Sie Mitglied werden **Domänen-Admins**.  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>Um die Zertifikatsperrliste aus CA1 auf WEB1 zu kopieren.  
  
1.  Klicken Sie auf ka1 führen Sie Windows PowerShell als Administrator aus, und klicken Sie dann veröffentlichen Sie die Zertifikatsperrliste mit den folgenden Befehl aus:  
  
    - Geben Sie `certutil -crl` ein, und drücken Sie dann die EINGABETASTE.  

    - Geben Sie zum Kopieren der Zertifikatssperrlisten auf die Dateifreigabe auf dem Webserver `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`, und drücken Sie dann die EINGABETASTE.  
  
2.  Um sicherzustellen, dass die Orte Ihrer CDP- und AIA-Erweiterung ordnungsgemäß konfiguriert sind, geben Sie `pkiview.msc`, und drücken Sie dann die EINGABETASTE. Pkiview wird geöffnet, Unternehmens-PKI-MMC.  
  
3.  Klicken Sie im linken Bereich auf den Zertifizierungsstellennamen.<p>Z. B. Wenn Ihr ZS-Name corp.-CA1-CA ist, klicken Sie auf **corp-CA1-CA**. 

4. In der Spalte Status des Ergebnisbereichs, stellen Sie sicher, dass die Werte für die folgenden die **OK**:

    - **Zertifikat der Zertifizierungsstelle**
    - **Speicherort für AIA #1**
    - **CDP-Speicherort #1**   
  
  
> [!TIP]  
> Wenn **Status** für jedes Element nicht ist **OK**, gehen Sie folgendermaßen vor:  
> -   Öffnen Sie die Freigabe auf Ihrem Webserver, um sicherzustellen, dass das Zertifikat und ein Zertifikat sperren Auflisten von Dateien auf die Freigabe erfolgreich kopiert wurden. Wenn sie auf die Freigabe nicht erfolgreich kopiert wurden, ändern Sie Ihre Kopierbefehle, mit der richtigen Quelle und freigeben Sie Ziel, und führen Sie die Befehle erneut aus.  
> -   Stellen Sie sicher, dass Sie auf der Registerkarte "CA-Erweiterungen" die korrekten Speicherorte für die CDP- und AIA eingegeben haben. Stellen Sie sicher, dass es keine zusätzlichen Leerzeichen oder andere Zeichen in die Speicherorte, die Sie angegeben haben.  
> -   Stellen Sie sicher, dass Sie die CRL und CA-Zertifikat auf den richtigen Speicherort auf Ihrem Webserver kopiert und der Speicherort die Position übereinstimmt, die Sie für die CDP- und AIA-Speicherorten für die Zertifizierungsstelle angegeben.  
> -   Stellen Sie sicher, dass Sie Berechtigungen für den virtuellen Ordner richtig konfiguriert haben, in dem der ZS-Zertifikat und die Zertifikatsperrliste gespeichert sind.  
  


