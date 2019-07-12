---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: Aktualisieren von Domänencontrollern auf Windows Server 2012 R2 und Windows Server 2012
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 6dda30bd15bedab8ea5ca8ca2e9597e1cc196e43
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443053"
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>Aktualisieren von Domänencontrollern auf Windows Server 2012 R2 und Windows Server 2012

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dieses Thema enthält Hintergrundinformationen zu Active Directory Domain Services in Windows Server 2012 R2 und Windows Server 2012 und wird der Prozess zum Upgraden von Domänencontrollern von Windows Server 2008 oder Windows Server 2008 R2 beschrieben.  
  
## <a name="BKMK_UpgradeWorkflow"></a>Upgradeschritte für Domain-controller  
Die empfohlene Vorgehensweise zum Upgrade einer Domäne besteht im Heraufstufen von Domänencontrollern, auf denen neuere Versionen von Windows Server ausgeführt werden, und ältere Domänencontroller nach Bedarf herabzustufen. Diese Methode empfiehlt sich gegenüber einem Upgrade des Betriebssystems auf einem vorhandenen Domänencontroller. Diese Liste umfasst allgemeine Schritte zu befolgen, bevor Sie einen Domänencontroller heraufstufen, der eine neuere Version von Windows Server ausgeführt wird:  
  
1. Stellen Sie sicher, dass der Zielserver die [Systemanforderungen](https://technet.microsoft.com/library/dn303418.aspx)erfüllt.  
2. Lesen Sie unter [Application compatibility](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)nach.  
3. Überprüfen Sie die Sicherheitseinstellungen. Weitere Informationen finden Sie unter [Veraltete Features und Verhaltensänderungen in Bezug auf AD DS unter Windows Server 2012](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures) und [Secure default settings in Windows Server 2008 und Windows Server 2008 R2](https://technet.microsoft.com/library/upgrade-domain-controllers-to-windows-server-2008-r2(WS.10).aspx#BKMK_SecureDefault).  
4. Überprüfen Sie die Verbindung zum Zielserver für den Computer, auf dem Sie die Ausführung des Installationsvorgangs planen.  
5. Überprüfen Sie, ob die erforderlichen Betriebsmasterrollen verfügbar sind.  

   - Zum Installieren des ersten Domänencontrollers, der Windows Server 2012 in einer vorhandenen Domäne und Gesamtstruktur ausgeführt wird, benötigt der Computer, in dem Sie die Installation ausführen, eine Verbindung mit dem Schemamaster zum Ausführen von Adprep/forestprep und dem Infrastrukturmaster zum Ausführen von Adprep / DomainPrep.  
   - Für die Installation des ersten Domänencontrollers in einer Domäne, für die das Gesamtstrukturschema bereits erweitert wurde, benötigen Sie nur eine Verbindung mit dem Infrastrukturmaster.  
   - Sie benötigen eine Verbindung mit dem Domänennamenmaster, um eine Domäne in einer vorhandenen Gesamtstruktur zu installieren oder zu entfernen.  
   - Für jede Domänencontrollerinstallation ist auch eine Verbindung mit dem RID-Master erforderlich.  
   - Wenn Sie den ersten schreibgeschützten Domänencontroller in einer vorhandenen Gesamtstruktur installieren, benötigen Sie eine Verbindung mit dem Infrastrukturmaster für jede Anwendungsverzeichnispartition (auch als NDNC (Non-Domain Naming Context) bezeichnet).  

6. Achten Sie darauf, dass Sie die erforderlichen Anmeldeinformationen zum Ausführen der AD DS-Installation angeben.  

   |Installationsaktion|Anforderungen bezüglich der Anmeldeinformationen|  
   |-----------------------|---------------------------|  
   |Neue Gesamtstruktur installieren|Lokaler Administrator auf dem Zielserver|  
   |Neue Domäne in einer vorhandenen Gesamtstruktur installieren|Organisations-Admins|  
   |Zusätzlichen Domänencontroller in einer vorhandenen Domäne installieren|Domänen-Admins|  
   |adprep/forestprep ausführen|Schema Admins, Organisations-Admins und Domänen-Admins|  
   |adprep/domainprep ausführen|Domänen-Admins|  
   |adprep/domainprep/gpprep ausführen|Domänen-Admins|  
   |adprep/rodcprep ausführen|Organisations-Admins|  

   Sie können Berechtigungen zum Installieren von AD DS delegieren. Weitere Informationen finden Sie unter [Installation Management Tasks](https://technet.microsoft.com/library/cc773327(WS.10).aspx).  

Schritt-für-Schritt-Anleitungen zum Heraufstufen von Windows Server 2012-Domänencontroller (neu und Replikat) mithilfe von Windows PowerShell-Cmdlets und Server-Manager finden Sie unter den folgenden Links:  

- [Installieren von Active Directory-Domänendiensten (Stufe 100)](https://technet.microsoft.com/library/hh472162.aspx)  
- [Installieren einer neuen Windows Server 2012 Active Directory-Gesamtstruktur (Stufe 200)](https://technet.microsoft.com/library/jj574166.aspx)  
- [Installieren eines Replikatdomänencontrollers für Windows Server 2012 in einer vorhandenen Domäne (Stufe 200)](https://technet.microsoft.com/library/jj574134.aspx)  
- [Installieren einer neuen Windows Server 2012 untergeordneten oder Active Directory Tree-Domäne (Stufe 200)](https://technet.microsoft.com/library/jj574105.aspx)  
- [Installieren Sie einen Windows Server 2012 Active Directory-Read-Only Domain Controller (RODC) (Stufe 200)](https://technet.microsoft.com/library/jj574152.aspx)  
- [Schrittweise Anleitung für die Einstellung von Windows Server 2012-Domänencontroller (En-US)](https://social.technet.microsoft.com/wiki/contents/articles/12370.step-by-step-guide-for-setting-up-windows-server-2012-domain-controller-en-us.aspx)  

## <a name="windows-update-considerations"></a>Überlegungen zu Windows

Vor Windows 8 verwaltete Windows Update einen eigenen internen Zeitplan für Suche, Download und Installation von Updates. Dazu musste der Windows Update-Agent ständig im Hintergrund laufen und verbrauchte Speicherplatz und andere Systemressourcen.  
  
Unter Windows 8 und Windows Server 2012 wurde das neue Feature [Automatische Wartung](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx)eingeführt. Automatische Wartung konsolidiert zahlreiche unterschiedliche Features, die bislang allesamt eine eigene Zeitplan- und Ausführungslogik hatten. Dank dieser Konsolidierung verbrauchen all diese Komponenten viel weniger Systemressourcen, arbeiten einheitlich, beachten den neuen [Connected Standby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) für neue Gerätetypen und verbrauchen weniger Batterie auf tragbaren Geräten.  
  
Da Windows Update ein Teil der automatischen Wartung in Windows 8 und Windows Server 2012 ist, gilt der interne Zeitplan zur Konfiguration von Tag und Uhrzeit für die Installation von Updates nicht mehr. Um ein einheitliches und vorhersehbares Neustartverhalten für alle Geräte und Computer in Ihrer Organisation, inklusive derer unter Windows 8 und Windows Server 2012, zu garantieren, lesen Sie den Microsoft KB-Artikel [2885694](https://support.microsoft.com/kb/2885694) (oder das kumulative Rollup für Oktober 2013 [2883201](https://support.microsoft.com/kb/2883201)). Konfigurieren Sie anschließend die Richtlinien gemäß des WSUS-Blogeintrags [Enabling a more predictable Windows Update experience for Windows 8 and Windows Server 2012 (KB 2885694)](http://blogs.technet.com/b/wsus/archive/2013/10/08/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694.aspx).  

## <a name="BKMK_NewWS2012R2"></a>Was ist neu in AD DS unter Windows Server 2012 R2?

In der folgenden Tabelle sind die neuen Features für AD DS in Windows Server 2012 R2 zusammengefasst, und es ist ein Link zu ausführlicheren Informationen angegeben, sofern diese verfügbar sind. Eine ausführlichere Erläuterung einiger Features und ihrer Anforderungen finden Sie unter [What's New in Active Directory in Windows Server 2012 R2](https://technet.microsoft.com/library/dn268294.aspx).  

|Feature|Beschreibung|  
|-----------|---------------|  
|[Workplace Join](https://technet.microsoft.com/library/dn280945.aspx)|Mit diesem Feature können Information-Worker ihre persönlichen Geräte mit der Firma verknüpfen, um Zugang zu Ressourcen und Diensten zu erhalten.|  
|[Webanwendungsproxy](https://technet.microsoft.com/library/dn280942.aspx)|Bietet Zugang zu Webanwendungen mit einem neuen Remotezugriffsrollendienst.|  
|[Active Directory-Verbunddienste (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|AD FS hat die Bereitstellung vereinfacht, erlaubt Benutzern den Zugriff auf Ressourcen mit persönlichen Geräten und unterstützt IT-Abteilungen bei der Verwaltung der Zugriffssteuerung.|  
|[SPN- und UPN-Eindeutigkeit](https://technet.microsoft.com/library/dn535779.aspx)|Domänencontroller unter Windows Server 2012 R2 blockieren die Erstellung doppelter Dienstprinzipalnamen (SPNs) und Benutzerprinzipalnamen (UPNs).|  
|[Winlogon Automatic Restart Sign-On (ARSO)](https://technet.microsoft.com/library/dn535772.aspx)|Ermöglicht Neustart und Verfügbarkeit von Sperrbildschirm-Anwendungen auf Windows 8.1-Geräten.|  
|[TPM-Schlüsselnachweis](https://technet.microsoft.com/library/dn581921.aspx)|Mit diesem Feature können CAs in ausgestellten Zertifikaten auf kryptografische Weise nachweisen, dass der private Schlüssel der Zertifikatanforderung durch ein Trusted Platform Module (TPM) geschützt ist.|  
|[Schutz und Verwaltung von Anmeldeinformationen](https://technet.microsoft.com/library/dn408190.aspx)|Neue Kontrollen zum Schutz von Anmeldeinformationen und zur Domänenauthentifizierung, um Identitätsdiebstahl zu verhindern.|  
|[Veraltung des Dateireplikationsdienst (FRS)](https://technet.microsoft.com/library/dn535775.aspx)|Die Windows Server 2003-Domänenfunktionsebene ist ebenfalls veraltet, da FRS auf funktionaler Ebene zu Replikation von SYSVOL verwendet wird. Wenn Sie also eine neue Domäne auf einem Server unter Windows Server 2012 R2 erstellen, muss die Domänenfunktionsebene Windows Server 2008 oder neuer sein. Sie können immer noch einen Domänencontroller hinzufügen, der Windows Server 2012 R2 mit einer vorhandenen Domäne ausgeführt wird, die über eine Windows Server 2003-Domänenfunktionsebene verfügt; Sie können nicht einfach eine neue Domäne auf dieser Ebene erstellen.|  
|[Neue Domänen- und Gesamtstruktur-Funktionsebenen](../active-directory-functional-levels.md)|Neue Funktionsebenen für Windows Server 2012 R2. In der Domänenfunktionsebene für Windows Server 2012 R2 sind neue Features verfügbar.|  
|[Änderungen am LDAP-Abfrageoptimierer](https://technet.microsoft.com/library/dn535775.aspx)|Leistungsoptimierungen bei der LDAP-Suche und bessere Suchzeiten bei komplexen Abfragen.|  
|[Verbesserungen am Ereignis 1644](https://technet.microsoft.com/library/dn535775.aspx)|Statistiken zu LDAP-Suchergebnissen wurden als Hilfe bei der Problembehandlung zum Ereignis mit der ID 1644 hinzugefügt.|  
|[Durchsatzverbesserung bei Active Directory-Replikation](https://technet.microsoft.com/library/dn535775.aspx)|Verbesserung des maximalen Durchsatzes bei der AD-Replikation von 40Mbps auf ca. 600 Mbps|  

## <a name="BKMK_WhatsNewAD"></a>Was ist neu in AD DS unter Windows Server 2012?

In der folgenden Tabelle sind die neuen Features für AD DS in Windows Server 2012 zusammengefasst, und es ist ein Link zu ausführlicheren Informationen angegeben, sofern diese verfügbar sind. Eine ausführlichere Erläuterung einiger Features und ihrer Anforderungen finden Sie unter [Neuigkeiten in Active Directory Domain Services (AD DS)](https://technet.microsoft.com/library/hh831477.aspx).  
  
|Feature|Beschreibung|  
|-----------|---------------|  
|Aktivierung über Active Directory (AD BA); siehe [Volume Activation Overview](https://technet.microsoft.com/library/hh831612.aspx)|Vereinfacht das Konfigurieren der Verteilung und Verwaltung von Volumenlizenzen für Software.|  
|[Active Directory-Verbunddienste (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|Fügt die Installation von Rollen über den Server-Manager, die einfachere Einrichtung von Vertrauensstellungen, die automatische Verwaltung von Vertrauensstellungen, Unterstützung des SAML-Protokolls und mehr hinzu.|  
|Verlorene Page Flush-Ereignisse in Active Directory|NTDS-ISAM-Ereignis 530 mit Jet-Fehler -1119 wird protokolliert, um verlorene Page Flush-Ereignisse für Active Directory-Datenbanken zu ermitteln.|  
|[Active Directory Papierkorb-Benutzeroberfläche](https://technet.microsoft.com/library/hh831702.aspx#ad_recycle_bin_mgmt)|Active Directory-Verwaltungscenter (ADAC) ermöglicht GUI-Verwaltung der Papierkorbfunktion, die ursprünglich unter Windows Server 2008 R2 eingeführt wurde.|  
|[Active Directory-Replikation und Topologieverwaltung Windows PowerShell-cmdlets](https://technet.microsoft.com/library/hh831757.aspx)|Unterstützt die Erstellung und Verwaltung von Active Directory-Standorten, Standortverknüpfungen, Verbindungsobjekten und mehr mithilfe von Windows PowerShell.|  
|[Dynamische Zugriffssteuerung](https://technet.microsoft.com/library/hh831717.aspx)|Neue anspruchsbasierte Autorisierungsplattform, die das vorhandene Modell der Zugriffssteuerung erweitert.|  
|[Benutzeroberfläche für differenzierte Kennwortrichtlinien](https://technet.microsoft.com/library/hh831702.aspx#fine_grained_pswd_policy_mgmt)|ADAC fügt GUI-Unterstützung für die Erstellung, Bearbeitung und Zuweisung von Kennworteinstellungsobjekten (PSOs) hinzu, die ursprünglich unter Windows Server 2008 eingeführt wurde.|  
|[Gruppenverwaltete Dienstkonten (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)|Neuer Sicherheitsprinzipaltyp, der als gMSA bezeichnet wird. Auf mehreren Hosts ausgeführte Dienste können unter demselben gMSA-Konto ausgeführt werden.|  
|[DirectAccess-Offline-Domänenbeitritt](https://technet.microsoft.com/library/jj574150.aspx)|Erweitert den Offline-Domänenbeitritt durch die Einfügung von DirectAccess-Voraussetzungen.|  
|[Schnelle Bereitstellung über das Klonen virtueller Domänencontroller (DC)](https://technet.microsoft.com/library/hh831734.aspx#virtualized_dc_cloning)|Virtualisierte Domänencontroller können schnell bereitgestellt werden, indem vorhandene virtuelle Domänencontroller mithilfe von Windows PowerShell-Cmdlets geklont werden.|  
|[RID-Pool-Änderungen](https://technet.microsoft.com/library/jj574229.aspx)|Fügt neue Überwachungsereignisse und Kontingente als Schutz vor der übermäßigen Nutzung des globalen RID-Pools hinzu. Verdoppelt optional die Größe des globalen RID-Pools, wenn der ursprüngliche Pool voll ausgelastet ist.|  
|Sicherer Zeitdienst|Erweitert die Sicherheit für W32tm, indem Schlüssel aus der Übertragung entfernt werden, die MD5-Hashfunktionen entfernt werden und für den Server die Authentifizierung mit Windows 8-Zeitclients erzwungen wird.|  
|[USN-rollbackschutz für virtualisierte Domänencontroller](https://technet.microsoft.com/library/hh831734.aspx#safe_virt_dc)|Das versehentliche Wiederherstellen der Sicherungen von Momentaufnahmen virtualisierter Domänencontroller verursacht kein USN-Rollback mehr.|  
|[Windows PowerShell-Verlaufsanzeige](https://technet.microsoft.com/library/hh831702.aspx#windows_powershell_history_viewer)|Ermöglicht Administratoren bei Verwendung des Active Directory-Verwaltungscenters das Anzeigen der Windows PowerShell-Befehle.|  
  
### <a name="BKMK_"></a>Automatische Wartung und Änderungen am Neustartverhalten nach Updates von Windows Update angewendet werden

Vor Windows 8 verwaltete Windows Update einen eigenen internen Zeitplan für Suche, Download und Installation von Updates. Dazu musste der Windows Update-Agent ständig im Hintergrund laufen und verbrauchte Speicherplatz und andere Systemressourcen.  
  
Unter Windows 8 und Windows Server 2012 wurde das neue Feature [Automatische Wartung](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx)eingeführt. Automatische Wartung konsolidiert zahlreiche unterschiedliche Features, die bislang allesamt eine eigene Zeitplan- und Ausführungslogik hatten. Dank dieser Konsolidierung verbrauchen all diese Komponenten viel weniger Systemressourcen, arbeiten einheitlich, beachten den neuen [Connected Standby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) für neue Gerätetypen und verbrauchen weniger Batterie auf tragbaren Geräten.  
  
Da Windows Update ein Teil der automatischen Wartung in Windows 8 und Windows Server 2012 ist, gilt der interne Zeitplan zur Konfiguration von Tag und Uhrzeit für die Installation von Updates nicht mehr. Um ein einheitliches und vorhersehbares Neustartverhalten für alle Geräte und Computer in Ihrer Organisation, inklusive derer unter Windows 8 und Windows Server 2012, zu garantieren, können Sie die folgenden Gruppenrichtlinien-Einstellungen konfigurieren:  

- **Computerkonfiguration | Richtlinien für | Administrative Vorlagen | Windows-Komponenten | Windows Update | Konfigurieren Sie automatische Updates**  
- **Computerkonfiguration | Richtlinien für | Administrative Vorlagen | Windows-Komponenten | Windows Update | Keinen automatischen Neustart durchführen, angemeldete Benutzer**  
- **Computerkonfiguration | Richtlinien für | Administrative Vorlagen | Windows-Komponenten | Wartungsplanungsmodul | Zufällige Verzögerung für Wartung**  

Die folgende Tabelle enthält einige Beispiele für die Konfiguration dieser Einstellungen, um das gewünschte Neustartverhalten zu erreichen.  

|||  
|-|-|  
|**Szenario**|**Empfohlene Konfiguration(en)**|  
|**WSUS verwaltet**<br /><br />– Installieren von Updates einmal pro Woche<br />-Neustart Freitag um 23 Uhr|Automatische Installation für Computer konfigurieren, autom. Neustart bis zum gewünschten Zeitpunkt verhindern<br /><br />**Richtlinie**: Automatische Updates konfigurieren (aktiviert)<br /><br />Automatische Updates konfigurieren: 4 – Autom. herunterladen und laut Zeitplan installieren<br /><br />**Richtlinie**: Keinen automatischen Neustart durchführen, angemeldete Benutzer (deaktiviert)<br /><br />**WSUS-Stichtage**: auf Freitag 23 Uhr einstellen|  
|**WSUS verwaltet**<br /><br />-Installationen von staffeln über unterschiedliche Uhrzeiten/Tage|Richten Sie Zielgruppen für verschiedene Computergruppen ein, die gemeinsam aktualisiert werden sollen<br /><br />Siehe obige Schritte für das vorherige Szenario<br /><br />Unterschiedliche Stichtage für unterschiedliche Zielgruppen|  
|**Nicht von WSUS verwaltet – keine Unterstützung für Stichtage**<br /><br />-Staffeln Installationen über unterschiedliche Uhrzeiten|**Richtlinie**: Automatische Updates konfigurieren (aktiviert)<br /><br />Automatische Updates konfigurieren: 4 – Autom. herunterladen und laut Zeitplan installieren<br /><br />**Registrierungsschlüssel:** Aktivieren Sie die im Microsoft KB-Artikel besprochenen Registrierungsschlüssel [2835627](https://support.microsoft.com/kb/2835627)<br /><br />**Richtlinie:** Zufällige Verzögerung für automatische Wartung (aktiviert)<br /><br />Stellen Sie **Zufällige Verzögerung für automatische Wartung** auf PT6H für eine 6-stündige zufällige Verzögerung, um das folgende Verhalten zu erreichen:<br /><br />-Updates werden an die konfigurierten Wartungszeit plus eine zufällige Verzögerung installiert werden.<br /><br />– Starten Sie für jeden Computer findet genau 3 Tage später statt<br /><br />Alternativ können Sie unterschiedliche Wartungszeiten für einzelne Computergruppen einstellen|  

Weitere Informationen zum Hintergrund dieser Änderungen finden Sie unter [Minimizing restarts after automatic updating in Windows Update](http://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx).  

## <a name="BKMK_InstallationChanges"></a>Änderungen an die Installation von AD DS Server-Rolle

Unter Windows Server 2003 bis Windows Server 2008 R2 haben Sie die x86- oder X64-Version des Befehlszeilentools %%amp;quot;Adprep.exe%%amp;quot; ausgeführt, bevor Sie den Assistenten zum Installieren von Active Directory (Dcpromo.exe) ausgeführt haben. %%amp;quot;Dcpromo.exe%%amp;quot; verfügte über die Optionen für die Installation vom Datenträger oder für die unbeaufsichtigte Installation.  
  
Ab Windows Server 2012 werden Befehlszeileninstallationen mithilfe des ADDSDeployment-Moduls in Windows PowerShell durchgeführt. GUI-basierte Heraufstufungen werden im Server-Manager mithilfe eines vollständig neuen AD DS-Konfigurations-Assistenten durchgeführt. Zur Vereinfachung des Installationsprozesses wurde ADPREP in die AD DS-Installation integriert und wird bei Bedarf automatisch ausgeführt. Die Windows PowerShell basierende AD DS-Konfigurationsassistenten zielt automatisch auf die Schema- und infrastrukturmasterrollen in den Domänen, in denen Domänencontroller hinzugefügt werden, und klicken Sie dann die erforderlichen ADPREP-Befehle auf den relevanten Domänencontrollern Remote ausgeführt.  
  
Anhand von Überprüfungen der Voraussetzungen im AD DS-Konfigurations-Assistenten werden mögliche Fehler vor Beginn der Installation erkannt. Fehlerzustände können korrigiert werden, um Bedenken bei einem teilweise abgeschlossenen Upgrade auszuräumen. Der Assistent exportiert ein Windows PowerShell-Skript mit allen Optionen, die während der grafischen Installation angegeben wurden.  
  
Zusammen führen die Änderungen bei der AD DS-Installation zu einer vereinfachten Installation von Domänencontrollerrollen und tragen zu einer Verringerung der Wahrscheinlichkeit von administrativen Fehlern bei. Dies gilt besonders, wenn Sie mehrere Domänencontroller über globale Regionen und Domänen hinweg einsetzen.  
Ausführlichere Informationen zu GUI- und auf Windows PowerShell basierenden Installationen sowie die Befehlszeilensyntax und Schritt-für-Schritt-Anleitungen finden Sie unter [Install Active Directory Domain Services](https://technet.microsoft.com/library/hh472162.aspx). Für Administratoren, die die Einführung von Schemaänderungen in einer Active Directory-Gesamtstruktur unabhängig von der Installation von Windows Server 2012-Domänencontrollern in einer bestehenden Gesamtstruktur steuern möchten, können Adprep.exe-Befehle weiterhin über eine Eingabeaufforderung mit erhöhten Rechten ausgeführt werden.  

## <a name="BKMK_DeprecatedFeatures"></a>Veraltete Features und verhaltensänderungen in Bezug auf AD DS unter Windows Server 2012

Für AD DS wurden einige Änderungen vorgenommen:  

- **Deprecation of Adprep32.exe**
   - Es ist nur eine Version von Adprep.exe vorhanden. Sie kann bei Bedarf auf 64-Bit-Servern mit Windows Server 2008 oder höher ausgeführt werden. Außerdem ist die Remoteausführung der Version möglich. Dies ist auch zwingend erforderlich, wenn die Ziel-Betriebsmasterrolle auf einem 32-Bit-Betriebssystem oder unter Windows Server 2003 gehostet wird.  
- **Veraltung von Dcpromo.exe**
   - Dcpromo ist mittlerweile veraltet in Windows Server 2012 nur noch mit einer Antwortdatei oder Befehlszeilenparametern, damit Organisationen Zeit für die Umstellung der vorhandenen Automatisierung auf die neuen Windows PowerShell-Installationsoptionen haben ausgeführt werden kann.  
- **LMHash für Benutzerkonten deaktiviert**
  - Mit sicheren Standardeinstellungen in Sicherheitsvorlagen unter Windows Server 2008, Windows Server 2008 R2 und Windows Server 2012 wird die NoLMHash-Richtlinie aktiviert, die in den Sicherheitsvorlagen von Windows 2000- und Windows Server 2003-Domänencontrollern deaktiviert ist. Deaktivieren Sie je nach Bedarf die NoLMHash-Richtlinie für LMHash-abhängige Clients, indem Sie die Schritte im KB-Artikel [946405](https://support.microsoft.com/kb/946405)verwenden.  

Ab Windows Server 2008 haben-Domänencontroller auch die folgenden sicheren Standardeinstellungen, gegenüber den Domänencontrollern, auf denen Windows Server 2003 oder Windows 2000 ausgeführt.

|||||  
|-|-|-|-|  
|Verschlüsselungstyp oder -richtlinie|Windows Server 2008-Standardeinstellung|Windows Server 2012- und Windows Server 2008 R2-Standardeinstellung|Kommentar|  
|AllowNT4Crypto|Disabled|Disabled|SMB-Clients (Server Message Block) von Drittanbietern sind möglicherweise nicht mit den sicheren Standardeinstellungen auf Domänencontrollern kompatibel. Um Interoperabilität zu erreichen, können diese Einstellungen jeweils auch gelockert werden, jedoch nur auf Kosten der Sicherheit. Weitere Informationen finden Sie unter [Artikel 942564](https://go.microsoft.com/fwlink/?LinkId=164558) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=164558).|  
|DES|Enabled|Disabled|[Artikel 977321](https://go.microsoft.com/fwlink/?LinkId=177717) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=177717)|  
|CBT/Erweiterter Schutz für integrierte Authentifizierung|Nicht zutreffend|Enabled|Finden Sie unter [Microsoft Security Advisory (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) (https://go.microsoft.com/fwlink/?LinkId=164559) und [Artikel 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251).<br /><br />Überprüfen und installieren Sie den Hotfix [Artikel 977073](https://go.microsoft.com/fwlink/?LinkId=186394) (https://go.microsoft.com/fwlink/?LinkId=186394) in der Microsoft Knowledge Base nach Bedarf.|  
|LMv2|Enabled|Disabled|[Artikel 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251)|  

## <a name="BKMK_SysReqs"></a>Betriebssystemanforderungen

Die mindestsystemanforderungen für Windows Server 2012 sind in der folgenden Tabelle aufgeführt. Weitere Informationen zu Systemanforderungen und Informationen zur Installationsvorbereitung finden Sie unter [Installing Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). Für die Installation einer neuen Active Directory-Gesamtstruktur gelten keine weiteren Systemanforderungen. Sie sollten jedoch ausreichend Arbeitsspeicher zum Zwischenspeichern des Inhalts der Active Directory-Datenbank hinzufügen, um die Leistung für Domänencontroller, LDAP-Clientanforderungen und Active Directory-fähige Anwendungen zu verbessern. Wenn Sie einen vorhandenen Domänencontroller aktualisieren oder einen neuen Domänencontroller zu einer vorhandenen Gesamtstruktur hinzufügen, können Sie mithilfe der Informationen im nächsten Abschnitt sicherstellen, dass der Server die Speicherplatzanforderungen erfüllt.  

|||  
|-|-|  
|Prozessor|1,4-GHz-Prozessor mit 64 Bit|  
|RAM|512 MB|  
|Freier Speicherplatz|32 GB|  
|Bildschirmauflösung|800 x 600 oder höher|  
|Sonstiges|DVD-Laufwerk, Tastatur, Internetzugriff|  

### <a name="BKMK_DiskSpaceDCWin8"></a>Speicherplatzanforderungen für Upgrades von Domänencontrollern

Dieser Abschnitt behandelt die speicherplatzanforderungen nur für ein Upgrade von Domänencontrollern von Windows Server 2008 oder Windows Server 2008 R2. Weitere Informationen zu den Speicherplatzanforderungen für Upgrades von Domänencontrollern auf frühere Versionen von Windows Server finden Sie unter [Disk space requirements for upgrading to Windows Server 2008](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008) oder [Disk space requirements for upgrading to Windows Server 2008 R2](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008R2).  
  
Bemessen Sie den Datenträger, auf dem die Active Directory-Datenbank und die Protokolldateien gehostet werden, so, dass genügend Platz für benutzerdefinierte und anwendungsgesteuerte Schemaerweiterungen und für von Anwendungen und Administratoren initiierte Indizes vorhanden ist. Berücksichtigen Sie auch den Platz für die Objekte und Attribute, die dem Verzeichnis im Laufe der Bereitstellungslebensdauer des Domänencontrollers (normalerweise 5 bis 8 Jahre) hinzugefügt werden. Die richtige Bemessung zur Bereitstellungszeit ist meist eine gute Investition gegenüber den höheren Kosten, die für die Erweiterung des Datenträgerspeichers nach der Bereitstellung anfallen. Weitere Informationen finden Sie unter [Capacity Planning for Active Directory Domain Services](https://social.technet.microsoft.com/wiki/contents/articles/14355.capacity-planning-for-active-directory-domain-services.aspx).  
  
Stellen Sie auf Domänencontrollern, für die Sie ein Upgrade ausführen möchten, sicher, dass auf dem zum Hosten der Active Directory-Datenbank (NTDS.DIT) verwendeten Laufwerk mindestens eine Speicherplatzmenge frei ist, die 20 % der Dateigröße von NTDS.DIT entspricht, bevor Sie das Betriebssystemupgrade starten. Wenn auf dem Datenträger kein ausreichender Speicherplatz verfügbar ist, kann das Upgrade fehlschlagen, und der Upgradekompatibilitätsbericht gibt einen Fehler mit dem Hinweis zurück, dass nicht genügend freier Speicherplatz vorhanden ist:  
  
In diesem Fall können Sie eine Offlinedefragmentierung der Active Directory-Datenbank ausführen, um zusätzlichen Speicherplatz zu gewinnen. Führen Sie anschließend das Upgrade erneut aus Weitere Informationen finden Sie unter [Compact the Directory Database File (Offline Defragmentation)](https://technet.microsoft.com/library/cc794920(v=WS.10).aspx).  
  
### <a name="available-skus"></a>Verfügbare SKUs

Insgesamt sind 4 Editionen von Windows Server verfügbar: Foundation, Essentials, Standard und Datacenter.
Von den Editionen Standard und Datacenter wird die AD DS-Rolle unterstützt.  
  
Bei den vorherigen Versionen haben sich die Windows Server-Editionen in Bezug auf die Unterstützung von Serverrollen, die Prozessoranzahl und die Unterstützung großer Arbeitsspeicher unterschieden. Die Standard- und Datacenter-Editionen von Windows Server unterstützen alle Features und zugrunde liegende Hardware variieren jedoch hinsichtlich der Virtualisierungsrechte - sind zwei virtuelle Instanzen zulässig, für die Standard Edition und eine unbegrenzte Anzahl virtuelle Instanzen für Datacenter zulässig sind Edition.  
  
### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows-Client- und Windows Server-Betriebssysteme mit Unterstützung für den Beitritt zu Windows Server-Domänen

Die folgenden Windows-Client- und Windows Server-Betriebssysteme werden für Domänenmitgliedscomputer mit Domänencontrollern unterstützt, auf denen Windows Server 2012 oder neuer ausgeführt wird:  
  
- Clientbetriebssysteme: Windows 8.1, Windows 8, Windows 7, Windows Vista
   - Computer unter Windows 8.1 oder Windows 8 können außerdem Domänen beitreten, deren Domänencontroller unter früheren Windows Server-Versionen laufen, inklusive Windows Server 2003 oder neuer. In diesem Fall kann es jedoch sein, dass einige Features von Windows 8 speziell konfiguriert werden müssen oder nicht verfügbar sind. Weitere Informationen zu diesen Features und Empfehlungen zur Verwaltung von Windows 8-Clients in Domänen mit Vorgängerversionen finden Sie unter [Running Windows 8 member computers in Windows Server 2003 domains](https://social.technet.microsoft.com/wiki/contents/articles/17361.running-windows-8-member-computers-in-windows-server-2003-domains.aspx).  
- Serverbetriebssysteme: Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2, Windows Server 2003  

## <a name="BKMK_UpgradePaths"></a>Unterstützte direkte Aktualisierungspfade

Domänencontroller, auf denen 64-Bit-Versionen von Windows Server 2008 oder Windows Server 2008 R2 ausführen, können auf Windows Server 2012 aktualisiert werden. Für Domänencontroller, auf denen Windows Server 2003 oder 32-Bit-Versionen von Windows Server 2008 ausgeführt werden, kann kein Upgrade durchgeführt werden. Wenn Sie diese ersetzen möchten, installieren Sie in der Domäne Domänencontroller, auf denen eine neuere Version von Windows Server ausgeführt wird, und entfernen Sie dann die Domänencontroller, auf denen Windows Server 2003 ausgeführt wird.  

|Ausgeführte Editionen|Mögliches Upgrade auf Editionen|  
|-------------------------------------|-------------------------------------|  
|Windows Server 2008 Standard mit SP2<br /><br />oder<br /><br />Windows Server 2008 Enterprise mit SP2|Windows Server2012 Standard<br /><br />oder<br /><br />Windows Server2012 Datacenter|  
|Windows Server 2008 Datacenter mit SP2|Windows Server2012 Datacenter|  
|Windows Web Server 2008|Windows Server2012 Standard|  
|Windows Server 2008 R2 Standard mit SP1<br /><br />oder<br /><br />Windows Server 2008 R2 Enterprise mit SP1|Windows Server2012 Standard<br /><br />oder<br /><br />Windows Server2012 Datacenter|  
|Windows Server 2008 R2 Datacenter mit SP1|Windows Server2012 Datacenter|  
|Windows Web Server 2008 R2|Windows Server2012 Standard|  
  
Weitere Informationen zu unterstützten Aktualisierungspfaden finden Sie unter [Evaluation Versions and Upgrade Options for Windows Server 2012](https://go.microsoft.com/fwlink/?LinkId=260917). Beachten Sie, dass Sie einen Domänencontroller, auf dem eine Evaluierungsversion von Windows Server 2012 ausgeführt wird, nicht direkt in eine Verkaufsversion konvertieren können. Installieren Sie stattdessen einen zusätzlichen Domänencontroller auf einem Server mit einer Verkaufsversion, und entfernen Sie AD DS von dem Domänencontroller mit der Evaluierungsversion.  
  
Aufgrund eines bekannten Problems können nicht Sie einen Domänencontroller aktualisieren, der Server Core-Installationsoption von Windows Server 2008 R2, Server Core-Installationen von Windows Server 2012 ausgeführt wird. Das Upgrade bleibt spät im Upgradeprozess mit einem schwarzen Bildschirm hängen. Beim Neustarten dieser Domänencontroller wird in der Datei %%amp;quot;boot.ini%%amp;quot; eine Option verfügbar gemacht, mit der ein Rollback auf die vorherige Betriebssystemversion durchgeführt wird. Bei einem weiteren Neustart wird das automatische Rollback zur vorherigen Betriebssystemversion ausgelöst. Bis eine Lösung verfügbar ist, wird empfohlen, die Sie installieren einen neuen Domänencontroller mit einer Server Core-Installation von Windows Server 2012 anstatt ein direktes Upgrade eines vorhandenen Domänencontrollers, das Server Core-Installationen von Windows Server ausgeführt wird. 2008 R2. Weitere Informationen finden Sie im KB-Artikel [2734222](https://support.microsoft.com/kb/2734222).  

## <a name="BKMK_FunctionalLevels"></a>Funktionale Funktionen und Anforderungen auf

Windows Server 2012 ist eine Windows Server 2003-Gesamtstrukturfunktionsebene erforderlich. D. h. bevor Sie einen Domänencontroller, der Windows Server 2012 zu einer vorhandenen Active Directory-Gesamtstruktur ausgeführt wird hinzufügen können, muss die Gesamtstrukturfunktionsebene auf WindowsServer 2003 oder höher sein. Dies bedeutet, dass Domänencontroller, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 ausgeführt wird, in derselben Gesamtstruktur betrieben werden können. Domänencontroller, auf denen Windows 2000 Server ausgeführt wird, werden jedoch nicht unterstützt und blockieren die Installation eines Domänencontrollers, auf dem Windows Server 2012 ausgeführt wird. Wenn die Gesamtstruktur Domänencontroller mit Windows Server 2003 oder höher enthält, die Gesamtstrukturfunktionsebene jedoch noch auf Windows 2000 basiert, wird die Installation ebenfalls blockiert.  
  
Windows 2000-Domänencontroller müssen entfernt werden, bevor der Gesamtstruktur Windows Server 2012-Domänencontroller hinzugefügt werden. Erwägen Sie in diesem Fall den folgenden Workflow:  

1. Installieren Sie Domänencontroller, auf denen Windows Server 2003 oder höher ausgeführt wird. Diese Domänencontroller können unter einer Evaluierungsversion von Windows Server bereitgestellt werden. Dieser Schritt erfordert außerdem die Ausführung von [adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx) als Voraussetzung für die Betriebssystemversion.  
2. Entfernen Sie die Windows 2000-Domänencontroller. Führen Sie eine ordnungsgemäße Herabstufung oder erzwungene Entfernung der Windows Server 2000-Domänencontroller aus der Domäne durch, und verwenden Sie %%amp;quot;Active Directory-Benutzer und -Computer%%amp;quot;, um die Domänencontrollerkonten für alle entfernten Domänencontroller zu entfernen.  
3. Stufen Sie die Gesamtstrukturfunktionsebene auf Windows Server 2003 oder höher herauf.  
4. Installieren Sie Domänencontroller, auf denen Windows Server 2012 ausgeführt wird.  
5. Entfernen Sie Domänencontroller, auf denen ältere Versionen von Windows Server ausgeführt werden.  

Die neue Domänenfunktionsebene von Windows Server 2012 ermöglicht ein neues Feature: die **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung** KDC-verwaltungsvorlagenrichtlinie sind zwei Einstellungen vorhanden (**immer Ansprüche bereitstellen** und **; Fehler bei authentifizierungsanforderungen ohne Armor**), die Domänenfunktionsebene auf Windows Server 2012 erfordern.  
  
Die Gesamtstrukturfunktionsebene Windows Server 2012 bietet keine neuen Features, aber es wird sichergestellt, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf die Domänenfunktionsebene von Windows Server 2012 ausgeführt wird. Die Domänenfunktionsebene Windows Server 2012 bietet keine weiteren neuen Features außer KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung. Sie stellt jedoch sicher, dass alle Domänencontroller in der Domäne auf Windows Server 2012 ausgeführt wird. Weitere Informationen zu weiteren Features, die auf verschiedenen Funktionsebenen verfügbar sind, finden Sie unter [Understanding Active Directory Domain Services (AD DS) Functional Levels](../active-directory-functional-levels.md).  
  
Nachdem Sie die Gesamtstrukturfunktionsebene auf einen bestimmten Wert festgelegt, nicht zurücksetzen oder Herabstufen der Funktionsebene der Gesamtstruktur, mit den folgenden Ausnahmen: Nachdem Sie die Gesamtstrukturfunktionsebene auf Windows Server 2012 heraufgestuft wurde, kann es zu Windows Server 2008 R2 gesenkt. Wenn Active Directory-Papierkorb nicht aktiviert wurde, können Sie auch die Gesamtstrukturfunktionsebene Windows Server 2012 auf Windows Server 2008 R2 oder Windows Server 2008 oder Windows Server 2008 R2 auf Windows Server 2008 herabsetzen. Wenn die Gesamtstrukturfunktionsebene auf Windows Server 2008 R2 festgelegt ist, kann nicht sie beispielsweise auf Windows Server 2003 zurückgesetzt werden.  
  
Nachdem Sie die Domänenfunktionsebene auf einen bestimmten Wert festgelegt, nicht zurücksetzen oder Herabstufen der Domäne mit den folgenden Ausnahmen: Wenn Sie die Domänenfunktionsebene auf Windows Server 2008 R2 oder Windows Server 2012 heraufstufen und die Gesamtstruktur-Funktion NAL-Ebene ist Windows Server 2008 oder niedriger ist, Sie haben die Möglichkeit, parallele, sichern die Domänenfunktionsebene auf WindowsServer 2008, oder Windows Server 2008 R2. Sie können die Domänenfunktionsebene nur von Windows Server 2012 auf Windows Server 2008 R2 oder Windows Server 2008 oder Windows Server 2008 R2 auf Windows Server 2008 herabstufen. Wenn die Domänenfunktionsebene auf Windows Server 2008 R2 festgelegt ist, kann er, z. B. auf Windows Server 2003 zurückgesetzt werden.  
  
Weitere Informationen zu Features, die auf niedrigeren Funktionsebenen verfügbar sind, finden Sie unter [Understanding Active Directory Domain Services (AD DS) Functional Levels](../active-directory-functional-levels.md).  
  
Neben den Funktionsebenen bietet ein Domänencontroller, der Windows Server 2012 ausgeführt wird. Weitere Funktionen, die nicht auf einem Domänencontroller verfügbar sind, die eine frühere Version von Windows Server ausgeführt wird. Beispielsweise kann ein Domänencontroller mit Windows Server 2012 für das Klonen virtueller Domänencontroller, verwendet werden, während ein Domänencontroller mit einer früheren Version von Windows Server nicht möglich. Klonen virtueller Domänencontroller und die Sicherheit virtueller Domänencontroller unter Windows Server 2012 besitzen jedoch keine Anforderungen bezüglich der Funktionsebene.  

> [!NOTE]  
> Microsoft Exchange Server 2013 erfordert die Gesamtstrukturfunktionsebene Windows Server 2003 oder höher.  

## <a name="BKMK_ServerRoles"></a>AD DS-Interoperabilität mit anderen Serverrollen und Windows-Betriebssystemen

AD DS wird auf den folgenden Windows-Betriebssystemen nicht unterstützt:  
  
- Windows MultiPoint Server  
- Windows Server 2012 Essentials  
  
AD DS kann nicht auf einem Server installiert werden, auf dem auch die folgenden Serverrollen oder Rollendienste ausgeführt werden:  
  
- Hyper-V Server  
- Remotedesktop-Verbindungsbroker  
  
## <a name="BKMK_OpsMasters"></a>Betriebsmasterrollen

Einige neue Features in Windows Server 2012 wirken sich auf Betriebsmasterrollen aus:  

- Der PDC-Emulator muss Windows Server 2012 zur Unterstützung von das Klonen virtueller Domänencontroller ausgeführt werden. Zum Klonen von Domänencontrollern gelten zusätzliche Voraussetzungen. Weitere Informationen finden Sie unter [Active Directory Domain Services (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx).  
- Wenn der PDC-Emulator mit Windows Server 2012 ausgeführt wird, werden neue Sicherheitsprinzipale erstellt.  
- Der RID-Master verfügt über eine neue Funktionalität für die RID-Ausstellung und -Überwachung. Die Verbesserungen umfassen eine optimierte Ereignisprotokollierung, besser geeignete Grenzen und die Möglichkeit, im Notfall die RID-Gesamtpoolzuweisung um ein Bit zu erhöhen. Weitere Informationen finden Sie unter [Managing RID Issuance](../../ad-ds/manage/Managing-RID-Issuance.md).  

> [!NOTE]  
> Obwohl sie sich nicht um Betriebsmasterrollen handelt, ist eine weitere Änderung in AD DS-Installation an, dass DNS-Serverrolle und der globale Katalog standardmäßig auf allen Domänencontrollern installiert werden, auf denen Windows Server 2012 ausgeführt.  

## <a name="BKMK_Virtual"></a>Virtualisieren von Domänencontrollern

Verbesserungen in AD DS ab Windows Server 2012 aktivieren, sicherere Virtualisierung von Domänencontrollern und die Möglichkeit, Klonen von Domänencontrollern. Das Klonen von Domänencontrollern ermöglicht wiederum eine schnelle Bereitstellung zusätzlicher Domänencontroller in einer neuen Domäne, und es bietet weitere Vorteile. Weitere Informationen finden Sie unter [Einführung in die Active Directory Domain Services &#40;AD DS&#41; Virtualisierung &#40;ebene100&#41;](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  

## <a name="BKMK_Admin"></a>Verwaltung von Windows Server 2012-Server

Verwenden der [Remoteserver-Verwaltungstools für Windows 8](https://www.microsoft.com/download/details.aspx?id=28972) zum Verwalten von Domänencontrollern und anderen Servern, auf denen Windows Server 2012 ausgeführt. Sie können die Windows Server 2012 Remoteserver-Verwaltungstools auf einem Computer ausführen, die Windows 8 ausgeführt wird.  

## <a name="BKMK_AppCompat"></a>Anwendungskompatibilität

In der folgenden Tabelle sind die allgemeinen Microsoft-Anwendungen mit Active Directory-Integration zusammengefasst. Es ist angegeben, unter welchen Versionen von Windows Server die Anwendungen installiert werden können und ob sich die Einführung von Windows Server 2012-Domänencontrollern auf die Anwendungskompatibilität auswirkt.  

|Produkt|Hinweise|  
|-----------|---------|  
|[Microsoft Configuration Manager 2007](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Configuration Manager 2007 mit SP2 (enthält Configuration Manager 2007 R2 und Configuration Manager 2007 R3):<br /><br />-   Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />-Windows Server 2012 Datacenter **beachten:** Auch wenn diese Produkte als Clients vollständig unterstützt werden, ist nicht geplant, die Unterstützung für die Bereitstellung dieser Produkte als Betriebssysteme mithilfe der Configuration Manager 2007-Funktion zum Bereitstellen von Betriebssystemen hinzuzufügen. Es werden auch keine Standortserver oder Standortsysteme für SKUs von Windows Server 2012 unterstützt.|  
|[Microsoft SharePoint 2007](https://support.microsoft.com/kb/2728964)|Microsoft Office SharePoint Server 2007 wird für die Installation unter Windows Server 2012 nicht unterstützt.|  
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|SharePoint 2010 Service Pack 2 ist erforderlich, zum Installieren und betreiben <br />SharePoint 2010 auf Windows Server 2012-Servern<br /><br />SharePoint 2010 Foundation Service Pack 2 ist für die Installation und den Betrieb vonSharePoint 2010 Foundation auf Windows Server 2012-Servern erforderlich.<br /><br />Beim Installationsvorgang von SharePoint Server 2010 (ohne Service Packs) tritt unter Windows Server 2012 ein Fehler auf.<br /><br />Das erforderliche SharePoint Server 2010-Installationsprogramm (PrerequisiteInstaller.exe) tritt der Fehler "dieses Programm hat Kompatibilitätsprobleme.%%amp;quot". Klicken Sie auf "Das Programm ohne Hilfestellung ausführen" wird der Fehler "wird überprüft, ob SharePoint installiert werden kann &#124; SharePoint Server 2010 (ohne Servicepacks) kann nicht unter Windows installiert werden Windows Server 2012."|  
|[Microsoft SharePoint 2013](https://technet.microsoft.com/library/cc262485(v=office.15).aspx)|Mindestanforderungen für einen Datenbankserver in einer Farm:<br /><br />64-Bit-Edition von Windows Server 2008 R2 Service Pack 1 (SP1) Standard, Enterprise oder Datacenter oder 64-Bit-Edition von Windows Server 2012 Standard oder Datacenter<br /><br />Mindestanforderungen für einen Einzelserver mit integrierter Datenbank:<br /><br />64-Bit-Edition von Windows Server 2008 R2 Service Pack 1 (SP1) Standard, Enterprise oder Datacenter oder 64-Bit-Edition von Windows Server 2012 Standard oder Datacenter<br /><br />Mindestanforderungen für Front-End-Webserver und Anwendungsserver in einer Farm:<br /><br />64-Bit-Edition von Windows Server 2008 R2 Service Pack 1 (SP1) Standard, Enterprise oder Datacenter oder 64-Bit-Edition von Windows Server 2012 Standard oder Datacenter|  
|[Microsoft System Center Configuration Manager 2012](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Configuration Manager Service Pack 1:<br /><br />Microsoft fügt seiner Clientunterstützungsmatrix mit der Veröffentlichung von Service Pack 1 die folgenden Betriebssysteme hinzu:<br /><br />-   Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter<br /><br />Alle Standortserverrollen, einschließlich Standortserver, SMS-Anbieter und Verwaltungspunkte, können auf Servern mit den folgenden Betriebssystemeditionen bereitgestellt werden:<br /><br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter|  
|[Microsoft Lync Server 2013](https://technet.microsoft.com/library/gg412883.aspx)|Lync Server 2013 erfordert Windows Server 2008 R2 oder Windows Server 2012. Die Anwendung kann nicht unter einer Server Core-Installation ausgeführt werden. Die Ausführung auf [virutellen Servern](https://technet.microsoft.com/library/gg399035.aspx). ist möglich.|  
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|Lync Server 2010 kann auf einer neuen (nicht per Upgrade erstellten) Installation von Windows Server 2012 installiert werden, wenn die [October 2012 cumulative updates for Lync Server](https://support.microsoft.com/?kbid=2493736) installiert wurden. Ein Upgrade des Betriebssystems auf Windows Server 2012 wird für eine bestehende Installation von Lync Server 2010 nicht unterstützt. Außerdem wird unter Windows Server 2012 auch nicht der Microsoft Lync Server 2010-Gruppenchatserver unterstützt.|  
|[System Center 2012 Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Mit System Center 2012 Endpoint Protection Service Pack 1 wird die Clientunterstützungsmatrix um die folgenden Betriebssysteme erweitert:<br /><br />-   Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter|  
|[System Center 2012 Forefront Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Mit FEP 2010 mit Updaterollup 1 wird die Clientunterstützungsmatrix um die folgenden Betriebssysteme erweitert:<br /><br />-   Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter|  
|Forefront Threat Management Gateway (TMG)|Für TMG wird nur die Ausführung unter Windows Server 2008 und Windows Server 2008 R2 unterstützt. Weitere Informationen finden Sie unter [System requirements for Forefront TMG](https://technet.microsoft.com/library/dd896981.aspx).|  
|Windows Server Update Services|Diese Version von WSUS unterstützt bereits Windows 8-basierte Computer oder Windows Server 2012-basierte Computer als Clients.|  
|Windows Server Update Services 3.0|Update-KB-Artikel [2734608](https://support.microsoft.com/kb/2734608) können Server, auf denen Windows Server Update Services (WSUS) 3.0 SP2 Updates für Computer bereitstellen, auf denen Windows 8 oder Windows Server 2012 ausgeführt werden: **Hinweis:** Kunden mit eigenständigen WSUS 3.0 SP2-Umgebungen oder System Center Configuration Manager 2007 Service Pack 2-Umgebungen mit WSUS 3.0 SP2 benötigen [2734608](https://support.microsoft.com/kb/2734608) ordnungsgemäße Verwaltung von Windows 8-basierte Computer oder Windows Server 2012 - -basierte Computer als Clients.|  
|[Exchange 2013](https://technet.microsoft.com/library/bb691354.aspx)|Windows Server 2012 Standard und Datacenter werden für die folgenden Rollen unterstützt: Schemamaster, globaler Katalogserver, Domänencontroller, Postfach- und Clientzugriffs-Serverrolle.<br /><br />Gesamtstrukturfunktionsebene: Windows Server 2003 oder höher<br /><br />Quelle: Exchange 2013-Systemanforderungen|  
|Exchange 2010|[Quelle: Exchange 2010 Service Pack 3](https://blogs.technet.com/b/exchange/archive/2012/09/25/announcing-exchange-2010-service-pack-3.aspx)<br /><br />Exchange 2010 mit Service Pack 3 kann auf Windows Server 2012-Mitgliedsservern installiert werden.<br /><br />Unter[Exchange 2010 System Requirements](https://technet.microsoft.com/library/aa996719(EXCHG.141).aspx) ist der aktuelle unterstützte Schemamaster, globale Katalog und Domänencontroller als Windows Server 2008 R2 angegeben.<br /><br />Gesamtstrukturfunktionsebene: Windows Server 2003 oder höher|  
|SQL Server 2012|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />SQL Server 2012 RTM wird unter Windows Server 2012 unterstützt.|  
|SQL Server 2008 R2|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Erfordert SQL Server 2008 R2 mit Service Pack 1 oder höher für die Installation unter Windows Server 2012.|  
|SQL Server 2008|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Erfordert SQL Server 2008 mit Service Pack 3 oder höher für die Installation unter Windows Server 2012.|  
|SQL Server 2005|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Wird für die Installation unter Windows Server 2012 nicht unterstützt.|  

## <a name="BKMK_KnownIssues"></a>Bekannte Probleme

In der folgenden Tabelle sind die mit der AD DS-Installation verbundenen bekannten Probleme aufgeführt.  

||||  
|-|-|-|  
|Titel und Nummer des KB-Artikels|Betroffener Technologiebereich|Problem/Beschreibung|  
|[2830145](https://support.microsoft.com/kb/2830145): SID S-1-18-1 und SID S-1-18-2 können unter Windows 7 oder Windows Server 2008 R2-basierten Computern in einer Domänenumgebung nicht zugeordnet werden|AD DS-Verwaltungs-API/Anwendungskompatibilität|Anwendungen, die die in Windows Server 2012 neu eingeführten neuen SIDs S-1-18-1 und S-1-18-2 verwenden, funktionieren unter Umständen nicht, da diese SIDs auf Windows 7 oder Windows Server 2008 R2-basierten Computern nicht aufgelöst werden können. Um dieses Problem zu lösen, installieren Sie den Hotfix auf den Windows 7 oder Windows Server 2008 R2-basierten Computern in der Domäne.|  
|[2737129](https://support.microsoft.com/kb/2737129): Gruppenrichtlinienvorbereitung wird nicht ausgeführt, wenn Sie eine vorhandene Domäne automatisch für Windows Server 2012 vorbereiten|AD DS-Installation|Adprep/domainprep/gpprep wird nicht automatisch als Teil der Installation des ersten Domänencontrollers ausgeführt, auf dem Windows Server 2012 in einer Domäne ausgeführt wird. Falls der Schritt in der Domäne noch nicht ausgeführt wurde, muss dies manuell erfolgen.|  
|[2737416](https://support.microsoft.com/kb/2737416): Wiederholung von Warnungen bei Bereitstellung Windows PowerShell-basierter Domänencontroller|AD DS-Installation|Warnungen können während der Überprüfung der Voraussetzungen und dann noch einmal während der Installation angezeigt werden.|  
|[2737424](https://support.microsoft.com/kb/2737424): Fehler "Das Format des angegebenen Domänennamens ist unzulässig" beim Versuch, Active Directory-Domänendienste von einem Domänencontroller zu entfernen|AD DS-Installation|Dieser Fehler wird angezeigt, wenn Sie den letzten Domänencontroller in einer Domäne entfernen, in der bereits vorab erstellte RODC-Konten vorhanden sind. Dies betrifft Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.|  
|[2737463](https://support.microsoft.com/kb/2737463): Domänencontroller startet nicht, c00002e2-Fehler tritt auf oder "Option auswählen" wird angezeigt|AD DS-Installation|Ein Domänencontroller startet nicht, weil ein Administrator %%amp;quot;Dism.exe%%amp;quot;, %%amp;quot;Pkgmgr.exe%%amp;quot; oder %%amp;quot;Ocsetup.exe%%amp;quot; zum Entfernen der DirectoryServices-DomainController-Rolle verwendet hat.|  
|[2737516](https://support.microsoft.com/kb/2737516): Beschränkungen der IFM-Überprüfung in Windows Server 2012-Server-Manager|AD DS-Installation|Wie im KB-Artikel erläutert, können für die IFM-Überprüfung Beschränkungen gelten.|  
|[2737535](https://support.microsoft.com/kb/2737535): Install-AddsDomainController-Cmdlet gibt Parametersatzfehler für RODC zurück|AD DS-Installation|Möglicherweise erhalten Sie einen Fehler beim Versuch, einen Server einem RODC-Konto zuzuordnen, wenn Sie Argumente angeben, mit denen das vorab erstellte RODC-Konto bereits aufgefüllt wurde.|  
|[2737560](https://support.microsoft.com/kb/2737560): Fehler "Für die Domäne konnte keine Exchange-Schemakonfliktüberprüfung ausgeführt werden" und Fehler bei Überprüfung der Voraussetzungen|AD DS-Installation|Bei der Überprüfung der Voraussetzungen tritt ein Fehler auf, wenn Sie den ersten Windows Server 2012-Domänencontroller in einer vorhandenen Domäne konfigurieren, weil für die Domänencontroller SeServiceLogonRight für den Netzwerkdienst fehlt oder weil WMI- oder DCOM-Protokolle blockiert sind.|  
|[2737797](https://support.microsoft.com/kb/2737797): AddsDeployment-Modul mit -Whatif-Argument zeigt falsche DNS-Ergebnisse an|AD DS-Installation|Der – WhatIf-Parameter zeigt-DNS-Server nicht installiert werden, aber sie werden.|  
|[2737807](https://support.microsoft.com/kb/2737807): Schaltfläche "Weiter" ist auf der Seite mit den Domänencontrolleroptionen nicht verfügbar|AD DS-Installation|Die Schaltfläche %%amp;quot;Weiter%%amp;quot; ist auf der Seite %%amp;quot;Domänencontrolleroptionen%%amp;quot; deaktiviert, weil die IP-Adresse des Zieldomänencontrollers keinem vorhandenen Subnetz oder Standort zugeordnet ist oder weil das DSRM-Kennwort nicht richtig eingegeben und bestätigt wurde.|  
|[2737935](https://support.microsoft.com/kb/2737935): Active Directory-Installation stoppt bei "NTDS-Einstellungsobjekt wird erstellt"|AD DS-Installation|Die Installation hängt, weil das lokale Administratorkennwort mit dem Administratorkennwort der Domäne übereinstimmt oder weil Netzwerkprobleme den Abschluss der kritischen Replikation verhindern.|  
|[2738060](https://support.microsoft.com/kb/2738060): Fehlermeldung "Zugriff verweigert" bei der Remoteerstellung einer untergeordneten Domäne mithilfe von Install-AddsDomain|AD DS-Installation|Sie erhalten den Fehler beim Ausführen von Install-ADDSDomain mit dem Invoke-Command-Cmdlet, wenn DNSDelegationCredential über ein falsches Kennwort verfügt.|  
|[2738697](https://support.microsoft.com/kb/2738697): Domänencontroller-Konfigurationsfehler "Server ist nicht funktionstüchtig" beim Konfigurieren eines Servers mit dem Server-Manager|AD DS-Installation|Sie erhalten diesen Fehler beim Versuch, AD DS auf einem Arbeitsgruppencomputer zu installieren, weil die NTLM-Authentifizierung deaktiviert ist.|  
|[2738746](https://support.microsoft.com/kb/2738746): Sie erhalten nach dem Anmelden an einem lokalen Domänenadministratorkonto Fehler vom Typ "Zugriff verweigert"|AD DS-Installation|Wenn Sie sich nicht mit dem integrierten Administratorkonto anmelden, sondern mit einem lokalen Administratorkonto, und dann eine neue Domäne erstellen, wird das Konto nicht der Gruppe %%amp;quot;Domänen-Admins%%amp;quot; hinzugefügt.|  
|[2743345](https://support.microsoft.com/kb/2743345): adprep/gpprep-Fehler "Die angegebene Datei wurde nicht gefunden" oder Absturz des Tools|AD DS-Installation|Sie erhalten diesen Fehler beim Ausführen von adprep/gpprep, weil der Infrastrukturmaster einen zusammenhanglosen Namespace implementiert.|  
|[2743367](https://support.microsoft.com/kb/2743367): Adprep-Fehler "Keine gültige Win32-Anwendung" unter Windows Server 2003, 64-Bit-Version|AD DS-Installation|Sie erhalten diesen Fehler, weil Windows Server 2012 Adprep unter Windows Server 2003 nicht ausgeführt werden kann.|  
|[2753560](https://support.microsoft.com/kb/2753560): ADMT 3.2- und PES 3.1-Installationsfehler unter Windows Server 2012|ADMT|ADMT 3.2 kann entwurfsbedingt unter Windows Server 2012 nicht installiert werden.|  
|[2750857](https://support.microsoft.com/kb/2750857): Diagnoseberichte der DFS-Replikation können in Internet Explorer 10 nicht richtig angezeigt werden|DFS-Replikation|Der Diagnosebericht der DFS-Replikation wird aufgrund von Änderungen an Internet Explorer 10 nicht richtig angezeigt.|  
|[2741537](https://support.microsoft.com/kb/2741537): Remoteaktualisierungen der Gruppenrichtlinie sind für Benutzer sichtbar|Gruppenrichtlinie|Dies liegt an geplanten Aufgaben, die jeweils im Kontext der einzelnen angemeldeten Benutzer ausgeführt werden. Die Beschaffenheit des Windows-Taskplaners erfordert in diesem Szenario eine interaktive Eingabeaufforderung.|  
|[2741591](https://support.microsoft.com/kb/2741591): ADM-Dateien sind unter SYSVOL in der GPMC-Infrastrukturstatusoption nicht vorhanden|Gruppenrichtlinie|Für die Gruppenrichtlinienreplikation kann "Replikation wird ausgeführt" melden, weil der GPMC-Infrastrukturstatus keine angepasste Filterregeln befolgt.|  
|[2737880](https://support.microsoft.com/kb/2737880): Fehler "Der Dienst kann nicht gestartet werden" bei AD DS-Konfiguration|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler beim Installieren oder Entfernen von AD DS oder beim Klonen, weil der Dienst %%amp;quot;DS-Rollenserver%%amp;quot; deaktiviert ist.|  
|[2742836](https://support.microsoft.com/kb/2742836): Zwei DHCP-Leases werden beim Verwenden der VDC-Klonfunktion für jeden Domänencontroller erstellt|Klonen virtueller Domänencontroller|Dies ist der Fall, weil der geklonte Domänencontroller vor dem Klonen und nach Abschluss des Klonens einen Lease erhalten hat.|  
|[2742844](https://support.microsoft.com/kb/2742844): Fehler beim Klonen des Domänencontrollers, und der Server wird unter Windows Server 2012 im Verzeichnisdienst-Wiederherstellungsmodus (DSRM) neu gestartet|Klonen virtueller Domänencontroller|Der geklonte Domänencontroller wird im Verzeichnisdienst-Wiederherstellungsmodus (DSRM) gestartet, weil das Klonen aus den im KB-Artikel aufgeführten Gründen nicht erfolgreich war.|  
|[2742874](https://support.microsoft.com/kb/2742874): Beim Klonen des Domänencontrollers werden nicht alle Dienstprinzipalnamen neu erstellt|Klonen virtueller Domänencontroller|Einige dreiteilige Dienstprinzipalnamen werden auf dem geklonten Domänencontroller aufgrund einer Einschränkung des Umbenennungsprozesses der Domäne nicht neu erstellt.|  
|[2742908](https://support.microsoft.com/kb/2742908): Fehler "Keine Anmeldeserver verfügbar" nach dem Klonen des Domänencontrollers|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler beim Versuch, sich nach dem Klonen eines virtualisierten Domänencontrollers anzumelden, weil das Klonen nicht erfolgreich war und der Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus gestartet wird. Melden Sie sich als %%amp;quot;.\administrator%%amp;quot; an, um den Fehler in Bezug auf das Klonen zu beheben.|  
|[2742916](https://support.microsoft.com/kb/2742916): Beim Klonen des Domänencontrollers tritt in "dcpromo.log" der Fehler 8610 auf|Klonen virtueller Domänencontroller|Beim Klonen tritt ein Fehler auf, weil der PDC-Emulator keine eingehende Replikation der Domänenpartition durchgeführt hat. Dies liegt wahrscheinlich daran, dass die Rolle übertragen wurde.|  
|[2742927](https://support.microsoft.com/kb/2742927): New-AdDcCloneConfig-Fehler "Der Indexwert liegt außerhalb des zulässigen Bereichs"|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler nach dem Ausführen des Cmdlets New-ADDCCloneConfigFile beim Klonen virtueller Domänencontroller. Dies liegt entweder daran, dass das Cmdlet nicht über eine Eingabeaufforderung mit erhöhten Rechten ausgeführt wurde, oder daran, dass die Gruppe %%amp;quot;Administratoren%%amp;quot; nicht im Zugriffstoken enthalten ist.|  
|[2742959](https://support.microsoft.com/kb/2742959): Beim Klonen des Domänencontrollers tritt der Fehler 8437 „Es wurde ein ungültiger Parameter für diesen Replikationsvorgang angegeben“ auf|Klonen virtueller Domänencontroller|Beim Klonen tritt ein Fehler auf, weil ein ungültiger Klonname oder ein doppelter NetBIOS-Name angegeben wurde.|  
|[2742970](https://support.microsoft.com/kb/2742970): Fehler beim Klonen des Domänencontrollers ohne Verzeichnisdienst-Wiederherstellungsmodus, doppelte Quelle und Kloncomputer|Klonen virtueller Domänencontroller|Der geklonte virtuelle Domänencontroller wird im Verzeichnisdienst-Wiederherstellungsmodus (Directory Services Repair Mode, DSRM) gestartet, indem ein doppelter Name als Quelldomänencontroller verwendet wird. Der Grund ist, dass die Datei %%amp;quot;DCCloneConfig.xml%%amp;quot; nicht am richtigen Speicherort erstellt wurde oder dass der Quelldomänencontroller vor dem Klonen neu gestartet wurde.|  
|[2743278](https://support.microsoft.com/kb/2743278): Fehler 0x80041005 beim Klonen des Domänencontrollers|Klonen virtueller Domänencontroller|Der geklonte Domänencontroller wird im Verzeichnisdienst-Wiederherstellungsmodus gestartet, weil nur ein WINS-Server angegeben wurde. Beim Angeben eines WINS-Servers müssen immer der bevorzugte und der alternative WINS-Server angegeben werden.|  
|[2745013](https://support.microsoft.com/kb/2745013): Fehlermeldung "Der Server ist nicht funktionstüchtig" beim Ausführen von New-AdDcCloneConfigFile in Windows Server 2012|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler nach dem Ausführen des Cmdlets New-ADDCCloneConfigFile, weil der Server keinen globalen Katalogserver kontaktieren kann.|  
|[2747974](https://support.microsoft.com/kb/2747974): Klonereignis 2224 für Domänencontroller liefert fehlerhaften Hinweis|Klonen virtueller Domänencontroller|Unter der Ereignis-ID 2224 wird fälschlicherweise angegeben, dass verwaltete Dienstkonten vor dem Klonen entfernt werden müssen. Eigenständige verwaltete Dienstkonten müssen entfernt werden, aber gruppenverwaltete Dienstkonten bewirken keine Blockierung des Klonens.|  
|[2748266](https://support.microsoft.com/kb/2748266): Entsperren eines Laufwerks mit BitLocker-Verschlüsselung nach dem Upgrade auf Windows 8 nicht möglich|BitLocker|Sie erhalten einen Fehler "Anwendung nicht gefunden", wenn Sie versuchen, ein Laufwerk auf einem Computer zu entsperren, die von Windows 7 aktualisiert wurde.|  

## <a name="see-also"></a>Siehe auch

[Evaluierungsressourcen für Windows Server 2012](https://technet.microsoft.com/evalcenter/hh708766.aspx)  
[Windows Server 2012-Evaluierungshandbuch](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf)  
[Installieren und Bereitstellen von WindowsServer 2012](https://technet.microsoft.com/library/hh831620.aspx)  
