---
title: "Konfigurieren von zusätzlichem LSA-Schutz"
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
ms.openlocfilehash: fcfb0dab10d28413cf4ad06dd583274f217c91fa
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-additional-lsa-protection"></a>Konfigurieren von zusätzlichem LSA-Schutz

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema für IT-Experten wird erläutert, konfigurieren Sie die zusätzlichen Schutz für den Prozess (Local Security Authority, LSA) von Code zu verhindern, die Anmeldeinformationen gefährden könnten.

Die LSA, einschließlich den Local Security Authority Server Service (LSASS) Prozess, Benutzer für die lokale und remote Anmeldung und Remoteanmeldung überprüft und lokale Sicherheitsrichtlinien. Das Betriebssystem Windows 8.1 bietet zusätzlichen Schutz für die lokale Sicherheitsinstanz zu verhindern, dass Auslesen des Arbeitsspeichers und das injizieren von code durch ungeschützte Prozesse. Dies bietet zusätzliche Sicherheit für die Anmeldeinformationen, die der lokalen Sicherheitsautorität gespeichert und verwaltet. Die geschützte prozesseinstellung für LSA kann in Windows 8.1 konfiguriert werden, aber es kann nicht unter Windows RT 8.1 konfiguriert werden. Wenn diese Einstellung in Verbindung mit dem sicheren Start verwendet wird, erfolgt zusätzlicher Schutz, da Deaktivieren des Registrierungsschlüssels HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa keine Wirkung hat.

### <a name="protected-process-requirements-for-plug-ins-or-drivers"></a>Geschützter prozessanforderungen für Plug-Ins oder Treiber
Für ein LSA-Plug-in oder Treiber erfolgreich als geschützter Prozess geladen werden soll müssen sie die folgenden Kriterien erfüllen:

1.  Überprüfung der Signatur

    Der geschützte Modus erfordert, dass alle Plug-Ins, die in die lokale Sicherheitsautorität geladen wird mit einem Microsoft-Signatur digital signiert ist. Aus diesem Grund tritt alle Plug-Ins, die nicht signierte oder sind nicht mit einem Microsoft-Signatur signiert, die im LSA geladen. Beispiele für diese Plug-Ins sind Smartcard-Treiber, kryptografische Plug-Ins und Kennwortfilter.

    LSA-Plug-ins, die Treiber, z. B. Smartcard-Treiber müssen mithilfe der WHQL-Zertifizierung signiert werden. Weitere Informationen finden Sie unter [WHQL-Freigabesignatur (Windows-Treiber)](https://msdn.microsoft.com/library/windows/hardware/ff553976%28v=vs.85%29.aspx).

    LSA-Plug-ins, die nicht über einen WHQL-Zertifizierungsprozess verfügen muss signiert werden, mithilfe der [dateisignierdiensts für LSA](https://go.microsoft.com/fwlink/?LinkId=392590).

2.  Zur Einhaltung der Microsoft Security Development Lifecycle (SDL)-Prozesses

    Alle Plug-Ins müssen die entsprechenden SDL-Prozess Richtlinien entsprechen. Weitere Informationen finden Sie in der [Microsoft Security Development Lifecycle (SDL) Anhang](https://msdn.microsoft.com/library/windows/desktop/cc307891.aspx).

    Auch wenn die Plug-Ins ordnungsgemäß mit einem Microsoft-Signatur signiert sind, kann ein plug-in geladen Nichteinhaltung des SDL-Prozesses führen.

#### <a name="recommended-practices"></a>Empfohlene Vorgehensweisen
Mithilfe der folgenden Liste die LSA-Schutzes gründlich zu testen, die aktiviert ist, bevor Sie das Feature Allgemein bereitstellen:

-   Identifizieren Sie alle LSA-Plug-ins und Treiber, die in Ihrer Organisation verwendet werden. 
    Dazu gehören von Microsoft stammende Treiber oder Plug-Ins wie z. B. Smartcard-Treiber und kryptografische Plug-Ins und eine intern entwickelte Software, die verwendet wird, um Kennwortfilter oder Benachrichtigungen über kennwortänderungen zu erzwingen.

-   Stellen Sie sicher, dass alle LSA-Plug-ins digital mit einem Microsoft-Zertifikat signiert sind, sodass das plug-in nicht nicht geladen.

-   Stellen Sie sicher, dass alle ordnungsgemäß signierten Plug-Ins erfolgreich in die lokale Sicherheitsautorität geladen werden kann und dass sie wie erwartet ausgeführt werden.

-   Verwenden Sie die Überwachungsprotokolle zum Identifizieren von LSA-Plug-ins und Treiber, die nicht als geschützter Prozess ausgeführt.

## <a name="how-to-identify-lsa-plug-ins-and-drivers-that-fail-to-run-as-a-protected-process"></a>Vorgehensweise beim Identifizieren von LSA-Plug-ins und Treiber, die nicht als geschützter Prozess ausgeführt werden.
In diesem Abschnitt beschriebenen Ereignisse befinden sich im Betriebsprotokoll Protokoll unter Anwendungs- und dienstprotokolle\microsoft\windows\codeintegrity%%amp;quot. Sie können Sie Identifizieren von LSA-Plug-ins und Treiber, die nicht aufgrund geladen werden. Zum Verwalten dieser Ereignisse können Sie die **Wevtutil** Befehlszeilentool. Informationen zu diesem Tool finden Sie unter [Wevtutil](../../administration/windows-commands/Wevtutil.md).

### <a name="before-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>Vor der Aktivierung: Identifizieren von Plug-Ins und Treibern, die lsass.exe geladen werden
Mithilfe des Überwachungsmodus können Sie Identifizieren von LSA-Plug-ins und-Treiber, die im LSA-Schutzmodus geladen. Im Überwachungsmodus, generiert das System Ereignisprotokolle, identifizieren alle-Plug-ins und-Treiber unter LSA geladen werden soll, wenn der LSA-Schutz aktiviert ist. Die Meldungen werden protokolliert, ohne die Plug-Ins oder Treiber blockieren.

##### <a name="to-enable-the-audit-mode-for-lsassexe-on-a-single-computer-by-editing-the-registry"></a>So aktivieren Sie den Überwachungsmodus für Lsass.exe auf einem einzelnen Computer durch Bearbeiten der Registrierung

1.  Öffnen Sie den Registrierungs-Editor (RegEdit.exe), und navigieren Sie zu dem Registrierungsschlüssel finden Sie unter: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution options\lsass.exe%%amp;quot.

2.  Legen Sie den Wert des Registrierungsschlüssels auf **AuditLevel = DWORD: 00000008**.

3.  Starten Sie den Computer neu.

Analysieren Sie die Ergebnisse von Ereignis 3065 und Ereignis 3066.

-   **Ereignis 3065**: Dieses Ereignis wird aufgezeichnet, dass es sich bei einer codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise lsass.exe) versucht hat, um einen bestimmten Treiber zu laden, der die sicherheitsanforderungen für freigegebene Abschnitte nicht erfüllt. Allerdings wurde aufgrund der Systemrichtlinie, die festgelegt wird, das Bild zugelassen, laden.

-   **Ereignis 3066**: Dieses Ereignis wird aufgezeichnet, dass es sich bei einer codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise lsass.exe) hat versucht, einen bestimmten Treiber zu laden, die die Anforderungen an Microsoft nicht erfüllt. Allerdings wurde aufgrund der Systemrichtlinie, die festgelegt wird, das Bild zugelassen, laden.

> [!IMPORTANT]
> Diese Betriebsereignisse werden nicht generiert, wenn ein Kerneldebugger angefügt und auf einem System aktiviert ist.
> 
> Wenn ein plug-in oder Treiber freigegebene Abschnitte enthält, wird Ereignis 3066 zusammen mit dem Ereignis 3065 protokolliert. Entfernen der freigegebenen Abschnitte sollte verhindern, dass der beiden Ereignisse auftreten, wenn das plug-in die Anforderungen an Microsoft nicht entspricht.

Um den Überwachungsmodus für mehrere Computer in einer Domäne zu aktivieren, können Sie die Registrierung der clientseitigen Erweiterung für Gruppenrichtlinien zum Bereitstellen des Lsass.exe Überwachungsebene Registrierungswerts. In diesem Fall müssen Sie eine HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution options\lsass.exe%%amp;quot Registrierungsschlüssel zu ändern.

##### <a name="to-create-the-auditlevel-value-setting-in-a-gpo"></a>Erstellen Sie die Einstellung des AuditLevel-Wert in einem Gruppenrichtlinienobjekt

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole (GPMC).

2.  Erstellen Sie ein neues Gruppenrichtlinienobjekt (GPO), die auf der Domänenebene verknüpft ist, oder, auf die Organisationseinheit, die Ihre Computerkonten enthält verknüpft ist. Oder Sie können auswählen, dass ein Gruppenrichtlinienobjekt, das bereits bereitgestellt ist.

3.  Maustaste auf das Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten** um den Gruppenrichtlinienverwaltungs-Editor zu öffnen.

4.  Erweitern Sie **Computerkonfiguration**, erweitern Sie **Voreinstellungen**, und erweitern Sie dann **Windows-Einstellungen**.

5.  Mit der rechten Maustaste **Registrierung**, zeigen Sie auf **neu**, und klicken Sie dann auf **Registrierungselement**. Die **neue Registrierungseigenschaften** Dialogfeld wird angezeigt.

6.  In der **Struktur** auf **HKEY_LOCAL_MACHINE.**

7.  In der **Schlüsselpfad** Liste, wechseln Sie zu **SOFTWARE\Microsoft\Windows NT\CurrentVersion\Image File Execution options\lsass.exe%%amp;quot**.

8.  In der **Wertname** geben **AuditLevel**.

9. In der **Werttyp** Feld, aktivieren Sie die **REG_DWORD**.

10. In der **Wert** geben **00000008**.

11. Klicken Sie auf **OK**.

> [!NOTE]
> Für das GPO wirksam wird, muss die GPO-Änderung auf allen Domänencontrollern in der Domäne repliziert werden.

Um für zusätzlichen LSA-Schutzes auf mehreren Computern teilnehmen, können Sie HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa ändern, indem Sie die Registrierung der clientseitigen Erweiterung für Gruppenrichtlinien verwenden. Informationen hierzu finden Sie unter [Konfigurieren von zusätzlichem LSA-Schutz von Anmeldeinformationen](#BKMK_HowToConfigure) in diesem Thema.

### <a name="after-opting-in-how-to-identify-plug-ins-and-drivers-loaded-by-the-lsassexe"></a>Nach der Aktivierung: Identifizieren von Plug-Ins und Treibern, die lsass.exe geladen werden
Das Ereignisprotokoll können zum Identifizieren von LSA-Plug-ins und Treiber, die im LSA-Schutzmodus geladen werden konnte. Wenn der per LSA geschützte Prozess aktiviert ist, generiert das System Ereignisprotokolle, die alle-Plug-ins und Treiber, die nicht unter Lokale Sicherheitsautorität geladen.

Analysieren Sie die Ergebnisse von Ereignis 3033 und Ereignis 3063.

-   **Ereignis 3033**: Dieses Ereignis wird aufgezeichnet, dass es sich bei einer codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise lsass.exe) hat versucht, einen Treiber zu laden, die die Anforderungen an Microsoft nicht erfüllt.

-   **Ereignis 3063**: Dieses Ereignis wird aufgezeichnet, dass es sich bei einer codeintegritätsprüfung ermittelt wurde, dass ein Prozess (normalerweise lsass.exe) hat versucht, einen Treiber zu laden, der die sicherheitsanforderungen für freigegebene Abschnitte nicht erfüllt.

Freigegebene Abschnitte sind in der Regel das Ergebnis von Programmiertechniken, die denen Instanzdaten mit anderen Prozessen interagieren, die die gleiche Sicherheitskontext verwendet. Dies kann zu Sicherheitsrisiken führen.

## <a name="BKMK_HowToConfigure"></a>Vorgehensweise beim Konfigurieren des zusätzlichen LSA-Schutzes für Anmeldeinformationen
Auf Geräten unter Windows 8.1 (mit oder ohne sicheren Start oder UEFI) ist durch Ausführen der Verfahrens in diesem Abschnitt beschriebenen Konfiguration möglich. Bei Geräten mit Windows RT 8.1 lsass.exe Protection immer aktiviert ist, und es kann nicht deaktiviert werden.

### <a name="on-x86-based-or-x64-based-devices-using-secure-boot-and-uefi-or-not"></a>Auf X86-basierten oder X64 64-Geräten mit sicherem Start und UEFI oder nicht
Auf X86-basierten oder X64 64-Geräten, die sicherer Start und UEFI verwenden, wird eine UEFI-Variable beim LSA-Schutz aktiviert ist, über die Registrierungsschlüssel in der UEFI-Firmware festgelegt. Wenn die Einstellung in der Firmware gespeichert wird, kann die UEFI-Variable nicht gelöscht oder in der Registrierung geändert. Die UEFI-Variable muss zurückgesetzt werden.

X86-basierten oder X64 64-Geräten, die nicht UEFI "oder" Sicherer Start deaktiviert sind, speichern Sie die Konfiguration für LSA-Schutz in der Firmware und verlassen sich ausschließlich auf das Vorhandensein des Registrierungsschlüssels nicht möglich. In diesem Szenario ist es möglich, mithilfe des Remotezugriffs auf dem Gerät LSA-Schutz zu deaktivieren.

Sie können die folgenden Verfahren verwenden, aktivieren oder Deaktivieren des LSA-Schutz:

##### <a name="to-enable-lsa-protection-on-a-single-computer"></a>So aktivieren Sie den LSA-Schutz auf einem einzelnen computer

1.  Öffnen Sie den Registrierungs-Editor (RegEdit.exe), und navigieren Sie zu dem Registrierungsschlüssel finden Sie unter: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa.

2.  Legen Sie den Wert des Registrierungsschlüssels auf: "RunAsPPL" = DWORD: 00000001.

3.  Starten Sie den Computer neu.

##### <a name="to-enable-lsa-protection-using-group-policy"></a>So aktivieren Sie LSA-Schutz mithilfe von Gruppenrichtlinien

1.  Öffnen Sie die Gruppenrichtlinien-Verwaltungskonsole (GPMC).

2.  Erstellen Sie ein neues Gruppenrichtlinienobjekt, das auf der Domänenebene verknüpft ist, oder, auf die Organisationseinheit, die Ihre Computerkonten enthält verknüpft ist. Oder Sie können auswählen, dass ein Gruppenrichtlinienobjekt, das bereits bereitgestellt ist.

3.  Maustaste auf das Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten** um den Gruppenrichtlinienverwaltungs-Editor zu öffnen.

4.  Erweitern Sie **Computerkonfiguration**, erweitern Sie **Voreinstellungen**, und erweitern Sie dann **Windows-Einstellungen**.

5.  Mit der rechten Maustaste **Registrierung**, zeigen Sie auf **neu**, und klicken Sie dann auf **Registrierungselement**. Die **neue Registrierungseigenschaften** Dialogfeld wird angezeigt.

6.  In der **Struktur** auf **HKEY_LOCAL_MACHINE**.

7.  In der **Schlüsselpfad** Liste, wechseln Sie zu **SYSTEM\CurrentControlSet\Control\Lsa**.

8.  In der **Wertname** geben **RunAsPPL**.

9. In der **Werttyp** auf die **REG_DWORD**.

10. In der **Wert** geben **00000001**.

11. Klicken Sie auf **OK**.

##### <a name="to-disable-lsa-protection"></a>So deaktivieren Sie den LSA-Schutz

1.  Öffnen Sie den Registrierungs-Editor (RegEdit.exe), und navigieren Sie zu dem Registrierungsschlüssel finden Sie unter: HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa.

2.  Löschen Sie den folgenden Wert aus dem Registrierungsschlüssel: "RunAsPPL" = DWORD: 00000001.

3.  Verwenden Sie das Tool (Local Security Authority, LSA) Protected Process Opt-Out, um die UEFI-Variable zu löschen, wenn das Gerät den sicheren Start verwendet wird.

    Weitere Informationen zum Tool "Ablehnen" finden Sie unter [herunterladen Local Security Authority (LSA) Protected Process Opt-Out im offiziellen Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=40897).

    Weitere Informationen zum Verwalten von sicheren Start finden Sie unter [UEFI-Firmware](https://technet.microsoft.com/library/hh824898.aspx).

    > [!WARNING]
    > Wenn der sichere Start deaktiviert ist, werden alle sicherer Start und UEFI bezogenen Konfigurationen zurückgesetzt. Sie sollten den sicheren Start deaktivieren, nur, wenn alle anderen Mittel zum Deaktivieren des LSA-Schutzes fehlgeschlagen ist.

### <a name="verifying-lsa-protection"></a>Überprüfen der LSA-Schutz
Um zu ermitteln, ob LSA beim Starten von Windows im geschützten Modus gestartet wurde, suchen Sie nach den folgenden WinInit-Ereignis in der **System** melden Sie sich unter **Windows-Protokolle**:

-   12: LSASS.exe wurde als geschützter Prozess mit Stufe gestartet: 4

## <a name="additional-resources"></a>Zusätzliche Ressourcen
[Schutz von Anmeldeinformationen und Verwaltung](credentials-protection-and-management.md)

[Dateisignierdiensts für LSA](https://go.microsoft.com/fwlink/?LinkId=392590)


