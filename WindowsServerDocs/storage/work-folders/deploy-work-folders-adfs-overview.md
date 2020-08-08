---
title: Arbeitsordner mit AD FS und webanwendungsproxy-Übersicht bereitstellen
ms.topic: article
ms.assetid: ea19f0f0-6cc0-4322-b387-c0873f7795ad
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.openlocfilehash: 386f7b4ad2646b09b06c98321385143d09483160
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87965977"
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-overview"></a>Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die Themen in diesem Abschnitt enthalten Anweisungen zum Bereitstellen von Arbeits Ordnern mit Active Directory-Verbunddienste (AD FS) (AD FS) und dem webanwendungsproxy. Die Anweisungen sind so konzipiert, dass Sie ein funktionsfähiges Arbeitsordner-Setup mit Client Computern erstellen können, die für die Verwendung von Arbeits Ordnern lokal oder über das Internet bereit sind.

Arbeitsordner ist eine Komponente, die in Windows Server 2012 R2 eingeführt wurde und es Information Workern ermöglicht, Arbeitsdateien zwischen ihren Geräten zu synchronisieren. Weitere Informationen über Arbeitsordner finden Sie unter [Übersicht: Arbeitsordner](Work-Folders-Overview.md).

Um Benutzern die Synchronisierung der Arbeitsordner über das Internet zu ermöglichen, müssen Sie Arbeitsordner über einen Reverseproxy veröffentlichen, sodass Arbeitsordner extern im Internet verfügbar sind. Der webanwendungsproxy, der in AD FS enthalten ist, ist eine Option, die Sie verwenden können, um Reverseproxyfunktionen bereitzustellen. Der webanwendungsproxy authentifiziert den Zugriff auf die Webanwendung für Arbeitsordner mit AD FS, damit Benutzer auf jedem Gerät von außerhalb des Unternehmensnetzwerks auf Arbeitsordner zugreifen können.

> [!NOTE]
>   Die in diesem Abschnitt behandelten Anweisungen gelten für eine Windows Server 2016-Umgebung. Wenn Sie Windows Server 2012 R2 verwenden, befolgen Sie die [Anweisungen unter Windows Server 2012 R2](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn747208(v=ws.11)).

Diese Themen stellen Folgendes bereit:

-   Schritt-für-Schritt-Anleitungen zum Einrichten und Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy über die Windows Server-Benutzeroberfläche. In den Anweisungen wird beschrieben, wie Sie eine einfache Testumgebung mit selbst signierten Zertifikaten einrichten. Anschließend können Sie das Testbeispiel als Leitfaden verwenden, um eine Produktionsumgebung zu erstellen, die öffentlich vertrauenswürdige Zertifikate verwendet.

## <a name="prerequisites"></a>Voraussetzungen
Um den Verfahren und Beispielen in diesen Themen folgen zu können, müssen die folgenden Komponenten bereit sein:

-   Eine Active Directory® Domänen Dienste-Gesamtstruktur mit Schema Erweiterungen in Windows Server 2012 R2 zur Unterstützung automatischer Verweise von PCs und Geräten an den korrekten Dateiserver, wenn Sie mehrere Dateiserver verwenden. Es ist vorzuziehen, dass DNS in der Gesamtstruktur aktiviert ist, dies ist jedoch nicht erforderlich.

-   Ein Domänen Controller: ein Server, auf dem die AD DS-Rolle aktiviert ist und der mit einer Domäne konfiguriert ist (für das Testbeispiel contoso.com).

    Ein Domänen Controller, auf dem mindestens Windows Server 2012 R2 ausgeführt wird, ist erforderlich, um die Geräteregistrierung für Workplace Join zu unterstützen. Wenn Sie Workplace Join nicht verwenden möchten, können Sie Windows Server 2012 auf dem Domänen Controller ausführen.

-   Zwei Server, die der Domäne hinzugefügt werden (z. b. contoso.com) und auf denen Windows Server 2016 ausgeführt wird. Ein Server wird für die AD FS verwendet, und die andere wird für Arbeitsordner verwendet.

-   Ein Server, der keiner Domäne beigetreten ist und auf dem Windows Server 2016 ausgeführt wird. Dieser Server führt den webanwendungsproxy aus, und er muss über eine Netzwerkkarte für die Netzwerk Domäne (z. b. contoso.com) und eine weitere Netzwerkkarte für das externe Netzwerk verfügen.

-   Ein in die Domäne eingebundener Client Computer, auf dem Windows 7 oder höher ausgeführt wird.

-   Ein nicht in die Domäne eingebundener Client Computer, auf dem Windows 7 oder höher ausgeführt wird.

Für die Testumgebung, die wir in diesem Handbuch abdecken, sollten Sie über die Topologie verfügen, die in der folgenden Abbildung dargestellt ist. Dabei kann es sich um physische oder virtuelle Computer (Virtual Machines, VMS) handeln.

![Das Diagramm zeigt die Netzwerksegmente "Internet", "DMZ" und "Netzwerk". Im Internet Segment: client2; in der DMZ: a WAP-Server; im "%"-Segment: Arbeitsordner Server, ein Domänen Controller, ein AD FS Server und CLIENT1](media/deploy-work-folders-adfs/WF_ADFS_WAP_Diagram.png)

## <a name="deployment-overview"></a>Übersicht über die Bereitstellung
In dieser Gruppe von Themen wird Schritt für Schritt erläutert, wie Sie AD FS, den webanwendungsproxy und die Arbeitsordner in einer Testumgebung einrichten. Die Komponenten werden in dieser Reihenfolge eingerichtet:

1.  AD FS

2.  Arbeitsordner

3.  Webanwendungsproxy

4.  Die in die Domäne eingebundenen Arbeitsstationen und Arbeitsstationen, die keiner Domäne beigetreten sind

Sie verwenden auch ein Windows PowerShell-Skript, um selbst signierte Zertifikate zu erstellen.

## <a name="deployment-steps"></a>Bereitstellungsschritte
Um die Bereitstellung mithilfe der Windows Server-Benutzeroberfläche auszuführen, führen Sie die Schritte in den folgenden Themen aus:

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 1, einrichten AD FS](deploy-work-folders-adfs-step1.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und dem webanwendungsproxy: Schritt 2 AD FS arbeiten nach der Konfiguration](deploy-work-folders-adfs-step2.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 3, Einrichten von Arbeits Ordnern](deploy-work-folders-adfs-step3.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 4](deploy-work-folders-adfs-step4.md)

-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy: Schritt 5: Einrichten von Clients](deploy-work-folders-adfs-step5.md)

## <a name="see-also"></a>Weitere Informationen
[Übersicht über](Work-Folders-Overview.md) 
 Arbeitsordner [Entwerfen einer Arbeitsordner Implementierung](Plan-Work-Folders.md) 
 Bereitstellen von [Arbeits Ordnern](Deploy-Work-Folders.md)

