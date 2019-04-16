---
ms.assetid: ef63d40c-a262-4a18-938d-b95c10680c0b
title: Autonomie im Vergleich zur Isolation
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 19613b209399c61747af6a2d1fbe243dbcb92225
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="autonomy-vs-isolation"></a>Autonomie im Vergleich zur Isolation

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie können Ihre logischen Active Directory-Struktur zu einer der folgenden entwerfen:  
  
-   **Autonomie**. Umfasst die unabhängige, jedoch nicht exklusive Kontrolle über eine Ressource. Wenn Sie Autonomie erreichen, müssen Administratoren die Berechtigung zum Verwalten von Ressourcen unabhängig; Es gibt jedoch Administratoren mit höheren Berechtigungen, die auch steuern, diese Ressourcen und Steuerung übernehmen, sofort bei Bedarf. Sie können Ihre logischen Active Directory-Struktur an die folgenden Typen von Autonomie entwerfen:  
  
    -   **Autonomie Service**. Dieser Typ von Autonomie umfasst die Kontrolle über alle oder einen Teil der Servicemanagement.  
  
    -   **Datenautonomie**. Dieser Typ von Autonomie umfasst die Kontrolle über alle oder einen Teil der Daten im Verzeichnis oder auf Mitgliedscomputern hinzugefügt. das Verzeichnis gespeichert.  
  
-   **Isolation**. Umfasst die unabhängige und exklusive Kontrolle über eine Ressource. Wenn Sie die Isolation erreichen, Administratoren besitzen die Berechtigung zum unabhängigen Verwalten einer Ressource, und kein anderer Administrator Steuerung übernehmen, sofort der Ressource. Sie können Ihre logischen Active Directory-Struktur an die folgenden Typen von Isolation entwerfen:  
  
    -   **Service-Isolation**. Verhindert, dass Administratoren (mit Ausnahme von den Administratoren, die speziell, zum Steuern von Servicemanagement gekennzeichnet sind) Steuerung oder dienstverwaltung zu stören.  
  
    -   **Datenisolierung**. Verhindert, dass Administratoren (mit Ausnahme von den Administratoren, die speziell zu steuern und Anzeigen von Daten aufgeführt sind) Steuerung oder Anzeigen einer Teilmenge von Daten im Verzeichnis oder auf Mitgliedscomputern in das Verzeichnis hinzugefügt.  
  
Administratoren, die lediglich Autonomie benötigen annehmen, dass andere Administratoren, die größer oder gleich Verwaltungsautorität größer oder gleich Steuerung der Dienst- oder Verwaltung verfügen. Administratoren, die Isolierung von Instanzen erfordern über exklusive Steuerung der Dienst- oder Verwaltung verfügen. Erstellen eines Entwurfs für Autonomie erreicht ist in der Regel kostengünstiger als Erstellen eines Entwurfs für Isolation erreicht.  
  
In Active Directory-Domänendiensten (AD DS) können Administratoren Verwaltung von Diensten und Administration an entweder Autonomie oder Trennung zwischen Organisationen delegieren. Die Kombination von Servicemanagement, Data Management, Autonomie und Isolation Anforderungen einer Organisation auswirken die Active Directory-Container, die verwendet werden, um die Verwaltung delegieren.  
  
## <a name="isolation-and-autonomy-requirements"></a>Anforderungen an die Isolation und Autonomie  
Die Anzahl der Gesamtstrukturen, die Sie bereitstellen müssen basiert auf die Anforderungen Autonomie und Trennung der einzelnen Gruppen in Ihrer Organisation. Um die Gesamtstruktur-entwurfsanforderungen zu identifizieren, müssen Sie die Anforderungen für alle Gruppen Autonomie und Isolation in Ihrer Organisation ermitteln. Insbesondere müssen Sie die Notwendigkeit datenisolierung, Daten-, Dienstisolation und Dienstautonomie ermitteln. Sie müssen auch eingeschränkter Konnektivität in Ihrer Organisation zu ermitteln.  
  
### <a name="data-isolation"></a>Datenisolation  
Datenisolation umfasst die exklusive Steuerung der Daten durch die Gruppe oder Organisation, die die Daten besitzt. Es ist wichtig zu beachten, dass Administratoren die Möglichkeit, eine Ressource-Administratoren steuern. Und -Administratoren müssen nicht die Möglichkeit, um zu verhindern, dass Administratoren den Zugriff auf die Ressourcen, die sie steuern. Aus diesem Grund können nicht Sie Datenisolation erreichen, wenn eine andere Gruppe innerhalb der Organisation für die Verwaltung von Diensten zuständig ist. Wenn eine Gruppe datenisolierung erforderlich ist, muss dieser Gruppe auch Verantwortung für die Verwaltung von Diensten davon ausgehen.  
  
Da Daten gespeichert, in AD DS und auf Computern in AD DS können nicht von Dienstadministratoren isoliert werden, die einzige Möglichkeit für eine Gruppe innerhalb einer Organisation, die vollständigen Datenisolation zu erreichen ist die Erstellung eine separate Gesamtstruktur für diese Daten. Organisationen, die für die die Folgen eines Angriffs durch Schadsoftware oder durch einen umgewandelte Dienstadministrator erhebliche sind können zum Erstellen einer separaten Gesamtstruktur um datenisolierung zu erreichen. Gesetzliche Anforderungen erstellen in der Regel müssen für diese Art von Datenisolation. Zum Beispiel:  
  
-   Eine Bank ist gesetzlich vorgeschrieben, um den Zugriff auf Daten beschränken, die für Clients in einer bestimmten Zuständigkeit für Benutzer, Computer und befindet sich unter die Gerichtsbarkeit Administratoren gehört. Obwohl der Institution Dienstadministratoren, die außerhalb der geschützten, funktionieren vertraut, wenn die Access-Einschränkung verletzt wird, wird der Institution sind nicht mehr in die Zuständigkeit Geschäfte können. Daher muss die Bank Daten von Dienstadministratoren außerhalb dieser Zuständigkeit isolieren. Beachten Sie, dass die Verschlüsselung nicht immer eine Alternative für diese Lösung ist. Verschlüsselung möglicherweise keine Daten von Dienstadministratoren schützen.  
  
-   Ein Schutz-Auftragnehmer ist gesetzlich vorgeschrieben, den Zugriff auf die Projektdaten an einen angegebenen Satz von Benutzern beschränken. Obwohl die Auftragnehmer Dienstadministratoren, die im Zusammenhang mit anderen Projekten Computersystemen zu verwalten vertraut, bewirkt ein Verstoß gegen diese Einschränkung Zugriff der Auftragnehmer Unternehmen verlieren.  
  
    > [!NOTE]  
    > Wenn Daten Isolation erforderlich ist, müssen Sie entscheiden, sollten Sie Ihre Daten von Dienstadministratoren oder Datenadministratoren und gewöhnliche Benutzer isolieren. Wenn Ihre Anforderung Isolation Isolation vom Datenadministratoren und gewöhnliche Benutzer basiert, können Sie Zugriffssteuerungslisten (ACLs), um die Daten zu isolieren. Für die Zwecke dieses Prozesses Design gilt Isolation vom Datenadministratoren und gewöhnliche Benutzer nicht Daten Isolation erforderlich.  
  
### <a name="data-autonomy"></a>Datenautonomie  
Datenautonomie umfasst die Möglichkeit einer Gruppe oder einer Organisation, einen eigenen Daten, einschließlich administrative Entscheidung über die Daten und alle erforderlichen administrativen Aufgaben ohne Genehmigung von einer anderen Zertifizierungsstelle durchführen zu verwalten.  
  
Datenautonomie verhindert nicht, dass Dienstadministratoren in der Gesamtstruktur auf die Daten zugreifen. Z. B. eine Gruppe Research in einem großen Unternehmen möchten die Projekt-spezifischen Daten selbst verwalten können, jedoch nicht erforderlich, um die Daten von anderen Administratoren in der Gesamtstruktur zu schützen.  
  
### <a name="service-isolation"></a>Isolation von Diensten  
Dienstisolation umfasst das exklusive Steuerung der Active Directory-Infrastruktur. Gruppen, die Dienstisolation erfordern erfordern, dass kein Administrator außerhalb der Gruppe der Betrieb des Verzeichnisdiensts beeinträchtigen kann.  
  
Normalerweise erstellen betrieblichen oder rechtliche Anforderungen müssen für die Dienstisolation. Zum Beispiel:  
  
-   Ein Unternehmen hat eine wichtige Anwendung, die Geräte bei der Fertigung steuert. Unterbrechung der Dienst auf andere Teile des Netzwerks der Organisation können nicht zugelassen, den Betrieb der Fabrik stören.  
  
-   Einem Hostinganbieter bietet mehrere Clients. Jeder Client erfordert Dienstisolation, sodass Unterbrechung des Diensts, der einen Client wirkt sich nicht auf die anderen Clients auswirkt.  
  
### <a name="service-autonomy"></a>Autonomie eines Dienstes  
Dienstautonomie umfasst die Möglichkeit, die Verwaltung der Infrastruktur ohne eine Voraussetzung für die exklusive Steuerung; z. B. wenn eine Gruppe möchte so ändern Sie die Infrastruktur (z. B. hinzufügen oder Entfernen von Domänen, ändern den Domain Name System (DNS)-Namespace oder Ändern des Schemas) ohne Genehmigung der Gesamtstrukturbesitzer.  
  
Dienstautonomie könnte innerhalb einer Organisation für eine Gruppe, die die Dienstebene von AD DS (durch Hinzufügen und Entfernen von Domänencontrollern nach Bedarf) steuern können möchte oder für eine Gruppe, die AD-aktivierte Anwendungen installieren, die schemaerweiterungen zu erfordern erforderlich sein.  
  
## <a name="limited-connectivity"></a>Eingeschränkter Konnektivität  
Wenn eine Gruppe in Ihrer Organisation Netzwerke besitzt, die von Geräten getrennt sind, die einschränken oder begrenzen die Konnektivität zwischen Netzwerken (z. B. Firewalls und Geräten (Network Address Translation, NAT)), kann dies beim Entwurf Ihrer Gesamtstruktur auswirken. Wenn Sie die Gesamtstruktur-entwurfsanforderungen identifiziert haben, müssen Sie die Speicherorte Beachten Sie, wo die Netzwerkkonnektivität eingeschränkt ist. Diese Informationen sind erforderlich, um Entscheidungen in Bezug auf die Gesamtstrukturentwurf aktivieren.  
  


