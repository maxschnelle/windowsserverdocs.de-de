---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: Wann sollte eine Verbundserverfarm erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 2e7c991cf87bc0e6914e158f0878bcadbede3c22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816231"
---
# <a name="when-to-create-a-federation-server-farm"></a>Wann sollte eine Verbundserverfarm erstellt werden?

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sollten Sie eine Verbundserverfarm erstellen, in Active Directory-Verbunddienste \(AD FS\) bei eine größere AD FS-Bereitstellung haben und Sie möchten Fehlertoleranz bereitzustellen, laden\-Lastenausgleich oder Skalierbarkeit für Ihre Verbunddienst der Organisation. Der Vorgang, erstellen zwei oder mehr Verbundserver in demselben Netzwerk, konfigurieren jeweils den gleichen Verbunddienst verwendet und Hinzufügen von der öffentliche Schlüssel der einzelnen Server ist token\-Signieren von Zertifikaten, die AD FS-Verwaltungs-Snap\-in erstellt eine Verbundserverfarm.  
  
Sie können entweder eine Verbundserverfarm erstellen oder zusätzliche Verbundserver zu einer vorhandenen Farm installieren, mit der AD FS Konfigurations-Assistenten. Weitere Informationen finden Sie unter [When to Create a Federation Server](When-to-Create-a-Federation-Server.md).  
  
> [!NOTE]  
> Bei der Auswahl der Option zum Erstellen einer **neuen Verbundserverfarm** verwenden die AD FS Konfigurations-Assistenten, versucht der Assistent zum Erstellen eines Containerobjekts \(für gemeinsame Nutzung von Zertifikaten\) in Active Directory. Aus diesem Grund ist es wichtig, dass Sie sich zuerst bei dem Computer anmelden, auf dem Sie die Verbundserverrolle einrichten, und zwar mit einem Konto, das über ausreichende Berechtigungen zum Erstellen dieses Containerobjekts in Active Directory verfügt.  
  
Vor dem Verbundserver als Farm gruppiert werden können, sie müssen zuerst gruppiert werden, damit Anforderungen unter einem einzelnen vollständig Domänennamen qualifiziert \(FQDN\) an verschiedenen Verbundserver in der Serverfarm weitergeleitet werden. Sie können den Server-Cluster erstellen, durch die Bereitstellung des Netzwerklastenausgleichs \(NLB\) innerhalb des Unternehmensnetzwerks. Dieses Handbuch wird davon ausgegangen, dass NLB entsprechend konfiguriert wurde, um jeder Verbundserver in der Farm zu Clustern.  
  
Weitere Informationen zum Konfigurieren eines Clusters-FQDN mit Microsoft NLB-Technologie finden Sie unter [angeben der Clusterparameter](https://go.microsoft.com/fwlink/?LinkID=74651).  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>Bewährte Methoden zum Bereitstellen einer Verbundserverfarm  
Die folgenden bewährten Methoden für die Bereitstellung eines Verbundservers in einer produktionsumgebung empfohlen:  
  
-   Wenn Sie mehrere Verbundserver zur gleichen Zeit einsetzen werden, oder Sie wissen, dass Sie weitere Server zur Farm im Laufe der Zeit hinzufügen möchten, sollten Sie Sie erstellen ein Serverabbild von einem vorhandenen Verbundserver in der Farm aus, und klicken Sie dann aus diesem Image installieren, bei Bedarf cr Erstellen zusätzlicher Verbundserver schnell.  
  
    > [!NOTE]  
    > Wenn Sie sich die Server-Image-Methode verwendet wird, für die Bereitstellung zusätzlicher Verbundserver entscheiden, müssen Sie nicht die Aufgaben in [Prüfliste: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md) jedes Mal, die Sie der Farm einen neuen Server hinzufügen möchten.  
  
-   Verwenden Sie NLB oder eine andere Art von clustering, um eine einzelne IP-Adresse für viele verbundservercomputer zugeordnet.  
  
-   Reservieren Sie eine statische IP-Adresse für jeden Verbundserver in der Farm und, abhängig von Ihrem Domain Name System \(DNS\) Konfiguration, einfügen, die ein Ausschluss für jede IP-Adresse Dynamic Host Configuration Protocol \(DHCP\). Microsoft NLB-Technologie erfordert, dass jedem Server, der am NLB-Cluster teilnimmt, eine statische IP-Adresse zugewiesen wird.  
  
-   Wenn die AD FS-Konfigurationsdatenbank in einer SQL­Datenbank gespeichert werden, vermeiden Sie die SQL-Datenbank aus mehreren Verbundservern zur gleichen Zeit bearbeiten.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>Konfigurieren von Verbundservern für eine Farm  
Die folgende Tabelle beschreibt die Aufgaben, die ausgeführt werden müssen, damit jedes Verbundservers in einer farmumgebung teilnehmen kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank verwenden|Eine Verbundserverfarm besteht aus zwei oder mehr Verbundserver, die gemeinsam die gleichen AD FS-Konfigurationsdatenbank und das Token\-Signieren von Zertifikaten. Die Konfigurationsdatenbank kann in jeder internen Windows-Datenbank oder in einer SQL Server-Datenbank gespeichert werden. Wenn Sie die Konfigurationsdatenbank in einer SQL-Datenbank speichern möchten, stellen Sie sicher, dass die Konfigurationsdatenbank möglich ist, sodass alle neuen Verbundserver darauf zugreifen können, die in der Farm beteiligt sind. **Hinweis**: Für farmszenarien ist es wichtig, dass die Konfigurationsdatenbank auf einem Computer befinden, die als Verbundserver in dieser Farm nicht auch beteiligt ist. Microsoft NLB erlaubt den Computern, die an einer Farm teilnehmen, nicht, miteinander zu kommunizieren. **Hinweis**: Stellen Sie sicher, dass die Identität der AD FS-AppPool in Internet Information Services \(IIS\) \) für jede Verbund-Server, der in der Farm beteiligt ist Lesezugriff auf die Konfigurationsdatenbank verfügt.|  
|Abrufen und Freigeben von Zertifikaten|Sie erhalten einen Einzelserver-Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle \(Zertifizierungsstelle\)– z. B. VeriSign. Sie können das Zertifikat klicken Sie dann konfigurieren, damit allen Verbundservern, die denselben privaten Schlüsselteil des Zertifikats freigeben. Weitere Informationen zur gemeinsamen Nutzung der gleichen Zertifikats finden Sie unter [Prüfliste: Das Einrichten eines Verbundservers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md). **Hinweis**: Die AD FS-Verwaltungs-Snap\-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.<br /><br />Weitere Informationen finden Sie unter [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md).|  
|Zeigen auf die gleiche SQL Server-Instanz|Wenn die AD FS-Konfigurationsdatenbank in einer SQL­Datenbank gespeichert werden, muss der neue Verbundserver auf derselben SQL Server-Instanz verweisen, die von anderen Verbundserver in der Farm verwendet wird, sodass der neue Server in der Farm teilnehmen kann.|  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in WindowsServer 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
