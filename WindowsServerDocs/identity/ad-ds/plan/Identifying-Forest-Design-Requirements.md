---
ms.assetid: 7d957ebb-3476-49d8-b00b-6e93b4a94778
title: Identifizieren von Gesamtstruktur-Entwurfsanforderungen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: bf8d9d164bf07151572785cda906be911f97b53e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835331"
---
# <a name="identifying-forest-design-requirements"></a>Identifizieren von Gesamtstruktur-Entwurfsanforderungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um eine Gesamtstrukturentwurf für Ihre Organisation zu erstellen, müssen Sie die geschäftlichen Anforderungen identifizieren, die die Verzeichnisstruktur zu berücksichtigen. Dies beinhaltet, wie viel Autonomie bestimmen die Gruppen in den Bedarf Ihrer Organisation zum Verwalten ihrer Netzwerkressourcen und angibt, ob jede Gruppe muss, um ihre Ressourcen im Netzwerk aus anderen Gruppen zu isolieren.  
  
Active Directory-Domänendienste (AD DS) ermöglicht es Ihnen zum Entwerfen einer Directory-Infrastruktur, die mehrere Gruppen innerhalb einer Organisation ausgelegt ist, die besondere verwaltungsanforderungen und strukturelle und operative Unabhängigkeit zwischen den Gruppen zu erreichen. Je nach Bedarf.  
  
Gruppen in Ihrer Organisation möglicherweise einige der folgenden Typen von Anforderungen:  
  
-   **Anforderungen an die Organisationsstruktur**. Teile einer Organisation möglicherweise teilnehmen, in einer freigegebenen Infrastruktur sparen Sie Kosten aber erfordern die Fähigkeit, unabhängig vom Rest des Unternehmens ausgeführt werden. Beispielsweise kann eine Research-Gruppe in einer großen Organisation müssen Kontrolle über ihre eigenen Research-Daten zu verwalten.  
  
-   **Betriebsanforderungen**. Ein Mitglied einer Organisation möglicherweise unique-Einschränkungen für die Konfiguration des Verzeichnisdienstes, Verfügbarkeit oder die Sicherheit zu platzieren oder Anwendungen, die unique-Einschränkungen für das Verzeichnis platzieren verwenden. Einzelne Unternehmenseinheiten innerhalb einer Organisation können z. B. AD-aktivierte Anwendungen, die der Directory-Schema ändern bereitstellen, die nicht von anderen Geschäftseinheiten bereitgestellt werden. Da alle Domänen in der Gesamtstruktur des Directory-Schemas gemeinsam verwendet wird, ist das Erstellen von mehreren Gesamtstrukturen eine Lösung für ein solches Szenario aus. Weitere Beispiele finden Sie in der folgenden Organisationen und Szenarien:  
  
    -   Militärische Organisationen  
  
    -   Hosting-Szenarios  
  
    -   Organisationen, die ein Verzeichnis zu verwalten, die verfügbar ist intern und extern (z. B. diejenigen, die von Benutzern im Internet öffentlich zugänglich sind)  
  
-   **Rechtliche Bestimmungen**. Einige Organisationen verfügen über rechtlichen Anforderungen für den Betrieb in eine bestimmte Art und Weise, z. B. Einschränken des Zugriffs auf bestimmte Informationen, wie in einem Business-Vertrag angegeben. Einige Organisationen verfügen über sicherheitsanforderungen, die in isolierten, internen Netzwerken ausgeführt werden. Die folgenden Anforderungen erfüllen kann zum Verlust des Vertrags und ggf. rechtliche Schritte führen.  
  
Identifizieren den Grad, zu dem Gruppen in Ihrer Organisation die potenziellen Gesamtstrukturbesitzer und ihrer Dienstadministratoren vertrauen können, und Identifizieren der Anforderungen Autonomie und Isolation für jeden Identifizieren Ihrer Gesamtstruktur-entwurfsanforderungen gehört die Gruppe in Ihrer Organisation.  
  
Das Designteam muss die Isolation und Autonomie Anforderungen für die Verwaltung von Dienst und die Daten für jede Gruppe in der Organisation dokumentieren, die AD DS verwenden möchte. Das Team muss alle Bereiche der eingeschränkte Konnektivität Beachten Sie außerdem, die die Bereitstellung von AD DS auswirken.  
  
Das Designteam muss die Isolation und Autonomie Anforderungen für die Verwaltung von Dienst und die Daten für jede Gruppe in der Organisation dokumentieren, die AD DS verwenden möchte. Das Team muss alle Bereiche der eingeschränkte Konnektivität Beachten Sie außerdem, die die Bereitstellung von AD DS auswirken. Bei einem Arbeitsblatt zur Unterstützung beim Dokumentieren der Regions, die Sie angegeben haben, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip aus [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) , und öffnen Sie "-Gesamtstruktur Entwerfen Sie Anforderungen an"(DSSLOGI_2.doc).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Dienstadministrator-Bereich der Zertifizierungsstelle](../../ad-ds/plan/Service-Administrator-Scope-of-Authority.md)  
  
-   [Autonomie im Vergleich zu Isolation](../../ad-ds/plan/Autonomy-vs.-Isolation.md)  
