---
title: Windows-Authentifizierungskonzepte
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 29d1db15-cae0-4e3d-9d8e-241ac206bb8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ee3fa19efa8c5098008749a467e649edcb5bb716
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876501"
---
# <a name="windows-authentication-concepts"></a>Windows-Authentifizierungskonzepte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Diese Referenzübersicht in diesem Thema wird beschrieben, die Konzepte, die auf denen Windows-Authentifizierung basiert.

Authentifizierung ist der Vorgang, durch den die Identität eines Objekts oder einer Person überprüft wird. Ziel der Authentifizierung eines Objekts ist es, sicherzustellen, dass das Objekt echt und unverfälscht ist. Wenn Sie eine Person authentifizieren, ist das Ziel, um sicherzustellen, dass die Person nicht über ein Eindringling ist.

Im Netzwerkkontext dient die Authentifizierung dazu, die Identität gegenüber einer Netzwerkanwendung oder -ressource nachzuweisen. Identität ist in der Regel durch einen kryptografischen Vorgang nachgewiesen, verwendet, die entweder ein Schlüssel nur für den Benutzer (wie bei Verschlüsselung mit öffentlichem Schlüssel) bekannt sind oder ein vorinstallierter Schlüssel. Auf der Serverseite der Authentifizierungskommunikation werden die signierten Daten mit einem bekannten Kryptografieschlüssel verglichen, um den Authentifizierungsversuch zu überprüfen.

Durch die Speicherung der Kryptografieschlüssel an einem zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory ist die empfohlene und standardmäßig verwendete Technologie für das Speichern von Identitätsinformationen, darunter die kryptografischen Schlüsseln, werden die Anmeldeinformationen des Benutzers. Active Directory ist für Standardimplementierungen von Kerberos und NTLM erforderlich.

Authentifizierungstechniken reichen von der einfachen Anmeldung, um ein Betriebssystem oder eine Anmeldung beim Dienst oder Anwendung, die basierend auf etwas, das nur der Benutzer, z. B. ein Kennwort zu leistungsfähigeren Sicherheitsmechanismen weiß, mit denen ein Benutzer identifiziert, der Benutzer has'such als Token, Zertifikate mit öffentlichen Schlüsseln, Bilder oder biologischen Attribute. In einer Unternehmensumgebung ist es Benutzer eventuell möglich, auf unterschiedliche Anwendungen auf verschiedenen Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesem Grund muss die Authentifizierung Umgebungen unterstützen, die auf anderen Plattformen und anderen Windows-Betriebssystemen basieren.

## <a name="authentication-and-authorization-a-travel-analogy"></a>Authentifizierung und Autorisierung: Eine Analogie Reisen
Eine Analogie Travel können Erläutern der Funktionsweise der Authentifizierung. Einige vorbereitende Aufgaben sind in der Regel erforderlich, auf dem Weg zu beginnen. Die mobilen muss die echte Identität auf ihren Host Behörden nachweisen. Dieser Beleg kann sein, in Form von Machbarkeitsstudien Citizenship, Geburtsort, einer persönlichen Gutschein, Fotos, oder was auch immer die Gesetze des Landes, Host erforderlich ist. Die mobilen die Identität wird durch die Ausstellung von einer Passport, überprüft, analog zu einem Systemkonto ausgestellt und von einer Organisation – der Sicherheitsprinzipal verwaltet wird. Das Passport-Konto und das beabsichtigte Ziel basieren auf einem Satz von Regeln und Bestimmungen, die von der Regierungsstelle ausgegeben.

**Die Reise**

Wenn die mobilen an der internationalen Grenze eingeht, ein Border-Wächter fordert zur Eingabe von Anmeldeinformationen und der mobilen stellt seine Passport. Der Prozess umfasst zwei Stufen:

-   Der Wächter authentifiziert das Passport-Konto an, überprüfen Sie, dass es eine Sicherheitsinstanz ausgestellt wurde, dass der örtliche Behörden (Vertrauensstellungen, zumindest um, Pässen ausgeben) vertraut, und überprüfen Sie, dass das Passport-Konto nicht geändert wurde.

-   Der Wächter authentifiziert der mobilen überprüfen, ob das Gesicht das Gesicht von Person abgebildet, auf der Passport entspricht und anderen erforderlichen Anmeldeinformationen in einem Zustand sind.

Wenn die Passport erweist sich als gültig ist, und die mobilen beweist, dessen Besitzer, Authentifizierung erfolgreich ist, und die mobilen kann Zugriff auf den Rahmen.

Transitive Vertrauensstellung zwischen den Sicherheitsbehörden ist die Grundlage für die Authentifizierung. Der Typ der Authentifizierung, die an eine internationale Grenze stattfindet basiert auf Vertrauenswürdigkeit. Der örtliche Behörden weiß nicht, den mobilen, aber es vertraut, dass die Host-Regierung festgelegt wurde. Wenn die Host-Regierung, die Passport ausgegeben, wussten es den mobilen entweder nicht. Es als vertrauenswürdig eingestuft, die Agentur, die die Geburtsurkunde oder andere Dokumentation ausgegeben. Die Agentur, die das Geburtsdatum Zertifikat ausgestellt hat, vertrauenswürdige wiederum der Arzt, die das Zertifikat signiert. Der Arzt bestätigt die mobilen des Geburtsdatum und versehen das Zertifikat mit dem direkten Nachweis der Identität des in diesem Fall mit der neugeborenen der Speicherbedarf. Vertrauensstellung, die auf diese Weise über vertrauenswürdigen Vermittler, übertragen werden, ist transitiv.

Transitive Vertrauensstellung ist die Grundlage für die Netzwerksicherheit in Windows-Client/Server-Architektur. Eine Vertrauensstellung Datenflüsse im gesamten einen Satz von Domänen, z. B. eine Struktur von Domäne, und stellt eine Beziehung zwischen einer Domäne und alle Domänen, die diese Domäne vertrauen. Z. B. vertraut wenn Domäne A eine transitive Vertrauensstellung mit Domäne B hat, und Domäne B Domäne C vertraut, dann Domäne A Domäne C.

Es gibt ein Unterschied zwischen Authentifizierung und Autorisierung. Bei der Authentifizierung beweist das System an, dass Sie sind, wer Sie vorgeben, dass Sie sind. Mit Autorisierung überprüft das System an, dass Sie über die Rechte zu tun, was Sie tun möchten. Um die Rahmen Analogie mit dem nächsten Schritt zu erstellen, ist lediglich authentifizieren, dass die mobilen den entsprechenden Besitzer einen gültigen Passport ist nicht unbedingt der mobilen zur Eingabe eines Landes autorisieren. Geben durch die Bereitstellung einfach ein Passport-Konto nur in Situationen, in dem das Land, die eingegeben wird unbegrenzt die Berechtigung für alle Bürger dieses bestimmten Landes zur geben erteilt, in einem anderen Land Bürger eines bestimmten Landes dürfen.

Auf ähnliche Weise können Sie alle Benutzer eine bestimmte Domänenberechtigungen für den Zugriff auf eine Ressource gewähren. Jeder Benutzer, die für diese Domäne gehört hat Zugriff auf die Ressource an, wie Kanada US-Bürger Kanada eingeben kann. Finden jedoch US-Bürger Brasilien oder Indien eingeben möchten, die sie keine Länder eingeben, indem Sie einen Passport darstellen, da beide dieser Länder Zugriff auf US-Bürger erfordern, um eine gültige Visa. Authentifizierung garantiert daher nicht den Zugriff auf Ressourcen oder Autorisierung, Ressourcen zu verwenden.

## <a name="credentials"></a>Anmeldeinformationen
Ein Passport-Konto und möglicherweise zugeordneten Visa sind die zulässigen Anmeldeinformationen für einen mobilen. Allerdings können diese Anmeldeinformationen können keinen mobilen eingeben oder den Zugriff auf alle Ressourcen innerhalb eines Landes. Beispielsweise sind zusätzliche Anmeldeinformationen erforderlich, auf einer Konferenz. In Windows können Anmeldeinformationen verwaltet werden, um Kontoinhabern um Ressourcen über das Netzwerk zugreifen, ohne wiederholt die Anmeldeinformationen zu erleichtern. Diese Art von Zugriff ermöglicht Benutzern, die einmal durch das System den Zugriff auf alle Anwendungen authentifiziert werden und für Datenquellen, dass sie berechtigt sind, ohne Eingabe einer anderen Konto-ID oder Kennwort verwenden. Die Windows-Plattform nutzt die Fähigkeit, eine einzelne Benutzeridentität (verwaltet von Active Directory) über das Netzwerk lokal im Zwischenspeicher Benutzeranmeldeinformationen in das Betriebssystem Local Security Authority (LSA) zu verwenden. Wenn ein Benutzer der Domäne anmeldet, verwenden Sie Pakete für Windows-Authentifizierung die Anmeldeinformationen transparent einmaliges Anmelden bereitstellen, bei der Authentifizierung der Anmeldeinformationen auf Netzwerkressourcen. Weitere Informationen zu Anmeldeinformationen finden Sie unter [Anmeldeinformationen-Prozesse bei der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md).

Eine Form der Multi-Factor Authentication für die mobilen möglicherweise die Anforderung zum tragen, und stellen mehrere Dokumente, um seine Identität wie z. B. eine Passport-Konto und die Konferenz-Registrierungsinformationen zu authentifizieren. Windows wird dieses Formular oder die Authentifizierung mit Smartcards, virtuellen Smartcards und biometrischen Technologien implementiert. 

## <a name="security-principals-and-accounts"></a>Die Sicherheitsprinzipale und Konten
In Windows ist jeder Benutzer, Dienst, Gruppe oder Computer, die Aktion initiieren kann ein Sicherheitsprinzipal. Sicherheitsprinzipale müssen Konten, die Domäne basieren oder werden lokal auf einem Computer ausführen können. Z. B. können Domäne eingebundenen Windows-Clientcomputern teilnehmen einer Netzwerkdomäne durch Kommunikation mit einem Domänencontroller, selbst wenn kein Benutzer angemeldet ist. Um die Kommunikation initiieren können, muss der Computer ein aktives Konto in der Domäne sein. Vor dem akzeptieren die Kommunikation auf dem Computer, auf dem Domänencontroller die lokalen Sicherheitsinstanz authentifiziert die Computeridentität und definiert dann Sicherheitskontext des Computers aus, genau wie für einen menschlichen Sicherheitsprinzipal. Dieser Sicherheitskontext definiert die Identität und die Funktionen von einem Benutzer oder Dienst auf einem bestimmten Computer oder Benutzer, Dienste, Gruppe, oder Computer in einem Netzwerk. Es definiert z. B. die Ressourcen, z. B. eine Dateifreigabe oder Drucker, das zugegriffen werden kann und die Aktionen, z. B. Lese-, Schreib- oder ändern, die von einem Benutzer, der Dienst oder der Computer, auf die Ressource ausgeführt werden können. Weitere Informationen finden Sie unter [Sicherheitsprinzipale](https://technet.microsoft.com/itpro/windows/keep-secure/security-principals).

Ein Konto ist eine Möglichkeit zur Identifizierung des Antragstellers – die Benutzer oder den Dienst – anfordert, Zugriff oder Ressourcen. Die mobilen, die die Authentizität Passport enthält verfügt über ein Konto mit dem Host Land. Benutzer, Gruppen von Benutzern, Objekten und -Dienste alle können einzelne Konten oder Konten freigeben. Konten können Mitglied der Gruppen und bestimmte Rechte und Berechtigungen zugewiesen werden können. Konten können auf dem lokalen Computer, Workgroup, Netzwerk beschränkt sein oder Mitglied einer Domäne zugewiesen werden.

Für jede Version von Windows sind integrierte Konten und die Sicherheitsgruppen, von denen sie Mitglieder sind definiert. Mithilfe von Sicherheitsgruppen können Sie zuweisen die gleichen Sicherheitsberechtigungen für viele Benutzer erfolgreich authentifiziert wurden, das Verwaltung vereinfacht. Regeln für das Ausstellen von Pässen möglicherweise, dass die mobilen zu bestimmten Gruppen, z. B. Business Sport- oder Government zugewiesen werden. Dadurch wird sichergestellt konsistente Codezugriffssicherheits-Berechtigungen für alle Mitglieder einer Gruppe. Mithilfe von Sicherheitsgruppen zum Zuweisen von Berechtigungen bleibt bedeutet, die Kontrolle über Ressourcen zugreifen, Konstanten und leicht zu verwalten und überwachen. Hinzufügen und Entfernen von Benutzern, die Zugriff auf den entsprechenden Sicherheitsgruppen benötigen je nach Bedarf, können Sie die Häufigkeit von Änderungen an Zugriffssteuerungslisten (ACLs) verringern.

Eigenständige verwaltete Dienstkonten und virtuelle Konten wurden eingeführt, in Windows Server 2008 R2 und Windows 7, für die Isolierung der eigenen Domäne erforderlichen Anwendungen, z. B. Microsoft Exchange Server und Internet Information Services (IIS) bereit Konten, sodass die Notwendigkeit von Administrator den Dienstprinzipalnamen (SPN) manuell zu verwalten und die Anmeldeinformationen für diese Konten. Gruppenverwaltete Dienstkonten in Windows Server 2012 eingeführt wurden und bietet die gleiche Funktionalität innerhalb der Domäne, aber erweitert diese Funktion auch über mehrere Server. Beim Herstellen einer Verbindung mit einem Dienst, der in einer Serverfarm gehostet wird (beispielsweise ein Netzwerklastenausgleich), erfordern die Authentifizierungsprotokolle mit gegenseitiger Authentifizierung, dass alle Instanzen der Dienste den gleichen Prinzipal verwenden.

Weitere Informationen zu Konten finden Sie unter:

-   [Active Directory-Konten](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-accounts)

-   [Active Directory-Sicherheitsgruppen](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-security-groups)

-   [Lokale Konten](https://technet.microsoft.com/itpro/windows/keep-bastion.local-accounts)

-   [Microsoft-Konten](https://technet.microsoft.com/itpro/windows/keep-secure/microsoft-accounts)

-   [Dienstkonten](https://technet.microsoft.com/itpro/windows/keep-secure/service-accounts)

-   [Besondere Identitäten](https://technet.microsoft.com/itpro/windows/keep-secure/special-identities)

## <a name="delegated-authentication"></a>Delegierte Authentifizierung
Um die Reise Analogie zu verwenden, möglicherweise Länder den gleichen Zugriff auf alle Elemente einer offiziellen behördlichen Delegierung ausgeben, solange die Delegaten bekannt sind. Diese Delegierung können einen Member, die die Autorität für die eines anderen Elements handeln. In Windows tritt ein, delegierte Authentifizierung, wenn ein Netzwerkdienst eine Authentifizierungsanforderung von einem Benutzer akzeptiert und geht von der Identität eines Benutzers, um eine neue Verbindung mit einem zweiten Netzwerkdienst zu initiieren. Um delegierte Authentifizierung zu unterstützen, müssen Sie einrichten, Servern, Front-End- oder der ersten Ebene, z.B. Webserver, die für die Behandlung von Clientanforderungen für die Authentifizierung verantwortlich sind und Back-End- oder n-Tier-Server, z. B. sehr große Datenbanken, die für die zuständig sind Speichern von Informationen aus. Sie können das Recht, delegierte Authentifizierung für Benutzer in Ihrer Organisation einrichten, um die administrative Last für Ihre Administratoren verringert delegieren.

Durch die Einrichtung von einem Dienst oder Computer für Delegierungszwecke vertraut, können Sie den Dienst oder Computer delegierte Authentifizierung abzuschließen, erhalten ein Ticket für den Benutzer, der die Anforderung stammt und auf Informationen für den Benutzer zuzugreifen. Dieses Modell beschränkt den Datenzugriff auf Back-End-Server nur für diesen Benutzer oder die Dienste, vorhanden Anmeldeinformationen mit den richtigen Zugriff Control-Token. Darüber hinaus ermöglicht es dateizugriffsüberwachung dieser Back-End-Ressourcen. Erforderlich ist, dass alle Daten mithilfe der Anmeldeinformationen zugegriffen werden, die an den Server für die Verwendung im Auftrag des Clients delegiert werden, stellen Sie sicher, dass der Server kann nicht beeinträchtigt werden, dass Sie Zugriff auf vertrauliche Informationen erlangen können auf anderen Servern gespeichert. Delegierte Authentifizierung eignet sich für Multi-Tier-Anwendungen, die Funktionen für einmalige Anmelden auf mehreren Computern verwendet werden soll.

### <a name="authentication-in-trust-relationships-between-domains"></a>Authentifizierung in Vertrauensstellungen zwischen Domänen
Die meisten Organisationen mit mehr als einer Domäne sind, müssen Benutzer Zugriff auf freigegebene Ressourcen, die in einer anderen Domäne befinden, wie die mobilen Ortswechsel zu verschiedenen Regionen, in dem Land zulässig ist. Zum Steuern dieses Zugriffs erfordert, dass Benutzer in einer Domäne können auch authentifiziert und autorisiert, Ressourcen in einer anderen Domäne zu verwenden. Um Funktionen für Authentifizierung und Autorisierung zwischen Clients und Servern in verschiedenen Domänen zu ermöglichen, muss eine Vertrauensstellung zwischen den beiden Domänen vorhanden sein. Vertrauensstellungen sind die zugrunde liegende Technologie, mit der sichere Kommunikation für Active Directory auftreten, und sind eine integrale Security-Komponente von der Netzwerkarchitektur von Windows Server.

Wenn eine Vertrauensstellung zwischen zwei Domänen vorhanden ist, vertrauen die Authentifizierungsmechanismen für jede Domäne der Authentifizierungen, die von der anderen Domäne. Vertrauensstellungen ermöglichen einen kontrollierten Zugriff auf gemeinsam genutzten Ressourcen in einer Ressourcendomäne – der vertrauenden Domäne – indem Sie überprüfen, Authentifizierung des eingehende Anforderungen von einer vertrauenswürdigen Zertifizierungsstelle: der vertrauenswürdigen Domäne stammen. Auf diese Weise fungieren die Vertrauensstellungen als Bridges, die jetzt nur Authentifizierung Anforderungen Travel zwischen Domänen überprüft.

Wie eine bestimmte Vertrauensstellung authentifizierungsanforderungen übergeben werden, hängt davon ab, wie er konfiguriert ist. Vertrauensstellungen können unidirektional, indem Sie Zugriff von der vertrauenswürdigen Domäne auf Ressourcen in der vertrauenden Domäne oder bidirektionale sein, indem Zugriff aus jeder Domäne auf Ressourcen in der anderen Domäne. Vertraut sind auch entweder nicht transitive, in der Groß-/Kleinschreibung nur zwischen den zwei vertrauenswürdige Partner-Domänen, oder transitive Vertrauensstellung, die in diesem Fall Vertrauensstellung erweitert automatisch auf alle weiteren Domänen, die einer der Partner vertraut.

Weitere Informationen zur Funktionsweise einer Vertrauensstellung finden Sie unter [wie Domänen- und Gesamtstruktur-Vertrauensstellungen Arbeit](https://technet.microsoft.com/library/cc773178(v=ws.10).aspx).

### <a name="protocol-transition"></a>Protokollübergang
Protokollübergang unterstützt Anwendungsentwickler, indem es Ihnen ermöglicht Anwendungen, die unterschiedliche Authentifizierungsmechanismen auf der Ebene des Benutzer-Authentifizierung unterstützt und durch den Wechsel zu das Kerberos-Protokoll für die Sicherheitsfeatures, wie gegenseitige Authentifizierung und die eingeschränkte Delegierung, in den nachfolgenden Anwendungsebenen.

Weitere Informationen zu den Protokollübergang, finden Sie unter [Kerberos-Protokollübergang und eingeschränkte Delegierung](https://technet.microsoft.com/library/cc758097(v=ws.10).aspx).

### <a name="constrained-delegation"></a>Eingeschränkte Delegierung
Eingeschränkter Delegierung ermöglicht Administratoren festlegen und Erzwingen von anwendungsvertrauensstellungsgrenzen durch Begrenzen des Bereichs, in dem Anwendungsdienste im Auftrag eines Benutzers handeln können. Sie können bestimmte Dienste angeben, von denen ein Computer, der für die Delegierung als vertrauenswürdig eingestuft wird Ressourcen anfordern kann. Die Flexibilität, die Autorisierung von Berechtigungen für Dienste einschränken kann Anwendungsentwurf für die Sicherheit zu verbessern, indem Sie die Möglichkeiten für die Gefährdung von nicht vertrauenswürdigen Diensten reduzieren.

Weitere Informationen zur eingeschränkten Delegierung finden Sie unter [Kerberos eingeschränkte Delegierung](../kerberos/kerberos-constrained-delegation-overview.md).

## <a name="see-also"></a>Siehe auch
[Windows-Anmeldung und Authentifizierung – technische Übersicht](https://technet.microsoft.com/library/dn269029.aspx)


