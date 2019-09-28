---
ms.assetid: 7a7ab95c-9cb3-4a7b-985a-3fc08334cf4f
title: Implementieren von Verwaltungsmodellen der geringste Rechte
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: c8ad9b00070d5daef2e5aee43cfdee2d192bddae
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367727"
---
# <a name="implementing-least-privilege-administrative-models"></a>Implementieren von Verwaltungsmodellen der geringste Rechte

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der folgende Auszug aus [dem Sicherheits Planungs Handbuch für Administrator Konten](https://technet.microsoft.com/library/cc162797.aspx)wird zuerst am 1. April 1999 veröffentlicht:

> "In den meisten sicherheitsbezogenen Schulungskursen und in der Dokumentation wird die Implementierung eines Prinzips der geringsten Rechte erläutert, die Unternehmen jedoch selten befolgt werden. Das Prinzip ist einfach, und die Auswirkung der ordnungsgemäßen Anwendung erhöht die Sicherheit und verringert das Risiko. Das Prinzip besagt, dass sich alle Benutzer mit einem Benutzerkonto anmelden müssen, das über die absoluten minimalen Berechtigungen verfügt, die zum Ausführen der aktuellen Aufgabe erforderlich sind, und nichts anderes. Dies bietet neben anderen Angriffen auch Schutz vor schädlichem Code. Dieses Prinzip gilt für Computer und die Benutzer dieser Computer.   
> "Ein Grund für dieses Prinzip ist, dass Sie einige interne Untersuchungen durchführen müssen. Beispielsweise müssen Sie die Zugriffsrechte ermitteln, die von einem Computer oder Benutzer tatsächlich benötigt werden, und diese dann implementieren. Für viele Organisationen könnte diese Aufgabe anfänglich wie eine große Menge an Arbeit erscheinen. Es ist jedoch ein wichtiger Schritt, um Ihre Netzwerkumgebung erfolgreich zu schützen.
> "Sie sollten allen Domänen Administrator Benutzern ihre Domänen Berechtigungen gemäß dem Konzept der geringsten Rechte erteilen. Wenn sich beispielsweise ein Administrator mit einem privilegierten Konto anmeldet und versehentlich ein Virus Programm ausführt, hat der Virus Administrator Zugriff auf den lokalen Computer und auf die gesamte Domäne. Wenn sich der Administrator stattdessen mit einem nicht privilegierten Konto (nicht administrativ) angemeldet hätte, wäre der Schaden Bereich des Virus nur der lokale Computer, weil er als lokaler Computerbenutzer ausgeführt wird.
> "In einem anderen Beispiel dürfen Konten, denen Administratorrechte auf Domänen Ebene erteilt werden, in einer anderen Gesamtstruktur nicht über erhöhte Rechte verfügen, auch wenn zwischen den Gesamtstrukturen eine Vertrauensstellung besteht. Diese Taktik hilft bei der Vermeidung von weit verbreiteten Schäden, wenn ein Angreifer die Gefährdung einer verwalteten Gesamtstruktur beeinträchtigt. Organisationen sollten Ihr Netzwerk regelmäßig überwachen, um Schutz vor nicht autorisierter Ausweitung von Berechtigungen zu haben. "  

Der folgende Auszug basiert auf dem [Microsoft Windows Security Resource Kit](https://www.microsoftpressstore.com/store/microsoft-windows-security-resource-kit-9780735621749), das erstmals in 2005 veröffentlicht wurde:  

> "Stellen Sie sich immer die Sicherheit vor, wenn Sie die geringste Menge an Berechtigungen gewähren, die für die Ausführung der Aufgabe erforderlich sind. Wenn eine Anwendung, die über zu viele Berechtigungen verfügt, kompromittiert werden soll, kann der Angreifer den Angriff möglicherweise über die Möglichkeiten hinaus erweitern, wenn die Anwendung unter den geringsten möglichen Berechtigungen hätte. Untersuchen Sie z. b. die Konsequenzen eines Netzwerkadministrators, wenn Sie eine e-Mail-Anlage mit einem Virus öffnen. Wenn der Administrator mit dem Domänen Administrator Konto angemeldet ist, hat der Virus Administratorrechte auf allen Computern in der Domäne und somit uneingeschränkten Zugriff auf fast alle Daten im Netzwerk. Wenn der Administrator mit einem lokalen Administrator Konto angemeldet ist, verfügt der Virus über Administratorrechte auf dem lokalen Computer und kann daher auf alle Daten auf dem Computer zugreifen und Schadsoftware wie z. b. die Protokollierungs Software für Schlüssel Striche auf der Computer. Wenn der Administrator mit einem normalen Benutzerkonto angemeldet ist, kann der Virus nur auf die Daten des Administrators zugreifen und Schadsoftware nicht installieren. Durch die Verwendung der geringsten Rechte, die zum Lesen von e-Mails erforderlich sind, wird in diesem Beispiel der potenzielle Bereich der Gefährdung erheblich reduziert. "  

## <a name="the-privilege-problem"></a>Das Berechtigungs Problem

Die in den vorangehenden Ausschnitten beschriebenen Prinzipien haben sich nicht geändert, aber bei der Bewertung von Active Directory Installationen finden wir ausnahmslos eine übermäßige Anzahl von Konten, denen Rechte und Berechtigungen gewährt wurden, die weit über die für die tägliche Ausführung erforderlichen Berechtigungen hinausgehen. tätig. Die Größe der Umgebung wirkt sich auf die unformatierte Anzahl von übermäßig privilegierten Konten aus, aber nicht auf die proportional großen Verzeichnisse haben möglicherweise Dutzende von Konten in den meisten privilegierten Gruppen, während große Installationen möglicherweise Hunderte oder sogar Tausende haben. Mit wenigen Ausnahmen, unabhängig von der Komplexität der Fähigkeiten und des Arsenals eines Angreifers, verfolgen Angreifer in der Regel den Weg des geringsten Widerstands. Sie erhöhen die Komplexität ihrer Werkzeuge und ihrer Herangehensweise nur dann, wenn und wenn einfachere Mechanismen fehlschlagen oder von Verteidigern vereitelt werden.  

Leider hat sich der Weg des geringsten Widerstands in vielen Umgebungen als die übermäßige Verwendung von Konten mit umfassenden und tiefgreifenden Berechtigungen erwiesen. Allgemeine Berechtigungen sind Rechte und Berechtigungen, die es einem Konto ermöglichen, bestimmte Aktivitäten in einem großen Querschnitt der Umgebung auszuführen, z. b. können Helpdeskmitarbeiter Berechtigungen erhalten, mit denen Sie die Kenn Wörter für viele Benutzerkonten zurücksetzen können.  

Deep-Berechtigungen sind leistungsstarke Berechtigungen, die auf einen schmalen auffüllungs Bereich angewendet werden, z. b. das Erteilen von Administrator Rechten auf einem Server, um Reparaturen ausführen zu können. Weder die allgemeine Berechtigung noch die Tiefe Berechtigung ist zwangsläufig gefährlich. Wenn jedoch viele Konten in der Domäne dauerhaft umfassende und umfassende Berechtigungen gewährt werden und nur eines der Konten kompromittiert ist, kann es schnell zum Neukonfigurieren der Umgebung für die die Zwecke des Angreifers oder sogar das zerstören von großen Segmenten der Infrastruktur.  

Pass-the-Hash-Angriffe, bei denen es sich um einen Typ von Angriffen zum Diebstahl von Anmelde Informationen handelt, sind allgegenwärtig, weil die Tools für die Ausführung frei verfügbar und einfach zu verwenden sind und viele Umgebungen anfällig für Angriffe sind. Pass-the-Hash-Angriffe sind jedoch nicht das wirkliche Problem. Der Kern des Problems ist zweierlei:  

1. Es ist in der Regel einfach, dass ein Angreifer umfassende Berechtigungen auf einem einzelnen Computer erhält und diese Berechtigung dann umfassend an andere Computer weiterleitet.  
2. Es gibt in der Regel zu viele permanente Konten, die über eine hohe Berechtigungsebene innerhalb der gesamten Rechen Landschaft verfügen.

Auch wenn Pass-the-Hash-Angriffe entfernt werden, würden Angreifer einfach andere Taktiken verwenden, nicht eine andere Strategie. Anstatt Schadsoftware zu erstellen, die Tools zum Diebstahl von Anmelde Informationen enthält, könnte Sie Schadsoftware, die Tastatureingaben protokolliert, oder eine beliebige Anzahl anderer Ansätze zum Erfassen von Anmelde Informationen nutzen, die in der gesamten Umgebung leistungsfähig sind. Unabhängig von den Taktiken bleiben die Ziele unverändert: Konten mit umfassenden und tiefgreifenden Berechtigungen.  

Das Gewähren von übermäßigen Berechtigungen wird nicht nur in Active Directory in kompromittierten Umgebungen gefunden. Wenn eine Organisation die Gewohnheit hat, mehr Berechtigungen zu erteilen, als erforderlich ist, wird Sie in der Regel in der gesamten Infrastruktur wie in den folgenden Abschnitten erläutert.  

## <a name="in-active-directory"></a>In Active Directory

In Active Directory wird häufig feststellen, dass die Gruppen "EA", "da" und "BA" eine übermäßige Anzahl von Konten enthalten. In den meisten Fällen enthält die EA-Gruppe einer Organisation die wenigsten Mitglieder, da Gruppen in der Regel einen Multiplikator der Anzahl der Benutzer in der EA-Gruppe enthalten und die Administratoren Gruppen in der Regel mehr Mitglieder als die Auffüllungen der anderen Gruppen enthalten. Dies ist häufig darauf zurückzuführen, dass Administratoren in gewisser Weise "weniger privilegiert" sind als das oder EAS. Obwohl die Rechte und Berechtigungen, die jeder dieser Gruppen gewährt werden, unterschiedlich sind, sollten Sie effektiv als gleichwertig betrachtet werden, da ein Mitglied von einem Mitglied von einem Mitglied der anderen beiden Elemente sein kann.  

## <a name="on-member-servers"></a>Auf Mitglieds Servern

Wenn wir die Mitgliedschaft der lokalen Administratoren Gruppen auf Mitglieds Servern in vielen Umgebungen abrufen, finden wir eine Mitgliedschaft von einigen wenigen lokalen Konten und Domänen Konten bis hin zu Dutzenden von Gruppen Gruppen, die, wenn Sie erweitert werden, Hunderte, sogar Tausende von Konten mit lokalen Administrator Berechtigungen auf den Servern. In vielen Fällen sind Domänen Gruppen mit großen Mitgliedschaften in den lokalen Administratoren Gruppen der Mitglieds Server enthalten, ohne dass Benutzer, die die Mitgliedschaften dieser Gruppen in der Domäne ändern können, die administrative Kontrolle über alle Systeme erhalten können. , in der die Gruppe in einer lokalen Administrator Gruppe eingefügt wurde.  

## <a name="on-workstations"></a>Auf Arbeitsstationen

Obwohl Arbeitsstationen in der Regel deutlich weniger Mitglieder in Ihren lokalen Administratoren Gruppen als Mitglieds Server sind, wird Benutzern in vielen Umgebungen die Mitgliedschaft in der lokalen Gruppe Administratoren auf Ihren eigenen Computern gewährt. Wenn dies der Fall ist, stellen diese Benutzer auch bei aktivierter UAC ein erhöhtes Risiko für die Integrität Ihrer Arbeitsstationen dar.  

> [!IMPORTANT]  
> Sie sollten sorgfältig überlegen, ob Benutzer Administratorrechte auf ihren Arbeitsstationen benötigen. wenn dies der Fall ist, empfiehlt es sich, ein separates lokales Konto auf dem Computer zu erstellen, der Mitglied der Gruppe "Administratoren" ist. Wenn Benutzer eine Rechte Erweiterung benötigen, können Sie die Anmelde Informationen für dieses lokale Konto für die Rechte Erweiterung darstellen, aber da es sich um ein lokales Konto handelt, kann es nicht verwendet werden, um andere Computer zu beeinträchtigen oder auf Domänen Ressourcen zuzugreifen Wie bei allen lokalen Konten sollten die Anmelde Informationen für das lokale privilegierte Konto jedoch eindeutig sein. Wenn Sie ein lokales Konto mit denselben Anmelde Informationen auf mehreren Arbeitsstationen erstellen, machen Sie die Computer für Pass-the-Hash-Angriffe verfügbar.  

## <a name="in-applications"></a>In Anwendungen

Bei Angriffen, bei denen es sich bei dem Ziel um das geistige Eigentum einer Organisation handelt, können Konten, denen innerhalb von Anwendungen leistungsstarke Berechtigungen erteilt wurden, als Ziel für die exfilterung von Daten eingesetzt werden. Obwohl den Konten, die Zugriff auf sensible Daten haben, möglicherweise keine erhöhten Rechte in der Domäne oder dem Betriebssystem erteilt wurden, können Konten, die die Konfiguration einer Anwendung ändern oder auf die von der Anwendung bereitgestellten Informationen zugreifen können. Stellen Sie Risiken dar.  

## <a name="in-data-repositories"></a>In Datenrepository

Wie bei anderen Zielen können Angreifer, die den Zugriff auf geistiges Eigentum in Form von Dokumenten und anderen Dateien suchen, auf die Konten abzielen, die den Zugriff auf die Dateispeicher steuern, Konten, die direkt auf die Dateien zugreifen können, oder sogar Gruppen oder Rollen, die über Zugriff auf die Dateien. Wenn z. b. ein Dateiserver zum Speichern von Vertragsdokumenten verwendet wird und den Dokumenten durch die Verwendung einer Active Directory Gruppe Zugriff gewährt wird, kann ein Angreifer, der die Mitgliedschaft der Gruppe ändern kann, kompromittierte Konten zur Gruppe hinzufügen und auf den Vertrag zugreifen. Dokumenten. In Fällen, in denen der Zugriff auf Dokumente von Anwendungen wie z. b. SharePoint bereitgestellt wird, können Angreifer die Anwendungen wie zuvor beschrieben als Ziel haben.  

## <a name="reducing-privilege"></a>Reduzieren von Berechtigungen

Je größer und komplexer eine Umgebung ist, desto schwieriger ist es, zu verwalten und zu sichern. In kleinen Unternehmen kann das überprüfen und reduzieren von Berechtigungen ein relativ einfacher Vorschlag sein, aber jeder zusätzliche Server, die Arbeitsstation, das Benutzerkonto und die Anwendung, die in einer Organisation verwendet werden, fügt ein weiteres Objekt hinzu, das gesichert werden muss. Da es schwierig oder sogar unmöglich sein kann, alle Aspekte der IT-Infrastruktur eines Unternehmens zu schützen, sollten Sie sich zunächst auf die Konten konzentrieren, deren Berechtigungen das größte Risiko darstellen, bei dem es sich in der Regel um die integrierten privilegierten Konten handelt. Gruppen in Active Directory und privilegierte lokale Konten auf Arbeitsstationen und Mitglieds Servern.  

### <a name="securing-local-administrator-accounts-on-workstations-and-member-servers"></a>Sichern von lokalen Administrator Konten auf Arbeitsstationen und Mitglieds Servern

Obwohl sich dieses Dokument auf die Sicherung von Active Directory konzentriert, wie bereits erläutert wurde, beginnen die meisten Angriffe auf das Verzeichnis als Angriffe gegen einzelne Hosts. Es können keine vollständigen Richtlinien zum Schützen von lokalen Gruppen auf Mitglieds Systemen bereitgestellt werden, aber die folgenden Empfehlungen können verwendet werden, um die lokalen Administrator Konten auf Arbeitsstationen und Mitglieds Servern zu sichern.  

#### <a name="securing-local-administrator-accounts"></a>Sichern von lokalen Administrator Konten

In allen Versionen von Windows, die derzeit unterstützt werden, ist das lokale Administrator Konto standardmäßig deaktiviert, wodurch das Konto für Pass-the-Hash-Angriffe und andere Angriffe auf Anmelde Informationen unbrauchbar wird. In Domänen, die ältere Betriebssysteme enthalten bzw. in denen lokale Administrator Konten aktiviert wurden, können diese Konten jedoch wie zuvor beschrieben verwendet werden, um die Kompromittierung über Mitglieds Server und Arbeitsstationen hinweg weiterzugeben. Aus diesem Grund werden die folgenden Steuerelemente für alle lokalen Administrator Konten auf in die Domäne eingebundenen Systemen empfohlen.  

Ausführliche Anweisungen zum Implementieren dieser Steuerelemente finden Sie in [anhang H: Lokale Administrator Konten und Gruppen werden gesichert @ no__t-0. Stellen Sie vor der Implementierung dieser Einstellungen jedoch sicher, dass lokale Administrator Konten in der Umgebung derzeit nicht verwendet werden, um Dienste auf Computern auszuführen oder andere Aktivitäten auszuführen, für die diese Konten nicht verwendet werden sollen. Testen Sie diese Einstellungen gründlich, bevor Sie Sie in einer Produktionsumgebung implementieren.  

#### <a name="controls-for-local-administrator-accounts"></a>Steuerelemente für lokale Administrator Konten

Integrierte Administrator Konten sollten nie als Dienst Konten auf Mitglieds Servern verwendet werden, und Sie sollten nicht für die Anmeldung bei lokalen Computern (außer im abgesicherten Modus) verwendet werden, auch wenn das Konto deaktiviert ist. Das Ziel der Implementierung der hier beschriebenen Einstellungen besteht darin, zu verhindern, dass das lokale Administrator Konto jedes Computers verwendet wird, es sei denn, die Schutz Kontrollen werden zum ersten Mal umgekehrt Indem Sie diese Steuerelemente implementieren und Administrator Konten für Änderungen überwachen, können Sie die Wahrscheinlichkeit eines Erfolgs eines Angriffs, der auf lokale Administrator Konten abzielt, erheblich reduzieren.  

##### <a name="configuring-gpos-to-restrict-administrator-accounts-on-domain-joined-systems"></a>Konfigurieren von Gruppenrichtlinien Objekten zum Einschränken von Administrator Konten auf in die Domäne eingebundenen Systemen

Fügen Sie in einer oder mehreren Gruppenrichtlinien Objekten, die Sie erstellen und mit dem Arbeitsstations-und Mitglied Server Organisationseinheiten in jeder Domäne verknüpfen, das Administrator Konto den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale richtlinien\benutzerrechte hinzu Zuweisungen**:  

- Zugriff vom Netzwerk auf diesen Computer verweigern
- Anmelden als Batchauftrag verweigern
- Anmelden als Dienst verweigern
- Anmelden über Remotedesktopdienste verweigern

Wenn Sie diesen Benutzerrechten Administrator Konten hinzufügen, geben Sie an, ob Sie das lokale Administrator Konto oder das Domänen Administrator Konto hinzufügen, indem Sie das Konto bezeichnen. Wenn Sie z. b. das Administrator Konto der Domäne nwtraders zu diesen Verweigerungs rechten hinzufügen möchten, geben Sie das Konto als **NWTRADERS\Administrator**ein, oder navigieren Sie zum Administrator Konto für die Domäne nwtraders. Um sicherzustellen, dass Sie das lokale Administrator Konto einschränken, geben Sie in der Gruppenrichtlinienobjekt-Editor in den Einstellungen für Benutzerrechte **Administrator** ein.  

> [!NOTE]  
> Auch wenn lokale Administrator Konten umbenannt werden, gelten die Richtlinien weiterhin.  

Mit diesen Einstellungen wird sichergestellt, dass das Administrator Konto eines Computers nicht zum Herstellen einer Verbindung mit den anderen Computern verwendet werden kann, auch wenn es versehentlich oder böswillig aktiviert ist. Lokale Anmeldungen, die das lokale Administrator Konto verwenden, können nicht vollständig deaktiviert werden, und Sie sollten dies nicht tun, da das lokale Administrator Konto eines Computers für die Verwendung in Notfall Wiederherstellungs Szenarien konzipiert ist.  

Wenn ein Mitglieds Server oder eine Arbeitsstation von der Domäne getrennt wird, ohne dass anderen lokalen Konten Administratorrechte erteilt wurden, kann der Computer im abgesicherten Modus gestartet werden, das Administrator Konto aktiviert werden, und das Konto kann dann verwendet werden, um Reparaturen auf dem Computer. Wenn Reparaturen abgeschlossen sind, sollte das Administrator Konto erneut deaktiviert werden.  

### <a name="securing-local-privileged-accounts-and-groups-in-active-directory"></a>Sichern von lokalen privilegierten Konten und Gruppen in Active Directory

*law-Nummer 6: Ein Computer ist nur so sicher, wie der Administrator vertrauenswürdig ist.* - [zehn unveränderliche Sicherheitsgesetze (Version 2,0)](https://technet.microsoft.com/security/hh278941.aspx)  

Die Informationen, die hier bereitgestellt werden, sollen allgemeine Richtlinien zum Sichern der integrierten Konten und Gruppen mit den meisten Berechtigungen in Active Directory bereitstellen. Ausführliche Schritt-für-Schritt-Anweisungen finden Sie auch in [anhang D: Sichern integrierter Administrator Konten in Active Directory @ no__t-0, [Anhang E: Sichern von Organisations-Admins-Gruppen in Active Directory @ no__t-0, [Anhang F: Sichern von Domänen-Admins-Gruppen in Active Directory @ no__t-0 und in [Anhang G: Sichern von Administratoren Gruppen in Active Directory @ no__t-0.  

Bevor Sie eine dieser Einstellungen implementieren, sollten Sie auch alle Einstellungen gründlich testen, um zu ermitteln, ob Sie für Ihre Umgebung geeignet sind. Nicht alle Organisationen können diese Einstellungen implementieren.  

#### <a name="securing-built-in-administrator-accounts-in-active-directory"></a>Sichern integrierter Administrator Konten in Active Directory

In jeder Domäne in Active Directory wird ein Administrator Konto im Rahmen der Erstellung der Domäne erstellt. Dieses Konto ist standardmäßig Mitglied der Gruppe "Domänen-Admins" und "Administratoren" in der Domäne. wenn es sich bei der Domäne um die Stamm Domäne der Gesamtstruktur handelt, ist das Konto auch Mitglied der Gruppe "Organisations-Admins". Die Verwendung des lokalen Administrator Kontos einer Domäne sollte nur für anfängliche buildaktivitäten und möglicherweise für Notfall Wiederherstellungs Szenarien reserviert werden. Um sicherzustellen, dass ein integriertes Administrator Konto verwendet werden kann, um Reparaturen zu beeinflussen, wenn keine anderen Konten verwendet werden können, sollten Sie die Standardmitgliedschaft des Administrator Kontos in keiner Domäne in der Gesamtstruktur ändern. Stattdessen sollten Sie die Richtlinien befolgen, um das Administrator Konto in jeder Domäne in der Gesamtstruktur zu schützen. Ausführliche Anweisungen zum Implementieren dieser Steuerelemente finden Sie in [anhang D: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

#### <a name="controls-for-built-in-administrator-accounts"></a>Steuerelemente für integrierte Administrator Konten

Das Ziel der Implementierung der hier beschriebenen Einstellungen besteht darin, zu verhindern, dass das Administrator Konto (keine Gruppe) der einzelnen Domänen verwendbar ist, es sei denn, eine Reihe von Steuerelementen wird umgekehrt. Indem Sie diese Steuerelemente implementieren und die Administrator Konten auf Änderungen überwachen, können Sie die Wahrscheinlichkeit eines erfolgreichen Angriffs durch die Nutzung des Administrator Kontos einer Domäne erheblich verringern. Für das Administrator Konto in jeder Domäne in der Gesamtstruktur sollten Sie die folgenden Einstellungen konfigurieren.  

##### <a name="enable-the-account-is-sensitive-and-cannot-be-delegated-flag-on-the-account"></a>Aktivieren Sie das Flag "Konto ist vertraulich und kann nicht delegiert werden" für das Konto.

Standardmäßig können alle Konten in Active Directory delegiert werden. Mithilfe der Delegierung kann ein Computer oder Dienst die Anmelde Informationen für ein Konto, das für den Computer oder den Dienst authentifiziert wurde, an andere Computer übertragen, um Dienste im Namen des Kontos abzurufen. Wenn Sie das Konto aktivieren und das Attribut für ein domänenbasiertes Konto **nicht delegiert werden kann** , können die Anmelde Informationen des Kontos nicht anderen Computern oder Diensten im Netzwerk angezeigt werden. Dadurch werden Angriffe eingeschränkt, von denen die Delegierung zur Verwendung des Anmelde Informationen des Kontos auf anderen Systemen.  

##### <a name="enable-the-smart-card-is-required-for-interactive-logon-flag-on-the-account"></a>Aktivieren Sie das Flag "Smartcard ist für die interaktive Anmeldung erforderlich" für das Konto.

Wenn Sie die **Smartcard für das interaktive Anmelde Attribut für** ein Konto aktivieren, setzt Windows das Kennwort des Kontos auf einen Zufallswert von 120 Zeichen zurück. Wenn Sie dieses Flag für integrierte Administrator Konten festlegen, stellen Sie sicher, dass das Kennwort für das Konto nicht nur lang und komplex ist, sondern keinem Benutzer bekannt ist. Es ist technisch nicht erforderlich, Smartcards für die Konten zu erstellen, bevor Sie dieses Attribut aktivieren. wenn möglich, sollten jedoch Smartcards für jedes Administrator Konto erstellt werden, bevor Sie die Konto Einschränkungen konfigurieren, und die Smartcards sollten in gespeichert werden. sichere Standorte.  

Obwohl das Festlegen der **Smartcard für das interaktive** Anmeldungs Kennzeichen das Kennwort des Kontos zurücksetzt, verhindert es, dass ein Benutzer mit rechten das Konto Kennwort zurücksetzt, indem das Konto auf einen bekannten Wert festgelegt wird und der Name des Kontos und das neue Konto verwendet werden. Kennwort für den Zugriff auf Ressourcen im Netzwerk. Aus diesem Grund sollten Sie die folgenden zusätzlichen Steuerelemente für das Konto implementieren.  

##### <a name="configuring-gpos-to-restrict-domains-administrator-accounts-on-domain-joined-systems"></a>Konfigurieren von GPOs zum Einschränken von Domänen Administrator Konten auf in die Domäne eingebundenen Systemen

Obwohl das deaktivierte Administrator Konto in einer Domäne das Konto effektiv unbrauchbar macht, sollten Sie zusätzliche Einschränkungen für das Konto implementieren, falls das Konto versehentlich oder böswillig aktiviert ist. Obwohl diese Steuerelemente letztendlich durch das Administrator Konto umgekehrt werden können, besteht das Ziel darin, Steuerelemente zu erstellen, die den Fortschritt eines Angreifers verlangsamen, und die Schäden einzuschränken, die das Konto verursachen kann.  

Fügen Sie in einer oder mehreren Gruppenrichtlinien Objekten, die Sie erstellen und mit Arbeitsstationen und Mitglied Server Organisationseinheiten verknüpft sind, in jeder Domäne das Administrator Konto jeder Domäne den folgenden Benutzerrechten in **Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien \ Zuweisungen von Benutzerrechten**:  

- Zugriff vom Netzwerk auf diesen Computer verweigern  
- Anmelden als Batchauftrag verweigern  
- Anmelden als Dienst verweigern  
- Anmelden über Remotedesktopdienste verweigern  

> [!NOTE]  
> Wenn Sie dieser Einstellung lokale Administrator Konten hinzufügen, müssen Sie angeben, ob Sie lokale Administrator Konten oder Domänen Administrator Konten konfigurieren möchten. Wenn Sie z. b. das lokale Administrator Konto der NWTraders-Domäne zu diesen Ablehnungs rechten hinzufügen möchten, müssen Sie das Konto entweder als **NWTRADERS\Administrator**eingeben oder zum lokalen Administrator Konto für die Domäne nwtraders navigieren. Wenn Sie in der Gruppenrichtlinienobjekt-Editor in diese Benutzerrechte Einstellungen **Administrator** eingeben, beschränken Sie das lokale Administrator Konto auf jedem Computer, auf den das Gruppenrichtlinien Objekt angewendet wird.  
>
> Es wird empfohlen, lokale Administrator Konten auf Mitglieds Servern und Arbeitsstationen auf die gleiche Weise wie Domänen basierte Administrator Konten zu beschränken. Daher sollten Sie in der Regel das Administrator Konto für jede Domäne in der Gesamtstruktur und das Administrator Konto für die lokalen Computer zu diesen Benutzerrechten Einstellungen hinzufügen. 

##### <a name="configuring-gpos-to-restrict-administrator-accounts-on-domain-controllers"></a>Konfigurieren von GPOs zum Einschränken von Administrator Konten auf Domänen Controllern

In jeder Domäne in der Gesamtstruktur sollte die Standard Domänen Controller-Richtlinie oder eine Richtlinie, die mit der Domänen Controller-Organisationseinheit verknüpft ist, geändert werden, um das Administrator Konto jeder Domäne den folgenden Benutzerrechten unter **Computerkonfiguration\Richtlinien\Windows-Einstellungen \Sicherheitseinstellungen\lokale Richtlinien\Zuweisen von Benutzerrechten**:  

- Zugriff vom Netzwerk auf diesen Computer verweigern  
- Anmelden als Batchauftrag verweigern  
- Anmelden als Dienst verweigern  
- Anmelden über Remotedesktopdienste verweigern  

> [!NOTE]  
> Mit diesen Einstellungen wird sichergestellt, dass das lokale Administrator Konto nicht zum Herstellen einer Verbindung mit einem Domänen Controller verwendet werden kann, obwohl sich das Konto, wenn es aktiviert ist, lokal bei Domänen Controllern anmelden kann. Da dieses Konto nur für Notfall Wiederherstellungs Szenarien aktiviert und verwendet werden soll, wird davon abgerechnet, dass der physische Zugriff auf mindestens einen Domänen Controller verfügbar ist oder dass andere Konten mit Berechtigungen für den Remote Zugriff auf Domänen Controller daran.  

##### <a name="configure-auditing-of-built-in-administrator-accounts"></a>Konfigurieren der Überwachung integrierter Administrator Konten

Wenn Sie das Administrator Konto jeder Domäne gesichert und deaktiviert haben, sollten Sie die Überwachung so konfigurieren, dass Änderungen am Konto überwacht werden. Wenn das Konto aktiviert ist, sein Kennwort zurückgesetzt wird oder andere Änderungen am Konto vorgenommen werden, sollten Warnungen an die Benutzer oder Teams gesendet werden, die für die Verwaltung von AD DS verantwortlich sind, zusätzlich zu den Teams für die Reaktion auf Vorfälle in Ihrer Organisation.  

### <a name="securing-administrators-domain-admins-and-enterprise-admins-groups"></a>Sichern von Administratoren, Domänen-Admins und Organisations-Admins-Gruppen

#### <a name="securing-enterprise-admin-groups"></a>Sichern von Unternehmens Administrator Gruppen

Die Gruppe "Organisations-Admins", die in der Stamm Domäne der Gesamtstruktur enthalten ist, sollte täglich keine Benutzer enthalten, mit Ausnahme des lokalen Administrator Kontos der Domäne, vorausgesetzt, Sie ist wie zuvor beschrieben geschützt und in [anhang D: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

Wenn EA-Zugriff erforderlich ist, sollten die Benutzer, deren Konten EA-Rechte und-Berechtigungen benötigen, vorübergehend in der Gruppe Organisations-Admins abgelegt werden. Obwohl Benutzer die Konten mit hohen Berechtigungen verwenden, sollten ihre Aktivitäten überwacht und vorzugsweise mit einem Benutzer durchgeführt werden, der die Änderungen durchführt, und ein anderer Benutzer beobachtet die Änderungen, um die Wahrscheinlichkeit eines unbeabsichtigten Missbrauchs oder einer Fehlkonfiguration zu minimieren. . Wenn die Aktivitäten abgeschlossen sind, sollten die Konten aus der EA-Gruppe entfernt werden. Dies kann mithilfe von manuellen Prozeduren und dokumentierten Prozessen, einer Drittanbieter-Software mit privilegierter Identitäts-/Zugriffsverwaltung (PIM/PAM) oder einer Kombination aus beidem erreicht werden. Richtlinien zum Erstellen von Konten, die zum Steuern der Mitgliedschaft privilegierter Gruppen in Active Directory verwendet werden können, werden in [attraktiven Konten für den Diebstahl von](../../../ad-ds/plan/security-best-practices/Attractive-Accounts-for-Credential-Theft.md) Anmelde Informationen bereitgestellt, und ausführliche Anweisungen finden Sie in [Anhang I: Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory @ no__t-0.  

Organisations-Admins sind standardmäßig Mitglieder der integrierten Gruppe "Administratoren" in jeder Domäne in der Gesamtstruktur. Das Entfernen der Gruppe "Organisations-Admins" aus den Administratoren Gruppen in den einzelnen Domänen ist eine ungeeignete Änderung. im Falle eines Notfall Wiederherstellungs Szenarios für die Gesamtstruktur sind EA-Rechte wahrscheinlich erforderlich. Wenn die Gruppe "Organisations-Admins" aus Administratoren Gruppen in einer Gesamtstruktur entfernt wurde, sollte Sie der Gruppe "Administratoren" in jeder Domäne hinzugefügt werden, und die folgenden zusätzlichen Steuerelemente müssen implementiert werden:  

- Wie bereits erwähnt, sollte die Gruppe "Organisations-Admins" keine Benutzer täglich enthalten, mit der möglichen Ausnahme des Administrator Kontos der Gesamtstruktur-Stamm Domäne, das wie in [anhang D beschrieben geschützt werden soll: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  
- In GPOs, die mit Organisationseinheiten verknüpft sind, die Mitglieds Server und Arbeitsstationen in jeder Domäne enthalten, sollte die EA-Gruppe den folgenden Benutzerrechten hinzugefügt werden:  
   - Zugriff vom Netzwerk auf diesen Computer verweigern  
   - Anmelden als Batchauftrag verweigern  
   - Anmelden als Dienst verweigern  
   - Lokal anmelden verweigern  
   - Verweigern Sie die Anmeldung über Remotedesktopdienste.  

Dadurch wird verhindert, dass Mitglieder der EA-Gruppe sich bei Mitglieds Servern und Arbeitsstationen anmelden. Wenn jumpserver zum Verwalten von Domänen Controllern und Active Directory verwendet werden, stellen Sie sicher, dass sich jumpserver in einer OE befinden, in der die restriktiven GPOs nicht verknüpft sind.  

- Die Überwachung sollte so konfiguriert werden, dass Warnungen gesendet werden, wenn Änderungen an den Eigenschaften oder der EA-Gruppe vorgenommen werden. Diese Warnungen sollten zumindest an Benutzer oder Teams gesendet werden, die für die Active Directory Administration und Reaktion auf Vorfälle verantwortlich sind. Außerdem sollten Sie Prozesse und Prozeduren zum vorübergehenden Auffüllen der EA-Gruppe definieren, einschließlich Benachrichtigungs Verfahren, wenn die berechtigte Auffüllung der Gruppe durchgeführt wird.  
  
#### <a name="securing-domain-admins-groups"></a>Sichern von Domänen Administratoren Gruppen

Wie bei der Gruppe "Organisations-Admins" sollten Mitglieder der Gruppe "Domänen-Admins" nur in Szenarios für die Erstellung oder Notfall Wiederherstellung benötigt werden. Es dürfen keine alltäglichen Benutzerkonten in der Gruppe "da" vorhanden sein, mit Ausnahme des lokalen Administrator Kontos für die Domäne, sofern Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  
  
Wenn der Zugriff auf das Konto erforderlich ist, sollten die Konten, die diese Zugriffsebene benötigen, vorübergehend in der Gruppe "da" für die betreffende Domäne platziert werden. Obwohl die Benutzer die Konten mit hohen Berechtigungen verwenden, sollten Aktivitäten überwacht und vorzugsweise mit einem Benutzer durchgeführt werden, der die Änderungen durchführt, und ein anderer Benutzer, der die Änderungen beobachtet, um die Wahrscheinlichkeit von unbeabsichtigtem Missbrauch oder falscher Konfiguration zu minimieren. Nachdem die Aktivitäten abgeschlossen wurden, sollten die Konten aus der Gruppe Domänen-Admins entfernt werden. Dies kann mithilfe von manuellen Prozeduren und dokumentierten Prozessen, über die bevorzugte Identitäts-/zugriffsverwaltungssoftware (PIM/PAM) von Drittanbietern oder eine Kombination aus beidem erreicht werden. Richtlinien zum Erstellen von Konten, die zum Steuern der Mitgliedschaft privilegierter Gruppen in Active Directory verwendet werden können, finden Sie in [anhang I: Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory @ no__t-0.  
  
Domänen-Admins sind standardmäßig Mitglieder der lokalen Administratoren Gruppen auf allen Mitglieds Servern und Arbeitsstationen in ihren jeweiligen Domänen. Diese Standard Schachtelung sollte nicht geändert werden, da Sie sich auf Unterstützungs-und Notfall Wiederherstellungsoptionen auswirkt. Wenn Domänen-Admins-Gruppen aus den lokalen Administratoren Gruppen auf den Mitglieds Servern entfernt wurden, sollten Sie der Gruppe "Administratoren" auf jedem Mitglieds Server und der Arbeitsstation in der Domäne über eingeschränkte Gruppeneinstellungen in verknüpften Gruppenrichtlinien Objekten hinzugefügt werden. Die folgenden allgemeinen Steuerelemente, die ausführlich in [anhang F beschrieben werden: Das Sichern von Domänen-Admins-Gruppen in Active Directory @ no__t-0 sollte ebenfalls implementiert werden.  

Für die Gruppe "Domänen-Admins" in jeder Domäne in der Gesamtstruktur:  

1. Entfernen Sie alle Mitglieder aus der Gruppe "da" mit der möglichen Ausnahme des integrierten Administrator Kontos für die Domäne, vorausgesetzt, dass Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  
2. In GPOs, die mit Organisationseinheiten verknüpft sind, die Mitglieds Server und Arbeitsstationen in jeder Domäne enthalten, sollte die Gruppe "da" den folgenden Benutzerrechten hinzugefügt werden:  
   - Zugriff vom Netzwerk auf diesen Computer verweigern  
   - Anmelden als Batchauftrag verweigern  
   - Anmelden als Dienst verweigern  
   - Lokal anmelden verweigern  
   - Anmelden über Remotedesktopdienste verweigern  
  
   Dadurch wird verhindert, dass sich Mitglieder der Gruppe "da" bei Mitglieds Servern und Arbeitsstationen anmelden. Wenn jumpserver zum Verwalten von Domänen Controllern und Active Directory verwendet werden, stellen Sie sicher, dass sich jumpserver in einer OE befinden, in der die restriktiven GPOs nicht verknüpft sind.  

3. Die Überwachung sollte so konfiguriert werden, dass Warnungen gesendet werden, wenn Änderungen an den Eigenschaften oder der Mitgliedschaft der Gruppe "da" vorgenommen werden. Diese Warnungen sollten zumindest an Benutzer oder Teams gesendet werden, die für die AD DS Administration und Reaktion auf Vorfälle verantwortlich sind. Außerdem sollten Sie Prozesse und Prozeduren zum vorübergehenden Auffüllen der da-Gruppe definieren, einschließlich Benachrichtigungs Prozeduren, wenn die berechtigte Auffüllung der Gruppe durchgeführt wird.  

#### <a name="securing-administrators-groups-in-active-directory"></a>Sichern von Administratoren Gruppen in Active Directory

Wie bei den EA-und da-Gruppen sollte die Mitgliedschaft in der Gruppe Administratoren (BA) nur in Build-oder Notfall Wiederherstellungs Szenarios erforderlich sein. Es dürfen keine alltäglichen Benutzerkonten in der Gruppe "Administratoren" vorhanden sein, mit Ausnahme des lokalen Administrator Kontos für die Domäne, sofern Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  

Wenn Administrator Zugriff erforderlich ist, sollten die Konten, die diese Zugriffsebene benötigen, vorübergehend in der Gruppe "Administratoren" für die betreffende Domäne platziert werden. Obwohl die Benutzer die Konten mit hohen Berechtigungen verwenden, sollten Aktivitäten überwacht und vorzugsweise mit einem Benutzer durchgeführt werden, der die Änderungen durchführt, und ein anderer Benutzer, der die Änderungen beobachtet, um die Wahrscheinlichkeit von unbeabsichtigtem Missbrauch oder falscher Konfiguration zu minimieren. Nachdem die Aktivitäten abgeschlossen wurden, sollten die Konten sofort aus der Gruppe "Administratoren" entfernt werden. Dies kann mithilfe von manuellen Prozeduren und dokumentierten Prozessen, über die bevorzugte Identitäts-/zugriffsverwaltungssoftware (PIM/PAM) von Drittanbietern oder eine Kombination aus beidem erreicht werden.  

Administratoren sind standardmäßig Besitzer der meisten AD DS Objekte in ihren jeweiligen Domänen. Die Mitgliedschaft in dieser Gruppe ist möglicherweise in Build-und Notfall Wiederherstellungs Szenarien erforderlich, in denen der Besitz oder die Fähigkeit, Objekte zu übernehmen, erforderlich ist. Außerdem erben das und EAS aufgrund der Standardmitgliedschaft in der Gruppe "Administratoren" eine Reihe ihrer Rechte und Berechtigungen. Die Standard Gruppen Schachtelung für privilegierte Gruppen in Active Directory sollte nicht geändert werden, und die Administratoren Gruppe jeder Domäne sollte wie in [anhang G beschrieben geschützt werden: Sichern von Administratoren Gruppen in Active Directory @ no__t-0 und in den folgenden allgemeinen Anweisungen.  

1. Entfernen Sie alle Mitglieder aus der Gruppe Administratoren, mit der Ausnahme, dass das lokale Administrator Konto für die Domäne verfügbar ist, vorausgesetzt, dass Sie wie in [anhang D beschrieben gesichert wurde: Sichern integrierter Administrator Konten in Active Directory @ no__t-0.  
2. Mitglieder der Gruppe "Administratoren" der Domäne sollten sich nie bei Mitglieds Servern oder Arbeitsstationen anmelden müssen. In mindestens einem Gruppenrichtlinien Objekt, das mit der Arbeitsstation und dem Mitglied Server Organisationseinheiten in jeder Domäne verknüpft ist, sollte die Gruppe Administratoren den folgenden Benutzerrechten hinzugefügt werden:  
   - Zugriff vom Netzwerk auf diesen Computer verweigern  
   - Anmelden als Batch Auftrag verweigern  
   - Anmelden als Dienst verweigern  
   - Dadurch wird verhindert, dass Mitglieder der Gruppe "Administratoren" zum Anmelden oder zum Herstellen einer Verbindung mit Mitglieds Servern oder Arbeitsstationen verwendet werden (es sei denn, es werden mehrere Kontrollen zuerst verletzt), wo Ihre Anmelde Informationen zwischengespeichert und somit kompromittiert werden könnten. Ein privilegiertes Konto sollte nie zum Anmelden bei einem System mit weniger Berechtigungen verwendet werden, und durch Erzwingen dieser Steuerelemente wird der Schutz gegen eine Reihe von Angriffen ermöglicht.  

3. Bei der Organisationseinheit "Domänen Controller" in jeder Domäne in der Gesamtstruktur sollten der Gruppe "Administratoren" die folgenden Benutzerrechte gewährt werden (sofern Sie nicht bereits über diese Rechte verfügen). Dadurch können die Mitglieder der Gruppe "Administratoren" die für eine Gesamtstruktur weites Notfall Wiederherstellungs Szenario:  
   - Auf diesen Computer vom Netzwerk aus zugreifen.  
   - Lokale Anmeldung zulassen  
   - Anmelden über Remotedesktopdienste zulassen  

4. Die Überwachung sollte so konfiguriert werden, dass Warnungen gesendet werden, wenn Änderungen an den Eigenschaften oder der Gruppe "Administratoren" vorgenommen werden. Diese Warnungen sollten zumindest an Mitglieder des Teams gesendet werden, das für die AD DS Verwaltung verantwortlich ist. Außerdem sollten Warnungen an Mitglieder des Sicherheitsteams gesendet werden, und es sollten Prozeduren zum Ändern der Mitgliedschaft der Gruppe "Administratoren" definiert werden. Insbesondere sollten diese Prozesse eine Prozedur enthalten, mit der das Sicherheitsteam benachrichtigt wird, wenn die Gruppe "Administratoren" geändert wird, sodass Sie beim Senden von Warnungen erwartet werden und kein Alarm ausgelöst wird. Außerdem müssen Prozesse, die das Sicherheitsteam Benachrichtigen, wenn die Verwendung der Gruppe "Administratoren" abgeschlossen ist und die verwendeten Konten aus der Gruppe entfernt wurden, implementiert werden.  

> [!NOTE]  
> Wenn Sie Einschränkungen für die Administratoren Gruppe in GPOs implementieren, wendet Windows die Einstellungen zusätzlich zur Administrator Gruppe der Domäne auf Mitglieder der lokalen Administratoren Gruppe eines Computers an. Daher sollten Sie bei der Implementierung von Einschränkungen für die Administratoren Gruppe Vorsicht walten lassen. Obwohl das verbieten von Netzwerk-, Batch-und Dienst Anmeldungen für Mitglieder der Gruppe "Administratoren" empfohlen wird, wenn es möglich ist, lokale Anmeldungen oder Anmeldungen nicht über Remotedesktopdienste einzuschränken. Durch das Blockieren dieser Anmelde Typen kann die legitime Verwaltung eines Computers durch Mitglieder der lokalen Administrator Gruppe blockiert werden. Der folgende Screenshot zeigt die Konfigurationseinstellungen, die den Missbrauch von integrierten lokalen Konten und Domänen Administrator Konten blockieren, sowie die Verwendung integrierter lokaler oder Domänen Administratoren Gruppen. Beachten Sie, dass das Benutzerrecht zum **Verweigern von Anmeldungen über Remotedesktopdienste** die Gruppe "Administratoren" nicht einschließt, da diese Anmeldungen auch für Konten blockiert werden, die Mitglieder der Gruppe "Administratoren" des lokalen Computers sind, wenn Sie in diese Einstellung eingeschlossen werden. Wenn Dienste auf Computern für die Ausführung im Zusammenhang mit einer der in diesem Abschnitt beschriebenen privilegierten Gruppen konfiguriert sind, kann das Implementieren dieser Einstellungen zu Fehlern bei Diensten und Anwendungen führen. Daher sollten Sie wie alle Empfehlungen in diesem Abschnitt die Einstellungen für die Anwendbarkeit in Ihrer Umgebung gründlich testen.  
>
> ![Verwaltungsmodelle mit geringstmöglichen Privilegien](media/Implementing-Least-Privilege-Administrative-Models/SAD_3.gif)  

### <a name="role-based-access-controls-rbac-for-active-directory"></a>Rollenbasierte Zugriffs Steuerung (Role-Based Access Control, RBAC) für Active Directory

Im Allgemeinen handelt es sich bei der rollenbasierten Zugriffs Steuerung (Role-Based Access Control, RBAC) um einen Mechanismus zum Gruppieren von Benutzern und zum Bereitstellen des Zugriffs auf Ressourcen basierend auf Im Fall von Active Directory ist die Implementierung von RBAC für AD DS das Erstellen von Rollen, an die Rechte und Berechtigungen delegiert werden, damit Mitglieder der Rolle alltägliche administrative Aufgaben ausführen können, ohne dass Ihnen übermäßig viele Berechtigungen gewährt werden. RBAC für Active Directory kann mithilfe von systemeigenen Tools und Schnittstellen entworfen und implementiert werden, indem Software genutzt wird, die Sie bereits besitzen, indem Sie Produkte von Drittanbietern oder eine beliebige Kombination aus diesen Ansätzen erwerben. Dieser Abschnitt enthält keine Schritt-für-Schritt-Anweisungen zur Implementierung der rollenbasierten Zugriffs Steuerung (RBAC) für Active Directory, sondern erläutert Faktoren, die Sie bei der Auswahl eines Ansatzes zur Implementierung von RBAC in ihren AD DS-Installationen berücksichtigen sollten.  

#### <a name="native-approaches-to-rbac-for-active-directory"></a>Systemeigene Ansätze für die RBAC für Active Directory

In der einfachsten RBAC-Implementierung können Sie Rollen als AD DS Gruppen implementieren und die Rechte und Berechtigungen für die Gruppen delegieren, die es Ihnen ermöglichen, die tägliche Verwaltung innerhalb des festgelegten Bereichs der Rolle auszuführen.  

In einigen Fällen können vorhandene Sicherheitsgruppen in Active Directory verwendet werden, um für eine Auftrags Funktion geeignete Rechte und Berechtigungen zu erteilen. Wenn bestimmte Mitarbeiter in Ihrer IT-Organisation z. b. für die Verwaltung und Verwaltung von DNS-Zonen und-Einträgen zuständig sind, kann die Delegierung dieser Zuständigkeiten so einfach sein wie das Erstellen eines Kontos für jeden DNS-Administrator und das Hinzufügen zum DNS. Gruppe "Administratoren" in Active Directory. Die Gruppe "DNS-Administratoren" verfügt im Gegensatz zu stärker privilegierten Gruppen über einige leistungsstarke Rechte in Active Directory, obwohl Mitgliedern dieser Gruppe Berechtigungen zugewiesen wurden, die Ihnen das Verwalten von DNS erlauben und weiterhin kompromittiert werden können, kann dies zu einer Erhöhung der Berechtigungen.

In anderen Fällen müssen Sie möglicherweise Sicherheitsgruppen erstellen und Rechte und Berechtigungen zum Active Directory von Objekten, Dateisystemobjekten und Registrierungs Objekten delegieren, damit Mitglieder der Gruppen bestimmte administrative Aufgaben ausführen können. Wenn Ihre helpdeskbediener z. b. für das Zurücksetzen von vergessenen Kenn Wörtern, die Unterstützung der Benutzer mit Konnektivitätsproblemen und die Problembehandlung von Anwendungseinstellungen zuständig sind, müssen Sie möglicherweise Delegierungs Einstellungen für Benutzer Objekte Active Directory in mit Berechtigungen, die helpdeskbenutzern das Herstellen einer Remote Verbindung mit den Computern der Benutzer ermöglichen, um die Konfigurationseinstellungen der Benutzer anzuzeigen oder zu ändern. Für jede von Ihnen definierte Rolle sollten Sie Folgendes bestimmen:  

1. Welche Aufgaben Mitglieder der Rolle täglich durchführen und welche Tasks seltener ausgeführt werden.  
2. Auf welchen Systemen und in welchen Anwendungs Mitgliedern einer Rolle Rechte und Berechtigungen gewährt werden sollen.  
3. Welchen Benutzern muss die Mitgliedschaft in einer Rolle gewährt werden.  
4. Wie die Verwaltung von Rollen Mitgliedschaften ausgeführt wird.  

In vielen Umgebungen kann es schwierig sein, rollenbasierte Zugriffs Steuerungen für die Verwaltung einer Active Directory Umgebung zu implementieren und zu warten. Wenn Sie klar definierte Rollen und Zuständigkeiten für die Verwaltung Ihrer IT-Infrastruktur festgelegt haben, können Sie zusätzliche Tools nutzen, um Sie bei der Erstellung einer verwaltbaren nbac-Bereitstellung zu unterstützen. Wenn z. b. Forefront Identity Manager (FIM) in Ihrer Umgebung verwendet wird, können Sie FIM verwenden, um die Erstellung und die Auffüllung von Verwaltungs Rollen zu automatisieren. Dies kann die laufende Verwaltung vereinfachen. Wenn Sie System Center Configuration Manager (SCCM) und System Center Operations Manager (SCOM) verwenden, können Sie anwendungsspezifische Rollen verwenden, um Verwaltungs-und Überwachungsfunktionen zu delegieren und außerdem eine konsistente Konfiguration und Überwachung über Systeme hinweg zu erzwingen. die Domäne. Wenn Sie eine Public Key-Infrastruktur (PKI) implementiert haben, können Sie Smartcards für die IT-Mitarbeiter, die für die Verwaltung der Umgebung verantwortlich sind, ausgeben und benötigen. Mithilfe der FIM-Anmelde Informationsverwaltung (FIM cm) können Sie die Verwaltung von Rollen und Anmelde Informationen für ihr administratives Personal auch kombinieren.  

In anderen Fällen kann es für eine Organisation vorzuziehen sein, eine RBAC-Software von Drittanbietern bereitzustellen, die "Out-of-Box"-Funktionen bereitstellt. Kommerzielle, nicht-Windows-und nicht-Windows-Verzeichnisse und-Betriebssysteme für die rollenbasierte Zugriffs Steuerung für Active Directory, Windows und nicht-Windows-Verzeichnisse werden von einer Reihe von Anbietern angeboten. Bei der Wahl zwischen nativen Lösungen und Drittanbieter Produkten sollten Sie die folgenden Faktoren berücksichtigen:  

1. Etat Durch die Investition in die Entwicklung von RBAC mithilfe von Software und Tools, die Sie möglicherweise bereits besitzen, können Sie die für die Bereitstellung einer Lösung beteiligten Softwarekosten reduzieren. Wenn Sie jedoch nicht über Mitarbeiter verfügen, die mit der Erstellung und Bereitstellung nativer RBAC-Lösungen vertraut sind, müssen Sie möglicherweise Beratungsressourcen einbinden, um Ihre Lösung zu entwickeln. Sie sollten die erwarteten Kosten für eine benutzerdefinierte Lösung mit den Kosten für die Bereitstellung einer "Standardlösung" abwägen, insbesondere wenn Ihr Budget begrenzt ist.  
2. Komposition der IT-Umgebung: Wenn Ihre Umgebung hauptsächlich aus Windows-Systemen besteht oder wenn Sie bereits Active Directory für die Verwaltung von nicht-Windows-Systemen und-Konten nutzen, können benutzerdefinierte native Lösungen die optimale Lösung für Ihre Anforderungen darstellen. Wenn Ihre Infrastruktur viele Systeme enthält, auf denen nicht Windows ausgeführt wird und die nicht von Active Directory verwaltet werden, müssen Sie möglicherweise die Optionen für die Verwaltung von nicht-Windows-Systemen getrennt von der Active Directory Umgebung in Erwägung gezogen.  
3. Berechtigungs Modell in der Lösung: Wenn ein Produkt in Active Directory die Platzierung seiner Dienst Konten in stark privilegierte Gruppen benötigt und keine Optionen anbietet, für die keine übermäßige Berechtigung für die RBAC-Software erteilt werden muss, haben Sie Ihre Active Directory Angriffe nicht wirklich reduziert. Oberfläche Sie haben nur die Zusammensetzung der am stärksten privilegierten Gruppen im Verzeichnis geändert. Wenn ein Anwendungshersteller keine Steuerelemente für Dienst Konten bereitstellen kann, die die Wahrscheinlichkeit minimieren, dass die Konten kompromittiert und böswillig verwendet werden, können Sie andere Optionen in Erwägung ziehen.  

### <a name="privileged-identity-management"></a>Privilegierte Identitätsverwaltung

Die privilegierte Identitätsverwaltung (privilegierte Identitätsverwaltung), manchmal auch als "privilegierte Kontoverwaltung" ("privilegierte Kontoverwaltung") oder "Verwaltung privilegierter Anmelde Informationen (PCM)" bezeichnet, ist das Entwerfen, erstellen und Implementieren von Ansätzen für die Verwaltung privilegierter Konten in Gas. Im Allgemeinen stellt PIM Mechanismen bereit, mit denen Konten temporäre Rechte und Berechtigungen erteilt werden, die zum Ausführen von Build-oder Break-fixfunktionen erforderlich sind, anstatt die Berechtigungen dauerhaft an Konten zu übernehmen. Ob PIM-Funktionen manuell erstellt werden oder über die Bereitstellung von Drittanbieter Software implementiert werden, kann eine oder mehrere der folgenden Features verfügbar sein:  
  
- Anmelde Informationen "Tresore", bei denen Kenn Wörter für privilegierte Konten "ausgecheckt" und ein anfängliches Kennwort zugewiesen werden, dann "eingecheckt", wenn Aktivitäten abgeschlossen sind, zu dem die Kenn Wörter für die Konten wieder zurückgesetzt werden.  
- Zeitgebundene Einschränkungen bei der Verwendung privilegierter Anmelde Informationen  
- Anmelde Informationen für einmalige Verwendung  
- Vom Workflow generierte Gewährung von Berechtigungen für die Überwachung und Berichterstellung von Aktivitäten, die ausgeführt werden, und automatisches Entfernen von Berechtigungen, wenn Aktivitäten abgeschlossen sind oder die zugewiesene Zeit abgelaufen ist  
- Ersetzung von hart codierten Anmelde Informationen, wie z. b. Benutzernamen und Kenn Wörter in Skripts mit APIs (Application Programming Interfaces), die das Abrufen von Anmelde Informationen aus Tresoren nach Bedarf zulassen  
- Automatische Verwaltung von Dienst Konto-Anmelde Informationen  

### <a name="creating-unprivileged-accounts-to-manage-privileged-accounts"></a>Erstellen nicht privilegierter Konten zum Verwalten privilegierter Konten

Eine der Herausforderungen bei der Verwaltung privilegierter Konten ist, dass standardmäßig die Konten, die privilegierte und geschützte Konten und Gruppen verwalten können, privilegierte und geschützte Konten sind. Wenn Sie geeignete RBAC-und PIM-Lösungen für Ihre Active Directory-Installation implementieren, können die Lösungen Ansätze enthalten, mit denen Sie die Mitgliedschaft der am stärksten privilegierten Gruppen im Verzeichnis effektiv auffüllen können, wobei nur die Gruppen aufgefüllt werden. temporär und bei Bedarf.  

Wenn Sie jedoch Native RBAC und PIM implementieren, sollten Sie die Erstellung von Konten ohne Berechtigungen und die einzige Funktion zum Auffüllen und Auffüllen privilegierter Gruppen in Active Directory bei Bedarf in Erwägung gezogen. [Anhang I: Zum Erstellen von Verwaltungs Konten für geschützte Konten und Gruppen in Active Directory @ no__t-0 finden Sie Schritt-für-Schritt-Anweisungen, die Sie zum Erstellen von Konten zu diesem Zweck verwenden können.  

### <a name="implementing-robust-authentication-controls"></a>Implementieren robuster Authentifizierungs Steuerelemente

*law-Nummer 6: Es gibt wirklich jemanden, der versucht, ihre Kenn Wörter zu erraten.* - [10 unveränderliche Gesetze der Sicherheitsverwaltung](https://technet.microsoft.com/library/cc722488.aspx)  

Pass-the-Hash-und andere Angriffe zum Diebstahl von Anmelde Informationen sind nicht spezifisch für Windows-Betriebssysteme und auch nicht neu. Der erste Pass-the-Hash-Angriff wurde in 1997 erstellt. In der Vergangenheit erforderten diese Angriffe angepasste Tools, waren in Ihrem Erfolg und benötigten Angreifern ein relativ hohes Maß an Fähigkeiten. Die Einführung von frei verfügbaren, leicht zu verwendenden Tools, die Anmelde Informationen nativ extrahieren, führte zu einer exponentiellen Zunahme der Anzahl und des Erfolgs von Angriffen zum Diebstahl von Anmelde Informationen in den letzten Jahren. Angriffe durch Diebstahl von Anmelde Informationen sind jedoch keineswegs die einzigen Mechanismen, mit denen Anmelde Informationen gezielt und kompromittiert werden.  

Obwohl Sie Steuerelemente implementieren sollten, um Sie vor Angriffen durch Diebstahl von Anmelde Informationen zu schützen, sollten Sie auch die Konten in Ihrer Umgebung identifizieren, für die am wahrscheinlichsten Angreifer als Ziel festzulegen sind, und robuste Authentifizierungs Steuerungen für diese implementieren. Buchhaltungs. Wenn Ihre privilegierten Konten eine Einzelfaktor Authentifizierung verwenden, wie z. b. Benutzernamen und Kenn Wörter (was Sie wissen, was ein Authentifizierungs Faktor ist), sind diese Konten schwach geschützt. Ein Angreifer muss lediglich über den Benutzernamen und das Kennwort des Kennworts verfügen, das dem Konto zugeordnet ist, und Pass-the-Hash-Angriffe sind nicht erforderlich, da der Angreifer sich als Benutzer bei Systemen authentifizieren kann, die einstufige Anmelde Informationen akzeptieren.  

Obwohl die Implementierung der Multi-Factor Authentication nicht vor Pass-the-Hash-Angriffen geschützt ist, kann die Implementierung der Multi-Factor Authentication in Kombination mit geschützten Systemen verwendet werden. Weitere Informationen zum Implementieren geschützter Systeme finden Sie unter [Implementieren von sicheren administrativen Hosts](../../../ad-ds/plan/security-best-practices/Implementing-Secure-Administrative-Hosts.md)und Authentifizierungs Optionen werden in den folgenden Abschnitten erläutert.  

#### <a name="general-authentication-controls"></a>Allgemeine Authentifizierungs Steuerelemente

Wenn Sie die Multi-Factor Authentication (z. b. Smartcards) nicht bereits implementiert haben, sollten Sie dies tun. Smartcards implementieren die durch die Hardware erzwungene Sicherheit privater Schlüssel in einem öffentlich/privat-Schlüsselpaar, wodurch verhindert wird, dass der private Schlüssel eines Benutzers aufgerufen oder verwendet wird, es sei denn, der Benutzer gibt die richtige PIN, Kennung oder biometrische Kennung für die Smartcard an. Auch wenn die PIN oder Kennung eines Benutzers von einer Tastatureingabe Protokollierung auf einem kompromittierten Computer abgefangen wird, muss die Karte auch physisch vorhanden sein, damit ein Angreifer die PIN oder Kennung wieder verwenden kann.

In Fällen, in denen sich komplexe Kenn Wörter aufgrund von Benutzer Beständigkeit als schwierig erwiesen haben, bieten Smartcards einen Mechanismus, mit dem Benutzer relativ einfache Pins oder Kennungen implementieren können, ohne dass die Anmelde Informationen anfällig für Brute-Force-oder Regenbogen Tabellen Angriffe. Smartcard-Pins werden nicht in Active Directory oder lokalen SAM-Datenbanken gespeichert, obwohl anmeldeinformationshashes weiterhin in LSASS-geschütztem Speicher auf Computern gespeichert werden können, auf denen Smartcards für die Authentifizierung verwendet wurden.  

#### <a name="additional-controls-for-vip-accounts"></a>Zusätzliche Steuerelemente für VIP-Konten

Ein weiterer Vorteil bei der Implementierung von Smartcards oder anderen Zertifikat basierten Authentifizierungsmechanismen besteht darin, dass Sie die Authentifizierungsmechanismus-Sicherheit nutzen können, um sensible Daten zu schützen, die für VIP-Benutzer zugänglich sind. Die Sicherung des Authentifizierungsmechanismus ist in Domänen verfügbar, in denen die Funktionsebene auf Windows Server 2012 oder Windows Server 2008 R2 festgelegt ist. Wenn die Authentifizierung aktiviert ist, wird eine vom Administrator festgelegte globale Gruppenmitgliedschaft zum Kerberos-Token eines Benutzers hinzugefügt, wenn die Anmelde Informationen des Benutzers bei der Anmeldung mithilfe einer Zertifikat basierten Anmelde Methode authentifiziert werden.  

Dies ermöglicht es Ressourcen Administratoren, den Zugriff auf Ressourcen (z. b. Dateien, Ordner und Drucker) zu steuern, je nachdem, ob sich der Benutzer mithilfe einer Zertifikat basierten Anmelde Methode anmeldet, zusätzlich zu dem verwendeten Zertifikattyp. Wenn sich ein Benutzer z. b. mit einer Smartcard anmeldet, kann der Zugriff des Benutzers auf Ressourcen im Netzwerk anders als der Zugriff angegeben werden, wenn der Benutzer keine Smartcard verwendet (d. h., wenn sich der Benutzer anmeldet, indem er einen Benutzernamen und ein Kennwort eingegeben hat). Weitere Informationen zur Authentifizierung des Authentifizierungsmechanismus finden Sie [in der schrittweisen Anleitung zum Sichern von Authentifizierungsmechanismen für AD DS in Windows Server 2008 R2](https://technet.microsoft.com/library/dd378897.aspx).  

#### <a name="configuring-privileged-account-authentication"></a>Konfigurieren der Authentifizierung privilegierter Konten

Aktivieren Sie in Active Directory für alle Administrator Konten die Option **Smartcard für interaktives Anmelde** Attribut anfordern, und überwachen Sie mindestens alle Attribute auf der Registerkarte **Konto** für das Konto (zum Beispiel CN, Name, Verwaltungs Benutzer Objekte "samAccountName", "UserPrincipalName" und "userAccountControl".  

Obwohl das Festlegen der **Smartcard für die interaktive Anmeldung** anfordern das Kennwort des Kontos auf einen Zufallswert von 120 Zeichen zurücksetzt und Smartcards für interaktive Anmeldungen erfordert, kann das Attribut dennoch von Benutzern mit Berechtigungen überschrieben werden. Dadurch können Sie Kenn Wörter für die Konten ändern, und die Konten können dann verwendet werden, um nicht interaktive Anmeldungen mit nur Benutzername und Kennwort einzurichten.  

In anderen Fällen können die Benutzer Prinzipal Namen (UPN)-Attribute für administrative oder VIP-Konten in Abhängigkeit von der Konfiguration von Konten in Active Directory und Zertifikat Einstellungen in Active Directory Zertifikat Diensten (AD CS) oder einer PKI eines Drittanbieters als Ziel Festlegung für eine bestimmte Art von Angriff, wie hier beschrieben.  

##### <a name="upn-hijacking-for-certificate-spoofing"></a>UPN-Hijacking für Zertifikat Spoofing

Obwohl eine gründliche Erörterung von Angriffen gegen Public Key Infrastructure (PKIs) den Rahmen dieses Dokuments sprengen würde, haben Angriffe gegen öffentliche und private PKIs seit 2008 exponentiell verstärkt. Verstöße gegen öffentliche PKIs wurden im großen und ganzen öffentlich gemacht, aber Angriffe auf die interne PKI einer Organisation sind vielleicht noch produktiver. Ein solcher Angriff nutzt Active Directory und Zertifikate, damit ein Angreifer die Anmelde Informationen anderer Konten auf eine Weise SPO, die schwer zu erkennen ist.  

Wenn ein Zertifikat für die Authentifizierung bei einem in die Domäne eingebundenen System angezeigt wird, wird der Inhalt des Antragstellers oder des "Subject Alternative Name (San)"-Attributs im Zertifikat verwendet, um das Zertifikat einem Benutzerobjekt in Active Directory zuzuordnen. Abhängig vom Zertifikattyp und seiner Erstellung enthält das Subject-Attribut in einem Zertifikat in der Regel einen allgemeinen Namen (CN) des Benutzers, wie im folgenden Screenshot gezeigt.  

![Verwaltungsmodelle mit geringstmöglichen Privilegien](media/Implementing-Least-Privilege-Administrative-Models/SAD_4.gif)  

Standardmäßig erstellt Active Directory den CN eines Benutzers, indem er den Vornamen des Kontos + "" und den Nachnamen verkettet. Allerdings sind CN-Komponenten von Benutzer Objekten in Active Directory nicht erforderlich oder garantiert eindeutig. Wenn Sie ein Benutzerkonto an einen anderen Speicherort im Verzeichnis verschieben, ändert sich der Distinguished Name (DN) des Kontos. Dies ist der vollständige Pfad zum Objekt im Verzeichnis, wie im unteren Bereich des vorherigen Screenshots dargestellt.  

Da es nicht garantiert werden kann, dass Zertifikat Antragsteller statisch oder eindeutig sind, wird der Inhalt des alternativen Antragsteller namens häufig verwendet, um das Benutzerobjekt in Active Directory zu suchen. Das San-Attribut für Zertifikate, die von Unternehmens Zertifizierungsstellen (Active Directory integrierter CAS) für Benutzer ausgestellt werden, enthält normalerweise den UPN oder die e-Mail-Adresse des Benutzers. Da UPNs in einer AD DS Gesamtstruktur eindeutig sind, wird das Auffinden eines Benutzer Objekts nach UPN häufig als Teil der Authentifizierung ausgeführt, mit oder ohne dass Zertifikate an dem Authentifizierungsprozess beteiligt sind.  

Die Verwendung von UPNs in San-Attributen in Authentifizierungs Zertifikaten kann von Angreifern zum Abrufen betrügerischer Zertifikate genutzt werden. Wenn ein Angreifer ein Konto kompromittiert hat, das die Möglichkeit hat, UPNs für Benutzer Objekte zu lesen und zu schreiben, wird der Angriff wie folgt implementiert:  

Das UPN-Attribut für ein Benutzerobjekt (z. b. ein VIP-Benutzer) wird vorübergehend in einen anderen Wert geändert. Das Attribut "Sam Account Name" und "CN" können zu diesem Zeitpunkt ebenfalls geändert werden. Dies ist jedoch in der Regel aus den zuvor beschriebenen Gründen nicht erforderlich.  

Wenn das UPN-Attribut für das Zielkonto geändert wurde, wird ein veraltetes Benutzerkonto oder das UPN-Attribut eines neu erstellten Benutzerkontos in den Wert geändert, der ursprünglich dem Zielkonto zugewiesen wurde. Veraltete, aktivierte Benutzerkonten sind Konten, die über einen längeren Zeitraum nicht angemeldet wurden, jedoch nicht deaktiviert wurden. Sie sind von Angreifern betroffen, die aus den folgenden Gründen "in Plain Sight ausblenden" möchten:  

1. Da das Konto zwar aktiviert, aber noch nicht verwendet wurde, ist es unwahrscheinlich, dass die Verwendung des Kontos Warnungen darauf auslöst, wie ein deaktiviertes Benutzerkonto aktiviert werden kann.  
2. Für die Verwendung eines vorhandenen Kontos ist das Erstellen eines neuen Benutzerkontos, das möglicherweise von den Administratoren bemerkt wird, nicht erforderlich.  
3. Veraltete Benutzerkonten, die weiterhin aktiviert sind, sind in der Regel Mitglieder der verschiedenen Sicherheitsgruppen und erhalten Zugriff auf Ressourcen im Netzwerk, wodurch der Zugriff vereinfacht und eine vorhandene Benutzer Population kombiniert werden kann.  

Das Benutzerkonto, auf dem der Ziel-UPN nun konfiguriert wurde, wird verwendet, um ein oder mehrere Zertifikate von Active Directory Zertifikat Diensten anzufordern.  

Wenn Zertifikate für das Konto des Angreifers abgerufen wurden, werden die UPNs für das "neue" Konto und das Zielkonto auf ihre ursprünglichen Werte zurückgegeben.  

Der Angreifer verfügt jetzt über ein oder mehrere Zertifikate, die für die Authentifizierung bei Ressourcen und Anwendungen bereitgestellt werden können, als ob der Benutzer der VIP-Benutzer ist, dessen Konto vorübergehend geändert wurde. Obwohl eine vollständige Erörterung aller Möglichkeiten, wie Zertifikate und PKI von Angreifern betroffen sein können, nicht in diesem Dokument behandelt wird, wird dieser Angriffs Mechanismus bereitgestellt, um zu veranschaulichen, warum Sie privilegierte und VIP-Konten in AD DS auf Änderungen überwachen sollten. , insbesondere für Änderungen an einem der Attribute auf der Registerkarte **Konto** für das Konto (z. b. cn, Name, sAMAccountName, userPrincipalName und userAccountControl). Zusätzlich zum Überwachen der Konten sollten Sie einschränken, wer die Konten so klein wie möglich in eine Gruppe von Administratoren ändern kann. Ebenso sollten die Konten von Administratoren geschützt und auf nicht autorisierte Änderungen überwacht werden.  
