---
title: Administer Software Restriction Policies
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8cc22093-67d1-47b6-9ddd-4569b6761ce9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 67ef99c95f10585ab72dee4bdf6512e715d13f4a
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="administer-software-restriction-policies"></a>Administer Software Restriction Policies

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

In diesem Thema für IT-Experten enthält Verfahren zum Verwalten von Anwendungssteuerungsrichtlinien mithilfe von Anfang (Software Restriction Policies, SRP) in Windows Server 2008 und Windows Vista.

## <a name="introduction"></a>Einführung in
(Software Restriction Policies, SRP) ist der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt, und die Fähigkeit zur Ausführung dieser Programme steuert. Mithilfe von Softwareeinschränkungsrichtlinien um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in dem Sie nur explizit angegebene Anwendungen ausführen können. Diese sind mit Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert, aber auch auf eigenständigen Computern konfiguriert werden. Weitere Informationen zu SRP finden Sie unter der [Softwareeinschränkungsrichtlinien](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, kann Windows AppLocker anstelle von oder zusammen mit SRP für einen Teil Ihrer anwendungssteuerungsstrategie verwendet werden.

Dieses Thema enthält:

-   [Zum Öffnen von Softwareeinschränkungsrichtlinien](#BKMK_Open_SRP)

-   [Zum Erstellen neuer Softwareeinschränkungsrichtlinien](#BKMK_Create_SRP)

-   [Hinzufügen oder Löschen eines designierten Dateityps](#BKMK_Add_Del)

-   [Um zu verhindern, dass Softwareeinschränkungsrichtlinien für lokale Administratoren](#BKMK_Prevent_Admin)

-   [So ändern Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien](#BKMK_Sec_Lvl)

-   [Anwenden von Softwareeinschränkungsrichtlinien auf DLLs](#BKMK_Apply_SRP_DLLs)

Informationen dazu, wie Sie bestimmte Aufgaben mit SRP finden Sie in der folgenden:

-   [Bestimmen Sie zulassen bzw. verweigern-Liste und des Anwendungsinventars für Richtlinien für Softwareeinschränkung](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

-   [Arbeiten Sie mit Software Restriction Policies Regeln](work-with-software-restriction-policies-rules.md)

-   [Verwenden von Richtlinien für Softwareeinschränkung zum Schutz Ihres Computers vor einem E-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

## <a name="BKMK_Open_SRP"></a>Zum Öffnen von Softwareeinschränkungsrichtlinien

-   [Für den lokalen computer](#BKMK_1)

-   [Sind für eine Domäne Site oder Organisationseinheit, und Sie ein, auf einem Mitgliedsserver oder einer Arbeitsstation, die einer Domäne angehört](#BKMK_2)

-   [Für einer Domäne oder Organisationseinheit, und Sie auf einem Domänencontroller oder auf einer Arbeitsstation mit den Remoteserver-Verwaltungstools installiert sind](#BKMK_3)

-   [Für einen Standort, und Sie werden auf einem Domänencontroller oder einer Arbeitsstation mit den Remoteserver-Verwaltungstools installiert](#BKMK_4)

### <a name="BKMK_1"></a>Für den lokalen computer

1.  Öffnen Sie die lokalen Sicherheitseinstellungen.

2.  Klicken Sie in der Konsolenstruktur auf **Softwareeinschränkungsrichtlinien**.

    **In welchen Bereichen?**

    -   Security Settings-Software Restriction Policies

> [!NOTE]
> Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Administratoren" auf dem lokalen Computer sein, oder Sie müssen die entsprechenden Berechtigungen delegiert.

### <a name="BKMK_2"></a>Sind für eine Domäne Site oder Organisationseinheit, und Sie ein, auf einem Mitgliedsserver oder einer Arbeitsstation, die einer Domäne angehört

1.  Öffnen Sie Microsoft Management Console (MMC).

2.  Auf der **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**, und klicken Sie dann auf **hinzufügen**.

3.  Klicken Sie auf **Editor für lokale Gruppenrichtlinien Objekt**, und klicken Sie dann auf **hinzufügen**.

4.  In **Gruppenrichtlinienobjekt auswählen**, klicken Sie auf **Durchsuchen**.

5.  In **für ein Gruppenrichtlinienobjekt Durchsuchen**, wählen Sie in der entsprechenden Domäne, Site oder Organisationseinheit (Group Policy Object, GPO)- oder eine neue zu erstellen, und klicken Sie dann auf **Fertig stellen**.

6.  Klicken Sie auf **schließen**, und klicken Sie dann auf **OK**.

7.  Klicken Sie in der Konsolenstruktur auf **Softwareeinschränkungsrichtlinien**.

    **In welchen Bereichen?**

    -   *Gruppe Richtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration oder

        Benutzer Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen Einstellungen/Softwareeinschränkungsrichtlinien

> [!NOTE]
> Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

### <a name="BKMK_3"></a>Für einer Domäne oder Organisationseinheit, und Sie auf einem Domänencontroller oder auf einer Arbeitsstation mit den Remoteserver-Verwaltungstools installiert sind

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole.

2.  Klicken Sie in der Konsolenstruktur auf die Gruppe Gruppenrichtlinienobjekt (GPO), die Sie Softwareeinschränkungsrichtlinien für öffnen möchten.

3.  Klicken Sie auf **bearbeiten** um das Gruppenrichtlinienobjekt zu öffnen, die Sie bearbeiten möchten. Sie können auch klicken **neu** erstellen ein neues Gruppenrichtlinienobjekt, und klicken Sie auf **bearbeiten**.

4.  Klicken Sie in der Konsolenstruktur auf **Softwareeinschränkungsrichtlinien**.

    **In welchen Bereichen?**

    -   *Gruppe Richtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration oder

        Benutzer Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen Einstellungen/Softwareeinschränkungsrichtlinien

> [!NOTE]
> Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

### <a name="BKMK_4"></a>Für einen Standort, und Sie werden auf einem Domänencontroller oder einer Arbeitsstation mit den Remoteserver-Verwaltungstools installiert

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole.

2.  Klicken Sie in der Konsolenstruktur auf der Website, der Sie Gruppenrichtlinien festlegen möchten.

    **In welchen Bereichen?**

    -   Active Directory-Standorte und-Dienste [*Domänencontrollername. Domänenname*] / Standorte/Standort

3.  Klicken Sie auf einen Eintrag in **Gruppenrichtlinienobjekt-Verknüpfungen** wählen Sie ein vorhandenes Gruppenrichtlinienobjekt (GPO), und klicken Sie dann auf **bearbeiten**. Sie können auch klicken **neu** erstellen ein neues Gruppenrichtlinienobjekt, und klicken Sie auf **bearbeiten**.

4.  Klicken Sie in der Konsolenstruktur auf **Softwareeinschränkungsrichtlinien**.

    **Wo**

    -   *Gruppe Richtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration oder

        Benutzer Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen Einstellungen/Softwareeinschränkungsrichtlinien

> [!NOTE]
> -   Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Administratoren" auf dem lokalen Computer sein, oder Sie müssen die entsprechenden Berechtigungen delegiert. Wenn der Computer einer Domäne angehört, um dieses Verfahren ausführen können möglicherweise Mitglieder der Gruppe Domänen-Admins.
> -   Richtlinieneinstellungen festgelegt, die auf Computern, unabhängig davon, welche sich Benutzer anmelden, angewendet werden, klicken Sie auf **Computerkonfiguration**.
> -   Klicken Sie zum Festlegen von Richtlinien, die für Benutzer, unabhängig davon, welche Computer sie melden Sie sich angewendet werden, auf **Benutzerkonfiguration**.

## <a name="BKMK_Create_SRP"></a>Zum Erstellen neuer Softwareeinschränkungsrichtlinien

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  Auf der **Aktion** Menü klicken Sie auf **neue Softwareeinschränkungsrichtlinien**.

> [!WARNING]
> -   Zum Ausführen dieses Verfahrens, abhängig von Ihrer Umgebung sind verschiedene Administratorrechte erforderlich:
> 
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für den lokalen Computer erstellen: Mitgliedschaft in der lokalen **Administratoren** Gruppe oder einer entsprechenden Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für einen Computer, die einer Domäne angehört erstellen, können Mitglieder der Gruppe Domänen-Admins dieses Verfahren ausführen.
> -   Wenn Softwareeinschränkungsrichtlinien für ein Gruppenrichtlinienobjekt (GPO), bereits erstellt wurden die **neue Softwareeinschränkungsrichtlinien** Befehl wird nur angezeigt, auf die **Aktion** Menü. So löschen Sie die Richtlinien für softwareeinschränkung, die auf ein Gruppenrichtlinienobjekt in der Konsolenstruktur angewendet werden mit der rechten Maustaste **Softwareeinschränkungsrichtlinien**, und klicken Sie dann auf **Softwareeinschränkungsrichtlinien löschen**. Wenn Sie Softwareeinschränkungsrichtlinien für ein Gruppenrichtlinienobjekt löschen, löschen Sie auch alle Software Restriction Policies Regeln für das Gruppenrichtlinienobjekt. Nachdem Sie Softwareeinschränkungsrichtlinien gelöscht haben, können Sie neue Softwareeinschränkungsrichtlinien für das Gruppenrichtlinienobjekt erstellen.

## <a name="BKMK_Add_Del"></a>Hinzufügen oder Löschen eines designierten Dateityps

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  Doppelklicken Sie im Detailbereich auf **Designierte Dateitypen**.

3.  Führen Sie einen der folgenden:

    -   Hinzufügen ein Dateityps in **Dateinamenerweiterung**, geben Sie den Dateinamen, und klicken Sie dann auf **hinzufügen**.

    -   So löschen Sie einen Dateityp in **Designierte Dateitypen**, klicken Sie auf den Dateityp aus, und klicken Sie dann auf **entfernen**.

> [!NOTE]
> -   Zum Ausführen dieses Verfahrens, abhängig von der Umgebung, in dem Sie hinzufügen oder löschen ein designierten Dateityps, sind verschiedene Administratorrechte erforderlich:
> 
>     -   Wenn Sie beim Hinzufügen oder ein designierten Dateityps für Ihren lokalen Computer löschen: Mitgliedschaft in der lokalen **Administratoren** Gruppe oder einer entsprechenden Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für einen Computer, die einer Domäne angehört erstellen, können Mitglieder der Gruppe Domänen-Admins dieses Verfahren ausführen.
> -   Möglicherweise ist es erforderlich, um eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt (GPO) erstellen, wenn noch nicht geschehen.
> -   Die Liste der designierten Dateitypen wird von allen Regeln für Computer Configuration und User Configuration für ein Gruppenrichtlinienobjekt verwendet.

## <a name="BKMK_Prevent_Admin"></a>Um zu verhindern, dass Softwareeinschränkungsrichtlinien für lokale Administratoren

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  Doppelklicken Sie im Detailbereich auf **Erzwingung**.

3.  Klicken Sie unter **Anwenden von Softwareeinschränkungsrichtlinien auf folgende Benutzer**, klicken Sie auf **alle Benutzer außer den lokalen Administratoren**.

> [!WARNING]
> -   Mitgliedschaft in der lokalen **Administratoren** Gruppe oder einer entsprechenden Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.
> -   Möglicherweise ist es erforderlich, um eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt (GPO) erstellen, wenn noch nicht geschehen.
> -   Ist es üblich, dass Benutzer als Mitglieder der Gruppe der lokalen Administratoren auf ihren Computern in Ihrer Organisation, sollten Sie nicht diese Option zu aktivieren.
> -   Wenn Sie eine Softwareeinschränkungsrichtlinien-Einstellung für den lokalen Computer definieren, verwenden Sie dieses Verfahren, um zu verhindern, dass lokale Administratoren dass Softwareeinschränkungsrichtlinien angewendet werden. Wenn Sie eine Softwareeinschränkungsrichtlinien-Einstellung für Ihr Netzwerk definieren, Filtern Sie benutzerrichtlinieneinstellungen basierend auf der Mitgliedschaft in Sicherheitsgruppen, die über eine Gruppenrichtlinie.

## <a name="BKMK_Sec_Lvl"></a>So ändern Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  Doppelklicken Sie im Detailbereich auf **Sicherheitsstufen**.

3.  Mit der rechten Maustaste der Sicherheitsstufe, die Sie als Standard festgelegt, und klicken Sie dann auf möchten **als Standard festlegen**.

> [!CAUTION]
> In bestimmten Verzeichnissen durch Festlegen der Ebene zu **nicht erlaubt** kann sich negativ auf das Betriebssystem auswirken.

> [!NOTE]
> -   Zum Ausführen dieses Verfahrens, abhängig von der Umgebung, bei denen Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien ändern, sind verschiedene Administratorrechte erforderlich.
> -   Möglicherweise ist es erforderlich, um eine neue Softwareeinschränkungsrichtlinien-Einstellung für dieses Gruppenrichtlinienobjekt (GPO) erstellen, wenn noch nicht geschehen.
> -   Klicken, Sie im Detailbereich wird die aktuelle Standardsicherheitsstufe durch einen schwarzen Kreis mit einem Häkchen angezeigt. Wenn Sie die aktuelle Standardsicherheitsstufe, mit der rechten Maustaste die **als Standard festlegen** Befehl nicht im Menü angezeigt.
> -   Software Restriction Policies Regeln werden erstellt, um Ausnahmen für die Standardsicherheitsstufe anzugeben. Wenn die Standardsicherheitsstufe festgelegt ist, um **Unrestricted**, kann mit Regeln Software, die nicht ausgeführt werden darf angegeben. Wenn die Standardsicherheitsstufe festgelegt ist, um **nicht erlaubt**, kann mit Regeln Software, die ausgeführt werden darf angegeben.
> -   Bei der Installation wird die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien für alle Dateien auf Ihrem System festgelegt ist, um **Unrestricted**.

## <a name="BKMK_Apply_SRP_DLLs"></a>Anwenden von Softwareeinschränkungsrichtlinien auf DLLs

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  Doppelklicken Sie im Detailbereich auf **Erzwingung**.

3.  Klicken Sie unter **Anwenden von Softwareeinschränkungsrichtlinien auf die folgenden**, klicken Sie auf **alle Softwaredateien**.

> [!NOTE]
> -   Zum Ausführen dieses Verfahrens müssen Sie Mitglied der Gruppe "Administratoren" auf dem lokalen Computer sein, oder Sie müssen die entsprechenden Berechtigungen delegiert. Wenn der Computer einer Domäne angehört, um dieses Verfahren ausführen können möglicherweise Mitglieder der Gruppe Domänen-Admins.
> -   In der Standardeinstellung überprüfen nicht Dynamic Link Libraries (DLLs) Richtlinien für softwareeinschränkung. Die Überprüfung von DLLs kann die Systemleistung beeinträchtigen, da Softwareeinschränkungsrichtlinien bei jedem einer DLL laden ausgewertet werden müssen. Allerdings können Sie entscheiden, DLL-Dateien zu überprüfen, ob Sie vor Viren, abzielt DLL-Dateien sind. Wenn die Standardsicherheitsstufe, um festgelegt ist **nicht erlaubt**, und Sie aktivieren die DLL-Überprüfung, müssen Software Restriction Policies Sie Regeln erstellen, mit denen jede DLL-Datei ausführen können.


