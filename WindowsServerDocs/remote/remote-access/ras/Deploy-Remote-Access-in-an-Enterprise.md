---
title: Bereitstellen des Remotezugriffs in einem Unternehmen
description: Dieses Thema bietet eine Einführung in das DirectAccess-Szenario in Windows Server 2016 für Unternehmen.
manager: brianlic
ms.topic: article
ms.assetid: 4781df0a-158b-4562-b8f5-32b27615a4f8
ms.author: lizross
author: eross-msft
ms.openlocfilehash: c65653b2014792eb844de7a82526eaacd3331de9
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971667"
---
# <a name="deploy-remote-access-in-an-enterprise"></a>Bereitstellen des Remotezugriffs in einem Unternehmen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält eine Einführung in das DirectAccess-Szenario für das Unternehmen.


> [!IMPORTANT]
> Zum Bereitstellen von DirectAccess mithilfe dieser Anleitung müssen Sie einen DirectAccess-Server verwenden, auf dem Windows Server 2016, Windows Server 2012 R2 oder Windows Server 2012 ausgeführt wird.

## <a name="before-you-begin-deploying-see-the-list-of-unsupported-configurations-known-issues-and-prerequisites"></a>Bevor Sie mit der Bereitstellung beginnen, sollten Sie sich die folgende Liste mit nicht unterstützten Konfigurationen, bekannten Problemen und Voraussetzungen ansehen:

-   [DirectAccess: Nicht unterstützte Konfigurationen](../directaccess/directaccess-unsupported-configurations.md)

-   [DirectAccess: Bekannte Probleme](../directaccess/directaccess-known-issues.md)

-   [Voraussetzungen für die Bereitstellung von DirectAccess](../directaccess/prerequisites-for-deploying-directaccess.md)

## <a name="scenario-description"></a><a name="BKMK_OVER"></a>Beschreibung des Szenarios
Der Remotezugriff bietet eine Reihe von Unternehmensfeatures, u. a. das Bereitstellen mehrerer Remotezugriffsserver in einem Cluster, in dem der Lastausgleich mithilfe des Windows-Netzwerklastenausgleichs oder eines externen Lastenausgleichs vorgenommen wird, das Einrichten einer Bereitstellung für mehrere Standorte mit Remotezugriffsservern, die sich an unterschiedlichen geografischen Standorten befinden, und das Bereitstellen von DirectAccess mit zweistufiger Clientauthentifizierung unter Verwendung eines Einmalkennworts (One-Time Passwort, OTP).

## <a name="in-this-scenario"></a>Inhalt dieses Szenarios
Jedes Unternehmensszenario wird in einem Dokument beschrieben, das Anweisungen zur Planung und zur Bereitstellung einschließt. Weitere Informationen finden Sie unter:

-   [Bereitstellen des Remote Zugriffs in einem Cluster](cluster/Deploy-Remote-Access-In-Cluster.md)

-   [Bereitstellen mehrerer RAS-Server in einer Bereitstellung mit mehreren Standorten](multisite/Deploy-Multiple-Remote-Access-Servers-in-a-Multisite-Deployment.md)

-   [Bereitstellen des Remotezugriffs mit OTP-Authentifizierung](otp/Deploy-RA-OTP.md)

-   [Bereitstellen von Remote Zugriff in einer Umgebung mit mehreren Gesamtstrukturen](multi-forest/Deploy-Remote-Access-in-a-Multi-Forest-Environment.md)

## <a name="practical-applications"></a><a name="BKMK_APP"></a>Praktische Anwendung
Remotezugriffsszenarios in einem Unternehmen bieten Folgendes:

-   **Erhöhung der Verfügbarkeit**. Das Bereitstellen mehrerer Remote Zugriffs Server in einem Cluster bietet Skalierbarkeit und erhöht die Kapazität für Durchsatz und Anzahl der Benutzer. Die Verwendung des Lastenausgleichs im Cluster sorgt für hohe Verfügbarkeit. Wenn ein Server im Cluster ausfällt, können Remotebenutzer weiterhin über einen anderen Server im Cluster auf das interne Unternehmensnetzwerk zugreifen. Das Failover erfolgt unbemerkt, wenn der Client mithilfe einer virtuellen IP-Adresse (VIP) eine Verbindung mit dem Cluster herstellt.

-   **Einfache Verwaltung**. Ein Cluster oder eine Bereitstellung mit mehreren Standorten kann mithilfe der Remote Zugriffs-Verwaltungskonsole, die auf einem der Cluster Server ausgeführt wird, als einzelne Entität konfiguriert und verwaltet werden. Darüber hinaus bietet eine Bereitstellung für mehrere Standorte Administratoren die Möglichkeit, die Remotezugriffsbereitstellung an Active Directory-Standorten auszurichten, wodurch eine einfachere Architektur erzielt wird. Gemeinsam genutzte Einstellungen können problemlos clusterserverübergreifend oder auf allen Einstiegspunktservern der Mehrstandort-Bereitstellung festgelegt werden. Die Remotezugriffseinstellungen können von jedem beliebigen Server im Cluster oder in der Bereitstellung und – mithilfe der Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT) – auch von einem Remotecomputer aus verwaltet werden. Darüber hinaus kann der ganze Cluster bzw. die Bereitstellung für mehrere Standorte über eine einzelne Remotezugriffs-Verwaltungskonsole überwacht werden.

-   **Kosteneffizienz** Mithilfe einer Remote Zugriffs Bereitstellung für mehrere Standorte können Unternehmen Remote Zugriffs Server an mehreren Standorten bereitstellen, die den Client Standorten entsprechen. Hierdurch verfügen Remoteclients unabhängig von ihrem Standort über berechenbare Zugriffsmöglichkeiten, die gleichzeitig zur Senkung von Kosten und Intranetbandbreite beitragen, indem der Clientdatenverkehr über das Internet zu dem nächstgelegenen Remotezugriffsserver weitergeleitet wird.

-   **Sicherheit**. Durch die Bereitstellung einer starken Client Authentifizierung mit einem einmaligen Kennwort anstelle von Standard Active Directory Kennwort erhöht sich die Sicherheit.

## <a name="roles-and-features-included-in-this-scenario"></a><a name="BKMK_NEW"></a>In diesem Szenario enthaltene Rollen und Features
In der folgenden Tabelle sind die für das Unternehmensszenario erforderlichen Rollen und Features aufgeführt:

|Rolle/Feature|Auf welche Weise dieses Szenario unterstützt wird|
|---------|-----------------|
|Remotezugriffs-Serverrolle|Diese Rolle wird mithilfe der Server-Manager-Konsole installiert und deinstalliert. Diese Rolle umfasst DirectAccess (zuvor ein Feature unter Windows Server 2008 R2) sowie die Routing- und RAS-Dienste (zuvor ein Rollendienst unter der Serverrolle für Netzwerkrichtlinien- und Zugriffsdienste). Die Remotezugriffs-Rolle besteht aus zwei Komponenten:<p>1. DirectAccess und RRAS (Routing and Remote Access Services): VPN-DirectAccess und VPN werden in der Remote Zugriffs-Verwaltungskonsole verwaltet.<br />2. RRAS-Routing-RRAS-Routing Features werden in der Legacy-Routing-und Remote Zugriffs Konsole verwaltet.<p>Die Remotezugriffs-Serverrolle ist von den folgenden Serverfeatures abhängig:<p>-Internetinformationsdienste (IIS): dieses Feature ist erforderlich, um den Netzwerkadressen Server und den Standardweb Test zu konfigurieren.<br />-Gruppenrichtlinien-Verwaltungskonsole Feature-Feature ist für DirectAccess erforderlich, um die Gruppenrichtlinie Objekte (GPOs) in Active Directory zu erstellen und zu verwalten, und muss als erforderliches Feature für die Server Rolle installiert werden.|
|Feature %%amp;quot;Tools für die Remotezugriffsverwaltung%%amp;quot;|So installieren Sie dieses Feature:<p>-Sie wird standardmäßig auf einem RAS-Server installiert, wenn die Remote Zugriffs Rolle installiert ist, und unterstützt die Benutzeroberfläche der Remote Verwaltungskonsole.<br />-Es kann optional auf einem Server installiert werden, auf dem die Remote Zugriffs-Server Rolle nicht ausgeführt wird. In diesem Fall wird es für die Remoteverwaltung eines RAS-Computers verwendet, der DirectAccess und VPN ausführt.<p>Das Feature "Tools für die Remotezugriffsverwaltung" besteht aus den folgenden Komponenten:<p>1. Remote Zugriffs-GUI und Befehlszeilen Tools<br />2. Remote Zugriffs Modul für Windows PowerShell<p>Abhängigkeiten umfassen:<p>1. Gruppenrichtlinien-Verwaltungskonsole<br />2. RAS-Verbindungs-Manager-Verwaltungskit (CMAK)<br />3. Windows PowerShell 3,0<br />4. grafische Verwaltungs Tools und Infrastruktur|
|Windows-Netzwerklastenausgleich|Dieses Feature ermöglicht den Lastenausgleich für mehrere Remotezugriffsserver.|



