---
title: Kopieren des Zertifizierungsstellen Zertifikats und der CRL in das virtuelle Verzeichnis
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: dougkim
ms.topic: article
ms.assetid: a1b5fa23-9cb1-4c32-916f-2d75f48b42c7
ms.author: lizross
author: eross-msft
ms.date: 07/19/2018
ms.openlocfilehash: cea33d8328a2233503fda61b4261213bedce0f3a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949564"
---
# <a name="copy-the-ca-certificate-and-crl-to-the-virtual-directory"></a>Kopieren des Zertifizierungsstellen Zertifikats und der CRL in das virtuelle Verzeichnis

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie die Zertifikat Sperr Liste und das Zertifikat der Unternehmens Stamm Zertifizierungsstelle von Ihrer Zertifizierungsstelle in ein virtuelles Verzeichnis auf dem Webserver kopieren und sicherstellen, dass AD CS ordnungsgemäß konfiguriert ist. Bevor Sie die folgenden Befehle ausführen, stellen Sie sicher, dass Sie die Verzeichnis-und Servernamen durch diejenigen ersetzen, die für die Bereitstellung geeignet sind.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe " **Domänen-Admins**" sein.

#### <a name="to-copy-the-certificate-revocation-list-from-ca1-to-web1"></a>So kopieren Sie die Zertifikat Sperr Liste von CA1 nach WEB1

1.  Führen Sie auf CA1 Windows PowerShell als Administrator aus, und veröffentlichen Sie dann die CRL mit dem folgenden Befehl:

    - Geben Sie `certutil -crl` ein, und drücken Sie dann die EINGABETASTE.

    - Wenn Sie das CA1-Zertifikat in die Dateifreigabe auf dem Webserver kopieren möchten, geben `copy C:\Windows\system32\certsrv\certenroll\*.crt \\WEB1\pki` Sie ein, und drücken Sie dann die EINGABETASTE.

    - Um die Zertifikat Sperr Listen auf die Dateifreigabe auf dem Webserver zu kopieren, geben Sie ein `copy C:\Windows\system32\certsrv\certenroll\*.crl \\WEB1\pki` , und drücken Sie dann die EINGABETASTE.

2.  Geben Sie ein `pkiview.msc` , und drücken Sie dann die EINGABETASTE, um zu überprüfen, ob Ihre CDP-und AIA-Erweiterungs Standorte ordnungsgemäß Die PKI-MMC für PKIView Enterprise wird geöffnet.

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



