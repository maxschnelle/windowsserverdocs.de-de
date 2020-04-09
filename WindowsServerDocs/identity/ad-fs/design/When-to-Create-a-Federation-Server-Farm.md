---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: Wann sollte eine Verbundserverfarm erstellt werden?
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 61e5c2c31ef4f6771c379c93e61b78640f4a180a
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80858503"
---
# <a name="when-to-create-a-federation-server-farm"></a>Wann sollte eine Verbundserverfarm erstellt werden?

Ziehen Sie in Erwägung, eine Verbund Serverfarm in Active Directory-Verbunddienste (AD FS) \(AD FS\) zu erstellen, wenn Sie über eine größere AD FS Bereitstellung verfügen und Fehlertoleranz, Lasten\-Ausgleich oder Skalierbarkeit für den Verbunddienst Ihrer Organisation bereitstellen möchten. Das Erstellen von zwei oder mehr Verbund Servern im gleichen Netzwerk, das Konfigurieren der einzelnen Server für die Verwendung desselben Verbunddienst und das Hinzufügen des öffentlichen Schlüssels des Tokens jedes Servers\-Signieren von Zertifikaten zum AD FS-Verwaltungs-Snap\-in erstellt eine Verbund Serverfarm.  
  
Mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server können Sie eine Verbund Serverfarm erstellen oder zusätzliche Verbund Server in einer vorhandenen Farm installieren. Weitere Informationen finden Sie unter [When to Create a Federation Server](When-to-Create-a-Federation-Server.md).  
  
> [!NOTE]  
> Wenn Sie die Option zum Erstellen einer **neuen Verbund Serverfarm** mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server auswählen, versucht der Assistent, ein Container Objekt \(für die Freigabe von Zertifikaten\) in Active Directory zu erstellen. Aus diesem Grund ist es wichtig, dass Sie sich zuerst bei dem Computer anmelden, auf dem Sie die Verbundserverrolle einrichten, und zwar mit einem Konto, das über ausreichende Berechtigungen zum Erstellen dieses Containerobjekts in Active Directory verfügt.  
  
Bevor Verbund Server als Farm gruppiert werden können, müssen Sie zuerst gruppiert werden, damit Anforderungen, die bei einem einzelnen voll qualifizierten Domänen Namen \(FQDN eintreffen\) an die verschiedenen Verbund Server in der Serverfarm weitergeleitet werden. Sie können den Server Cluster erstellen, indem Sie den Netzwerk Lastenausgleich \(NLB-\) innerhalb des Unternehmensnetzwerks bereitstellen. In dieser Anleitung wird davon ausgegangen, dass NLB entsprechend konfiguriert wurde, um jeden der Verbund Server in der Farm zu gruppieren.  
  
Weitere Informationen zum Konfigurieren eines Cluster-FQDN mit Microsoft NLB-Technologie finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?LinkID=74651).  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>Bewährte Methoden zum Bereitstellen einer Verbundserverfarm  
Wir empfehlen die folgenden bewährten Methoden für die Bereitstellung eines Verbund Servers in einer Produktionsumgebung:  
  
-   Wenn Sie mehrere Verbund Server gleichzeitig bereitstellen oder wissen, dass Sie der Farm über einen Zeitraum weitere Server hinzufügen werden, sollten Sie in Erwägung gezogen werden, ein Server Abbild eines vorhandenen Verbund Servers in der Farm zu erstellen und dann von diesem Abbild zu installieren, wenn Sie zusätzliche Verbund Server schnell erstellen müssen.  
  
    > [!NOTE]  
    > Wenn Sie sich dafür entscheiden, die Server Abbild Methode zum Bereitstellen zusätzlicher Verbund Server zu verwenden, müssen Sie die Aufgaben in Prüfliste [: Einrichten eines Verbund Servers](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md) jedes Mal ausführen, wenn Sie der Farm einen neuen Server hinzufügen möchten.  
  
-   Verwenden Sie NLB oder eine andere Form des Clustering, um eine einzelne IP-Adresse für viele Verbund Server Computer zuzuweisen.  
  
-   Reservieren Sie eine statische IP-Adresse für jeden Verbund Server in der Farm, und fügen Sie je nach Domain Name System \(DNS-\) Konfiguration einen Ausschluss für jede IP-Adresse in das Dynamic Host Configuration-Protokoll \(DHCP-\)ein. Microsoft NLB-Technologie erfordert, dass jedem Server, der am NLB-Cluster teilnimmt, eine statische IP-Adresse zugewiesen wird.  
  
-   Wenn die AD FS Konfigurations Datenbank in einer SQL-Datenbank gespeichert wird, sollten Sie die SQL-Datenbank nicht gleichzeitig von mehreren Verbund Servern bearbeiten.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>Konfigurieren von Verbundservern für eine Farm  
In der folgenden Tabelle werden die Aufgaben beschrieben, die durchgeführt werden müssen, damit jeder Verbund Server in eine Umgebung mit einem Server eingebunden werden kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank verwenden|Eine Verbund Serverfarm besteht aus zwei oder mehr Verbund Servern, die dieselben AD FS Konfigurations Datenbank und Token\-Signatur Zertifikaten gemeinsam verwenden. Die Konfigurationsdatenbank kann in jeder internen Windows-Datenbank oder in einer SQL Server-Datenbank gespeichert werden. Wenn Sie beabsichtigen, die Konfigurations Datenbank in einer SQL-Datenbank zu speichern, stellen Sie sicher, dass der Zugriff auf die Konfigurations Datenbank möglich ist, damit von allen neuen Verbund Servern, die an der Farm teilnehmen, auf Sie zugegriffen werden kann. **Hinweis:** Bei Farm Szenarios ist es wichtig, dass sich die Konfigurations Datenbank auf einem Computer befindet, der nicht auch als Verbund Server in der Farm verwendet wird. Microsoft NLB erlaubt den Computern, die an einer Farm teilnehmen, nicht, miteinander zu kommunizieren. **Hinweis:** Stellen Sie sicher, dass die Identität des AD FS AppPool in Internetinformationsdienste \(IIS-\)\)auf jedem Verbund Server, der an der Farm teilnimmt, über Lesezugriff auf die Konfigurations Datenbank verfügt.|  
|Abrufen und Freigeben von Zertifikaten|Sie können ein einzelnes Server Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle \(ca\)abrufen, z. –. VeriSign. Anschließend können Sie das Zertifikat so konfigurieren, dass alle Verbund Server den gleichen privaten Schlüsselteil des Zertifikats gemeinsam verwenden. Weitere Informationen zur gemeinsamen Nutzung des gleichen Zertifikats finden Sie unter [Checklist: Setting Up a Federation Server](../../ad-fs/deployment/Checklist--Setting-Up-a-Federation-Server.md). **Hinweis:** Der AD FS-Verwaltungs-Snap\-in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.<p>Weitere Informationen finden Sie unter [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md).|  
|Zeigen auf die gleiche SQL Server-Instanz|Wenn die AD FS Konfigurations Datenbank in einer SQL-Datenbank gespeichert wird, muss der neue Verbund Server auf dieselbe SQL Server Instanz verweisen, die von anderen Verbund Servern in der Farm verwendet wird, damit der neue Server an der Farm teilnehmen kann.|  
  
## <a name="see-also"></a>Weitere Informationen
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
