---
title: Neues in IPAM
description: In diesem Thema wird beschrieben, die IP-Adressverwaltung (IPAM) Funktionen, die neue oder geänderte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 04838cba63805d20ba31629ed9c8e95290046320
ms.sourcegitcommit: 29ad32b9dea298a7fe81dcc33d2a42d383018e82
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/15/2019
ms.locfileid: "65624686"
---
# <a name="whats-new-in-ipam"></a>Neues in IPAM

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema wird beschrieben, die IP-Adressverwaltung (IPAM) Funktionen, die neue oder geänderte in Windows Server 2016.  
  
IPAM stellt umfassend anpassbare Verwaltungs- und Überwachungsfunktionen Funktionen für die IP-Adresse und DNS-Infrastruktur in einem Unternehmen oder Cloud-Dienstanbieter (CSP)-Netzwerk bereit. Sie können überwachen, überwachen und Verwalten von Servern mit Dynamic Host Configuration-Protokoll (DHCP) und Domain Name System (DNS) mithilfe von IPAM.  
  
## <a name="BKMK_IPAM2012R2"></a>Updates im IPAM-Server  
Im folgenden werden die neuen und verbesserten Features von IPAM unter Windows Server 2016.  
  
|Feature/Funktionalität|Neu oder verbessert|Beschreibung|  
|--------------------------|-------------------|---------------|  
|[Verbesserte Verwaltung von IP-Adresse](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|Verbessert|IPAM-Funktionen werden für Szenarien wie das Behandeln von /32 für IPv4 und IPv6-/128 Subnetze, und Suchen von kostenlose Subnetze von IP-Adressen und Bereiche in eine IP-Adressblock verbessert.|  
|[Verbesserte Verwaltung von DNS-Dienst](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|Neu|IPAM unterstützt die DNS-Ressourceneintrag, bedingte Weiterleitung und Verwaltung der DNS-Zone für Domäne Active Directory-integriert und zugrunde liegender Datei DNS-Server.|  
|[Integrierte DNS, DHCP und IP-Adresse (DDI)-Verwaltung](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|Verbessert|Viele neue Funktionen und integrierte Lifecycle-Verwaltungsvorgänge aktiviert sind, wie z. B. das Visualisieren von Ressourcen für alle DNS-Datensätze, die eine IP-Adresse betreffen, beheben, automatisierte Inventarisierung von IP-Adressen, die basierend auf DNS-Ressourceneinträgen und lebenszyklusverwaltung für IP-Adresse für sowohl DNS- und DHCP-Vorgänge.|  
|[Unterstützung für mehrere Active Directory-Gesamtstruktur](#bkmk_ad)|Neu|Sie können IPAM verwenden, verwalten Sie die DNS- und DHCP-Server, der mehrere Active Directory-Gesamtstrukturen aus, wenn eine bidirektionale Vertrauensstellung zwischen der Gesamtstruktur, auf dem IPAM installiert ist, und jede vorhandene remote vorhanden ist.|  
|[Endgültiges Löschen von Nutzungsdaten](#bkmk_purge)|Neu|Sie können nun die Größe der IPAM-Datenbank reduzieren, durch das Löschen von der IP-Adresse Nutzungsdaten, die älter als ein Datum ist, die Sie angeben.|  
|[Windows PowerShell-Unterstützung für die rollenbasierte Zugriffssteuerung](#bkmk_ps)|Neu|Sie können Windows PowerShell verwenden, zum Festlegen von zugriffsbereichen für IPAM-Objekte.|  
  
### <a name="EIP"></a>Verbesserte Verwaltung von IP-Adresse  
Die folgenden Funktionen verbessern die Verwaltungsfunktionen der IPAM-Adresse.  
>[!NOTE]
>Finden Sie in der IPAM-Windows-PowerShell-Befehlsreferenz [(IP Address Management, IPAM)-Server-Cmdlets in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/module/ipamserver/).  
  
#### <a name="support-for-31-32-and-128-subnets"></a>Unterstützung für /31 /32 und /128 Subnetze  
IPAM in Windows Server 2016 jetzt unterstützen /31, /32 und /128 Subnetzen. Zum Beispiel ein Subnetz mit zwei Adresse (/ 31 IPv4) für eine PPP-Verbindung zwischen zwei Switches können erforderlich sein. Außerdem erfordern einige Switches einzelne Loopback-Adressen (/ 32 für IPv4, / 128 für IPv6).  
  
#### <a name="find-free-subnets-with-find-ipamfreesubnet"></a>**Kostenlose Subnetze mit Find-IpamFreeSubnet suchen**  
  
Dieser Befehl gibt die Subnetze, die für die Zuordnung verfügbar sind zurück erhält eine IP-Block, Präfixlänge und Anzahl der angeforderten Subnetze.   
  
Wenn die Anzahl der verfügbaren Subnetze kleiner als die Anzahl der angeforderten Subnetze ist, werden die verfügbaren Subnetze zurückgegeben, mit einer Warnung gibt an, dass die verfügbare Zahl kleiner als die angeforderte Anzahl ist.  
  
>[!NOTE]
>Diese Funktion ist nicht tatsächlich die Subnetzen zugeordnet, es werden nur die Verfügbarkeit gemeldet. Allerdings für die Cmdlet-Ausgabe weitergeleitet werden kann, um die **hinzufügen-IpamSubnet** Befehl aus, um das Subnetz zu erstellen.  
  
Weitere Informationen finden Sie unter [suchen-IpamFreeSubnet](https://docs.microsoft.com/en-us/powershell/module/ipamserver/Find-IpamFreeSubnet).  
  
#### <a name="find-free-address-ranges-with-find-ipamfreerange"></a>**Kostenlose-Adressbereiche mit Find-IpamFreeRange suchen**  
  
Dieser neue Befehl gibt verfügbaren IP-Adressbereiche angegeben wird, ein IP-Subnetz, die Anzahl der Adressen, die im Bereich erforderlich sind und die Anzahl der angeforderten Bereiche.   
  
Der Befehl sucht nach eine kontinuierliche Reihe von verfügbaren IP-Adressen, die die Anzahl der angeforderten Adressen entsprechen. Der Vorgang wird wiederholt, bis die angeforderte Anzahl der Bereiche gefunden, oder -zur Verfügung, bis nicht mehr verfügbar sind Adressbereiche.  
  
> [!NOTE]
> Diese Funktion nicht tatsächlich die Bereiche reserviert, er meldet nur ihre Verfügbarkeit. Allerdings für die Cmdlet-Ausgabe weitergeleitet werden kann, um die **hinzufügen-IpamRange** Befehl aus, um den Bereich festzulegen.  
  
Weitere Informationen finden Sie unter [suchen-IpamFreeRange](https://docs.microsoft.com/en-us/powershell/module/ipamserver/Find-IpamFreeRange).  
  
### <a name="EDNS"></a>Verbesserte Verwaltung von DNS-Dienst  
IPAM in Windows Server 2016 unterstützt jetzt die Ermittlung von dateibasierten, Domäne-DNS-Server in einer Active Directory-Gesamtstruktur, die in der IPAM ausgeführt wird.  
  
Darüber hinaus wurden die folgenden DNS-Funktionen hinzugefügt:  
  
-   DNS-Zonen und Ressource zeichnet Auflistung (außer diejenigen, die für DNSSEC) von DNS-Servern mit WindowsServer 2008 oder höher auf.  
  
-   Konfigurieren (erstellen, ändern und löschen) Eigenschaften und Operationen auf allen Arten von-Ressourceneinträge (außer diejenigen, die für DNSSEC).  
  
-   Konfigurieren (erstellen, ändern und löschen) Eigenschaften und Operationen für alle Typen von DNS-Zonen, einschließlich der primären sekundäre und Stubzonen).  
  
-   Aufgaben auf sekundären und Stubzonen, unabhängig davon, ob ausgelöst werden soll, wenn sie-Lookupzonen Reverse oder vorwärts werden. Beispiele für Aufgaben wie z. B. **Übertragung vom Master** oder **neue Kopie der Zone vom Master übertragen**.  
  
-   Rollenbasierte Zugriffssteuerung für die unterstützten DNS-Konfiguration (DNS-Einträgen und DNS-Zonen).  
  
-   Weiterleitungen mit Bedingungen und Konfigurationsaufgaben (erstellen, löschen, bearbeiten).  
  
### <a name="DDI"></a>Integrierte DNS, DHCP und IP-Adresse (DDI)-Verwaltung  
Wenn Sie eine IP-Adresse im IP-Adressbestand anzeigen, können Sie in der Detailansicht auf alle DNS-Ressourceneinträge mit der IP-Adresse verknüpft ist, finden Sie unter.  
  
Als Teil des DNS-Datensatz Ressourcensammlung sammelt IPAM die PTR-Einträge für die DNS-Zonen reverse-Lookup. Für alle reverse-Lookupzonen alle IP-Adressbereich zugeordnet sind, erstellt IPAM den IP-Adresseinträge für alle PTR-Einträge, die in den entsprechenden zugeordneten IP-Adressbereich dieser Zone gehören. Wenn die IP-Adresse bereits vorhanden ist, ist die PTR-Eintrag einfach die IP-Adresse zugeordnet. Die IP-Adressen werden nicht automatisch erstellt, wenn die reverse-Lookupzone keine IP-Adressbereich zugeordnet ist.  
  
Wenn in einer reverse-Lookup-Zone über IPAM ein PTR-Eintrag erstellt wird, wird die IP-adressbestand auf die gleiche Weise aktualisiert, wie oben beschrieben. Während der nachfolgenden Sammlung da die IP-Adresse bereits im System vorhanden sind wird der PTR-Eintrag einfach mit dieser IP-Adresse zugeordnet werden.  
  
### <a name="bkmk_ad"></a>Unterstützung für mehrere Active Directory-Gesamtstruktur  
IPAM konnte sich in Windows Server 2012 R2 um zu ermitteln und Verwalten von DNS und DHCP-Servern, die zu derselben Active Directory-Gesamtstruktur wie der IPAM-Server gehören. Jetzt können Sie verwalten, DNS- und DHCP-Server gehört zu einer anderen AD-Gesamtstruktur, wenn sie eine bidirektionale Vertrauensstellung mit der Gesamtstruktur verfügt, auf dem IPAM-Server installiert ist. Wechseln Sie zu der **Serverermittlung konfigurieren** Dialogfeld ein, und fügen Sie die Domänen von einem anderen vertrauenswürdigen Gesamtstrukturen, die Sie verwalten möchten. Nachdem Sie die Server ermittelt wurden, ist die Verwaltungsoberfläche genauso wie bei den Servern, die zur selben Gesamtstruktur gehören, auf dem IPAM installiert ist.  
  
Weitere Informationen finden Sie unter [Verwalten von Ressourcen in mehreren Active Directory-Gesamtstrukturen](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)  
  
### <a name="bkmk_purge"></a>Endgültiges Löschen von Nutzungsdaten  
Löschen von Nutzungsdaten können Sie die Größe der IPAM-Datenbank durch Löschen der alten IP-Adressdaten Auslastung zu verringern. Zum Löschen von Daten ausführen, geben Sie ein Datum und IPAM löscht alle Datenbankeinträge, die älter sind als oder gleich dem Datum angeben.   
  
Weitere Informationen finden Sie unter [Löschen von Nutzungsdaten](../../technologies/ipam/Purge-Utilization-Data.md).  
  
### <a name="bkmk_ps"></a>Windows PowerShell-Unterstützung für die rollenbasierte Zugriffssteuerung  
Sie können jetzt Windows PowerShell verwenden, Role Based Access Control zu konfigurieren. Sie können Windows PowerShell-Befehle zum Abrufen von DNS und DHCP-Objekte in IPAM, und ändern ihre zugriffsbereiche verwenden. Aus diesem Grund können Sie Windows PowerShell-Skripts, um die Zuweisung von zugriffsbereichen für die folgenden Objekte schreiben.  
  
-   IP-Adressbereich  
  
-   IP-Adressblock  
  
-   Subnetze von IP-Adressen  
  
-   IP-Adressbereiche  
  
-   DNS-Server  
  
-   DNS-Zonen  
  
-   DNS-Weiterleitungen mit Bedingungen  
  
-   DNS-Ressourceneinträgen  
  
-   DHCP-Server  
  
-   DHCP-Bereichsgruppierungen  
  
-   DHCP-Bereiche  
  
Weitere Informationen finden Sie unter [verwalten rollenbasierte Zugriffssteuerung mit Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) und [(IP Address Management, IPAM)-Server-Cmdlets in Windows PowerShell](https://docs.microsoft.com/en-us/powershell/module/ipamserver/).  

