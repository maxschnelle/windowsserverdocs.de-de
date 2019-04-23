---
title: Richtlinien zur Softwareeinschränkung (Software Restriction Policies, SRP) – Technische Übersicht
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc7013b0-0efd-40fd-bd6d-75128adbd0b8
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: d007d55ced9c6a18581eaedb4edb66db9eeccab9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830851"
---
# <a name="software-restriction-policies-technical-overview"></a>Richtlinien zur Softwareeinschränkung (Software Restriction Policies, SRP) – Technische Übersicht

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird beschrieben, Richtlinien für softwareeinschränkung, wann und wie die Funktion, welche Änderungen wurden in früheren Versionen implementiert und enthält Links zu zusätzlichen Ressourcen zum Erstellen und Bereitstellen von Richtlinien für softwareeinschränkung beginnend mit Windows Server 2008 und Windows Vista.

## <a name="introduction"></a>Einführung
Richtlinien für softwareeinschränkung bieten Administratoren eine Gruppe richtlinienbestimmten Mechanismus zum Identifizieren von Software und steuern die Möglichkeit, auf dem lokalen Computer auszuführen. Diese Richtlinien können verwendet werden, auf Computern unter Microsoft Windows-Betriebssystemen (beginnend mit Windows Server 2003 und Windows XP Professional) für bekannte Konflikte zu schützen und die Computer vor sicherheitsbedrohungen schädlichen Viren zu schützen und Trojanische Pferde. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, mit der Sie ausschließlich die Ausführung explizit ausgewiesene Anwendungen zulassen. Richtlinien für Softwareeinschränkung sind mit Microsoft Active Directory und Gruppenrichtlinien verknüpft. Sie können Richtlinien für Softwareeinschränkung auch auf eigenständigen Computern erstellen.

Richtlinien für Softwareeinschränkung sind Vertrauensrichtlinien. Hierbei handelt es sich um von einem Administrator festgelegte Vorschriften, um die Ausführung von Skripts und anderem Code zu beschränken, der als nicht als absolut vertrauenswürdig erachtet wird. Die Richtlinien für Softwareeinschränkung-Erweiterung auf den Editor für lokale Gruppenrichtlinien bietet eine zentrale Benutzeroberfläche, die über der die Einstellungen für das Einschränken der Verwendung von Anwendungen verwaltet werden können, auf dem lokalen Computer oder in einer Domäne.

## <a name="procedures"></a>Verfahren

-   [Verwalten von Richtlinien für Softwareeinschränkung](administer-software-restriction-policies.md)

    -   [Ermitteln von zulassen bzw. verweigern-Liste und des Anwendungsinventars für Richtlinien für Softwareeinschränkung](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

    -   [Arbeiten Sie mit Richtlinien für die Softwareeinschränkungsregeln](work-with-software-restriction-policies-rules.md)

    -   [Verwenden von Richtlinien für Softwareeinschränkungen zum Schutz Ihres Computers vor einem e-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

-   [Problembehandlung bei Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md)

## <a name="software-restriction-policy-usage-scenarios"></a>Softwarebenutzungsszenarien für Einschränkung-Richtlinie
Geschäftsbenutzer zusammenarbeiten mithilfe von E-mail, instant messaging und Peer-zu-Peer-Anwendungen. Diesen zusammenarbeitselementen erhöhen, insbesondere bei der Nutzung des Internets Business zu berechnen, also auch die Bedrohungen durch Schadsoftware, z. B. Würmer, Viren, und böswillige Benutzer oder Angreifer Bedrohungen.

Benutzer empfangen möglicherweise schädlichen Code in vielen Formen, die von native ausführbare Windows-Dateien (.exe-Dateien), bis hin zu Makros in Dokumenten (z. B. doc-Dateien), Skripts (z. B. vbs-Dateien). Böswillige Benutzer oder Angreifer verwenden häufig Social-Engineering-Methoden, um Benutzern die Ausführung von Code mit Viren und Würmer zu erhalten. (Social-Engineering ist ein Begriff für Konten von Personen zu offenbaren, ihr Kennwort oder eine Form der Sicherheitsinformationen.) Wenn dieser Code aktiviert ist, können sie Denial-of-Service-Angriffe auf das Netzwerk zu generieren, oder private Daten mit dem Internet zu senden, gefährden die Sicherheit des Computers oder den Inhalt der Festplatte beschädigen.

IT-Organisationen und Benutzer müssen sein können, um zu bestimmen, welche Software sicher ausgeführt werden kann und welche nicht. Mit der eine große Anzahl und die Formulare, die bösartigen Code ausführen können, ist dies eine schwierige Aufgabe.

Um ihre Netzwerkcomputer von gefährlicher Code und unbekannten oder nicht unterstützten Software zu schützen, können Unternehmen Richtlinien für softwareeinschränkung als Teil ihrer gesamten Sicherheitsstrategie implementieren.

Administratoren können Richtlinien für Softwareeinschränkung für die folgenden Aufgaben verwenden:

-   Definieren, was als vertrauenswürdiger Code gilt.

-   Entwerfen einer flexiblen Gruppenrichtlinie zum Regulieren von Skripts, ausführbaren Dateien und ActiveX-Steuerelementen.

Richtlinien für Softwareeinschränkung werden durch das Betriebssystem und von Anwendungen (beispielsweise Skriptanwendungen) durchgesetzt, die Richtlinien für Softwareeinschränkungen erfüllen.

Administratoren können Richtlinien für Softwareeinschränkung insbesondere für die folgenden Zwecke verwenden:

-   Geben Sie die Software (ausführbare Dateien) auf Clientcomputern ausgeführt werden kann

-   Verhindern, dass Benutzer bestimmte Programme auf gemeinsam genutzten Computern ausführen.

-   Geben Sie, wer vertrauenswürdige Herausgeber hinzufügen kann, auf den Clientcomputern

-   Festlegen der Reichweite der Richtlinien für softwareeinschränkung (angeben, ob Richtlinien alle Benutzer auswirken oder nur eine Teilmenge von Benutzern auf den Clientcomputern)

-   Verhindern, dass ausführbare Dateien auf dem lokalen Computer, in einer Organisationseinheit, am Standort oder in der Domäne ausgeführt werden. Dies wäre in adäquat, wenn Sie Richtlinien für Softwareeinschränkung nicht verwenden, um potenziellen Problemen durch böswillige Benutzer zu begegnen.

## <a name="BKMK_Diffs_Changes"></a>Unterschiede und Änderungen an der Funktionalität
Es sind keine Änderungen an der Funktionalität in Richtlinien für Softwareeinschränkung für Windows Server 2012 und Windows 8.

**Unterstützte Versionen**

Richtlinien für Softwareeinschränkung können nur auf konfiguriert und angewendet, die auf Computern mit mindestens Windows Server 2003, einschließlich Windows Server 2012 und Windows XP enthält, einschließlich Windows 8.

> [!NOTE]
> Richtlinien für Softwareeinschränkungen keine bestimmte Versionen des Windows Client Operating System Anfangs mit Windows Vista. Computer, die nicht in einer Domäne von der Gruppenrichtlinie verwaltet wird möglicherweise nicht verteilte Richtlinien.

**Vergleichen von anwendungssteuerungsfunktionen in Richtlinien für Softwareeinschränkung und AppLocker**

In der folgenden Tabelle werden die Features und Funktionen von AppLocker und den Richtlinien für Softwareeinschränkung verglichen.

|Anwendungssteuerungsfunktion|Softwareeinschränkungsrichtlinien|AppLocker|
|----------------|----|-------|
|Bereich|Richtlinien für Softwareeinschränkung können auf allen Windows-Betriebssystemen ab Windows XP und Windows Server 2003 angewendet werden.|AppLocker-Richtlinien gelten nur für Windows Server 2008 R2, Windows Server 2012, Windows 7 und Windows 8.|
|Richtlinienerstellung|SRP-Richtlinien werden mithilfe von Gruppenrichtlinien verwaltet, und nur der Administrator des GPO kann die SRP-Richtlinie aktualisieren. Der Administrator auf dem lokalen Computer kann die im lokalen GPO definierten SRP-Richtlinien ändern.|AppLocker-Richtlinien werden mithilfe von Gruppenrichtlinien verwaltet, und nur der Administrator des GPO kann die Richtlinie aktualisieren. Der Administrator auf dem lokalen Computer kann die im lokalen GPO definierten AppLocker-Richtlinien ändern.<br /><br />Mit AppLocker können Fehlermeldungen so angepasst werden, dass Benutzer auf eine Webseite für Hilfe verwiesen werden.|
|Richtlinienwartung|SRP-Richtlinien müssen mithilfe des Snap-Ins „Lokale Sicherheitsrichtlinie“ (bei lokal erstellten Richtlinien) oder der Gruppenrichtlinien-Verwaltungskonsole (GPMC) aktualisiert werden.|AppLocker-Richtlinien können mithilfe des Snap-Ins „Lokale Sicherheitsrichtlinie“ (bei lokal erstellten Richtlinien), der GPMC oder den Windows PowerShell-Cmdlets für AppLocker aktualisiert werden.|
|Richtlinienanwendung|SRP-Richtlinien werden über eine Gruppenrichtlinie verteilt.|AppLocker-Richtlinien werden über eine Gruppenrichtlinie verteilt.|
|Erzwingungsmodus|Richtlinien für Softwareeinschränkung funktioniert in der "deny Listenmodus", in dem Administratoren Regeln für Dateien erstellen können, die sie nicht möchten, um in dieser Organisation zu ermöglichen, während der Rest der Datei ausgeführt werden dürfen in der Standardeinstellung.<br /><br />Richtlinien für Softwareeinschränkung kann auch in die "Listenmodus zulassen" konfiguriert werden, die in der Standardeinstellung werden alle Dateien blockiert, und Administratoren müssen erstellen Zulassungsregeln für Dateien, die sie zulassen möchten.|AppLocker standardmäßig funktioniert in die "Listenmodus zulassen", in dem nur die Dateien ausführen, für die es wird ein entsprechender Zulassungsregel zulässig sind.|
|Steuerbare Dateitypen|SRP kann die folgenden Dateitypen steuern:<br /><br />: Ausführbare Dateien<br />-Dlls<br />-Skripts<br />-Windows Installationsprogramme<br /><br />SRP kann nicht jeden Dateityp separat steuern. Alle SRP-Regeln sind in einer zentralen Regelsammlung enthalten.|AppLocker kann folgende Dateitypen steuern:<br /><br />: Ausführbare Dateien<br />-Dlls<br />-Skripts<br />-Windows Installationsprogramme<br />-Paket-apps und -Installer (Windows Server 2012 und Windows 8)<br /><br />AppLocker verwaltet für alle fünf Dateitypen eine separate Regelsammlung.|
|Designierte Dateitypen|SRP unterstützt eine erweiterbare Liste von Dateitypen, die als ausführbar gelten. Administratoren können Erweiterungen für Dateien hinzufügen, die als ausführbar gelten sollten.|Dies wird durch AppLocker nicht unterstützt. AppLocker unterstützt derzeit die folgenden Dateierweiterungen:<br /><br />-Ausführbare Dateien (".exe", ".com")<br />-Dlls (".ocx", ".dll")<br />-Skripts (vbs, js,. ps1, .cmd,. bat)<br />-Windows Installer (.msi, .mst, .msp)<br />-Installer für app-Installer (.appx)|
|Regeltypen|SRP unterstützt vier Regeltypen:<br /><br />-Hash<br />-Path<br />-Signatur<br />-Der Internetzone|AppLocker unterstützt drei Regeltypen:<br /><br />-Hash<br />-Path<br />-Verleger|
|Bearbeiten des Hashwerts|Richtlinien für Softwareeinschränkung können Administratoren benutzerdefinierte Hashwerte bereitgestellt.|AppLocker berechnet den Hashwert selbst. Intern wird den SHA1-Authenticode-Hash für portierbare ausführbare Dateien (exe- und Dll) und Windows Installer und ein SHA1-Flatfile-Hash für den Rest.|
|Unterstützung für verschiedene Sicherheitsstufen|Mit Richtlinien für Softwareeinschränkung können Administratoren die Berechtigungen angeben, mit denen eine app ausgeführt werden kann. Daher können Administratoren eine Regel konfigurieren, Editor mit eingeschränkten Berechtigungen und nicht mit Administratorrechten immer ausgeführt wird.<br /><br />Unter Windows Vista und früheren Versionen hat SRP mehrere Sicherheitsstufen unterstützt. Unter Windows 7 wurde die Liste auf nur zwei Ebenen beschränkt: Nicht zulässig und uneingeschränkten (Standardbenutzer übersetzt nicht erlaubt).|AppLocker unterstützt keine Sicherheitsstufen.|
|Verwalten von App-Pakete und Installer für app-Pakete|Nicht möglich|APPX ist ein gültiger Dateityp, den AppLocker verwalten kann.|
|Ausrichten einer Regel auf einen Benutzer bzw. eine Benutzergruppe|SRP-Regeln gelten für alle Benutzer auf einem bestimmten Computer.|AppLocker-Regeln können auf einen bestimmten Benutzer bzw. eine Benutzergruppe ausgerichtet werden.|
|Unterstützung für Regelausnahmen|SRP unterstützt keine Regelausnahmen.|AppLocker-Regeln können Ausnahmen verfügen über die Administratoren zum Erstellen von Regeln, z. B. "Können alle von Windows mit Ausnahme von Regedit.exe" zu ermöglichen.|
|Unterstützung für Überwachungsmodus|SRP unterstützt den Überwachungsmodus nicht. Die einzige Möglichkeit zum Testen von SRP-Richtlinien ist das Einrichten einer Testumgebung und das Durchführen einiger Experimente.|AppLocker unterstützt den Überwachungsmodus. Dies ermöglicht Administratoren das Testen der Auswirkung der Richtlinie in der echten Produktionsumgebung ohne die Benutzerfreundlichkeit zu beeinträchtigen. Sobald Sie mit den Ergebnissen zufrieden sind, können Sie mit dem Erzwingen der Richtlinie beginnen.|
|Unterstützung für den Export und Import von Richtlinien|SRP unterstützt keinen Import/Export von Richtlinien.|AppLocker unterstützt das Importieren und Exportieren von Richtlinien. Dies ermöglicht Ihnen das Erstellen einer AppLocker-Richtlinie auf einem Beispielcomputer, das Testen der Richtlinie sowie das anschließende Exportieren und erneute Importieren in das gewünschte GPO.|
|Regelerzwingung|Intern erfolgt die Erzwingung von SRP-Regeln im weniger sicheren Benutzermodus.|Intern werden AppLocker-Regeln für die exe- und DLL-im Kernel-Modus erzwungen, die sicherer ist als sie in den Benutzermodus erzwingen.|

## <a name="system-requirements"></a>Systemanforderungen
Richtlinien für softwareeinschränkung können nur auf konfiguriert und angewendet, die auf Computern mit mindestens Windows Server 2003 und Windows XP. Der Gruppenrichtlinie ist erforderlich, um Gruppenrichtlinienobjekte zu verteilen, die Richtlinien für softwareeinschränkung enthalten.

## <a name="software-restriction-policies-components-and-architecture"></a>Software Restriction Policies-Komponenten und Architektur
Richtlinien für softwareeinschränkung bieten einen Mechanismus für das Betriebssystem und Anwendungen, die zum Einschränken der laufzeitausführung von Softwareprogrammen kompatibel mit Richtlinien für softwareeinschränkung.

Auf einer hohen Ebene besteht aus Richtlinien für softwareeinschränkung die folgenden Komponenten:

-   Richtlinien für softwareeinschränkung API. Die Application Programming Interfaces (APIs) werden zum Erstellen und konfigurieren Sie die Regeln, die die Softwareeinschränkungsrichtlinie zu bilden. Es gibt Richtlinien für softwareeinschränkung-APIs für Abfragen, Verarbeitung und Erzwingen von Richtlinien für softwareeinschränkung auch.

-   Ein Software Restriction Policies-Verwaltungstool. Dies umfasst die **Richtlinien für Softwareeinschränkung** Erweiterung der **lokalen Gruppenrichtlinienobjekt-Editor** -Snap-in, die von Administratoren zum Erstellen und Bearbeiten von Richtlinien für softwareeinschränkung verwenden.

-   Eine Reihe von Betriebssystem-APIs und Anwendungen aufrufen, die die Richtlinien für softwareeinschränkung APIs zur Durchsetzung von Richtlinien für softwareeinschränkung zur Laufzeit bereitzustellen.

-   Active Directory und Gruppenrichtlinien. Richtlinien für softwareeinschränkung hängen von der Infrastruktur der Gruppenrichtlinie Richtlinien für softwareeinschränkung aus Active Directory die entsprechenden Clients und für die Bereichsdefinition und Filtern die Anwendung dieser Richtlinien in den entsprechenden weitergegeben werden. Zielcomputer.

-   Authenticode und WinVerify vertrauen APIs, die verwendet werden, um signierte ausführbare Dateien zu verarbeiten.

-   Die Ereignisanzeige. Die Funktionen, die von der Software Restriction Richtlinien Protokollereignisse in den Protokollen der Ereignisanzeige verwendet.

-   Resultierende Resultant Set of Policies (RSoP), die bei der Diagnose für die effektive Richtlinie, die an einen Client angewendet werden können.

Weitere Informationen zu SRP-Architektur, SRP-Regeln, Prozesse und-Interaktionen verwaltet werden, finden Sie unter [wie Software Restriction Policies Work](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx) in der technischen Bibliothek zu Windows Server 2003.

## <a name="BKMK_Best_Practices"></a>Bewährte Methoden

### <a name="do-not-modify-the-default-domain-policy"></a>Ändern Sie die Standardrichtlinie nicht.

-   Wenn Sie nicht die Standarddomänenrichtlinie bearbeiten, müssen Sie immer die Standarddomänenrichtlinie erneut anwenden, falls ein Problem mit Ihrer benutzerdefinierten Domänenrichtlinie auftritt.

### <a name="create-a-separate-group-policy-object-for-software-restriction-policies"></a>Erstellen Sie eine separate Richtlinien für softwareeinschränkung Gruppenrichtlinienobjekt.

-   Wenn Sie eine separate Gruppe Gruppenrichtlinienobjekt (GPO) Richtlinien für softwareeinschränkung erstellen, können Sie Richtlinien für softwareeinschränkung in einem Notfall deaktivieren, ohne den Rest Ihrer Domäne-Richtlinie zu deaktivieren.

### <a name="if-you-experience-problems-with-applied-policy-settings-restart-windows-in-safe-mode"></a>Wenn Sie Probleme mit angewendeten Richtlinieneinstellungen auftreten, starten Sie Windows im abgesicherten Modus neu.

-   Richtlinien für softwareeinschränkung gültig nicht, wenn Windows im abgesicherten Modus gestartet wird. Wenn Sie versehentlich eine Arbeitsstation mit Richtlinien für softwareeinschränkung sperren, den Computer im abgesicherten Modus neu starten, melden Sie sich als lokaler Administrator, ändern Sie die Richtlinie, führen Sie **Gpupdate**, den Computer neu starten, und melden Sie sich normal.

### <a name="use-caution-when-defining-a-default-setting-of-disallowed"></a>Verwenden Sie vorsichtig, wenn nicht erlaubt die Standardeinstellung zu definieren.

-   Wenn Sie die Standardeinstellung definieren **nicht erlaubt**, die Software ist nicht zulässig, mit Ausnahme von Software, die explizit zugelassen wird. Jede Datei, die Sie öffnen möchten muss eine Regel, Richtlinien für softwareeinschränkungen verfügen, die geöffnet werden kann.

-   Um zu verhindern, dass Administratoren sich selbst aus dem System, sperren, wenn die Standardsicherheitsstufe, um festgelegt ist **nicht erlaubt**, vier Registrierungspfadregeln werden automatisch erstellt. Sie löschen oder ändern diese Registrierungspfadregeln; Dies wird jedoch nicht empfohlen.

### <a name="for-best-security-use-access-control-lists-in-conjunction-with-software-restriction-policies"></a>Verwenden Sie Zugriffssteuerungslisten in Verbindung mit Richtlinien für softwareeinschränkung, für die optimale Sicherheit.

-   Benutzer könnten versuchen, Richtlinien für softwareeinschränkung zu umgehen, indem umbenennen oder Verschieben von Dateien mit unzulässigen oder uneingeschränkte Dateien überschrieben. Daher empfiehlt es sich, dass Sie die Zugriffssteuerungslisten (ACLs) verwenden, um Benutzern den zum Ausführen dieser Aufgaben erforderlichen Zugriff zu verweigern.

### <a name="test-new-policy-settings-thoroughly-in-test-environments-before-applying-the-policy-settings-to-your-domain"></a>Testen Sie neue Richtlinieneinstellungen für die gründlich in testumgebungen vor dem Anwenden der Richtlinieneinstellungen mit der Domäne.

-   Neue Richtlinieneinstellungen möglicherweise anders, als ursprünglich erwartet fungieren. Testen von verringert die Wahrscheinlichkeit, dass ein Problem auftreten, wenn Sie Einstellungen in Ihrem Netzwerk bereitstellen.

-   Sie können eine Testdomäne, die getrennt von der Internetdomäne Ihrer Organisation, in dem neue Richtlinieneinstellungen testen einrichten. Sie können auch die Richtlinieneinstellungen testen, erstellen einen Test GPO und Verknüpfung mit einer Testorganisationseinheit. Wenn Sie die Richtlinieneinstellungen mit Benutzern von Webleistungstests gründlich getestet haben, können Sie den Test-GPO mit Ihrer Domäne verknüpfen.

-   Stellen Sie keine Programme oder Dateien **nicht erlaubt** ohne dies zu testen, um festzustellen, was die Auswirkungen werden kann. Einschränkungen für bestimmte Dateien können den Vorgang von Ihrem Computer oder Netzwerk erheblich beeinträchtigen.

-   Informationen, die falsch eingegeben oder Eingeben von Fehlern kann zu einer richtlinieneinstellung führen, die nicht wie erwartet ausgeführt wird. Neue Richtlinieneinstellungen für die testen, bevor Sie diese anwenden, kann unerwartetes Verhalten verhindern.

### <a name="filter-user-policy-settings-based-on-membership-in-security-groups"></a>Benutzerrichtlinieneinstellungen basierend auf der Mitgliedschaft in Sicherheitsgruppen zu filtern.

-   Sie können angeben, Benutzer oder Gruppen, die für die Sie keine richtlinieneinstellung für die anzuwendende durch deaktivieren möchten der **Gruppenrichtlinie übernehmen** und **lesen** Kontrollkästchen, die sich auf befinden die **Sicherheit**Registerkarte im Dialogfeld "Eigenschaften" für das Gruppenrichtlinienobjekt.

-   Wenn die Leseberechtigung verweigert wird, wird die richtlinieneinstellung nicht durch den Computer heruntergeladen. Daher wird weniger Bandbreite verbraucht durch Herunterladen der Richtlinieneinstellungen ist nicht erforderlich, wodurch im Netzwerk schneller ausgeführt. Um die Read-Berechtigung zu verweigern, wählen Sie **Verweigern** für die **lesen** Kontrollkästchen auf der **Sicherheit** Registerkarte im Dialogfeld "Eigenschaften" für das Gruppenrichtlinienobjekt.

### <a name="do-not-link-to-a-gpo-in-another-domain-or-site"></a>Verknüpfen Sie nicht an einem GPO in einer anderen Domäne oder dem Standort.

-   Verknüpfen mit einem Gruppenrichtlinienobjekt in einer anderen Domäne oder dem Standort kann zu Leistungseinbußen führen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

|Inhaltstyp|Verweise|
|--------|-------|
|**Planung**|[Richtlinien zur Softwareeinschränkung technische Referenz](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)|
|**Betrieb**|[Verwalten von Richtlinien für Softwareeinschränkung](administer-software-restriction-policies.md)|
|**Problembehandlung**|[Richtlinien für Softwareeinschränkung Problembehandlung (2003)](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)|
|**Sicherheit**|[Bedrohungen und Gegenmaßnahmen für Softwareeinschränkungsrichtlinien Richtlinien (2008)](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)<br /><br />[Bedrohungen und Gegenmaßnahmen für Softwareeinschränkungsrichtlinien Richtlinien (2008 R2)](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)|
|**Tools und Einstellungen**|[Richtlinien für Softwareeinschränkung – Tools und Einstellungen (2003)](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)|
|**Communityressourcen**|[Die Sperrung von Anwendungen mit Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|


