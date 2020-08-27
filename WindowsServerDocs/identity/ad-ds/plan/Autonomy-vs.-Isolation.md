---
ms.assetid: ef63d40c-a262-4a18-938d-b95c10680c0b
title: Autonomie im Vergleich zur Isolation
author: iainfoulds
ms.author: iainfou
manager: daveba
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: eccbfc7767821a15d32d6aabef156861cb409f40
ms.sourcegitcommit: 1dc35d221eff7f079d9209d92f14fb630f955bca
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/26/2020
ms.locfileid: "88941210"
---
# <a name="autonomy-vs-isolation"></a>Autonomie im Vergleich zur Isolation

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie können Ihre Active Directory logische Struktur entwerfen, um eine der folgenden Optionen zu erreichen:

-   **Autonomie**. Umfasst unabhängige, aber nicht exklusive Kontrolle über eine Ressource. Wenn Sie Autonomie erreichen, haben Administratoren die Berechtigung, Ressourcen unabhängig zu verwalten. Administratoren mit höherer Autorität verfügen jedoch über die Kontrolle über diese Ressourcen und können bei Bedarf die Kontrolle entziehen. Sie können Ihre Active Directory logische Struktur entwerfen, um die folgenden Arten von Autonomie zu erreichen:

    -   **Dienst Autonomie**. Diese Art von Autonomie umfasst die Kontrolle über die gesamte oder einen Teil der Dienst Verwaltung.

    -   **Daten Autonomie**. Diese Art von Autonomie umfasst die Kontrolle über die gesamten oder einen Teil der im Verzeichnis gespeicherten Daten oder auf Mitglieds Computern, die mit dem Verzeichnis verknüpft sind.

-   **Isolation**: Umfasst unabhängige und exklusive Kontrolle über eine Ressource. Wenn Sie Isolation erreichen, haben Administratoren die Berechtigung, eine Ressource unabhängig zu verwalten, und kein anderer Administrator kann die Kontrolle über die Ressource entziehen. Sie können Ihre Active Directory logische Struktur entwerfen, um die folgenden Isolations Typen zu erreichen:

    -   **Dienst Isolation**. Verhindert, dass Administratoren (außer Administratoren, die speziell zum Steuern der Dienst Verwaltung vorgesehen sind) die Dienst Verwaltung Steuern oder beeinträchtigen.

    -   **Daten Isolation**. Verhindert, dass Administratoren (außer Administratoren, die speziell zum Steuern oder Anzeigen von Daten vorgesehen sind) Steuern oder eine Teilmenge der Daten im Verzeichnis oder auf Mitglieds Computern anzeigen können, die mit dem Verzeichnis verknüpft sind.

Administratoren, die nur Autonomie benötigen, akzeptieren, dass andere Administratoren, die über die gleiche oder eine höhere Verwaltungs Autorität verfügen, eine gleichmäßige Kontrolle über die Dienst-oder Datenverwaltung haben Administratoren, die Isolation benötigen, haben eine exklusive Kontrolle über die Dienst-oder Datenverwaltung. Das Erstellen eines Entwurfs zum Erreichen von Autonomie ist im Allgemeinen kostengünstiger als das Erstellen eines Entwurfs zum Erreichen von Isolation.

In Active Directory Domain Services (AD DS) können Administratoren sowohl die Dienst Verwaltung als auch die Datenverwaltung delegieren, um entweder Autonomie oder Isolation zwischen Unternehmen zu erreichen. Die Kombination aus Dienst Verwaltung, Datenverwaltung, Autonomie und Isolations Anforderungen eines Unternehmens wirkt sich auf die Active Directory Container aus, die zum Delegieren der Verwaltung verwendet werden.

## <a name="isolation-and-autonomy-requirements"></a>Isolations-und Autonomie Anforderungen
Die Anzahl der Gesamtstrukturen, die Sie bereitstellen müssen, basiert auf den Autonomie-und Isolations Anforderungen der einzelnen Gruppen innerhalb Ihrer Organisation. Zum Ermitteln der Gesamtstruktur-Entwurfs Anforderungen müssen Sie die Autonomie-und Isolations Anforderungen für alle Gruppen in Ihrer Organisation ermitteln. Insbesondere müssen Sie die Notwendigkeit der Daten Isolation, Daten Autonomie, Dienst Isolation und Dienst Autonomie ermitteln. Außerdem müssen Sie in Ihrer Organisation Bereiche mit eingeschränkter Konnektivität identifizieren.

### <a name="data-isolation"></a>Datenisolation
Die Daten Isolation umfasst die exklusive Kontrolle über Daten durch die Gruppe oder Organisation, die die Daten besitzt. Es ist wichtig zu beachten, dass Dienst Administratoren die Möglichkeit haben, die Kontrolle über eine Ressource von Daten Administratoren zu entfernen. -Und-Daten Administratoren können nicht verhindern, dass Dienst Administratoren auf die von Ihnen kontrollierten Ressourcen zugreifen können. Daher können Sie keine Daten Isolation erreichen, wenn eine andere Gruppe innerhalb des Unternehmens für die Dienst Verwaltung verantwortlich ist. Wenn eine Gruppe eine Daten Isolation erfordert, muss diese Gruppe auch für die Dienst Verwaltung verantwortlich sein.

Da Daten, die in AD DS und auf mit AD DS verbundenen Computern gespeichert sind, nicht von Dienst Administratoren isoliert werden können, besteht die einzige Möglichkeit für eine Gruppe innerhalb einer Organisation darin, eine separate Gesamtstruktur für diese Daten zu erstellen. Organisationen, für die die Konsequenzen eines Angriffs durch Schadsoftware oder einen erzwungenen Dienst Administrator beträchtlich sind, können eine separate Gesamtstruktur erstellen, um die Daten Isolation zu erreichen. Gesetzliche Anforderungen machen in der Regel einen Bedarf an dieser Art von Daten Isolation. Beispiel:

-   Ein Finanzinstitut ist gesetzlich vorgeschrieben, um den Zugriff auf Daten zu beschränken, die zu Clients in einem bestimmten Zuständigkeitsbereich gehören, und zwar für Benutzer, Computer und Administratoren, die sich in diesem Bereich befinden. Obwohl die-Einrichtung Dienst Administratoren vertraut, die außerhalb des geschützten Bereichs arbeiten, kann die Einrichtung bei Verstößen gegen die Zugriffsbeschränkung nicht mehr Unternehmen in diesem Zuständigkeitsbereich durchführen. Daher muss die Finanz Einrichtung Daten von Dienst Administratoren außerhalb dieses Gerichts nicht isolieren. Beachten Sie, dass die Verschlüsselung nicht immer eine Alternative zu dieser Lösung ist. Bei der Verschlüsselung werden Daten von Dienst Administratoren möglicherweise nicht geschützt.

-   Ein Verteidigungs Auftragnehmer ist gesetzlich vorgeschrieben, um den Zugriff auf Projektdaten auf eine bestimmte Gruppe von Benutzern einzuschränken. Der Auftragnehmer vertraut zwar Dienst Administratoren, die Computersysteme im Zusammenhang mit anderen Projekten kontrollieren, aber ein Verstoß gegen diese Zugriffsbeschränkung führt dazu, dass der Auftragnehmer das Geschäft verliert.

    > [!NOTE]
    > Wenn Sie eine Daten Isolations Anforderung haben, müssen Sie entscheiden, ob Sie Ihre Daten von Dienst Administratoren oder Daten Administratoren und normalen Benutzern isolieren müssen. Wenn die Isolations Anforderung auf der Isolation von Daten Administratoren und normalen Benutzern basiert, können Sie die Daten mithilfe von Zugriffs Steuerungs Listen (Access Control Lists, ACLs) isolieren. Im Rahmen dieses Entwurfsprozesses wird die Isolation von Daten Administratoren und normalen Benutzern nicht als Daten Isolations Anforderung betrachtet.

### <a name="data-autonomy"></a>Daten Autonomie
Die Daten Autonomie besteht darin, dass eine Gruppe oder Organisation ihre eigenen Daten verwalten kann, einschließlich administrativer Entscheidungen über die Daten und Durchführung erforderlicher administrativer Aufgaben, ohne dass eine Genehmigung von einer anderen Zertifizierungsstelle erforderlich ist.

Durch die Daten Autonomie wird nicht verhindert, dass Dienst Administratoren in der Gesamtstruktur auf die Daten zugreifen. So kann es beispielsweise vorkommen, dass eine Forschungsgruppe in einer großen Organisation ihre projektspezifischen Daten selbst verwalten kann, aber nicht die Daten von anderen Administratoren in der Gesamtstruktur sichern muss.

### <a name="service-isolation"></a>Dienstisolierung
Die Dienst Isolation umfasst die exklusive Kontrolle der Active Directory Infrastruktur. Für Gruppen, die eine Dienst Isolation erfordern, ist es erforderlich, dass kein Administrator außerhalb der Gruppe den Betrieb des Verzeichnis Dienstanbieter beeinträchtigt.

Betriebliche oder gesetzliche Anforderungen bilden in der Regel einen Bedarf an Dienst Isolation. Beispiel:

-   Ein Fertigungsunternehmen verfügt über eine wichtige Anwendung, die die Geräte auf dem Werks Niveau steuert. Unterbrechungen im Dienst in anderen Teilen des Netzwerks der Organisation dürfen den Betrieb des werksbodens nicht beeinträchtigen.

-   Ein Hostingunternehmen stellt den Dienst für mehrere Clients bereit. Jeder Client benötigt eine Dienst Isolation, damit jegliche Dienstunterbrechungen, die sich auf einen Client auswirken, keine Auswirkung auf die anderen Clients hat.

### <a name="service-autonomy"></a>Dienst Autonomie
Die Dienst Autonomie umfasst die Möglichkeit, die Infrastruktur zu verwalten, ohne dass exklusive Kontrolle erforderlich ist. Dies ist beispielsweise der Fall, wenn eine Gruppe Änderungen an der Infrastruktur vornehmen möchte (z. b. das Hinzufügen oder Entfernen von Domänen, das Ändern des Domain Name System (DNS)-Namespace oder das Ändern des Schemas), ohne den Gesamtstruktur Besitzer zu genehmigen.

Für eine Gruppe, die in der Lage sein soll, die Dienst Ebene AD DS zu steuern (durch Hinzufügen und Entfernen von Domänen Controllern, bei Bedarf), oder für eine Gruppe, die in der Lage sein muss, Verzeichnis aktivierte Anwendungen zu installieren, für die Schema Erweiterungen erforderlich sind.

## <a name="limited-connectivity"></a>Eingeschränkte Konnektivität
Wenn eine Gruppe in Ihrer Organisation über Netzwerke verfügt, die durch Geräte getrennt sind, die die Konnektivität zwischen Netzwerken einschränken oder beschränken (z. b. Firewalls und NAT-Geräte (Network Address Translation)), kann dies Auswirkungen auf den Gesamtstruktur Entwurf haben. Wenn Sie die Gesamtstruktur-Entwurfs Anforderungen ermitteln, achten Sie darauf, dass Sie die Speicherorte beachten, an denen Sie eine begrenzte Netzwerkverbindung haben Diese Informationen sind erforderlich, damit Sie Entscheidungen bezüglich des Gesamtstruktur Entwurfs treffen können.



