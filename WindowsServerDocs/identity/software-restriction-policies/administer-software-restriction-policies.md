---
title: Verwalten der Richtlinien für Softwareeinschränkung
description: Windows Server-Sicherheit
ms.prod: windows-server
ms.technology: security-software-restriction-policies
ms.topic: article
ms.assetid: 8cc22093-67d1-47b6-9ddd-4569b6761ce9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 88e745b6951ab27f22cc412ee63f792d30775d14
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855113"
---
# <a name="administer-software-restriction-policies"></a>Verwalten der Richtlinien für Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema für IT-Experten finden Sie Verfahren zum Verwalten von Anwendungs Steuerungs Richtlinien mithilfe von Software Einschränkungs Richtlinien (SRP) ab Windows Server 2008 und Windows Vista.

## <a name="introduction"></a>Einführung
Die Richtlinien für Softwareeinschränkung (Software Restriction Policies, SRP) sind ein auf der Gruppenrichtlinie basierendes Feature, das Softwareprogramme identifiziert, die auf Computern in einer Domäne ausgeführt werden, und die Fähigkeit zur Ausführung dieser Programme steuert. Sie können Richtlinien für Softwareeinschränkung auch verwenden, um eine stark eingeschränkte Konfiguration für Computer zu erstellen, in der Sie ausschließlich die Ausführung explizit angegebener Anwendungen zulassen. Diese sind in Microsoft Active Directory Domain Services und Gruppenrichtlinie integriert, können aber auch auf eigenständigen Computern konfiguriert werden. Weitere Informationen zu SRP finden Sie in den [Richtlinien für Software Einschränkung](software-restriction-policies.md).

Ab Windows Server 2008 R2 und Windows 7 kann Windows AppLocker anstelle von oder in zusammen mit SRP für einen Teil ihrer Anwendungs Steuerungsstrategie verwendet werden.

Dieses Thema enthält:

-   [So öffnen Sie Richtlinien für Software Einschränkung](#BKMK_Open_SRP)

-   [So erstellen Sie neue Richtlinien für Software Einschränkung](#BKMK_Create_SRP)

-   [So können Sie einen bestimmten Dateityp hinzufügen oder löschen](#BKMK_Add_Del)

-   [So verhindern Sie, dass Software Einschränkungs Richtlinien auf lokale Administratoren angewendet werden](#BKMK_Prevent_Admin)

-   [So ändern Sie die Standard Sicherheitsstufe von Software Einschränkungs Richtlinien](#BKMK_Sec_Lvl)

-   [So wenden Sie Richtlinien für Software Einschränkung auf DLLs an](#BKMK_Apply_SRP_DLLs)

Informationen zum Ausführen bestimmter Aufgaben mithilfe von SRP finden Sie in den folgenden Bereichen:

-   [Festlegen der Zulassungs-und Verweigerungs Liste und des Anwendungs Bestands für Richtlinien für Software Einschränkung](determine-allow-deny-list-and-application-inventory-for-software-restriction-policies.md)

-   [Arbeiten mit Regeln der Richtlinien für Softwareeinschränkung](work-with-software-restriction-policies-rules.md)

-   [Verwenden von Richtlinien für Software Einschränkung zum Schutz Ihres Computers vor einem e-Mail-Virus](use-software-restriction-policies-to-help-protect-your-computer-against-an-email-virus.md)

## <a name="to-open-software-restriction-policies"></a><a name="BKMK_Open_SRP"></a>So öffnen Sie Richtlinien für Software Einschränkung

-   [Für den lokalen Computer](#BKMK_1)

-   [Für eine Domäne, Site oder Organisationseinheit, und Sie befinden sich auf einem Mitglieds Server oder einer Arbeitsstation, die mit einer Domäne verknüpft ist](#BKMK_2)

-   [Für eine Domäne oder Organisationseinheit, und Sie befinden sich auf einem Domänen Controller oder einer Arbeitsstation, auf der die Remoteserver-Verwaltungstools installiert ist.](#BKMK_3)

-   [Für einen-Standort und Sie befinden sich auf einem Domänen Controller oder auf einer Arbeitsstation, auf der die-Remoteserver-Verwaltungstools installiert ist.](#BKMK_4)

### <a name="for-your-local-computer"></a><a name="BKMK_1"></a>Für den lokalen Computer

1.  Öffnen Sie %%amp;quot;Lokale Sicherheitseinstellungen%%amp;quot;.

2.  Klicken Sie in der Konsolen Struktur auf **Richtlinien für Software Einschränkung**.

    **Was?**

    -   Sicherheitseinstellungen/Richtlinien für Software Einschränkung

> [!NOTE]
> Um die folgenden Schritte durchführen zu können, müssen Sie als Mitglied der Gruppe „Administratoren“ auf dem lokalen Computer angemeldet sein, oder Ihnen müssen die entsprechenden Rechte übertragen worden sein.

### <a name="for-a-domain-site-or-organizational-unit-and-you-are-on-a-member-server-or-on-a-workstation-that-is-joined-to-a-domain"></a><a name="BKMK_2"></a>Für eine Domäne, Site oder Organisationseinheit, und Sie befinden sich auf einem Mitglieds Server oder einer Arbeitsstation, die mit einer Domäne verknüpft ist

1.  Öffnen Sie die Microsoft Management Console (MMC).

2.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**, und klicken Sie dann auf **Hinzufügen**.

3.  Klicken Sie auf **Lokaler Gruppenrichtlinienobjekt-Editor** und anschließend auf **Hinzufügen**.

4.  Klicken Sie unter **Gruppenrichtlinienobjekt auswählen** auf **Durchsuchen**.

5.  Wählen Sie in **nach einem Gruppenrichtlinie Objekt suchen**ein Gruppenrichtlinie Objekt (GPO) in der entsprechenden Domäne, Site oder Organisationseinheit aus, oder erstellen Sie ein neues, und klicken Sie dann auf **Fertig**stellen.

6.  Klicken Sie auf **Schließen**und dann auf **OK**.

7.  Klicken Sie in der Konsolen Struktur auf **Richtlinien für Software Einschränkung**.

    **Was?**

    -   *Gruppenrichtlinie Objekt* [*Computername*] Richtlinie/Computer Konfiguration oder

        Benutzerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Richtlinien für Software Einschränkung

> [!NOTE]
> Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

### <a name="for-a-domain-or-organizational-unit-and-you-are-on-a-domain-controller-or-on-a-workstation-that-has-the-remote-server-administration-tools-installed"></a><a name="BKMK_3"></a>Für eine Domäne oder Organisationseinheit, und Sie befinden sich auf einem Domänen Controller oder einer Arbeitsstation, auf der die Remoteserver-Verwaltungstools installiert ist.

1.  Öffnen Sie Gruppenrichtlinien-Verwaltungskonsole.

2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf das Gruppenrichtlinie Objekt (GPO), für das Sie Software Einschränkungs Richtlinien öffnen möchten.

3.  Klicken Sie auf **Bearbeiten**, um das zu bearbeitende Gruppenrichtlinienobjekt zu öffnen. Sie können auch auf **Neu** klicken, um ein neues Gruppenrichtlinienobjekt zu erstellen, und anschließend auf **Bearbeiten** klicken.

4.  Klicken Sie in der Konsolen Struktur auf **Richtlinien für Software Einschränkung**.

    **Was?**

    -   *Gruppenrichtlinie Objekt* [*Computername*] Richtlinie/Computer Konfiguration oder

        Benutzerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Richtlinien für Software Einschränkung

> [!NOTE]
> Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe "Domänen-Admins" sein.

### <a name="for-a-site-and-you-are-on-a-domain-controller-or-on-a-workstation-that-has-the-remote-server-administration-tools-installed"></a><a name="BKMK_4"></a>Für einen-Standort und Sie befinden sich auf einem Domänen Controller oder auf einer Arbeitsstation, auf der die-Remoteserver-Verwaltungstools installiert ist.

1.  Öffnen Sie Gruppenrichtlinien-Verwaltungskonsole.

2.  Klicken Sie in der Konsolen Struktur mit der rechten Maustaste auf die Website, für die Sie Gruppenrichtlinie festlegen möchten.

    **Was?**

    -   Active Directory Sites und Dienste [*Domain_Controller_Name. domain_name*]/Sites/Site

3.  Klicken Sie in **Gruppenrichtlinie Objekt Verknüpfungen** auf einen Eintrag, um ein vorhandenes Gruppenrichtlinie Objekt (GPO) auszuwählen, und klicken Sie dann auf **Bearbeiten**. Sie können auch auf **Neu** klicken, um ein neues Gruppenrichtlinienobjekt zu erstellen, und anschließend auf **Bearbeiten** klicken.

4.  Klicken Sie in der Konsolen Struktur auf **Richtlinien für Software Einschränkung**.

    **Wobei**

    -   *Gruppenrichtlinie Objekt* [*Computername*] Richtlinie/Computer Konfiguration oder

        Benutzerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Richtlinien für Software Einschränkung

> [!NOTE]
> -   Um die folgenden Schritte durchführen zu können, müssen Sie als Mitglied der Gruppe „Administratoren“ auf dem lokalen Computer angemeldet sein, oder Ihnen müssen die entsprechenden Rechte übertragen worden sein. Damit Mitglieder der Gruppe „Domänen-Admins“ diese Schritte ausführen zu können, muss der Computer zu einer Domäne gehören.
> -   Wenn Sie Richtlinien Einstellungen festlegen möchten, die auf Computer angewendet werden, klicken Sie auf **Computerkonfiguration**, unabhängig davon, welche Benutzer sich bei Ihnen anmelden.
> -   Um Richtlinien Einstellungen festzulegen, die auf Benutzer angewendet werden, und zwar unabhängig davon, auf welchem Computer Sie sich anmelden, klicken Sie auf **Benutzerkonfiguration**.

## <a name="to-create-new-software-restriction-policies"></a><a name="BKMK_Create_SRP"></a>So erstellen Sie neue Richtlinien für Software Einschränkung

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Klicken Sie im Menü **Aktion** auf **Neue Richtlinien für Softwareeinschränkung erstellen**.

> [!WARNING]
> -   Abhängig von Ihrer Umgebung sind für das Verfahren verschiedene Administratorrechte erforderlich:
> 
>     -   Wenn Sie neue Software Einschränkungs Richtlinien für Ihren lokalen Computer erstellen, müssen Sie mindestens Mitglied der lokalen Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um dieses Verfahren ausführen zu können.
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für einen Computer erstellen, der einer Domäne angehört, kann dieses Verfahren von Mitgliedern der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; ausgeführt werden.
> -   Falls für ein Gruppenrichtlinienobjekt (Group Policy Object, GPO) bereits Softwareeinschränkungsrichtlinien erstellt wurden, wird der Befehl **Neue Richtlinien für Softwareeinschränkung erstellen** im Menü **Aktion** nicht angezeigt. Klicken Sie zum Löschen der auf ein Gruppenrichtlinienobjekt angewendeten Softwareeinschränkungsrichtlinien in der Konsolenstruktur mit der rechten Maustaste auf **Richtlinien für Softwareeinschränkung**, und klicken Sie anschließend auf **Richtlinien für Softwareeinschränkungen löschen**. Wenn Sie Software Einschränkungs Richtlinien für ein GPO löschen, löschen Sie auch alle Regeln für Software Einschränkungs Richtlinien für dieses Gruppenrichtlinien Objekt. Nach dem Löschen der Softwareeinschränkungsrichtlinien können Sie neue Softwareeinschränkungsrichtlinien für das Gruppenrichtlinienobjekt erstellen.

## <a name="to-add-or-delete-a-designated-file-type"></a><a name="BKMK_Add_Del"></a>So können Sie einen bestimmten Dateityp hinzufügen oder löschen

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Designierte Dateitypen**.

3.  Führen Sie eine der folgenden Aktionen aus:

    -   Geben Sie zum Hinzufügen eines Dateityps unter **Dateinamenerweiterung** die Dateinamenerweiterung ein, und klicken Sie dann auf **Hinzufügen**.

    -   Klicken Sie zum Löschen eines Dateityps unter **Designierte Dateitypen** auf den Dateityp, und klicken Sie dann auf **Entfernen**.

> [!NOTE]
> -   Abhängig von der Umgebung, in der Sie einen designierten Dateityp hinzufügen oder entfernen, sind für das Verfahren verschiedene Administratorrechte erforderlich:
> 
>     -   Wenn Sie einen festgelegten Dateityp für den lokalen Computer hinzufügen oder löschen: die Mitgliedschaft in der lokalen Gruppe " **Administratoren** " oder eine entsprechende Gruppe ist mindestens erforderlich, um dieses Verfahren abzuschließen.
>     -   Wenn Sie neue Softwareeinschränkungsrichtlinien für einen Computer erstellen, der einer Domäne angehört, kann dieses Verfahren von Mitgliedern der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; ausgeführt werden.
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Die Liste der vorgesehenen Dateitypen wird von allen Regeln für die Computer Konfiguration und die Benutzerkonfiguration für ein Gruppenrichtlinien Objekt gemeinsam verwendet.

## <a name="to-prevent-software-restriction-policies-from-applying-to-local-administrators"></a><a name="BKMK_Prevent_Admin"></a>So verhindern Sie, dass Software Einschränkungs Richtlinien auf lokale Administratoren angewendet werden

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Erzwingen**.

3.  Klicken Sie unter **Richtlinien für Softwareeinschränkung auf folgende Benutzer anwenden** auf **Alle Benutzer außer den lokalen Administratoren**.

> [!WARNING]
> -   Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in der lokalen Gruppe **Administratoren** oder eine gleichwertige Berechtigung erforderlich.
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Falls Benutzer in Ihrer Organisation in der Regel Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; auf ihren Computern sind, möchten Sie diese Option möglicherweise nicht aktivieren.
> -   Wenn Sie eine Softwareeinschränkungsrichtlinien-Einstellung für den lokalen Computer festlegen, verhindern Sie mithilfe dieses Verfahrens, dass Softwareeinschränkungsrichtlinien auf lokale Administratoren angewendet werden. Wenn Sie eine Software Einschränkungs Richtlinien Einstellung für Ihr Netzwerk definieren, Filtern Sie die Benutzerrichtlinien Einstellungen basierend auf der Mitgliedschaft in Sicherheitsgruppen über Gruppenrichtlinie.

## <a name="to-change-the-default-security-level-of-software-restriction-policies"></a><a name="BKMK_Sec_Lvl"></a>So ändern Sie die Standard Sicherheitsstufe von Software Einschränkungs Richtlinien

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Sicherheitsstufen**.

3.  Klicken Sie mit der rechten Maustaste auf die Sicherheitsstufe, die Sie als Standard festlegen möchten, und klicken Sie dann auf **Als Standard**.

> [!CAUTION]
> In bestimmten Verzeichnissen kann es sich negativ auf das Betriebssystem auswirken, wenn Sie als Standardsicherheitsstufe **Nicht erlaubt** festlegen.

> [!NOTE]
> -   Abhängig von der Umgebung, für die Sie die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien ändern, sind für das Verfahren verschiedene Administratorrechte erforderlich:
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für dieses Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Im Detailbereich ist die aktuelle Standardsicherheitsstufe durch einen schwarzen Kreis mit einem Häkchen angegeben. Wenn Sie mit der rechten Maustaste auf die aktuelle Standardsicherheitsstufe klicken, wird der Befehl **Als Standard** nicht im Menü angezeigt.
> -   Regeln für Software Einschränkungs Richtlinien werden erstellt, um Ausnahmen für die Standard Sicherheitsstufe anzugeben. Wenn als Standardsicherheitsstufe **Nicht eingeschränkt** festgelegt ist, kann mit Regeln Software angegeben werden, die nicht ausgeführt werden darf. Wenn als Standardsicherheitsstufe **Nicht erlaubt** festgelegt ist, kann mit Regeln Software angegeben werden, die ausgeführt werden darf.
> -   Bei der Installation wird die Standardsicherheitsstufe der Softwareeinschränkungsrichtlinien für alle Dateien im System auf **Nicht eingeschränkt** festgelegt.

## <a name="to-apply-software-restriction-policies-to-dlls"></a><a name="BKMK_Apply_SRP_DLLs"></a>So wenden Sie Richtlinien für Software Einschränkung auf DLLs an

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Doppelklicken Sie im Detailbereich auf **Erzwingen**.

3.  Klicken Sie unter **Richtlinien für Softwareeinschränkung anwenden auf** auf **Alle Softwaredateien**.

> [!NOTE]
> -   Um die folgenden Schritte durchführen zu können, müssen Sie als Mitglied der Gruppe „Administratoren“ auf dem lokalen Computer angemeldet sein, oder Ihnen müssen die entsprechenden Rechte übertragen worden sein. Damit Mitglieder der Gruppe „Domänen-Admins“ diese Schritte ausführen zu können, muss der Computer zu einer Domäne gehören.
> -   Standardmäßig werden Dynamic Link Libraries (DLLs) von Softwareeinschränkungsrichtlinien nicht überprüft. Die Überprüfung von DLLs kann die Systemleistung beeinträchtigen, da Softwareeinschränkungsrichtlinien bei jedem Laden einer DLL ausgewertet werden müssen. Sie können DLLs jedoch überprüfen, wenn Sie Bedenken bzgl. eines DLL-Virus haben. Wenn die Standard Sicherheitsstufe auf unzulässig festgelegt ist und Sie die DLL-Überprüfung **aktivieren, müssen**Sie Regeln für Software Einschränkungs Richtlinien erstellen, die die jeweilige dll-Durchführung erlauben.


