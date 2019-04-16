---
title: Übersicht über die Bereitstellung von Server-Zertifikat
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: ca5c3e04-ae25-4590-97f3-0376a9c2a9a2
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4650c99325def63fd0df25989c661230fada3dac
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="server-certificate-deployment-overview"></a>Übersicht über die Bereitstellung von Server-Zertifikat

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Thema enthält die folgenden Abschnitte.  
  
-   [Die zertifikatbereitstellungskomponenten Server](#bkmk_components)
  
-   [Server Certificate Deployment Prozess (Übersicht)](#bkmk_process)
  
## <a name="bkmk_components"></a>Die zertifikatbereitstellungskomponenten Server
So installieren Sie Active Directory-Zertifikatdienste (AD CS) als eine Unternehmens-Stammzertifizierungsstelle (CA) und Serverzertifikate für Server registrieren, auf dem Netzwerkrichtlinienserver (Network Policy Server, NPS), Routing- und RAS-Dienst (RRAS), oder NPS- und RRAS ausgeführt werden, können Sie dieses Handbuch verwenden.


Wenn Sie mit der zertifikatbasierten Authentifizierung SDN bereitstellen, müssen Server ein Serverzertifikat zu verwenden, um ihre Identität zu anderen Servern belegen, damit sie sichere Kommunikation erzielen.
  
Die folgende Abbildungzeigt die Komponenten, die die Bereitstellung von Serverzertifikaten auf Servern in Ihrer SDN-Infrastruktur erforderlich sind.
  
![Server Certificate Deployment erforderliche Infrastruktur](../../../media/Nps-Certs/Nps-Certs.jpg)  
  
> [!NOTE]  
> In der obigen Abbildungsind mehrere Server dargestellt: DC1, CA1, WEB1 und viele SDN Servern. Dieses Handbuch enthält Anweisungen für die Bereitstellung und Konfiguration von CA1 und WEB1 und zum Konfigurieren von DC1, die in diesem Handbuch wird davon ausgegangen, dass Sie bereits in Ihrem Netzwerk installiert haben. Wenn Sie Active Directory-Domäne nicht bereits installiert haben, Sie können dazu die [Kernnetzwerkhandbuch](https://technet.microsoft.com/library/mt604042.aspx) für Windows Server2016.  
  
Weitere Informationen über die einzelnen Elemente in der obigen Abbildunggezeigt finden Sie in der folgenden:  
  
-   [CA1](#bkmk_ca1)  
  
-   [WEB1](#bkmk_web1)  
  
-   [DC1](#bkmk_dc1)  
  
-   [NPS1](#bkmk_nps1)  
  
### <a name="bkmk_ca1"></a>CA1 mit der AD CS-Serverrolle  
In diesem Szenario ist die Stammzertifizierungsstelle (CA) auch eine ausstellende Zertifizierungsstelle. Die Zertifizierungsstelle stellt Zertifikate für Server-Computer, die die korrekten Sicherheitsberechtigungen zum Registrieren eines Zertifikats verfügen. Active Directory-Zertifikatdienste (AD CS) ist für Zertifizierungsstelle 1 installiert.  
  
Bei größeren Netzwerken oder, in denen Sicherheitsbedenken Begründung bereitstellen können Sie trennen Sie die Rollen der Stammzertifizierungsstelle und ausstellende Zertifizierungsstelle und untergeordnete Zertifizierungsstellen, die Ausstellen von Zertifizierungsstellen bereitstellen.  
  
Die sicherste-Bereitstellungen wird der Unternehmens-Stammzertifizierungsstelle offline und physisch sicheren übernommen.   
  
#### <a name="capolicyinf"></a>CAPolicy.inf  
Vor der Installation von AD CS konfigurieren Sie die CAPolicy.inf-Datei mit spezifischen Einstellungen für die Bereitstellung.  
  
#### <a name="copy-of-the-ras-and-ias-servers-certificate-template"></a>Kopieren der **RAS- und IAS-Server** Zertifikatvorlage  
Bei der Bereitstellung von Serverzertifikaten stellen Sie eine Kopie der **RAS- und IAS-Server** Zertifikatvorlage, und konfigurieren Sie die Vorlage entsprechend Ihren Anforderungen und die Anweisungen in diesem Handbuch.   
  
Sie verwenden eine Kopie der ursprünglichen Vorlage, anstatt die Vorlage so, dass die Konfiguration der ursprünglichen Vorlage für die zukünftige Verwendung beibehalten wird. Konfigurieren Sie die Kopie der **RAS- und IAS-Server** Vorlage so, dass die Zertifizierungsstelle Zertifikate erstellen kann Probleme für die Gruppen in Active Directory-Benutzer und Computer, die Sie angeben.  
  
#### <a name="additional-ca1-configuration"></a>Zusätzliche Konfiguration für Zertifizierungsstelle 1  
Die Zertifizierungsstelle veröffentlicht eine Zertifikatsperrliste (CRL), die Computer überprüfen müssen, um sicherzustellen, dass Zertifikate, die sie als Identitätsnachweis angezeigt werden, gültige Zertifikate sind und nicht widerrufen wurde. Sie müssen mit den richtigen Speicherort der Zertifikatsperrliste die Zertifizierungsstelle konfigurieren, sodass Computer, wo wissen Sie während der Authentifizierung für die Sperrliste zu suchen.  
  
### <a name="bkmk_web1"></a>WEB1 unter der Serverrolle für Webdienste (IIS)  
Auf dem Computer mit der Serverrolle Webserver (IIS), WEB1, müssen Sie einen Ordner im Windows-Explorer für die Verwendung als Speicherort für die Zertifikatsperrlisten und AIA erstellen.  
  
#### <a name="virtual-directory-for-the-crl-and-aia"></a>Virtuelles Verzeichnis für die Zertifikatsperrlisten und AIA  
Nachdem Sie in Windows-Explorer einen Ordner erstellen, müssen Sie den Ordner konfigurieren, als virtuelles Verzeichnis in Internet Information Services (IIS) Manager sowie Konfigurieren der Zugriffssteuerungsliste für das virtuelle Verzeichnis für Computer zugelassen auf die AIA- und CDP-zugreifen, nachdem sie es veröffentlicht werden.  
  
### <a name="bkmk_dc1"></a>DC1 Ausführung der AD DS und DNS-Serverrollen  
DC1 ist der Domänencontroller und DNS-Server in Ihrem Netzwerk.  
  
#### <a name="group-policy-default-domain-policy"></a>Gruppieren Sie die Richtlinie Standarddomänenrichtlinie  
Nach der Konfiguration der Zertifikatvorlage für die Zertifizierungsstelle können Sie die Standarddomänenrichtlinie in der Gruppenrichtlinie konfigurieren, damit Zertifikate automatisch registrierte für NPS und RAS-Server sind. Gruppenrichtlinien wird in AD DS auf dem Server DC1 konfiguriert.  
  
#### <a name="dns-alias-cname-resource-record"></a>DNS-alias (CNAME) Resource record  
Erstellen Sie ein Aliasressourceneintrags (CNAME) für den Webserver, um sicherzustellen, dass andere Computer finden können, der Server als auch den AIA und die Zertifikatsperrliste, die auf dem Server gespeichert sind. Darüber hinaus bietet die Verwendung eines Alias CNAME-Ressourceneintrag Flexibilität, damit Sie den Webserver für andere Zwecke verwenden, z.B. Hosting von Websites und FTP-Sites verwenden können.  
  
### <a name="bkmk_nps1"></a>NPS1 auf der Netzwerkrichtlinienserver-Rollendienst der Serverrolle Netzwerkrichtlinien- und Zugriffsdienste  
Der NPS-Server wird installiert, wenn die Aufgaben in Windows Server2016 Core Network Guide, sodass vor dem Durchführen der Aufgaben in dieser Anleitung eine bereits sollte oder mehrere NPS-Servern im Netzwerk installiert.  
  
#### <a name="group-policy-applied-and-certificate-enrolled-to-servers"></a>Gruppenrichtlinien und Zertifikat registrierten Servern  
Nachdem Sie die Zertifikatvorlage und die automatische Registrierung konfiguriert haben, können Sie Gruppenrichtlinien auf allen Zielservern aktualisieren. Zu diesem Zeitpunkt registrieren der Server das Serverzertifikat von einer Zertifizierungsstelle 1.  
  
### <a name="bkmk_process"></a>Server Certificate Deployment Prozess (Übersicht)  
  
> [!NOTE]  
> Die Detail zum Ausführen dieser Schrittefinden Sie in den Abschnitt [Server Certificate Deployment](../../../core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md).  
  
Die Registrierung von Zertifikaten zu konfigurieren, wird in diese Stufen:  
  
1.  Installieren Sie auf WEB1 die Rolle "Webserver (IIS)".  
  
2.  Erstellen Sie auf DC1 ein Aliaseintrag (CNAME) des Webservers WEB1.  
  
3.  Konfigurieren Sie den Webserver hosten die Zertifikatsperrliste der Zertifizierungsstelle, und klicken Sie dann die Zertifikatsperrliste zu veröffentlichen und kopieren Sie das Zertifikat der Stammzertifizierungsstelle des Unternehmens in das neue virtuelle Verzeichnis.  
  
4.  Weisen Sie auf dem Computer, in dem Sie planen, installieren Sie AD CS den Computer eine statische IP-Adresse, Umbenennen des Computers, den Computer der Domäne hinzufügen und melden Sie sich bei dem Computer mit einem Benutzerkonto, das Mitglied der Gruppen Domänen-Admins und Organisations-Admins ist.  
  
5.  Konfigurieren Sie auf dem Computer, in dem Sie planen, installieren Sie AD CS die CAPolicy.inf-Datei mit Einstellungen, die für Ihre Bereitstellung spezifisch sind.  
  
6.  Installieren der AD CS-Serverrolle und der Zertifizierungsstelle zusätzliche Konfigurationen vornehmen.  
  
7.  Kopieren Sie das Zertifikat Zertifikatsperrliste und des Zertifizierungsstellenzertifikats von CA1, auf die Freigabe auf dem Webserver WEB1.  
  
8.  Konfigurieren Sie eine Kopie der Zertifikatvorlage RAS- und IAS-Server, auf der Zertifizierungsstelle. Die Zertifizierungsstelle stellt Zertifikate basierend auf einer Zertifikatvorlage, damit Sie die Vorlage für das Serverzertifikat konfigurieren müssen, bevor die Zertifizierungsstelle ein Zertifikat ausstellen kann.  
  
9.  Konfigurieren von Serverzertifikaten in der Gruppenrichtlinie. Wenn Sie die automatische Registrierung konfigurieren, erhalten alle Server, die Sie automatisch mit Active Directory-Gruppenmitgliedschaften angegeben haben ein Serverzertifikat an, wenn die Gruppenrichtlinien auf jedem Server aktualisiert werden. Wenn Sie später weitere Server hinzufügen, erhalten sie automatisch ein Serverzertifikat zu.  
  
10. Aktualisieren von Gruppenrichtlinien auf Servern. Wenn Gruppenrichtlinien aktualisiert wird, erhalten die Server das Serverzertifikat, das auf der Vorlage basiert, die Sie im vorherigen Schrittkonfiguriert. Dieses Zertifikat wird von der Server seine Identität gegenüber Clientcomputern ausweisen und andere Server während der Authentifizierung verwendet.  
  
    > [!NOTE]  
    > Alle Domänenmitgliedscomputer erhalten automatisch die Unternehmens-Stammzertifizierungsstelle Zertifikat ohne die Konfiguration der automatischen Registrierung. Dieses Zertifikat unterscheidet sich das Serverzertifikat, konfigurieren und verteilen, indem Sie mithilfe der automatischen Registrierung zur Verfügung. Zertifikat der Zertifizierungsstelle wird automatisch im Zertifikatspeicher vertrauenswürdige Stammzertifizierungsstellen für alle Domänenmitgliedscomputer installiert, damit sie Zertifikate als vertrauenswürdig eingestuft werden, die von dieser Zertifizierungsstelle ausgestellt werden.   
  
10. Stellen Sie sicher, dass alle Server ein gültiges Serverzertifikat registriert haben.  
  


