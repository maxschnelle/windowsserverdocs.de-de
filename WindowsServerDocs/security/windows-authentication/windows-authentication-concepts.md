---
title: Windows-Authentifizierungskonzepte
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-windows-auth
ms.topic: article
ms.assetid: 29d1db15-cae0-4e3d-9d8e-241ac206bb8b
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4051bfea26d5c96d02132b50373f56b7b17ce5fb
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80857473"
---
# <a name="windows-authentication-concepts"></a>Windows-Authentifizierungskonzepte

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

In diesem Referenz Übersichts Thema werden die Konzepte beschrieben, auf denen die Windows-Authentifizierung basiert.

Authentifizierung ist der Vorgang, durch den die Identität eines Objekts oder einer Person überprüft wird. Ziel der Authentifizierung eines Objekts ist es, sicherzustellen, dass das Objekt echt und unverfälscht ist. Wenn Sie eine Person authentifizieren, besteht das Ziel darin, zu überprüfen, ob die Person kein Imposter ist.

Im Netzwerkkontext dient die Authentifizierung dazu, die Identität gegenüber einer Netzwerkanwendung oder -ressource nachzuweisen. In der Regel wird die Identität durch einen kryptografischen Vorgang nachgewiesen, der einen Schlüssel verwendet, der nur dem Benutzer bekannt ist (wie bei der Kryptografie mit öffentlichem Schlüssel) oder ein gemeinsam verwendeter Schlüssel. Auf der Serverseite der Authentifizierungskommunikation werden die signierten Daten mit einem bekannten Kryptografieschlüssel verglichen, um den Authentifizierungsversuch zu überprüfen.

Durch die Speicherung der Kryptografieschlüssel an einem zentralen Ort wird der Authentifizierungsvorgang skalierbar und verwaltbar. Active Directory ist die empfohlene und Standardtechnologie zum Speichern von Identitätsinformationen, die die kryptografischen Schlüssel enthalten, bei denen es sich um die Anmelde Informationen des Benutzers handelt. Active Directory ist für Standardimplementierungen von Kerberos und NTLM erforderlich.

Die Authentifizierungstechniken reichen von der einfachen Anmeldung bei einem Betriebssystem oder der Anmeldung bei einem Dienst oder einer Anwendung, der Benutzer auf der Grundlage von etwas, das nur dem Benutzer bekannt ist (z. b. ein Kennwort), zu leistungsfähigeren Sicherheitsmechanismen, die von Benutzern verwendet werden, wie z. b. Token, öffentliche Schlüssel Zertifikate, Bilder oder biologische Attribute, identifiziert. In einer Unternehmensumgebung ist es Benutzer eventuell möglich, auf unterschiedliche Anwendungen auf verschiedenen Arten von Servern an einem einzigen Standort oder auch standortübergreifend zugreifen. Aus diesem Grund muss die Authentifizierung Umgebungen unterstützen, die auf anderen Plattformen und anderen Windows-Betriebssystemen basieren.

## <a name="authentication-and-authorization-a-travel-analogy"></a>Authentifizierung und Autorisierung: eine Reise Analogie
Eine Reise Analogie kann Ihnen helfen, die Funktionsweise der Authentifizierung zu erläutern. In der Regel sind einige Vorbereitungsaufgaben erforderlich, um die Journey zu beginnen. Der Reisende muss seine tatsächliche Identität seinen Host Behörden nachweisen. Diese Prüfung kann in Form von Nachweis der Bürgerschaft, Geburts Stelle, persönlichen gutschafts-, Foto-und Foto-oder sonstigen Anforderungen des Gastlandes erfolgen. Die Identität des Reisenden wird durch die Ausstellung eines Passport überprüft. Dies entspricht einem von einer Organisation ausgestellten und verwalteten Systemkonto (dem Sicherheits Prinzipal). Der Passport und das beabsichtigte Ziel basieren auf einer Reihe von Regeln und Vorschriften, die von der behördlichen Behörde ausgestellt wurden.

**Die Journey**

Wenn der Reisende an der internationalen Grenze eintrifft, fordert ein Border Guard Anmelde Informationen an, und der Reiseleiter zeigt seinen Passport an. Der Prozess ist zweifache:

-   Der Schutz authentifiziert den Passport, indem er überprüft, ob er von einer Sicherheits Autorität ausgestellt wurde, die von der lokalen Regierung als vertrauenswürdig eingestuft wird.

-   Der Wächter authentifiziert den Benutzer, indem er überprüft, ob das Gesicht mit dem Gesicht der Person übereinstimmt, die auf dem Passport abgebildet ist, und dass andere erforderliche Anmelde Informationen in Ordnung sind.

Wenn der Passport-Wert gültig ist und der Reisende seinen Besitzer bestätigt, ist die Authentifizierung erfolgreich, und dem Reisenden kann der Zugriff über den Rahmen gestattet werden.

Transitive Vertrauensstellung zwischen Sicherheitsbehörden ist die Grundlage für die Authentifizierung. der Authentifizierungstyp, der an einem internationalen Rahmen stattfindet, basiert auf der Vertrauensstellung. Die lokale Regierung kennt den Reisenden nicht, aber Sie vertraut der Host Regierung. Wenn die Host Behörde den Passport ausgestellt hat, hat Sie den Reisenden nicht kennen gelernt. Er hat der Agentur vertraut, die das Geburts Zertifikat oder eine andere Dokumentation ausgestellt hat. Die Agentur, die das Geburts Zertifikat ausgestellt hat, hat wiederum den Arzt, der das Zertifikat signiert hat, als vertrauenswürdig eingestuft. Der Arzt hat den Geburtstag des Reisenden miterlebt und das Zertifikat mit einem direkten Nachweis der Identität versehen, in diesem Fall mit dem Speicherbedarf der Neugeborenen. Vertrauens Stellungen, die auf diese Weise über den vertrauenswürdigen Vermittler übertragen werden, sind transitiv.

Transitive Vertrauensstellung ist die Grundlage für die Netzwerksicherheit in der Windows-Client-/Serverarchitektur. Eine Vertrauensstellung fließt in eine Gruppe von Domänen, wie z. b. eine Domänen Struktur, und bildet eine Beziehung zwischen einer Domäne und allen Domänen, die dieser Domäne vertrauen. Wenn Domäne a z. b. eine transitiv Vertrauensstellung mit Domäne b aufweist und Domäne b Domäne c vertraut, vertraut Domäne a Domäne c.

Es gibt einen Unterschied zwischen Authentifizierung und Autorisierung. Mit der-Authentifizierung beweist das System, dass Sie Sie sind. Mit der Autorisierung überprüft das System, ob Sie über die Rechte verfügen, was Sie tun möchten. Um die Rahmen Analogie zum nächsten Schritt zu übernehmen, ist die reine Authentifizierung, dass der Reisende der ordnungsgemäße Besitzer eines gültigen Passport ist, nicht zwangsläufig autorisiert, den Reisenden in ein Land einzugeben. Die Einwohner eines bestimmten Landes können in ein anderes Land eintreten, indem Sie einfach nur in Situationen, in denen das Land eingegeben wird, eine unbegrenzte Berechtigung für alle Bürger dieses bestimmten Landes gewähren.

Auf ähnliche Weise können Sie allen Benutzern aus einer bestimmten Domäne Berechtigungen für den Zugriff auf eine Ressource gewähren. Jeder Benutzer, der zu dieser Domäne gehört, hat Zugriff auf die Ressource, ebenso wie Kanada es US-Bürgern ermöglicht, Kanada einzugeben. Allerdings haben US-Bürger, die versuchen, in Brasilien oder Indien zu eintreten, festzustellen, dass Sie diese Länder nicht nur durch die Darstellung eines Passport eingeben können Die Authentifizierung garantiert daher nicht den Zugriff auf Ressourcen oder die Autorisierung für die Verwendung von Ressourcen.

## <a name="credentials"></a>Anmeldeinformationen
Ein Passport-und möglicherweise zugeordnetes Visum sind die akzeptierten Anmelde Informationen für einen Reisenden. Mit diesen Anmelde Informationen kann ein Reisender jedoch nicht auf alle Ressourcen in einem Land zugreifen oder darauf zugreifen. Beispielsweise sind für die Teilnahme an einer Konferenz zusätzliche Anmelde Informationen erforderlich. In Windows können Anmelde Informationen verwaltet werden, damit Kontoinhaber über das Netzwerk auf Ressourcen zugreifen können, ohne dass Sie wiederholt ihre Anmelde Informationen angeben müssen. Diese Art des Zugriffs ermöglicht Benutzern das einmalige Authentifizieren von Benutzern, um auf alle Anwendungen und Datenquellen zuzugreifen, für die Sie autorisiert sind, ohne einen anderen Konto Bezeichner oder ein anderes Kennwort einzugeben. Die Windows-Plattform nutzt die Möglichkeit, eine einzelne Benutzeridentität (durch Active Directory) im Netzwerk zu verwenden, indem Benutzer Anmelde Informationen lokal in der lokalen Sicherheits Autorität (LSA) des Betriebssystems zwischengespeichert werden. Wenn sich ein Benutzer bei der Domäne anmeldet, verwenden Windows-Authentifizierungs Pakete die Anmelde Informationen transparent, um beim Authentifizieren der Anmelde Informationen für Netzwerkressourcen Single Sign-on bereitzustellen. Weitere Informationen zu Anmelde Informationen finden Sie unter Anmelde Informationen für [Prozesse in der Windows-Authentifizierung](credentials-processes-in-windows-authentication.md).

Eine Form der Multi-Factor Authentication für den Reisenden ist möglicherweise die Anforderung, mehrere Dokumente zu übertragen und zu präsentieren, um Ihre Identität zu authentifizieren, z. b. Pass-und Konferenz Registrierungsinformationen. Windows implementiert dieses Formular oder die Authentifizierung mithilfe von Smartcards, virtuellen Smartcards und biometrischen Technologien. 

## <a name="security-principals-and-accounts"></a>Sicherheits Prinzipale und Konten
In Windows ist jeder Benutzer, jeder Dienst, jede Gruppe oder jeder Computer, der eine Aktion initiieren kann, ein Sicherheits Prinzipal. Sicherheits Prinzipale verfügen über Konten, die auf einem Computer lokal sein können oder Domänen basiert sind. Beispielsweise können Windows-Client Computer, die einer Domäne angehören, an einer Netzwerk Domäne teilnehmen, indem Sie mit einem Domänen Controller kommunizieren, auch wenn kein Benutzer angemeldet ist. Zum Initiieren der Kommunikation muss der Computer über ein aktives Konto in der Domäne verfügen. Vor der Annahme der Kommunikation vom Computer wird die Identität des Computers von der lokalen Sicherheits Autorität auf dem Domänen Controller authentifiziert. Anschließend wird der Sicherheitskontext des Computers genau wie für einen Human Security Principal definiert. Dieser Sicherheitskontext definiert die Identität und die Funktionen eines Benutzers oder Diensts auf einem bestimmten Computer oder einem Benutzer, einem Dienst, einer Gruppe oder einem Computer in einem Netzwerk. Er definiert z. b. die Ressourcen, z. b. eine Dateifreigabe oder einen Drucker, auf die zugegriffen werden kann, sowie die Aktionen, wie z. b. lesen, schreiben oder ändern, die von einem Benutzer, einem Dienst oder einem Computer auf dieser Ressource ausgeführt werden können. Weitere Informationen finden Sie unter [Sicherheits Prinzipale](https://technet.microsoft.com/itpro/windows/keep-secure/security-principals).

Ein Konto ist ein Mittel zum Identifizieren eines Anforderer: der Benutzer oder der Dienst, der den Zugriff oder die Ressourcen anfordert. Der Reisende, der den authentischen Passport innehat, verfügt über ein Konto mit dem hostland. Benutzer, Gruppen von Benutzern, Objekten und Diensten können über einzelne Konten oder Freigabe Konten verfügen. Konten können Mitglied von Gruppen sein, und Ihnen können bestimmte Rechte und Berechtigungen zugewiesen werden. Konten können auf den lokalen Computer, die Arbeitsgruppe, das Netzwerk oder die zugewiesene Mitgliedschaft zu einer Domäne beschränkt werden.

Integrierte Konten und die Sicherheitsgruppen, von denen Sie Mitglieder sind, werden für jede Windows-Version definiert. Mithilfe von Sicherheitsgruppen können Sie den gleichen Sicherheits Berechtigungen für viele Benutzer zuweisen, die erfolgreich authentifiziert wurden, wodurch die Zugriffs Verwaltung vereinfacht wird. Regeln für das Ausstellen von Pässen erfordern möglicherweise, dass der Reisende bestimmten Gruppen zugewiesen wird, z. b. Geschäfts-, Touristen-oder Regierungsbehörden. Durch diesen Vorgang wird sichergestellt, dass für alle Mitglieder einer Gruppe konsistente Sicherheits Berechtigungen erteilt werden. Durch die Verwendung von Sicherheitsgruppen zum Zuweisen von Berechtigungen bedeutet dies, dass die Zugriffs Steuerung von Ressourcen konstant und einfach zu verwalten und zu überwachen ist. Durch Hinzufügen und Entfernen von Benutzern, die bei Bedarf Zugriff von den entsprechenden Sicherheitsgruppen benötigen, können Sie die Häufigkeit von Änderungen an Zugriffs Steuerungs Listen (ACLs) minimieren.

Eigenständige verwaltete Dienst Konten und virtuelle Konten wurden in Windows Server 2008 R2 und Windows 7 eingeführt, um erforderliche Anwendungen wie Microsoft Exchange Server und Internetinformationsdienste (IIS) mit der Isolation ihrer eigenen Domänen Konten bereitzustellen, während ein Administrator den Dienst Prinzipal Namen (Service Principal Name, SPN) und die Anmelde Informationen für diese Konten nicht mehr manuell verwalten muss. Gruppen verwaltete Dienst Konten wurden in Windows Server 2012 eingeführt und bieten die gleiche Funktionalität innerhalb der Domäne, erweitern diese Funktionalität aber auch auf mehrere Server. Beim Herstellen einer Verbindung mit einem Dienst, der in einer Serverfarm gehostet wird (beispielsweise ein Netzwerklastenausgleich), erfordern die Authentifizierungsprotokolle mit gegenseitiger Authentifizierung, dass alle Instanzen der Dienste den gleichen Prinzipal verwenden.

Weitere Informationen zu Konten finden Sie unter:

-   [Active Directory Konten](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-accounts)

-   [Sicherheitsgruppen Active Directory](https://technet.microsoft.com/itpro/windows/keep-secure/active-directory-security-groups)

-   [Lokale Konten](https://technet.microsoft.com/itpro/windows/keep-bastion.local-accounts)

-   [Microsoft-Konten](https://technet.microsoft.com/itpro/windows/keep-secure/microsoft-accounts)

-   [Dienst Konten](https://technet.microsoft.com/itpro/windows/keep-secure/service-accounts)

-   [Besondere Identitäten](https://technet.microsoft.com/itpro/windows/keep-secure/special-identities)

## <a name="delegated-authentication"></a>Delegierte Authentifizierung
Um die Reise Analogie zu verwenden, können Länder den gleichen Zugriff für alle Mitglieder einer offiziellen behördlichen Delegierung ausgeben, so lange die Delegaten bekannt sind. Diese Delegierung ermöglicht einem Mitglied das agieren der Autorität eines anderen Mitglieds. In Windows erfolgt die delegierte Authentifizierung, wenn ein Netzwerkdienst eine Authentifizierungsanforderung von einem Benutzer akzeptiert und die Identität dieses Benutzers annimmt, um eine neue Verbindung mit einem zweiten Netzwerkdienst zu initiieren. Zur Unterstützung der delegierten Authentifizierung müssen Sie Front-End-Server oder Server der ersten Ebene einrichten, wie z. b. Webserver, die für die Verarbeitung von Client Authentifizierungsanforderungen und Back-End-oder n-Tier-Servern (z. b. große Datenbanken) verantwortlich sind, die für das Speichern von Informationen verantwortlich sind Sie können das Recht zum Einrichten der delegierten Authentifizierung für Benutzer in Ihrer Organisation delegieren, um die administrative Belastung Ihrer Administratoren zu verringern.

Wenn Sie einen Dienst oder Computer als vertrauenswürdig für die Delegierung einrichten, können Sie diesen Dienst oder Computer für die delegierte Authentifizierung festlegen, ein Ticket für den Benutzer erhalten, der die Anforderung sendet, und dann auf Informationen für diesen Benutzer zugreifen. Dieses Modell schränkt den Datenzugriff auf Back-End-Server nur auf die Benutzer oder Dienste ein, die Anmelde Informationen mit den korrekten Zugriffs Steuerungs Token darstellen. Außerdem ermöglicht es die Zugriffs Überwachung für diese Back-End-Ressourcen. Durch die Anforderung, dass auf alle Daten über Anmelde Informationen zugegriffen werden muss, die zur Verwendung im Auftrag des Clients an den Server delegiert werden, stellen Sie sicher, dass der Server nicht kompromittiert werden kann und dass Sie Zugriff auf vertrauliche Informationen erhalten können, die auf anderen Servern gespeichert sind. Die delegierte Authentifizierung ist nützlich für Anwendungen mit mehreren Ebenen, die für die Verwendung Single Sign-On Funktionen auf mehreren Computern konzipiert sind.

### <a name="authentication-in-trust-relationships-between-domains"></a>Authentifizierung in Vertrauens Stellungen zwischen Domänen
Die meisten Organisationen, die über mehr als eine Domäne verfügen, müssen den Benutzern den Zugriff auf gemeinsam genutzte Ressourcen in einer anderen Domäne erlauben, ebenso wie der Reisende in verschiedene Regionen im Land einreisen darf. Um diesen Zugriff zu steuern, ist es erforderlich, dass Benutzer in einer Domäne auch authentifiziert und autorisiert werden können, Ressourcen in einer anderen Domäne zu verwenden. Zum Bereitstellen von Authentifizierungs-und Autorisierungs Funktionen zwischen Clients und Servern in verschiedenen Domänen muss eine Vertrauensstellung zwischen den beiden Domänen vorhanden sein. Vertrauens Stellungen sind die zugrunde liegende Technologie, mit der gesicherte Active Directory Kommunikation stattfindet und eine integrale Sicherheitskomponente der Windows Server-Netzwerkarchitektur ist.

Wenn eine Vertrauensstellung zwischen zwei Domänen besteht, Vertrauen die Authentifizierungsmechanismen für jede Domäne den Authentifizierungen aus der anderen Domäne. Vertrauens Stellungen unterstützen den kontrollierten Zugriff auf freigegebene Ressourcen in einer Ressourcen Domäne (die vertrauende Domäne), indem Sie überprüfen, ob eingehende Authentifizierungsanforderungen von einer vertrauenswürdigen Zertifizierungsstelle stammen, der vertrauenswürdigen Domäne. Auf diese Weise fungieren Vertrauens Stellungen als Bridges, bei denen nur überprüfte Authentifizierungsanforderungen zwischen Domänen übertragen werden können.

Wie eine bestimmte Vertrauensstellung Authentifizierungsanforderungen übergibt, hängt von der Konfiguration ab. Vertrauens Stellungen können unidirektional sein, indem der Zugriff von der vertrauenswürdigen Domäne auf Ressourcen in der vertrauenden Domäne bereitgestellt wird (oder bidirektional), indem der Zugriff von jeder Domäne auf Ressourcen in der anderen Domäne gewährt wird. Vertrauens Stellungen sind ebenfalls nicht transitiv. in diesem Fall besteht nur eine Vertrauensstellung zwischen den beiden vertrauenswürdigen Partner Domänen oder transitiv. in diesem Fall wird die Vertrauensstellung automatisch auf alle anderen Domänen ausgedehnt, denen beide Partner vertraut sind.

Informationen zur Funktionsweise einer Vertrauensstellung finden Sie unter [Funktionsweise von Domänen-und](https://technet.microsoft.com/library/cc773178(v=ws.10).aspx)Gesamtstruktur-Vertrauens Stellungen.

### <a name="protocol-transition"></a>Protokoll Übergang
Der Protokoll Übergang unterstützt Anwendungsentwickler, indem es Anwendungen ermöglicht, verschiedene Authentifizierungsmechanismen auf der Benutzer Authentifizierungs Ebene zu unterstützen und in den nachfolgenden Anwendungsebenen auf das Kerberos-Protokoll für Sicherheitsfeatures wie z. b. gegenseitige Authentifizierung und eingeschränkte Delegierung zu wechseln.

Weitere Informationen zum Protokoll Übergang finden Sie unter [Kerberos-Protokoll Übergang und eingeschränkte Delegierung](https://technet.microsoft.com/library/cc758097(v=ws.10).aspx).

### <a name="constrained-delegation"></a>Eingeschränkte Delegierung
Die eingeschränkte Delegierung bietet Administratoren die Möglichkeit, Anwendungs Vertrauensstellungs Grenzen anzugeben und zu erzwingen, indem Sie den Bereich einschränken, in dem Anwendungsdienste im Auftrag eines Benutzers agieren können. Sie können bestimmte Dienste angeben, von denen ein Computer, der für die Delegierung vertrauenswürdig ist, Ressourcen anfordern kann. Die Flexibilität, Autorisierungs Rechte für Dienste einzuschränken, trägt dazu bei, den Entwurf der Anwendungssicherheit zu verbessern, indem die Möglichkeiten der Gefährdung durch nicht vertrauenswürdige Dienste verringert

Weitere Informationen zur eingeschränkten Delegierung finden Sie unter [Übersicht über die eingeschränkte Kerberos-Delegierung](../kerberos/kerberos-constrained-delegation-overview.md).

## <a name="see-also"></a>Siehe auch
[Technische Übersicht über die Windows-Anmeldung und-Authentifizierung](https://technet.microsoft.com/library/dn269029.aspx)


