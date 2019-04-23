---
title: Arbeiten mit Regeln der Richtlinien für die Softwareeinschränkung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-software-restriction-policies
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a8047d5-9bb9-4bed-bc8f-583a237731e2
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 2dd1810b50f4f02be99eb2e2c0893501f99d1e93
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59844951"
---
# <a name="work-with-software-restriction-policies-rules"></a>Arbeiten mit Regeln der Richtlinien für die Softwareeinschränkung

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema beschreibt Verfahren, die Arbeit mit Zertifikat "," Path "," Internet-Zone und Hash-Regeln, die mithilfe von Richtlinien für Softwareeinschränkung.

## <a name="introduction"></a>Einführung
Mit Richtlinien für softwareeinschränkung können Sie Ihre computerumgebung vor nicht vertrauenswürdiger Software schützen, indem Sie festlegen, welche Software ausgeführt werden darf. Sie können die Standardsicherheitsstufe der definieren **uneingeschränkt** oder **nicht erlaubt** (Group Policy Object, GPO), damit Software entweder erlaubt ist zulässig, wird standardmäßig ausgeführt. Sie können Ausnahmen für diese Standardsicherheitsstufe vornehmen, durch das Erstellen von Softwareeinschränkungsrichtlinien für bestimmte Software Richtlinien Regeln. Wird als Standardsicherheitsstufe beispielsweise **Nicht erlaubt** festgelegt, können Sie Regeln erstellen, die die Ausführung bestimmter Software zulassen. Die Typen von Regeln lauten wie folgt aus:

-   **Zertifikatregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [Arbeiten mit Zertifikatregeln](#BKMK_Cert_Rules).

-   **Hashregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [Arbeiten mit Hashregeln](#BKMK_Hash_Rules).

-   **Internetzonenregeln**

    Anleitungen finden Sie im [arbeiten mit der Zone des Internets Regeln](#BKMK_Internet_Zone_Rules).

-   **Pfadregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [Arbeiten mit Pfadregeln](#BKMK_Path_Rules).

Weitere Informationen über andere Aufgaben zum Verwalten von Richtlinien für Softwareeinschränkung finden Sie unter [Administer Software Restriction Policies](administer-software-restriction-policies.md).

## <a name="BKMK_Cert_Rules"></a>Arbeiten mit Zertifikatregeln
Richtlinien für softwareeinschränkung können auch Software anhand ihres Signaturzertifikats identifizieren. Sie können eine Zertifikatregel erstellen, die Software identifiziert und anschließend ihre Ausführung abhängig von der Sicherheitsstufe zulässt oder verweigert. Sie können Zertifikatregeln beispielsweise verwenden, um Software aus einer vertrauenswürdigen Quelle in einer Domäne automatisch ohne Benutzeraufforderung zu vertrauen. Sie können mithilfe von Zertifikatregeln auch Dateien in nicht zulässigen Bereichen des Betriebssystems ausführen. Zertifikatregeln sind nicht standardmäßig aktiviert.

Wenn Regeln für die Domäne, die mithilfe von Gruppenrichtlinien erstellt werden, müssen Sie Berechtigungen zum Erstellen oder Ändern eines Gruppenrichtlinienobjekts verfügen. Beim Erstellen von Regeln für den lokalen Computer benötigen Sie Administratorrechte für diesen Computer.

#### <a name="to-create-a-certificate-rule"></a>So erstellen Sie eine Zertifikatregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  In der Konsolenstruktur oder im Detailbereich, mit der Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **neue Zertifikatregel**.

3.  Klicken Sie auf **Durchsuchen**, und wählen Sie ein Zertifikat oder eine signierte Datei aus.

4.  In **Sicherheitsstufe**, klicken Sie auf **nicht erlaubt** oder **uneingeschränkt**.

5.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.

> [!NOTE]
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Zertifikatregeln sind nicht standardmäßig aktiviert.
> -   Zertifikatregeln wirken sich nur auf die Dateitypen aus, die im Detailbereich von %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; unter **Designierte Dateitypen** aufgeführt sind. Dort finden Sie eine Liste der designierten Dateitypen, die für alle Regeln gilt.
> -   Richtlinien, für softwareeinschränkung wirksam wird müssen Benutzer die Richtlinieneinstellungen beim Abmelden von und Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Softwareeinschränkungsregel Richtlinien auf die Richtlinieneinstellungen angewendet wird, wird eine Rangfolge der Regeln für das Behandeln von Konflikten.

### <a name="enabling-certificate-rules"></a>Aktivieren von Zertifikatregeln
Abhängig von Ihrer Umgebung stehen verschiedene Vorgehensweisen zum Aktivieren von Zertifikatregeln zur Verfügung:

-   [Für den lokalen computer](#BKMK_1)

-   [Für ein Gruppenrichtlinienobjekt, und Sie auf einem Server befinden, die einer Domäne angehört](#BKMK_2)

-   [Für ein Gruppenrichtlinienobjekt, und Sie befinden sich auf einem Domänencontroller oder eine Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde.](#BKMK_3)

-   [Für nur Domäne sind die Controller, und Sie auf einem Domänencontroller oder auf einer Arbeitsstation, die die Remote Server Administration Tools Pack installiert wurde](#BKMK_4)

#### <a name="BKMK_1"></a>So aktivieren Sie Zertifikatregeln für Ihren lokalen computer

1.  Öffnen Sie %%amp;quot;Lokale Sicherheitseinstellungen%%amp;quot;.

2.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich unter Sicherheitseinstellungen/lokale Richtlinien.

3.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Verwenden von Zertifikatregeln auf ausführbare Windows-Dateien für Richtlinien für Softwareeinschränkung**.

4.  Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

#### <a name="BKMK_2"></a>Sind zum Aktivieren von Zertifikatregeln für ein Gruppenrichtlinienobjekt, und Sie auf einem Server, der einer Domäne angehört

1.  Öffnen Sie die Microsoft Management Console (MMC).

2.  Klicken Sie im Menü **Datei** auf **Snap-In hinzufügen/entfernen**, und klicken Sie dann auf **Hinzufügen**.

3.  Klicken Sie auf **Lokaler Gruppenrichtlinienobjekt-Editor** und anschließend auf **Hinzufügen**.

4.  Klicken Sie unter **Gruppenrichtlinienobjekt auswählen** auf **Durchsuchen**.

5.  In **für ein Gruppenrichtlinienobjekt, das Durchsuchen**, wählen Sie in der entsprechenden Domäne, Site oder Organisationseinheit (Group Policy Object, GPO)- oder ein neues erstellen, und klicken Sie dann auf **Fertig stellen**.

6.  Klicken Sie auf **Schließen**und dann auf **OK**.

7.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich im *Gruppenrichtlinienobjekt* [*ComputerName*] Richtlinie/Computer Configuration/Windows-Einstellungen/Sicherheitseinstellungen / Lokale Richtlinien /.

8.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Verwenden von Zertifikatregeln auf ausführbare Windows-Dateien für Richtlinien für Softwareeinschränkung**.

9. Wurde diese Richtlinieneinstellung noch nicht definiert, aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

10. Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

#### <a name="BKMK_3"></a>Regeln für ein Gruppenrichtlinienobjekt, das Zertifikat zu aktivieren, und Sie sind auf einem Domänencontroller oder auf einer Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde

1.  Öffnen Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;.

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, für das Zertifikatregeln aktiviert werden sollen.

3.  Klicken Sie auf **Eigenschaften** und dann auf die Registerkarte **Gruppenrichtlinie**.

4.  Klicken Sie auf **Bearbeiten**, um das zu bearbeitende Gruppenrichtlinienobjekt zu öffnen. Sie können auch auf **Neu** klicken, um ein neues Gruppenrichtlinienobjekt zu erstellen, und anschließend auf **Bearbeiten** klicken.

5.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich im *Gruppenrichtlinienobjekt*[*ComputerName*] Richtlinie/Computer Configuration/Windows-Einstellungen/Sicherheitseinstellungen / Lokale Richtlinien.

6.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Verwenden von Zertifikatregeln auf ausführbare Windows-Dateien für Richtlinien für Softwareeinschränkung**.

7.  Wurde diese Richtlinieneinstellung noch nicht definiert, aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

8.  Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

#### <a name="BKMK_4"></a>Sind Zertifikatregeln nur für Domänencontroller, und Sie zum Aktivieren auf einem Domänencontroller oder auf einer Arbeitsstation, die den Remoteserver-Verwaltungstools installiert wurde

1.  Öffnen Sie die Domänencontroller-Sicherheitseinstellungen.

2.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** (unter Richtlinie *Gruppenrichtlinienobjekt* für [*Computername*]/Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/Lokale Richtlinien).

3.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Verwenden von Zertifikatregeln auf ausführbare Windows-Dateien für Richtlinien für Softwareeinschränkung**.

4.  Wurde diese Richtlinieneinstellung noch nicht definiert, aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

5.  Führen Sie eine der folgenden Aktionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **Aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **Deaktiviert**.

> [!NOTE]
> Sie müssen dieses Verfahren ausführen, damit Zertifikatregeln wirksam werden.

### <a name="set-trusted-publisher-options"></a>Legen Sie Optionen für vertrauenswürdige Herausgeber
Immer mehr Softwareherausgeber und Anwendungsentwickler verwenden Softwaresignierung, um zu bestätigen, dass ihre Anwendungen aus einer vertrauenswürdigen Quelle stammen. Viele Benutzer kennen jedoch die mit den installierten Anwendungen verbundenen Signaturzertifikate nicht oder schenken diesen wenig Beachtung.

Mit den Richtlinieneinstellungen auf der Registerkarte **Vertrauenswürdige Herausgeber** der Richtlinie für die Überprüfung des Zertifikatpfads können Administratoren steuern, welche Zertifikate akzeptiert werden können, da sie von einem vertrauenswürdigen Herausgeber stammen.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-local-computer"></a>So konfigurieren Sie die Richtlinieneinstellungen für vertrauenswürdige Herausgeber für einen lokalen Computer

1.  Auf der **starten** geben **"Gpedit.msc"** und drücken Sie dann die EINGABETASTE.

2.  Klicken Sie in der Konsolenstruktur unter **Richtlinie für %%amp;quot;Lokaler Computer%%amp;quot;\Computerkonfiguration\Richtlinien\Windows-Einstellungen\Sicherheitseinstellungen** auf **Richtlinien öffentlicher Schlüssel**.

3.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

4.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**, wählen Sie die gewünschten Richtlinienoptionen aus, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-domain"></a>So konfigurieren Sie die Richtlinieneinstellungen für vertrauenswürdige Herausgeber für eine Domäne

1.  Open **Gruppenrichtlinienverwaltung**.

2.  Doppelklicken Sie in der Konsolenstruktur auf **Group Policy Objects** in der Gesamtstruktur und Domäne, enthält die **Default Domain Policy** Gruppe Gruppenrichtlinienobjekt (GPO), die Sie bearbeiten möchten.

3.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt **Standarddomänenrichtlinie**, und klicken Sie dann auf **Bearbeiten**.

4.  Klicken Sie in der Konsolenstruktur unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen** auf **Richtlinien öffentlicher Schlüssel**.

5.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

6.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**, wählen Sie die gewünschten Richtlinienoptionen aus, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-local-computer"></a>So lassen Sie nur für Administratoren das Verwalten von Zertifikaten, die für Codesignaturen verwendet werden, für einen lokalen Computer zu

1.  Auf der **starten** Bildschirm, Typ, **"Gpedit.msc"** in die **Programme / Dateien durchsuchen** oder in Windows 8 auf dem Desktop, und drücken Sie dann die EINGABETASTE.

2.  Doppelklicken Sie in der Konsolenstruktur unter **Standarddomänenrichtlinie** oder **Richtlinie für "Lokaler Computer"** auf **Computerkonfiguration**, **Windows-Einstellungen** und **Sicherheitseinstellungen**, und klicken Sie dann auf **Richtlinien öffentlicher Schlüssel**.

3.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

4.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**.

5.  Klicken Sie unter **Verwaltung von vertrauenswürdigen Herausgebern** auf **Nur Administratoren sind berechtigt, %%amp;quot;Vertrauenswürdige Herausgeber%%amp;quot; zu verwalten**, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-domain"></a>So lassen Sie nur für Administratoren das Verwalten von Zertifikaten, die für Codesignaturen verwendet werden, für eine Domäne zu

1.  Open **Gruppenrichtlinienverwaltung**.

2.  Doppelklicken Sie in der Konsolenstruktur auf **Group Policy Objects** in der Gesamtstruktur und Domäne, enthält die **Default Domain Policy** Gruppenrichtlinienobjekt, das Sie bearbeiten möchten.

3.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt **Standarddomänenrichtlinie**, und klicken Sie dann auf **Bearbeiten**.

4.  Klicken Sie in der Konsolenstruktur unter **Computerkonfiguration\Windows-Einstellungen\Sicherheitseinstellungen** auf **Richtlinien öffentlicher Schlüssel**.

5.  Doppelklicken Sie auf **Einstellungen für die Überprüfung des Zertifikatpfades**, und klicken Sie dann auf die Registerkarte **Vertrauenswürdige Herausgeber**.

6.  Aktivieren Sie das Kontrollkästchen **Diese Richtlinieneinstellungen definieren**, implementieren Sie die gewünschten Änderungen, und klicken Sie dann auf **OK**, um die neuen Einstellungen zu übernehmen.

## <a name="BKMK_Hash_Rules"></a>Arbeiten mit Hashregeln
Ein Hash ist eine Reihe von Bytes mit einer festen Länge, der eindeutig ein Softwareprogramm oder eine Datei angibt. Der Hash wird durch einen Hashalgorithmus berechnet. Wenn für ein Softwareprogramm eine Hashregel erstellt wird, wird von den Softwareeinschränkungsrichtlinien ein Hash des Programms berechnet. Wenn ein Benutzer versucht, ein Softwareprogramm zu öffnen, wird ein Hash des Programms mit vorhandenen Hashregeln für Softwareeinschränkungsrichtlinien verglichen. Der Hash eines Softwareprogramms ist immer gleich, unabhängig vom Speicherort des Programms auf dem Computer. Wird ein Softwareprogramm jedoch in irgendeiner Weise geändert, ändert sich auch sein Hash. Er entspricht dann nicht mehr dem Hash in der Hashregel für Softwareeinschränkungsrichtlinien.

Sie können beispielsweise eine Hashregel erstellen und als Sicherheitsstufe **Nicht erlaubt** festlegen, um die Ausführung einer bestimmten Datei durch Benutzer zu verhindern. Eine Datei kann umbenannt oder in einen anderen Ordner verschoben werden – der Hash bleibt derselbe. Durch Änderungen an der Datei selbst ändert sich jedoch auch der Hashwert, und die Datei kann dadurch Einschränkungen umgehen.

#### <a name="to-create-a-hash-rule"></a>So erstellen Sie eine Hashregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  In der Konsolenstruktur oder im Detailbereich, mit der Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **Neue Hashregel**.

3.  Klicken Sie auf **Durchsuchen** um eine Datei zu suchen.

    > [!NOTE]
    > In Windows XP ist es möglich, fügen Sie einen vorab berechneten Hash in **Dateihash**. In Windows Server 2008 R2, Windows 7 und höher ist diese Option nicht verfügbar.

4.  In **Sicherheitsstufe**, klicken Sie auf **nicht erlaubt** oder **uneingeschränkt**.

5.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.

> [!NOTE]
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Hashregeln können für Viren oder Trojaner erstellt werden, um ihre Ausführung zu verhindern.
> -   Wenn Sie möchten anderen Personen eine Hashregel verwenden, sodass ein Virus nicht ausgeführt werden kann, berechnen Sie den Hash des Virus mithilfe von Richtlinien für softwareeinschränkung und dann per e-mail den Hashwert an die andere Personen. Versenden Sie niemals den Virus selbst.
> -   Wenn ein Virus per E-mail gesendet wurde, können Sie auch eine Pfadregel, um zu verhindern, dass bei der Ausführung von e-Mail-Anlagen erstellen.
> -   Eine umbenannte oder in einen anderen Ordner verschobene Datei ergibt denselben Hash. Jede Änderung an der Datei selbst führt zu einem anderen Hash.
> -   Hashregeln wirken sich nur auf die Dateitypen aus, die im Detailbereich von %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; unter **Designierte Dateitypen** aufgeführt sind. Dort finden Sie eine Liste der designierten Dateitypen, die für alle Regeln gilt.
> -   Richtlinien, für softwareeinschränkung wirksam wird müssen Benutzer die Richtlinieneinstellungen beim Abmelden von und Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Softwareeinschränkungsregel Richtlinien auf die Richtlinieneinstellungen angewendet wird, wird eine Rangfolge der Regeln für das Behandeln von Konflikten.

## <a name="BKMK_Internet_Zone_Rules"></a>Arbeiten mit der Zone des Internets-Regeln
Internetzonenregeln gelten nur für Windows Installer-Pakete. Mit einer Zonenregel kann Software aus einer durch Internet Explorer angegebenen Zone identifiziert werden. Diese Zonen sind %%amp;quot;Internet%%amp;quot;, %%amp;quot;Lokales Intranet%%amp;quot;, %%amp;quot;Eingeschränkte Sites%%amp;quot;, %%amp;quot;Vertrauenswürdige Sites%%amp;quot; und %%amp;quot;Eigener Computer%%amp;quot;. Eine Internetzonenregel soll verhindern, dass Benutzer Software herunterladen und installieren.

#### <a name="to-create-an-internet-zone-rule"></a>So erstellen Sie eine Internetzonenregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  In der Konsolenstruktur oder im Detailbereich, mit der Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **Neue Internetzonenregel**.

3.  Klicken Sie unter **Internetzone** auf eine Internetzone.

4.  In **Sicherheitsstufe**, klicken Sie auf **nicht erlaubt** oder **uneingeschränkt**, und klicken Sie dann auf **OK**.

> [!NOTE]
> -   Möglicherweise muss eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Zonenregeln gelten nur für Dateien mit der Erweiterung %%amp;quot;.msi%%amp;quot;. Dabei handelt es sich um Windows Installer-Pakete.
> -   Richtlinien, für softwareeinschränkung wirksam wird müssen Benutzer die Richtlinieneinstellungen beim Abmelden von und Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Softwareeinschränkungsregel Richtlinien auf die Richtlinieneinstellungen angewendet wird, wird eine Rangfolge der Regeln für das Behandeln von Konflikten.

## <a name="BKMK_Path_Rules"></a>Arbeiten mit Pfadregeln
Eine Pfadregel identifiziert Software anhand des Dateipfads. Wenn auf einem Computer beispielsweise die Standardsicherheitsstufe **Nicht erlaubt** festgelegt ist, können Sie jedem Benutzer dennoch unbeschränkten Zugriff auf einen bestimmten Ordner gewähren. Sie können eine Pfadregel erstellen, indem Sie den Dateipfad verwenden und als Sicherheitsstufe der Pfadregel **Nicht eingeschränkt** festlegen. Häufig verwendete Pfade für diesen Regeltyp: %userprofile%, %windir%, %appdata%, %programfiles%, und %temp%. Außerdem können Sie Registrierungspfadregeln erstellen, die den Registrierungsschlüssel der Software als Pfad verwenden.

Da diese Regeln anhand des Pfads angegeben werden, gilt die Pfadregel nicht mehr, wenn ein Softwareprogramm verschoben wird.

#### <a name="to-create-a-path-rule"></a>So erstellen Sie eine Pfadregel

1.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

2.  In der Konsolenstruktur oder im Detailbereich, mit der Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **neue Pfadregel**.

3.  Geben Sie unter **Pfad** den Pfad ein, oder klicken Sie zum Suchen einer Datei oder eines Ordners auf **Durchsuchen**.

4.  In **Sicherheitsstufe**, klicken Sie auf **nicht erlaubt** oder **uneingeschränkt**.

5.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.

> [!CAUTION]
> -   In bestimmten Ordnern, z. B. die Windows-Ordner, durch Festlegen der Sicherheits auf **nicht erlaubt** kann sich negativ auf den Vorgang des Betriebssystems auswirken. Stellen Sie sicher, dass die Ausführung einer wichtigen Komponente des Betriebssystems oder eines davon abhängigen Programms nicht verhindert wird.

> [!NOTE]
> -   Möglicherweise müssen neue Softwareeinschränkungsrichtlinien für das Gruppenrichtlinienobjekt erstellt werden, sofern noch nicht geschehen.
> -   Wenn Sie eine Pfadregel für Software mit der Sicherheitsstufe **Nicht erlaubt** erstellen, können Benutzer die Software dennoch ausführen, indem sie sie an einen anderen Speicherort kopieren.
> -   Für Pfadregeln sind die Platzhalterzeichen %%amp;quot;*%%amp;quot; und %%amp;quot;?%%amp;quot; zulässig.
> -   In Pfadregeln können Umgebungsvariablen wie %%amp;quot;%programfiles%%%amp;quot; oder %%amp;quot;%systemroot%%%amp;quot; verwendet werden.
> -   Wenn Sie eine Pfadregel für Software erstellen möchten und nicht wissen, wo sie auf dem Computer gespeichert ist, aber den Registrierungsschlüssel besitzen, können Sie eine Registrierungspfadregel erstellen.
> -   Um zu verhindern, dass Benutzer-e-Mail-Anlagen ausführen, können Sie eine Pfadregel für das Anlagenverzeichnis Ihres e-Mail-Programms erstellen, die verhindert, dass die Benutzer-e-Mail-Anlagen ausführen.
> -   Pfadregeln wirken sich nur auf die Dateitypen aus, die im Detailbereich von %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot; unter **Designierte Dateitypen** aufgeführt sind. Dort finden Sie eine Liste der designierten Dateitypen, die für alle Regeln gilt.
> -   Richtlinien, für softwareeinschränkung wirksam wird müssen Benutzer die Richtlinieneinstellungen beim Abmelden von und Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Softwareeinschränkungsregel Richtlinien auf die Richtlinieneinstellungen angewendet wird, wird eine Rangfolge der Regeln für das Behandeln von Konflikten.

#### <a name="to-create-a-registry-path-rule"></a>So erstellen Sie eine Registrierungspfaddatei

1.  Auf der **starten** Bildschirm, und geben Sie "regedit".

2.  Klicken Sie in der Konsolenstruktur mit der rechten Maustaste auf den Registrierungsschlüssel, für den eine Regel erstellt werden soll, und klicken Sie dann auf **Schlüsselnamen kopieren**. Notieren Sie den Wertnamen im Detailbereich.

3.  Öffnen Sie %%amp;quot;Richtlinien für Softwareeinschränkung%%amp;quot;.

4.  In der Konsolenstruktur oder im Detailbereich, mit der Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **neue Pfadregel**.

5.  In **Pfad**, fügen Sie den Registrierungsschlüsselnamen, gefolgt von den Wertnamen.

6.  Schließen Sie den Registrierungspfad in Prozentzeichen (%), z. B. % HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PlatformSDK\Directories\InstallDir% an.

7.  In **Sicherheitsstufe**, klicken Sie auf **nicht erlaubt** oder **uneingeschränkt**.

8.  Geben Sie unter **Beschreibung** eine Beschreibung für die Regel ein, und klicken Sie anschließend auf **OK**.


