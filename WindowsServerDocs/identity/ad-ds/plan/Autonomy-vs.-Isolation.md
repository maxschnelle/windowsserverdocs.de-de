---
ms.assetid: ef63d40c-a262-4a18-938d-b95c10680c0b
title: Autonomie im Vergleich zu Isolierung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 765a25d3d1ffdb4df473e1fb5bb65e532934aca9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59867571"
---
# <a name="autonomy-vs-isolation"></a>Autonomie im Vergleich zu Isolierung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können die logische Struktur Ihrer Active Directory erreichen Sie eine der folgenden entwerfen:  
  
-   **Autonomie**. Umfasst die unabhängige, aber keine exklusive Kontrolle über eine Ressource. Wenn Sie Autonomie erreichen, haben Administratoren die Berechtigung zum Verwalten von Ressourcen unabhängig; Administratoren mit der Autorität für die größer sind jedoch vorhanden, die auch Kontrolle über diese Ressourcen und können übernehmen Sie die Kontrolle sofort bei Bedarf. Sie können Ihre logischen Active Directory-Struktur, um die folgenden Typen von Autonomie zu erreichen entwerfen:  
  
    -   **Dienst Autonomie**. Diese Art von Autonomie umfasst die Kontrolle über alle oder einen Teil der dienstverwaltung.  
  
    -   **Datenautonomie**. Diese Art von Autonomie umfasst die Kontrolle über alle oder einen Teil der Daten im Verzeichnis oder auf Computern, die eingebunden in das Verzeichnis angehören.  
  
-   **Isolation**. Umfasst die unabhängige und exklusive Kontrolle über eine Ressource. Wenn Sie Isolation erreichen, kann Administratoren berechtigt, auf eine Ressource unabhängig zu verwalten, und kein anderer Administrator sofort Steuerung über die Ressource. Sie können Ihre logischen Active Directory-Struktur, um die folgenden Typen von Isolierung zu erzielen entwerfen:  
  
    -   **Service Isolation**. Verhindert, dass Administratoren (mit Ausnahme von Administratoren, die speziell zum Steuern der dienstverwaltung gekennzeichnet sind) Steuerung oder dienstverwaltung behindert.  
  
    -   **Die Datenisolation**. Verhindert, dass Administratoren (mit Ausnahme von Administratoren, die speziell zum Steuerelement oder Anzeigen von Daten vorgesehen sind) aus steuern oder eine Teilmenge der Daten anzeigen, in das Verzeichnis oder auf Mitgliedscomputer in das Verzeichnis eingebunden.  
  
Administratoren, die nur die Autonomie benötigen akzeptieren, dass Administratoren, die größer oder gleich Verwaltungsberechtigungen verfügen größer oder gleich Kontrolle über die Verwaltung von Dienst oder Daten haben. Administratoren, die Isolation benötigen haben die exklusive Kontrolle über die Dienst- und Verwaltung. Erstellen eines Entwurfs, Autonomie zu erreichen, ist in der Regel weniger aufwendig als bei der Erstellung eines Entwurfs um Isolierung zu erzielen.  
  
In Active Directory Domain Services (AD DS) können Administratoren delegieren und dienstverwaltung und Verwaltung von Daten an die Autonomie oder Trennung zwischen Organisationen zu erreichen. Die Kombination der dienstverwaltung, beeinträchtigen Data Management, Autonomie und Isolation Anforderungen einer Organisation die Active Directory-Container, die verwendet werden, um die Verwaltung delegieren.  
  
## <a name="isolation-and-autonomy-requirements"></a>Anforderungen an Isolation und Autonomie  
Die Anzahl der Gesamtstrukturen, die Sie bereitstellen müssen basiert auf den Anforderungen Autonomie und Trennung der einzelnen Gruppen innerhalb Ihrer Organisation. Um Ihre Gesamtstruktur-entwurfsanforderungen zu identifizieren, müssen Sie die Autonomie und Isolation Anforderungen für alle Gruppen in Ihrer Organisation ermitteln. Insbesondere müssen Sie die Notwendigkeit für die Datenisolation, Datenautonomie, Isolation von Diensten und die Autonomie eines Dienstes identifizieren. Sie müssen auch Bereiche der eingeschränkte Konnektivität in Ihrem Unternehmen ermitteln.  
  
### <a name="data-isolation"></a>Datenisolation  
Die Datenisolation umfasst die exklusive Kontrolle über Daten, indem Sie die Gruppe oder Organisation, die die Daten besitzt. Es ist wichtig zu beachten, dass Administratoren die Möglichkeit, die Kontrolle über eine Ressource von Datenadministratoren haben. Und Datenadministratoren haben nicht die Möglichkeit, um zu verhindern, dass Administratoren den Zugriff auf die Ressourcen, die sie steuern. Sie können nicht aus diesem Grund die Datenisolation erzielen, wenn eine andere Gruppe innerhalb der Organisation für die Verwaltung von Diensten zuständig ist. Wenn eine Gruppe die Datenisolation erforderlich ist, muss dieser Gruppe außerdem Verantwortung für die dienstverwaltung wird.  
  
Da Daten in AD DS und auf Computern in AD DS können nicht von Dienstadministratoren isoliert werden, erstellen Sie eine separate Gesamtstruktur für die Daten ist die einzige Möglichkeit für eine Gruppe innerhalb einer Organisation, die vollständigen datenisolierung zu erzielen. Organisationen, die für die die Folgen eines Angriffs durch böswillige Software oder von einem umgewandelt Dienstadministrator umfangreich sind entscheiden sich möglicherweise zum Erstellen einer separaten Gesamtstruktur zur datenisolierung zu erzielen. Rechtliche Anforderungen werden in der Regel müssen für diesen Typ, der die Datenisolation erstellt. Zum Beispiel:  
  
-   Ein Finanzinstitut ist gesetzlich erforderlich, um den Zugriff auf Daten zu begrenzen, die für Clients in einer bestimmten Rechtsprechung gespeichert, Benutzern, Computern und Administratoren in diesem Land gehört. Auch wenn der Träger Dienstadministratoren vertraut, die außerhalb der geschützten, funktionieren, wenn die Access-Einschränkung verletzt wird, werden die Einrichtung nicht mehr möglich, Unternehmen, die Sie in diesem Land. Aus diesem Grund muss die Bank Daten von Dienstadministratoren außerhalb dieser Zuständigkeit isolieren. Beachten Sie, dass die Verschlüsselung nicht immer eine Alternative zu dieser Lösung ist. Verschlüsselung kann Daten von Dienstadministratoren nicht geschützt werden.  
  
-   Ein Auftragnehmer Defense ist gesetzlich erforderlich, den Zugriff auf Projektdaten zu einer angegebenen Menge von Benutzern einschränken. Zwar die Auftragnehmeranforderungsseite Dienstadministratoren, die steuern, Computersysteme, die im Zusammenhang mit anderen Projekten vertraut, verursacht ein Verstoß gegen diese Einschränkung für den Zugriff den Auftragnehmer Unternehmen verloren gehen.  
  
    > [!NOTE]  
    > Wenn Sie eine Anforderung der Isolation Daten verfügen, müssen Sie entscheiden, ob Sie Ihre Daten, die von Administratoren oder von Data-Administratoren und normale Benutzer isolieren müssen. Wenn Ihre Anforderung der Isolation zur Isolierung von Datenadministratoren und normale Benutzer basiert, können Sie Zugriffssteuerungslisten (ACLs), um die Daten zu isolieren. Im Rahmen dieser Entwurfsprozess wird in isoliert von Datenadministratoren und normale Benutzer die Anforderung der Isolation einer Daten nicht berücksichtigt.  
  
### <a name="data-autonomy"></a>Datenautonomie  
Datenautonomie umfasst die Möglichkeit einer Gruppe oder Organisation, eine eigene Daten, einschließlich administrative Entscheidungen zu den Daten, und alle erforderlichen administrativen Aufgaben ohne die Notwendigkeit zur Genehmigung von einer anderen Zertifizierungsstelle ausführen zu verwalten.  
  
Datenautonomie verhindert nicht, dass Dienstadministratoren in der Gesamtstruktur auf die Daten zugreift. Z. B. eine Research-Gruppe in einer großen Organisation ihre projektspezifische Daten selbst verwalten möchten, jedoch nicht zum Schützen der Daten von anderen Administratoren in der Gesamtstruktur erforderlich.  
  
### <a name="service-isolation"></a>Isolation von Diensten  
Isolation von Diensten umfasst die exklusive Kontrolle über die Active Directory-Infrastruktur. Gruppen, die Isolation von Diensten müssen erfordern, dass kein Administrator außerhalb der Gruppe durch den Vorgang des Verzeichnisdiensts beeinträchtigt werden kann.  
  
Betriebs- oder rechtliche Anforderungen werden in der Regel müssen für die Isolation von Diensten erstellt. Zum Beispiel:  
  
-   Ein Unternehmen verfügt über eine wichtige Anwendung, die Geräte am Herstellerstandort steuert. Unterbrechungen des Diensts auf andere Teile des Netzwerks der Organisation können keine Auswirkung auf den der Vorgang der Fabrik zulässig.  
  
-   Einem Hostingunternehmen stellt Dienst an mehrere Clients bereit. Isolation von Diensten für jeden Client erforderlich, damit die Unterbrechung des Diensts, die ein Client wirkt sich nicht auf den anderen Clients auswirkt.  
  
### <a name="service-autonomy"></a>Die Autonomie eines Dienstes  
Die Autonomie eines Dienstes umfasst die Möglichkeit zum Verwalten der Infrastruktur, ohne eine Voraussetzung für die exklusive Kontrolle; z. B. wenn eine Gruppe versucht wird, Ändern der Infrastruktur (z. B. hinzufügen oder Entfernen von Domänen, ändern den Domain Name System (DNS)-Namespace ein, oder Ändern des Schemas) ohne die Genehmigung des Besitzers Gesamtstruktur.  
  
Die Autonomie eines Dienstes ist möglicherweise erforderlich, innerhalb einer Organisation für eine Gruppe, die möchte, um den Servicelevel von AD DS (durch Hinzufügen und entfernen Domänencontroller, je nach Bedarf) steuern zu können oder für eine Gruppe, die AD-aktivierte Anwendungen installiert werden muss, ist die schemaerweiterungen erforderlich.  
  
## <a name="limited-connectivity"></a>Eingeschränkte Konnektivität  
Wenn eine Gruppe in Ihrer Organisation Netzwerke, die von den Geräten getrennt sind, die zu beschränken oder Konnektivität zwischen Netzwerken (z. B. Firewalls und -Geräten (Network Address Translation, NAT)) zu beschränken besitzt, kann dies beim Entwurf Ihrer Gesamtstruktur auswirken. Wenn Sie Ihre Gesamtstruktur-entwurfsanforderungen identifiziert haben, achten Sie darauf, dass Sie beachten Sie die Speicherorte, in dem Sie über eine Netzwerkverbindung eingeschränkte haben. Diese Informationen sind erforderlich, um Sie bei Ihren Entscheidungen in Bezug auf die Gesamtstrukturentwurf zu aktivieren.  
  


