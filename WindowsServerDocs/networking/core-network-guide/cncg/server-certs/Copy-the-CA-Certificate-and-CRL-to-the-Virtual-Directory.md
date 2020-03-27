---
title: Kopieren des Zertifizierungsstellen Zertifikats und der CRL in das virtuelle Verzeichnis
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: dougkim
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.date: 07/19/2018
ms.openlocfilehash: 275bec5c950ea20c3a7d5a933648cf7e068164d1
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318357"
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>Kopieren des Zertifizierungsstellen Zertifikats und der CRL in das virtuelle Verzeichnis

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mit diesem Verfahren können Sie die Zertifikat Sperr Liste und das Zertifikat der Unternehmens Stamm Zertifizierungsstelle von Ihrer Zertifizierungsstelle in ein virtuelles Verzeichnis auf dem Webserver kopieren und sicherstellen, dass AD CS ordnungsgemäß konfiguriert ist. Bevor Sie die folgenden Befehle ausführen, stellen Sie sicher, dass Sie die Verzeichnis-und Servernamen durch diejenigen ersetzen, die für die Bereitstellung geeignet sind.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe " **Domänen-Admins**" sein.  
  
#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>So kopieren Sie die Zertifikat Sperr Liste von CA1 nach WEB1  
  
1.  Führen Sie auf CA1 Windows PowerShell als Administrator aus, und veröffentlichen Sie dann die CRL mit dem folgenden Befehl:  
  
    - Geben Sie `certutil -crl` ein, und drücken Sie dann die EINGABETASTE.  

    - Geben Sie `copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki`ein, und drücken Sie dann die EINGABETASTE, um das CA1-Zertifikat in die Dateifreigabe auf dem Webserver zu kopieren.  
    
    - Geben Sie `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki`ein, und drücken Sie dann die EINGABETASTE, um die Zertifikat Sperr Listen auf die Dateifreigabe auf dem Webserver zu kopieren.  
  
2.  Geben Sie `pkiview.msc`ein, und drücken Sie dann die EINGABETASTE, um zu überprüfen, ob Ihre CDP-und AIA-Erweiterungs Standorte ordnungsgemäß Die PKI-MMC für PKIView Enterprise wird geöffnet.  
  
3.  Klicken Sie im linken Bereich auf den Namen Ihrer Zertifizierungsstelle.<p>Wenn Ihr ZS-Name beispielsweise Corp-CA1-ca lautet, klicken Sie auf **Corp-CA1-ca**. 

4. Überprüfen Sie in der Spalte Status des Ergebnis Bereichs, ob die Werte für **Folgendes angezeigt werden**:

    - **Zertifizierungsstellen Zertifikat**
    - **AIA-Speicherort #1**
    - **CDP-Speicherort #1**   
  
  
> [!TIP]  
> Wenn der **Status** für ein beliebiges Element nicht in **Ordnung**ist, gehen Sie wie folgt vor:  
> -   Öffnen Sie die Freigabe auf dem Webserver, um zu überprüfen, ob die Zertifikat-und Zertifikat Sperr Listen Dateien erfolgreich in die Freigabe kopiert wurden. Wenn Sie nicht erfolgreich auf die Freigabe kopiert wurden, ändern Sie die Kopier Befehle mit der richtigen Datei Quelle und dem Freigabe Ziel, und führen Sie die Befehle erneut aus.  
> -   Vergewissern Sie sich, dass Sie die richtigen Speicherorte für CDP und AIA auf der Registerkarte ZS-Erweiterungen eingegeben haben. Stellen Sie sicher, dass an den von Ihnen angegebenen Speicherorten keine zusätzlichen Leerzeichen oder andere Zeichen vorhanden sind.  
> -   Vergewissern Sie sich, dass Sie die Zertifikat Sperr Liste und das Zertifizierungsstellen Zertifikat an den richtigen Speicherort auf dem Webserver kopiert haben und dass der Speicherort mit dem Speicherort übereinstimmt, den Sie für die CDP-und AIA-Standorte der Zertifizierungsstelle  
> -   Vergewissern Sie sich, dass Sie die Berechtigungen für den virtuellen Ordner, in dem das Zertifizierungsstellen Zertifikat und die CRL gespeichert sind  
  


