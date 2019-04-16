---
ms.assetid: eafdddc3-40d7-4a75-8f4f-a45294aabfc8
title: Implementieren sichere Administrative Hosts
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 42be89311f11ecc6a967b8b40600b53311253b89
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="implementing-secure-administrative-hosts"></a>Implementieren sichere Administrative Hosts

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sichere administrative Hosts sind Arbeitsstationen oder Servern, die speziell für die Zwecke der Erstellung von sicheren Plattformen aus denen privilegierte Konten in Active Directory oder Ausführen von Verwaltungsaufgaben auf Domänencontrollern, Domäne Angehörige Systeme und Anwendungen, die Domäne Angehörige Systeme unter konfiguriert wurden. In diesem Fall bezieht sich "privilegierte Konten", nicht nur für Konten, die Mitglieder der am häufigsten privilegierten Gruppen in Active Directory sind, sondern auch für Konten, die zugewiesenen Rechte und Berechtigungen, mit die administrative Aufgaben ausgeführt werden können.  
  
Diese Konten möglicherweise beim Helpdesk-Konten, die die Möglichkeit zum Zurücksetzen von Kennwörtern für die meisten Benutzer in einer Domäne, Konten, die zum Verwalten von DNS-Einträge und Zonen verwendet werden oder für Konten, die für die Verwaltung verwendet werden. Sichere administrative Hosts auf Verwaltungsfunktionen vorgesehen sind, und sie führen keine Software, z. B. e-Mail-Anwendungen, Webbrowser oder Produktivitätssoftware wie Microsoft Office.  
  
Obwohl "mit hohen Berechtigungen" Konten und Gruppen entsprechend der am häufigsten repräsentative Motoröltemperatur geschützten sein soll, ist dies nicht die Notwendigkeit, schützen Konten und Gruppen, die mehr Standardbenutzer, die Rechte Konten gewährt wurden auszuschließen.  
  
Eine sichere administrative Hosts kann eine dedizierte Arbeitsstation sein, die wird nur für administrative Aufgaben ein Mitgliedsserver verwendet, der die Remotedesktop-Gatewayserver-Serverrolle ausgeführt wird und mit dem IT-Anwender, die zum Ausführen der Verwaltung des Zielhosts oder ein Server, der Hyper-V-Rolle ausgeführt und bietet einen eindeutigen virtueller Computer für jeden Benutzer IT für ihre Verwaltungsaufgaben verwenden, verbinden. In vielen Umgebungen können Kombinationen von alle drei Methoden implementiert werden.  
  
Implementieren sichere administrative Hosts erfordert, Planung und Konfiguration, die mit Ihrer Organisation Größe, Verwaltungsmethoden, Risikobereitschaft und Budget konsistent ist. Überlegungen und Optionen für das Implementieren von sicheren administrative Hosts sind für die Verwendung bei der Entwicklung einer administrativen Strategie für Ihre Organisation geeigneten hier bereitgestellt.  
  
## <a name="principles-for-creating-secure-administrative-hosts"></a>Prinzipien für das Erstellen von sicheren Administrative Hosts  
Um effektiv Systeme vor Angriffen zu schützen, sollte ein paar allgemeine Prinzipien beachten stehen:  
  
1.  Sie sollten nie ein vertrauenswürdiges Systems (d. h. einem sicheren Server z. B. ein Domänencontroller) verwalten, von einer weniger vertrauenswürdigen Host (d. h. eine Arbeitsstation, die nicht auf demselben Sicherheitsgrad wie die Systeme gesichert wird, verwaltet).  
  
2.  Sie sollten sich nicht auf einem einzelnen authentifizierungsfaktors verlassen, beim Ausführen privilegierter Aktivitäten; Das heißt, sollten Kombinationen aus Benutzername und Kennwort nicht akzeptabel Authentifizierung betrachtet werden, da nur ein einzelner Faktor (etwas, das Sie kennen) dargestellt wird. Sie sollten erwägen, in denen Anmeldeinformationen generiert und zwischengespeichert oder gespeichert in administrative Szenarien.  
  
3.  Obwohl die meisten Angriffe in der aktuellen Bedrohungslage Malware und böswilliger hacking nutzen zu können, lassen Sie physische Sicherheit beim Entwerfen und implementieren sichere administrative Hosts nicht.  
  
### <a name="account-configuration"></a>Konfiguration des Dienstkontos  
Auch wenn Ihre Organisation nicht aktuell Smartcards verwenden, sollten Sie für privilegierte Konten und sichere administrative Hosts implementieren. Administrative Hosts sollte für die Smartcard-Anmeldung für alle Konten erforderlich, ändern die folgende Einstellung in einem Gruppenrichtlinienobjekt, das mit den administrativen Hosts mit Organisationseinheiten verknüpft ist, indem Sie konfiguriert werden:  
  
**Computer Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Sicherheitsoptionen\Interaktive Anmeldung: Smartcard erforderlich**  
  
Diese Einstellung werden alle interaktive Anmeldungen an eine Smartcard, unabhängig von der Konfiguration auf ein einzelnes Konto in Active Directory verwenden muss.  
  
Sie sollten auch konfigurieren, dass sichere administrative Hosts um Anmeldung nur von autorisierten Konten zu erlauben, die in konfiguriert werden können:  
  
**Computer Computerkonfiguration\Richtlinien\Windows Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien / Einstellungen\Sicherheitseinstellungen\Lokale Richtlinien\Zuweisen von Benutzerrechten**  
  
Dies gewährt interaktive (und gegebenenfalls Remote Desktop Services) Anmelderechte nur von autorisierten Benutzern das sichere administrative Hosts.  
  
### <a name="physical-security"></a>Physische Sicherheit  
Für die administrative Hosts als vertrauenswürdig eingestuft werden müssen sie konfiguriert und auf demselben Sicherheitsgrad wie die Systeme, die sie verwalten geschützt werden. Der Empfehlungen den meisten [Domain-Controller vor Angriffen schützen](../../../ad-ds/plan/security-best-practices/Securing-Domain-Controllers-Against-Attack.md) gelten auch für die Hosts, die zum Verwalten von Domänencontrollern und AD DS-Datenbank verwendet werden. Eine der Herausforderungen Implementieren von sicheren administrative Systemen in den meisten Umgebungen ist physischer Sicherheit schwieriger zu implementieren, da diese Computer häufig in Bereichen befinden, die nicht so sicher wie Server im Datencenter, z. B. administrative Benutzerdesktops gehostet werden kann.  
  
Physische Sicherheit umfasst die physischen Zugriff auf den administrativen Hosts steuern. In einem kleinen Unternehmen kann dies bedeuten, dass Sie verwalten, einer dedizierten administrativen Arbeitsstationen, die gehalten wird in einer Office oder einer Schreibtischschublade nicht gesperrt. Oder es kann ein Hinweis darauf, dass Sie der Verwaltung von Active Directory oder Ihren Domänencontrollern durchführen müssen, Sie an den Domänencontroller direkt anmelden.  
  
In mittelgroßen Organisationen können Sie erwägen, Implementieren von sicheren "springen administrative Server", die an einem sicheren Ort im Büro befinden und werden verwendet, wenn die Verwaltung von Active Directory oder als Domänencontroller erforderlich ist. Sie können auch Administratorarbeitsstationen implementieren, die an sicheren Orten nicht in Verwendung, mit oder ohne sprungbrettservern gesperrt sind.  
  
In großen Organisationen können Sie die Datacenter-untergebracht sprungbrettservern bereitstellen, die streng kontrollierten auf Active Directory Zugriff; Domänencontroller; und -Datei, drucken oder Anwendungsserver. Implementierung von eine sprungbrettserverarchitektur ist wahrscheinlich eine Kombination von sicheren Arbeitsstationen und Servern in großen Umgebungen enthalten.  
  
Unabhängig von der Größe Ihrer Organisation und das Design Ihrer administrativen Hosts physische Computern vor unberechtigtem Zugriff oder Diebstahl schützen, und sollte BitLocker Drive Encryption zum Verschlüsseln und schützen Sie die Laufwerke auf administrativen Hosts verwenden. Durch die Implementierung von BitLocker auf administrativen Hosts, können auch, wenn ein Host gestohlen wird oder seine Laufwerke entfernt werden, Sie stellen Sie sicher, dass die Daten auf dem Laufwerk nicht zugegriffen werden kann, dass nicht autorisierte Benutzer.  
  
### <a name="operating-system-versions-and-configuration"></a>Betriebssystemversionen und -Konfiguration  
Alle administrativen Hosts an, ob Servern oder Arbeitsstationen, sollte das neueste Betriebssystem in Ihrer Organisation verwendet, weiter oben in diesem Dokument beschriebenen Gründen ausgeführt. Durch Ausführen von aktuellen Betriebssystemen, Ihrem Verwaltungspersonal Vorteile von neuen Sicherheitsfeatures, vollständige Unterstützung und zusätzliche Funktionen, die in das Betriebssystem eingeführt. Wenn Sie ein neues Betriebssystem bewerten, indem sie zunächst auf den administrativen Hosts bereitgestellt, müssen Sie darüber hinaus Vertrautmachen mit der neuen Features, Einstellungen und Management Mechanismen, die sie bietet, die anschließend bei der Planung breiteren Bereitstellung des Betriebssystems genutzt werden können. Dann werden die ausgeklügelten Benutzer in Ihrer Organisation auch die Benutzer, die das neue Betriebssystem kennen und am besten für die Unterstützung positioniert sind.  
  
### <a name="microsoft-security-configuration-wizard"></a>Microsoft-Sicherheitskonfigurations-Assistenten  
Wenn Sie als Teil der Strategie für die administrative Host sprungbrettservern implementieren, sollten Sie den integrierten Sicherheitskonfigurations-Assistenten verwenden, so konfigurieren Sie den Dienst, Registrierung, überwachen und Firewall-Einstellungen für den Server-Angriffsfläche zu verringern. Wenn die Konfigurationseinstellungen des Sicherheitskonfigurations-Assistenten gesammelt und konfiguriert wurde, können die Einstellungen in ein GPO konvertiert werden, die verwendet wird, um eine konsistente Basiskonfiguration für alle Sprunglisten-Server zu erzwingen. Sie können das Gruppenrichtlinienobjekt zum Implementieren der Sicherheit Einstellungen spezifische wechselserver weiter bearbeiten und können alle Einstellungen mit zusätzlichen Baseline-Einstellungen, die von Microsoft Security Compliance Manager extrahiert kombinieren.  
  
### <a name="microsoft-security-compliance-manager"></a>Microsoft Security Compliance Manager  
Die [Microsoft Security Compliance Manager](https://technet.microsoft.com/library/cc677002.aspx) ist ein Tool, frei verfügbar, die Sicherheitskonfigurationen integriert, die von Microsoft, basierend auf der Konfiguration des Betriebssystems Version und die Rolle, empfohlen werden und sammelt in ein einzelnes Tool und die UI, die zum Erstellen und konfigurieren Baseline-Sicherheitsrichtlinie für Domänencontroller verwendet werden kann. Microsoft Security Compliance Manager-Vorlagen können kombiniert werden, mit den Sicherheitskonfigurations-Assistenten Einstellungen, und das umfassende von Konfigurationsbasislinien für Sprunglisten Server bereitgestellt und erzwungen mithilfe von GPOs, die an die Organisationseinheiten in der Sprungliste Server in Active Directory befinden bereitgestellt werden.  
  
> [!NOTE]  
> Zum Zeitpunkt dieses Artikels Microsoft Security Compliance Manager enthält keine sprungbrettservern oder andere sichere administrative Hosts spezifische Einstellungen, aber Security Compliance Manager (SCM) kann weiterhin zum erste Basislinien für Ihre administrativen Hosts zu erstellen. Um die Hosts zu schützen, sollten Sie jedoch weitere Sicherheitseinstellungen für sehr sichere Arbeitsstationen und Server anwenden.  
  
### <a name="applocker"></a>AppLocker  
Administrative Hosts und virtuellen Machinesshould werden mit Skripts, Tools und Anwendung weiße über AppLocker oder einer Drittanbieter-Einschränkung Anwendungssoftware konfiguriert. Administrative Anwendungen oder Dienstprogramme, die nicht zum Sichern von Einstellungen entsprechen, sollten aktualisiert oder ersetzt mit Tools, die Entwicklung von sicheren und Verwaltungsmethoden entspricht. Wenn neue oder zusätzliche Tools auf einem administrativen Host benötigt wird, Anwendungen und Dienstprogramme gründlich getestet werden, und wenn die Tools für die Bereitstellung auf administrativen Hosts geeignet ist, können sie auf der Systeme weiße hinzugefügt werden.  
  
### <a name="rdp-restrictions"></a>RDP-Einschränkungen  
Obwohl die jeweiligen Konfiguration je nach Architektur Ihrer administrativen Systeme variiert sollten Sie die Einschränkungen, die auf dem Konten und -Computer herstellen (Remotedesktopprotokoll) Verbindungen mit verwalteten Systemen, z. B. die Verwendung von Remotedesktop-Gatewayserver (RD-Gateway) springen Server zum Steuern des Zugriffs auf Domänencontroller und andere verwaltete verwendet werden können einfügen Systeme von autorisierten Benutzern und Systemen.  
  
Sie sollten interaktive Anmeldungen von autorisierten Benutzern erlauben und entfernen oder sogar blockieren andere Anmeldetypen, die nicht für den Zugriff auf Server erforderlich sind.  
  
### <a name="patch-and-configuration-management"></a>Patch und Verwaltung  
Kleinere Organisationen benötigen möglicherweise angeboten, wie Windows Update oder [Windows Server Update Services](https://technet.microsoft.com/windowsserver/bb332157) (WSUS) für die Bereitstellung von Updates für Windows-Systemen zu verwalten, während in größeren Organisationen Patch und Konfiguration Unternehmensverwaltungssoftware wie System Center Configuration Manager implementieren können. Unabhängig von der Mechanismen, mit denen, die Sie verwenden, um Updates für Ihre Server und Arbeitsstation Auffüllung bereitzustellen, sollten Sie separate Bereitstellungen für Hochsicherheitssystemen wie z. B. Domänencontroller, Zertifizierungsstellen und administrativen Hosts. Durch die Trennung dieser Systeme über die allgemeine Management-Infrastruktur, wenn Ihre Management-Software oder eines Diensts Konten gefährdet sind, kann die Gefährdung einfach auf die sicherste Systeme in Ihrer Infrastruktur erweitert werden.  
  
Obwohl Sie keine manuelle Aktualisierung Prozesse für die sichere Systeme implementieren sollten, sollten Sie eine separate Infrastruktur für die Aktualisierung von sicherer Systems konfigurieren. Auch in sehr großen Organisationen kann diese Infrastruktur in der Regel über dedizierte WSUS-Server und GPOs für gesicherte Systeme implementiert werden.  
  
### <a name="blocking-internet-access"></a>Sperren des Internetzugriffs  
Administrative Hosts sollte nicht gestattet werden, auf das Internet zugreifen, und sollten sie in der Lage, ein Unternehmensintranet zu suchen. Webbrowser und ähnliche Apps sollten auf administrativen Hosts nicht zugelassen werden. Sie können Zugriff auf das Internet für sichere Hosts über eine Kombination von Umkreis-Firewall-Einstellungen, WFAS Konfiguration und "Schwarzes Loch" Proxykonfiguration auf sichere Hosts blockieren. Sie können auch Anwendungswhitelisting verwenden, um zu verhindern, dass von Webbrowsern auf administrativen Hosts verwendet wird.  
  
### <a name="virtualization"></a>Virtualisierung  
Wenn möglich, sollten Sie die Implementierung von virtuellen Computern als administrative Hosts. Verwenden der Virtualisierung, können Sie pro Benutzer erstellen administrative Systeme, die zentral gespeichert und verwaltet werden, und die können problemlos heruntergefahren werden bei nicht in Gebrauch, um sicherzustellen, dass die Anmeldeinformationen nicht aktiv auf den administrativen Systemen gelassen werden. Sie können auch erzwingen, dass virtuelle administrativen Hosts, einen Anfangssnapshot nach jeder Verwendung sicherstellen zurückgesetzt werden, dass die virtuellen Computer unberührte bleiben. Weitere Informationen zu den Optionen für die Virtualisierung von administrativen Hosts finden Sie im folgenden Abschnitt.  
  
## <a name="sample-approaches-to-implementing-secure-administrative-hosts"></a>Beispiel für Ansätze zum Implementieren von sicheren Administrative Hosts  
Unabhängig davon, wie Sie entwerfen und Bereitstellen Ihrer Infrastruktur administrative Hosts sollten Sie die Richtlinien in "Prinzipien für Erstellen von sicheren Administrative Hosts" weiter oben in diesem Thema Bedenken. Jede der hier beschriebenen Verfahren bietet allgemeine Informationen, wie Sie "Verwaltung" und "Produktivität" Systeme, die von Ihrer IT-Abteilung verwendet trennen können. Produktivitäts-Systeme sind Computer, die IT-Administratoren einsetzen, e-Mails, im Internet surfen und allgemeine Produktivitätssoftware wie Microsoft Office verwenden. Administrative Systeme sind Computer, auf denen abgesichert sind und zum Ziel gesetzt, die für die tägliche Verwaltung der IT-Umgebung verwenden.  
  
Die einfachste Methode zum Implementieren von sicheren administrative Hosts ist Ihre IT-Mitarbeiter mit sicheren Arbeitsstationen bereitstellen, von dem sie administrative Aufgaben ausführen können. In einer reinen Arbeitsstation-Implementierung wird jeder administrativen Arbeitsstation zum Starten von Verwaltungstools und RDP-Verbindungen zum Verwalten von Servern und anderer Infrastruktur verwendet. Nur Arbeitsstation-Implementierungen können effektiv in kleineren Organisationen sein, obwohl größere und komplexere Infrastrukturen verteilte Design für administrative Hosts in denen dedizierten administrativen Servern und Arbeitsstationen verwendet werden, profitieren können, wie unter "Implementieren von sicheren Administrative Arbeitsstationen und springen Server" weiter unten in diesem Thema.  
  
### <a name="implementing-separate-physical-workstations"></a>Implementieren von separaten physischen Arbeitsstationen  
Eine Möglichkeit, administrativen Hosts zu implementieren ist jeder IT-Benutzer zwei Arbeitsstationen ausstellen. Eine Arbeitsstation dient mit einem "regular" Benutzerkonto zum Ausführen von Aktivitäten wie die Überprüfung von e-Mail und Produktivitäts-Apps verwenden, während die zweite Arbeitsstation ausschließlich auf Verwaltungsfunktionen vorgesehen ist.  
  
Für die Arbeitsstation Produktivität kann die IT-Mitarbeiter reguläre Benutzerkonten anstelle der Verwendung von privilegierter Konten anmelden ungeschützte Computer zugewiesen werden. Die administrative Arbeitsstation eine repräsentative Motoröltemperatur kontrollierten Konfiguration konfiguriert werden, und die IT-Mitarbeiter sollten ein anderes Konto verwenden, um die Administratorarbeitsstationen anmelden.  
  
Wenn Sie Smartcards implementiert haben, Administratorarbeitsstationen Smartcard-Anmeldung muss konfiguriert werden, und IT-Mitarbeiter gegeben werden separate Konten für administrative verwenden, auch für die Verwendung von Smartcards für die interaktive Anmeldung konfiguriert. Die administrativen Hosts sollte verstärkt wie zuvor beschrieben, und nur bestimmte IT Benutzer dürfen, die Anmeldung an der Verwaltungsarbeitsstation.  
  
#### <a name="pros"></a>Experten  
Separate physische Systeme implementiert wird, können Sie sicherstellen, dass jeder Computer für die Rolle entsprechend konfiguriert ist und IT-Anwender administrative Systemen Risiko versehentlich verfügbar machen können.  
  
#### <a name="cons"></a>Nachteile  
  
-   Implementieren von separaten physischen Computern erhöht die Kosten für Hardware.  
  
-   Protokollierung auf einem physischen Computer mit Anmeldeinformationen, die zur Verwaltung von remote-Systems verwendet werden, werden die Anmeldeinformationen im Speicher zwischenspeichert.  
  
-   Wenn administrative Arbeitsstationen nicht sicher gespeichert sind, kann über Mechanismen wie physische Hardware Keylogger oder andere physische Angriffe manipulieren anfällig werden.  
  
### <a name="implementing-a-secure-physical-workstation-with-a-virtualized-productivity-workstation"></a>Implementieren einer sicheren physischen Arbeitsstation mit einer Arbeitsstation virtualisierten Produktivität  
Bei dieser Herangehensweise IT-Anwender erhalten eine gesicherte administrativen Arbeitsstationen, die von dem sie alltägliche administrative Funktionen durchführen können mithilfe der Remoteserver-Verwaltungstools (RSAT) oder RDP-Verbindungen mit Servern innerhalb ihres Bereichs der Verantwortung. Wenn IT-Anwender Aufgaben ausführen müssen, können sie mit einer remote Produktivität Arbeitsstation als virtueller Computer ausgeführt über RDP verbinden. Separate Anmeldeinformationen für jede Arbeitsstation verwendet werden soll, und Steuerelemente, z. B. Smartcards implementiert werden sollte.  
  
#### <a name="pros"></a>Experten  
  
-   Administrativen Arbeitsstationen und Produktivität Arbeitsstationen sind getrennt.  
  
-   IT-Mitarbeiter mit sicheren Arbeitsstationen produktionsarbeitsstationen herstellen können Sie separate Anmeldeinformationen und Smartcards und privilegierte Anmeldeinformationen sind nicht auf dem Computer weniger sicheren hinterlegt.  
  
#### <a name="cons"></a>Nachteile  
  
-   Implementierung der Lösung erfordert, Entwurf und Implementierung und stabile Virtualisierungsoptionen.  
  
-   Wenn die physischen Arbeitsstationen nicht sicher gespeichert sind, kann physische Angriffe anfällig werden, die die Hardware oder das Betriebssystem und die machen Kommunikation abgefangen werden.  
  
### <a name="implementing-a-single-secure-workstation-with-connections-to-separate-productivity-and-administrative-virtual-machines"></a>Implementieren einer sicheren Workstation mit Verbindungen mit "Produktivität" und "Administratoren" virtuelle Computer trennen  
Bei dieser Vorgehensweise können Sie IT-Anwender ausstellen eine physischen Workstation, gesperrt ist wie zuvor beschrieben, und auf dem IT-Benutzer haben keinen privilegierten Zugriff. Sie können bereitstellen Remote Desktop Services-Verbindungen mit virtuellen Maschinen auf dedizierten Servern gehostet bietet IT-Mitarbeiter eine virtuelle Maschine, die e-Mail und andere Produktivitäts-Apps ausgeführt wird und eine zweite virtuelle Computer, der als der Benutzer dedizierten administrativen Hosts konfiguriert ist.  
  
Fordern Sie Smartcard- oder andere mehrstufige Anmeldung für die virtuellen Computer, verwenden separate Konten als das Konto, das verwendet wird, um die physischen Computer anmelden. Nachdem ein IT-Benutzer zu einem physikalischen Computer anmeldet, können sie ihre Produktivität Smartcard-PIN verwenden, Verbindung mit ihren Computer remote Produktivität und ein separates Konto und Smartcard-Verbindung mit ihrer Computer für die Remoteverwaltung.  
  
#### <a name="pros"></a>Experten  
  
-   IT-Anwender können eine einzelne physische Arbeitsstation.  
  
-   Durch separate Konten für den virtuellen Hosts und Remote Desktop Services-Verbindungen zu virtuellen Computern erforderlich sind werden IT-Anwender Anmeldeinformationen nicht im Arbeitsspeicher auf dem lokalen Computer zwischengespeichert.  
  
-   Die physischen Hosts kann auf demselben Sicherheitsgrad wie administrative Hosts, reduziert die Wahrscheinlichkeit, dass der Gefährdung des lokalen Computers gesichert werden.  
  
-   In Fällen, in denen des Benutzers ein IT-Produktivität virtuellen Computer oder seine administrativen virtuelle Maschine beschädigt wurden, kann die virtuelle Maschine problemlos in einen Zustand "als funktionierend bekannte" zurückgesetzt werden.  
  
-   Wenn der physische Computer gefährdet ist, kann werden keine privilegierten Anmeldeinformationen im Speicher zwischengespeichert, und die Verwendung von Smartcards Gefährdung der Anmeldeinformationen durch Keylogger.  
  
#### <a name="cons"></a>Nachteile  
  
-   Implementierung der Lösung erfordert, Entwurf und Implementierung und stabile Virtualisierungsoptionen.  
  
-   Wenn die physischen Arbeitsstationen nicht sicher gespeichert sind, kann physische Angriffe anfällig werden, die die Hardware oder das Betriebssystem und die machen Kommunikation abgefangen werden.  
  
### <a name="implementing-secure-administrative-workstations-and-jump-servers"></a>Implementieren von sicheren administrativen Arbeitsstationen und Sprungbrettservern  
Als Alternative zum Schutz von administrativer Arbeitsstationen oder in Kombination mit ihnen können Sie sichere sprungbrettservern implementieren, und Administratoren können den Sprung-Servern, die mithilfe von RDP und Smartcards für administrative Aufgaben eine Verbindung herstellen.  
  
Sprungbrettservern sollte konfiguriert werden, führen Sie den Remotedesktopgateway-Rolle Möglichkeit zum Implementieren von Einschränkungen für Verbindungen mit dem Server Sprunglisten und zu Zielservern, die von diesem verwaltet werden. Wenn möglich, Sie sollten auch Installieren der Hyper-V-Rolle und erstellen [persönliche virtuelle Desktops](https://technet.microsoft.com/library/dd759174.aspx) oder andere pro-Benutzer virtuelle Maschinen für Administratoren, die für ihre Aufgaben auf den sprungbrettservern verwendet.  
  
Gewähren den Administratoren pro Benutzer virtuelle Maschinen auf dem sprungbrettserver, Sie die physischen Sicherheit für die Arbeitsstationen für Administratoren bereitstellen und Administratoren ihre virtuellen Maschinen nicht in Gebrauch Herunterfahren oder zurücksetzen können. Wenn Sie nicht die Hyper-V-Rolle und den Remotedesktopgateway-Rolle auf demselben Host administrative installieren möchten, können Sie diese auf separaten Computern installieren.  
  
Nach Möglichkeit sollte Remoteserver-Verwaltungstools zum Verwalten von Servern verwendet werden. Das Feature "Remoteserver-Verwaltungstools (RSAT)" sollte auf virtuellen Maschinen von den Benutzern (oder der sprungbrettserver, wenn Sie nicht pro Benutzer virtuelle Computer für die Verwaltung implementieren) installiert werden und administrative Mitarbeiter sollten an ihre virtuellen Maschinen Ausführen von Verwaltungsaufgaben über RDP verbinden.  
  
In Fällen, wenn ein Administrator zu einem Zielserver direkt verwalten über RDP verbinden muss sollten RD-Gateway konfiguriert werden die Verbindung kann nur dann, wenn die entsprechenden Benutzer und Computer, zum Herstellen der Verbindung auf den Zielserver verwendet werden hergestellt werden. Die Ausführung der Remoteserver-Verwaltungstools (oder ähnlich) Tools verboten werden auf Systemen, die nicht Management-Systeme, z. B. allgemeinen Verwendung Arbeitsstationen und Servern, die nicht Servern wechseln.  
  
#### <a name="pros"></a>Experten  
  
-   Sprungbrettservern erstellen, können Sie bestimmte Server "Zonen" (Sammlungen von Systemen mit ähnlichen Anforderungen für Konfiguration, Verbindung und Sicherheit) in Ihrem Netzwerk zugeordnet und erfordern, dass die Verwaltung der einzelnen Zonen administrative Mitarbeiter, die die Verbindung über sichere administrative Hosts zu einem festgelegten "" Zonenserver erreicht wird.  
  
-   Durch die Zuordnung sprungbrettservern Zonen, präzise Steuerelemente für die Verbindungseigenschaften und konfigurationsanforderungen implementieren können, und versucht, eine Verbindung nicht dazu berechtigte Systeme einfach identifizieren können.  
  
-   Durch die Implementierung von pro-Administrator virtuelle Maschinen auf sprungbrettservern, erzwingen Sie Herunterfahren und der virtuellen Computer in einen bekannten einwandfreien Zustand zurücksetzen, wenn Sie administrative Aufgaben abgeschlossen sind. Durch das Erzwingen Herunterfahren (oder Neustarten) der virtuellen Computer, wenn Sie administrative Aufgaben abgeschlossen sind, die virtuellen Computer kann nicht als Ziel von Angreifern verwendet werden, noch werden Methoden des anmeldeinformationsdiebstahls möglich, da Arbeitsspeicher zwischengespeicherten Anmeldeinformationen nicht nach einem Neustart beibehalten werden.  
  
#### <a name="cons"></a>Nachteile  
  
-   Dedizierte Server sind für Sprunglisten-Server erforderlich, physischen oder virtuellen.  
  
-   Implementierung festgelegten Server springen und Administratorarbeitsstationen erfordert sorgfältige Planung und Konfiguration, die alle in der Umgebung konfigurierten Sicherheitszonen zugeordnet ist.  
  


