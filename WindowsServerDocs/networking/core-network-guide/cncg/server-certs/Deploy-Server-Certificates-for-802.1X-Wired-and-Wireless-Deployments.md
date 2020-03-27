---
title: Bereitstellen von Serverzertifikaten für drahtgebundene und drahtlose 802.1X-Bereitstellungen
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 0a39ecae-39cc-4f26-bd6f-b71ed02fc4ad
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 0636fc321b4e94351628fd577526a8e81b4fc4cf
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318309"
---
# <a name="deploy-server-certificates-for-8021x-wired-and-wireless-deployments"></a>Bereitstellen von Serverzertifikaten für drahtgebundene und drahtlose 802.1X-Bereitstellungen

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mithilfe dieses Handbuchs können Sie Server Zertifikate für die Remote Zugriffs-und NPS-Infrastruktur Server (Network Policy Server, Netzwerk Richtlinien Server) bereitstellen.   

Dieses Handbuch enthält die folgenden Abschnitte:  

-   [Voraussetzungen für die Verwendung dieses Handbuchs](#bkmk_pre)  

-   [Nicht in diesem Handbuch enthaltene Informationen](#bkmk_not)  

-   [Technologie Übersichten](#bkmk_tech)  

-   [Übersicht über die Server Zertifikat Bereitstellung](Server-Certificate-Deployment-Overview.md)  

-   [Planen der Bereitstellung von Server Zertifikaten](Server-Certificate-Deployment-Planning.md)  

-   [Server Zertifikat Bereitstellung](Server-Certificate-Deployment.md)  

### <a name="digital-server-certificates"></a>**Zertifikate für digitale Server**  
Dieses Handbuch enthält Anweisungen zur Verwendung von Active Directory Zertifikat Diensten (AD CS) zum automatischen Registrieren von Zertifikaten für RAS-und NPS-Infrastruktur Server. AD CS ermöglicht Ihnen das Erstellen einer Public Key-Infrastruktur (PKI) und die Bereitstellung von Kryptografie mit öffentlichem Schlüssel, digitalen Zertifikaten und Funktionen für digitale Signaturen in Ihrer Organisation.  

Wenn Sie Zertifikate für digitale Server für die Authentifizierung zwischen Computern im Netzwerk verwenden, stellen die Zertifikate Folgendes bereit:   

1. Vertraulichkeit durch Verschlüsselung.  
2. Integrität durch digitale Signaturen.  
3. Authentifizierung durch Zuordnen von Zertifikat Schlüsseln zu Computer-, Benutzer-oder Geräte Konten in einem Computernetzwerk.  

### <a name="server-types"></a>**Server Typen**  
Mithilfe dieses Handbuchs können Sie Server Zertifikate für die folgenden Server Typen bereitstellen.  
- Server, auf denen der RAS-Dienst ausgeführt wird, bei denen es sich um DirectAccess-oder Standard-VPN-Server (virtuelles privates Netzwerk) handelt und die Mitglieder der Gruppe " **RAS-und IAS-Server** " sind.  
- Server, auf denen der Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird, die Mitglieder der Gruppe " **RAS-und IAS-Server** " sind.  

### <a name="advantages-of-certificate-autoenrollment"></a>**Vorteile der automatischen Zertifikat Registrierung**  
Die automatische Registrierung von Server Zertifikaten, auch als automatische Registrierung bezeichnet, bietet die folgenden Vorteile.  

- Die AD CS-Zertifizierungsstelle registriert automatisch ein Serverzertifikat für alle NPS-und Remote Zugriffs Server.  
- Alle Computer in der Domäne erhalten automatisch Ihr Zertifizierungsstellen Zertifikat, das im Speicher der vertrauenswürdigen Stamm Zertifizierungsstellen auf jedem Domänen Mitglieds Computer installiert ist. Aus diesem Grund vertrauen alle Computer in der Domäne den Zertifikaten, die von der Zertifizierungsstelle ausgestellt werden. Diese Vertrauensstellung ermöglicht Ihren Authentifizierungs Servern, Ihre Identitäten einander nachzuweisen und eine sichere Kommunikation zu gewährleisten.  
- Anders als bei der Aktualisierung Gruppenrichtlinie ist die manuelle Neukonfiguration der einzelnen Server nicht erforderlich.  
- Jedes Serverzertifikat enthält den Zweck der Server Authentifizierung und den Zweck der Client Authentifizierung in EKU-Erweiterungen (Enhanced Key Usage).  
- Skalierbarkeit. Nachdem Sie die Stamm Zertifizierungsstelle Ihres Unternehmens mit dieser Anleitung bereitgestellt haben, können Sie Ihre Public Key-Infrastruktur (PKI) erweitern, indem Sie untergeordnete Unternehmens Zertifizierungsstellen  
- Verwaltbarkeit. Sie können AD CS mithilfe der AD CS-Konsole oder mithilfe von Windows PowerShell-Befehlen und-Skripts verwalten.  
- Einfachheit. Sie geben die Server, die Server Zertifikate registrieren, mithilfe von Active Directory Gruppenkonten und Gruppenmitgliedschaften an.   
- Wenn Sie Server Zertifikate bereitstellen, basieren die Zertifikate auf einer Vorlage, die Sie mit den Anweisungen in diesem Handbuch konfigurieren. Dies bedeutet, dass Sie verschiedene Zertifikat Vorlagen für bestimmte Server Typen anpassen können, oder Sie können für alle Server Zertifikate, die Sie ausgeben möchten, dieselbe Vorlage verwenden.  

## <a name="prerequisites-for-using-this-guide"></a><a name="bkmk_pre"></a>Voraussetzungen für die Verwendung dieses Handbuchs  

Dieses Handbuch enthält Anweisungen zum Bereitstellen von Server Zertifikaten mithilfe von AD CS und der Server Rolle Webserver (IIS) in Windows Server 2016. Im folgenden finden Sie die Voraussetzungen für die Ausführung der Verfahren in diesem Handbuch.  

- Sie müssen ein Kern Netzwerk mithilfe des Windows Server 2016-Kern Netzwerk Handbuchs bereitstellen, oder Sie müssen bereits über die im Handbuch zum Hauptnetzwerk bereitgestellten Technologien verfügen, die im Netzwerk ordnungsgemäß installiert sind und ordnungsgemäß funktionieren. Zu diesen Technologien gehören TCP/IP V4, DHCP, Active Directory Domain Services (AD DS), DNS und NPS.  
  >[!NOTE]
  >Das Windows Server 2016-Kern Netzwerk Handbuch ist in der technischen Bibliothek für Windows Server 2016 verfügbar. Weitere Informationen finden Sie im [Handbuch](../../../core-network-guide/Core-Network-Guide.md)zum Hauptnetzwerk.

- Sie müssen den Abschnitt Planning dieses Handbuchs lesen, um sicherzustellen, dass Sie für diese Bereitstellung vorbereitet sind, bevor Sie die Bereitstellung ausführen.  
- Die Schritte in diesem Handbuch müssen in der Reihenfolge ausgeführt werden, in der Sie angezeigt werden. Stellen Sie Ihre Zertifizierungsstelle nicht bereit, ohne die Schritte auszuführen, die zur Bereitstellung des Servers führen, oder die Bereitstellung schlägt fehl.  
- Sie müssen darauf vorbereitet sein, zwei neue Server in Ihrem Netzwerk bereitzustellen: einen Server, auf dem Sie AD CS als Stamm Zertifizierungsstelle des Unternehmens installieren werden, und einen Server, auf dem Sie den Webserver (IIS) installieren, damit Ihre Zertifizierungsstelle die Zertifikat Sperr Liste im Web veröffentlichen kann. Servers.   

>[!NOTE]  
>Sie sind darauf vorbereitet, den Web-und AD CS-Servern, die Sie mit diesem Handbuch bereitstellen, eine statische IP-Adresse zuzuweisen. Außerdem können Sie die Computer gemäß den Benennungs Konventionen Ihrer Organisation benennen. Außerdem müssen Sie die Computer der Domäne hinzufügen.  

## <a name="what-this-guide-does-not-provide"></a><a name="bkmk_not"></a>Was diese Anleitung nicht bietet  
Diese Anleitung enthält keine ausführlichen Anweisungen zum Entwerfen und Bereitstellen einer Public Key-Infrastruktur (PKI) mithilfe von AD CS. Es wird empfohlen, die AD CS-Dokumentation und die PKI-Entwurfsdokumentation zu lesen, bevor Sie die Technologien in diesem Handbuch bereitstellen.   

## <a name="technology-overviews"></a><a name="bkmk_tech"></a>Technologie Übersichten  
Im folgenden finden Sie Technologie Übersichten für AD CS und Webserver (IIS).  

### <a name="active-directory-certificate-services"></a>Active Directory-Zertifikatsdienste  
AD CS in Windows Server 2016 bietet anpassbare Dienste zum Erstellen und Verwalten der X. 509-Zertifikate, die in Software Sicherheitssystemen verwendet werden, die Public Key-Technologien einsetzen. Organisationen können AD CS verwenden, um die Sicherheit zu erhöhen, indem Sie die Identität einer Person, eines Geräts oder Diensts an einen entsprechenden öffentlichen Schlüssel binden. AD CS umfasst auch Features, mit denen Sie die Zertifikat Registrierung und die Sperrung in einer Vielzahl von skalierbaren Umgebungen verwalten können.  

Weitere Informationen finden Sie unter [Übersicht über Active Directory Zertifikat Dienste](https://technet.microsoft.com/library/hh831740.aspx) und [Entwurfs Leit Fäden für die Public Key-Infrastruktur](https://social.technet.microsoft.com/wiki/contents/articles/2901.public-key-infrastructure-design-guidance.aspx).  

### <a name="web-server-iis"></a>Web Server (IIS)  

Die Rolle "Webserver (IIS)" in Windows Server 2016 bietet eine sichere, einfach zu verwaltende, modulare und erweiterbare Plattform für das zuverlässige Hosting von Websites, Diensten und Anwendungen. Mit IIS können Sie Informationen für Benutzer im Internet, in einem Intranet oder in einem Extranet freigeben. IIS ist eine einheitliche Webplattform, die IIS, ASP.net, FTP-Dienste, PHP und Windows Communication Foundation (WCF) integriert.  

Weitere Informationen finden Sie unter [Webserver (IIS): Übersicht](https://technet.microsoft.com/library/hh831725.aspx).  
