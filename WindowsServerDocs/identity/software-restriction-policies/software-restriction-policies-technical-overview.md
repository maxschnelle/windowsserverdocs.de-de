---
title: Richtlinien zur Softwareeinschränkung (Software Restriction Policies, SRP) – Technische Übersicht
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: dc7013b0-0efd-40fd-bd6d-75128adbd0b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 38625a8d416345a6a7ed40c021b55aa10d1fd92f
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855273"
---
# <a name="software-restriction-policies-technical-overview"></a>Richtlinien zur Softwareeinschränkung (Software Restriction Policies, SRP) – Technische Übersicht

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden Richtlinien für Software Einschränkung beschrieben, wann und wie die Funktion verwendet wird, welche Änderungen in früheren Releases implementiert wurden, und es werden Links zu zusätzlichen Ressourcen bereitgestellt, die Ihnen beim Erstellen und Bereitstellen von Richtlinien für Software Einschränkung ab Windows helfen. Server 2008 und Windows Vista.

## <a name="introduction"></a>Einführung
Software Einschränkungs Richtlinien bieten Administratoren einen Gruppenrichtlinie gesteuerten Mechanismus zum Identifizieren von Software und Steuern der Möglichkeit, auf dem lokalen Computer auszuführen. Diese Richtlinien können verwendet werden, um Computer, auf denen Microsoft Windows-Betriebssysteme ausgeführt werden (ab Windows Server 2003 und Windows XP Professional), vor bekannten Konflikten zu schützen und die Computer vor Sicherheitsbedrohungen wie bösartigen Viren zu schützen. und Trojaner. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, mit der Sie ausschließlich die Ausführung explizit ausgewiesene Anwendungen zulassen. Richtlinien für Softwareeinschränkung sind mit Microsoft Active Directory und Gruppenrichtlinien verknüpft. Sie können Richtlinien für Softwareeinschränkung auch auf eigenständigen Computern erstellen.

Richtlinien für Softwareeinschränkung sind Vertrauensrichtlinien. Hierbei handelt es sich um von einem Administrator festgelegte Vorschriften, um die Ausführung von Skripts und anderem Code zu beschränken, der als nicht als absolut vertrauenswürdig erachtet wird. Die Erweiterung für Software Einschränkungs Richtlinien für den Editor für lokale Gruppenrichtlinien bietet eine einzelne Benutzeroberfläche, über die die Einstellungen zum Einschränken der Anwendungs Verwendung auf dem lokalen Computer oder in einer Domäne verwaltet werden können.

## <a name="procedures"></a>Verfahren

-   [Verwalten der Richtlinien für Softwareeinschränkung](administer-software-restriction-policies.md)

    -   [Festlegen der Zulassungs-und Verweigerungs Liste und des Anwendungs Bestands für Richtlinien für Software Einschränkung](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

    -   [Arbeiten mit Regeln der Richtlinien für Softwareeinschränkung](work-with-software-restriction-policies-rules.md)

    -   [Verwenden von Richtlinien für Software Einschränkung zum Schutz Ihres Computers vor einem e-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

-   [Behandeln von Problemen mit Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md)

## <a name="software-restriction-policy-usage-scenarios"></a>Verwendungs Szenarien für Software Einschränkungs Richtlinien
Geschäfts Benutzer können mithilfe von e-Mail-, Instant Messaging-und Peer-to-Peer-Anwendungen zusammenarbeiten. Wenn sich diese Zusammenarbeit erhöhen, insbesondere bei der Verwendung des Internets beim Business Computing, sollten Sie daher die Bedrohungen von schädlichem Code wie Würmer, Viren und böswillige Benutzer-oder Angreifer Bedrohungen durchführen.

Benutzer erhalten möglicherweise feindlichen Code in vielen Formularen und reichen von nativen ausführbaren Windows-Dateien (exe-Dateien) bis hin zu Makros in Dokumenten (z. b. doc-Dateien) bis hin zu Skripts (z. b. VB-Dateien). Böswillige Benutzer oder Angreifer verwenden häufig Social Engineering-Methoden, um Benutzern das Ausführen von Code mit Viren und Würmern zu verschaffen. (Social Engineering ist ein Begriff, mit dem Personen das Kennwort oder eine Form von Sicherheitsinformationen offenlegen.) Wenn dieser Code aktiviert ist, kann er Denial-of-Service-Angriffe im Netzwerk erzeugen, sensible oder private Daten an das Internet senden, die Sicherheit des Computers gefährden oder den Inhalt des Festplatten Laufwerks beschädigen.

IT-Organisationen und Benutzer müssen feststellen können, welche Software sicher ausgeführt werden kann und was nicht. Mit den großen Zahlen und Formularen, die der feindliche Code annehmen kann, wird dies zu einer schwierigen Aufgabe.

Um Ihre Netzwerk Computer vor Schadsoftware und unbekannter oder nicht unterstützter Software zu schützen, können Organisationen Software Einschränkungs Richtlinien als Teil ihrer gesamten Sicherheitsstrategie implementieren.

Administratoren können Richtlinien für Softwareeinschränkung für die folgenden Aufgaben verwenden:

-   Definieren, was als vertrauenswürdiger Code gilt.

-   Entwerfen einer flexiblen Gruppenrichtlinie zum Regulieren von Skripts, ausführbaren Dateien und ActiveX-Steuerelementen.

Richtlinien für Softwareeinschränkung werden durch das Betriebssystem und von Anwendungen (beispielsweise Skriptanwendungen) durchgesetzt, die Richtlinien für Softwareeinschränkungen erfüllen.

Administratoren können Richtlinien für Softwareeinschränkung insbesondere für die folgenden Zwecke verwenden:

-   Geben Sie an, welche Software (ausführbare Dateien) auf Client Computern ausgeführt werden kann.

-   Verhindern, dass Benutzer bestimmte Programme auf gemeinsam genutzten Computern ausführen.

-   Angeben, wer vertrauenswürdige Herausgeber zu Client Computern hinzufügen kann

-   Festlegen des Umfangs der Richtlinien für Software Einschränkung (geben Sie an, ob die Richtlinien alle Benutzer oder eine Teilmenge von Benutzern auf Client Computern betreffen)

-   Verhindern, dass ausführbare Dateien auf dem lokalen Computer, in einer Organisationseinheit, am Standort oder in der Domäne ausgeführt werden. Dies wäre in adäquat, wenn Sie Richtlinien für Softwareeinschränkung nicht verwenden, um potenziellen Problemen durch böswillige Benutzer zu begegnen.

## <a name="differences-and-changes-in-functionality"></a><a name="BKMK_Diffs_Changes"></a>Unterschiede und Funktionsänderungen
Es gibt keine Änderungen an der Funktionalität von SRP für Windows Server 2012 und Windows 8.

**Unterstützte Versionen**

Software Einschränkungs Richtlinien können nur auf Computern konfiguriert werden, auf denen mindestens Windows Server 2003 ausgeführt wird, einschließlich Windows Server 2012 und mindestens Windows XP, einschließlich Windows 8.

> [!NOTE]
> Bestimmte Editionen des Windows-Client Betriebssystems, die mit Windows Vista beginnen, verfügen nicht über Richtlinien für Software Einschränkungen. Computer, die nicht von Gruppenrichtlinie in einer Domäne verwaltet werden, erhalten möglicherweise keine verteilten Richtlinien.

**Vergleichen von Anwendungs Steuerungsfunktionen in Richtlinien für Software Einschränkung und AppLocker**

In der folgenden Tabelle werden die Features und Funktionen von AppLocker und den Richtlinien für Softwareeinschränkung verglichen.

|Anwendungssteuerungsfunktion|Softwareeinschränkungsrichtlinien|AppLocker|
|----------------|----|-------|
|Gültigkeitsbereich|Richtlinien für Softwareeinschränkung können auf allen Windows-Betriebssystemen ab Windows XP und Windows Server 2003 angewendet werden.|AppLocker-Richtlinien gelten nur für Windows Server 2008 R2, Windows Server 2012, Windows 7 und Windows 8.|
|Richtlinienerstellung|SRP-Richtlinien werden mithilfe von Gruppenrichtlinien verwaltet, und nur der Administrator des GPO kann die SRP-Richtlinie aktualisieren. Der Administrator auf dem lokalen Computer kann die im lokalen GPO definierten SRP-Richtlinien ändern.|AppLocker-Richtlinien werden mithilfe von Gruppenrichtlinien verwaltet, und nur der Administrator des GPO kann die Richtlinie aktualisieren. Der Administrator auf dem lokalen Computer kann die im lokalen GPO definierten AppLocker-Richtlinien ändern.<p>Mit AppLocker können Fehlermeldungen so angepasst werden, dass Benutzer auf eine Webseite für Hilfe verwiesen werden.|
|Richtlinienwartung|SRP-Richtlinien müssen mithilfe des Snap-Ins „Lokale Sicherheitsrichtlinie“ (bei lokal erstellten Richtlinien) oder der Gruppenrichtlinien-Verwaltungskonsole (GPMC) aktualisiert werden.|AppLocker-Richtlinien können mithilfe des Snap-Ins „Lokale Sicherheitsrichtlinie“ (bei lokal erstellten Richtlinien), der GPMC oder den Windows PowerShell-Cmdlets für AppLocker aktualisiert werden.|
|Richtlinienanwendung|SRP-Richtlinien werden über eine Gruppenrichtlinie verteilt.|AppLocker-Richtlinien werden über eine Gruppenrichtlinie verteilt.|
|Erzwingungsmodus|SRP funktioniert im "Ablehnungs Listenmodus", in dem Administratoren Regeln für Dateien erstellen können, die in diesem Unternehmen nicht zulässig sind, während der Rest der Datei standardmäßig ausgeführt werden darf.<p>SRP kann auch im Zulassungs Listenmodus so konfiguriert werden, dass standardmäßig alle Dateien gesperrt sind und Administratoren Zulassungsregeln für Dateien erstellen müssen, die Sie zulassen möchten.|AppLocker funktioniert standardmäßig im Zulassungs Listenmodus, in dem nur die Dateien ausgeführt werden können, für die eine entsprechende Zulassungs Regel vorhanden ist.|
|Steuerbare Dateitypen|SRP kann die folgenden Dateitypen steuern:<p>-Ausführbare Dateien<br />-DLLs<br />-Skripts<br />-Windows-Installationsprogramme<p>SRP kann nicht jeden Dateityp separat steuern. Alle SRP-Regeln sind in einer zentralen Regelsammlung enthalten.|AppLocker kann folgende Dateitypen steuern:<p>-Ausführbare Dateien<br />-DLLs<br />-Skripts<br />-Windows-Installationsprogramme<br />-Gepackte apps und Installationsprogramme (Windows Server 2012 und Windows 8)<p>AppLocker verwaltet für alle fünf Dateitypen eine separate Regelsammlung.|
|Designierte Dateitypen|SRP unterstützt eine erweiterbare Liste von Dateitypen, die als ausführbar gelten. Administratoren können Erweiterungen für Dateien hinzufügen, die als ausführbar gelten sollten.|Dies wird durch AppLocker nicht unterstützt. AppLocker unterstützt derzeit die folgenden Dateierweiterungen:<p>-Ausführbare Dateien (. exe,. com)<br />-DLLs (". ocx", ". dll")<br />-Scripts (. VSB,. js,. ps1,. cmd,. bat)<br />-Windows-Installationsprogramme (. msi,. MST,. msp)<br />-App-Pakete mit Paketen (. AppX)|
|Regeltypen|SRP unterstützt vier Regeltypen:<p>-Hash<br />-Path<br />-Signatur<br />-Internet Zone|AppLocker unterstützt drei Regeltypen:<p>-Hash<br />-Path<br />-Publisher|
|Bearbeiten des Hashwerts|Mit SRP können Administratoren benutzerdefinierte Hashwerte bereitstellen.|AppLocker berechnet den Hashwert selbst. Intern wird der SHA1-Authenticode-Hash für portable ausführbare Dateien (exe und dll) und Windows Installer und ein SHA1-Flatfile-Hash für den Rest verwendet.|
|Unterstützung für verschiedene Sicherheitsstufen|Mit SRP können Administratoren die Berechtigungen angeben, mit denen eine app ausgeführt werden kann. Daher kann ein Administrator eine Regel so konfigurieren, dass Editor immer mit eingeschränkten Berechtigungen und nie mit Administratorrechten ausgeführt wird.<p>Unter Windows Vista und früheren Versionen hat SRP mehrere Sicherheitsstufen unterstützt. Unter Windows 7 wurde diese Liste auf zwei Ebenen beschränkt: unzulässig und uneingeschränkt (der grundlegende Benutzer wird in unzulässig übersetzt).|AppLocker unterstützt keine Sicherheitsstufen.|
|Verwalten von App-Paketen und Installer für App-Pakete|Nicht möglich|APPX ist ein gültiger Dateityp, den AppLocker verwalten kann.|
|Ausrichten einer Regel auf einen Benutzer bzw. eine Benutzergruppe|SRP-Regeln gelten für alle Benutzer auf einem bestimmten Computer.|AppLocker-Regeln können auf einen bestimmten Benutzer bzw. eine Benutzergruppe ausgerichtet werden.|
|Unterstützung für Regelausnahmen|SRP unterstützt keine Regelausnahmen.|AppLocker-Regeln können Ausnahmen aufweisen, die es Administratoren ermöglichen, Regeln wie "alles von Windows zulassen außer regedit. exe" zu erstellen.|
|Unterstützung für Überwachungsmodus|SRP unterstützt den Überwachungsmodus nicht. Die einzige Möglichkeit zum Testen von SRP-Richtlinien ist das Einrichten einer Testumgebung und das Durchführen einiger Experimente.|AppLocker unterstützt den Überwachungsmodus. Dies ermöglicht Administratoren das Testen der Auswirkung der Richtlinie in der echten Produktionsumgebung ohne die Benutzerfreundlichkeit zu beeinträchtigen. Sobald Sie mit den Ergebnissen zufrieden sind, können Sie mit dem Erzwingen der Richtlinie beginnen.|
|Unterstützung für den Export und Import von Richtlinien|SRP unterstützt keinen Import/Export von Richtlinien.|AppLocker unterstützt das Importieren und Exportieren von Richtlinien. Dies ermöglicht Ihnen das Erstellen einer AppLocker-Richtlinie auf einem Beispielcomputer, das Testen der Richtlinie sowie das anschließende Exportieren und erneute Importieren in das gewünschte GPO.|
|Regelerzwingung|Intern erfolgt die Erzwingung von SRP-Regeln im weniger sicheren Benutzermodus.|Intern werden AppLocker-Regeln für exe-Dateien und DLLs im Kernel Modus erzwungen, der sicherer ist als das erzwingen im Benutzermodus.|

## <a name="system-requirements"></a>Systemanforderungen
Software Einschränkungs Richtlinien können nur auf Computern konfiguriert werden, auf denen mindestens Windows Server 2003 und mindestens Windows XP ausgeführt werden. Gruppenrichtlinie ist erforderlich, um Gruppenrichtlinie Objekte zu verteilen, die Software Einschränkungs Richtlinien enthalten.

## <a name="software-restriction-policies-components-and-architecture"></a>Komponenten und Architektur von Software Einschränkungs Richtlinien
Software Einschränkungs Richtlinien bieten einen Mechanismus für das Betriebssystem und Anwendungen, die mit Software Einschränkungs Richtlinien kompatibel sind, um die Lauf Zeit Ausführung von Softwareprogrammen einzuschränken.

Auf hoher Ebene bestehen Richtlinien für Software Einschränkung aus den folgenden Komponenten:

-   API für Software Einschränkungs Richtlinien. Die Anwendungs Programmierschnittstellen (Application Programming Interfaces, APIs) werden zum Erstellen und Konfigurieren der Regeln verwendet, die die Software Einschränkungs Richtlinie bilden. Es gibt auch APIs für Richtlinien für Software Einschränkung zum Abfragen, verarbeiten und Erzwingen von Software Einschränkungs Richtlinien.

-   Ein Verwaltungs Tool für Software Einschränkungs Richtlinien. Dies umfasst die **Software Einschränkungs Richtlinien** Erweiterung des **lokalen Gruppenrichtlinienobjekt-Editor** -Snap-Ins, die Administratoren verwenden, um die Richtlinien für Software Einschränkung zu erstellen und zu bearbeiten.

-   Eine Reihe von Betriebssystem-APIs und-Anwendungen, die die Richtlinien für Software Einschränkungs Richtlinien aufzurufen, um die Richtlinien zur Software Einschränkung zur Laufzeit zu erzwingen.

-   Active Directory und Gruppenrichtlinie. Software Einschränkungs Richtlinien hängen von der Gruppenrichtlinie-Infrastruktur ab, um die Richtlinien für Software Einschränkung vom Active Directory an die entsprechenden Clients weiterzuleiten, und zum einschränken und Filtern der Anwendung dieser Richtlinien auf die geeignete Zielcomputer.

-   Authenticode-und winverify-Vertrauensstellungs-APIs, die zum Verarbeiten signierter ausführbarer Dateien verwendet werden

-   Ereignisanzeige. Die von Software Einschränkungs Richtlinien verwendeten Funktionen protokollieren Ereignisse in den Ereignisanzeige Protokollen.

-   Richtlinien Ergebnissatz (RSoP), der bei der Diagnose der effektiven Richtlinie helfen kann, die auf einen Client angewendet wird.

Weitere Informationen zur SRP-Architektur und zur Verwaltung von Regeln, Prozessen und Interaktionen durch SRP finden Sie unter [Funktionsweise von Software Einschränkungs Richtlinien](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx) in der technischen Bibliothek für Windows Server 2003.

## <a name="best-practices"></a><a name="BKMK_Best_Practices"></a>Bewährte Methoden

### <a name="do-not-modify-the-default-domain-policy"></a>Ändern Sie nicht die Standard Domänen Richtlinie.

-   Wenn Sie die Standard Domänen Richtlinie nicht bearbeiten, haben Sie immer die Möglichkeit, die Standard Domänen Richtlinie erneut anzuwenden, wenn bei Ihrer benutzerdefinierten Domänen Richtlinie etwas schief geht.

### <a name="create-a-separate-group-policy-object-for-software-restriction-policies"></a>Erstellen Sie ein separates Gruppenrichtlinie Objekt für Richtlinien für Software Einschränkung.

-   Wenn Sie ein separates Gruppenrichtlinie Objekt (GPO) für Richtlinien für Software Einschränkung erstellen, können Sie Richtlinien für Software Einschränkung in einem Notfall deaktivieren, ohne den Rest der Domänen Richtlinie zu deaktivieren.

### <a name="if-you-experience-problems-with-applied-policy-settings-restart-windows-in-safe-mode"></a>Wenn Probleme mit den angewendeten Richtlinien Einstellungen auftreten, starten Sie Windows im abgesicherten Modus neu.

-   Richtlinien für Software Einschränkung gelten nicht, wenn Windows im abgesicherten Modus gestartet wird. Wenn Sie versehentlich eine Arbeitsstation mit Software Einschränkungs Richtlinien sperren, starten Sie den Computer im abgesicherten Modus neu, melden Sie sich als lokaler Administrator an, ändern Sie die Richtlinie, führen Sie **gpupdate**aus, starten Sie den Computer neu, und melden Sie sich dann normal an.

### <a name="use-caution-when-defining-a-default-setting-of-disallowed"></a>Gehen Sie vorsichtig vor, wenn Sie die Standardeinstellung nicht zulässig definieren.

-   Wenn Sie die Standardeinstellung nicht **zulässig**definieren, ist die gesamte Software nicht zulässig, mit Ausnahme der explizit zugelassenen Software. Jede Datei, die Sie öffnen möchten, muss über eine Regel für Software Einschränkungs Richtlinien verfügen, die das Öffnen ermöglicht.

-   Wenn die Standard Sicherheitsstufe auf unzulässig festgelegt ist, werden automatisch vier Registrierungs Pfad Regeln erstellt, um Administratoren vor dem Sperren des **Systems zu schützen**. Diese Registrierungs Pfad Regeln können gelöscht oder geändert werden. Dies wird jedoch nicht empfohlen.

### <a name="for-best-security-use-access-control-lists-in-conjunction-with-software-restriction-policies"></a>Verwenden Sie zur optimalen Sicherheit Zugriffs Steuerungs Listen in Verbindung mit Richtlinien für Software Einschränkung.

-   Benutzer versuchen möglicherweise, Richtlinien für Software Einschränkung zu umgehen, indem Sie unzulässige Dateien umbenennen oder verschieben oder nicht beschränkte Dateien überschreiben. Daher wird empfohlen, Zugriffs Steuerungs Listen (ACLs) zu verwenden, um Benutzern den Zugriff zu verweigern, der zum Ausführen dieser Aufgaben erforderlich ist.

### <a name="test-new-policy-settings-thoroughly-in-test-environments-before-applying-the-policy-settings-to-your-domain"></a>Testen Sie neue Richtlinien Einstellungen in Testumgebungen gründlich, bevor Sie die Richtlinien Einstellungen auf Ihre Domäne anwenden.

-   Neue Richtlinien Einstellungen können anders agieren als ursprünglich erwartet. Das Testen verringert die Wahrscheinlichkeit, dass ein Problem auftritt, wenn Sie Richtlinien Einstellungen in Ihrem Netzwerk bereitstellen.

-   Sie können eine Test Domäne unabhängig von der Domäne Ihrer Organisation einrichten, in der neue Richtlinien Einstellungen getestet werden sollen. Sie können die Richtlinien Einstellungen auch testen, indem Sie ein Test-GPO erstellen und es mit einer Test Organisationseinheit verknüpfen. Wenn Sie die Richtlinien Einstellungen mit Test Benutzern gründlich getestet haben, können Sie das Test-GPO mit Ihrer Domäne verknüpfen.

-   Legen Sie keine Programme oder Dateien als nicht **zulässig** fest, ohne zu testen, um zu sehen, was der Effekt sein kann. Einschränkungen für bestimmte Dateien können den Betrieb Ihres Computers oder Netzwerks erheblich beeinträchtigen.

-   Informationen, die falsch eingegeben werden oder Fehler eingeben, können zu einer Richtlinien Einstellung führen, die nicht wie erwartet ausgeführt wird. Wenn Sie neue Richtlinien Einstellungen vor der Anwendung testen, kann dies zu unerwartetem Verhalten werden.

### <a name="filter-user-policy-settings-based-on-membership-in-security-groups"></a>Filtern Sie die Benutzerrichtlinien Einstellungen basierend auf der Mitgliedschaft in Sicherheitsgruppen.

-   Sie können Benutzer oder Gruppen angeben, für die keine Richtlinien Einstellung angewendet werden soll, indem Sie die Kontrollkästchen **anwenden Gruppenrichtlinie** und **Lesen** aktivieren, die sich auf der Registerkarte **Sicherheit** des Dialog Felds Eigenschaften für das Gruppenrichtlinien Objekt befinden.

-   Wenn die Berechtigung Lesen verweigert wird, wird die Richtlinien Einstellung nicht vom Computer heruntergeladen. Dadurch wird die geringere Bandbreite genutzt, indem unnötige Richtlinien Einstellungen heruntergeladen werden, wodurch das Netzwerk schneller funktionieren kann. Wenn Sie die Berechtigung Lesen verweigern möchten, aktivieren Sie das Kontrollkästchen **verweigern** für das Kontrollkästchen **Lesen** , das sich auf der Registerkarte **Sicherheit** des Dialog Felds Eigenschaften für das Gruppenrichtlinien Objekt befindet.

### <a name="do-not-link-to-a-gpo-in-another-domain-or-site"></a>Nicht mit einem Gruppenrichtlinien Objekt in einer anderen Domäne oder Website verknüpfen.

-   Das Verknüpfen mit einem Gruppenrichtlinien Objekt in einer anderen Domäne oder Website kann zu einer schlechten Leistung führen.

## <a name="additional-resources"></a>Weitere Ressourcen

|Art des Inhalts|Verweise|
|--------|-------|
|**Planung**|[Technische Referenz für Software Einschränkungs Richtlinien](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)|
|**Betrieb**|[Verwalten der Richtlinien für Softwareeinschränkung](administer-software-restriction-policies.md)|
|**Problembehandlung**|[Problembehandlung bei Richtlinien für Software Einschränkung (2003)](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)|
|**Sicherheit**|[Bedrohungen und Gegenmaßnahmen für Richtlinien für Software Einschränkung (2008)](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)<p>[Bedrohungen und Gegenmaßnahmen für Richtlinien für Software Einschränkung (2008 R2)](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)|
|**Tools und Einstellungen**|[Tools und Einstellungen für Richtlinien für Software Einschränkung (2003)](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)|
|**Communityressourcen**|[Sperren von Anwendungen mit Richtlinien für Software Einschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|


