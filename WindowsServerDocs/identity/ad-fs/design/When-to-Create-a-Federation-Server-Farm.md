---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: Wann sollte eine Verbundserverfarm erstellt
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e7c991cf87bc0e6914e158f0878bcadbede3c22
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-create-a-federation-server-farm"></a>Wann sollte eine Verbundserverfarm erstellt

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sollten Sie eine Verbundserverfarm in Active Directory Federation Services \(AD FS\) erstellen, wenn Sie eine größere AD FS-Bereitstellung und Fehlertoleranz, Load\ Lastenausgleich oder Skalierbarkeit Verbunddienst Ihrer Organisation bereitstellen möchten. Erstellen Sie zwei oder mehr Verbundserver in einem Netzwerk, wird erstellt Konfiguration mithilfe des gleichen Verbunddiensts und den öffentlichen Schlüssel des Signaturzertifikaten für jeden Server Token\ AD FS-Verwaltungs-Snap-In hinzufügen eine Verbundserverfarm.  
  
Sie können eine Verbundserverfarm erstellen oder zusätzliche Verbundserver in einer vorhandenen Farm mit AD FS Federation Server-Konfigurations-Assistenten installieren. Weitere Informationen finden Sie unter [When to Create a Federation Server](When-to-Create-a-Federation-Server.md).  
  
> [!NOTE]  
> Wenn Sie die Option zum Erstellen einer **neue Verbundserverfarm** mit AD FS Federation Server-Konfigurations-Assistenten, der Assistent wird versucht, ein Containerobjekt erstellen \(for Sharing certificates\) in Active Directory. Daher ist es wichtig, dass Sie zuerst auf dem Computer anmelden, in dem Sie die Verbundserver-Rolle, über ein Konto einrichten, die in Active Directory zum Erstellen dieses Containerobjekts über ausreichende Berechtigungen verfügt.  
  
Vor dem Verbundserver als Farm gruppiert werden können, müssen sie zunächst zusammengefasst werden, damit Anforderungen, die auf einem einzelnen vollständig ankommen Domänennamen \(FQDN\) an die verschiedenen Federation Server in der Serverfarm weitergeleitet werden. Sie können den Server-Cluster erstellen, durch die Bereitstellung von Netzwerklastenausgleich \(NLB\) innerhalb des Unternehmensnetzwerks. Dieses Handbuch wird davon ausgegangen, dass NLB entsprechend konfiguriert wurde, dass jeder Verbundserver in der Farm Cluster.  
  
Weitere Informationen zum Konfigurieren eines Clusters-FQDN mit Microsoft NLB-Technologie finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?LinkID=74651).  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>Bewährte Methoden zum Bereitstellen einer Verbundserverfarm  
Die folgenden bewährten Methoden für die Bereitstellung von einem Verbundserver in einer Produktionsumgebung empfohlen:  
  
-   Wenn Sie mehrere Verbundserver zur gleichen Zeit einsetzen werden, oder Sie wissen, dass Sie weitere Server der Farm mit der Zeit hinzufügen möchten, sollten Sie ein Serverabbild von einem vorhandenen Federation Server in der Farm erstellen und das anschließende Installieren von dem Abbild aus, wenn Sie zusätzliche Verbundserver schnell erstellen müssen.  
  
    > [!NOTE]  
    > Wenn Sie die serverabbildmethode zur Bereitstellung zusätzlicher Verbundserver verwenden möchten, müssen Sie nicht die Aufgaben in [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md) jedes Mal, die Sie der Farm einen neuen Server hinzufügen möchten.  
  
-   Verwenden Sie NLB oder eine andere Art von Clustering, um eine einzelne IP-Adresse für viele Verbundservercomputer zugeordnet werden.  
  
-   Reservieren Sie eine statische IP-Adresse für jeden Verbundserver in der Farm und, abhängig von Ihrer Konfiguration Domain Name System \(DNS\) einen Ausschluss für jede IP-Adresse in das Dynamic Host Configuration-Protokoll \(DHCP\). Microsoft NLB-Technologie erfordert, dass jedem Server, die Teil des NLB-Clusters ist eine statische IP-Adresse zugewiesen werden.  
  
-   Wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbank gespeichert wird, zu vermeiden, die SQL-Datenbank aus mehreren Verbundservern gleichzeitig bearbeiten.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>Konfigurieren von Verbundservern für eine farm  
Die folgende Tabelle beschreibt die Aufgaben, die ausgeführt werden müssen, damit jeder Verbundserver in einer farmumgebung teilnehmen kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank verwenden|Eine Verbundserverfarm besteht aus zwei oder mehr Verbundserver, die die gleiche AD FS-Konfiguration freigeben Datenbank und Token\-Signaturzertifikaten. Die Konfigurationsdatenbank kann in einer internen Windows-Datenbank oder in einer SQL Server-Datenbank gespeichert werden. Wenn Sie die Konfigurationsdatenbank in einer SQLDatenbank speichern möchten, stellen Sie sicher, dass die Konfigurationsdatenbank möglich ist, damit alle neuen Verbundserver darauf zugreifen können, die in der Farm beteiligt sind. **Hinweis:** für farmszenarien ist wichtig, dass die Datenbank auf einem Computer befinden, der als Verbundserver in dieser Farm nicht auch teilnimmt. Microsoft NLB lässt kein Computern zu, die Teil einer Farm miteinander kommunizieren. **Hinweis:** stellen Sie sicher, dass die Identität der AD FS-AppPool in Internet Information Services \(IIS\)\) auf jedem Verbundserver, der in der Farm beteiligt ist Lesezugriff auf die Konfigurationsdatenbank verfügt.|  
|Abrufen und Freigeben von Zertifikaten|Sie erhalten einen Einzelserver-Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle \ (CA\) – z.B. VeriSign. Sie können das Zertifikat dann konfigurieren, sodass allen Verbundservern der gleichen privaten Teil des Zertifikats teilen. Weitere Informationen zur gemeinsamen Nutzung der gleichen Zertifikats finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md). **Hinweis:** AD FS-Verwaltungs-Snap-In bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.<br /><br />Weitere Informationen finden Sie unter [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md).|  
|Zeigen Sie auf die gleiche SQL Server-Instanz|Wenn die AD FS-Konfigurationsdatenbank in einer SQL-Datenbank gespeichert wird, muss der neue Verbundserver auf die gleiche SQL Server-Instanz verweisen, die von anderen Verbundservern in der Farm verwendet wird, sodass der neue Server in der Farm teilnehmen kann.|  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
