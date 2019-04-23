---
title: Anmeldeinformationen-Prozesse in der Windows-Authentifizierung
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: security-windows-auth
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 48c60816-fb8b-447c-9c8e-800c2e05b14f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 52d50a1bb6bfbe9d35146f362a2a5184df0a6504
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839861"
---
# <a name="credentials-processes-in-windows-authentication"></a>Anmeldeinformationen-Prozesse in der Windows-Authentifizierung

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Referenzthema für IT-Experten wird beschrieben, wie Windows-Authentifizierung für Anmeldeinformationen verarbeitet.

Verwaltung von Windows-Anmeldeinformationen werden mit dem das Betriebssystem die Anmeldeinformationen für den Dienst oder der Benutzer empfängt und sichert diese Informationen für die zukünftige Darstellung für das Ziel authentifizieren. Im Fall von einem Computer einer Domäne ist das Ziel authentifizierende der Domänencontroller. Bei der Authentifizierung verwendeten Anmeldeinformationen sind digitale Dokumente, die die Identität des Benutzers in eine Form von Authentizität, z. B. ein Zertifikat, ein Kennwort oder eine PIN für die Machbarkeitsstudie zuordnen.

Standardmäßig werden die Windows-Anmeldeinformationen für die Datenbank der Sicherheitskontenverwaltung (Security Accounts Manager, SAM) auf dem lokalen Computer oder für Active Directory auf einem Computer einer Domäne angehört, über den Winlogon-Dienst überprüft. Anmeldeinformationen werden durch Eingabe des Benutzers gesammelt, wenn Sie auf der Benutzeroberfläche für Anmeldung oder programmgesteuert über die Anwendungsprogrammierschnittstelle (API) zum Authentifizieren Ziel angezeigt werden.

Informationen zur lokalen Sicherheit befindet sich in der Registrierung unter **HKEY_LOCAL_MACHINE\SECURITY**. Gespeicherter Informationen enthält Richtlinieneinstellungen, Standardwerte für die Sicherheit und Kontoinformationen, wie z. B. die zwischengespeicherten Anmeldeinformationen. Eine Kopie der SAM-Datenbank wird auch hier gespeichert werden, obwohl es schreibgeschützt ist.

Das folgende Diagramm zeigt die Komponenten, die erforderlich sind und die Pfade, Anmeldeinformationen zum Authentifizieren des Benutzers oder Prozesses für eine erfolgreiche Anmeldung durch das System ergreifen.

![Diagramm zeigt die Komponenten, die erforderlich sind und die Pfade, die Anmeldeinformationen werden durch das System zum Authentifizieren des Benutzers oder Prozesses für eine erfolgreiche Anmeldung.](../media/credentials-processes-in-windows-authentication/AuthN_LSA_Architecture_Client.gif)

Die folgende Tabelle beschreibt die einzelnen Komponenten, die Verwaltung von Anmeldeinformationen zum Zeitpunkt der Anmeldung bei der Authentifizierung.

**Authentication-Komponenten für alle Systeme**

|Component|Beschreibung|
|-------|--------|
|Anmelden des Benutzers|Winlogon.exe wird der ausführbaren Datei, die für die Verwaltung von sicheren Benutzerinteraktionen verantwortlich. Der Winlogon-Dienst initiiert des Anmeldevorgangs für Windows-Betriebssysteme, indem Sie die gesammelten durch den Benutzer auf dem sicheren Desktop (Logon-UI), Local Security Authority (LSA) über Secur32.dll Anmeldeinformationen übergeben.|
|Anwendungen|Anwendung oder Dienst-Anmeldungen, die nicht interaktive Anmeldung erfordern. Die meisten Prozesse, die vom Benutzer initiiert wurden, die mithilfe der Secur32.dll, wohingegen Prozesse, die beim Start, z. B. Dienste initiiert im Kernelmodus ausgeführt werden, mithilfe von Ksecdd.sys im Benutzermodus ausgeführt werden.<br /><br />Weitere Informationen zu Benutzer- und Kernelmodus finden Sie in diesem Thema Anwendungen "und" User Mode "oder" Dienste "und" Kernel-Modus.|
|Secur32.dll|Die multiple Authentifizierungsanbieter, die die Grundlage für den Authentifizierungsprozess zu bilden.|
|Lsasrv.dll|Der LSA-Server-Dienst, der sowohl Sicherheitsrichtlinien erzwingt und als Sicherheitspaket-Manager für die lokale Sicherheitsautorität fungiert. Die LSA enthält die Negotiate-Funktion, wählt das NTLM oder Kerberos-Protokoll nach der Bestimmung, welches Protokoll erfolgreich ist.|
|Security Support Provider|Eine Reihe von Anbietern, die eine oder mehrere Authentifizierungsprotokolle einzeln aufgerufen werden können. Der Standardsatz von Anbietern kann mit jeder Version des Windows-Betriebssystems ändern und benutzerdefinierte Anbieter geschrieben werden können.|
|Netlogon.dll|Die Dienste, die der Anmeldedienst führt lauten wie folgt aus:<br /><br />– Sicherer Kanal (nicht zu verwechseln mit Schannel) des Computers zu einem Domänencontroller verwaltet.<br />-Übergibt die Anmeldeinformationen des Benutzers über einen sicheren Kanal an den Domänencontroller, und die Domäne Sicherheits-IDs (SIDs) und die Benutzerrechte für den Benutzer zurückgegeben.<br />-Dienstressourceneinträge in das Domain Name System (DNS) und DNS zum Auflösen von Namen in der IP (Internet Protocol)-Adressen der Domänencontroller verwendet.<br />-Das Replikationsprotokoll basierend auf einen Remoteprozeduraufruf (RPC) für die Synchronisierung der primäre Domänencontroller (PDCs) und Sicherungsdomänencontroller (BDCs) implementiert.|
|Samsrv.dll|Den Security Accounts Manager (SAM), der lokalen Sicherheitskonten gespeichert sind, erzwingt lokal gespeicherte Richtlinien und -APIs unterstützt.|
|Registrierung|Die Registrierung enthält eine Kopie der SAM-Datenbank, lokaler sicherheitsrichtlinieneinstellungen, Standardwerte für die Sicherheit und Kontoinformationen, die nur für das System zugänglich sind.|

Dieses Thema enthält die folgenden Abschnitte:

-   [Eingabe der Anmeldeinformationen für die Benutzeranmeldung](#BKMK_CrentialInputForUserLogon)

-   [Eingabe von Anmeldeinformationen für die Anwendung und -Anmeldung](#BKMK_CredentialInputForApplicationAndServiceLogon)

-   [Lokale Sicherheitsautorität](#BKMK_LSA)

-   [Zwischengespeicherte Anmeldeinformationen und Validierung](#BKMK_CachedCredentialsAndValidation)

-   [Speichern von Anmeldeinformationen und Validierung](#BKMK_CredentialStorageAndValidation)

-   [SAM-Datenbank](#BKMK_SAM)

-   [Lokale Domänen und vertrauenswürdigen Domänen](#BKMK_LocalDomainsAndTrustedDomains)

-   [Zertifikate im Windows-Authentifizierung](#BKMK_CertificatesInWindowsAuthentication)

## <a name="BKMK_CrentialInputForUserLogon"></a>Eingabe der Anmeldeinformationen für die Benutzeranmeldung
In Windows Server 2008 und Windows Vista wurde die Graphical Identification and Authentication (GINA)-Architektur mit einem Credential Provider-Modell, ersetzt, was es möglich, verschiedene Anmeldetypen mithilfe von Logon-Kacheln aufzulisten. Beide Modelle werden nachfolgend beschrieben.

**GINA-Architektur**

Die Architektur Graphical Identification and Authentication (GINA) gilt für die Windows Server 2003, Microsoft Windows 2000 Server, Windows XP und Windows 2000 Professional-Betriebssysteme. In diesen Systemen erstellt jede interaktive anmeldesitzung eine separate Instanz des Winlogon-Diensts. Die GINA-Architektur ist in den Prozessbereich von Windows-Anmeldung verwendet, empfängt und verarbeitet die Anmeldeinformationen und nimmt Aufrufe an die authentifizierungsschnittstellen durch LSALogonUser.

Die Instanzen der Windows-Anmeldung für eine interaktive Anmeldung, die in Sitzung 0 ausgeführt werden soll. Systemdienste für Sitzung 0-Hosts und andere wichtige Prozesse, einschließlich des Prozesses (Local Security Authority, LSA).

Das folgende Diagramm zeigt den anmeldeinformationsprozess für Windows Server 2003, Microsoft Windows 2000 Server, Windows XP und Microsoft Windows 2000 Professional.

![Das Diagramm zeigt den anmeldeinformationsprozess für Windows Server 2003, Microsoft Windows 2000 Server, Windows XP und Microsoft Windows 2000 Professional](../media/credentials-processes-in-windows-authentication/AuthN_GINA_Architecture.gif)

**Anmeldeinformationsanbieter-Architektur**

Die Anmeldeinformationsanbieter-Architektur gilt den Versionen der **gilt für** Liste am Anfang dieses Themas. In diesen Systemen wird mithilfe von Anmeldeinformationsanbietern Eingabearchitektur für die Anmeldeinformationen zu einem erweiterbaren Entwurf geändert. Diese Anbieter werden durch die anderen Kacheln auf dem sicheren Desktop dargestellt, die eine beliebige Anzahl von Anmeldeszenarios - verschiedene Konten für die derselbe Benutzer und die unterschiedlichen Authentifizierungsmethoden, z. B. Kennwort, Smartcard und Biometrie zulassen.

Mit die Anmeldeinformationsanbieter-Architektur beginnt Winlogon immer Logon-Benutzeroberfläche, nachdem es ein secure Attention Sequence-Ereignis empfängt. Anmeldebenutzeroberfläche fragt jeden Anmeldeinformationsanbieter für die Anzahl der verschiedene Arten von Anmeldeinformationen, die den Anbieter so konfiguriert ist, zum Auflisten von. Anmeldeinformationsanbieter haben die Möglichkeit einer dieser Kacheln als Standard angeben. Nachdem Sie alle Anbieter ihre Kacheln aufgelistet haben, zeigt sie an Logon-Benutzeroberfläche für den Benutzer. Der Benutzer interagiert mit eine Kachel, um ihre Anmeldeinformationen angeben. Anmeldebenutzeroberfläche sendet diese Anmeldeinformationen für die Authentifizierung.

Anmeldeinformationsanbieter sind keine Mechanismen zum erzwingen. Sie dienen zum Erfassen und Anmeldeinformationen zu serialisieren. Die lokale Sicherheitsautorität und Authentifizierung Pakete Erzwingen der Sicherheit.

Anmeldeinformationsanbieter sind auf dem Computer registriert und sind für Folgendes zuständig:

-   Beschreiben die Anmeldeinformationen für die Authentifizierung erforderlich.

-   Behandeln von Kommunikation und Logik in die externe Authentifizierung Behörden.

-   Verpacken von Anmeldeinformationen für die interaktive und netzwerkanmeldung.

Verpacken von Anmeldeinformationen für die interaktive und netzwerkanmeldung umfasst der Prozess der Serialisierung. Durch das Serialisieren von Anmeldeinformationen können mehrere Kacheln der Anmeldung auf die Anmeldebenutzeroberfläche angezeigt werden. Aus diesem Grund kann die Organisation der Logon-Anzeige, z. B. Benutzer, die Zielsysteme für die Anmeldung, die vor der Anmeldung Zugriff auf das Netzwerk und die Arbeitsstation sperren/entsperren Richtlinien – durch die Verwendung von benutzerdefinierten Anmeldeinformationsanbieter steuern. Mehrere Anmeldeinformationsanbieter können gleichzeitig auf demselben Computer vorhanden sein.

Einmaliges Anmelden (SSO)-Anbieter können als eine standard-Anmeldeinformationsanbieter oder als Pre-Logon-Access Provider entwickelt werden.

Jede Version von Windows enthält ein Standard-Anmeldeinformationsanbieter und einen Standardwert Pre-Logon-Access Provider (PLAP), auch bekannt als der SSO-Anbieter. Der SSO-Anbieter ermöglicht Benutzern das Herstellen eine Verbindung mit einem Netzwerk vor der Anmeldung auf dem lokalen Computer. Wenn dieser Anbieter implementiert ist, ist der Anbieter nicht aufgezählt werden Kacheln auf der Benutzeroberfläche für Anmeldung.

Ein SSO-Anbieter ist in den folgenden Szenarien verwendet werden soll:

-   **Netzwerkanmeldung Authentifizierung und -Computer werden durch verschiedene Anmeldeinformationsanbieter behandelt.** Abweichungen in diesem Szenario:

    -   Ein Benutzer hat die Möglichkeit der Verbindung mit einem Netzwerk, z. B. eine Verbindung herstellen, um ein virtuelles privates Netzwerk (VPN), vor der Anmeldung auf dem Computer, aber es ist nicht erforderlich, diese Verbindung herstellen.

    -   Zum Abrufen von Informationen, die während der interaktiven Authentifizierung auf dem lokalen Computer verwendet, ist die Netzwerkauthentifizierung erforderlich.

    -   Mehrere Netzwerk-Authentifizierungen werden gefolgt von einem anderen Szenarien. Beispielsweise ein Benutzer authentifiziert sich gegenüber einem Internetdienstanbieter (ISP) authentifiziert sich mit einem VPN und Anmeldeinformationen für ihr Benutzerkonto wird lokal zum Anmelden verwendet.

    -   Zwischengespeicherte Anmeldeinformationen sind deaktiviert, und eine RAS-Dienste-Verbindung über VPN muss vor der lokalen Anmeldung zur Authentifizierung des Benutzers.

    -   Ein Domänenbenutzer verfügt nicht über ein lokales Konto auf eine Domäne eingebundenen Computer eingerichtet und muss eine RAS-Dienste-Verbindung über VPN-Verbindung vor dem Abschluss der interaktiven Anmeldung herstellen.

-   **Von der gleichen Anmeldeinformationsanbieter netzwerkanmeldung Authentifizierung und -Computer behandelt.** In diesem Szenario muss der Benutzer eine Verbindung mit dem Netzwerk vor der Anmeldung am Computer herstellen.

**Logon-Kachel-enumeration**

Der Anmeldeinformationsanbieter listet Logon-Kacheln in den folgenden Fällen:

-   Für diese Betriebssysteme, die festgelegt werden, der **gilt für** Liste am Anfang dieses Themas.

-   Der Anmeldeinformationsanbieter listet auf die Kacheln für die Anmeldung an der Arbeitsstation. Der Anmeldeinformationsanbieter serialisiert in der Regel die Anmeldeinformationen für die Authentifizierung bei der lokalen Sicherheitsinstanz. Dieser Vorgang wird für jeden Benutzer und zu bestimmten Zielsystemen jedes Benutzers angezeigt.

-   Die Architektur für Anmeldung und Authentifizierung kann Benutzer Kacheln, die durch den der Anmeldeinformationsanbieter aufgezählt verwenden, um eine Arbeitsstation zu entsperren. In der Regel der derzeit angemeldete Benutzer wird die Kachel "Standard", aber wenn mehr als ein Benutzer angemeldet ist, werden zahlreiche Kacheln angezeigt.

-   Der Anmeldeinformationsanbieter listet Kacheln als Reaktion auf eine benutzeranforderung an ihr Kennwort oder andere private Informationen, wie z. B. eine PIN zu ändern. Der derzeit angemeldete Benutzer ist in der Regel die Kachel "Standard". Wenn mehr als ein Benutzer angemeldet ist, werden jedoch zahlreiche Kacheln angezeigt.

-   Der Anmeldeinformationsanbieter listet Kacheln, die basierend auf den serialisierten Anmeldeinformationen für die Authentifizierung auf Remotecomputern verwendet werden. UI-Anmeldeinformationen verwendet nicht die gleiche Instanz des Anbieters als die Benutzeroberfläche für Anmeldung, Entsperren der Arbeitsstation oder Kennwort ändern. Aus diesem Grund kann keine Zustandsinformationen im Anbieter zwischen Instanzen von Anmeldeinformationen-Benutzeroberfläche verwaltet werden. Diese Struktur ergibt eine Kachel für die einzelnen Remotecomputer-Anmeldung, vorausgesetzt, dass die Anmeldeinformationen ordnungsgemäß serialisiert wurden. Dieses Szenario wird auch in der User Account Control (UAC) verwendet und kann zu verhindern, dass nicht autorisierte Änderungen an einem Computer durch den Benutzer-Berechtigung oder die ein Administratorkennwort aufzufordern, bevor die Übergabe von Aktionen, die Betrieb des Computers beeinträchtigen können nützlich sein oder könnte, die Einstellungen, die andere Benutzer des Computers auswirken ändern.

Das folgende Diagramm zeigt den anmeldeinformationsprozess für die Betriebssysteme, die festgelegt werden, der **gilt für** Liste am Anfang dieses Themas.

![Diagramm den anmeldeinformationsprozess für die Betriebssysteme, die festgelegt werden zeigt, der ** gilt für ** Liste am Anfang dieses Themas](../media/credentials-processes-in-windows-authentication/AuthN_CredMan_CredProv.gif)

## <a name="BKMK_CredentialInputForApplicationAndServiceLogon"></a>Eingabe von Anmeldeinformationen für die Anwendung und -Anmeldung
Windows-Authentifizierung dient zur Verwaltung von Anmeldeinformationen für Anwendungen oder Dienste, die keine Benutzerinteraktion erfordern. Anwendungen im Benutzermodus sind im Hinblick auf welche Ressourcen sie Zugriff haben, während Dienste uneingeschränkten Zugriff auf den Systemspeicher und externen Geräten verfügen können beschränkt.

Systemdienste und auf Transportebene Anwendungen Zugriff auf ein Security Support Provider (SSP) über die Security Support Provider Interface (SSPI) in Windows, die Funktionen, die zum Aufzählen der auf einem System verfügbaren Sicherheitspakete bereitstellt werden, Auswählen einer Paket, und verwenden das Paket um eine authentifizierte Verbindung zu erhalten.

Wenn eine Client/Server-Verbindung authentifiziert wird:

-   Die Anwendung auf der Clientseite der Verbindung und sendet Sie Anmeldeinformationen an den Server mithilfe der SSPI-Funktion `InitializeSecurityContext (General)`.

-   Die Anwendung auf dem Server, der die Verbindung mit der SSPI-Funktion reagiert `AcceptSecurityContext (General)`.

-   Die SSPI-Funktionen `InitializeSecurityContext (General)` und `AcceptSecurityContext (General)` werden wiederholt, bis alle erforderlichen Authentifizierungsinformationen Nachrichten ausgetauscht wurden, um entweder gelingen oder Fehlschlagen der Authentifizierung.

-   Nachdem die Verbindung authentifiziert wurde, verwendet die LSA auf dem Server Informationen vom Client, um dem Sicherheitskontext zu erstellen, der was ein Zugriffstoken enthält.

-   Der Server kann dann die SSPI-Funktion aufrufen `ImpersonateSecurityContext` das Zugriffstoken an einen Thread Identitätswechsel für den Dienst angefügt.

**Anwendungen und User-Modus**

Benutzermodus in Windows besteht aus zwei Systemen, die mit der Übergabe von e/a-Anforderungen an die entsprechenden Kernelmodustreiber: die Umgebung, die Anwendungen für viele verschiedene Betriebssysteme ausgeführt wird, und die ganzzahlige, operiert spezifische Funktionen für das Umgebungssystem.

Das ganzzahlige System system'specific Betriebsfunktionen für das Umgebungssystem verwaltet und besteht aus einem Systemprozess "Security" (die LSA), eine Workstation-Dienst und einen Server-Dienst. Systemprozess Sicherheit befasst sich mit Sicherheitstoken, gewährt oder verweigert Zugriffsberechtigungen für Benutzerkonten, die anhand der Berechtigungen für Buildressourcen, verarbeitet anmeldeanforderungen und initiiert die Anmeldeauthentifizierung und bestimmt, welche Ressourcen das Betriebssystem die Anforderungen zu überwachen.

Anwendungen können im Benutzermodus ausgeführt werden, kann die Anwendung als Prinzipal, einschließlich der im Sicherheitskontext des lokalen Systemkonto (SYSTEM) ausführen. Anwendungen können auch im Kernelmodus ausgeführt, kann die Anwendung im Sicherheitskontext des lokalen Systemkonto (SYSTEM) ausführen.

SSPI ist verfügbar, über das Secur32.dll-Modul, das eine API zum Abrufen von integrierte Sicherheitsdienste für Authentifizierung, Nachrichtenintegrität und Datenschutz von Nachrichten verwendet wird. Es bietet eine Abstraktionsschicht zwischen Protokollen auf Anwendungsebene und Sicherheitsprotokolle. Da verschiedene Anwendungen verschiedene Möglichkeiten zum Authentifizieren von Benutzern und verschiedene Möglichkeiten zum Verschlüsseln von Daten erfordern bei der Übertragung über ein Netzwerk oder identifizieren, bietet SSPI eine Möglichkeit, die Dynamic Link Libraries (DLLs) zugreifen, die verschiedene Authentifizierungsoptionen zu enthalten und kryptografische Funktionen. Diese DLLs werden als Security Support Provider (SSP) bezeichnet.

Verwaltete Dienstkonten und virtuellen Konten wurden eingeführt, in Windows Server 2008 R2 und Windows 7 wichtigen Anwendungen, wie z. B. Microsoft SQL Server und Internet Information Services (IIS), die Isolierung der eigenen Domänenkonten zu ermöglichen während beseitigen, dass ein Administrator den Dienstprinzipalnamen (SPN) manuell zu verwalten und die Anmeldeinformationen für diese Konten. Weitere Informationen zu diesen Features und ihrer Rolle bei der Authentifizierung finden Sie unter [verwalteten Dienst Konten Dokumentation für Windows 7 und Windows Server 2008 R2](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx) und [Gruppe verwaltete Dienstkonten: Übersicht](../group-managed-service-accounts/group-managed-service-accounts-overview.md).

**Dienste und Kernel-Modus**

Obwohl die meisten Windows-Anwendungen im Sicherheitskontext des Benutzers, die sie gestartet wird ausgeführt, gilt dies nicht der Dienste. Viele Windows-Dienste, z.B. Netzwerk- und Druckdienste, werden vom Dienstcontroller gestartet, wenn der Benutzer den Computer startet. Diese Dienste werden möglicherweise als lokaler Dienst oder lokales System ausgeführt und können weiterhin ausgeführt, nachdem der letzte Benutzer abgemeldet.

> [!NOTE]
> Dienste, die normalerweise in den Sicherheitskontexten, bekannt als lokales Systemkonto (SYSTEM), Netzwerkdienst oder lokaler Dienst ausgeführt werden.  Windows Server 2008 R2 eingeführt, Dienste, die unter einem verwalteten Dienstkonto ausgeführt, die Domänenprinzipale sind.

Vor dem Starten eines Diensts, protokolliert Dienstcontroller mithilfe des Kontos, das für den Dienst festgelegt wurde und klicken Sie dann den Dienstanmeldeinformationen für die Authentifizierung durch die LSA auf. Der Windows-Dienst implementiert eine programmgesteuerte Schnittstelle, die den dienststeuerungs-Manager zum Steuern des Diensts verwenden können. Ein Windows-Dienst kann automatisch gestartet werden, wenn das System gestartet wird, oder manuell mit einem Service Control-Programm. Z. B. bei ein Windows-Client-Computer einer Domäne beitritt, der Messenger-Dienst auf dem Computer eine Verbindung mit einem Domänencontroller her und öffnet einen sicheren Kanal darauf. Um eine authentifizierte Verbindung zu erhalten, muss der Dienst über Anmeldeinformationen verfügen, die dem Remotecomputer Local Security Authority (LSA) vertraut. Bei der Kommunikation mit anderen Computern im Netzwerk verwendet LSA die Anmeldeinformationen für das Domänenkonto des lokalen Computers an, wie alle anderen Dienste, die im Sicherheitskontext des lokalen Systems und Network Service ausgeführt wird. Dienste auf dem lokalen Computer als SYSTEM ausgeführt werden, damit Anmeldeinformationen nicht an die LSA angezeigt werden müssen.

Die Datei Ksecdd.sys verwaltet und mit diesen Anmeldeinformationen verschlüsselt und einen lokalen Prozeduraufruf in die lokale Sicherheitsautorität verwendet. Der Dateityp DRV (Treiber) und bekannt ist als die Kernelmodus-Security Support Provider (SSP) und in den Versionen die **gilt für** Liste am Anfang dieses Themas, ist der FIPS 140-2 Level 1-kompatibel.

Kernel-Modus hat vollen Zugriff auf die Hardware- und Ressourcen des Computers. Kernel-Modus wird beendet, im Benutzermodus-Dienste und Anwendungen Zugriff auf kritische Bereiche des Betriebssystems, die sie keinen Zugriff auf haben sollte.

## <a name="BKMK_LSA"></a>Lokale Sicherheitsautorität
Der Local Security Authority (LSA) ist eine geschützte Systemprozess, der eine Authentifizierung und Anmeldung von Benutzern, sich bei dem lokalen Computer. Darüber hinaus verwaltet die LSA Informationen zu allen Aspekten der lokalen Sicherheitsgruppe auf einem Computer (diese Aspekte werden zusammenfassend als die lokale Sicherheitsrichtlinie bezeichnet), und es bietet verschiedene Dienste für die Übersetzung zwischen den Namen und die Sicherheits-IDs (SIDs). Systemprozess Sicherheit, Local Security Authority Server Service (LSASS), nachverfolgung von Sicherheitsrichtlinien und die Konten, die auf einem Computer gelten.

Die LSA überprüft die Identität eines Benutzers auf dessen Grundlage die von den folgenden zwei Entitäten, die das Konto des Benutzers ausgegeben:

-   **Lokale Sicherheitsautorität.** Überprüfen der Sicherheitskontenverwaltung (Security Accounts Manager, SAM)-Datenbank, die sich auf demselben Computer befinden kann die LSA Benutzerinformationen überprüfen. Alle Server Arbeitsstation oder Member kann es sich um lokale Benutzerkonten und Informationen zu lokalen Gruppen speichern. Diese Konten können jedoch verwendet werden, für den Zugriff auf nur die Arbeitsstation bzw. den Computer.

-   **Security-Autorität für die lokale Domäne oder einer vertrauenswürdigen Domäne.** Die LSA kontaktiert der Entität, die das Konto ausgegeben und die Überprüfung der Anforderungen, die das Konto gültig ist und die die Anforderung stammt aus der Besitzer des Kontos.

Der Subsystemdienst für die lokale Sicherheitsautorität (Local Security Authority Subsystem Service, LSASS) speichert Anmeldeinformationen für Benutzer mit aktiven Windows-Sitzungen im Arbeitsspeicher. Die gespeicherten Anmeldeinformationen können Benutzer nahtlos auf Netzwerkressourcen wie Dateifreigaben, Exchange Server-Postfächer und SharePoint-Websites zugreifen, ohne die Anmeldeinformationen für jeden Remotedienst erneut eingeben.

LSASS kann Anmeldeinformationen in verschiedenen Formaten speichern. Diese umfassen Folgendes:

-   Reversibel verschlüsselter Nur-Text

-   Kerberos-Tickets (Ticket granting Tickets (TGTs), Diensttickets)

-   NT-Hash

-   LAN Manager (LM)-hash

Wenn der Benutzer Windows anmeldet mit eine Smartcard, LSASS ein nur-Text-Kennwort nicht gespeichert, aber sie speichert den entsprechenden NT-Hashwert für das Konto und den nur-Text-PIN für die Smartcard. Wenn das Kontoattribut für eine Smartcard aktiviert ist, die für die interaktive Anmeldung erforderlich ist, wird für das Konto automatisch ein zufälliger NT-Hashwert anstelle des ursprünglichen Kennworthashes generiert. Der automatisch beim Festlegen des Attributs generierte Kennworthash wird nicht geändert.

Wenn ein Benutzer auf einem Windows-basierte Computer mit einem Kennwort, die mit Hashes von LAN Manager (LM) kompatibel ist anmeldet, ist dieser Authentifikator im Arbeitsspeicher vorhanden.

Die Speicherung von Nur-Text-Anmeldeinformationen im Arbeitsspeicher kann nicht deaktiviert werden, auch nicht, wenn die diese Informationen anfordernden Anmeldeinformationsanbieter deaktiviert sind.

Die gespeicherten Anmeldeinformationen direkt zugeordnet sind die Local Security Authority Subsystem Service (LSASS)-anmeldesitzungen, die nach dem letzten gestartet wurden, neu starten, und nicht geschlossen wurden. LSA-Sitzungen mit gespeicherten LSA-Anmeldeinformationen werden beispielsweise erstellt, wenn ein Benutzer eine der folgenden Aktionen ausführt:

-   Bei einer lokalen oder Remote Desktop Protocol (RDP)-Sitzung auf dem Computer anmeldet

-   Ausführen einer Aufgabe mit der Option **RunAs**

-   Ausführen eines aktiven Windows-Diensts auf dem Computer

-   Ausführen einer geplanten Aufgabe oder eines Batchauftrags

-   Ausführen einer Aufgabe auf dem lokalen Computer mithilfe eines Remoteverwaltungstools

In einigen Fällen werden die geheime LSA-Schlüssel, die geheime Datenelemente, die nur für Systemprozesse-Konto zugänglich sind sind, auf dem Festplattenlaufwerk gespeichert. Einige dieser geheimen Schlüssel sind Anmeldeinformationen, die nach dem Neustart beibehalten werden müssen und verschlüsselt auf dem Festplattenlaufwerk gespeichert werden. Als geheime LSA-Schlüssel gespeicherte Anmeldeinformationen können Folgendes umfassen:

-   Kontokennwort für das Konto des Computers Active Directory Domain Services (AD DS)

-   Kontokennwörter für auf dem Computer konfigurierte Windows-Dienste

-   Kontokennwörter für konfigurierte geplante Aufgaben

-   Kontokennwörter für IIS-Anwendungspools und -Websites

-   Kennwörter für Microsoft-Konten

Betriebssystem des Clients in Windows 8.1 eingeführt wurde, stellt die zusätzlichen Schutz für die lokale Sicherheitsautorität zu verhindern, dass Auslesen des Arbeitsspeichers und das injizieren von code durch ungeschützte Prozesse bereit. Dieser Schutz erhöht die Sicherheit für die Anmeldeinformationen, die der lokalen Sicherheitsautorität gespeichert und verwaltet.

Weitere Informationen zu diesen zusätzlichen Schutz, finden Sie unter [Configuring Additional LSA Protection](../credentials-protection-and-management/configuring-additional-lsa-protection.md).

## <a name="BKMK_CachedCredentialsAndValidation"></a>Zwischengespeicherte Anmeldeinformationen und Validierung
Überprüfungsmechanismen verlassen sich auf die Darstellung von Anmeldeinformationen zum Zeitpunkt der Anmeldung. Allerdings verwendet, wenn der Computer von einem Domänencontroller getrennt wird und der Benutzer ist Domänenanmeldeinformationen darstellen, Windows den Prozess der zwischengespeicherten Anmeldeinformationen in der Überprüfungsmechanismus.

Jedes Mal, wenn ein Benutzer einer Domäne anmeldet Windows speichert die angegebenen Anmeldeinformationen und speichert sie in der Struktur "Security" in der Registrierung des Betriebssystems.

Mit zwischengespeicherten Anmeldeinformationen kann der Benutzer zu einem Domänenmitglied melden Sie sich ohne eine Verbindung zu einem Domänencontroller innerhalb der Domäne.


## <a name="BKMK_CredentialStorageAndValidation"></a>Speichern von Anmeldeinformationen und Validierung
Es ist nicht immer wünschenswert, einen Satz von Anmeldeinformationen für den Zugriff auf verschiedene Ressourcen verwenden. Beispielsweise kann ein Administrator verwenden möchten administrative anstelle der Anmeldeinformationen des Benutzers beim Zugriff auf eine remote-Server. Auf ähnliche Weise, wenn ein Benutzer auf externe Ressourcen, z. B. ein Bankkonto zugreift können er nur Anmeldeinformationen verwenden, die ihre Domänenanmeldeinformationen unterscheiden. In den folgenden Abschnitten werden die Unterschiede in der Verwaltung von Anmeldeinformationen zwischen aktuellen Versionen von Windows-Betriebssysteme und die Betriebssysteme Windows Vista und Windows XP beschrieben.

### <a name="remote-logon-credential-processes"></a>Remoteanmeldung Anmeldeinformationen-Prozesse
Der Remote Desktop Protocol (RDP) verwaltet die Anmeldeinformationen des Benutzers, der mit einem Remotecomputer her, mit dem Remotedesktopclient, die in Windows 8 eingeführt wurde. Die Anmeldeinformationen im Nur-Text-Format werden für den Zielhost gesendet, in dem der Host versucht, den Authentifizierungsprozess durchzuführen und, wenn erfolgreich, verbindet sich der Benutzer auf zulässige Ressourcen. RDP die Anmeldeinformationen nicht auf dem Client gespeichert, aber die Anmeldeinformationen für die Domäne des Benutzers befinden sich im LSASS.

Eingeführt in Windows Server 2012 R2 und Windows 8.1, bietet eingeschränkten Administratormodus zusätzliche Sicherheit für Remoteanmeldung-Szenarien. In diesem Modus Remote Desktop bewirkt, dass die Clientanwendung mit der unidirektionalen NT-Funktion (NTOWF) den Netzwerk-Anmeldung Abfrage / Rückmeldung oder ein Kerberos-Dienstticket verwenden, bei der Authentifizierung mit dem Remotehost. Nach der Authentifizierung des Administrators hat der Administrator die entsprechenden Anmeldeinformationen im LSASS keinen, da sie nicht mit dem Remotehost bereitgestellt wurden. Stattdessen kann der Administrator die Anmeldeinformationen des Computerkontos für die Sitzung. Administratoranmeldeinformationen sind nicht für den Remotehost bereitgestellt, damit Aktionen als Computerkonto ausgeführt werden. Ressourcen sind auch auf das Computerkonto beschränkt, und der Administrator kann nicht auf Ressourcen mit dem sein eigenes Konto zugreifen.

### <a name="automatic-restart-sign-on-credential-process"></a>Automatischer Neustart-anmelden-Prozess
Wenn ein Benutzer auf einem Windows 8.1-Gerät anmeldet, speichert LSA die Anmeldeinformationen des Benutzers im verschlüsselten Speicher, die nur über LSASS.exe zugegriffen werden kann. Wenn Windows Update einen automatischen Neustart ohne Benutzeranwesenheit initiiert, werden diese Anmeldeinformationen verwendet, so konfigurieren Sie die automatische Anmeldung für den Benutzer.

Beim Neustart wird der Benutzer wird über den Mechanismus für die automatische Anmeldung automatisch angemeldet, und klicken Sie dann der Computer zusätzlich zum Schutz der Sitzung des Benutzers gesperrt ist. Das Sperren wurde während der Verwaltung von Anmeldeinformationen durch die LSA erfolgt über Windows-Anmeldung initiiert. Automatisch anmelden und Sperren die Sitzung des Benutzers in der Konsole des Benutzers sperren Anwendungen wird neu gestartet wurde und verfügbar.

Weitere Informationen zu nach einem, finden Sie unter [Winlogon automatischen Neustart anmelden &#40;nach einem&#41;](winlogon-automatic-restart-sign-on-arso.md).

### <a name="stored-user-names-and-passwords-in-windows-vista-and-windows-xp"></a>Gespeicherte Benutzernamen und Kennwörter in Windows Vista und Windows XP
In Windows Server 2008, Windows Server 2003, Windows Vista und Windows XP **gespeicherte Benutzernamen und Kennwörter** in der Systemsteuerung vereinfacht die Verwaltung und Verwendung von mehrere Sätze von Anmeldeinformationen angeben, einschließlich der verwendeten x. 509-Zertifikate mit Smartcards und Windows Live-Anmeldeinformationen (jetzt als "Microsoft-Konto" bezeichnet). Die Anmeldeinformationen - Teil des Benutzerprofils - werden gespeichert, bis Sie benötigt. Dadurch kann die Sicherheit auf einer Basis pro Ressource erhöhen, sicherstellen, dass ein Kennwort gefährdet ist, sie nicht die gesamte Sicherheit beeinträchtigt ist.

Nachdem ein Benutzer anmeldet und versucht, zusätzliche durch Kennwort geschützte Ressourcen, z. B. eine Freigabe auf einem Server zugreifen, und wenn Standard-Anmeldeinformationen des Benutzers für den Zugriff nicht ausreichen **gespeicherte Benutzernamen und Kennwörter** wird abgefragt . Wenn alternative Anmeldeinformationen mit der richtigen Anmeldeinformationen im gespeichert wurden **gespeicherte Benutzernamen und Kennwörter**, diese Anmeldeinformationen werden verwendet, um Zugriff zu erhalten. Andernfalls wird der Benutzer aufgefordert, um neue Anmeldeinformationen angeben, der für die Wiederverwendung, die weiter unten in der anmeldesitzung oder während einer nachfolgenden Sitzung gespeichert werden können.

Die folgenden Einschränkungen gelten:

-   Wenn **gespeicherte Benutzernamen und Kennwörter** enthält ungültige oder falsche Anmeldeinformationen aus, für eine bestimmte Ressource, die Zugriff auf die Ressource verweigert wird, und die **gespeicherte Benutzernamen und Kennwörter** Dialogfeld nicht angezeigt werden.

-   **Gespeicherte Benutzernamen und Kennwörter** speichert Anmeldeinformationen nur für NTLM, Kerberos-Protokoll, Microsoft-Konto (früher Windows Live ID) und Secure Sockets Layer (SSL)-Authentifizierung. Einige Versionen von Internet Explorer verwalten ihre eigenen Cache für die Standardauthentifizierung.

Diese Anmeldeinformationen werden eine verschlüsselte lokale Profil eines Benutzers im Verzeichnis der Pfadwert Data\Microsoft\Credentials und \Documents. Daher können diese Anmeldeinformationen mit dem Benutzer wechseln, wenn Netzwerkrichtlinie des Benutzers servergespeicherte Benutzerprofile unterstützt. Allerdings verfügt der Benutzer Kopien **gespeicherte Benutzernamen und Kennwörter** auf zwei verschiedenen Computern und ändert sich die Anmeldeinformationen, die die Ressource auf einem von diesen Computern zugeordnet sind die Änderung nicht weitergegeben  **Gespeicherte Benutzernamen und Kennwörter** auf dem zweiten Computer.

### <a name="windows-vault-and-credential-manager"></a>Windows-Tresor und Anmeldeinformations-Manager
Anmeldeinformations-Manager wurde als Feature Control Panel zum Speichern und Verwalten von Benutzernamen und Kennwörter in Windows Server 2008 R2 und Windows 7 eingeführt. Anmeldeinformations-Manager ermöglicht Benutzern das Speichern von Anmeldeinformationen, die relevant für die anderen Systemen und Websites in der sicheren Windows-Tresor. Dieses Feature wird von einigen Versionen von Internet Explorer für die Authentifizierung bei Websites verwenden.

Die Verwaltung der Anmeldeinformationen mithilfe der Anmeldeinformationsverwaltung wird durch den Benutzer auf dem lokalen Computer gesteuert. Benutzer können Anmeldeinformationen von unterstützten Browsern und Windows-Anwendungen speichern, um ihnen das erneute Anmelden bei diesen Ressourcen zu erleichtern. Anmeldeinformationen werden auf dem Computer in das Profil des Benutzers in speziellen verschlüsselten Ordnern gespeichert. Anwendungen, die dieses Feature (durch Verwendung von Anmeldinformationsverwaltungs-APIs), wie Webbrowsern und apps zu unterstützen, können die richtigen Anmeldeinformationen mit anderen Computern und Websites während des Anmeldevorgangs darstellen.

Wenn eine Website, eine Anwendung oder einem anderen Computer fordert Authentifizierung über NTLM oder Kerberos-Protokoll, ein Dialogfeld angezeigt wird in der Auswahl der **Standardanmeldeinformationen aktualisieren** oder **Kennwort speichern**Kontrollkästchen. Das Dialogfeld zu öffnen, in dem einen Benutzer Anmeldeinformationen lokal speichern zu können, wird von einer Anwendung generiert, die die Anmeldinformationsverwaltungs-APIs unterstützt. Wenn der Benutzer wählt die **Kennwort speichern** Kontrollkästchen Anmeldeinformations-Manager verfolgt des des Benutzers Benutzername, Kennwort und Weitere Informationen zu den Authentifizierungsdienst, der verwendet wird.

Das nächste Mal, das der Dienst verwendet wird, das liefert Anmeldeinformations-Manager automatisch die Anmeldeinformationen, die im Windows-Tresor gespeichert sind. Werden diese nicht akzeptiert, wird der Benutzer zur Eingabe der richtigen Information für den Zugriff aufgefordert. Wenn der Zugriff mit den neuen Anmeldeinformationen gewährt wird, wird Credential Manager überschreibt die vorherige Anmeldeinformationen durch die neue und speichert dann die neue Anmeldeinformationen im Windows-Tresor.

## <a name="BKMK_SAM"></a>SAM-Datenbank
(Security Accounts Manager, SAM) ist eine Datenbank, die lokale Benutzerkonten und-Gruppen speichert. Er befindet sich auf alle Windows-Betriebssystem; Wenn ein Computer einer Domäne angehört, verwaltet jedoch Active Directory Domänenkonten in Active Directory-Domäne.

Beispielsweise beteiligen, Clientcomputer mit Windows-Betriebssystem in einer Netzwerkdomäne durch Kommunikation mit einem Domänencontroller, selbst wenn kein Benutzer angemeldet ist. Um die Kommunikation initiieren können, muss der Computer ein aktives Konto in der Domäne sein. Vor dem akzeptieren die Kommunikation auf dem Computer, die LSA auf dem Domänencontroller authentifiziert die Computeridentität und klicken Sie dann den computersicherheitskontext erstellt, genau wie für einen menschlichen Sicherheitsprinzipal. Dieser Sicherheitskontext definiert die Identität und die Funktionen von einem Benutzer oder Dienst auf einem bestimmten Computer oder Benutzer, Dienst oder Computer in einem Netzwerk. Definiert z. B. das Zugriffstoken im Sicherheitskontext enthalten sind, die Ressourcen (z. B. eine Dateifreigabe oder Drucker), auf die zugegriffen werden können und die Aktionen (z. B. Lese-, Schreib- oder ändern), die von diesem Prinzipal - ein Benutzer, Computer oder Dienst auf, die ausgeführt werden können die Ressource.

Der Sicherheitskontext eines Benutzers oder Computers kann variieren, von einem Computer in eine andere, z. B. wenn ein Benutzer auf einem Server oder einer Arbeitsstation als die primäre Arbeitsstation des Benutzers anmeldet. Sie können auch aus einer Sitzung variieren, in eine andere, z. B. wenn ein Administrator die Rechte und Berechtigungen des Benutzers ändert. Darüber hinaus ist der Sicherheitskontext in der Regel unterschiedliche, wenn ein Benutzer oder Computer einzeln, in einem Netzwerk oder als Teil einer Active Directory-Domäne ausgeführt wird.

## <a name="BKMK_LocalDomainsAndTrustedDomains"></a>Lokale Domänen und vertrauenswürdigen Domänen
Wenn eine Vertrauensstellung zwischen zwei Domänen vorhanden ist, wird die Gültigkeit der Authentifizierungen, die von der anderen Domäne die Authentifizierungsmechanismen für jede Domäne abhängig. Vertraut, dass Hilfe kontrollierten Zugriff auf freigegebene Ressourcen in einer Ressourcendomäne (der vertrauenden Domäne) bereitstellen, indem Sie überprüfen, dass die Authentifizierung der eingehenden Anforderungen von einer vertrauenswürdigen Zertifizierungsstelle (der vertrauenswürdigen Domäne) stammen. Auf diese Weise fungieren die Vertrauensstellungen als Bridges, die jetzt nur Authentifizierung Anforderungen Travel zwischen Domänen überprüft.

Wie eine bestimmte Vertrauensstellung authentifizierungsanforderungen übergeben werden, hängt davon ab, wie er konfiguriert ist. Vertrauensstellungen können unidirektional, indem Sie Zugriff von der vertrauenswürdigen Domäne auf Ressourcen in der vertrauenden Domäne oder bidirektionale sein, indem Zugriff aus jeder Domäne auf Ressourcen in der anderen Domäne. Vertrauensstellungen sind auch in diesem Fall nur zwischen den zwei vertrauenswürdige Partner-Domänen eine Vertrauensstellung vorhanden ist nicht transitiv oder transitiv, in diesem Fall eine Vertrauensstellung automatisch erweitert, um keine weiteren Domänen, die einer der Partner vertraut.

Weitere Informationen zu Domänen- und Gesamtstruktur-Vertrauensstellungen in Bezug auf Authentifizierung finden Sie unter [der delegierten Authentifizierung und Vertrauensstellungen](https://technet.microsoft.com/library/dn169022.aspx).

## <a name="BKMK_CertificatesInWindowsAuthentication"></a>Zertifikate im Windows-Authentifizierung
Eine public Key-Infrastruktur (PKI) ist die Kombination von Software, verschlüsselungstechnologien, Prozesse und Dienste, die eine Organisation zum Schutz der Kommunikation und der Business-Transaktionen zu ermöglichen. Die Möglichkeit einer PKI zum Sichern der Kommunikation und Geschäftstransaktionen basiert auf den Austausch von digitalen Zertifikaten, die zwischen authentifizierten Benutzern und vertrauenswürdige Ressourcen.

Ein digitales Zertifikat ist ein elektronisches Dokument, das Informationen über die Entität, der er angehört, die Entität, die, der es ausgestellt wurde, eine eindeutige Seriennummer oder einige andere eindeutige ID, Ausstellung und Ablaufdatum und einen digitalen Fingerabdruck enthält.

Authentifizierung ist der Prozess der Ermittlung, ob ein remoter Host vertrauenswürdig ist. Um die Vertrauenswürdigkeit herzustellen, muss der Remotehost eine akzeptable Authentifizierungszertifikat angeben.

Remotehosts Abrufen eines Zertifikats von einer Zertifizierungsstelle (CA) hergestellt werden deren Vertrauenswürdigkeit. Die Zertifizierungsstelle, wiederum Zertifizierung von einer höheren Autorität umgestellt haben, haben eine Vertrauenskette erstellt. Um zu bestimmen, ob ein Zertifikat vertrauenswürdig ist, muss eine Anwendung bestimmen die Identität der Stamm-ZS, und dann ermitteln, ob es vertrauenswürdig ist.

Auf ähnliche Weise muss die remote-Host oder dem lokalen Computer ermitteln, ob das vom Benutzer oder der Anwendung bereitgestellte Zertifikat echt ist. Das vom Benutzer über die lokale Sicherheitsautorität und SSPI vorgelegte Zertifikat wird für die Authentizität auf dem lokalen Computer für die lokale Anmeldung, im Netzwerk oder in der Domäne über die Zertifikatspeicher in Active Directory ausgewertet.

Hashalgorithmen, wie z. B. Secure Hash Algorithm 1 (SHA1), daher erzeugt ein Zertifikat, die Authentifizierungsdaten durchläuft, um einen Message Digest zu erstellen. Der Message Digest ist mit der private Schlüssel des Absenders um zu beweisen, dass der Message Digest vom Absender erstellt wurde dann digital signiert.

> [!NOTE]
> SHA1 ist die Standardeinstellung in Windows 7 und Windows Vista, aber es wurde geändert in SHA2 in Windows 8.

**Smartcard-Authentifizierung**

Smartcard-Technologie ist ein Beispiel einer zertifikatbasierten Authentifizierung. Mit einem Netzwerk mit einer Smartcard anmelden bietet eine starke Form der Authentifizierung, da Kryptographie basierenden Identifikation und Nachweis des rechtmäßigen Besitzes beim Authentifizieren eines Benutzers zu einer Domäne verwendet. Active Directory-Zertifikatdienste (AD CS) bietet die kryptografischen basierende Identifikation über die Ausstellung eines Zertifikats für jede Smartcard-Anmeldung.

Weitere Informationen über die Smartcard-Authentifizierung finden Sie unter den [technische Referenz für Windows Smart Card](https://technet.microsoft.com/library/ff404297.aspx).

Virtuelle Smartcard-Technologie wurde in Windows 8 eingeführt. Wird die Smartcard-Zertifikat auf dem PC speichert, und klicken Sie dann mithilfe des Geräts vor Manipulationen sicher Trusted Platform Module (TPM)-Sicherheitschip geschützt. Auf diese Weise wird praktisch der PC die Smartcard die PIN des Benutzers empfangen müssen, um authentifiziert werden.

**Remote- und wireless-Authentifizierung**

Remote und wireless-Authentifizierung ist eine andere Technologie, die Zertifikate für die Authentifizierung verwendet. Der Internetauthentifizierungsdienst (IAS) und VPN-Server verwenden, Extensible Authentication Protocol – Transport Level Security (EAP-TLS), Internet Protocol Security (IPsec) oder PEAP Protected Extensible Authentication Protocol () um zertifikatbasierte Authentifizierung für viele Arten von Netzwerkzugriffen, einschließlich virtuelles privates Netzwerk (VPN) und wireless-Verbindungen durchgeführt werden.

Weitere Informationen zu einer zertifikatbasierten Authentifizierung in Netzwerken, finden Sie unter [Netzwerkzugriffsauthentifizierung und Zertifikaten](https://technet.microsoft.com/library/cc759575(WS.10).aspx).

## <a name="BKMK_SeeAlso"></a>Siehe auch
[Windows-Authentifizierungskonzepte](https://technet.microsoft.com/library/d169018.aspx)


