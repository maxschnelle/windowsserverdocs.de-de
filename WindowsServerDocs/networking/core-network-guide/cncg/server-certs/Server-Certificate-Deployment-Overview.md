---
title: Serverzertifikatbereitstellung – Übersicht
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: ca5c3e04-ae25-4590-97f3-0376a9c2a9a2
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 318bab675cc633034731e369b5da2bbb40d810b0
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87949414"
---
# <a name="server-certificate-deployment-overview"></a>Serverzertifikatbereitstellung – Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält folgende Abschnitte:

-   [Komponenten der Server Zertifikat Bereitstellung](#bkmk_components)

-   [Übersicht über den Server Zertifikat Bereitstellungs Prozess](#bkmk_process)

## <a name="server-certificate-deployment-components"></a><a name="bkmk_components"></a>Komponenten der Server Zertifikat Bereitstellung
Mithilfe dieses Handbuchs können Sie Active Directory Zertifikat Dienste (AD CS) als Unternehmens-Stamm Zertifizierungsstelle (Certification Authority, ca) installieren und Server Zertifikate für Server registrieren, auf denen der Netzwerk Richtlinien Server (Network Policy Server, NPS), der Routing-und RAS-Dienst (RRAS) oder NPS und RRAS ausgeführt werden.


Wenn Sie Sdn mit Zertifikat basierter Authentifizierung bereitstellen, müssen Server ein Serverzertifikat verwenden, um Ihre Identitäten anderen Servern nachzuweisen, damit Sie eine sichere Kommunikation erreichen.

Die folgende Abbildung zeigt die Komponenten, die für die Bereitstellung von Server Zertifikaten für Server in ihrer Sdn-Infrastruktur erforderlich sind.

![Erforderliche Infrastruktur für die Server Zertifikat Bereitstellung](../../../media/Nps-Certs/Nps-Certs.jpg)

> [!NOTE]
> In der obigen Abbildung werden mehrere Server dargestellt: DC1, CA1, WEB1 und viele Sdn-Server. Dieses Handbuch enthält Anweisungen für die Bereitstellung und Konfiguration von CA1 und WEB1 sowie für die Konfiguration von DC1, bei der in diesem Handbuch davon ausgegangen wird, dass Sie bereits in Ihrem Netzwerk installiert haben. Wenn Sie Ihre Active Directory Domäne noch nicht installiert haben, können Sie dazu das Handbuch zum Haupt [Netzwerk](https://technet.microsoft.com/library/mt604042.aspx) für Windows Server 2016 verwenden.

Weitere Informationen zu den Elementen, die in der obigen Abbildung dargestellt werden, finden Sie hier:

-   [CA1](#bkmk_ca1)

-   [WEB1](#bkmk_web1)

-   [DC1](#bkmk_dc1)

-   [NPS1](#bkmk_nps1)

### <a name="ca1-running-the-ad-cs-server-role"></a><a name="bkmk_ca1"></a>CA1 Ausführen der AD CS-Server Rolle
In diesem Szenario ist die Stamm Zertifizierungsstelle des Unternehmens ebenfalls eine ausstellende Zertifizierungsstelle. Die Zertifizierungsstelle gibt Zertifikate für Server Computer aus, die über die richtigen Sicherheits Berechtigungen zum Registrieren eines Zertifikats verfügen. Die Active Directory Zertifikat Dienste (AD CS) werden auf CA1 installiert.

Bei größeren Netzwerken oder bei Sicherheitsrisiken, die eine Begründung darstellen, können Sie die Rollen der Stamm Zertifizierungsstelle und der ausstellenden Zertifizierungsstelle trennen und untergeordnete CAS bereitstellen, die Zertifizierungsstellen

Bei den sichersten bereit Stellungen wird die Stamm Zertifizierungsstelle des Unternehmens offline geschaltet und physisch gesichert.

#### <a name="capolicyinf"></a>CAPolicy. inf
Vor der Installation von AD CS konfigurieren Sie die Datei CAPolicy. inf mit spezifischen Einstellungen für die Bereitstellung.

#### <a name="copy-of-the-ras-and-ias-servers-certificate-template"></a>Kopieren der **RAS-und IAS-Server-** Zertifikat Vorlage
Wenn Sie Server Zertifikate bereitstellen, erstellen Sie eine Kopie der **RAS-und IAS-Server** -Zertifikat Vorlage, und konfigurieren Sie die Vorlage entsprechend Ihren Anforderungen und den Anweisungen in diesem Handbuch.

Sie verwenden eine Kopie der Vorlage anstelle der ursprünglichen Vorlage, damit die Konfiguration der ursprünglichen Vorlage für eine mögliche zukünftige Verwendung beibehalten wird. Sie konfigurieren die Kopie der Vorlage für **RAS-und IAS-Server** , sodass die Zertifizierungsstelle Server Zertifikate erstellen kann, die für die Gruppen in Active Directory von Ihnen angegebenen Benutzern und Computern ausgegeben werden.

#### <a name="additional-ca1-configuration"></a>Zusätzliche CA1-Konfiguration
Von der Zertifizierungsstelle wird eine Zertifikat Sperr Liste (CRL) veröffentlicht, die von Computern überprüft werden muss, um sicherzustellen, dass Zertifikate, die Ihnen als Identitätsnachweis angezeigt werden, gültige Zertifikate sind und nicht widerrufen wurden. Sie müssen die Zertifizierungsstelle mit dem richtigen Speicherort der CRL konfigurieren, damit die Computer wissen, wo die Zertifikat Sperr Liste während des Authentifizierungs Vorgangs gesucht werden soll.

### <a name="web1-running-the-web-services-iis-server-role"></a><a name="bkmk_web1"></a>WEB1 Ausführen der Web Services (IIS)-Server Rolle
Auf dem Computer, auf dem die Webserver Rolle "Webserver (IIS)" (WEB1) ausgeführt wird, müssen Sie in Windows-Explorer einen Ordner erstellen, der als Speicherort für die Zertifikat Sperr Liste und AIA verwendet werden kann.

#### <a name="virtual-directory-for-the-crl-and-aia"></a>Virtuelles Verzeichnis für die CRL und AIA
Nachdem Sie einen Ordner in Windows-Explorer erstellt haben, müssen Sie den Ordner als virtuelles Verzeichnis in Internetinformationsdienste (IIS)-Manager konfigurieren und die Zugriffs Steuerungs Liste für das virtuelle Verzeichnis konfigurieren, um Computern den Zugriff auf AIA und CRL zu ermöglichen, nachdem Sie dort veröffentlicht wurden.

### <a name="dc1-running-the-ad-ds-and-dns-server-roles"></a><a name="bkmk_dc1"></a>DC1 Ausführen der AD DS-und DNS-Server Rollen
DC1 ist der Domänen Controller und DNS-Server in Ihrem Netzwerk.

#### <a name="group-policy-default-domain-policy"></a>Standard Domänen Richtlinie Gruppenrichtlinie
Nachdem Sie die Zertifikat Vorlage auf der Zertifizierungsstelle konfiguriert haben, können Sie die Standard Domänen Richtlinie in Gruppenrichtlinie konfigurieren, damit Zertifikate automatisch auf NPS-und RAS-Servern registriert werden. Gruppenrichtlinie ist in AD DS auf dem Server "DC1" konfiguriert.

#### <a name="dns-alias-cname-resource-record"></a>DNS-Alias (CNAME)-Ressourcen Daten Satz
Sie müssen einen Alias Ressourcen Daten Satz (CNAME) für den Webserver erstellen, um sicherzustellen, dass der Server von anderen Computern sowie von AIA und der CRL, die auf dem Server gespeichert sind, gefunden werden kann. Außerdem bietet die Verwendung eines Alias-CNAME-Ressourceneinsatzes Flexibilität, sodass Sie den Webserver für andere Zwecke verwenden können, z. b. das Hosting von Web-und FTP-Sites.

### <a name="nps1-running-the-network-policy-server-role-service-of-the-network-policy-and-access-services-server-role"></a><a name="bkmk_nps1"></a>NPS1 Ausführen des Netzwerk Richtlinien Server-Rollen Diensts der Server Rolle "Netzwerk Richtlinien-und Zugriffs Dienste"
Der NPS wird installiert, wenn Sie die Aufgaben im Windows Server 2016-Kern Netzwerk Handbuch ausführen, sodass Sie vor dem Ausführen der Aufgaben in diesem Handbuch bereits einen oder mehrere NPSS in Ihrem Netzwerk installiert haben.

#### <a name="group-policy-applied-and-certificate-enrolled-to-servers"></a>Gruppenrichtlinie angewendete und auf Server registrierte Zertifikate
Nachdem Sie die Zertifikat Vorlage und die automatische Registrierung konfiguriert haben, können Sie Gruppenrichtlinie auf allen Ziel Servern aktualisieren. Zu diesem Zeitpunkt registrieren die Server das Serverzertifikat von CA1.

### <a name="server-certificate-deployment-process-overview"></a><a name="bkmk_process"></a>Übersicht über den Server Zertifikat Bereitstellungs Prozess

> [!NOTE]
> Ausführliche Informationen zur Ausführung dieser Schritte finden Sie im Abschnitt [Server Zertifikat Bereitstellung](../../../core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md).

Der Vorgang zum Konfigurieren der Serverzertifikat Registrierung erfolgt in den folgenden Phasen:

1.  Installieren Sie auf WEB1 die Rolle "Webserver (IIS)".

2.  Erstellen Sie auf DC1 einen Alias (CNAME)-Datensatz für Ihren Webserver, WEB1.

3.  Konfigurieren Sie den Webserver zum Hosten der CRL von der Zertifizierungsstelle. veröffentlichen Sie anschließend die Zertifikat Sperr Liste, und kopieren Sie das Zertifikat der Stamm Zertifizierungsstelle der Zertifizierungsstelle in das neue virtuelle Verzeichnis.

4.  Weisen Sie auf dem Computer, auf dem Sie AD CS installieren möchten, dem Computer eine statische IP-Adresse zu, benennen Sie den Computer um, fügen Sie den Computer der Domäne hinzu, und melden Sie sich dann am Computer mit einem Benutzerkonto an, das Mitglied der Gruppen Domänen-Admins und Organisations-Admins ist.

5.  Konfigurieren Sie auf dem Computer, auf dem Sie AD CS installieren möchten, die Datei CAPolicy. inf mit den Einstellungen, die für die Bereitstellung spezifisch sind.

6.  Installieren Sie die AD CS-Server Rolle, und führen Sie eine zusätzliche Konfiguration der Zertifizierungsstelle aus.

7.  Kopieren Sie die Zertifikat Sperr Liste und das Zertifizierungsstellen Zertifikat von CA1 in die Freigabe auf dem Webserver WEB1.

8.  Konfigurieren Sie auf der Zertifizierungsstelle eine Kopie der RAS-und IAS-Server-Zertifikat Vorlage. Die Zertifizierungsstelle gibt Zertifikate auf der Grundlage einer Zertifikat Vorlage aus. Daher müssen Sie die Vorlage für das Serverzertifikat konfigurieren, bevor die Zertifizierungsstelle ein Zertifikat ausgeben kann.

9.  Konfigurieren Sie die automatische Registrierung von Server Zertifikaten in Gruppenrichtlinie. Wenn Sie die automatische Registrierung konfigurieren, erhalten alle Server, die Sie mit Active Directory Gruppenmitgliedschaften angegeben haben, automatisch ein Serverzertifikat, wenn Gruppenrichtlinie auf jedem Server aktualisiert wird. Wenn Sie später weitere Server hinzufügen, erhalten Sie automatisch auch ein Serverzertifikat.

10. Aktualisieren Sie Gruppenrichtlinie auf den Servern. Wenn Gruppenrichtlinie aktualisiert wird, erhalten die Server das Serverzertifikat, das auf der Vorlage basiert, die Sie im vorherigen Schritt konfiguriert haben. Dieses Zertifikat wird vom Server verwendet, um seine Identität bei Client Computern und anderen Servern während des Authentifizierungs Vorgangs nachzuweisen.

    > [!NOTE]
    > Alle Domänen Mitglieds Computer erhalten automatisch das Zertifikat der Stamm Zertifizierungsstelle der Stamm Zertifizierungsstelle, ohne die automatische Registrierung zu konfigurieren. Dieses Zertifikat unterscheidet sich von dem Serverzertifikat, das Sie mithilfe der automatischen Registrierung konfigurieren und verteilen. Das Zertifikat der Zertifizierungsstelle wird automatisch im Zertifikat Speicher für vertrauenswürdige Stamm Zertifizierungsstellen für alle Domänen Mitglieds Computer installiert, sodass Sie von dieser Zertifizierungsstelle ausgegebene Zertifikate als vertrauenswürdig eingestuft werden.

10. Vergewissern Sie sich, dass alle Server ein gültiges Serverzertifikat registriert haben.



