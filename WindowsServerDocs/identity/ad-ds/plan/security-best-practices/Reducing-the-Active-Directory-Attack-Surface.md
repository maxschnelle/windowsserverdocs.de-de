---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: Reduzieren der Angriffsfläche für Active Directory
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 6044c12744c29d5c13cef03c811349cfbb7d1ded
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520129"
---
# <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Abschnitt konzentriert sich auf technische Kontrollen, die implementiert werden müssen, um die Angriffsfläche der Active Directory Installation zu verringern. Der-Abschnitt enthält die folgenden Informationen:

- Bei der [Implementierung von Verwaltungs Modellen mit geringsten Rechten](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) geht es um das Risiko, dass die Verwendung von Konten mit hohen Berechtigungen für die tägliche Verwaltung und die Implementierung von Empfehlungen für die Implementierung von, um das Risiko von privilegierten Konten zu verringern.

- Die [Implementierung sicherer administrativer Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md) beschreibt die Prinzipien der Bereitstellung dedizierter, sicherer Verwaltungssysteme sowie einige Beispiel Ansätze für eine sichere administrative Host Bereitstellung.

- Das Schützen von [Domänen Controllern gegen Angriffe](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) erläutert Richtlinien und Einstellungen, die, obwohl Sie den Empfehlungen für die Implementierung sicherer administrativer Hosts ähneln, einige Domänen Controller spezifische Empfehlungen enthalten, mit denen sichergestellt werden kann, dass die Domänen Controller und die Systeme, die zur Verwaltung verwendet werden, gut geschützt sind.

## <a name="privileged-accounts-and-groups-in-active-directory"></a>Privilegierte Konten und Gruppen in Active Directory
Dieser Abschnitt enthält Hintergrundinformationen zu privilegierten Konten und Gruppen in Active Directory, die die Gemeinsamkeiten und Unterschiede zwischen privilegierten Konten und Gruppen in Active Directory erläutern sollen. Wenn Sie diese Unterschiede verstehen, ob Sie die Empfehlungen in der [Implementierung von Verwaltungs Modellen mit geringsten Rechten](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) wörtlich implementieren oder Sie für Ihre Organisation anpassen möchten, verfügen Sie über die Tools, die Sie zum sicheren schützen der einzelnen Gruppen und Konten benötigen.

### <a name="built-in-privileged-accounts-and-groups"></a>Integrierte privilegierte Konten und Gruppen
Active Directory ermöglicht die Delegierung der Verwaltung und unterstützt das Prinzip der geringsten Rechte bei der Zuweisung von Rechten und Berechtigungen. "Reguläre" Benutzer, die über Konten in einer Domäne verfügen, sind standardmäßig in der Lage, einen Großteil der im Verzeichnis gespeicherten Daten zu lesen, aber nur eine sehr begrenzte Menge von Daten im Verzeichnis ändern zu können. Benutzern, die zusätzliche Berechtigungen benötigen, kann die Mitgliedschaft in verschiedenen "privilegierten" Gruppen erteilt werden, die in das Verzeichnis integriert sind, damit Sie bestimmte Aufgaben im Zusammenhang mit ihren Rollen ausführen können, aber keine Aufgaben ausführen können, die für ihre Aufgaben nicht relevant sind. Organisationen können auch Gruppen erstellen, die auf bestimmte Auftrags Zuständigkeiten zugeschnitten sind und über differenzierte Rechte und Berechtigungen verfügen, mit denen IT-Mitarbeiter alltägliche administrative Funktionen ausführen können, ohne Rechte und Berechtigungen zu erteilen, die überschreiten, was für diese Funktionen erforderlich ist.

In Active Directory sind drei integrierte Gruppen die höchsten Berechtigungs Gruppen im Verzeichnis: Organisations-Admins, Domänen-Admins und Administratoren. Die Standardkonfiguration und-Funktionen der einzelnen Gruppen werden in den folgenden Abschnitten beschrieben:

#### <a name="highest-privilege-groups-in-active-directory"></a>Gruppen mit den höchsten Berechtigungen in Active Directory

##### <a name="enterprise-admins"></a>Organisationsadministratoren
Enterprise Admins (EA) ist eine Gruppe, die nur in der Stamm Domäne der Gesamtstruktur vorhanden ist. Sie ist standardmäßig Mitglied der Gruppe "Administratoren" in allen Domänen in der Gesamtstruktur. Das integrierte Administrator Konto in der Stamm Domäne der Gesamtstruktur ist das einzige Standard Mitglied der EA-Gruppe. EAS erhalten Rechte und Berechtigungen, die es Ihnen ermöglichen, Gesamtstruktur weite Änderungen (d. h. Änderungen, die alle Domänen in der Gesamtstruktur betreffen) zu implementieren, z. b. das Hinzufügen oder Entfernen von Domänen, das Einrichten von Gesamtstruktur-Vertrauens Stellungen oder das erhöhen In einem ordnungsgemäß entworfenen und implementierten Delegierungs Modell ist die EA-Mitgliedschaft nur erforderlich, wenn zunächst die Gesamtstruktur erstellt oder bestimmte Gesamtstruktur weite Änderungen vorgenommen werden, z. b. das Einrichten einer Gesamtstruktur-Vertrauensstellung. Die meisten Rechte und Berechtigungen, die der EA-Gruppe erteilt werden, können an Benutzer und Gruppen mit geringeren Berechtigungen delegiert werden.

##### <a name="domain-admins"></a>Domänenadministratoren

Jede Domäne in einer Gesamtstruktur verfügt über eine eigene Domänen-Admins-Gruppe, die Mitglied der Administratoren Gruppe dieser Domäne und Mitglied der lokalen Administratoren Gruppe auf allen Computern ist, die der Domäne hinzugefügt werden. Das einzige Standard Mitglied der Gruppe "da" für eine Domäne ist das integrierte Administrator Konto für diese Domäne. Das ist in ihren Domänen "All-leistenfähig", während EAS über eine Gesamtstruktur weite Berechtigung verfügt. In einem ordnungsgemäß entworfenen und implementierten Delegierungs Modell sollten Domänen-Admins nur in Szenarios mit Unterbrechung erforderlich sein (z. b. in Situationen, in denen ein Konto mit hohen Berechtigungsstufen auf jedem Computer in der Domäne erforderlich ist). Obwohl die systemeigene Active Directory Delegierungs Mechanismen die Delegierung in den Genuss der Verwendung von da-Konten nur in Notfallszenarien ermöglichen, kann das Erstellen eines effektiven Delegierungs Modells sehr zeitaufwändig sein, und viele Organisationen nutzen Tools von Drittanbietern, um den Prozess zu beschleunigen.

##### <a name="administrators"></a>Administrators
Die dritte Gruppe ist die integrierte Domänen lokale Administratoren Gruppe (BA), in der die und EAS gruppiert sind. Dieser Gruppe werden viele direkte Rechte und Berechtigungen im Verzeichnis und auf Domänen Controllern erteilt. Die Gruppe "Administratoren" für eine Domäne hat jedoch keine Berechtigungen für Mitglieds Server oder Arbeitsstationen. Dies erfolgt über die Mitgliedschaft in der lokalen Administrator Gruppe der Computer, der die Berechtigung local gewährt wird.

> [!NOTE]
> Obwohl es sich hierbei um die Standardkonfigurationen dieser privilegierten Gruppen handelt, kann ein Mitglied einer der drei Gruppen das Verzeichnis manipulieren, um die Mitgliedschaft in einer der anderen Gruppen zu erhalten. In einigen Fällen ist es trivial, eine Mitgliedschaft in den anderen Gruppen zu erhalten. in anderen Fällen ist es jedoch schwieriger, aber aus Sicht der möglichen Berechtigungen sollten alle drei Gruppen als effektiv gleichwertig betrachtet werden.

##### <a name="schema-admins"></a>Schema-Admins

Eine vierte privilegierte Gruppe, Schema-Admins (SA), ist nur in der Stamm Domäne der Gesamtstruktur vorhanden und verfügt nur über das integrierte Administrator Konto dieser Domäne als Standard Mitglied, ähnlich der Gruppe "Organisations-Admins". Die Gruppe "Schema-Admins" soll nur vorübergehend und gelegentlich aufgefüllt werden (wenn eine Änderung des AD DS Schema erforderlich ist).

Obwohl die Gruppe SA die einzige Gruppe ist, die das Active Directory Schema ändern kann (d. h., die zugrunde liegenden Datenstrukturen des Verzeichnisses, z. b. Objekte und Attribute), ist der Umfang der Rechte und Berechtigungen der SA-Gruppe stärker eingeschränkt als die zuvor beschriebenen Gruppen. Außerdem wird häufig feststellen, dass Unternehmen geeignete Verfahren für die Verwaltung der Mitgliedschaft in der SA-Gruppe entwickelt haben, da die Mitgliedschaft in der Gruppe in der Regel nur selten benötigt wird und nur für kurze Zeiträume. Dies gilt technisch gesehen auch für die Gruppen "EA", "da" und "BA" in Active Directory, aber es ist weitaus weniger üblich, dass Organisationen ähnliche Praktiken für diese Gruppen wie für die Gruppe "SA" implementiert haben.

#### <a name="protected-accounts-and-groups-in-active-directory"></a>Geschützte Konten und Gruppen in Active Directory
Innerhalb Active Directory werden ein Standardsatz privilegierter Konten und Gruppen, die als "geschützte" Konten und Gruppen bezeichnet werden, anders gesichert als andere Objekte im Verzeichnis. Alle Konten, die über eine direkte oder transitiv Mitgliedschaft in einer geschützten Gruppe verfügen (unabhängig davon, ob die Mitgliedschaft von Sicherheits-oder Verteiler Gruppen abgeleitet ist), erben diese eingeschränkte Sicherheit.


Wenn ein Benutzer beispielsweise Mitglied einer Verteiler Gruppe ist, die wiederum Mitglied einer geschützten Gruppe in Active Directory ist, wird das Benutzerobjekt als geschütztes Konto gekennzeichnet. Wenn ein Konto als geschütztes Konto gekennzeichnet ist, wird der Wert des Attributs adminCount für das Objekt auf 1 festgelegt.

> [!NOTE]
> Obwohl die transitiv Mitgliedschaft in einer geschützten Gruppe eine gruppierte Verteilung und gruppierte Sicherheitsgruppen umfasst, erhalten Konten, die Mitglieder von gruppierten Verteiler Gruppen sind, nicht die SID der geschützten Gruppe in ihren Zugriffs Token. Verteiler Gruppen können jedoch in Active Directory in Sicherheitsgruppen konvertiert werden. aus diesem Grund sind Verteiler Gruppen in der Enumeration geschützter Gruppenmitglieder enthalten. Wenn eine geschützte, gruppierte Verteiler Gruppe jemals in eine Sicherheitsgruppe konvertiert wird, erhalten die Konten, die Mitglieder der früheren Verteiler Gruppe sind, anschließend die SID der übergeordneten geschützten Gruppe in ihren Zugriffs Token bei der nächsten Anmeldung.

In der folgenden Tabelle sind die standardmäßigen geschützten Konten und Gruppen in Active Directory nach Betriebssystemversion und Service Pack Ebene aufgeführt.

**Standardmäßige geschützte Konten und Gruppen in Active Directory nach Betriebs System-und Service Pack-Version (SP)**

|**Windows 2000 <SP4**|**Windows 2000 SP4-Windows Server 2003**|**Windows Server 2003 SP1 und höher**|**Windows Server 2008-Windows Server 2012**|
|--|--|--|--|
|Administrators|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|
||Administrator|Administrator|Administrator|
||Administrators|Administrators|Administrators|
|Domänenadministratoren|Sicherungsoperatoren|Sicherungsoperatoren|Sicherungsoperatoren|
||Zertifikatherausgeber|||
||Domänenadministratoren|Domänenadministratoren|Domänenadministratoren|
|Organisationsadministratoren|Domänencontroller|Domänencontroller|Domänencontroller|
||Organisationsadministratoren|Organisationsadministratoren|Organisationsadministratoren|
||Krbtgt|Krbtgt|Krbtgt|
||Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|
||||Read-only-Domänencontroller|
||Replicator|Replicator|Replicator|
|Schema-Admins|Schema-Admins||Schema-Admins|

##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder und SDPROP
Im System Container jeder Active Directory Domäne wird automatisch ein Objekt mit dem Namen "AdminSDHolder" erstellt. Das AdminSDHolder-Objekt dient dazu, sicherzustellen, dass die Berechtigungen für geschützte Konten und Gruppen durchgängig erzwungen werden, unabhängig davon, wo sich die geschützten Gruppen und Konten in der Domäne befinden.

Alle 60 Minuten (standardmäßig) wird ein als Security Descriptor Propagator (SDProp) bezeichnetes Prozess auf dem Domänen Controller ausgeführt, der die PDC-Emulatorrolle der Domäne enthält. SDPROP vergleicht die Berechtigungen für das AdminSDHolder-Objekt der Domäne mit den Berechtigungen für die geschützten Konten und Gruppen in der Domäne. Wenn die Berechtigungen für eines der geschützten Konten und Gruppen nicht mit den Berechtigungen für das AdminSDHolder-Objekt übereinstimmen, werden die Berechtigungen für die geschützten Konten und Gruppen so zurückgesetzt, dass Sie mit denen des AdminSDHolder-Objekts der Domäne übereinstimmen.

Die Vererbung von Berechtigungen ist für geschützte Gruppen und Konten deaktiviert. Dies bedeutet, dass selbst dann, wenn die Konten oder Gruppen an verschiedene Speicherorte im Verzeichnis verschoben werden, keine Berechtigungen von ihren neuen übergeordneten Objekten geerbt werden. Die Vererbung ist auch für das AdminSDHolder-Objekt deaktiviert, sodass Berechtigungs Änderungen an den übergeordneten Objekten die Berechtigungen von AdminSDHolder nicht ändern.

> [!NOTE]
> Wenn ein Konto aus einer geschützten Gruppe entfernt wird, wird es nicht mehr als geschütztes Konto betrachtet, aber sein Attribut adminCount bleibt auf 1 festgelegt, wenn es nicht manuell geändert wird. Das Ergebnis dieser Konfiguration ist, dass die ACLs des Objekts nicht mehr von SDPROP aktualisiert werden, aber das Objekt erbt weiterhin keine Berechtigungen von seinem übergeordneten Objekt. Daher kann sich das Objekt in einer Organisationseinheit (OU) befinden, an die Berechtigungen delegiert wurden, aber das zuvor geschützte Objekt erbt diese Delegierten Berechtigungen nicht. Ein Skript zum Suchen und Zurücksetzen früherer geschützter Objekte in der Domäne finden Sie im [Microsoft-Support Artikel 817433](https://support.microsoft.com/?id=817433).

###### <a name="adminsdholder-ownership"></a>Besitz von AdminSDHolder
Die meisten Objekte in Active Directory befinden sich im Besitz der BA-Gruppe der Domäne. Das AdminSDHolder-Objekt ist jedoch standardmäßig im Besitz der-da-Gruppe der Domäne. (Dies ist eine Situation, in der das Ihre Rechte und Berechtigungen nicht über die Mitgliedschaft in der Gruppe "Administratoren" für die Domäne ableitet.)

In früheren Windows-Versionen als Windows Server 2008 können Besitzer eines Objekts die Berechtigungen des Objekts ändern. Dies schließt auch Berechtigungen ein, die Sie ursprünglich nicht haben. Daher verhindern die Standard Berechtigungen für das AdminSDHolder-Objekt einer Domäne, dass Benutzer, die Mitglied von BA-oder EA-Gruppen sind, die Berechtigungen für das AdminSDHolder-Objekt einer Domäne ändern können. Allerdings können Mitglieder der Gruppe "Administratoren" für die Domäne den Besitz des Objekts übernehmen und sich selbst zusätzliche Berechtigungen erteilen. Dies bedeutet, dass dieser Schutz rudimentär ist und nur das Objekt vor versehentlichen Änderungen durch Benutzer schützt, die keine Mitglieder der Gruppe "da" in der Domäne sind. Außerdem verfügen die Gruppen BA und EA (falls zutreffend) über die Berechtigung, die Attribute des AdminSDHolder-Objekts in der lokalen Domäne (Stamm Domäne für EA) zu ändern.

> [!NOTE]
> Ein Attribut für das AdminSDHolder-Objekt dSHeuristics ermöglicht die eingeschränkte Anpassung (Entfernung) von Gruppen, die als geschützte Gruppen angesehen werden und von AdminSDHolder und SDPROP betroffen sind. Diese Anpassung sollte in Erwägung gezogen werden, wenn Sie implementiert wird. es gibt jedoch gültige Situationen, in denen die Änderung von dSHeuristics auf AdminSDHolder nützlich ist. Weitere Informationen zum Ändern des dSHeuristics-Attributs für ein AdminSDHolder-Objekt finden Sie in den Microsoft-Support Artikeln [817433](https://support.microsoft.com/?id=817433) und [973840](https://support.microsoft.com/kb/973840)und in [Anhang C: geschützte Konten und Gruppen in Active Directory](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).

Obwohl die am meisten privilegierten Gruppen in Active Directory hier beschrieben werden, gibt es eine Reihe von anderen Gruppen, denen erhöhte Rechte gewährt wurden. Weitere Informationen zu den standardmäßigen und integrierten Gruppen in Active Directory und den jeweils zugewiesenen Benutzerrechten finden Sie unter [Anhang B: privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md).
