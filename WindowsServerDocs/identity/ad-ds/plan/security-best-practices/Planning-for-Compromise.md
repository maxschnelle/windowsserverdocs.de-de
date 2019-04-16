---
ms.assetid: 6f50476c-a1f1-48fb-999b-76c4c3816496
title: Planen von Kompromisse
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7cb87e6b9d1ace15050dcbff8b3c6d864c2a18f0
ms.sourcegitcommit: f2e98f8b7828730b83a3cc8f0e33d4e4db1b16e1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/02/2018
---
# Planen von Kompromisse

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetz Nummer eins: Niemand geht davon aus, dass nichts schlechten bis bedeutet daran auftreten kann.* - [10 unveränderlichen Gesetze zur Verwaltung der Sicherheit](https://technet.microsoft.com/library/cc722488.aspx)  
  
Wiederherstellungsplänen in vielen Organisationen Konzentration auf Landes-/ Datenverluste oder Fehlern, die Verlust der computing Services führen wiederherstellen. Jedoch bei der Arbeit mit betroffenen Kunden wir häufig feststellen, dass beabsichtigt Kompromisse Wiederherstellen nicht vorhanden ist in Wiederherstellungsplans. Dies gilt besonders, wenn die Kompromisse angegeben, ergibt sich Diebstahl geistiges Eigentum oder absichtlich löschen, die logische Grenzen (z. B. Beseitigung der alle Active Directory-Domänen oder alle Server) (z. B. anstatt physische Schutzvorrichtungen nutzt Löschen eines Datencenters). Obwohl eine Organisation Reaktion Pläne, die ursprüngliche Aktivitäten sein kann werden soll, wenn eine Beschädigung erkannt wird definieren, lassen Sie diese Pläne häufig vor, um eine Kompromisse ergeben, die den gesamten Computer-Infrastruktur wirkt sich auf Weg.  
  
Da Active Directory Rich-Identität und Access-Verwaltungsfunktionen für Benutzer, Server, Arbeitsstationen und Applications bietet, ist es ausnahmslos Ziel von Angreifern. Wenn eine er hohen Berechtigungen Zugriff auf eine Active Directory-Domäne oder Domänencontroller verschafft hat, kann, die von Access zum zugreifen, steuern oder sogar löschen gesamte Active Directory-Struktur genutzt werden.  
  
Dieses Dokument enthält einige der am häufigsten verwendeten Angriffen auf Windows und Active Directory diskutiert und Gegenmaßnahmen, die Sie zum Verringern der Oberfläche Angriffen, aber die einzige sichere Möglichkeit zum Wiederherstellen bei einem vollständigen Vorfall von Active Directory implementieren können werden muss für die Kompromisse vorbereitet, bevor er eintritt. In diesem Abschnitt behandelt kleiner auf technische Implementierungsdetails als vorherigen Abschnitten dieses Dokuments und mehr über auf hoher Ebene empfohlene, mit denen Sie erstellen, eine umfassende umfassende und systematisch zu sichern und Verwalten Ihrer Organisation kritische ist Business und IT-Ressourcen.  
  
Ob Ihre Infrastruktur nie ausgesetzt war, hat resisted Verstoßes, versucht oder succumbed Angriffen und wurde vollständig gefährdet, sollten Sie planen für die unvermeidbare tatsächlich, dass Sie wieder angegriffen werden. Es ist nicht möglich, Angriffen, aber es möglicherweise tatsächlich um möglich, signifikante Verletzung oder Global Kompromisse zu verhindern. Jedes Unternehmen sollten eng ausgewertet werden ihre vorhandene Risiko Management-Programme, und nehmen notwendigen Anpassungen an generelle Maß Sicherheitsrisiko verringern, indem Sie angeglichene Investitionen Prevention, Erkennung, Eingrenzung und Wiederherstellung vornehmen.  
  
Zum Erstellen effektiver Schutz während der Bereitstellung von Diensten weiterhin zu den Benutzern und Unternehmen, die Ihre Infrastruktur und Applikationen abhängig sind Sie möglicherweise müssen berücksichtigen neuartige Methoden, um zu verhindern, erkennen, und Kompromisse in Ihrer Umgebung enthalten, und klicken Sie dann wiederherstellen aus die Kompromisse. Die Vorgehensweisen und Empfehlungen in diesem Dokument möglicherweise nicht helfen Ihnen eine beschädigte Active Directory-Installation reparieren, aber helfen Ihnen, Ihre nächsten Vorkommen zu sichern.  
  
Empfehlungen zum Wiederherstellen von Active Directory-Struktur werden in präsentiert [Windows Server 2012: Planen von Active Directory-Gesamtstruktur Wiederherstellung](https://www.microsoft.com/download/details.aspx?id=16506). Möglicherweise können, um zu verhindern, dass Ihre neue Umgebung vollständig Missbrauch von, aber auch, wenn dies nicht möglich ist, werden Sie Tools zum Wiederherstellen und wieder die Kontrolle über Ihre Umgebung erhalten haben.  
  
## Neuer Ansatz für die Vorgehensweise  
*Recht Zahl acht: schwierig, einem Netzwerk Schutz ist direkt proportional zu seiner Komplexität.* - [10 unveränderlichen Gesetze zur Verwaltung der Sicherheit](https://technet.microsoft.com/library/cc722488.aspx)  
  
Es ist im Allgemeinen gut zulässigen, dass, wenn ein Angreifer SYSTEM, Administrator, Stamm oder gleichwertigen Zugriff auf einen Computer, unabhängig vom Betriebssystem erhalten hat der Computer nicht mehr vertrauenswürdigen anzusehen kann, unabhängig davon, wie viele anstrengungen vorgenommen werden, "Säubern" der System. Active Directory unterscheidet sich nicht. Wenn ein Angreifer berechtigten Zugriff auf eine Domänencontroller oder einem hohen Berechtigungen Konto in Active Directory erhalten hat, es sei denn, Sie haben einen Eintrag jeder Änderung der Angreifer macht oder einer guten Sicherungskopie, können Sie nie Verzeichnis zum Wiederherstellen eines vollständig vertrauenswürdigen Zustand.  
  
Wenn ein Mitglied Server- oder einer Arbeitsstationen ist gefährdet und die von einem Angreifer geändert, der Computer ist nicht mehr vertrauenswürdigen, aber benachbarten uneingeschränkte Servern und Arbeitsstationen Arecompromise von einem Computer impliziert nicht, dass alle Computer beeinträchtigt werden.  
  
In einer Active Directory-Domäne gehostet alle Controller jedoch Replikate der gleichen AD DS-Datenbank. Wenn ein einzelne Domänencontroller gefährdet wird und ein Angreifer die AD DS-Datenbank ändert, repliziert diese Änderungen in jedem anderen Domänencontroller in der Domäne, und klicken Sie je nach der Partition, in der die Änderungen vorgenommen werden, die Gesamtstruktur. Auch wenn Sie jeder Domänencontroller in der Gesamtstruktur wieder zu installieren, sind Sie einfach die Hosts erneut installieren auf denen AD DS-Datenbank gespeichert ist. Bösartige Änderungen an Active Directory repliziert neu installierter Domänencontroller auf einfach zu Domänencontroller repliziert werden, die nach Jahren ausgeführt wurden.  
  
Bei der Beurteilung betroffenen Umgebungen, suchen wir häufig, was davon ausgegangen wurde, werden die ersten Verstoß gegen "Event" tatsächlich nach Wochen, Monate oder sogar Jahre ausgelöst wurde nach Angreifern Anfangs die Umgebung gefährdet hatte. Angreifern die Anmeldeinformationen für hohen Berechtigungen Konten lange normalerweise abgerufen werden, bevor eine Verletzung erkannt wurde, und sie diese Konten, um das Directory, Domain Controller, Mitgliedsservern, Arbeitsstationen manipulieren genutzt, und auch nicht Windows verbunden Systeme.  
  
Diese Ergebnisse sind konsistent mit mehrere Ergebnisse in Verizons 2012 Daten Verstoß gegen Untersuchungen den Bericht, die besagt:  
  
-   98 Prozent der Daten Verletzung von externen Agents Stammsuche  
  
-   85 % der Verletzung von Daten erstellen, Wochen oder mehr zu entdecken  
  
-   92 % der Anfragen von einem Drittanbieter gefunden wurden und  
  
-   97 % der Verletzung wurden vermeidbare, obwohl Sie einfache oder fortgeschrittene Steuerelemente.  
  
Eine Kompromisse in den oben beschriebenen Ausmaß effektiv irreparable sind und das standardmäßige Ratschläge, um "Glätten und Quelltabelle" jeder beschädigte System ist einfach nicht möglich ist oder überhaupt möglich ist Active Directory gefährdet oder gelöscht wurden. Wiederherstellen auch in einem sicher funktionierenden Zustand beseitigt nicht die Fehler, die die Umgebung an erster Stelle gefährdet zulässig.  
  
Obwohl Sie jeden Bereich von Ihrer Infrastruktur schützen müssen, muss ein Angreifer nur finden genügend Lücken in Ihren Schutz auf das gewünschte Ziel zu erhalten. Wenn Ihre Umgebung relativ einfache und ursprünglichen und in der Vergangenheit gut verwaltete, dann Implementieren der Vorschläge oben in diesem Dokument wird möglicherweise eine extrem einfache Lösung.  
  
Jedoch wir haben bereits festgestellt, die die ältere, größere und komplexere der Umgebung, die sehr viel eher bereit ist es die Ratschläge in diesem Dokument unmöglich oder sogar unmöglich implementiert werden können, die. Es ist viel Schutz schwieriger eine Infrastruktur nach dem Vorfall als ist völlig starten und zu eine Umgebung zu erstellen, die ist gegen Angriffen und zu beeinträchtigen. Aber wie zuvor beschrieben, es ist kein kleine Unternehmen gesamte Active Directory-Struktur neu erstellen. Es wird empfohlen, diesen Gründen ist eine weitere konzentrieren, zielgerichteten Ansatz zum Sichern Ihrer Active Directory-Gesamtstrukturen.  
  
Erwägen Sie statt Konzentration auf, und versuchen, alle Maßnahmen beheben, die "fehlerhafte" vorhanden sind, ausgehend von ein Ansatz, in dem Sie priorisieren, was besonders wichtig für Ihr Geschäft und in Ihrer Infrastruktur verfügbar ist. Anstelle eine Umgebung mit veraltet, unauffindbar Betriebssysteme und Anwendungen ausgefüllt Behebung von Problemen auf versuchen, erwägen Sie das Erstellen einer neuen kleinen, sicheren Umgebung in die können Sie problemlos der Benutzer, Systeme und Informationen, die am häufigsten entscheidend, sind port Ihrer Business.  
  
In diesem Abschnitt beschreiben wir einen Ansatz, den eine ursprünglichen AD DS-Gesamtstruktur, die als erstellen können "Nutzungsdauer Boot" oder "secure Zelle" für eine Core Business-Infrastruktur fungiert. Eine ursprünglichen Gesamtstruktur ist einfach ein neu installierten Active Directory-Struktur, die in der Regel in Größe und Umfang eingeschränkt ist, und das ist eine integrierte mithilfe des aktuellen Betriebssysteme, Anwendungen und in [beschriebenen Grundsätze, verringern der Active Directory-Angriffen Fläche](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md).  
  
Durch Implementieren der empfohlene Konfiguration Einstellungen in einem neu erstellten Gesamtstruktur, Sie können eine AD DS-Installation, die von Grund auf mit sicheren Einstellungen und Methoden basiert erstellen, und Sie können die Probleme, die Unterstützung von älteren Systemen begleiten reduzieren und Applikationen. Während Sie ausführliche Anweisungen für die Planung und Implementierung von einer ursprünglichen AD DS-Installation außerhalb des Gültigkeitsbereichs dieses Dokuments sind, sollten Sie folgen einige allgemeine Grundsätze und Richtlinien zum Erstellen einer "sicheren Zelle" in der Sie Ihre wichtigsten unterbringen können Posten. Diese Richtlinien werden wie folgt aus:  
  
1.  Grundsätze für die Trennung und Sichern von kritischen Ressourcen zu identifizieren.  
  
2.  Definieren eines Plans beschränkt, Risiko-basierten an.  
  
3.  Nutzen Sie erforderlichenfalls Migration "nonmigratory".  
  
4.  Implementieren "kreative Beseitigung".  
  
5.  Isolieren Sie älterer Betriebssysteme und Anwendungen.  
  
6.  Sicherheit für Endbenutzer zu vereinfachen.  
  
### Identifizieren von Prinzipien für Trennung und Sichern von kritischen Ressourcen  

Die Merkmale der ursprünglichen Umgebung, die Sie zur House kritischen Ressourcen erstellen können große Unterschiede aufweisen. Sie können beispielsweise eine ursprünglichen Struktur erstellen, in der Sie migrieren nur Benutzer VIP und vertrauliche Daten, die nur diese Benutzer zugreifen können. Sie können eine ursprünglichen Gesamtstruktur, in dem Sie nicht nur VIP migrieren, erstellen Benutzer, die Sie als einer administrative Struktur, implementieren Implementieren der Prinzipien beschrieben, die in [den Active Directory Angriffsfläche](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md) sichere administrative Konten zu erstellen, aber und Hosts, die zum Verwalten Ihrer legacy Gesamtstrukturen aus der ursprünglichen Gesamtstruktur verwendet werden können. Sie möglicherweise eine "spezielle" Gesamtstruktur implementieren, die Konten, berechtigten Konten und Systeme, fordern zusätzlichen Sicherheit wie Servern mit Active Directory Certificate Services (AD CS) mit dem alleiniges Ziel Trennung diese aus weniger sicheren VIP aufnimmt Gesamtstrukturen. Schließlich können Sie implementieren eine ursprünglichen Gesamtstruktur, die den de facto Speicherort für alle neuen Benutzer Systeme, Anwendungen und Daten wird ermöglicht es Ihnen, Ihre Legacygesamtstruktur über Verluste schließlich außer Betrieb setzen.  
  
Unabhängig davon, ob die ursprünglichen Gesamtstruktur eine Reihe von Benutzern enthält und Systeme oder es die Grundlage für eine kürzere Migration bildet, befolgen Sie diese Prinzipien der Planung:  
  
1.  Wird davon ausgegangen Sie, dass Ihre legacy Gesamtstrukturen gefährdet sind.  
  
2.  Konfigurieren Sie eine ursprünglichen Umgebung um eine Legacygesamtstruktur, als vertrauenswürdig einzustufen nicht, obwohl Sie konfigurieren können, um eine ursprünglichen Gesamtstruktur als vertrauenswürdig einzustufen Abwärtskompatibilität.  
  
3.  Nicht migriere Benutzerkonten oder Gruppen aus einer Legacygesamtstruktur auf einer ursprünglichen-Umgebung, wenn es besteht die Möglichkeit, dass die Konten Gruppenmitgliedschaft, SID-Verlauf oder andere Attribute Absicht möglicherweise geändert wurde. Verwenden Sie stattdessen "nonmigratory" Vorgehensweisen eine ursprünglichen Gesamtstruktur gefüllt wird. (Nonmigratory Vorgehensweisen werden später in diesem Abschnitt beschrieben).  
  
4.  Migrieren Sie Computern zum ursprünglichen Gesamtstrukturen nicht aus legacy Gesamtstrukturen. Implementieren frisch installiert-Server in der ursprünglichen Struktur, Installieren von Applications auf den Servern neu installierten und Migrieren von Anwendungsdaten auf die neu installierten Systeme. Kopieren Sie für Dateiserver Daten in den Servern neu installierter, festlegen Sie ACLs mithilfe von Benutzern und Gruppen in der neuen Gesamtstruktur und dann erstellen Sie drucken Servern auf ähnliche Weise.  
  
5.  Die Installation von älteren Betriebssystemen oder Anwendungen in der ursprünglichen Gesamtstruktur nicht zulassen. Wenn eine Anwendung kann nicht aktualisiert und frisch installiert werden, lassen Sie sie in der Legacygesamtstruktur und erwägen Sie kreativ Beseitigung auf der Anwendungsfunktionalität ersetzen.  
  
### Definieren eines Migrationsplans für beschränkt, Risiko-basierten  
Erstellen eine begrenzte, Risiko-basierten Migrations-Plan einfach bedeutet, die bei der Entscheidung, welche Benutzer,-Anwendungen und Daten in Ihrer ursprünglichen Gesamtstruktur, migrieren Sie werden Migration Ziele basierend auf den Grad des Risikos gekennzeichnet sollen, der Ihre Organisation bereitgestellt werden, wenn eine, der der Benutzer oder Systeme gefährdet wird. VIP-Benutzer, deren Konten am ehesten Ziel von Angreifern sein, sollten in der ursprünglichen Gesamtstruktur befinden. Programme, die wichtige geschäftliche Funktionen auf neu erstellten Server in der ursprünglichen Struktur installiert werden soll, und vertrauliche Daten verschoben werden soll, Bereitstellen gesicherter Server in der ursprünglichen Struktur.  
  
Wenn Sie noch nicht über die wichtigsten Benutzer löschen Bild verfügen, arbeiten Systeme,-Anwendungen und Daten in der Active Directory-Umgebung mit Business Einheiten, um sie zu kennzeichnen. Wie sollten Sie alle Server ein, auf dem kritischen Programme ausführen, oder wichtige Daten werden gespeichert, muss, jeder erforderliche für Unternehmen bei Anwendung identifiziert werden. Identifizieren die Benutzer und Ressourcen, die für Ihre Organisation Funktion weiterhin erforderlich sind, erstellen Sie eine natürlich mit Prioritätsstufe Sammlung von Anlagen, nach denen sich konzentrieren.  
  
### Nutzung von "Nonmigratory" Migration  
Ob Sie wissen, dass Ihre Umgebung geworden ist, davon ausgehen Sie, dass er ist gefährdet oder einfach lieber nicht zu migrieren vorhandener Daten und Objekten ein älteres Active Directory-Installation auf eine neue, erwägen Sie die Migrations-Vorgehensweisen, die nicht technisch durchführen Objekte "migrieren".  
  
### Benutzerkonten  
In einer herkömmlichen Active Directory Migration von einer Gesamtstruktur in eine andere wird das Attribut SIDHistory (SID-Verlauf) für Objekte im zum Speichern von Benutzer-SID und die SIDs der Gruppen, dass Benutzer die Mitglieder in der Legacygesamtstruktur Waren verwendet. Wenn Benutzerkonten in eine neue Gesamtstruktur migriert werden und sie Zugriff auf Ressourcen in der Legacygesamtstruktur, werden die SIDs im SID-Verlauf einer Access-Token zu erstellen, können die Benutzern den Zugriff auf Ressourcen, dem sie Access hatten, bevor die Konten migriert wurden, verwendet.  
  
Warten, dass die SID-Verlauf, allerdings in einigen Umgebungen problematische erwiesen hat kann da Benutzer Access Token mit aktuellen und zurückliegende SIDs Auffüllen von token Aufblasen führen. Token Aufblasen ist ein Problem bei dem verwendet, die Anzahl der SIDs, die in Access-Token des Benutzers gespeichert sein muss größer oder gleich den Abstand im Token zur Verfügung.  
  
Obwohl in begrenztem Umfang token Größen erhöht werden können, ist die ultimative Lösung zu token Aufblasen zum Verringern der Anzahl der SIDs Benutzerkonten, zugeordnet, indem rationalisieren Gruppenmitgliedschaft, Beseitigung SID-Verlauf oder eine Kombination aus beiden. Weitere Informationen zu token Aufblasen finden Sie unter [MaxTokenSize und Kerberos Token Aufblasen](http://blogs.technet.com/b/shanecothran/archive/2010/07/16/maxtokensize-and-kerberos-token-bloat.aspx).  
  
Statt Migrieren von Benutzern von einer legacy-Umgebung (vor allem eine in der Gruppenmitgliedschaften und SID Verläufe möglicherweise gefährdet) mit SID-Verlauf, erwägen Sie die Nutzung von Metaverzeichnis Applications "Benutzer migrieren" ohne SID-Verläufe auszuführen in der neuen Gesamtstruktur. Bei der Erstellung von Benutzerkonten in der neuen Gesamtstruktur können Sie eine metadirectory Anwendung, die Konten zu ihren entsprechenden Konten in der Legacygesamtstruktur zuordnen.  
  
Um den neuen Benutzerzugriff auf Ressourcen in der Legacygesamtstruktur bereitzustellen, können Sie der metadirectory Werkzeuge verwenden, um Ressourcengruppen zu identifizieren, in denen die ältere Benutzerkonten der Zugriff gewährt wurde, und klicken Sie dann die neue Benutzerkonten zu diesen Gruppen hinzufügen. Abhängig von Ihrer Gruppenstrategie in der Legacygesamtstruktur müssen Sie zum Erstellen von Gruppen der lokalen Domäne für den Zugriff auf Ressourcen oder Konvertieren von vorhandenen Gruppen in Gruppen der lokalen Domäne an, damit die neuen Konten Ressourcengruppen hinzugefügt werden. Konzentrieren zuerst auf die wichtigsten Applikationen und Daten und deren Migrieren in der neuen Umgebung (mit oder ohne SID-Verlauf), können Sie die Menge des Aufwand in der legacy-Umgebung begrenzen.  
  

  
### Server und Arbeitsstationen  
In einer herkömmlichen Migration von einem Active Directory ist Gesamtstruktur zu einer anderen, Migrieren von Computern oft relativ einfach im Vergleich zum Migrieren von Benutzern, Gruppen und Applikationen. Je nach der Rolle des Computers kann die Migration in einer neuen Gesamtstruktur so einfach wie das Trennen einer alten Domäne und die Teilnahme an eine neue sein. Computerkonten intakt migrieren jedoch in einer ursprünglichen Gesamtstruktur führt zu weiteren Produktkosten des Zwecks der Erstellung einer frischen-Umgebung. Statt migrieren (potenziell betroffenen, unauffindbar oder veraltet) Computer in eine neue Gesamtstruktur ausmacht, sollten Sie frisch Server und Arbeitsstationen in der neuen Umgebung installieren. Sie können Daten in der Legacygesamtstruktur auf Systeme in der ursprünglichen Gesamtstruktur Systeme, aber nicht die Systeme dieser House die Daten migrieren.  
  
### Anwendungen  

Applikationen können die wichtigste Herausforderung bei jeder Migration von einer Gesamtstruktur in eine andere präsentieren, aber im Falle einer Migrations "nonmigratory" ist eine der grundlegendsten Prinzipien, die angewendet werden soll, dass in der ursprünglichen Gesamtstruktur Applikationen aktuellen sein soll, unterstützt und frisch installiert. Daten können von Anwendungsinstanzen in der alten Gesamtstruktur mögliche migriert werden. In Situationen, in denen eine Anwendung "in der ursprünglichen Gesamtstruktur neu erstellt werden kann", sollten Sie Ansätze kreative Beseitigung oder Trennung der legacy-Anwendungen, wie im folgenden Abschnitt beschrieben.  
  
### Implementieren kreative Beseitigung  
Kreative Beseitigung ist eine Wirtschaftlichkeit Ausdruck aus, der economic Development beim Löschen des einer früheren Reihenfolge erstellt werden. In den letzten Jahren hat der Ausdruck auf Informationstechnologie angewendet wurde. Es bezieht sich normalerweise auf Verfahren nach der alten Infrastruktur beseitigt wird, nicht durch Aktualisieren it, aber sie durch etwas ganz neuen ersetzen. Die 2011 [Gartner Symposium ITXPO](http://www.gartner.com/technology/symposium/orlando/) für CIOs und IT-Führungskräften verständlicher kreative Beseitigung als eines der zugehörigen Key Designs für Verringerung der Kosten und erhöht Effizienz. Verbesserte Sicherheit sind möglich als Balanceakt des Prozesses.  

Beispielsweise kann eine Organisation mehrere Business Einheiten bestehen, die eine andere Anwendung zu verwenden, die ähnliche Funktionalität mit unterschiedlichen Grad der Unterstützung für Modernity und Lieferanten ausführt. In der Vergangenheit IT möglicherweise beibehalten werden muss jede Business-Einheit Anwendung separat und Konsolidierung steigern würde versuchen, um herauszufinden, welche Anwendung die optimale Funktionalität zur Verfügung, und dann Daten in die Migration bestehen die Anwendung von den anderen.  
  
In kreative Beseitigung, statt der Pflege veraltete oder redundante Applications vollständig neue Applikationen zum Migrieren von Daten in die neuen Applikationen ersetzen die alte implementieren und außer Betrieb setzen die alten Anwendungen und die Systeme, auf denen sie ausgeführt. In einigen Fällen können Sie kreativ Beseitigung der legacy Applikationen durch eine neue Anwendung in Ihrer eigenen Infrastruktur bereitstellen implementieren, aber wann immer möglich, sollten Sie Betracht, stattdessen gezogen werden die Anwendung in einen Cloud-basierte Lösung.  
  
Durch die Bereitstellung von Cloud-basierten Anwendungen älterer Versionen für Applikationen ersetzen Sie nicht nur reduzieren, Wartung steigern und Kosten, aber Sie Ihrer Organisation Angriffsfläche durch beseitigen älterer Betriebssysteme und Anwendungen, die Schwachstellen präsentieren reduzieren Angreifern zu nutzen. Dieser Ansatz bietet eine schnellere Möglichkeit für eine Organisation in die gewünschte Funktionalität und gleichzeitig beseitigt legacy Ziele in der Infrastruktur zu erhalten. Obwohl das Prinzip der kreative Beseitigung nicht für alle IT-Ressourcen gilt, bereitgestellt oft realisierbar zur Behandlung von älteren Systemen und Applikationen beim Bereitstellen von gleichzeitig robuste, sicheren, Cloud-basierten Anwendungen.  
  
### Isolieren Legacy-Betriebssysteme und Anwendungen  
Migrieren Ihre geschäftlich relevanten Anwender und Systeme zu einer ursprünglichen, sichere Umgebung Balanceakt ist, dass Ihre Legacygesamtstruktur wird weniger wichtige Informationen und Systeme enthalten sein. Zwar die älterer Betriebssysteme und Anwendungen, die in der Umgebung weniger sicher bleiben möglicherweise erhöhten Risiko Kompromisse präsentieren, stellen sie auch eine reduzierte Schwere der Kompromisse dar. Durch Homing und Ihre Anlagen kritische geschäftliche Modernisierung, können Sie konzentrieren Bereitstellen von effektiven Management und Überwachung während ohne legacy Einstellungen und Protokolle berücksichtigt werden müssen.  
  
Wenn Sie Ihre kritischen Daten einer ursprünglichen Gesamtstruktur verlagert haben, können Sie Optionen zum Bewerten weiter isoliert älterer Betriebssysteme und Anwendungen in Ihre "main" AD DS-Gesamtstruktur. Obwohl Sie möglicherweise, kreative Beseitigung zum Ersetzen einer Anwendung und die Server implementieren, auf denen ausgeführt wird, in anderen Fällen sollten zusätzliche Isolation unsicherste Betriebssysteme und Anwendungen Sie. Beispielsweise erstellen eine Anwendung, die durch bestimmte Benutzer verwendet wird, aber der erfordert, dass legacy Anmeldeinformationen wie LAN Manager-Hashes in einer kleinen Domäne migriert werden können, Sie Systeme unterstützt, für die Ihnen kein Ersatz zur Verfügung stehen.  
  
Durch diese Systeme, wo sie Implementierung von legacy Einstellungen mehr, Domänen entfernen, können Sie die Sicherheit dieser Domänen später konfigurieren, um nur die aktuelle Betriebssysteme und Applikationen unterstützen erhöhen. Zwar es empfehlenswert älterer Betriebssysteme und Anwendungen, wann immer möglich, außer Betrieb setzen ist. Wenn außer Betrieb einfach nicht für ein kleines Segment Ihrer legacy Population soweit möglich ist, können Sie es in einer separaten Domäne (oder Gesamtstruktur) Trennung schrittweisen Verbesserung in den Rest der legacy-Installation ausführen.  
  
### Vereinfachung der Sicherheit für Endbenutzer  
In den meisten Organisationen müssen Benutzer mit Zugriff auf die am häufigsten vertrauliche Informationen aufgrund der Art der ihre Rollen in der Organisation häufig die minimalen Zeitdauer widmen zu lernen komplexe Access Einschränkungen und Steuerelemente. Obwohl Sie eine umfassende Sicherheit Education-Programm für alle Benutzer in Ihrer Organisation haben, sollten Sie auch den Fokus erhält Sicherheit so einfach wie möglich verwenden, indem Sie Steuerelemente, die als transparent und Vereinfachung Prinzipien, welche Benutzer sind eingehalten Sie werden.  
  
Beispielsweise können Sie eine Richtlinie definieren, in die Geschäftsführer und andere VIPs erforderlich sind, sichere Arbeitsstationen zu verwenden, um vertrauliche Daten und Systeme, zuzugreifen so, dass sie mit den anderen Geräten auf weniger wichtige Daten zugreifen. Dies ist ein einfaches Prinzip für Benutzer, die Beachtung verdienen, aber Sie können eine Reihe von Back-End-Steuerelementen zum Erzwingen des Ansatzes dazu beitragen, implementieren.  

Sie können [Authentifizierung Verfahren Assurance](https://technet.microsoft.com/library/dd391847(v=WS.10).aspx) verwenden, um zuzulassen, dass die Benutzer auf vertrauliche Daten zuzugreifen, nur, wenn er in deren sichere Systeme mit einer ihrer Smartcard angemeldet haben, und können die Systeme steuern, aus denen sie können, IPsec und Benutzer Rechte Einschränkungen Verbinden Sie mit sensiblen Datenrepositorys. Können Sie das [Microsoft Data Klassifizierung Toolkit](https://www.microsoft.com/download/details.aspx?id=27123) Aufbau einer Datei robuste Klassifizierung Infrastruktur und können Sie [Dynamische Access Control](http://blogs.technet.com/b/windowsserver/archive/2012/05/22/introduction-to-windows-server-2012-dynamic-access-control.aspx) zum Einschränken des Zugriffs auf Daten anhand einer Zugriffsversuch Merkmale implementieren übersetzen Business Regeln in technischen Steuerelemente.  
  
Aus der Sicht des Benutzers, den Zugriff auf vertrauliche Daten von einem gesicherten System "nur Works" und aus einem ungeschützte System vergeblich versucht, "einfach nicht". Jedoch sind hinsichtlich der für die Überwachung und Verwaltung Ihrer Umgebung, Ihnen hilft identifiable Muster in Zugriff von Benutzern auf vertrauliche Daten und Systeme, denen es einfacher für Sie abweichenden Access Versuche erkennen erstellen.  
  
Erwägen Sie alternative Ansätze für die Authentifizierung in Umgebungen, welche Benutzer Schutz vor langen, komplexen Kennwörter weist nicht genügend Kennwortrichtlinien, besonders für Benutzer von VIP geführt haben, ob mit einer Smartcard (die eine Reihe von Formularfaktoren nützlich sein und mit zusätzlichen Funktionen, Authentifizierung Stärken) vertrauenswürdige Speicherchips Platform-Modul (TPM) in den Computern der Benutzer biometrische Steuerelemente, z. B. Finger-Streifen Leser oder sogar Authentifizierungsdaten, die durch gesichert werden. Zwar kombinierte Authentifizierung Anmeldeinformationen Diebstahl Angriffen nicht verhindert wird, wenn ein Computer bereits durch benennen Ihre Benutzer einfach zu verwendendes Authentifizierung Steuerelemente gefährdet ist, können Sie zuweisen eine sichere Kennwörter die Konten der Benutzer für die herkömmliche Benutzer Anmeldename und das Kennwort Steuerelemente sind schwerfällig.  
