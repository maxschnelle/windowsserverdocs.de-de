---
ms.assetid: 6f50476c-a1f1-48fb-999b-76c4c3816496
title: Planen der Gefährdung
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: ee1416a00fc0d347b7e05cb12c83f3d3532d693f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360138"
---
# <a name="planning-for-compromise"></a>Planen der Gefährdung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

*law Nr. 1: Niemand glaubt, dass nichts zu tun hat, bis es passiert.* - [10 unveränderliche Gesetze der Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Notfall Wiederherstellungs Pläne in vielen Unternehmen konzentrieren sich auf die Wiederherstellung nach regionalen Notfällen oder Ausfällen, die zu einem Verlust der Computerdienste führen. Bei der Arbeit mit kompromittierten Kunden wird jedoch häufig feststellen, dass die Wiederherstellung nach einem absichtlichen Kompromiss in Ihren Notfall Wiederherstellungs Plänen fehlt. Dies trifft vor allem dann zu, wenn die Gefährdung zu Diebstahl von geistigem Eigentum oder absichtlicher Zerstörung führt, die logische Grenzen (z. b. die Zerstörung aller Active Directory Domänen oder aller Server) anstelle physischer Grenzen (z. b. Zerstörung eines Rechenzentrums). Obwohl eine Organisation möglicherweise Pläne für die Reaktion auf Vorfälle hat, die die anfänglichen Aktivitäten definieren, die bei der Ermittlung einer Gefährdung durchführen werden, lassen diese Pläne oft die Schritte zur Wiederherstellung nach einem kompromittierten Kompromiss aus  
  
Da Active Directory umfassende Identitäts-und Zugriffs Verwaltungsfunktionen für Benutzer, Server, Arbeitsstationen und Anwendungen bereitstellt, ist es unweigerlich von Angreifern betroffen. Wenn ein Angreifer über einen hohen privilegierten Zugriff auf eine Active Directory Domäne oder einen Domänen Controller verfügt, kann dieser Zugriff genutzt werden, um auf die gesamte Active Directory Gesamtstruktur zuzugreifen, Sie zu steuern oder sogar zu zerstören.  
  
In diesem Dokument wurden einige der gängigsten Angriffe auf Windows und Active Directory und Gegenmaßnahmen erläutert, die Sie implementieren können, um die Angriffsfläche zu reduzieren. die einzige Möglichkeit, die Lösung im Falle einer umfassenden Gefährdung von Active Directory wiederherzustellen, besteht darin, vor dem Auftreten der Kompromittierung vorbereitet. In diesem Abschnitt geht es um weniger technische Implementierungsdetails als in den vorherigen Abschnitten dieses Dokuments, und Sie erfahren mehr über allgemeine Empfehlungen, die Sie zum Erstellen eines ganzheitlichen, umfassenden Ansatzes zum Sichern und Verwalten der wichtigen Anwendungen Ihrer Organisation verwenden können. Geschäfts-und IT-Ressourcen.  
  
Unabhängig davon, ob Ihre Infrastruktur nie angegriffen wurde, den versuchten Verletzungen widerstanden hat oder Angriffe ausgesetzt war und vollständig kompromittiert wurde, sollten Sie die unausweichliche Realität planen, dass Sie erneut und wieder angegriffen werden. Es ist nicht möglich, Angriffe zu verhindern, aber es ist möglicherweise sogar möglich, bedeutende Verletzungen oder einen großen Kompromiss zu vermeiden. Jede Organisation sollte Ihre bestehenden Risiken für das Risikomanagement genau auswerten und notwendige Anpassungen vornehmen, um das Gesamtniveau der Sicherheits Anfälligkeit durch ausgeglichene Investitionen in Verhinderung, Erkennung, Kapselung und Wiederherstellung zu verringern.  
  
Um effektive Schutzmaßnahmen zu gewährleisten und gleichzeitig den Benutzern und Unternehmen, die von Ihrer Infrastruktur und Ihren Anwendungen abhängen, Dienste bereitzustellen, müssen Sie möglicherweise neue Möglichkeiten in Erwägung gezogen werden, um eine Gefährdung in Ihrer Umgebung zu verhindern, zu erkennen und zu gefährden und dann von der Kompromiss. Die in diesem Dokument beschriebenen Vorgehensweisen und Empfehlungen helfen Ihnen möglicherweise nicht, eine kompromittierte Active Directory Installation zu reparieren, aber Sie können Ihnen dabei helfen, Ihre nächste zu sichern.  
  
Empfehlungen für die Wiederherstellung einer Active Directory Gesamtstruktur finden Sie unter [windows Server 2012: Planen der Active Directory Gesamtstruktur Wiederherstellung @ no__t-0. Möglicherweise können Sie verhindern, dass Ihre neue Umgebung vollständig kompromittiert wird. selbst wenn dies nicht möglich ist, verfügen Sie über Tools, die Sie wiederherstellen und die Kontrolle über Ihre Umgebung erlangen.  
  
## <a name="rethinking-the-approach"></a>Umdenken des Ansatzes  
*law, Nummer 8: Die Schwierigkeit, ein Netzwerk zu verteidigen, ist direkt proportional zu seiner Komplexität.* - [10 unveränderliche Gesetze der Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  
  
Es ist in der Regel gut zu akzeptieren, dass ein Angreifer, unabhängig vom Betriebssystem, System-, Administrator-, Stamm-oder äquivalente Zugriffsrechte auf einen Computer erhalten hat. Dies gilt unabhängig davon, wie viele Maßnahmen zum "bereinigen" der Anlage. Active Directory ist nicht anders. Wenn ein Angreifer in Active Directory privilegierten Zugriff auf einen Domänen Controller oder ein Konto mit weitreichenden Berechtigungen erhalten hat, können Sie das Verzeichnis niemals vollständig wiederherstellen, wenn Sie nicht alle Änderungen des Angreifers oder einer als funktionierend bekannten Sicherung feststellen. vertrauenswürdiger Zustand.  
  
Wenn ein Mitglieds Server oder eine Arbeitsstation kompromittiert und von einem Angreifer geändert wird, ist der Computer nicht mehr vertrauenswürdig, aber benachbarte nicht gefährdete Server und Arbeitsstationen können weiterhin vertrauenswürdig sein. Die Kompromittierung eines Computers impliziert nicht, dass alle Computer kompromittiert sind.  
  
In einer Active Directory Domäne hosten alle Domänen Controller jedoch Replikate derselben AD DS Datenbank. Wenn ein einzelner Domänen Controller kompromittiert ist und ein Angreifer die AD DS Datenbank ändert, werden diese Änderungen auf allen anderen Domänen Controllern in der Domäne repliziert, und zwar abhängig von der Partition, in der die Änderungen vorgenommen werden, der Gesamtstruktur. Auch wenn Sie jeden Domänen Controller in der Gesamtstruktur neu installieren, müssen Sie die Hosts, auf denen sich die AD DS Datenbank befindet, einfach neu installieren. Böswillige Änderungen an Active Directory werden so problemlos auf neu installierte Domänen Controller repliziert, wie Sie auf Domänen Controllern repliziert werden, die seit Jahren ausgeführt werden.  
  
Bei der Bewertung kompromittierter Umgebungen wird häufig feststellen, dass das Ereignis, das als erste Sicherheitsverletzung angesehen wurde, tatsächlich nach Wochen, Monaten oder sogar Jahren ausgelöst wurde, nachdem Angreifer die Umgebung anfänglich kompromittiert hatten. Angreifer haben in der Regel die Anmelde Informationen für Konten mit hohen Berechtigungen erhalten, bevor eine Sicherheitsverletzung erkannt wurde, und diese Konten genutzt, um das Verzeichnis, die Domänen Controller, Mitglieds Server, Arbeitsstationen und sogar verbundene nicht-Windows zu kompromittieren. Systeme.  
  
Diese Ergebnisse sind mit mehreren Ergebnissen in den 2012-Berichten für die Datenverletzung von Verizon konsistent, in denen Folgendes angezeigt wird:  
  
-   98 Prozent der Datenverletzungen von externen Agents  
  
-   85 Prozent der Datenverletzungen haben Wochen oder mehr zum Ermitteln benötigt.  
  
-   92 Prozent der Vorfälle wurden von einem Drittanbieter erkannt.  
  
-   97 Prozent der Verstöße waren durch einfache oder zwischen Steuerelemente vermeidbar.  
  
Eine Gefährdung des zuvor beschriebenen Grades ist praktisch irreparabel, und die Standard Empfehlung "vereinfachen und neu erstellen" für jedes gefährdete System ist einfach nicht realisierbar oder sogar möglich, wenn Active Directory kompromittiert oder zerstört wurde. Selbst wenn die Wiederherstellung in einen bekannten Zustand funktioniert, werden die Fehler, die eine Gefährdung der Umgebung ermöglichten, nicht beseitigt.  
  
Obwohl Sie alle Facetten ihrer Infrastruktur verteidigen müssen, muss ein Angreifer nur genügend Mängel in ihren Verteidigungsmaßnahmen finden, um das gewünschte Ziel zu erreichen. Wenn Ihre Umgebung relativ einfach und intakt und in der Vergangenheit gut verwaltet ist, kann die Implementierung der Empfehlungen, die weiter oben in diesem Dokument bereitgestellt werden, ein einfacher Vorschlag sein.  
  
Wir haben jedoch festgestellt, dass der ältere, größere und komplexere die Umgebung ist, umso wahrscheinlicher ist es, dass die Empfehlungen in diesem Dokument nicht mehr implementiert werden können. Es ist wesentlich schwieriger, eine Infrastruktur zu sichern, als Sie neu starten und eine Umgebung erstellen können, die gegen Angriffe und Gefährdung resistent ist. Wie bereits erwähnt, ist es aber nicht von geringem Unternehmen, eine gesamte Active Directory Gesamtstruktur neu zu erstellen. Aus diesen Gründen wird empfohlen, einen fokussierten zielgerichteten Ansatz zum Sichern Ihrer Active Directory Gesamtstrukturen zu erhalten.  
  
Anstatt sich mit dem Schwerpunkt zu beschäftigen und alle Probleme zu beheben, die "beschädigt" sind, sollten Sie sich einen Ansatz ansehen, bei dem Sie basierend auf dem, was für Ihr Unternehmen und ihre Infrastruktur am wichtigsten ist, priorisieren. Anstatt zu versuchen, eine Umgebung zu beheben, die mit veralteten, falsch konfigurierten Systemen und Anwendungen gefüllt ist, sollten Sie eine neue kleine, sichere Umgebung erstellen, in der Sie die Benutzer, Systeme und Informationen, die für Ihre Wirtschafts.  
  
In diesem Abschnitt wird ein Ansatz beschrieben, mit dem Sie eine ungeschützte AD DS Gesamtstruktur erstellen können, die als "Lebenszyklus" oder "sichere Zelle" für Ihre zentrale Geschäftsinfrastruktur fungiert. Eine unberührte Gesamtstruktur ist einfach eine neu installierte Active Directory Gesamtstruktur, die in der Regel in Größe und Bereich beschränkt ist und die mit aktuellen Betriebssystemen, Anwendungen und den in der [Reduzierung des Active Directory Angriffs beschriebenen Prinzipien erstellt wird. -Oberfläche](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md).  
  
Indem Sie die empfohlenen Konfigurationseinstellungen in einer neu erstellten Gesamtstruktur implementieren, können Sie eine AD DS Installation erstellen, die von Grund auf mit sicheren Einstellungen und Verfahren erstellt wurde, und Sie können die Herausforderungen, die die Unterstützung älterer Systeme begleiten, reduzieren und Bereich. Ausführliche Anweisungen für den Entwurf und die Implementierung einer unverfälAD DS Installation sind nicht Gegenstand dieses Dokuments. Sie sollten jedoch einige allgemeine Prinzipien und Richtlinien befolgen, um eine "sichere Zelle" zu erstellen, in die Sie Ihre kritischsten Grenzen bringen können. Werten. Diese Richtlinien lauten wie folgt:  
  
1.  Identifizieren Sie die Prinzipien für das getrennte und sichere sichern kritischer Ressourcen.  
  
2.  Definieren Sie einen eingeschränkten, risikobasierten Migrationsplan.  
  
3.  Nutzen Sie ggf. "nicht Migrationen"-Migrationen.  
  
4.  Implementieren Sie "Creative Zerstörung".  
  
5.  Isolieren Sie ältere Systeme und Anwendungen.  
  
6.  Vereinfachen Sie die Sicherheit für Endbenutzer.  
  
### <a name="identifying-principles-for-segregating-and-securing-critical-assets"></a>Erkennen von Prinzipien zum Trennen und sichern kritischer Ressourcen  

Die Merkmale der unberührten Umgebung, die Sie zum beherbergen kritischer Ressourcen erstellen, können stark variieren. Sie können z. b. eine unberührte Gesamtstruktur erstellen, in die nur VIP-Benutzer und sensible Daten migriert werden, auf die nur diese Benutzer zugreifen können. Sie können eine ungeschützte Gesamtstruktur erstellen, in der Sie nicht nur VIP-Benutzer migrieren, sondern Sie als administrative Gesamtstruktur implementieren. dabei werden die in [reduzieren der Active Directory Angriffsfläche](../../../ad-ds/plan/security-best-practices/../../../ad-ds/plan/security-best-practices/Reducing-the-Active-Directory-Attack-Surface.md) beschriebenen Prinzipien zum Erstellen sicherer Administrator Konten implementiert. und Hosts, die verwendet werden können, um Ihre Legacy-Gesamtstrukturen aus der unberührten Gesamtstruktur zu verwalten. Sie können eine "zweckgebundene" Gesamtstruktur implementieren, die VIP-Konten, privilegierte Konten und Systeme mit zusätzlichen Sicherheitsfunktionen erfordert, wie z. b. Server, auf denen Active Directory Zertifikat Dienste (AD CS) ausgeführt werden, mit dem einzigen Ziel, Sie von weniger Sicherheit zu trennen. Wester. Schließlich können Sie eine nicht vollständig vorhandene Gesamtstruktur implementieren, die der Speicherort für alle neuen Benutzer, Systeme, Anwendungen und Daten ist, sodass Sie Ihre Legacy-Gesamtstruktur schließlich per Nachweis außer Betrieb nehmen können.  
  
Unabhängig davon, ob Ihre ursprüngliche Gesamtstruktur eine Handvoll Benutzer und Systeme enthält oder die Basis für eine aggressivere Migration ist, sollten Sie diese Prinzipien in ihrer Planung beachten:  
  
1.  Nehmen Sie an, dass Ihre Legacy-Gesamtstrukturen kompromittiert wurden.  
  
2.  Konfigurieren Sie keine ursprüngliche Umgebung, um einer Legacy Gesamtstruktur zu vertrauen. Sie können jedoch eine Legacy Umgebung so konfigurieren, dass eine nicht vertrauenswürdige Gesamtstruktur vertrauenswürdig ist.  
  
3.  Migrieren Sie Benutzerkonten oder Gruppen nicht aus einer Legacy-Gesamtstruktur in eine ursprüngliche Umgebung, wenn es möglich ist, dass die Gruppenmitgliedschaften, der SID-Verlauf oder andere Attribute der Konten in böswilliger Absicht geändert wurden. Verwenden Sie stattdessen "nicht-Migrations Ansätze", um eine unberührte Gesamtstruktur aufzufüllen. (Nicht wandernde Ansätze werden weiter unten in diesem Abschnitt beschrieben.)  
  
4.  Migrieren Sie keine Computer aus Legacy-Gesamtstrukturen zu unberührten Gesamtstrukturen. Implementieren Sie neu installierte Server in der unberührten Gesamtstruktur, installieren Sie Anwendungen auf den neu installierten Servern, und migrieren Sie Anwendungsdaten zu den neu installierten Systemen. Kopieren Sie für Dateiserver Daten auf neu installierte Server, legen Sie ACLs mithilfe von Benutzern und Gruppen in der neuen Gesamtstruktur fest, und erstellen Sie dann Druckserver auf ähnliche Weise.  
  
5.  Erlauben Sie nicht, ältere Betriebssysteme oder Anwendungen in der ursprünglichen Gesamtstruktur zu installieren. Wenn eine Anwendung nicht aktualisiert und neu installiert werden kann, lassen Sie Sie in der Legacy-Gesamtstruktur aus, und denken Sie daran, die Funktionalität der Anwendung zu ersetzen.  
  
### <a name="defining-a-limited-risk-based-migration-plan"></a>Definieren eines beschränkten, risikobasierten Migrationsplans  
Das Erstellen eines begrenzten, risikobasierten Migrationsplans bedeutet einfach, dass Sie bei der Entscheidung, welche Benutzer, Anwendungen und Daten in ihre ursprüngliche Gesamtstruktur migriert werden sollen, Migrations Ziele ermitteln müssen, die auf dem Grad des Risikos basieren, dem Ihre Organisation ausgesetzt ist, wenn eines der die Benutzer oder Systeme sind gefährdet. VIP-Benutzer, deren Konten höchstwahrscheinlich von Angreifern als Ziel festgenommen werden, sollten in der unberührten Gesamtstruktur abgelegt werden. Anwendungen, die wichtige Geschäftsfunktionen bereitstellen, sollten auf neu erstellten Servern in der ursprünglichen Gesamtstruktur installiert werden, und hochsensible Daten sollten auf gesicherte Server in der ursprünglichen Gesamtstruktur verschoben werden.  
  
Wenn Sie nicht bereits über ein eindeutiges Bild der geschäftskritischen Benutzer, Systeme, Anwendungen und Daten in Ihrer Active Directory Umgebung verfügen, können Sie die Geschäftseinheiten verwenden, um Sie zu identifizieren. Alle Anwendungen, die für das Unternehmen erforderlich sind, sollten identifiziert werden, ebenso wie alle Server, auf denen kritische Anwendungen ausgeführt werden, oder wichtige Daten gespeichert werden. Indem Sie die Benutzer und Ressourcen identifizieren, die für Ihre Organisation erforderlich sind, können Sie eine auf natürliche Weise priorisierte Sammlung von Ressourcen erstellen, auf die Sie sich konzentrieren möchten.  
  
### <a name="leveraging-nonmigratory-migrations"></a>Nutzen von "nicht Migrationen"-Migrationen  
Ob Sie wissen, dass Ihre Umgebung kompromittiert wurde, dass Sie kompromittiert wurde, oder Sie bevorzugen, ältere Daten und Objekte nicht von einer Legacy-Active Directory Installation zu einer neuen zu migrieren, sollten Migrations Ansätze in Erwägung ziehen, die technisch nicht "migrieren"-Objekte.  
  
### <a name="user-accounts"></a>Benutzerkonten  
Bei einer herkömmlichen Active Directory Migration von einer Gesamtstruktur zu einer anderen wird das SIDHistory-Attribut (SID-Verlauf) für Benutzer Objekte zum Speichern der Benutzer-SID und der SIDs von Gruppen verwendet, in denen Benutzer Mitglieder der Legacy Gesamtstruktur waren. Wenn Benutzerkonten zu einer neuen Gesamtstruktur migriert werden und Sie auf Ressourcen in der Legacy-Gesamtstruktur zugreifen, werden die SIDs im SID-Verlauf verwendet, um ein Zugriffs Token zu erstellen, mit dem Benutzer auf Ressourcen zugreifen können, auf die Sie vor dem Migrieren der Konten zugreifen konnten.  
  
Das Verwalten des SID-Verlaufs ist in einigen Umgebungen jedoch bereits problematisch, da das Auffüllen der Zugriffs Token von Benutzern mit aktuellen und historischen SIDs das tokenbloat zur Folge haben kann. Tokenbloat ist ein Problem, bei dem die Anzahl der SIDs, die im Zugriffs Token eines Benutzers gespeichert werden müssen, die im Token verfügbare Menge an Speicherplatz verwendet oder überschreitet.  
  
Obwohl die Größe von tokengrößen auf einen begrenzten Block erweitert werden kann, besteht die ultimative Lösung für tokenbloat darin, die Anzahl der mit Benutzerkonten verknüpften SIDs zu reduzieren, ob durch das rationalisieren von Gruppenmitgliedschaften, das Eliminieren des SID-Verlaufs oder eine Kombination aus beidem. Weitere Informationen zum tokenbloat finden Sie unter [MaxTokenSize und Kerberos Token Bloat](http://blogs.technet.com/b/shanecothran/archive/2010/07/16/maxtokensize-and-kerberos-token-bloat.aspx).  
  
Anstatt Benutzer aus einer Legacy Umgebung (insbesondere eine, in der Gruppenmitgliedschaften und SID-Verläufe kompromittiert werden können) mithilfe des SID-Verlaufs zu migrieren, sollten Sie die Verwendung von metaverzeichnisanwendungen zum Migrieren von Benutzern, ohne die SID-Verläufe in der neuen Gesamtstruktur. Wenn Benutzerkonten in der neuen Gesamtstruktur erstellt werden, können Sie eine metaverzeichnisanwendung verwenden, um die Konten den entsprechenden Konten in der Legacy-Gesamtstruktur zuzuordnen.  
  
Um den neuen Benutzerkonten den Zugriff auf Ressourcen in der Legacy-Gesamtstruktur zu ermöglichen, können Sie mithilfe der metaverzeichnistools Ressourcengruppen identifizieren, denen die Legacy Konten der Benutzer Zugriff gewährt haben, und dann die neuen Konten der Benutzer diesen Gruppen hinzufügen. Abhängig von ihrer Gruppen Strategie in der Legacy-Gesamtstruktur müssen Sie möglicherweise lokale Domänen Gruppen für den Zugriff auf Ressourcen erstellen oder vorhandene Gruppen in lokale Domänen Gruppen konvertieren, damit die neuen Konten Ressourcengruppen hinzugefügt werden können. Wenn Sie sich zunächst auf die wichtigsten Anwendungen und Daten konzentrieren und Sie in die neue Umgebung migrieren (mit oder ohne SID-Verlauf), können Sie den Umfang des Aufwands in der Legacy Umgebung einschränken.  
  

  
### <a name="servers-and-workstations"></a>Server und Arbeitsstationen  
Bei einer herkömmlichen Migration von einer Active Directory-Gesamtstruktur zu einer anderen ist die Migration von Computern im Vergleich zum Migrieren von Benutzern, Gruppen und Anwendungen häufig relativ einfach. Abhängig von der Computer Rolle kann die Migration zu einer neuen Gesamtstruktur so einfach sein wie das Aufheben der Trennung einer alten Domäne und das beitreten zu einer neuen Gesamtstruktur. Das Migrieren von Computer Konten in eine unberührte Gesamtstruktur würde jedoch den Zweck der Erstellung einer neuen Umgebung zunichte machen. Anstatt (potenziell kompromittierte, falsch konfigurierte oder veraltete) Computer Konten in eine neue Gesamtstruktur zu migrieren, sollten Sie Server und Arbeitsstationen in der neuen Umgebung neu installieren. Sie können Daten aus Systemen in der Legacy-Gesamtstruktur zu Systemen in der unberührten Gesamtstruktur migrieren, jedoch nicht zu den Systemen, die die Daten beherbergen.  
  
### <a name="applications"></a>Anwendungen  

Anwendungen können die größte Herausforderung bei der Migration von einer Gesamtstruktur zu einer anderen darstellen, aber im Fall einer "nicht migrationalen" Migration sollten Sie eine der grundlegendsten Prinzipien anwenden, wenn Anwendungen in der ursprünglichen Gesamtstruktur aktuell sind, unterstützt und neu installiert. Nach Möglichkeit können Daten von Anwendungs Instanzen in der alten Gesamtstruktur migriert werden. In Situationen, in denen eine Anwendung nicht in der ursprünglichen Gesamtstruktur "neu erstellt" werden kann, sollten Sie Ansätze wie die kreative Zerstörung oder die Isolation von Legacy Anwendungen wie im folgenden Abschnitt beschrieben berücksichtigen.  
  
### <a name="implementing-creative-destruction"></a>Implementieren von Creative Destruction  
Creative Destruction ist ein Wirtschaftsbegriff, der die wirtschaftliche Entwicklung beschreibt, die durch die Zerstörung einer früheren Bestellung erstellt wurde. In den letzten Jahren wurde der Begriff auf die Informationstechnologie angewendet. Er bezieht sich in der Regel auf Mechanismen, durch die die alte Infrastruktur entfernt wird, nicht durch ein Upgrade, sondern durch eine vollständig neue Ersetzung. Das 2011 [Gartner-Symposium (ITxpo](http://www.gartner.com/technology/symposium/orlando/) ) für CIOs und leitende IT-Führungskräfte stellte kreative Zerstörung als eines der wichtigsten Designs für Kostensenkung und Steigerung der Effizienz dar. Verbesserungen der Sicherheit sind als natürlicher Ausfall des Prozesses möglich.  

Beispielsweise kann eine Organisation aus mehreren Geschäftseinheiten bestehen, die eine andere Anwendung verwenden, die eine ähnliche Funktionalität mit unterschiedlichen Stufen von Modernität und Hersteller Unterstützung ausführt. In der Vergangenheit war es möglicherweise für die getrennte Verwaltung der einzelnen Geschäftseinheiten zuständig, und bei der Konsolidierung besteht der Versuch, herauszufinden, welche Anwendung die beste Funktionalität bot, und dann die Daten zu migrieren. Anwendung von anderen.  
  
Bei der kreativen Zerstörung, anstatt veraltete oder redundante Anwendungen zu verwalten, implementieren Sie völlig neue Anwendungen, um die alte zu ersetzen, Daten in die neuen Anwendungen zu migrieren und die alten Anwendungen und die Systeme, auf denen Sie ausgeführt werden, außer Betrieb zu setzen. In einigen Fällen können Sie eine kreative Zerstörung von Legacy Anwendungen implementieren, indem Sie eine neue Anwendung in ihrer eigenen Infrastruktur bereitstellen. Sie sollten die Anwendung jedoch möglichst in eine cloudbasierte Lösung portieren.  
  
Indem Sie cloudbasierte Anwendungen bereitstellen, um ältere interne Anwendungen zu ersetzen, verringern Sie nicht nur den Wartungsaufwand und die Kosten, sondern reduzieren die Angriffsfläche Ihrer Organisation, indem Sie Legacy Systeme und Anwendungen, die Sicherheitsrisiken darstellen, eliminieren. , den Angreifer nutzen können. Diese Vorgehensweise ermöglicht es einer Organisation, die gewünschte Funktionalität zu erhalten und gleichzeitig Legacy Ziele in der Infrastruktur zu eliminieren. Obwohl das Prinzip der kreativen Zerstörung nicht für alle IT-Ressourcen gilt, bietet es eine häufig verwendbare Option zum eliminieren älterer Systeme und Anwendungen, während gleichzeitig robuste, sichere und cloudbasierte Anwendungen bereitgestellt werden.  
  
### <a name="isolating-legacy-systems-and-applications"></a>Isolieren von Legacy Systemen und Anwendungen  
Ein natürliches Wachstum bei der Migration Ihrer geschäftskritischen Benutzer und Systeme in eine unberührte, sichere Umgebung besteht darin, dass Ihre Legacy-Gesamtstruktur weniger wertvolle Informationen und Systeme enthalten wird. Obwohl ältere Systeme und Anwendungen, die in der weniger sicheren Umgebung verbleiben, das Risiko einer Gefährdung darstellen können, stellen Sie auch einen geringeren Schweregrad der Gefährdung dar. Indem Sie Ihre wichtigen Geschäftsressourcen neu Hosting und modernisieren, können Sie sich auf die Bereitstellung effektiver Verwaltungs-und Überwachungsfunktionen konzentrieren, ohne ältere Einstellungen und Protokolle zu erfüllen.  
  
Wenn Sie Ihre wichtigen Daten in einer unberührten Gesamtstruktur wieder hergestellt haben, können Sie die Optionen zur weiteren Isolierung von Legacy Systemen und Anwendungen in ihrer "Main"-AD DS Gesamtstruktur auswerten. Obwohl Sie eine kreative Zerstörung implementieren können, um eine Anwendung und die Server, auf denen Sie ausgeführt wird, zu ersetzen, können Sie in anderen Fällen eine zusätzliche Isolation der am wenigsten sicheren Systeme und Anwendungen in Erwägung gezogen. Beispielsweise kann eine Anwendung, die von einigen wenigen Benutzern verwendet wird, aber ältere Anmelde Informationen wie LAN-Manager-Hashes erfordert, zu einer kleinen Domäne migriert werden, die Sie erstellen, um Systeme zu unterstützen, für die keine Ersatzoptionen vorhanden sind.  
  
Indem Sie diese Systeme aus Domänen entfernen, in denen Sie die Implementierung veralteter Einstellungen erzwingen, können Sie die Sicherheit der Domänen anschließend erhöhen, indem Sie Sie so konfigurieren, dass nur aktuelle Betriebssysteme und Anwendungen unterstützt werden. Es empfiehlt sich jedoch, ältere Systeme und Anwendungen möglichst außer Betrieb zu nehmen. Wenn die Außerbetriebnahme für ein kleines Segment Ihrer Legacy Population nicht möglich ist, können Sie diese in einer separaten Domäne (oder Gesamtstruktur) aufteilen, um inkrementelle Verbesserungen im Rest der Legacy Installation durchzuführen.  
  
### <a name="simplifying-security-for-end-users"></a>Vereinfachen der Sicherheit für Endbenutzer  
In den meisten Organisationen haben Benutzer, die Zugriff auf die vertraulichsten Informationen aufgrund der Art ihrer Rollen in der Organisation haben, häufig den geringsten Zeitaufwand für das Erlernen komplexer Zugriffsbeschränkungen und-Steuerelemente. Obwohl Sie über ein umfassendes Sicherheits Schulungsprogramm für alle Benutzer in Ihrer Organisation verfügen sollten, sollten Sie sich auch darauf konzentrieren, die Sicherheit so einfach wie möglich zu gestalten, indem Sie Steuerelemente implementieren, die transparent sind, und die Prinzipien vereinfachen, mit denen Benutzer einhält.  
  
Beispielsweise können Sie eine Richtlinie definieren, in der Führungskräfte und andere VIPs für den Zugriff auf sensible Daten und Systeme sichere Arbeitsstationen benötigen, sodass Sie Ihre anderen Geräte für den Zugriff auf weniger sensible Daten verwenden können. Dies ist ein einfaches Prinzip, das Benutzer merken können, aber Sie können eine Reihe von Back-End-Steuerelementen implementieren, um den Ansatz zu erzwingen.  

Mithilfe der [Assurance-Authentifizierung](https://technet.microsoft.com/library/dd391847(v=WS.10).aspx) können Sie Benutzern nur den Zugriff auf sensible Daten gestatten, wenn Sie sich mit ihren Smartcards bei ihren sicheren Systemen angemeldet haben. Außerdem können Sie mithilfe von IPSec und Einschränkungen für Benutzerrechte die Systeme steuern, von denen Sie abhängig sind. Stellen Sie eine Verbindung mit sensiblen Daten Depots her. Sie können das [Microsoft-Toolkit zur Datenklassifizierung](https://www.microsoft.com/download/details.aspx?id=27123) verwenden, um eine robuste Datei Klassifizierungs Infrastruktur zu erstellen, und Sie können [dynamische Access Control](http://blogs.technet.com/b/windowsserver/archive/2012/05/22/introduction-to-windows-server-2012-dynamic-access-control.aspx) implementieren, um den Zugriff auf Daten auf der Grundlage von Merkmalen eines Zugriffs Versuchs einzuschränken und zu übersetzen. Geschäftsregeln in technische Steuerelemente.  
  
Aus Sicht des Benutzers ist der Zugriff auf sensible Daten von einem gesicherten System "funktioniert einfach", und es wird versucht, dies über ein ungesichertes System zu tun. Aus Sicht der Überwachung und Verwaltung Ihrer Umgebung helfen Sie jedoch dabei, identifizierbare Muster in der Art und Weise zu erstellen, in der Benutzer auf sensible Daten und Systeme zugreifen. so können Sie anormale Zugriffsversuche leichter erkennen.  
  
In Umgebungen, in denen Benutzer gegen lange, komplexe Kenn Wörter zu nicht ausreichenden Kenn Wort Richtlinien geführt haben, insbesondere für VIP-Benutzer, sollten Sie alternative Authentifizierungs Ansätze in Erwägung gezogen, ob über Smartcards (in einer Reihe von Formfaktoren und mit zusätzlichen Features zur Verstärkung der Authentifizierung), biometrischen Steuerelementen wie Fingerabdrucklesern oder sogar Authentifizierungsdaten, die durch Trusted Platform Module (TPM)-Chips auf den Computern der Benutzer gesichert werden. Obwohl die mehrstufige Authentifizierung keine Angriffe auf Anmelde Informationen verhindert, wenn ein Computer bereits kompromittiert ist, indem die Benutzer benutzerfreundliche Authentifizierungs Steuerungen erhalten, können Sie den Konten der Benutzer, für die der herkömmliche Benutzer die Steuerelemente für Namen und Kenn Wörter sind unhandlich.  
