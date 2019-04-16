---
ms.assetid: 7d957ebb-3476-49d8-b00b-6e93b4a94778
title: Identifizieren von Gesamtstruktur-Entwurfsanforderungen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 91d551e5d7b6daa6b1476570dad57e85d3bc163f
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="identifying-forest-design-requirements"></a>Identifizieren von Gesamtstruktur-Entwurfsanforderungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Zum Erstellen eines Gesamtstrukturentwurfs für Ihre Organisation müssen Sie die geschäftsanforderungen ermitteln, die die Verzeichnisstruktur zu berücksichtigen. Dies beinhaltet, wie viel Eigenständigkeit bestimmen die Gruppen in Ihrer Organisation benötigen zum Verwalten von ihre Netzwerkressourcen und ob jede Gruppe benötigt, um ihre Ressourcen im Netzwerk aus anderen Gruppen zu isolieren.  
  
Active Directory-Domänendienste (AD DS) können Sie zum Entwerfen einer Directory-Infrastruktur, die mehrere Gruppen innerhalb einer Organisation ermöglicht, die besondere verwaltungsanforderungen und strukturelle und betriebliche Unabhängigkeit zwischen Gruppen bei Bedarf zu erzielen.  
  
Gruppen in Ihrer Organisation möglicherweise einige der folgenden Typen von Anforderungen:  
  
-   **Anforderungen an die Organisationsstruktur**. Teilen einer Organisation können eine gemeinsame Infrastruktur Kosten sparen, aber es ist erforderlich, unabhängig vom Rest der Organisation arbeiten teilnehmen. Eine Gruppe Research in einem großen Unternehmen müssen möglicherweise die Kontrolle über alle ihre eigenen Daten Research.  
  
-   **Betriebsanforderungen**. Ein Teil des Unternehmens möglicherweise eindeutige Einschränkungen für die Konfiguration des Verzeichnisdienstes, Verfügbarkeit oder Sicherheit zu platzieren oder Anwendungen, die eindeutige Einschränkungen für das Verzeichnis zu speichern. Einzelnen Geschäftseinheiten innerhalb einer Organisation können z. B. AD-aktivierte Anwendungen, die das Verzeichnisschema ändern bereitstellen, die nicht von anderen Geschäftseinheiten bereitgestellt werden. Da Verzeichnisschema zwischen allen Domänen in der Gesamtstruktur freigegeben ist, ist das Erstellen von mehreren Gesamtstrukturen eine Lösung für ein solches Szenario. Weitere Beispiele finden Sie in der folgenden Organisationen und Szenarien:  
  
    -   Folgendem Organisationen  
  
    -   Hosting-Szenarios  
  
    -   Organisationen, die ein Verzeichnis zu verwalten, die intern und extern (z. B. solche, die von Benutzern im Internet öffentlich zugänglich sind.)  
  
-   **Gesetzlichen Vorschriften**. Einige Organisationen haben gesetzliche Vorschriften für den Betrieb in eine bestimmte Art und Weise, z. B. Einschränken des Zugriffs auf bestimmte Informationen in einem Unternehmen Vertrag. Einige Organisationen haben sicherheitsanforderungen in isolierten internen Netzwerken ausgeführt werden. Die folgenden Anforderungen erfüllen kann zum Verlust des Vertrags und möglicherweise rechtliche Schritte führen.  
  
Identifizieren der Gesamtstruktur-entwurfsanforderungen gehört, identifiziert den Grad für den Gruppen in Ihrer Organisation die mögliche Gesamtstrukturbesitzer und Dienstadministratoren vertrauen können, und Identifizieren der Anforderungen Autonomie und Isolation für jede Gruppe in Ihrer Organisation.  
  
Das Entwurfsteam muss die Anforderungen für Dienst- und Verwaltung für jede Gruppe in der Organisation Isolation und Autonomie dokumentieren, die AD DS verwenden möchte. Das Team muss auch Bereiche mit eingeschränkter Verbindung beachten, die die Bereitstellung von AD DS beeinflussen könnten.  
  
Das Entwurfsteam muss die Anforderungen für Dienst- und Verwaltung für jede Gruppe in der Organisation Isolation und Autonomie dokumentieren, die AD DS verwenden möchte. Das Team muss auch Bereiche mit eingeschränkter Verbindung beachten, die die Bereitstellung von AD DS beeinflussen könnten. Für ein Arbeitsblatt, hilft Ihnen bei der dokumentieren die Bereiche, die Sie festgelegt haben, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip).  
  
## <a name="in-this-section"></a>In diesem Abschnitt  
  
-   [Dienstadministrator Autoritätsumfang](../../ad-ds/plan/Service-Administrator-Scope-of-Authority.md)  
  
-   [Autonomie im Vergleich zur Isolation](../../ad-ds/plan/Autonomy-vs.-Isolation.md)  
  


