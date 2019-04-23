---
title: Verwalten der Richtlinien für Softwareeinschränkung
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
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863591"
---
# <a name="administer-software-restriction-policies"></a>Verwalten der Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema für IT-Spezialisten enthält Verfahren zum Verwalten von Anwendungssteuerungsrichtlinien, die mit Windows Server 2008 und Windows Vista (Software Restriction Policies, SRP) ab.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese in Microsoft Active Directory-Domänendienste und Gruppenrichtlinien integriert sind, aber auch auf eigenständigen Computern konfiguriert werden. Weitere Informationen zu SRP finden Sie unter den [Richtlinien für Softwareeinschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7, Windows AppLocker anstelle oder zusammen mit Richtlinien für Softwareeinschränkung für einen Teil Ihrer anwendungssteuerungsstrategie dienen.

Dieses Thema enthält:

-   [Um Richtlinien für Softwareeinschränkung zu öffnen.](#BKMK_Open_SRP)

-   [Erstellen Sie neue Richtlinien für softwareeinschränkung](#BKMK_Create_SRP)

-   [Hinzufügen oder Löschen eines designierten Dateityps](#BKMK_Add_Del)

-   [Um zu verhindern, dass Softwareeinschränkungsrichtlinien für lokale Administratoren](#BKMK_Prevent_Admin)

-   [So ändern Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien](#BKMK_Sec_Lvl)

-   [Anwenden von Softwareeinschränkungsrichtlinien auf DLLs](#BKMK_Apply_SRP_DLLs)

Informationen zum Ausführen bestimmte Aufgaben mithilfe von Richtlinien für Softwareeinschränkung finden Sie hier:

-   [Ermitteln von zulassen bzw. verweigern-Liste und des Anwendungsinventars für Richtlinien für Softwareeinschränkung](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

-   [Arbeiten Sie mit Richtlinien für die Softwareeinschränkungsregeln](work-with-software-restriction-policies-rules.md)

-   [Verwenden von Richtlinien für Softwareeinschränkungen zum Schutz Ihres Computers vor einem e-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

## <a name="BKMK_Open_SRP"></a>Um Richtlinien für Softwareeinschränkung zu öffnen.

-   [Für den lokalen computer](#BKMK_1)

-   [Sind für eine Domäne Standort oder die Organisationseinheit, und Sie ein, auf einem Mitgliedsserver oder einer Arbeitsstation, die mit einer Domäne verknüpft ist](#BKMK_2)

-   [Für eine Domäne oder Organisationseinheit, und Sie sind auf einem Domänencontroller oder auf einer Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde.](#BKMK_3)

-   [Für einen Standort, und Sie sind auf einem Domänencontroller oder auf einer Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde.](#BKMK_4)

### <a name="BKMK_1"></a>Für den lokalen computer

1.  Öffnen Sie %%amp;quot;Lokale Sicherheitseinstellungen%%amp;quot;.

2.  Klicken Sie in der Konsolenstruktur auf **Richtlinien für Softwareeinschränkung**.

    **In welchen Bereichen?**

    -   Security-Einstellungen/Richtlinien für Softwareeinschränkung

> [!NOTE]
> Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer ein Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein oder Ihnen muss die entsprechende Berechtigung übertragen worden sein.

### <a name="BKMK_2"></a>Sind für eine Domäne Standort oder die Organisationseinheit, und Sie ein, auf einem Mitgliedsserver oder einer Arbeitsstation, die mit einer Domäne verknüpft ist

1.  Öffnen Sie die Microsoft Management Console (MMC).

2.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**, und klicken Sie dann auf **Hinzufügen**.

3.  Klicken Sie auf **Lokaler Gruppenrichtlinienobjekt-Editor** und anschließend auf **Hinzufügen**.

4.  Klicken Sie unter **Gruppenrichtlinienobjekt auswählen** auf **Durchsuchen**.

5.  In **für ein Gruppenrichtlinienobjekt, das Durchsuchen**, wählen Sie in der entsprechenden Domäne, Site oder Organisationseinheit (Group Policy Object, GPO)- oder ein neues erstellen, und klicken Sie dann auf **Fertig stellen**.

6.  Klicken Sie auf **Schließen**und dann auf **OK**.

7.  Klicken Sie in der Konsolenstruktur auf **Richtlinien für Softwareeinschränkung**.

    **In welchen Bereichen?**

    -   *Gruppenrichtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration oder

        User Configuration/Windows-Einstellungen/Sicherheitseinstellungen Settings/Richtlinien für Softwareeinschränkung

> [!NOTE]
> Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

### <a name="BKMK_3"></a>Für eine Domäne oder Organisationseinheit, und Sie sind auf einem Domänencontroller oder auf einer Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde.

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole.

2.  In der Konsolenstruktur mit der rechten Maustaste die Gruppe Gruppenrichtlinienobjekt (GPO), die Sie für Richtlinien für softwareeinschränkung öffnen möchten.

3.  Klicken Sie auf **Bearbeiten**, um das zu bearbeitende Gruppenrichtlinienobjekt zu öffnen. Sie können auch auf **Neu** klicken, um ein neues Gruppenrichtlinienobjekt zu erstellen, und anschließend auf **Bearbeiten** klicken.

4.  Klicken Sie in der Konsolenstruktur auf **Richtlinien für Softwareeinschränkung**.

    **In welchen Bereichen?**

    -   *Gruppenrichtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration oder

        User Configuration/Windows-Einstellungen/Sicherheitseinstellungen Settings/Richtlinien für Softwareeinschränkung

> [!NOTE]
> Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

### <a name="BKMK_4"></a>Für einen Standort, und Sie sind auf einem Domänencontroller oder auf einer Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde.

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole.

2.  In der Konsolenstruktur mit der rechten Maustaste der Website, der Sie Gruppenrichtlinien festlegen möchten.

    **In welchen Bereichen?**

    -   Active Directory-Standorte und-Dienste [*Domänencontrollername. Domänenname*] / Sites/Standort

3.  Klicken Sie auf einen Eintrag im **Gruppenrichtlinienobjekt-Verknüpfungen** , wählen ein vorhandenes Gruppenrichtlinienobjekt (GPO), und klicken Sie dann auf **bearbeiten**. Sie können auch auf **Neu** klicken, um ein neues Gruppenrichtlinienobjekt zu erstellen, und anschließend auf **Bearbeiten** klicken.

4.  Klicken Sie in der Konsolenstruktur auf **Richtlinien für Softwareeinschränkung**.

    **WHERE**

    -   *Gruppenrichtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration oder

        User Configuration/Windows-Einstellungen/Sicherheitseinstellungen Settings/Richtlinien für Softwareeinschränkung

> [!NOTE]
> -   Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer ein Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein oder Ihnen muss die entsprechende Berechtigung übertragen worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen.
> -   Um die Richtlinieneinstellungen vorgeben, die auf Computern, unabhängig davon, welche Benutzer beim Anmelden, angewendet werden, klicken Sie auf **Computerkonfiguration**.
> -   Um die Richtlinieneinstellungen vorgeben, die für Benutzer angewendet wird, unabhängig davon, welche Computer sie melden Sie sich an, klicken Sie auf **Benutzerkonfiguration**.

## <a name="BKMK_Create_SRP"></a>Erstellen Sie neue Richtlinien für softwareeinschränkung

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Klicken Sie im Menü **Aktion** auf **Neue Richtlinien für Softwareeinschränkung erstellen**.

> [!WARNING]
> -   Abhängig von Ihrer Umgebung sind für das Verfahren verschiedene Administratorrechte erforderlich:
> 
>     -   Bei der Erstellung neuer Softwareeinschränkungsrichtlinien für Ihren lokalen Computer: Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für einen Computer erstellen, der einer Domäne angehört, kann dieses Verfahren von Mitgliedern der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; ausgeführt werden.
> -   Falls für ein Gruppenrichtlinienobjekt (Group Policy Object, GPO) bereits Softwareeinschränkungsrichtlinien erstellt wurden, wird der Befehl **Neue Richtlinien für Softwareeinschränkung erstellen** im Menü **Aktion** nicht angezeigt. Klicken Sie zum Löschen der auf ein Gruppenrichtlinienobjekt angewendeten Softwareeinschränkungsrichtlinien in der Konsolenstruktur mit der rechten Maustaste auf **Richtlinien für Softwareeinschränkung**, und klicken Sie anschließend auf **Richtlinien für Softwareeinschränkungen löschen**. Wenn Sie Richtlinien für softwareeinschränkung für ein Gruppenrichtlinienobjekt löschen, löschen Sie auch alle Softwareeinschränkungsregeln Richtlinien für das Gruppenrichtlinienobjekt ein. Nach dem Löschen der Softwareeinschränkungsrichtlinien können Sie neue Softwareeinschränkungsrichtlinien für das Gruppenrichtlinienobjekt erstellen.

## <a name="BKMK_Add_Del"></a>Hinzufügen oder Löschen eines designierten Dateityps

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Designierte Dateitypen**.

3.  Führen Sie eine der folgenden Aktionen aus:

    -   Geben Sie zum Hinzufügen eines Dateityps unter **Dateinamenerweiterung** die Dateinamenerweiterung ein, und klicken Sie dann auf **Hinzufügen**.

    -   Klicken Sie zum Löschen eines Dateityps unter **Designierte Dateitypen** auf den Dateityp, und klicken Sie dann auf **Entfernen**.

> [!NOTE]
> -   Abhängig von der Umgebung, in der Sie einen designierten Dateityp hinzufügen oder entfernen, sind für das Verfahren verschiedene Administratorrechte erforderlich:
> 
>     -   Beim Hinzufügen bzw. Löschen eines designierten Dateityps für Ihren lokalen Computer: Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für einen Computer erstellen, der einer Domäne angehört, kann dieses Verfahren von Mitgliedern der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; ausgeführt werden.
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Die Liste der designierten Dateitypen wird von allen Regeln für Computer Configuration und User Configuration für ein Gruppenrichtlinienobjekt verwendet.

## <a name="BKMK_Prevent_Admin"></a>Um zu verhindern, dass Softwareeinschränkungsrichtlinien für lokale Administratoren

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Erzwingen**.

3.  Klicken Sie unter **Richtlinien für Softwareeinschränkung auf folgende Benutzer anwenden** auf **Alle Benutzer außer den lokalen Administratoren**.

> [!WARNING]
> -   Grundvoraussetzung zur Ausführung dieses Vorgangs ist die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Mitgliedschaft.
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Falls Benutzer in Ihrer Organisation in der Regel Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; auf ihren Computern sind, möchten Sie diese Option möglicherweise nicht aktivieren.
> -   Wenn Sie eine Softwareeinschränkungsrichtlinien-Einstellung für den lokalen Computer festlegen, verhindern Sie mithilfe dieses Verfahrens, dass Softwareeinschränkungsrichtlinien auf lokale Administratoren angewendet werden. Wenn Sie eine Softwareeinschränkungsrichtlinien-Einstellung für Ihr Netzwerk definieren, Filtern Sie basierte auf der Mitgliedschaft in Sicherheitsgruppen, die über die Gruppenrichtlinie benutzerrichtlinieneinstellungen.

## <a name="BKMK_Sec_Lvl"></a>So ändern Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Sicherheitsstufen**.

3.  Klicken Sie mit der rechten Maustaste auf die Sicherheitsstufe, die Sie als Standard festlegen möchten, und klicken Sie dann auf **Als Standard**.

> [!CAUTION]
> In bestimmten Verzeichnissen kann es sich negativ auf das Betriebssystem auswirken, wenn Sie als Standardsicherheitsstufe **Nicht erlaubt** festlegen.

> [!NOTE]
> -   Abhängig von der Umgebung, für die Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien ändern, sind für das Verfahren verschiedene Administratorrechte erforderlich:
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für dieses Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Im Detailbereich ist die aktuelle Standardsicherheitsstufe durch einen schwarzen Kreis mit einem Häkchen angegeben. Wenn Sie mit der rechten Maustaste auf die aktuelle Standardsicherheitsstufe klicken, wird der Befehl **Als Standard** nicht im Menü angezeigt.
> -   Richtlinien für die Softwareeinschränkungsregeln werden erstellt, um Ausnahmen für die Standardsicherheitsstufe anzugeben. Wenn als Standardsicherheitsstufe **Nicht eingeschränkt** festgelegt ist, kann mit Regeln Software angegeben werden, die nicht ausgeführt werden darf. Wenn als Standardsicherheitsstufe **Nicht erlaubt** festgelegt ist, kann mit Regeln Software angegeben werden, die ausgeführt werden darf.
> -   Bei der Installation wird die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien für alle Dateien im System auf **Nicht eingeschränkt** festgelegt.

## <a name="BKMK_Apply_SRP_DLLs"></a>Anwenden von Softwareeinschränkungsrichtlinien auf DLLs

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Erzwingen**.

3.  Klicken Sie unter **Richtlinien für Softwareeinschränkung anwenden auf** auf **Alle Softwaredateien**.

> [!NOTE]
> -   Um diese Schritte ausführen zu können, müssen Sie auf dem lokalen Computer ein Mitglied der Gruppe %%amp;quot;Administratoren%%amp;quot; sein oder Ihnen muss die entsprechende Berechtigung übertragen worden sein. Wenn der Computer zu einer Domäne gehört, können möglicherweise Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren ausführen.
> -   Standardmäßig werden Dynamic Link Libraries (DLLs) von Softwareeinschränkungsrichtlinien nicht überprüft. Die Überprüfung von DLLs kann die Systemleistung beeinträchtigen, da Softwareeinschränkungsrichtlinien bei jedem Laden einer DLL ausgewertet werden müssen. Sie können DLLs jedoch überprüfen, wenn Sie Bedenken bzgl. eines DLL-Virus haben. Wenn die Standardsicherheitsstufe, um festgelegt ist **nicht erlaubt**, und Sie aktivieren die DLL überprüfen, müssen softwareeinschränkungen Richtlinien Sie Regeln erstellen, mit denen jede DLL-Datei ausführen können.


