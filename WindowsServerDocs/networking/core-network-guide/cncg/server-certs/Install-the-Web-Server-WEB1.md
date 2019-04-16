---
title: Installieren des Webservers WEB1
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: pashort
author: shortpatti
ms.openlocfilehash: e818eac49719b394a2c73cc125a2e7ba9ea80c82
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-the-web-server-web1"></a>Installieren des Webservers WEB1

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Die Rolle "Webserver (IIS)" in Windows Server 2016 bietet eine sichere, einfach zu verwaltende, modulare und erweiterbare Plattform für ein zuverlässiges hosting von Websites, Diensten und Anwendungen. Mit IIS können Sie Informationen gemeinsamen mit Benutzern im Internet, Intranet oder einem extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.NET, FTP-Dienste, PHP und Windows Communication Foundation (WCF) integriert wird.  

Bei der Bereitstellung von Serverzertifikaten bietet der Webserver einen Speicherort, an dem Sie die Zertifikatssperrliste (CRL) für die Zertifizierungsstelle (CA) veröffentlichen können. Nach der Veröffentlichung steht die Zertifikatsperrliste an alle Computer in Ihrem Netzwerk, damit sie diese Liste während des Authentifizierungsprozesses verwenden können, um sicherzustellen, dass Zertifikate von anderen Computern nicht gesperrt werden.   

Wenn ein Zertifikat in der Zertifikatsperrliste als gesperrt ist, der Aufwand für die Authentifizierung ein Fehler auftritt und vertrauenden eine Entität, die ein Zertifikat, das nicht mehr gültig ist, verfügt der Computer geschützt ist.  

Bevor Sie die Rolle Webserver (IIS) installieren, stellen Sie sicher, dass Sie den Servernamen und die IP-Adresse konfiguriert haben und den Computer der Domäne angehören.  

## <a name="to-install-the-web-server-iis-server-role"></a>So installieren Sie die Serverrolle Webserver (IIS)  
Um dieses Verfahren auszuführen, müssen Sie Mitglied der werden die **Administratoren** Gruppe.  

>[!NOTE]  
>Zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell öffnen Sie PowerShell, geben Sie den folgenden Befehl, und drücken Sie dann die EINGABETASTE.  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  Klicken Sie im Server-Manager auf **verwalten**, und klicken Sie dann auf **Hinzufügen von Rollen und Features**. Das Hinzufügen von Rollen und Features-Assistent wird geöffnet.  
2.  In **Vorbemerkungen**, klicken Sie auf **Weiter**.  

**Hinweis:**   
Die **Vorbemerkungen** Seite des Hinzufügen von Rollen und Features Assistenten wird nicht angezeigt, wenn Sie bereits Hinzufügen von Rollen und Features Assistenten ausgeführt haben und **diese Seite standardmäßig überspringen** zu diesem Zeitpunkt.  

3.  Auf der **Installationstyp** auf **Weiter**.  
4.  Auf der **Serverauswahl** auf **Weiter**.  
5.  Auf der **Serverrollen** Seite **Webserver (IIS)**, und klicken Sie dann auf **Weiter**.  
6.  Klicken Sie auf **Weiter** bis Sie akzeptiert haben alle Standardeinstellungen Webserver, und klicken Sie dann auf **installieren**.  
7.  Stellen Sie sicher, dass alle Installationen erfolgreich waren, und klicken Sie dann auf **schließen**.
