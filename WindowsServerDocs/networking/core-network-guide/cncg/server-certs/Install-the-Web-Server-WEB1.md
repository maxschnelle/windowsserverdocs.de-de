---
title: Installieren des Webservers WEB1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: f51c9e38-98bb-49c1-9d39-427d07021499
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ad8106c9c8330dd1b8632b3672d6413c1a1faaf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356218"
---
# <a name="install-the-web-server-web1"></a>Installieren des Webservers WEB1

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Die Rolle "Webserver (IIS)" in Windows Server 2016 bietet eine sichere, einfach zu verwaltende, modulare und erweiterbare Plattform für das zuverlässige Hosting von Websites, Diensten und Anwendungen. Mit IIS können Sie Informationen für Benutzer im Internet, in einem Intranet oder in einem Extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.net, FTP-Dienste, PHP und Windows Communication Foundation (WCF) integriert.  

Wenn Sie Server Zertifikate bereitstellen, stellt Ihr Webserver einen Speicherort bereit, an dem Sie die Zertifikat Sperr Liste (CRL) für Ihre Zertifizierungsstelle (Certification Authority, ca) veröffentlichen können. Nach der Veröffentlichung ist der Zugriff auf die Zertifikat Sperr Liste für alle Computer in Ihrem Netzwerk möglich, sodass diese Liste während des Authentifizierungsprozesses verwendet werden kann, um zu überprüfen, ob die von anderen Computern vorgelegten Zertifikate nicht widerrufen werden.   

Wenn ein Zertifikat auf der CRL als gesperrt eingestuft wird, schlägt der Authentifizierungs Aufwand fehl, und Ihr Computer ist nicht vertrauenswürdig für eine Entität, die über ein Zertifikat verfügt, das nicht mehr gültig ist.  

Vergewissern Sie sich vor der Installation der Rolle "Webserver (IIS)", dass Sie den Server Namen und die IP-Adresse konfiguriert haben und dass der Computer der Domäne hinzugefügt wurde.  

## <a name="to-install-the-web-server-iis-server-role"></a>So installieren Sie die Serverrolle "Webserver (IIS)"  
Sie müssen Mitglied der Gruppe **Administratoren** sein, um diesen Vorgang auszuführen.  

>[!NOTE]  
>Um dieses Verfahren mithilfe von Windows PowerShell auszuführen, öffnen Sie PowerShell, geben Sie den folgenden Befehl ein, und drücken Sie dann die EINGABETASTE.  
`Install-WindowsFeature Web-Server -IncludeManagementTools`  

1.  Klicken Sie im Server-Manager auf **Verwalten**und dann auf **Rollen und Features hinzufügen**. Der Assistent zum Hinzufügen von Rollen und Features wird geöffnet.  
2.  Klicken Sie auf der Seite **Vorbemerkungen** auf **Weiter**.  

**Hinweis**   
Die Seite **Vorbemerkungen** des Assistenten zum Hinzufügen von Rollen und Features wird nicht angezeigt, wenn Sie zuvor den Assistenten zum Hinzufügen von Rollen und Features ausgeführt haben und Sie **Diese Seite standardmäßig überspringen** ausgewählt haben.  

3. Klicken Sie auf der Seite **Installationstyp** auf **Weiter**.  
4. Klicken Sie auf der Seite **Server Auswahl** auf **weiter**.  
5. Wählen Sie auf der Seite **Server Rollen** die Option **Webserver (IIS)** aus, und klicken Sie dann auf **weiter**.  
6. Klicken Sie auf **Weiter**, bis Sie alle Standardeinstellungen für Webserver akzeptiert haben, und klicken Sie dann auf **Installieren**.  
7. Stellen Sie sicher, dass alle Installationen erfolgreich waren, und klicken Sie dann auf **Schließen**.
