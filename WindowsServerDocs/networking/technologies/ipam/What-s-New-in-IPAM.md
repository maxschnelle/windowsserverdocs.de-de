---
title: Neues in IPAM
description: In diesem Thema werden die IPAM-Funktionen (IP Address Management) beschrieben, die in Windows Server 2016 neu oder geändert wurden.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ipam
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f2f2f1a5-ac2f-41b7-a495-98ad0e2a9b20
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fc19a58482df5dfbfb4ea324f317bbe1b27bf834
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405598"
---
# <a name="whats-new-in-ipam"></a>Neues in IPAM

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden die IPAM-Funktionen (IP Address Management) beschrieben, die in Windows Server 2016 neu oder geändert wurden.  
  
IPAM bietet hochgradig anpassbare Verwaltungs-und Überwachungsfunktionen für die IP-Adresse und die DNS-Infrastruktur in einem Unternehmens-oder clouddienstanbieter-Netzwerk (CSP). Sie können Server, auf denen DHCP (Dynamic Host Configuration Protocol) ausgeführt wird, und Domain Name System (DNS) mithilfe von IPAM überwachen, überwachen und verwalten.  
  
## <a name="BKMK_IPAM2012R2"></a>Updates auf dem IPAM-Server  
Im folgenden finden Sie die neuen und verbesserten Features für IPAM unter Windows Server 2016.  
  
|Feature/Funktionalität|Neu oder verbessert|Beschreibung|  
|--------------------------|-------------------|---------------|  
|[Erweiterte IP-Adressverwaltung](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EIP)|Verbessert|Die IPAM-Funktionen werden für Szenarien verbessert, wie z. b. das Verarbeiten von IPv4/32-und IPv6/128-Subnetzen und das Auffinden von Subnetzen und Bereichen für freie IP-Adressen in einem|  
|[Erweiterte DNS-Dienst Verwaltung](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#EDNS)|Neu|IPAM unterstützt DNS-Ressourcen Einträge, bedingte Weiterleitungen und DNS-Zonenverwaltung sowohl für in die Domäne eingebundenen Active Directory integrierte als auch für Datei gestützte DNS-Server.|  
|[Integrierte DNS-, DHCP-und IP-Adressverwaltung (DDI)](../../technologies/ipam/../../technologies/ipam/../../technologies/ipam/What-s-New-in-IPAM.md#DDI)|Verbessert|Es sind mehrere neue Oberflächen und integrierte Lebenszyklus Verwaltungsvorgänge aktiviert, z. b. das Visualisieren aller DNS-Ressourcen Einträge, die sich auf eine IP-Adresse beziehen, die automatisierte Inventur von IP-Adressen auf der Grundlage von DNS-Ressourcen Einträgen und die Lebenszyklus Verwaltung für DNS-und DHCP-Vorgänge.|  
|[Unterstützung mehrerer Active Directory-Gesamtstrukturen](#bkmk_ad)|Neu|Mit IPAM können Sie die DNS-und DHCP-Server mehrerer Active Directory Gesamtstrukturen verwalten, wenn eine bidirektionale Vertrauensstellung zwischen der Gesamtstruktur vorhanden ist, in der IPAM installiert ist, und den einzelnen Remote Gesamtstrukturen.|  
|[Verwendungs Daten bereinigen](#bkmk_purge)|Neu|Sie können jetzt die IPAM-Datenbankgröße verringern, indem Sie die Nutzungsdaten für die IP-Adresse löschen, die älter als ein von Ihnen angefügungs Datum ist.|  
|[Windows PowerShell-Unterstützung für rollenbasierte Access Control](#bkmk_ps)|Neu|Sie können Windows PowerShell verwenden, um Zugriffs Bereiche für IPAM-Objekte festzulegen.|  
  
### <a name="EIP"></a>Erweiterte IP-Adressverwaltung  
Die folgenden Features verbessern die IPAM-Adress Verwaltungsfunktionen.  
>[!NOTE]
>Die IPAM-Windows PowerShell-Befehlsreferenz finden Sie unter [IP Address Management (IPAM) Server Cmdlets in Windows PowerShell](https://docs.microsoft.com/powershell/module/ipamserver/).  
  
#### <a name="support-for-31-32-and-128-subnets"></a>Unterstützung für Subnetze/31,/32 und/128  
IPAM unter Windows Server 2016 unterstützt nun Subnetze/31,/32 und/128. Beispielsweise kann ein zwei Adresssubnetz (/31 IPv4) für eine Punkt-zu-Punkt-Verknüpfung zwischen Switches erforderlich sein. Außerdem erfordern einige Switches möglicherweise einzelne Loopback Adressen (/32 für IPv4,/128 für IPv6).  
  
#### <a name="find-free-subnets-with-find-ipamfreesubnet"></a>**Suchen von kostenlosen Subnetzen mit "Find-ipamfreesubnet"**  
  
Dieser Befehl gibt Subnetze zurück, die für die Zuordnung verfügbar sind. dabei wird ein IP-Block, eine Präfix Länge und eine Anzahl angeforderter Subnetze angegeben.   
  
Wenn die Anzahl der verfügbaren Subnetze kleiner ist als die Anzahl der angeforderten Subnetze, werden die verfügbaren Subnetze mit einer Warnung zurückgegeben, die darauf hinweist, dass die Anzahl der verfügbaren Subnetze kleiner ist als die angeforderte Anzahl.  
  
>[!NOTE]
>Diese Funktion weist die Subnetze nicht tatsächlich zu, sondern meldet nur ihre Verfügbarkeit. Die Ausgabe des Cmdlets kann jedoch an den Befehl **Add-ipamsubnet** weitergeleitet werden, um das Subnetz zu erstellen.  
  
Weitere Informationen finden Sie unter [Find-ipamfreesubnet](https://docs.microsoft.com/powershell/module/ipamserver/Find-IpamFreeSubnet).  
  
#### <a name="find-free-address-ranges-with-find-ipamfreerange"></a>**Suchen von kostenlosen Adressbereichen mit "Find-ipamfreerange"**  
  
Mit diesem neuen Befehl werden verfügbare IP-Adressbereiche mit einem IP-Subnetz, die Anzahl der benötigten Adressen im Bereich und die Anzahl der angeforderten Bereiche zurückgegeben.   
  
Der Befehl sucht nach einer fortlaufenden Reihe von nicht zugeordneten IP-Adressen, die der Anzahl der angeforderten Adressen entsprechen. Der Prozess wird wiederholt, bis die angeforderte Anzahl von Bereichen gefunden wird oder wenn keine weiteren verfügbaren Adressbereiche verfügbar sind.  
  
> [!NOTE]
> Diese Funktion weist die Bereiche nicht tatsächlich zu, sondern meldet nur ihre Verfügbarkeit. Die Ausgabe des Cmdlets kann jedoch an den Befehl **Add-ipamrange** weitergeleitet werden, um den Bereich zu erstellen.  
  
Weitere Informationen finden Sie unter [Find-ipamfreerange](https://docs.microsoft.com/powershell/module/ipamserver/Find-IpamFreeRange).  
  
### <a name="EDNS"></a>Erweiterte DNS-Dienst Verwaltung  
IPAM in Windows Server 2016 unterstützt jetzt die Ermittlung von dateibasierten, in die Domäne eingebundenen DNS-Servern in einer Active Directory Gesamtstruktur, in der IPAM ausgeführt wird.  
  
Außerdem wurden die folgenden DNS-Funktionen hinzugefügt:  
  
-   DNS-Zonen und Ressourcen Einträge Sammlung (außer denen, die sich auf DNSSEC beziehen) von DNS-Servern unter Windows Server 2008 oder höher.  
  
-   Konfigurieren (erstellen, ändern und löschen) von Eigenschaften und Vorgängen für alle Typen von Ressourcen Datensätzen (außer bei DNSSEC).  
  
-   Konfigurieren (erstellen, ändern, löschen) von Eigenschaften und Vorgängen für alle Arten von DNS-Zonen (z. b. primäre sekundäre und Stubzonen).  
  
-   Ausgelöste Tasks in sekundären und Stubzonen, unabhängig davon, ob es sich um Forward-oder Reverse-Lookupzonen handelt. Beispielsweise Tasks, z. b. die **Übertragung vom Master** oder das **übertragen einer neuen Kopie der Zone vom Master**.  
  
-   Rollenbasierte Zugriffs Steuerung für die unterstützte DNS-Konfiguration (DNS-Einträge und DNS-Zonen).  
  
-   Sammlung und Konfiguration bedingter Weiterleitungen (erstellen, löschen, bearbeiten).  
  
### <a name="DDI"></a>Integrierte DNS-, DHCP-und IP-Adressverwaltung (DDI)  
Wenn Sie eine IP-Adresse im IP-Adress bestand anzeigen, können Sie in der Detailansicht alle DNS-Ressourcen Einträge anzeigen, die der IP-Adresse zugeordnet sind.  
  
Als Teil der DNS-Ressourcen Daten Satz Sammlung sammelt IPAM die PTR-Einträge für die DNS-Reverse-Lookupzonen. Für alle Reverse-Lookupzonen, die einem beliebigen IP-Adressbereich zugeordnet sind, erstellt IPAM die IP-Adresseinträge für alle PTR-Einträge, die zu dieser Zone gehören, im entsprechenden zugeordneten IP-Adressbereich. Wenn die IP-Adresse bereits vorhanden ist, wird der PTR-Datensatz einfach dieser IP-Adresse zugeordnet. Die IP-Adressen werden nicht automatisch erstellt, wenn die Reverse-Lookupzone keinem IP-Adressbereich zugeordnet ist.  
  
Wenn ein PTR-Datensatz in einer Reverse-Lookupzone über IPAM erstellt wird, wird die IP-Adress Inventur auf die gleiche Weise wie oben beschrieben aktualisiert. Da die IP-Adresse im System bereits vorhanden ist, wird der PTR-Datensatz bei der nachfolgenden Sammlung einfach dieser IP-Adresse zugeordnet.  
  
### <a name="bkmk_ad"></a>Unterstützung mehrerer Active Directory-Gesamtstrukturen  
In Windows Server 2012 R2 konnte IPAM DNS-und DHCP-Server ermitteln und verwalten, die zu derselben Active Directory Gesamtstruktur gehören wie der IPAM-Server. Nun können Sie DNS-und DHCP-Server verwalten, die zu einer anderen AD-Gesamtstruktur gehören, wenn eine bidirektionale Vertrauensstellung mit der Gesamtstruktur besteht, in der der IPAM-Server installiert ist. Sie können das Dialogfeld **Server Ermittlung konfigurieren** aufrufen und Domänen aus den anderen vertrauenswürdigen Gesamtstrukturen hinzufügen, die Sie verwalten möchten. Nachdem die Server ermittelt wurden, ist die Verwaltung die gleiche wie für die Server, die zur gleichen Gesamtstruktur gehören, in der IPAM installiert ist.  
  
Weitere Informationen finden Sie unter [Verwalten von Ressourcen in mehreren Active Directory](../../technologies/ipam/Manage-Resources-in-Multiple-Active-Directory-Forests.md) Gesamtstrukturen.  
  
### <a name="bkmk_purge"></a>Verwendungs Daten bereinigen  
Durch das Löschen von Verwendungs Daten können Sie die IPAM-Datenbankgröße verringern, indem Sie alte Daten zur IP-Adress Auslastung löschen. Zum Löschen von Daten geben Sie ein Datum an, und IPAM löscht alle Datenbankeinträge, die älter oder gleich dem Datum sind, das Sie angeben.   
  
Weitere Informationen finden Sie unter Löschen von [Verwendungs Daten](../../technologies/ipam/Purge-Utilization-Data.md).  
  
### <a name="bkmk_ps"></a>Windows PowerShell-Unterstützung für rollenbasierte Access Control  
Sie können jetzt Windows PowerShell verwenden, um rollenbasierte Access Control zu konfigurieren. Sie können Windows PowerShell-Befehle verwenden, um DNS-und DHCP-Objekte in IPAM abzurufen und deren Zugriffs Bereiche zu ändern. Aus diesem Grund können Sie Windows PowerShell-Skripts schreiben, um den folgenden Objekten Zugriffs Bereiche zuzuweisen.  
  
-   IP-Adressraum  
  
-   IP-Adressblock  
  
-   IP-adresssubnetze  
  
-   IP-Adressbereiche  
  
-   DNS-Server  
  
-   DNS-Zonen  
  
-   DNS-Weiterleitungen mit Bedingungen  
  
-   DNS-Ressourcen Einträge  
  
-   DHCP-Server  
  
-   DHCP-Bereichsgruppierungen  
  
-   DHCP-Bereiche  
  
Weitere Informationen finden Sie unter [Verwalten von rollenbasierten Access Control mit Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md) und [Cmdlets für die IP-Adressverwaltung (IPAM) Server in Windows PowerShell](https://docs.microsoft.com/powershell/module/ipamserver/).  

