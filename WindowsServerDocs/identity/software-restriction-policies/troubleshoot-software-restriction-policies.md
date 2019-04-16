---
title: "Problembehandlung bei Richtlinien für Softwareeinschränkung"
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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="troubleshoot-software-restriction-policies"></a>Problembehandlung bei Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema beschreibt häufig auftretende Probleme und ihre Lösungen bei der Behandlung von (Software Restriction Policies, SRP) ab Windows Server2008 und Windows Vista.

## <a name="introduction"></a>Einführung in
(Software Restriction Policies, SRP) ist der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt, und die Fähigkeit zur Ausführung dieser Programme steuert. Mithilfe von Softwareeinschränkungsrichtlinien um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in dem Sie nur explizit angegebene Anwendungen ausführen können. Diese sind mit Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert, aber auch auf eigenständigen Computern konfiguriert werden. Weitere Informationen zu SRP finden Sie unter der [Softwareeinschränkungsrichtlinien](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, kann Windows AppLocker anstelle von oder zusammen mit SRP für einen Teil Ihrer anwendungssteuerungsstrategie verwendet werden.

### <a name="windows-cannot-open-a-program"></a>Ein Programm kann nicht geöffnet werden.
Benutzer erhalten die Meldung "Windows dieses Programm öffnen können, weil es von einer Softwareeinschränkungsrichtlinie verhindert wurde. Weitere Informationen öffnen Sie die Ereignisanzeige, oder wenden Sie sich an den Systemadministrator." Oder in der Befehlszeile eine Meldung "das System das angegebene Programm nicht ausgeführt werden kann."

**Ursache:** die Standardsicherheitsstufe (oder eine Regel) erstellt wurde, damit das Softwareprogramm festgelegt ist, als **nicht erlaubt**, und daher nicht gestartet.

**Lösung:** suchen Sie im Ereignisprotokoll für eine detaillierte Beschreibung der Nachricht. Die Meldung im Ereignisprotokoll gibt an, welches Programm festgelegt ist, als **nicht erlaubt** und welche Regel auf die Anwendung angewendet wird.

### <a name="modified-software-restriction-policies-are-not-taking-effect"></a>Geänderte Richtlinien für Softwareeinschränkung sind nicht wirksam
**Ursache:** Softwareeinschränkungsrichtlinien, die in einer Domäne mithilfe von Gruppenrichtlinien angegeben sind überschreiben alle Einstellungen, die lokal konfiguriert werden. Dies kann bedeutet, dass es ist eine Einstellung aus der Domäne, die die Richtlinieneinstellung außer Kraft setzt.

**Ursache:** Gruppenrichtlinien möglicherweise nicht die Einstellungen aktualisiert haben. Gruppenrichtlinie wendet Änderungen in regelmäßigen Abständen Richtlinieneinstellungen; Daher ist es wahrscheinlich, dass die Richtlinie ändert, die im Verzeichnis vorgenommen wurden, noch nicht aktualisiert wurde.

**Lösungen:**

1.  Der Computer, auf dem Sie Softwareeinschränkungsrichtlinien ändern, für das Netzwerk eine Verbindung mit einen Domänencontroller herstellen muss. Stellen Sie sicher, dass der Computer mit einem Domänencontroller herstellen kann.

2.  Aktualisieren Sie Richtlinie vom Netzwerk ab- und dann auf das Netzwerk erneut anmelden. Wenn eine Richtlinie über eine Gruppenrichtlinie angewendet wird, werden diese Richtlinien wieder anmelden aktualisiert werden.

3.  Sie können Einstellungen mit dem Befehlszeilenprogramm Gpupdate oder Abmelden und melden Sie sich dann wieder an Ihren Computer aktualisieren. Führen Sie für optimale Ergebnisse "gpupdate", und melden Sie sich dann aus, und melden Sie sich wieder bei Ihrem Computer. Die Sicherheitseinstellungen werden in der Regel auf einer Arbeitsstation oder einem Server alle 90Minuten und auf einem Domänencontroller alle 5Minuten aktualisiert. Die Einstellungen werden auch alle 16 Stunden aktualisiert, unabhängig davon, ob Änderungen erfolgt sind. Hierbei handelt es sich um konfigurierbare Einstellungen, sodass Aktualisierungsintervalle in jeder Domäne unterscheiden können.

4.  Überprüfen, welche Richtlinien gelten. Überprüfen Sie die Richtlinien auf Domänenebene für **kein Vorrang** Einstellungen.

5.  Softwareeinschränkungsrichtlinien, die in einer Domäne mithilfe von Gruppenrichtlinien angegeben sind außer Kraft setzen alle Richtlinien, die lokal konfiguriert werden. Verwenden Sie Gpresult-Befehlszeilentool, um zu bestimmen, was im Endeffekt die Richtlinie ist. Dies kann bedeutet, dass eine Richtlinie aus der Domäne, die Ihre lokale Einstellung überschrieben wird.

6.  Wenn SRP und AppLocker-Richtlinien im selben Gruppenrichtlinienobjekt befinden, AppLocker-Einstellungen Vorrang unter Windows7, Windows Server2008 R2 und höher. Es wird empfohlen, SRP und AppLocker-Richtlinien in unterschiedlichen Gruppenrichtlinienobjekten aufgenommen werden sollen.

### <a name="after-adding-a-rule-through-srp-you-cannot-log-on-to-your-computer"></a>Nach dem Hinzufügen einer Regel über SRP, können Sie auf Ihrem Computer anmelden
**Ursache:** Computers viele Programme und Dateien zugreift, beim Starten. Möglicherweise haben versehentlich Festlegen eines dieser Programme oder Dateien **nicht erlaubt**. Da der Computer das Programm oder die Datei zugreifen kann, kann er nicht ordnungsgemäß gestartet.

**Lösung:** starten Sie den Computer im abgesicherten Modus, melden Sie sich als lokaler Administrator, und ändern Sie Softwareeinschränkungsrichtlinien, damit die Anwendung oder Datei ausführen können.

### <a name="a-new-policy-setting-is-not-applying-to-a-specific-file-name-extension"></a>Eine neue Einstellung wird nicht auf einer bestimmten Dateinamenerweiterung anwenden.
**Ursache:** die Dateinamenerweiterung ist nicht in der Liste der unterstützten Dateitypen.

**Lösung:** fügen Sie die Dateinamenerweiterung der Liste der Dateitypen, die von SRP unterstützt.

Richtlinien für Softwareeinschränkung beheben das Problem des regulieren von unbekannt oder nicht vertrauenswürdigem Code. Richtlinien für Softwareeinschränkung sind Sicherheitseinstellungen, Software erkennen und Steuern der Ausführung auf einem lokalen Computer in einen Standort, Domäne oder Organisationseinheit ausgeführt werden und können über ein Gruppenrichtlinienobjekt implementiert werden.

### <a name="a-default-rule-is-not-restricting-as-expected"></a>Eine Standardregel ist nicht wie erwartet einschränken
**Ursache:** Regeln, die in einer bestimmten Reihenfolge angewendet werden, wodurch Standardregeln von bestimmte Regeln überschrieben werden können. SRP gilt Regeln in der folgenden Reihenfolge (die speziell für allgemeine):

1.  Hashregeln

2.  Zertifikatregeln

3.  Pfadregeln

4.  Internetzone Regeln

5.  Standardregeln

**Lösung:** bewerten Sie die Regeln schränkt die Anwendung und ggf. entfernen, mit Ausnahme der Standard-Regel.

### <a name="unable-to-discover-which-restrictions-are-applied"></a>Nicht erkennen, welche Einschränkungen angewendet werden
**Ursache:** kein offensichtlich Grund für unerwartetes Verhalten und GPO-Aktualisierung ist nicht das Problem behoben, sodass weitere Untersuchung notwendig ist.

**Lösungen:**

1.  Untersuchen Sie das Systemereignisprotokoll Filtern auf der Quelle "Softwareeinschränkungsrichtlinie." Die Einträge Status explizit an, welche Regel für jede Anwendung implementiert wird.

2.  Erweiterte Protokollierung zu aktivieren. Weitere Informationen finden Sie unter [zulassen bzw. verweigern-Liste zu ermitteln und des Anwendungsinventars für Richtlinien für Softwareeinschränkung](software-restriction-policies.md) Weitere Informationen.


