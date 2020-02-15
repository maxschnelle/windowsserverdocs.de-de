---
title: Remoteserver-Verwaltungstools
description: Thema der obersten Ebene für Remoteserver-Verwaltungstools
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-rsat
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d54a1f5e-af68-497e-99be-97775769a7a7
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: 4e6452947af236f3021d493a42f536fed0cd110a
ms.sourcegitcommit: 07c9d4ea72528401314e2789e3bc2e688fc96001
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76822333"
---
# <a name="remote-server-administration-tools"></a>Remoteserver-Verwaltungstools

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema unterstützt die Remoteserver-Verwaltungstools für Windows 10.

> [!IMPORTANT]
> Ab dem Windows 10-Update vom Oktober 2018 ist RSAT als Sammlung von **Features bei Bedarf** in Windows 10 selbst enthalten. Weitere Anweisungen zur Installation finden Sie unter **Wann welche RSAT-Version verwendet werden sollte**.

Mit RSAT können IT-Administratoren Windows Server-Rollen und -Funktionen von einem Windows 10-PC aus verwalten.

Die Remoteserver-Verwaltungstools beinhalten Server-Manager, Microsoft Management Console-Snap-Ins (MMC), Konsolen, Windows PowerShell-Cmdlets und -Anbieter sowie Befehlszeilentools für die Verwaltung von Rollen und Features, die auf Windows Server ausgeführt werden.

Zu den Remoteserver-Verwaltungstools zählen Windows PowerShell-Cmdlet-Module, die zum Verwalten von Rollen und Features verwendet werden können, die auf Remoteservern ausgeführt werden. Obwohl die Windows PowerShell-Remoteverwaltung unter Windows Server 2016 standardmäßig aktiviert ist, ist sie unter Windows 10 standardmäßig nicht aktiviert. Führen Sie zur Ausführung von Cmdlets, die Teil der Remoteserver-Verwaltungstools sind, für einen Remoteserver `Enable-PSremoting` in einer Windows PowerShell-Sitzung aus, die mit erhöhten Benutzerrechten (d. h. „Als Administrator ausführen“) nach der Installation der Remoteserver-Verwaltungstools auf Ihrem Windows-Clientcomputer geöffnet wurde.

## <a name="BKMK_Thresh"></a>Remoteserver-Verwaltungstools für Windows 10
Verwenden Sie die Remoteserver-Verwaltungstools für Windows 10, um bestimmte Technologien auf Computern zu verwalten, auf denen Windows Server 2019, Windows Server 2016, Windows Server 2012 R2 und in eingeschränkten Fällen Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird.

Die Remoteserver-Verwaltungstools für Windows 10 umfassen Unterstützung für die Remoteverwaltung von Computern, auf denen die Server Core-Installationsoption oder die Konfiguration „Minimale Serverschnittstelle“ von Windows Server 2016. Windows Server 2012 R2 ausgeführt wird (in eingeschränkten Fällen auch die Server Core-Installationsoptionen von Windows Server 2012). Die Remoteserver-Verwaltungstools für Windows 10 können nicht unter allen Versionen des Windows Server-Betriebssystems installiert werden.

### <a name="tools-available-in-this-release"></a>Tools, die in dieser Version verfügbar sind
Eine Liste der Tools, die in den Remoteserver-Verwaltungstools für Windows 10 verfügbar sind, finden Sie in der Tabelle unter [Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT) für Windows-Betriebssysteme](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

### <a name="system-requirements"></a>Systemanforderungen
Remoteserver-Verwaltungstools für Windows 10 können nur auf Computern mit Windows 10 installiert werden. Remoteserver-Verwaltungstools können nicht auf Computern mit Windows RT 8.1 oder auf anderen SOC-Geräten (System on a Chip) installiert werden.

Remoteserver-Verwaltungstools für Windows 10 können unter x86- und x64-basierten Editionen von Windows 10 ausgeführt werden.

> [!IMPORTANT]
> Es ist nicht ratsam, Remoteserver-Verwaltungstools für Windows 10 auf einem Computer zu installieren, auf dem Verwaltungsprogramme für Windows 8.1, Windows 8, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 oder Windows 2000 Server ausgeführt werden. Entfernen Sie alle älteren Versionen von Verwaltungsprogrammen oder Remoteserver-Verwaltungstools – einschließlich ältere Vorabversionen und Versionen der Tools für unterschiedliche Sprachen oder Gebietsschemas – vom Computer, bevor Sie die Remoteserver-Verwaltungstools für Windows 10 installieren.

Um diese Version von Server-Manager für den Zugriff auf und die Verwaltung von Remoteservern mit Windows Server 2012 R2 , Windows Server 2012 oder Windows Server 2008 R2 zu verwenden, müssen Sie mehrere Updates installieren, um die älteren Windows Server-Betriebssysteme mit Hilfe von Server-Manager verwaltbar zu machen. Ausführliche Informationen dazu, wie Sie Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 für die Verwaltung mit dem Server-Manager in den Remoteserver-Verwaltungstools für Windows 10 vorbereiten können, finden Sie unter [Verwalten von mehreren Remoteservern mit dem Server-Manager](https://technet.microsoft.com/library/hh831456.aspx).

Die Windows PowerShell- und Server-Manager-Remoteverwaltung muss auf Remoteservern aktiviert werden, um diese mithilfe von Tools verwalten zu können, die Teil der Remoteserver-Verwaltungstools für Windows 10 sind. Remoteverwaltung ist auf Servern mit Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 standardmäßig aktiviert. Weitere Informationen zum Aktivieren der deaktivierten Remoteverwaltung finden Sie unter [Verwalten von mehreren Remoteservern mit dem Server-Manager](https://go.microsoft.com/fwlink/p/?LinkId=241358).

## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>Installieren, Deinstallieren und Aktivieren/Deaktivieren der RSAT-Tools

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-or-later"></a>Verwenden von FoD (Features on Demand, Features bei Bedarf), um bestimmte RSAT-Tools unter dem Windows 10-Update vom Oktober 2018 oder höher zu installieren

Ab dem Windows 10-Update vom Oktober 2018 ist RSAT als Sammlung von **Features bei Bedarf** in Windows 10 selbst enthalten. Anstatt ein RSAT-Paket herunterzuladen, können Sie jetzt einfach zu **Optionale Features verwalten** unter **Einstellungen** navigieren und auf **Feature hinzufügen** klicken, um die Liste der verfügbaren RSAT-Tools anzuzeigen. Wählen Sie die gewünschten RSAT-Tools aus, und installieren Sie sie. Um den Installationsfortschritt anzuzeigen, klicken Sie auf die Schaltfläche **Zurück**, um den Status auf der Seite **Optionale Features verwalten** anzuzeigen.

Weitere Informationen finden Sie in der [Liste der RSAT-Tools, die über **Features bei Bedarf** verfügbar ist](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat). Zusätzlich zur Installation über die grafische App für **Einstellungen** können Sie auch bestimmte RSAT-Tools über die Befehlszeile oder über Automatisierung mithilfe von [**DISM/Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods) installieren.

Ein Vorteil von Features bei Bedarf besteht darin, dass die installierten Features über Windows 10-Versionsupgrades hinweg bestehen bleiben.

#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>So deinstallieren Sie bestimmte RSAT-Tools unter dem Windows 10-Update vom Oktober 2018 oder höher (nach der Installation mit FoD)

Öffnen Sie unter Windows 10 die App **Einstellungen**, navigieren Sie zu **Optionale Features verwalten**, wählen Sie die gewünschten RSAT-Tools aus, die Sie entfernen möchten, und deinstallieren Sie sie dann. Beachten Sie, dass Abhängigkeiten in einigen Fällen manuell deinstalliert werden müssen. Insbesondere wenn das RSAT-Tool A vom RSAT-Tool B benötigt wird, tritt bei der Deinstallation von RSAT-Tool A ein Fehler auf, wenn RSAT-Tool B noch installiert ist. Deinstallieren Sie in diesem Fall zuerst das RSAT-Tool B, und deinstallieren Sie dann das RSAT-Tool A. Beachten Sie auch, dass das Deinstallieren eines RSAT-Tools in einigen Fällen möglicherweise zu gelingen scheint, auch wenn das Tool noch installiert ist. In diesem Fall wird das Tool durch das Neustarten des PCs entfernt.

Weitere Informationen finden Sie in der [Liste der RSAT-Tools und seiner Abhängigkeiten](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat). Zusätzlich zur Deinstallation über die grafische App für Einstellungen können Sie auch bestimmte RSAT-Tools über die Befehlszeile oder über Automatisierung mithilfe von [**DISM/Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods) deinstallieren.

### <a name="when-to-use-which-rsat-version"></a>Wann sollte welche RSAT-Version verwendet werden?

Wenn Sie eine Version von Windows 10 vor dem Update vom Oktober 2018 (1809) verwenden, können Sie **Features bei Bedarf** nicht verwenden. Sie müssen das RSAT-Paket herunterladen und installieren.

- **Installieren Sie RSAT-FoDs direkt aus Windows 10, wie oben beschrieben**: Bei der Installation unter Windows 10, Update vom Oktober 2018 (1809) oder höher für die Verwaltung von Windows Server 2019 oder früheren Versionen.

- **Laden Sie das WS_1803 RSAT-Paket herunter, und installieren Sie es wie unten beschrieben**: Bei der Installation unter Windows 10, Update vom April 2018 (1803) oder früher für die Verwaltung von Windows Server, Version 1803 oder Windows Server, Version 1709.

- **Laden Sie das WS_2016 RSAT-Paket herunter, und installieren Sie es wie unten beschrieben**: Bei der Installation unter Windows 10, Update vom April 2018 (1803) oder früher für die Verwaltung von Windows Server 2016 oder früheren Versionen.

#### <a name="BKMK_installthresh"></a>Herunterladen des RSAT-Pakets, um die Remoteserver-Verwaltungstools für Windows 10 zu installieren

1.  Laden Sie die Remoteserver-Verwaltungstools für das Windows 10-Paket aus dem [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=404281) herunter. Sie können das Installationsprogramm entweder über die Download Center-Website ausführen oder das Downloadpaket auf einem lokalen Computer oder einer lokalen Freigabe speichern.

    > [!IMPORTANT]
    > Sie können Remoteserver-Verwaltungstools für Windows 10 nur auf Computern installieren, die Windows 10 ausführen. Remoteserver-Verwaltungstools können nicht auf Computern mit Windows RT 8.1 oder auf anderen SOC-Geräten (System on a Chip) installiert werden.

2.  Wenn Sie das Downloadpaket auf einem lokalen Computer oder einer Freigabe speichern, doppelklicken Sie auf das Installationsprogramm **WindowsTH-KB2693643-x64.msu** oder **WindowsTH-KB2693643-x86.msu**. Dies richtet sich nach der Architektur des Computers, auf dem Sie die Tools installieren möchten.

3.  Wenn Sie im Dialogfeld **Eigenständiges Windows Update-Installationsprogramm** zum Installieren des Updates aufgefordert werden, klicken Sie auf **Ja**.

4.  Lesen Sie die Lizenzbedingungen, und akzeptieren Sie sie. Klicken Sie auf **Ich stimme zu**.

5.  Es dauert einige Minuten, bis die Installation beendet ist.

##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-after-rsat-package-install"></a>So deinstallieren Sie die Remoteserver-Verwaltungstools für Windows 10 (nach der Installation des RSAT-Pakets)

1. Klicken Sie auf dem Desktop auf **Start**, **Alle Apps**, **Windows System**und **Systemsteuerung**.

2. Klicken Sie unter **Programme**auf **Programm deinstallieren**.

3. Klicken Sie auf **Installierte Updates anzeigen**.

4. Klicken Sie mit der rechten Maustaste auf **Update für Microsoft Windows (KB2693643)** , und klicken Sie dann auf **Deinstallieren**.

5. Wenn Sie gefragt werden, ob Sie das Update wirklich deinstallieren möchten, klicken Sie auf **Ja**.
   E
   ##### <a name="to-turn-off-specific-tools-after-rsat-package-install"></a>So deaktivieren Sie bestimmte Tools (nach der Installation des RSAT-Pakets)

6. Klicken Sie auf dem Desktop auf **Start**, **Alle Apps**, **Windows System**und **Systemsteuerung**.

7. Klicken Sie auf **Programme**und dann unter **Programme und Features** auf **Windows-Features ein- oder ausschalten**.

8. Erweitern Sie im Dialogfeld **Windows-Features** die Option **Remoteserver-Verwaltungstools**und dann entweder den Unterpunkt **Rollenverwaltungstools** oder **Featureverwaltungstools**.

9. Deaktivieren Sie die Kontrollkästchen für alle Tools, die Sie deaktivieren möchten.

   > [!NOTE]
   > Wenn Sie Server-Manager deaktivieren, muss der Computer neu gestartet werden, und Tools, auf die über das Menü **Extras** von Server-Manager zugegriffen werden konnte, müssen über den Ordner **Verwaltungstools** geöffnet werden.

10. Klicken Sie auf **OK**, wenn Sie alle Tools deaktiviert haben, die Sie nicht verwenden möchten.

### <a name="run-remote-server-administration-tools"></a>Ausführen der Remoteserver-Verwaltungstools

> [!NOTE]
> Nach der Installation der Remoteserver-Verwaltungstools für Windows 10 wird der Ordner **Verwaltungstools** im **Startmenü** angezeigt. Sie können von folgenden Orten auf die Tools zugreifen.
>
> -   Das Menü **Extras** in der Server-Manager-Konsole.
> -   **Systemsteuerung\System und Sicherheit\Verwaltungstools**
> -   Eine Verknüpfung aus dem Ordner **Verwaltungstools** , die auf dem Desktop gespeichert wird (klicken Sie dazu mit der rechten Maustaste auf den Link **Systemsteuerung\System und Sicherheit\Verwaltungstools** und dann auf **Verknüpfung erstellen**).

Die als Teil der Remoteserver-Verwaltungstools für Windows 10 installierten Tools können nicht zum Verwalten des lokalen Clientcomputers verwendet werden. Unabhängig vom ausgeführten Tool müssen Sie einen Remoteserver oder mehrere Remoteserver angeben, für die das Tool ausgeführt werden soll. Da die meisten Tools in Server-Manager integriert sind, fügen Sie Remoteserver, die Sie verwalten möchten, dem Server Manager-Serverpool hinzu. Danach können Sie den Server mit den Tools im Menü **Extras** verwalten. Weitere Informationen zum Hinzufügen von Servern zum Serverpool und zum Erstellen benutzerdefinierter Gruppen von Servern finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://go.microsoft.com/fwlink/p/?LinkId=241353) und [Erstellen und Verwalten von Servergruppen](https://go.microsoft.com/fwlink/?LinkId=247328).

In den Remoteserver-Verwaltungstools für Windows 10 wird auf alle GUI-basierten Serververwaltungstools (z. B. MMC-Snap-Ins und Dialogfelder) über das Menü **Extras** der Server-Manager-Konsole zugegriffen. Obwohl auf dem Computer mit den Remoteserver-Verwaltungstools für Windows 10 ein clientbasiertes Betriebssystem ausgeführt wird, wird Server-Manager (in Remoteserver-Verwaltungstools für Windows 10 integriert) auf dem Clientcomputer standardmäßig automatisch geöffnet. Beachten Sie, dass in der Server-Manager-Konsole, die auf einem Clientcomputer ausgeführt wird, keine Seite **Lokaler Server** vorhanden ist.

##### <a name="to-start-server-manager-on-a-client-computer"></a>So starten Sie den Server-Manager auf einem Clientcomputer

1.  Klicken Sie im Menü **Start** auf **Alle Apps**und **Verwaltungstools**.

2.  Klicken Sie im Ordner **Verwaltungstools** auf **Server-Manager**.

Obwohl sie im Menü **Extras** der Server-Manager-Konsole nicht aufgeführt sind, werden Windows PowerShell-Cmdlets und Eingabeaufforderung-Verwaltungstools für Rollen und Features ebenfalls als Teil der Remoteserver-Verwaltungstools installiert. Wenn Sie z. B. eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten („Als Administrator ausführen“) öffnen und das Cmdlet `Get-Command -Module RDManagement` ausführen, ist in den Ergebnissen eine Liste von Remotedesktopdienste-Cmdlets enthalten, die nach der Installation der Remoteserver-Verwaltungstools für die Ausführung auf dem lokalen Computer verfügbar sind. Dazu müssen die Cmdlets jedoch einen Remoteserver als Ziel verwenden, auf dem die Rolle „Remotedesktopdienste“ ganz oder teilweise ausgeführt wird.

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>So starten Sie Windows PowerShell mit erhöhten Benutzerrechten („Als Administrator ausführen“)

1.  Klicken Sie im Menü **Start** auf **Alle Apps**, **Windows System**und **Windows PowerShell**.

2.  Wenn Sie Windows PowerShell als Administrator über den Desktop ausführen möchten, klicken Sie mit der rechten Maustaste auf die **Windows PowerShell**-Verknüpfung und dann auf **Als Administrator ausführen**.

> [!NOTE]
> Sie können eine Windows PowerShell-Sitzung starten, die einen bestimmten Server als Ziel verwendet, indem Sie mit der rechten Maustaste auf einer Rollen- oder Gruppenseite von Server-Manager auf einen verwalteten Server klicken und dann auf **Windows PowerShell** klicken.


## <a name="known-issues"></a>Bekannte Probleme

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**Problem**: RSAT-FoD-Installation schlägt mit Fehlercode 0x800f0954 fehl

> **Auswirkungen**: RSAT-FoDs unter Windows 10, Version 1809 (Update vom Oktober 2018) in WSUS-/Configuration Manager-Umgebungen
> 
> **Lösung**: Zum Installieren von FoDs auf einem in die Domäne eingebundenen PC, der Updates über WSUS oder Configuration Manager erhält, müssen Sie eine Gruppenrichtlinieneinstellungen ändern, um das Herunterladen von FoDs direkt von Windows Update oder aus einer lokalen Freigabe zu aktivieren. Weitere Informationen und Anweisungen zum Ändern dieser Einstellung finden Sie unter [Vorgehensweise: Verfügbarmachen von Features on Demand und Language Packs bei Verwendung von WSUS/SCCM](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs).

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**Problem**: RSAT-FoD-Installation über die App „Einstellungen“ zeigt Status/Fortschritt nicht an

> **Auswirkungen**: RSAT-FoDs unter Windows 10, Version 1809 (Update vom Oktober 2018)
> 
> **Lösung**: Um den Installationsfortschritt anzuzeigen, klicken Sie auf die Schaltfläche **Zurück**, um den Status auf der Seite **Optionale Features verwalten** anzuzeigen.

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**Problem**: RSAT-FoD-Deinstallation über die App „Einstellungen“ schlägt möglicherweise fehl

> **Auswirkungen**: RSAT-FoDs unter Windows 10, Version 1809 (Update vom Oktober 2018)
> 
> **Lösung**: In einigen Fällen sind Deinstallationsfehler darauf zurückzuführen, dass Abhängigkeiten manuell deinstalliert werden müssen. Insbesondere wenn das RSAT-Tool A vom RSAT-Tool B benötigt wird, tritt bei der Deinstallation von RSAT-Tool A ein Fehler auf, wenn RSAT-Tool B noch installiert ist. Deinstallieren Sie in diesem Fall zuerst das RSAT-Tool B, und deinstallieren Sie dann das RSAT-Tool A. Weitere Informationen finden Sie in der Liste der RSAT-FoDs einschließlich ihrer Abhängigkeiten.

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**Problem**: Die RSAT-FoD-Installation ist anscheinend erfolgreich, aber das Tool ist weiterhin installiert.

> **Auswirkungen**: RSAT-FoDs unter Windows 10, Version 1809 (Update vom Oktober 2018)
> 
> **Lösung**: Das Tool wird durch Neustarten des PCs entfernt.

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**Problem**: RSAT fehlt nach dem Windows 10-Upgrade

> **Auswirkungen**: Beliebige RSAT .MSU-Paketinstallation (vor RSAT-FoDs) wird nicht automatisch neu installiert.
> 
> **Lösung**: Eine RSAT-Installation kann über Betriebssystemupgrades hinweg nicht beibehalten werden, weil RSAT .MSU als Windows Update-Paket übermittelt wird. Installieren Sie RSAT nach dem Upgrade von Windows 10 erneut. Beachten Sie, dass diese Einschränkung einer der Gründe für die Umstellung auf FoDs ab Windows 10, Version 1809 ist. Die installierten RSAT-FoDs bleiben in zukünftigen Windows 10-Versionsupgrades erhalten.

## <a name="see-also"></a>Weitere Informationen
>- [Remoteserver-Verwaltungstools für Windows 10](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Remoteserver-Verwaltungstools (Remote Server Administration Tools, RSAT) für Windows Vista, Windows 7, Windows 8, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 und Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?LinkID=221055)
