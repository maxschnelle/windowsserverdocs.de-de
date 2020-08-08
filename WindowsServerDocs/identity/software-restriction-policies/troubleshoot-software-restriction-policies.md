---
title: Problembehandlung bei Richtlinien für Softwareeinschränkung
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 4fd53736-03e7-4bf9-ba90-d1212d93e19a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 6e4d31dd6e434c5a5b18491ea7f73b92c993e05a
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953007"
---
# <a name="troubleshoot-software-restriction-policies"></a>Problembehandlung bei Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden häufige Probleme und ihre Lösungen bei der Problembehandlung von Software Einschränkungs Richtlinien (SRP) ab Windows Server 2008 und Windows Vista beschrieben.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese sind in Microsoft Active Directory Domain Services und Gruppenrichtlinie integriert, können aber auch auf eigenständigen Computern konfiguriert werden. Weitere Informationen zu SRP finden Sie in den [Richtlinien für Software Einschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7 kann Windows AppLocker anstelle von oder in zusammen mit SRP für einen Teil ihrer Anwendungs Steuerungsstrategie verwendet werden.

### <a name="windows-cannot-open-a-program"></a>Ein Programm kann nicht geöffnet werden.
Benutzer erhalten eine Meldung mit dem Hinweis, dass das Programm von Windows nicht geöffnet werden kann, da es durch eine Software Einschränkungs Richtlinie verhindert wurde. Öffnen Sie Ereignisanzeige, oder wenden Sie sich an Ihren Systemadministrator, um weitere Informationen zu erhalten. Oder in der Befehlszeile wird eine Meldung angezeigt, dass das System das angegebene Programm nicht ausführen kann.

**Ursache:** Die Standard Sicherheitsstufe (oder eine Regel) wurde erstellt, sodass das Softwareprogramm als unzulässig fest **gelegt wurde.** daher wird es nicht gestartet.

**Lösung:** Suchen Sie im Ereignisprotokoll nach einer ausführlichen Beschreibung der Nachricht. Die Ereignisprotokoll Meldung gibt an, welches Software **Programm als unzulässig** festgelegt wurde und welche Regel auf das Programm angewendet wird.

### <a name="modified-software-restriction-policies-are-not-taking-effect"></a>Geänderte Richtlinien für Software Einschränkung werden nicht wirksam.
**Ursache:** Software Einschränkungs Richtlinien, die über Gruppenrichtlinie in einer Domäne angegeben sind, überschreiben alle lokal konfigurierten Richtlinien Einstellungen. Dies könnte darauf hindeuten, dass es eine Richtlinien Einstellung aus der Domäne gibt, die Ihre Richtlinien Einstellung überschreibt.

**Ursache:** Gruppenrichtlinie hat seine Richtlinien Einstellungen möglicherweise nicht aktualisiert. Gruppenrichtlinie wendet regelmäßig Änderungen an Richtlinien Einstellungen an. Daher ist es wahrscheinlich, dass die im Verzeichnis vorgenommenen Richtlinien Änderungen noch nicht aktualisiert wurden.

**Lösungen**

1.  Auf dem Computer, auf dem Sie die Software Einschränkungs Richtlinien für das Netzwerk ändern, muss eine Verbindung mit einem Domänen Controller hergestellt werden können. Stellen Sie sicher, dass der Computer einen Domänen Controller kontaktieren kann.

2.  Aktualisieren Sie die Richtlinie, indem Sie sich vom Netzwerk abmelden und sich dann erneut beim Netzwerk anmelden. Wenn eine Richtlinie über Gruppenrichtlinie angewendet wird, werden diese Richtlinien durch die Protokollierung wieder in aktualisiert.

3.  Sie können die Richtlinien Einstellungen mithilfe des Befehlszeilen-Hilfsprogramms gpupdate aktualisieren, oder indem Sie sich von abmelden und sich dann wieder bei Ihrem Computer anmelden. Führen Sie gpupdate aus, und melden Sie sich dann wieder bei Ihrem Computer an, um optimale Ergebnisse zu erzielen. Im Allgemeinen werden die Sicherheitseinstellungen alle 90 Minuten auf einer Arbeitsstation oder einem Server und alle fünf Minuten auf einem Domänen Controller aktualisiert. Die Einstellungen werden außerdem alle 16 Stunden aktualisiert, unabhängig davon, ob Änderungen erfolgt sind. Diese Einstellungen können konfiguriert werden, sodass sich die Aktualisierungsintervalle in jeder Domäne unterscheiden können.

4.  Überprüfen Sie die geltenden Richtlinien. Überprüfen Sie Richtlinien auf Domänen Ebene auf **keine Überschreibungs** Einstellungen

5.  Software Einschränkungs Richtlinien, die über Gruppenrichtlinie in einer Domäne angegeben sind, überschreiben alle lokal konfigurierten Richtlinien. Verwenden Sie das gpresult-Befehlszeilen Tool, um die Auswirkungen der Richtlinie zu ermitteln. Dies könnte bedeuten, dass eine Richtlinie aus der Domäne vorhanden ist, die Ihre lokale Einstellung überschreibt.

6.  Wenn sich die SRP-und AppLocker-Richtlinien Einstellungen im gleichen GPO befinden, haben AppLocker-Einstellungen unter Windows 7, Windows Server 2008 R2 und höher Vorrang. Es wird empfohlen, die Richtlinien Einstellungen von SRP und AppLocker in verschiedenen Gruppenrichtlinien Objekten zu platzieren.

### <a name="after-adding-a-rule-through-srp-you-cannot-log-on-to-your-computer"></a>Nachdem Sie eine Regel über SRP hinzugefügt haben, können Sie sich nicht mehr bei Ihrem Computer anmelden.
**Ursache:** Der Computer greift beim Start auf viele Programme und Dateien zu. Möglicherweise haben Sie eine dieser Programme oder Dateien **versehentlich als unzulässig**festgelegt. Da der Computer nicht auf das Programm oder die Datei zugreifen kann, kann er nicht ordnungsgemäß gestartet werden.

**Lösung:** Starten Sie den Computer im abgesicherten Modus, melden Sie sich als lokaler Administrator an, und ändern Sie dann die Richtlinien für Software Einschränkung, damit das Programm oder die Datei ausgeführt werden kann.

### <a name="a-new-policy-setting-is-not-applying-to-a-specific-file-name-extension"></a>Eine neue Richtlinien Einstellung gilt nicht für eine bestimmte Dateinamenerweiterung.
**Ursache:** Die Dateinamenerweiterung ist nicht in der Liste der unterstützten Dateitypen enthalten.

**Lösung:** Fügen Sie der Liste der von SRP unterstützten Dateitypen die Dateinamenerweiterung hinzu.

Software Einschränkungs Richtlinien lösen das Problem der Regelung von unbekanntem oder nicht vertrauenswürdigem Code. Software Einschränkungs Richtlinien sind Sicherheitseinstellungen zum Identifizieren von Software und Steuern der Möglichkeit, auf einem lokalen Computer, an einem Standort, einer Domäne oder einer Organisationseinheit ausgeführt zu werden, und können über ein GPO implementiert werden.

### <a name="a-default-rule-is-not-restricting-as-expected"></a>Eine Standardregel schränkt nicht erwartungsgemäß ein.
**Ursache:** Regeln, die in einer bestimmten Reihenfolge angewendet werden, die dazu führen können, dass Standardregeln durch bestimmte Regeln überschrieben werden. SRP wendet Regeln in der folgenden Reihenfolge an (am spezifischsten an der allgemeinen Reihenfolge):

1.  Hashregeln

2.  Zertifikatregeln

3.  Pfadregeln

4.  Internet Zonen Regeln

5.  Standardregeln

**Lösung:** Evaluieren Sie die Regeln, die die Anwendung einschränken, und entfernen Sie ggf. alle außer der Standardregel.

### <a name="unable-to-discover-which-restrictions-are-applied"></a>Es konnte nicht ermittelt werden, welche Einschränkungen angewendet werden.
**Ursache:** Es gibt keine offensichtliche Ursache für das unerwartete Verhalten, und die GPO-Aktualisierung hat das Problem nicht gelöst, sodass eine weitere Untersuchung erforderlich ist.

**Lösungen**

1.  Untersuchen Sie das System Ereignisprotokoll, und Filtern Sie nach der Quelle "Software Einschränkungs Richtlinie". Die Einträge geben explizit an, welche Regel für die einzelnen Anwendungen implementiert wird.

2.  Aktivieren Sie die erweiterte Protokollierung. Weitere Informationen finden Sie unter [bestimmen der Zulassungs-und Verweigerungs Liste und Anwendungs Inventur für Software Einschränkungs Richtlinien](software-restriction-policies.md) .


