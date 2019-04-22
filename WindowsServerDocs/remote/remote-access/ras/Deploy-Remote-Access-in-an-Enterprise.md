---
title: Bereitstellen des Remotezugriffs in einem Unternehmen
description: Dieses Thema enthält eine Einführung in das DirectAccess-Szenario, in Windows Server 2016 für das Unternehmen.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4781df0a-158b-4562-b8f5-32b27615a4f8
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f110ad945139da3b07b33bbb0adb3e8084743fdb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812241"
---
# <a name="deploy-remote-access-in-an-enterprise"></a>Bereitstellen des Remotezugriffs in einem Unternehmen

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält eine Einführung in das DirectAccess-Szenario für das Unternehmen.  
  
  
> [!IMPORTANT]  
> Zum Bereitstellen von DirectAccess mithilfe dieser Anleitung müssen Sie einen DirectAccess-Server verwenden, auf der Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.  
  
## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>Bevor Sie mit der Bereitstellung beginnen, sollten Sie sich die folgende Liste mit nicht unterstützten Konfigurationen, bekannten Problemen und Voraussetzungen ansehen:  
  
-   [DirectAccess nicht unterstützte Konfigurationen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/directaccess-unsupported-configurations)  
  
-   [DirectAccess – bekannte Probleme](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/directaccess-known-issues)  
  
-   [Voraussetzungen für die Bereitstellung von DirectAccess) Voraussetzungen](https://technet.microsoft.com/windows-server-docs/networking/remote-access/directaccess/prerequisites-for-deploying-directaccess)  
  
## <a name="BKMK_OVER"></a>Beschreibung des Szenarios  
Der Remotezugriff bietet eine Reihe von Unternehmensfeatures, u. a. das Bereitstellen mehrerer Remotezugriffsserver in einem Cluster, in dem der Lastausgleich mithilfe des Windows-Netzwerklastenausgleichs oder eines externen Lastenausgleichs vorgenommen wird, das Einrichten einer Bereitstellung für mehrere Standorte mit Remotezugriffsservern, die sich an unterschiedlichen geografischen Standorten befinden, und das Bereitstellen von DirectAccess mit zweistufiger Clientauthentifizierung unter Verwendung eines Einmalkennworts (One-Time Passwort, OTP).  
  
## <a name="in-this-scenario"></a>Inhalt dieses Szenarios  
Jedes Unternehmensszenario wird in einem Dokument beschrieben, das Anweisungen zur Planung und zur Bereitstellung einschließt. Weitere Informationen finden Sie in den folgenden Themen:  
  
-   [Bereitstellen des Remotezugriffs in einem cluster](cluster/Deploy-Remote-Access-In-Cluster.md)  
  
-   [Bereitstellen Sie mehrerer Remotezugriffsserver in einer Bereitstellung für mehrere Standorte](multisite/Deploy-Multiple-Remote-Access-Servers-in-a-Multisite-Deployment.md)  
  
-   [Bereitstellen des Remotezugriffs mit OTP-Authentifizierung](otp/Deploy-RA-OTP.md)  
  
-   [Bereitstellen des Remotezugriffs in einer Umgebung mit mehreren Gesamtstrukturen](multi-forest/Deploy-Remote-Access-in-a-Multi-Forest-Environment.md)  
  
## <a name="BKMK_APP"></a>Praktische Anwendungen  
Remotezugriffsszenarios in einem Unternehmen bieten Folgendes:  
  
-   **Erhöhte Verfügbarkeit**. Bereitstellen mehrerer Remotezugriffsserver in einem Cluster bietet Skalierbarkeit und erhöht die Kapazität für den Durchsatz und Anzahl von Benutzern. Die Verwendung des Lastenausgleichs im Cluster sorgt für hohe Verfügbarkeit. Wenn ein Server im Cluster ausfällt, können Remotebenutzer weiterhin über einen anderen Server im Cluster auf das interne Unternehmensnetzwerk zugreifen. Das Failover erfolgt unbemerkt, wenn der Client mithilfe einer virtuellen IP-Adresse (VIP) eine Verbindung mit dem Cluster herstellt.  
  
-   **Erleichterte Verwaltung**. Ein Cluster oder die Bereitstellung für mehrere Standorte kann als eine einzelne Entität mithilfe der Remotezugriffs-Verwaltungskonsole auf einem der Clusterserver ausgeführt wird konfiguriert und verwaltet werden. Darüber hinaus bietet eine Bereitstellung für mehrere Standorte Administratoren die Möglichkeit, die Remotezugriffsbereitstellung an Active Directory-Standorten auszurichten, wodurch eine einfachere Architektur erzielt wird. Gemeinsam genutzte Einstellungen können problemlos clusterserverübergreifend oder auf allen Einstiegspunktservern der Mehrstandort-Bereitstellung festgelegt werden. Die Remotezugriffseinstellungen können von jedem beliebigen Server im Cluster oder in der Bereitstellung und – mithilfe der Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT) – auch von einem Remotecomputer aus verwaltet werden. Darüber hinaus kann der ganze Cluster bzw. die Bereitstellung für mehrere Standorte über eine einzelne Remotezugriffs-Verwaltungskonsole überwacht werden.  
  
-   **Kosteneffizienz**. Eine remotezugriffsbereitstellung für mehrere Standorte kann Unternehmen möglich, Remotezugriffsserver an mehreren Standorten, die clientstandorten entsprechen bereitzustellen. Hierdurch verfügen Remoteclients unabhängig von ihrem Standort über berechenbare Zugriffsmöglichkeiten, die gleichzeitig zur Senkung von Kosten und Intranetbandbreite beitragen, indem der Clientdatenverkehr über das Internet zu dem nächstgelegenen Remotezugriffsserver weitergeleitet wird.  
  
-   **Sicherheit**. Bereitstellung der strengen Clientauthentifizierung mit einem Einmalkennwort (OTP) anstelle eines standardmäßigen Active Directory-Kennworts erhöht die Sicherheit.  
  
## <a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und features  
In der folgenden Tabelle sind die für das Unternehmensszenario erforderlichen Rollen und Features aufgeführt:  
  
|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|  
|---------|-----------------|  
|Remotezugriffs-Serverrolle|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<br /><br />1.  DirectAccess und Routing- und RAS-Dienste (RRAS) VPN – DirectAccess und VPN werden gemeinsam in der Remotezugriffs-Verwaltungskonsole verwaltet.<br />2.  RRAS-Routing – RRAS-Routingfeatures werden in der älteren Routing- und RAS-Konsole verwaltet.<br /><br />Die Remotezugriffs-Serverrolle ist von den folgenden Serverfeatures abhängig:<br /><br />-Internetinformationsdienste (IIS) – dieses Feature ist erforderlich, um die Netzwerk-Speicherort Server und den standardwebtest zu konfigurieren.<br />-Gruppe Gruppenrichtlinien-Verwaltungskonsole-Feature - Feature von DirectAccess zu erstellen und verwalten die Gruppenrichtlinienobjekte (GPOs) in Active Directory erforderlich ist, und es muss als erforderliches Feature für die Serverrolle installiert sein.|  
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<br /><br />– Es wird standardmäßig auf einem RAS-Server installiert, wenn die Rolle "Remotezugriff" installiert ist, und unterstützt die Benutzeroberfläche der RAS-Konsole.<br />– sie können optional auf einem Server nicht mit der RAS-Serverrolle installiert werden. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<br /><br />Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<br /><br />1.  Benutzeroberfläche für RAS und Befehlszeilentools<br />2.  RAS-Modul für Windows PowerShell<br /><br />Abhängigkeiten umfassen:<br /><br />1.  Gruppenrichtlinien-Verwaltungskonsole<br />2.  RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />3.  Windows PowerShell 3.0<br />4.  Grafische Verwaltungstools und Infrastruktur|  
|Windows-Netzwerklastenausgleich|Dieses Feature ermöglicht den Lastenausgleich für mehrere Remotezugriffsserver.|  
  

  


