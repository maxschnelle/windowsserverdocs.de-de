---
title: Serverzertifikatbereitstellung – Übersicht
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: ca5c3e04-ae25-4590-97f3-0376a9c2a9a2
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 0cafa4bdeb80b22d6bac4ad09bcae9436cda97c8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877821"
---
# <a name="server-certificate-deployment-overview"></a>Serverzertifikatbereitstellung – Übersicht

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält die folgenden Abschnitte:  
  
-   [Server-zertifikatbereitstellungskomponenten](#bkmk_components)
  
-   [Übersicht über Server-Zertifikat den Bereitstellungsprozess](#bkmk_process)
  
## <a name="bkmk_components"></a>Server-zertifikatbereitstellungskomponenten
Sie können dieses Handbuch zum Installieren von Active Directory-Zertifikatdienste (AD CS) als eine Unternehmens-Stammzertifizierungsstelle (CA) und Serverzertifikate auf Servern, auf dem Netzwerkrichtlinienserver (Network Policy Server, NPS), Routing- und RAS-Dienst (RRAS), ausgeführt werden oder sowohl NPS und RRAS.


Wenn Sie SDN mit der zertifikatbasierten Authentifizierung bereitstellen, müssen Server ein Serverzertifikat zu verwenden, um auf andere Server ihre Identität nachweisen, sodass sie die sichere Kommunikation erreichen.
  
Die folgende Abbildung zeigt die Komponenten, die zum Bereitstellen von Serverzertifikaten auf Servern in Ihrer SDN-Infrastruktur erforderlich sind.
  
![Server Certificate Deployment erforderlichen Infrastruktur](../../../media/Nps-Certs/Nps-Certs.jpg)  
  
> [!NOTE]  
> Mehrere Server, sind in der obigen Abbildung dargestellt: DC1, CA1, WEB1 und viele SDN-Server. Dieses Handbuch enthält Anweisungen zum Bereitstellen und Konfigurieren von CA1 und WEB1, und klicken Sie zum Konfigurieren von DC1, der in diesem Handbuch wird davon ausgegangen, dass Sie bereits in Ihrem Netzwerk installiert haben. Wenn Sie Active Directory-Domäne nicht bereits installiert haben, Sie können hierzu mit der [Core Network Guide](https://technet.microsoft.com/library/mt604042.aspx) für Windows Server 2016.  
  
Weitere Informationen über jedes Element in der Abbildung oben dargestellt finden Sie hier:  
  
-   [CA1](#bkmk_ca1)  
  
-   [WEB1](#bkmk_web1)  
  
-   [DC1](#bkmk_dc1)  
  
-   [NPS1](#bkmk_nps1)  
  
### <a name="bkmk_ca1"></a>CA1 AD CS-Serverrolle ausgeführt  
In diesem Szenario ist die Stammzertifizierungsstelle der Zertifizierungsstelle (CA) auch eine ausstellende Zertifizierungsstelle. Die Zertifizierungsstelle stellt Zertifikate für Server-Computer, die die korrekten Sicherheitsberechtigungen, um ein Zertifikat zu registrieren. Active Directory-Zertifikatdienste (AD CS) ist auf CA1 installiert.  
  
Für größere Netzwerke oder, in denen die Sicherheitsrisiken Begründung angeben können Sie unterschiedliche Rollen der Stammzertifizierungsstelle und ausstellende Zertifizierungsstelle und Bereitstellen von untergeordnete Zertifizierungsstellen, die von Zertifizierungsstellen ausgegeben werden.  
  
In den sichersten Bereitstellungen stammen die Stammzertifizierungsstelle des Unternehmens offline und physisch gesichert.   
  
#### <a name="capolicyinf"></a>CAPolicy.inf  
Bevor Sie AD CS installieren, konfigurieren Sie die CAPolicy.inf-Datei mit spezifischen Einstellungen für die Bereitstellung.  
  
#### <a name="copy-of-the-ras-and-ias-servers-certificate-template"></a>Kopie der **RAS- und IAS-Server** Zertifikatvorlage  
Wenn Sie Server-Zertifikate bereitstellen, stellen Sie eine Kopie der **RAS- und IAS-Server** Zertifikatvorlage aus, und klicken Sie dann die Vorlage entsprechend Ihren Anforderungen und die Anweisungen in diesem Handbuch konfigurieren.   
  
Sie verwenden eine Kopie der Vorlage anstelle der ursprünglichen Vorlage, damit die Konfiguration der ursprünglichen Vorlage für die zukünftige Verwendung beibehalten wird. Sie konfigurieren, dass die Kopie der **RAS- und IAS-Server** Vorlage, damit die Zertifizierungsstelle Serverzertifikate erstellen kann, gibt er den Gruppen in Active Directory-Benutzer und Computer, die Sie angeben.  
  
#### <a name="additional-ca1-configuration"></a>Zusätzliche CA1-Konfiguration  
Die Zertifizierungsstelle veröffentlicht eine Zertifikatsperrliste (CRL), die Computer überprüfen müssen, um sicherzustellen, dass die Zertifikate, die sie als Identitätsnachweis angezeigt werden, gültige Zertifikate sind und nicht widerrufen wurde. Sie müssen die Zertifizierungsstelle, damit Sie wissen, wo Sie für die Sperrliste während des Authentifizierungsvorgangs zu suchen, Computer mit den richtigen Speicherort der Zertifikatsperrliste konfigurieren.  
  
### <a name="bkmk_web1"></a>WEB1 Web Services (IIS)-Serverrolle ausgeführt  
Auf dem Computer mit der Serverrolle Webserver (IIS) WEB1, müssen Sie einen Ordner im Windows-Explorer für die Verwendung als Speicherort für die Zertifikatsperrlisten und AIA erstellen.  
  
#### <a name="virtual-directory-for-the-crl-and-aia"></a>Virtuelles Verzeichnis für die Zertifikatsperrlisten und AIA  
Nachdem Sie einen Ordner im Windows-Explorer erstellen, müssen Sie den Ordner als ein virtuelles Verzeichnis (Internet Information Services, IIS) Manager als auch die Zugriffssteuerungsliste für das virtuelle Verzeichnis konfigurieren, dass Computer können auf die AIA- und CDP-konfigurieren. nach dem werden sie es veröffentlicht.  
  
### <a name="bkmk_dc1"></a>DC1 Ausführen der AD DS und DNS-Server-Rollen  
DC1 ist der Domänencontroller und DNS-Server in Ihrem Netzwerk.  
  
#### <a name="group-policy-default-domain-policy"></a>Gruppe der Standarddomänenrichtlinie für Richtlinie  
Nachdem Sie auf der Zertifizierungsstelle die Zertifikatvorlage konfigurieren, können Sie die Standarddomänenrichtlinie in der Gruppenrichtlinie konfigurieren, damit, dass Zertifikate automatisch registrierte auf NPS- und RAS-Server sind. Die Gruppenrichtlinie wird in AD DS auf dem Server DC1 konfiguriert.  
  
#### <a name="dns-alias-cname-resource-record"></a>DNS-alias (CNAME) Resource record  
Sie müssen angeben, erstellen ein Aliasressourceneintrags (CNAME) für den Webserver aus, um sicherzustellen, dass andere Computer finden können, dem Server als auch die AIA und die Zertifikatsperrliste, die auf dem Server gespeichert sind. Darüber hinaus bietet die mit einem Alias CNAME-Ressourceneintrag Flexibilität, damit Sie den Webserver für andere Zwecke, beispielsweise zum Hosten von Websites und FTP-Sites verwenden können.  
  
### <a name="bkmk_nps1"></a>NPS1 auf der Netzwerkrichtlinienserver-Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste  
Der Netzwerkrichtlinienserver ist installiert, beim Ausführen von Aufgaben in Windows Server 2016 Core Network Guide, also vor dem Ausführen der Aufgaben in diesem Handbuch, wenn Sie bereits haben eine oder mehrere NPSs im Netzwerk installiert.  
  
#### <a name="group-policy-applied-and-certificate-enrolled-to-servers"></a>Die Gruppenrichtlinie angewendet und Zertifikat registriert wird, auf Servern  
Nachdem Sie die Zertifikatvorlage und die automatische Registrierung konfiguriert haben, können Sie die Gruppenrichtlinie auf alle Zielserver aktualisieren. Zu diesem Zeitpunkt registrieren die Server für das Serverzertifikat von einer Zertifizierungsstelle 1.  
  
### <a name="bkmk_process"></a>Übersicht über Server-Zertifikat den Bereitstellungsprozess  
  
> [!NOTE]  
> Informationen zum Ausführen dieser Schritte finden Sie im Abschnitt [Serverzertifikatbereitstellung](../../../core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md).  
  
Der Vorgang zum Konfigurieren der zertifikatregistrierung Server erfolgt in dieser Phasen:  
  
1.  Installieren Sie auf WEB1 die Rolle Webserver (IIS) ein.  
  
2.  Erstellen Sie auf DC1 ein Aliaseintrag (CNAME) für Ihre Web-Server, WEB1.  
  
3.  Konfigurieren Sie Ihren Webserver so hosten die Zertifikatsperrliste der Zertifizierungsstelle, und klicken Sie dann veröffentlichen Sie die Zertifikatsperrliste aus, und kopieren Sie das Zertifikat der Stammzertifizierungsstelle des Unternehmens in das neue virtuelle Verzeichnis ein.  
  
4.  Weisen Sie auf dem Computer, in dem Sie AD CS installieren möchten den Computer eine statische IP-Adresse, Umbenennen des Computers, fügen Sie den Computer der Domäne, und melden Sie sich bei dem Computer mit einem Benutzerkonto, das Mitglied der Gruppen Domänen-Admins und Organisations-Admins ist.  
  
5.  Konfigurieren Sie auf dem Computer, in dem Sie planen, AD CS installieren die CAPolicy.inf-Datei mit Einstellungen, die für Ihre Bereitstellung spezifisch sind.  
  
6.  Installieren der AD CS-Serverrolle und zusätzliche Konfigurationen auf der Zertifizierungsstelle durchführen.  
  
7.  Kopieren Sie die CRL und CA-Zertifikat aus CA1, auf die Freigabe auf dem Webserver WEB1.  
  
8.  Konfigurieren Sie eine Kopie der Zertifikatvorlage RAS- und IAS-Server, auf der Zertifizierungsstelle. Die Zertifizierungsstelle stellt Zertifikate basierend auf dem eine Zertifikatvorlage, damit Sie die Vorlage für das Serverzertifikat konfigurieren müssen, bevor die Zertifizierungsstelle ein Zertifikat ausstellen kann.  
  
9.  Konfigurieren von Serverzertifikaten in der Gruppenrichtlinie. Wenn Sie die automatische Registrierung konfigurieren, erhalten alle Server, die Sie mit Active Directory-Gruppenmitgliedschaften automatisch angegeben haben ein Zertifikat aus, wenn die Gruppenrichtlinie auf jedem Server aktualisiert wird. Wenn Sie später weitere Server hinzufügen, erhalten sie automatisch ein Serverzertifikat zu.  
  
10. Aktualisieren Sie die Gruppenrichtlinie auf Servern. Wenn Gruppenrichtlinien aktualisiert wird, erhalten die Servern das Serverzertifikat, basierend auf der Vorlage, die Sie im vorherigen Schritt konfiguriert. Dieses Zertifikat wird während der Authentifizierung durch den Server an seine Identität gegenüber Clientcomputern ausweisen kann und anderen Servern verwendet.  
  
    > [!NOTE]  
    > Alle Domänenmitgliedscomputer erhalten automatisch die Stammzertifizierungsstelle des Zertifikats der Zertifizierungsstelle ohne die Konfiguration der automatischen Registrierung. Dieses Zertifikat unterscheidet sich das Serverzertifikat, konfigurieren und zu verteilen, indem Sie mithilfe der automatischen Registrierung zur Verfügung. Zertifikat der Zertifizierungsstelle, wird automatisch im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für alle Domänenmitgliedscomputer installiert, damit sie Zertifikate, die von dieser Zertifizierungsstelle ausgestellt werden, vertrauen werden.   
  
10. Stellen Sie sicher, dass alle Server ein gültiges Serverzertifikat registriert haben.  
  


