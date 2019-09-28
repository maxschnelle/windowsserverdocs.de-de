---
ms.assetid: 7d957ebb-3476-49d8-b00b-6e93b4a94778
title: Identifizieren von Gesamtstruktur-Entwurfsanforderungen
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/07/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 41caeca82819eaea3d86d5f1eb4883ab8bbf53cc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408792"
---
# <a name="identifying-forest-design-requirements"></a>Identifizieren von Gesamtstruktur-Entwurfsanforderungen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Um einen Gesamtstruktur Entwurf für Ihre Organisation zu erstellen, müssen Sie die geschäftlichen Anforderungen ermitteln, die Ihre Verzeichnisstruktur erfüllen muss. Dies umfasst die Festlegung, wie viel Autonomie die Gruppen in Ihrer Organisation benötigen, um Ihre Netzwerkressourcen zu verwalten, und ob die einzelnen Gruppen ihre Ressourcen im Netzwerk von anderen Gruppen isolieren müssen.  
  
Mit Active Directory Domain Services (AD DS) können Sie eine Verzeichnis Infrastruktur entwerfen, die mehrere Gruppen innerhalb einer Organisation mit eindeutigen Verwaltungsanforderungen und der strukturellen und operativen Unabhängigkeit zwischen Gruppen unterstützt. nach Bedarf.  
  
Für Gruppen in Ihrer Organisation sind möglicherweise einige der folgenden Arten von Anforderungen erforderlich:  
  
-   **Anforderungen an die Organisationsstruktur**. Teile einer Organisation könnten an einer gemeinsam genutzten Infrastruktur teilnehmen, um Kosten zu sparen, müssen jedoch unabhängig vom Rest der Organisation agieren können. Beispielsweise muss eine Forschungsgruppe innerhalb einer großen Organisation möglicherweise die Kontrolle über alle eigenen Forschungsdaten behalten.  
  
-   **Betriebliche Anforderungen**. Ein Teil einer Organisation kann eindeutige Einschränkungen der Verzeichnisdienst Konfiguration, der Verfügbarkeit oder der Sicherheit oder Anwendungen verwenden, die UNIQUE-Einschränkungen für das Verzeichnis platzieren. Beispielsweise können einzelne Geschäftseinheiten innerhalb eines Unternehmens Verzeichnis aktivierte Anwendungen bereitstellen, die das Verzeichnisschema ändern, das nicht von anderen Geschäftseinheiten bereitgestellt wird. Da das Verzeichnisschema für alle Domänen in der Gesamtstruktur freigegeben ist, ist das Erstellen mehrerer Gesamtstrukturen eine Lösung für ein solches Szenario. Weitere Beispiele finden Sie in den folgenden Organisationen und Szenarien:  
  
    -   Militärische Organisationen  
  
    -   Hostingszenarios  
  
    -   Organisationen, die ein Verzeichnis verwalten, das sowohl intern als auch extern verfügbar ist (z. b. solche, die für Benutzer im Internet öffentlich zugänglich sind)  
  
-   **Rechtliche Anforderungen**. Einige Organisationen haben gesetzliche Anforderungen für eine bestimmte Methode, z. b. das Einschränken des Zugriffs auf bestimmte Informationen, wie in einem Geschäftsvertrag angegeben. Einige Organisationen verfügen über Sicherheitsanforderungen, um auf isolierten internen Netzwerken zu arbeiten. Wenn diese Anforderungen nicht erfüllt werden, kann dies zu einem Verlust des Vertrags und möglicherweise zu rechtlichen Aktionen führen.  
  
Zum Identifizieren der Gesamtstruktur-Entwurfs Anforderungen müssen Sie angeben, inwieweit Gruppen in Ihrer Organisation den potenziellen Gesamtstruktur Besitzern und deren Dienst Administratoren vertrauen können und welche Autonomie-und Isolations Anforderungen für die einzelnen in Ihrer Organisation gruppieren.  
  
Das Entwurfs Team muss die Isolations-und Autonomie Anforderungen für die Dienst-und Datenverwaltung für jede Gruppe in der Organisation dokumentieren, die AD DS verwenden soll. Das Team muss auch alle Bereiche eingeschränkter Konnektivität beachten, die sich auf die Bereitstellung von AD DS auswirken können.  
  
Das Entwurfs Team muss die Isolations-und Autonomie Anforderungen für die Dienst-und Datenverwaltung für jede Gruppe in der Organisation dokumentieren, die AD DS verwenden soll. Das Team muss auch alle Bereiche eingeschränkter Konnektivität beachten, die sich auf die Bereitstellung von AD DS auswirken können. Für ein Arbeitsblatt, das Sie bei der Dokumentation der identifizierten Regionen unterstützt, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip aus den [Auftrags Hilfen für das Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558) herunter, und öffnen Sie "Gesamtstruktur-Entwurfs Anforderungen" ( DSSLOGI_2. doc).  
  
## <a name="in-this-section"></a>Inhalt dieses Abschnitts  
  
-   [Dienstadministrator: Autoritätsumfang](../../ad-ds/plan/Service-Administrator-Scope-of-Authority.md)  
  
-   [Gegenüberstellung von Autonomie und Isolation](../../ad-ds/plan/Autonomy-vs.-Isolation.md)  
