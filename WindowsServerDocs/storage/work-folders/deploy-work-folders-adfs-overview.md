---
title: Bereitstellen von Arbeitsordnern mit AD FS und Webanwendungsproxy
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
ms.assetid: ea19f0f0-6cc0-4322-b387-c0873f7795ad
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.openlocfilehash: 40cc953ce7393781497d957fc8e6690c5c9abc0b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365925"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-overview"></a>Arbeitsordner mit AD FS und webanwendungsproxy bereitstellen: Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die Themen in diesem Abschnitt enthalten Anweisungen für die Bereitstellung von Arbeitsordnern mit Active Directory-Verbunddiensten (AD FS) und Webanwendungsproxy. Die Anweisungen behandeln die Einrichtung von Arbeitsordnern mit Clientcomputern für die sofortige Verwendung von Arbeitsordnern entweder lokal oder über das Internet.  
  
Arbeitsordner ist eine in in Windows Server 2012 R2 eingeführte Komponente, die Mitarbeitern das Synchronisieren von Dateien zwischen Geräten ermöglicht. Weitere Informationen zu Arbeitsordnern finden Sie unter [Übersicht: Arbeitsordner](Work-Folders-Overview.md).  
  
Um Benutzern die Synchronisierung der Arbeitsordner über das Internet zu ermöglichen, müssen Sie Arbeitsordner über einen Reverseproxy veröffentlichen, sodass Arbeitsordner extern im Internet verfügbar sind. Die in Active Directory-Verbunddiensten (AD FS) enthaltene Webanwendungsproxy ist eine Option zur Bereitstellung von Reverseproxyfunktionen. Die Reverseproxyimplementierung führt eine Präauthentifizierung des Zugriffs auf Webanwendungsproxy mit AD FS durch, damit die Benutzer auf Arbeitsordner von außerhalb des Unternehmensnetzwerks zugreifen können. 

> [!NOTE]
>   Die in diesem Abschnitt enthaltenen Anweisungen gelten für eine Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, folgen Sie den [Anweisungen für Windows Server 2012 R2](https://technet.microsoft.com/library/dn747208(v=ws.11).aspx).
  
Diese Themen enthalten folgende Informationen:  
  
-   Step-by-step Anweisungen zur Einrichtung und Bereitstellung von Arbeitsordnern mit AD FS und Webanwendungsproxy über die Benutzeroberfläche von Windows Server. Die Anweisungen beschreiben das Einrichten einer Testumgebungen mit selbstsignierten Zertifikaten. Orientieren Sie sich an dem Beispiel, um eine Produktionsumgebung zu erstellen, die öffentlich vertrauenswürdige Zertifikate verwendet.  
  
## <a name="prerequisites"></a>Erforderliche Komponenten  
Um den Verfahrensweisen und Beispielen in diesen Themen zu folgen, benötigen Sie folgende Komponente:  
  
-   Eine Active Directory®-Domänendienste-Gesamtstruktur mit Schemaerweiterungen in Windows Server 2012 R2 zum Unterstützen der automatischen Weiterleitung von Computern und Geräten an den korrekten Server, wenn mehrere Server verwendet werden. Es wird empfohlen, dass DNS in der Gesamtstruktur aktiviert ist, dies ist jedoch nicht erforderlich.  
  
-   Ein Domänen Controller: Ein Server, auf dem die AD DS-Rolle aktiviert ist und der mit einer Domäne konfiguriert ist (für das Testbeispiel contoso.com).  
  
    Es ist ein Domänencontroller erforderlich, auf dem mindestens Windows Server 2012 R2 ausgeführt wird, um die Geräteregistrierung für Workplace Join zu unterstützen. Wenn Sie Workplace Join nicht verwenden möchten, können Sie Windows Server 2012 auf dem Domänencontroller ausführen.  
  
-   Zwei mit der Domäne verknüpfte Server (z. B. contoso.com), auf denen Windows Server 2016 ausgeführt werden. Ein für AD FS und ein für Arbeitsordner verwendeter Server.  
  
-   Ein Server, der mit keiner Domäne verknüpft ist und auf dem Windows Server 2016 ausgeführt wird. Dieser Server führt die Webanwendungsproxy aus und muss über eine Netzwerkkarte für die Netzwerkdomäne (z. B. contoso.com) und eine andere Netzwerkkarte für das externe Netzwerk verfügen.  
  
-   Eine mit einer Domäne verknüpfter Clientcomputer, auf dem Windows 7 oder höher ausgeführt wird.  
  
-   Eine nicht mit einer Domäne verknüpfter Clientcomputer, auf dem Windows 7 oder höher ausgeführt wird.  
  
Für die in dieser Anleitung beschriebene Testumgebung sollten Sie über die in der folgenden Abbildung dargestellten Topologie verfügen. Bei diesen Hosts kann es sich um physische oder virtuelle Computer (VMs) handeln. 
  
![Diagramm mit Internet, DMZ und Contoso-Netzwerksegmenten. Im Internet Segment: CLIENT2 in der DMZ: a WAP-Server; im "%"-Segment: Arbeitsordner Server, ein Domänen Controller, ein AD FS Server und CLIENT1](media/deploy-work-folders-adfs/WF_ADFS_WAP_Diagram.png)

## <a name="deployment-overview"></a>Bereitstellungsübersicht  
In dieser Themengruppe zeigen wir Ihnen ein schrittweises Beispiel zur Einrichtung von AD FS, Webanwendungsproxy und Arbeitsordnern in einer Testumgebung. Die Komponenten werden in folgender Reihenfolge eingerichtet:  
  
1.  AD FS  
  
2.  Arbeitsordner  
  
3.  Webanwendungsproxy  
  
4.  Eine mit einer Domäne verbundene Arbeitsstation und eine nicht mit einer Domäne verbundene Arbeitsstation  
  
Wir verwenden ein Windows PowerShell-Skript zur Erstellung von selbstsignierten Zertifikaten.  
  
## <a name="deployment-steps"></a>Bereitstellungsschritte  
Führen Sie die Schritte in diesen Themen aus, um die Bereitstellung mit einer Windows Server-Benutzeroberfläche auszuführen:  
  
-   [arbeits Ordner mit AD FS und dem webanwendungsproxy bereitstellen: Schritt 1: Einrichten AD FS @ no__t-0  
  
-   [arbeits Ordner mit AD FS und dem webanwendungsproxy bereitstellen: Schritt 2, AD FS Arbeit nach der Konfiguration @ no__t-0  
  
-   [arbeits Ordner mit AD FS und dem webanwendungsproxy bereitstellen: Schritt 3: Einrichten von Arbeits Ordnern @ no__t-0  
  
-   [arbeits Ordner mit AD FS und dem webanwendungsproxy bereitstellen: Schritt 4: Einrichten des webanwendungsproxys @ no__t-0  
  
-   [arbeits Ordner mit AD FS und dem webanwendungsproxy bereitstellen: Schritt 5: Einrichten von Clients @ no__t-0  

## <a name="see-also"></a>Siehe auch  
[Übersicht über Arbeitsordner](Work-Folders-Overview.md)  
[Entwerfen einer Arbeitsordnerimplementierung](Plan-Work-Folders.md)  
[Bereitstellen von Arbeitsordnern](Deploy-Work-Folders.md)  
  

