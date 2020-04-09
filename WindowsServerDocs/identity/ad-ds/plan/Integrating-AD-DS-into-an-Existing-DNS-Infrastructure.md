---
ms.assetid: 4981b32f-741e-4afc-8734-26a8533ac530
title: Integrieren von AD DS in eine vorhandene DNS-Infrastruktur
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: cf069102f409247832204546f3e1c15de7238bd3
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80822273"
---
# <a name="integrating-ad-ds-into-an-existing-dns-infrastructure"></a>Integrieren von AD DS in eine vorhandene DNS-Infrastruktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Wenn Ihre Organisation bereits über einen vorhandenen Domain Name System (DNS)-Server Dienst verfügt, muss der DNS für Active Directory Domain Services Besitzer (AD DS) mit dem DNS-Besitzer für Ihre Organisation zusammenarbeiten, um AD DS in die vorhandene Infrastruktur zu integrieren. Dies umfasst das Erstellen eines DNS-Servers und einer DNS-Client Konfiguration.  
  
## <a name="creating-a-dns-server-configuration"></a>Erstellen einer DNS-Serverkonfiguration  
Wenn Sie AD DS in einen vorhandenen DNS-Namespace integrieren, empfiehlt es sich, folgende Schritte durchzuführen:  
  
-   Installieren Sie den DNS-Server Dienst auf allen Domänen Controllern in der Gesamtstruktur. Dies bietet Fehlertoleranz, wenn einer der DNS-Server nicht verfügbar ist. Auf diese Weise müssen sich Domänen Controller nicht auf andere DNS-Server für die Namensauflösung verlassen. Dadurch wird auch die Verwaltungs Umgebung vereinfacht, da alle Domänen Controller über eine einheitliche Konfiguration verfügen.  
  
-   Konfigurieren Sie den Active Directory-Gesamtstruktur-Stamm Domänen Controller zum Hosten der DNS-Zone für die Active Directory Gesamtstruktur  
  
-   Konfigurieren Sie die Domänen Controller für jede regionale Domäne, um die DNS-Zonen zu hosten, die Ihren Active Directory Domänen entsprechen.  
  
-   Konfigurieren Sie die Zone mit den Active Directory Gesamtstruktur weiten Serverlocatorpunkt-Datensätzen (d. h. dem _msdcs. *Name* Zone) für die Replikation auf jeden DNS-Server in der Gesamtstruktur mithilfe der Gesamtstruktur weiten DNS-Anwendungsverzeichnis Partition.  
  
    > [!NOTE]  
    > Wenn der DNS-Server Dienst mit dem Assistent zum Installieren von Active Directory Domain Services installiert wird (Wir empfehlen diese Option), werden alle vorherigen Tasks automatisch ausgeführt. Weitere Informationen finden Sie unter Bereitstellen [einer Windows Server 2008](https://technet.microsoft.com/library/cc731174.aspx)-Gesamtstruktur-Stamm Domäne.  
  
    > [!NOTE]  
    > AD DS verwendet Gesamtstruktur übergreifende Serverlocatorpunkt-Einträge, um Replikations Partnern das Auffinden der anderen und das Auffinden von globalen Katalog Servern zu ermöglichen. In AD DS werden die Gesamtstruktur weiten Serverlocatorpunkt-Einträge in der _msdcs gespeichert. *Name* -Zone. Da die Informationen in der Zone allgemein verfügbar sein müssen, wird diese Zone über die Gesamtstruktur übergreifende DNS-Anwendungsverzeichnis Partition auf allen DNS-Servern in der Gesamtstruktur repliziert.  
  
Die vorhandene DNS-Struktur bleibt intakt. Sie müssen keine Server oder Zonen verschieben. Sie müssen lediglich eine Delegierung für Ihre Active Directory integrierten DNS-Zonen aus Ihrer vorhandenen DNS-Hierarchie erstellen.  
  
## <a name="creating-the-dns-client-configuration"></a>Erstellen der DNS-Client Konfiguration  
Zum Konfigurieren von DNS auf Client Computern muss das DNS für AD DS Besitzer das Benennungs Schema des Computers angeben und angeben, wie die Clients DNS-Server finden. In der folgenden Tabelle werden die empfohlenen Konfigurationen für diese Entwurfs Elemente aufgelistet.  
  
|Entwurfselement|Konfiguration|  
|------------------|-----------------|  
|Computer Benennung|Standard Benennung verwenden. Wenn ein Computer mit Windows 2000, Windows XP, Windows Server 2003, Windows Server 2008 oder Windows Vista einer Domäne Beitritt, weist er sich selbst einen vollständig qualifizierten Domänen Namen (Fully Qualified Domain Name, FQDN) zu, der den Hostnamen des Computers und den Namen der Active Directory Domäne enthält.|  
|Konfiguration des Client Resolvers|Konfigurieren Sie Client Computer so, dass Sie auf einen beliebigen DNS-Server im Netzwerk verweisen.|  
  
> [!NOTE]  
> Active Directory Clients und Domänen Controllern können Ihre DNS-Namen auch dann dynamisch registrieren, wenn Sie nicht auf den DNS-Server verweisen, der für ihre Namen autorisierend ist.  
  
Ein Computer verfügt möglicherweise über einen anderen DNS-Namen, wenn die Organisation zuvor den Computer statisch in DNS registriert hat oder wenn die Organisation zuvor eine integrierte DHCP-Lösung (Dynamic Host Configuration Protocol) bereitgestellt hat. Wenn Ihre Client Computer bereits über einen registrierten DNS-Namen verfügen und die Domäne, der Sie beitreten, auf Windows Server 2008 AD DS aktualisiert wird, haben Sie zwei verschiedene Namen:  
  
-   Der vorhandene DNS-Name  
  
-   Der neue vollständig qualifizierte Domänen Name (FQDN)  
  
Clients können weiterhin über einen der Namen gefunden werden. Alle vorhandenen DNS-, DHCP-oder integrierten DNS/DHCP-Lösungen bleiben intakt. Die neuen Primärnamen werden automatisch erstellt und mithilfe von dynamischem Update aktualisiert. Sie werden automatisch mithilfe der Bereinigung bereinigt.  
  
Wenn Sie die Kerberos-Authentifizierung beim Herstellen einer Verbindung mit einem Server unter Windows 2000, Windows Server 2003 oder Windows Server 2008 nutzen möchten, müssen Sie sicherstellen, dass der Client eine Verbindung mit dem Server unter Verwendung des primär namens herstellt.  
  


