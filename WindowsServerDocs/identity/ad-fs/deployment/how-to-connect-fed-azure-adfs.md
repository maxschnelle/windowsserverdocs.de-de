---
title: Active Directory-Verbunddienste in Azure | Microsoft-Dokumentation
description: In diesem Dokument lernen Sie, wie Sie für die Bereitstellung von AD FS in Azure für hohe Verfügbarkeit zu erzielen.
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: ''
ms.assetid: 692a188c-badc-44aa-ba86-71c0e8074510
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/28/2018
ms.subservice: hybrid
ms.author: billmath
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f075f91e97f806555507bfc0e0c5f3d1589a71e6
ms.sourcegitcommit: 63926404009f9e1330a4a0aa8cb9821a2dd7187e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/29/2019
ms.locfileid: "67469651"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Bereitstellen von Active Directory-Verbunddienste in Azure
AD FS bietet einen vereinfachten und sicheren Identitätsverbund sowie einmaliges Anmelden (SSO) Funktionen. Verbund mit Azure AD oder O365 ermöglicht Benutzern die Authentifizierung mit lokalen Anmeldeinformationen und Zugriff auf Ressourcen in der Cloud. Es wird daher wichtig, dass eine hochverfügbare AD FS-Infrastruktur, um den Zugriff auf Ressourcen sicherzustellen, dass sowohl lokal und in der Cloud. Bereitstellen von AD FS in Azure helfen bei der hochverfügbarkeit mit wenig Aufwand erforderlich.
Es gibt mehrere Vorteile bei der Bereitstellung von AD FS in Azure, einige davon sind unten aufgeführt:

* **Hohe Verfügbarkeit** -mit der Leistungsfähigkeit von Azure-Verfügbarkeitsgruppen werden soll, stellen Sie sicher, eine Infrastruktur mit hoher verfügbare.
* **Einfache Skalierung** – mehr Leistung benötigen? Einfache Migration zu leistungsfähigeren Computern von nur wenigen Klicks in Azure
* **Standortübergreifende Redundanz** – mit geografischen Redundanz von Azure können Sie sicher sein, dass Ihre Infrastruktur auf der ganzen Welt hoch verfügbar ist
* **Einfache Verwaltung** – stark vereinfachten Verwaltungsfunktionen im Azure-Portal, Verwalten der Infrastruktur ist sehr einfach und problemlos 

## <a name="design-principles"></a>Designprinzipien
![Bereitstellungsentwurf](./media/how-to-connect-fed-azure-adfs/deployment.png)

Das obige Diagramm zeigt die empfohlene grundlegende Topologie Bereitstellung von AD FS-Infrastruktur in Azure zu beginnen. Die grundlegenden Prinzipien für die verschiedenen Komponenten der Topologie sind unten aufgeführt:

* **DC / AD FS-Servern**: Wenn Sie weniger als 1.000 Benutzer haben, können Sie AD FS-Rolle einfach auf Ihren Domänencontrollern installieren. Bereitstellen Sie Wenn Sie nicht, dass Auswirkungen auf die Leistung auf den Domänencontrollern möchten, oder wenn Sie mehr als 1.000 Benutzer haben, können Sie AD FS auf separaten Servern.
* **WAP-Server** – es ist zum Bereitstellen von Web Application Proxy-Server erforderlich sind, sodass Benutzer des AD FS erreichen können, wenn sie nicht im Unternehmensnetzwerk auch sind.
* **DMZ**: Die Webanwendungsproxy-Server im Umkreisnetzwerk platziert werden, und nur TCP/443-Zugriff zwischen dem Umkreisnetzwerk und dem internen Subnetz zulässig ist.
* **Load Balancer**: Es wird empfohlen, um sicherzustellen, dass die hochverfügbarkeit von AD FS und Webanwendungsproxy-Servern, mithilfe eines internen Load Balancers für AD FS-Server und Azure Load Balancer für Webanwendungsproxy-Server.
* **Verfügbarkeitsgruppen**: Um Redundanz für Ihre AD FS-Bereitstellung zu gewährleisten, empfiehlt es sich, dass Sie zwei oder mehr virtuelle Computer in einer Verfügbarkeitsgruppe für ähnliche Workloads gruppieren. Diese Konfiguration wird sichergestellt, dass während eines geplanten oder ungeplanten wartungsereignisses mindestens ein virtueller Computer zur Verfügung stehen
* **Storage-Konten**: Es wird empfohlen, zwei Speicherkonten haben. Ein einzelnes Speicherkonto kann zur Erstellung einer einzelnen Fehlerquelle führen und kann dazu führen, dass die Bereitstellung in einem Szenario mit wahrscheinlich nicht mehr verfügbar, in dem das Speicherkonto ausfällt. Zwei Speicherkonten können jedem Fehlerpunkt ein Speicherkonto zugeordnet werden soll.
* **Netzwerktrennung**:  Webanwendungsproxy-Server sollten in einem separaten DMZ-Netzwerk bereitgestellt werden. Sie können ein virtuelles Netzwerk in zwei Subnetze unterteilen und dann die Webanwendungsproxy-Server in einem isolierten Subnetz bereitstellen. Sie können einfach Konfigurieren der Einstellungen für netzwerksicherheitsgruppen für jedes Subnetz und nur die erforderliche Kommunikation zwischen den zwei Subnetzen zulassen. Weitere Details werden pro Bereitstellungsszenario ist unten angegeben.

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Schritte zum Bereitstellen von AD FS in Azure
Die Schritte in diesem Abschnitt beschreiben die Anleitung zum Bereitstellen der unten dargestellte AD FS-Infrastruktur in Azure.

### <a name="1-deploying-the-network"></a>1. Bereitstellen des Netzwerks
Wie oben beschrieben, können Sie entweder zwei Subnetze in einem einzelnen virtuellen Netzwerk erstellen sonst zwei gänzlich unterschiedliche virtuelle Netzwerke (VNet) erstellen. In diesem Artikel konzentrieren, die ein einzelnes virtuelles Netzwerk bereitstellen und es in zwei Subnetze unterteilen. Dies ist derzeit ein einfacherer Ansatz, da zwei separaten VNets eine VNet-zu-VNet-Gateway für die Kommunikation erforderlich wäre.

**1.1 erstellen Sie virtuellen Netzwerks**

![Virtuelles Netzwerk erstellen](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Im Azure-Portal können virtuelles Netzwerk auswählen und Sie das virtuelle Netzwerk und ein Subnetz sofort mit nur einem Klick bereitstellen. INT-Subnetz wird auch definiert und steht jetzt für virtuelle Computer hinzugefügt werden.
Der nächste Schritt ist ein weiteres Subnetz im Netzwerk, d. h. des DMZ-Subnetzes hinzu. Erstellen des DMZ-Subnetzes

* Wählen Sie das neu erstellte Netzwerk
* Wählen Sie in den Eigenschaften des Subnetzes
* Im Subnetz von Bereich, klicken Sie auf die Schaltfläche "hinzufügen"
* Geben Sie das Subnetz Name und die Adressrauminformationen zum Erstellen des Subnetzes

![Subnetz](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![DMZ-Subnetz](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1.2. Erstellen der netzwerksicherheitsgruppen**

Eine Netzwerksicherheitsgruppe (NSG) enthält eine Liste der Zugriffssteuerungsliste (ACL)-Regeln, die zulassen oder Verweigern von Netzwerkdatenverkehr an Ihre VM-Instanzen in einem virtuellen Netzwerk. NSGs können Subnetzen oder einzelnen VM-Instanzen innerhalb dieses Subnetzes zugeordnet werden. Wenn eine NSG einem Subnetz zugeordnet ist, wenden die ACL-Regeln für alle VM-Instanzen in diesem Subnetz.
In dieser Anleitung erstellen wir zwei NSGs: jeweils eine für ein internes Netzwerk und eine DMZ. Sie werden Namen NSG_INT und NSG_DMZ bzw. bezeichnet werden.

![Erstellen Sie NSG](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

Nachdem die NSG erstellt wurde, wird 0 eingehende und 0 ausgehende Regeln vorhanden sein. Sobald die Rollen auf den entsprechenden Servern installiert und funktionsfähig sind, können die eingehenden und ausgehenden Regeln gemäß der gewünschten Sicherheitsebene vorgenommen werden.

![NSG initialisieren](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

Nachdem die NSGs erstellt wurden, ordnen Sie NSG_INT Subnetz INT und NSG_DMZ dem Subnetz DMZ. Screenshot mit einem Beispiel ist unten angegeben:

![NSG konfigurieren](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* Klicken Sie auf die Subnetze, um den Bereich für Subnetze zu öffnen.
* Wählen Sie das Subnetz der NSG zugeordnet werden soll 

Nach der Konfiguration sollte der Bereich für Subnetze wie folgt aussehen:

![Subnetze nach NSG](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1.3. Erstellen einer Verbindung mit lokalen**

Wir benötigen eine Verbindung mit einem lokalen, um den Domänencontroller (DC) in Azure bereitzustellen. Azure bietet verschiedene Verbindungsoptionen, um Ihre lokale Infrastruktur mit Ihrer Azure-Infrastruktur verbinden.

* Punkt-zu-Standort
* Vnet-Standort-zu-Standort
* ExpressRoute

Es wird empfohlen, ExpressRoute zu verwenden. ExpressRoute ermöglicht Ihnen das Erstellen privater Verbindungen zwischen Azure-Datencentern und Infrastruktur, lokal oder in einer kollokationsumgebung befindet. ExpressRoute-Verbindungen werden nicht über das öffentliche Internet übertragen. Sie bieten mehr Zuverlässigkeit, höhere Geschwindigkeit, niedrigere Latenzzeiten und mehr Sicherheit als herkömmliche Verbindungen über das Internet.
Zwar wird empfohlen, ExpressRoute zu verwenden, können Sie eine beliebige Verbindungsmethode, die sich am besten für Ihre Organisation auswählen. Weitere Informationen zu ExpressRoute und den verschiedenen Verbindungsoptionen mit ExpressRoute finden unter [ExpressRoute – technische Übersicht](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Erstellen von Speicherkonten
Um hochverfügbarkeit zu sorgen und die Abhängigkeit von einem einzelnen Speicherkonto zu vermeiden, können Sie zwei Speicherkonten erstellen. Teilen Sie die Computer in jeder verfügbarkeitsgruppe in zwei Gruppen, und weisen Sie jeder Gruppe ein separates Speicherkonto.

![Erstellen von Speicherkonten](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Erstellen von Verfügbarkeitsgruppen
Erstellen Sie für jede Rolle (DC/AD FS und WAP) Verfügbarkeitsgruppen, die 2 Computern mindestens enthalten soll. Dadurch können höhere Verfügbarkeit für jede Rolle. Beim Erstellen der verfügbarkeitsgruppe festgelegt wird, ist es wichtig, Folgendes festlegen:

* **Fehlerdomänen**: Virtuelle Computer in der gleichen Fehlerdomäne gemeinsam nutzen, die gleiche Stromquelle und physischen Netzwerkswitch. Mindestens 2 Fehlerdomänen werden empfohlen. Der Standardwert ist 3, und lassen Sie ihn für diese Bereitstellung
* **Updatedomänen**: Computer, die der gleichen updatedomäne angehören, werden zusammen während eines Updates neu gestartet. Möchten Sie über mindestens 2 updatedomänen verfügen. Der Standardwert ist 5, und lassen Sie ihn für diese Bereitstellung

![Verfügbarkeitsgruppen](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

Erstellen Sie die folgenden Verfügbarkeitsgruppen:

| Verfügbarkeitsgruppe | Role-Eigenschaft | Fehlerdomänen | Updatedomänen |
|:---:|:---:|:---:|:--- |
| contosodcset |DC/ADFS |3 |5 |
| contosowapset |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Bereitstellung virtueller Maschinen
Der nächste Schritt ist zum Bereitstellen virtueller Computer, auf denen die verschiedenen Rollen in Ihrer Infrastruktur gehostet werden. Mindestens zwei Computer werden in jeder verfügbarkeitsgruppe empfohlen. Erstellen Sie vier virtuelle Computer für die grundlegende Bereitstellung.

| Computer | Role-Eigenschaft | Subnetz | Verfügbarkeitsgruppe | Storage-Konto | IP-Adresse |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |contosodcset |contososac1 |Statisch |
| contosodc2 |DC/ADFS |INT |contosodcset |contososac2 |Statisch |
| contosowap1 |WAP |DMZ |contosowapset |contososac1 |Statisch |
| contosowap2 |WAP |DMZ |contosowapset |contososac2 |Statisch |

Wie Sie bemerkt haben vielleicht, verfügt über keine NSG angegeben wurde. Dies ist, da es sich bei Azure, die Sie der NSG auf Subnetzebene verwenden kann. Anschließend können Sie den computerdatenverkehr steuern, durch die individuelle NSG verwenden entweder dem Subnetz oder andernfalls den NIC-Objekt zugeordnet. Weitere Informationen zum [was eine Netzwerksicherheitsgruppe (NSG) ist](https://aka.ms/Azure/NSG).
Statische IP-Adresse wird empfohlen, wenn Sie das DNS verwalten. Sie können Azure DNS verwenden und stattdessen in der DNS-Einträgen für Ihre Domäne verweisen, auf die neuen Computer über die Azure FQDNs.
Bereich für virtuelle Computer sollte wie folgt aussehen, nachdem die Bereitstellung abgeschlossen ist:

![Bereitgestellte virtuelle Computer](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. Konfigurieren des Domänencontrollers / AD FS-Server
 Um jede eingehende Anforderung authentifizieren zu können, müssen die AD FS auf dem Domänencontroller herstellen. Um die kostspielige Reise von Azure zum lokalen DC für die Authentifizierung zu speichern, wird empfohlen, ein Replikat des Domänencontrollers in Azure bereitstellen. Um hochverfügbarkeit zu erzielen, empfiehlt es zum Erstellen einer verfügbarkeitsgruppe mit mindestens 2-Domänencontroller.

| Domänencontroller | Role-Eigenschaft | Storage-Konto |
|:---:|:---:|:---:|
| contosodc1 |Replikat |contososac1 |
| contosodc2 |Replikat |contososac2 |

* Fördern Sie die beiden Server als Replikatdomänencontroller mit DNS
* Konfigurieren Sie die AD FS-Server durch Installieren der AD FS-Serverrolle mithilfe des Server-Managers.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Deploying Internal Load Balancer (ILB)
**6.1. Erstellen des ILB**

Zum Bereitstellen eines ILB hinzufügen auf Load Balancers im Azure-Portal und klicken Sie auf (+).

> [!NOTE]
> Wenn Sie nicht sehen **Load Balancer** klicken Sie im Menü auf **Durchsuchen** in der unteren linken Ecke des Portals und blättern Sie **Load Balancer**.  Klicken Sie dann auf den gelben Stern, um sie auf das Menü hinzuzufügen. Wählen Sie jetzt die neue Load Balancer-Symbol, öffnen Sie den Bereich, um die Konfiguration des Load Balancers zu beginnen.
> 
> 

![Load Balancer durchsuchen](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **Name**: Geben Sie einen anderen geeigneten Namen für dem Load balancer
* **Schema**: Da dieser Load Balancer vor den AD FS-Server platziert werden und für interne Netzwerkverbindungen nur gedacht ist, wählen Sie "Intern"
* **Virtual Network**: Wählen Sie das virtuelle Netzwerk, in dem Sie AD FS bereitstellen
* **Subnetz**: Wählen Sie hier das interne Subnetz
* **IP-Adresszuweisung**: Statisch

![Interner Load balancer](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

Nachdem Sie auf erstellen und der Bereitstellung des ILB, Sie sollten sehen, in der Liste der Load balancer:

![Load Balancers nach ILB](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

Als Nächstes wird zum Konfigurieren der Back-End-Pool und den Back-End-Test.

**6.2. Konfigurieren des ILB-Back-End-Pools**

Wählen Sie den neu erstellten ILB im Load Balancer. Der Einstellungsbereich wird geöffnet. 

1. Wählen Sie die Back-End-Pools aus den Einstellungsbereich
2. Klicken Sie im Back-End-Pool Bereich hinzufügen auf die virtuellen Computer hinzufügen
3. Es wird ein Bereich angezeigt werden, in dem Sie die verfügbarkeitsgruppe auswählen können
4. Wählen Sie die AD FS-verfügbarkeitsgruppe

![Konfigurieren des ILB-Back-End-Pools](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6.3. Konfigurieren des Tests**

Wählen Sie im Bereich mit den Einstellungen für ILB Integritätstests.

1. Klicken Sie auf Hinzufügen
2. Die Details für den Test ein. **Name**: Prüfpunkt Name b an. **Protokoll**: HTTP c. **Port**: 80 (HTTP) d. **Pfad**: / Adfs/Probe e. **Intervall**: 5 (Standardwert) – ist dies das Intervall, mit dem ILB die Computer im Back-End-Pool f suchen. **Fehlerschwellenwert**: 2 (Standardwert) – ist dies der Schwellenwert von aufeinander folgender Testfehler, die nach denen ILB einen Computer im Back-End-Pool nicht mehr reagiert und keinen Datenverkehr mehr sendet es deklarieren.

![Konfigurieren Sie die ILB-Test](./media/how-to-connect-fed-azure-adfs/ilbdeployment4.png)

Wir verwenden den Endpunkt festlegen, der explizit für integritätsprüfungen in einer AD FS-Umgebung erstellt wurde, in denen keine vollständige Überprüfung der HTTPS-Pfad möglich.  Dies ist wesentlich besser als eine basic-Port 443-Überprüfung, die den Status einer modernen AD FS-Bereitstellung nicht genau widerspiegelt.  Weitere Informationen hierzu finden Sie unter https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/.

**6.4. Erstellen von lastenausgleichsregeln**

Um den Datenverkehr effektiv ausgleichen zu können, sollte der ILB mit lastenausgleichsregeln konfiguriert werden. Um eine lastenausgleichsregel zu erstellen, 

1. Wählen Sie die Load Balancer-Regel im Einstellungsbereich "des ILB
2. Klicken Sie auf Hinzufügen klicken Sie im Bereich für den Lastenausgleich
3. In der hinzufügen-Lastenausgleich-Bedienfeld "Regel" ein. **Name**: Geben Sie einen Namen für die Regel b. **Protokoll**: Wählen Sie TCP-c. **Port**: 443. d. **Back-End-Port**: 443 e. **Back-End-Pool**: Wählen Sie den Pool, die, den Sie erstellt haben, für die AD FS-, früheren f Clusters. **Probe**: Wählen Sie den Test, der zuvor erstellten für AD FS-Server

![Konfigurieren Sie ILB-ausgleichsregeln](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6.5. Aktualisieren des DNS mit ILB**

Wechseln Sie zu Ihrem DNS-Server aus, und erstellen Sie einen CNAME-Eintrag für den ILB. Der CNAME sollte für den Verbunddienst mit der IP-Adresse, die auf die IP-Adresse des ILB verweisen. Für das Beispiel ist die ILB-DIP-Adresse 10.3.0.8 verwiesen, und der installierte Verbunddienst "FS.contoso.com" lautet, dann erstellen Sie einen CNAME-Eintrag für "FS.contoso.com" auf 10.3.0.8 verwiesen.
Dadurch wird sichergestellt, dass die gesamte Kommunikation in Bezug auf "FS.contoso.com" End über den ilb läuft und richtig weitergeleitet.

### <a name="7-configuring-the-web-application-proxy-server"></a>7. Konfigurieren des Webanwendungsproxy-Servers
**7.1. Konfigurieren der Webanwendungsproxy-Server für AD FS-Server zu erreichen.**

Um sicherzustellen, dass Webanwendungsproxy-Server die AD FS-Server hinter dem ILB erreichen können, erstellen Sie einen Eintrag in der %systemroot%\system32\drivers\etc\hosts für den ILB. Beachten Sie, dass der distinguished Name (DN) mit dem Namen des Verbunddiensts, z. B. "FS.contoso.com" werden soll. Und der IP-Eintrag sollte der ILB IP-Adresse (Beispiel 10.3.0.8).

**7.2. Installieren der Webanwendungsproxy-Rolle**

Nachdem Sie sichergestellt haben, dass Webanwendungsproxy-Server die AD FS-Server hinter dem ILB erreichen können, können Sie als Nächstes die Webanwendungsproxy-Server installieren. Webanwendungsproxy-Server müssen die Domäne nicht hinzugefügt werden. Installieren Sie die Webanwendungsproxy-Rollen auf den beiden Webanwendungsproxy-Servern, indem Sie die Remotezugriffs-Rolle auswählen. Der Server-Manager werden Sie zum Abschließen der WAP-Installation geführt.
Lesen Sie weitere Informationen zum Bereitstellen von WAP [installieren und konfigurieren Sie die Webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8.  Bereitstellen des (öffentlichen) Load Balancers mit Internetzugriff
**8.1.  Erstellen des (öffentlichen) Load Balancers mit Internetzugriff**

Klicken Sie im Azure-Portal wählen Sie Load Balancer, und klicken Sie dann auf Hinzufügen. Geben Sie die folgenden Informationen im Bereich Create Load balancer

1. **Name**: Namen für den Load balancer
2. **Schema**: Öffentlich – diese Option weist Azure, dass es sich bei diesen Load Balancer eine öffentliche Adresse erforderlich ist.
3. **IP-Adresse**: Erstellen Sie eine neue IP-Adresse (dynamisch)

![Lastenausgleichsmodul mit Internetzugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

Nach der Bereitstellung wird der Load Balancer in der Load Balancer-Liste angezeigt.

![Load Balancer-Liste](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8.2. Zuweisen einer DNS-Bezeichnung zur öffentlichen IP**

Klicken Sie auf den neu erstellten Load-Balancer-Eintrag in der Load Balancer-Bereich, um den Bereich für die Konfiguration zu öffnen. Führen Sie die folgenden Schritte aus, um die DNS-Bezeichnung für die öffentliche IP-Adresse zu konfigurieren:

1. Klicken Sie auf die öffentliche IP-Adresse. Dadurch wird den Bereich für die öffentliche IP-Adresse und die Einstellungen geöffnet.
2. Klicken Sie auf der Konfiguration
3. Geben Sie eine DNS-Bezeichnung. Dadurch werden die öffentlichen DNS-Bezeichnung, die Sie von überall, z.B. "contosofs.westus.cloudapp.Azure.com" zugreifen können. Sie können einen Eintrag im externen DNS für den Verbunddienst (z. B. "FS.contoso.com") hinzufügen, die in der DNS-Bezeichnung des externen Load Balancers (contosofs.westus.cloudapp.azure.com) aufgelöst wird.

![Konfigurieren des Load Balancers mit Internetzugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![Konfigurieren des Load Balancers (DNS) für den Internetzugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8.3. Konfigurieren Sie für den Internetzugriff (öffentlichen) Load Balancer-Back-End-pool** 

Führen Sie die gleichen Schritte wie beim Erstellen der internen Load Balancer, um die Back-End-Adresspool für den Internetzugriff (öffentlichen) Load Balancer als der verfügbarkeitsgruppe für die WAP-Server zu konfigurieren. Zum Beispiel: "contosowapset".

![Konfigurieren des Back-End-Pools des öffentlichen Lastenausgleichs](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8.4. Konfigurieren des Tests**

Führen Sie die gleichen Schritte wie beim Konfigurieren des internen Load Balancers, um den Test für den Back-End-Pool von WAP-Servern konfigurieren.

![Konfigurieren Sie die Überprüfung des öffentlichen Lastenausgleichs](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8.5. Erstellen von lastenausgleichsregeln**

Führen Sie die gleichen Schritte wie für den ILB so konfigurieren Sie die lastenausgleichsregel für TCP 443.

![Ausgleichsregeln für Load Balancer, die Internet mit Internetzugriff konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. Schützen des Netzwerks
**9.1. Schützen des internen Subnetzes**

Generell benötigen Sie die folgenden Regeln, um Ihr internes Subnetz (in der Reihenfolge der unten aufgeführten) effizient zu sichern.

| Regel | Beschreibung | Fluss |
|:--- |:--- |:---:|
| AllowHTTPSFromDMZ |Die HTTPS-Kommunikation von DMZ zulassen |Inbound |
| DenyInternetOutbound |Kein Zugriff auf das internet |Outbound |

![INT-Zugriffsregeln (eingehend)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9.2. Schützen des DMZ-Subnetzes**

| Regel | Beschreibung | Fluss |
|:--- |:--- |:---:|
| AllowHTTPSFromInternet |HTTPS aus dem Internet an die DMZ zulassen |Inbound |
| DenyInternetOutbound |Alles außer HTTPS-VERBINDUNGEN zum Internet blockiert |Outbound |

![EXT-Zugriffsregeln (eingehend)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> Wenn der Clientbenutzer-Zertifikatauthentifizierung (ClientTLS-Authentifizierung mit X509 von Benutzerzertifikaten) erforderlich ist, und klicken Sie dann die AD FS TCP erfordert Port 49443 für eingehenden Zugriff aktiviert werden.
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10. Testen der AD FS-Anmeldung
Die einfachste Möglichkeit ist, werden zum Testen der AD FS mithilfe der Seite "IdpInitiatedSignon.aspx". Damit Sie so vorgehen, es ist erforderlich, um auf die AD FS-Eigenschaften "idpinitiatedsignon" zu aktivieren. Führen Sie die Schritte unten aus, um die AD FS-Installation überprüfen

1. Führen Sie die unten angegebene Cmdlet auf dem AD FS-Server mithilfe von PowerShell, um es "aktiviert" festzulegen.
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true 
2. Zugriff auf alle externen Computer, die Https:\//adfs-server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx.  
3. Daraufhin sollte die AD FS-Seite wie die folgende:

![Anmeldeseite testen](./media/how-to-connect-fed-azure-adfs/test1.png)

Bei erfolgreicher Anmeldung werden sie Sie mit einer Erfolgsmeldung bereitstellen wie unten dargestellt:

![Erfolgreiche Durchführung testen](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Vorlage für die Bereitstellung von AD FS in Azure
Die Vorlage stellt ein 6-Computer-Setup, je 2 für Domänencontroller, AD FS und WAP bereit.

[AD FS in Azure – Bereitstellungsvorlage](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Sie können ein vorhandenes virtuelles Netzwerk verwenden oder ein neues VNET erstellen, beim Bereitstellen der Vorlage. Die verschiedenen verfügbaren Parameter für die Bereitstellung anpassen sind unten aufgeführt, mit der Beschreibung der Verwendung des Parameters im Bereitstellungsprozess. 

| Parameter | Beschreibung |
|:--- |:--- |
| Speicherort |Die Region, die Ressourcen in, z. B. Osten USA bereitzustellen. |
| StorageAccountType |Der Typ des Speicherkontos erstellt |
| VirtualNetworkUsage |Gibt an, ob ein neues virtuelles Netzwerk erstellt werden, oder eine bereits vorhandene verwenden |
| VirtualNetworkName |Der Name des virtuellen Netzwerks zu erstellen, die Nutzung von vorhandenen oder neuen virtuellen Netzwerks obligatorisch. |
| VirtualNetworkResourceGroupName |Gibt den Namen der Ressourcengruppe, in dem das vorhandene virtuelle Netzwerk befindet. Wenn Sie ein vorhandenes virtuelles Netzwerk verwenden möchten, ist dies ein obligatorischer Parameter, damit die Bereitstellung in die ID des vorhandenen virtuellen Netzwerks zu ermitteln |
| VirtualNetworkAddressRange |Der Adressbereich des neuen VNET erforderlich, wenn ein neues virtuelles Netzwerk erstellen |
| InternalSubnetName |Der Name des internen Subnetzes, diese obligatorisch beide virtuelle Netzwerke (neu oder vorhanden) |
| InternalSubnetAddressRange |Der Adressbereich des internen Subnetzes, das die Domänencontroller und AD FS-Server erforderliche enthält, wenn ein neues virtuelles Netzwerk erstellen. |
| DMZSubnetAddressRange |Der Adressbereich des dmz-Subnetzes, das die Windows-Proxyservern, obligatorische enthält, wenn ein neues virtuelles Netzwerk erstellen. |
| DMZSubnetName |Der Name des internen Subnetzes, diese obligatorisch beide virtuelle Netzwerke (neu oder vorhanden). |
| ADDC01NICIPAddress |Die interne IP-Adresse des ersten Domänencontrollers, diese IP-Adresse wird dem Domänencontroller statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein |
| ADDC02NICIPAddress |Die interne IP-Adresse des zweiten Domänencontrollers, diese IP-Adresse wird dem Domänencontroller statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein |
| ADFS01NICIPAddress |Die interne IP-Adresse des ersten AD FS-Servers, diese IP-Adresse wird zum ADFS-Server statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein |
| ADFS02NICIPAddress |Die interne IP-Adresse des zweiten AD FS-Servers, diese IP-Adresse wird zum ADFS-Server statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein |
| WAP01NICIPAddress |Die interne IP-Adresse des ersten WAP-Servers, diese IP-Adresse wird dem WAP-Server statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des DMZ-Subnetzes sein |
| WAP02NICIPAddress |Die interne IP-Adresse des zweiten WAP-Servers, diese IP-Adresse wird dem WAP-Server statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des DMZ-Subnetzes sein |
| ADFSLoadBalancerPrivateIPAddress |Die interne IP-Adresse des AD FS-Lastenausgleichs, diese IP-Adresse des Load Balancers wird statisch zugewiesen werden und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein |
| ADDCVMNamePrefix |VM-Namenspräfix für Domänencontroller |
| ADFSVMNamePrefix |VM-Namenspräfix für AD FS-Server |
| WAPVMNamePrefix |VM-Namenspräfix für WAP-Server |
| ADDCVMSize |Die Vm-Größe der Domänencontroller |
| ADFSVMSize |Vm-Größe der AD FS-Server |
| WAPVMSize |Die Vm-Größe der WAP-Server |
| AdminUserName |Der Name des lokalen Administrators der virtuellen Computer |
| AdminPassword |Das Kennwort für das lokale Administratorkonto der virtuellen Computer |

## <a name="additional-resources"></a>Zusätzliche Ressourcen
* [Verfügbarkeitsgruppen](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [Interner Load Balancer](https://aka.ms/Azure/ILB/Internal)
* [Internet Load-Balancer mit Internetzugriff](https://aka.ms/Azure/ILB/Internet)
* [Storage-Konten](https://aka.ms/Azure/Storage)
* [Virtuelle Azure-Netzwerke](https://aka.ms/Azure/VNet)
* [AD FS und Webanwendungsproxy-Links](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Nächste Schritte
* [Integrieren Ihrer lokalen Identitäten in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity)
* [Konfigurieren und Verwalten von AD FS mit Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Hohe Verfügbarkeit gebietsübergreifende AD FS-Bereitstellung in Azure mit Azure Traffic Manager](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
