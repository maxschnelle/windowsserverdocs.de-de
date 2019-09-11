---
title: Active Directory-Verbunddienste (AD FS) in Azure | Microsoft-Dokumentation
description: In diesem Dokument erfahren Sie, wie Sie AD FS in Azure bereitstellen, um eine hohe Verfügbarkeit zu erhalten.
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
ms.openlocfilehash: 15ebf21973f78ad705aca77e178005dfa9529cf2
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70868220"
---
# <a name="deploying-active-directory-federation-services-in-azure"></a>Bereitstellen von Active Directory-Verbunddienste (AD FS) in Azure
AD FS bietet vereinfachte, gesicherte Funktionen für Identitäts Verbund und Web Single Sign-on (SSO). Der Verbund mit Azure AD oder O365 ermöglicht es Benutzern, sich mit lokalen Anmelde Informationen zu authentifizieren und auf alle Ressourcen in der Cloud zuzugreifen. Daher ist es wichtig, dass Sie über eine hoch verfügbare AD FS-Infrastruktur verfügen, um den Zugriff auf Ressourcen sowohl lokal als auch in der Cloud sicherzustellen. Wenn Sie AD FS in Azure bereitstellen, können Sie die Hochverfügbarkeit mit minimalem Aufwand erreichen.
Es gibt mehrere Vorteile beim Bereitstellen von AD FS in Azure, einige davon sind unten aufgeführt:

* **Hohe Verfügbarkeit** : mit der Leistungsfähigkeit von Azure-Verfügbarkeits Gruppen stellen Sie eine hochverfügbare Infrastruktur sicher.
* **Leicht skalierbar** – benötigen Sie mehr Leistung? Einfache Migration zu leistungsfähigeren Computern mit wenigen Klicks in Azure
* Regions **übergreifende Redundanz** – mit der georedundanz von Azure können Sie sicher sein, dass Ihre Infrastruktur auf der ganzen Welt hoch verfügbar ist.
* **Einfache** Verwaltung – mit stark vereinfachten Verwaltungs Optionen in Azure-Portal ist die Verwaltung Ihrer Infrastruktur sehr einfach und unkompliziert. 

## <a name="design-principles"></a>Designprinzipien
![Bereitstellungs Entwurf](./media/how-to-connect-fed-azure-adfs/deployment.png)

Das obige Diagramm zeigt die empfohlene grundlegende Topologie, um mit der Bereitstellung Ihrer AD FS Infrastruktur in Azure zu beginnen. Die Prinzipien hinter den verschiedenen Komponenten der Topologie sind unten aufgeführt:

* **DC/ADFS-Server**: Wenn Sie weniger als 1.000 Benutzer haben, können Sie einfach AD FS Rolle auf Ihren Domänen Controllern installieren. Wenn Sie keine Auswirkungen auf die Leistung der Domänen Controller haben oder mehr als 1.000 Benutzer haben, stellen Sie AD FS auf separaten Servern bereit.
* **WAP-Server** – es ist erforderlich, webanwendungsproxy-Server bereitzustellen, damit Benutzer die AD FS erreichen können, wenn Sie sich auch nicht im Unternehmensnetzwerk befinden.
* **DMZ**: Die webanwendungsproxy-Server werden in der DMZ platziert, und nur der TCP/443-Zugriff ist zwischen der DMZ und dem internen Subnetz zulässig.
* **Lasten Ausgleichs**Module: Um die Hochverfügbarkeit von AD FS und webanwendungsproxy-Servern sicherzustellen, empfehlen wir die Verwendung eines internen Load Balancers für AD FS Server und Azure Load Balancer für webanwendungsproxy-Server
* **Verfügbarkeits Gruppen**: Um Redundanz für Ihre AD FS-Bereitstellung bereitzustellen, empfiehlt es sich, mindestens zwei virtuelle Computer in einer Verfügbarkeits Gruppe für ähnliche Workloads zu gruppieren. Durch diese Konfiguration wird sichergestellt, dass während eines geplanten oder ungeplanten Wartungs Ereignisses mindestens ein virtueller Computer verfügbar ist.
* **Speicher Konten**: Es wird empfohlen, zwei Speicher Konten zu haben. Ein einzelnes Speicherkonto kann dazu führen, dass eine Single Point of Failure erstellt wird, und kann dazu führen, dass die Bereitstellung in einem unwahrscheinlichen Szenario, in dem das Speicherkonto ausfällt, nicht mehr verfügbar ist. Zwei Speicher Konten helfen dabei, ein Speicherkonto für jede Fehler Zeile zuzuordnen.
* **Netzwerk Trennung**:  Webanwendungsproxy-Server sollten in einem separaten DMZ-Netzwerk bereitgestellt werden. Sie können ein virtuelles Netzwerk in zwei Subnetze aufteilen und dann die webanwendungsproxy-Server in einem isolierten Subnetz bereitstellen. Sie können einfach die Einstellungen für die Netzwerk Sicherheitsgruppe für jedes Subnetz konfigurieren und nur die erforderliche Kommunikation zwischen den beiden Subnetzen zulassen. Je nach Bereitstellungs Szenario werden weitere Details angegeben.

## <a name="steps-to-deploy-ad-fs-in-azure"></a>Schritte zum Bereitstellen von AD FS in Azure
In den Schritten in diesem Abschnitt wird erläutert, wie Sie die unten dargestellte AD FS-Infrastruktur in Azure bereitstellen.

### <a name="1-deploying-the-network"></a>1. Bereitstellen des Netzwerks
Wie oben beschrieben, können Sie entweder zwei Subnetze in einem einzelnen virtuellen Netzwerk erstellen oder zwei vollständig unterschiedliche virtuelle Netzwerke (vnet) erstellen. Dieser Artikel konzentriert sich auf die Bereitstellung eines einzelnen virtuellen Netzwerks und das Aufteilen in zwei Subnetze. Dies ist zurzeit ein einfacherer Ansatz, da für zwei separate vnets ein vnet-zu-vnet-Gateway für die Kommunikation erforderlich ist.

**1,1 Erstellen eines virtuellen Netzwerks**

![Virtuelles Netzwerk erstellen](./media/how-to-connect-fed-azure-adfs/deploynetwork1.png)

Wählen Sie im Azure-Portal die Option virtuelles Netzwerk aus, und Sie können das virtuelle Netzwerk und ein Subnetz sofort mit nur einem Mausklick bereitstellen. Das int-Subnetz ist ebenfalls definiert und jetzt zum Hinzufügen von VMS bereit.
Der nächste Schritt besteht darin, dem Netzwerk ein weiteres Subnetz hinzuzufügen, d. h. das DMZ-Subnetz. Um das DMZ-Subnetz zu erstellen, können Sie einfach

* Wählen Sie das neu erstellte Netzwerk aus.
* Wählen Sie in den Eigenschaften Subnetz aus.
* Klicken Sie im Subnetzbereich auf die Schaltfläche hinzufügen.
* Geben Sie den Subnetznamen und die Adressraum Informationen zum Erstellen des Subnetzes an.

![Subnetz](./media/how-to-connect-fed-azure-adfs/deploynetwork2.png)

![Subnetz DMZ](./media/how-to-connect-fed-azure-adfs/deploynetwork3.png)

**1,2. Erstellen der Netzwerk Sicherheitsgruppen**

Eine Netzwerk Sicherheitsgruppe (NSG) enthält eine Liste von Regeln für die Access Control Liste (ACL), mit denen Netzwerk Datenverkehr für Ihre VM-Instanzen in einem Virtual Network zugelassen oder verweigert wird. Nsgs können entweder Subnetzen oder einzelnen VM-Instanzen in diesem Subnetz zugeordnet werden. Wenn eine NSG einem Subnetz zugeordnet ist, gelten die ACL-Regeln für alle VM-Instanzen in diesem Subnetz.
Im Rahmen dieser Anleitung werden zwei nsgs erstellt: jeweils eine für ein internes Netzwerk und eine DMZ. Sie werden als NSG_INT bzw. NSG_DMZ bezeichnet.

![Erstellen einer NSG](./media/how-to-connect-fed-azure-adfs/creatensg1.png)

Nachdem die NSG erstellt wurde, gibt es 0 eingehende und 0 ausgehende Regeln. Nachdem die Rollen auf den jeweiligen Servern installiert und funktionsfähig sind, können die eingehenden und ausgehenden Regeln entsprechend der gewünschten Sicherheitsstufe vorgenommen werden.

![Initialisieren der NSG](./media/how-to-connect-fed-azure-adfs/nsgint1.png)

Nachdem die nsgs erstellt wurden, ordnen Sie NSG_INT mit Subnetz int und NSG_DMZ mit Subnetz DMZ zu. Der folgende Screenshot zeigt ein Beispiel:

![NSG konfigurieren](./media/how-to-connect-fed-azure-adfs/nsgconfigure1.png)

* Klicken Sie auf Subnetze, um den Bereich für Subnetze zu öffnen.
* Wählen Sie das Subnetz aus, das der NSG zugeordnet werden soll. 

Nach der Konfiguration sollte der Bereich für Subnetze wie folgt aussehen:

![Subnetze nach NSG](./media/how-to-connect-fed-azure-adfs/nsgconfigure2.png)

**1,3. Verbindung mit lokalem Standort erstellen**

Wir benötigen eine Verbindung mit dem lokalen Standort, um den Domänen Controller (DC) in Azure bereitzustellen. Azure bietet verschiedene Konnektivitätsoptionen, um Ihre lokale Infrastruktur mit ihrer Azure-Infrastruktur zu verbinden.

* Punkt-zu-Standort
* Standort-zu-Standort-Virtual Network
* ExpressRoute

Es wird empfohlen, expressroute zu verwenden. Mit expressroute können Sie private Verbindungen zwischen Azure-Rechenzentren und der Infrastruktur erstellen, die sich an Ihrem Standort oder in einer Co-Location-Umgebung befindet. Expressroute-Verbindungen werden nicht über das öffentliche Internet geleitet. Sie bieten mehr Zuverlässigkeit, schnellere Geschwindigkeiten, geringere Latenzzeiten und mehr Sicherheit als herkömmliche Verbindungen über das Internet.
Obwohl es empfohlen wird, expressroute zu verwenden, können Sie eine beliebige Verbindungsmethode auswählen, die für Ihre Organisation am besten geeignet ist. Weitere Informationen zu expressroute und den verschiedenen Konnektivitätsoptionen mithilfe von expressroute finden Sie unter [expressroute Technical Overview](https://aka.ms/Azure/ExpressRoute).

### <a name="2-create-storage-accounts"></a>2. Erstellen von Speicher Konten
Um Hochverfügbarkeit zu gewährleisten und die Abhängigkeit von einem einzelnen Speicherkonto zu vermeiden, können Sie zwei Speicher Konten erstellen. Unterteilen Sie die Computer in jeder Verfügbarkeits Gruppe in zwei Gruppen, und weisen Sie jeder Gruppe dann ein separates Speicherkonto zu.

![Erstellen von Speicher Konten](./media/how-to-connect-fed-azure-adfs/storageaccount1.png)

### <a name="3-create-availability-sets"></a>3. Erstellen von Verfügbarkeits Gruppen
Erstellen Sie für jede Rolle (DC/AD FS und WAP) Verfügbarkeits Gruppen, die mindestens zwei Computer enthalten. Dadurch erhalten Sie eine höhere Verfügbarkeit für jede Rolle. Beim Erstellen der Verfügbarkeits Gruppen ist es von entscheidender Bedeutung, Folgendes zu bestimmen:

* **Fehler Domänen**: Virtuelle Computer in derselben Fehler Domäne nutzen denselben Stromquellen-und physischen Netzwerk Switch. Es werden mindestens 2 Fehler Domänen empfohlen. Der Standardwert ist 3, und Sie können ihn für diese Bereitstellung unverändert lassen.
* **Update Domänen**: Computer, die derselben Update Domäne angehören, werden während eines Updates neu gestartet. Sie möchten mindestens zwei Update Domänen haben. Der Standardwert ist 5, und Sie können ihn für diese Bereitstellung unverändert lassen.

![Verfügbarkeits Gruppen](./media/how-to-connect-fed-azure-adfs/availabilityset1.png)

Erstellen Sie die folgenden Verfügbarkeits Gruppen.

| Verfügbarkeits Gruppe | Rolle | Fehlerdomänen | Aktualisieren von Domänen |
|:---:|:---:|:---:|:--- |
| Conto sodcset |DC/ADFS |3 |5 |
| "Configuration Manager-apset" |WAP |3 |5 |

### <a name="4-deploy-virtual-machines"></a>4. Bereitstellung virtueller Maschinen
Der nächste Schritt besteht darin, virtuelle Computer bereitzustellen, auf denen die verschiedenen Rollen in Ihrer Infrastruktur gehostet werden. Mindestens zwei Computer werden in jeder Verfügbarkeits Gruppe empfohlen. Erstellen Sie vier virtuelle Computer für die grundlegende Bereitstellung.

| Computer | Rolle | Subnetz | Verfügbarkeitsgruppe | Speicherkonto | IP-Adresse |
|:---:|:---:|:---:|:---:|:---:|:---:|
| contosodc1 |DC/ADFS |INT |Conto sodcset |contososac1 |Statisch |
| contosodc2 |DC/ADFS |INT |Conto sodcset |contososac2 |Statisch |
| contosowap1 |WAP |DMZ |"Configuration Manager-apset" |contososac1 |Statisch |
| contosowap2 |WAP |DMZ |"Configuration Manager-apset" |contososac2 |Statisch |

Wie Sie vielleicht bemerkt haben, wurde keine NSG angegeben. Dies liegt daran, dass Sie mit Azure NSG auf Subnetzebene verwenden können. Anschließend können Sie den Computernetzwerk Datenverkehr mithilfe der einzelnen NSG steuern, die entweder dem Subnetz oder dem NIC-Objekt zugeordnet ist. Weitere Informationen finden Sie unter [Was ist eine Netzwerk Sicherheitsgruppe (NSG)](https://aka.ms/Azure/NSG)?.
Die statische IP-Adresse wird empfohlen, wenn Sie das DNS verwalten. Sie können Azure DNS und stattdessen in den DNS-Einträgen für Ihre Domäne verwenden. Weitere Informationen hierzu finden Sie unter den neuen Computern Ihrer Azure-FQDNs.
Der Bereich Ihres virtuellen Computers sollte nach Abschluss der Bereitstellung wie folgt aussehen:

![Virtual Machines bereitgestellt](./media/how-to-connect-fed-azure-adfs/virtualmachinesdeployed_noadfs.png)

### <a name="5-configuring-the-domain-controller--ad-fs-servers"></a>5. Konfigurieren der Domänen Controller/AD FS Server
 Um eingehende Anforderungen zu authentifizieren, muss AD FS den Domänen Controller kontaktieren. Es wird empfohlen, ein Replikat des Domänen Controllers in Azure bereitzustellen, um die teure Reise von Azure zum lokalen DC für die Authentifizierung zu sparen. Um Hochverfügbarkeit zu erreichen, empfiehlt es sich, eine Verfügbarkeits Gruppe von mindestens zwei Domänen Controllern zu erstellen.

| Domänencontroller | Rolle | Speicherkonto |
|:---:|:---:|:---:|
| contosodc1 |Replikat |contososac1 |
| contosodc2 |Replikat |contososac2 |

* Herauf Stufen der beiden Server als Replikat Domänen Controller mit DNS
* Konfigurieren Sie die AD FS Server, indem Sie die AD FS Rolle mithilfe des Server-Managers installieren.

### <a name="6-deploying-internal-load-balancer-ilb"></a>6. Bereitstellen interner Load Balancer (ILB)
**6,1. Erstellen des ILB**

Wählen Sie zum Bereitstellen eines ILB im Azure-Portal die Option Load Balancer aus, und klicken Sie auf hinzufügen (+).

> [!NOTE]
> Wenn **Load Balancer** im Menü nicht angezeigt werden, klicken Sie unten links im Portal auf **Durchsuchen** , und Scrollen Sie so lange, bis die **Load Balancer**angezeigt werden.  Klicken Sie dann auf den gelben Stern, um ihn dem Menü hinzuzufügen. Wählen Sie nun das Symbol neues Lasten Ausgleichs Modul aus, um den Bereich zu öffnen und mit der Konfiguration des Load Balancers zu beginnen.
> 
> 

![Lasten Ausgleichs Modul durchsuchen](./media/how-to-connect-fed-azure-adfs/browseloadbalancer.png)

* **Name**: Legen Sie dem Load Balancer einen passenden Namen zu.
* **Schema**: Da dieser Load Balancer vor den AD FS Servern platziert wird und nur für interne Netzwerkverbindungen gedacht ist, wählen Sie "intern" aus.
* **Virtual Network**: Wählen Sie das virtuelle Netzwerk aus, in dem Sie Ihre AD FS bereitstellen.
* **Subnetz**: Wählen Sie hier das interne Subnetz aus.
* **IP-Adresszuweisung**: Statisch

![Interner Load Balancer](./media/how-to-connect-fed-azure-adfs/ilbdeployment1.png)

Nachdem Sie auf Erstellen und das ILB bereitgestellt haben, sollte es in der Liste der Load Balancer angezeigt werden:

![Lasten Ausgleichs Module nach ILB](./media/how-to-connect-fed-azure-adfs/ilbdeployment2.png)

Im nächsten Schritt konfigurieren Sie den Back-End-Pool und den Back-End-Test.

**6,2. ILB-Backend-Pool konfigurieren**

Wählen Sie im Bereich "Lasten Ausgleichs Module" den neu erstellten ILB aus. Der Bereich "Einstellungen" wird geöffnet. 

1. Wählen Sie im Einstellungsbereich Back-End-Pools aus.
2. Klicken Sie im Bereich Back-End-Pool hinzufügen auf virtuellen Computer hinzufügen.
3. Ihnen wird ein Bereich angezeigt, in dem Sie die Verfügbarkeits Gruppe auswählen können.
4. AD FS Verfügbarkeits Gruppe auswählen

![ILB-Backend-Pool konfigurieren](./media/how-to-connect-fed-azure-adfs/ilbdeployment3.png)

**6,3. Konfigurieren des Tests**

Wählen Sie im Bereich ILB-Einstellungen die Option Integritätstests aus.

1. Klicken Sie auf Hinzufügen
2. Stellen Sie Details für Test a bereit. **Name**: Testname b. **Protokoll**: HTTP c. **Port**: 80 (http) d. **Pfad**:/ADFS/Probe e. **Intervall**: 5 (Standardwert) – Dies ist das Intervall, in dem ILB die Computer im Back-End-Pool f testet. Fehlerhafter **Schwellenwert Grenzwert**: 2 (Standardwert) – Dies ist der Schwellenwert von aufeinander folgenden Test Fehlern, nach denen der ILB einen Computer im Back-End-Pool als nicht reagierend deklariert und keinen Datenverkehr mehr an ihn sendet.

![ILB-Test konfigurieren](./media/how-to-connect-fed-azure-adfs/ilbdeployment4.png)

Wir verwenden den/ADFS/Probe-Endpunkt, der explizit für Integritäts Überprüfungen in einer AD FS Umgebung erstellt wurde, in der keine vollständige HTTPS-Pfad Überprüfung erfolgen kann.  Dies ist wesentlich besser als bei einer grundlegenden Port 443-Überprüfung, die den Status einer modernen AD FS Bereitstellung nicht exakt widerspiegelt.  Weitere Informationen hierzu finden Sie unter https://blogs.technet.microsoft.com/applicationproxyblog/2014/10/17/hardware-load-balancer-health-checks-and-web-application-proxy-ad-fs-2012-r2/.

**6,4. Erstellen von Lasten Ausgleichs Regeln**

Um den Datenverkehr effektiv auszugleichen, sollte der ILB mit Lasten Ausgleichs Regeln konfiguriert werden. Um eine Lasten Ausgleichs Regel zu erstellen, 

1. Wählen Sie im Bereich "Einstellungen" des ILB die Lasten Ausgleichs Regel aus.
2. Klicken Sie im Bereich "Lasten Ausgleichs Regel" auf hinzufügen.
3. Im Bereich "Lasten Ausgleichs Regel hinzufügen". **Name**: Geben Sie einen Namen für die Regel b an. **Protokoll**: Wählen Sie TCP c aus. **Port**: 443 d. **Backend-Port**: 443 e. **Backend-Pool**: Wählen Sie den Pool aus, den Sie zuvor für den AD FS Cluster f erstellt haben. Test: Wählen Sie den zuvor für AD FS Server erstellten Test aus.

![Konfigurieren von ILB-Ausgleichs Regeln](./media/how-to-connect-fed-azure-adfs/ilbdeployment5.png)

**6,5. Aktualisieren von DNS mit ILB**

Wechseln Sie zu Ihrem DNS-Server, und erstellen Sie einen CNAME für den ILB. Der CNAME muss für den Verbund Dienst mit der IP-Adresse sein, die auf die IP-Adresse des ILB verweist. Wenn die ILB-DIP-Adresse beispielsweise 10.3.0.8 und der Verbund Dienst FS.contoso.com lautet, erstellen Sie einen CNAME für FS.contoso.com, der auf 10.3.0.8 zeigt.
Dadurch wird sichergestellt, dass die gesamte Kommunikation bezüglich FS.contoso.com am ILB endet und entsprechend weitergeleitet wird.

### <a name="7-configuring-the-web-application-proxy-server"></a>7. Konfigurieren des webanwendungsproxy-Servers
**7,1. Konfigurieren der webanwendungsproxy-Server für das erreichen AD FS Server**

Um sicherzustellen, dass webanwendungsproxy-Server die AD FS Server hinter dem ILB erreichen können, erstellen Sie einen Datensatz in%SystemRoot%\system32\drivers\etc\hosts für den ILB. Beachten Sie, dass der Distinguished Name (DN) der Verbund Dienst Name (z. b. fs.contoso.com) sein sollte. Und der IP-Eintrag sollte die IP-Adresse des ILB lauten (wie im Beispiel 10.3.0.8).

**7,2. Installieren der webanwendungsproxy-Rolle**

Nachdem Sie sichergestellt haben, dass webanwendungsproxy-Server die AD FS Server hinter ILB erreichen können, können Sie als nächstes die webanwendungsproxy-Server installieren. Webanwendungsproxy-Server müssen nicht der Domäne hinzugefügt werden. Installieren Sie die webanwendungsproxy-Rollen auf den beiden webanwendungsproxy-Servern, indem Sie die Rolle RAS Der Server-Manager führt Sie durch den Abschluss der WAP-Installation.
Weitere Informationen zum Bereitstellen von WAP finden Sie unter [Installieren und Konfigurieren des webanwendungsproxy-Servers](https://technet.microsoft.com/library/dn383662.aspx).

### <a name="8--deploying-the-internet-facing-public-load-balancer"></a>8.  Bereitstellen der (öffentlichen) Load Balancer mit Internet Zugriff
**8,1.  Erstellen (Public) mit Internet Zugriff (öffentlich) Load Balancer**

Wählen Sie im Azure-Portal die Option Lasten Ausgleichs Module aus, und klicken Sie dann auf hinzufügen. Geben Sie im Panel Load Balancer erstellen die folgenden Informationen ein:

1. **Name**: Name des Load Balancers
2. **Schema**: Öffentlich – diese Option weist Azure an, dass dieser Load Balancer eine öffentliche Adresse benötigt.
3. **IP-Adresse**: Neue IP-Adresse erstellen (dynamisch)

![Load Balancer mit Internet Zugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment1.png)

Nach der Bereitstellung wird der Load Balancer in der Liste der Lasten Ausgleichs Module angezeigt.

![Liste der Lasten Ausgleichs Module](./media/how-to-connect-fed-azure-adfs/elbdeployment2.png)

**8,2. Zuweisen einer DNS-Bezeichnung zur öffentlichen IP-Adresse**

Klicken Sie im Bereich "Lasten Ausgleichs Module" auf den neu erstellten Load Balancer-Eintrag, um den Bereich für die Konfiguration zu aktivieren. Führen Sie die folgenden Schritte aus, um die DNS-Bezeichnung für die öffentliche IP zu konfigurieren:

1. Klicken Sie auf die öffentliche IP-Adresse. Dadurch wird der Bereich für die öffentliche IP-Adresse und die zugehörigen Einstellungen geöffnet.
2. Klicken Sie auf Konfiguration.
3. Geben Sie eine DNS-Bezeichnung an. Dies wird zu der öffentlichen DNS-Bezeichnung, auf die Sie von überall aus zugreifen können, z. b. contosofs.westus.cloudapp.Azure.com. Sie können einen Eintrag im externen DNS für den Verbund Dienst (z. b. fs.contoso.com) hinzufügen, der in die DNS-Bezeichnung des externen Load Balancers (contosofs.westus.cloudapp.Azure.com) aufgelöst wird.

![Konfigurieren des Load Balancers mit Internet Zugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment3.png) 

![Konfigurieren des Load Balancers mit Internet Zugriff (DNS)](./media/how-to-connect-fed-azure-adfs/elbdeployment4.png)

**8,3. Konfigurieren des Back-End-Pools für Load Balancer mit Internet Zugriff (Public)** 

Führen Sie dieselben Schritte wie bei der Erstellung des internen Load Balancers aus, um den Back-End-Pool für die Load Balancer mit Internet Zugriff (Public) als Verfügbarkeits Gruppe für die WAP-Server zu konfigurieren. Beispiel: "".

![Konfigurieren des Back-End-Pools für Load Balancer mit Internet Zugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment5.png)

**8,4. Test konfigurieren**

Führen Sie dieselben Schritte wie beim Konfigurieren des internen Load Balancers aus, um den Test für den Back-End-Pool von WAP-Servern zu konfigurieren.

![Überprüfung der Load Balancer mit Internet Zugriff konfigurieren](./media/how-to-connect-fed-azure-adfs/elbdeployment6.png)

**8,5. Erstellen von Lasten Ausgleichs Regeln**

Führen Sie die gleichen Schritte wie in ILB aus, um die Lasten Ausgleichs Regel für TCP 443 zu konfigurieren.

![Konfigurieren von Ausgleichs Regeln für Load Balancer mit Internet Zugriff](./media/how-to-connect-fed-azure-adfs/elbdeployment7.png)

### <a name="9-securing-the-network"></a>9. Sichern des Netzwerks
**9,1. Sichern des internen Subnetzes**

Insgesamt benötigen Sie die folgenden Regeln, um das interne Subnetz effizient zu schützen (in der unten aufgeführten Reihenfolge).

| Regel | Beschreibung | Fluss |
|:--- |:--- |:---:|
| "Zuweisung" |HTTPS-Kommunikation mit DMZ zulassen |Inbound |
| Denyinternetoutbound |Kein Zugriff auf das Internet |Outbound |

![INT-Zugriffsregeln (eingehend)](./media/how-to-connect-fed-azure-adfs/nsg_int.png)

**9,2. Sichern des DMZ-Subnetzes**

| Regel | Beschreibung | Fluss |
|:--- |:--- |:---:|
| "Zuweisung mit dem Internet" |HTTPS aus dem Internet mit der DMZ zulassen |Inbound |
| Denyinternetoutbound |Alles außer HTTPS und Internet ist blockiert. |Outbound |

![EXT-Zugriffsregeln (eingehend)](./media/how-to-connect-fed-azure-adfs/nsg_dmz.png)

> [!NOTE]
> Wenn die Client Zertifikat Authentifizierung (clienttls-Authentifizierung mit X509-Benutzer Zertifikaten) erforderlich ist, muss für AD FS der TCP-Port 49443 für den eingehenden Zugriff aktiviert werden.
> 
> 

### <a name="10-test-the-ad-fs-sign-in"></a>10. Testen der AD FS Anmeldung
Die einfachste Möglichkeit besteht darin, AD FS auf der Seite idpinitiatedsignon. aspx zu testen. Um dies zu erreichen, ist es erforderlich, idpinitiatedsignon in den AD FS Eigenschaften zu aktivieren. Führen Sie die folgenden Schritte aus, um das AD FS Setup zu überprüfen

1. Führen Sie das folgende Cmdlet auf dem AD FS Server mithilfe von PowerShell aus, um es auf "aktiviert" festzulegen.
   Set-ADF sproperties-enableidpinitiatedsignonpage $true 
2. Greifen Sie von einem beliebigen externen Computer aus\/auf https:/ADFS-Server.contoso.com/adfs/ls/IdpInitiatedSignon.aspx zu.  
3. Die AD FS Seite sollte wie folgt angezeigt werden:

![Test Anmeldeseite](./media/how-to-connect-fed-azure-adfs/test1.png)

Bei erfolgreicher Anmeldung wird Ihnen eine Erfolgsmeldung angezeigt, wie unten dargestellt:

![Erfolgreicher Test](./media/how-to-connect-fed-azure-adfs/test2.png)

## <a name="template-for-deploying-ad-fs-in-azure"></a>Vorlage zum Bereitstellen von AD FS in Azure
Die Vorlage stellt eine 6-Computer Einrichtung bereit, jeweils 2 für Domänen Controller, AD FS und WAP.

[AD FS in der Azure-Bereitstellungs Vorlage](https://github.com/paulomarquesc/adfs-6vms-regular-template-based)

Beim Bereitstellen dieser Vorlage können Sie ein vorhandenes virtuelles Netzwerk verwenden oder ein neues vnet erstellen. Die verschiedenen Parameter, die für die Anpassung der Bereitstellung verfügbar sind, sind unten aufgeführt, und es wird die Beschreibung der Verwendung des Parameters im Bereitstellungs Prozess aufgeführt. 

| Parameter | Beschreibung |
|:--- |:--- |
| Speicherort |Die Region, in der die Ressourcen bereitgestellt werden sollen, z.b. "USA, Osten". |
| StorageAccountType |Der Typ des erstellten Speicher Kontos. |
| Virtualnetworkusage |Gibt an, ob ein neues virtuelles Netzwerk erstellt oder ein vorhandenes virtuelles Netzwerk verwendet wird. |
| VirtualNetworkName |Der Name des zu erstellenden Virtual Network, erforderlich für die Verwendung vorhandener oder neuer virtueller Netzwerke |
| Virtualnetworkresourcegroupname |Gibt den Namen der Ressourcengruppe an, in der sich das vorhandene virtuelle Netzwerk befindet. Wenn Sie ein vorhandenes virtuelles Netzwerk verwenden, wird dies zu einem obligatorischen Parameter, sodass die Bereitstellung die ID des vorhandenen virtuellen Netzwerks finden kann. |
| Virtualnetworkaddressrange |Der Adressbereich des neuen vnet, erforderlich, wenn ein neues virtuelles Netzwerk erstellt wird. |
| Internalsubnetname |Der Name des internen Subnetzes, erforderlich für die Optionen für die Verwendung virtueller Netzwerke (neu oder vorhanden) |
| Internalsubnetaddressrange |Der Adressbereich des internen Subnetzes, das die Domänen Controller und ADFS-Server enthält. Dies ist obligatorisch, wenn ein neues virtuelles Netzwerk erstellt wird. |
| Dmzsubnetaddressrange |Der Adressbereich des DMZ-Subnetzes, das die Windows-Anwendungs Proxy Server enthält. Dies ist obligatorisch, wenn ein neues virtuelles Netzwerk erstellt wird. |
| Dmzsubnetname |Der Name des internen Subnetzes, erforderlich für die Optionen für die Verwendung virtueller Netzwerke (neu oder vorhanden). |
| ADDC01NICIPAddress |Die interne IP-Adresse des ersten Domänen Controllers. diese IP-Adresse wird dem Domänen Controller statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADDC02NICIPAddress |Die interne IP-Adresse des zweiten Domänen Controllers. diese IP-Adresse wird dem Domänen Controller statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADFS01NICIPAddress |Die interne IP-Adresse des ersten AD FS-Servers. diese IP-Adresse wird dem AD FS-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| ADFS02NICIPAddress |Die interne IP-Adresse des zweiten ADFS-Servers. diese IP-Adresse wird dem AD FS-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| WAP01NICIPAddress |Die interne IP-Adresse des ersten WAP-Servers. diese IP-Adresse wird dem WAP-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des DMZ-Subnetzes sein. |
| WAP02NICIPAddress |Die interne IP-Adresse des zweiten WAP-Servers. diese IP-Adresse wird dem WAP-Server statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des DMZ-Subnetzes sein. |
| Adlesloadbalancerprivateipaddress |Die interne IP-Adresse des AD FS-Lasten Ausgleichs. diese IP-Adresse wird dem Load Balancer statisch zugewiesen und muss eine gültige IP-Adresse innerhalb des internen Subnetzes sein. |
| Addcvmnameprefix |Namens Präfix für virtuelle Computer für Domänen Controller |
| Adbsvmnameprefix |VM-namens Präfix für ADFS-Server |
| Wapvmnameprefix |VM-namens Präfix für WAP-Server |
| Addcvmsize |Die VM-Größe der Domänen Controller |
| Adbsvmsize |Die VM-Größe der AD FS-Server |
| Wapvmsize |Die VM-Größe der WAP-Server |
| AdminUserName |Der Name des lokalen Administrators der virtuellen Computer |
| AdminPassword |Das Kennwort für das lokale Administrator Konto der virtuellen Computer |

## <a name="additional-resources"></a>Zusätzliche Ressourcen
* [Verfügbarkeits Gruppen](https://aka.ms/Azure/Availability) 
* [Azure Load Balancer](https://aka.ms/Azure/ILB)
* [Interner Load Balancer](https://aka.ms/Azure/ILB/Internal)
* [Load Balancer mit Internet Zugriff](https://aka.ms/Azure/ILB/Internet)
* [Speicher Konten](https://aka.ms/Azure/Storage)
* [Virtuelle Azure-Netzwerke](https://aka.ms/Azure/VNet)
* [AD FS und webanwendungsproxy-Links](https://aka.ms/ADFSLinks) 

## <a name="next-steps"></a>Nächste Schritte
* [Integrieren Ihrer lokalen Identitäten in Azure Active Directory](https://docs.microsoft.com/azure/active-directory/hybrid/whatis-hybrid-identity)
* [Konfigurieren und Verwalten Ihrer AD FS mithilfe Azure AD Connect](/azure/active-directory/hybrid/how-to-connect-fed-whatis)
* [Regions übergreifende Hochverfügbarkeit AD FS Bereitstellung in Azure mit Azure Traffic Manager](active-directory-adfs-in-azure-with-azure-traffic-manager.md)
