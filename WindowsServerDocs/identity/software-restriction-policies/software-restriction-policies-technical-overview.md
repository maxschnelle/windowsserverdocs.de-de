---
title: Software Restriction Policies Technical Overview
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="software-restriction-policies-technical-overview"></a>Software Restriction Policies Technical Overview

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema werden die Richtlinien für Softwareeinschränkung, wann und wie Sie die Funktion verwenden, welche Änderungen wurden in früheren Versionen implementiert und enthält Links zu weiteren Ressourcen helfen Ihnen beim Erstellen und Bereitstellen von Softwareeinschränkungsrichtlinien ab Windows Server2008 und Windows Vista.

## <a name="introduction"></a>Einführung in
Richtlinien für Softwareeinschränkung bieten Administratoren eine Gruppenrichtlinie gesteuert Mechanismus für die Software erkennen und Steuern der Ausführung auf dem lokalen Computer ausgeführt werden. Diese Richtlinien können zum Schutz von Computern unter Microsoft Windows-Betriebssysteme (beginnend mit Windows Server2003 und Windows XP Professional) vor bekannten Konflikten und schützen Sie den Computer vor Sicherheitsrisiken wie z.B. Viren und Trojanische Pferde verwendet werden. Sie können Richtlinien für Softwareeinschränkung auch verwenden, eine stark eingeschränkte Konfiguration für Computer zu erstellen, in dem Sie nur explizit angegebene Anwendungen ausführen können. Richtlinien für Softwareeinschränkung sind mit Microsoft Active Directory und Gruppenrichtlinien integriert. Sie können Richtlinien für Softwareeinschränkung auch auf eigenständigen Computern erstellen.

Richtlinien für Softwareeinschränkung sind Vertrauensrichtlinien, die hierbei Vorschriften durch den Administrator eingeschränkt, Skripts und anderem Code, der nicht vollständig vertrauenswürdigen ausgeführt werden. Die Erweiterung von Softwareeinschränkungsrichtlinien auf den Editor für lokale Gruppenrichtlinien bietet eine einzige Benutzeroberfläche, über die die Einstellungen für das Einschränken der Verwendung von Anwendungen verwaltet werden können, auf dem lokalen Computer oder in einer Domäne.

## <a name="procedures"></a>Verfahren

-   [Administer Software Restriction Policies](administer-software-restriction-policies.md)

    -   [Bestimmen Sie zulassen bzw. verweigern-Liste und des Anwendungsinventars für Richtlinien für Softwareeinschränkung](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

    -   [Arbeiten Sie mit Software Restriction Policies Regeln](work-with-software-restriction-policies-rules.md)

    -   [Verwenden von Richtlinien für Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

-   [Problembehandlung bei Richtlinien für Softwareeinschränkung](troubleshoot-software-restriction-policies.md)

## <a name="software-restriction-policy-usage-scenarios"></a>Software Restriction Gruppenrichtlinien-Verwendungsszenarien
Unternehmensbenutzer Zusammenarbeit mithilfe von E-Mails, instant Messaging und Peer-to-Peer-Apps. Diese Zusammenarbeit erhöhen, insbesondere bei der Nutzung des Internets in Unternehmenscomputern, also die Risiken von schädlichem Code, z.B. Würmer, Viren, und böswillige Benutzer oder Angreifer Bedrohungen möglich.

Benutzer erhalten möglicherweise schädlichen Code in vielen Formen, angefangen bei systemeigenen Windows ausführbare Dateien (.exe files), Makros in Dokumenten (z.B. doc-Dateien), Skripts (z.B. vbs-Dateien). Böswillige Benutzer oder Angreifer verwenden häufig Social-Engineering-Methoden, um Benutzern das Ausführen von Code mit Viren und Würmer abzurufen. (Social-Engineering ist eine Personen hereinzulegen, damit ihr Kennwort oder andere Sicherheitsinformationen verwendeter Begriff.) Wenn diese Art von Code aktiviert ist, kann Denial-of-Service-Angriffe auf das Netzwerk zu generieren, vertrauliche oder private Daten an das Internet senden, die Sicherheit des Computers gefährden oder den Inhalt der Festplatte beschädigen.

IT-Organisationen und Benutzer müssen möglicherweise ermitteln, welche Software ausgeführt werden kann und welche nicht. Die große Anzahl und Formen, die schädlichen Code ausführen können, wird dies eine schwierige Aufgabe.

Organisationen können von Softwareeinschränkungsrichtlinien als Teil ihrer gesamten Sicherheitsstrategie implementieren, um den Computern vor schädlichen Code und unbekannte oder nicht unterstützte Software zu schützen.

Administratoren können Richtlinien für Softwareeinschränkung für die folgenden Aufgaben:

-   Definieren Sie, was als vertrauenswürdiger Code gilt

-   Entwerfen einer flexiblen Gruppenrichtlinie zum Regulieren von Skripts, ausführbaren Dateien und ActiveX-Steuerelemente

Richtlinien für Softwareeinschränkung werden erzwungen, indem Sie das Betriebssystem und Anwendungen (beispielsweise skriptanwendungen), die Einhaltung der Richtlinien für Softwareeinschränkung.

Insbesondere können Administratoren Richtlinien für Softwareeinschränkung für folgende Zwecke:

-   Geben Sie an, welche Software (ausführbare Dateien) auf Clientcomputern ausgeführt werden können

-   Verhindern Sie, dass Benutzer bestimmte Programme auf gemeinsam genutzten Computern ausführen.

-   Geben Sie an, wer vertrauenswürdige Herausgeber hinzufügen kann, auf Clientcomputern

-   Legen Sie den Umfang der Softwareeinschränkungsrichtlinien (angeben, ob Richtlinien alle Benutzer auswirken oder eine Teilmenge der Benutzer auf Clientcomputern)

-   Verhindern Sie, dass ausführbare Dateien, die auf dem lokalen Computer, Organisationseinheit (OU), Standort oder Domäne ausgeführt werden. Dies wäre in adäquat, wenn Sie nicht von Softwareeinschränkungsrichtlinien zu potenziellen Problemen durch böswillige Benutzer verwenden.

## <a name="BKMK_Diffs_Changes"></a>Unterschiede und Änderungen an der Funktionalität
Es gibt keine Änderungen an der Funktionalität in SRP für Windows Server2012 und Windows8.

**Unterstützte Versionen**

Softwareeinschränkungsrichtlinien können nur auf konfiguriert und angewendet, die auf Computern, auf denen mindestens Windows Server2003, Windows Server2012, einschließlich und mindestens Windows XP, einschließlich Windows8.

> [!NOTE]
> Softwareeinschränkungsrichtlinien keinen bestimmten Editionen von der Windows Client-Betriebssystem ab Windows Vista. Computer, die nicht in einer Domäne von der Gruppenrichtlinie verwaltet wird möglicherweise nicht verteilte Richtlinien empfangen.

**Vergleichen von anwendungssteuerungsfunktionen in Richtlinien für Softwareeinschränkung und AppLocker**

In der folgende Tabelle werden die Features und Funktionen des Feature (Software Restriction Policies, SRP) und AppLocker verglichen.

|Anwendungssteuerungsfunktion|SRP|AppLocker|
|----------------|----|-------|
|Bereich|SRP-Richtlinien können auf allen Windows-Betriebssystemen ab Windows XP und Windows Server2003 angewendet werden.|AppLocker-Richtlinien gelten nur für Windows Server2008 R2, Windows Server2012, Windows7 und Windows8.|
|Erstellen von Richtlinien|SRP-Richtlinien werden mithilfe von Gruppenrichtlinien verwaltet, und nur der Administrator des GPO kann die SRP-Richtlinie aktualisieren. Der Administrator auf dem lokalen Computer kann die im lokalen GPO definierten SRP-Richtlinien ändern.|AppLocker-Richtlinien werden mithilfe von Gruppenrichtlinien verwaltet, und nur der Administrator des GPO kann die Richtlinie aktualisieren. Der Administrator auf dem lokalen Computer kann die im lokalen GPO definierten AppLocker-Richtlinien ändern.<br /><br />Mit AppLocker können Fehlermeldungen, um Benutzer auf eine Webseite für Hilfe verweisen.|
|Verwalten der Richtlinie|SRP-Richtlinien müssen aktualisiert werden, indem Sie das Snap-In lokale Sicherheitsrichtlinie (wenn es sich bei lokal erstellten Richtlinien) oder der Gruppenrichtlinien-Verwaltungskonsole (GPMC).|AppLocker-Richtlinien können über das lokale Sicherheitsrichtlinie Snap-In (wenn es sich bei lokal erstellten Richtlinien), oder der Gruppenrichtlinien-Verwaltungskonsole oder der Windows PowerShell AppLocker-Cmdlets aktualisiert werden.|
|Die Anwendung von Richtlinien|SRP-Richtlinien werden über eine Gruppenrichtlinie verteilt.|AppLocker-Richtlinien werden über eine Gruppenrichtlinie verteilt.|
|Erzwingungsmodus|SRP funktioniert in der "Verweigerungslistenmodus", in dem Administratoren Regeln für Dateien, die sie nicht möchten, um in diesem Unternehmen zu ermöglichen, während die übrigen Dateien ausgeführt werden dürfen standardmäßig erstellen können.<br /><br />SRP kann auch in der "Zulassungslistenmodus" konfiguriert werden, dass die standardmäßig alle Dateien blockiert werden und müssen Administratoren erstellen können Sie Regeln für Dateien, die sie zulassen möchten.|AppLocker standardmäßig funktioniert in den "Zulassungslistenmodus", in dem von nur die Dateien für die es ist einer entsprechenden Zulassungsregel ausgeführt werden dürfen.|
|Dateitypen, die gesteuert werden können|SRP kann die folgenden Dateitypen steuern:<br /><br />-Ausführbare Dateien<br />-DLLs<br />-Skripts<br />-Windows Installer<br /><br />SRP kann nicht jeden Dateityp separat steuern. Alle SRP-Regeln sind in einer zentralen Regelsammlung enthalten.|AppLocker kann folgende Dateitypen steuern:<br /><br />-Ausführbare Dateien<br />-DLLs<br />-Skripts<br />-Windows Installer<br />-Regeln für Paket-Apps und -Installer (Windows Server2012 und Windows8)<br /><br />AppLocker verwaltet eine separate Regelsammlung, für jede der fünf Dateitypen.|
|Designierte Dateitypen|SRP unterstützt eine erweiterbare Liste von Dateitypen, die als ausführbar gelten. Administratoren können Erweiterungen für Dateien hinzufügen, die als ausführbar gelten sollten.|AppLocker wird dies nicht unterstützt. AppLocker unterstützt derzeit die folgenden Dateierweiterungen:<br /><br />-Ausführbare Dateien (.exe, .com)<br />-DLLs (.ocx, DLL-Datei)<br />-Skripts (.vbs, js, ps1, .cmd,. bat)<br />-Windows Installer (.msi, .mst, .msp)<br />-App-Paket-Installer (.appx)|
|Typen von Regeln|SRP unterstützt vier Regeltypen:<br /><br />-Hash<br />-Pfad<br />-Signatur<br />-Internetzone|AppLocker unterstützt drei Regeltypen:<br /><br />-Hash<br />-Pfad<br />-Herausgeber|
|Bearbeiten des Hashwerts|Mit SRP können Administratoren benutzerdefinierte Hashwerte bereitgestellt.|AppLocker berechnet den Hashwert selbst. Intern verwendet den SHA1-Authenticode-Hash für portierbare ausführbare Dateien (exe- und DLL-Datei) sowie Windows Installer und SHA1-Flatfile-Hash für den Rest.|
|Unterstützung für verschiedene Sicherheitsstufen|Mit SRP können Administratoren die Berechtigungen angeben, mit denen eine App ausgeführt werden kann. Der Administrator kann daher eine Regel konfigurieren, dass Editor immer ausgeführt wird, mit eingeschränkten Berechtigungen und nie mit Administratorrechten.<br /><br />SRP unter Windows Vista und früheren Versionen unterstützt mehrere Sicherheitsstufen. Unter Windows7 wurde diese Liste auf nur zwei Stufen beschränkt: "nicht erlaubt" und uneingeschränkten (Standardbenutzer nicht erlaubt).|AppLocker unterstützt keine Sicherheitsstufen.|
|Verwalten von App-Pakete und Installer für App-Pakete|Kann nicht|AppX ist ein gültiger Dateityp, den AppLocker verwalten kann.|
|Ausrichten einer Regel auf einen Benutzer oder eine Gruppe von Benutzern|SRP-Regeln gelten für alle Benutzer auf einem bestimmten Computer.|AppLocker-Regeln können auf einen bestimmten Benutzer oder eine Gruppe von Benutzern ausgerichtet werden.|
|Unterstützung für Regelausnahmen|SRP unterstützt keine Regelausnahmen|AppLocker-Regeln können Ausnahmen aufweisen, die Administratoren zum Erstellen von Regeln wie z.B. "Können alle von Windows mit Ausnahme von Regedit.exe" zu ermöglichen.|
|Unterstützung für Überwachungsmodus|SRP unterstützt den Überwachungsmodus nicht. Die einzige Möglichkeit zum Testen von SRP-Richtlinien ist eine Testumgebung einrichten und durchführen einiger Experimente.|AppLocker unterstützt den Überwachungsmodus. Dies ermöglicht Administratoren das Testen der Auswirkung der Richtlinie in der echten Produktionsumgebung ohne die Benutzerfreundlichkeit zu beeinträchtigen. Wenn Sie mit den Ergebnissen zufrieden sind, können Sie erzwingen der Richtlinie beginnen.|
|Unterstützung für den Export und Import von Richtlinien|SRP unterstützt keine Richtlinie importieren/exportieren.|AppLocker unterstützt das Importieren und Exportieren von Richtlinien. Dies ermöglicht Ihnen das Erstellen von AppLocker-Richtlinie auf einem Beispielcomputer Testen dieser Richtlinie exportieren und Importieren in das gewünschte GPO.|
|Die Regelerzwingung|Intern erfolgt die Erzwingung von SRP-Regeln im weniger sicheren Benutzermodus.|Intern werden AppLocker-Regeln für exe- und DLL-Dateien im Kernelmodus erzwungen; dies sicherer als die Erzwingung im Benutzermodus.|

## <a name="system-requirements"></a>Systemanforderungen
Softwareeinschränkungsrichtlinien können nur auf konfiguriert und angewendet, die auf Computern, auf denen mindestens Windows Server2003 und Windows XP. Gruppenrichtlinien ist erforderlich, um Gruppenrichtlinienobjekte zu verteilen, die Richtlinien für Softwareeinschränkung enthalten.

## <a name="software-restriction-policies-components-and-architecture"></a>Software Restriction Richtlinien Komponenten und Architektur
Richtlinien für Softwareeinschränkung bieten einen Mechanismus für das Betriebssystem und Anwendungen, die für die Ausführung Runtime Softwareprogramme einschränken mit Softwareeinschränkungsrichtlinien kompatibel.

Richtlinien für Softwareeinschränkung umfassen auf hoher Ebene die folgenden Komponenten:

-   Richtlinien für Softwareeinschränkung API. Die Anwendungsprogrammierschnittstellen (APIs) dienen zum Erstellen und konfigurieren Sie die Regeln, die der Softwareeinschränkungsrichtlinien zu bilden. Außerdem stehen Softwareeinschränkungsrichtlinien APIs für Abfragen, Verarbeitung und Durchsetzung von Softwareeinschränkungsrichtlinien.

-   Ein Software Restriction Richtlinien Management-Tool. Dies umfasst die **Softwareeinschränkungsrichtlinien** Erweiterung der der **Editor für lokale Gruppenrichtlinien Objekt** -Snap-In, die von Administratoren erstellen und bearbeiten die Richtlinien für Softwareeinschränkung verwenden.

-   Eine Reihe von Betriebssystem-APIs und Anwendungen aufrufen, die die Softwareeinschränkungsrichtlinien APIs für die Durchsetzung von Softwareeinschränkungsrichtlinien zur Laufzeit bereitzustellen.

-   Active Directory und Gruppenrichtlinien. Richtlinien für Softwareeinschränkung hängen von der Gruppenrichtlinieninfrastruktur die Softwareeinschränkungsrichtlinien aus Active Directory an die entsprechenden Clients und für die Bereichsdefinition und Filtern der Anwendung dieser Richtlinien mit den entsprechenden Zielcomputern weitergegeben.

-   Authenticode und WinVerify vertrauen-APIs werden verwendet, um die signierte ausführbare Dateien verarbeiten.

-   Der Ereignisanzeige. Die Funktionen von Software Restriction Richtlinien Protokollieren von Ereignissen in die Protokolle der Ereignisanzeige verwendet.

-   Resultierende Festlegen von Richtlinien (RSoP), die hilfreich sind, die bei der Diagnose von der effektiven Richtlinie, die auf einem Client angewendet werden.

Weitere Informationen zu SRP-Architektur SRP-Regeln, Prozesse und Interaktionen verwaltet werden, finden Sie unter [Software Restriction Policies Funktionsweise](https://technet.microsoft.com/library/cc786941(v=WS.10).aspx) in der technischen Bibliothek zu Windows Server2003.

## <a name="BKMK_Best_Practices"></a>Bewährte Methoden

### <a name="do-not-modify-the-default-domain-policy"></a>Ändern Sie nicht die Standarddomänenrichtlinie.

-   Wenn Sie nicht die Standarddomänenrichtlinie bearbeiten, müssen Sie immer die Standarddomänenrichtlinie erneut anwenden, wenn ein Problem mit der angepassten Domänenrichtlinie auftritt.

### <a name="create-a-separate-group-policy-object-for-software-restriction-policies"></a>Erstellen Sie ein separates Gruppenrichtlinienobjekt für Softwareeinschränkungsrichtlinien.

-   Wenn Sie eine separate Gruppenrichtlinienobjekt (GPO) für Richtlinien für Softwareeinschränkung erstellen, können Sie Softwareeinschränkungsrichtlinien im Notfall deaktivieren, ohne den Rest der Domänenrichtlinie deaktivieren.

### <a name="if-you-experience-problems-with-applied-policy-settings-restart-windows-in-safe-mode"></a>Wenn Sie Probleme mit angewendeten Richtlinieneinstellungen haben, starten Sie Windows im abgesicherten Modus neu.

-   Richtlinien für Softwareeinschränkung werden nicht angewendet, wenn Windows im abgesicherten Modus gestartet wird. Wenn Sie versehentlich eine Arbeitsstation mit Softwareeinschränkungsrichtlinien sperren, starten Sie den Computer im abgesicherten Modus neu, melden Sie sich als lokaler Administrator, ändern Sie die Richtlinie, führen Sie **Gpupdate**, starten Sie den Computer neu, und melden Sie sich normal.

### <a name="use-caution-when-defining-a-default-setting-of-disallowed"></a>Seien Sie vorsichtig beim Definieren der Standardeinstellung nicht erlaubt.

-   Wenn Sie eine Standardeinstellung von definieren **nicht erlaubt**, die Software ist nicht zulässig, mit Ausnahme von Software, die explizit zugelassen wurde. Alle Dateien, die Sie öffnen möchten hat eine Regel, die Richtlinien Softwareeinschränkungsrichtlinien aufweisen, die sie öffnen können.

-   Um zu verhindern, dass Administratoren sich selbst aus dem System sperren, wenn die Standardsicherheitsstufe, um festgelegt ist **nicht erlaubt**, vier Registrierungspfadregeln werden automatisch erstellt. Sie können löschen oder ändern diese Registrierungspfadregeln; Dies ist jedoch nicht empfohlen.

### <a name="for-best-security-use-access-control-lists-in-conjunction-with-software-restriction-policies"></a>Verwenden Sie für optimale Sicherheit Zugriffssteuerungslisten in Verbindung mit Richtlinien für Softwareeinschränkung.

-   Benutzer können versuchen, Softwareeinschränkungsrichtlinien durch das Umbenennen oder verschieben unzulässige Dateien oder durch Überschreiben der uneingeschränkte Dateien zu umgehen. Daher empfiehlt es sich, dass Sie die Zugriffssteuerungslisten (ACLs) verwenden, um Benutzern den zum Ausführen dieser Aufgaben erforderlichen Zugriff zu verweigern.

### <a name="test-new-policy-settings-thoroughly-in-test-environments-before-applying-the-policy-settings-to-your-domain"></a>Testen Sie neue Richtlinieneinstellungen gründlich in Testumgebungen vor dem Anwenden der Richtlinieneinstellungen zu Ihrer Domäne.

-   Neue Richtlinieneinstellungen möglicherweise anders als erwartet ursprünglich fungieren. Tests beeinträchtigt ist die Wahrscheinlichkeit, dass ein Problem auftritt, wenn Sie Einstellungen in Ihrem Netzwerk bereitstellen.

-   Sie können eine Testdomäne getrennt von der Internetdomäne Ihrer Organisation, in dem Sie neue Richtlinieneinstellungen testen einrichten. Sie können auch die Einstellungen durch eine Test-GPO erstellen und verknüpfen es auf einer Testorganisationseinheit testen. Wenn Sie die Richtlinieneinstellungen mit Testbenutzer gründlich getestet haben, können Sie das Test-GPO mit Ihrer Domäne verknüpfen.

-   Stellen Sie keine Programme oder Dateien, um **nicht erlaubt** ohne vorheriges Testen, um festzustellen, was der Effekt sein kann. Einschränkungen für bestimmte Dateien können den Betrieb von Ihrem Computer oder ein Netzwerk erheblich beeinträchtigen.

-   Informationen, falsch eingegeben werden, oder Tipp-kann eine Einstellung führen, die nicht wie erwartet ausgeführt wird. Testen neue Richtlinieneinstellungen, ehe sie können zu unerwartetem Verhalten vorzubeugen.

### <a name="filter-user-policy-settings-based-on-membership-in-security-groups"></a>Filtern Sie benutzerrichtlinieneinstellungen basierend auf der Mitgliedschaft in Sicherheitsgruppen.

-   Sie können angeben, Benutzer oder Gruppen, die für die Sie keine Einstellung durch Deaktivieren des anwenden möchten die **"Gruppenrichtlinie übernehmen"** und **lesen** Kontrollkästchen, die sich auf befinden der **Security** Registerkarte im Dialogfeld "Eigenschaften" für das Gruppenrichtlinienobjekt.

-   Wenn die Berechtigung "Lesen" verweigert wird, wird die Richtlinieneinstellung nicht durch den Computer heruntergeladen. Daher ist weniger Bandbreite verbraucht durch Herunterladen unnötige Einstellungen, wodurch das Netzwerk schneller funktioniert. Um die Berechtigung "Lesen", aktivieren Sie **Verweigern** für die **lesen** Kontrollkästchen auf der **Security** Registerkarte im Dialogfeld "Eigenschaften" für das Gruppenrichtlinienobjekt.

### <a name="do-not-link-to-a-gpo-in-another-domain-or-site"></a>Verknüpfen Sie nicht mit einem Gruppenrichtlinienobjekt in einer anderen Domäne oder des Standorts.

-   Verknüpfung mit einem Gruppenrichtlinienobjekt in einer anderen Domäne oder des Standorts kann zu Leistungseinbußen führen.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

|Inhaltstyp|Verweise|
|--------|-------|
|**Planen der**|[Technische Referenz zu Software Restriction Policies](https://technet.microsoft.com/library/cc728085(v=WS.10).aspx)|
|**Vorgänge**|[Administer Software Restriction Policies](administer-software-restriction-policies.md)|
|**Problembehandlung**|[Richtlinien für Softwareeinschränkung Problembehandlung (2003)](https://technet.microsoft.com/library/cc737011(v=WS.10).aspx)|
|**Sicherheit**|[Bedrohungen und Gegenmaßnahmen für Software Restriction Policies (2008)](https://technet.microsoft.com/library/dd349795(v=WS.10).aspx)<br /><br />[Bedrohungen und Gegenmaßnahmen für Software Restriction Policies (2008 R2)](https://technet.microsoft.com/library/hh125926(v=WS.10).aspx)|
|**Tools und Einstellungen**|[Richtlinien für Softwareeinschränkung Tools und Einstellungen (2003)](https://technet.microsoft.com/library/cc782454(v=WS.10).aspx)|
|**Community-Ressourcen**|[Sperren von Anwendungen mit Richtlinien für Softwareeinschränkung](https://technet.microsoft.com/magazine/2008.06.srp.aspx?pr=blog)|


