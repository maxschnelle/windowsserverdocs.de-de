---
ms.assetid: 7a7ab95c-9cb3-4a7b-985a-3fc08334cf4f
title: Implementieren von Verwaltungsmodellen der geringsten Berechtigungen
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9716d442446b2705dfd2803d061cb884a5e72fbe
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="implementing-least-privilege-administrative-models"></a>Implementieren von Verwaltungsmodellen der geringsten Berechtigungen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Im folgenden Auszug aus ist [der Administrator Konten Planungshandbuch für die Sicherheit](https://technet.microsoft.com/library/cc162797.aspx), erstmals am 1. April 1999 veröffentlicht:  
  
> "Am sicherheitsbezogene Schulungskurse und Dokumentation erläutern die Implementierung einer Prinzip der geringsten Berechtigung, doch Organisationen nur selten führen Sie es. Das Prinzip ist einfach, und der Effekt des es ordnungsgemäß erheblich erhöht die Sicherheit und reduziert das Risiko. Das Prinzip besagt, dass alle Benutzer mit einem Benutzerkonto anmelden sollten, die absoluten minimalen erforderlichen Berechtigungen zum Abschließen der aktuellen Aufgabe und nichts mehr verfügt. Auf diese Weise bietet Schutz vor schädlichen Code und anderen Angriffen. Dieses Prinzip gilt für Computer und die Benutzer dieser Computer.   
> "Ein Grund dafür, dass dieses Prinzips ist, dass Sie interne Recherche gezwungen. Beispielsweise müssen Sie bestimmen, welche Zugriffsrechte, die einen Computer oder Benutzer wirklich benötigt und implementieren. Für viele Organisationen mag nachfolgend zunächst wie viel Arbeit; Es ist jedoch ein wichtiger Schritt der Netzwerkumgebung erfolgreich gesichert.   
> "Sie sollten alle Domänenbenutzer Administrator ihre Domänenberechtigungen nach dem Prinzip der geringsten Rechte gewähren. Wenn ein Administrator mit einem privilegierten Konto anmeldet und versehentlich ein Virusprogramm ausgeführt wird, erhält der Virus z. B. administrativen Zugriff auf den lokalen Computer und auf die gesamte Domäne. Der Administrator stattdessen mit einem (Nichtadministratorkonto) nicht privilegierten Konto angemeldet haben, wäre der Virus Bereich der Beschädigung nur dem lokalen Computer, da sie als Benutzer eines lokalen Computer ausgeführt wird.   
> "In einem weiteren Beispiel Konten, die Sie auf Domänenebene Administratorrechte gewähren, müssen nicht in einer anderen Gesamtstruktur erhöhten haben, auch wenn zwischen den Gesamtstrukturen eine Vertrauensstellung besteht. Diese Taktik vermieden Schäden, wenn ein Angreifer eine verwaltete Gesamtstruktur zu manipulieren. Organisationen sollten regelmäßig mit ihrem Netzwerk zum Schutz vor nicht autorisierten Ausweitung von rechten überwachen."  
  
Im folgenden Auszug aus ist der [Microsoft Windows Security Resource Kit](https://www.microsoft.com/learning/en/us/book.aspx?ID=6815&locale=en-us), erste veröffentlichte in 2005:  
  
> "Immer der Sicherheit in Bezug auf die Gewährung des geringsten Berechtigungen zum Ausführen der Aufgabe vorstellen. Wenn eine Anwendung, die zu viele Berechtigungen gefährdet werden sollte, der Angreifer möglicherweise zum Erweitern des Angriffs über Was wäre die Anwendung unter der geringsten Berechtigungen möglich war. Untersuchen Sie beispielsweise die Folgen eines Netzwerkadministrators unwissentlich öffnen e-Mail-Anlage, die einen Virus gestartet wird. Wenn der Administrator mithilfe der Domänenadministratorkontos Administratorkonto angemeldet ist, wird der Virus über Administratorrechte auf allen Computern in der Domäne verfügen und somit uneingeschränkten Zugriff auf nahezu alle Daten im Netzwerk. Wenn der Administrator angemeldet ist mit einem lokalen Administratorkonto an, der Virus über Administratorrechte auf dem lokalen Computer verfügen und somit wäre können Sie den Zugriff auf alle Daten auf dem Computer und Schadsoftware wie z. B. Protokollierung Schlüssel Strich Software auf dem Computer installieren. Wenn der Administrator mit einem normalen Benutzerkonto angemeldet ist, wird der Virus haben nur Zugriff auf Daten für den Administrator und ist nicht in der Lage, schädliche Software zu installieren. Mit den geringsten Berechtigungen zum Lesen von e-Mails, in diesem Beispiel wird das potenzielle Ausmaß der Gefährdung erheblich reduziert."  
  
## <a name="the-privilege-problem"></a>Das Problem Rechte  
In der vorherigen Auszüge beschriebenen Grundsätze wurden nicht geändert, aber bei der Beurteilung Active Directory-Installationen, finden wir einige Grundlagen zu großen Anzahl von Konten, die weit für alltägliche Aufgaben erforderlichen Berechtigungen gewährt wurden. Die Größe der Umgebung wirkt sich auf die Zahlen übermäßig privilegierten Konten ab, aber nicht auf die Verzeichnisse Proportionmidsized möglicherweise Dutzende von Konten in den meisten sehr privilegierten Gruppen, während große Installationen Hunderte oder Tausende sein können. Angreifer gelangen mit wenigen Ausnahmen unabhängig von der professionelle Fähigkeiten und Arsenal ein Angreifer, in der Regel den Weg des geringsten Widerstands. Erhöhen sie die Komplexität der Tools und Verfahren, nur wenn einfacher Mechanismen ausgefallen sind oder von führen konnten.  
  
Leider hat den Weg des geringsten Widerstands in vielen Umgebungen erwiesen viele Konten mit umfassenden und Tiefen Berechtigung. Umfassende Berechtigungen sind Rechte und Berechtigungen, die ein Konto zum Ausführen von bestimmter Aktivitäten z. B. über einen großen Querschnitt von der Umgebung zu ermöglichen, können Helpdesk-Mitarbeiter Berechtigungen gewährt werden, mit denen die Kennwörter für viele Benutzerkonten zurücksetzen können.  
  
Umfassende Rechte sind leistungsstarke Berechtigungen, die auf eine schmale Segment der Bevölkerung angewendet werden, repariert eine solche erteilen einen Techniker über Administratorrechte auf einem Server, um sie auszuführen. Umfassende Rechte weder umfassende Rechte ist unbedingt gefährlich, aber wenn viele Konten in der Domäne dauerhaft breit und umfassende Rechte gewährt werden, wenn nur eines der Konten gefährdet ist, schnell verwendet werden neu konfigurieren, die Umgebung des Angreifers Zwecke oder sogar um bei der Großteil der Infrastruktur zu zerstören.  
  
Pass-the-Hash-Angriffen, die ein Angriffstyp Credential Theft sind, sind weit verbreitete, da die Tools zu deren Ausführung frei verfügbar und leicht zu bedienende ist und vielen Umgebungen für Angriffe anfällig sind. Pass-the-Hash-Angriffe sind jedoch nicht das eigentliche Problem. Das Problem zugrunde bietet zwei Vorteile:  
  
1.  Es ist ein Angreifer auf, um umfassende Rechte auf einem einzelnen Computer zu erhalten und dann die Berechtigungen für andere Computer in der Regel einfach.  
  
2.  Es gibt in der Regel zu viele permanente Konten mit hohen Berechtigungen über die IT-Landschaft.  
  
Auch wenn die Pass-the-Hash-Angriffen eliminiert werden, verwenden Angreifer einfach verschiedene Taktiken, keine andere Strategie. Anstatt dem Anpflanzen Malware, die den Diebstahl von Anmeldeinformationen Tools enthält, können sie Anpflanzen Malware, die Tastatureingaben protokolliert oder nutzen eine beliebige Anzahl von andere Ansätze zum Erfassen von Anmeldeinformationen, die in der gesamten Umgebung leistungsstarke sind. Unabhängig von der Taktiken Ziele bleiben gleich: Konten mit umfassenden und Tiefen Berechtigung.  
  
Eine übermäßige Rechte gewähren ist nicht nur in Active Directory in gefährdeten Umgebungen gefunden. Wenn eine Organisation auch gewähren weitere Berechtigungen als nötig entwickelt wurde, ist es in der Regel innerhalb der Infrastruktur, wie in den folgenden Abschnitten beschrieben gefunden.  
  
## <a name="in-active-directory"></a>In Active Directory  
In Active Directory ist es üblich, fest, dass die Gruppen EA, DA und BA eine zu große Anzahl von Konten enthalten. In den meisten Fällen einer Organisation EA-Gruppe enthält, die nur sehr wenige Mitglieder, DA Gruppen enthalten in der Regel von der Anzahl der Benutzer in der Gruppe EA Multiplikator und Administratorgruppen enthalten in der Regel mehr Elemente als der Bevölkerung der anderen Gruppen zusammengefasst. Dies ist häufig aufgrund von dem glauben, die Administratoren aus irgendeinem Grund sind "weniger Berechtigungen" als DAs oder EAs. Während die Rechte und Berechtigungen für jede dieser Gruppen unterscheiden, sollten sie effektiv gleichermaßen leistungsstarke Gruppen betrachtet werden, da ein Mitglied einer Trick Mitglied die anderen beiden vornehmen kann.  
  
## <a name="on-member-servers"></a>Auf Mitgliedsservern  
Wenn wir die Mitgliedschaft der lokalen Administratorgruppe auf Mitgliedsservern in vielen Umgebungen abrufen, finden wir Mitgliedschaft von eine Handvoll von lokalen und Domänenkonten, bis hin zu zahlreichen verschachtelten Gruppen, die erweitert, Hunderte einzublenden, sogar Tausende von Konten mit lokalen Administratorrechten auf den Servern. In vielen Fällen sind Gruppen der Domäne mit großen Mitgliedschaften in den Mitgliedsserver lokalen Administratorgruppe, ohne Gedanken über die Tatsache geschachtelt, die jeder Benutzer, der die Mitgliedschaften der Gruppen in der Domäne ändern kann administrative Kontrolle erlangen kann, der alle Systeme, auf denen die Gruppe in einer lokalen Administratorengruppe geschachtelt ist.  
  
## <a name="on-workstations"></a>Auf Arbeitsstationen  
Obwohl Arbeitsstationen in der Regel deutlich weniger Elemente in ihrer lokalen Administratorgruppe verfügen als Mitgliedsserver ist, klicken Sie in vielen Umgebungen tun werden Benutzer Mitglied der Gruppe der lokalen Administratorgruppe auf ihren Computern gewährt. In diesem Fall auch wenn UAC aktiviert ist, stellen diese Benutzer einem erhöhten Risiko ausgesetzt, um die Integrität von ihren Arbeitsstationen.  
  
> [!IMPORTANT]  
> Sie sollten sorgfältig überlegen, ob die Benutzer müssen über Administratorrechte auf ihren Arbeitsstationen, und wenn dies der Fall, möglicherweise besser ein separates lokales Konto auf dem Computer zu erstellen, die Mitglied der Gruppe "Administratoren" ist. Wenn Benutzer für erhöhte Rechte erforderlich sind, können sie die Anmeldeinformationen des lokalen Kontos erhöhte Rechte vorhanden, aber da das Konto lokal ist, nicht verwendet werden, gefährden andere Computer oder auf Domänenressourcen zugreifen. Wie bei lokalen Konten, sollte jedoch die Anmeldeinformationen für das lokale privilegierte Konto eindeutig sein; Wenn Sie ein lokales Konto mit den gleichen Anmeldeinformationen auf mehreren Arbeitsstationen erstellen, setzen Sie die Computer Pass-the-Hash-Angriffen.  
  
## <a name="in-applications"></a>In Anwendungen  
Bei Angriffen, in denen das Ziel geistigen Eigentums der Organisation ist, können Konten, die leistungsstarken in Anwendungen Berechtigungen verwendet werden, um Exfiltration von Daten zu ermöglichen. Obwohl die Konten, die Zugriff auf sensible Daten ohne erhöhte Rechte in der Domäne oder des Betriebssystems erteilt worden sind, bietet Konten, die die Konfiguration einer Anwendung oder der Zugriff auf die Informationen der Anwendung bearbeiten können Risiko vorhanden.  
  
## <a name="in-data-repositories"></a>Daten-Repositorys  
Wie bei anderen Zielen der Fall ist, um Zugriff auf geistiges Eigentum in Form von Dokumente und andere Dateien können Angreifer die Konten, dass Steuern des Zugriffs auf die Datei gespeichert werden, Konten, die direkten Zugriff auf die Dateien, oder auch Gruppen oder Rollen, die auf die Dateien zugreifen. Wenn ein Dateiserver verwendet wird, um den Vertragsdokumente speichern und Zugriff auf die Dokumente durch die Verwendung von Active Directory-Gruppen, kann ein Angreifer, der die Mitgliedschaft der Gruppe ändern kann z. B. kompromittierte Konten zur Gruppe hinzufügen und Zugriff auf den Vertrag für Dokumente. In Fällen, in dem Zugriff auf Dokumente von Anwendungen wie z. B. SharePoint bereitgestellt wird, können Angreifer die Anwendungen abzielen, wie zuvor beschrieben.  
  
## <a name="reducing-privilege"></a>Reduzieren die Berechtigung  
Je größer und komplizierter einer Umgebung, desto schwieriger ist zum Verwalten und sichern. In kleineren Unternehmen überprüfen und reduziert die Berechtigung wurde möglicherweise eine relativ einfache Lösung, jedes zusätzlichen Server, Arbeitsstationen, Benutzerkonto und Anwendung in einer Organisation fügt jedoch ein anderes Objekt, das geschützt werden muss. Da es schwierig oder sogar unmöglich ausgeführt werden kann, Sichern Sie jeden Aspekt der Organisation IT-Infrastruktur, konzentrieren Sie Aufwand zuerst auf die Konten, deren Zugriffsrechte das größte Risiko erstellen, die in der Regel der integrierten privilegierten Konten und Gruppen in Active Directory und lokale privilegierte Konten auf Arbeitsstationen und Servern.  
  
### <a name="securing-local-administrator-accounts-on-workstations-and-member-servers"></a>Sichern von lokalen Administratorkonten auf Arbeitsstationen und Servern  
Obwohl dieses Dokument geht von Active Directory zu, wie zuvor beschrieben wurden, beginnen die meisten Angriffe auf das Verzeichnis als Angriffe auf den einzelnen Hosts. Vollständige Richtlinien für die Sicherung von lokaler Gruppen auf Member-Systemen können nicht bereitgestellt werden, aber die folgenden Empfehlungen können verwendet werden, können Sie die lokalen Administratorkonten auf Arbeitsstationen und Servern zu sichern.  
  
#### <a name="securing-local-administrator-accounts"></a>Sichern von lokalen Administratorkonten  
Für alle Versionen von Windows derzeit im grundlegenden Support enthalten wird das lokale Administratorkonto standardmäßig deaktiviert, dadurch wird das Konto für Pass-the-Hash und anderen Methoden des anmeldeinformationsdiebstahls unbrauchbar. Allerdings können in Domänen mit älteren Betriebssystemen oder in die lokalen Administratorkonten aktiviert wurden, diese Konten verwendet werden wie zuvor beschrieben Gefährdung auf Mitgliedsservern und Arbeitsstationen verteilt. Aus diesem Grund werden die folgenden Steuerelemente für alle lokalen Administratorkonten auf Domäne Angehörige Systeme empfohlen.  
  
Detaillierte Anweisungen für die Implementierung dieser Steuerelemente finden Sie unter [Anhang H: schützen lokaler Administratorkonten und-Gruppen](../../../ad-ds/plan/security-best-practices/Appendix-H--Securing-Local-Administrator-Accounts-and-Groups.md). Vor der Implementierung dieser Einstellungen, jedoch gewährleistet, dass lokale Administratorkonten zurzeit nicht verwendeten in der Umgebung zum Ausführen von Diensten auf Computern oder zum Ausführen von anderen Aktivitäten, die für die diese Konten nicht verwendet werden soll. Testen Sie diese Einstellungen sorgfältig vor der Implementierung in einer produktionsumgebung.  
  
#### <a name="controls-for-local-administrator-accounts"></a>Steuerelemente für die lokale Administratorkonten  
Integrierter Administratorkonten nie als Dienstkonten auf Mitgliedsservern verwendet werden soll, noch sollten sie auf lokalen Computern anmelden verwendet werden (außer im abgesicherten Modus zulässig ist, auch wenn das Konto deaktiviert ist). Das Ziel der Implementierung der hier beschriebenen Einstellungen ist um zu verhindern, dass lokale Administratorkonto des Computers verwendet wird, es sei denn, Kontrollmechanismen zuerst rückgängig gemacht werden. Durch diese Steuerelemente implementieren, und überwachen Administratorkonten für Änderungen, können Sie erheblich der Wahrscheinlichkeit des Erfolgs eines Angriffs, lokale Administratorkonten von Zielen reduzieren.  
  
##### <a name="configuring-gpos-to-restrict-administrator-accounts-on-domain-joined-systems"></a>Konfigurieren von Gruppenrichtlinienobjekten über Administratorkonten für die Domäne Angehörige Systeme zu beschränken  
Fügen Sie das Administratorkonto in ein oder mehrere Gruppenrichtlinienobjekte, die Sie erstellen und auf Arbeitsstationen und Server in jeder Domäne Organisationseinheiten verknüpfen, um die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  
  
-   Zugriff vom Netzwerk auf diesen Computer verweigern  
  
-   Anmelden als Batchauftrag verweigern  
  
-   Anmelden als Dienst verweigern  
  
-   Anmelden über Remotedesktopdienste verweigern  
  
Wenn Sie diese Benutzerrechte Administratorkonten hinzufügen, geben Sie, ob Sie Hinzufügen des lokalen Administratorkontos oder den Domänenadministrator Konto durch, dass Sie das Konto beschriften. Z. B. die Rechte der Domäne NWTRADERS Administratorkonto anmelden, um diese verweigert, hinzufügen, geben Sie das Konto als **NWTRADERS\Administrator**, oder suchen Sie das Administratorkonto für die Domäne NWTRADERS. Um sicherzustellen, dass Sie das lokale Administratorkonto beschränken, geben Sie **Administrator** in diesen Benutzerrechte Einstellungen im Gruppenrichtlinienobjekt-Editor.  
  
> [!NOTE]  
> Auch wenn die lokale Administratorkonten umbenannt werden, werden weiterhin die Richtlinien gelten.  
  
Diese Einstellung werden sichergestellt, dass Administratorkonto des Computers zur Verbindung mit der anderen Computern verwendet werden kann, auch wenn es versehentlich oder böswillig aktiviert ist. Lokale Anmeldung mit dem lokalen Administratorkonto kann nicht vollständig deaktiviert werden, noch sollten Sie versuchen, dafür Da lokale Administratorkonto des Computers im Notfall-Wiederherstellungsszenarien verwendet werden soll.  
  
Sollten einem Mitgliedsserver oder einer Arbeitsstation werden getrennt von der Domäne mit anderen lokalen Konten erteilt administrative Berechtigungen, der Computer im abgesicherten Modus gestartet werden kann, kann das Administratorkonto aktiviert werden und das Konto kann dann verwendet, um Reparaturen auf dem Computer wirksam. Wenn Reparaturen abgeschlossen sind, sollte das Administratorkonto wieder deaktiviert werden.  
  
### <a name="securing-local-privileged-accounts-and-groups-in-active-directory"></a>Sichern von lokalen privilegierte Konten und Gruppen in Active Directory  
*Recht Zahl sechs: ein Computer ist nur so sicher wie der Administrator vertrauenswürdig ist.* - [Zehn unveränderlichen Gesetze zur Sicherheit (Version 2.0)](https://technet.microsoft.com/security/hh278941.aspx)  
  
Die hier bereitgestellte Informationen soll allgemeine Richtlinien für das Sichern der höchsten Rechte integrierten Konten und Gruppen in Active Directory zu erhalten. Ausführliche Anleitung finden Sie außerdem [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md), [Anhang E: Schützen von Organisationsadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory.md), [Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md), und im [Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md).  
  
Bevor Sie die folgenden Einstellungen implementieren, sollten Sie auch alle Einstellungen sorgfältig durch, um festzustellen, ob sie für Ihre Umgebung geeignet sind testen. Nicht alle Organisationen werden kann diese Einstellungen implementiert.  
  
#### <a name="securing-built-in-administrator-accounts-in-active-directory"></a>Schützen integrierter Administratorkonten in Active Directory  
In jeder Domäne in Active Directory wird ein Administratorkonto im Rahmen der Erstellung der Domäne erstellt. Dieses Konto ist standardmäßig ein Mitglied der Administrator-Gruppen in der Domäne und Domänen-Admins und die Domäne der Gesamtstruktur-Stammdomäne, das Konto ist auch ein Mitglied der Gruppe "Organisations-Admins". Verwendung des lokalen Administratorkontos in einer Domäne sollten nur für Aktivitäten der ersten Erstellung und möglicherweise Notfall-Wiederherstellungsszenarien reserviert werden. Um sicherzustellen, dass eine integrierte Administratorkonto verwendet werden kann, um Reparaturen wirksam, wenn keine anderen Konten verwendet werden können, sollten Sie die Standardmitgliedschaft des Administratorkontos in einer beliebigen Domäne in der Gesamtstruktur nicht ändern. Stattdessen, Sie sollten die folgenden Richtlinien zum Schutz für das Administratorkonto in jeder Domäne in der Gesamtstruktur. Detaillierte Anweisungen für die Implementierung dieser Steuerelemente finden Sie unter [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
#### <a name="controls-for-built-in-administrator-accounts"></a>Steuerelemente für integrierter Administratorkonten  
Das Ziel der Implementierung der hier beschriebenen Einstellungen werden Administratorkonto für jede Domäne (keine Gruppe) zu verhindern, dass von verwendet werden, es sei denn, eine Reihe von Steuerelementen vertauscht sind. Diese Steuerelemente implementieren und die Administratorkonten für die Änderungen zu überwachen, können Sie die Wahrscheinlichkeit für erfolgreiche Angriffe deutlich reduzieren, durch die Nutzung von einem Domänen Administratorkonto. Für das Administratorkonto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren.  
  
##### <a name="enable-the-account-is-sensitive-and-cannot-be-delegated-flag-on-the-account"></a>Aktivieren Sie das Flag für das Konto die "Konto ist vertraulich und kann nicht delegiert werden"  
Standardmäßig können alle Konten in Active Directory delegiert werden. Delegierung ermöglicht, einen Computer oder die Anmeldeinformationen für ein Konto an, die auf dem Computer authentifiziert hat oder Diensts an andere Computer, um Dienste im Auftrag des Kontos zu erhalten. Wenn Sie aktivieren die **Konto ist vertraulich und kann nicht delegiert werden** Attribut für ein Konto domänenbasierten nicht die Anmeldeinformationen des Kontos auf andere Computer oder Dienste im Netzwerk, die Angriffe, die Delegierung beschränkt auf die Anmeldeinformationen des Kontos auf anderen Systemen verwenden nutzen gestellt werden.  
  
##### <a name="enable-the-smart-card-is-required-for-interactive-logon-flag-on-the-account"></a>Aktivieren Sie das Flag "Smartcard ist erforderlich für die interaktive Anmeldung" für das Konto  
Wenn Sie aktivieren die **Smartcard ist erforderlich für die interaktive Anmeldung** Attribut für ein Konto, Windows setzt das Kennwort des Kontos auf einen zufälligen Wert von 120 Zeichen. Durch Festlegen dieses Flag auf integrierten Administratorkonten, stellen Sie sicher, dass das Kennwort für das Konto nicht nur lang und komplex ist, aber nicht für alle Benutzer bekannt ist. Es ist nicht technisch erforderlich um Smartcards für die Konten vor der Aktivierung dieses Attribut zu erstellen, aber wenn möglich, Smartcards für jedes Konto Administrator vor der Konfiguration der Kontenbeschränkungen erstellt werden soll und Smartcards sollte an sicheren Orten gespeichert werden.  
  
Obwohl durch das Festlegen der **Smartcard ist erforderlich für die interaktive Anmeldung** Flag setzt das Kennwort des Kontos, es verhindert nicht, dass einen Benutzer mit Zugriff auf das Kennwort des Benutzerkontos über das Konto auf einen bekannten Wert festlegen und Verwenden des Kontos und neue Kennwort zum Zugriff auf Ressourcen im Netzwerk zurücksetzen. Aus diesem Grund sollten Sie die folgenden zusätzlichen Steuerelemente für das Konto implementieren.  
  
##### <a name="disable-the-account"></a>Deaktivieren Sie das Konto  
Wenn das Administratorkonto nicht deaktiviert ist, deaktivieren Sie ihn, wenn Sie die Konfiguration der Eigenschaften des Kontos abgeschlossen haben. Dadurch wird verhindert, dass das Konto für einen bestimmten Zweck verwendet wird, es sei denn, es zuerst aktiviert wird. In einem Notfallwiederherstellungsszenario, in denen keine Konten Reparaturvorgänge der AD DS-Umgebung verfügbar sind, können Sie einen Domänencontroller im abgesicherten Modus starten, melden Sie sich lokal mit dem integrierten Administratorkonto an (die lokale Anmeldung nie gesperrt ist) und der Domänen Administratorkonto, aktivieren Sie bei Bedarf.  
  
##### <a name="configuring-gpos-to-restrict-domains-administrator-accounts-on-domain-joined-systems"></a>Konfigurieren von Gruppenrichtlinienobjekten Domäne Administratorkonten auf Systemen Domäne beschränken  
Obwohl das Konto deaktivieren des Administratorkontos in einer Domäne effektiv unbrauchbar ist, sollten Sie zusätzliche Einschränkungen für das Konto implementieren, für den Fall, dass das Konto versehentlich oder böswillig aktiviert ist. Obwohl diese Steuerelemente letztendlich durch das Administratorkonto storniert werden können, Ziel ist es, Steuerelemente erstellen, die ein Angreifer Fortschritt verlangsamen und Limit die Beschädigung das Konto anrichten kann.  
  
Fügen Sie in ein oder mehrere Gruppenrichtlinienobjekte, die Sie erstellen und auf Arbeitsstationen und Server in jeder Domäne Organisationseinheiten verknüpfen, Administratorkonto für jede Domäne auf die folgenden Benutzerrechte in **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  
  
-   Zugriff vom Netzwerk auf diesen Computer verweigern  
  
-   Anmelden als Batchauftrag verweigern  
  
-   Anmelden als Dienst verweigern  
  
-   Anmelden über Remotedesktopdienste verweigern  
  
> [!NOTE]  
> Wenn Sie diese Einstellung auf lokale Administratorkonten hinzufügen, müssen Sie angeben, ob Sie lokale Administratorkonten oder Domänenadministratorkonten konfigurieren. Zum Beispiel Rechte zum Hinzufügen der Domäne NWTRADERS lokalen Administratorkonto anmelden, um diese verweigern, geben Sie entweder das Konto als **NWTRADERS\Administrator**, oder suchen Sie nach dem lokalen Administratorkonto für die Domäne NWTRADERS. Bei der Eingabe **Administrator** in den Einstellungen im Gruppenrichtlinienobjekt-Editor für diese Benutzer Rechte schränken Sie das lokale Administratorkonto auf jedem Computer, auf die das Gruppenrichtlinienobjekt angewendet wird.  
>   
> Es wird empfohlen, lokale Administratorkonten auf Mitgliedsservern und Arbeitsstationen in die gleiche Weise wie Administratorkonten domänenbasierten einschränken. Aus diesem Grund sollten Sie diese Benutzer Rechte Einstellungen in der Regel das Administratorkonto für jede Domäne in der Gesamtstruktur und das Administratorkonto für den lokalen Computer hinzufügen. Der folgende Screenshot zeigt ein Beispiel für das Blockieren von lokalen Administratorkonten und ein Domänenadministratorkonto ausführt, Anmeldungen, die für diese Konten nicht erforderlich, sollte die Benutzerrechte konfigurieren.  

>   
> ![geringsten Berechtigungen Admin-Modelle](media/Implementing-Least-Privilege-Administrative-Models/SAD_20.gif)  
  
##### <a name="configuring-gpos-to-restrict-administrator-accounts-on-domain-controllers"></a>Konfigurieren von Gruppenrichtlinienobjekten Administratorkonten auf Domänencontrollern einschränken  
In jeder Domäne in der Gesamtstruktur, die Standarddomänencontroller-Richtlinie oder eine Richtlinie, die mit der Domänencontroller-Organisationseinheit verknüpft sollte geändert werden, um die folgenden Benutzerrechte in jeder Domänenadministratorkonto hinzufügen **Computer Computerkonfiguration\Richtlinien\Windows Settings\Security Einstellungen\Sicherheitseinstellungen\Lokale Einstellungen\Benutzername\Lokale Rechte Zuweisungen**:  
  
-   Zugriff vom Netzwerk auf diesen Computer verweigern  
  
-   Anmelden als Batchauftrag verweigern  
  
-   Anmelden als Dienst verweigern  
  
-   Anmelden über Remotedesktopdienste verweigern  
  
> [!NOTE]  
> Diese Einstellung werden sichergestellt, dass das lokale Administratorkonto für die Verbindung zu einem Domänencontroller verwendet werden kann, auch wenn das Konto, wenn aktiviert, lokal auf Domänencontrollern anmelden kann. Da dieses Konto sollte nur aktiviert und im Notfall-Wiederherstellungsszenarien verwendet werden, es wird davon ausgegangen, dass die physischer Zugriff auf mindestens ein Domänencontroller verfügbar ist oder andere Konten mit Berechtigungen für den Remotezugriff auf den Domänencontrollern verwendet werden können.  
  
##### <a name="configure-auditing-of-built-in-administrator-accounts"></a>Konfigurieren Sie die Überwachung von integrierter Administratorkonten  
Wenn Sie gesicherte Administratorkonto für jede Domäne und er deaktiviert haben, sollten Sie die Überwachung zum Überwachen von Änderungen für das Konto konfigurieren. Wenn das Konto aktiviert ist, dessen Kennwort zurückgesetzt wird oder andere Änderungen werden an das Konto vorgenommen, sollten Warnungen an die Benutzer oder Teams, die für die Verwaltung von AD DS, zusätzlich zur Reaktion auf Sicherheitsvorfälle Teams in Ihrer Organisation gesendet werden.  
  
### <a name="securing-administrators-domain-admins-and-enterprise-admins-groups"></a>Sichern von Administratoren, Domänen-Admins und Organisations-Admins sein  
  
#### <a name="securing-enterprise-admin-groups"></a>Schützen von Administratorgruppen Enterprise  
Die Gruppe "Organisations-Admins", die in der Gesamtstruktur-Stammdomäne untergebracht ist, sollte keine Benutzer täglich, mit Ausnahme des lokalen Administratorkontos der Domäne enthalten, sofern er gesichert ist, wie zuvor beschrieben und in [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
EA Access erforderlich ist, sollten die Benutzer, deren Konten EA-Rechte und Berechtigungen erfordern, vorübergehend in der Gruppe "Organisations-Admins" platziert werden. Obwohl Benutzer höher privilegierten Konten verwenden, sollte ihre Aktivitäten überwacht und vorzugsweise mit einem Benutzer, die die Änderungen ausführen und ein anderer Benutzer nehmen die Änderungen zu minimieren die Wahrscheinlichkeit einer unbeabsichtigten Missbrauch oder die Fehlkonfiguration ausgeführt werden. Wenn Sie die Aktivitäten abgeschlossen haben, sollten die Konten aus der EA-Gruppe entfernt werden. Dies über manuelle Verfahren erreicht werden kann und Prozesse, Software von Drittanbieter-privileged Identity/Access Management (PIM/PAM) oder eine Kombination aus beiden dokumentiert. Richtlinien für Konten erstellen, die verwendet werden, kann die Mitgliedschaft der privilegierten Gruppen in Active Directory steuern finden Sie unter [attraktive Konten für den Diebstahl von Anmeldeinformationen](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md) und detaillierte Anweisungen finden Sie unter [Anhang I: Erstellen von Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
Organisations-Admins sind, werden standardmäßig Mitgliedern der integrierten Administratorengruppe in jeder Domäne in der Gesamtstruktur. Entfernen der Gruppe Organisations-Admins aus der Gruppe "Administratoren" in jeder Domäne wird eine falsche Änderung da im Falle einer Gesamtstruktur Disaster Recovery-Szenario EA-Rechte werden wahrscheinlich aufgefordert werden. Wenn die Gruppe "Organisations-Admins" von Administratorgruppen in einer Gesamtstruktur entfernt wurde, sollten Sie die Gruppe "Administratoren" in jeder Domäne hinzugefügt werden und die folgenden zusätzlichen Steuerelemente implementiert werden sollte:  
  
-   Wie oben beschrieben, sollte der Gruppe Organisations-Admins enthalten keine Benutzer täglich, mit Ausnahme von der Gesamtstruktur-Stammdomäne-Administratorkonto, das gesichert werden muss, wie unter [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
-   In Gruppenrichtlinienobjekten, die mit den Organisationseinheiten mit Mitgliedsservern und Arbeitsstationen in jeder Domäne verknüpft ist muss die folgenden Berechtigungen die EA-Gruppe hinzugefügt werden:  
  
    -   Zugriff vom Netzwerk auf diesen Computer verweigern  
  
    -   Anmelden als Batchauftrag verweigern  
  
    -   Anmelden als Dienst verweigern  
  
    -   Lokal anmelden verweigern  
  
    -   Verweigern Sie anmelden über Remotedesktopdienste.  
  
Dadurch wird verhindert, dass Mitglieder der Gruppe der EA Protokollierung auf Mitgliedsservern und Arbeitsstationen. Sprunglisten Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass sprungbrettservern in einer Organisationseinheit befinden, der die restriktive Gruppenrichtlinienobjekte nicht verknüpft sind.  
  
-   Überwachung sollte konfiguriert werden, um Warnungen zu senden, wenn auf die Eigenschaften oder die Mitgliedschaft der Gruppe EA Änderungen vorgenommen werden. Diese Warnungen sollten, zumindest für Benutzer oder Teams der Active Directory-Verwaltung und Incident-Antwort gesendet werden. Sie sollten auch festlegen, Prozesse und Verfahren für das Auffüllen vorübergehend der EA-Gruppe, einschließlich Benachrichtigung wie folgt vor, wenn legitime Auffüllung der Gruppe ausgeführt wird.  
  
#### <a name="securing-domain-admins-groups"></a>Schützen von Domänenadministratorgruppen  
Wie bei der Gruppe "Organisations-Admins" der Fall ist, sollten nur in Build oder Disaster Recovery-Szenarien Mitglied der Gruppe Domänen-Admins erforderlich sein. Wird keine tägliche Benutzerkonten in der Gruppe DA mit Ausnahme von dem lokalen Administratorkonto für die Domäne, wenn es gemäß gesichert wurde [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
DA der Zugriff erforderlich ist, sollte die Konten benötigen diese Zugriffsebene vorübergehend in der Gruppe DA für die betreffende Domäne platziert werden. Auch wenn der Benutzer die privilegierten Konten verwenden, sollten Aktivitäten überwacht und vorzugsweise mit einem Benutzer, die die Änderungen ausführen und ein anderer Benutzer nehmen die Änderungen zu minimieren die Wahrscheinlichkeit einer unbeabsichtigten Missbrauch oder die Fehlkonfiguration ausgeführt werden. Wenn Sie die Aktivitäten abgeschlossen haben, sollten die Konten aus der Gruppe "Domänen-Admins" entfernt werden. Dies über manuelle Verfahren erreicht werden kann und Prozesse, die über Software von Drittanbietern Identity/Systemzugriff Management (PIM/PAM), oder eine Kombination aus beiden dokumentiert. Richtlinien für Konten erstellen, die verwendet werden, kann die Mitgliedschaft der privilegierten Gruppen in Active Directory steuern finden Sie unter [Anhang I: Erstellen von Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md).  
  
Domänen-Admins sind standardmäßig Mitglieder der lokalen Administratorgruppe auf allen Servern und Arbeitsstationen in ihren jeweiligen Domänen. Diese Standardeinstellung Schachtelung sollte nicht geändert werden, da Wartungsfreundlichkeit und Disaster Recovery-Optionen betroffen sind. Wenn Gruppen Domänen-Admins aus der lokalen Administratorgruppe auf dem Mitgliedsserver entfernt wurden, sollten sie die Gruppe "Administratoren" auf jedem Mitgliedsserver und Arbeitsstationen in der Domäne über eingeschränkte Gruppe von Einstellungen in verknüpften Gruppenrichtlinienobjekten hinzugefügt werden. Die folgenden allgemeinen Steuerelemente, die in detailliert beschrieben werden [Anhang F: Schützen von Domänenadministratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-F--Securing-Domain-Admins-Groups-in-Active-Directory.md) sollten außerdem implementiert werden.  
  
Für die Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur:  
  
1.  Entfernen Sie alle Mitglieder aus der Gruppe DA mit Ausnahme des integrierten Administratorkontos für die Domäne bereitgestellten gesichert wurde gemäß [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
2.  In Gruppenrichtlinienobjekten, die mit den Organisationseinheiten mit Mitgliedsservern und Arbeitsstationen in jeder Domäne verknüpft ist sollten die DA-Gruppe die folgenden Berechtigungen hinzugefügt werden:  
  
    -   Zugriff vom Netzwerk auf diesen Computer verweigern  
  
    -   Anmelden als Batchauftrag verweigern  
  
    -   Anmelden als Dienst verweigern  
  
    -   Lokal anmelden verweigern  
  
    -   Anmelden über Remotedesktopdienste verweigern  
  
    Dadurch wird verhindert, dass Mitglieder der Gruppe der DA Protokollierung auf Mitgliedsservern und Arbeitsstationen. Sprunglisten Server zum Verwalten von Domänencontrollern und Active Directory verwendet werden, sicher, dass sprungbrettservern in einer Organisationseinheit befinden, der die restriktive Gruppenrichtlinienobjekte nicht verknüpft sind.  
  
3.  Überwachung sollte konfiguriert werden, um Warnungen zu senden, wenn auf die Eigenschaften oder die Mitgliedschaft der Gruppe DA Änderungen vorgenommen werden. Diese Warnungen sollten, zumindest für Benutzer oder Teams der AD DS-Administration und Incident-Antwort gesendet werden. Sie sollten auch festlegen, Prozesse und Verfahren für das Auffüllen vorübergehend der DA-Gruppe, einschließlich Benachrichtigung wie folgt vor, wenn legitime Auffüllung der Gruppe ausgeführt wird.  
  
#### <a name="securing-administrators-groups-in-active-directory"></a>Schützen von Administratorgruppen in Active Directory  
Wie bei den Gruppen EA und DA der Fall ist, sollten die Mitgliedschaft in der Gruppe Administratoren (BA) nur in Build oder Disaster Recovery-Szenarien erforderlich sein. Wird keine tägliche Benutzerkonten in der Gruppe "Administratoren" mit Ausnahme von dem lokalen Administratorkonto für die Domäne, wenn es gemäß gesichert wurde [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
Wenn Administratoren den Zugriff erforderlich ist, sollte die Konten benötigen diese Zugriffsebene vorübergehend in der Gruppe "Administratoren" für die betreffende Domäne platziert werden. Auch wenn der Benutzer die privilegierten Konten verwenden, sollten Aktivitäten überwacht und vorzugsweise, mit der ein Benutzer die Änderungen ausführen und ein anderer Benutzer nehmen die Änderungen zu minimieren die Wahrscheinlichkeit einer unbeabsichtigten Missbrauch oder die Fehlkonfiguration ausgeführt. Wenn Sie die Aktivitäten abgeschlossen haben, sollten die Konten umgehend aus der Gruppe "Administratoren" entfernt werden. Dies über manuelle Verfahren erreicht werden kann und Prozesse, die über Software von Drittanbietern Identity/Systemzugriff Management (PIM/PAM), oder eine Kombination aus beiden dokumentiert.  
  
Administratoren sind, werden standardmäßig die Besitzer der Großteil der AD DS-Objekte in den jeweiligen Domänen. Mitgliedschaft in dieser Gruppe kann in Build und Disaster Recovery-Szenarien erforderlich sein, in dem Besitz oder die Fähigkeit des Besitzes von Objekten erforderlich ist. Darüber hinaus erben DAs und EAs zahlreiche ihre Rechte und Berechtigungen durch ihre Standardmitgliedschaft in der Gruppe "Administratoren". Standardmäßig Schachtelung von Gruppen, für die privilegierte Gruppen in Active Directory nicht geändert werden sollte, und jede Domäne in der Gruppe "Administratoren" sollte gesichert werden, wie unter [Anhang G: Schützen von Administratorgruppen in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-G--Securing-Administrators-Groups-in-Active-Directory.md), und im Allgemeinen unten stehenden Anweisungen aus.  
  
1.  Entfernen Sie alle Mitglieder aus der Gruppe "Administratoren" mit Ausnahme des lokalen Administratorkontos für die Domäne bereitgestellten gesichert wurde gemäß [Anhang D: schützen integrierter Administratorkonten in Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  
  
2.  Mitglieder der Domäne "Administratoren" sollte nie auf Mitgliedsservern oder Arbeitsstationen anmelden müssen. In ein oder mehrere Gruppenrichtlinienobjekte mit den Arbeitsstationen und Server in jeder Domäne Organisationseinheiten verknüpft ist muss die folgenden Berechtigungen der Gruppe "Administratoren" hinzugefügt werden:  
  
    -   Zugriff vom Netzwerk auf diesen Computer verweigern  
  
    -   Verweigern Sie Anmelden als Batchauftrag,  
  
    -   Anmelden als Dienst verweigern  
  
    -   Dadurch wird verhindert, dass Mitglieder der Administratorengruppe anmelden oder verbinden auf Mitgliedsservern oder Arbeitsstationen (es sei denn, die mehrere Steuerelemente zuerst verletzt werden) verwendet wird, wobei ihre Anmeldeinformationen konnte werden zwischengespeichert und dadurch beeinträchtigt. Ein Konto mit Berechtigungen sollten nie verwendet werden, um eine weniger Berechtigungen System anmelden, und diese Kontrollen zu erzwingen, bietet Schutz gegen eine Reihe von Angriffen.  
  
3.  An die Organisationseinheit in jeder Domäne in der Gesamtstruktur, die Gruppe "Administratoren" die folgenden Benutzer erteilt werden sollten Domänencontroller Rechte (sofern sie noch nicht über diese Rechte verfügen), die die Mitglieder der Gruppe "Administratoren" für eine Gesamtstruktur Notfallwiederherstellungsszenario erforderlichen Funktionen ausführen können:  
  
    -   Auf diesen Computer vom Netzwerk aus zugreifen.  
  
    -   Lokal anmelden zulassen  
  
    -   Anmelden über Remotedesktopdienste zulassen  
  
4.  Überwachung sollte konfiguriert werden, um Warnungen zu senden, wenn Änderungen an die Eigenschaften oder Mitglied der Gruppe "Administratoren" vorgenommen werden. Diese Warnungen sollten, mindestens Mitglied des Teams für die AD DS-Verwaltung gesendet werden. Warnungen für Mitglieder des Sicherheitsteams auch gesendet werden soll, und Verfahren zum Ändern der Mitgliedschaft der Gruppe "Administratoren" definiert werden sollen. Insbesondere sollten diese Prozesse ein Verfahren enthalten, mit dem das Sicherheitsteam benachrichtigt wird, wenn die Gruppe "Administratoren" werden sollen, die geändert werden, sodass bei Warnungen gesendet werden, diese zu erwarten sind und kein Alarm ausgelöst wird. Darüber hinaus sollte die Prozesse an das Sicherheitsteam benachrichtigen, wenn die Verwendung der Gruppe "Administratoren" abgeschlossen wurde und die verwendeten Konten aus der Gruppe entfernt wurden implementiert werden.  
  
> [!NOTE]  
> Beim Implementieren von Einschränkungen für die Gruppe "Administratoren" in Gruppenrichtlinienobjekten, wendet Windows die Einstellungen auf Mitglieder der lokalen Administratorengruppe des Computers zusätzlich zu der Domäne der Gruppe "Administratoren". Sie sollten daher Vorsicht walten, beim Implementieren von Einschränkungen für die Gruppe "Administratoren". Obwohl Verbot Netzwerk "," Batch "und" Dienst-Anmeldungen für Mitglieder der Gruppe "Administratoren" wird empfohlen, wo es implementiert werden, nicht schränken Sie Lokaler Anmeldungen oder Anmeldungen über Remote Desktop Services ein. Blockieren diese Anmeldetypen können legitime Verwaltung eines Computers von Mitgliedern der lokalen Gruppe "Administratoren" blockiert werden. Der folgende Screenshot zeigt Konfigurationseinstellungen, die die blockieren unsachgemäße Verwendung des integrierten lokalen und Domäne Administratorkonten, zusätzlich zu den Missbrauch der integrierten Gruppe der lokalen oder Administratoren. Beachten Sie, dass die **anmelden über Remotedesktopdienste Verweigern** Benutzerrecht nicht der Gruppe "Administratoren" enthalten, da in dieser Einstellung Standardstylesheet auch diese Anmeldungen für Konten blockieren würde, die Mitglieder der Administratorgruppe des lokalen Computers befinden. Dienste auf Computern für die Ausführung im Kontext einer privilegierten Gruppen in diesem Abschnitt beschriebenen konfiguriert sind, kann diese Einstellungen implementieren Dienste und Anwendungen zu Fehlern führen. Aus diesem Grund sollten wie bei allen die Empfehlungen in diesem Abschnitt können Sie gründlich Einstellungen für die Anwendbarkeit in Ihrer Umgebung testen.  

>   
> ![geringsten Berechtigungen Admin-Modelle](media/Implementing-Least-Privilege-Administrative-Models/SAD_3.gif)  
  
### <a name="role-based-access-controls-rbac-for-active-directory"></a>Rollenbasierte Zugriffssteuerung (RBAC) für Active Directory  
Im Allgemeinen sind rollenbasierten Zugriffskontrolle (RBAC) einen Mechanismus zum Gruppieren von Benutzern und den Zugriff auf Ressourcen auf Grundlage von Geschäftsregeln. Im Fall von Active Directory ist das Implementieren von RBAC für AD DS erstellen Rollen auf die Rechte und Berechtigungen delegiert werden sollen, können Mitglieder der Rolle alltägliche Verwaltungsaufgaben ausführen, ohne ihnen übermäßige Rechte gewähren. RBAC für Active Directory kann entworfen und implementiert über systemeigenen Tools und Schnittstellen, durch die Nutzung von Software, die Sie bereits besitzen können durch den Erwerb von Drittanbieter-Produkten oder eine beliebige Kombination dieser Methoden. Dieser Abschnitt bietet eine schrittweise Anleitung zum Implementieren von RBAC für Active Directory, stattdessen werden jedoch Faktoren, die Sie berücksichtigen sollten, in das Auswählen eines Ansatzes für die Implementierung von RBAC in AD DS-Installationen.  
  
#### <a name="native-approaches-to-rbac-for-active-directory"></a>Systemeigene Ansätze zum RBAC für Active Directory  
Die einfachste RBAC-Implementierung können Sie implementieren Rollen wie AD DS-Gruppen und Delegieren von rechten und Berechtigungen zu den Gruppen, die tägliche Verwaltung innerhalb des angegebenen Bereichs der Rolle ausführen zu können.  
  
In einigen Fällen können vorhandene Sicherheitsgruppen in Active Directory verwendet werden, Rechte und Berechtigungen für eine Funktion zu gewähren. Z. B. wenn bestimmte Mitarbeiter in Ihrer IT-Organisation für die Verwaltung und Wartung von DNS-Zonen und Einträge verantwortlich sind, kann diese Aufgaben zu delegieren so einfach wie das Erstellen eines Kontos für jeden DNS-Administrator erstellt und der DNS-Admins in Active Directory hinzugefügt werden. Die DNS-Administratorgruppe, im Gegensatz zu mehr sehr privilegierten Gruppen weist einige leistungsstarke Rechte in Active Directory, obwohl Mitglieder dieser Gruppe zugewiesenen Berechtigungen wurden, mit denen DNS verwalten können.  
  
In anderen Fällen müssen Sie zum Erstellen von Sicherheitsgruppen und Rechte und Berechtigungen für Active Directory-Objekte, Dateisystemobjekte und Registrierungsobjekte können Mitglieder der Gruppen dafür vorgesehenen administrative Aufgaben zu delegieren. Z. B. Wenn Ihr Helpdesk-Operatoren für das Zurücksetzen von vergessener Kennwörtern verantwortlich sind, müssen zur Unterstützung von Benutzern mit Verbindungsprobleme und Problembehandlung von App-Einstellungen Sie delegierungseinstellungen für die von Benutzerobjekten in Active Directory mit Berechtigungen zu kombinieren, mit denen Benutzer beim Helpdesk auf Benutzercomputern anzeigen oder Ändern von Einstellungen für die Konfiguration der Benutzer eine Remoteverbindung herstellen. Für jede Rolle, die Sie definieren, sollten Sie Folgendes bestimmen:  
  
1.  Welche Aufgaben Mitglieder der Rolle führen täglich und welche Aufgaben nicht so häufig ausgeführt werden.  
  
2.  Auf welche Systeme und in welche Anwendungen sollten Mitglieder einer Rolle Rechte und Berechtigungen gewährt werden.  
  
3.  Welche Benutzer die Mitgliedschaft in einer Rolle gewährt werden soll.  
  
4.  Wie wird die Verwaltung von Mitgliedschaften ausgeführt.  
  
In vielen Umgebungen kann manuell erstellen rollenbasierte Zugriffssteuerung für die Verwaltung von Active Directory-Umgebung sehr aufwendig, implementieren und verwalten. Wenn Sie Rollen und Aufgaben für die Verwaltung der IT-Infrastruktur klar definiert haben, empfiehlt es sich um zusätzliche Tools, um Ihnen bei der Erstellung einer verwaltbaren einheitlichen RBAC-Bereitstellung zu nutzen. Z. B. wenn Forefront Identity Manager (FIM) in Ihrer Umgebung verwendet wird, können FIM Sie zum Automatisieren, das Erstellen und Auffüllen von Administratorrollen, die laufende Verwaltung vereinfachen können. Wenn Sie System Center Configuration Manager (SCCM) und System Center Operations Manager (SCOM) verwenden, können Sie anwendungsspezifische Rollen zum Delegieren der Verwaltung und Überwachung von Funktionen verwenden, und auch erzwingen, konsistente Konfiguration und Überwachung auf Systeme in der Domäne. Wenn Sie eine public Key-Infrastruktur (PKI) implementiert haben, können Sie ausstellen und Smartcards für IT-Mitarbeiter, die für die Verwaltung verantwortlichen der Umgebung erforderlich. Mit der Verwaltung von FIM Anmeldeinformationen (FIM CM) können Sie auch Verwaltung von Rollen und die Anmeldeinformationen für Ihre administrative Mitarbeiter kombinieren.  
  
In anderen Fällen ist es möglicherweise besser für eine Organisation, sollten die Bereitstellung von Drittanbieter-RBAC-Software, die "Out-of-Box" Funktionen bereitstellt. Für kommerzielle Zwecke, einsatzbereite (COTS)-Lösungen für RBAC für Active Directory, Windows, und nicht-Windows-Verzeichnisse und Betriebssysteme werden durch eine Reihe von Herstellern angeboten. Bei der Wahl zwischen systemeigenen Lösungen und Drittanbieter-Produkten, sollten Sie die folgenden Faktoren:  
  
1.  Budget: Investition in die Entwicklung der RBAC mithilfe von Software und Tools, mit denen, die Sie bereits besitzen können, können Sie die Softwarekosten, die beim Bereitstellen einer Lösung reduzieren. Es sei denn, Sie Mitarbeiter, die an erstellen und Bereitstellen von systemeigenen RBAC-Lösungen sind, müssen Sie jedoch möglicherweise consulting Ressourcen zum Entwickeln Ihrer Lösung zu interagieren. Sie sollten die erwarteten Kosten für eine benutzerdefinierte Lösung mit der Kosten für das Bereitstellen einer Lösung "Out-of-Box" sorgfältig abwägen, insbesondere dann, wenn Ihr Budget begrenzt ist.  
  
2.  Komposition der IT-Umgebung: Wenn Ihre Umgebung in erster Linie von Windows-Systemen besteht, oder wenn Sie bereits Active Directory für die Verwaltung von nicht-Windows-Systemen und Konten nutzen, einheitliche Lösungen können werden die optimale Lösung für Ihre Anforderungen bereitgestellt. Wenn Ihre Infrastruktur viele Systeme, die nicht Windows ausgeführt wird und nicht von Active Directory verwaltet werden enthält, müssen Sie möglicherweise Optionen für die Verwaltung von nicht-Windows-Systemen, unabhängig von der Active Directory-Umgebung berücksichtigen.  
  
3.  Modell für die Berechtigungen in der Lösung: Wenn ein Produkt stützt sich auf die Platzierung der Dienstkonten in sehr privilegierten Gruppen in Active Directory und werden nicht Angebotsoptionen, die keine übermäßige Rechte erfordern gewährt der RBAC-Software Ihre Active Directory wirklich nicht reduziert Angriff Surfaceyou nur geändert haben die Zusammensetzung der am häufigsten privilegierten Gruppen im Verzeichnis. Es sei denn, ein App-Anbieters Steuerelemente für Dienstkonten, die die Wahrscheinlichkeit, dass die Konten gefährdet und in böswilliger Absicht verwendet werden zu minimieren bereitstellen können, sollten Sie andere Optionen erwägen.  

  
### <a name="privileged-identity-management"></a>Privileged Identitätsmanagement  
Privileged Identitätsmanagement (PIM), auch bezeichnet als privilegierten Konto Management (PAM) privilegierter Anmeldeinformationen Management (PCM) wird auf der Planung, Erstellung, Implementierung von Vorgehensweisen für die Verwaltung von privilegierten Konten in Ihrer Infrastruktur. Im Allgemeinen PIM bietet Mechanismen, die mit denen Konten temporäre Zugriffsrechte erteilt werden, und beheben Sie erforderliche Berechtigungen zum Ausführen von Build oder Unterbrechung, Funktionen, anstatt die Berechtigungen für Konten dauerhaft verbunden zu verlassen. PIM-Funktionalität wird manuell erstellt oder über implementiert ist möglicherweise die Bereitstellung von Software von Drittanbietern, eine oder mehrere der folgenden Funktionen zur Verfügung:  
  

-   Anmeldeinformationen Sie "Depots,", in denen Kennwörter für privilegierte Konten sind "ausgecheckt" und ein anfängliches Kennwort zugewiesen, und dann "Einchecken" bei Aktivitäten abgeschlossen haben dabei Kennwörter erneut auf die Konten zurückgesetzt werden, von.  
  
-   Zeitgebundene Einschränkungen für die Verwendung privilegierter Anmeldeinformationen  
  
-   Anmeldeinformationen einem nur einmal verwenden  
  
-   Workflow generierten Gewährung der Berechtigung mit Überwachung und Berichterstattung von Aktivitäten und automatische Entfernen von Berechtigungen Aktivitäten abgeschlossen sind, oder vorgesehene Zeit ist abgelaufen.  
  
-   Austausch von Anmeldeinformationen hartcodiert, z. B. Benutzernamen und Kennwörter in Skripts mit Anwendungsprogrammierschnittstellen (APIs) zu ermöglichen, Anmeldeinformationen von Depots nach Bedarf abgerufen werden sollen  
  
-   Automatische Verwaltung von Anmeldeinformationen für das Dienstkonto  
  
### <a name="creating-unprivileged-accounts-to-manage-privileged-accounts"></a>Erstellen von nicht privilegierten Konten zum Verwalten von privilegierter Konten  
Eine der Herausforderungen bei der Verwaltung von privilegierten Konten besteht darin, dass in der Standardeinstellung werden die Konten, die privilegierte und geschützte Konten verwalten können und Gruppen werden privilegierte Konten geschützt. Wenn Sie die entsprechenden RBAC und PIM-Lösungen für die Active Directory-Installation implementieren, umfassen die Lösungen Ansätze, mit die Sie die Mitgliedschaft der am häufigsten privilegierten Gruppen im Verzeichnis Auffüllen von Gruppen nur vorübergehend und bei Bedarf effektiv depopulate können.  
  
Wenn Sie systemeigene RBAC und PIM implementieren, jedoch sollten Sie Konten, die keine Berechtigung und die einzige Funktion des Auffüllen und depopulating privilegierten Gruppen in Active Directory bei Bedarf erstellt. [Anhang I: Erstellen von Management-Konten für geschützte Konten und Gruppen in Active Directory](../../../ad-ds/manage/component-updates/../../../ad-ds/manage/component-updates/Appendix-I--Creating-Management-Accounts-for-Protected-Accounts-and-Groups-in-Active-Directory.md) bietet eine schrittweise Anleitung, die Sie zum Erstellen von Konten für diesen Zweck verwenden können.  
  
### <a name="implementing-robust-authentication-controls"></a>Implementieren von Unternehmensnetzwerk  
*Recht Zahl sechs: Es besteht eine Person, die es versucht, die Kennwörter zu erraten.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Pass-the-Hash und anderen Methoden des anmeldeinformationsdiebstahls werden nicht speziell für Windows-Betriebssysteme, noch sind Sie sie neu. Der erste Pass-the-Hash-Angriffs wurde 1997 erstellt. In der Vergangenheit jedoch diese Angriffe benutzerdefinierte Tools erforderlich, wurden in ihren Erfolg hit-or-miss und Angreifer haben einen relativ hohen Grad an Fähigkeiten erforderlich. Die Einführung von kostenlos, einfach zu verwendende Tools, die systemeigene Anmeldeinformationen extrahiert hat einen exponentiellen Anstieg in die Anzahl und den Erfolg der Methoden des anmeldeinformationsdiebstahls in den letzten Jahren geführt. Methoden des anmeldeinformationsdiebstahls sind jedoch nicht die einzigen Mechanismen, Anmeldeinformationen vorgesehen und gefährdet sind.  
  
Obwohl Sie Steuerelemente zum Schutz gegen Methoden des anmeldeinformationsdiebstahls implementieren sollten, sollten Sie auch identifizieren Sie die Konten in Ihrer Umgebung, die am ehesten Ziel von Angreifern sein, und Unternehmensnetzwerk-Steuerelemente für diese Konten zu implementieren. Wenn Ihre Konten mit hohen Berechtigungen einzelner Faktor-Authentifizierung, z. B. Benutzernamen und Kennwörter verwenden (beide "etwas, das Sie kennen," einen authentifizierungsfaktor handelt), werden diese Konten schwach geschützt sind. Ein Angreifer benötigt lediglich Kenntnisse über den Benutzernamen und das Kennwort des Kontos bekannt und Pass-the-Hash-Angriffe sind nicht Requiredthe Angreifer als der Benutzer auf allen Systemen authentifizieren kann, die einzelnen-Anmeldeinformationen akzeptieren.  
  
Obwohl mehrstufige Authentifizierung implementieren schützt Sie nicht vor Pass-the-Hash-Angriffen, mehrstufige Authentifizierung in Kombination mit geschützten Systeme können implementieren. Weitere Informationen zum Implementieren von geschützten Systeme finden Sie unter [Implementieren von sicheren Administrative Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md), Authentifizierungsoptionen sind in den folgenden Abschnitten beschrieben.  
  
#### <a name="general-authentication-controls"></a>Allgemeine Authentifizierung Steuerelemente  
Wenn Sie nicht bereits mehrstufigen Authentifizierung z. B. Smartcards implementiert haben, können Sie auf diese Weise. Smartcards Implementieren der Hardware erzwungene Sicherheit privater Schlüssel in ein öffentliches / privates Schlüsselpaar privaten Schlüssel eines Benutzers Zugriff auf den oder verwendet, wenn der Benutzer die richtige PIN, Kennung oder biometrischen Kennung für die Smartcard zeigt verhindern. Auch wenn die PIN eines Benutzers oder die Kennung von einem Keylogger auf einem kompromittierten Computer, für die ein Angreifer die PIN oder Kennung, wiederverwenden abgefangen wird muss die Karte auch physisch vorhanden sein.  
  
In Fällen, in denen lange, komplexe Kennwörter schwierig zu implementieren aufgrund der Benutzerseite nachgewiesen haben, bieten Smartcards einen Mechanismus, mit dem Benutzer problemlos relativ einfache PINs oder Kennungen verwenden ohne die Anmeldeinformationen anfällig für brute-Force- oder Rainbow-Table-Angriffe implementieren können. Smartcard-PINs werden nicht in Active Directory oder in der lokalen SAM-Datenbank gespeichert, obwohl anmeldeinformationshashes trotzdem in LSASS-geschützten Speicher auf Computern gespeichert werden möglicherweise auf denen Smartcards zur Authentifizierung verwendet wurden.  
  
#### <a name="additional-controls-for-vip-accounts"></a>Zusätzliche Steuerelemente für VIP-Konten  
Ein weiterer Vorteil der Implementierung von Smartcards oder anderen Mechanismen für die zertifikatbasierte Authentifizierung ist die Möglichkeit zur Nutzung von Authentifizierungsmechanismussicherung zum Schutz sensibler Daten, die für VIP-Benutzer zugegriffen werden kann. Zur Authentifizierungsmechanismussicherung finden Sie in Domänen, in denen die Funktionsebene zu Windows Server 2012 oder Windows Server 2008 R2 festgelegt ist. Wenn diese Option aktiviert ist, hinzugefügt zur Authentifizierungsmechanismussicherung eine globale Gruppe Administrator festgelegte Mitgliedschaft Kerberos-Token des Benutzers, wenn die Anmeldeinformationen des Benutzers authentifiziert werden, während der Anmeldung mit einem zertifikatbasierten Anmeldemethode.  
  
Dadurch können Administratoren die Ressource steuern den Zugriff auf Ressourcen wie Dateien, Ordner und Drucker, basierend auf, ob die Anmeldung über ein Verfahren zur zertifikatbasierten Anmeldung, zusätzlich zu den Typ des Zertifikats verwendet. Z. B. wenn ein Benutzer mit einer Smartcard anmeldet, der Benutzer den Zugriff auf Ressourcen im Netzwerk kann als angegeben werden verschiedene aus welchen der Zugriff ist, wenn der Benutzer eine Smartcard nicht verwendet (d. h., wenn der Benutzer anmeldet durch Eingabe einer Kombination aus Benutzername und Kennwort). Weitere Informationen zur Authentifizierungsmechanismussicherung finden Sie unter der [zur Authentifizierungsmechanismussicherung für AD DS in Windows Server 2008 R2-Leitfaden](https://technet.microsoft.com/library/dd378897.aspx).  
  
#### <a name="configuring-privileged-account-authentication"></a>Konfigurieren der privilegierten Konto-Authentifizierung  
In Active Directory für alle Administratorkonten, Aktivieren der **Smartcard für die interaktive Anmeldung erforderlich** -Attribut, und überwachen Sie Änderungen an (mindestens), eines der Attribute auf die **Konto** Registerkarte für das Konto (z. B. Cn, Name, sAMAccountName, UserPrincipalName und UserAccountControl) Administrator-Objekte.  
  
Obwohl durch das Festlegen der **Smartcard für die interaktive Anmeldung erforderlich** auf Konten wird zurückgesetzt, das Kennwort des Kontos auf einen zufälligen Wert von 120 Zeichen und erfordert Smartcards für die interaktive Anmeldung, das Attribut kann Benutzer mit Berechtigungen, die sie zum Ändern der Kennwörter von Konten ermöglichen dennoch überschrieben werden, und die Konten können dann verwendet werden, um nicht interaktive Anmeldungen nur mit Benutzername und Kennwort herzustellen.  
  
In anderen Fällen abhängig von der Konfigurations der Konten in Active Directory und das Zertifikat-Einstellungen in Active Directory-Zertifikatdienste (AD CS) oder ein Drittanbieter-PKI, Benutzerprinzipalname (UPN) Attribute für administrative oder VIP-Konten können für eine bestimmte Art von Angriff, bestimmt, wie hier beschrieben.  
  
##### <a name="upn-hijacking-for-certificate-spoofing"></a>UPN-Übernahme Spoofing-Zertifikat  
Obwohl eine ausführliche Beschreibung eines Angriffs auf die public Key-Infrastrukturen (PKI) außerhalb des Bereichs dieses Dokuments ist, haben Angriffe auf öffentliche und private PKIs exponentiell seit 2008 erhöht. Verstöße gegen öffentlichen PKIs Allgemein veröffentlicht wurde, aber Angriffe auf einer Organisation interne PKI sind vielleicht sogar noch konnte. Ein solcher Angriff nutzt Active Directory und Zertifikate, um ein Angreifer die Anmeldeinformationen eines anderen Konten in einer Weise zu spoofen, die schwer zu erkennen sein können.  
  
Wird ein Zertifikat für die Authentifizierung mit einem System Domäne angezeigt, wird der Inhalt der Antragsteller oder das Attribut (Subject Alternative Name, SAN) im Zertifikat verwendet, um das Zertifikat eines Benutzerobjekts in Active Directory zugeordnet. Je nach Typ des Zertifikats und wie er erstellt wird enthält der Antragsteller-Attributs in einem Zertifikat in der Regel eines Benutzers allgemeiner Name (CN), wie im folgenden Screenshot dargestellt.  
  
![geringsten Berechtigungen Admin-Modelle](media/Implementing-Least-Privilege-Administrative-Models/SAD_4.gif)  
  
Standardmäßig erstellt Active Directory eines Benutzers CN durch Verketten der Vorname des Kontos + "" + Nachname. Jedoch CN-Komponenten von Benutzerobjekten in Active Directory nicht erforderlich oder garantiert eindeutig sind, und Verschieben eines Benutzerkontos an einen anderen Speicherort in das Verzeichnis ändert das Konto definierter Name (DN), der den vollständigen Pfad zu dem Objekt in das Verzeichnis, wie im unteren Bereich des vorherigen Screenshot gezeigt.  
  
Da Antragstellernamen des Zertifikats nicht statische oder eindeutig sein garantiert werden, den Inhalt des alternativen Antragstellernamen häufig werden die User-Objekt in Active Directory gefunden. Das SAN-Attribut für Benutzer von Enterprise-Zertifizierungsstellen ausgestellten Zertifikate (Active Directory integrierte CAs) in der Regel UPN oder e-Mail-Adresse des Benutzers enthält. Da UPNs in einer AD DS-Gesamtstruktur eindeutig sein garantiert, wird das Suchen nach einem Objekt vom UPN im Rahmen der Authentifizierung, mit oder ohne Zertifikate, die bei der Authentifizierung beteiligten häufig ausgeführt.  
  
Die Verwendung von UPNs im SAN-Attribute in Clientauthentifizierungszertifikate kann von Angreifern abrufen gefälschter Zertifikate genutzt werden. Ein Angreifer ein kompromittiertes Konto hat, das die Möglichkeit zum Lesen und Schreiben von UPNs von Benutzerobjekten verfügt, ist der Angriff folgendermaßen implementiert:  
  
Das UPN-Attribut für eine User-Objekt (z. B. eine VIP-Benutzer) wird vorübergehend auf einen anderen Wert geändert. Die SAM-Kontonamenattribut und CN kann auch zu diesem Zeitpunkt geändert werden, obwohl dies in der Regel nicht weiter oben beschriebenen Gründen erforderlich ist.  
  
Wenn die UPN-Attribut für das Zielkonto geändert wurde, wird ein veralteter, aktiviertes Benutzerkonto oder eine neu erstellte Benutzerkonto UPN-Attribut auf den Wert geändert, die ursprünglich zum Zielkonto zugewiesen wurde. Veraltete aktivierte Benutzerkonten sind Konten, die nicht für einen längeren Zeitraum angemeldet haben, aber nicht deaktiviert wurden. Sie werden als Ziel von Angreifern verwendet, die beabsichtigen, "einfache wie den folgenden Gründen"ausblenden":  
  
1.  Da das Konto aktiviert ist, aber noch nicht verwendet wurden, ist mit dem Konto unwahrscheinlich Trigger Warnungen die Möglichkeit, die ein deaktiviertes Benutzerkonto aktivieren kann.  
  
2.  Ein vorhandenes Konto erforderlich nicht das Erstellen eines neuen Benutzerkontos, die durch administrative Mitarbeiter festgestellt werden kann.  
  
3.  Veraltete Benutzerkonten, die weiterhin aktiviert sind in der Regel Mitglieder der verschiedenen Sicherheitsgruppen und Zugriff auf Ressourcen im Netzwerk, einfacheren Zugriff und "Überblenden" um eine Anzahl von vorhandenen Benutzern gewährt werden.  
  
Das Benutzerkonto, das auf dem Ziel UPN nun konfiguriert wurde wird verwendet, eine oder mehrere Zertifikate von Active Directory-Zertifikatdienste anfordern.  
  
Wenn Zertifikate für das Konto des Angreifers abgerufen wurden, werden die UPNs auf das Konto "neue" und das Zielkonto auf ihre ursprünglichen Werte zurückgegeben.  
  
Der Angreifer verfügt nun über ein oder mehrere Zertifikate, die für die Authentifizierung auf Ressourcen und Anwendungen angegeben werden können, als ob der Benutzer die VIP-Benutzer ist, dessen Konto vorübergehend geändert wurde. Obwohl ausführliche Informationen zu allen Optionen, in denen Zertifikate und PKI von Angreifern Ziel, würde den Rahmen dieses Dokuments ist, wird dieser Angriffs Mechanismus bereitgestellt, um veranschaulichen, warum Sie privilegierten und VIP-Konten für Änderungen, insbesondere für Änderungen von Attributen in AD DS auf überwacht sollten die **Konto** Registerkarte für das Konto (z. b. Cn, Name, sAMAccountName, UserPrincipalName und UserAccountControl). Zusätzlich zur Überwachung der Konten, sollten Sie einschränken, den Konten an, als klein eine Reihe von Administratoren wie möglich geändert werden kann. Entsprechend sollten die Konten von Administratoren geschützt und nicht autorisierte Änderungen überwacht werden.  
  


