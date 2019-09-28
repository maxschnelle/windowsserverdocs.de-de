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
ms.openlocfilehash: 121914f721cda7cbf0a117527b69568032d5541b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71387090"
---
# <a name="remote-server-administration-tools"></a>Remoteserver-Verwaltungstools

>Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema wird Remoteserver-Verwaltungstools für Windows 10 unterstützt.

> [!IMPORTANT]
> Ab dem Windows 10-Update vom Oktober 2018 ist RSAT als Satz von **Features Bedarfs** gesteuert in Windows 10 enthalten. Weitere Informationen zur Installation finden **Sie unter Wann sollte die RSAT-Version unten verwendet** werden.

RSAT ermöglicht IT-Administratoren die Verwaltung von Windows Server-Rollen und-Features auf einem Windows 10-PC.

Remoteserver-Verwaltungstools umfasst Server-Manager, Microsoft Management Console (MMC)-Snap-Ins,-Konsolen, Windows PowerShell-Cmdlets und-Anbieter sowie einige Befehlszeilen Tools zum Verwalten von Rollen und Features, die unter Windows Server ausgeführt werden.

Remoteserver-Verwaltungstools enthält Windows PowerShell-Cmdlet-Module, die zum Verwalten von Rollen und Features verwendet werden können, die auf Remote Servern ausgeführt werden. Obwohl die Windows PowerShell-Remote Verwaltung unter Windows Server 2016 standardmäßig aktiviert ist, ist Sie unter Windows 10 standardmäßig nicht aktiviert. Zum Ausführen von Cmdlets, die Teil Remoteserver-Verwaltungstools für einen Remote Server sind, führen Sie `Enable-PSremoting` in einer Windows PowerShell-Sitzung aus, die mit erhöhten Benutzerrechten (d. h. als Administrator ausführen) auf dem Windows-Client Computer geöffnet wurde, nachdem Sie installiert haben. Remoteserver-Verwaltungstools.

## <a name="BKMK_Thresh"></a>Remoteserver-Verwaltungstools für Windows 10
Verwenden Sie Remoteserver-Verwaltungstools für Windows 10, um bestimmte Technologien auf Computern zu verwalten, auf denen Windows Server 2016, Windows Server 2012 R2 und in eingeschränkten Fällen Windows Server 2012 oder Windows Server 2008 R2 ausgeführt wird.

Remoteserver-Verwaltungstools für Windows 10 bietet Unterstützung für die Remote Verwaltung von Computern, auf denen die Server Core-Installationsoption oder die Konfiguration der minimalen Server Schnittstelle von Windows Server 2016, Windows Server 2012 R2 und eingeschränkt ausgeführt wird. Fälle, die Server Core-Installationsoptionen von Windows Server 2012. Allerdings können Remoteserver-Verwaltungstools für Windows 10 nicht unter allen Versionen des Windows Server-Betriebssystems installiert werden.

### <a name="tools-available-in-this-release"></a>Tools, die in dieser Version verfügbar sind
eine Liste der Tools, die in Remoteserver-Verwaltungstools für Windows 10 verfügbar sind, finden Sie in der Tabelle in [Remoteserver-Verwaltungstools (RSAT) für Windows-Betriebssysteme](https://support.microsoft.com/help/2693643/remote-server-administration-tools-rsat-for-windows-operating-systems).

### <a name="system-requirements"></a>Systemanforderungen
Remoteserver-Verwaltungstools für Windows 10 kann nur auf Computern installiert werden, auf denen Windows 10 ausgeführt wird. Remoteserver-Verwaltungstools kann nicht auf Computern installiert werden, auf denen Windows RT 8,1 oder andere System-on-Chip-Geräte ausgeführt werden.

Remoteserver-Verwaltungstools für Windows 10 wird auf x86-basierten und x64-basierten Editionen von Windows 10 ausgeführt.

> [!IMPORTANT]
> Remoteserver-Verwaltungstools für Windows 10 sollte nicht auf einem Computer installiert werden, auf dem Verwaltungsprogramme für Windows 8.1, Windows 8, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 oder Windows 2000 Server ausgeführt werden. Entfernen Sie alle älteren Versionen von Verwaltungs Tools Pack oder Remoteserver-Verwaltungstools, einschließlich früherer vorab Versionen und Versionen der Tools für unterschiedliche Sprachen oder Gebiets Schemas vom Computer, bevor Sie die Remote Server Verwaltung installieren. Tools für Windows 10.

Wenn Sie diese Version von Server-Manager für den Zugriff auf und die Verwaltung von Remote Servern mit Windows Server 2012 R2, Windows Server 2012 oder Windows Server 2008 R2 verwenden möchten, müssen Sie mehrere Updates installieren, um die älteren Windows Server-Betriebssysteme mithilfe von SE verwaltbar zu machen. rvername-Manager. Ausführliche Informationen zum Vorbereiten von Windows Server 2012 R2, Windows Server 2012 und Windows Server 2008 R2 für die Verwaltung mithilfe von Server-Manager in Remoteserver-Verwaltungstools für Windows 10 finden Sie unter [Verwalten von mehreren Remote Servern mit dem Server. Manager](https://technet.microsoft.com/library/hh831456.aspx):

Die Remote Verwaltung von Windows PowerShell und Server-Manager muss auf Remote Servern aktiviert sein, um diese mithilfe von Tools verwalten zu können, die Bestandteil von Remoteserver-Verwaltungstools für Windows 10 sind. Die Remote Verwaltung ist auf Servern mit Windows Server 2016, Windows Server 2012 R2 und Windows Server 2012 standardmäßig aktiviert. Weitere Informationen zum Aktivieren der deaktivierten Remoteverwaltung finden Sie unter [Verwalten von mehreren Remoteservern mit dem Server-Manager](https://go.microsoft.com/fwlink/p/?LinkId=241358).

## <a name="install-uninstall-and-turn-offon-rsat-tools"></a>Installieren, deinstallieren und Deaktivieren von RSAT-Tools

### <a name="use-features-on-demand-fod-to-install-specific-rsat-tools-on-windows-10-october-2018-update-or-later"></a>Verwenden Sie Features on Demand (FOD), um bestimmte RSAT-Tools unter Windows 10-Update vom Oktober 2018 oder später zu installieren.

Ab dem Windows 10-Update vom Oktober 2018 ist RSAT als Satz von **Features bei Bedarf** direkt von Windows 10 enthalten. Anstatt ein RSAT-Paket herunterzuladen, können Sie die **Option optionale Features** in den **Einstellungen** verwalten und dann auf **Funktion hinzufügen** klicken, um die Liste der verfügbaren RSAT-Tools anzuzeigen. Wählen Sie die gewünschten RSAT-Tools aus, und installieren Sie Sie. Um den Installationsfortschritt anzuzeigen, klicken Sie auf die Schaltfläche **zurück** , um den Status auf der Seite **optionale Features verwalten** anzuzeigen.

Weitere Informationen finden Sie [in der Liste der verfügbaren RSAT-Tools über **Features bei Bedarf**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat). Zusätzlich zur Installation über die app "grafische **Einstellungen** " können Sie auch bestimmte RSAT-Tools über die Befehlszeile oder die Automatisierung mithilfe von " [**dismus/Add-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)" installieren.

Ein Vorteil von Features bei Bedarf besteht darin, dass die installierten Features über Windows 10-Versions Upgrades hinweg beibehalten werden.

#### <a name="to-uninstall-specific-rsat-tools-on-windows-10-october-2018-update-or-later-after-installing-with-fod"></a>So deinstallieren Sie bestimmte RSAT-Tools unter Windows 10 Oktober 2018 Update oder höher (nach der Installation mit FOD)

Öffnen Sie unter Windows 10 die app " **Einstellungen** ", navigieren Sie zu " **optionale Features verwalten**", und wählen Sie die gewünschten RSAT-Tools aus, die Sie entfernen möchten. Beachten Sie, dass die Abhängigkeiten in einigen Fällen manuell deinstalliert werden müssen. Insbesondere wenn RSAT-Tool a von RSAT-Tool b benötigt wird, tritt bei der Deinstallation von RSAT-Tool a ein Fehler auf, wenn RSAT-Tool b noch installiert ist. Deinstallieren Sie in diesem Fall zuerst RSAT-Tool B, und deinstallieren Sie dann das RSAT-Tool a. Beachten Sie auch, dass das Deinstallieren eines RSAT-Tools in einigen Fällen möglicherweise fehlschlägt, auch wenn das Tool noch installiert ist. In diesem Fall wird durch das Neustarten des PCs das Tool entfernt.

Weitere Informationen finden Sie [in der Liste der RSAT-Tools einschließlich Abhängigkeiten](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-non-language-fod#remote-server-administration-tools-rsat). Neben der Deinstallation über die app "grafische Einstellungen" können Sie auch bestimmte RSAT-Tools über die Befehlszeile oder die Automatisierung mithilfe von " [**dismus/Remove-Capability**](https://docs.microsoft.com/windows-hardware/manufacture/desktop/features-on-demand-v2--capabilities#using-dism-add-capability-to-add-or-remove-fods)" deinstallieren.

### <a name="when-to-use-which-rsat-version"></a>Wann sollte die RSAT-Version verwendet werden?

Wenn Sie vor dem Update vom Oktober 2018 (1809) eine Version von Windows 10 verwenden, können Sie **Features bei Bedarf**nicht verwenden. Sie müssen das RSAT-Paket herunterladen und installieren.

- **Installieren Sie RSAT-fods direkt von Windows 10, wie oben beschrieben**: Bei der Installation unter Windows 10 Oktober 2018 Update (1809) oder höher für die Verwaltung von Windows Server 2019 oder früheren Versionen.

- **Herunterladen und Installieren des WS_1803 RSAT-Pakets, wie unten beschrieben**: Bei der Installation unter Windows 10 April 2018 Update (1803) oder früher für die Verwaltung von Windows Server, Version 1803 oder Windows Server, Version 1709.

- **Herunterladen und Installieren des WS2016 RSAT-Pakets, wie unten beschrieben**: Bei der Installation unter Windows 10 April 2018 Update (1803) oder früher für die Verwaltung von Windows Server 2016 oder früheren Versionen.

#### <a name="BKMK_installthresh"></a>RSAT-Paket herunterladen, um Remoteserver-Verwaltungstools für Windows 10 zu installieren

1.  Laden Sie die Remoteserver-Verwaltungstools für das Windows 10-Paket aus dem [Microsoft Download Center](https://go.microsoft.com/fwlink/?LinkID=404281)herunter. Sie können das Installationsprogramm entweder über die Download Center-Website ausführen oder das Downloadpaket auf einem lokalen Computer oder einer lokalen Freigabe speichern.

    > [!IMPORTANT]
    > Sie können nur Remoteserver-Verwaltungstools für Windows 10 auf Computern installieren, auf denen Windows 10 ausgeführt wird. Remoteserver-Verwaltungstools kann nicht auf Computern installiert werden, auf denen Windows RT 8,1 oder andere System-on-Chip-Geräte ausgeführt werden.

2.  Wenn Sie das Downloadpaket auf einem lokalen Computer oder einer Freigabe speichern, doppelklicken Sie auf das Installationsprogramm **WindowsTH-KB2693643-x64.msu** oder **WindowsTH-KB2693643-x86.msu**. Dies richtet sich nach der Architektur des Computers, auf dem Sie die Tools installieren möchten.

3.  Wenn Sie im Dialogfeld **Eigenständiges Windows Update-Installationsprogramm** zum Installieren des Updates aufgefordert werden, klicken Sie auf **Ja**.

4.  Lesen Sie die Lizenzbedingungen, und akzeptieren Sie sie. Klicken Sie auf **Ich stimme zu**.

5.  Es dauert einige Minuten, bis die Installation beendet ist.

##### <a name="to-uninstall-remote-server-administration-tools-for-windows-10-after-rsat-package-install"></a>So deinstallieren Sie Remoteserver-Verwaltungstools für Windows 10 (nach der Installation des RSAT-Pakets)

1. Klicken Sie auf dem Desktop auf **Start**, **Alle Apps**, **Windows System** und **Systemsteuerung**.

2. Klicken Sie unter **Programme** auf **Programm deinstallieren**.

3. Klicken Sie auf **Installierte Updates anzeigen**.

4. Klicken Sie mit der rechten Maustaste auf **Update für Microsoft Windows (KB2693643)** , und klicken Sie dann auf **Deinstallieren**.

5. Wenn Sie gefragt werden, ob Sie das Update wirklich deinstallieren möchten, klicken Sie auf **Ja**.
   S
   ##### <a name="to-turn-off-specific-tools-after-rsat-package-install"></a>So deaktivieren Sie bestimmte Tools (nach der Installation des RSAT-Pakets)

6. Klicken Sie auf dem Desktop auf **Start**, **Alle Apps**, **Windows System** und **Systemsteuerung**.

7. Klicken Sie auf **Programme**und dann unter **Programme und Features** auf **Windows-Features ein- oder ausschalten**.

8. Erweitern Sie im Dialogfeld **Windows-Features** die Option **Remoteserver-Verwaltungstools**und dann entweder den Unterpunkt **Rollenverwaltungstools** oder **Featureverwaltungstools**.

9. Deaktivieren Sie die Kontrollkästchen für alle Tools, die Sie deaktivieren möchten.

   > [!NOTE]
   > Wenn Sie Server-Manager deaktivieren, muss der Computer neu gestartet werden, und Tools, **auf die über das Menü Extras** von Server-Manager zugegriffen werden kann, müssen über den Ordner **Verwaltung** geöffnet werden.

10. Klicken Sie auf **OK**, wenn Sie alle Tools deaktiviert haben, die Sie nicht verwenden möchten.

### <a name="run-remote-server-administration-tools"></a>Ausführen der Remoteserver-Verwaltungstools

> [!NOTE]
> Nachdem Sie Remoteserver-Verwaltungstools für Windows 10 installiert haben, wird der Ordner **Verwaltungs Tools** im **Startmenü** angezeigt. Sie können von folgenden Orten auf die Tools zugreifen.
>
> -   Das **Menü Extras in der Server-Manager** Konsole.
> -   **Systemsteuerung\System und Sicherheit\Verwaltungstools**.
> -   Eine Verknüpfung aus dem Ordner **Verwaltungstools**, die auf dem Desktop gespeichert wird (klicken Sie dazu mit der rechten Maustaste auf den Link **Systemsteuerung\System und Sicherheit\Verwaltungstools** und dann auf **Verknüpfung erstellen**).

Die Tools, die als Teil von Remoteserver-Verwaltungstools für Windows 10 installiert werden, können nicht zum Verwalten des lokalen Client Computers verwendet werden. Unabhängig davon, welches Tool Sie ausführen, müssen Sie einen Remote Server oder mehrere Remote Server angeben, auf denen das Tool ausgeführt werden soll. Da die meisten Tools in Server-Manager integriert sind, fügen Sie Remote Server, die Sie verwalten möchten, dem Server-Manager Server-Pool hinzu, bevor Sie den Server mit den **Tools im Menü Extras** verwalten. Weitere Informationen zum Hinzufügen von Servern zum Serverpool und zum Erstellen benutzerdefinierter Gruppen von Servern finden Sie unter [Hinzufügen von Servern zu Server-Manager](https://go.microsoft.com/fwlink/p/?LinkId=241353) und [Erstellen und Verwalten von Servergruppen](https://go.microsoft.com/fwlink/?LinkId=247328).

In Remoteserver-Verwaltungstools für Windows 10 wird auf alle GUI-basierten Server Verwaltungs Tools, wie z. b. MMC-Snap-Ins und Dialogfelder, über **das Menü Extras der Server-Manager** Konsole zugegriffen. Obwohl auf dem Computer, auf dem Remoteserver-Verwaltungstools für Windows 10 ausgeführt wird, ein Client basiertes Betriebssystem ausgeführt wird, wird nach der Installation der Tools Server-Manager, der in Remoteserver-Verwaltungstools für Windows 10 enthalten ist, standardmäßig automatisch geöffnet. auf dem Client Computer. Beachten Sie, dass in der Server-Manager-Konsole, die auf einem Client Computer ausgeführt wird, keine Seite **lokaler Server** vorhanden ist.

##### <a name="to-start-server-manager-on-a-client-computer"></a>So starten Sie den Server-Manager auf einem Clientcomputer

1.  Klicken Sie im Menü **Start** auf **Alle Apps** und **Verwaltungstools**.

2.  Klicken Sie im Ordner **Verwaltungstools** auf **Server-Manager**.

Obwohl Sie im Menü Extras der Server-Manager-Konsole nicht aufgeführt sind, werden Windows PowerShell-Cmdlets und Eingabeaufforderung- **Verwaltungs Tools auch** für Rollen und Features im Rahmen Remoteserver-Verwaltungstools installiert. Wenn Sie z. b. eine Windows PowerShell-Sitzung mit erhöhten Benutzerrechten (als Administrator ausführen) öffnen und das Cmdlet `Get-Command -Module RDManagement` ausführen, enthalten die Ergebnisse eine Liste der Remote Desktop Dienste-Cmdlets, die jetzt nach der Installation auf dem lokalen Computer ausgeführt werden können. Remoteserver-Verwaltungstools, sofern die Cmdlets auf einen Remote Server abzielen, der die Rolle "Remote Desktop Dienste" oder einen Teil der Remote Desktop Dienste ausgeführt hat.

##### <a name="to-start-windows-powershell-with-elevated-user-rights-run-as-administrator"></a>So starten Sie Windows PowerShell mit erhöhten Benutzerrechten („Als Administrator ausführen“)

1.  Klicken Sie im Menü **Start** auf **Alle Apps**, **Windows System** und **Windows PowerShell**.

2.  Wenn Sie Windows PowerShell als Administrator über den Desktop ausführen möchten, klicken Sie mit der rechten Maustaste auf die Verknüpfung **Windows PowerShell** , und klicken Sie dann auf **als Administrator ausführen**.

> [!NOTE]
> Sie können eine Windows PowerShell-Sitzung, die auf einen bestimmten Server ausgerichtet ist, auch starten, indem Sie in Server-Manager mit der rechten Maustaste auf einen verwalteten Server auf einer Rollen-oder Gruppenseite klicken und dann auf **Windows PowerShell**klicken.


## <a name="known-issues"></a>Bekannte Probleme

### <a name="issue-rsat-fod-installation-fails-with-error-code-0x800f0954"></a>**Problem**: RSAT-FOD-Installation schlägt fehl mit Fehlercode 0x800f0954

> **Auswirkung**: RSAT-fods unter Windows 10 1809 (Oktober 2018-Update) in WSUS/SCCM-Umgebungen
> 
> **Lösung**: Zum Installieren von fods auf einem in die Domäne eingebundenen PC, von dem Updates über WSUS oder SCCM empfangen werden, müssen Sie eine Gruppenrichtlinie Einstellungen ändern, um das Herunterladen von fods direkt von Windows Update oder einer lokalen Freigabe zu aktivieren. Weitere Informationen und Anweisungen zum Ändern dieser Einstellung finden Sie unter Gewusst [wie: Bedarfs gesteuerte Features und Sprachpakete bei Verwendung von WSUS/SCCM verfügbar machen](https://docs.microsoft.com/windows/deployment/update/fod-and-lang-packs).

---

### <a name="issue-rsat-fod-installation-via-settings-app-does-not-show-statusprogress"></a>**Problem**: RSAT-FOD-Installation über die app "Einstellungen" zeigt Status/Fortschritt nicht an

> **Auswirkung**: RSAT-fods unter Windows 10 1809 (Update vom Oktober 2018)
> 
> **Lösung**: Um den Installationsfortschritt anzuzeigen, klicken Sie auf die Schaltfläche **zurück** , um den Status auf der Seite **optionale Features verwalten** anzuzeigen.

---

### <a name="issue-rsat-fod-uninstallation-via-settings-app-may-fail"></a>**Problem**: RSAT-FOD-Installation über die Einstellungs-APP schlägt möglicherweise fehl

> **Auswirkung**: RSAT-fods unter Windows 10 1809 (Update vom Oktober 2018)
> 
> **Lösung**: In einigen Fällen sind Deinstallations Fehler darauf zurückzuführen, dass Abhängigkeiten manuell deinstalliert werden müssen. Insbesondere wenn RSAT-Tool a von RSAT-Tool b benötigt wird, tritt bei der Deinstallation von RSAT-Tool a ein Fehler auf, wenn RSAT-Tool b noch installiert ist. Deinstallieren Sie in diesem Fall zuerst RSAT-Tool B, und deinstallieren Sie dann das RSAT-Tool a. Weitere Informationen finden Sie in der Liste der RSAT-fods einschließlich Abhängigkeiten.

---

### <a name="issue-rsat-fod-uninstallation-appears-to-succeed-but-the-tool-is-still-installed"></a>**Problem**: Die RSAT-FOD-Installation ist anscheinend erfolgreich, aber das Tool ist weiterhin installiert.

> **Auswirkung**: RSAT-fods unter Windows 10 1809 (Update vom Oktober 2018)
> 
> **Lösung**: Durch Neustarten des PCs wird das Tool entfernt.

---

### <a name="issue-rsat-missing-after-windows-10-upgrade"></a>**Problem**: RSAT fehlt nach dem Windows 10-Upgrade

> **Auswirkung**: Beliebige RSAT. Die MSU-Paketinstallation (vor RSAT-fods) wird nicht automatisch neu installiert.
> 
> **Lösung**: Eine RSAT-Installation kann aufgrund von RSAT nicht über Betriebssystem Upgrades hinweg beibehalten werden. MSU wird als Windows Update Paket übermittelt. Installieren Sie RSAT nach dem Upgrade von Windows 10 erneut. Beachten Sie, dass diese Einschränkung einen der Gründe für die Umstellung auf die fods seit Windows 10 1809 ist. Die installierten RSAT-fods bleiben in zukünftigen Windows 10-Versions Upgrades erhalten.

## <a name="see-also"></a>Siehe auch
>- [Remoteserver-Verwaltungstools für Windows 10](https://go.microsoft.com/fwlink/?LinkID=404281)
>- [Remoteserver-Verwaltungstools (RSAT) für Windows Vista, Windows 7, Windows 8, Windows Server 2008, Windows Server 2008 R2, Windows Server 2012 und Windows Server 2012 R2](https://go.microsoft.com/fwlink/p/?LinkID=221055)
