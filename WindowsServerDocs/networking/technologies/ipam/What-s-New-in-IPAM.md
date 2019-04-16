---
title: Was ist neu in IPAM
description: In diesem Thema werden die IP-Adressverwaltung (IPAM)-Funktionen, die neuen oder geänderten in Windows Server 2016 beschrieben.
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
ms.openlocfilehash: b90cd1ab223e38cbf5933b58a594b32d5e3d4858
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="whats-new-in-ipam"></a>Was ist neu in IPAM

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema werden die IP-Adressverwaltung (IPAM)-Funktionen, die neuen oder geänderten in Windows Server 2016 beschrieben.  
  
IPAM bietet äußerst anpassbare Verwaltungs- und Überwachungsfunktionen für die IP-Adresse und DNS-Infrastruktur in einem Netzwerk Enterprise oder Windows-Verwaltungsinstrumentation (Cloud Service Provider, CSP). Sie können überwachen, überwachen und Verwalten von Servern mit Dynamic Host Configuration-Protokoll (DHCP) und Domain Name System (DNS) mithilfe von IPAM.  
  
## <a name="BKMK_IPAM2012R2"></a>Updates in der IPAM-Server  
Im folgenden werden die neuen und verbesserten Features für IPAM in Windows Server 2016.  
  
|Die Funktionalität|Neue oder verbesserte|Beschreibung|  
|--------------------------|-------------------|---------------|  
|[Erweiterte IP-Adressverwaltung](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|Verbesserte|IPAM-Funktionen werden für Szenarien wie das Behandeln von /32 IPv4 und IPv6-/128 Subnetze und finden kostenlose Subnetze von IP-Adressen und Adressbereiche in einem IP-Adressblock verbessert.|  
|[Verbesserte Verwaltung von DNS-Dienst](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|Neu|IPAM unterstützt die DNS-Ressourceneintrag, Weiterleitung und Verwaltung von DNS-Zone für Domäne Active Directory-integriert und Sicherungsdatei DNS-Server.|  
|[Integrierte DNS, DHCP und IP-Adresse (DDI)-Verwaltung](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|Verbesserte|Mehrere neue Funktionen und integrierte Lifecycle Management Operations aktiviert sind, z. B. alle DNS-Ressourceneinträge, die auf eine IP-Adresse beziehen visualisieren, automatisierten Inventur der IP-Adressen, die auf der Grundlage von DNS-Ressourceneinträgen und IP-Adresse lebenszyklusverwaltung für DNS- und DHCP-Vorgänge.|  
|[Unterstützung für mehrere Active Directory-Gesamtstruktur](#bkmk_ad)|Neu|Sie können IPAM verwenden, verwalten Sie die DNS- und DHCP-Server von mehreren Active Directory-Gesamtstrukturen, wenn eine bidirektionale Vertrauensstellung zwischen der Gesamtstruktur, auf dem IPAM installiert ist, und die einzelnen der Remotegesamtstrukturen ist.|  
|[Endgültiges Löschen von Nutzungsdaten](#bkmk_purge)|Neu|Sie können jetzt die Größe der IPAM-Datenbank reduzieren, durch das Löschen der IP-Adresse mit Daten, die älter als ein Datum, die Sie angeben.|  
|[Windows PowerShell-Unterstützung für Role Based Access Control](#bkmk_ps)|Neu|Sie können Windows PowerShell verwenden, zum Festlegen von zugriffsbereichen für IPAM-Objekte.|  
  
### <a name="EIP"></a>Erweiterte IP-Adressverwaltung  
Die folgenden Features verbessern die Verwaltungsfunktionen von IPAM-Adresse.  
>[!NOTE]
>Die IPAM Windows PowerShell-Befehlsverzeichnis finden Sie unter [IP-Adressverwaltung (IPAM) Server-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj553807.aspx).  
  
#### <a name="support-for-31-32-and-128-subnets"></a>Unterstützung für /31, /32 und /128 Subnetze  
IPAM in Windows Server 2016 nun unterstützt /31, /32 und /128 Subnetzen. Angenommen, ein Subnetz mit zwei Adresse (/ 31 IPv4) für einen PPP-Verbindung zwischen zwei Switches können erforderlich sein. Darüber hinaus einige Switches unter Umständen einzelne Loopbackadressen (/ 32 für IPv4, / 128 für IPv6).  
  
#### **<a name="find-free-subnets-with-find-ipamfreesubnet"></a>Finden Sie kostenlose Subnetze mit suchen IpamFreeSubnet**  
  
Mit diesem Befehl wird die Subnetze, die zur Verfügung standen, erhält eine IP-Block, Präfixlänge und Anzahl der angeforderten Subnetze.   
  
Ist die Anzahl der verfügbaren Subnetze kleiner als die Anzahl der angeforderten Subnetze, werden die verfügbaren Subnetze zurückgegeben, mit der Warnung, dass der Wert kleiner als die Anzahl angefordert wird.  
  
>[!NOTE]
>Diese Funktion nicht tatsächlich reserviert ist die Subnetze, es wird lediglich die Verfügbarkeit. Allerdings kann die Cmdlet-Ausgabe geleitet werden, um die **hinzufügen IpamSubnet** Befehl aus, um das Subnetz zu erstellen.  
  
Weitere Informationen finden Sie unter [suchen IpamFreeSubnet](https://technet.microsoft.com/library/mt712782.aspx).  
  
#### **<a name="find-free-address-ranges-with-find-ipamfreerange"></a>Finden Sie kostenlose Adressbereiche mit suchen IpamFreeRange**  
  
Diese neuen Befehl gibt verfügbaren IP-Adressbereiche erhält eine IP-Subnetz, die Anzahl der Adressen, die im Bereich erforderlich sind und die Anzahl der Bereiche, die angefordert.   
  
Der Befehl sucht nach einer Reihe von verfügbaren IP-Adressen, die die Anzahl der angeforderten Adressen entsprechen. Der Vorgang wird wiederholt, bis die angeforderte Anzahl der Bereiche gefunden wird, oder -verfügbar, bis es nicht mehr verfügbar Adressbereiche sind.  
  
> [!NOTE]
> Diese Funktion nicht tatsächlich die Bereiche reserviert, es wird lediglich die Verfügbarkeit. Allerdings kann die Cmdlet-Ausgabe geleitet werden, um die **Add-IpamRange** Befehl aus, um den Bereich zu erstellen.  
  
Weitere Informationen finden Sie unter [suchen IpamFreeRange](https://technet.microsoft.com/library/mt712772.aspx).  
  
### <a name="EDNS"></a>Verbesserte Verwaltung von DNS-Dienst  
IPAM in Windows Server 2016 unterstützt jetzt die Ermittlung von dateibasierten, Domäne-DNS-Server in einer Active Directory-Gesamtstruktur, die in der IPAM ausgeführt wird.  
  
Darüber hinaus wurden die folgenden DNS-Funktionen hinzugefügt:  
  
-   DNS-Zonen und Ressource zeichnet Sammlung (mit Ausnahme derer, die an DNSSEC) von DNS-Servern unter WindowsServer 2008 oder höher.  
  
-   Konfigurieren (erstellen, ändern und löschen) Eigenschaften und Operationen auf allen Arten von Ressourceneinträgen (mit Ausnahme derer, die an DNSSEC).  
  
-   Konfigurieren (erstellen, ändern oder löschen) Eigenschaften und Operationen auf allen Arten von DNS-Zonen, einschließlich primären sekundäre und Stubzonen).  
  
-   Aufgaben auf sekundären und Stubzonen, unabhängig davon ausgelöst werden soll, wenn sie vorwärts oder reverse-Lookupzonen. Beispielsweise Aufgaben wie z. B. **Übertragung vom Master** oder **neue Kopie der Zone vom Master übertragen**.  
  
-   Rollenbasierte Zugriffssteuerung für die unterstützten DNS-Konfiguration (DNS-Einträge und DNS-Zonen).  
  
-   Bedingte Weiterleitung und Konfigurationsaufgaben (erstellen, löschen, bearbeiten).  
  
### <a name="DDI"></a>Integrierte DNS, DHCP und IP-Adresse (DDI)-Verwaltung  
Wenn Sie eine IP-Adresse in die IP-Adressbestand anzeigen, können Sie in der Detailansicht an alle DNS-Ressourceneinträge IP-Adresse zugeordnet ist.  
  
Als Teil DNS-Datensatz Erfassung sammelt IPAM PTR-Einträge für die DNS-reverse-Lookup-Zonen. Für alle der reverse-Lookupzonen, die alle IP-Adressbereich zugeordnet sind, erstellt IPAM den IP-Adresseinträgen für alle PTR-Einträge, die für diese Zone in den entsprechenden zugeordnete IP-Adressbereich, gehören. Wenn die IP-Adresse bereits vorhanden ist, ist die PTR-Eintrag einfach diese IP-Adresse zugeordnet. Die IP-Adressen werden nicht automatisch erstellt, wenn der reverse-Lookupzone keine IP-Adressbereich zugeordnet ist.  
  
Wenn in einer reverse-Lookupzone durch IPAM ein PTR-Eintrag erstellt wird, wird die IP-adressbestand auf die gleiche Weise aktualisiert, wie oben beschrieben. Bei nachfolgenden Sammlung, da die IP-Adresse bereits im System vorhanden sind werden PTR-Eintrag einfach mit der entsprechenden IP-Adresse zugeordnet.  
  
### <a name="bkmk_ad"></a>Unterstützung für mehrere Active Directory-Gesamtstruktur  
In Windows Server 2012 R2 konnte IPAM ermitteln und Verwalten von DNS- und DHCP-Servern, die zu derselben Active Directory-Gesamtstruktur wie der IPAM-Server gehören. Jetzt können Sie die DNS- und DHCP-Server zu einer anderen Active Directory-Gesamtstruktur gehören, wenn er über eine bidirektionale Vertrauensstellung mit der Gesamtstruktur verfügt, auf der IPAM-Server installiert ist. Wechseln Sie zu der **Serverermittlung konfigurieren** Dialogfeld ein, und fügen Sie aus den anderen vertrauenswürdigen Gesamtstrukturen, die Sie verwalten möchten. Nachdem der Server ermittelt wurden, ist die Verwaltungsfunktionen identisch mit denen für die Server, die zur selben Gesamtstruktur gehören, auf dem IPAM installiert ist.  
  
Weitere Informationen finden Sie unter [Verwalten von Ressourcen in mehreren Active Directory-Gesamtstrukturen](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md)  
  
### <a name="bkmk_purge"></a>Endgültiges Löschen von Nutzungsdaten  
Löschen von Nutzungsdaten können Sie die Größe der IPAM-Datenbank durch Löschen alte IP-Adressdaten Auslastung verringern. Zum Löschen von Daten ausführen, geben Sie ein Datum und IPAM löscht alle Einträge in der Datenbank, die älter als sind oder gleich dem Datum angeben.   
  
Weitere Informationen finden Sie unter [Löschen von Nutzungsdaten](../../technologies/ipam/Purge-Utilization-Data.md).  
  
### <a name="bkmk_ps"></a>Windows PowerShell-Unterstützung für Role Based Access Control  
Windows PowerShell können jetzt rollenbasierte Zugriffssteuerung konfigurieren. Sie können Windows PowerShell-Befehle zum Abrufen von DNS- und DHCP-Objekte in IPAM und ändern ihre zugriffsbereiche verwenden. Aus diesem Grund können Sie Windows PowerShell-Skripts, um die folgenden Objekte zugriffsbereiche zuzuweisen schreiben.  
  
-   IP-Adressraums  
  
-   IP-Adressblock  
  
-   Subnetze von IP-Adressen  
  
-   IP-Adressbereiche  
  
-   DNS-Server  
  
-   DNS-Zonen  
  
-   DNS-Weiterleitungen  
  
-   DNS-Ressourceneinträgen  
  
-   DHCP-Server  
  
-   DHCP-bereichsgruppierungen  
  
-   DHCP-Bereiche  
  
Weitere Informationen finden Sie unter [verwalten Role Based Access Control mit Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) und [IP-Adressverwaltung (IPAM) Server-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/jj553807.aspx).  

