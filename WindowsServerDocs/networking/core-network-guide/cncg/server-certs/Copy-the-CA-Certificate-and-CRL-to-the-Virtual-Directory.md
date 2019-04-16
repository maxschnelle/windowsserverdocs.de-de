---
title: Kopieren Sie das Zertifizierungsstellenzertifikat und die Zertifikatsperrliste auf das virtuelle Verzeichnis
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e37bfce7f8cf33fd7fcb5e6227d783c28bd29d35
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>Kopieren Sie das Zertifizierungsstellenzertifikat und die Zertifikatsperrliste auf das virtuelle Verzeichnis

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Sie können dieses Verfahren verwenden, Zertifikatsperrliste und Unternehmen das Zertifikat der Stammzertifizierungsstelle von der Zertifizierungsstelle auf ein virtuelles Verzeichnis auf dem Webserver zu kopieren und um sicherzustellen, dass AD CS ordnungsgemäß konfiguriert ist. Bevor Sie die folgenden Befehle ausführen, stellen Sie sicher, dass Sie mit den Verzeichnis- und Server ersetzen, die für Ihre Bereitstellung geeignet sind.  
  
Zum Ausführen dieses Verfahrens müssen Sie Mitglied der sein **Domänen-Admins **.  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>Um die Zertifikatsperrliste von CA1 auf WEB1 zu kopieren  
  
1.  Für Zertifizierungsstelle 1 Windows PowerShell als Administrator ausführen, und klicken Sie dann Veröffentlichen der Zertifikatsperrliste mithilfe des folgenden Befehls:  
  
    - Typ `certutil -crl`, und drücken Sie dann die EINGABETASTE.  
  
    - Um das Zertifikat der Zertifizierungsstelle in der Dateifreigabe auf dem Webserver zu kopieren, geben Sie `copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki`, und drücken Sie dann die EINGABETASTE.  
    - Geben Sie zum Kopieren der Zertifikatsperrlisten auf die Dateifreigabe auf dem Webserver `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`, und drücken Sie dann die EINGABETASTE.  
  
2. Geben Sie zum Neustarten von AD CS `Restart-Service certsvc`, und drücken Sie dann die EINGABETASTE.  
  
2.  Um sicherzustellen, dass die CDP- und AIA-Erweiterung Speicherorte ordnungsgemäß konfiguriert sind, geben Sie `pkiview.msc`, und drücken Sie dann die EINGABETASTE. Pkiview öffnet Unternehmens-PKI-MMC.  
  
3.  Klicken Sie auf den Zertifizierungsstellennamen. Wenn beispielsweise der Name der Zertifizierungsstelle corp-Zertifizierungsstelle 1-CA ist, klicken Sie auf **corp-Zertifizierungsstelle 1-CA **. Klicken Sie im Detailbereich, überprüfen Sie, ob die **Status** Wert für die **Zertifizierungsstellenzertifikat**, **AIA Speicherort 1**, und **CDP-Speicherort 1** sind alle **OK **.  
  
Die folgende Abbildungzeigt den Ergebnisbereich Pkiview mit dem Status OK für alle Elemente.  
  
! [adcs_pkiviewmedia/adcs_pkiview.png)  
  
> [!IMPORTANT]  
> Wenn **Status** für ein Element nicht **OK**, gehen Sie folgendermaßen vor:  
> -   Öffnen Sie die Freigabe auf dem Webserver, um sicherzustellen, dass das Zertifikat und das Zertifikat Widerruf Dateien erfolgreich auf die Freigabe kopiert wurden. Wenn sie auf die Freigabe nicht erfolgreich kopiert wurden, ändern Sie Ihre Kopierbefehle mit den korrekten Quelle und freigeben Sie Ziel, und führen Sie die Befehle erneut aus.  
> -   Stellen Sie sicher, dass Sie auf der Registerkarte Zertifizierungsstelle Erweiterungen sicherstellen, dass die richtigen Speicherorte für die CDP- und AIA eingegeben haben, die es sind keine zusätzlichen Leerzeichen oder andere Zeichen an den Speicherorten, die Sie angegeben haben.  
> -   Stellen Sie sicher, dass Sie das Zertifikat Zertifikatsperrlisten und Zertifizierungsstellenzertifikate an den richtigen Speicherort auf dem Webserver abgelegt und der Speicherort der Speicherort entspricht, den Sie für die CDP- und AIA-Speicherorten auf der Zertifizierungsstelle bereitgestellt.  
> -   Stellen Sie sicher, dass Sie Berechtigungen für das virtuelle Verzeichnis ordnungsgemäß konfiguriert, in dem der ZS-Zertifikat und die Zertifikatsperrliste gespeichert sind.  
  


