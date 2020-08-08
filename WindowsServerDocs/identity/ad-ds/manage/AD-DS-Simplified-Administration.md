---
ms.assetid: f74eec9a-2485-4ee0-a0d8-cce01250a294
title: Vereinfachte Verwaltung für AD DS
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.openlocfilehash: 61961acf9fc1c858fddb4da70b4899e229ec6a3d
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87956977"
---
# <a name="ad-ds-simplified-administration"></a>Vereinfachte Verwaltung für AD DS

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

In diesem Thema werden die Funktionen und Vorteile der Bereitstellung und Verwaltung von Windows Server 2012-Domänen Controllern sowie die Unterschiede zwischen der Bereitstellung des Betriebssystem-DC und der neuen Windows Server 2012-Implementierung erläutert.

In Windows Server 2012 wurde die nächste Generation von Active Directory Domain Services vereinfachte Verwaltung eingeführt, und die Neuerstellung der Domäne war seit Windows 2000 Server der größte. Die vereinfachte AD DS-Administration ist eine Umsetzung der Erfahrungen zwölf Jahren Active Directory und bietet Architekten und Administratoren ein flexibleres, intuitiveres und leichter zu unterstützendes Administrationserlebnis. Hierzu mussten wir neue Versionen existierender Technologien erstellen und die Funktionen einiger Komponenten aus Windows Server 2008 R2 erweitern.

Die vereinfachte AD DS-Administration ist ein neuartiger Weg der Domänen-Bereitstellung.

- Die AD DS-Rollenbereitstellung ist nun Teil der neuen Server-Manager-Architektur und erlaubt die Remote-Installation
- Als AD DS-Bereitstellungs- und Konfigurations-Engine dient nun Windows PowerShell, selbst bei Verwendung des neuen AD DS-Konfigurations-Assistenten
- Schemaerweiterung, Gesamtstruktur- und Domänenvorbereitung sind automatisch Teil der Domänencontroller-Heraufstufung und umfassen keine separaten Aufgaben mehr auf speziellen Servern wie z. B. dem Schemamaster
- Zur Heraufstufung gehört nun eine Voraussetzungsprüfung, bei der die Bereitschaft von Gesamtstruktur und Domäne für den neuen Domänencontroller geprüft und somit Fehler bei der Heraufstufung vermieden werden
- Das Active Directory-Modul für Windows PowerShell enthält nun Cmdlets für die Verwaltung von Replikationstopologien, dynamische Zugriffssteuerung und andere Operationen
- Die Windows Server 2012-Gesamtstrukturfunktionsebene enthält keine neuen Features, und die Domänenfunktionsebene wird nur für einen Teil der neuen Kerberos-Features benötigt. Administratoren sind daher weniger häufig auf homogene Domänencontroller-Umgebungen angewiesen
- Virtualisierte Domänencontroller werden nun vollständig unterstützt, um automatische Bereitstellung zu unterstützen und Rollbackschutz zu bieten
   - Weitere Informationen zu virtualisierten Domänen Controllern finden [Sie unter Einführung in Active Directory Domain Services &#40;AD DS&#41; Virtualization &#40;Ebene 100&#41;](../../ad-ds/Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md).

Außerdem wurden zahlreiche Verbesserungen in den Bereichen Verwaltung und Wartung vorgenommen:

- Das Active Directory-Verwaltungscenter enthält einen grafischen Active Directory-Papierkorb, differenzierte Kennwortrichtlinien und die Windows PowerShell-Verlaufsanzeige
- Der neue Server-Manager bietet AD DS-spezifische Bildschirme für die Leistungsüberwachung, Analyse bewährter Methoden, kritische Dienste und Ereignisprotokolle
- Gruppenverwaltete Dienstkonten unterstützen mehrere Computer mit denselben Sicherheitsprinzipalen
- Verbesserungen bei der Ausstellung von relativen Bezeichnern (RIDs) zur Erleichterung der Verwaltung älterer Active Directory-Domänen

AD DS von anderen neuen Features, die in Windows Server 2012 enthalten sind, wie z. b.:

- NIC-Teaming und Data Center Bridging
- DNS-Sicherheit und schnellere, in AD integrierte Zonenverfügbarkeit nach dem Hochfahren
- Verbesserungen der Zuverlässigkeit und Skalierbarkeit von Hyper-V
- BitLocker-Netzwerkentsperrung
- Zusätzliche Windows PowerShell-Module für die Komponentenverwaltung

## <a name="adprep-integration"></a>ADPREP-Integration

Erweiterungen des Gesamtstrukturschemas und Domänenvorbereitung in Active Directory sind nun in den Konfigurationsprozess des Domänencontrollers integriert. Wenn Sie einen neuen Domänencontroller in einer bestehenden Gesamtstruktur heraufstufen, erkennt der Prozess den Upgradestatus und die Phasen für Schemaerweiterung und Domänenvorbereitung werden automatisch ausgeführt. Der Benutzer, der den ersten Windows Server 2012-Domänencontroller installiert, muss weiterhin ein Unternehmens-Admin und Schema-Admin sein oder entsprechende gültige alternative Anmeldeinformationen eingeben.

Adprep.exe ist weiterhin auf der DVD enthalten, um Gesamtstrukturen und Domänen separat vorbereiten zu können. Die mit Windows Server 2012 ausgelieferte Version des Tools ist abwärtskompatibel mit Windows Server 2008 x64 und Windows Server 2008 R2. Adprep.exe unterstützt außerdem remote-forestprep und remote-domainprep, genau wie die ADDSDeployment-basierten Konfigurationstools für Domänencontroller.

Weitere Informationen zu Adprep und zur Gesamtstrukturvorbereitung in älteren Betriebssystemen finden Sie unter [Running Adprep (Windows Server 2008 R2)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd464018(v=ws.10)).

## <a name="server-manager-ad-ds-integration"></a>AD DS-Integration mit Server-Manager

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_Dashboard.png)

Server-Manager dient als Hub für Serververwaltungsaufgaben. Das Dashboardähnliche Aussehen aktualisiert die Ansichten installierter Rollen und Remote-Servergruppen automatisch in regelmäßigen Abständen. Server-Manager ermöglicht die zentralisierte Verwaltung lokaler und remote-Server ohne jeglichen Konsolenzugriff.

Active Directory Domain Services ist eine dieser Hub-Rollen. Wenn Sie Server-Manager auf einem Domänen Controller oder auf einem Windows 8-Remoteserver-Verwaltungstools ausführen, werden wichtige aktuelle Probleme in den Domänen Controllern in Ihrer Gesamtstruktur angezeigt.

Zu diesen Ansichten zählen:

- Serververfügbarkeit
- Systemmonitor-Warnungen für hohe CPU- und Speicherauslastung
- Der Status AD DS-spezifischer Windows-Dienste
- Neue verzeichnisdienstbezogene Warnungen und Fehler im Ereignisprotokoll
- Analyse der Umsetzung bewährter Methoden in einem Domänencontroller anhand einer Reihe von Microsoft festgelegter Regeln

## <a name="active-directory-administrative-center-recycle-bin"></a>Active Directory-Verwaltungscenter - Papierkorb

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_ADAC.png)

Mit Windows Server 2008 R2 wurde der Active Directory-Papierkorb eingeführt, mit dem gelöschte Active Directory-Objekte auch ohne Datensicherung, Neustart des AD DS-Dienstes oder Neustart von Domänencontrollern wiederhergestellt werden können.

Windows Server 2012 erweitert die Windows PowerShell-basierten Wiederherstellungskapazitäten um eine neue grafische Oberfläche im Active Directory-Verwaltungscenter. Dort können Administratoren den Papierkorb aktivieren und gelöschte Objekte in den Domänenkontexten der Gesamtstruktur suchen und wiederherstellen, ohne dafür direkt irgendwelche Windows PowerShell-Cmdlets ausführen zu müssen. Active Directory-Verwaltungscenter und Active Directory-Papierkorb verwenden unter der Oberfläche weiterhin Windows PowerShell. Sie können Ihre alten Skripts und Prozeduren also weiterhin verwenden.

Weitere Informationen zum Active Directory-Papierkorb finden Sie unter [Active Directory Recycle Bin Step-by-Step Guide (Windows Server 2008 R2)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd392261(v=ws.10)).

## <a name="active-directory-administrative-center-fine-grained-password-policy"></a>Active Directory-Verwaltungscenter - differenzierte Kennwortrichtlinien (FGPP)

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_FGPP.png)

Mit Windows Server 2008 wurden die differenzierten Kennwortrichtlinien eingeführt, mit denen Administratoren unterschiedliche Kennwort- und Kontosperrungsrichtlinien pro Domäne konfigurieren können. Auf diese Weise können Domänen flexiblere Kennwortregeln auf Basis von Benutzern und Gruppen enthalten. Diese Funktion enthielt jedoch keine grafische Oberfläche und musste von Administratoren mithilfe von Ldp.exe oder Adsiedit.msc konfiguriert werden. Mit Windows Server 2008 R2 wurde das Active Directory-Modul für Windows PowerShell eingeführt, mit dem Administratoren eine Befehlszeilenschnittstelle für FGPP zur Verfügung haben.

Windows Server 2012 enthält eine grafische Benutzeroberfläche für die differenzierten Kontorichtlinien. Dieser neue Dialog ist im Active Directory-Verwaltungscenter untergebracht und vereinfacht die FGPP-Verwaltung für alle Administratoren.

Weitere Informationen zu fein abgestimmten Kennwortrichtlinien finden Sie unter [Schrittweise Anleitung für die Konfiguration abgestimmter Kennwort- und Kontosperrungsrichtlinien für AD DS (Windows Server 2008 R2)](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770842(v=ws.10)).

## <a name="active-directory-administrative-center-windows-powershell-history-viewer"></a>Active Directory-Verwaltungscenter - PowerShell-Verlaufsanzeige

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_HistoryViewer.png)

Mit Windows Server 2008 R2 wurde das Active Directory-Verwaltungscenter eingeführt, welches das ältere, seit Windows 2000 enthaltene, Active Directory-Benutzer und -Computer-Snap-In ersetzt. Das Active Directory-Verwaltungscenter bietet eine grafische Verwaltungsoberfläche für das damals noch neue Active Directory-Modul für Windows PowerShell.

Das Active Directory-Modul enthält jedoch über einhundert Cmdlets, was zu einer steilen Lernkurve für neue Administratoren führt. Da Windows PowerShell jedoch eng mit der Windows-Verwaltungsstrategie integriert ist, enthält das Active Directory-Verwaltungscenter nun eine Ansicht, mit der Sie die Cmdlet-Ausführung in der grafischen Benutzeroberfläche beobachten können. Sie können mit einer einfach zu bedienenden Oberfläche suchen, kopieren, den Verlauf löschen und Notizen hinzufügen. Administratoren können die grafische Benutzeroberfläche zum Erstellen und Ändern von Objekten verwenden und diese anschließend in der Verlaufsanzeige betrachten, um sich mit Windows PowerShell-Skripts vertraut zu machen und die Beispiele zu modifizieren.

## <a name="ad-replication-windows-powershell"></a>AD-Replikation mit Windows PowerShell

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_PSNewADReplSite.png)

Mit Windows Server 2012 wurde das Active Directory Windows PowerShell-Modul um zusätzliche Active Directory-Replikations-Cmdlets erweitert. Mit diesen Cmdlets können neue oder existierende Standorte, Subnetze, Verbindungen, Standortverknüpfungen und Brücken konfiguriert werden. Außerdem geben die Cmdlets Informationen zu Active Directory-Replikations-Metadaten, Replikationsstatus, Warteschlangen und Versionsvektoren zurück. Die Einführung dieser Replikations-Cmdlets - gemeinsam mit den Bereitstellungs- und anderen AD DS-Cmdlets - ermöglichen die Verwaltung von Gesamtstrukturen allein mithilfe von Windows PowerShell. Auf diese Weise erhalten Administratoren neue Möglichkeiten zur Bereitstellung und Verwaltung von Windows Server 2012 ohne grafische Benutzeroberfläche, wodurch wiederum Angriffsoberfläche und Wartungsanforderungen gesenkt werden. Dies ist besonders wichtig bei der Bereitstellung von Servern in Hochsicherheitsnetzwerken wie z. B. Secret Internet Protocol Router (SIPR) und Unternehmens-DMZs.

Weitere Informationen zur AD DS-Standorttopologie und -Replikation finden Sie unter [Windows Server Technical Reference](/previous-versions/windows/it-pro/windows-server-2003/cc739127(v=ws.10)).

## <a name="rid-management-and-issuance-improvements"></a>Verbesserungen bei der RID-Ausstellung und -Verwaltung

Mit Windows 2000 Active Directory wurde der RID-Master eingeführt, der Pools mit relativen Bezeichnern an Domänencontroller ausstellt, um Sicherheits-IDs (SIDs) für Vertrauensnehmer wie z. B. Benutzer, Gruppen und Computer zu generieren.  Dieser globale RID-Raum ist standardmäßig auf 2<sup>30</sup> (bzw. 1.073.741.823) SIDs pro Domäne begrenzt. SIDs können nicht in den Pool zurückgegeben oder erneut ausgestellt werden. Mit der Zeit können die SIDs in großen Domänen knapp werden oder durch versehentliche massenhafte Ausstellung erschöpft werden.

Windows Server 2012 behandelt zahlreiche Probleme bei der RID-Ausstellung und -Verwaltung, die von Kunden und dem Microsoft-Kundensupport seit der Einführung der ersten Active Directory-Domänen im Jahr 1999 entdeckt wurden. Dazu gehören:

- Regelmäßige RID-Verbrauchswarnungen werden in das Ereignisprotokoll geschrieben
- Ereignisse werden geschrieben, wenn ein Administrator einen RID-Pool ungültig macht
- Für die RID-Blockgröße wird nun eine Obergrenze erzwungen
- Künstliche RID-Obergrenzen werden erzwungen und protokolliert, wenn der globale RID-Raum knapp wird. Auf diese Weise können Administratoren reagieren, bevor der globale Raum erschöpft ist
- Der globale RID-Raum kann nun um ein Bit erhöht und somit auf 2<sup>31</sup> (2.147.483.648 SIDs) vergrößert werden

Weitere Informationen zu RIDs und dem RID-Master finden Sie unter [How Security Identifiers Work](/previous-versions/windows/it-pro/windows-server-2003/cc778824(v=ws.10)).

## <a name="ad-ds-role-deployment-and-management-architecture"></a>AD DS-Rollenbereitstellung und Verwaltungsarchitektur

Server-Manager und ADDSDeployment Windows PowerShell verwenden die folgenden Kernassemblys für die Bereitstellung und Verwaltung von AD DS-Rollen:

- Microsoft.ADroles.Aspects.dll
- Microsoft.ADroles.Instrumentation.dll
- Microsoft.ADRoles.ServerManager.Common.dll
- Microsoft.ADRoles.UI.Common.dll
- Microsoft.DirectoryServices.Deployment.Types.dll
- Microsoft.DirectoryServices.ServerManager.dll
- Addsdeployment.psm1
- Addsdeployment.psd1

Beide Komponenten verwenden Windows PowerShell und dessen Remote-Aufrufbefehl für die Remote-Rolleninstallation und -Konfiguration.

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_DepDLLs.png)

In Windows Server 2012 wurden außerdem zahlreiche frühere Heraufstufungsoperationen aus LSASS.EXE umgestaltet, als Teil von:

- DS-Rollenserverdienst (DsRoleSvc)
- DSRoleSvc.dll (geladen vom DsRoleSvc-Dienst)

Dieser Dienst muss installiert sein und laufen, um virtuelle Domänencontroller herauf- oder herabstufen oder klonen zu können. Bei der AD DS-Rolleninstallation wird dieser Dienst installiert und standardmäßig für manuellen Start konfiguriert. Deaktivieren Sie diesen Dienst nicht.

## <a name="adprep-and-prerequisite-checking-architecture"></a>ADPrep- und Voraussetzungsprüfungsarchitektur

Adprep muss nun nicht mehr auf dem Schemamaster ausgeführt werden. Adprep kann remote auf einem beliebigen Computer unter Windows Server 2008 x64 oder einer neueren Version ausgeführt werden.

> [!NOTE]
> Adprep verwendet LDAP zum Importieren von Schxx.ldf-Dateien und verbindet sich nicht automatisch neu, wenn die Verbindung zum Schemamaster während des Importvorgangs abbricht. Der Schemamaster wird als Teil dieses Importvorgangs in einen bestimmten Modus versetzt, und die automatische Verbindungswiederherstellung wird deaktiviert, da die LDAP-Verbindung andernfalls nicht im richtigen Modus wiederhergestellt würde. In diesem Fall würde das Schema nicht korrekt aktualisiert werden.

Die Voraussetzungsprüfung stellt sicher, dass bestimmte Bedingungen erfüllt sind. Diese Bedingungen sind Voraussetzung für die erfolgreiche AD DS-Installation. Ein Teil dieser Bedingungen kann direkt korrigiert werden, bevor die Installation fortgesetzt wird. Außerdem wird erkannt, wenn eine Gesamtstruktur oder Domäne nicht vorbereitet wurde, und der Adprep-Bereitstellungscode wird automatisch ausgeführt.

### <a name="adprep-executables-dlls-ldfs-files"></a>Ausführbare ADPrep-Dateien, DLLs, LDFs, Dateien

- ADprep.dll
- Ldifde.dll
- Csvde.dll
- Sch14.ldf - Sch56.ldf
- Schupgrade.cat
- *dcpromo.csv

Der zuvor in ADprep.exe untergebrachte AD-Vorbereitungscode ist nun in adprep.dll enthalten. Auf diese Weise können sowohl ADPrep.exe als auch das ADDSDeployment Windows PowerShell-Modul die Bibliothek für dieselben Aufgaben verwenden und haben denselben Funktionsumfang. Adprep.exe ist auf dem Installationsmedium enthalten, wird jedoch von den automatischen Prozessen nicht direkt aufgerufen. Nur Administratoren führen Adprep.exe manuell aus. Adprep.exe kann nur unter Windows Server 2008 x64 und neueren Betriebssystemen ausgeführt werden. Ldifde.exe und csvde.exe wurden ebenfalls als DLLs umgestaltet, die vom Vorbereitungsprozess geladen werden. Die Schemaerweiterung verwendet weiterhin die LDF-Dateien mit geprüften Signaturen, wie in früheren Betriebssystemversionen.

![vereinfachte Verwaltung](media/AD-DS-Simplified-Administration/ADDS_SMI_TR_AdprepDLLs.png)

> [!IMPORTANT]
> Es existiert kein 32-Bit Adprep32.exe-Tool für Windows Server 2012. Sie benötigen mindestens einen Computer unter Windows Server 2008 x64, Windows Server 2008 R2 oder Windows Server 2012, der als Domänencontroller, Mitgliedsserver oder in einer Arbeitsgruppe läuft, um Gesamtstruktur und Domäne vorbereiten zu können. Adprep.exe läuft nicht unter Windows Server 2003 x64.

## <a name="prerequisite-checking"></a><a name="BKMK_PrereuisiteChecking"></a>Voraussetzungsprüfung

Das in den verwalteten Code von ADDSDeployment Windows PowerShell integrierte System zur Voraussetzungsprüfung funktioniert je nach Operation auf unterschiedliche Arten. Die folgenden Tabellen beschreiben die einzelnen Tests, deren jeweilige Anwendungsfälle und erläutern, was und wie genau geprüft wird. Diese Tabellen sind hilfreich, wenn Probleme auftreten, bei denen die Prüfung fehlschlägt und die Fehlermeldung nicht zur Problembehandlung ausreicht.

Diese Tests schreiben in den Ereignisprotokollkanal **Verzeichnisdienste-Bereitstellung** unter der Aufgabenkategorie **Core**, immer mit der Ereignis-ID **103**.

### <a name="prerequisite-windows-powershell"></a>Windows PowerShell - Voraussetzungen

Für jedes Domänencontroller-Bereitstellungs-Cmdlet existiert ein ADDSDeployment Windows PowerShell-Cmdlet. Die Cmdlets haben sehr ähnliche Argumente wie ihre jeweiligen Gegenstücke.

- Test-ADDSDomainControllerInstallation
- Test-ADDSDomainControllerUninstallation
- Test-ADDSDomainInstallation
- Test-ADDSForestInstallation
- Test-ADDSReadOnlyDomainControllerAccountCreation

Diese Cmdlets müssen normalerweise nicht ausgeführt werden, da sie standardmäßig automatisch von den Bereitstellungs-Cmdlets aufgerufen werden.

#### <a name="prerequisite-tests"></a><a name="BKMK_ADDSInstallPrerequisiteTests"></a>Voraussetzungsprüfungen

| Prüfungsname | Protokolle<p>used | Erklärung und Hinweise |
|--|--|--|
| VerifyAdminTrusted<p>ForDelegationProvider | LDAP | Prüft, ob Sie die Berechtigung "Ermöglichen, dass Computer- und Benutzerkonten für Delegierungszwecke vertraut wird" (SeEnableDelegationPrivilege) auf dem existierenden Partner-Domänencontroller haben. Hierfür wird Zugriff auf Ihr konstruiertes tokenGroups-Attribut benötigt.<p>Wird nicht verwendet, wenn ein Microsoft Windows Server 2003-Domänencontroller kontaktier wird. Sie müssen diese Berechtigung vor der Heraufstufung manuell bestätigen |
| VerifyADPrep<p>Voraussetzungen (Gesamtstruktur) | LDAP | Sucht und kontaktiert den Schemamaster mithilfe des rootDSE namingContexts-Attributs und dem Schema-Namenskontext-Attribut fsmoRoleOwner. Ermittelt, welche Vorbereitungsoperationen (forestprep, domainprep oder rodcprep) für die AD DS-Installation benötigt werden. Prüft, ob objectVersion für das Schema wie erwartet ist und ob eine weitere Erweiterung benötigt wird. |
| VerifyADPrep<p>Voraussetzungen (Domäne und RODC) | LDAP | Sucht und kontaktiert den Infrastruktur-Master mithilfe des rootDSE namingContexts-Attributs und dem Infrastrukturcontainer-Attribut fsmoRoleOwner. Im Fall einer RODC-Installation wird bei dieser Prüfung der Domänennamenmaster gesucht und sichergestellt, dass dieser online ist. |
| CheckGroup<p>Mitgliedschaft | LDAP,<p>RPC über SMB (LSARPC) | Prüft, ob der Benutzer Mitglied der Gruppen Domänen-Admins bzw. Unternehmens-Admins ist, je nach Operation (DA beim Hinzufügen oder Herabstufen eines Domänencontrollers, UA beim Hinzufügen oder Entfernen einer Domäne) |
| CheckForestPrep<p>GroupMembership | LDAP,<p>RPC über SMB (LSARPC) | Prüft, ob der Benutzer Mitglied der Gruppen Schema-Admins und Unternehmens-Admins ist und ob er die Berechtigung zur Verwaltung der Überwachungs- und Sicherheitsereignisprotokolle (SesScurityPrivilege) auf den existierenden Domänencontrollern hat |
| CheckDomainPrep<p>GroupMembership | LDAP,<p>RPC über SMB (LSARPC) | Prüft, ob der Benutzer Mitglied der Gruppe Domänen-Admins ist und ob er die Berechtigung zur Verwaltung der Überwachungs- und Sicherheitsereignisprotokolle (SesScurityPrivilege) auf den existierenden Domänencontrollern hat |
| CheckRODCPrep<p>GroupMembership | LDAP,<p>RPC über SMB (LSARPC) | Prüft, ob der Benutzer Mitglied der Gruppe Unternehmens-Admins ist und ob er die Berechtigung zur Verwaltung der Überwachungs- und Sicherheitsereignisprotokolle (SesScurityPrivilege) auf den existierenden Domänencontrollern hat |
| VerifyInitSync<p>AfterReboot | LDAP | Prüft, ob der Schemamaster seit dem Neustart mindestens einmal repliziert wurde, indem ein Dummywert für das rootDSE-Attribut becomeSchemaMaster gesetzt wird |
| VerifySFUHotFix<p>Übernommen | LDAP | Prüft, ob das existierende Gesamtstruktur-Schema bekannte problematische SFU2-Erweiterungen für das UID-Attribut mit OID 1.2.840.113556.1.4.7000.187.102 enthält<p>([https://support.microsoft.com/kb/821732](https://support.microsoft.com/kb/821732)) |
| VerifyExchange<p>SchemaFixed | LDAP, WMI, DCOM, RPC | Überprüfen Sie, ob das vorhandene Gesamtstruktur Schema noch keine Problem Austausch 2000-Erweiterungen ms-Exch-Assistant-Name, ms-Exch-LabeledURI und MS-Exch-House-Identifier () enthält. [https://support.microsoft.com/kb/314649](https://support.microsoft.com/kb/314649) |
| VerifyWin2KSchema<p>Konsistenz | LDAP | Prüft, ob das existierende Gesamtstruktur-Schema konsistente (nicht auf falsche Weise extern modifizierte) Core-Attribute und Klassen enthält. |
| DCPromo | DRSR über RPC,<p>LDAP,<p>DNS<p>RPC über SMB (SAMR) | Prüft die an den Heraufstufungscode übergebene Befehlszeilensyntax und testet die Heraufstufung. Prüft, ob die Gesamtstruktur bzw. Domäne bereits existiert, falls diese neu erstellt werden. |
| VerifyOutbound<p>ReplicationEnabled | LDAP, DRSR über SMB, RPC über SMB (LSARPC) | Prüft, ob die Replikation in ausgehender Richtund in dem als Replikationspartner angegebenen Domänencontroller aktiviert ist. Dazu wird das Optionsattribut des NTDS-Einstellungsobjekts für NTDSDSA_OPT_DISABLE_OUTBOUND_REPL (0x00000004) ausgelesen |
| VerifyMachineAdmin<p>Kennwort | DRSR über RPC,<p>LDAP,<p>DNS<p>RPC über SMB (SAMR) | Prüft, ob das für DSRM eingestellte Wiederherstellungskennwort für den abgesicherten Modus die Komplexitätsanforderungen erfüllt. |
| VerifySafeModePassword | *N/V* | Prüft, ob das lokale Administratorkennwort die Komplexitätsanforderungen der Computer-Sicherheitsrichtlinie erfüllt. |
