---
title: Installieren des Webservers WEB1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ef4f10a6ac1998850758f2c9db86bfd950c1ad70
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59833281"
---
# <a name="install-the-web-server-web1"></a>Installieren des Webservers WEB1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die Rolle "Webserver (IIS)" in Windows Server 2016 bietet eine sichere, leicht zu verwaltende, modulare und erweiterbare Plattform für das zuverlässige hosting von Websites, Diensten und Anwendungen. Mit IIS können Sie Informationen für Benutzer auf das Internet, Intranet oder in einem extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.NET, FTP-Dienste, PHP, und Windows Communication Foundation (WCF) integriert ist.  

Wenn Sie Server-Zertifikate bereitstellen, bietet Ihrem Webserver einen Speicherort, in dem Sie die Zertifikatsperrliste (CRL) Ihrer Zertifizierungsstelle (CA) veröffentlichen können. Nach der Veröffentlichung ist die Zertifikatsperrliste auf allen Computern in Ihrem Netzwerk zugegriffen werden kann, so, dass sie diese Liste während der Authentifizierung verwenden können, um sicherzustellen, dass von anderen Computern bereitgestellten Zertifikate nicht widerrufen werden.   

Wenn ein Zertifikat in der Zertifikatsperrliste als gesperrt ist, der Aufwand für die Authentifizierung schlägt fehl, und Ihr Computer ist geschützt, vertrauenden eine Entität, die ein Zertifikat verfügt, die nicht mehr gültig ist.  

Bevor Sie die Rolle Webserver (IIS) installieren, stellen Sie sicher, dass Sie den Servernamen und die IP-Adresse konfiguriert haben, und der Domäne des Computers hinzugefügt haben.  

## <a name="to-install-the-web-server-iis-server-role"></a>So installieren Sie die Serverrolle "Webserver (IIS)"  
Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.  

>[!NOTE]  
>Zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell öffnen Sie PowerShell, geben Sie den folgenden Befehl aus, und drücken Sie dann die EINGABETASTE.  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.  
2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.  

**Hinweis**   
Die **Vorbemerkungen** des Hinzufügen von Rollen und Features-Assistenten nicht angezeigt wird, wenn Sie, zuvor Hinzufügen von Rollen und Features-Assistenten ausgeführt haben, und Sie ausgewählt **auf dieser Seite standardmäßig überspringen** zu diesem Zeitpunkt.  

3.  Klicken Sie auf der Seite **Installationstyp** auf **Weiter**.  
4.  Auf der **Serverauswahl** auf **Weiter**.  
5.  Auf der **Serverrollen** Seite **Webserver (IIS)**, und klicken Sie dann auf **Weiter**.  
6.  Klicken Sie auf **Weiter**, bis Sie alle Standardeinstellungen für Webserver akzeptiert haben, und klicken Sie dann auf **Installieren**.  
7.  Stellen Sie sicher, dass alle Installationen erfolgreich waren, und klicken Sie dann auf **Schließen**.
