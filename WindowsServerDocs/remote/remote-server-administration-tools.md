---
title: Remoteserver-Verwaltungstools
description: Oberste Ebene Thema für den Remoteserver-Verwaltungstools
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-rsat
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: d54a1f5e-af68-497e-99be-97775769a7a7
author: coreyp-at-msft
ms.author: coreyp
manager: dansimp
ms.openlocfilehash: cc4b0eb51b477ec175040b46c9563f81955c0be3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59846211"
---
# <a name="remote-server-administration-tools"></a>Remoteserver-Verwaltungstools

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema unterstützt Remote Server Administration Tools für Windows 10.

> [!IMPORTANT]
> Ab Windows 10 Oktober 2018 Update, Remoteserver-Verwaltungstools wird als eine Reihe von **Features bei Bedarf** unter Windows 10 selbst. Finden Sie unter **verwenden die RSAT-Clientversion** unten installationsanweisungen.

Remoteserver-Verwaltungstools kann IT-Administratoren, die Windows Server-Rollen und Features von Windows 10-PCs zu verwalten.

Remoteserver-Verwaltungstools umfassen, Server-Manager, Microsoft Management Console (Mmc)-Snap-ins, Konsolen, Windows PowerShell-Cmdlets und Anbieter, sowie einige Befehlszeilentools zum Verwalten von Rollen und Features, die auf Windows Server ausgeführt.

Remoteserver-Verwaltungstools umfasst Windows PowerShell-Cmdlet-Module, die verwendet werden können, zum Verwalten von Rollen und Features, die auf Remoteservern ausgeführt werden. Obwohl Windows PowerShell-Remoteverwaltung unter Windows Server 2016 standardmäßig aktiviert ist, ist es nicht standardmäßig unter Windows 10 aktiviert. Führen Sie zur Ausführung von Cmdlets, die Teil der Remoteserver-Verwaltungstools für einen Remoteserver `Enable-PSremoting` in einer Windows PowerShell-Sitzung, die mit erhöhten Benutzerrechten (die als Administrator ausführen) auf dem Windows-Clientcomputer nach geöffnet wurde Installieren Remoteserver-Verwaltungstools.

## <a name="BKMK_Thresh"></a>Remoteserver-Verwaltungstools für Windows 10
Verwenden Sie Remote Server Administration Tools für Windows 10, zum Verwalten spezieller Technologies auf Computern, auf denen Windows Server 2016, Windows Server 2012 R2 ausgeführt werden und in selteneren Fällen, Windows Server 2012 oder Windows Server 2008 R2.

Remote Server Administration Tools für Windows 10 bietet Unterstützung für die Remoteverwaltung von Computern, die die Server Core-Installationsoption oder die Minimal Server Interface-Konfiguration von Windows Server 2016, Windows Server 2012 R2 und in eingeschränkten ausgeführt werden Fälle, die Server Core-Installationsoptionen von Windows Server 2012. Allerdings kann nicht Remote Server Administration Tools für Windows 10 unter allen Versionen des Betriebssystems Windows Server installiert werden.

### <a name="tools-available-in-this-release"></a>Tools, die in dieser Version verfügbar sind
eine Liste der Tools in Remote Server Administration Tools für Windows 10, finden Sie unter der Tabelle im [Remote Server-Verwaltungstools (RSAT) für Windows-Betriebssysteme](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

### <a name="system-requirements"></a>Systemanforderungen
Remote Server Administration Tools für Windows 10 kann nur auf Computern installiert werden, auf denen Windows 10 ausgeführt werden. Remoteserver-Verwaltungstools können nicht auf Computern installiert werden, auf denen Windows RT 8.1 oder andere System on a Chip Geräte ausgeführt werden.

Remote Server Administration Tools für Windows 10, die auf sowohl X86-basierten und X64-basierten Editionen von Windows 10 ausgeführt wird.

> [!IMPORTANT]
> Remote Server Administration Tools für Windows 10 sollte nicht auf einem Computer installiert werden, auf dem Verwaltungsprogramme für Windows 8.1, Windows 8, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 oder Windows 2000 Server ausgeführt wird. Entfernen Sie alle ältere Versionen von Verwaltungsprogrammen oder Remoteserver-Verwaltungstools, einschließlich ältere Vorabversionen und Versionen der Tools für unterschiedliche Sprachen oder Gebietsschemas auf dem Computer, vor der Installation von Remote Server Administration Tools für Windows 10.

Um diese Version von Server-Manager zum Zugreifen auf und Verwalten von Remoteservern mit Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 verwenden, müssen Sie mehrere Updates, die älteren Windows Server-Betriebssysteme mit Se verwaltbar zu machen installieren. rvername Manager. Ausführliche Informationen dazu, wie Sie Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 für die Verwaltung mit Server-Manager in Remote Server Administration Tools für Windows 10 vorbereiten können, finden Sie unter [Manage Multiple, Remote Servers mit Server-Manager](https://technet.microsoft.com/library/hh831456.aspx).

Remoteverwaltung von Windows PowerShell und Server-Manager muss auf Remoteservern aktiviert werden, um diese mithilfe von Tools, die Teil der Remote Server Administration Tools für Windows 10 zu verwalten. Remoteverwaltung ist auf Servern standardmäßig aktiviert, die Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 ausgeführt werden. Weitere Informationen zum Aktivieren der deaktivierten Remoteverwaltung finden Sie unter [Verwalten von mehreren Remoteservern mit dem Server-Manager](https://go.microsoft.com/fwlink/p/?LinkId=241358).

## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>Installieren, deinstallieren und das Deaktivieren bzw. Aktivieren von RSAT-tools

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-or-later"></a>Verwenden Sie die Features bei Bedarf (Feature-On) zum Installieren von bestimmten RSAT-Verwaltungstools unter Windows 10 Oktober 2018 aktualisieren zu können, oder höher

Ab Windows 10 Oktober 2018 Update, Remoteserver-Verwaltungstools wird als eine Reihe von **Features bei Bedarf** direkt aus Windows 10. Jetzt anstelle einer RSAT-Paket herunterladen kann man geht einfach zu **optionale Features verwalten** in **Einstellungen** , und klicken Sie auf **Hinzufügen einer Funktion** auf die Liste der verfügbaren RSAT-Tools finden Sie unter. Wählen Sie aus, und installieren Sie die bestimmten RSAT-Tools, die Sie benötigen. Um den Installationsstatus anzuzeigen, klicken Sie auf die **wieder** Schaltfläche, um den Status Anzeigen der **optionale Features verwalten** Seite.

Finden Sie unter den [Liste von RSAT-tools über **Features bei Bedarf**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat). Neben der Installation über die grafische **Einstellungen** -app können Sie auch bestimmte RSAT-Tools über die Befehlszeile oder mithilfe von Automation installieren [ **DISM /Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods).

Ein Vorteil der Features bei Bedarf ist, dass die installierten Features, die über Windows 10-Versionsupgrade beibehalten werden.

#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>So deinstallieren Sie bestimmte RSAT-Tools unter Windows 10 Oktober 2018 aktualisieren oder höher (nach der Installation mit Feature-On)

Öffnen Sie auf Windows 10, die **Einstellungen** wechseln Sie zur app **optionale Features verwalten**, wählen Sie, und deinstallieren Sie die einzelnen RSAT-Tools, die Sie entfernen möchten. Beachten Sie, in einigen Fällen Sie Abhängigkeiten manuell zu deinstallieren müssen. Insbesondere wenn RSAT-Tools ein RSAT-Tools B benötigt wird, fehl wählen Sie dann So deinstallieren Sie RSAT-Tools ein, wenn RSAT-Tools B noch installiert ist. In diesem Fall zuerst deinstallieren Sie RSAT-Tools B, und deinstallieren Sie RSAT-Tools A. Beachten Sie, dass in einigen Fällen, deinstallieren ein Tool für die Remoteserver-Verwaltungstools kann scheinbar erfolgreich verlaufen, obwohl das Tool noch installiert ist. Neustarten des PCs wird in diesem Fall das Entfernen des Tools abgeschlossen werden.

Finden Sie unter den [Liste der RSAT-Tools, einschließlich der Abhängigkeiten](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat). Zusätzlich zur Deinstallation über die grafische Einstellungen-app können Sie auch bestimmte RSAT-Tools über die Befehlszeile oder mithilfe von Automation Deinstallieren [ **DISM /Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods).

### <a name="when-to-use-which-rsat-version"></a>Verwenden Sie die RSAT-Clientversion

Wenn Sie eine Version von Windows 10 vor dem Oktober 2018 (1809) aktualisiert haben, es werden nicht möglich, verwenden Sie **Features bei Bedarf**. Sie benötigen zum Herunterladen und installieren das RSAT-Paket.

- **Installieren Sie Remoteserver-Verwaltungstools FODs direkt von Windows 10, wie oben beschrieben**: Bei der Installation auf Windows 10 Oktober 2018 aktualisieren (1809) oder höher, für die Verwaltung von Windows Server-2019 oder frühere Versionen.

- **Herunterladen und installieren Sie WS_1803 RSAT-Paket aus, wie unten kurz umrissen**: Bei der Installation auf Windows 10 April 2018 aktualisieren (1803) oder früher, für die Verwaltung von Windows Server, Version 1803 oder Windows Server, Version 1709.

- **Herunterladen und installieren Sie WS2016 RSAT-Paket aus, wie unten kurz umrissen**: Bei der Installation auf Windows 10 April 2018 aktualisieren (1803) oder früher, für die Verwaltung von Windows Server 2016 oder früheren Versionen.

#### <a name="BKMK_installthresh"></a>Herunterladen Sie die RSAT-Paket zum Installieren von Remote Server Administration Tools für Windows 10

1.  Laden Sie das Remote Server Administration Tools für Windows 10-Paket aus der [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=404281). Sie können das Installationsprogramm entweder über die Download Center-Website ausführen oder das Downloadpaket auf einem lokalen Computer oder einer lokalen Freigabe speichern.

    > [!IMPORTANT]
    > Sie können nur Remote Server Administration Tools für Windows 10 auf Computern installieren, auf denen Windows 10 ausgeführt werden. Remoteserver-Verwaltungstools können nicht auf Computern installiert werden, auf denen Windows RT 8.1- oder andere System on a Chip Geräte ausgeführt werden.

2.  Wenn Sie das Downloadpaket auf einem lokalen Computer oder einer Freigabe speichern, doppelklicken Sie auf das Installationsprogramm **WindowsTH-KB2693643-x64.msu** oder **WindowsTH-KB2693643-x86.msu**. Dies richtet sich nach der Architektur des Computers, auf dem Sie die Tools installieren möchten.

3.  Wenn Sie im Dialogfeld **Eigenständiges Windows Update-Installationsprogramm** zum Installieren des Updates aufgefordert werden, klicken Sie auf **Ja**.

4.  Lesen Sie die Lizenzbedingungen, und akzeptieren Sie sie. Klicken Sie auf **Ich stimme zu**.

5.  Es dauert einige Minuten, bis die Installation beendet ist.

##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-after-rsat-package-install"></a>So deinstallieren Sie Remoteserver-Verwaltungstools für Windows 10 (nach der Installation der RSAT-Paket)

1.  Klicken Sie auf dem Desktop auf **Start**, **Alle Apps**, **Windows System** und **Systemsteuerung**.

2.  Klicken Sie unter **Programme** auf **Programm deinstallieren**.

3.  Klicken Sie auf **Installierte Updates anzeigen**.

4.  Klicken Sie mit der rechten Maustaste auf **Update für Microsoft Windows (KB2693643)**, und klicken Sie dann auf **Deinstallieren**.

5.  Wenn Sie gefragt werden, ob Sie das Update wirklich deinstallieren möchten, klicken Sie auf **Ja**.
S
##### <a name="to-turn-off-specific-tools-after-rsat-package-install"></a>So deaktivieren Sie bestimmte Tools (nach dem RSAT-Paket installieren)

1.  Klicken Sie auf dem Desktop auf **Start**, **Alle Apps**, **Windows System** und **Systemsteuerung**.

2.  Klicken Sie auf **Programme**und dann unter **Programme und Features** auf **Windows-Features ein- oder ausschalten**.

3.  Erweitern Sie im Dialogfeld **Windows-Features** die Option **Remoteserver-Verwaltungstools**und dann entweder den Unterpunkt **Rollenverwaltungstools** oder **Featureverwaltungstools**.

4.  Deaktivieren Sie die Kontrollkästchen für alle Tools, die Sie deaktivieren möchten.

    > [!NOTE]
    > Wenn Sie aus Server-Manager aktivieren, muss der Computer neu gestartet werden und Tools, die zwar über die **Tools** im Menü von Server-Manager muss geöffnet sein, aus der **Verwaltung** Ordner.

5.  Klicken Sie auf **OK**, wenn Sie alle Tools deaktiviert haben, die Sie nicht verwenden möchten.

### <a name="run-remote-server-administration-tools"></a>Ausführen der Remoteserver-Verwaltungstools

> [!NOTE]
> Nach der Installation von Remote Server Administration Tools für Windows 10, die **Verwaltung** Ordner wird angezeigt, auf die **starten** Menü. Sie können von folgenden Orten auf die Tools zugreifen.
>
> -   Die **Tools** in der Server-Manager-Konsole.
> -   **Systemsteuerung\System und Sicherheit\Verwaltungstools**.
> -   Eine Verknüpfung aus dem Ordner **Verwaltungstools**, die auf dem Desktop gespeichert wird (klicken Sie dazu mit der rechten Maustaste auf den Link **Systemsteuerung\System und Sicherheit\Verwaltungstools** und dann auf **Verknüpfung erstellen**).

Die Tools, die als Teil der Remote Server Administration Tools für Windows 10 installiert können nicht verwendet werden, auf den lokalen Clientcomputer zu verwalten. Unabhängig vom ausgeführten Tool müssen Sie einen Remoteserver oder mehrere Remoteserver vorhanden sind und auf dem zum Ausführen des Tools angeben. Da die meisten Tools mit Server-Manager integriert sind, fügen Sie Remoteserver, die Sie vor der Verwaltung des Servers mithilfe der Tools im Serverpool des Server-Managers verwalten möchten hinzu der **Tools** Menü. Weitere Informationen zum Hinzufügen von Servern zum Serverpool und zum Erstellen benutzerdefinierter Gruppen von Servern finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://go.microsoft.com/fwlink/p/?LinkId=241353) und [Erstellen und Verwalten von Servergruppen](https://go.microsoft.com/fwlink/?LinkId=247328).

In Remoteserver-Verwaltungstools für Windows 10, alle GUI-basierten Serververwaltungstools, z. B. Mmc-Snap-ins und Dialogfelder, erfolgt der Zugriff aus dem **Tools** im Menü der Server-Manager-Konsole. Obwohl der Computer, der Remote Server Administration Tools für Windows 10 ausgeführt wird. eine Client-basiertes Betriebssystem zur Verfügung steht, nach der Installation der Verwaltungstools ausgeführt wird, Server-Manager in Remote Server Administration Tools für Windows 10 enthalten standardmäßig automatisch geöffnet auf dem Clientcomputer. Beachten Sie, dass es keine **lokalen Server** Seite in der Server-Manager-Konsole, die auf einem Clientcomputer ausgeführt wird.

##### <a name="to-start-server-manager-on-a-client-computer"></a>So starten Sie den Server-Manager auf einem Clientcomputer

1.  Klicken Sie im Menü **Start** auf **Alle Apps** und **Verwaltungstools**.

2.  Klicken Sie im Ordner **Verwaltungstools** auf **Server-Manager**.

Obwohl sie in Server-Manager-Konsole nicht aufgeführt sind **Tools** Menü, Windows PowerShell-Cmdlets und Eingabeaufforderung-Verwaltungstools werden auch installiert für Rollen und Features als Teil der Remoteserver-Verwaltungstools. Wenn Sie eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten (als Administrator ausführen) öffnen, und führen Sie das Cmdlet beispielsweise `Get-Command -Module RDManagement`, die Ergebnisse enthalten eine Liste von remote Desktop Services-Cmdlets, die nun auf dem lokalen Computer nach der Ausführung zur Verfügung stehen Installieren Remoteserver-Verwaltungstools, solange die-Cmdlets auf einem Remoteserver gerichtet sind, die ganz oder teilweise von der remote Desktop Services-Rolle ausgeführt wird.

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>So starten Sie Windows PowerShell mit erhöhten Benutzerrechten („Als Administrator ausführen“)

1.  Klicken Sie im Menü **Start** auf **Alle Apps**, **Windows System** und **Windows PowerShell**.

2.  Führen Sie Windows PowerShell als Administrator über den Desktop Maustaste der **Windows PowerShell** Kontextmenü, und klicken Sie dann auf **als Administrator ausführen**.

> [!NOTE]
> Sie können auch eine Windows PowerShell-Sitzung, die einen bestimmten Server ausgerichtet ist, indem Sie mit der rechten Maustaste in eines verwalteten Servers auf einer Rollen- oder Gruppenseite im Server-Manager und klicken Sie dann auf Starten **Windows PowerShell**.


## <a name="known-issues"></a>Bekannte Probleme

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**Problem**: RSAT FOD-Installation schlägt fehl, mit dem Fehlercode 0x800f0954

> **Auswirkungen**: Remoteserver-Verwaltungstools FODs unter Windows 10-1809 (Oktober 2018 Update) in Umgebungen mit WSUS/SCCM

> **Auflösung**: Zum Installieren der Updates über WSUS oder SCCM empfängt FODs auf eine Domäne eingebundenen PC müssen Sie eine gruppenrichtlinieneinstellung herunterladen FODs direkt über Windows Update oder eine lokale Freigabe zu ändern. Weitere Informationen und Anweisungen zum Ändern dieser Einstellung finden Sie unter [wie Funktionen auf Nachfrage und Language Packs zur Verfügung stellen bei der Verwendung von WSUS/SCCM](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs).

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**Problem**: Status/Bearbeitung von RSAT FOD-Installation über die app "Einstellungen" nicht angezeigt.

> **Auswirkungen**: Remoteserver-Verwaltungstools FODs unter Windows 10-1809 (Oktober 2018 Update)

> **Auflösung**: Um den Installationsstatus anzuzeigen, klicken Sie auf die **wieder** Schaltfläche, um den Status Anzeigen der **optionale Features verwalten** Seite.

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**Problem**: RSAT FOD Deinstallation über die app "Einstellungen" kann fehlschlagen.

> **Auswirkungen**: Remoteserver-Verwaltungstools FODs unter Windows 10-1809 (Oktober 2018 Update)

> **Auflösung**: In einigen Fällen sind Deinstallation Fehler aufgrund von müssen Sie Abhängigkeiten manuell zu deinstallieren. Insbesondere wenn RSAT-Tools ein RSAT-Tools B benötigt wird, fehl wählen Sie dann So deinstallieren Sie RSAT-Tools ein, wenn RSAT-Tools B noch installiert ist. In diesem Fall zuerst deinstallieren Sie RSAT-Tools B, und deinstallieren Sie RSAT-Tools A. Finden Sie in der Liste der Remoteserver-Verwaltungstools FODs, einschließlich der Abhängigkeiten.

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**Problem**: RSAT FOD Deinstallation angezeigt wird, erfolgreich ausgeführt werden kann, aber das Tool ist weiterhin installiert.

> **Auswirkungen**: Remoteserver-Verwaltungstools FODs unter Windows 10-1809 (Oktober 2018 Update)

> **Auflösung**: Neustarten des PCs wird das Entfernen des Tools abgeschlossen.

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**Problem**: Remoteserver-Verwaltungstools fehlt, nach dem upgrade von Windows 10

> **Auswirkungen**: Alle Remoteserver-Verwaltungstools. MSU-Paket-Installation (vor der Remoteserver-Verwaltungstools FODs) nicht automatisch neu installiert

> **Auflösung**: Eine Installation der Remoteserver-Verwaltungstools kann nicht bei Betriebssystemupgrades aufgrund der Remoteserver-Verwaltungstools nicht beibehalten werden. MSU, die als ein Windows Update-Paket bereitgestellt werden. Installieren Sie Remoteserver-Verwaltungstools, später ein Upgrade von Windows 10. Beachten Sie, dass diese Einschränkung einen der Gründe warum wir, beginnend mit Windows 10-1809 FODs verschoben haben. RSAT FODs die installiert werden, wird über zukünftige Upgrades von Windows 10-Version beibehalten.

## <a name="see-also"></a>Siehe auch
>- [Remoteserver-Verwaltungstools für Windows 10](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Remoteserver-Verwaltungstools (RSAT) für Windows Vista, Windows 7, Windows 8, WindowsServer 2008, Windows Server 2008 R2, WindowsServer 2012 und Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?LinkID=221055)


