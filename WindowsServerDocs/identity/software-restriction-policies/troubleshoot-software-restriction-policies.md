---
title: Problembehandlung bei Richtlinien für Softwareeinschränkung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4fd53736-03e7-4bf9-ba90-d1212d93e19a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: abf592930f5347fa10e83c644671f68f9dc1a3f6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59872381"
---
# <a name="troubleshoot-software-restriction-policies"></a>Problembehandlung bei Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema beschreibt allgemeine Probleme und Lösungen, bei der Problembehandlung von Windows Server 2008 und Windows Vista (Software Restriction Policies, SRP) ab.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese in Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert sind, aber auch auf eigenständigen Computern konfiguriert werden. Weitere Informationen zu SRP finden Sie unter den [Richtlinien für Softwareeinschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, Windows AppLocker anstelle oder zusammen mit Richtlinien für Softwareeinschränkung für einen Teil Ihrer anwendungssteuerungsstrategie dienen.

### <a name="windows-cannot-open-a-program"></a>Windows kann kein Programm geöffnet werden.
Benutzer erhalten eine Meldung mit dem Text "Windows dieses Programms öffnen können, da es durch eine Richtlinie für softwareeinschränkung verhindert wurde. Weitere Informationen öffnen Sie-Ereignisanzeige zu, oder wenden Sie sich an Ihren Systemadministrator." Oder, in der Befehlszeile eine Meldung besagt "das System das angegebene Programm nicht ausgeführt werden kann."

**Ursache:** Die Standardsicherheitsstufe (oder eine Regel) erstellt wurde, damit das Softwareprogramm festgelegt ist, als **nicht erlaubt**, und daher wird er nicht gestartet.

**Lösung:** Suchen Sie in das Ereignisprotokoll für eine detaillierte Beschreibung der Nachricht. Die Meldung im Ereignisprotokoll gibt an, welche Softwareprogramm als festgelegt wurde **nicht erlaubt** und an das Programm die Regel angewendet wird.

### <a name="modified-software-restriction-policies-are-not-taking-effect"></a>Geänderte Richtlinien für softwareeinschränkung sind nicht wirksam
**Ursache:** Richtlinien für softwareeinschränkung, die in einer Domäne über die Gruppenrichtlinie angegeben werden, überschreiben Richtlinieneinstellungen, die lokal. Möglicherweise heißt das, dass es ist eine richtlinieneinstellung aus der Domäne, die Ihre richtlinieneinstellung außer Kraft gesetzt wird.

**Ursache:** Die Gruppenrichtlinie kann die Richtlinieneinstellungen nicht aktualisiert haben. Gruppenrichtlinie wendet die Änderungen in regelmäßigen Abständen an den Richtlinieneinstellungen für; aus diesem Grund ist es wahrscheinlich, dass die richtlinienänderungen, die im Verzeichnis vorgenommen wurden, noch nicht aktualisiert wurde.

**Lösungen:**

1.  Der Computer, auf dem Sie Richtlinien für softwareeinschränkung für das Netzwerk ändern, muss auf einem Domänencontroller herstellen können. Stellen Sie sicher, dass der Computer einen Domänencontroller herstellen kann.

2.  Die Aktualisierungsrichtlinie von außerhalb des Netzwerks anmelden, und klicken Sie dann auf das Netzwerk erneut anmelden. Wenn keine Richtlinie über die Gruppenrichtlinie angewendet wird, werden diese Richtlinien wieder anmelden aktualisiert werden.

3.  Sie können Richtlinieneinstellungen, die mit dem Befehlszeilen-Hilfsprogramm Gpupdate oder beim Abmelden von, und melden Sie sich dann wieder bei Ihrem Computer aktualisieren. Für optimale Ergebnisse Ausführen von Gpupdate, und melden Sie sich dann aus, und melden Sie sich wieder bei Ihrem Computer. Die Sicherheitseinstellungen werden im Allgemeinen alle 90 Minuten auf einer Arbeitsstation oder einen Server und auf einem Domänencontroller alle 5 Minuten aktualisiert. Die Einstellungen werden außerdem alle 16 Stunden aktualisiert, unabhängig davon, ob Änderungen erfolgt sind. Dies sind die konfigurierbaren Einstellungen, damit Aktualisierungsintervalle in jeder Domäne möglicherweise unterscheiden.

4.  Überprüfen, welche Richtlinien gelten. Überprüfen Sie die Richtlinien auf Domänenebene für **kein Vorrang** Einstellungen.

5.  Richtlinien für softwareeinschränkung, die in einer Domäne über die Gruppenrichtlinie angegeben werden, überschreiben alle Richtlinien, die lokal. Verwenden Sie Gpresult-Befehlszeilentool, um zu bestimmen, was im Endeffekt die Richtlinie ist. Dies möglicherweise impliziert, dass es sich bei einer Richtlinie aus der Domäne, die Ihre lokale Einstellung außer Kraft gesetzt wird.

6.  Wenn das gleiche GPO SRP und AppLocker-Richtlinieneinstellungen werden, AppLocker-Einstellungen Vorrang unter Windows 7, Windows Server 2008 R2 und höher. Es wird empfohlen, Richtlinien für Softwareeinschränkung und AppLocker-Richtlinieneinstellungen in unterschiedlichen GPOs zu platzieren.

### <a name="after-adding-a-rule-through-srp-you-cannot-log-on-to-your-computer"></a>Nach dem Hinzufügen einer Regel über Richtlinien für Softwareeinschränkung, können Sie auf Ihrem Computer anmelden
**Ursache:** Ihr Computer greift auf vielen Programmen und Dateien beim Starten. Legen Sie möglicherweise haben versehentlich diese Programme oder Dateien **nicht erlaubt**. Da der Computer das Programm oder die Datei zugreifen kann, kann er nicht ordnungsgemäß gestartet.

**Lösung:** Starten Sie den Computer im abgesicherten Modus, melden Sie sich als lokaler Administrator an und ändern Sie dann die Richtlinien für softwareeinschränkung damit das Programm oder die Datei ausführen können.

### <a name="a-new-policy-setting-is-not-applying-to-a-specific-file-name-extension"></a>Eine neue Einstellung wird nicht auf eine bestimmte Dateinamenerweiterung angewendet.
**Ursache:** Die Dateierweiterung ist nicht in der Liste der unterstützten Dateitypen.

**Lösung:** Hinzufügen der Erweiterungs der Liste der Dateitypen, die von SRP unterstützt werden.

Richtlinien für softwareeinschränkung regulieren von unbekannten oder nicht vertrauenswürdigen Code das Problem zu beheben. Richtlinien für softwareeinschränkung sind Sicherheitseinstellungen zum Identifizieren von Software und steuern die Möglichkeit zur Ausführung auf einem lokalen Computer in einer Site, Domäne oder Organisationseinheit, und können über ein Gruppenrichtlinienobjekt implementiert werden.

### <a name="a-default-rule-is-not-restricting-as-expected"></a>Eine Standardregel ist nicht einschränken, wie erwartet
**Ursache:** Regeln, die in einer bestimmten Reihenfolge angewendet werden, wodurch Standardregeln, die durch bestimmte Regeln überschrieben werden können. Richtlinien für Softwareeinschränkung wendet Regeln in der folgenden Reihenfolge (die meisten spezifisch für allgemeine) an:

1.  Hashregeln

2.  Zertifikatregeln

3.  Pfadregeln

4.  Regeln für Internetzone

5.  Standardregeln

**Lösung:** Bewerten Sie die Regeln, die die Anwendung beschränken und bei Bedarf, entfernen Sie alle bis auf die Standardregel.

### <a name="unable-to-discover-which-restrictions-are-applied"></a>Kann nicht ermitteln, welche Einschränkungen angewendet werden
**Ursache:** Es gibt keine offensichtliche Ursache für das unerwartete Verhalten und GPO-Aktualisierung ist nicht das Problem gelöst, damit weitere Untersuchung erforderlich ist.

**Lösungen:**

1.  Untersuchen Sie das Systemereignisprotokoll, die Filterung auf der Datenquelle "Richtlinie für Softwareeinschränkung". Die Einträge Zustand explizit an, welche Regel für jede Anwendung implementiert wird.

2.  Aktivieren Sie erweiterte Protokollierung. Finden Sie unter [zulassen bzw. verweigern-Liste zu bestimmen und des Anwendungsinventars für Richtlinien für Softwareeinschränkung](software-restriction-policies.md) für Weitere Informationen.


