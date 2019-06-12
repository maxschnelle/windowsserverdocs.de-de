---
title: Bereitstellen von Serverzertifikaten für drahtgebundene und drahtlose 802.1X-Bereitstellungen
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2d4cdcd11e0eb334064ddefec0eda775ffccff2c
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446472"
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Bereitstellen von Serverzertifikaten für drahtgebundene und drahtlose 802.1X-Bereitstellungen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Handbuch verwenden, Serverzertifikate für die Infrastruktur-Server Remotezugriff und Netzwerkrichtlinienserver (Network Policy Server, NPS) bereitstellen.   

Dieses Handbuch enthält die folgenden Abschnitte:  

-   [Voraussetzungen für die Verwendung dieses Handbuchs](#bkmk_pre)  

-   [Nicht in diesem Handbuch enthaltene Informationen](#bkmk_not)  

-   [Technologieübersicht](#bkmk_tech)  

-   [Übersicht über die Bereitstellung von Server-Zertifikat](Server-Certificate-Deployment-Overview.md)  

-   [Planen der Bereitstellung SSL](Server-Certificate-Deployment-Planning.md)  

-   [Bereitstellung von Serverzertifikaten](Server-Certificate-Deployment.md)  

### <a name="digital-server-certificates"></a>**Digitale Serverzertifikate**  
Dieses Handbuch enthält Anweisungen für die Verwendung von Active Directory-Zertifikatdienste (AD CS), Zertifikate, um den Remotezugriff und NPS-Infrastruktur-Server automatisch zu registrieren. AD CS ermöglichen Ihnen eine public Key-Infrastruktur (PKI) zu erstellen und Bereitstellen von Kryptografie mit öffentlichem Schlüssel, digitale Zertifikate und digitale Signatur-Funktionen für Ihre Organisation.  

Wenn Sie digital Serverzertifikate für die Authentifizierung zwischen Computern in Ihrem Netzwerk verwenden, geben Sie die Zertifikate:   

1. Datenvertraulichkeit durch Verschlüsselung.  
2. Integrität durch digitale Signaturen.  
3. Authentifizierung durch Zuordnung von Zertifikatschlüsseln mit-Computer, Benutzer oder Gerät Konten in einem Computernetzwerk.  

### <a name="server-types"></a>**Server-Typen**  
Mithilfe dieses Handbuchs können Sie Serverzertifikate, die folgenden Typen von Servern bereitstellen.  
- Server, die ausgeführt werden, die RAS-Dienst, die sich DirectAccess oder standard virtuelles privates Netzwerk (VPN)-Server, und die Mitglieder von der **RAS- und IAS-Server** Gruppe.  
- Server, auf denen dem Dienst (Network Policy Server, NPS) sind Mitglieder der **RAS- und IAS-Server** Gruppe.  

### <a name="advantages-of-certificate-autoenrollment"></a>**Vorteile der automatischen Registrierung von Zertifikaten**  
Automatische Registrierung von Serverzertifikaten, auch als automatische Registrierung bezeichnet, bietet die folgenden Vorteile.  

- Die AD CS-Zertifizierungsstelle (CA) wird automatisch ein Zertifikat für alle Ihre NPS und RAS-Server registriert.  
- Alle Computer in der Domäne erhalten automatisch Ihr CA-Zertifikat, das in der vertrauenswürdigen Stammzertifizierungsstellen installiert wird auf alle Domänenmitgliedscomputer zu speichern. Aus diesem Grund vertrauen alle Computer in der Domäne, die Zertifikate, die von der Zertifizierungsstelle ausgestellt werden. Diese Vertrauensstellung ermöglicht Ihrer Authentifizierungsserver Beweisen ihre Identitäten miteinander, und engagieren Sie sich in die sichere Kommunikation.  
- Als Aktualisieren der Gruppenrichtlinie, ist die manuelle Neukonfiguration von jedem Server nicht erforderlich.  
- Jedes Serverzertifikat umfasst den Zertifizierungszweck der Serverauthentifizierung und Zertifizierungszweck der Clientauthentifizierung in erweiterten Schlüsselverwendung (EKU)-Erweiterungen.  
- Skalierbarkeit. Nach der Bereitstellung Ihrer Unternehmens-Stammzertifizierungsstelle in diesem Leitfaden, können Sie Ihre public Key-Infrastruktur (PKI) erweitern, durch das Hinzufügen von Enterprise-Zertifizierungsstellen.  
- Verwaltbarkeit. Sie können AD CS mithilfe der AD CS-Konsole oder mithilfe von Windows PowerShell-Befehle und-Skripts verwalten.  
- Einfachheit. Sie geben die Servern, die Serverzertifikate mithilfe von Active Directory-Gruppe-Konten und Gruppenmitgliedschaften zu registrieren.   
- Wenn Sie Server-Zertifikate bereitstellen, werden die Zertifikate basierend auf einer Vorlage, die Sie mit den Anweisungen in diesem Handbuch konfigurieren. Dies bedeutet, dass können Sie unterschiedliche Zertifikatvorlagen für bestimmte Servertypen anpassen, oder Sie können die gleiche Vorlage für alle Serverzertifikate, die Sie ausgeben möchten.  

## <a name="bkmk_pre"></a>Voraussetzungen für die Verwendung dieses Handbuchs  

Dieses Handbuch enthält Anweisungen zum Bereitstellen von Serverzertifikaten mithilfe von AD CS und die Webserver (IIS)-Serverrolle in Windows Server 2016. Es folgen die Voraussetzungen für die Durchführung der Verfahren in diesem Handbuch.  

- Müssen Sie ein Hauptnetzwerk mithilfe der Windows Server 2016 Core Network Guide bereitstellen, oder Sie müssen bereits die Technologien, die in das Handbuch zum Hauptnetzwerk installiert und ordnungsgemäß funktioniert, in Ihrem Netzwerk bereitgestellt haben. Zu diesen Technologien zählen TCP/IP-v4, DHCP, Active Directory Domain Services (AD DS), DNS- und NPS.  
  >[!NOTE]
  >Windows Server 2016 Core Network Guide ist in der technischen Bibliothek zu Windows Server 2016 verfügbar. Weitere Informationen finden Sie unter [Core Network Guide](../../../core-network-guide/Core-Network-Guide.md).

- Sie müssen im Planungsabschnitt dieses Handbuchs, um sicherzustellen, dass Sie für diese Bereitstellung vorbereitet sind, vor der Durchführung der bereitstellungs lesen.  
- Sie müssen die Schritte in diesem Handbuch in der Reihenfolge ausführen, in denen sie angezeigt werden. Gehen Sie nicht, und Bereitstellen Sie Ihrer Zertifizierungsstelle, ohne den Schritten, die für die Bereitstellung von dem Server oder der Bereitstellung führen fehl.  
- Sie müssen vorbereitet sein, zum Bereitstellen von zwei neuer Servern in Ihrem Netzwerk – ein Server, auf denen Sie AD CS als Stammzertifizierungsstelle des Unternehmens installieren möchten, und ein Server, auf dem Sie Webserver (IIS) installieren, damit die Zertifizierungsstelle die Zertifikatsperrliste (CRL) auf die Web-Se veröffentlichen können rvername.   

>[!NOTE]  
>Sie sind bereit, die die Web-Apps und AD CS-Server eine statische IP-Adresse zuweisen, die Sie mit diesem Handbuch ebenfalls, benennen Sie die Computer entsprechend der Benennungskonventionen Ihrer Organisation bereitstellen. Darüber hinaus müssen Sie die Computer mit der Domäne verknüpfen.  

## <a name="bkmk_not"></a>Was dieses Handbuch bietet keine  
Dieses Handbuch bietet keine umfassende Informationen zum Entwerfen und Bereitstellen einer public Key-Infrastruktur (PKI) mit AD CS. Es wird empfohlen, dass Sie AD CS-Dokumentation und die Dokumentation des PKI-Entwurf vor der Bereitstellung der Technologien in diesem Handbuch überprüfen.   

## <a name="bkmk_tech"></a>Technologieübersicht  
Es folgen Technologieübersicht für AD CS- und Webserver (IIS).  

### <a name="active-directory-certificate-services"></a>Active Directory-Zertifikatdienste  
AD CS in Windows Server 2016 bietet anpassbare Dienste zum Erstellen und Verwalten von x. 509-Zertifikate, die in Softwaresicherheitssystemen verwendet werden, die Technologien für öffentliche Schlüssel verwenden. Organisationen können AD CS verwenden, um Sicherheit zu verbessern, indem Sie die Identität einer Person, Geräts oder des Diensts an einen entsprechenden öffentlichen Schlüssel binden. AD CS umfasst auch Funktionen, die Ihnen ermöglichen, die Registrierung von Zertifikaten und Zertifikatsperrlisten in einer Vielzahl von skalierbaren Umgebungen verwalten.  

Weitere Informationen finden Sie unter [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) und [Public Key-Infrastruktur-Entwurfsrichtlinien](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx).  

### <a name="web-server-iis"></a>Webserver (IIS)  

Die Rolle "Webserver (IIS)" in Windows Server 2016 bietet eine sichere, leicht zu verwaltende, modulare und erweiterbare Plattform für das zuverlässige hosting von Websites, Diensten und Anwendungen. Mit IIS können Sie Informationen für Benutzer auf das Internet, Intranet oder in einem extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.NET, FTP-Dienste, PHP, und Windows Communication Foundation (WCF) integriert ist.  

Weitere Informationen finden Sie unter [Webserver (IIS)-Übersicht](https://technet.microsoft.com/library/hh831725.aspx).  
