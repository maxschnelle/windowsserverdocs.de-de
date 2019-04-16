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
ms.openlocfilehash: 27e124c971926edd33f102fe6009a0c552c6d814
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="windows-authentication-concepts"></a>Windows-Authentifizierungskonzepte

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Referenzthema für (Übersicht) beschreibt die Konzepte, die auf denen Windows-Authentifizierung basiert.

Authentifizierung ist ein Prozess zur Überprüfung der Identität eines Objekts oder einer Person. Wenn Sie ein Objekt authentifizieren, ist das Ziel, stellen Sie sicher, dass das Objekt um eine Originalversion handelt. Wenn Sie eine Person authentifizieren, ist das Ziel, stellen Sie sicher, dass die Person, die nicht von einem Betrüger ist.

In einem Netzwerk Kontext dient die Authentifizierung der Nachweis der Identität zu einer Netzwerkanwendung oder -Ressource. In der Regel ist die Identität durch einen kryptografischen Vorgang nachgewiesen, verwendet, die entweder ein Schlüssel nur für den Benutzer (wie bei der Kryptografie mit öffentlichem Schlüssel) bekannt sind oder ein vorinstallierter Schlüssel. Die Serverseite der Authentifizierung vergleicht die signierten Daten mit einem bekannten Kryptografieschlüssel, um den Authentifizierungsversuch zu überprüfen.

Speichern die kryptografischen Schlüssel an einem sicheren, zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory ist die empfohlene und standardmäßig verwendete Technologie zum Speichern von Identitätsinformationen, darunter die kryptografischen Schlüssel, die mit werden die Anmeldeinformationen des Benutzers. Active Directory ist für Standardimplementierungen von Kerberos und NTLM-Standard erforderlich.

Um ein Betriebssystem oder eine Anmeldung beim Dienst oder Anwendung, die Benutzer identifiziert die verfügbaren Authentifizierungstechniken reichen von der einfachen Anmeldung anhand von etwas nur der Benutzer weiß, wie z.B. ein Kennwort zu leistungsfähigeren Sicherheitsmechanismen, bei denen der Benutzer has'such als Token, Zertifikate mit öffentlichem Schlüssel, Bilder oder biologische Attributen. In einer Unternehmensumgebung können Benutzer mehrere Anwendungen auf verschiedenen Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesen Gründen muss die Authentifizierung Umgebungen für andere Plattformen und für andere Windows-Betriebssysteme unterstützen.

## <a name="authentication-and-authorization-a-travel-analogy"></a>Authentifizierung und Autorisierung: eine Reise Analogie
Erläutern Sie die Funktionsweise der Authentifizierung ist eine Reise Analogie helfen. Einige vorbereitende Schrittesind in der Regel erforderlich, um die Reise zu beginnen. Der Urlaub muss sich "true" Host Behörde identifizieren. Dieser Nachweis befinden in Form von Identitätsnachweis Staatsangehörigkeit, Geburtsort, einen persönlichen Beleg, Fotos oder den Inhalt erforderlich ist, das Recht des Landes. Der Urlaub Identität wird durch die Ausstellung eines Passports überprüft, was wiederum analog zu einem Systemkonto ausgestellt und von einer Organisation – der Sicherheitsprinzipal verwaltet. Die Passport- und das gewünschte Ziel basieren auf einen Satz von Regeln und Bestimmungen, die von der staatlichen Behörde ausgestellte.

**Die Reise**

Der Urlaub Grenze der internationalen empfangen werden, einen Rahmen Guard fordert zur Eingabe von Anmeldeinformationen und die Reisenden stellt seine Passport. Der Prozess hat zwei:

-   Mit dem Blocker authentifiziert den Passport, überprüfen Sie, dass es eine Sicherheitsinstanz ausgestellt wurde, dass der lokale Behörden (Vertrauensstellungen, zumindest zum Ausstellen von Passport) vertraut, und überprüfen Sie, dass die Passport nicht geändert wurde.

-   Mit dem Blocker authentifiziert den Urlaub überprüfen, dass die Oberfläche das Gesicht von der Person, die auf den Passport dargestellten übereinstimmt und andere Anmeldeinformationen ordnungsgemäß sind.

Wenn die Passport erweist sich als gültig ist und der Urlaub erweist sich als Besitzer sein, Authentifizierung ist erfolgreich, und der Urlaub kann über den Rahmen Zugriff zugelassen werden.

Transitive Vertrauensstellungen zwischen Zertifizierungsstellen Sicherheit ist die Grundlage für die Authentifizierung. die Art der Authentifizierung, die eine internationale Grenze stattfindet basiert auf Vertrauensstellung. Die lokale Behörden weiß nicht, die Reisenden, aber ihr vertraut, dass die Host-Regierung hat. Wenn die Host-Regierung den Passport ausgegeben, der Urlaub nicht entweder bekannt. Sie als vertrauenswürdig eingestuft, die Stelle, die das Geburtsdatum Zertifikat oder andere Dokumentation ausgestellt. Die Stelle, die das Geburtsdatum hat, vertrauenswürdige wiederum Arztes, die das Zertifikat signiert. Arztes haben die Reisenden Geburtsdatum und das Zertifikat mit direkten Nachweis der Identität, in diesem Fall mit der neugeborenen Speicherbedarf. Vertrauensstellung, die auf diese Weise über eine vertrauenswürdige zwischengeschaltete übertragen werden ist transitiv.

Transitive Vertrauensstellung ist die Grundlage für die Netzwerksicherheit in der Windows-Client/Server-Architektur. Eine Vertrauensstellung gilt für eine Gruppe von Domänen, z.B. eine Domänenstruktur, und bildet eine Beziehung zwischen einer Domäne und alle Domänen, die dieser Domäne vertrauen. Z.B. vertraut Domäne A hat eine transitive Vertrauensstellung zur Domäne B und Domäne B Domäne C vertraut, dann Domäne A Domäne C.

Es gibt ein Unterschied zwischen Authentifizierung und Autorisierung. Bei der Authentifizierung weist das System, dass Sie sich befinden, die Sie sagen, dass Sie sich befinden. Mit der Autorisierung überprüft das System, dass Sie sind berechtigt, was Sie tun möchten. Um die Analogie Rahmen mit dem nächsten Schrittin Anspruch nehmen, wird lediglich authentifizieren, dass die Reisenden der Eigentümer von einem gültigen Passport ist nicht unbedingt der Urlaub, geben Sie ein Land autorisieren. Artenvielfalt der einem bestimmten Land dürfen einem anderen Land eingeben, indem Sie einfach einen Passport nur in Fällen, in denen das Land, der eingegeben wird unbegrenzt die Berechtigung für alle Bürger von diesem bestimmten Land zur geben erteilt, darstellen.

Auf ähnliche Weise können Sie alle Benutzer auf eine bestimmte Domänenberechtigungen den Zugriff auf eine Ressource gewähren. Jeder Benutzer, die für diese Domäne gehört, hat Zugriff auf die Ressource, genauso wie Kanada US-Bürger gebe Kanada. Suchen, US-Bürger Brasilien oder Indien eingeben möchte, dass sie die Länder, indem Sie einfach einen Passport darstellen, da beide dieser Länder erforderlich sind, besuchen die US-Bürger, um eine gültige Visa eingeben können. Daher garantiert Authentifizierung nicht den Zugriff auf Ressourcen oder Autorisierung, Ressourcen zu verwenden.

## <a name="credentials"></a>Anmeldeinformationen
Einen Passport und ggf. zugeordnete Visa sind die akzeptierten Anmeldeinformationen für ein Urlaub. Allerdings können diese Anmeldeinformationen keine Urlaub eingeben oder den Zugriff auf alle Ressourcen in einem Land. Beispielsweise müssen zusätzliche Anmeldeinformationen eine Konferenz besuchen. In Windows können Anmeldeinformationen verwaltet werden, für den Kontoinhaber auf Ressourcen über das Netzwerk zugreifen, ohne wiederholt Anmeldeinformationen eingeben können. Diese Art des Zugriffs kann Benutzer, die durch das System den Zugriff auf alle Anwendungen authentifiziert werden und Datenquellen, dass sie autorisiert sind, verwenden, ohne Sie zu einem anderen Konto-ID oder Ihr Kennwort eingeben. Die Windows-Plattform nutzt die Möglichkeit, eine einzelne Benutzeridentität (von Active Directory verwaltet) über das Netzwerk zu verwenden, indem Sie lokal Zwischenspeichern von Anmeldeinformationen in das Betriebssystem Local Security Authority (LSA). Wenn ein Benutzer an der Domäne anmeldet, Windows-Authentifizierungspakete transparent die Anmeldeinformationen verwenden einmaliges Anmelden bereitzustellen, wenn die Anmeldeinformationen auf Netzwerkressourcen zu authentifizieren. Weitere Informationen zu Anmeldeinformationen finden Sie unter [Anmeldeinformationen-Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md).

Eine Form der Multi-Factor Authentication für den Urlaub möglicherweise die Anforderung und darstellen mehrerer Dokumente, um seine Identität wie z.B. eine Registrierungsinformationen Passport und Konferenz zu authentifizieren. Windows implementiert dieses Formular oder die Authentifizierung mit Smartcards, virtuelle Smartcards und biometrische Technologien. 

## <a name="security-principals-and-accounts"></a>Sicherheitsprinzipale und Konten
In Windows ist jeder Benutzer, Dienst, Gruppe oder Computer, die Aktion initiieren kann einen Sicherheitsprinzipal. Sicherheitsprinzipale haben Konten, die domänenbasierte werden oder lokal auf einem Computer werden können. Beispielsweise können Windows-Clientcomputer Domäne teilnehmen, in einer Netzwerkdomäne durch Kommunikation mit einem Domänencontroller, auch wenn kein Benutzer angemeldet ist. Um die Kommunikation initiieren können, muss der Computer ein aktives Konto in der Domäne verfügen. Vor der Annahme von Verbindungen mit dem Computer, auf dem Domänencontroller die lokale Sicherheitsautorität authentifiziert die Identität des Computers und des Computers Sicherheitskontext definiert, genau wie für einen menschlichen Sicherheitsprinzipal. Dieser Sicherheitskontext definiert die Identität und die Funktionen von einem Benutzer oder Dienst auf einem bestimmten Computer oder ein Benutzer, Dienst, Gruppe oder Computer in einem Netzwerk. Es definiert z.B. die Ressourcen, z.B. eine Dateifreigabe oder Drucker, das zugegriffen werden kann und die Aktionen, wie z.B. Lese-, Schreib- oder ändern, die durch einen Benutzer, der Dienst oder der Computer, auf die Ressource ausgeführt werden können. Weitere Informationen finden Sie unter [Sicherheitsprinzipale](https://technet.microsoft.com/itpro/windows/keep-secure/security-principals).

Ein Konto ist eine Möglichkeit zum Identifizieren des Antragstellers – die Benutzer oder den Dienst - Zugriff oder Ressourcen anfordern. Der Urlaub, die den authentischen Passport enthält verfügt über ein Konto mit dem Host Land. Benutzer, Gruppen von Benutzern, Objekten und Dienste alle können einzelne Konten oder Konten teilen. Konten können Mitglied der Gruppe und bestimmte Rechte und Berechtigungen zugewiesen werden können. Kann auf dem lokalen Computer, Arbeitsgruppe, Netzwerk beschränkt sein oder Mitglied einer Domäne zugewiesen werden.

Für jede Version von Windows sind integrierte Konten und die Sicherheitsgruppen, die sie Mitglieder sind definiert. Mithilfe von Sicherheitsgruppen können Sie zuweisen die gleichen Sicherheitsberechtigungen für viele Benutzer, die erfolgreich authentifiziert werden, die Verwaltung vereinfacht. Regeln für das Ausstellen von Passport möglicherweise bestimmte Gruppen, z.B. Unternehmen oder Sport- oder Regierungsbehörden der Urlaub zugewiesen werden. Dieser Prozess wird eine konsistente Sicherheitsberechtigungen für alle Mitglieder einer Gruppe sichergestellt. Verwenden von Sicherheitsgruppen zum Zuweisen von Berechtigungen bleibt bedeutet, die Steuerung der Ressourcen zugreifen Konstanten und einfach zu verwalten und überwachen. Hinzufügen und Entfernen von Benutzern, die Zugriff auf den entsprechenden Sicherheitsgruppen benötigen, je nach Bedarf, können Sie die Häufigkeit von Änderungen an Zugriffssteuerungslisten (ACLs) minimieren.

Eigenständige verwaltete Dienstkonten und virtuelle Konten in Windows Server2008 R2 und Windows7, die erforderliche Anwendungen stellen eingeführt wurden, z.B. Microsoft Exchange Server und IIS (Internetinformationsdienste), die Isolierung der eigenen Domänenkonten, während die Notwendigkeit von einem Administrator manuell entfernen den Dienstprinzipalnamen (SPN) und die Anmeldeinformationen für diese Konten zu verwalten. Gruppe verwaltete Dienstkonten wurden in Windows Server2012 eingeführt und bietet die gleiche Funktionalität innerhalb der Domäne, aber auch, dass eine Funktion erstreckt sich über mehrere Server. Beim Verbinden mit einem Dienst in einer Serverfarm, z.B. Netzwerklastenausgleich, müssen die gegenseitige Authentifizierung unterstützende Authentifizierungsprotokolle alle Instanzen der Dienste den gleichen Prinzipal verwenden.

Weitere Informationen zu Konten finden Sie unter:

-   [Active Directory-Konten](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-accounts)

-   [Active Directory-Sicherheitsgruppen](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-security-groups)

-   [Lokale Konten](https://technet.microsoft.com/itpro/windows/keep-secure/local-accounts)

-   [Microsoft-Konten](https://technet.microsoft.com/itpro/windows/keep-secure/microsoft-accounts)

-   [Dienstkonten](https://technet.microsoft.com/itpro/windows/keep-secure/service-accounts)

-   [Besondere Identitäten](https://technet.microsoft.com/itpro/windows/keep-secure/special-identities)

## <a name="delegated-authentication"></a>Delegierte Authentifizierung
Um die Reise Analogie zu verwenden, möglicherweise Ländern den gleichen Zugriff für alle Mitglieder einer offiziellen staatliche Delegierung ausstellen, solange die Delegaten bekannt sind. Diese Delegierung wir einen Member wirken sich auf die Berechtigungen eines anderen Elements. In Windows tritt auf, delegierte Authentifizierung, wenn ein Netzwerkdienst eine Authentifizierungsanforderung von einem Benutzer akzeptiert und wird die Identität des Benutzers zum Initiieren einer neuen Verbindungs mit einem zweiten Netzwerkdienst angenommen. Um delegierte Authentifizierung unterstützen, müssen Sie einrichten, Front-End- oder der ersten Ebene Servern, z.B. Webserver, die für die Behandlung von Client-Authentifizierungsanfragen verantwortlich sind und Back-End "oder" n-Tier-Server, z.B. großen Datenbanken, die zum Speichern von Informationen verursachen. Sie können das Recht, delegierte Authentifizierung für Benutzer in Ihrer Organisation einrichten, um den administrativen Arbeitsaufwand der Administratoren zu reduzieren delegieren.

Durch die Einrichtung von einem Dienst oder der Computer für Delegierungszwecke vertraut, können Sie den Dienst oder Computer delegierte Authentifizierung abzuschließen, erhalten ein Ticket für den Benutzer, der die Anforderung stellt, und dann auf Informationen des Benutzers zugreifen. Dieses Modell schränkt Zugriffe auf Daten auf Back-End-Server nur für diesen Benutzer oder Dienste, Anmeldeinformationen mit der richtigen Steuerelement Zugriffstoken. Darüber hinaus ermöglicht es Zugriff Überwachung dieser Back-End-Ressourcen. Gefordert, wird, dass alle Daten über Anmeldeinformationen zugegriffen wird, die an den Server für die Verwendung im Auftrag des Clients delegiert werden Stellen Sie sicher, dass der Server kann nicht kompromittiert werden und darin, dass Sie Zugriff auf vertrauliche Informationen erlangen können auf anderen Servern gespeichert. Delegierte Authentifizierung ist hilfreich für Multi-Tier-Anwendungen, die einen einzelne SSO-Funktionen auf mehreren Computern verwenden.

### <a name="authentication-in-trust-relationships-between-domains"></a>Authentifizierung in Vertrauensstellungen zwischen Domänen
Die meisten Organisationen mit mehreren Domänen vorliegen, dass einem müssen Benutzern Zugriff auf freigegebene Ressourcen, die sich in einer anderen Domäne befinden wie der Urlaub in verschiedenen Regionen, in dem Land Reisen zulässig ist. Zum Steuern dieses Zugriffs erfordert, dass Benutzer in einer Domäne auch authentifiziert und autorisiert werden können, Ressourcen in einer anderen Domäne zu verwenden. Um die Authentifizierung und Autorisierung Funktionen zwischen Clients und Servern in anderen Domänen bereitstellen, muss eine Vertrauensstellung zwischen den beiden Domänen vorhanden sein. Vertrauensstellungen sind die zugrunde liegende Technologie, mit der sichere Active Directory-Kommunikation auftreten und sind ein wesentlicher Sicherheitskomponente der Windows Server-Netzwerkarchitektur.

Wenn eine Vertrauensstellung zwischen zwei Domänen vorhanden ist, vertrauen die Authentifizierungsmechanismen für jede Domäne der Authentifizierungen von der anderen Domäne stammen. Vertrauensstellungen ermöglichen die für den kontrollierten Zugriff auf freigegebene Ressourcen in einer Ressourcendomäne – der vertrauenden Domäne – überprüfen Sie die Authentifizierung des eingehende Anforderungen von einer vertrauenswürdigen Zertifizierungsstelle – der vertrauenswürdigen Domäne stammen. Auf diese Weise fungieren Vertrauensstellungen als Brücken, mit denen nur Authentifizierung Anforderungen Reise zwischen Domänen überprüft.

Wie eine bestimmte Vertrauensstellung Authentifizierungsanfragen übergibt, hängt davon ab, wie es konfiguriert ist. Vertrauensstellungen können durch den Zugriff der vertrauenswürdigen Domäne auf Ressourcen in der vertrauenden Domäne eine unidirektionale oder bidirektionale werden, indem der Zugriff aus jeder Domäne auf Ressourcen in der anderen Domäne. Vertrauensstellungen sind auch entweder nicht transitive, in der Groß-/Kleinschreibung nur zwischen den zwei vertrauenswürdigen Partnerdomänen oder transitive Vertrauensstellung, die in diesem Fall Vertrauensstellung automatisch auf alle anderen Domänen, die einem der Partner vertraut erweitert.

Informationen zur Funktionsweise von einer Vertrauensstellung finden Sie unter [wie Domänen- und Gesamtstruktur-Vertrauensstellungen Arbeit](https://technet.microsoft.com/library/cc773178(v=ws.10).aspx).

### <a name="protocol-transition"></a>Protokollübergang
Protokollübergang Anwendungsentwickler unterstützt, können Sie Anwendungen, die andere Authentifizierungsmechanismen auf der Ebene des Benutzer-Authentifizierung unterstützen und der Wechsel auf die Kerberos-Protokoll für Sicherheitsfeatures wie die gegenseitige Authentifizierung und die eingeschränkte Delegierung in den nachfolgenden Anwendungsebenen.

Weitere Informationen zu Protokollübergang, finden Sie unter [Kerberos-Protokollübergang und eingeschränkte Delegierung](https://technet.microsoft.com/library/cc758097(v=ws.10).aspx).

### <a name="constrained-delegation"></a>Die eingeschränkte Delegierung
Die eingeschränkte Delegierung ermöglicht Administratoren das Festlegen und erzwingen, durch das Einschränken des Bereichs, in dem Anwendungsdienste im Auftrag eines Benutzers agieren kann. Sie können bestimmte Dienste angeben, von denen ein Computer, der für Delegierungszwecke vertraut wird, Ressourcen anfordern kann. Die Flexibilität, begrenzen, Autorisierungsrechte für Dienste verbessert Anwendungsdesign Sicherheit durch reduzieren die Möglichkeiten für die Gefährdung von nicht vertrauenswürdigen Diensten.

Weitere Informationen zur eingeschränkten Delegierung finden Sie unter [Kerberos Constrained Delegation (Übersicht)](../kerberos/kerberos-constrained-delegation-overview.md).

## <a name="see-also"></a>Siehe auch
[Windows-Anmeldung und Authentifizierung (technische Übersicht)](https://technet.microsoft.com/library/dn269029.aspx)


