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
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="credentials-processes-in-windows-authentication"></a>Anmeldeinformationen-Prozesse in der Windows-Authentifizierung

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Referenzthema für IT-Experten wird beschrieben, wie Windows-Authentifizierung für Anmeldeinformationen verarbeitet.

Verwaltung von Windows-Anmeldeinformationen werden mit dem das Betriebssystem die Anmeldeinformationen aus dem Dienst oder der Benutzer erhält und sichert die Informationen für zukünftige Präsentation an das Ziel der Authentifizierung. Im Fall von einem Computer einer Domäne angehört ist das Ziel der Authentifizierung der Domänencontroller. Bei der Authentifizierung verwendeten Anmeldeinformationen werden digitale Dokumente, die die Identität des Benutzers in eine Form von Nachweis der Authentizität, z.B. ein Zertifikat, ein Kennwort oder eine PIN zuordnen.

Standardmäßig werden die Windows-Anmeldeinformationen für die Sicherheitskontenverwaltung (Security Accounts Manager, SAM)-Datenbank auf dem lokalen Computer oder anhand von Active Directory auf einem Computer einer Domäne angehört, über den Winlogon-Dienst überprüft. Anmeldeinformationen werden durch eine Benutzereingabe gesammelt, wenn Sie auf der Benutzeroberfläche für die Anmeldung oder programmgesteuert über die Anwendungsprogrammierschnittstelle (API), mit dem authentifizierenden Ziel angezeigt werden.

Lokale Sicherheitsinformationen befindet sich in der Registrierung unter **HKEY_LOCAL_MACHINE\SECURITY**. Gespeicherter Informationen enthält Richtlinieneinstellungen, Standardwerte für die Sicherheit und Kontoinformationen, wie z.B. zwischengespeicherte Anmeldeinformationen. Eine Kopie der SAM-Datenbank wird ebenfalls hier gespeichert werden, obwohl es schreibgeschützt ist.

Das folgende Diagramm zeigt die Komponenten, die erforderlich sind und der Pfade, Anmeldeinformationen zum Authentifizieren des Benutzers oder der Prozess für eine erfolgreiche Anmeldung über das System zu nutzen.

![Diagramm zeigt die Komponenten, die erforderlich sind und der Pfade, die Anmeldeinformationen werden durch das System zum Authentifizieren des Benutzers oder der Prozess für eine erfolgreiche Anmeldung.](../media/credentials-processes-in-windows-authentication/AuthN_LSA_Architecture_Client.gif)

Die folgende Tabelle beschreibt jede Komponente, die Verwaltung von Anmeldeinformationen zum Zeitpunkt der Anmeldung bei der Authentifizierung.

**Authentication-Komponenten für alle Systeme**

|Komponente|Beschreibung|
|-------|--------|
|Anmeldung des Benutzers|Winlogon.exe ist die ausführbare Datei für die Verwaltung von sicheren Benutzerinteraktionen zuständig. Der Winlogon-Dienst initiiert der Anmeldeprozess für Windows-Betriebssysteme durch Übergabe der gesammelten durch den Benutzer auf dem sicheren Desktop (Anmeldung, UI) zu Local Security Authority (LSA) über Secur32.dll Anmeldeinformationen.|
|App-Anmeldung|Die Anwendung oder Dienst Anmeldungen, die keine interaktive Anmeldung erforderlich ist. Die meisten Prozesse, die durch den Benutzer im Benutzermodus ausgeführt wird, mithilfe von Secur32.dll während initiiert beim Systemstart, wie Dienste, Prozesse im Kernelmodus ausgeführt werden, mithilfe von Ksecdd.sys initiiert werden.<br /><br />Weitere Informationen zu Benutzermodus und Kernelmodus finden Sie in diesem Thema Anwendungen und Benutzer oder Dienste und Kernelmodus.|
|Secur32.dll|Die mehrere Authentifizierungsanbieter, der aus die Grundlage für die Authentifizierung verarbeiten.|
|Lsasrv.dll|Der LSA-Server-Dienst, die erzwingt Sicherheitsrichtlinien und fungiert als Sicherheitspaket-Manager für die lokale Sicherheitsautorität. Die LSA enthält der Negotiate-Funktion, die wählt die NTLM- oder Kerberos-Protokoll nach feststellen, welches Protokoll erfolgreich ausgeführt werden kann.|
|Security Support Provider|Eine Reihe von Anbieter, die eine oder mehrere Authentifizierungsprotokolle einzeln aufrufen können. Die Standardgruppe von Anbieter kann mit jeder Version von Windows-Betriebssystem ändern und benutzerdefinierte Anbieter geschrieben werden können.|
|Netlogon.dll|Die Dienste, die der Netlogon-Dienst führt lauten wie folgt:<br /><br />-Sorgt für sicheren Kanal (nicht zu verwechseln mit Schannel) des Computers zu einem Domänencontroller.<br />-Übergibt die Anmeldeinformationen des Benutzers über einen sicheren Kanal mit dem Domänencontroller und Domänen-Sicherheits-IDs (SIDs) und Benutzerrechte für den Benutzer zurückgegeben.<br />-Veröffentlicht Ressourceneinträge für Dienste in Domain Name System (DNS) und DNS zum Auflösen von Namen zu IP (Internet Protocol)-Adressen der Domänencontroller verwendet.<br />-Replikationsprotokolls basierend auf der Remoteprozeduraufruf (RPC) für die Synchronisierung von primären Domänencontroller (PDCs) und Domänencontrollern (Sicherungsdomänencontroller) implementiert.|
|Samsrv.dll|Die Sicherheitskontenverwaltung (SAM), der lokalen Sicherheitskonten gespeichert sind, erzwingt Richtlinien für lokal gespeicherte und APIs unterstützt.|
|Registrierung|Die Registrierung enthält eine Kopie der SAM-Datenbank, lokale Richtlinieneinstellungen, Standardwerte für die Sicherheit und Kontoinformationen, die nur für das System verfügbar ist.|

Dieses Thema enthält die folgenden Abschnitte:

-   [Eingabe von Anmeldeinformationen für die Anmeldung des Benutzers](#BKMK_CrentialInputForUserLogon)

-   [Eingabe von Anmeldeinformationen für die Anwendung und -Anmeldung](#BKMK_CredentialInputForApplicationAndServiceLogon)

-   [Local Security Authority](#BKMK_LSA)

-   [Überprüfung und Anmeldeinformationen](#BKMK_CachedCredentialsAndValidation)

-   [Überprüfung und Speicherung von Anmeldeinformationen](#BKMK_CredentialStorageAndValidation)

-   [SAM-Datenbank](#BKMK_SAM)

-   [Lokale Domänen und vertrauenswürdigen Domänen](#BKMK_LocalDomainsAndTrustedDomains)

-   [Zertifikate in der Windows-Authentifizierung](#BKMK_CertificatesInWindowsAuthentication)

## <a name="BKMK_CrentialInputForUserLogon"></a>Eingabe von Anmeldeinformationen für die Anmeldung des Benutzers
In Windows Server2008 und Windows Vista wurde die Graphical Identification and Authentication (GINA)-Architektur mit einem Anmeldeinformationsanbieter ersetzt, die verschiedenen Anmeldetypen durch die Verwendung von anmeldekacheln auflisten möglich. Beide Modelle werden nachfolgend beschrieben.

**GINA-Architektur**

Die Architektur Graphical Identification and Authentication (GINA) gilt für die Betriebssysteme Windows Server2003, Microsoft Windows2000 Server, Windows XP und Windows2000 Professional. In diesen Systemen erstellt jeder Sitzung interaktive Anmeldung eine separate Instanz der Winlogon-Dienst. Die GINA-Architektur des von Winlogon belegten Prozess geladen wird, empfängt und verarbeitet die Anmeldeinformationen und ruft die Schnittstellen Authentifizierung über LSALogonUser.

Führen Sie die Instanzen von Windows-Anmeldung bei einer interaktiven Anmeldung in Sitzung 0. Sitzung 0 Hosts Systemdienste und andere wichtige Prozesse, einschließlich des Prozess (Local Security Authority, LSA).

Das folgende Diagramm zeigt den Anmeldeinformationsprozess für Windows Server2003, Microsoft Windows2000 Server, Windows XP und Microsoft Windows2000 Professional.

![Das Diagramm zeigt den Anmeldeinformationsprozess für Windows Server2003, Microsoft Windows2000 Server, Windows XP und Microsoft Windows2000 Professional](../media/credentials-processes-in-windows-authentication/AuthN_GINA_Architecture.gif)

**Anmeldeinformationsanbieter-Architektur**

Der Anmeldeinformationsanbieter-Architektur bezieht sich auf diese Versionen, die im angegebenen der **gilt für** -Liste am Anfang dieses Themas. In diesen Systemen wird mithilfe von Anmeldeinformationsanbieter die Anmeldeinformationen Input-Architektur zu einem erweiterbaren Entwurf geändert. Diese Anbieter werden durch die verschiedenen anmeldekacheln auf dem sicheren Desktop dargestellt, die eine beliebige Anzahl von Anmeldeszenarios – verschiedene Konten für den gleichen Benutzer und andere Authentifizierungsmethoden, z.B. Kennwort, Smartcards und biometrische Daten zu ermöglichen.

Mit der Anmeldeinformationsanbieter-Architektur beginnt Winlogon immer Anmeldung UI nach einer sicheren Aufmerksamkeit Sequenz-Ereignis Erhalt. Anmeldebenutzeroberfläche fragt jedes Anmeldeinformationsanbieter für die Anzahl der verschiedene Arten von Anmeldeinformationen, die der Anbieter konfiguriert ist, dass aufgelistet werden. Anmeldeinformationsanbieter haben die Möglichkeit, eine der folgenden Kacheln als Standard festlegen. Nachdem alle Anbieter ihre Kacheln aufgezählt haben, werden Sie von Anmeldung UI für den Benutzer angezeigt. Der Benutzer interagiert mit einer Kachel, ihre Anmeldeinformationen einzugeben. Anmeldebenutzeroberfläche sendet diese Anmeldeinformationen für die Authentifizierung.

Anmeldeinformationsanbieter sind keine Mechanismen zum erzwingen. Sie werden verwendet, sammeln und Anmeldeinformationen zu serialisieren. Die Pakete Local Security Authority und Authentifizierung erzwingen der Sicherheit.

Anbieter von Benutzeranmeldeinformationen auf dem Computer registriert sind, und sind verantwortlich für die folgenden:

-   Beschreiben die Anmeldeinformationen für die Authentifizierung erforderlich.

-   Behandeln von Kommunikation und Logik mit externen Zertifizierungsstellen.

-   Verpacken von Anmeldeinformationen für die interaktive und Netzwerk anmelden.

Verpacken von Anmeldeinformationen für die interaktive und Netzwerkanmeldung den Prozess der Serialisierung enthält. Durch eine Serialisierung Anmeldeinformationen können mehrere anmeldekacheln auf der Anmeldebenutzeroberfläche angezeigt werden. Daher kann die Organisation die Anmeldung-Anzeige, z.B. Benutzer, die Zielsysteme für die Anmeldung, die vor der Anmeldung den Zugriff auf die Netzwerk- und Arbeitsstation sperren und entsperren Sie Richtlinien – durch die Verwendung von benutzerdefinierten Anmeldeinformationsanbieter steuern. Mehrere Anmeldeinformationsanbieter können auf demselben Computer installiert sein.

Einzelne einmaliges Anmelden (SSO)-Anbieter können als eine Standard-Anmeldeinformationsanbieter oder als Pre-Logon-Access Provider entwickelt werden.

Jede Version von Windows enthält ein Standard-Anmeldeinformationsanbieter und eine standardmäßige Pre-Logon-Access Provider PLAP (Pre), auch bekannt als die SSO-Anbieter. Die SSO-Anbieter kann Benutzer eine Verbindung mit einem Netzwerk vor dem Anmelden auf dem lokalen Computer herstellen. Wenn dieser Anbieter implementiert wird, werden der Anbieter Kacheln auf der Benutzeroberfläche der Anmeldung nicht aufgezählt.

Ein SSO-Anbieter ist vorgesehen, in den folgenden Szenarien verwendet werden:

-   **Netzwerkanmeldung Benutzerauthentifizierung und von anderen Anmeldeinformationsanbieter behandelt werden.** Für dieses Szenario Variationen:

    -   Ein Benutzer ist hat die Möglichkeit, Herstellen einer Verbindung mit einem Netzwerk, z.B. Herstellen einer Verbindung mit einem virtuellen privaten Netzwerk (VPN), vor der Anmeldung auf dem Computer jedoch nicht erforderlich für diese Verbindung.

    -   Die Authentifizierung ist erforderlich, zum Abrufen von Informationen, die während der interaktiven Authentifizierung auf dem lokalen Computer verwendet.

    -   Mehrere Netzwerk-Authentifizierungen eines der anderen Szenarien folgen. Beispielsweise ein Benutzer authentifiziert sich gegenüber einem Internetdienstanbieter (ISP) einer VPN-Verbindung authentifiziert und verwendet dann die Anmeldeinformationen für ein Benutzerkonto lokal anmelden.

    -   Zwischengespeicherte Anmeldeinformationen sind deaktiviert, und eine RAS-Dienste-Verbindung über VPN ist zum Authentifizieren des Benutzers vor lokalen Anmeldung erforderlich.

    -   Ein Domänenbenutzer verfügt nicht über ein lokales Konto auf einem Computer einer Domäne eingerichtet und muss eine Verbindung RAS-Dienste über VPN-Verbindung vor dem Abschluss der interaktiven Anmeldung herstellen.

-   **Netzwerkanmeldung Benutzerauthentifizierung und von der gleichen Anmeldeinformationsanbieter behandelt werden.** In diesem Szenario muss der Benutzer eine Verbindung mit dem Netzwerk vor der Anmeldung am Computer.

**Anmeldung Kachel enumeration**

Der Anmeldeinformationsanbieter listet anmeldekacheln in den folgenden Fällen:

-   Für diese Betriebssysteme in der **gilt für** -Liste am Anfang dieses Themas.

-   Der Anmeldeinformationsanbieter zählt die Kacheln für die Anmeldung an der Arbeitsstation. Der Anmeldeinformationsanbieter serialisiert in der Regel die Anmeldeinformationen für die Authentifizierung auf die lokale Sicherheitsautorität. Dieser Prozess wird Kacheln für jeden Benutzer und bestimmte Zielsysteme des Benutzers angezeigt.

-   Die Architektur für Anmeldung und Authentifizierung kann Benutzer Kacheln, die von der Anmeldeinformationsanbieter aufgelistet verwenden, um eine Arbeitsstation zu entsperren. Der derzeit angemeldete Benutzer wird die Standardkachel normalerweise mehr als ein Benutzer angemeldet ist, werden zahlreiche Kacheln angezeigt.

-   Der Anmeldeinformationsanbieter listet Kacheln als Antwort auf eine Anforderung an den ihr Kennwort oder andere private Informationen, z.B. eine PIN ändern. In der Regel ist der aktuell angemeldete Benutzer die Standardkachel. Wenn mehr als ein Benutzer angemeldet ist, werden jedoch zahlreiche Kacheln angezeigt.

-   Der Anmeldeinformationsanbieter listet Kacheln basierend auf den serialisierten Anmeldeinformationen für die Authentifizierung auf Remote-PCs verwendet werden. Anmeldeinformationen UI verwendet nicht dieselbe Instanz des Anbieters als die Anmeldung UI, Entsperren einer Arbeitsstation oder Kennwort ändern. Aus diesem Grund kann Informationen vom Provider zwischen Instanzen von Anmeldeinformationen verwaltet werden. Diese Struktur führt zu einer Kachel für die einzelnen Remotecomputer Anmeldung, vorausgesetzt, dass die Anmeldeinformationen richtig serialisiert wurden. Dieses Szenario wird auch in User Account Control (UAC) verwendet, die verhindern, können nicht autorisierte Änderungen an einem Computer der Benutzer nach Ihrer Zustimmung oder Eingabe eines Administratorkennworts aufgefordert, vor dem Zulassen von Aktionen, die konnte den Betrieb des PCs beeinträchtigen oder konnte die Änderung von Einstellungen, die andere Benutzer des Computers auswirken.

Das folgende Diagramm zeigt den Anmeldeinformationsprozess für die Betriebssysteme in der **gilt für** -Liste am Anfang dieses Themas.

![Diagramm den Anmeldeinformationsprozess für die Betriebssysteme zeigt in der ** gilt für **-Liste am Anfang dieses Themas](../media/credentials-processes-in-windows-authentication/AuthN_CredMan_CredProv.gif)

## <a name="BKMK_CredentialInputForApplicationAndServiceLogon"></a>Eingabe von Anmeldeinformationen für die Anwendung und -Anmeldung
Windows-Authentifizierung dient zum Verwalten von Anmeldeinformationen für Anwendungen oder Dienste, die keine Interaktion des Benutzers erfordern. Anwendungen im Benutzermodus können nur im Hinblick auf welche Ressourcen sie Zugriff haben während Dienste uneingeschränkten Zugriff auf den Systemspeicher und externe Geräte verfügen können.

System-Dienste und Anwendungen auf der Übertragungsebene zugreifen, ein Security Support Provider (SSP) über die Security Support Provider-Schnittstelle (SSPI) in Windows, die Funktionen zum Aufzählen von Paketen des im System verfügbar, das Auswählen eines Pakets und verwenden dieses Paket erhalten Sie eine authentifizierte Verbindung bereitstellt.

Wenn eine Client/Server-Verbindung authentifiziert wird:

-   Die Anwendung auf der Clientseite der Verbindung sendet Anmeldeinformationen an den Server mithilfe der SSPI-Funktion `InitializeSecurityContext (General)`.

-   Die Anwendung auf dem Server, der die Verbindung mit der SSPI-Funktion reagiert `AcceptSecurityContext (General)`.

-   Die SSPI-Funktionen `InitializeSecurityContext (General)`und `AcceptSecurityContext (General)`werden wiederholt, bis alle erforderlichen Authentifizierungsnachrichten ausgetauscht wurden, um entweder erfolgreich oder nicht erfolgreich authentifiziert.

-   Nachdem die Verbindung authentifiziert wurde, verwendet die LSA auf dem Server Informationen vom Client den Sicherheitskontext enthält ein Zugriffstoken zu erstellen.

-   Der Server kann dann die SSPI-Funktion aufrufen `ImpersonateSecurityContext`ein Thread Identitätswechsel für den Dienst das Zugriffstoken an.

**Anwendungen und Benutzermodus**

Benutzermodus in Windows besteht aus zwei Systemen, die mit der Übergabe von E/A-Anforderungen an die entsprechenden Kernelmodus-Treiber: das Umgebungssystem, in der Anwendung für viele verschiedene Arten von Betriebssystemen ausgeführt wird, und das wesentlicher System, das System-spezifische Funktionen für das Umgebungssystem ausgeführt wird.

Das System ein wesentlicher Bestandteil des Betriebssystems System'specific Funktionen für die Umgebungssystem verwaltet und besteht aus einem Systemprozess Sicherheit (LSA), eine Arbeitsstationsdienst und einen Server-Dienst. Der Systemprozess Sicherheit Sicherheitstoken handhabt, gewährt oder Zugriffsberechtigungen für Benutzerkonten, die basierend auf den über die Berechtigung verweigert, Anmeldeanfragen behandelt und initiiert die Authentifizierung bei der Anmeldung und bestimmt, welche Systemressourcen, das Betriebssystem überwachen muss.

Anwendungen können in Benutzermodus ausgeführt, in dem die Anwendung kann als ein Prinzipal, einschließlich im Sicherheitskontext des lokalen Systems (SYSTEM) ausgeführt. Anwendungen können auch im Kernelmodus ausgeführt, in dem die Anwendung im Sicherheitskontext des lokalen Systems (SYSTEM) ausführen kann.

SSPI ist über das Modul Secur32.dll, das eine API zum Abrufen von integrierten Sicherheitsdiensten für Authentifizierung, Integrität und Datenschutz von Nachrichten ist verfügbar. Es enthält eine Abstraktionsschicht zwischen Protokollen auf Anwendungsebene und Sicherheitsprotokollen. Da unterschiedliche Anwendungen benötigen verschiedene Methoden zum Authentifizieren von Benutzern und anderen Methoden zum Verschlüsseln von Daten bei der Übertragung über ein Netzwerk oder identifizieren, ermöglicht das SSPI Dynamic Link Libraries (DLLs) zugreifen, die andere Authentifizierung und kryptografischen Funktionen enthalten. Diese DLL-Dateien werden als Security Support Provider (SSP) bezeichnet.

Verwaltete und virtuellen Dienstkonten in Windows Server2008 R2 eingeführt wurden und Windows7 in wichtigen Anwendungen, wie Microsoft SQL Server und IIS (Internetinformationsdienste), die Isolierung der eigenen Domänenkonten ermöglichen, während die Notwendigkeit von einem Administrator manuell zu eliminieren verwalten, den Dienstprinzipalnamen (SPN) und die Anmeldeinformationen für diese Konten. Weitere Informationen zu diesen Features und ihre Rolle bei der Authentifizierung finden Sie unter [Managed Service Accounts Dokumentation für Windows7 und Windows Server2008 R2](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx) und [Gruppe verwaltete Dienstkonten: Übersicht](../group-managed-service-accounts/group-managed-service-accounts-overview.md).

**Dienste und Kernel-Modus**

Obwohl die meisten Windows-Anwendungen im Sicherheitskontext des Benutzers, die sie gestartet wird ausgeführt, gilt dies nicht der Dienste. Viele Windows-Dienste, z.B. Netzwerk- und Druckdienste, werden durch die Dienstcontroller gestartet, wenn der Benutzer des Computers beginnt. Diese Dienste möglicherweise als lokaler Dienst oder das lokale Systemkonto ausführen und möglicherweise weiterhin ausgeführt, nachdem Sie der letzten Benutzer sich abmeldet.

> [!NOTE]
> Dienste, die normalerweise in den Sicherheitskontexten bekannt als lokales System (SYSTEM), Netzwerkdienst oder lokaler Dienst ausgeführt werden.  Windows Server2008 R2 eingeführt, die Domänenprinzipale sind Dienste, die unter einem verwalteten Dienstkonto ausgeführt wird.

Vor dem Start von eines Diensts anmeldet Dienstcontroller mit dem Konto, das für den Dienst festgelegt wurde, und zeigt den Dienst-Anmeldeinformationen für die Authentifizierung von der LSA. Der Windows-Dienst implementiert eine Programmierschnittstelle, die den dienststeuerungs-Manager verwenden kann, um den Dienst zu steuern. Ein Windows-Dienst kann automatisch gestartet werden, wenn das System gestartet wird oder manuell mit ein. Wenn beispielsweise ein Windows-Clientcomputer einer Domäne beitritt, der Messenger-Dienst auf dem Computer eine Verbindung mit einem Domänencontroller herstellt und öffnet einen sicheren Kanal zu. Um eine authentifizierte Verbindung zu erhalten, muss der Dienst Anmeldeinformationen verfügen, die dem Remotecomputer Local Security Authority (LSA) vertraut. Bei der Kommunikation mit anderen Computern im Netzwerk verwendet LSA die Anmeldeinformationen für das Domänenkonto des lokalen Computers, wie alle anderen Dienste, die im Sicherheitskontext des lokalen Systems und Netzwerkdienst ausgeführt. Die Dienste auf dem lokalen Computer als SYSTEM ausgeführt werden, sodass Anmeldeinformationen nicht auf die lokale Sicherheitsinstanz angezeigt werden müssen.

Die Datei Ksecdd.sys verwaltet und diese Anmeldeinformationen verschlüsselt und lokalen Prozeduraufruf in die lokale Sicherheitsautorität verwendet. Der Dateityp DRV (Treiber) und bekannt ist als die Kernelmodus-Security Support Provider (SSP) und in diesen Versionen im angegebenen der **gilt für** am Anfang dieses Themas aufgelistet, die FIPS 140-2 Stufe 1-kompatibel ist.

Kernel-Modus verfügt über vollständigen Zugriff auf die Hardware- und Systemeinstellungen Ressourcen des Computers. Kernel-Modus wird beendet, Benutzermodus-Dienste und Anwendungen am Zugriff auf kritische Bereiche des Betriebssystems, der sie nicht den Zugriff auf.

## <a name="BKMK_LSA"></a>Local Security Authority
Local Security Authority (LSA) ist ein geschütztes System-Prozess, der authentifiziert und Benutzer auf dem lokalen Computer anmeldet. Darüber hinaus LSA verwaltet Informationen zu allen Aspekten der lokalen Sicherheit auf einem Computer (diese Aspekte werden zusammen als die lokale Sicherheitsrichtlinie bezeichnet), und bietet verschiedene Dienste für die Übersetzung zwischen Namen und Sicherheits-IDs (SIDs). Der Systemprozess Sicherheit, Local Security Authority Server Service (LSASS), hält den Überblick über die Sicherheitsrichtlinien und die Konten, die auf einem Computer aktiviert sind.

Die LSA überprüft die Identität eines Benutzers basierend auf der die folgenden zwei Elemente, die das Konto des Benutzers ausgegeben:

-   **Lokale Sicherheitsautorität.** Die LSA kann Benutzerinformationen durch Überprüfen der Sicherheitskontenverwaltung (Security Accounts Manager, SAM)-Datenbank befindet sich auf demselben Computer überprüfen. Alle Arbeitsstationen oder Mitgliedsservern Server kann es sich um lokale Benutzerkonten und Informationen zu lokalen Gruppen speichern. Allerdings können diese Konten für den Zugriff auf nur der Arbeitsstation oder des Computers verwendet werden.

-   **Sicherheitsautorität für die lokale Domäne oder einer vertrauenswürdigen Domäne.** Die LSA kontaktiert der Entität, die das Konto ausgestellt und Überprüfung der Anforderungen, die das Konto gültig ist und, die die Anforderung stammt aus der Kontoinhaber.

Die Local Security Authority Subsystem Service (LSASS) speichert Anmeldeinformationen für Benutzer mit aktiven Windows-Sitzungen im Arbeitsspeicher. Die gespeicherten Anmeldeinformationen können Benutzer nahtlos auf die Netzwerkressourcen wie Dateifreigaben, Exchange Server-Postfächer und SharePoint-Websites zugreifen, ohne ihre Anmeldeinformationen für jeden Remotedienst erneut eingeben zu müssen.

LSASS kann Anmeldeinformationen in verschiedenen Formaten speichern:

-   Reversibel verschlüsselter Nur-Text

-   Kerberos-Tickets (Ticket-granting Tickets (TGTs), Diensttickets)

-   NT-hash

-   LAN Manager (LM)-hash

Wenn der Benutzer bei Windows anmeldet mithilfe einer Smartcard, LSASS wird ein Nur-Text-Kennwort nicht gespeichert, aber den entsprechenden NT-Hashwert für das Konto und das Nur-Text-PIN für die Smartcard gespeichert. Wenn das Kontoattribut für eine Smartcard, die für die interaktive Anmeldung erforderlich ist aktiviert ist, wird ein zufälliger NT-Hashwert automatisch für das Konto anstelle des ursprünglichen Kennworthashes generiert. Der Hashwert des Kennworts, die automatisch generiert wird, wenn das Attribut festgelegt ist, wird nicht geändert.

Wenn ein Benutzer auf einem Windows-basierten Computer mit einem Kennwort, die mit LAN Manager (LM)-Hashes kompatibel ist anmeldet, ist dieser Authentifikator im Arbeitsspeicher vorhanden.

Die Speicherung von Nur-Text-Anmeldeinformationen im Arbeitsspeicher kann nicht deaktiviert werden, selbst wenn der Anbieter von Benutzeranmeldeinformationen, die sie benötigen deaktiviert sind.

Die gespeicherten Anmeldeinformationen direkt im Zusammenhang mit der Local Security Authority Subsystem Service (LSASS)-anmeldesitzungen, die nach der letzten gestartet wurden neu starten und nicht geschlossen wurden. LSA-Sitzungen mit gespeicherten LSA-Anmeldeinformationen werden beispielsweise erstellt, wenn ein Benutzer eine der folgenden ausführt:

-   An einem lokalen oder Remote Desktop Protocol (RDP)-Sitzung auf dem Computer anmeldet

-   Ausführen einer Aufgabe mithilfe der **RunAs** Option

-   Ausführen ein aktiven Windows-Diensts auf dem Computer

-   Führt einen geplanten Auftrag Aufgabe oder eines Batchauftrags

-   Führt einen Task auf dem lokalen Computer mithilfe eines Remoteverwaltungstools

In einigen Fällen werden die geheime LSA-Schlüssel, die geheimen Datenteile, die nur für SYSTEM-Konto Prozessen zugänglich sind sind, auf dem Festplattenlaufwerk gespeichert. Einige dieser geheimen Schlüssel sind Anmeldeinformationen, die nach dem Neustart beibehalten werden müssen, und sie werden in verschlüsselter Form auf dem Festplattenlaufwerk gespeichert. Als geheime LSA-Schlüssel gespeicherte Anmeldeinformationen können Folgendes umfassen:

-   Kennwort für das Konto des Computers Active Directory-Domänendienste (AD DS)

-   Kontokennwörter für Windows-Dienste, die auf dem Computer konfiguriert sind

-   Kontokennwörter für konfigurierte geplante Aufgaben

-   Kontokennwörter für IIS-Anwendungspools und -Websites

-   Kennwörter für Microsoft-Konten

In Windows8.1 eingeführt wurde, bietet das Clientbetriebssystem zusätzlichen Schutz für die lokale Sicherheitsinstanz zu verhindern, dass Auslesen des Arbeitsspeichers und das injizieren von Code durch ungeschützte Prozesse. Dieser Schutz erhöht die Sicherheit für die Anmeldeinformationen, die der lokalen Sicherheitsautorität gespeichert und verwaltet.

Weitere Informationen zu diesen zusätzlichen Schutz, finden Sie unter [Configuring Additional LSA Protection](../credentials-protection-and-management/configuring-additional-lsa-protection.md).

## <a name="BKMK_CachedCredentialsAndValidation"></a>Überprüfung und Anmeldeinformationen
Überprüfung Mechanismen sind abhängig von der Darstellung von Anmeldeinformationen bei der Anmeldung. Allerdings verwendet, wenn der Computer nicht mit einem Domänencontroller verbunden ist, und der Benutzer wird Domänenanmeldeinformationen darstellen, Windows den Prozess der zwischengespeicherten Anmeldeinformationen in der Überprüfung Mechanismus.

Jedes Mal, wenn ein Benutzer zu einer Domäne anmeldet Windows die Anmeldeinformationen zwischenspeichert und speichert sie in der Struktur "Security" in der Registrierung des Betriebssystems.

Mit zwischengespeicherten Anmeldeinformationen kann der Benutzer anmelden Mitglied einer Domäne ohne eine Verbindung zu einem Domänencontroller in dieser Domäne.


## <a name="BKMK_CredentialStorageAndValidation"></a>Überprüfung und Speicherung von Anmeldeinformationen
Es ist nicht immer wünschenswert sein, einen Satz von Anmeldeinformationen für den Zugriff auf andere Ressourcen zu verwenden. Beispielsweise kann ein Administrator verwenden möchten administrative anstatt Benutzeranmeldeinformationen beim Zugriff auf einen Remoteserver. Wenn ein Benutzer, externe Ressourcen, z.B. ein Bankkonto zugreift, können er nur Anmeldeinformationen auch, die Anmeldeinformationen für die Domäne unterscheiden. Die folgenden Abschnitte beschreiben die Unterschiede in der Verwaltung von Anmeldeinformationen zwischen der aktuellen Versionen von Windows-Betriebssysteme sowie die Betriebssysteme Windows Vista und Windows XP.

### <a name="remote-logon-credential-processes"></a>Remoteanmeldung Anmeldeinformationen-Prozesse
Die RDP (Remotedesktopprotokoll) verwaltet die Anmeldeinformationen des Benutzers, der über den Remotedesktopclient, die in Windows8 eingeführt wurde mit einem Remotecomputer her. In dem der Host versucht, den Authentifizierungsvorgang auszuführen und, wenn dies erfolgreich war, verbindet sich der Benutzer auf die zugelassenen Ressourcen, werden die Anmeldeinformationen in Klartext an den Zielhost gesendet. RDP speichert nicht die Anmeldeinformationen auf dem Client, aber die Anmeldeinformationen des Benutzers Domäne in LSASS gespeichert sind.

In Windows Server2012 R2 und Windows8.1 eingeführt wurde, bietet eingeschränkten Administratormodus zusätzliche Sicherheit für Remoteanmeldung Szenarien. Dieser Modus von Remotedesktop führt dazu, dass die Client-Anwendung eine Netzwerk-Anmeldung NTLM-mit unidirektionalen NT-Funktion (NTOWF) oder ein Kerberos-Dienstticket verwenden, bei der Authentifizierung mit dem Remotehost. Nachdem der Administrator authentifiziert wurde, besitzt der Administrator die entsprechenden Anmeldeinformationen im LSASS keine da sie nicht mit dem Remotehost angegeben wurden. In diesem Fall hat der Administrator die Kontoanmeldeinformationen für den Computer für die Sitzung. Aktionen durchgeführt werden, als das Computerkonto der Administratoranmeldeinformationen nicht mit dem Remotehost angegeben werden. Ressourcen sind auch auf das Computerkonto beschränkt, und der Administrator Ressourcen mit seinem eigenen Konto kann nicht zugegriffen werden.

### <a name="automatic-restart-sign-on-credential-process"></a>Automatischen Neustart anmelden Credential-Prozess
Wenn ein Benutzer auf einem Windows8.1-Gerät anmeldet, speichert LSA die Anmeldeinformationen des Benutzers im verschlüsselten Speicher, die nur über LSASS.exe zugegriffen werden kann. Wenn Windows Update einen automatischen Neustart ohne Benutzeranwesenheit initiiert, werden diese Anmeldeinformationen verwendet, so konfigurieren Sie die automatische Anmeldung für den Benutzer.

Beim Neustart wird der angemeldete Benutzer wird automatisch über den Mechanismus für die automatische Anmeldung, und klicken Sie dann der Computer außerdem zum Schutz der Sitzung des Benutzers gesperrt ist. Das Sperren wird über Windows-Anmeldung initiiert, während die Verwaltung von Anmeldeinformationen von LSA ausgeführt wird. Automatisch anmelden, und Sperren die Sitzung des Benutzers auf der Konsole die Anwendungen des Benutzers gesperrten Bildschirm ist Neustart und Verfügbarkeit.

Weitere Informationen zu nach einem, finden Sie unter [Winlogon automatischen Neustart anmelden & 40; Nach einem & 41;](winlogon-automatic-restart-sign-on-arso.md).

### <a name="stored-user-names-and-passwords-in-windows-vista-and-windows-xp"></a>Gespeicherte Benutzernamen und Kennwörter in Windows Vista und Windows XP
In Windows Server2008, Windows Server2003, Windows Vista und Windows XP **gespeicherte Benutzernamen und Kennwörter** in der Systemsteuerung vereinfacht die Verwaltung und Verwendung von mehrere Sätze von Anmeldeinformationen, z.B. x. 509-Zertifikate für Smartcards und Windows Live-Anmeldeinformationen (jetzt als "Microsoft-Konto" bezeichnet). Die Anmeldeinformationen – Teil des Benutzerprofils – werden gespeichert, bis Sie benötigt. Diese Aktion kann die Sicherheit auf einer pro Ressourcenbasis erhöhen, sicherstellen, dass ein Kennwort gefährdet ist, sie nicht alle Sicherheit beeinträchtigt wird.

Nachdem ein Benutzer anmeldet und versucht, den Zugriff auf kennwortgeschützte Ressourcen, z.B. eine Freigabe auf einem Server, und wenn Standard-Anmeldeinformationen des Benutzers zugreifen, nicht ausreichen **gespeicherte Benutzernamen und Kennwörter** abgefragt wird. Wenn Sie alternative Anmeldeinformationen mit den richtigen Anmeldeinformationen in gespeichert haben **gespeicherte Benutzernamen und Kennwörter**, die Anmeldeinformationen für den Zugriff verwendet werden. Andernfalls wird der Benutzer aufgefordert, neue Anmeldeinformationen angeben, der für die Wiederverwendung, weiter unten in der Sitzung oder während einer nachfolgenden Sitzung gespeichert werden können.

Die folgenden Einschränkungen gelten:

-   Wenn **gespeicherte Benutzernamen und Kennwörter** oder ungültige Anmeldeinformationen enthält, für eine bestimmte Ressource, die Zugriff auf die Ressource verweigert wird, und die **gespeicherte Benutzernamen und Kennwörter** Dialogfeld nicht angezeigt.

-   **Gespeicherte Benutzernamen und Kennwörter** speichert Anmeldeinformationen nur für NTLM, Kerberos-Protokoll, Microsoft-Konto (früher Windows Live ID) und Secure Sockets Layer (SSL)-Authentifizierung. Einige Versionen von Internet Explorer verwalten ihre eigenen Cache für die Standardauthentifizierung.

Diese Anmeldeinformationen werden eine verschlüsselte lokale Profil eines Benutzers in der \Documents und Pfadwert Data\Microsoft\Credentials Verzeichnis. Daher können diese Anmeldeinformationen mit der Benutzer übertragen, wenn der Benutzer Netzwerkrichtlinie servergespeicherte Benutzerprofile unterstützt. Allerdings hat der Benutzer Kopien **gespeicherte Benutzernamen und Kennwörter** auf zwei verschiedenen Computern und ändert die Anmeldeinformationen, die die Ressource auf einem dieser Computer zugeordnet sind die Änderung nicht weitergegeben **gespeicherte Benutzernamen und Kennwörter** auf dem zweiten Computer.

### <a name="windows-vault-and-credential-manager"></a>Windows-Tresor und Anmeldeinformations-Manager
Anmeldeinformations-Manager wurde in Windows Server2008 R2 und Windows7 eingeführt, als der Systemsteuerung Feature zum Speichern und Verwalten von Benutzernamen und Kennwörter. Anmeldeinformations-Manager ermöglicht Benutzern das Speichern von Anmeldeinformationen für andere Systeme und Websites in einem sicheren Schließfach für Windows. Einige Versionen von Internet Explorer verwenden Sie dieses Feature für die Authentifizierung auf Websites.

Verwaltung von Anmeldeinformationen mithilfe der Anmeldeinformationsverwaltung wird durch den Benutzer auf dem lokalen Computer gesteuert. Benutzer können speichern und Anmeldeinformationen von unterstützten Browsern und Windows-Desktopanwendungen bequemes muss auf diese Ressourcen anmelden. Anmeldeinformationen werden auf dem Computer mit dem Profil des Benutzers in speziellen verschlüsselten Ordnern gespeichert. Anwendungen, die dieses Feature (durch die Verwendung von Anmeldinformationsverwaltungs-APIs), wie Webbrowsern und Apps zu unterstützen, können die richtigen Anmeldeinformationen auf anderen Computern und Websites während des Anmeldevorgangs darstellen.

Wenn eine Website, eine Anwendung oder einem anderen Computer Anforderung der Authentifizierung über NTLM oder Kerberos-Protokoll, ein Dialogfeld angezeigt wird in der Auswahl der **Standardanmeldeinformationen aktualisieren** oder **Kennwort speichern** Kontrollkästchen. Dieses Dialogfeld, in dem einen Benutzer Anmeldeinformationen lokal speichern kann, wird von einer Anwendung generiert, die die Anmeldinformationsverwaltungs-APIs unterstützt. Wenn der Benutzer wählt die **Kennwort speichern** Kontrollkästchen, Anmeldeinformations-Manager hält den Überblick über den Benutzernamen, Kennwort, und Informationen für den Authentifizierungsdienst, der verwendet wird.

Der Dienst verwendet wird, das nächste Mal Anmeldeinformations-Manager stellt automatisch bereit, die Anmeldeinformationen, die in der Windows-Tresor gespeichert ist. Wenn es nicht akzeptiert wird, wird der Benutzer die richtigen Informationen aufgefordert. Wenn der Zugriff mit den neuen Anmeldeinformationen gewährt wird, wird Anmeldeinformations-Manager überschreibt die vorherige Anmeldeinformationen mit dem neuen Konto und speichert die neue Anmeldeinformationen in der Windows-Tresor.

## <a name="BKMK_SAM"></a>SAM-Datenbank
Die Sicherheitskontenverwaltung (SAM) ist eine Datenbank, die lokale Benutzerkonten und Gruppen gespeichert. In jedem Windows-Betriebssystem vorhanden ist. Wenn ein Computer einer Domäne angehört, verwaltet Active Directory jedoch Domänenkonten in Active Directory-Domänen.

Z.B. Teilnahme an Clientcomputern, die mit einem Windows-Betriebssystem einer Netzwerkdomäne durch Kommunikation mit einem Domänencontroller, auch wenn kein Benutzer angemeldet ist. Um die Kommunikation initiieren können, muss der Computer ein aktives Konto in der Domäne verfügen. Vor der Annahme von Verbindungen mit dem Computer, auf dem Domänencontroller authentifiziert die Identität des Computers und dann Sicherheitskontext des Computers erstellt, wie es für einen menschlichen Sicherheitsprinzipal. Dieser Sicherheitskontext definiert die Identität und die Funktionen von einem Benutzer oder Dienst auf einem bestimmten Computer oder Benutzer, Dienst oder Computer in einem Netzwerk. Definiert beispielsweise das Zugriffstoken, das den Sicherheitskontext enthaltenen Ressourcen (z.B. eine Dateifreigabe oder Drucker), auf die zugegriffen werden können und die Aktionen (z.B. lesen, schreiben oder ändern), die von der Prinzipal – Benutzer, Computer oder Dienst auf, die durchgeführt werden können die Ressource.

Sicherheitskontext eines Benutzers oder Computers variiert von einem Computer auf einen anderen, z.B. wenn ein Benutzer auf einem Server oder einer Arbeitsstation als der primäre Arbeitsstation des Benutzers anmeldet. Sie können auch von einer Sitzung variieren, in eine andere, z.B. wenn ein Administrator Rechte und Berechtigungen des Benutzers ändert. Darüber hinaus ist der Sicherheitskontext unterschiedliche, wenn ein Benutzer oder Computer einzeln, in einem Netzwerk oder als Teil der Active Directory-Domäne betrieben wird.

## <a name="BKMK_LocalDomainsAndTrustedDomains"></a>Lokale Domänen und vertrauenswürdigen Domänen
Wenn zwischen zwei Domänen eine Vertrauensstellung vorhanden ist, abhängig von die Authentifizierungsmechanismen für jede Domäne die Gültigkeit der Authentifizierungen von der anderen Domäne stammen. Vertraut, dass Hilfe kontrollierten Zugriff auf freigegebene Ressourcen in einer Ressourcendomäne (der vertrauenden Domäne) bereitstellen, indem sichergestellt wird, dass die eingehenden Authentifizierungsanforderungen von einer vertrauenswürdigen Zertifizierungsstelle (der vertrauenswürdigen Domäne) stammen. Auf diese Weise fungieren Vertrauensstellungen als Brücken, mit denen nur Authentifizierung Anforderungen Reise zwischen Domänen überprüft.

Wie eine bestimmte Vertrauensstellung Authentifizierungsanfragen übergibt, hängt davon ab, wie es konfiguriert ist. Vertrauensstellungen können durch den Zugriff der vertrauenswürdigen Domäne auf Ressourcen in der vertrauenden Domäne eine unidirektionale oder bidirektionale werden, indem der Zugriff aus jeder Domäne auf Ressourcen in der anderen Domäne. Vertrauensstellungen sind auch in diesem Fall nur zwischen den zwei Partnerdomänen eine Vertrauensstellung besteht nicht transitiv oder transitiv in diesem Fall wird eine Vertrauensstellung auf keine weiteren Domänen, die einem der Partner vertraut.

Informationen zu Domänen- und Gesamtstruktur-Vertrauensstellungen in Bezug auf Authentifizierung finden Sie unter [der delegierten Authentifizierung und Vertrauensstellungen](https://technet.microsoft.com/library/dn169022.aspx).

## <a name="BKMK_CertificatesInWindowsAuthentication"></a>Zertifikate in der Windows-Authentifizierung
Eine public Key-Infrastruktur (PKI) ist die Kombination von Software, verschlüsselungstechnologien, Prozesse und Dienste, die eine Organisation zum Schutz der Kommunikation und Transaktionen zu ermöglichen. Die Möglichkeit einer PKI zum Sichern der Kommunikation und geschäftlichen Transaktionen basiert auf den Austausch von digitalen Zertifikaten zwischen authentifizierten Benutzern und vertrauenswürdigen Ressourcen.

Ein digitales Zertifikat ist ein elektronisches Dokument, das Informationen über die Entität, der er gehört, die Entität, der es ausgestellt wurde, eine eindeutige Seriennummer oder einige andere eindeutige Kennung, Ausstellung und Ablaufdaten und ein digitaler Fingerabdruck enthält.

Authentifizierung ist der Prozess bestimmen, ob es sich bei ein Remotehost vertrauenswürdig sind. Um die Vertrauenswürdigkeit einzurichten, muss der Remotehost eine akzeptable Clientauthentifizierungszertifikat bereitstellen.

Remote-Hosts herstellen ihre Vertrauenswürdigkeit Abrufen eines Zertifikats von einer Zertifizierungsstelle (CA). Die Zertifizierungsstelle kann, wiederum Zertifizierung von einer höheren, haben eine Vertrauenskette erstellt. Um zu bestimmen, ob ein Zertifikat vertrauenswürdig ist, muss eine Anwendung ermitteln, die Identität der Stamm-CA und festlegen, ob dieser vertrauenswürdig ist.

Ebenso muss dem Remotehost oder lokalen Computer ermitteln, ob der vom Benutzer oder der Anwendung das Zertifikat echt ist. Die vom Benutzer durch die LSA und SSPI vorgelegte Zertifikat wird für Authentizität auf dem lokalen Computer für die lokale Anmeldung, im Netzwerk oder in der Domäne über die Stores Zertifikat in Active Directory ausgewertet.

Um ein Zertifikat, Authentifizierungsdaten erzeugen können Sie Hashalgorithmen, wie z.B. Secure Hash Algorithm 1 (SHA1), durchläuft, um einen Message Digest zu erstellen. Message Digest wird dann digital signiert, mithilfe des privaten Schlüssels des Absenders nachweisen, dass der Nachrichtenhash vom Absender erstellt wurde.

> [!NOTE]
> SHA1 ist die Standardeinstellung in Windows7 und Windows Vista, jedoch wurde geändert in SHA2 in Windows8.

**Smartcard-Authentifizierung**

Smartcard-Technologie ist ein Beispiel für die zertifikatbasierte Authentifizierung. Mit einem Netzwerk mit einer Smartcard anmelden bietet eine starke Form der Authentifizierung, da Kryptografie basierende Identifizierung und mittels beim Authentifizieren eines Benutzers in einer Domäne verwendet. Active Directory-Zertifikatdienste (AD CS) enthält die kryptografischen basierende Identifizierung über die Ausstellung eines Zertifikats für jede Smartcard-Anmeldung.

Weitere Informationen zur Smartcard-Authentifizierung finden Sie unter der [technische Referenz zu Windows Smart Card](https://technet.microsoft.com/library/ff404297.aspx).

Virtuelle Smartcard-Technologie wurde in Windows8 eingeführt. Er speichert die Smartcard-Zertifikat in den PC, und klicken Sie dann mithilfe des Geräts manipulationssichere Trusted Platform Module (TPM)-Security-Chip geschützt. Auf diese Weise wird der PC tatsächlich die Smartcard die PIN des Benutzers erhalten müssen, um authentifiziert werden.

**Remote und WLAN-Authentifizierung**

Remote und Wireless-Authentifizierung ist eine weitere Technologie, die Zertifikate für die Authentifizierung verwendet. Den Internetauthentifizierungsdienst (IAS) und die VPN-Server verwenden die Extensible Authentication Protocol – Transport LevelSecurity (EAP-TLS), Protected Extensible Authentication-Protokoll (PEAP) oder Internet Protocol Security (IPsec) zertifikatbasierte Authentifizierung für viele Arten des Netzwerkzugriffs, einschließlich virtuelles privates Netzwerk (VPN) und Funkverbindungen ausführen.

Informationen über die zertifikatbasierte Authentifizierung bei Netzwerken finden Sie unter [Netzwerkzugriffsauthentifizierung und Zertifikate](https://technet.microsoft.com/library/cc759575(WS.10).aspx).

## <a name="BKMK_SeeAlso"></a>Siehe auch
[Windows-Authentifizierungskonzepte](https://technet.microsoft.com/library/d169018.aspx)


