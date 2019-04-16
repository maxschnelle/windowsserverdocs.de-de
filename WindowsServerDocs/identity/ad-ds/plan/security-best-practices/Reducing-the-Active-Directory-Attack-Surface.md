---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: "Reduzieren der Angriffsfläche für Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: b2de254076b10a1a75d658f006c2245d523de6b7
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieser Abschnittkonzentriert sich auf technische Kontrollen zu implementieren, um die Angriffsfläche der Active Directory-Installation reduzieren. Der Abschnittenthält die folgende Informationen:  
  
-   [Implementieren von Verwaltungsmodellen der geringsten](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) geht es um das Risiko, die die Verwendung von sehr privilegierten Konten für die tägliche Verwaltung zeigt neben der Bereitstellung von Empfehlungen zum Implementieren, um das Risiko zu reduzieren, die privilegierten Konten vorhanden, zu identifizieren.  
  
-   [Implementieren sichere Administrative Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md) Prinzipien beschrieben, für die Bereitstellung von dedizierten und sichere administrative Systeme, zusätzlich zu den Beispielen in eine sichere administrative Hosts Bereitstellung nähert.  
  
-   [Sichern von Domänencontrollern vor Angriffen Domäne](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) erläutert Richtlinien und Einstellungen, die zwar ähnlich wie die Empfehlungen für die Implementierung der sichere administrative Hosts einige Domain Controller-spezifische Empfehlungen enthalten können Sie sicherstellen, dass der Domänencontroller und die Systeme verwendet, um deren Verwaltung gut gesichertes sind.  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>Privilegierte Konten und Gruppen in Active Directory  
Dieser Abschnittenthält Hintergrundinformationen zu privilegierten Konten und Gruppen in Active Directory der Commonalities und die Unterschiede zwischen der privilegierten Konten und Gruppen in Active Directory werden soll. Verstehen Sie diese Unterschiede, ob Sie implementieren, die Ratschläge in [implementieren geringsten Verwaltungsmodellen](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) wörtlich oder festlegen, dass sie für Ihre Organisation anzupassen, können Sie die Tools zum Schützen von jeder Gruppe und entsprechend berücksichtigen.  
  
### <a name="built-in-privileged-accounts-and-groups"></a>Integrierte privilegierte Konten und Gruppen  
Active Directory ermöglicht die Delegierung von Verwaltung und unterstützt das Prinzip der geringsten Rechte und Berechtigungen zuweisen. "Regular" Benutzer mit Konten in einer Domäne sind, standardmäßig, lesen Sie ähnlich wie in dem Verzeichnis gespeichert werden jedoch nur einen sehr eingeschränkten Satz von Daten in das Verzeichnis zu ändern. Benutzer, die zusätzliche Rechte benötigen können Mitgliedschaften in verschiedenen "privilegierten" Gruppen gewährt werden, die in das Verzeichnis integriert sind, sodass sie möglicherweise bestimmte Aufgaben im Zusammenhang mit ihren Rollen ausführen, aber können keine Aufgaben, die für ihre Aufgaben nicht relevant sind. Organisationen können auch Gruppen erstellen, die sind auf bestimmte Aufgaben zugeschnitten und präzise Rechte und Berechtigungen, mit denen IT-Mitarbeiter die tägliche Verwaltungsaufgaben ohne Gewähren von rechten und Berechtigungen, die für diese Funktionen erforderlich sind überschreiten gewährt werden.  
  
In Active Directory sind drei integrierte Gruppen die höchsten Berechtigung Gruppen in das Verzeichnis: Organisations-Admins, Domänen-Admins und Administratoren. Die Standardkonfiguration und Funktionen der einzelnen Gruppen werden in den folgenden Abschnitten beschrieben:  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Höchste Berechtigung Gruppen in Active Directory  
  
##### <a name="enterprise-admins"></a>Organisations-Admins  
Organisations-Admins (EA) ist eine Gruppe, die nur in der Stammdomäne der Gesamtstruktur vorhanden ist, und es wird standardmäßig ein Mitglied der Gruppe "Administratoren" in allen Domänen in der Gesamtstruktur. Das integrierte Administratorkonto in der Stammdomäne der Gesamtstruktur ist die einzige standardmäßig Mitglied der EA-Gruppe. EAs werden Rechte und Berechtigungen, mit denen sie zum Implementieren der Gesamtstruktur Änderungen (Änderungen, die alle Domänen in der Gesamtstruktur auswirken,) gewährt, z.B. hinzufügen oder Entfernen von Domänen, Einrichten von Gesamtstrukturvertrauensstellungen oder Gesamtstruktur-Funktionsebenen auslösen. In einem Delegierungsmodell ordnungsgemäß Gestaltung und Implementierung ist EA-Mitgliedschaft erforderlich, nur, wenn zuerst die Gesamtstruktur erstellen oder bestimmte Gesamtstruktur ändern z. B. eine ausgehende Gesamtstruktur-Vertrauensstellung einrichten. Die meisten Rechte und Berechtigungen der Gruppe EA können zu weniger rechten Benutzern und Gruppen delegiert werden.  
  
##### <a name="domain-admins"></a>Domänen-Admins  

Jede Domäne in einer Gesamtstruktur verfügt über eine eigene Gruppe Domänen-Admins (DA), die Mitglied der Administratorengruppe für diese Domäne und ein Mitglied der lokalen Gruppe Administratoren auf jedem Computer, der Mitglied der Domäne ist. Das einzige Standardmitglied der Gruppe DA für eine Domäne ist das integrierte Administratorkonto für diese Domäne. DAs sind EAs gesamtstrukturweite Berechtigung "all-powerful" in ihrer Domäne. In einem Delegierungsmodell ordnungsgemäß Gestaltung und Implementierung sollte Mitglied der Gruppe Domänen-Admins erforderlich nur in "break Glass" Szenarien (z.B. Situationen, in denen ein Konto mit hohen Rechten auf jedem Computer in der Domäne erforderlich ist). Obwohl systemeigene Active Directory-Delegierung Mechanismen Delegierung zulassen, wenn es möglich ist, DA Konten nur im Notfall Szenarien verwenden, erstellen eine effektive Delegierungsmodell kann zeitraubend sein und viele Organisationen nutzen Drittanbieter-Tools, um den Vorgang zu beschleunigen.  
  
##### <a name="administrators"></a>Administratoren  
Die dritte Gruppe ist die integrierte Gruppe der lokalen Domäne Administratoren (BA) in die DAs und EAs geschachtelt sind. Diese Gruppe erhält viele der direkten Rechte und Berechtigungen im Verzeichnis und auf den Domänencontrollern. Die Gruppe "Administratoren" für eine Domäne hat jedoch keine Berechtigungen auf Mitgliedsservern oder auf Arbeitsstationen. Es ist über die Mitgliedschaft in der Computer lokalen Gruppe "Administratoren", die lokalen Berechtigung gewährt wird.  
  
> [!NOTE]  
> Obwohl dies die Standardkonfiguration dieser privilegierten Gruppen sind, können Sie ein Mitglied einer der drei Gruppen das Verzeichnis, um die Mitgliedschaft in einer der anderen Gruppen erhalten bearbeiten. In einigen Fällen ist es sehr einfach zu Mitgliedschaft in der anderen Gruppen zu erhalten, während in anderen schwieriger ist, aber aus der Perspektive der potenziellen Rechte, alle drei Gruppen entspricht dürfte sein.  
  
##### <a name="schema-admins"></a>Schema-Admins  

Ein viertes privilegierten Gruppe Schema Admins (SA), nur in der Stammdomäne der Gesamtstruktur vorhanden ist und nur die Domäne integrierten Administratorkonto Standardmitglied, ähnlich wie der Gruppe "Organisations-Admins" ist. Die Gruppe "Schema-Admins" dient nur vorübergehend und gelegentlich (bei Änderung der AD DS-Schema erforderlich ist) aufgefüllt werden.  
  
Obwohl die SA-Gruppe die einzige Gruppe, die Active Directory-Schema (demnach, das Verzeichnis zugrunde liegenden Datenstrukturen wie Objekte und Attribute) ändern können ist, ist der Umfang der SA-Gruppennamens Rechte und Berechtigungen stärker eingeschränkt sind als die zuvor beschriebenen Gruppen. Es ist auch feststellen, dass Unternehmen geeignete Methoden für die Verwaltung der Mitgliedschaft der Gruppe "SA" entwickelt haben, da die Mitgliedschaft in der Gruppe in der Regel nur selten erforderlich ist, und nur für kurze Zeit üblich. Dies gilt technisch EA, DA und BA Gruppen in Active Directory, jedoch weit weniger häufig feststellen, dass Organisationen ähnliche Methoden für diese Gruppen für die Gruppe "SA" implementiert haben.  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>Geschützte Konten und Gruppen in Active Directory  
In Active Directory ein Standardsatz von privilegierten Konten und Gruppen namens "geschützte" Konten und Gruppen werden anders als andere Objekte im Verzeichnis gesichert. Jedes Konto, das direkte oder transitive Mitgliedschaft in einer geschützten Gruppe (unabhängig davon, ob die Mitgliedschaft von Sicherheits- oder Verteilergruppe Gruppen abgeleitet ist) wurde erbt diese Eingeschränkte Sicherheit.  

  
Wenn ein Benutzer Mitglied einer Verteilergruppe d.h., das wiederum wird z.B. ein Mitglied einer geschützten Gruppe in Active Directory, die User-Objekt als ein geschütztes Konto gekennzeichnet. Wenn ein Konto als ein geschütztes Konto gekennzeichnet ist, wird der Wert des Attributs AdminCount für das Objekt auf 1 festgelegt.  
  
> [!NOTE]
> Zwar transitive Mitgliedschaft in einer geschützten Gruppe geschachtelten Verteilerliste und geschachtelte Sicherheitsgruppen enthält, erhalten Konten, die Mitglieder von geschachtelten Verteilergruppen sind keine der geschützten Gruppen SID in ihrem Zugriffstoken. Verteilergruppen können jedoch zu Sicherheitsgruppen in Active Directory konvertiert werden, weshalb Verteilergruppen in geschützten Gruppe Mitglied Enumeration enthalten sind. Eine geschützte verschachtelte Verteilergruppe immer in eine Sicherheitsgruppe konvertiert werden soll, geschützt, die Konten, die Mitglieder der Verteilungspunktgruppe der ersten anschließend das übergeordnete Element empfangen werden Gruppen SID in ihrem Zugriffstoken bei der nächsten Anmeldung.  
  
Die folgende Tabelle enthält die-geschützte Standardkonten und Gruppen in Active Directory von Betriebssystem und Service Pack-Stufe.  
  
**Standard-geschützte Konten und Gruppen in Active Directory von Betriebssystem und Service Pack (SP)**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 < SP4**|**Windows2000 SP4 – Windows Server 2003**|**Windows Server 2003 SP1 oder höher**|**Windows Server 2008 – Windows Server 2012**|  
|Administratoren|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|  
||Administrator|Administrator|Administrator|  
||Administratoren|Administratoren|Administratoren|  
|Domänen-Admins|Sicherungs-Operatoren|Sicherungs-Operatoren|Sicherungs-Operatoren|  
||Zertifikatherausgeber|||  
||Domänen-Admins|Domänen-Admins|Domänen-Admins|  
|Organisations-Admins|Domänencontroller|Domänencontroller|Domänencontroller|  
||Organisations-Admins|Organisations-Admins|Organisations-Admins|  
||KRBTGT|KRBTGT|KRBTGT|  
||Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|  
||||Read-only Domain Controller|  
||Replicator|Replicator|Replicator|  
|Schema-Admins|Schema-Admins||Schema-Admins|  
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder und SDProp  
Im Systemcontainer jeder Active Directory-Domäne wird ein Objekt namens AdminSDHolder automatisch erstellt. Das AdminSDHolder-Objekt dient, stellen Sie sicher, dass die Berechtigungen für geschützte Konten und Gruppen durchgängig erzwungen werden, unabhängig davon, wo sich die geschützten Gruppen und Konten in der Domäne befinden.  

Alle 60Minuten (standardmäßig) führt genannte Sicherheitsbeschreibungspropagierer (SDProp) auf dem Domänencontroller, der der Domäne PDC-Emulatorrolle enthält. SDProp vergleicht die Berechtigungen für die Domäne AdminSDHolder-Objekt mit den Berechtigungen für die geschützte Konten und Gruppen in der Domäne. Wenn die Berechtigungen für geschützte Konten und Gruppen die Berechtigungen für das AdminSDHolder-Objekt nicht übereinstimmen, werden die Berechtigungen für die geschützte Konten und Gruppen zurückgesetzt, um die Domäne AdminSDHolder-Objekt übereinstimmen.  
  
Vererbung von Berechtigungen ist auf geschützten Gruppen und Konten, deaktiviert das bedeutet, dass auch wenn die Konten oder Gruppen an andere Standorte im Verzeichnis verschoben werden, sie Berechtigungen von ihren neuen übergeordneten Objekten nicht erben. Vererbung ist auch für das AdminSDHolder-Objekt deaktiviert, sodass Berechtigungen-Änderungen an den übergeordneten Objekten nicht die Berechtigungen des AdminSDHolder ändern.  
  
> [!NOTE]
> Wenn ein Konto aus einer geschützten Gruppe entfernt wird, ist es nicht mehr als ein geschütztes Konto, aber seine AdminCount Attribut bleibt auf 1 festgelegt, wenn sie nicht manuell geändert wird. Das Ergebnis dieser Konfiguration ist das Objekt ACLs SDProp nicht mehr aktualisiert, dass das Objekt noch nicht erbt Berechtigungen vom übergeordneten Objekt. Daher kann das Objekt in einer Organisationseinheit (OU) befinden, auf die Berechtigungen delegiert haben, aber des zuvor geschützten Objekts nicht erben diese Berechtigungen. Ein Skript zum Suchen und Zurücksetzen der zuvor geschützten Objekte in der Domäne finden Sie in der [Microsoft Support-Artikel 817433](https://support.microsoft.com/?id=817433).  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder Besitz  
Die meisten Objekte in Active Directory sind im Besitz der Domäne BA Gruppe. Allerdings, das AdminSDHolder-Objekt wird standardmäßig der Domäne DA Gruppe gehört. (Dies ist eine Situation, in dem DAs nicht ihre Rechte und Berechtigungen über die Mitgliedschaft in der Gruppe "Administratoren" für die Domäne abgeleitet sind.)  
  
In Windows-Versionen vor Windows Server2008 können Besitzer eines Objekts ändern Berechtigungen des Objekts, einschließlich selbst erteilen von Berechtigungen, die sie ursprünglich nicht verfügt. Aus diesem Grund zu verhindern, dass die Berechtigungen für eine Domäne AdminSDHolder-Objekt Mitglieder BA oder EA-Gruppen die Berechtigungen für eine Domäne AdminSDHolder-Objekt zu ändern. Allerdings können Mitglieder der Gruppe "Administratoren" für die Domäne Übernehmen des Besitzes des Objekts und selbst zusätzliche Rechte gewähren, was bedeutet, dass dieser Schutz einfache ist und nur schützt das Objekt versehentlichen Ändern von Benutzern, die nicht Mitglied der Gruppe "DA" in der Domäne sind. Darüber hinaus die BA und EA (sofern zutreffend) Gruppen über die Berechtigung zum Ändern der Attribute das AdminSDHolder-Objekt in der lokalen Domäne (Stammdomäne für EA).  
  
> [!NOTE]  
> Attribut für das AdminSDHolder-Objekt dSHeuristics, ermöglicht eine begrenzte Anpassung (Entfernung) von Gruppen, die gelten als geschützte Gruppen und von AdminSDHolder und SDProp betroffen sind. Diese Anpassung muss sorgfältig überlegt werden, wenn sie implementiert ist, es zwar gültige Situationen, in der Anpassung der dSHeuristics auf AdminSDHolder hilfreich. Weitere Informationen zur Änderung des Attributs dSHeuristics für ein Objekt AdminSDHolder finden Sie im Microsoft Support-Artikel [817433](https://support.microsoft.com/?id=817433) und [973840](https://support.microsoft.com/kb/973840), und im [AnhangC: geschützte Konten und Gruppen in Active Directory](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
Obwohl die meisten privilegierten Gruppen in Active Directory hier beschrieben werden, es gibt eine Reihe von anderen Gruppen, die erteilt wurden erweiterte Berechtigungsebene. Weitere Informationen zu allen über standardmäßige und integrierte Gruppen in Active Directory und zu den einzelnen zugewiesen wurden, finden Sie unter [AnhangB: privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md).  
  


