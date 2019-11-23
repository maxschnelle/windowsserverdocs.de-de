---
ms.assetid: eafdddc3-40d7-4a75-8f4f-a45294aabfc8
title: Implementieren von sicheren Verwaltungshosts
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 56986f2ea9f49bdfc1194ae5342798793524e86c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408610"
---
# <a name="implementing-secure-administrative-hosts"></a>Implementieren von sicheren Verwaltungshosts

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichere administrative Hosts sind Arbeitsstationen oder Server, die speziell für die Erstellung sicherer Plattformen konfiguriert wurden, von denen privilegierte Konten administrative Aufgaben in Active Directory oder auf Domänen Controllern ausführen können. in die Domäne eingebundenen Systemen und Anwendungen, die auf in die Domäne eingebundenen Systemen ausgeführt werden. In diesem Fall bezieht sich "privilegierte Konten" nicht nur auf Konten, die Mitglieder der am stärksten privilegierten Gruppen in Active Directory sind, sondern auf alle Konten, denen Rechte und Berechtigungen zugewiesen wurden, die das Ausführen administrativer Aufgaben ermöglichen.  
  
Diese Konten können helpdeskkonten sein, die für die meisten Benutzer in einer Domäne Kenn Wörter zurücksetzen können, Konten, die zum Verwalten von DNS-Einträgen und-Zonen verwendet werden, oder Konten, die für die Konfigurations Verwaltung verwendet werden. Sichere administrative Hosts sind für Verwaltungsfunktionen reserviert und führen keine Software aus, wie z. b. e-Mail-Anwendungen, Webbrowser oder Produktivitätssoftware, wie z. b. Microsoft Office.  
  
Obwohl es sich bei den Konten und Gruppen mit den meisten Berechtigungen um die stringoffensichtlichsten Konten und Gruppen handeln sollte, entfällt dadurch die Notwendigkeit, Konten und Gruppen zu schützen, denen Berechtigungen oberhalb der Standardbenutzer Konten erteilt wurden.  
  
Ein sicherer Administrator kann eine dedizierte Arbeitsstation sein, die nur für administrative Aufgaben verwendet wird, ein Mitglieds Server, auf dem die Remotedesktop Gateway-Server Rolle ausgeführt wird und mit dem der Benutzer eine Verbindung zur Verwaltung von Zielhosts herstellt, oder ein Server, auf dem ausgeführt wird. die Hyper-V-Rolle und stellt für jeden IT-Benutzer einen eindeutigen virtuellen Computer für die administrativen Aufgaben bereit. In vielen Umgebungen können Kombinationen aus allen drei Ansätzen implementiert werden.  
  
Die Implementierung sicherer administrativer Hosts erfordert Planung und Konfiguration, die mit der Größe des Unternehmens, den administrativen Verfahren, der Risikobereitschaft und dem Budget in Einklang steht. Hier finden Sie Überlegungen und Optionen für die Implementierung sicherer administrativer Hosts, die Sie für die Entwicklung einer für Ihre Organisation geeigneten Verwaltungs Strategie verwenden können.  
  
## <a name="principles-for-creating-secure-administrative-hosts"></a>Grundsätze zum Erstellen sicherer administrativer Hosts  
Zur effektiven Absicherung von Systemen gegen Angriffe sollten einige allgemeine Prinzipien berücksichtigt werden:  
  
1.  Sie sollten niemals ein vertrauenswürdiges System (d. h. einen sicheren Server, z. b. einen Domänen Controller) von einem nicht vertrauenswürdigen Host (d. h. eine Arbeitsstation, die nicht auf denselben Grad gesichert ist wie die von ihm verwalteten Systeme) verwalten.  
  
2.  Beim Ausführen privilegierter Aktivitäten sollten Sie sich nicht auf einen einzelnen Authentifizierungs Faktor verlassen. Das heißt, Benutzernamen-und Kenn Wortkombinationen sollten nicht als akzeptable Authentifizierung angesehen werden, da nur ein einzelner Faktor (etwas, das Sie wissen) repräsentiert wird. Sie sollten in Erwägung gezogen werden, wo Anmelde Informationen in administrativen Szenarien generiert, zwischengespeichert oder gespeichert werden.  
  
3.  Obwohl die meisten Angriffe in der aktuellen Bedrohungslandschaft Schadsoftware und böswillige Hacker verwenden, lassen Sie die physische Sicherheit nicht zu, wenn Sie sichere administrative Hosts entwerfen und implementieren.  
  
### <a name="account-configuration"></a>Konto Konfiguration  
Auch wenn Ihre Organisation derzeit keine Smartcards verwendet, sollten Sie diese für privilegierte Konten und sichere administrative Hosts implementieren. Administrative Hosts sollten so konfiguriert werden, dass eine Smartcard-Anmeldung für alle Konten erforderlich ist, indem Sie die folgende Einstellung in einem Gruppenrichtlinien Objekt ändern, das mit den Organisationseinheiten verknüpft ist, die administrative Hosts enthalten  
  
**Computerkonfiguration\Richtlinien\Windows-Einstellungen\Lokale richtlinien\sicherheitsoptions\interaktive Anmeldung: Smartcard erforderlich**  
  
Diese Einstellung erfordert, dass alle interaktiven Anmeldungen eine Smartcard verwenden, unabhängig von der Konfiguration eines einzelnen Kontos in Active Directory.  
  
Sie sollten auch sichere administrative Hosts so konfigurieren, dass Anmeldungen nur von autorisierten Konten zugelassen werden, die in konfiguriert werden können:  
  
**Computerkonfiguration\Richtlinien\Windows-Einstellungen\Lokale richtlinien\sicherheitseinstellungen\lokale Richtlinien\Zuweisen von Benutzerrechten**  
  
Dadurch werden die Anmelde Rechte (und, sofern zutreffend, Remotedesktopdienste) nur autorisierten Benutzern des sicheren administrativen Hosts gewährt.  
  
### <a name="physical-security"></a>Physische Sicherheit  
Damit administrative Hosts als vertrauenswürdig eingestuft werden, müssen Sie so konfiguriert und geschützt werden, wie die Systeme, die Sie verwalten. Die meisten der Empfehlungen zum Schützen von [Domänen Controllern gegen Angriffe](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) gelten auch für die Hosts, die zur Verwaltung von Domänen Controllern und der AD DS-Datenbank verwendet werden. Eine der Herausforderungen bei der Implementierung sicherer administrativer Systeme in den meisten Umgebungen besteht darin, dass die physische Sicherheit schwieriger zu implementieren ist, da sich diese Computer häufig in Bereichen befinden, die nicht so sicher sind wie Server, die in Rechenzentren gehostet werden, z. b. Desktops von Administratoren.  
  
Die physische Sicherheit beinhaltet die Steuerung des physischen Zugriffs auf administrative Hosts. In einem kleinen Unternehmen bedeutet dies möglicherweise, dass Sie eine dedizierte administrative Arbeitsstation verwalten, die in einer Büro-oder Desk-Schublade gesperrt bleibt, wenn Sie nicht verwendet wird. Wenn Sie die Verwaltung von Active Directory oder Ihren Domänen Controllern ausführen müssen, können Sie sich beim Domänen Controller direkt anmelden.  
  
In mittelständischen Unternehmen sollten Sie die Implementierung sicherer Verwaltungs-"Jump-Server" in einem sicheren Büro in einem Büro in Erwägung gezogen und bei der Verwaltung von Active Directory oder Domänen Controllern verwendet werden. Sie können auch Verwaltungs Arbeitsstationen implementieren, die an sicheren Orten gesperrt sind, wenn Sie nicht verwendet werden, mit oder ohne Sprung Server.  
  
In großen Unternehmen können Sie in einem Rechenzentrum bereitgestellte Sprung Server bereitstellen, die streng kontrollierten Zugriff auf Active Directory bereitstellen. Domänen Controller; und Datei-, Druck-oder Anwendungsserver. Die Implementierung einer Jump Server-Architektur umfasst höchstwahrscheinlich eine Kombination aus sicheren Arbeitsstationen und Servern in großen Umgebungen.  
  
Unabhängig von der Größe Ihrer Organisation und dem Entwurf Ihrer administrativen Hosts sollten Sie physische Computer vor unbefugtem Zugriff oder Diebstahl schützen und die Laufwerke auf administrativen Hosts mithilfe von BitLocker-Laufwerkverschlüsselung verschlüsseln und schützen. . Durch die Implementierung von BitLocker auf administrativen Hosts können Sie sicherstellen, dass die Daten auf dem Laufwerk nicht autorisierten Benutzern zugänglich sind, auch wenn ein Host gestohlen oder seine Datenträger entfernt werden.  
  
### <a name="operating-system-versions-and-configuration"></a>Betriebs System Versionen und-Konfiguration  
Alle administrativen Hosts, unabhängig davon, ob Server oder Arbeitsstationen, sollten das neueste Betriebssystem ausführen, das in Ihrer Organisation verwendet wird, aus den in diesem Dokument beschriebenen Gründen. Durch die Ausführung aktueller Betriebssysteme profitieren Ihre administrativen Mitarbeiter von neuen Sicherheitsfeatures, vollständigen Hersteller Unterstützung und zusätzlichen Funktionen, die im Betriebssystem eingeführt werden. Wenn Sie ein neues Betriebssystem evaluieren, indem Sie es zunächst für administrative Hosts bereitstellen, müssen Sie sich mit den neuen Features, Einstellungen und Verwaltungsmechanismen vertraut machen, die es bietet und die anschließend bei der Planung genutzt werden können. breitere Bereitstellung des Betriebssystems. Die ausgereiftesten Benutzer in Ihrer Organisation sind dann auch die Benutzer, die mit dem neuen Betriebssystem vertraut sind und am besten zur Unterstützung der IT-Abteilung verwendet werden.  
  
### <a name="microsoft-security-configuration-wizard"></a>Sicherheitskonfigurations-Assistent von Microsoft  
Wenn Sie Jump-Server als Teil ihrer Verwaltungs Host Strategie implementieren, sollten Sie den integrierten Sicherheitskonfigurations-Assistenten verwenden, um Dienst-, Registrierungs-, Überwachungs-und Firewalleinstellungen zu konfigurieren, um die Angriffsfläche des Servers zu verringern. Wenn die Konfigurationseinstellungen des Sicherheitskonfigurations-Assistenten gesammelt und konfiguriert wurden, können die Einstellungen in ein Gruppenrichtlinien Objekt konvertiert werden, das zum Erzwingen einer konsistenten Baselineversion auf allen Jump-Servern verwendet wird. Sie können das Gruppenrichtlinien Objekt weiter bearbeiten, um für Jump-Server spezifische Sicherheitseinstellungen zu implementieren. Außerdem können Sie alle Einstellungen mit zusätzlichen Baseline-Einstellungen kombinieren, die vom Microsoft Security Compliance Manager extrahiert werden.  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft Security Compliance Manager  
Bei [Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx) handelt es sich um ein kostenlos verfügbares Tool, mit dem Sicherheits Konfigurationen integriert werden, die von Microsoft basierend auf der Betriebssystemversion und der Rollen Konfiguration empfohlen werden, und die in einem einzigen Tool und einer Benutzeroberfläche zum Erstellen und Konfigurieren von Baseline-Sicherheitseinstellungen für Domänen Controller verwendet werden. Microsoft Security Compliance Manager-Vorlagen können mit den Einstellungen für den Sicherheitskonfigurations-Assistenten kombiniert werden, um umfassende konfigurationsbaselines für Jump-Server zu erstellen, die von GPOs bereitgestellt und erzwungen werden, die in den Organisationseinheiten bereitgestellt werden in Active Directory.  
  
> [!NOTE]  
> Zum Zeitpunkt der Erstellung dieses Artikels enthält Microsoft Security Compliance Manager keine speziellen Einstellungen für Jump-Server oder andere sichere administrative Hosts, aber Security Compliance Manager (SCM) kann weiterhin verwendet werden, um anfängliche Basis Linien für ihre Verwaltung zu erstellen. Wirte. Zum ordnungsgemäßen Sichern der Hosts sollten Sie jedoch zusätzliche Sicherheitseinstellungen anwenden, die für hochgradig gesicherte Arbeitsstationen und Server geeignet sind.  
  
### <a name="applocker"></a>AppLocker  
Administrative Hosts und virtuelle Maschinen sollten mit Skript-, Tool-und anwendungswhitelists über AppLocker oder eine Anwendungs Einschränkungs Software eines Drittanbieters konfiguriert werden. Alle administrativen Anwendungen oder Hilfsprogramme, die keine sicheren Einstellungen einhalten, sollten aktualisiert oder durch Tools ersetzt werden, die sicheren Entwicklungs-und Verwaltungsverfahren entsprechen. Wenn neue oder zusätzliche Tools auf einem administrativen Host benötigt werden, sollten die Anwendungen und Dienstprogramme gründlich getestet werden, und wenn die Tools für die Bereitstellung auf administrativen Hosts geeignet sind, können Sie den Whitelists der Systeme hinzugefügt werden.  
  
### <a name="rdp-restrictions"></a>RDP-Einschränkungen  
Obwohl die spezifische Konfiguration abhängig von der Architektur ihrer administrativen Systeme variiert, sollten Sie Einschränkungen beachten, welche Konten und Computer verwendet werden können, um Remotedesktopprotokoll (RDP)-Verbindungen mit verwalteten Systemen herzustellen. beispielsweise die Verwendung von Remotedesktop Gateway-(RD-Gateway) Jump-Servern, um den Zugriff auf Domänen Controller und andere verwaltete Systeme von autorisierten Benutzern und Systemen aus zu steuern.  
  
Sie sollten interaktive Anmeldungen durch autorisierte Benutzer zulassen und andere Anmelde Typen entfernen oder blockieren, die für den Server Zugriff nicht benötigt werden.  
  
### <a name="patch-and-configuration-management"></a>Patch-und Konfigurations Verwaltung  
Kleinere Unternehmen können sich auf Angebote wie Windows Update oder [Windows Server Update Services](https://technet.microsoft.com/windowsserver/bb332157) (WSUS) verlassen, um die Bereitstellung von Updates für Windows-Systeme zu verwalten. größere Unternehmen implementieren jedoch möglicherweise die Software System Center Configuration Manager zur Verwaltung von Patches und Configuration Management, z. b. Unabhängig von den Mechanismen, die Sie zum Bereitstellen von Aktualisierungen Ihrer allgemeinen Server-und Arbeitsstations Population verwenden, sollten Sie separate bereit Stellungen für hochgradig sichere Systeme wie z. b. Domänen Controller, Zertifizierungsstellen und administrative Hosts in Erwägung gezogen. Wenn Sie diese Systeme von der allgemeinen Verwaltungsinfrastruktur trennen, kann die Gefährdung nicht einfach auf die sichersten Systeme in Ihrer Infrastruktur ausgeweitet werden, wenn Ihre Verwaltungssoftware oder Dienst Konten kompromittiert sind.  
  
Obwohl Sie keine manuellen Update Prozesse für sichere Systeme implementieren sollten, sollten Sie eine separate Infrastruktur zum Aktualisieren sicherer Systeme konfigurieren. Auch in sehr großen Organisationen kann diese Infrastruktur in der Regel über dedizierte WSUS-Server und GPOs für gesicherte Systeme implementiert werden.  
  
### <a name="blocking-internet-access"></a>Blockieren des Internet Zugriffs  
Administrator Hosts dürfen nicht auf das Internet zugreifen dürfen und sollten nicht in der Lage sein, das Intranet einer Organisation zu durchsuchen. Webbrowser und ähnliche Anwendungen sollten auf administrativen Hosts nicht zugelassen werden. Sie können den Internet Zugriff für sichere Hosts über eine Kombination aus Umkreis-Firewall-Einstellungen, wfas-Konfiguration und "Black Hole"-Proxykonfiguration auf sicheren Hosts blockieren. Sie können auch anwendungswhitelists verwenden, um zu verhindern, dass Webbrowser auf administrativen Hosts verwendet werden.  
  
### <a name="virtualization"></a>Virtualisierung  
Wenn möglich, sollten Sie die Implementierung virtueller Maschinen als administrative Hosts in Erwägung gezogen. Mithilfe der Virtualisierung können Sie benutzerspezifische Verwaltungssysteme erstellen, die zentral gespeichert und verwaltet werden und problemlos heruntergefahren werden können, wenn Sie nicht verwendet werden. Dadurch wird sichergestellt, dass die Anmelde Informationen auf den administrativen Systemen nicht aktiviert sind. Außerdem kann es erforderlich sein, dass virtuelle administrative Hosts nach jeder Verwendung auf eine anfängliche Momentaufnahme zurückgesetzt werden, um sicherzustellen, dass die virtuellen Computer intakt bleiben. Weitere Informationen zu den Optionen für die Virtualisierung von administrativen Hosts finden Sie im folgenden Abschnitt.  
  
## <a name="sample-approaches-to-implementing-secure-administrative-hosts"></a>Beispiel Ansätze für die Implementierung sicherer administrativer Hosts  
Unabhängig davon, wie Sie Ihre administrative Host Infrastruktur entwerfen und bereitstellen, sollten Sie die Richtlinien unter "Prinzipien zum Erstellen sicherer administrativer Hosts" weiter oben in diesem Thema berücksichtigen. Jeder der hier beschriebenen Ansätze bietet allgemeine Informationen darüber, wie Sie "administrative" und "Produktivitäts Systeme" trennen können, die von Ihrem IT-Personal verwendet werden. Produktivitäts Systeme sind Computer, die IT-Administratoren verwenden, um e-Mails zu prüfen, das Internet zu durchsuchen und allgemeine Produktivitätssoftware zu verwenden, wie z. b. Microsoft Office. Verwaltungssysteme sind Computer, die für die tägliche Verwaltung einer IT-Umgebung festgeschrieben und dediziert wurden.  
  
Die einfachste Möglichkeit, sichere administrative Hosts zu implementieren, besteht darin, Ihren IT-Mitarbeitern gesicherte Arbeitsstationen bereitzustellen, von denen Sie administrative Aufgaben ausführen können. Bei einer reinen Arbeitsstations Implementierung wird jede administrative Arbeitsstation zum Starten von Verwaltungs Tools und RDP-Verbindungen zum Verwalten von Servern und anderen Infrastrukturen verwendet. Reine Arbeitsstations Implementierungen können in kleineren Organisationen wirksam sein, aber größere komplexere Infrastrukturen können von einem verteilten Entwurf für administrative Hosts profitieren, in denen dedizierte administrative Server und Arbeitsstationen verwendet werden. weiter unten in diesem Thema unter "Implementieren sicherer administrativer Arbeitsstationen und Jump Server" beschrieben.  
  
### <a name="implementing-separate-physical-workstations"></a>Implementieren von separaten physischen Arbeitsstationen  
Eine Möglichkeit, administrative Hosts zu implementieren, besteht darin, jeden Benutzer zwei Arbeitsstationen auszustellen. Eine Arbeitsstation wird mit einem "regulären" Benutzerkonto verwendet, um Aktivitäten wie das Überprüfen von e-Mails und die Verwendung von Produktivitätsanwendungen auszuführen, während die zweite Arbeitsstation ausschließlich für administrative Funktionen reserviert ist.  
  
Für die Arbeitsstation der Produktivität können IT-Mitarbeiter reguläre Benutzerkonten erhalten, anstatt privilegierte Konten zum Anmelden bei ungesicherten Computern zu verwenden. Die Verwaltungs Arbeitsstation sollte mit einer stringmentell kontrollierten Konfiguration konfiguriert werden, und die IT-Mitarbeiter sollten ein anderes Konto für die Anmeldung bei der administrativen Arbeitsstation verwenden.  
  
Wenn Sie Smartcards implementiert haben, müssen administrative Arbeitsstationen so konfiguriert werden, dass Smartcardanmeldungen erforderlich sind, und IT-Mitarbeitern sollten separate Konten für die administrative Verwendung zugewiesen werden. Außerdem müssen Sie für die Verwendung von Smartcards für die interaktive Anmeldung konfiguriert werden. Der administrative Host sollte wie zuvor beschrieben festgelegt werden, und nur bestimmte IT-Benutzer sollten sich lokal bei der administrativen Arbeitsstation anmelden dürfen.  
  
#### <a name="pros"></a>Vorteile  
Durch die Implementierung separater physischer Systeme können Sie sicherstellen, dass jeder Computer ordnungsgemäß für seine Rolle konfiguriert ist und dass IT-Benutzer nicht versehentlich Verwaltungssysteme zum Risiko verfügbar machen können.  
  
#### <a name="cons"></a>Nachteile  
  
-   Durch die Implementierung separater physischer Computer werden die Hardwarekosten erhöht.  
  
-   Bei der Anmeldung an einem physischen Computer mit Anmelde Informationen, die zur Verwaltung von Remote Systemen verwendet werden, werden die Anmelde Informationen im Speicher zwischengespeichert.  
  
-   Wenn administrative Arbeitsstationen nicht sicher gespeichert werden, sind Sie möglicherweise anfällig für die Gefährdung durch Mechanismen wie z. b. die Protokollierung von physischen Hardware Schlüsseln oder andere physische Angriffe.  
  
### <a name="implementing-a-secure-physical-workstation-with-a-virtualized-productivity-workstation"></a>Implementieren einer sicheren physischen Arbeitsstation mit einer virtualisierten Produktivitäts Arbeitsstation  
Bei dieser Vorgehensweise erhalten IT-Benutzer eine gesicherte administrative Arbeitsstation, von der aus Sie tägliche Verwaltungsfunktionen durchführen können, indem Sie Remoteserver-Verwaltungstools (RSAT) oder RDP-Verbindungen zu Servern innerhalb ihres Zuständigkeitsbereichs verwenden. Wenn Benutzer Produktivitäts Aufgaben durchführen müssen, können Sie über RDP eine Verbindung mit einer Remote-Produktivitäts Arbeitsstation herstellen, die als virtueller Computer ausgeführt wird. Für jede Arbeitsstation sollten separate Anmelde Informationen verwendet werden, und es sollten Steuerelemente wie Smartcards implementiert werden.  
  
#### <a name="pros"></a>Vorteile  
  
-   Administrative Arbeitsstationen und Produktivitäts Arbeitsstationen werden getrennt.  
  
-   IT-Mitarbeiter, die sichere Arbeitsstationen verwenden, um eine Verbindung mit Produktivitäts Arbeitsstationen herzustellen, können separate Anmelde Informationen und Smartcards verwenden, und privilegierte Anmelde Informationen werden nicht auf dem weniger sicheren Computer abgelegt.  
  
#### <a name="cons"></a>Nachteile  
  
-   Zum Implementieren der Lösung sind Entwurfs-und Implementierungs arbeiten sowie stabile Virtualisierungsoptionen erforderlich.  
  
-   Wenn die physischen Arbeitsstationen nicht sicher gespeichert werden, sind Sie möglicherweise anfällig für physische Angriffe, die die Hardware oder das Betriebssystem gefährden und anfällig für das Abfangen von Kommunikationen machen.  
  
### <a name="implementing-a-single-secure-workstation-with-connections-to-separate-productivity-and-administrative-virtual-machines"></a>Implementieren einer einzelnen sicheren Arbeitsstation mit Verbindungen zur Trennung von "Produktivität" und "administrativer" Virtual Machines  
Bei dieser Vorgehensweise können Sie IT-Benutzer eine einzelne physische Arbeitsstation ausstellen, die wie zuvor beschrieben gesperrt ist und für die die Benutzer keinen privilegierten Zugriff haben. Sie können Remotedesktopdienste Verbindungen mit virtuellen Computern bereitstellen, die auf dedizierten Servern gehostet werden, und IT-Mitarbeitern einen virtuellen Computer bereitstellen, auf dem e-Mails und andere Produktivitätsanwendungen ausgeführt werden, sowie einen zweiten virtuellen Computer, der als Benutzer dedizierter administrativer Host.  
  
Sie sollten für die virtuellen Computer eine Smartcard oder eine andere mehrstufige Anmeldung benötigen, und zwar mit anderen Konten als dem Konto, das für die Anmeldung beim physischen Computer verwendet wird. Nachdem ein IT-Benutzer sich an einem physischen Computer anmeldet, kann er seine Produktivitäts-Smartcard verwenden, um eine Verbindung mit dem Remote Produktivitäts Computer und einem separaten Konto und einer Smartcard herzustellen, um eine Verbindung mit dem Remote Verwaltungs Computer herzustellen.  
  
#### <a name="pros"></a>Vorteile  
  
-   IT-Benutzer können eine einzelne physische Arbeitsstation verwenden.  
  
-   Wenn Sie separate Konten für die virtuellen Hosts benötigen und Remotedesktopdienste Verbindungen mit den virtuellen Maschinen herstellen, werden die Anmelde Informationen der IT-Benutzer nicht im Arbeitsspeicher auf dem lokalen Computer zwischengespeichert.  
  
-   Der physische Host kann auf denselben Grad wie administrative Hosts gesichert werden, wodurch die Wahrscheinlichkeit einer Gefährdung des lokalen Computers beeinträchtigt wird.  
  
-   In Fällen, in denen der virtuelle Computer für die Produktivität eines IT-Benutzers oder der virtuelle Computer möglicherweise kompromittiert wurde, kann der virtuelle Computer problemlos auf einen "bekannten guten" Zustand zurückgesetzt werden.  
  
-   Wenn der physische Computer kompromittiert ist, werden keine privilegierten Anmelde Informationen im Arbeitsspeicher zwischengespeichert, und die Verwendung von Smartcards kann die Kompromittierung von Anmelde Informationen durch Tastatureingaben verhindern.  
  
#### <a name="cons"></a>Nachteile  
  
-   Zum Implementieren der Lösung sind Entwurfs-und Implementierungs arbeiten sowie stabile Virtualisierungsoptionen erforderlich.  
  
-   Wenn die physischen Arbeitsstationen nicht sicher gespeichert werden, sind Sie möglicherweise anfällig für physische Angriffe, die die Hardware oder das Betriebssystem gefährden und anfällig für das Abfangen von Kommunikationen machen.  
  
### <a name="implementing-secure-administrative-workstations-and-jump-servers"></a>Implementieren sicherer administrativer Arbeitsstationen und Jump-Server  
Als Alternative zum Sichern administrativer Arbeitsstationen oder in Kombination mit Ihnen können Sie sichere Jump-Server implementieren, und Administratoren können mithilfe von RDP und Smartcards eine Verbindung mit den Sprung Servern herstellen, um administrative Aufgaben auszuführen.  
  
Jump-Server sollten so konfiguriert werden, dass Sie die Remotedesktop Gateway-Rolle ausführen, damit Sie Einschränkungen für Verbindungen mit dem Jump-Server und Ziel Servern implementieren können, die von ihm verwaltet werden. Wenn möglich, sollten Sie auch die Hyper-V-Rolle installieren und [Persönliche virtuelle Desktops](https://technet.microsoft.com/library/dd759174.aspx) oder andere pro-Benutzer-VMS erstellen, damit Administratoren ihre Aufgaben auf den Sprung Servern verwenden können.  
  
Indem Sie die benutzerspezifischen virtuellen Maschinen pro Benutzer auf dem Sprung Server bereitstellen, stellen Sie physische Sicherheit für die administrativen Arbeitsstationen bereit, und Administratoren können Ihre virtuellen Maschinen zurücksetzen oder Herunterfahren, wenn Sie nicht verwendet werden. Wenn Sie nicht möchten, dass die Hyper-V-Rolle und die Remotedesktop Gateway-Rolle auf demselben administrativen Host installiert werden, können Sie Sie auf separaten Computern installieren.  
  
Wenn möglich, sollten Remote Verwaltungs Tools zum Verwalten von Servern verwendet werden. Die Funktion Remoteserver-Verwaltungstools (RSAT) sollte auf den virtuellen Computern der Benutzer installiert werden (oder auf dem Jump Server, wenn Sie keine benutzerspezifischen virtuellen Maschinen für die Verwaltung implementieren), und die administrativen Mitarbeiter sollten über RDP eine Verbindung mit Ihrem virtuelle Computer zum Ausführen administrativer Aufgaben.  
  
In Fällen, in denen ein Administrator eine Verbindung über RDP mit einem Zielserver herstellen muss, um ihn direkt zu verwalten, sollte RD-Gateway so konfiguriert werden, dass die Verbindung nur hergestellt werden kann, wenn der entsprechende Benutzer und Computer zum Herstellen der Verbindung mit dem Ziel verwendet werden. Servers. Die Ausführung von RSAT-Tools (oder ähnlichen Tools) sollte auf Systemen, die nicht als Verwaltungssysteme vorgesehen sind, nicht zulässig sein, wie z. b. allgemeine Arbeitsstationen und Mitglieds Server, die keine Sprung Server sind.  
  
#### <a name="pros"></a>Vorteile  
  
-   Durch das Erstellen von Sprung Servern können Sie bestimmte Server "Zonen" (Sammlungen von Systemen mit ähnlichen Konfigurations-, Verbindungs-und Sicherheitsanforderungen) in Ihrem Netzwerk zuordnen und verlangen, dass die Verwaltung der einzelnen Zonen durch das administrative Personal erreicht wird. Herstellen einer Verbindung zwischen sicheren administrativen Hosts und einem vorgesehenen "Zone"-Server.  
  
-   Durch die Zuordnung von Jump-Servern zu Zonen können Sie präzise Steuerelemente für Verbindungs Eigenschaften und Konfigurations Anforderungen implementieren und problemlos versuchen, die Verbindung von nicht autorisierten Systemen herzustellen.  
  
-   Durch die Implementierung von virtuellen Computern pro Administrator auf Jump-Servern erzwingen Sie das Herunterfahren und Zurücksetzen der virtuellen Maschinen in einen bekannten Zustand, wenn administrative Aufgaben abgeschlossen sind. Durch das Erzwingen des herunter Fahrens (oder Neustarts) der virtuellen Maschinen, wenn administrative Aufgaben abgeschlossen sind, können die virtuellen Computer weder von Angreifern als auch von Angreifern angegriffen werden  
  
#### <a name="cons"></a>Nachteile  
  
-   Dedizierte Server sind für Jump-Server erforderlich, unabhängig davon, ob physisch oder virtuell.  
  
-   Das Implementieren von vorgesehenen Sprung Servern und administrativen Arbeitsstationen erfordert eine sorgfältige Planung und Konfiguration, die allen in der Umgebung konfigurierten Sicherheitszonen zugeordnet ist.  
  


