---
ms.assetid: 6f50476c-a1f1-48fb-999b-76c4c3816496
title: Planen der Gefährdung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0f6a30c91590667a0894b52ec7c188a43bd5e351
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835571"
---
# <a name="planning-for-compromise"></a>Planen der Gefährdung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*Gesetz Nummer eins: Niemand ist davon überzeugt, dass alle fehlerhaften, auftreten kann, bis dies der Fall ist.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Pläne zur notfallwiederherstellung in vielen Organisationen konzentrieren Sie sich zum Wiederherstellen von regionalen Ausfällen oder Fehlern, die Verlust der computing-Dienste. Allerdings bei der Arbeit mit kompromittierten Kunden wir häufig feststellen, dass das Wiederherstellen aus beabsichtigt Gefährdung nicht vorhanden ist in ihre Pläne zur notfallwiederherstellung. Dies gilt besonders bei Gefährdung führt Diebstahl von geistigem Eigentum oder absichtliche Zerstörung, die logische Begrenzungen (z. B. die Zerstörung von alle Active Directory-Domänen oder alle Server) (z. B. statt physischen Grenzen nutzt Zerstörung eines Datencenters). Obwohl eine Organisation zur Reaktion auf Vorfälle Pläne, die Definieren der anfänglichen Aktivitäten aufweisen kann an, die bei eine Gefährdung erkannt wird, lassen Sie diese Pläne häufig Schritte zur Wiederherstellung nach einer Gefährdung, die die gesamte IT-Infrastruktur wirkt sich auf Weg.  
  
Da Active Directory eine umfassende Funktionen zur Identitäts- und Zugriffs für Benutzer, Server, Arbeitsstationen und Anwendungen bereitstellt, ist es immer das Ziel von Angreifern. Wenn ein Angreifer hoch privilegierten Zugriff auf eine Active Directory-Domäne bzw. diesen Domänencontroller hinzugefügt werden, kann, dass der Zugriff genutzt werden, um Zugriff auf, zu steuern oder sogar zerstört der Active Directory-Gesamtstruktur.  
  
In diesem Dokument wurde beschrieben, einige der geläufigsten Angriffsarten für Windows und Active Directory und Gegenmaßnahmen, die Sie implementieren können, um die Angriffsfläche, aber die einzige sichere Möglichkeit, im Falle einer umfassenden Gefährdung der Active Directory wiederherzustellen verringern werden sollen für die Beeinträchtigung vorbereitet, bevor sie vorgenommen. Dieser Abschnitt konzentriert sich weniger auf die technische Implementierungsdetails als den vorherigen Abschnitten dieses Dokuments und mehr auf allgemeinen Empfehlungen, die Sie verwenden können, erstellen ein ganzheitlichen und umfassender Ansatz zum Sichern und Verwalten Ihrer Organisation wichtige des Geschäfts- und IT-Ressourcen.  
  
Ob Ihre Infrastruktur niemals angegriffen wurde, hat bei sich versucht sicherheitsverletzungen, oder Angriffe succumbed und wurden vollständig kompromittiert, sollten Sie für die unvermeidliche Realität, dass Sie immer wieder neu angegriffen werden werden. Es ist nicht möglich, Angriffe zu verhindern, aber es tatsächlich möglicherweise erhebliche sicherheitsverletzungen oder Großhandel gefährdungen zu verhindern. Jede Organisation sollte genau bewerten ihre vorhandenen Risiko-Management-Programme, und stellen notwendigen Anpassungen vor, um ihre allgemeinen Ebene des Sicherheitsrisikos verringern, indem mit Lastenausgleich Investitionen in Verhinderung, Erkennung, Kapselung und Recovery vornehmen.  
  
Zum Erstellen von effizienten Schutz und Dienste weiterhin zu den Benutzern und Unternehmen, die abhängig von Ihrer Infrastruktur und Anwendungen bereitstellen, kann auf neuartige Weise, um zu verhindern, sollten erkennen, und enthalten Kompromiss in Ihrer Umgebung und dann wiederherstellen aus die Beeinträchtigung. Die Methoden und Empfehlungen in diesem Dokument können nicht helfen Ihnen eine gefährdete Active Directory-Installation zu reparieren, jedoch können Sie Ihre darauffolgenden zu schützen.  
  
Empfehlungen für die Wiederherstellung von Active Directory-Gesamtstruktur werden angezeigt, [Windows Server 2012: Planen der Wiederherstellung der Active Directory-Gesamtstruktur](https://www.microsoft.com/download/details.aspx?id=16506). Möglicherweise können Sie die neue Umgebung gefährdet werden vollständig zu verhindern, dass, aber selbst wenn Sie keine Möglichkeit, müssen Sie Tools zum Wiederherstellen und wieder die Kontrolle über Ihre Umgebung erhalten.  
  
## <a name="rethinking-the-approach"></a>Neuer Ansatz für den Ansatz  
*Gesetz Nummer 8: Die Schwierigkeit der Verteidigung eines Netzwerks ist direkt proportional zu seiner Komplexität.* - [10 unveränderlichen Gesetze zur Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Es ist allgemein anerkannten, dass wenn ein Angreifer, SYSTEM, Administrator, Stamm oder entsprechende Zugriff auf einen Computer, unabhängig vom Betriebssystem erhalten hat, diesem Computer nicht mehr berücksichtigt werden kann vertrauenswürdig ist, unabhängig davon, wie viele bemühungen vorgenommen werden, zu "bereinigen" der System. Active Directory ist nicht anders. Wenn ein Angreifer privilegierten Zugriff auf einem Domänencontroller oder ein Konto in Active Directory abgerufen hat, es sei denn, Sie verfügen über einen Datensatz, der alle Änderungen, die der Angreifer führt oder einer als funktionierend bekannten Sicherung, können Sie nicht wiederherstellen, auf das Verzeichnis eine vollständig der Vertrauenswürdigkeitsstatus.  
  
Bei einem Mitgliedsserver oder einer Arbeitsstation beeinträchtigt und werden, von einem Angreifer geändert, der Computer nicht mehr vertrauenswürdig ist, aber benachbarten um Server und Arbeitsstationen können immer noch vertrauenswürdig sein. Gefährdung eines Computers bedeutet nicht, dass alle Computer gefährdet sind.  
  
Jedoch nicht in einer Active Directory-Domäne alle Domänencontroller Replikate derselben AD DS-Datenbank hosten. Wenn ein einzelner Domänencontroller gefährdet ist, und ein Angreifer, AD DS-Datenbank ändert, replizieren diese Änderungen auf alle anderen Domänencontroller in der Domäne, und abhängig von der Partition, in dem die Änderungen vorgenommen werden, die Gesamtstruktur. Auch wenn Sie alle Domänencontroller in der Gesamtstruktur neu installieren, werden Sie die Hosts einfach neu installieren, wenn auf denen AD DS-Datenbank befindet. Schädliche Änderungen an Active Directory repliziert neu installierte Domänencontroller auf genauso einfach wie mit Domänencontrollern repliziert werden, die jahrelang ausgeführt werden.  
  
Bei der Bewertung gefährdeten Umgebungen, finden wir häufig, wie sich das erste Breach "Ereignis" definitionsprozesse tatsächlich nach Wochen, Monate oder sogar Jahre ausgelöst wurde nach dem Angreifer zunächst die Umgebung beeinträchtigt haben. Angreifer die Anmeldeinformationen für hoch privilegierten Konten, die lange in der Regel abgerufen werden, bevor eine Verletzung wurde erkannt, und sie diese Konten, um das Verzeichnis, Domänencontroller, Mitgliedsserver, Arbeitsstationen zu gefährden genutzt, und nicht-Windows selbst besteht Systeme.  
  
Diese Ergebnisse entsprechen einige Ergebnisse im Verizon 2012 Data Breach Untersuchungen Bericht, die, in der angegeben:  
  
-   98 Prozent der datenschutzverletzungen von externen Agents durchgeführt  
  
-   85 Prozent der datenschutzverletzungen dauerte, Wochen oder länger, um zu ermitteln  
  
-   92 % der Incidents wurden von einem Drittanbieter gefunden und  
  
-   97 Prozent von Sicherheitsverstößen vermeidbar, obwohl der einfache oder um Steuerelemente für fortgeschrittene.  
  
Ein Kompromiss, den Grad an, die zuvor beschriebenen ist effektiv irreparablen, und die standardmäßige Ratschläge, die "löschen und neu aufsetzen" alle betroffenen Systems ist einfach nicht möglich oder sogar möglich, wenn Active Directory beschädigt oder zerstört wurde. Sogar in einen bekannten guten Zustand wiederherstellen ist nicht die Mängel beseitigt, die die Umgebung im vornherein gefährdet zulässig.  
  
Obwohl Sie alle Aspekte Ihrer Infrastruktur zu schützen müssen, muss ein Angreifer nur genügend Fehler zu ermitteln, in der Verteidigung, um das gewünschte Ziel zu erhalten. Wenn die Umgebung relativ einfach und makellose und in der Vergangenheit gut verwalteten, implementieren Sie dann auf die Empfehlungen weiter oben in diesem Dokument wird möglicherweise eine einfache Lösung.  
  
Aber wir haben festgestellt, die die älteren, größeren und komplexeren der Umgebung, desto wahrscheinlicher ist es, dass die Empfehlungen in diesem Dokument nicht realisierbar oder noch nicht implementiert werden soll. Es ist viel schwieriger, um eine Infrastruktur nach dem Fakt zu sichern, als es ist völlig starten und eine Umgebung zu erstellen, die ist gegen Angriffe und beeinträchtigen. Aber wie bereits erwähnt, es ist kein kleine Unternehmen, um eine gesamte Active Directory-Gesamtstruktur neu zu erstellen. Aus diesen Gründen wird empfohlen, eine konzentrieren, zielgerichteten Ansatz zum Schützen Ihrer Active Directory-Gesamtstrukturen.  
  
Anstatt konzentrieren, und versuchen, alles zu korrigieren, "fehlerhaft" aufweisen, sollten Sie Sie, dass ein Ansatz, in dem Sie priorisieren, entsprechend dem Inhalt am wichtigsten für Ihr Unternehmen und in Ihrer Infrastruktur. Anstatt zu versuchen, eine Umgebung, gefüllt mit veralteten, falsch konfigurierte Systeme und Anwendungen zu beheben, sollten Sie erstellen eine neue kleine, sichere Umgebung, die in der können Sie problemlos den Benutzern, Systeme und Informationen, die wichtigsten sind Portieren Ihrer Business.  
  
In diesem Abschnitt beschreiben wir einen Ansatz mit dem Sie eine makellose AD DS-Gesamtstruktur, die als erstellen können "Leben Schiff" oder "sichere Zelle" für Ihre Business-Kerninfrastruktur dient. Eine makellose Gesamtstruktur ist einfach eine neu installierte Active Directory-Gesamtstruktur, die in der Regel in der Größe und Umfang begrenzt ist, und die wird erstellt, mit der aktuellen Betriebssystemen, Anwendungen und mit den Prinzipien, die in beschriebenen [reduzieren die aktive Directory Angriffsfläche](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md).  
  
Implementieren Sie die empfohlenen Konfigurationseinstellungen in einer neu erstellten Gesamtstruktur an, Sie können AD DS-Installation, die von Grund auf mithilfe von Sicherheitseinstellungen und Methoden basiert erstellen und Sie können die Herausforderungen, die mit der Unterstützung von älterer Systems verringern und Anwendungen. Detaillierte Anweisungen zum Entwurf und Implementierung einer makellose AD DS-Installation über den Rahmen dieses Dokuments sind, sollten Sie folgen einige allgemeine Prinzipien und Richtlinien zum Erstellen einer "sicheren Zelle" in der Sie Ihre wichtigsten untergebracht werden können Ressourcen. Diese Richtlinien sind wie folgt aus:  
  
1.  Identifizieren Sie Prinzipien für die Trennung und schützen kritische Ressourcen.  
  
2.  Definieren Sie einen beschränkt, risikobasierten Migrationsplan.  
  
3.  Nutzen Sie "nonmigratory" Migrationen, bei Bedarf.  
  
4.  Implementieren von "creative Zerstörung."  
  
5.  Isolieren Sie ältere Systeme und Anwendungen.  
  
6.  Vereinfachen Sie die Sicherheit für Endbenutzer.  
  
### <a name="identifying-principles-for-segregating-and-securing-critical-assets"></a>Identifizieren Prinzipien für einzuschränken, und Sichern von kritischen Ressourcen  

Die Merkmale der makellose Umgebung, die Sie für kritische Ressourcen Haus erstellen, können stark variieren. Sie können z. B. eine makellose Gesamtstruktur zu erstellen, in der Sie migrieren nur von VIP-Benutzer und vertrauliche Daten, die nur dieser Benutzer zugreifen können. Sie können eine makellose Gesamtstruktur, in dem Sie nicht migrieren, erstellen nur VIP-Benutzer, aber die Sie als Entwurf einer administrativen Gesamtstruktur zu implementieren, Implementieren der Prinzipien in beschriebenen [die Active Directory-Angriffsfläche verkleinern](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md) zum sicheren erstellen Administratorkonten und Hosts, die zum Verwalten Ihrer legacy-Gesamtstrukturen aus der ursprünglichen Gesamtstruktur verwendet werden können. Sie können eine "spezielle" Gesamtstruktur implementieren, die VIP-Konten, privilegierten Konten und Systeme, die zusätzliche Sicherheit, z. B. Server mit Active Directory-Zertifikatdienste (AD CS) mit dem einzigen Ziel werden aus den weniger sicheren Trennung erfordern enthält Gesamtstrukturen. Schließlich können Sie implementieren eine makellose Gesamtstruktur, die den de-facto-Speicherort für alle neuen Benutzer, die Systeme, Anwendungen und Daten, wird dadurch können Sie die legacy-Gesamtstruktur über aufgrund von Abnutzung letztendlich außer Betrieb nehmen.  
  
Unabhängig davon, ob die makellose Gesamtstruktur eine Reihe von Benutzern enthält und Systemen oder Paket die Grundlage für die umfangreichere wiederherstellungsanforderungen erforderlich Migration bildet befolgen Sie diese Prinzipien in Ihre Planung:  
  
1.  Angenommen Sie, Ihre legacy-Gesamtstrukturen gefährdet sind.  
  
2.  Konfigurieren Sie eine makellose Umgebung für eine Gesamtstruktur legacy vertrauen nicht, auch wenn Sie eine ältere Umgebung für eine makellose Gesamtstruktur-Vertrauensstellung konfigurieren können.  
  
3.  Migrieren Sie nicht-Benutzerkonten oder-Gruppen aus einer Gesamtstruktur legacy für eine makellose Umgebung, wenn es besteht die Möglichkeit, dass die Konten Gruppenmitgliedschaften, SID-Verlauf oder andere Attribute in böswilliger Absicht möglicherweise geändert wurde. Verwenden Sie stattdessen "nonmigratory" Ansätze, um eine makellose Gesamtstruktur zu füllen. (Nonmigratory Ansätze werden weiter unten in diesem Abschnitt beschrieben.)  
  
4.  Migrieren Sie die Computer nicht von legacy-Gesamtstrukturen, für makellose Gesamtstrukturen. Implementieren von neu installierten Server in der Gesamtstruktur makellose, Anwendungen auf die neu installierten Server installieren und Anwendungsdaten zu migrieren, auf die neu installierte Systeme. Für Dateiserver Kopieren von Daten in den neu installierten Server, Festlegen von ACLs mithilfe von Benutzern und Gruppen in der neuen Gesamtstruktur und erstellen Sie dann den Druckserver auf ähnliche Weise.  
  
5.  Lassen Sie nicht die Installation von älteren Betriebssystemen oder Anwendungen in der ursprünglichen Gesamtstruktur. Wenn eine Anwendung kann nicht aktualisiert und neu installiert werden, lassen Sie sie in der Gesamtstruktur legacy, und berücksichtigen Sie creative Zerstörung, um die Funktionalität der Anwendung zu ersetzen.  
  
### <a name="defining-a-limited-risk-based-migration-plan"></a>Definieren eines Plans für die Migration begrenzt, risikobasierten  
Erstellen eine begrenzte, risikobasierten Migrationsplan einfach bedeutet, dass bei der Entscheidung, welche Benutzer, Anwendungen und Daten, um in Ihrer Gesamtstruktur makellose migrieren Sie Migration Ziele basierend auf den Grad der Risiken identifizieren sollte, Ihrer Organisation bereitgestellt werden, wenn mindestens eine, der die Benutzer oder Systeme gefährdet ist. VIP-Benutzer, deren Konten am ehesten vor Angriffen zu schützen, sollten in der ursprünglichen Gesamtstruktur befinden. Anwendungen, die ermöglichen, wichtige Geschäftsfunktionen, die auf die neu erstellte Server in der ursprünglichen Gesamtstruktur installiert werden soll, und streng vertrauliche Daten verschoben werden soll, um gesicherte Server in der ursprünglichen Gesamtstruktur.  
  
Wenn Sie nicht bereits über ein klares Bild von den wichtigsten Benutzern verfügen, arbeiten Systeme, Anwendungen und Daten in der Active Directory-Umgebung mit Geschäftseinheiten auf sie zu identifizieren. Jede Anwendung, die erforderlich sind, für das Unternehmen ausgeführt werden sollte angegeben werden, wie sollten Sie alle Server, auf denen kritische Anwendungen ausgeführt oder kritische Daten gespeichert. Durch identifizieren, die Benutzer und Ressourcen, die für Ihre Organisation weiterhin erforderlich sind, erstellen Sie eine auf natürliche Weise nach Priorität geordnete Sammlung von Ressourcen auf dem sich konzentrieren.  
  
### <a name="leveraging-nonmigratory-migrations"></a>Nutzung von "Nonmigratory" Migrationen  
Ob Sie wissen, dass Ihre Umgebung gefährdet ist, den Verdacht, dass er kompromittiert wurde, oder einfach nicht möchten, dass ältere Daten und Objekte von einer älteren Active Directory-Installation zu einem neuen Gerät migrieren, sollten Sie berücksichtigen Migrationsansätze, die technisch nicht ausführen. Objekte mit "migrieren".  
  
### <a name="user-accounts"></a>Benutzerkonten  
In einer herkömmlichen Active Directory Migration aus einer Gesamtstruktur in eine andere wird das SIDHistory (SID-Verlauf)-Attribut für User-Objekte verwendet, zum Speichern von Benutzer-SID und die SIDs der Gruppen, denen Benutzer Mitglied in der Gesamtstruktur legacy waren. Wenn Benutzerkonten werden in eine neue Gesamtstruktur migriert und Zugriff auf Ressourcen in der Gesamtstruktur legacy, werden die SIDs in der SID-Verlauf ein Zugriffstoken zu erstellen, können die Benutzer zum Zugriff auf Ressourcen, die auf die sie Zugriff hatten, bevor die migrierten Konten, verwendet.  
  
Warten, dass die SID-Verlauf jedoch problematisch in einigen Umgebungen bewährt hat kann Auffüllen des Zugriffstoken für Benutzer mit der aktuellen und vergangenen SIDs token Überfrachtung führen. Token Überfrachtung ist ein Problem in der die Anzahl von SIDs, die im Zugriffstoken des Benutzers gespeichert werden muss verwendet oder diese übersteigt der Menge des Speicherplatzes, die im Token verfügbar.  
  
Tokengröße in beschränktem Umfang erhöht werden können, zwar die ultimative Lösung token Überfrachtung zum Reduzieren von der Anzahl von SIDs von Benutzerkonten, zugeordnet, von Gruppenmitgliedschaften, beseitigen der SID-Verlauf oder eine Kombination aus beidem rationalisieren. Weitere Informationen zu token Aufblähung führen, finden Sie unter [MaxTokenSize und Kerberos Token Müll](http://blogs.technet.com/b/shanecothran/archive/2010/07/16/maxtokensize-and-kerberos-token-bloat.aspx).  
  
Anstatt Migrieren von Benutzern aus einem legacy-Umgebung (insbesondere eine in der Gruppenmitgliedschaften und den SID-Verlauf beeinträchtigt werden) durch die Verwendung des SID-Verlaufs, erwägen Sie die Verwendung von Metaverzeichnis Anwendungen für die Benutzer, "Migration", ohne mit der SID-Verlauf in der neuen Gesamtstruktur. Wenn Benutzerkonten in der neuen Gesamtstruktur erstellt werden, können Sie eine Metaverzeichnis-Anwendung, um die Konten auf ihre entsprechenden Konten in der Gesamtstruktur legacy zuzuordnen.  
  
Um den neuen Benutzerkonten Zugriff auf Ressourcen in der Gesamtstruktur legacy bereitzustellen, können Sie die Metaverzeichnis-Tools verwenden, um Ressourcengruppen zu identifizieren, in denen der ältere Benutzerkonten Zugriff gewährt wurden, und klicken Sie dann diesen Gruppen der Benutzer neue Konten hinzufügen. Je nach Ihrer Gruppenstrategie für die in der Gesamtstruktur legacy müssen Sie die lokalen Domänengruppen für den Ressourcenzugriff zu erstellen, oder konvertieren vorhandene Gruppen für lokale Domänengruppen, um die neuen Konten für Ressourcengruppen hinzugefügt werden können. Konzentrieren sich zunächst auf die meisten kritischen Anwendungen und Daten, und sie in die neue Umgebung (mit oder ohne SID-Verlauf) zu migrieren, können Sie die Menge der Aufwand in der Legacyumgebung einschränken.  
  

  
### <a name="servers-and-workstations"></a>Server und Arbeitsstationen  
Bei der herkömmlichen Migration von einer Active Directory ist der Gesamtstruktur auf einem anderen, Migrieren von Computern häufig relativ einfach im Vergleich zum Migrieren von Benutzern, Gruppen und Anwendungen. Abhängig von der Computerrolle kann die Migration zu einer neuen Gesamtstruktur so einfach wie eine alte Domäne getrennt, und verknüpfen eine neue sein. Computerkonten intakt migrieren allerdings in eine makellose Gesamtstruktur widerlegen des Zwecks des Erstellens einer neuen Umgebung. Anstatt die Migration (potenziell kompromittierte, falsch konfigurierten oder veraltet) in eine neue Gesamtstruktur-Computerkonten, sollten Sie die Server und Arbeitsstationen in der neuen Umgebung neu installieren. Sie können Daten von Systemen in der Gesamtstruktur legacy-Systeme in der ursprünglichen Gesamtstruktur, aber nicht die Systeme, die Daten des Hauses migrieren.  
  
### <a name="applications"></a>Anwendungen  

Anwendungen können die wichtigste Herausforderung bei jeder Migration aus einer Gesamtstruktur in eine andere vorhanden, aber bei einer Migration "nonmigratory" ist eines der grundlegenden Prinzipien, die Sie angewendet werden soll, dass Anwendungen in der Gesamtstruktur makellose aktuellen werden soll, unterstützt und neu installiert. Daten können von Anwendungsinstanzen in der alten Gesamtstruktur möglichst migriert werden. In Situationen, in denen eine Anwendung "in der ursprünglichen Gesamtstruktur neu erstellt werden kann", sollten Sie Ansätze wie z. B. creative Zerstörung oder Isolierung von legacy-Anwendungen, wie im folgenden Abschnitt beschrieben.  
  
### <a name="implementing-creative-destruction"></a>Implementieren von Creative Zerstörung  
Creative Zerstörung ist ein Wirtschaftlichkeit-Ausdruck, der beschreibt, wirtschaftliche Entwicklung durch die Zerstörung von einer vorherigen Reihenfolge erstellt. In den letzten Jahren wurde der Begriff auf Informationstechnologie angewendet. Er verweist in der Regel auf die Mechanismen, durch die alten Infrastruktur beseitigt ist, nicht durch ein Upgrade, aber sie durch etwas vollständig neues ersetzen. Die 2011 [Gartner Symposium ITXPO](http://www.gartner.com/technology/symposium/orlando/) für CIOs und IT-Führungskräften creative Zerstörung als eines der wichtigen Themen für die Reduzierung der Kosten und erhöht in Effizienz angezeigt. Verbesserungen bei der Sicherheit sind als Balanceakt des Prozesses möglich.  

Beispielsweise kann eine Organisation aus mehreren Geschäftseinheiten bestehen, die eine andere Anwendung verwenden, die ähnliche Funktionalität, mit verschiedenen Isolationsgraden Modernity und Anbieter nicht unterstützt wird. In der Vergangenheit IT möglicherweise verantwortlich für die einzelnen Geschäftseinheiten Anwendung separat Verwaltung und Konsolidierung bemühungen würde es wird versucht, um zu ermitteln, welche Anwendung die beste Funktionalität zur Verfügung und das anschließende Migrieren von Daten in die bestehen die Anwendung von den anderen.  
  
In creative Zerstörung anstatt veraltete oder redundante Anwendungen verwalten Sie völlig neue Anwendungen, ersetzen Sie die alte, Migrieren von Daten in die neuen Anwendungen zu implementieren und außer Betrieb setzen die alten Anwendungen und die Systeme, auf denen sie ausgeführt. In einigen Fällen können creative Zerstörung von Legacyanwendungen durch Bereitstellen einer neuen Anwendung in Ihrer eigenen Infrastruktur implementiert, aber nach Möglichkeit sollten Sie die Anwendung in einer Cloud-basierten Lösung stattdessen portieren.  
  
Durch die Bereitstellung von Cloud-basierte Anwendungen interne Legacyanwendungen ersetzen Sie nicht nur Wartung einfacher wird und die Kosten reduzieren, aber Sie reduzieren Angriffsfläche Ihrer Organisation durch Wegfall der älteren Systemen und Anwendungen, die Sicherheitsrisiken darstellen Angreifer nutzen. Dieser Ansatz bietet eine schnellere Methode für eine Organisation, um die gewünschte Funktionalität zu erhalten, sodass Sie gleichzeitig ältere Ziele in der Infrastruktur. Obwohl das Prinzip der kreative Zerstörung nicht für alle IT-Ressourcen gilt, wird eine häufig geeignete Option zum Eliminieren von älteren Systemen und Anwendungen während der Bereitstellung von gleichzeitig stabile, sichere, in der Cloud-basierten Anwendungen.  
  
### <a name="isolating-legacy-systems-and-applications"></a>Isolieren ältere Systeme und Anwendungen  
Migrieren Ihre geschäftskritischen Benutzer und Systeme, auf eine makellose, sichere Umgebung Balanceakt ist, dass es sich bei Ihrer Gesamtstruktur legacy weniger wertvolle Informationen und Systeme enthält. Obwohl die älteren Systemen und Anwendungen, die zurückbleiben, in dem weniger sicheren Umgebung erhöhten Risiko einer Kompromittierung vorhanden sein können, stellen sie außerdem einen geringeren Schweregrad der Gefährdung dar. Homing und modernisieren Ihre geschäftskritischen Ressourcen, können Sie sich konzentrieren auf Bereitstellung effektive Verwaltung und Überwachung von beim ohne legacy-Einstellungen und Protokollen zu ermöglichen.  
  
Wenn Sie Ihre kritischen Daten in eine makellose Gesamtstruktur verwaltet haben, können Sie Optionen zum Auswerten weiter zu isolieren, ältere Systeme und Anwendungen in der "main" AD DS-Gesamtstruktur. Obwohl Sie implementieren, können creative Zerstörung zum Ersetzen einer Anwendung und den Servern, die auf denen er ausgeführt wird, in anderen Fällen sollten zusätzliche Isolierung der am wenigsten sichere Systeme und Anwendungen Sie. Z. B. Erstellen einer Anwendung, die durch eine Reihe von Benutzern verwendet wird, aber erfordert, dass ältere Anmeldeinformationen wie LAN-Manager-Hashwerte auf eine kleine Domäne migriert werden, können, Sie um Systeme zu unterstützen, für die Sie keine Optionen für das ersetzen verfügen.  
  
Durch diese Systeme von Domänen, in denen Implementierung von älteren Einstellungen gezwungen ist, entfernen, können Sie anschließend die Sicherheit der Domänen erhöhen, durch konfigurieren, um nur die aktuellen Betriebssystemen und Anwendungen zu unterstützen. Allerdings es empfehlenswert, zur Außerbetriebnahme von älteren Systemen und Anwendungen, wann immer möglich ist. Wenn außerbetriebsetzung einfach nicht für ein kleines Segment Ihrer legacy-Flotte möglich ist, können Sie es in einer separaten Domäne (oder Gesamtstruktur) ausschließen inkrementelle Verbesserungen, die im weiteren Verlauf der Vorgänger-Installation ausführen.  
  
### <a name="simplifying-security-for-end-users"></a>Vereinfachung der Sicherheit für Endbenutzer  
In den meisten Organisationen haben Benutzer mit Zugriff auf die vertraulichen Informationen aufgrund der Art ihrer Rollen in der Organisation ist häufig die möglichst geringem Zeitaufwand zu lernen, komplexe zugriffsbeschränkungen und Steuerelemente zu widmen. Auch wenn Sie eine umfassende Education-Programm für alle Benutzer in Ihrer Organisation haben, sollten Sie auch konzentrieren auf die Sicherheit so einfach wie möglich durch die Implementierung der Steuerelemente, die transparent und vereinfachen Prinzipien auf die Benutzer verwenden entsprechen.  
  
Beispielsweise können Sie eine Richtlinie definieren, in der Führungskräften und anderen virtuellen IP-Adressen erforderlich sind, sichere Arbeitsstationen zu verwenden, um den Zugriff auf vertrauliche Daten und Systeme, sodass sie ihren anderen Geräten zu verwenden, um weniger vertrauliche Daten zuzugreifen. Dies ist eine einfache Prinzip zu merken, aber Sie können eine Reihe von Back-End-Steuerelementen können Sie zum Erzwingen des Ansatzes implementieren.  

Können Sie [Authentifizierungsmechanismuszusicherung](https://technet.microsoft.com/library/dd391847(v=WS.10).aspx) , die Benutzern auf sensible Daten zugreifen, nur, wenn sie ihre Systeme zu schützen ihre Smartcards mit angemeldet haben, und Verwenden von IPsec und Zuweisen von Einschränkungen für die Kontrolle der Systeme, die von denen sie auf vertrauliche Datenrepositorys eine Verbindung herstellen können. Können Sie die [Microsoft-Toolkit zur Datenklassifizierung](https://www.microsoft.com/download/details.aspx?id=27123) zum Erstellen einer robusten dateiklassifizierungsinfrastruktur und Sie können implementieren [Dynamic Access Control](http://blogs.technet.com/b/windowsserver/archive/2012/05/22/introduction-to-windows-server-2012-dynamic-access-control.aspx) den Zugriff auf Daten auf der Grundlage beschränken Eigenschaften der einen Zugriffsversuch, die Übersetzung von Geschäftsregeln in technische Sicherheitselemente.  
  
Aus der Perspektive des Benutzers, den Zugriff auf vertrauliche Daten aus einem gesicherten "einfach funktioniert?", und es wird versucht, die von einem ungesicherten System dazu "einfach nicht." Allerdings werden aus der Perspektive der Überwachung und Verwaltung Ihrer Umgebung, Sie dazu bei, identifizierbaren Muster im wie Benutzer vertrauliche Daten und Systeme erleichtert es Ihnen zugreifen, erkennen anomale Zugriffsversuche erstellen.  
  
In Umgebungen, in denen Absicherung gegen lange, komplexe Kennwörter nicht genügend Kennwortrichtlinien, insbesondere für die VIP-Benutzer, resultiert, sollten Sie alternativen Ansätze zur Authentifizierung, egal ob über Smartcards (die in einer Reihe von Formfaktoren stammen und mit zusätzlichen Funktionen zur Stärkung der Authentifizierung) vertrauenswürdigen biometrische Steuerelemente wie z. B. Finger Wischen Leser oder sogar Authentifizierungsdaten, die durch gesichert werden Platform Module (TPM) in den Computern der Benutzer-chips. Obwohl Multi-Factor Authentication Angriffen mit gestohlenen Anmeldeinformationen nicht verhindert, wenn ein Computer bereits durch die Vergabe von Benutzer leicht zu bedienende authentifizierungssteuerelemente, gefährdet ist, können Sie robuster Kennwörter für die Konten der Benutzer zuweisen, für die herkömmliche Benutzer Name und Kennwort-Steuerelemente sind sehr unhandlich.  
