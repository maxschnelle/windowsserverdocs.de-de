---
ms.assetid: 8f994e2e-6c07-43f0-aef4-75f8b2c9a144
title: Beibehalten einer sicheren Umgebung
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a22b1a0d776540e8ee2f2c223a1087bd88adaa47
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80821173"
---
# <a name="maintaining-a-more-secure-environment"></a>Beibehalten einer sicheren Umgebung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Recht Nummer 10: die Technologie ist kein Allheilmittel.* - [10 unveränderliche Gesetze der Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Wenn Sie eine verwaltbare, sichere Umgebung für Ihre wichtigen Geschäftsressourcen erstellt haben, sollten Sie sich mit dem Schwerpunkt befassen, um sicherzustellen, dass Sie sicher verwaltet werden. Obwohl Sie über spezielle technische Kontrollen verfügen, um die Sicherheit Ihrer AD DS-Installationen zu erhöhen, bietet Technologie allein keine Umgebung, in der Sie nicht in Zusammenarbeit mit dem Unternehmen zusammenarbeitet, um eine sichere, nutzbare Infrastruktur zu erhalten. Die Empfehlungen in diesem Abschnitt sind für die Verwendung als Richtlinien gedacht, mit denen Sie nicht nur eine effektive Sicherheit, sondern auch eine effektive Lebenszyklus Verwaltung entwickeln können.  
  
In einigen Fällen verfügt Ihre IT-Organisation möglicherweise bereits über eine enge Arbeitsbeziehung mit Geschäftseinheiten, was die Implementierung dieser Empfehlungen erleichtert. In Organisationen, in denen IT-und Geschäftseinheiten nicht eng verbunden sind, müssen Sie zunächst eine Executive-sponsoringanforderung erwerben, um eine engere Beziehung zwischen IT und Geschäftseinheiten herzustellen. Die [Zusammenfassung des Executive](../../../ad-ds/manage/component-updates/Executive-Summary.md) ist als eigenständiges Dokument für die Executive Review gedacht und kann an Entscheidungsträger in Ihrer Organisation verteilt werden.  
  
## <a name="creating-business-centric-security-practices-for-active-directory"></a>Erstellen von geschäftsorientierten Sicherheitsmethoden für Active Directory  
In der Vergangenheit wurde die Informationstechnologie in vielen Organisationen als Supportstruktur und Kostenstelle angesehen. IT-Abteilungen waren häufig größtenteils von geschäftlichen Benutzern getrennt, und Interaktionen waren auf ein Anforderungs Antwort Modell beschränkt, bei dem das Unternehmen Ressourcen angefordert hat und reagierte.  
  
Da die Technologie weiterentwickelt und sich weiterentwickelt hat, ist die Vision "ein Computer auf jedem Desktop" für einen Großteil der Welt erfolgreich und sogar durch die große Bandbreite an leicht zugänglichen Technologien verfügbar, die heute verfügbar sind. Die Informationstechnologie ist keine Support Funktion mehr, sondern eine zentrale Geschäftsfunktion. Wenn Ihre Organisation nicht mehr funktionieren konnte, wenn alle IT-Dienste nicht verfügbar waren, ist das Unternehmen der Organisation zumindest teilweise eine Informationstechnologie.  
  
Um effektive Wiederherstellungs Pläne für Kompromisse zu erstellen, müssen IT-Dienste eng mit Geschäftseinheiten in Ihrer Organisation zusammenarbeiten, um nicht nur die wichtigsten Komponenten der IT-Landschaft, sondern die für das Unternehmen erforderlichen wichtigen Funktionen zu identifizieren. Wenn Sie identifizieren, was für Ihre Organisation als Ganzes wichtig ist, können Sie sich auf die Sicherung der Komponenten konzentrieren, die den größten Nutzen haben. Dies ist keine Empfehlung, um die Sicherheit von Systemen und Daten mit geringem Wert zu entziehen. Vielmehr sollten Sie, wie Sie Dienst Ebenen für die Betriebszeit des Systems definieren, die Sicherheitskontrolle und die Überwachung basierend auf der Wichtigkeit von Assets definieren.  
  
Wenn Sie in das Erstellen einer aktuellen, sicheren und verwaltbaren Umgebung investiert haben, können Sie den Fokus auf die effektive Verwaltung verlagern und sicherstellen, dass Sie über effektive Lebenszyklus Verwaltungsprozesse verfügen, die nicht nur durch IT, sondern durch das Unternehmen bestimmt werden. Um dies zu erreichen, müssen Sie nicht nur mit dem Unternehmen Partnergemäß arbeiten, sondern auch das Unternehmen in den Besitz von Daten und Systemen in Active Directory investieren.  
  
Wenn Daten und Systeme in Active Directory ohne designierte Besitzer, Geschäftsinhaber und IT-Besitzer eingeführt werden, gibt es keine klare Verantwortungskette für die Bereitstellung, Verwaltung, Überwachung und Aktualisierung, und das System wird schließlich außer Betrieb gesetzt. Dies führt zu Infrastrukturen, in denen Systeme die Organisation zum Risiko machen, aber nicht außer Betrieb gesetzt werden können, weil der Besitz unklar ist. Befolgen Sie die in diesem Abschnitt beschriebenen Prinzipien, um den Lebenszyklus der Benutzer, Daten, Anwendungen und Systeme, die von der Active Directory Installation verwaltet werden, effektiv zu verwalten.  
  
### <a name="assign-a-business-owner-to-active-directory-data"></a>Active Directory Daten einen Geschäfts Besitzer zuweisen  
Daten in Active Directory sollten einen identifizierten Geschäfts Besitzer haben, d. h. eine angegebene Abteilung oder ein Benutzer, der der Kontaktpunkt für Entscheidungen über den Lebenszyklus des Assets ist. In einigen Fällen ist der Geschäftsinhaber einer Komponente von Active Directory eine IT-Abteilung oder ein Benutzer. Infrastrukturkomponenten, wie z. b. Domänen Controller, DHCP-und DNS-Server, und Active Directory werden wahrscheinlich von ihr als "Besitzer" verwendet. Für Daten, die AD DS zur Unterstützung des Unternehmens hinzugefügt werden (z. b. neue Mitarbeiter, neue Anwendungen und neue Informations Depots), sollte eine bestimmte Geschäftseinheit oder ein bestimmtes Benutzer mit den Daten verknüpft werden.  
  
Unabhängig davon, ob Sie Active Directory verwenden, um den Besitz von Daten im Verzeichnis aufzuzeichnen, oder ob Sie eine separate Datenbank zum Nachverfolgen von IT-Ressourcen implementieren, kein Benutzerkonto erstellt werden muss, kein Server oder keine Arbeitsstation installiert werden muss und keine Anwendung ohne einen festgelegten Besitzer des Datensatzes bereitgestellt werden soll. Der Versuch, den Besitz von Systemen nach der Bereitstellung in der Produktion einzurichten, kann in manchen Fällen eine Herausforderung darstellen. Daher sollte der Besitz zu dem Zeitpunkt eingerichtet werden, zu dem die Daten in Active Directory eingeführt werden.  
  
### <a name="implement-business-driven-lifecycle-management"></a>Implementieren der geschäftsorientierten Lebenszyklus Verwaltung  
Die Lebenszyklus Verwaltung sollte für alle Daten in Active Directory implementiert werden. Wenn z. b. eine neue Anwendung in eine Active Directory Domäne eingeführt wird, sollte der Geschäfts Besitzer der Anwendung in regelmäßigen Abständen die fortgesetzte Verwendung der Anwendung bestätigen. Wenn eine neue Version einer Anwendung veröffentlicht wird, sollte der Geschäftsinhaber der Anwendung informiert werden und entscheiden, ob und wann die neue Version implementiert wird.  
  
Wenn ein Geschäftsinhaber entscheidet, die Bereitstellung einer neuen Version einer Anwendung nicht zu genehmigen, sollte dieser Geschäftsinhaber auch über das Datum benachrichtigt werden, an dem die aktuelle Version nicht mehr unterstützt wird, und für die Festlegung verantwortlich sein soll, ob die Anwendung außer Betrieb genommen oder ersetzt wird. Das Ausführen von Legacy Anwendungen und die nicht unterstützte Option sollte keine Option sein.  
  
Wenn Benutzerkonten in Active Directory erstellt werden, sollten ihre Vorgesetzten von Datensätzen bei der Objekt Erstellung benachrichtigt werden, und Sie müssen in regelmäßigen Abständen die Gültigkeit des Kontos bestätigen. Durch die Implementierung eines Geschäfts-und regulären Nachweis der Gültigkeit der Daten sind die Personen, die am besten zur Identifizierung von Anomalien in den Daten gerüstet sind, die Personen, die die Daten überprüfen.  
  
Beispielsweise können Angreifer Benutzerkonten erstellen, die als gültige Konten angezeigt werden, die den Benennungs Konventionen Ihrer Organisation und der Objekt Platzierung folgen. Um diese Konto Erstellungen zu erkennen, können Sie eine tägliche Aufgabe implementieren, die alle Benutzer Objekte ohne einen designierten Geschäfts Besitzer zurückgibt, damit Sie die Konten untersuchen können. Wenn Angreifer Konten erstellen und einen Geschäfts Besitzer zuweisen, kann der Geschäftsinhaber schnell ermitteln, ob das Konto legitim ist, indem er eine Aufgabe implementiert, die die Erstellung eines neuen Objekts an den designierten Geschäftsinhaber meldet.  
  
Sie sollten ähnliche Ansätze für Sicherheits-und Verteiler Gruppen implementieren. Obwohl es sich bei einigen Gruppen möglicherweise um funktionale Gruppen handelt, die von der IT erstellt werden, können Sie alle Gruppen, die im Besitz eines bestimmten Benutzers sind, abrufen und den Benutzer auffordern, die Gültigkeit der Mitgliedschaften zu bestätigen. Ähnlich wie bei der Erstellung des Benutzerkontos können Sie Änderungen an der Berichterstattungs Gruppe für den designierten Geschäftsinhaber veranlassen. Umso mehr Routine ist es, dass ein Geschäftsinhaber der Gültigkeit oder Invalidität von Daten in Active Directory attestiert wird. umso besser ist es, dass Sie Anomalien identifizieren, die auf Prozessfehler oder tatsächliche Gefährdung hindeuten können.  
  
### <a name="classify-all-active-directory-data"></a>Alle Active Directory Daten klassifizieren  
Zusätzlich zum Aufzeichnen eines Geschäfts Besitzers für alle Active Directory Daten zu dem Zeitpunkt, zu dem Sie dem Verzeichnis hinzugefügt werden, sollten Sie auch Geschäftsinhaber benötigen, um Klassifizierung für die Daten bereitzustellen. Wenn beispielsweise eine Anwendung geschäftskritische Daten speichert, sollte der Geschäftsinhaber die Anwendung entsprechend der Klassifizierungs Infrastruktur Ihrer Organisation als solche Bezeichnung bezeichnen.  
  
Einige Organisationen implementieren Richtlinien für die Datenklassifizierung, die Daten entsprechend der Beschädigung bezeichnen, die eine offen setzung der Daten verursachen würde, wenn Sie gestohlen oder verfügbar gemacht wird. Andere Organisationen implementieren die Datenklassifizierung, die Daten nach Wichtigkeit, nach Zugriffs Anforderungen und nach Beibehaltung bezeichnet. Unabhängig vom Daten Klassifizierungs Modell, das in Ihrer Organisation verwendet wird, sollten Sie sicherstellen, dass Sie die Klassifizierung auf Active Directory Daten anwenden können, nicht nur auf "Datei" Daten. Wenn das Konto eines Benutzers ein VIP-Konto ist, sollte es in der assetklassifizierungs-Datenbank identifiziert werden (unabhängig davon, ob dies mithilfe von Attributen für die Objekte in AD DS implementiert wird oder ob separate Asset-Klassifizierungs Datenbanken bereitgestellt werden).  
  
In Ihrem Daten Klassifizierungs Modell sollten Sie die Klassifizierung für AD DS Daten wie die folgenden einschließen.  
  
### <a name="systems"></a>Systems  
Sie sollten nicht nur Daten klassifizieren, sondern auch deren Server Population. Sie sollten für jeden Server wissen, welches Betriebssystem installiert ist, welche allgemeinen Rollen der Server bereitstellt, welche Anwendungen auf dem Server ausgeführt werden, der IT-Besitzer des Datensatzes und den Geschäftsinhaber des Datensatzes (falls zutreffend). Für alle Daten oder Anwendungen, die auf dem Server ausgeführt werden, benötigen Sie eine Klassifizierung, und der Server sollte gemäß den Anforderungen für die unterstützten Workloads und die auf das System und die Daten geltenden Klassifizierungen gesichert werden. Sie können Server auch nach der Klassifizierung ihrer Arbeits Auslastungen gruppieren, sodass Sie schnell die Server identifizieren können, die am ehesten überwacht und am ehesten konfiguriert werden sollen.  
  
### <a name="applications"></a>Anwendungen  
Sie sollten Anwendungen nach Funktionalität klassifizieren (was Sie tun), Benutzerbasis (die die Anwendungen verwendet) und das Betriebssystem, auf dem Sie ausgeführt werden. Sie sollten Datensätze verwalten, die Versionsinformationen, den Patchstatus und andere relevante Informationen enthalten. Sie sollten Anwendungen auch nach den Typen von Daten klassifizieren, die Sie verarbeiten, wie zuvor beschrieben.  
  
### <a name="users"></a>Benutzer  
Unabhängig davon, ob Sie als "VIP"-Benutzer oder als kritische Konten bezeichnet werden oder eine andere Bezeichnung verwenden, sollten die Konten in Ihren Active Directory Installationen, die höchstwahrscheinlich von Angreifern betroffen sind, markiert und überwacht werden. In den meisten Organisationen ist es einfach nicht möglich, alle Aktivitäten aller Benutzer zu überwachen. Wenn Sie jedoch die kritischen Konten in der Active Directory-Installation identifizieren können, können Sie diese Konten auf Änderungen überwachen, wie weiter oben in diesem Dokument beschrieben.  
  
Sie können auch beginnen, eine Datenbank mit "erwartetem Verhalten" für diese Konten zu erstellen, während Sie die Konten überwachen. Wenn Sie z. b. feststellen, dass ein bestimmter Executive seine gesicherte Arbeitsstation verwendet, um von seinem Büro und von seinem Zuhause aus auf geschäftskritische Daten zuzugreifen, aber nur selten von anderen Standorten aus, wenn Sie versuchen, auf Daten zuzugreifen, indem er sein Konto auf einem nicht autorisierten Computer oder einen Standort in der Nähe eines Standorts auf der ganzen Welt verwendet.  
  
Wenn Sie Geschäftsinformationen in Ihre Infrastruktur integrieren, können Sie diese Geschäftsinformationen verwenden, um falsch positive Ergebnisse zu identifizieren. Wenn z. b. Executive Travel in einem Kalender aufgezeichnet wird, der für das Überwachen der Umgebung verantwortliche IT-Personal verfügbar ist, können Sie Verbindungsversuche mit den bekannten Standorten der Führungskräfte korrelieren.  
  
Nehmen wir an, Executive a befindet sich normalerweise in Chicago und verwendet eine gesicherte Arbeitsstation, um von seinem Schreibtisch auf geschäftskritische Daten zuzugreifen, und ein Ereignis wird durch einen fehlgeschlagenen Versuch ausgelöst, auf die Daten von einer nicht geschützten Arbeitsstation in Atlanta zuzugreifen. Wenn Sie überprüfen können, ob der Executive zurzeit in Atlanta ist, können Sie das Ereignis auflösen, indem Sie sich an den Executive oder den Assistenten des Executive wenden, um zu ermitteln, ob es sich bei dem Zugriffsfehler um das Ergebnis der Überprüfung der gesicherten Arbeitsstation zum Zugreifen auf die Daten handelt. Wenn Sie ein Programm erstellen, das die in [Planen](../../../ad-ds/plan/security-best-practices/Planning-for-Compromise.md)der Gefährdung beschriebenen Ansätze verwendet, können Sie damit beginnen, eine Datenbank mit erwartetem Verhalten für die wichtigsten Konten in Ihrer Active Directory-Installation zu erstellen, die Ihnen helfen können, Angriffe schneller zu erkennen und darauf zu reagieren.  
  


