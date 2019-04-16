---
ms.assetid: 8f994e2e-6c07-43f0-aef4-75f8b2c9a144
title: Verwalten einer sicheren Umgebung
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7d471ee2ba73ef7425464e1aa928c75318f7dd82
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="maintaining-a-more-secure-environment"></a>Verwalten einer sicheren Umgebung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

*Recht Zahl zehn: Technologie ist kein Allheilmittel.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Bei der Erstellung einer verwaltbaren und sicheren Umgebung für Ihre unternehmenskritischen Objekte sollten konzentrieren Sie sich ändern, um sicherzustellen, dass sie sicher verwaltet wird. Auch wenn Sie bestimmte technische Sicherheitselemente zum Erhöhen der Sicherheit von AD DS-Installationen erhalten haben, schützen Technologie allein keine Umgebung, in dem es funktioniert nicht in Zusammenarbeit mit dem Unternehmen um eine sichere, benutzerfreundliche Infrastruktur zu verwalten. Die allgemeine Empfehlungen in diesem Abschnitt sollen als Richtlinien verwendet werden, die Sie verwenden können, nicht nur wirksame, aber effektives Lifecycle Management zu entwickeln.  
  
In einigen Fällen möglicherweise Ihre IT-Organisation bereits über eine enge Beziehung der Arbeiten mit Geschäftseinheiten verfügen, implementieren diese Empfehlungen vereinfachen wird. In Organisationen, in dem es und Geschäftseinheiten nicht eng verbunden sind, müssen Sie möglicherweise zunächst Führungskräfte für zu fälschen eine näher Beziehung zwischen IT und Unternehmenseinheiten. Die [Zusammenfassung](../../../ad-ds/manage/component-updates/Executive-Summary.md) soll hilfreich, da kein eigenständiges Dokument zur executive überprüfen und ihn für Entscheidungsträger in Ihrer Organisation verteilt werden kann.  
  
## <a name="creating-business-centric-security-practices-for-active-directory"></a>Erstellen von Business-orientierte Sicherheitsmaßnahmen für Active Directory  
In der Vergangenheit wurde Informationstechnologie in vielen Organisationen als eine Supportstruktur und eine Kostenstelle angezeigt. IT-Abteilungen wurden häufig größtenteils getrennt von Business-Benutzer und -Interaktionen beschränkt auf eine Anforderung / Antwort-Modell, in dem das Unternehmen Ressourcen angefordert, und IT geantwortet.  
  
Als Technologie weiterentwickelt und übertragen, hat die Vision "eines Computers auf jedem Desktop" effektiv für einen Großteil der ganzen Welt übergeben werden, und auch durch die Breite Palette an leicht zugänglichen Technologien erhältliche Weltrekordergebnisse wurde. IT ist nicht mehr eine Support-Funktion, sondern eine zentrale betriebliche Funktion. Wenn Ihre Organisation nicht fortgesetzt werden konnte, funktioniert, wenn alle IT-Dienste nicht verfügbar waren, ist Ihre Organisation mindestens im Teil Informationstechnologie.  
  
Zum effektiven Kompromiss Recovery-Pläne erstellen, müssen IT-Dienste eng mit Geschäftseinheiten in Ihrer Organisation nicht nur die wichtigsten Komponenten der IT-Landschaft, aber die wichtigen Funktionen, die vom Unternehmen benötigten identifizieren. Durch die Ermittlung, was für Ihre Organisation als Ganzes wichtig ist, können Sie sich konzentrieren zum Sichern von Komponenten, die den größten Nutzen sind. Dies stellt keine Empfehlung, die Sicherheit der niedrigen Wert Systeme und Daten shirk. Stattdessen wie Sie Servicelevels für Systembetriebszeit definieren, sollten Sie Ebenen der Sicherheitskontrolle Definition und Überwachung auf der Wichtigkeit der Ressource basiert.  
  
Wenn Sie beim Erstellen einer Umgebung aktuellen, sicheren und verwaltbaren investiert haben, können Sie den Fokus verschieben, effektiv verwaltet und sicherstellen, dass Sie effektive Lifecycle Management-Prozesse, die nur von bestimmt sind nicht IT, sondern durch das Unternehmen. Um dies zu erreichen, müssen Sie nicht nur an partner mit dem Unternehmen, sondern das Unternehmen in "Besitzer" der Daten und Systeme in Active Directory zu investieren.  
  
Wenn Daten und Systeme ohne festgelegten Besitzer, Geschäftsinhaber und IT-Besitzer in Active Directory eingeführt werden, ist es keine klare Kette Verantwortung für die Bereitstellung, Verwaltung, Überwachung, aktualisieren und schließlich Außerbetriebsetzen des Systems. Dies führt zu Infrastrukturen, in denen Systeme Risiken die Organisation verfügbar zu machen und können nicht außer Betrieb gesetzt werden, da Besitz unklar ist. Um den Lebenszyklus der Benutzer, Daten, Anwendungen und die Installation von Active Directory verwalteten Systeme effektiv zu verwalten, sollten Sie die in diesem Abschnitt beschriebenen Prinzipien folgen.  
  
### <a name="assign-a-business-owner-to-active-directory-data"></a>Active Directory-Daten einen geschäftlichen Besitzer zuweisen  
Daten in Active Directory muss einen identifizierten geschäftlichen Besitzer, d. h. einer angegebenen Abteilung oder Benutzer, der Kontaktpunkt für Entscheidungen über den Lebenszyklus der Ressource ist. In einigen Fällen werden die geschäftlichen Besitzer einer Komponente von Active Directory eine IT-Abteilung oder einen Benutzer. Komponenten wie Domänencontroller, DHCP und DNS-Server und Active Directory-Infrastruktur werden wahrscheinlich "Besitz" IT. Für Daten, die in AD DS zur Unterstützung des Unternehmens (z. B. neue Mitarbeiter, neue Anwendungen und neue Informationen Repositories), einem bestimmten Unternehmen ist sollten Einheit oder Benutzer mit den Daten verknüpft werden.  
  
Ob Sie Active Directory verwenden, um Besitz von Daten in das Verzeichnis, oder implementieren Sie eine separate Datenbank für die Verfolgung von IT-Ressourcen, kein Benutzerkonto erstellt werden soll, sollte keine Server oder einer Arbeitsstation installiert werden und keine Anwendung bereitgestellt werden soll, ohne einen bestimmten Besitzer des Datensatzes. Bei dem Versuch, den Besitz von Systemen herstellen, nachdem sie in der produktionsumgebung bereitgestellt wurden, haben kann am besten eine große Herausforderung, und in einigen Fällen nicht möglich sein. Aus diesem Grund sollten Besitz Zeitpunkt hergestellt werden, die die Daten in Active Directory eingeführt werden.  
  
### <a name="implement-business-driven-lifecycle-management"></a>Implementieren Sie unternehmensspezifischen Lifecycle Management  
Verwaltung des Lebenszyklus sollte für alle Daten in Active Directory implementiert werden. Z. B. bei eine neue Anwendung in einer Active Directory-Domäne eingeführt wird, sollte die geschäftlichen Besitzer der Anwendung in regelmäßigen Abständen erwartet, die fortgesetzte Verwendung der Anwendung abschließen. Wenn eine neue Version einer Anwendung veröffentlicht wird, wird die Anwendung geschäftlichen Besitzer sollte informiert werden und sollten entscheiden, ob und wann die neue Version implementiert werden.  
  
Entscheidet sich Eigentümer eines Unternehmens nicht für die Bereitstellung einer neuen Version einer Anwendung zu genehmigen, sollten die geschäftlichen Besitzer des Datums auch benachrichtigt werden, wenn die aktuelle Version nicht mehr unterstützt werden, und ermitteln, ob die Anwendung außer Betrieb gesetzt oder ersetzt werden sollte. Und ältere Anwendung ausgeführt wird und nicht unterstützte zu halten, sollten keine Option.  
  
Wenn Benutzerkonten in Active Directory erstellt werden, sollte Abteilungsleiter Datensatz zur Erstellung des Objekts benachrichtigt und erforderlich, um die Gültigkeit des Kontos in regelmäßigen Abständen nachzuweisen. Durch die Implementierung eines Unternehmens-Lebenszyklus und als Nachweis der Gültigkeit der Daten gesteuert, sind die Personen, die am besten zum Identifizieren von Anomalien in den Daten ausgestattet sind Personen, die die Daten zu überprüfen.  
  
Beispielsweise können Angreifer Erstellen von Benutzerkonten, die angezeigt werden, um gültige Benutzerkonten werden folgenden Benennungskonventionen Ihrer Organisation und die Objekt-Platzierung. So erkennen Sie diese der kontoerstellung bemerken, können Sie tägliche Aufgabe implementieren, die alle Benutzerobjekte ohne Eigentümer eines bestimmten Unternehmens zurückgegeben, damit Sie die Konten untersuchen können. Wenn Angreifer Konten erstellen und weisen Sie der Eigentümer eines Unternehmens, durch die Implementierung einer Aufgabe, die objekterstellung einer neuen an den Besitzer der dafür vorgesehenen Business meldet, kann der Besitzer eines Unternehmens, ob das Konto legitim ist schnell identifizieren.  
  
Sie sollten ähnliche Ansätze für Sicherheits-und Verteilergruppen implementieren. Obwohl einige Gruppen Funktionsgruppen erstellt werden können IT durch jede Gruppe mit einem Besitzer erstellt haben, können alle Gruppen, die im Besitz eines bestimmten Benutzers abrufen und muss der Benutzer die Gültigkeit ihre Mitgliedschaft nachzuweisen. Ähnlich wie Ansatz wird bei der Erstellung von Benutzerkonten, können Sie reporting Gruppe Änderungen an der dafür vorgesehenen Geschäftsinhaber auslösen. Die weitere Routine, die es wird für den Eigentümer eines Unternehmens, der Gültigkeit oder Ungültigkeit von Daten in Active Directory, die mehr ausgestattet nachzuweisen, dass Sie sind Anomalien zu identifizieren, die Prozess- oder tatsächliche Kompromittierung hinweisen können.  
  
### <a name="classify-all-active-directory-data"></a>Alle Active Directory-Daten klassifizieren  
Zusätzlich zur Aufzeichnung der Eigentümer eines Unternehmens für alle Active Directory-Daten zu dem Zeitpunkt, die sie in das Verzeichnis hinzugefügt wird, sollten Sie auch Geschäftsinhaber Klassifizierung für die Daten bereitstellen voraussetzen. Z. B. wenn eine Anwendung geschäftskritische Daten gespeichert werden, sollten den geschäftlichen Besitzer die Anwendung als solche gemäß der Infrastruktur der Organisation Klassifizierung beschriften.  
  
Einige Unternehmen implementieren Policies zur Klassifizierung von Daten die Bezeichnung Daten gemäß den Schaden verursacht, den Offenlegung von Daten verursachen würde, wenn es gestohlen oder verfügbar gemacht wurden. Anderen Organisationen Implementieren von Bedeutung, zugriffsanforderungen und Aufbewahrung Beschriftungen Daten Klassifizierung von Daten. Unabhängig von der Klassifizierung Datenmodell in Ihrer Organisation verwendet sollten Sie sicherstellen, dass Sie die Klassifizierung anwenden, um Active Directory-Daten, nicht nur auf "file" Daten sind. Wenn dem Konto eines Benutzers eine VIP-Konto ist, sollte in der Anlage Klassifizierung Datenbank angegeben werden (, ob Sie dies über die Verwendung von Attributen für die Objekte in AD DS implementieren, oder ob Sie separate Ressource Klassifizierung Datenbanken bereitstellen).  
  
In Ihrem Datenmodell Ihren Klassifizierung sollten Sie die Klassifizierung für AD DS-Daten wie die folgenden einschließen.  
  
### <a name="systems"></a>Systeme  
Sie sollten nicht nur Daten, sondern auch ihre Server Einwohnerzahlen zu klassifizieren. Für jeden Server, sollten Sie wissen, welches Betriebssystem installiert ist, welche allgemeinen Rollen der Server bereitstellt, welche Anwendungen ausgeführt werden auf dem Server, der IT-Besitzer des Eintrags und den geschäftlichen Besitzer der Datensatz, sofern zutreffend. Für alle Daten oder Anwendungen, die auf dem Server ausgeführt Sie sollten die Klassifizierung erfordern, und muss der Server gesichert werden gemäß den Anforderungen für arbeitsauslastungen, die sie unterstützt und die Klassifizierungen, die auf dem System und die Daten angewendet. Sie können auch Server durch die Klassifizierung von Arbeitslasten, gruppieren, mit der Sie schnell auf die Server identifizieren, die die am ehesten überwachten und die meisten repräsentative Motoröltemperatur konfiguriert werden soll.  
  
### <a name="applications"></a>Anwendungen  
Sie sollten klassifizieren Anwendungen nach Funktionen (was sie tun), Benutzerbasis (die die Anwendungen verwendet wird) und das Betriebssystem auf dem sie ausgeführt werden. Sollten Sie die Datensätze beibehalten, die Versionsinformationen Patchstatus und weiteren relevanten Informationen enthalten. Sie sollten auch Anwendungen von den Typen der Daten klassifizieren, die sie verarbeiten, wie zuvor beschrieben.  
  
### <a name="users"></a>Benutzer  
Ob Sie "VIP" Benutzer "," kritische Konten anrufen oder eine andere Bezeichnung verwenden, sollte die Konten in Ihrer Active Directory-Installationen, die am wahrscheinlichsten Ziel von Angreifern sein gekennzeichnet und überwacht werden. In den meisten Unternehmen ist es einfach nicht möglich, alle Aktivitäten aller Benutzer zu überwachen. Wenn Sie die wichtigen Konten in Ihrer Active Directory-Installation zu identifizieren sind, können Sie diese Konten für Änderungen, wie weiter oben in diesem Dokument beschrieben überwachen.  
  
Sie können auch beginnen, um eine Datenbank mit "erwartete Verhalten" für diese Konten zu erstellen, wie Sie die Konten überwachen. Z. B. Wenn Sie feststellen, dass einer bestimmten Executive seine gesicherten Arbeitsstation verwendet, um Zugriff auf Unternehmensdaten von seinem Arbeitsplatz und seine Startseite, aber nur selten an anderen Speicherorten, wenn angezeigt wird versucht, den Zugriff auf Daten mit seinem Konto von einem nicht autorisierten Computer oder an einem Ort in der Mitte auf, wissen Sie, dass der Vorgesetzte momentan nicht befindet, können Sie schneller zu identifizieren und diese anormale Verhalten untersuchen.  
  
Durch die Integration von Unternehmensdaten in die Infrastruktur, können Sie die Geschäftsinformationen um falsch positive Ergebnisse identifizieren. Wenn Führungskräfte Reise in einem Kalender, die für IT-Mitarbeiter verantwortlich gespeichert ist für die Überwachung der Umgebung zugänglich ist, können Sie z. B. versucht, eine Verbindung mit der Führungskräfte bekannter Positionen korrelieren.  
  
Angenommen, Executive ein befindet sich normalerweise in Chicago und mithilfe eine sichere Arbeitsstation Schreibtisch geschäftskritische Daten zugreifen, und ein Ereignis wird ausgelöst, indem Sie einen Fehler beim Zugriff auf die Daten aus einer unsicheren Arbeitsstation in Atlanta befinden. Wenn Sie können überprüfen, ob der Vorgesetzte in Atlanta aktuell ist, können Sie das Ereignis beheben, wenden Sie sich an den Vorgesetzter oder der Vorgesetzte-Assistenten, um festzustellen, ob der Fehler beim Zugriff auf das Ergebnis der Vorgesetzte die gesicherte Arbeitsstation zu verwenden, um Zugriff auf die Daten vergessen wurde. Erstellen Sie ein Programm, das die folgenden Abschnitten beschrieben verwendet [für Sicherheitsgefährdungen](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md), können Sie die Datenbank der erwartete Verhalten für "wichtigste" Konten in Ihrer Active Directory-Installation, die potenziell Sie schneller helfen erkennen und auf Angriffe reagieren mit beginnen.  
  


