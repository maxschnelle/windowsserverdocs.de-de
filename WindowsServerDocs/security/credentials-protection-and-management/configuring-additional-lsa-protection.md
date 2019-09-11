---
title: Konfigurieren von zusätzlichem LSA-Schutz
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 038e7c2b-c032-491f-8727-6f3f01116ef9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 90efc49b0d7ff6edd8367cece42bf7f2950de952
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70870556"
---
# <a name="configuring-additional-lsa-protection"></a>Konfigurieren von zusätzlichem LSA-Schutz

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Spezialisten erfahren Sie, wie Sie den zusätzlichen Schutz für den Prozess der lokalen Sicherheitsautorität (Local Security Authority, LSA) konfigurieren, um eine Codeinjizierung mit einer möglichen Beeinträchtigung der Anmeldeinformationen zu verhindern.

Mithilfe der lokalen Sicherheitsautorität, die auch den LSASS-Prozess (Local Security Authority Subsystem Service, Subsystemdienst für die lokale Sicherheitsautorität) umfasst, werden Benutzer für die lokale Anmeldung und Remoteanmeldung überprüft und lokale Sicherheitsrichtlinien erzwungen. Das Betriebssystem Windows 8.1 bietet zusätzlichen Schutz für die LSA, um das Lesen von Speicher und Code Injektion durch nicht geschützte Prozesse zu verhindern. Dies sorgt für eine erhöhte Sicherheit in Bezug auf Anmeldeinformationen, die von der lokalen Sicherheitsautorität gespeichert und verwaltet werden. Die geschützte Prozess Einstellung für LSA kann in Windows 8.1 konfiguriert werden, Sie kann jedoch nicht in Windows RT 8,1 konfiguriert werden. Wenn diese Einstellung zusammen mit dem sicheren Start verwendet wird, erhöht dies den Schutz, da das Deaktivieren des Registrierungsschlüssels HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa keine Wirkung hat.

### <a name="protected-process-requirements-for-plug-ins-or-drivers"></a>Anforderungen an den geschützten Prozess für Plug-Ins oder Treiber
Damit ein LSA-Plug-In oder -Treiber erfolgreich als geschützter Prozess geladen werden kann, muss er die folgenden Kriterien erfüllen:

1.  Signaturüberprüfung

    Der geschützte Modus erfordert, dass alle Plug-Ins, die in die lokale Sicherheitsautorität geladen werden, mit einer Microsoft-Signatur digital signiert werden. Daher können alle Plug-Ins, die nicht signiert sind bzw. nicht mit einer Microsoft-Signatur signiert sind, in der lokalen Sicherheitsautorität nicht geladen werden. Beispiele für diese Plug-Ins sind Smartcard-Treiber, kryptografische Plug-Ins und Kennwortfilter.

    LSA-Plug-Ins, bei denen es sich um Treiber handelt, z. B. Smartcard-Treiber, müssen mithilfe der WHQL-Zertifizierung signiert werden. Weitere Informationen finden Sie unter [WHQL-releasesignatur](https://msdn.microsoft.com/library/windows/hardware/ff553976%28v=vs.85%29.aspx).

    LSA-Plug-Ins, die nicht über einen WHQL-Zertifizierungsprozess verfügen, müssen mithilfe des [Dateisignierdiensts für LSA](https://go.microsoft.com/fwlink/?LinkId=392590)signiert werden.

2.  Anleitung zur Einhaltung des Microsoft Security Development Lifecycle (SDL)-Prozesses

    Alle Plug-Ins müssen die Vorgaben zur Einhaltung des jeweiligen SDL-Prozesses erfüllen. Weitere Informationen finden Sie unter [Microsoft Security Development Lifecycle (SDL) – Anhang](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx).

    Auch wenn die Plug-Ins ordnungsgemäß mit einer Microsoft-Signatur signiert sind, kann eine Nichteinhaltung des SDL-Prozesses beim Laden eines Plug-Ins zu einem Fehler führen.

#### <a name="recommended-practices"></a>Empfohlene Vorgehensweisen
Nutzen Sie die folgende Liste, um eingehend zu testen, ob der LSA-Schutz aktiviert ist, bevor Sie das Feature allgemein bereitstellen:

-   Identifizieren Sie alle LSA-Plug-Ins und -Treiber, die in Ihrer Organisation verwendet werden. 
    Dazu gehören nicht von Microsoft stammende Treiber oder Plug-Ins, z. B. Smartcard-Treiber und kryptografische Plug-Ins, und eine intern entwickelte Software, die eingesetzt wird, um Kennwortfilter oder Benachrichtigungen über Kennwortänderungen zu erzwingen.

-   Stellen Sie sicher, dass alle LSA-Plug-Ins digital mit einem Microsoft-Zertifikat signiert sind, damit beim Laden des Plug-Ins kein Fehler auftritt.

-   Stellen Sie sicher, dass alle ordnungsgemäß signierten Plug-Ins erfolgreich in die lokale Sicherheitsautorität geladen werden können und dass sie sich wie erwartet verhalten.

-   Verwenden Sie die Überwachungsprotokolle zum Identifizieren von LSA-Plug-Ins und -Treibern, die nicht als geschützter Prozess ausgeführt werden können.

#### <a name="limitations-introduced-with-enabled-lsa-protection"></a>Mit aktiviertem LSA-Schutz eingeführte Einschränkungen

Wenn LSA-Schutz aktiviert ist, können Sie kein benutzerdefiniertes LSA-Plug-in Debuggen
Es ist nicht möglich, einen Debugger an LSASS anzufügen, wenn es sich um einen geschützten Prozess handelt.
Im Allgemeinen gibt es keine unterstützte Möglichkeit zum Debuggen eines laufenden geschützten Prozesses.

## <a name="how-to-identify-lsa-plug-ins-and-drivers-that-fail-to-run-as-a-protected-process"></a>Identifizieren von LSA-Plug-Ins und -Treibern, die nicht als geschützter Prozess ausgeführt werden können
Die in diesem Abschnitt beschriebenen Ereignisse sind im Betriebsprotokoll unter %%amp;quot;Anwendungs- und Dienstprotokolle\Microsoft\Windows\CodeIntegrity%%amp;quot; enthalten. Sie stellen eine Hilfe beim Identifizieren von LSA-Plug-Ins und -Treibern dar, die aufgrund von Signaturproblemen nicht geladen werden können. Zum Verwalten dieser Ereignisse können Sie das Befehlszeilentool **wevtutil** verwenden. Informationen zu diesem Befehl finden Sie unter [Wevtutil](../../administration/windows-commands/Wevtutil.md).

### <a name="before-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>Vor der Aktivierung: Identifizieren von Plug-Ins und Treibern, die von "lsass.exe" geladen werden
Mithilfe des Überwachungsmodus können Sie LSA-Plug-Ins und -Treiber identifizieren, die im LSA-Schutzmodus nicht geladen werden können. Im Überwachungsmodus werden vom System Ereignisprotokolle generiert und alle Plug-Ins und Treiber identifiziert, die unter der lokalen Sicherheitsautorität nicht geladen werden können, wenn der LSA-Schutz aktiviert ist. Die Meldungen werden protokolliert, ohne die Plug-Ins oder Treiber zu blockieren.

##### <a name="to-enable-the-audit-mode-for-lsassexe-on-a-single-computer-by-editing-the-registry"></a>So aktivieren Sie den Überwachungsmodus für %%amp;quot;Lsass.exe%%amp;quot; auf einem einzelnen Computer per Bearbeitung der Registrierung

1.  Öffnen Sie den Registrierungs-Editor (RegEdit.exe), und navigieren Sie zum Registrierungsschlüssel unter: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe.

2.  Legen Sie den Wert des Registrierungsschlüssels wie folgt fest: **AuditLevel=dword:00000008**.

3.  Starten Sie den Computer neu.

Analysieren Sie die Ergebnisse von Ereignis 3065 und Ereignis 3066.

Anschließend werden diese Ereignisse möglicherweise in Ereignisanzeige angezeigt: Microsoft-Windows-codeintegrity/Operational:

-   **Ereignis 3065**: Mit diesem Ereignis wird aufgezeichnet, dass bei einer Codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise "lsass.exe") einen bestimmten Treiber zu laden versucht hat, der die Sicherheitsanforderungen für freigegebene Abschnitte nicht erfüllt. Aufgrund der festgelegten Systemrichtlinie wurde das Laden des Images jedoch zugelassen.

-   **Ereignis 3066**: Mit diesem Ereignis wird aufgezeichnet, dass bei einer Codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise "lsass.exe") einen bestimmten Treiber zu laden versucht hat, der die Anforderungen an die Microsoft-Signaturebene nicht erfüllt. Aufgrund der festgelegten Systemrichtlinie wurde das Laden des Images jedoch zugelassen.

> [!IMPORTANT]
> Diese Betriebsereignisse werden nicht generiert, wenn auf einem System ein Kerneldebugger angefügt und aktiviert ist.
> 
> Wenn ein Plug-In oder Treiber freigegebene Abschnitte enthält, wird Ereignis 3066 zusammen mit dem Ereignis 3065 protokolliert. Durch das Entfernen der freigegebenen Abschnitte sollte verhindert werden, dass diese beiden Ereignisse eintreten, es sei denn, das Plug-In erfüllt die Anforderungen an die Microsoft-Signaturebene nicht.

Zum Aktivieren des Überwachungsmodus für mehrere Computer in einer Domäne können Sie die clientseitige Registrierungserweiterung für die Gruppenrichtlinie verwenden, um den Überwachungsebenen-Registrierungswert für %%amp;quot;Lsass.exe%%amp;quot; bereitzustellen. Sie müssen den Registrierungsschlüssel %%amp;quot;HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe%%amp;quot; ändern.

##### <a name="to-create-the-auditlevel-value-setting-in-a-gpo"></a>So erstellen Sie die Einstellung des AuditLevel-Werts in einem Gruppenrichtlinienobjekt

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC).

2.  Erstellen Sie ein neues Gruppenrichtlinienobjekt (Group Policy Object, GPO), das auf der Domänenebene verknüpft ist oder das mit der Organisationseinheit verknüpft ist, die Ihre Computerkonten enthält. Alternativ dazu können Sie ein GPO auswählen, das schon bereitgestellt wurde.

3.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, und klicken Sie dann auf **Bearbeiten**, um den Gruppenrichtlinienverwaltungs-Editor zu öffnen.

4.  Erweitern Sie nacheinander **Computerkonfiguration**, **Einstellungen** und dann **Windows-Einstellungen**.

5.  Klicken Sie mit der rechten Maustaste auf **Registrierung**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Registrierungselement**. Das Dialogfeld **Neue Registrierungseigenschaften** wird angezeigt.

6.  Klicken Sie in der Liste **Struktur** auf **HKEY_LOCAL_MACHINE.**

7.  Navigieren Sie in der Liste **Schlüsselpfad** zu **SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\LSASS.exe**.

8.  Geben Sie im Feld **Wertname** Folgendes ein: **AuditLevel**.

9. Klicken Sie im Feld **Werttyp** auf **REG_DWORD**, um diese Option auszuwählen.

10. Geben Sie im Feld **Wert** Folgendes ein: **00000008**.

11. Klicken Sie auf **OK**.

> [!NOTE]
> Damit das GPO wirksam wird, muss die GPO-Änderung auf alle Domänencontroller der Domäne repliziert werden.

Zum Aktivieren des zusätzlichen LSA-Schutzes auf mehreren Computern können Sie die clientseitige Registrierungserweiterung für die Gruppenrichtlinie verwenden, indem Sie %%amp;quot;HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa%%amp;quot; ändern. Informationen zu den erforderlichen Schritten finden Sie unter [Konfigurieren des zusätzlichen LSA-Schutzes für Anmeldeinformationen](#BKMK_HowToConfigure) in diesem Thema.

### <a name="after-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>Nach der Aktivierung: Identifizieren von Plug-Ins und Treibern, die von "lsass.exe" geladen werden
Sie können das Ereignisprotokoll verwenden, um LSA-Plug-Ins und -Treiber zu identifizieren, die im LSA-Schutzmodus nicht geladen werden konnten. Wenn der per LSA geschützte Prozess aktiviert ist, werden vom System Ereignisprotokolle generiert. Damit können alle Plug-Ins und Treiber identifiziert werden, die im LSA-Modus nicht geladen werden konnten.

Analysieren Sie die Ergebnisse von Ereignis 3033 und Ereignis 3063.

Anschließend werden diese Ereignisse möglicherweise in Ereignisanzeige angezeigt: Microsoft-Windows-codeintegrity/Operational:

-   **Ereignis 3033**: Mit diesem Ereignis wird aufgezeichnet, dass bei einer Codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise "lsass.exe") einen Treiber zu laden versucht hat, der die Anforderungen an die Microsoft-Signaturebene nicht erfüllt.

-   **Ereignis 3063**: Mit diesem Ereignis wird aufgezeichnet, dass bei einer Codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise "lsass.exe") einen Treiber zu laden versucht hat, der die Sicherheitsanforderungen für freigegebene Abschnitte nicht erfüllt.

Freigegebene Abschnitte sind in der Regel das Ergebnis von Programmiertechniken, bei denen Instanzdaten mit anderen Prozessen interagieren können, für die der gleiche Sicherheitskontext verwendet wird. Dies kann zu Sicherheitsrisiken führen.

## <a name="BKMK_HowToConfigure"></a>Konfigurieren des zusätzlichen LSA-Schutzes für Anmelde Informationen
Auf Geräten mit Windows 8.1 (mit oder ohne sicheren Start oder UEFI) ist die Konfiguration möglich, indem die in diesem Abschnitt beschriebenen Verfahren ausgeführt werden. Bei Geräten, auf denen Windows RT 8,1 ausgeführt wird, ist der Schutz von LSASS. exe immer aktiviert und kann nicht deaktiviert werden.

### <a name="on-x86-based-or-x64-based-devices-using-secure-boot-and-uefi-or-not"></a>Auf x86-basierten oder x64-basierten Geräten mit oder ohne %%amp;quot;Sicherer Start%%amp;quot; und UEFI
Auf x86-basierten oder x64-basierten Geräten, für die %%amp;quot;Sicherer Start%%amp;quot; und UEFI verwendet wird, wird in der UEFI-Firmware eine UEFI-Variable festgelegt, wenn der LSA-Schutz mithilfe des Registrierungsschlüssels aktiviert wird. Wenn die Einstellung in der Firmware gespeichert wird, kann die UEFI-Variable im Registrierungsschlüssel nicht gelöscht oder geändert werden. Die UEFI-Variable muss zurückgesetzt werden.

x86-basierte oder x64-basierte Geräte, die UEFI oder %%amp;quot;Sicherer Start%%amp;quot; nicht unterstützen, werden deaktiviert, können die Konfiguration für den LSA-Schutz in der Firmware nicht speichern und sind vollständig vom Vorhandensein des Registrierungsschlüssels abhängig. In diesem Fall ist es möglich, den LSA-Schutz zu deaktivieren, indem der Remotezugriff auf das Gerät genutzt wird.

Sie können die folgenden Verfahren verwenden, um den LSA-Schutz zu aktivieren oder zu deaktivieren:

##### <a name="to-enable-lsa-protection-on-a-single-computer"></a>So aktivieren Sie den LSA-Schutz auf einem einzelnen Computer

1.  Öffnen Sie den Registrierungs-Editor (RegEdit.exe), und navigieren Sie zum Registrierungsschlüssel unter: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa.

2.  Legen Sie den Wert des Registrierungsschlüssels wie folgt fest: "RunAsPPL"=dword:00000001.

3.  Starten Sie den Computer neu.

##### <a name="to-enable-lsa-protection-using-group-policy"></a>So aktivieren Sie den LSA-Schutz mithilfe der Gruppenrichtlinie

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole (Group Policy Management Console, GPMC).

2.  Erstellen Sie ein neues Gruppenrichtlinienobjekt, das auf der Domänenebene verknüpft ist oder das mit der Organisationseinheit verknüpft ist, die Ihre Computerkonten enthält. Alternativ dazu können Sie ein GPO auswählen, das schon bereitgestellt wurde.

3.  Klicken Sie mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, und klicken Sie dann auf **Bearbeiten**, um den Gruppenrichtlinienverwaltungs-Editor zu öffnen.

4.  Erweitern Sie nacheinander **Computerkonfiguration**, **Einstellungen** und dann **Windows-Einstellungen**.

5.  Klicken Sie mit der rechten Maustaste auf **Registrierung**, zeigen Sie auf **Neu**, und klicken Sie dann auf **Registrierungselement**. Das Dialogfeld **Neue Registrierungseigenschaften** wird angezeigt.

6.  Klicken Sie in der Liste **Struktur** auf **HKEY_LOCAL_MACHINE**.

7.  Navigieren Sie in der Liste **Schlüsselpfad** zu **SYSTEM\CurrentControlSet\Control\Lsa**.

8.  Geben Sie im Feld **Wertname** Folgendes ein: **RunAsPPL**.

9. Klicken Sie im Feld **Werttyp** auf **REG_DWORD**.

10. Geben Sie im Feld **Wert** Folgendes ein: **00000001**.

11. Klicken Sie auf **OK**.

##### <a name="to-disable-lsa-protection"></a>So deaktivieren Sie den LSA-Schutz

1.  Öffnen Sie den Registrierungs-Editor (RegEdit.exe), und navigieren Sie zum Registrierungsschlüssel unter: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa.

2.  Löschen Sie den folgenden Wert aus dem Registrierungsschlüssel: "RunAsPPL"=dword:00000001.

3.  Verwenden Sie das Tool zum Deaktivieren des geschützten LSA-Prozesses (Local Security Authority (LSA) Protected Process Opt-out), um die UEFI-Variable zu löschen, wenn für das Gerät "Sicherer Start" genutzt wird.

    Weitere Informationen zu diesem Tool finden Sie auf der [Seite zum Download von Local Security Authority (LSA) Protected Process Opt-out im offiziellen Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=40897).

    Weitere Informationen zum Verwalten von "Sicherer Start" finden Sie unter [UEFI-Firmware](https://technet.microsoft.com/library/hh824898.aspx).

    > [!WARNING]
    > Wenn %%amp;quot;Sicherer Start%%amp;quot; deaktiviert ist, werden alle auf %%amp;quot;Sicherer Start%%amp;quot; und UEFI bezogenen Konfigurationen zurückgesetzt. Sie sollten %%amp;quot;Sicherer Start%%amp;quot; nur deaktivieren, wenn alle anderen Mittel zum Deaktivieren des LSA-Schutzes nicht zum Erfolg führen.

### <a name="verifying-lsa-protection"></a>Überprüfen des LSA-Schutzes
Wenn Sie ermitteln möchten, ob LSA beim Starten von Windows im geschützten Modus gestartet wurde, können Sie im Protokoll **System** unter **Windows-Protokolle** nach dem folgenden WinInit-Ereignis suchen:

-   12: "LSASS.exe" wurde als geschützter Prozess mit folgender Stufe gestartet: 4

## <a name="additional-resources"></a>Zusätzliche Ressourcen
[Schutz und Verwaltung von Anmeldeinformationen](credentials-protection-and-management.md)

[Datei Signatur Dienst für LSA](https://go.microsoft.com/fwlink/?LinkId=392590)


