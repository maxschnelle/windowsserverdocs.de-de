---
title: Bereitstellen von Serverzertifikaten für 802.1X-authentifizierte Kabel- und Drahtlosnetzwerke Bereitstellungen
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fda9b2b53d088cc389e98cf96fecd748419bc6e2
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Bereitstellen von Serverzertifikaten für 802.1X-authentifizierte Kabel- und Drahtlosnetzwerke Bereitstellungen

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Handbuch können Serverzertifikate für die Infrastrukturserver Remotezugriff und Netzwerkrichtlinienserver (Network Policy Server, NPS) bereitstellen.   

Dieses Handbuch enthält die folgenden Abschnitte.  

-   [Voraussetzungen für die Verwendung dieses Handbuchs](#bkmk_pre)  

-   [Was dieses Handbuch bietet keine](#bkmk_not)  

-   [Technologieübersichten](#bkmk_tech)  

-   [Übersicht über die Bereitstellung von Server-Zertifikat](Server-Certificate-Deployment-Overview.md)  

-   [Planen der Bereitstellung SSL](Server-Certificate-Deployment-Planning.md)  

-   [Bereitstellung von Serverzertifikaten](Server-Certificate-Deployment.md)  

### **<a name="digital-server-certificates"></a>Digitale Zertifikate**  
Dieses Handbuch enthält Anweisungen für die Verwendung von Active Directory-Zertifikatdienste (AD CS) zur automatischen Registrierung von Zertifikaten für RAS und Netzwerkrichtlinienserver-Infrastruktur. AD CS können Sie eine public Key-Infrastruktur (PKI) zu erstellen und Bereitstellen von Kryptografie mit öffentlichem Schlüssel, digitale Zertifikate und Funktionen für digitale Signatur für Ihre Organisation.  

Wenn Sie digitale Zertifikate für die Authentifizierung zwischen Computern in Ihrem Netzwerk verwenden, geben die Zertifikate:   

1. Vertraulichkeit durch Verschlüsselung.  
2. Integrität durch digitale Signaturen.  
3. Authentifizierung durch Computer, Benutzer oder Gerät Konten in einem Computernetzwerk Zertifikatschlüssel zuordnen.  

### **<a name="server-types"></a>Server-Typen**  
Mithilfe dieses Handbuchs können Sie Serverzertifikate für die folgenden Typen von Servern bereitstellen.  
- Server, die das RAS-Dienst ausgeführt werden, die sich DirectAccess oder Server Standard virtuelle private Netzwerke (VPN) und Mitglieder der **RAS- und IAS-Server** Gruppe.  
- Server, auf denen dem Netzwerkrichtlinienserver (Network Policy Server, NPS)-Dienst sind Mitglieder der **RAS- und IAS-Server** Gruppe.  

### **<a name="advantages-of-certificate-autoenrollment"></a>Vorteile der automatischen Registrierung von Zertifikaten**  
Automatische Registrierung von Serverzertifikaten, auch als bezeichnet die automatische Registrierung, bietet die folgenden Vorteile.  

- Die AD CS-Zertifizierungsstelle (CA) registriert wird automatisch ein Serverzertifikat für alle NPS und RAS-Server.  
- Alle Computer in der Domäne erhalten automatisch Ihrer CA-Zertifikat, das in den Speicher vertrauenswürdiger Stammzertifizierungsstellen installiert wird auf alle Domänenmitgliedscomputer speichern. Aus diesem Grund vertrauen alle Computer in der Domäne der Zertifikate, die von der Zertifizierungsstelle ausgestellt wurden. Diese Vertrauensstellung ermöglicht der Authentifizierung, die miteinander ihre Identität nachweisen und sichere Kommunikation vor.  
- Die manuelle Neukonfiguration von jedem Server ist als die Aktualisierung der Gruppenrichtlinie, nicht erforderlich.  
- Jedes Zertifikat enthält die Serverauthentifizierung und Clientauthentifizierung in erweiterten Schlüsselverwendung (EKU)-Erweiterungen.  
- Skalierbarkeit. Nach der Bereitstellung Ihrer Unternehmens-Stammzertifizierungsstelle in diesem Handbuch, können Sie Ihre public Key-Infrastruktur (PKI) durch Hinzufügen von Enterprise-Zertifizierungsstellen erweitern.  
- Verwaltbarkeit. Sie können AD CS mithilfe der AD CS-Konsole oder mithilfe von Windows PowerShell-Befehle und -Skripts verwalten.  
- Der Einfachheit halber. Sie geben Sie die Server, die Serverzertifikate mithilfe von Active Directory-Gruppenkonten und Gruppenmitgliedschaft zu registrieren.   
- Bei der Bereitstellung von Serverzertifikaten basieren die Zertifikate auf einer Vorlage, die Sie mit den Anweisungen in diesem Handbuch zu konfigurieren. Dies bedeutet, dass Sie unterschiedliche Zertifikatvorlagen für bestimmte Servertypen anpassen können, oder Sie können dieselbe Vorlage für alle Zertifikate, die Sie ausstellen möchten.  

## <a name="bkmk_pre"></a>Voraussetzungen für die Verwendung dieses Handbuchs  

Dieses Handbuch enthält Anweisungen zum Bereitstellen von Serverzertifikaten mithilfe von AD CS und die Serverrolle Webserver (IIS) in Windows Server2016. Es folgen die Voraussetzungen für die Durchführung der Verfahrens in diesem Handbuch.  

- Sie müssen ein Hauptnetzwerk mithilfe von Windows Server2016 Core Network Guide bereitstellen, oder müssen Sie vorher die Technologien, die im Kernnetzwerkhandbuch beschriebenen installiert und ordnungsgemäß in Ihrem Netzwerk bereitgestellt haben. Zu diesen Technologien zählen TCP/IP-v4, DHCP, Active Directory Domain Services (AD DS), DNS- und NPS.  
>[!NOTE]
>Windows Server2016 Core Network Guide ist in der technischen Bibliothek zu Windows Server2016 verfügbar. Weitere Informationen finden Sie unter [Kernnetzwerkhandbuch](../../../core-network-guide/Core-Network-Guide.md).

- Sie müssen im Planungsabschnitt dieses Handbuchs, um sicherzustellen, dass Sie für die Bereitstellung vorbereitet sind, vor dem Durchführen der Bereitstellungstyps lesen.  
- Sie müssen die Schrittein diesem Handbuch in der Reihenfolge ausführen, in denen sie angezeigt werden. Springen im Voraus nicht, und die Zertifizierungsstelle bereitstellen, ohne den Schritten, die Sie zum Bereitstellen von dem Server oder Ihrer Bereitstellung führen schlägt fehl.  
- Sie müssen darauf vorbereitet, zum Bereitstellen von zwei neuer Servern in Ihrem Netzwerk - ein Server, auf dem Sie AD CS als Unternehmens-Stammzertifizierungsstelle installieren möchten, und ein Server, auf dem Sie Webserver (IIS) installieren, damit die Zertifizierungsstelle die Zertifikatssperrliste (CRL) auf dem Webserver veröffentlichen kann.   

>[!NOTE]  
>Sie können die Web- und AD CS-Server eine statische IP-Adresse zuweisen, die Sie in diesem Handbuch auch und nennen Sie die Computer gemäß der Benennungskonventionen Ihrer Organisation bereitstellen. Darüber hinaus muss der Computer der Domäne beitreten.  

## <a name="bkmk_not"></a>Was dieses Handbuch bietet keine  
Dieses Handbuch bietet keine umfassende Anweisungen für das Entwerfen und Bereitstellen einer public Key-Infrastruktur (PKI) mit AD CS. Es wird empfohlen, dass Sie AD CS-Dokumentation und Dokumentation zur PKI-Design vor der Bereitstellung der Technologien in diesem Handbuch zu überprüfen.   

## <a name="bkmk_tech"></a>Technologieübersichten  
Folgendes sind Technologieübersichten für AD CS und Webserver (IIS).  

### <a name="active-directory-certificate-services"></a>Active Directory-Zertifikatdienste  
AD CS in Windows Server2016 bietet anpassbare Dienste zum Erstellen und Verwalten der x. 509-Zertifikate, die in Softwaresicherheitssystemen verwendet werden, die von öffentlichen Schlüsseln zur Verfügung. Organisationen können AD CS verwenden, um die Sicherheit zu erhöhen, indem Sie die Identität einer Person, Gerät oder Dienst zu einem entsprechenden öffentlichen Schlüssel binden. AD CS umfasst auch Features, mit die Sie die Registrierung von Zertifikaten und Sperren in einer Vielzahl von skalierbare Umgebung verwalten können.  

Weitere Informationen finden Sie unter [Active Directory Certificate Services Overview](https://technet.microsoft.com/library/hh831740.aspx) und [Public Key-Infrastruktur-Designleitfaden ](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx).  

### <a name="web-server-iis"></a>Webserver (IIS)  

Die Rolle "Webserver (IIS)" in Windows Server2016 bietet eine sichere, einfach zu verwaltende, modulare und erweiterbare Plattform für ein zuverlässiges Hosting von Websites, Diensten und Anwendungen. Mit IIS können Sie Informationen gemeinsamen mit Benutzern im Internet, Intranet oder einem extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.NET, FTP-Dienste, PHP und Windows Communication Foundation (WCF) integriert wird.  

Weitere Informationen finden Sie unter [Webserver (IIS): Übersicht ](https://technet.microsoft.com/library/hh831725.aspx).  
