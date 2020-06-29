---
ms.assetid: c91c7196-ee0d-4856-8cfb-4c38494ccf1f
title: Übersicht über Arbeitsordner
ms.prod: windows-server
ms.technology: storage-work-folders
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 06/15/2020
description: 'Eine Übersicht über Arbeitsordner: eine Server Rolle in Windows Server, die Benutzern eine konsistente Möglichkeit bietet, auf Arbeitsdateien von PCs und Geräten zuzugreifen.'
ms.openlocfilehash: 6385249e15312615ea2ca9145fa4c2ff47bd13d9
ms.sourcegitcommit: 771db070a3a924c8265944e21bf9bd85350dd93c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/27/2020
ms.locfileid: "85475207"
---
# <a name="work-folders-overview"></a>Übersicht über Arbeitsordner

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows 10, Windows 8.1, Windows 7

In diesem Thema werden Arbeitsordner erläutert, ein Rollen Dienst für Dateiserver unter Windows Server, der Benutzern eine konsistente Möglichkeit bietet, von ihren PCs und Geräten auf Ihre Arbeitsdateien zuzugreifen.

Wenn Sie Arbeitsordner auf Windows 10, Windows 7 oder einem Android-oder IOS-Gerät herunterladen oder verwenden möchten, finden Sie hier weitere Informationen:

- [Arbeitsordner für Windows 10](https://support.microsoft.com/help/12370/windows-10-work-folders)
- [Arbeitsordner für Windows 7 (64-Bit-Download)](https://www.microsoft.com/download/details.aspx?id=42558)
- [Arbeitsordner für Windows 7 (32-Bit-Download)](https://www.microsoft.com/download/details.aspx?id=42559)
- [Arbeitsordner für IOS](https://itunes.apple.com/app/work-folders/id950878067)
- [Arbeitsordner für Android](https://play.google.com/store/apps/details?id=com.microsoft.workfolders)

## <a name="role-description"></a>Rollenbeschreibung

 Benutzer können nicht nur mit Firmen-PCs sondern auch mit ihren eigenen Computern und Geräten auf Arbeitsdaten zugreifen und mit ihnen arbeiten. Dies wird als BYOD (bring-your-own-device) bezeichnet. Benutzer erhalten einen komfortablen Ort, um Arbeitsdateien zu speichern und von beliebigem Ort aus darauf zuzugreifen. Organisationen behalten die Kontrolle über Unternehmensdaten durch Speichern der Dateien auf zentral verwalteten Dateiservern und optionale Festlegung von Benutzerrichtlinien für Geräte (z.B. Verschlüsselung und Sperrbildschirmkennwörter).

 Arbeitsordner können mit vorhandenen bereit Stellungen von Ordner Umleitung, Offlinedateien und Basis Ordnern bereitgestellt werden. In Arbeits Ordnern werden Benutzer Dateien in einem Ordner auf dem Server gespeichert, der als *Synchronisierungs Freigabe*bezeichnet wird. Sie können einen Ordner angeben, der bereits Benutzerdaten enthält. Dadurch können Sie Arbeitsordner übernehmen, ohne Server und Daten zu migrieren oder die vorhandene Lösung sofort auszulagern.

## <a name="practical-applications"></a>Praktische Anwendung

 Administratoren können Arbeitsordner verwenden, um Benutzern Zugriff auf Ihre Arbeitsdateien zu gewähren und gleichzeitig zentralisierte Speicherung und Kontrolle über die Daten der Organisation zu behalten. Einige bestimmte Anwendungen für Arbeitsordner umfassen Folgendes:

-   Bereitstellen eines einzelnen Zugriffs Punkts für Arbeitsdateien von der Arbeit eines Benutzers und von persönlichen Computern und Geräten

-   Greifen Sie offline auf Arbeitsdateien zu, und synchronisieren Sie dann mit dem zentralen Dateiserver, wenn der PC oder das Gerät das nächste Internet oder Intranetkonnektivität hat.

-   Bereitstellung mit vorhandenen bereit Stellungen von Ordner Umleitung, Offlinedateien und Basis Ordnern

-   Verwenden vorhandener Technologien zur Dateiserver Verwaltung, z. b. Datei Klassifizierung und Ordner Kontingente, zum Verwalten von Benutzerdaten

-   Angeben von Sicherheitsrichtlinien, um PCs und Geräte des Benutzers anzuweisen, Arbeitsordner zu verschlüsseln und ein Kennwort für den Sperrbildschirm zu verwenden

-   Verwenden des Failoverclustering mit Arbeits Ordnern zum Bereitstellen einer Lösung mit hoher Verfügbarkeit

## <a name="important-functionality"></a>Wichtige Funktionalität

 Arbeitsordner beinhalten die folgenden Funktionen.

| Funktionalität | Verfügbarkeit | BESCHREIBUNG |
| ------------------- | ------------------ | ----------------- |
| Rollen Dienst "Arbeitsordner" in Server-Manager | Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 | Datei-und Speicherdienste bieten eine Möglichkeit, Synchronisierungs Freigaben (Ordner, in denen die Arbeitsdateien des Benutzers gespeichert sind) einzurichten, Arbeitsordner zu überwachen und Synchronisierungs Freigaben und den Benutzer Zugriff zu verwalten |
| Arbeitsordner-Cmdlets | Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 | Ein Windows PowerShell-Modul, das umfassende Cmdlets zum Verwalten von Arbeitsordner Servern enthält |
| Integration von Arbeits Ordnern in Windows | Windows 10<p> Windows 8.1<p> Windows RT 8.1<p> Windows 7 (Download erforderlich) | Arbeitsordner bieten die folgenden Funktionen auf Windows-Computern:<p> -Ein System Steuerungselement, das Arbeitsordner einrichtet und überwacht.<br />-Datei-Explorer-Integration, die den einfachen Zugriff auf Dateien in Arbeits Ordnern ermöglicht<br />-Ein Synchronisierungs Modul, das Dateien an einen und von einem zentralen Dateiserver überträgt und gleichzeitig die Akku Lebensdauer und die Systemleistung maximiert |
| Arbeitsordner-App für Geräte | Android<p> Apple iPhone und iPad® | Eine APP, die gängigen Geräten den Zugriff auf Dateien in Arbeits Ordnern ermöglicht |

## <a name="new-and-changed-functionality"></a>Neue und geänderte Funktionalität

In der folgenden Tabelle werden einige der wichtigsten Änderungen in den Arbeits Ordnern beschrieben.

| Feature/Funktionalität | Neu oder aktualisiert? | Beschreibung |
| ---------------------------- | --------------------- | ----------------- |
| Verbesserte Protokollierung. | Neu in Windows Server 2019 | Ereignisprotokolle auf dem Arbeitsordner Server können zum Überwachen der Synchronisierungs Aktivität und zum Identifizieren von Benutzern verwendet werden, bei denen Synchronisierungs Sitzungen fehlschlagen. Verwenden Sie die Ereignis-ID 4020 im Ereignisprotokoll Microsoft-Windows-syncshare/Operational, um zu ermitteln, für welche Benutzer Synchronisierungs Sitzungen fehlschlagen. Verwenden Sie die Ereignis-ID 7000 und Ereignis-ID 7001 im Ereignisprotokoll Microsoft-Windows-syncshare/Reporting, um Benutzer zu überwachen, die das Hochladen und Herunterladen von Synchronisierungs Sitzungen erfolgreich abgeschlossen haben. |
| Leistungsindikatoren | Neu in Windows Server 2019 | Die folgenden Leistungsindikatoren wurden hinzugefügt: Bytes heruntergeladen/Sek., hochgeladene Bytes/Sek., verbundene Benutzer, heruntergeladene Dateien/Sek., hochgeladene Dateien/Sek., Benutzer mit Änderungs Erkennung, eingehende Anforderungen/Sek. und ausstehende Anforderungen. |
| Verbesserte Serverleistung | Aktualisiert in Windows Server 2019 | Leistungsverbesserungen wurden vorgenommen, um mehr Benutzer pro Server zu verarbeiten. Der Grenzwert pro Server variiert und basiert auf der Anzahl der Dateien und der Datei Änderung. Zum Ermitteln des Limits pro Server sollten Benutzer in Phasen dem Server hinzugefügt werden. |
| On-Demand-Dateizugriff | Zu Windows 10 Version 1803 hinzugefügt | Ermöglicht Ihnen, alle Dateien anzuzeigen und darauf zuzugreifen. Sie steuern, welche Dateien auf dem PC gespeichert und offline verfügbar sind. Die restlichen Dateien sind immer sichtbar und belegen keinen Speicherplatz auf Ihrem PC, aber Sie benötigen eine Verbindung mit dem Dateiserver für Arbeitsordner, um darauf zuzugreifen. |
| Unterstützung für Azure AD-Anwendungs Proxy | Zu Windows 10, Version 1703, Android, IOS hinzugefügt | Remote Benutzer können mithilfe Azure AD Anwendungs Proxys sicher auf Ihre Dateien auf dem Arbeitsordner Server zugreifen. |
| Schnellere Änderungs Replikation | Aktualisiert in Windows 10 und Windows Server 2016 | Werden unter Windows Server 2012 R2 Dateiänderungen auf die Arbeitsordner-Server synchronisiert, werden die Clients nicht über die Änderung benachrichtigt, und es dauert bis zu 10 Minuten, bis die Aktualisierungen verfügbar sind. Bei Verwendung von Windows Server 2016 benachrichtigt der Arbeitsordner Server sofort Windows 10-Clients, und die Dateiänderungen werden sofort synchronisiert. Diese Funktion ist neu in Windows Server 2016 und erfordert einen Windows 10-Client. Wenn Sie einen älteren Client verwenden oder der Server "Arbeitsordner" Windows Server 2012 R2 ist, wird der Client weiterhin alle 10 Minuten nach Änderungen suchen. |
| Integriert in Windows Information Protection (WIP) | Zu Windows 10 Version 1607 hinzugefügt | Wenn ein Administrator WIP bereitstellt, können Arbeitsordner den Schutz von Daten erzwingen, indem die Daten auf dem PC verschlüsselt werden. Die Verschlüsselung verwendet einen Schlüssel, der mit der Unternehmens-ID verknüpft ist, die mithilfe eines unterstützten Pakets für die Verwaltung mobiler Geräte wie Microsoft InTune Remote zurückgesetzt werden kann. |

## <a name="software-requirements"></a>Softwareanforderungen

Für Arbeitsordner gelten die folgenden Softwareanforderungen für Dateiserver und die Netzwerkinfrastruktur:

-   Ein Server, auf dem Windows Server 2019, Windows Server 2016 oder Windows Server 2012 R2 zum Hosting von Synchronisierungs Freigaben mit Benutzer Dateien ausgeführt wird

-   Ein mit dem NTFS-Dateisystem formatiertes Volume zum Speichern von Benutzerdateien

-   Sie müssen Kennwortrichtlinien für Gruppenrichtlinien verwenden, um Kennwortrichtlinien auf Computern mit Windows 7 zu erzwingen. Sie müssen die Computer mit Windows 7 auch aus Kennwortrichtlinien für Arbeitsordner ausschließen (wenn Sie diese verwenden).

-   Ein Serverzertifikat für jeden Dateiserver, der Arbeitsordner hostet. Diese Zertifikate müssen von einer Zertifizierungsstelle (Certification Authority, ca) sein, die von Ihren Benutzern als vertrauenswürdig eingestuft wird – idealerweise eine öffentliche Zertifizierungsstelle.

-   Optionale Eine Active Directory Domain Services-Gesamtstruktur mit den-Schema Erweiterungen in Windows Server 2012 R2 zur Unterstützung der automatischen referenzierende von PCs und Geräten an den korrekten Dateiserver, wenn mehrere Dateiserver verwendet werden.

Für die von Benutzern durchgeführte Synchronisierung über das Internet gelten die folgenden zusätzlichen Anforderungen:

-   Die Möglichkeit, einen Server über das Internet zugänglich zu machen, indem Veröffentlichungs Regeln im Reverseproxy oder Netzwerk Gateway Ihrer Organisation erstellt werden.

-   Optionale Einen öffentlich registrierten Domänen Namen und die Möglichkeit, zusätzliche öffentliche DNS-Einträge für die Domäne zu erstellen

-   (Optional) Active Directory-Verbunddienste (AD FS)-Infrastruktur bei Verwendung der AD FS-Authentifizierung.

Für Arbeitsordner gelten die folgenden Softwareanforderungen für Clientcomputer:

-   Auf PCs und Geräten muss eines der folgenden Betriebssysteme ausgeführt werden:

    -   Windows 10

    -   Windows 8.1

    -   Windows RT 8.1

    -   Windows 7

    -   Android 4,4 KitKat und höher

    -   iOS 10.2 und höher

-   Computer mit Windows 7 müssen eine der folgenden Versionen von Windows ausführen:

    -   Windows 7 Professional

    -   Windows 7 Ultimate

    -   Windows 7 Enterprise

-   Windows 7-PCs müssen mit der Domäne Ihrer Organisation verknüpft werden (Sie können nicht zu einer Arbeitsgruppe hinzugefügt werden).

-   Ausreichend freier Speicherplatz auf einem lokalen NTFS-formatierten Laufwerk, um alle Dateien des Benutzers in Arbeits Ordnern zu speichern, zuzüglich weiterer 6 GB freier Speicherplatz, wenn sich die Arbeitsordner auf dem Systemlaufwerk befinden, wie dies standardmäßig der Fall ist. Für Arbeitsordner wird standardmäßig der folgende Speicherort verwendet: **%UserProfile%\Work Folders**

     Benutzer können den Speicherort jedoch während der Installation ändern (mit dem NTFS-Dateisystem formatierte microSD-Karten und USB-Laufwerke werden als Speicherorte unterstützt, die Synchronisierung wird allerdings beendet, wenn die Laufwerke entfernt werden).

     Die maximale Größe für einzelne Dateien beträgt standardmäßig 10 GB. Es gibt keine Speicherbegrenzung pro Benutzer, Administratoren können jedoch mit der Kontingentfunktion des Ressourcen-Managers für Dateiserver Kontingente implementieren.

-   Arbeitsordner unterstützen nicht das Rollback des Status virtueller Maschinen von virtuellen Client Computern. Führen Sie Sicherungs- und Wiederherstellungsvorgänge stattdessen innerhalb des virtuellen Clientcomputers mithilfe der Systemabbildsicherung oder einer anderen Sicherungsanwendung durch.

## <a name="work-folders-compared-to-other-sync-technologies"></a>Arbeitsordner im Vergleich zu anderen Synchronisierungs Technologien

In der folgenden Tabelle wird erläutert, wie verschiedene Microsoft Sync-Technologien positioniert werden und wann Sie verwendet werden.

| | Arbeitsordner | Offlinedateien | OneDrive for Business | OneDrive |
| - | ------------------ | ------------------- | -------------------------- | -------------- |
| **Zusammenfassung der Technologie** | Synchronisieren von Dateien, die auf einem Dateiserver gespeichert sind, mit PCs und Geräten | Synchronisiert Dateien, die auf einem Dateiserver gespeichert sind, mit PCs, die Zugriff auf das Unternehmensnetzwerk haben (kann durch Arbeitsordner ersetzt werden). | Synchronisiert Dateien, die in Office 365 oder in SharePoint gespeichert sind, mit PCs und Geräten innerhalb oder außerhalb eines Unternehmensnetzwerks und bietet Funktionen für die Zusammenarbeit in Dokumenten. | Synchronisieren persönlicher Dateien, die in onedrive gespeichert sind, mit PCs, Macintosh-Computern und Geräten |
| **Bereitstellen des Benutzer Zugriffs auf Arbeitsdateien** | Ja | Ja | Ja | Nein |
| **Clouddienst** | Keine | Keine | Office 365 | Microsoft OneDrive |
| **Interne Netzwerkserver** | Dateiserver unter Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 | Dateiserver | SharePoint Server (optional) | Keine |
| **Unterstützte Clients** | PCs, Ios, Android | PCs in einem Unternehmensnetzwerk oder über DirectAccess, VPNs oder andere Remote Zugriffs Technologien | PCs, Ios, Android, Windows Phone | PCs, Mac-Computer, Windows Phone, Ios, Android |

> [!NOTE]
>  Zusätzlich zu den in der obigen Tabelle aufgeführten Synchronisierungs Technologien bietet Microsoft andere Replikations Technologien, einschließlich DFS-Replikation, die für die Server-zu-Server-Replikation konzipiert ist, und BranchCache, der als WAN-Beschleunigungs Technologie für Zweigstellen konzipiert ist. Weitere Informationen finden Sie unter [DFS-Namespaces und DFS-Replikation](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) und [Übersicht über BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx) .

## <a name="server-manager-information"></a>Informationen zum Server-Manager

Arbeitsordner sind Teil der Datei-und Speicherdienste-Rolle. Sie können Arbeitsordner mithilfe des Assistenten zum Hinzufügen von Rollen und Features oder des- `Install-WindowsFeature` Cmdlets installieren. Beide Methoden führen folgendes aus:

-   Fügt die **Arbeitsordner** Seite den **Datei-und Speicherdiensten** in Server-Manager

-   Installiert den Windows Sync-Freigabe Dienst, der von Windows Server zum Hosten von Synchronisierungs Freigaben verwendet wird.

-   Hiermit wird das Windows PowerShell-Modul syncshare installiert, um Arbeitsordner auf dem Server zu verwalten.

## <a name="interoperability-with-windows-azure-virtual-machines"></a>Interoperabilität mit virtuellen Computern in Windows Azure

 Sie können diesen Windows Server-Rollen Dienst auf einem virtuellen Computer in Windows Azure ausführen. Dieses Szenario wurde mit Windows Server 2012 R2, Windows Server 2016 und Windows Server 2019 getestet.

Weitere Informationen zu den ersten Schritten mit virtuellen Windows Azure-Computern finden Sie auf der [Windows Azure-Website](http://www.windowsazure.com/documentation/services/virtual-machines).

## <a name="see-also"></a>Siehe auch

| Inhaltstyp | Referenzen |
| ------------------ | ---------------- |
| **Produktbewertung** | -   [Arbeitsordner für Android – veröffentlicht](https://blogs.technet.microsoft.com/filecab/2016/03/16/work-folders-for-android-released) (Blogbeitrag)<br />-   [Arbeitsordner für IOS – iPad-App-Version](https://blogs.technet.com/b/filecab/archive/2015/01/16/work-folders-for-ios-ipad-app-release.aspx) (Blogbeitrag)<br />-   [Einführung in Arbeitsordner unter Windows Server 2012 R2](https://blogs.technet.com/b/filecab/archive/2013/07/09/introducing-work-folders-on-windows-server-2012-r2.aspx) (Blogbeitrag)<br />-   [Einführung in Arbeitsordner](https://channel9.msdn.com/posts/Introduction-to-Work-Folders) (Channel 9-Video)<br />-   [Test Umgebungs Bereitstellung für Arbeitsordner](https://blogs.technet.com/b/filecab/archive/2013/07/10/work-folders-test-lab-deployment.aspx) (Blogbeitrag)<br />-   [Arbeitsordner für Windows 7](https://blogs.technet.com/b/filecab/archive/2014/04/24/work-folders-for-windows-7.aspx) (Blogbeitrag) |
| **Bereitstellung** | -   [Entwerfen einer Arbeitsordner Implementierung](plan-work-folders.md)<br />-   [Bereitstellen von Arbeits Ordnern](deploy-work-folders.md)<br />-   [Bereitstellen von Arbeits Ordnern mit AD FS und webanwendungsproxy (WAP)](deploy-work-folders-adfs-overview.md)<br />-   [Bereitstellen von Arbeits Ordnern mit Azure AD Anwendungs Proxy](https://blogs.technet.microsoft.com/filecab/2017/05/31/enable-remote-access-to-work-folders-using-azure-active-directory-application-proxy/)<br />- [Migrations Handbuch für Offlinedateien (CSC) zu Arbeits Ordnern](https://blogs.technet.microsoft.com/filecab/2016/08/12/offline-files-csc-to-work-folders-migration-guide/)<br />-   [Überlegungen zur Leistung von Arbeitsordner Bereitstellungen](https://blogs.technet.com/b/filecab/archive/2013/11/01/performance-considerations-for-large-scale-work-folders-deployments.aspx)<br />-   [Arbeitsordner für Windows 7 (64-Bit-Download)](https://www.microsoft.com/download/details.aspx?id=42558)<br />-   [Arbeitsordner für Windows 7 (32-Bit-Download)](https://www.microsoft.com/download/details.aspx?id=42559) |
| **Vorgänge** | -   [Arbeitsordner iPad-App: FAQ](https://windows.microsoft.com/windows/work-folders-ipad-faq) (für Benutzer)<br />-   [Arbeitsordner-Zertifikat Verwaltung](https://blogs.technet.com/b/filecab/archive/2013/08/09/work-folders-certificate-management.aspx) (Blogbeitrag)<br />-   Über [Wachen von Windows Server 2012 R2-Arbeitsordner Bereitstellungen](https://blogs.technet.com/b/filecab/archive/2013/10/15/monitoring-windows-server-2012-r2-work-folders-deployments.aspx) (Blogbeitrag)<br />-   [Cmdlets für syncshare (Arbeitsordner) in Windows PowerShell](https://docs.microsoft.com/powershell/module/syncshare/?view=win10-ps)<br />-   [Speicher-und Dateidienste PowerShell-Cmdlets kurz Referenzkarte für Windows Server 2012 R2 Preview Edition](https://blogs.technet.com/b/filecab/archive/2013/07/30/storage-and-file-services-powershell-cmdlets-quick-reference-card-for-windows-server-2012-r2-preview-edition.aspx) |
| **Problembehandlung** | -   [Windows Server 2012 R2 – Auflösen von Port Konflikten mit IIS-Websites und Arbeits Ordnern](https://blogs.technet.com/b/filecab/archive/2013/10/15/windows-server-2012-r2-resolving-port-conflict-with-iis-websites-and-work-folders.aspx) (Blogbeitrag)<br />-   [Häufige Fehler in Arbeits Ordnern](https://social.technet.microsoft.com/wiki/contents/articles/30578.common-errors-in-work-folders.aspx) |
| **Communityressourcen** | -   [Forum zu Datei Diensten und Speicher](https://social.technet.microsoft.com/Forums/windowsserver/home?forum=winserverfiles)<br />-   [Das Speicher Team im Microsoft-Datei CAB-Blog](https://blogs.technet.com/b/filecab/)<br />-   [Fragen Sie den Verzeichnisdienste-Teamblog](https://blogs.technet.com/b/askds/) |
| **Verwandte Technologien** | -   [Speicherung in Windows Server 2016](../storage.yml)<br>-   [Datei-und Speicherdienste](https://technet.microsoft.com/library/hh831487(v=ws.11).aspx)<br />-   [Datei Server Ressourcen-Manager](https://technet.microsoft.com/library/hh831701(v=ws.11).aspx)<br />-   [Ordner Umleitung, Offlinedateien und Roamingbenutzerprofile](https://technet.microsoft.com/library/hh848267(v=ws.11).aspx)<br />-   [BranchCache](https://technet.microsoft.com/library/hh831696(v=ws.11).aspx)<br />-   [DFS-Namespaces und-DFS-Replikation](https://technet.microsoft.com/library/jj127250(v=ws.11).aspx) |
