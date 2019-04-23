---
ms.assetid: 864ad4bc-8428-4a8b-8671-cb93b68b0c03
title: Reduzieren der Angriffsfläche für Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: d692641d316b5fe7206cc3f413bdcfc9b74675b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59874151"
---
# <a name="reducing-the-active-directory-attack-surface"></a>Reduzieren der Angriffsfläche für Active Directory

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieser Abschnitt konzentriert sich auf technische Kontrollen zu implementieren, um die Angriffsfläche der Active Directory-Installation zu verringern. Der Abschnitt enthält die folgende Informationen an:  
  
-   [Implementieren von Verwaltungsmodellen der geringsten](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) konzentriert sich auf das Risiko, die die Verwendung von weitgehende identifizieren Konten für alltägliche Verwaltungsaufgaben enthält zusätzlich zur Bereitstellung von Empfehlungen zu implementieren, um das Risiko zu reduzieren, Dieses privilegierte Konten vorhanden.  
  
-   [Implementieren sichere Administrative Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md) werden Prinzipien beschrieben, für die Bereitstellung von Systemen über die Verwaltung von dedizierten, sicheren, zusätzlich zu einigen Beispiel einer Bereitstellung von sicheren administrative Hosts erreicht.  
  
-   [Sichern von Domain Controller gegen Angriffe](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) beschreibt Richtlinien und Einstellungen, die zwar ähnlich wie die Empfehlungen für die Implementierung der sichere administrative Hosts, einige Domain Controller-spezifische Empfehlungen zum enthalten Stellen Sie sicher, dass die Domänencontroller und die Systeme verwendet, um deren Verwaltung ausreichend gesichert sind.  
  
## <a name="privileged-accounts-and-groups-in-active-directory"></a>Privilegierte Konten und Gruppen in Active Directory  
Dieser Abschnitt enthält Hintergrundinformationen zu privilegierten Konten und Gruppen in Active Directory vorgesehen, die gemeinsamkeiten und Unterschiede zwischen privilegierte Konten und Gruppen in Active Directory beschreiben. Verstehen Sie diese Unterschiede, angibt, ob Sie implementieren die Empfehlungen in [implementieren mit Minimalprivilegien Verwaltungsmodellen](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Implementing-Least-Privilege-Administrative-Models.md) wörtliche oder für Ihre Organisation anpassen möchten, stehen Ihnen die Tools Sie müssen Sichern Sie jede Gruppe bzw. ein Konto entsprechend an.  
  
### <a name="built-in-privileged-accounts-and-groups"></a>Integrierte privilegierte Konten und Gruppen  
Active Directory ermöglicht die Delegierung der Verwaltung und unterstützt das Prinzip der geringsten Rechte beim Zuweisen von rechten und Berechtigungen. "Regular" Benutzer mit Konten in einer Domäne sind, in der Standardeinstellung lesen Großteil, was im Verzeichnis gespeichert ist, aber es können nur einen sehr eingeschränkten Satz von Daten in das Verzeichnis ändern. Benutzer, die zusätzliche Berechtigungen benötigen können Mitgliedschaften in Gruppen mit verschiedenen "Berechtigungen" erteilt werden, die in das Verzeichnis erstellt werden, sodass sie möglicherweise bestimmte Aufgaben im Zusammenhang mit ihren Rollen ausführen, aber können keine Aufgaben ausführen, die für ihre Aufgaben nicht relevant sind. Organisationen können auch Gruppen erstellen, die bestimmten Auftrag Aufgaben zugeschnitten sind, und erhalten differenzierte Rechte und Berechtigungen, mit denen alltägliche administrative Funktionen auszuführen, ohne zu gewähren, Rechte und Berechtigungen, was IT-Mitarbeiter für diese Funktionen ist erforderlich.  
  
Innerhalb von Active Directory sind drei integrierte Gruppen den höchsten Berechtigungen Gruppen im Verzeichnis: Organisations-Admins "," Domänen-Admins "und" Administratoren ". Die Standardkonfiguration und die Funktionen der einzelnen Gruppen werden in den folgenden Abschnitten beschrieben:  
  
#### <a name="highest-privilege-groups-in-active-directory"></a>Höchste Berechtigung Gruppen in Active Directory  
  
##### <a name="enterprise-admins"></a>Organisations-Admins  
Enterprise-Administratoren (EA) ist eine Gruppe, die nur in der Stammdomäne der Gesamtstruktur vorhanden ist, und es wird standardmäßig ein Mitglied der Gruppe "Administratoren" in allen Domänen in der Gesamtstruktur. Das integrierte Administratorkonto in der Stammdomäne der Gesamtstruktur ist die einzige standardmäßig Mitglied der Gruppe "EA". EAs erhalten Rechte und Berechtigungen, mit denen zum Implementieren von Gesamtstruktur-Änderungen (d. h. Änderungen, die alle Domänen in der Gesamtstruktur auswirken), z. B. hinzufügen oder Entfernen von Domänen, Einrichten von Gesamtstrukturvertrauensstellungen oder Gesamtstruktur-Funktionsebenen auslösen. In einem Delegierungsmodell richtig entworfene und implementierte muss EA-Mitgliedschaft nur, wenn zunächst die Gesamtstruktur zu erstellen oder bestimmte Gesamtstruktur Änderungen, z. B. eine ausgehende Gesamtstruktur-Vertrauensstellung einrichten. Die meisten Rechte und Berechtigungen der Gruppe "EA" können weniger privilegierten Benutzern und Gruppen delegiert werden.  
  
##### <a name="domain-admins"></a>Domänen-Admins  

Jede Domäne in einer Gesamtstruktur verfügt über eine eigene Gruppe Domänen-Admins (DA), die ein Mitglied der Domäne die Gruppe "Administratoren" und ein Mitglied der lokalen Administratorengruppe auf jedem Computer, die mit der Domäne verknüpft ist. Das einzige Standardmitglied der Gruppe "Daten" für eine Domäne ist das integrierte Administratorkonto für diese Domäne. DAs sind EAs Gesamtstruktur Berechtigung "Anmeldeinformationssätze" in ihren Domänen. In einem Delegierungsmodell richtig entworfene und implementierte sollten Domänen-Admins-Mitgliedschaft werden erforderlich sind nur in "break-Glass-Szenarien (z. B. in Situationen, in denen ein Konto mit hohen Berechtigungen auf jedem Computer in der Domäne erforderlich ist). Obwohl systemeigene Active Directory-Delegierung Mechanismen Delegierung können, sofern es möglich ist, DA Konten nur in Notfällen Szenarien verwenden, erstellen ein Modell für die effektive Delegierung kann zeitaufwändig sein, und viele Organisationen nutzen Drittanbieter-Tools, um den Prozess zu beschleunigen.  
  
##### <a name="administrators"></a>Administratoren  
Die dritte Gruppe ist die integrierte Gruppe der lokalen Domäne Administratoren (BA) in der Datenzugriffsdienst- und EAs geschachtelt sind. Diese Gruppe erhält viele direkte Zugriffsrechte und Berechtigungen in das Verzeichnis, und auf einem Domänencontroller. Die Gruppe "Administratoren" für eine Domäne weist jedoch keine Berechtigungen auf Mitgliedsservern oder auf Arbeitsstationen. Es ist über die Mitgliedschaft in der Computer lokalen Gruppe Administratoren, die lokale Berechtigung gewährt wird.  
  
> [!NOTE]  
> Obwohl diese die Standardkonfigurationen dieser privilegierten Gruppen sind, kann ein Mitglied einer der drei Gruppen das Verzeichnis, um Mitglied einer der anderen Gruppen bearbeiten. In einigen Fällen ist es einfach, Mitgliedschaft in den anderen Gruppen, zu erhalten, während in anderen Fällen es schwieriger ist, aber aus der Perspektive von möglichen Berechtigungen, alle drei Gruppen entspricht angesehen werden.  
  
##### <a name="schema-admins"></a>Schema-Admins  

Eine vierte privilegierten Gruppe Schema Admins (SA), nur in der Stammdomäne der Gesamtstruktur vorhanden ist, und ist nur der Domäne des integrierten Administratorkonto als ein Standardelement, ähnlich wie die Gruppe "Unternehmensadministratoren". Die Schema-Admins-Gruppe nur vorübergehend, und gelegentlich (bei Änderung der AD DS-Schema erforderlich ist) aufgefüllt werden soll.  
  
Der Gruppe "SA" die einzige Gruppe ist, die Active Directory-Schema (d. h., das Verzeichnis des zugrunde liegenden Datenstrukturen wie z. B. Objekte und Attribute) ändern, können zwar der Rahmen der SA-Gruppennamens Rechte und Berechtigungen mehr Einschränkungen als die zuvor beschriebenen Gruppen. Es ist auch üblich, feststellen, dass Organisationen die entsprechenden Methoden für die Verwaltung der Mitgliedschaft der Gruppe "SA" entwickelt haben, da die Mitgliedschaft in der Gruppe in der Regel nur selten erforderlich ist, und nur für kurze Zeit. Dies ist technisch gesehen der EA, DA und BA Gruppen in Active Directory, ebenfalls "true", jedoch weit weniger häufig feststellen, dass Organisationen ähnliche Methoden für diese Gruppen wie bei der Gruppe "SA" implementiert haben.  
  
#### <a name="protected-accounts-and-groups-in-active-directory"></a>Geschützte Konten und Gruppen in Active Directory  
Klicken Sie innerhalb von Active Directory ein Standardsatz von privilegierten Konten und Gruppen namens "protected" Konten und Gruppen anders als andere Objekte im Verzeichnis gesichert. Jedes Konto, das direkt oder transitives Mitglied in einer geschützten Gruppe (unabhängig davon, ob die Mitgliedschaft in Sicherheits-oder Verteilergruppen abgeleitet wird) erbt diese Eingeschränkte Sicherheit.  

  
Wenn ein Benutzer ein Mitglied einer Verteilergruppe d. h., das wiederum wird z. B. ein Mitglied einer geschützten Gruppe in Active Directory, User-Objekt als geschützte Konto gekennzeichnet. Wenn ein Konto als geschützte Konto gekennzeichnet ist, wird der Wert des Attributs AdminCount für das Objekt auf 1 festgelegt.  
  
> [!NOTE]
> Zwar transitive Mitgliedschaft in einer geschützten Gruppe geschachtelten Verteilerliste und geschachtelte Sicherheitsgruppen enthält, werden der geschützten Gruppe SID von Konten, die Mitglieder von geschachtelten Verteilergruppen sind nicht in ihrem Zugriffstoken angezeigt. Verteilergruppen können jedoch zu Sicherheitsgruppen in Active Directory konvertiert werden, weshalb Verteilergruppen in geschützten Memberenumeration enthalten sind. Eine geschützte verschachtelte Verteilergruppe immer in eine Sicherheitsgruppe konvertiert werden soll, geschützt, die Konten, die Mitglieder der Verteilergruppe frühere anschließend das übergeordnete Element erhält des Gruppen-SID in ihrem Zugriffstoken bei der nächsten Anmeldung.  
  
Die folgende Tabelle enthält, der standardmäßig geschützten-Konten und Gruppen in Active Directory, Betriebssystem und Service Pack-Version.  
  
**Standardwerte für geschützte Konten und Gruppen in Active Directory vom Betriebssystem und Service Pack (SP)-Version**  
  
|||||  
|-|-|-|-|  
|**Windows 2000 <SP4**|**Windows 2000 SP4 -Windows Server 2003**|**Windows Server 2003 SP1+**|**Windows Server 2008 -Windows Server 2012**|  
|Administratoren|Konten-Operatoren|Konten-Operatoren|Konten-Operatoren|  
||Administrator|Administrator|Administrator|  
||Administratoren|Administratoren|Administratoren|  
|Domänen-Admins|Sicherungsoperatoren|Sicherungsoperatoren|Sicherungsoperatoren|  
||Zertifikatherausgeber|||  
||Domänen-Admins|Domänen-Admins|Domänen-Admins|  
|Organisations-Admins|Domänencontroller|Domänencontroller|Domänencontroller|  
||Organisations-Admins|Organisations-Admins|Organisations-Admins|  
||Krbtgt|Krbtgt|Krbtgt|  
||Druck-Operatoren|Druck-Operatoren|Druck-Operatoren|  
||||Read-only-Domänencontroller|  
||Replikations-Operator|Replikations-Operator|Replikations-Operator|  
|Schema-Admins|Schema-Admins||Schema-Admins|  
  
##### <a name="adminsdholder-and-sdprop"></a>AdminSDHolder und SDProp  
Im Systemcontainer jeder Active Directory-Domäne wird ein Objekt namens AdminSDHolder automatisch erstellt. Stellen Sie sicher, dass die Berechtigungen für geschützte Konten und Gruppen durchgängig erzwungen werden, unabhängig davon, wo sich die geschützte Gruppen und Konten in der Domäne befinden, ist der Zweck des das AdminSDHolder-Objekt werden.  

Alle 60 Minuten (standardmäßig), führt einen Prozess, der als Sicherheitsbeschreibungspropagierer (SDProp) bezeichnet, auf dem Domänencontroller, der der Domäne des PDC-Emulatorrolle enthält. SDProp vergleicht die Berechtigungen für die Domäne AdminSDHolder-Objekt mit den Berechtigungen für die geschützte Konten und Gruppen in der Domäne. Wenn die Berechtigungen für jedes geschützte Konten und Gruppen die Berechtigungen für das AdminSDHolder-Objekt nicht übereinstimmen, werden die Berechtigungen für die geschützte Konten und Gruppen zurückgesetzt, um der Domäne AdminSDHolder-Objekt übereinstimmen.  
  
Vererbung von Berechtigungen ist in geschützten Gruppen und Konten, deaktiviert das bedeutet, dass selbst wenn die Konten oder Gruppen im Verzeichnis an unterschiedliche Positionen verschoben werden, auf sie nicht von ihren neuen übergeordneten Objekten Berechtigungen erben. Vererbung ist auch für das AdminSDHolder-Objekt deaktiviert, sodass berechtigungsänderungen an den übergeordneten Objekten nicht die Berechtigungen des AdminSDHolder ändern.  
  
> [!NOTE]
> Wenn ein Konto aus einer geschützten Gruppe entfernt wird, ist es nicht mehr als ein geschütztes Konto, aber die AdminCount Attribut bleibt auf 1 festgelegt wird, wenn es nicht manuell geändert wird. Das Ergebnis dieser Konfiguration ist, dass des Objekts ACLs werden nicht mehr von SDProp aktualisiert, aber das Objekt immer noch keine Berechtigungen vom übergeordneten Objekt erbt. Aus diesem Grund kann das Objekt in einer Organisationseinheit (OU) befinden, auf die Berechtigungen delegiert wurden, aber das zuvor geschützte Objekt werden nicht an diese delegierte Berechtigungen vererbt. Ein Skript zum Suchen und Zurücksetzen von ehemals geschützte Objekte in der Domäne finden Sie in der [Microsoft Support-Artikel 817433](https://support.microsoft.com/?id=817433).  
  
###### <a name="adminsdholder-ownership"></a>AdminSDHolder Besitz  
Die meisten Objekte in Active Directory sind im Besitz der Domäne BA Gruppe. Allerdings, das AdminSDHolder-Objekt in der Standardeinstellung die Domänengruppe DA gehört. (Dies ist eine Situation, in der DAs nicht ihre Rechte und Berechtigungen über die Mitgliedschaft in der Gruppe "Administratoren" für die Domäne abgeleitet sind.)  
  
In früheren Versionen von Windows als Windows Server 2008 können Besitzer eines Objekts Berechtigungen des Objekts, einschließlich, gewähren selbst Berechtigungen, die sie ursprünglich keine ändern. Aus diesem Grund zu verhindern, dass die Standardberechtigungen für AdminSDHolder-Objekt einer Domäne Benutzer, die Mitglieder von BA oder EA-Gruppen die Berechtigungen für eine Domäne AdminSDHolder-Objekt zu ändern. Mitglied der Gruppe "Administratoren" für die Domäne können jedoch Übernehmen des Besitzes des Objekts und selbst weitere Berechtigungen gewähren, was bedeutet, dass dieser Schutz rudimentäre ist und wird nur das Objekt, für die versehentliche Änderung durch Benutzer, die geschützt keine Mitglieder der Gruppe "Daten" in der Domäne. Darüber hinaus die BA und EA (falls zutreffend) Gruppen über die Berechtigung zum Ändern der Attribute in der lokalen Domäne (Stammdomäne für EA) das AdminSDHolder-Objekt.  
  
> [!NOTE]  
> Ein Attribut für das AdminSDHolder-Objekt dSHeuristics, ermöglicht die begrenzte Anpassungen (entfernen) von Gruppen, die geschützte Gruppen gelten und AdminSDHolder und SDProp betroffen sind. Diese Anpassung sollten sorgfältig bedacht werden, wenn sie implementiert ist, allerdings gültige Situationen stehen, in denen Änderung der dSHeuristics auf AdminSDHolder nützlich ist. Weitere Informationen über die Änderung des dSHeuristics-Attributs für ein AdminSDHolder-Objekt finden Sie in den Artikeln der Microsoft-Support [817433](https://support.microsoft.com/?id=817433) und [973840](https://support.microsoft.com/kb/973840), und klicken Sie in [Anhang C: Geschützte Konten und Gruppen in Active Directory](Appendix-C--Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
Obwohl die meisten privilegierten Gruppen in Active Directory hier beschrieben werden, es gibt eine Reihe von anderen Gruppen, die gewährt wurden, erhöhte Berechtigungsebene. Weitere Informationen zu allen Standard- oder integrierte Gruppen in Active Directory und den jeweils zugewiesenen Benutzerrechte finden Sie unter [Anhang B: Privilegierte Konten und Gruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-B--Privileged-Accounts-and-Groups-in-Active-Directory.md).  
  


