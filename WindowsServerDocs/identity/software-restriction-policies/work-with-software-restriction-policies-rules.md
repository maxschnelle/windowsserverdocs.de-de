---
title: Arbeiten mit Regeln der Richtlinien für die Softwareeinschränkung
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 4a8047d5-9bb9-4bed-bc8f-583a237731e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 619564d618ba542e915f19ba69884a48652c8bbc
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87952976"
---
# <a name="work-with-software-restriction-policies-rules"></a>Arbeiten mit Regeln der Richtlinien für die Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden Verfahren zum Arbeiten mit Zertifikaten, Pfaden, Internet Zonen und Hash Regeln mithilfe von Richtlinien für Software Einschränkung beschrieben.

## <a name="introduction"></a>Einführung
Mit Richtlinien für Software Einschränkung können Sie Ihre Computerumgebung vor nicht vertrauenswürdiger Software schützen, indem Sie identifizieren und angeben, welche Software ausgeführt werden darf. Sie können die Standard Sicherheitsstufe " **uneingeschränkt** " oder "unzulässig" für ein Gruppenrichtlinie Objekt (GPO) definieren, damit Softwarestandard mäßig zugelassen oder **nicht zulässig ist** . Sie können Ausnahmen für diese Standard Sicherheitsstufe vornehmen, indem Sie Regeln für Software Einschränkungs Richtlinien für bestimmte Software erstellen. Wird als Standardsicherheitsstufe beispielsweise **Nicht erlaubt** festgelegt, können Sie Regeln erstellen, die die Ausführung bestimmter Software zulassen. Die Typen von Regeln lauten wie folgt:

-   **Zertifikatregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [Arbeiten mit Zertifikatregeln](#BKMK_Cert_Rules).

-   **Hashregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [Arbeiten mit Hashregeln](#BKMK_Hash_Rules).

-   **Internetzonenregeln**

    Informationen zu Verfahren finden Sie unter [Arbeiten mit Internet Zonen Regeln](#BKMK_Internet_Zone_Rules).

-   **Pfadregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [Arbeiten mit Pfadregeln](#BKMK_Path_Rules).

Informationen zu anderen Aufgaben für die Verwaltung von Richtlinien für Software Einschränkung finden Sie unter [Verwalten von Richtlinien für Software Einschränkung](administer-software-restriction-policies.md).

## <a name="working-with-certificate-rules"></a><a name="BKMK_Cert_Rules"></a>Arbeiten mit Zertifikatregeln
Software Einschränkungs Richtlinien können auch Software anhand ihres Signatur Zertifikats identifizieren. Sie können eine Zertifikatregel erstellen, die Software identifiziert und anschließend ihre Ausführung abhängig von der Sicherheitsstufe zulässt oder verweigert. Sie können Zertifikatregeln beispielsweise verwenden, um Software aus einer vertrauenswürdigen Quelle in einer Domäne automatisch ohne Benutzeraufforderung zu vertrauen. Sie können mithilfe von Zertifikatregeln auch Dateien in nicht zulässigen Bereichen des Betriebssystems ausführen. Zertifikatregeln sind nicht standardmäßig aktiviert.

Wenn Regeln für die Domäne mithilfe von Gruppenrichtlinie erstellt werden, müssen Sie über Berechtigungen zum Erstellen oder Ändern eines Gruppenrichtlinie Objekts verfügen. Beim Erstellen von Regeln für den lokalen Computer benötigen Sie Administratorrechte für diesen Computer.

#### <a name="to-create-a-certificate-rule"></a>So erstellen Sie eine Zertifikatregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Klicken Sie in der Konsolen Struktur oder im Detailbereich mit der rechten Maustaste auf **zusätzliche Regeln**, und klicken Sie dann auf **neue Zertifikat Regel**.

3.  Klicken Sie auf **Durchsuchen**, und wählen Sie ein Zertifikat oder eine signierte Datei aus.

4.  Klicken Sie unter **Sicherheitsstufe**auf nicht **zulässig** oder **uneingeschränkt**.

5.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.

> [!NOTE]
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Zertifikatregeln sind nicht standardmäßig aktiviert.
> -   Zertifikatregeln wirken sich nur auf die Dateitypen aus, die im Detailbereich von %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; unter **Designierte Dateitypen** aufgeführt sind. Dort finden Sie eine Liste der designierten Dateitypen, die für alle Regeln gilt.
> -   Damit Richtlinien für Software Einschränkung wirksam werden, müssen Benutzer die Richtlinien Einstellungen aktualisieren, indem Sie sich von abmelden und sich bei ihren Computern anmelden.
> -   Wenn mehr als eine Regel für Software Einschränkungs Richtlinien auf Richtlinien Einstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

### <a name="enabling-certificate-rules"></a>Aktivieren von Zertifikatregeln
Abhängig von Ihrer Umgebung stehen verschiedene Vorgehensweisen zum Aktivieren von Zertifikatregeln zur Verfügung:

-   [Für den lokalen Computer](#BKMK_1)

-   [Für ein Gruppenrichtlinie Objekt, und Sie befinden sich auf einem Server, der einer Domäne hinzugefügt wird.](#BKMK_2)

-   [Für ein Gruppenrichtlinie Objekt, und Sie befinden sich auf einem Domänen Controller oder auf einer Arbeitsstation, auf der die Remoteserver-Verwaltungstools installiert ist.](#BKMK_3)

-   [Nur für Domänen Controller, und Sie befinden sich auf einem Domänen Controller oder auf einer Arbeitsstation, auf der das Remoteserver-Verwaltungstools Pack installiert ist.](#BKMK_4)

#### <a name="to-enable-certificate-rules-for-your-local-computer"></a><a name="BKMK_1"></a>So aktivieren Sie Zertifikat Regeln für den lokalen Computer

1.  Öffnen Sie %%amp;quot;Lokale Sicherheitseinstellungen%%amp;quot;.

2.  Klicken Sie in der Konsolen Struktur unter Sicherheitseinstellungen/Lokale Richtlinien auf **Sicherheitsoptionen** .

3.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatsregeln zur Durchsetzung von Softwareeinschränkungsrichtlinien auf Windows-Programme anwenden**.

4.  Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

#### <a name="to-enable-certificate-rules-for-a-group-policy-object-and-you-are-on-a-server-that-is-joined-to-a-domain"></a><a name="BKMK_2"></a>So aktivieren Sie Zertifikat Regeln für ein Gruppenrichtlinie Objekt, und Sie befinden sich auf einem Server, der einer Domäne hinzugefügt wird

1.  Öffnen Sie die Microsoft Management Console (MMC).

2.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**, und klicken Sie dann auf **Hinzufügen**.

3.  Klicken Sie auf **Lokaler Gruppenrichtlinienobjekt-Editor** und anschließend auf **Hinzufügen**.

4.  Klicken Sie unter **Gruppenrichtlinienobjekt auswählen** auf **Durchsuchen**.

5.  Wählen Sie in **nach einem Gruppenrichtlinie Objekt suchen**ein Gruppenrichtlinie Objekt (GPO) in der entsprechenden Domäne, Site oder Organisationseinheit aus, oder erstellen Sie ein neues, und klicken Sie dann auf **Fertig**stellen.

6.  Klicken Sie auf **Schließen** und dann auf **OK**.

7.  Klicken Sie in der Konsolen Struktur auf **Sicherheitsoptionen** , die sich unter *GroupPolicyObject* [*Computername*] Richtlinie/Computer Konfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Lokale Richtlinien/befinden.

8.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatsregeln zur Durchsetzung von Softwareeinschränkungsrichtlinien auf Windows-Programme anwenden**.

9. Wurde diese Richtlinieneinstellung noch nicht definiert, aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

10. Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

#### <a name="to-enable-certificate-rules-for-a-group-policy-object-and-you-are-on-a-domain-controller-or-on-a-workstation-that-has-the-remote-server-administration-tools-installed"></a><a name="BKMK_3"></a>So aktivieren Sie Zertifikat Regeln für ein Gruppenrichtlinie Objekt, und Sie befinden sich auf einem Domänen Controller oder einer Arbeitsstation, auf der die Remoteserver-Verwaltungstools installiert ist

1.  Öffnen Sie „Active Directory-Benutzer und -Computer“.

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, für das Zertifikatregeln aktiviert werden sollen.

3.  Klicken Sie auf **Eigenschaften** und dann auf die Registerkarte **Gruppenrichtlinie**.

4.  Klicken Sie auf **Bearbeiten**, um das zu bearbeitende Gruppenrichtlinienobjekt zu öffnen. Sie können auch auf **Neu** klicken, um ein neues Gruppenrichtlinienobjekt zu erstellen, und anschließend auf **Bearbeiten** klicken.

5.  Klicken Sie in der Konsolen Struktur auf **Sicherheitsoptionen** , die sich unter *GroupPolicyObject*[*Computername*] Richtlinie/Computer Konfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Lokale Richtlinien befinden.

6.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatsregeln zur Durchsetzung von Softwareeinschränkungsrichtlinien auf Windows-Programme anwenden**.

7.  Wurde diese Richtlinieneinstellung noch nicht definiert, aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

8.  Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

#### <a name="to-enable-certificate-rules-for-only-domain-controllers-and-you-are-on-a-domain-controller-or-on-a-workstation-that-has-the-remote-server-administration-tools-installed"></a><a name="BKMK_4"></a>So aktivieren Sie Zertifikat Regeln nur für Domänen Controller, und Sie befinden sich auf einem Domänen Controller oder einer Arbeitsstation, auf der die Remoteserver-Verwaltungstools installiert ist

1.  Öffnen Sie die Domänencontroller-Sicherheitseinstellungen.

2.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** (unter Richtlinie *Gruppenrichtlinienobjekt* für [*Computername*]/Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Lokale Richtlinien).

3.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatsregeln zur Durchsetzung von Softwareeinschränkungsrichtlinien auf Windows-Programme anwenden**.

4.  Wurde diese Richtlinieneinstellung noch nicht definiert, aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

5.  Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

> [!NOTE]
> Sie müssen dieses Verfahren ausführen, damit Zertifikatregeln wirksam werden.

### <a name="set-trusted-publisher-options"></a>Festlegen von Optionen für vertrauenswürdige Verleger
Immer mehr Softwareherausgeber und Anwendungsentwickler verwenden Softwaresignierung, um zu bestätigen, dass ihre Anwendungen aus einer vertrauenswürdigen Quelle stammen. Viele Benutzer kennen jedoch die mit den installierten Anwendungen verbundenen Signaturzertifikate nicht oder schenken diesen wenig Beachtung.

Mit den Richtlinieneinstellungen auf der Registerkarte **Vertrauenswürdige Herausgeber** der Richtlinie für die Validierung des Zertifikatpfads können Administratoren steuern, welche Zertifikate akzeptiert werden können, da sie von einem vertrauenswürdigen Herausgeber stammen.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-local-computer"></a>So konfigurieren Sie die Richtlinieneinstellungen für vertrauenswürdige Herausgeber für einen lokalen Computer

1.  Geben Sie auf dem **Start** Bildschirm**gpeer dit. msc** ein, und drücken Sie dann die EINGABETASTE.

2.  Klicken Sie in der Konsolenstruktur unter **Richtlinie für %%amp;quot;Lokaler Computer%%amp;quot;\Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen** auf **Richtlinien öffentlicher Schlüssel**.

3.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

4.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**, wählen Sie die gewünschten Richtlinienoptionen aus, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-domain"></a>So konfigurieren Sie die Richtlinieneinstellungen für vertrauenswürdige Herausgeber für eine Domäne

1.  Öffnen Sie **Gruppenrichtlinienverwaltung**.

2.  Doppelklicken Sie in der Konsolen Struktur auf **Gruppenrichtlinie Objekte** in der Gesamtstruktur und Domäne, die das **Standard Domänen Richtlinien** -Gruppenrichtlinie Objekt (GPO) enthält, das Sie bearbeiten möchten.

3.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt **Standarddomänenrichtlinie**, und klicken Sie dann auf **Bearbeiten**.

4.  Klicken Sie in der Konsolenstruktur unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen** auf **Richtlinien öffentlicher Schlüssel**.

5.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

6.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**, wählen Sie die gewünschten Richtlinienoptionen aus, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-local-computer"></a>So lassen Sie nur für Administratoren das Verwalten von Zertifikaten, die für Codesignaturen verwendet werden, für einen lokalen Computer zu

1.  Geben Sie auf dem **Start** Bildschirm auf dem Desktop in den **Programmen Programme/Dateien durchsuchen den Text** **gpeer dit. msc** ein, und drücken Sie dann die EINGABETASTE.

2.  Doppelklicken Sie in der Konsolenstruktur unter **Standarddomänenrichtlinie** oder **Richtlinie für "Lokaler Computer"** auf **Computerkonfiguration**, **Windows-Einstellungen** und **Sicherheitseinstellungen**, und klicken Sie dann auf **Richtlinien öffentlicher Schlüssel**.

3.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

4.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

5.  Klicken Sie unter **Verwaltung von vertrauenswürdigen Herausgebern** auf **Nur Administratoren sind berechtigt, %%amp;quot;Vertrauenswürdige Herausgeber%%amp;quot; zu verwalten**, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-domain"></a>So lassen Sie nur für Administratoren das Verwalten von Zertifikaten, die für Codesignaturen verwendet werden, für eine Domäne zu

1.  Öffnen Sie **Gruppenrichtlinienverwaltung**.

2.  Doppelklicken Sie in der Konsolen Struktur auf **Gruppenrichtlinie Objekte** in der Gesamtstruktur und Domäne, die das **Standard Domänen Richtlinien** -Gruppenrichtlinien Objekt enthält, das Sie bearbeiten möchten.

3.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt **Standarddomänenrichtlinie**, und klicken Sie dann auf **Bearbeiten**.

4.  Klicken Sie in der Konsolenstruktur unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen** auf **Richtlinien öffentlicher Schlüssel**.

5.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

6.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**, implementieren Sie die gewünschten Änderungen, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

## <a name="working-with-hash-rules"></a><a name="BKMK_Hash_Rules"></a>Arbeiten mit Hashregeln
Ein Hash ist eine Reihe von Bytes mit einer festen Länge, der eindeutig ein Softwareprogramm oder eine Datei angibt. Der Hash wird durch einen Hashalgorithmus berechnet. Wenn für ein Softwareprogramm eine Hashregel erstellt wird, wird von den Softwareeinschränkungsrichtlinien ein Hash des Programms berechnet. Wenn ein Benutzer versucht, ein Softwareprogramm zu öffnen, wird ein Hash des Programms mit vorhandenen Hashregeln für Softwareeinschränkungsrichtlinien verglichen. Der Hash eines Softwareprogramms ist immer gleich, unabhängig vom Speicherort des Programms auf dem Computer. Wird ein Softwareprogramm jedoch in irgendeiner Weise geändert, ändert sich auch sein Hash. Er entspricht dann nicht mehr dem Hash in der Hashregel für Softwareeinschränkungsrichtlinien.

Sie können beispielsweise eine Hashregel erstellen und als Sicherheitsstufe **Nicht erlaubt** festlegen, um die Ausführung einer bestimmten Datei durch Benutzer zu verhindern. Eine Datei kann umbenannt oder in einen anderen Ordner verschoben werden – der Hash bleibt derselbe. Durch Änderungen an der Datei selbst ändert sich jedoch auch der Hashwert, und die Datei kann dadurch Einschränkungen umgehen.

#### <a name="to-create-a-hash-rule"></a>So erstellen Sie eine Hashregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Klicken Sie in der Konsolen Struktur oder im Detailbereich mit der rechten Maustaste auf **zusätzliche Regeln**, und klicken Sie dann auf **neue Hashregel**.

3.  Klicken Sie auf **Durchsuchen** , um eine Datei zu suchen.

    > [!NOTE]
    > In Windows XP kann ein vorab berechneter Hash in den **Dateihash**eingefügt werden. In Windows Server 2008 R2, Windows 7 und höheren Versionen ist diese Option nicht verfügbar.

4.  Klicken Sie unter **Sicherheitsstufe**auf nicht **zulässig** oder **uneingeschränkt**.

5.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.

> [!NOTE]
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Hashregeln können für Viren oder Trojaner erstellt werden, um ihre Ausführung zu verhindern.
> -   Wenn Sie möchten, dass andere Benutzer eine Hashregel verwenden, damit ein Virus nicht ausgeführt werden kann, berechnen Sie den Hash des Virus mithilfe von Richtlinien für Software Einschränkung, und senden Sie dann den Hashwert an die anderen Personen. Niemals eine e-Mail an den Virus selbst senden.
> -   Wenn ein Virus per e-Mail gesendet wurde, können Sie auch eine Pfadregel erstellen, um die Ausführung von e-Mail-Anlagen zu verhindern.
> -   Eine umbenannte oder in einen anderen Ordner verschobene Datei ergibt denselben Hash. Jede Änderung an der Datei selbst führt zu einem anderen Hash.
> -   Hashregeln wirken sich nur auf die Dateitypen aus, die im Detailbereich von %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; unter **Designierte Dateitypen** aufgeführt sind. Dort finden Sie eine Liste der designierten Dateitypen, die für alle Regeln gilt.
> -   Damit Richtlinien für Software Einschränkung wirksam werden, müssen Benutzer die Richtlinien Einstellungen aktualisieren, indem Sie sich von abmelden und sich bei ihren Computern anmelden.
> -   Wenn mehr als eine Regel für Software Einschränkungs Richtlinien auf Richtlinien Einstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

## <a name="working-with-internet-zone-rules"></a><a name="BKMK_Internet_Zone_Rules"></a>Arbeiten mit Internet Zonen Regeln
Internetzonenregeln gelten nur für Windows Installer-Pakete. Mit einer Zonenregel kann Software aus einer durch Internet Explorer angegebenen Zone identifiziert werden. Diese Zonen sind %%amp;quot;Internet%%amp;quot;, %%amp;quot;Lokales Intranet%%amp;quot;, %%amp;quot;Eingeschränkte Sites%%amp;quot;, %%amp;quot;Vertrauenswürdige Sites%%amp;quot; und %%amp;quot;Eigener Computer%%amp;quot;. Eine Internet Zonen Regel ist so konzipiert, dass Benutzer das herunterladen und Installieren von Software verhindern können.

#### <a name="to-create-an-internet-zone-rule"></a>So erstellen Sie eine Internetzonenregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Klicken Sie in der Konsolen Struktur oder im Detailbereich mit der rechten Maustaste auf **zusätzliche Regeln**, und klicken Sie dann auf **neue Internet Zonen Regel**.

3.  Klicken Sie unter **Internetzone** auf eine Internetzone.

4.  Klicken Sie unter **Sicherheitsstufe**auf nicht **zugelassen** oder **uneingeschränkt**, und klicken Sie dann auf **OK**.

> [!NOTE]
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Zonenregeln gelten nur für Dateien mit der Erweiterung %%amp;quot;.msi%%amp;quot;. Dabei handelt es sich um Windows Installer-Pakete.
> -   Damit Richtlinien für Software Einschränkung wirksam werden, müssen Benutzer die Richtlinien Einstellungen aktualisieren, indem Sie sich von abmelden und sich bei ihren Computern anmelden.
> -   Wenn mehr als eine Regel für Software Einschränkungs Richtlinien auf Richtlinien Einstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

## <a name="working-with-path-rules"></a><a name="BKMK_Path_Rules"></a>Arbeiten mit Pfadregeln
Eine Pfadregel identifiziert Software anhand des Dateipfads. Wenn auf einem Computer beispielsweise die Standardsicherheitsstufe **Nicht erlaubt** festgelegt ist, können Sie jedem Benutzer dennoch unbeschränkten Zugriff auf einen bestimmten Ordner gewähren. Sie können eine Pfadregel erstellen, indem Sie den Dateipfad verwenden und als Sicherheitsstufe der Pfadregel **Nicht eingeschränkt** festlegen. Häufig verwendete Pfade für diesen Regeltyp: %userprofile%, %windir%, %appdata%, %programfiles%, und %temp%. Außerdem können Sie Registrierungspfadregeln erstellen, die den Registrierungsschlüssel der Software als Pfad verwenden.

Da diese Regeln anhand des Pfads angegeben werden, gilt die Pfadregel nicht mehr, wenn ein Softwareprogramm verschoben wird.

#### <a name="to-create-a-path-rule"></a>So erstellen Sie eine Pfadregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  Klicken Sie in der Konsolen Struktur oder im Detailbereich mit der rechten Maustaste auf **zusätzliche Regeln**, und klicken Sie dann auf **neue Pfadregel**.

3.  Geben Sie unter **Pfad** den Pfad ein, oder klicken Sie zum Suchen einer Datei oder eines Ordners auf **Durchsuchen**.

4.  Klicken Sie unter **Sicherheitsstufe**auf nicht **zulässig** oder **uneingeschränkt**.

5.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.

> [!CAUTION]
> -   In bestimmten Ordnern, z. b. im Windows-Ordner, kann das Festlegen der Sicherheitsstufe auf "nicht **zulässig** " die Betriebssystem Vorgänge beeinträchtigen. Stellen Sie sicher, dass die Ausführung einer wichtigen Komponente des Betriebssystems oder eines davon abhängigen Programms nicht verhindert wird.

> [!NOTE]
> -   Möglicherweise müssen neue Softwareeinschränkungsrichtlinien für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Wenn Sie eine Pfadregel für Software mit der Sicherheitsstufe **Nicht erlaubt** erstellen, können Benutzer die Software dennoch ausführen, indem sie sie an einen anderen Speicherort kopieren.
> -   Für Pfadregeln sind die Platzhalterzeichen %%amp;quot;*%%amp;quot; und %%amp;quot;?%%amp;quot; zulässig.
> -   In Pfadregeln können Umgebungsvariablen wie %%amp;quot;%programfiles%%%amp;quot; oder %%amp;quot;%systemroot%%%amp;quot; verwendet werden.
> -   Wenn Sie eine Pfadregel für Software erstellen möchten und nicht wissen, wo sie auf dem Computer gespeichert ist, aber den Registrierungsschlüssel besitzen, können Sie eine Registrierungspfadregel erstellen.
> -   Damit Benutzer keine e-Mail-Anhänge ausführen können, können Sie eine Pfadregel für das Anlagen Verzeichnis Ihres e-Mail-Programms erstellen, das verhindert, dass Benutzer e-Mail-Anhänge ausführen
> -   Pfadregeln wirken sich nur auf die Dateitypen aus, die im Detailbereich von %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; unter **Designierte Dateitypen** aufgeführt sind. Dort finden Sie eine Liste der designierten Dateitypen, die für alle Regeln gilt.
> -   Damit Richtlinien für Software Einschränkung wirksam werden, müssen Benutzer die Richtlinien Einstellungen aktualisieren, indem Sie sich von abmelden und sich bei ihren Computern anmelden.
> -   Wenn mehr als eine Regel für Software Einschränkungs Richtlinien auf Richtlinien Einstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

#### <a name="to-create-a-registry-path-rule"></a>So erstellen Sie eine Registrierungspfaddatei

1.  Geben Sie auf dem Bildschirm **Start** den Befehl regedit ein.

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf den Registrierungsschlüssel, für den eine Regel erstellt werden soll, und klicken Sie dann auf **Schlüsselnamen kopieren**. Notieren Sie den Wertnamen im Detailbereich.

3.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

4.  Klicken Sie in der Konsolen Struktur oder im Detailbereich mit der rechten Maustaste auf **zusätzliche Regeln**, und klicken Sie dann auf **neue Pfadregel**.

5.  Fügen Sie unter **Pfad**den Namen des Registrierungsschlüssels ein, gefolgt vom Wertnamen.

6.  Schließen Sie den Registrierungs Pfad in Prozentzeichen (%) ein, z. b .% HKEY_LOCAL_MACHINE \software\microsoft\platformsdk\directories\installdir%.

7.  Klicken Sie unter **Sicherheitsstufe**auf nicht **zulässig** oder **uneingeschränkt**.

8.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.


