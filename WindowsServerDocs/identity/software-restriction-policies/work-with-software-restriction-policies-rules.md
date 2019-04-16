---
title: Arbeiten Sie mit Software Restriction Policies Regeln
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
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="work-with-software-restriction-policies-rules"></a>Arbeiten Sie mit Software Restriction Policies Regeln

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema beschreibt Verfahren arbeiten mit Zertifikat, Pfad, Internet Zone und Hash-Regeln mithilfe von Softwareeinschränkungsrichtlinien.

## <a name="introduction"></a>Einführung in
Mit Softwareeinschränkungsrichtlinien können Sie Ihre EDV-Umgebung vor nicht vertrauenswürdiger Software schützen, indem Sie festlegen, welche Software ausgeführt werden darf. Sie können die Standardsicherheitsstufe der definieren **Unrestricted** oder **nicht erlaubt** für ein Gruppenrichtlinienobjekt (GPO) so, dass Software entweder zugelassen ist zulässig, wird standardmäßig ausgeführt. Sie können Ausnahmen für diese Standardsicherheitsstufe vornehmen, indem Softwareeinschränkungsrichtlinien Regeln der Richtlinien für bestimmte Software erstellen. Wenn als Standardsicherheitsstufe festgelegt ist, um z. B. **nicht erlaubt**, Sie können Regeln erstellen, die zum Ausführen bestimmter Software zulassen. Die Typen von Regeln sind wie folgt:

-   **Zertifikatregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [arbeiten mit Zertifikatregeln](#BKMK_Cert_Rules).

-   **Hashregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [arbeiten mit Hashregeln](#BKMK_Hash_Rules).

-   **Internetzonenregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [arbeiten mit Regeln der Zone des Internets](#BKMK_Internet_Zone_Rules).

-   **Pfadregeln**

    Informationen zu entsprechenden Verfahren finden Sie unter [arbeiten mit Pfadregeln](#BKMK_Path_Rules).

Informationen über andere Aufgaben zum Verwalten von Softwareeinschränkungsrichtlinien finden Sie unter [Administer Software Restriction Policies](administer-software-restriction-policies.md).

## <a name="BKMK_Cert_Rules"></a>Arbeiten mit Zertifikatregeln
Richtlinien für softwareeinschränkung können auch Software anhand ihres Signaturzertifikats identifizieren. Sie können eine Zertifikatregel erstellen, die Software identifiziert und ermöglicht es, oder, abhängig von der Sicherheitsstufe ausführen die Software ist nicht zulässig. Beispielsweise können Sie Zertifikatregeln, um Software aus einer vertrauenswürdigen Quelle in einer Domäne automatisch zu vertrauen, ohne den Benutzer aufzufordern. Sie können Zertifikatregeln auch verwenden, um Dateien in nicht zulässigen Bereichen des Betriebssystems auszuführen. Zertifikatregeln sind nicht standardmäßig aktiviert.

Bei der Erstellung von Regeln für die Domäne mithilfe von Gruppenrichtlinien müssen Sie die Berechtigungen zum Erstellen oder Bearbeiten eines Gruppenrichtlinienobjekts verfügen. Wenn Sie Regeln für den lokalen Computer erstellen, müssen Sie auf diesem Computer Administratorrechte besitzen.

#### <a name="to-create-a-certificate-rule"></a>Erstellen Sie eine Zertifikatregel

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  In der Konsolenstruktur oder im Detailbereich mit der rechten Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **neue Zertifikatregel**.

3.  Klicken Sie auf **Durchsuchen**, und wählen Sie dann ein Zertifikat oder eine signierte Datei.

4.  In **Sicherheitsstufe**, klicken Sie entweder **nicht erlaubt** oder **Unrestricted**.

5.  In **Beschreibung**, geben Sie eine Beschreibung für diese Regel ein, und klicken Sie dann auf **OK**.

> [!NOTE]
> -   Es ist möglicherweise erforderlich, um eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt (GPO) erstellen, wenn Sie nicht bereits geschehen.
> -   Zertifikatregeln sind nicht standardmäßig aktiviert.
> -   Nur die Dateitypen, die von Zertifikatregeln betroffen sind sind für die aufgelisteten **Designierte Dateitypen** klicken Sie im Detailbereich für Softwareeinschränkungsrichtlinien. Es gibt eine Liste der designierten Dateitypen, die von allen Regeln gemeinsam verwendet wird.
> -   Für Softwareeinschränkungsrichtlinien wirksam wird müssen Benutzer Richtlinieneinstellungen von Abmelden und zum Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Software Restriction Richtlinien Regel Richtlinieneinstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

### <a name="enabling-certificate-rules"></a>Aktivieren von Zertifikatregeln
Es gibt unterschiedliche Verfahren zum Aktivieren von Zertifikatregeln abhängig von Ihrer Umgebung:

-   [Für den lokalen computer](#BKMK_1)

-   [Für ein Gruppenrichtlinienobjekt, und Sie auf einem Server, der einer Domäne angehört](#BKMK_2)

-   [Für ein Gruppenrichtlinienobjekt, und Sie auf einem Domänencontroller oder einer Arbeitsstation arbeiten, die die Remoteserver-Verwaltungstools installiert wurde](#BKMK_3)

-   [Sind ausschließlich für Domänencontroller, wobei Sie ein, auf einem Domänencontroller oder einer Arbeitsstation, die das Remote Server Administration Tools Pack installiert ist](#BKMK_4)

#### <a name="BKMK_1"></a>So aktivieren Sie Zertifikatregeln für den lokalen computer

1.  Öffnen Sie die lokalen Sicherheitseinstellungen.

2.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich unter/Lokale Sicherheitsrichtlinien.

3.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatregeln auf Windows-Programme für Softwareeinschränkungsrichtlinien**.

4.  Führen Sie eine der folgenden Optionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **deaktiviert**.

#### <a name="BKMK_2"></a>Werden zum Aktivieren von Zertifikatregeln für ein Gruppenrichtlinienobjekt, und Sie auf einem Server, der einer Domäne angehört

1.  Öffnen Sie Microsoft Management Console (MMC).

2.  Auf der **Datei** Menü klicken Sie auf **Snap-In hinzufügen/entfernen**, und klicken Sie dann auf **hinzufügen**.

3.  Klicken Sie auf **Editor für lokale Gruppenrichtlinien Objekt**, und klicken Sie dann auf **hinzufügen**.

4.  In **Gruppenrichtlinienobjekt auswählen**, klicken Sie auf **Durchsuchen**.

5.  In **für ein Gruppenrichtlinienobjekt Durchsuchen**, wählen Sie in der entsprechenden Domäne, Site oder Organisationseinheit (Group Policy Object, GPO)- oder eine neue zu erstellen, und klicken Sie dann auf **Fertig stellen**.

6.  Klicken Sie auf **schließen**, und klicken Sie dann auf **OK**.

7.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich unter *Gruppenrichtlinienobjekt* [*ComputerName*] Richtlinie/Computer Configuration/Windows-Einstellungen/Sicherheitseinstellungen/lokale Richtlinien /.

8.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatregeln auf Windows-Programme für Softwareeinschränkungsrichtlinien**.

9. Wenn diese richtlinieneinstellung noch nicht definiert wurde, wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen.

10. Führen Sie eine der folgenden Optionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **deaktiviert**.

#### <a name="BKMK_3"></a>So aktivieren Sie die Zertifikat-Regeln für ein Gruppenrichtlinienobjekt, und auf einem Domänencontroller oder einer Arbeitsstation mit den Remoteserver-Verwaltungstools installiert sind

1.  Active Directory-Benutzer und -Computer zu öffnen.

2.  Klicken Sie in der Konsolenstruktur auf die Gruppe Gruppenrichtlinienobjekt (GPO) für die Sie Zertifikatregeln aktivieren möchten.

3.  Klicken Sie auf **Eigenschaften**, und klicken Sie dann auf die **Gruppenrichtlinien** Registerkarte.

4.  Klicken Sie auf **bearbeiten** um das Gruppenrichtlinienobjekt zu öffnen, die Sie bearbeiten möchten. Sie können auch klicken **neu** erstellen ein neues Gruppenrichtlinienobjekt, und klicken Sie auf **bearbeiten**.

5.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich unter *Gruppenrichtlinienobjekt*[*ComputerName*] Richtlinie/Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/lokale Richtlinien.

6.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatregeln auf Windows-Programme für Softwareeinschränkungsrichtlinien**.

7.  Wenn diese richtlinieneinstellung noch nicht definiert wurde, wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen.

8.  Führen Sie eine der folgenden Optionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **deaktiviert**.

#### <a name="BKMK_4"></a>Sind Zertifikatregeln nur für Domänencontroller, und Sie zum Aktivieren auf einem Domänencontroller oder einer Arbeitsstation mit den Remoteserver-Verwaltungstools installiert

1.  Öffnen Sie die Domänencontroller-Sicherheitseinstellungen.

2.  Klicken Sie in der Konsolenstruktur auf **Sicherheitsoptionen** befindet sich unter *Gruppenrichtlinienobjekt* [*ComputerName*] Richtlinie/Computerkonfiguration/Windows-Einstellungen/Sicherheitseinstellungen/lokale Richtlinien.

3.  Doppelklicken Sie im Detailbereich auf **Systemeinstellungen: Zertifikatregeln auf Windows-Programme für Softwareeinschränkungsrichtlinien**.

4.  Wenn diese richtlinieneinstellung noch nicht definiert wurde, wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen.

5.  Führen Sie eine der folgenden Optionen aus, und klicken Sie dann auf **OK**:

    -   Klicken Sie zum Aktivieren von Zertifikatregeln auf **aktiviert**.

    -   Klicken Sie zum Deaktivieren von Zertifikatregeln auf **deaktiviert**.

> [!NOTE]
> Sie müssen dieses Verfahren ausführen, damit Zertifikatregeln wirksam werden können.

### <a name="set-trusted-publisher-options"></a>Festlegen von Optionen für vertrauenswürdige Herausgeber
Signieren von Software wird verwendet von immer mehr Softwareherausgeber und Anwendungsentwickler um zu überprüfen, ob ihre Anwendungen von einer vertrauenswürdigen Quelle stammen. Jedoch viele Benutzer nicht verstehen oder schenken diesen wenig Beachtung Signaturzertifikate zugeordneten Anwendungen, die sie installieren.

Die Richtlinieneinstellungen in der **vertrauenswürdige Herausgeber** auf der Registerkarte der Zertifikatpfads kann Administratoren steuern, welche Zertifikate akzeptiert werden können, da Sie von einem vertrauenswürdigen Herausgeber stammen.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-local-computer"></a>So konfigurieren Sie die Einstellungen für vertrauenswürdige Herausgeber für einen lokalen computer

1.  Auf der **starten** geben**gpedit.msc** und drücken Sie dann die EINGABETASTE.

2.  In der Konsolenstruktur unter **lokaler Computer-Einstellungen\sicherheitseinstellungen**, klicken Sie auf **Richtlinien öffentlicher Schlüssel**.

3.  Doppelklicken Sie auf **Einstellungen für die Überprüfung von Zertifikaten Pfad**, und klicken Sie dann auf die **vertrauenswürdige Herausgeber** Registerkarte.

4.  Wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen, wählen Sie die Richtlinieneinstellungen, die im Diagramm angezeigt werden sollen, und klicken Sie dann auf **OK** zum Anwenden der neuen Einstellungen.

##### <a name="to-configure-the-trusted-publishers-policy-settings-for-a-domain"></a>So konfigurieren Sie die Einstellungen für vertrauenswürdige Herausgeber für eine Domäne

1.  Öffnen **Gruppenrichtlinienverwaltung**.

2.  Doppelklicken Sie in der Konsolenstruktur auf **Group Policy Objects** in der Gesamtstruktur und Domäne, enthält die **Default Domain Policy** Gruppenrichtlinienobjekt (GPO), die Sie bearbeiten möchten.

3.  Mit der rechten Maustaste die **Default Domain Policy** Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**.

4.  In der Konsolenstruktur unter **Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen**, klicken Sie auf **Richtlinien öffentlicher Schlüssel**.

5.  Doppelklicken Sie auf **Einstellungen für die Überprüfung von Zertifikaten Pfad**, und klicken Sie dann auf die **vertrauenswürdige Herausgeber** Registerkarte.

6.  Wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen, wählen Sie die Richtlinieneinstellungen, die im Diagramm angezeigt werden sollen, und klicken Sie dann auf **OK** zum Anwenden der neuen Einstellungen.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-local-computer"></a>Nur Administratoren zum Verwalten von Zertifikaten für die Codesignatur für einen lokalen Computer zulassen

1.  Auf der **starten** geben, **gpedit.msc** in der **Programme und Dateien suchen** oder in Windows 8, auf dem Desktop, und drücken Sie dann die EINGABETASTE.

2.  In der Konsolenstruktur unter **Default Domain Policy** oder **Richtlinie des lokalen Computers**, doppelklicken Sie auf **Computerkonfiguration**, **Windows-Einstellungen**, und **Sicherheitseinstellungen**, und klicken Sie dann auf **Richtlinien öffentlicher Schlüssel**.

3.  Doppelklicken Sie auf **Einstellungen für die Überprüfung von Zertifikaten Pfad**, und klicken Sie dann auf die **vertrauenswürdige Herausgeber** Registerkarte.

4.  Wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen.

5.  Klicken Sie unter **vertrauenswürdige Herausgeber Management**, klicken Sie auf **können nur Administratoren zum Verwalten von vertrauenswürdige Herausgeber**, und klicken Sie dann auf **OK** zum Anwenden der neuen Einstellungen.

##### <a name="to-allow-only-administrators-to-manage-certificates-used-for-code-signing-for-a-domain"></a>Nur Administratoren zum Verwalten von Zertifikaten für die Codesignatur für eine Domäne zulassen

1.  Öffnen **Gruppenrichtlinienverwaltung**.

2.  Doppelklicken Sie in der Konsolenstruktur auf **Group Policy Objects** in der Gesamtstruktur und Domäne, enthält die **Default Domain Policy** Gruppenrichtlinienobjekt, das Sie bearbeiten möchten.

3.  Mit der rechten Maustaste die **Default Domain Policy** Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**.

4.  In der Konsolenstruktur unter **Computerkonfiguration\Windows-Einstellungen\sicherheitseinstellungen**, klicken Sie auf **Richtlinien öffentlicher Schlüssel**.

5.  Doppelklicken Sie auf **Einstellungen für die Überprüfung von Zertifikaten Pfad**, und klicken Sie dann auf die **vertrauenswürdige Herausgeber** Registerkarte.

6.  Wählen Sie die **diese Richtlinieneinstellungen definieren** Kontrollkästchen, implementieren Sie die Änderungen, die Sie möchten, und klicken Sie dann auf **OK** zum Anwenden der neuen Einstellungen.

## <a name="BKMK_Hash_Rules"></a>Arbeiten mit Hashregeln
Ein Hash ist eine Reihe von Bytes mit einer festen Länge, die ein Softwareprogramm oder eine Datei eindeutig identifiziert. Der Hash wird durch einen Hashalgorithmus berechnet. Wenn für ein Softwareprogramm eine Hashregel erstellt wird, Berechnen von Softwareeinschränkungsrichtlinien einen Hash des Programms. Wenn ein Benutzer versucht, ein Softwareprogramm zu öffnen, wird ein Hash des Programms mit vorhandenen Hashregeln für Softwareeinschränkungsrichtlinien verglichen. Der Hash eines Softwareprogramms ist immer gleich, unabhängig davon, wo sich die Anwendung auf dem Computer befindet. Sollte ein Softwareprogramm in keiner Weise geändert werden, jedoch der Hashwert ändert sich auch, und sie nicht mehr den Hash in der Hashregel für Softwareeinschränkungsrichtlinien übereinstimmt.

Sie können beispielsweise eine Hashregel erstellen und legen Sie die Sicherheitsstufe auf **nicht erlaubt** um zu verhindern, dass Benutzer eine bestimmte Datei ausführen. Eine Datei kann umbenannt oder in einen anderen Ordner verschoben und dennoch denselben Hash. Änderungen an der Datei selbst wird jedoch auch der Hashwert geändert, und der lassen Sie die Einschränkungen zu umgehen.

#### <a name="to-create-a-hash-rule"></a>Erstellen Sie eine Hashregel

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  In der Konsolenstruktur oder im Detailbereich mit der rechten Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **Neue Hashregel**.

3.  Klicken Sie auf **Durchsuchen** um eine Datei zu suchen.

    > [!NOTE]
    > In Windows XP ist es möglich, fügen Sie einen zuvor berechneten Hash in **Dateihash**. In Windows Server 2008 R2, Windows 7 oder höher ist diese Option nicht verfügbar.

4.  In **Sicherheitsstufe**, klicken Sie entweder **nicht erlaubt** oder **Unrestricted**.

5.  In **Beschreibung**, geben Sie eine Beschreibung für diese Regel ein, und klicken Sie dann auf **OK**.

> [!NOTE]
> -   Möglicherweise ist es erforderlich, um eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt (GPO) erstellen, wenn noch nicht geschehen.
> -   Für einen Virus oder ein trojanisches Pferd, um zu verhindern, dass ausführen kann eine Hashregel erstellt werden.
> -   Wenn Sie möchten andere Benutzer eine Hashregel so, dass Viren ausgeführt werden kann, berechnet den Hash des Virus mithilfe von Softwareeinschränkungsrichtlinien und per e-mail an die anderen Teilnehmer den Hashwert. Versenden Sie niemals den Virus selbst.
> -   Wenn ein Virus per E-mail gesendet wurde, können Sie auch zur Ausführung von e-Mail-Anlagen zu verhindern, dass eine Pfadregel erstellen.
> -   Eine Datei, die umbenannt oder in einen anderen Ordner Ergebnisse in den gleichen Hash verschoben wird. Jede Änderung an der Datei selbst führt zu einem anderen Hash.
> -   Nur die Dateitypen, die von Hashregeln betroffen sind sind für die aufgelisteten **Designierte Dateitypen** klicken Sie im Detailbereich für Softwareeinschränkungsrichtlinien. Es gibt eine Liste der designierten Dateitypen, die von allen Regeln gemeinsam verwendet wird.
> -   Für Softwareeinschränkungsrichtlinien wirksam wird müssen Benutzer Richtlinieneinstellungen von Abmelden und zum Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Software Restriction Richtlinien Regel Richtlinieneinstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

## <a name="BKMK_Internet_Zone_Rules"></a>Arbeiten mit Regeln der Zone des Internets
Internetzonenregeln gelten nur für Windows Installer-Pakete. Mit einer Zonenregel kann Software aus einer Zone zu identifizieren, die über Internet Explorer angegeben ist. Diese Zonen sind Internet, lokales Intranet, eingeschränkte Sites, vertrauenswürdige Sites und Arbeitsplatz. Eine Internetzonenregel soll verhindern, dass Benutzer Software herunterladen und installieren.

#### <a name="to-create-an-internet-zone-rule"></a>Erstellen Sie eine Internetzonenregel

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  In der Konsolenstruktur oder im Detailbereich mit der rechten Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **Neue Internetzonenregel**.

3.  In **Internetzone**, klicken Sie auf eine Internetzone.

4.  In **Sicherheitsstufe**, klicken Sie entweder **nicht erlaubt** oder **Unrestricted**, und klicken Sie dann auf **OK**.

> [!NOTE]
> -   Möglicherweise ist es erforderlich, um eine neue Softwareeinschränkungsrichtlinien-Einstellung für das Gruppenrichtlinienobjekt (GPO) erstellen, wenn noch nicht geschehen.
> -   Zonenregeln gelten nur für Dateien mit Dateityp MSI, die Windows Installer-Pakete sind.
> -   Für Softwareeinschränkungsrichtlinien wirksam wird müssen Benutzer Richtlinieneinstellungen von Abmelden und zum Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Software Restriction Richtlinien Regel Richtlinieneinstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

## <a name="BKMK_Path_Rules"></a>Arbeiten mit Pfadregeln
Eine Pfadregel identifiziert Software anhand des Dateipfads. Wenn Sie über einen Computer verfügen, die Standardsicherheitsstufe der verfügt z. B. **nicht erlaubt**, können Sie dennoch uneingeschränkten Zugriff auf einen bestimmten Ordner für jeden Benutzer gewähren. Sie können eine Pfadregel erstellen, indem Sie den Dateipfad und zum Festlegen der Sicherheitsstufe der Pfadregel **Unrestricted**. Häufig verwendete Pfade für diese Art der Regel sind % USERPROFILE%, % windir%, % appdata%, % ProgramFiles% und % Temp%. Sie können auch Registrierung Pfadregeln erstellen, die den Registrierungsschlüssel der Software als Pfad verwenden.

Da diese Regeln anhand des Pfads angegeben werden, wenn ein Softwareprogramm verschoben wird, gilt die Pfadregel nicht mehr.

#### <a name="to-create-a-path-rule"></a>Erstellen Sie eine Pfadregel

1.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

2.  In der Konsolenstruktur oder im Detailbereich mit der rechten Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **neue Pfadregel**.

3.  In **Pfad**, geben Sie einen Pfad ein, oder klicken Sie auf **Durchsuchen** um eine Datei oder einen Ordner zu suchen.

4.  In **Sicherheitsstufe**, klicken Sie entweder **nicht erlaubt** oder **Unrestricted**.

5.  In **Beschreibung**, geben Sie eine Beschreibung für diese Regel ein, und klicken Sie dann auf **OK**.

> [!CAUTION]
> -   In bestimmten Ordnern, z. B. Windows-Ordner, Festlegen der Sicherheitsstufe auf **nicht erlaubt** können sich negativ auf den Betrieb von Ihrem Betriebssystem auswirken. Stellen Sie sicher, dass Sie eine wichtige Komponente des Betriebssystems oder eines abhängigen Programms nicht verhindert werden.

> [!NOTE]
> -   Möglicherweise ist es erforderlich, neue Softwareeinschränkungsrichtlinien für das Gruppenrichtlinienobjekt (GPO) erstellen, wenn noch nicht geschehen.
> -   Wenn Sie eine Pfadregel für Software mit der Sicherheitsstufe erstellen **nicht erlaubt**, Benutzer können die Software dennoch ausführen, indem Sie sie an einen anderen Speicherort kopieren.
> -   Sind die Platzhalterzeichen, die von der Pfadregel unterstützt werden * und?.
> -   Sie können Umgebungsvariablen wie % ProgramFiles% "oder" systemroot%, in der Pfadregel.
> -   Wenn Sie eine Pfadregel für Software erstellen, wenn Sie nicht wissen, in dem sie auf einem Computer gespeichert ist, aber Sie den Registrierungsschlüssel besitzen möchten, können Sie eine Registrierungspfadregel erstellen.
> -   Um zu verhindern, dass Benutzer e-Mail-Anlagen ausführen, können Sie eine Pfadregel für das Anlagenverzeichnis Ihres e-Mail-Programms erstellen, die verhindert, dass Benutzer e-Mail-Anlagen ausführen.
> -   Nur die Dateitypen, die von Pfadregeln betroffen sind sind für die aufgelisteten **Designierte Dateitypen** klicken Sie im Detailbereich für Softwareeinschränkungsrichtlinien. Es gibt eine Liste der designierten Dateitypen, die von allen Regeln gemeinsam verwendet wird.
> -   Für Softwareeinschränkungsrichtlinien wirksam wird müssen Benutzer Richtlinieneinstellungen von Abmelden und zum Anmelden bei ihren Computern aktualisieren.
> -   Wenn mehr als eine Software Restriction Richtlinien Regel Richtlinieneinstellungen angewendet wird, gibt es eine Rangfolge der Regeln für die Behandlung von Konflikten.

#### <a name="to-create-a-registry-path-rule"></a>Erstellen Sie eine Registrierungspfadregel

1.  Auf der **starten** Bildschirm, geben Sie regedit ein.

2.  In der Konsolenstruktur mit der Maustaste des Registrierungsschlüssels, die Sie verwenden möchten, erstellen Sie eine Regel für, und klicken Sie dann auf **Schlüsselnamen kopieren**. Beachten Sie den Wertnamen im Detailbereich.

3.  Öffnen Sie die Richtlinien für Softwareeinschränkung.

4.  In der Konsolenstruktur oder im Detailbereich mit der rechten Maustaste **zusätzliche Regeln**, und klicken Sie dann auf **neue Pfadregel**.

5.  In **Pfad**, fügen Sie den Namen des Registrierungsschlüssels, gefolgt vom Wert ein.

6.  Schließen Sie den Registrierungspfad in Prozentzeichen (%), z. B. % HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\PlatformSDK\Directories\InstallDir%.

7.  In **Sicherheitsstufe**, klicken Sie entweder **nicht erlaubt** oder **Unrestricted**.

8.  In **Beschreibung**, geben Sie eine Beschreibung für diese Regel ein, und klicken Sie dann auf **OK**.


