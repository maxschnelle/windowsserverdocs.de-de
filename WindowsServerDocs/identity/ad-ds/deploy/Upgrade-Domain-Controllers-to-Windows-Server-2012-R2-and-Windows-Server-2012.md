---
ms.assetid: e4c31187-f15f-410b-bb79-8d63e2f2b421
title: "Aktualisieren von Domänencontrollern auf Windows Server2012 R2 und Windows Server 2012"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e317c5a939d417bac844c4080223d7b5e0eec149
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="upgrade-domain-controllers-to-windows-server-2012-r2-and-windows-server-2012"></a>Aktualisieren von Domänencontrollern auf Windows Server2012 R2 und Windows Server 2012

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Dieses Thema enthält Hintergrundinformationen zu Active Directory-Domänendienste in Windows Server 2012 R2 und Windows Server 2012, und es wird der Prozess zum Upgraden von Domänencontrollern von Windows Server 2008 oder Windows Server 2008 R2.  
  
-   [Schritte zum Upgrade von Domain controller](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_UpgradeWorkflow)  
  
-   [Was ist neu in Windows Server 2012?](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_WhatsNewEight)  
  
-   [Was ist neu in AD DS in Windows Server 2012 R2?](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_NewWS2012R2)  
  
-   [Was ist neu in AD DS in Windows Server 2012?](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_WhatsNewAD)  
  
-   [Ändert sich die Installation von AD DS Server-Rolle](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_InstallationChanges)  
  
-   [Veraltete Features und verhaltensänderungen in Bezug auf AD DS in Windows Server 2012](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures)  
  
-   [Betriebssystemanforderungen](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_SysReqs)  
  
-   [Unterstützte direkte Aktualisierungspfade](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_UpgradePaths)  
  
-   [Funktionale-Level-Funktionen und Anforderungen](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_FunctionalLevels)  
  
-   [AD DS-Interoperabilität mit anderen Serverrollen und Windows-Betriebssysteme](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_ServerRoles)  
  
-   [Betriebsmasterrollen](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_OpsMasters)  
  
-   [Virtualisieren von Domänencontrollern, auf denen Windows Server 2012 ausgeführt.](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_Virtual)  
  
-   [Verwaltung von Windows Server 2012-Servern](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_Admin)  
  
-   [Die Anwendungskompatibilität](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat)  
  
-   [Bekannte Probleme](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_KnownIssues)  
  
## <a name="BKMK_UpgradeWorkflow"></a>Schritte zum Upgrade von Domain controller  
Die empfohlene Methode zur Aktualisierung einer Domäne ist Heraufstufen von Domänencontrollern, die neuere Versionen von Windows Server ausgeführt und ältere Domänencontroller nach Bedarf herabzustufen. Diese Methode wird empfohlen, ein Upgrade des Betriebssystems von einem vorhandenen Domänencontroller. Diese Liste umfasst allgemeine Schritte zu befolgen, bevor Sie einen Domänencontroller heraufstufen, der eine neuere Version von Windows Server ausgeführt wird:  
  
1.  Überprüfen Sie, ob der Zielserver erfüllt [Systemanforderungen](https://technet.microsoft.com/library/dn303418.aspx).  
  
2.  Vergewissern Sie sich [Anwendungskompatibilität](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_AppCompat).  
  
3.  Überprüfen Sie die Sicherheitseinstellungen. Weitere Informationen finden Sie unter [veraltete Features und verhaltensänderungen in Bezug auf AD DS in Windows Server 2012](../../ad-ds/deploy/Upgrade-Domain-Controllers-to-Windows-Server-2012-R2-and-Windows-Server-2012.md#BKMK_DeprecatedFeatures) und [sichere Standardeinstellungen in Windows Server 2008 und Windows Server 2008 R2](https://technet.microsoft.com/library/upgrade-domain-controllers-to-windows-server-2008-r2(WS.10).aspx#BKMK_SecureDefault).  
  
4.  Überprüfen Sie die Verbindung mit dem Zielserver auf dem Computer, um die Installation ausgeführt werden soll.  
  
5.  Überprüfen Sie die Verfügbarkeit der erforderlichen Betriebsmasterrollen verfügbar:  
  
    -   Zum Installieren des ersten Domänencontrollers, der Windows Server 2012 in einer vorhandenen Domäne und Gesamtstruktur ausgeführt wird, benötigt der Computer, auf dem die Installation ausgeführt, Konnektivität mit dem Schemamaster, um Adprep/forestprep ausführen zu können und dem Infrastrukturmaster, um Adprep/domainprep ausführen zu können.  
  
    -   Zum Installieren des ersten Domänencontrollers in einer Domäne, in denen das Gesamtstrukturschema bereits erweitert ist, benötigen Sie nur eine Verbindung mit dem Infrastrukturmaster.  
  
    -   Zum Installieren oder Entfernen von Domänen in einer vorhandenen Gesamtstruktur, benötigen Sie eine Verbindung mit dem Domänennamenmaster.  
  
    -   Jede Domänencontrollerinstallation ist auch Verbindungen mit dem RID-Master erforderlich.  
  
    -   Wenn Sie den ersten schreibgeschützten Domänencontroller in einer vorhandenen Gesamtstruktur installieren, benötigen Sie eine Verbindung mit dem Infrastrukturmaster für jede Anwendungsverzeichnispartition, auch bekannt als nicht-Domänennamenskontext oder NDNC.  
  
6.  Achten Sie darauf, dass Sie die erforderlichen Anmeldeinformationen zum Ausführen der AD DS-Installation angeben.  
  
    |Installationsaktion|Anforderungen an die Anmeldeinformationen|  
    |-----------------------|---------------------------|  
    |Installieren einer neuen Gesamtstruktur|Lokaler Administrator auf dem Zielserver|  
    |Installieren Sie eine neue Domäne in einer vorhandenen Gesamtstruktur|Organisations-Admins|  
    |Installieren Sie einen zusätzlichen Domänencontroller in einer vorhandenen Domäne|Domänen-Admins|  
    |Adprep/forestprep ausführen|Schema-Admins, Organisations-Admins und Domänen-Admins|  
    |Adprep/domainprep ausführen|Domänen-Admins|  
    |Adprep/domainprep / gpprep ausführen|Domänen-Admins|  
    |Adprep/rodcprep ausführen|Organisations-Admins|  
  
    Sie können Berechtigungen zum Installieren von AD DS delegieren. Weitere Informationen finden Sie unter [Installation Management Tasks](https://technet.microsoft.com/library/cc773327(WS.10).aspx).  
  
Schritte-für-Schritt-Anleitung zur Förderung der neu und Replikat Windows Server 2012-Domänencontrollern mit Windows PowerShell-Cmdlets und Server-Manager finden Sie in den folgenden Links:  
  
-   [Installieren von Active Directory-Domänendienste (Stufe 100)](https://technet.microsoft.com/library/hh472162.aspx)  
  
-   [Installieren einer neuen Windows Server 2012 Active Directory-Gesamtstruktur (Stufe 200)](https://technet.microsoft.com/library/jj574166.aspx)  
  
-   [Installieren Sie einen Windows Server 2012-Domänencontrollerreplikats in einer vorhandenen Domäne (Stufe 200)](https://technet.microsoft.com/library/jj574134.aspx)  
  
-   [Installieren einer neuen Windows Server 2012 Active Directory untergeordneten oder Gesamtstrukturdomäne (Stufe 200)](https://technet.microsoft.com/library/jj574105.aspx)  
  
-   [Installieren Sie einen Windows Server 2012 Active Directory schreibgeschützten Domänencontroller (RODC) (Stufe 200)](https://technet.microsoft.com/library/jj574152.aspx)  
  
-   [Schrittweise Anleitung für die Einstellung von Windows Server 2012-Domänencontroller (En-US)](https://social.technet.microsoft.com/wiki/contents/articles/12370.step-by-step-guide-for-setting-up-windows-server-2012-domain-controller-en-us.aspx)  
  
## <a name="BKMK_WhatsNewEight"></a>Was ist neu in Windows Server 2012?  
Neue Features nach Serverrolle und Technologiebereich aufgelistet in der folgenden Tabelle. Weitere Whitepaper, Videodemonstrationen und Präsentationen zu anderen Features in Windows Server 2012 finden Sie unter [Server und Cloudplattform](https://www.microsoft.com/server-cloud/default.aspx).  
  
||||  
|-|-|-|  
|[Active Directory-Zertifikatdienste (AD CS)](https://technet.microsoft.com/library/hh831373.aspx)|[Active Directory-Rechteverwaltungsdienste (AD RMS)](https://technet.microsoft.com/library/hh831554.aspx)|[BitLocker-Laufwerkverschlüsselung](https://technet.microsoft.com/library/hh831412.aspx)|  
|[BranchCache](https://technet.microsoft.com/library/jj127252.aspx)|[Dynamic Host Configuration-Protokoll (DHCP)](https://technet.microsoft.com/library/jj200226.aspx)|[Domain Name System (DNS)](https://technet.microsoft.com/library/jj200224.aspx)|  
|[Failover-Clusterunterstützung](https://technet.microsoft.com/library/hh831414.aspx)|[File Server Resource Manager](https://technet.microsoft.com/library/hh831746.aspx)|[Gruppenrichtlinie](https://technet.microsoft.com/library/jj574108.aspx)|  
|[Hyper-V](https://technet.microsoft.com/library/hh831410.aspx)|[IP-Adressverwaltung (IPAM)](https://technet.microsoft.com/library/jj200214.aspx)|[Kerberos-Authentifizierung](https://technet.microsoft.com/library/hh831747.aspx)|  
|[Verwaltete Dienstkonten](https://technet.microsoft.com/library/hh831451.aspx)|[Netzwerke](https://technet.microsoft.com/library/jj200215.aspx)|[Remote Desktop Services](https://technet.microsoft.com/library/hh831527.aspx)|  
|[Die Sicherheitsüberwachung](https://technet.microsoft.com/library/hh849638.aspx)|[Server-Manager](https://blogs.technet.com/b/servermanager/archive/2012/06/27/server-manager-power-of-many-simplicity-of-one.aspx)|[Smartcards](https://technet.microsoft.com/library/hh849637.aspx)|  
|[TLS/SSL (Schannel SSP)](https://technet.microsoft.com/library/hh831771.aspx)|[Windows-Bereitstellungsdienste](https://technet.microsoft.com/library/hh974416.aspx)|[WindowsPowerShell 3.0](https://technet.microsoft.com/library/hh857339)|  
  
### <a name="automatic-maintenance-and-changes-to-restart-behavior-after-updates-are-applied-by-windows-update"></a>Automatische Wartung und Änderungen am Neustartverhalten nach Updates von Windows Update angewendet werden  
Vor der Veröffentlichung von Windows 8 verwaltete Windows Update einen eigenen internen Zeitplan zur Suche nach Updates und zum Herunterladen und installieren können. Es ist erforderlich, dass der Windows Update-Agent immer im Hintergrund laufen und verbrauchte Arbeitsspeicher und andere Systemressourcen.  
  
Windows 8 und Windows Server 2012 jetzt ein neues Feature namens [automatische Wartung](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx). Automatische Wartung konsolidiert zahlreiche unterschiedliche Features, die jeweils verwendet, um eine eigene Zeitplan- und Ausführungslogik. Dank dieser Konsolidierung verbrauchen all diese Komponenten viel weniger Systemressourcen, arbeiten einheitlich, beachten den neuen [Verbindungsstandby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) für neue Gerätetypen und verbrauchen weniger Batterie auf tragbaren Geräten.  
  
Da Windows Update ein Teil der automatischen Wartung in Windows 8 und Windows Server 2012 ist, ist der interne Zeitplan für die Konfiguration von Tag und die Zeit zum Installieren von Updates nicht mehr gültig. Um zu gewährleisten einheitliches, vorhersehbares Neustartverhalten für alle Geräte und Computer in Ihrem Unternehmen, einschließlich derer, die Windows 8 und Windows Server 2012 ausgeführt werden, finden Sie im Microsoft KB-Artikel [2885694](https://support.microsoft.com/kb/2885694) (oder finden Sie unter kumulative Rollup für Oktober 2013 [2883201](https://support.microsoft.com/kb/2883201)), konfigurieren Sie Richtlinieneinstellungen, die in der WSUS-Blogbeitrag beschriebenen [eine besser berechenbare Windows Update-Umgebung für Windows 8 und Windows Server 2012 (KB 2885694) aktivieren](http://blogs.technet.com/b/wsus/archive/2013/10/08/enabling-a-more-predictable-windows-update-experience-for-windows-8-and-windows-server-2012-kb-2885694.aspx).  
  

## <a name="BKMK_NewWS2012R2"></a>Was ist neu in AD DS in Windows Server 2012 R2?  
In der folgende Tabelle sind die neuen Features für AD DS in Windows Server 2012 R2 mit einem Link zu ausführlicheren Informationen wird zusammengefasst. Eine ausführlichere Erläuterung einiger Features und ihrer Anforderungen finden Sie unter [What's New in Active Directory unter Windows Server 2012 R2](https://technet.microsoft.com/library/dn268294.aspx).  
  
|Funktion|Beschreibung|  
|-----------|---------------|  
|[Arbeitsplatzbeitritt](https://technet.microsoft.com/library/dn280945.aspx)|Können Information-Worker ihre persönlichen Geräte mit ihrem Unternehmen den Zugriff auf Unternehmensressourcen und Dienste hinzufügen.|  
|[Web Application Proxy](https://technet.microsoft.com/library/dn280942.aspx)|Bietet Zugriff auf Webanwendung, die mit einem neuen Remotezugriffs-Rollendienst.|  
|[Active Directory-Verbunddienste](https://technet.microsoft.com/library/hh831502.aspx)|AD FS hat die vereinfachte Bereitstellung und erlaubt Benutzern den Zugriff auf Ressourcen über persönliche Geräte und unterstützt IT-Abteilungen, die Zugriffskontrolle zu verwalten.|  
|[SPN- und UPN-Eindeutigkeit](https://technet.microsoft.com/library/dn535779.aspx)|Domänencontroller unter Windows Server 2012 R2 blockieren die Erstellung doppelter Dienstprinzipalnamen (SPN) und Benutzerprinzipalnamen (UPNs).|  
|[Windows-Anmeldung automatisch Neustart anmelden (nach einem)](https://technet.microsoft.com/library/dn535772.aspx)|Aktiviert die Sperrbildschirm-Anwendungen neu gestartet und auf Windows 8.1-Geräten verfügbar sein.|  
|[TPM-Schlüsselnachweis](https://technet.microsoft.com/library/dn581921.aspx)|Ermöglicht die Zertifizierungsstellen mit dem kryptografisch in ein ausgestelltes Zertifikat bestätigt, dass der private Schlüssel der zertifikatanforderung tatsächlich durch ein Trusted Platform Module (TPM) geschützt ist.|  
|[Schutz von Anmeldeinformationen und Verwaltung](https://technet.microsoft.com/library/dn408190.aspx)|Neue Anmeldeinformationen und authentifizierungssteuerelemente um den Diebstahl von Anmeldeinformationen zu verringern.|  
|[Abschreibung von Dateireplikationsdienst (FRS)](https://technet.microsoft.com/library/dn535775.aspx)|Die Windows Server 2003-Domänenfunktionsebene ist ebenfalls veraltet, da auf der Funktionsebene FRS zum Replizieren von SYSVOL verwendet wird. Bedeutet, dass Sie eine neue Domäne auf einem Server erstellen, die Windows Server 2012 R2 ausgeführt wird, um die Domänenfunktionsebene muss sein WindowsServer 2008 oder neuer. Sie können weiterhin einen Domänencontroller hinzufügen, der Windows Server 2012 R2 zu einer vorhandenen Domäne ausgeführt wird, eine Windows Server 2003-Domänenfunktionsebene verfügt. Sie können nicht nur eine neue Domäne auf dieser Ebene erstellen.|  
|[Neue Domänen- und Gesamtstrukturfunktionsebenen](../active-directory-functional-levels.md)|Es gibt neue Funktionsebenen für Windows Server 2012 R2. Neue Features sind unter Windows Server 2012 R2-Domänenfunktionsebene verfügbar.|  
|[Änderungen am LDAP-Abfrageoptimierer](https://technet.microsoft.com/library/dn535775.aspx)|Leistungsverbesserung in LDAP-Suche und bessere Suchzeiten bei komplexen Abfragen.|  
|[Ereignis 1644](https://technet.microsoft.com/library/dn535775.aspx)|Ereignis-ID 1644 bei der Problembehandlung wurden Statistiken zu LDAP-Suche hinzugefügt.|  
|[Active Directory durchsatzverbesserung bei der Replikation](https://technet.microsoft.com/library/dn535775.aspx)|Passt die maximalen Durchsatz Active Directory-Replikation von 40Mbps auf ca. 600 Mbps|  
  
## <a name="BKMK_WhatsNewAD"></a>Was ist neu in AD DS in Windows Server 2012?  
In der folgende Tabelle sind die neuen Features für AD DS in Windows Server 2012 zusammengefasst, mit einem Link zu ausführlicheren Informationen, wo es verfügbar ist. Eine ausführlichere Erläuterung einiger Features und ihrer Anforderungen finden Sie unter [What's New in Active Directory-Domänendienste (AD DS)](https://technet.microsoft.com/library/hh831477.aspx).  
  
|Funktion|Beschreibung|  
|-----------|---------------|  
|Active Directory-basierte Aktivierung (AD BA) finden Sie unter [Volumenaktivierung: Übersicht](https://technet.microsoft.com/library/hh831612.aspx)|Vereinfacht das Konfigurieren der Verteilung und Verwaltung von Volumenlizenzen für Software.|  
|[Active Directory-Verbunddienste (AD FS)](https://technet.microsoft.com/library/hh831502.aspx)|Fügt die Installation von Rollen über Server-Manager vereinfacht, Einrichtung, automatische Verwaltung von Vertrauensstellungen, Unterstützung des SAML-Protokolls und mehr.|  
|Active Directory verlorene Page flush-Ereignisse|NTDS-ISAM-Ereignis 530 mit Jet-Fehler-1119 wird protokolliert, um verlorene Page flush-Ereignisse für Active Directory-Datenbanken zu ermitteln.|  
|[Active Directory Papierkorb-Benutzeroberfläche](https://technet.microsoft.com/library/hh831702.aspx#ad_recycle_bin_mgmt)|Active Directory-Verwaltungscenter (ADAC) ermöglicht GUI-Verwaltung der Papierkorbfunktion, die ursprünglich in Windows Server 2008 R2 eingeführt wurde.|  
|[Active Directory-Replikation und Topologieverwaltung von Windows PowerShell-cmdlets](https://technet.microsoft.com/library/hh831757.aspx)|Unterstützt die Erstellung und Verwaltung von Active Directory-Standorte, standortverknüpfungen, Verbindungsobjekten und mehr mithilfe von Windows PowerShell.|  
|[Dynamische Zugriffssteuerung](https://technet.microsoft.com/library/hh831717.aspx)|Neue anspruchsbasierten Authentifizierung-Plattform, die das Modell der Zugriffssteuerung erweitert.|  
|[Benutzeroberfläche für differenzierte Kennwortrichtlinien](https://technet.microsoft.com/library/hh831702.aspx#fine_grained_pswd_policy_mgmt)|ADAC fügt GUI-Unterstützung für die Erstellung, Bearbeitung und Zuweisung von PSOs ursprünglich in Windows Server 2008 hinzugefügt.|  
|[Gruppenverwaltete Dienstkonten (gMSA)](https://technet.microsoft.com/library/hh831782.aspx)|Ein neuer sicherheitsprinzipaltyp als gMSA bezeichnet. Auf mehreren Hosts ausgeführte Dienste können unter demselben gMSA-Konto ausgeführt werden.|  
|[DirectAccess-Offline-Domänenbeitritt](https://technet.microsoft.com/library/jj574150.aspx)|Offline-Domänenbeitritt erweitert durch DirectAccess erforderliche Komponenten einschließlich.|  
|[Schnelle Entwicklung durch Klonen virtueller Domänencontroller (DC)](https://technet.microsoft.com/library/hh831734.aspx#virtualized_dc_cloning)|Virtualisierte Domänencontroller können schnell durch Klonen vorhandenen virtuelle Domänencontroller mit Windows PowerShell-Cmdlets bereitgestellt werden.|  
|[RID-Pool-Änderungen](https://technet.microsoft.com/library/jj574229.aspx)|Fügt neue Überwachungsereignisse und Kontingente als Schutz vor der übermäßigen Nutzung des globalen RID-Pools. Verdoppelt optional die Größe des globalen RID-Pool, wenn der ursprüngliche Pool voll ausgelastet ist.|  
|Sicherer Zeitdienst|Erhöht die Sicherheit für W32tm durch Entfernen der geheime Schlüssel aus der Übertragung, die MD5-Hashfunktionen entfernt und den Server zur Authentifizierung mit Windows 8-zeitclients|  
|[USN-rollbackschutz für virtualisierte Domänencontroller](https://technet.microsoft.com/library/hh831734.aspx#safe_virt_dc)|Das versehentliche Wiederherstellen der Sicherungen von virtualisierten Domänencontrollern Momentaufnahmen nicht mehr bewirkt, dass USN-Rollback.|  
|[Windows PowerShell-Verlaufsanzeige](https://technet.microsoft.com/library/hh831702.aspx#windows_powershell_history_viewer)|Ermöglichen Sie es Administratoren, die Windows PowerShell-Befehle bei Verwendung von ADAC anzeigen.|  
  
### <a name="BKMK_"></a>Automatische Wartung und Änderungen am Neustartverhalten nach Updates von Windows Update angewendet werden  
Vor der Veröffentlichung von Windows 8 verwaltete Windows Update einen eigenen internen Zeitplan zur Suche nach Updates und zum Herunterladen und installieren können. Es ist erforderlich, dass der Windows Update-Agent immer im Hintergrund laufen und verbrauchte Arbeitsspeicher und andere Systemressourcen.  
  
Windows 8 und Windows Server 2012 jetzt ein neues Feature namens [automatische Wartung](https://msdn.microsoft.com/library/windows/desktop/hh848037(v=vs.85).aspx). Automatische Wartung konsolidiert zahlreiche unterschiedliche Features, die jeweils verwendet, um eine eigene Zeitplan- und Ausführungslogik. Dank dieser Konsolidierung verbrauchen all diese Komponenten viel weniger Systemressourcen, arbeiten einheitlich, beachten den neuen [Verbindungsstandby](https://msdn.microsoft.com/library/windows/hardware/jj248729.aspx) für neue Gerätetypen und verbrauchen weniger Batterie auf tragbaren Geräten.  
  
Da Windows Update ein Teil der automatischen Wartung in Windows 8 und Windows Server 2012 ist, ist der interne Zeitplan für die Konfiguration von Tag und die Zeit zum Installieren von Updates nicht mehr gültig. Um sicherzustellen, dass einheitliches, vorhersehbares Neustartverhalten für alle Geräte und Computer in Ihrem Unternehmen, einschließlich derer, die Ausführen von Windows 8 und Windows Server 2012 können Sie die folgenden gruppenrichtlinieneinstellungen konfigurieren:  
  
-   **Computerkonfiguration | Richtlinien | Administrative Vorlagen | Windows-Komponenten | Windows Update | Konfigurieren von automatischen Updates**  
  
-   **Computerkonfiguration | Richtlinien | Administrative Vorlagen | Windows-Komponenten | Windows Update | Keinen automatischen Neustart für angemeldete Benutzer**  
  
-   **Computerkonfiguration | Richtlinien | Administrative Vorlagen | Windows-Komponenten | Wartungsplanungsmodul | Zufällige Verzögerung für Wartung**  
  
Die folgende Tabelle enthält einige Beispiele zum Konfigurieren der Einstellungen für die gewünschte Neustartverhalten zu erreichen.  
  
|||  
|-|-|  
|**Szenario**|**Empfohlene Konfigurationen**|  
|**WSUS verwaltet.**<br /><br />-Installieren von Updates einmal pro Woche<br />-Neustart freitags um 23 Uhr|Für Computer automatisch installieren, Autom. Neustart bis zum gewünschten Zeitpunkt verhindern<br /><br />**Richtlinie**: Automatische Updates konfigurieren (aktiviert)<br /><br />Automatische Updates konfigurieren: 4 – Autom. herunterladen und laut Zeitplan installieren<br /><br />**Richtlinie**: keinen automatischen Neustart für angemeldete Benutzer (deaktiviert)<br /><br />**WSUS-Stichtage**: auf Freitag 23 Uhr festlegen|  
|**WSUS verwaltet.**<br /><br />-Installationen von staffeln über unterschiedliche Uhrzeiten/Tage|Richten Sie Zielgruppen für verschiedene Gruppen von Computern, die gemeinsam aktualisiert werden sollen<br /><br />Siehe obige Schritte für das vorherige Szenario<br /><br />Unterschiedliche Stichtage für unterschiedliche Zielgruppen|  
|**Nicht von WSUS verwaltet – keine Unterstützung für Stichtage**<br /><br />-Staffeln Installationen über unterschiedliche Uhrzeiten|**Richtlinie**: Automatische Updates konfigurieren (aktiviert)<br /><br />Automatische Updates konfigurieren: 4 – Autom. herunterladen und laut Zeitplan installieren<br /><br />**Registrierungsschlüssel:** aktivieren Sie das im Microsoft KB-Artikel besprochenen Registrierungsschlüssel [2835627](https://support.microsoft.com/kb/2835627)<br /><br />**Richtlinie:** zufällige Verzögerung für automatische Wartung (aktiviert)<br /><br />Legen Sie **zufällige Verzögerung für die regelmäßige Wartung** auf PT6H für 6-stündige zufällige Verzögerung, um Folgendes bereitzustellen:<br /><br />-Updates werden am konfigurierten Wartungszeit plus eine zufällige Verzögerung installiert.<br /><br />– Starten Sie für jeden Computer genau 3 Tage später stattfinden soll<br /><br />Sie können auch festlegen Sie unterschiedliche Wartungszeiten für jede Gruppe von Computern|  
  
Weitere Informationen darüber, warum der Windows-Entwicklungsteam diese Änderungen implementiert werden, finden Sie unter [Minimizing Restarts nach der automatischen Updates von Windows Update](http://blogs.msdn.com/b/b8/archive/2011/11/14/minimizing-restarts-after-automatic-updating-in-windows-update.aspx).  
  
## <a name="BKMK_InstallationChanges"></a>Ändert sich die Installation von AD DS Server-Rolle  
In Windows Server 2003 bis Windows Server 2008 R2, Sie ausgeführt haben, die X86 oder X64 Version des Adprep.exe-Befehlszeilentools vor dem Ausführen der Installations-Assistent für Active Directory Dcpromo.exe und Dcpromo.exe verfügte, von einem Medium oder für die unbeaufsichtigte Installation zu installieren.  
  
Ab Windows Server 2012, werden sich Befehlszeileninstallationen mithilfe des ADDSDeployment-Moduls in Windows PowerShell durchgeführt. GUI-basierte heraufstufungen werden im Server-Manager mit einem vollständig neuen AD DS-Konfigurationsassistenten ausgeführt. Zur Vereinfachung des Installationsprozesses ADPREP wurde in der AD DS-Installation integriert und wird bei Bedarf automatisch ausgeführt. Die Windows PowerShell basierende AD DS-Konfigurationsassistenten zielt automatisch auf die Schema- und infrastrukturmasterrollen in den Domänen, in denen Domänencontroller hinzugefügt werden, und klicken Sie dann die erforderlichen ADPREP-Befehle auf den relevanten Domänencontrollern Remote ausgeführt.  
  
Voraussetzungsprüfungen in der AD DS-Installations-Assistent identifiziert potenzielle Fehler vor Beginn der Installation. Fehlerzustände können korrigiert werden, um Bedenken bei einem teilweise abgeschlossenen Upgrade zu vermeiden. Der Assistent exportiert ein Windows PowerShell-Skript mit allen Optionen, die während der grafischen Installation angegeben wurden.  
  
Zusammen Änderungen bei der AD DS-Installation vereinfachen die Installation von domänencontrollerrollen und reduzieren die Wahrscheinlichkeit von administrativen Fehlern, insbesondere, wenn Sie mehrere Domänencontroller über globale Regionen und Domänen hinweg einsetzen.  
Ausführlichere Informationen zu GUI- und Windows PowerShell basierenden Installationen sowie die Befehlszeilensyntax und schrittweise Anleitungen finden Sie unter [installieren Sie Active Directory-Domänendienste](https://technet.microsoft.com/library/hh472162.aspx). Für Administratoren, die die Einführung von schemaänderungen in einer Active Directory-Gesamtstruktur unabhängig von der Installation von Windows Server 2012-Domänencontrollern in einer bestehenden Gesamtstruktur steuern möchten, können Adprep.exe-Befehle an einer Eingabeaufforderung mit erhöhten Rechten ausgeführt werden.  
  
## <a name="BKMK_DeprecatedFeatures"></a>Veraltete Features und verhaltensänderungen in Bezug auf AD DS in Windows Server 2012  
Es gibt einige Änderungen in Bezug auf AD DS:  
  
-   **Abschreibung von Adprep32.exe**  
  
    Es ist nur eine Version von Adprep.exe, und es oder höher ausgeführt, Bedarf auf 64-Bit-Servern, auf denen Windows Server 2008 ausgeführt werden kann. Sie können Remote ausgeführt werden und muss Remote ausgeführt werden, wenn die Ziel-Betriebsmasterrolle gehostet wird auf einem 32-Bit-Betriebssystem oder Windows Server 2003.  
  
-   **Abschreibung von Dcpromo.exe**  
  
    Dcpromo ist veraltet, obwohl in Windows Server 2012 nur sie weiterhin mit einer Antwortdatei oder Befehlszeilenparametern damit Organisationen Zeit für die Umstellung der vorhandenen Automatisierung auf die neue Windows PowerShell-Installationsoptionen haben erhalten ausgeführt werden kann.  
  
-   **LMHash für Benutzerkonten deaktiviert**  
  
    Sicheren Sie Standardeinstellungen in Vorlagen für Windows Server 2008, Windows Server 2008 R2 und Windows Server 2012 die NoLMHash-Richtlinie aktivieren, die in den Sicherheitsvorlagen von Windows 2000 und Windows Server 2003-Domänencontrollern deaktiviert ist. Deaktivieren Sie die NoLMHash-Richtlinie für LMHash-abhängige Clients als erforderlich ist, verwenden die Schritte im KB-Artikel [946405](https://support.microsoft.com/kb/946405).  
  
Ab Windows Server 2008, können Domänencontroller auch die folgenden sicheren Standardeinstellungen, gegenüber den Domänencontrollern, auf denen Windows Server 2003 oder Windows 2000 ausgeführt werden.  
  
|||||  
|-|-|-|-|  
|Verschlüsselungstyp oder-Richtlinie|Windows Server 2008-Standardeinstellung|Windows Server 2012 und Windows Server 2008 R2-Standardeinstellung|Kommentar|  
|AllowNT4Crypto|Deaktiviert|Deaktiviert|Drittanbieter-Server Message Block (SMB)-Clients können möglicherweise nicht mit den sicheren Standardeinstellungen auf Domänencontrollern kompatibel. In allen Fällen können diese Einstellungen auf Interoperabilität, aber nur auf Kosten der Sicherheit gelockert werden. Weitere Informationen finden Sie unter [Artikel 942564](https://go.microsoft.com/fwlink/?LinkId=164558) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=164558).|  
|DES|Aktiviert|Deaktiviert|[Artikel 977321](https://go.microsoft.com/fwlink/?LinkId=177717) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=177717)|  
|CBT/erweiterter Schutz für integrierte Authentifizierung|N/V|Aktiviert|Weitere Informationen finden Sie unter [Microsoft Security Advisory (937811)](https://go.microsoft.com/fwlink/?LinkId=164559) (https://go.microsoft.com/fwlink/?LinkId=164559) und [Artikel 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251).<br /><br />Überprüfen und installieren Sie den Hotfix [Artikel 977073](https://go.microsoft.com/fwlink/?LinkId=186394) (https://go.microsoft.com/fwlink/?LinkId=186394) in der Microsoft Knowledge Base nach Bedarf.|  
|LMv2|Aktiviert|Deaktiviert|[Artikel 976918](https://go.microsoft.com/fwlink/?LinkId=178251) in der Microsoft Knowledge Base (https://go.microsoft.com/fwlink/?LinkId=178251)|  
  
## <a name="BKMK_SysReqs"></a>Betriebssystemanforderungen  
In der folgenden Tabelle sind die Mindestanforderungen für Windows Server 2012 aufgeführt. Weitere Informationen zu den Systemanforderungen und Informationen zur installationsvorbereitung finden Sie unter [Installieren von Windows Server 2012](https://technet.microsoft.com/library/jj134246.aspx). Es gibt keine zusätzlichen Systemanforderungen zum Installieren einer neuen Active Directory-Gesamtstruktur, aber Sie sollten ausreichend Arbeitsspeicher zum der Inhalt von Active Directory-Datenbank zwischengespeichert, um die Verbesserung der Leistung für Domänencontroller, LDAP-Clientanforderungen und Active Directory-fähige Anwendungen hinzufügen. Wenn Sie einen vorhandenen Domänencontroller aktualisieren oder einen neuen Domänencontroller zu einer vorhandenen Gesamtstruktur hinzufügen, überprüfen Sie im nächsten Abschnitt, um sicherzustellen, dass der Server die speicherplatzanforderungen erfüllt.  
  
|||  
|-|-|  
|Prozessor|1,4-Ghz-64-Bit-Prozessor|  
|RAM|512 MB|  
|Freier Speicherplatz|32GB|  
|Bildschirmauflösung|800 x 600 oder höher|  
|Sonstige|DVD-Laufwerk, Tastatur, Internetzugriff|  
  
### <a name="BKMK_DiskSpaceDCWin8"></a>Speicherplatzanforderungen für ein Upgrade von Domänencontrollern  
Dieser Abschnitt behandelt die speicherplatzanforderungen nur für ein Upgrade von Domänencontrollern von Windows Server 2008 oder Windows Server 2008 R2. Weitere Informationen zu den speicherplatzanforderungen für ein Upgrade von Domänencontrollern auf frühere Versionen von Windows Server finden Sie unter [Erforderlicher Speicherplatz für das Upgrade auf Windows Server 2008](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008) oder [Erforderlicher Speicherplatz für das Upgrade auf Windows Server 2008 R2](https://technet.microsoft.com/library/cc754463(WS.10).aspx#BKMK_2008R2).  
  
Die Größe des Datenträgers, auf dem die Active Directory-Datenbank und-Protokolldateien gehostet wird, berücksichtigen Sie die benutzerdefinierte und anwendungsgesteuerte schemaerweiterungen, Anwendung und Administratoren initiierte Indizes auch den Platz für die Objekte und Attribute, die Sie in das Verzeichnis Laufe der bereitstellungslebensdauer des Domänencontrollers (normalerweise 5 bis 8 Jahre) hinzugefügt werden. Die richtige Bemessung zur Bereitstellungszeit ist in der Regel eine gute Investition im Vergleich zu höheren Kosten nach der Bereitstellung von Speicher zu erweitern. Weitere Informationen finden Sie unter [Capacity Planning for Active Directory Domain Services](https://social.technet.microsoft.com/wiki/contents/articles/14355.capacity-planning-for-active-directory-domain-services.aspx).  
  
Stellen Sie auf Domänencontrollern, die Sie aktualisieren möchten sicher, dass das Laufwerk, das Active Directory-hosts-(NTDS Datenbank. DIT) verfügt über freien Speicherplatz, der mindestens 20 % von der NTDS darstellt. DIT-Datei vor dem Beginn der Aktualisierung des Betriebssystems. Wenn nicht genügend freier Speicherplatz auf dem Volume vorhanden ist, kann das Upgrade fehlschlagen, und der upgradekompatibilitätsbericht gibt einen Fehler, der angibt, nicht genügend freier Speicherplatz:  
  
In diesem Fall können Sie versuchen Sie eine Offlinedefragmentierung der Active Directory-Datenbank, um zusätzlichen Speicherplatz zu gewinnen, und wiederholen Sie die Aktualisierung. Weitere Informationen finden Sie unter [Komprimieren der Verzeichnisdatenbankdatei (Offlinedefragmentierung)](https://technet.microsoft.com/library/cc794920(v=WS.10).aspx).  
  
### <a name="available-skus"></a>Verfügbaren SKUs  
Insgesamt sind 4 Editionen von Windows Server: Foundation, Essentials, Standard und Datacenter.   
Die beiden Editionen, die die AD DS-Rolle unterstützen werden Standard- und Datacenter.  
  
In früheren Versionen abweichenden Windows Server-Editionen in der Unterstützung für Serverrollen, die Anzahl der Prozessoren und die Unterstützung großer Arbeitsspeicher. Die Standard- und Datacenter-Editionen von Windows Server unterstützen alle Features und die zugrunde liegende Hardware variieren jedoch hinsichtlich der Virtualisierungsrechte - sind zwei virtuelle Instanzen zulässig, Standard Edition und für Datacenter Edition unbegrenzte virtuelle Instanzen zulässig sind.  
  
### <a name="windows-client-and-windows-server-operating-systems-that-are-supported-to-join-windows-server-domains"></a>Windows-Client und Windows Server-Betriebssysteme, die unterstützt werden, um Windows Server-Domänen beitreten  
Die folgenden Windows-Client und Windows Server-Betriebssysteme werden für Domänenmitgliedscomputer mit Domänencontrollern, auf denen Windows Server 2012 oder höher:  
  
-   Clientbetriebssysteme: Windows 8.1, Windows 8, Windows 7, Windows Vista 
  
    Computer, auf denen Windows 8.1 Windows 8 oder können außerdem Domänen beitreten, die Domänencontroller, zur früheren Version von Windows Server, einschließlich Windows Server 2003 oder höher verfügen. In diesem Fall jedoch einige Features von Windows 8 möglicherweise eine zusätzliche Konfiguration oder möglicherweise nicht verfügbar. Weitere Informationen zu diesen Features und Empfehlungen zur Verwaltung von Windows 8-Clients in Domänen mit Vorgängerversionen finden Sie unter [Ausführen von Windows 8-Computern in Windows Server 2003-Domänen](https://social.technet.microsoft.com/wiki/contents/articles/17361.running-windows-8-member-computers-in-windows-server-2003-domains.aspx).  
  
-   Serverbetriebssysteme: WindowsServer 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2, Windows Server 2003  
  
## <a name="BKMK_UpgradePaths"></a>Unterstützte direkte Aktualisierungspfade  
Domänencontroller, auf denen 64-Bit-Versionen von Windows Server 2008 oder Windows Server 2008 R2 können auf Windows Server 2012 aktualisiert werden. Sie können keine Domänencontroller aktualisieren, auf denen Windows Server 2003 oder 32-Bit-Versionen von Windows Server 2008 ausgeführt. Um diese ersetzen möchten, installieren Sie Domänencontroller, die eine höhere Version von Windows Server in der Domäne ausgeführt, und klicken Sie dann entfernen Sie die Domänencontroller, auf denen Windows Server 2003.  
  
|Wenn Sie diese Editionen ausgeführt werden|Sie können auf diesen Editionen aktualisieren.|  
|-------------------------------------|-------------------------------------|  
|Windows Server 2008 Standard mit SP2<br /><br />ODER<br /><br />Windows Server 2008 Enterprise mit SP2|Windows Server 2012 Standard<br /><br />ODER<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 Datacenter mit SP2|Windows Server 2012 Datacenter|  
|Windows Web Server 2008|Windows Server 2012 Standard|  
|Windows Server 2008 R2 Standard mit SP1<br /><br />ODER<br /><br />Windows Server 2008 R2 Enterprise mit SP1|Windows Server 2012 Standard<br /><br />ODER<br /><br />Windows Server 2012 Datacenter|  
|Windows Server 2008 R2 Datacenter mit SP1|Windows Server 2012 Datacenter|  
|Windows Web Server 2008 R2|Windows Server 2012 Standard|  
  
Weitere Informationen zu unterstützten Aktualisierungspfaden finden Sie unter [Evaluierungsversionen und Upgradeoptionen für Windows Server 2012](https://go.microsoft.com/fwlink/?LinkId=260917). Beachten Sie, dass einen Domänencontroller, der eine Evaluierungsversion von Windows Server 2012 direkt in eine Verkaufsversion ausgeführt wird, nicht konvertiert werden kann. In diesem Fall installieren Sie einen zusätzlichen Domänencontroller auf einem Server, der eine Verkaufsversion ausgeführt wird, und Entfernen von AD DS von dem Domänencontroller, der die Evaluierungsversion ausgeführt wird.  
  
Aufgrund eines bekannten Problems können Sie einen Domänencontroller nicht aktualisieren, der auf einer Server Core-Installation von Windows Server 2012 Server Core-Installationsoption von Windows Server 2008 R2 ausgeführt wird. Das Upgrade wird auf einem schwarzen Bildschirm spät im Upgradeprozess hängen. Beim Neustarten dieser Domänencontroller stellt eine Option in der Datei "Boot.ini" Rollback auf die vorherige Betriebssystemversion. Bei einem weiteren Neustart wird das automatische Rollback zur vorherigen Betriebssystemversion ausgelöst. Bis eine Lösung verfügbar ist, wird empfohlen, dass Sie installieren einen neuen Domänencontroller mit einer Server Core-Installation von Windows Server 2012 anstatt direktes Upgrade eines vorhandenen Domänencontrollers, das Server Core-Installationsoption von Windows Server 2008 R2 ausgeführt wird. Weitere Informationen finden Sie im KB-Artikel [2734222](https://support.microsoft.com/kb/2734222).  
  
## <a name="BKMK_FunctionalLevels"></a>Funktionale-Level-Funktionen und Anforderungen  
 Windows Server 2012 ist eine Windows Server 2003-Gesamtstrukturfunktionsebene erforderlich. Das heißt, bevor Sie einen Domänencontroller, der zu einer vorhandenen Active Directory-Gesamtstruktur Windows Server 2012 ausgeführt wird hinzufügen können, muss die Gesamtstrukturfunktionsebene auf WindowsServer 2003 oder höher sein. Dies bedeutet, die Domänencontroller, auf denen Windows Server 2008 R2, Windows Server 2008 oder Windows Server 2003 können in derselben Gesamtstruktur betrieben werden, aber die Domänencontroller, auf denen Windows 2000 Server werden nicht unterstützt und blockieren die Installation eines Domänencontrollers, der Windows Server 2012 ausgeführt wird. Enthält die Gesamtstruktur Domänencontroller unter Windows Server 2003 oder höher die Gesamtstrukturfunktionsebene jedoch Ebene ist immer noch Windows 2000, die Installation ebenfalls blockiert.  
  
Windows 2000-Domänencontroller müssen vor dem Hinzufügen von Windows Server 2012-Domänencontrollern der Gesamtstruktur entfernt werden. In diesem Fall sollten Sie den folgenden Workflow:  
  
1.  Installieren Sie Domänencontroller, auf denen WindowsServer 2003 oder höher ausgeführt werden. Dieser Domänencontroller können auf eine Evaluierungsversion von Windows Server bereitgestellt werden. Dieser Schritt erfordert außerdem [Ausführen von adprep.exe](https://technet.microsoft.com/library/dd464018(WS.10).aspx) als Voraussetzung für das Betriebssystem zu veröffentlichen.  
  
2.  Entfernen Sie die Windows 2000-Domänencontroller. Führen Sie eine Herabstufung oder das Entfernen von Windows Server 2000-Domänencontroller aus der Domäne und verwendete Active Directory-Benutzer und-Computer um die Domänencontrollerkonten für alle entfernten Domänencontroller zu entfernen.  
  
3.  Heraufstufen der Gesamtstrukturfunktionsebene auf Windows Server 2003 oder höher.  
  
4.  Installieren Sie Domänencontroller, auf denen Windows Server 2012 ausgeführt wird.  
  
5.  Entfernen Sie Domänencontroller, auf denen frühere Versionen von Windows Server ausführen.  
  
Die neue Domänenfunktionsebene von Windows Server 2012 ermöglicht ein neues Feature: die **KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos armoring** KDC-Richtlinie für administrative Vorlagen sind zwei Einstellungen (**immer Ansprüche bereitstellen** und **Authentifizierungsanfragen**), die Windows Server 2012 als Domänenfunktionsebene erforderlich.  
  
Die Gesamtstrukturfunktionsebene Windows Server2012 bietet neuen Funktionen, aber es wird sichergestellt, dass alle in der Gesamtstruktur erstellten neuen Domänen automatisch auf die Domänenfunktionsebene Windows Server2012. Die Domänenfunktionsebene Windows Server 2012 bietet keine weiteren neuen Features außer KDC-Unterstützung für Ansprüche, Verbundauthentifizierung und Kerberos-hochrüstung. Sie stellt jedoch sicher, dass alle Domänencontroller in der Domäne mit Windows Server 2012 ausgeführt wird. Weitere Informationen zu anderen Features, die auf verschiedenen Funktionsebenen verfügbar sind, finden Sie unter [Grundlegendes zur Active Directory-Domänendienste (AD DS) Functional Levels](../active-directory-functional-levels.md).  
  
Nachdem Sie die Gesamtstrukturfunktionsebene auf einen bestimmten Wert festgelegt haben, können Sie diese zurücksetzen oder herabstufen Funktionsebene der Gesamtstruktur, mit Ausnahme der folgenden: nach dem Heraufstufen der Gesamtstrukturfunktionsebene auf Windows Server 2012, können Sie es für Windows Server 2008 R2 herabstufen. Wenn Active Directory-Papierkorb nicht aktiviert wurde, können Sie auch die Gesamtstrukturfunktionsebene von Windows Server 2012 zu Windows Server 2008 R2 oder Windows Server 2008 oder Windows Server 2008 R2, Windows Server 2008 herabstufen. Wenn die Gesamtstrukturfunktionsebene auf Windows Server 2008 R2 festgelegt ist, kann es, z. B. für Windows Server 2003 zurückgesetzt werden.  
  
Nachdem Sie die Domänenfunktionsebene auf einen bestimmten Wert festgelegt haben, können Sie diese zurücksetzen oder herabstufen die Domänenfunktionsebene auf, mit Ausnahme der folgenden: Wenn Sie Heraufstufen der Domänenfunktionsebene Windows Server 2008 R2 oder Windows Server 2012, und wenn die Gesamtstrukturfunktionsebene auf Windows Server 2008 oder niedriger ist, haben Sie die Möglichkeit, die Domänenfunktionsebene auf Zurücksetzen "zurück" auf Windows Server 2008 oder Windows Server 2008 R2. Sie können die Domänenfunktionsebene nur von Windows Server 2012 zu Windows Server 2008 R2 oder Windows Server 2008 oder Windows Server 2008 R2, Windows Server 2008 herabstufen. Wenn die Domänenfunktionsebene auf Windows Server 2008 R2 festgelegt ist, kann es, z. B. für Windows Server 2003 zurückgesetzt werden.  
  
Weitere Informationen zu Features, die auf niedrigeren Funktionsebenen verfügbar sind, finden Sie unter [Grundlegendes zur Active Directory-Domänendienste (AD DS) Functional Levels](../active-directory-functional-levels.md).  
  
Neben den Funktionsebenen bietet ein Domänencontroller mit Windows Server2012 zusätzliche Features, die nicht auf einem Domänencontroller verfügbar sind, die eine frühere Version von Windows Server ausgeführt wird. Ein Domänencontroller mit Windows Server2012 kann z.B. für das Klonen virtueller Domänencontroller, verwendet werden, während ein Domänencontroller mit einer früheren Version von Windows Server kann nicht. Aber das Klonen virtueller Domänencontroller und virtuellen Domäne existieren in Windows Server 2012 haben keine Anforderungen bezüglich der Funktionsebene.  
  
> [!NOTE]  
> Microsoft Exchange Server 2013 erfordert eine Gesamtstruktur-Funktionsebene von WindowsServer 2003 oder höher.  
  
## <a name="BKMK_ServerRoles"></a>AD DS-Interoperabilität mit anderen Serverrollen und Windows-Betriebssysteme  
AD DS wird auf den folgenden Windows-Betriebssystemen nicht unterstützt:  
  
-   Windows MultiPoint Server  
  
-   Windows Server 2012 Essentials  
  
AD DS kann auf einem Server installiert werden, die auch die folgenden Serverrollen oder Rollendienste ausgeführt wird:  
  
-   Hyper-V Server  
  
-   Remotedesktop-Verbindungsbroker  
  
## <a name="BKMK_OpsMasters"></a>Betriebsmasterrollen  
Einige neue Features in Windows Server 2012 Einfluss auf die Betriebsmasterrollen:  
  
-   Der PDC-Emulator muss Windows Server 2012, um Unterstützung für das Klonen virtueller Domänencontroller ausgeführt werden. Es gibt zusätzliche erforderliche Komponenten zum Klonen von Domänencontrollern. Weitere Informationen finden Sie unter [Active Directory-Domänendienste (AD DS) Virtualization](https://technet.microsoft.com/library/hh831734.aspx).  
  
-   Der PDC-Emulator Windows Server 2012 ausgeführt wird, werden neue Sicherheitsprinzipale erstellt.  
  
-   Der RID-Master verfügt über neue RID-Ausstellung und Überwachungsfunktionen. Die Verbesserungen umfassen eine bessere ereignisprotokollierung, besser geeignete Grenzen und die Möglichkeit, im Notfall - erhöhen Sie die RID-pool Zuordnung um ein Bit. Weitere Informationen finden Sie unter [Managing RID Issuance](../../ad-ds/manage/Managing-RID-Issuance.md).  
  
> [!NOTE]  
> Wenn sie sich nicht um Betriebsmasterrollen sind, ist eine weitere Änderung in AD DS-Installation, dass DNS-Serverrolle und der globale Katalog standardmäßig auf allen Domänencontrollern installiert werden, auf denen Windows Server 2012 ausgeführt.  
  
## <a name="BKMK_Virtual"></a>Virtualisieren von Domänencontrollern  
Verbesserungen in AD DS ab Windows Server 2012 aktivieren, sicherere Virtualisierung von Domänencontrollern und die Möglichkeit zum Klonen von Domänencontrollern. Das Klonen von Domänencontrollern wiederum ermöglicht die schnelle Bereitstellung zusätzlicher Domänencontroller in einer neuen Domäne und vieles mehr. Weitere Informationen finden Sie unter [Introduction to Active Directory Domain Services & #40; AD DS & #41; Virtualisierung & #40; Stufe 100 & #41; ](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).  
  
## <a name="BKMK_Admin"></a>Verwaltung von Windows Server 2012-Servern  
Verwenden der [Remoteserver-Verwaltungstools für Windows 8](https://www.microsoft.com/download/details.aspx?id=28972) zum Verwalten von Domänencontrollern und anderen Servern, auf denen Windows Server 2012 ausgeführt. Sie können die Windows Server 2012 Remoteserver-Verwaltungstools auf einem Computer ausführen, die Windows 8 ausgeführt wird.  
  
## <a name="BKMK_AppCompat"></a>Die Anwendungskompatibilität  
In der folgende Tabelle werden die Active Directory-integrierte Microsoft-Anwendung behandelt. Die Tabelle enthält, welche Versionen von Windows Server, der die Anwendung installiert werden können und gibt an, ob die Einführung von Windows Server 2012-Domänencontrollern die Anwendungskompatibilität auswirkt.  
  
|Produkt|Notizen|  
|-----------|---------|  
|[Microsoft Configuration Manager 2007](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|Configuration Manager 2007 mit SP2 (enthält Configuration Manager 2007 R2 und Configuration Manager 2007 R3):<br /><br />– Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter **Hinweis:** Obwohl diese vollständig als Clients unterstützt, ist nicht geplant Hinzufügen der Unterstützung für diese Betriebssysteme mithilfe der Configuration Manager 2007-betriebssystembereitstellungsfeature bereitstellen. Darüber hinaus werden keine Standortserver oder Standortsysteme auf eine beliebige SKU von Windows Server 2012 unterstützt.|  
|[Microsoft SharePoint 2007](https://support.microsoft.com/kb/2728964)|Microsoft Office SharePoint Server 2007 wird für die Installation unter Windows Server 2012 nicht unterstützt.|  
|[Microsoft SharePoint 2010](https://support.microsoft.com/kb/2724471)|SharePoint 2010 Service Pack 2 ist zum Installieren und betreiben erforderlich <br />SharePoint 2010 auf Windows Server 2012-Servern<br /><br />SharePoint 2010 Foundation Service Pack 2 ist zum Installieren und betreiben von SharePoint 2010 Foundation auf Windows Server 2012-Servern erforderlich.<br /><br />Der Installationsvorgang von SharePoint Server 2010 (ohne Servicepacks) tritt ein Fehler auf Windows Server 2012<br /><br />Das erforderliche SharePoint Server 2010-Installationsprogramm (PrerequisiteInstaller.exe) tritt der Fehler "dieses Programm hat Kompatibilitätsprobleme". Klicken Sie auf "Führen Sie das Programm ohne Hilfestellung" zeigt die Fehlermeldung "überprüfen, ob SharePoint installiert werden kann und #124; SharePoint Server 2010 (ohne Servicepacks) kann nicht auf Windows Server 2012. installiert werden"|  
|[Microsoft SharePoint 2013](https://technet.microsoft.com/library/cc262485(v=office.15).aspx)|Mindestanforderungen für einen Datenbankserver in einer farm<br /><br />Die 64-Bit-Edition von Windows Server 2008 R2 Service Pack 1 (SP1) Standard, Enterprise oder Datacenter oder 64-Bit-Edition von Windows Server 2012 Standard oder Datacenter<br /><br />Mindestanforderungen für einen Einzelserver mit integrierter Datenbank:<br /><br />Die 64-Bit-Edition von Windows Server 2008 R2 Service Pack 1 (SP1) Standard, Enterprise oder Datacenter oder 64-Bit-Edition von Windows Server 2012 Standard oder Datacenter<br /><br />Mindestanforderungen für Front-End-Webserver und Anwendungsserver in einer Farm:<br /><br />Die 64-Bit-Edition von Windows Server 2008 R2 Service Pack 1 (SP1) Standard, Enterprise oder Datacenter oder 64-Bit-Edition von Windows Server 2012 Standard oder Datacenter.|  
|[Microsoft System Center Configuration Manager 2012](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Configuration Manager Service Pack 1:<br /><br />Microsoft wird den folgenden Betriebssystemen clientunterstützungsmatrix mit der Veröffentlichung von Service Pack 1 hinzugefügt:<br /><br />– Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter<br /><br />Alle Standortserverrollen - einschließlich Standortserver, SMS-Anbieter und Verwaltungspunkte - können auf Servern mit den folgenden betriebssystemeditionen bereitgestellt werden:<br /><br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter|  
|[Microsoft Lync Server 2013](https://technet.microsoft.com/library/gg412883.aspx)|Lync Server 2013 erfordert Windows Server 2008 R2 oder Windows Server 2012. Es kann nicht auf einer Server Core-Installation ausgeführt werden. Es kann ausgeführt werden, auf [virtuellen Server](https://technet.microsoft.com/library/gg399035.aspx).|  
|[Lync Server 2010](https://support.microsoft.com/kb/2777359)|Lync Server 2010 kann auf einer neuen (nicht per Upgrade erstellten) Installation Windows Server 2012 installiert werden, wenn [Oktober 2012 kumulativen Updates für Lync Server](https://support.microsoft.com/?kbid=2493736) installiert sind. Aktualisieren des Betriebssystems auf Windows Server 2012 für eine vorhandene Installation von Lync Server 2010 wird nicht unterstützt. Microsoft Lync Server 2010 Gruppe Chat-Server wird unter Windows Server 2012 auch nicht unterstützt.|  
|[System Center 2012 Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|System Center 2012 Endpoint Protection Service Pack 1 wird die clientunterstützungsmatrix um die folgenden Betriebssysteme aktualisieren.<br /><br />– Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter|  
|[System Center 2012 Forefront Endpoint Protection](http://blogs.technet.com/b/configmgrteam/archive/2012/09/10/support-questions-about-windows-8-and-windows-server-2012.aspx)|FEP 2010 mit Updaterollup 1 wird die clientunterstützungsmatrix um die folgenden Betriebssysteme aktualisieren:<br /><br />– Windows 8 Pro<br />– Windows 8 Enterprise<br />– Windows Server 2012 Standard<br />– Windows Server 2012 Datacenter|  
|Forefront Threat Management Gateway (TMG)|TMG wird nur auf Windows Server 2008 und Windows Server 2008 R2 ausgeführt werden unterstützt. Weitere Informationen finden Sie unter [System Requirements for Forefront TMG](https://technet.microsoft.com/library/dd896981.aspx).|  
|Windows Server Update Services|Diese Version von WSUS unterstützt bereits Windows 8-basierte Computer oder Windows Server 2012-basierte Computer als Clients.|  
|Windows Server Update Services 3.0|Update-KB-Artikel [2734608](https://support.microsoft.com/kb/2734608) können Server, auf denen Windows Server Update Services (WSUS) 3.0 SP2 ausgeführt werden Updates für Computer bereitstellen, auf denen Windows 8 oder Windows Server 2012 ausgeführt werden: **Hinweis:** Kunden mit eigenständigen WSUS 3.0 SP2-Umgebungen oder System Center Configuration Manager 2007 Service Pack 2-Umgebungen mit WSUS 3.0 SP2 benötigen [2734608](https://support.microsoft.com/kb/2734608) ordnungsgemäß auf Computern mit Windows 8 oder Windows Server 2012-basierte Computer als Clients verwalten.|  
|[Exchange 2013](https://technet.microsoft.com/library/bb691354.aspx)|Windows Server 2012 Standard und Datacenter werden für die folgenden Rollen unterstützt: Schemamaster, globaler Katalogserver, Domänencontroller, Postfach- und Clientzugriffs-Serverrolle<br /><br />Gesamtstrukturfunktionsebene: WindowsServer 2003 oder höher<br /><br />Quelle: Exchange 2013-Systemanforderungen|  
|Exchange 2010|[Quelle: Exchange 2010 Service Pack 3](https://blogs.technet.com/b/exchange/archive/2012/09/25/announcing-exchange-2010-service-pack-3.aspx)<br /><br />Exchange 2010 mit Service Pack 3 kann auf Windows Server 2012-Mitgliedsservern installiert werden.<br /><br />[Exchange 2010 – Systemanforderungen](https://technet.microsoft.com/library/aa996719(EXCHG.141).aspx) Listet die neuesten unterstützten Schemas, globale Katalog und Domänencontroller als Windows Server 2008 R2.<br /><br />Gesamtstrukturfunktionsebene: WindowsServer 2003 oder höher|  
|SQLServer 2012|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />SQL Server 2012 RTM wird unter Windows Server 2012 unterstützt.|  
|SQL Server 2008 R2|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Erfordert SQL Server 2008 R2 mit Service Pack 1 oder höher, um auf Windows Server 2012 zu installieren.|  
|SQLServer 2008|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Erfordert SQL Server 2008 mit Service Pack 3 oder höher, um auf Windows Server 2012 zu installieren.|  
|SQLServer 2005|Quelle: KB [2681562](https://support.microsoft.com/kb/2681562)<br /><br />Zum Installieren von auf Windows Server 2012 unterstützt nicht.|  
  
## <a name="BKMK_KnownIssues"></a>Bekannte Probleme  
Die folgende Tabelle enthält bekannte Probleme im Zusammenhang mit AD DS-Installation.  
  
||||  
|-|-|-|  
|Titel und Nummer des KB-Artikel|Betroffener Technologiebereich|Problem/Beschreibung|  
|[2830145](https://support.microsoft.com/kb/2830145): SID S-1-18-1 und SID S-1-18-2 können nicht unter Windows 7 oder Windows Server 2008 R2-basierten Computern in einer domänenumgebung nicht zugeordnet werden|AD DS-Management/App-Kompatibilität|Anwendungen, die SID S-1-18-1 und SID S-1-18-2, die in Windows Server 2012 neu sind, möglicherweise nicht, da die SIDs auf Windows 7 oder Windows Server 2008 R2-basierten Computern aufgelöst werden kann. Um dieses Problem zu beheben, installieren Sie den Hotfix auf dem Windows 7 oder Windows Server 2008 R2-basierten Computern in der Domäne.|  
|[2737129](https://support.microsoft.com/kb/2737129): gruppenrichtlinienvorbereitung wird nicht ausgeführt, wenn Sie eine vorhandene Domäne automatisch für Windows Server 2012 vorbereiten|AD DS-Installation|Adprep/domainprep / gpprep wird nicht automatisch ausgeführt, als Teil der Installation des ersten Domänencontrollers, der Windows Server 2012 in einer Domäne ausgeführt wird. Wenn es nicht bereits in der Domäne ausgeführt wurde, muss es manuell ausgeführt werden.|  
|[2737416](https://support.microsoft.com/kb/2737416): Wiederholung von Warnungen bei Windows PowerShell-basierte Bereitstellung von Domänencontrollern|AD DS-Installation|Warnungen bei der Prüfung der erforderlichen Komponenten angezeigt werden können, und dann noch einmal während der Installation.|  
|[2737424](https://support.microsoft.com/kb/2737424): "Das Format des angegebenen Domänennamens ist ungültig" Fehler beim Versuch, Active Directory-Domänendienste von einem Domänencontroller zu entfernen.|AD DS-Installation|Dieser Fehler wird angezeigt, wenn Sie den letzten Domänencontroller in einer Domäne entfernen, in denen vorab erstellte RODC-Konten noch vorhanden sind. Dies betrifft Windows Server 2012, Windows Server 2008 R2 und Windows Server 2008.|  
|[2737463](https://support.microsoft.com/kb/2737463): Domänencontroller startet nicht, c00002e2-Fehler auftritt, oder "Option auswählen" werden angezeigt.|AD DS-Installation|Ein Domänencontroller startet nicht, da ein Administrator Dism.exe, Pkgmgr.exe oder Ocsetup.exe zum Entfernen der DirectoryServices-DomainController-Rolle verwendet.|  
|[2737516](https://support.microsoft.com/kb/2737516): Beschränkungen der IFM-Überprüfung in Windows Server 2012-Server-Manager|AD DS-Installation|IFM-Überprüfung kann begrenzt ist, wie im KB-Artikel erläutert.|  
|[2737535](https://support.microsoft.com/kb/2737535): Install-AddsDomainController-Cmdlet gibt parametersatzfehler für RODC|AD DS-Installation|Sie können einen Fehler empfangen, wenn Sie versuchen, einen Server an ein RODC-Konto verbinden, wenn Sie die Argumente, die bereits aufgefüllt werden auf das vorab erstellte RODC-Konto angeben.|  
|[2737560](https://support.microsoft.com/kb/2737560): "Kann nicht Exchange-schemakonfliktüberprüfung" Fehler, und Überprüfung der Voraussetzungen ein Fehler auftritt|AD DS-Installation|Überprüfung der Voraussetzungen ein Fehler auftritt, wenn Sie den ersten Windows Server 2012-Domänencontroller in einer vorhandenen Domäne konfigurieren, da Domänencontroller die SeServiceLogonRight für Netzwerkdienst fehlt oder weil WMI- oder DCOM-Protokolle blockiert sind.|  
|[2737797](https://support.microsoft.com/kb/2737797): AddsDeployment-Modul mit - Whatif-Argument zeigt falsche DNS-Ergebnisse|AD DS-Installation|Der – WhatIf-Parameter zeigt-DNS-Server nicht installiert werden, aber es werden.|  
|[2737807](https://support.microsoft.com/kb/2737807): das nächste Schaltfläche ist nicht verfügbar, auf der Seite Domänencontrolleroptionen|AD DS-Installation|Die Schaltfläche "Weiter" ist auf der Seite Domänencontrolleroptionen deaktiviert, weil die IP-Adresse des Zieldomänencontrollers keinem vorhandenen Subnetz oder Standort zugeordnet ist, oder weil das DSRM-Kennwort ist nicht richtig eingegeben und bestätigt.|  
|[2737935](https://support.microsoft.com/kb/2737935): active Directory-Installation stoppt bei der Phase "NTDS-Einstellungsobjekts erstellen"|AD DS-Installation|Die Installation hängt, weil das lokale Administratorkennwort der Domäne übereinstimmt oder weil Netzwerkprobleme kritische Replikation durch Netzwerkfehler verhindert.|  
|[2738060](https://support.microsoft.com/kb/2738060): "Zugriff verweigert" angezeigt wird, wenn Sie eine untergeordnete Domäne Remote erstellen, indem Sie mithilfe von Install-AddsDomain|AD DS-Installation|Die Fehlermeldung wird angezeigt, wenn Sie Install-ADDSDomain mit dem Invoke-Command-Cmdlet ausführen, wenn dnsdelegationcredential über ein falsches Kennwort verfügt.|  
|[2738697](https://support.microsoft.com/kb/2738697): "der Server ist nicht funktionstüchtig" Domänencontroller-Konfigurationsfehler beim Konfigurieren eines Servers mit dem Server-Manager|AD DS-Installation|Sie erhalten diesen Fehler, wenn Sie versuchen, die AD DS auf einem Arbeitsgruppencomputer zu installieren, da die NTLM-Authentifizierung deaktiviert ist.|  
|[2738746](https://support.microsoft.com/kb/2738746): Sie erhalten Zugriff verweigert wird, nach dem Anmelden an einem lokalen Domänenadministratorkonto|AD DS-Installation|Wenn Sie über ein lokales Administratorkonto statt über das integrierte Administratorkonto anmelden, und klicken Sie dann eine neue Domäne erstellen, wird das Konto nicht der Gruppe "Domänen-Admins" hinzugefügt.|  
|[2743345](https://support.microsoft.com/kb/2743345): Adprep/gpprep-Fehler "das System nicht die angegebene Datei nicht gefunden" oder Absturz des Tools|AD DS-Installation|Sie erhalten diesen Fehler beim Ausführen Adprep/gpprep, weil der Infrastrukturmaster implementiert ist einen separaten namespace|  
|[2743367](https://support.microsoft.com/kb/2743367): Adprep "keine gültige Win32-Anwendung" Fehler unter Windows Server 2003, 64-Bit-Version|AD DS-Installation|Sie erhalten diesen Fehler, da Windows Server 2012 Adprep unter Windows Server 2003 ausgeführt werden kann.|  
|[2753560](https://support.microsoft.com/kb/2753560): ADMT 3.2 und PES 3.1-Installationsfehler unter Windows Server 2012|ADMT|ADMT 3.2 kann entwurfsbedingt unter Windows Server 2012 installiert werden.|  
|[2750857](https://support.microsoft.com/kb/2750857): DFS-Replikation Diagnoseberichte nicht ordnungsgemäß in Internet Explorer 10 anzeigen|DFS-Replikation|Der Diagnosebericht der DFS-Replikation wird aufgrund von Änderungen in Internet Explorer 10 nicht richtig angezeigt.|  
|[2741537](https://support.microsoft.com/kb/2741537): remoteaktualisierungen der Gruppenrichtlinie sind für Benutzer sichtbar|Gruppenrichtlinie|Dies liegt an geplanten Aufgaben, die im Kontext der einzelnen angemeldeten Benutzer ausgeführt. Die Windows-Taskplaners erfordert in diesem Szenario eine interaktive Eingabeaufforderung.|  
|[2741591](https://support.microsoft.com/kb/2741591): ADM-Dateien nicht in SYSVOL in der GPMC-infrastrukturstatusoption vorhanden sind.|Gruppenrichtlinie|Für die Gruppenrichtlinienreplikation kann "Replikation" melden, weil der GPMC-Infrastrukturstatus keine angepasste Filterregeln befolgt.|  
|[2737880](https://support.microsoft.com/kb/2737880): "der Dienst kann nicht gestartet werden" Fehler bei AD DS-Konfiguration|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler beim Installieren oder Entfernen von AD DS oder Klonen, weil der DS-rollenserverdienst deaktiviert ist.|  
|[2742836](https://support.microsoft.com/kb/2742836): zwei DHCP-Leases werden für jeden Domänencontroller erstellt, wenn Sie das Feature zum Klonen VDC verwenden|Klonen virtueller Domänencontroller|Dies geschieht, weil der geklonte Domänencontroller einen Lease erhalten, bevor Sie das Klonen und erneut beim Klonen abgeschlossen wurde.|  
|[2742844](https://support.microsoft.com/kb/2742844): Domänencontroller der Klonvorgang fehl und der Server neu gestartet wird im Verzeichnisdienst-Wiederherstellungsmodus in Windows Server 2012|Klonen virtueller Domänencontroller|Der geklonte Domänencontroller wird im Verzeichnisdienst-Wiederherstellungsmodus, weil das Klonen einer Vielzahl von im KB-Artikel aufgeführten Gründen ein Fehler aufgetreten ist.|  
|[2742874](https://support.microsoft.com/kb/2742874): Klonen des Domänencontrollers werden nicht neu erstellt alle Dienstprinzipalnamen|Klonen virtueller Domänencontroller|Einige dreiteilige Dienstprinzipalnamen werden auf dem geklonten Domänencontroller aufgrund einer Einschränkung des umbenennungsprozesses der Domäne nicht wiederhergestellt.|  
|[2742908](https://support.microsoft.com/kb/2742908): "keine Anmeldeserver verfügbar" Fehler nach dem Klonen des Domänencontrollers|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler, wenn Sie versuchen, sich anzumelden, nachdem der Fehler beim Klonen eines virtualisierten Domänencontrollers, weil das Klonen und der Domänencontroller im Verzeichnisdienst-Wiederherstellungsmodus gestartet wird. Melden Sie sich als. \administrator Behandlung des Fehlers beim Klonen.|  
|[2742916](https://support.microsoft.com/kb/2742916): Klonen des Domänencontrollers tritt der Fehler 8610 in "Dcpromo.log"|Klonen virtueller Domänencontroller|Fehler beim Klonen, weil der PDC-Emulator keine eingehende Replikation der Domänenpartition, ist wahrscheinlich, da die Rolle übertragen wurde ausgeführt hat.|  
|[2742927](https://support.microsoft.com/kb/2742927): "Index lag außerhalb des zulässigen Bereichs" New-AdDcCloneConfig-Fehler|Klonen virtueller Domänencontroller|Die Fehlermeldung wird angezeigt, nach dem Ausführen von Cmdlets New-ADDCCloneConfigFile beim Klonen von virtueller Domänencontrollern, da das Cmdlet nicht über ein Eingabeaufforderungsfenster mit erhöhten Rechten ausgeführt wurde oder weil das Zugriffstoken nicht der Gruppe "Administratoren" enthält.|  
|[2742959](https://support.microsoft.com/kb/2742959): Klonen des Domänencontrollers tritt der Fehler 8437: "Ungültiger Parameter wurde für diesen Replikationsvorgang angegeben"|Klonen virtueller Domänencontroller|Fehler beim Klonen des ein ungültiger klonname oder ein doppelter NetBIOS-Name angegeben wurde.|  
|[2742970](https://support.microsoft.com/kb/2742970): DC Klonen tritt ein Fehler ohne Verzeichnisdienst-Wiederherstellungsmodus, doppelte Quelle und den geklonten Computer|Klonen virtueller Domänencontroller|Der geklonte virtuelle Domänencontroller wird in Directory Services Repair Verzeichnisdienstwiederherstellungsmodus (DSRM), indem ein doppelter Name als Quelldomänencontroller, da die Datei DCCloneConfig.xml nicht am richtigen Speicherort erstellt wurde oder weil der Quelldomänencontroller vor dem Klonen neu gestartet wurde.|  
|[2743278](https://support.microsoft.com/kb/2743278): Fehler 0 x 80041005 beim Klonen des Domänencontrollers|Klonen virtueller Domänencontroller|Der geklonte Domänencontroller wird im DSRM gestartet, weil nur ein WINS-Server angegeben wurde. Wenn WINS-Server angegeben ist, müssen immer der bevorzugte und alternative WINS-Server angegeben werden.|  
|[2745013](https://support.microsoft.com/kb/2745013): Fehlermeldung "Server ist nicht funktionstüchtig", wenn das Ausführen von New-AdDcCloneConfigFile in Windows Server 2012|Klonen virtueller Domänencontroller|Sie erhalten diesen Fehler, nachdem Sie das Cmdlet "New-ADDCCloneConfigFile" ausgeführt, da der Server mit einen globalen Katalogserver herstellen kann.|  
|[2747974](https://support.microsoft.com/kb/2747974): klonereignis 2224 Domänencontroller liefert fehlerhaften Hinweis|Klonen virtueller Domänencontroller|Ereignis-ID 2224 wird fälschlicherweise, dass verwaltete Dienstkonten vor dem Klonen entfernt werden müssen. Eigenständige verwaltete Dienstkonten müssen entfernt werden, aber Gruppenverwaltete Dienstkonten bewirken keine Blockierung klonen.|  
|[2748266](https://support.microsoft.com/kb/2748266): ein Laufwerks mit BitLocker-Verschlüsselung kann nicht entsperrt werden, nach dem upgrade auf Windows 8|BitLocker|"Anwendung wurde nicht gefunden" wird angezeigt, wenn Sie versuchen, ein Laufwerk auf einem Computer zu entsperren, die von Windows 7 aktualisiert wurde.|  
  
## <a name="see-also"></a>Siehe auch  
[Evaluierungsressourcen für Windows Server 2012](https://technet.microsoft.com/evalcenter/hh708766.aspx)  
[Windows Server 2012-Evaluierungshandbuch](https://download.microsoft.com/download/5/B/2/5B254183-FA53-4317-B577-7561058CEF42/WS%202012%20Evaluation%20Guide.pdf)  
[Installieren und Bereitstellen von WindowsServer 2012](https://technet.microsoft.com/library/hh831620.aspx)  
  


