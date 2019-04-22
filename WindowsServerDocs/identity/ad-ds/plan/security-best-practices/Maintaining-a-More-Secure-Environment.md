---
ms.assetid: 8f994e2e-6c07-43f0-aef4-75f8b2c9a144
title: Beibehalten einer sicheren Umgebung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 554f841473d79edbac19ce4c53e99f5a43fa2b23
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59821701"
---
# <a name="maintaining-a-more-secure-environment"></a>Beibehalten einer sicheren Umgebung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetz Nummer zehn: Technologie ist kein Allheilmittel.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Wenn Sie eine verwaltbare, sichere Umgebung für Ihre geschäftskritischen Ressourcen erstellt haben, sollte Ihre den Fokus zu verschieben, um sicherzustellen, dass es sicher beibehalten wird. Obwohl Sie spezifische technische Sicherheitselemente zum Erhöhen der Sicherheits Ihrer AD DS-Installationen gewährt haben, Technologie allein nicht schützt eine Umgebung, in dem sie funktioniert nicht in Zusammenarbeit mit dem Unternehmen eine sichere, verwendbare Infrastruktur verwalten. Die allgemeinen Empfehlungen in diesem Abschnitt sollen als Richtlinien verwendet werden, die Sie verwenden können, um nicht nur effektive Sicherheit, sondern auch effektive Anwendungslebenszyklus-Verwaltung zu entwickeln.  
  
In einigen Fällen möglicherweise Ihre IT-Organisation bereits ein Schließen arbeitsbeziehungen Geschäftseinheiten, die erleichtern diese Empfehlungen zu implementieren. In Organisationen, in dem sie und Geschäftseinheiten sind nicht eng verbunden, müssen Sie möglicherweise rufen Sie zunächst die Führungskräfte für bemühungen zu fälschen eine engere Beziehung zwischen IT und Unternehmenseinheiten. Die [zusammenfassenden](../../../ad-ds/manage/component-updates/Executive-Summary.md) soll nützlich sein, wie ein eigenständiges Dokument für executive überprüfen und Entscheidungsträger in Ihrem Unternehmen verteilt werden kann.  
  
## <a name="creating-business-centric-security-practices-for-active-directory"></a>Erstellen geschäftskritische Sicherheitsmaßnahmen für Active Directory  
In der Vergangenheit wurde Informationstechnologie bei vielen Unternehmen als eine Supportstruktur und einer Kostenstelle angesehen. IT-Abteilungen häufig größtenteils von Business-Benutzern und die Interaktionen, die auf ein Anforderung / Antwort-Modell, in dem das Unternehmen von Ressourcen angeforderten, beschränkt getrennt wurden, und IT-geantwortet hat.  
  
Wie die Technologie weiterentwickelt und weitergegeben, hat die Vision "eines Computers für jeden Desktop" effektiv zur Übergabe für den Großteil der Welt kommen, und auch durch die Vielfalt an problemlos Technologien, die derzeit verfügbaren Weltrekordergebnisse wurde. Informationstechnologie ist nicht mehr eine Support-Funktion, sondern einer zentralen Geschäftsfunktion. Wenn Ihre Organisation nicht funktioniert weiterhin, wenn alle IT-Dienste nicht verfügbar waren, ist Ihrer Organisation Unternehmen, zumindest teilweise Informationstechnologie.  
  
Zum effektiven Kompromiss Wiederherstellungspläne erstellen, müssen IT-Dienste mit Geschäftseinheiten in Ihrer Organisation zum Identifizieren nicht nur der wichtigsten Komponenten der IT-Landschaft, aber die wichtigen Funktionen, die vom Unternehmen benötigten eng zusammenarbeiten. Durch die Ermittlung, was für Ihr Unternehmen als Ganzes wichtig ist, können Sie schwerpunktmäßig die Komponenten, die besonders wertvoll. Dies ist es nicht um eine Empfehlung für die Sicherheit der niedrigen Wert Systeme und Daten shirk. Vielmehr, wie Sie Servicelevels für Systembetriebszeit definieren, sollten Sie, dass die Definition von Maß an steuerungsmöglichkeiten für Sicherheit und Überwachung auf der Wichtigkeit des Medienobjekts basierend.  
  
Wenn Sie beim Erstellen einer aktuellen, sicheren und verwaltbaren Umgebung investiert haben, können Sie ändert den Fokus, effektiv verwalten und sicherstellen, dass Sie effektiv Lifecycle Management-Prozesse verfügen, die nur von bestimmt sind nicht IT, sondern durch das Unternehmen. Um dies zu erreichen, müssen Sie nicht nur für eine Partnerschaft mit dem Unternehmen, sondern auch das Unternehmen in "Besitzer" der Daten und Systeme in Active Directory zu investieren.  
  
Wenn Daten und Systeme in Active Directory ohne festgelegte, Unternehmensinhaber und IT-Besitzer eingeführt werden, ist gibt es keine klare Kette von Verantwortung für die Bereitstellung, Verwaltung, Überwachung, aktualisieren und schließlich Außerbetriebsetzen des Systems. Dies führt in Infrastrukturen der Ebene in denen Systeme, verfügbar machen von der Organisation, Risiko, aber darf nicht außer Betrieb genommen werden, da unklar, den Besitz ist. Zur effektiven Verwaltung des Lebenszyklus von Benutzern, Daten, Anwendungen und Systeme, die von Ihrer Installation von Active Directory verwaltet werden, sollten Sie die in diesem Abschnitt beschriebenen Prinzipien folgen.  
  
### <a name="assign-a-business-owner-to-active-directory-data"></a>Weisen Sie Eigentümer eines Unternehmens zu Active Directory-Daten  
Daten in Active Directory verfügen, dass ein identifizierten Geschäftsinhaber, also mit einer angegebenen Abteilung oder einem Benutzer, der den Kontaktpunkt für Entscheidungen über den Lebenszyklus des Medienobjekts ist. In einigen Fällen werden die Geschäftsinhaber von einer Komponente von Active Directory eine IT-Abteilung oder einen Benutzer. Infrastrukturkomponenten wie Domänencontroller, DHCP und DNS-Server und Active Directory werden in den meisten Fällen "Besitz" IT. Für Daten, die in AD DS zur Unterstützung des Unternehmens (z. B. neue Mitarbeiter, neue Anwendungen und neue Informationen Repositorys), einer entsprechenden zuständigen hinzukommt, sollten Einheit oder Benutzer mit den Daten zugeordnet werden.  
  
Sowohl bei Verwendung von Active Directory zum Aufzeichnen des Besitzes der Daten in das Verzeichnis, oder, ob Sie eine separate Datenbank zum Nachverfolgen von IT-Ressourcen implementieren, kein Benutzerkonto erstellt werden soll, sollten keine Server oder einer Arbeitsstation installiert werden und keine Anwendung bereitgestellt werden soll ohne einen angegebenen Besitzer des Datensatzes. Beim Einrichten des Besitzes von Systemen, nachdem sie in der Produktion bereitgestellt wurde, haben kann bestenfalls schwierig, und in einigen Fällen unmöglich sein. Aus diesem Grund sollten den Besitz zum Zeitpunkt festgelegt werden, die die Daten in Active Directory eingeführt werden.  
  
### <a name="implement-business-driven-lifecycle-management"></a>Implementieren von geschäftsorientierten Anwendungslebenszyklus-Verwaltung  
Verwaltung des Identitätslebenszyklus sollten für alle Daten in Active Directory implementiert werden. Z. B. wenn eine neue Anwendung in Active Directory-Domäne eingeführt wird, sollte, die geschäftlichen Besitzer der Anwendung in regelmäßigen Abständen erwartet werden, die durch die fortgesetzte Nutzung der Anwendung bestätigen. Wenn eine neue Version einer Anwendung veröffentlicht wird, ist Geschäftsinhaber von der Anwendung sollte informiert werden und muss entscheiden, ob und wann die neue Version implementiert werden.  
  
Wenn Inhaber eines Unternehmens entscheidet sich nicht für die Bereitstellung einer neuen Version einer Anwendung genehmigen, sollte diese Geschäftsinhaber auch des Datums benachrichtigt werden bei der aktuellen Version wird nicht mehr unterstützt und sollte zu bestimmen, ob die Anwendung wird zuständig sein außer Betrieb genommen oder ersetzt werden. Beibehalten von älteren Anwendungen, die ausgeführt wird und nicht unterstützten sollte sich nicht auf eine Option aus.  
  
Wenn in Active Directory-Benutzerkonten erstellt werden, deren Manager des Datensatzes benachrichtigt bei der objekterstellung und erforderlich, um die Gültigkeit des Kontos in regelmäßigen Abständen zu bestätigen. Durch die Implementierung eines Unternehmens gesteuerten Lebenszyklus und reguläre Nachweis der Gültigkeit der Daten, sind die Personen, die am besten zum Identifizieren von datenanomalien ausgestattet sind Personen, die die Daten überprüfen.  
  
Beispielsweise können Angreifer erstellen Benutzerkonten, die angezeigt werden, um gültige Benutzerkonten werden folgende Benennungskonventionen und objektplatzierung Ihrer Organisation. Um diese der kontoerstellung zu erkennen, können Sie tägliche Aufgabe implementieren, die alle Benutzerobjekte ohne einen entsprechenden zuständigen Besitzer zurückgibt, damit Sie die Konten untersuchen können. Wenn Angreifer Konten erstellen und der Inhaber eines Unternehmens zuweisen durch die Implementierung einer Aufgabe, die objekterstellung einer neuen an den Besitzer des entsprechenden zuständigen meldet, kann der Geschäftseigentümer schnell identifizieren, ob das Konto legitim ist.  
  
Implementieren Sie ähnliche Ansätze zur Sicherheits-und Verteilergruppen. Auch wenn einige Gruppen funktionalen Gruppen erstellt werden können IT, erstellen Sie jede Gruppe und einem angegebenen Besitzer an, Sie können alle Gruppen im Besitz eines angegebenen Benutzers abgerufen und muss der Benutzer die Gültigkeit des ihre Mitgliedschaft bestätigen. Ähnlich wie bei den Ansatz, die mit dem Benutzerkonto erstellen, können Sie reporting gruppenänderungen an den Besitzer des entsprechenden zuständigen auslösen. Die weitere Routine, die es für den Inhaber eines Unternehmens bestätigen, dass Sie sind, um Anomalien zu identifizieren, die Prozess- oder tatsächlichen Kompromittierung hinweisen können die Gültigkeit oder unerheblichkeit der Daten in Active Directory, die besser darauf vorbereitet wird.  
  
### <a name="classify-all-active-directory-data"></a>Alle Active Directory-Daten klassifizieren  
Zusätzlich zur Erfassung der Inhaber eines Unternehmens für alle Active Directory-Daten zu dem Zeitpunkt, die sie zum Verzeichnis hinzugefügt wird, sollten Sie auch Geschäftsinhaber zu Klassifizierung für die Daten anfordern. Z. B. wenn eine Anwendung unternehmenskritischen Daten gespeichert werden, sollte die Geschäftsinhaber die Anwendung daher gemäß Ihrer Organisation Classification Infrastructure, FCI bezeichnen.  
  
Einige Organisationen Implementieren von Richtlinien für die datenklassifizierung dieser Bezeichnung gemäß den Schaden, den Offenlegung von Daten fallen würde, wenn es gestohlen oder verfügbar gemacht wurden. Andere Organisationen Implementieren von datenklassifizierung, Bezeichnungen von Bedeutung, durch die Anforderungen für den Zugriff und Aufbewahrung. Unabhängig von der Klassifizierung Datenmodell in Ihrer Organisation verwendet sollten Sie sicherstellen, dass Sie die Klassifizierung anwenden, um Active Directory-Daten, nicht nur für "file"-Daten sind. Wenn es sich bei dem Konto eines Benutzers ein VIP-Konto handelt, sollten in Ihrer Medienobjekt Klassifikation Datenbank identifiziert werden (, ob Sie dies über die Verwendung von Attributen für die Objekte in AD DS implementieren, oder ob Sie separate Medienobjekt Klassifikation Datenbanken bereitstellen).  
  
In Ihrem Datenmodell für die Klassifizierung sollten Sie die Klassifizierung für AD DS-Daten wie die folgende einschließen.  
  
### <a name="systems"></a>Systeme  
Sie sollten nicht nur Daten, sondern auch deren Einwohnerzahlen Server klassifiziert werden. Für jeden Server, sollten Sie wissen, welches Betriebssystem installiert ist, welche allgemeinen Rollen, die der Server bereitstellt, welche Anwendungen ausgeführt werden auf dem Server, der IT-Besitzer des Datensatzes und der Geschäftsinhaber des Datensatzes, sofern zutreffend. Für alle Daten oder Anwendungen, die auf dem Server ausgeführt werden fordern Sie von Klassifizierung und der Server muss geschützt werden, gemäß den Anforderungen für arbeitsauslastungen, die es unterstützt und die Klassifizierungen, die auf das System und die Daten angewendet. Sie können auch von Servern mit der die Klassifizierung ihrer Workloads, gruppieren, wodurch Sie schnell die Server zu identifizieren, die die am ehesten überwachten und die meisten repräsentative Motoröltemperatur konfiguriert werden sollen.  
  
### <a name="applications"></a>Anwendungen  
Klassifizieren Sie Anwendungen durch Funktionen, die (was sie tun), Benutzerbasis (die die Anwendungen verwendet werden) und das Betriebssystem auf dem sie ausgeführt. Sie sollten Einträge beibehalten, die Versionsinformationen, des Status von Sicherheitspatches und andere relevante Informationen enthalten. Sie sollten auch Anwendungen von den Typen von Daten klassifizieren, die sie wie zuvor beschrieben behandeln.  
  
### <a name="users"></a>Benutzer  
Ob Sie "VIP" Benutzer "," kritische Konten anrufen oder eine andere Bezeichnung verwenden, sollten die Konten in Ihrer Active Directory-Installationen, die am ehesten auf das Ziel von Angreifern gekennzeichnet und überwacht werden. In den meisten Organisationen ist es einfach nicht möglich, alle Aktivitäten aller Benutzer überwachen. Wenn Sie identifizieren die kritischen Konten in Ihrer Active Directory-Installation sind, können Sie jedoch diese Konten für Änderungen, die weiter oben in diesem Dokument beschrieben überwachen.  
  
Sie können auch beginnen, eine Datenbank mit "Erwartetes Verhalten" für diese Konten zu erstellen, wie Sie die Konten überwachen. Wenn Sie feststellen, dass eine bestimmte Führungskräfte verwendet beispielsweise seiner sichere Arbeitsstation auf geschäftskritische Daten zugreifen aus seinem Büro und aus seiner Heimat, jedoch selten an anderen Speicherorten, wenn Sie versuchen, auf Daten zugreifen, mit seinem Konto eines nicht autorisierten Computers finden Sie unter oder Speicherort auf der Hälfte der Angestellte wissen ist nicht aktuell gespeichert, Sie schnell identifizieren und untersuchen Sie dieses ungewöhnlichen Verhaltens können.  
  
Geschäftsinformationen in Ihre Infrastruktur integrieren, können Sie diese Informationen für Business um falsch positive Ergebnisse zu erkennen. Wenn in einem Kalender executive Travel aufgezeichnet wird, die für IT-Mitarbeiter, die für die Überwachung der umgebungs verantwortlich ist, können Sie z. B. versucht, eine Verbindung mit bekannten Speicherorten die Führungskräfte korrelieren.  
  
Angenommen, ein befindet sich normalerweise in Chicago und eine sichere Arbeitsstation Zugriff auf geschäftskritische Daten aus seinem Schreibtisch verwendet und ein Ereignis wird ausgelöst, durch einen fehlgeschlagenen Versuch für den Datenzugriff über eine nicht gesicherte Workstation, die sich in München befinden. Wenn Sie sehen, stellen Sie sicher, dass die derzeit in Atlanta dabei ist, können Sie beheben des Ereignisses wenden Sie sich an der Angestellte oder der Führungskraft-Assistenten, um festzustellen, ob der Fehler beim Zugriff auf das Ergebnis der Angestellte Versäumnis, verwenden Sie die sichere Arbeitsstation hat Zugriff auf die Daten. Erstellen Sie ein Programm, die in beschriebenen Ansätze verwendet [Planen der Gefährdung](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md), Sie können beginnen, erstellen Sie eine Datenbank mit dem erwarteten Verhalten für die meisten "important" Konten in Ihrer Active Directory-Installation, die Möglicherweise können Sie weitere schnell erkennen und reagieren auf Angriffe.  
  


