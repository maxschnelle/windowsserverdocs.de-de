---
title: Anmeldeinformationen-Prozesse in der Windows-Authentifizierung
description: Windows Server-Sicherheit
ms.topic: article
ms.assetid: 48c60816-fb8b-447c-9c8e-800c2e05b14f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: ace3310b14a6a0ca049c30b165d40b244e042e02
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87942439"
---
# <a name="credentials-processes-in-windows-authentication"></a>Anmeldeinformationen-Prozesse in der Windows-Authentifizierung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Referenz Thema für IT-Experten wird beschrieben, wie die Windows-Authentifizierung Anmelde Informationen verarbeitet.

Bei der Verwaltung von Windows-Anmelde Informationen handelt es sich um den Prozess, mit dem das Betriebssystem die Anmelde Informationen vom Dienst oder Benutzer empfängt und diese Informationen für die zukünftige Präsentation des authentifizier enden Ziels sichert. Bei einem Computer, der einer Domäne beigetreten ist, ist das authentifizier Ende Ziel der Domänen Controller. Die Anmelde Informationen, die bei der Authentifizierung verwendet werden, sind digitale Dokumente, die die Identität des Benutzers einer Art von Echtheit zuweisen, z. b. ein Zertifikat, ein Kennwort oder eine PIN.

Standardmäßig werden Windows-Anmelde Informationen anhand der SAM-Datenbank (Security Accounts Manager) auf dem lokalen Computer oder mit Active Directory auf einem in die Domäne eingebundenen Computer über den Winlogon-Dienst überprüft. Anmelde Informationen werden über Benutzereingaben auf der Anmelde Benutzeroberfläche oder Programm gesteuert über die Anwendungsprogrammierschnittstelle (Application Programming Interface, API) erfasst, die dem authentifizier enden Ziel angezeigt werden.

Lokale Sicherheitsinformationen werden in der Registrierung unter **HKEY_LOCAL_MACHINE \Security**gespeichert. Zu den gespeicherten Informationen gehören Richtlinien Einstellungen, Standard Sicherheitswerte und Kontoinformationen, wie z. b. zwischengespeicherte Anmelde Informationen. Hier wird auch eine Kopie der SAM-Datenbank gespeichert, obwohl sie schreibgeschützt ist.

Das folgende Diagramm zeigt die erforderlichen Komponenten und die Pfade, die von den Anmelde Informationen über das System übernommen werden, um den Benutzer oder den Prozess für eine erfolgreiche Anmeldung zu authentifizieren.

![Diagramm, das die erforderlichen Komponenten und die Pfade anzeigt, die die Anmelde Informationen über das System zum Authentifizieren des Benutzers oder Prozesses für eine erfolgreiche Anmeldung benötigen.](../media/credentials-processes-in-windows-authentication/AuthN_LSA_Architecture_Client.gif)

In der folgenden Tabelle werden die einzelnen Komponenten beschrieben, mit denen Anmelde Informationen im Authentifizierungsprozess zum Zeitpunkt der Anmeldung verwaltet werden.

**Authentifizierungs Komponenten für alle Systeme**

|Komponente|BESCHREIBUNG|
|-------|--------|
|Anmelden des Benutzers|Winlogon.exe ist die ausführbare Datei, die für die Verwaltung sicherer Benutzerinteraktionen zuständig ist. Der Winlogon-Dienst initiiert den Anmeldevorgang für Windows-Betriebssysteme, indem er die von der Benutzeraktion gesammelten Anmelde Informationen auf dem sicheren Desktop (Anmelde Benutzeroberfläche) über Secur32.dll an die lokale Sicherheits Autorität (Local Security Authority, LSA) übergibt.|
|Anwendungs Anmeldung|Anwendungs-oder Dienst Anmeldungen, die keine interaktive Anmeldung erfordern. Die meisten vom Benutzer initiierten Prozesse werden mithilfe von Secur32.dll im Benutzermodus ausgeführt, während Prozesse, die beim Start initiiert werden (z. b. Dienste), mithilfe von Ksecdd.sys im Kernel Modus ausgeführt werden.<p>Weitere Informationen zum Benutzermodus und Kernel Modus finden Sie unter Anwendungen und Benutzermodus oder Dienste und Kernel Modus in diesem Thema.|
|Secur32.dll|Die Anbieter für mehrfache Authentifizierung, die die Grundlage für den Authentifizierungsprozess bilden.|
|Lsasrv.dll|Der LSA-Server Dienst, der beide Sicherheitsrichtlinien erzwingt und als Sicherheitspaket-Manager für die LSA fungiert. Die LSA enthält die Funktion "aushandeln", die das NTLM-oder Kerberos-Protokoll auswählt, nachdem ermittelt wurde, welches Protokoll erfolgreich sein soll.|
|Anbieter für Sicherheitsunterstützung|Eine Gruppe von Anbietern, die ein oder mehrere Authentifizierungsprotokolle einzeln aufrufen können. Der Standardsatz von Anbietern kann sich mit jeder Version des Windows-Betriebssystems ändern, und es können benutzerdefinierte Anbieter geschrieben werden.|
|Netlogon.dll|Die vom Anmeldedienst ausgeführten Dienste lauten wie folgt:<p>: Verwaltet den sicheren Kanal des Computers (nicht zu verwechseln mit SChannel) mit einem Domänen Controller.<br />: Übergibt die Anmelde Informationen des Benutzers über einen sicheren Kanal an den Domänen Controller und gibt die Domänen Sicherheits-IDs (SIDs) und Benutzerrechte für den Benutzer zurück.<br />: Veröffentlicht Dienst Ressourcen Einträge im Domain Name System (DNS) und verwendet DNS, um Namen in die IP-Adressen von Domänen Controllern aufzulösen.<br />: Implementiert das Replikations Protokoll auf der Grundlage von Remote Prozedur Aufruf (RPC) zum Synchronisieren von primären Domänen Controllern (PDCs) und Sicherungs Domänen Controllern (BDCs).|
|Samsrv.dll|Der Security Accounts Manager (Sam), der lokale Sicherheits Konten speichert, erzwingt lokal gespeicherte Richtlinien und unterstützt APIs.|
|Registrierung|Die Registrierung enthält eine Kopie der SAM-Datenbank, Einstellungen für lokale Sicherheitsrichtlinien, Standard Sicherheitswerte und Kontoinformationen, die nur für das System zugänglich sind.|

Dieses Thema enthält folgende Abschnitte:

-   [Eingabe der Anmelde Informationen für die Benutzeranmeldung](#BKMK_CrentialInputForUserLogon)

-   [Eingabe der Anmelde Informationen für die Anmeldung von Anwendungen und Diensten](#BKMK_CredentialInputForApplicationAndServiceLogon)

-   [Lokale Sicherheitsautorität](#BKMK_LSA)

-   [Zwischengespeicherte Anmelde Informationen und Validierung](#BKMK_CachedCredentialsAndValidation)

-   [Speicherung und Validierung von Anmelde Informationen](#BKMK_CredentialStorageAndValidation)

-   [SAM-Datenbank](#BKMK_SAM)

-   [Lokale Domänen und vertrauenswürdige Domänen](#BKMK_LocalDomainsAndTrustedDomains)

-   [Zertifikate in der Windows-Authentifizierung](#BKMK_CertificatesInWindowsAuthentication)

## <a name="credential-input-for-user-logon"></a><a name="BKMK_CrentialInputForUserLogon"></a>Eingabe der Anmelde Informationen für die Benutzeranmeldung
In Windows Server 2008 und Windows Vista wurde die Gina-Architektur (Graphical Identification and Authentication) durch ein Anmelde Informationsanbieter-Modell ersetzt, das es ermöglicht, unterschiedliche Anmelde Typen durch die Verwendung von Anmelde Kacheln aufzuzählen. Beide Modelle werden unten beschrieben.

**Grafische Identifizierungs-und Authentifizierungs Architektur**

Die Graphical Identification and Authentication (Gina)-Architektur gilt für die Betriebssysteme Windows Server 2003, Microsoft Windows 2000 Server, Windows XP und Windows 2000 Professional. In diesen Systemen erstellt jede interaktive Anmelde Sitzung eine separate Instanz des Winlogon-Diensts. Die Gina-Architektur wird in den von Winlogon verwendeten Prozessbereich geladen, empfängt und verarbeitet die Anmelde Informationen und führt die Aufrufe der Authentifizierungs Schnittstellen über LsaLogonUser durch.

Die Instanzen von Winlogon für eine interaktive Anmeldung werden in Sitzung 0 ausgeführt. Sitzung 0 hostet Systemdienste und andere kritische Prozesse, einschließlich des LSA-Prozesses (Local Security Authority, lokale Sicherheits Autorität).

Das folgende Diagramm zeigt den Anmelde Informationsprozess für Windows Server 2003, Microsoft Windows 2000 Server, Windows XP und Microsoft Windows 2000 Professional.

![Diagramm, das den Anmelde Informationsprozess für Windows Server 2003, Microsoft Windows 2000 Server, Windows XP und Microsoft Windows 2000 Professional anzeigt](../media/credentials-processes-in-windows-authentication/AuthN_GINA_Architecture.gif)

**Architektur des Anmelde Informationsanbieters**

Die Anmelde Informationsanbieter-Architektur gilt für die Versionen, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind. In diesen Systemen wurde die Eingabe Architektur der Anmelde Informationen mithilfe von Anmelde Informationsanbietern in einen erweiterbaren Entwurf geändert. Diese Anbieter werden durch die verschiedenen Anmelde Kacheln auf dem sicheren Desktop dargestellt, die eine beliebige Anzahl von Anmelde Szenarios zulassen: verschiedene Konten für denselben Benutzer und verschiedene Authentifizierungsmethoden, z. b. Kennwort, Smartcard und Biometrie.

Bei der Architektur des Anmelde Informationsanbieters startet Winlogon immer die Anmelde Benutzeroberfläche, nachdem Sie ein sicheres Ereignis für die Ereignis Ereignis Erstellung erhalten hat. Anmelde Benutzeroberfläche fragt jeden Anmelde Informationsanbieter für die Anzahl unterschiedlicher Anmelde Informationstypen ab, für die der Anbieter für die Aufzählung konfiguriert ist. Anmelde Informationsanbieter haben die Möglichkeit, eine dieser Kacheln als Standard anzugeben. Nachdem alle Anbieter Ihre Kacheln aufgezählt haben, werden Sie von der Anmelde Benutzeroberfläche dem Benutzer angezeigt. Der Benutzer interagiert mit einer Kachel, um seine Anmelde Informationen anzugeben. Die Anmelde Benutzeroberfläche übermittelt diese Anmelde Informationen zur Authentifizierung.

Anmelde Informationsanbieter sind keine Erzwingungs Mechanismen. Sie werden verwendet, um Anmelde Informationen zu erfassen und zu serialisieren. Die lokale Sicherheits Autorität und die Authentifizierungs Pakete erzwingen die Sicherheit.

Anmelde Informationsanbieter werden auf dem Computer registriert und sind für Folgendes verantwortlich:

-   Beschreiben der Anmelde Informationen, die für die Authentifizierung erforderlich sind.

-   Verarbeiten von Kommunikation und Logik mit externen Authentifizierungs stellen.

-   Verpacken von Anmelde Informationen für die interaktive und die Netzwerk Anmeldung.

Das Verpacken von Anmelde Informationen für die interaktive und Netzwerk Anmeldung schließt den Prozess der Serialisierung ein. Durch das Serialisieren von Anmelde Informationen können mehrere Anmelde Kacheln auf der Anmelde Benutzeroberfläche angezeigt werden. Aus diesem Grund kann Ihre Organisation die Anmelde Anzeige steuern, z. b. Benutzer, Zielsysteme für die Anmeldung, Zugriff vor der Anmeldung auf das Netzwerk und Richtlinien zum Sperren/Entsperren von Richtlinien durch Verwendung von angepassten Anmelde Informationsanbietern. Mehrere Anmelde Informationsanbieter können auf demselben Computer nebeneinander vorhanden sein.

Anbieter für einmaliges Anmelden (Single Sign-on, SSO) können als Standard Anmelde Informationsanbieter oder als Pre-Logon-Access-Anbieter entwickelt werden.

Jede Version von Windows enthält einen standardmäßigen Anmelde Informationsanbieter und einen standardmäßigen Pre-Logon-Access-Anbieter (PLAP), der auch als SSO-Anbieter bezeichnet wird. Der SSO-Anbieter ermöglicht es Benutzern, eine Verbindung mit einem Netzwerk herzustellen, bevor Sie sich beim lokalen Computer anmelden. Wenn dieser Anbieter implementiert ist, listet der Anbieter keine Kacheln auf der Anmelde Benutzeroberfläche auf.

Ein SSO-Anbieter sollte in den folgenden Szenarien verwendet werden:

-   **Netzwerk Authentifizierung und Computer Anmeldung werden von verschiedenen Anmelde Informationsanbietern verarbeitet.** Zu den Abweichungen dieses Szenarios gehören:

    -   Ein Benutzer hat die Möglichkeit, eine Verbindung mit einem Netzwerk herzustellen, z. b. das Herstellen einer Verbindung mit einem virtuellen privaten Netzwerk (VPN), bevor er sich beim Computer anmeldet, jedoch nicht für diese Verbindung benötigt wird.

    -   Zum Abrufen von Informationen, die während der interaktiven Authentifizierung auf dem lokalen Computer verwendet werden, ist eine Netzwerk Authentifizierung erforderlich.

    -   Auf mehrere Netzwerk Authentifizierungen folgt eines der anderen Szenarien. Ein Benutzer authentifiziert sich beispielsweise bei einem Internet Dienstanbieter (Internet Service Provider, ISP), authentifiziert sich bei einem VPN und verwendet dann seine Anmelde Informationen für das Benutzerkonto, um sich lokal anzumelden.

    -   Zwischengespeicherte Anmelde Informationen sind deaktiviert, und vor der lokalen Anmeldung ist eine Remote Zugriffs Dienste-Verbindung über VPN erforderlich, um den Benutzer zu authentifizieren.

    -   Ein Domänen Benutzer verfügt über kein lokales Konto, das auf einem in die Domäne eingebundenen Computer eingerichtet wurde, und muss vor dem Abschließen der interaktiven Anmeldung eine Remote Zugriffs Dienste-Verbindung über eine VPN-Verbindung herstellen.

-   **Netzwerk Authentifizierung und Computer Anmeldung werden vom gleichen Anmelde Informationsanbieter verarbeitet.** In diesem Szenario muss der Benutzer eine Verbindung mit dem Netzwerk herstellen, bevor er sich beim Computer anmelden kann.

**Anmelde Kachel-Enumeration**

Der Anmelde Informationsanbieter listet die Anmelde Kacheln in den folgenden Instanzen auf:

-   Für die Betriebssysteme, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind.

-   Der Anmelde Informationsanbieter listet die Kacheln für die Arbeitsstations Anmeldung auf. Der Anmelde Informationsanbieter serialisiert in der Regel Anmelde Informationen für die Authentifizierung bei der lokalen Sicherheits Autorität. Bei diesem Vorgang werden für jeden benutzerspezifische Kacheln angezeigt, die für die Zielsysteme der einzelnen Benutzer spezifisch sind.

-   Mit der Anmelde-und Authentifizierungs Architektur kann ein Benutzer Kacheln verwenden, die vom Anmelde Informationsanbieter aufgelistet werden, um eine Arbeitsstation zu entsperren. In der Regel ist der aktuell angemeldete Benutzer die Standard Kachel, aber wenn mehr als ein Benutzer angemeldet ist, werden zahlreiche Kacheln angezeigt.

-   Der Anmelde Informationsanbieter listet Kacheln als Reaktion auf eine Benutzer Anforderung auf, um Ihr Kennwort oder andere private Informationen, wie z. b. eine PIN, zu ändern. In der Regel ist der aktuell angemeldete Benutzer die Standard Kachel. Wenn jedoch mehr als ein Benutzer angemeldet ist, werden zahlreiche Kacheln angezeigt.

-   Der Anmelde Informationsanbieter listet Kacheln auf der Grundlage der serialisierten Anmelde Informationen auf, die für die Authentifizierung auf Remote Computern verwendet werden sollen. Die Benutzeroberfläche für Anmelde Informationen verwendet nicht die gleiche Instanz des Anbieters wie die Anmelde Benutzeroberfläche, die Sperre für die Arbeitsstation oder das Ändern des Kennworts. Daher können Zustandsinformationen im Anbieter zwischen Instanzen der Benutzeroberfläche für Anmelde Informationen nicht beibehalten werden. Diese Struktur ergibt eine Kachel für jede Remote Computer Anmeldung, vorausgesetzt, dass die Anmelde Informationen ordnungsgemäß serialisiert wurden. Dieses Szenario wird auch in der Benutzerkontensteuerung (User Account Control, UAC) verwendet, die dazu beiträgt, nicht autorisierte Änderungen an einem Computer zu verhindern, indem der Benutzer aufgefordert wird, Berechtigungen oder ein Administrator Kennwort einzugeben, bevor er Aktionen zulässt, die sich potenziell auf den Betrieb des Computers auswirken könnten oder Einstellungen ändern können, die andere Benutzer des Computers betreffen

Das folgende Diagramm zeigt den Anmelde Informationsprozess für die Betriebssysteme, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind.

![Diagramm, das den Anmelde Informationsprozess für die Betriebssysteme anzeigt, die in der Liste * * gilt für * * am Anfang dieses Themas angegeben sind.](../media/credentials-processes-in-windows-authentication/AuthN_CredMan_CredProv.gif)

## <a name="credential-input-for-application-and-service-logon"></a><a name="BKMK_CredentialInputForApplicationAndServiceLogon"></a>Eingabe der Anmelde Informationen für die Anmeldung von Anwendungen und Diensten
Die Windows-Authentifizierung dient zum Verwalten von Anmelde Informationen für Anwendungen oder Dienste, für die keine Benutzerinteraktion erforderlich ist. Anwendungen im Benutzermodus sind auf die Systemressourcen beschränkt, auf die Sie Zugriff haben, während Dienste uneingeschränkten Zugriff auf den Systemspeicher und externe Geräte haben können.

System Dienste und Anwendungen auf Transport Ebene greifen über die Security Support Provider-Schnittstelle (SSPI) in Windows auf einen Security Support Provider (SSP) zu, der Funktionen zum Auflisten der auf einem System verfügbaren Sicherheitspakete, zum Auswählen eines Pakets und zum Verwenden dieses Pakets zum Abrufen einer authentifizierten Verbindung bereitstellt.

Wenn eine Client/Server-Verbindung authentifiziert wird:

-   Die Anwendung auf der Clientseite der Verbindung sendet mithilfe der SSPI-Funktion Anmelde Informationen an den Server `InitializeSecurityContext (General)` .

-   Die Anwendung auf der Serverseite der Verbindung antwortet mit der SSPI-Funktion `AcceptSecurityContext (General)` .

-   Die SSPI `InitializeSecurityContext (General)` -Funktionen und `AcceptSecurityContext (General)` werden wiederholt, bis alle erforderlichen Authentifizierungs Nachrichten zur erfolgreichen oder fehlerhaften Authentifizierung ausgetauscht wurden.

-   Nachdem die Verbindung authentifiziert wurde, werden von der LSA auf dem Server Informationen vom Client verwendet, um den Sicherheitskontext zu erstellen, der ein Zugriffs Token enthält.

-   Der Server kann dann die SSPI-Funktion aufrufen `ImpersonateSecurityContext` , um das Zugriffs Token an einen Identitätswechsel Thread für den Dienst anzufügen.

**Anwendungen und Benutzermodus**

Der Benutzermodus in Windows besteht aus zwei Systemen, die e/a-Anforderungen an die entsprechenden Kernelmodustreiber übergeben können: das Umgebungs System, das Anwendungen ausführt, die für viele verschiedene Betriebssystem Typen geschrieben wurden, und das integrale System, das systemspezifische Funktionen im Namen des Umgebungs Systems betreibt.

Das integrale System verwaltet betriebssystemspezifische Funktionen im Namen des Umgebungs Systems und besteht aus einem Sicherheitssystem Prozess (LSA), einem Arbeitsstations Dienst und einem Server Dienst. Der Sicherheitssystem Prozess behandelt Sicherheits Token, erteilt oder verweigert Berechtigungen für den Zugriff auf Benutzerkonten auf der Grundlage von Ressourcen Berechtigungen, verarbeitet Anmelde Anforderungen und initiiert die Anmelde Authentifizierung und bestimmt, welche Systemressourcen das Betriebssystem überwachen muss.

Anwendungen können im Benutzermodus ausgeführt werden, in dem die Anwendung als beliebiger Prinzipal ausgeführt werden kann, einschließlich im Sicherheitskontext des lokalen Systems (System). Anwendungen können auch im Kernel Modus ausgeführt werden, in dem die Anwendung im Sicherheitskontext des lokalen Systems (System) ausgeführt werden kann.

SSPI ist über das Modul Secur32.dll verfügbar, das eine API zum Abrufen integrierter Sicherheitsdienste für Authentifizierung, Nachrichten Integrität und Nachrichten Schutz ist. Es stellt eine Abstraktions Ebene zwischen Protokollen auf Anwendungsebene und Sicherheitsprotokollen bereit. Da für verschiedene Anwendungen unterschiedliche Methoden zum identifizieren oder Authentifizieren von Benutzern und zum Verschlüsseln von Daten während der Übertragung über ein Netzwerk erforderlich sind, bietet SSPI eine Möglichkeit für den Zugriff auf DLLs (Dynamic-Link Libraries), die unterschiedliche Authentifizierungs-und Kryptografiefunktionen enthalten. Diese DLLs werden als Security Support Provider (SSPs) bezeichnet.

Verwaltete Dienst Konten und virtuelle Konten wurden in Windows Server 2008 R2 und Windows 7 eingeführt, um wichtige Anwendungen, wie z. b. Microsoft SQL Server und Internetinformationsdienste (IIS), mit der Isolation ihrer eigenen Domänen Konten bereitzustellen. gleichzeitig entfällt die Notwendigkeit, dass ein Administrator den Dienst Prinzipal Namen (SPN) und die Anmelde Informationen für diese Konten manuell verwaltet. Weitere Informationen zu diesen Features und deren Rolle bei der Authentifizierung finden Sie in der [Dokumentation zu verwalteten Dienst Konten für Windows 7 und Windows Server 2008 R2](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx) und [Übersicht über Gruppen verwaltete Dienst Konten](../group-managed-service-accounts/group-managed-service-accounts-overview.md).

**Dienste und Kernel Modus**

Obwohl die meisten Windows-Anwendungen im Sicherheitskontext des Benutzers ausgeführt werden, der Sie startet, gilt dies nicht für die Dienste. Viele Windows-Dienste, z. b. Netzwerk-und Druckdienste, werden vom Dienst Controller gestartet, wenn der Benutzer den Computer startet. Diese Dienste können als lokaler Dienst oder lokales System ausgeführt werden und werden möglicherweise weiterhin ausgeführt, nachdem sich der letzte Benutzer abgemeldet hat.

> [!NOTE]
> Dienste werden normalerweise in Sicherheits Kontexten ausgeführt, die als lokales System (System), Netzwerkdienst oder lokaler Dienst bezeichnet werden.  Windows Server 2008 R2 hat Dienste eingeführt, die unter einem verwalteten Dienst Konto ausgeführt werden, bei dem es sich um Domänen Prinzipale handelt.

Vor dem Starten eines dienstanders meldet sich der Dienst Controller mit dem Konto an, das für den Dienst bestimmt ist, und zeigt dann die Anmelde Informationen des Dienstanbieter für die Authentifizierung durch die LSA an. Der Windows-Dienst implementiert eine programmgesteuerte Schnittstelle, mit der der Service Controller-Manager den Dienst steuern kann. Ein Windows-Dienst kann automatisch gestartet werden, wenn das System gestartet oder manuell mit einem Dienst Steuerungsprogramm gestartet wird. Wenn ein Windows-Client Computer z. b. einer Domäne Beitritt, stellt der Messenger-Dienst auf dem Computer eine Verbindung mit einem Domänen Controller her und öffnet einen sicheren Kanal. Zum Abrufen einer authentifizierten Verbindung muss der Dienst über Anmelde Informationen verfügen, denen die lokale Sicherheits Autorität (LSA) des Remote Computers vertraut. Bei der Kommunikation mit anderen Computern im Netzwerk werden von der LSA die Anmelde Informationen für das Domänen Konto des lokalen Computers verwendet, ebenso wie alle anderen Dienste, die im Sicherheitskontext des lokalen Systems und des Netzwerk Diensts ausgeführt werden. Dienste auf dem lokalen Computer werden als System ausgeführt, sodass keine Anmelde Informationen für die LSA angezeigt werden müssen.

Diese Anmelde Informationen werden von der Datei Ksecdd.sys verwaltet und verschlüsselt, und es wird ein lokaler Prozedur Aufrufe in die LSA verwendet. Der Dateityp ist "drv (Driver)" und wird als SSP (Kernel Mode Security Support Provider) bezeichnet, und in den Versionen, die in der Liste **gilt für** am Anfang dieses Themas angegeben sind, ist "fps 140-2 Level 1-kompatibel".

Der Kernel Modus verfügt über Vollzugriff auf die Hardware-und Systemressourcen des Computers. Der Kernel Modus hindert benutzermodusdienste und-Anwendungen daran, auf kritische Bereiche des Betriebssystems zuzugreifen, auf die Sie keinen Zugriff haben sollen.

## <a name="local-security-authority"></a><a name="BKMK_LSA"></a>Lokale Sicherheitsautorität
Bei der lokalen Sicherheits Autorität (Local Security Authority, LSA) handelt es sich um einen geschützten System Prozess, der Benutzer auf dem lokalen Computer authentifiziert und protokolliert. Außerdem verwaltet LSA Informationen über alle Aspekte der lokalen Sicherheit auf einem Computer (diese Aspekte werden zusammen als lokale Sicherheitsrichtlinie bezeichnet) und bietet verschiedene Dienste für die Übersetzung zwischen Namen und Sicherheits-IDs (SIDs). Der Sicherheitssystem Prozess (Local Security Authority Server Service, LSASS) verfolgt die Sicherheitsrichtlinien und die Konten, die auf einem Computersystem wirksam sind.

Die LSA überprüft die Identität eines Benutzers, je nachdem, welche der folgenden beiden Entitäten das Konto des Benutzers ausgegeben hat:

-   **Lokale Sicherheits Autorität.** Die LSA kann Benutzerinformationen überprüfen, indem Sie die SAM-Datenbank (Security Accounts Manager) auf demselben Computer überprüfen. Auf allen Arbeitsstationen und Mitglieds Servern können lokale Benutzerkonten und Informationen zu lokalen Gruppen gespeichert werden. Diese Konten können jedoch nur für den Zugriff auf diese Arbeitsstation oder den Computer verwendet werden.

-   **Sicherheits Autorität für die lokale Domäne oder für eine vertrauenswürdige Domäne.** Die LSA kontaktiert die Entität, die das Konto ausgestellt hat, und fordert die Überprüfung an, dass das Konto gültig ist und die Anforderung vom Kontoinhaber stammt.

Der Subsystemdienst für die lokale Sicherheitsautorität (Local Security Authority Subsystem Service, LSASS) speichert Anmeldeinformationen für Benutzer mit aktiven Windows-Sitzungen im Arbeitsspeicher. Mit den gespeicherten Anmelde Informationen können Benutzer nahtlos auf Netzwerkressourcen wie Dateifreigaben, Exchange Server-Postfächer und SharePoint-Websites zugreifen, ohne Ihre Anmelde Informationen für jeden Remote Dienst erneut eingeben zu müssen.

LSASS kann Anmeldeinformationen in verschiedenen Formaten speichern. Diese umfassen Folgendes:

-   Reversibel verschlüsselter Nur-Text

-   Kerberos-Tickets (Ticket-Tickets (TGTs), Dienst Tickets)

-   NT-Hash

-   LAN-Manager (LM)-Hash

Wenn sich der Benutzer unter Verwendung einer Smartcard bei Windows anmeldet, speichert LSASS kein nur-Text-Kennwort, sondern speichert den entsprechenden NT-Hashwert für das Konto und die nur-Text-PIN für die Smartcard. Wenn das Kontoattribut für eine Smartcard aktiviert ist, die für die interaktive Anmeldung erforderlich ist, wird für das Konto automatisch ein zufälliger NT-Hashwert anstelle des ursprünglichen Kennworthashes generiert. Der automatisch beim Festlegen des Attributs generierte Kennworthash wird nicht geändert.

Wenn sich ein Benutzer bei einem Windows-basierten Computer mit einem Kennwort anmeldet, das mit dem LAN-Manager (LM)-Hashes kompatibel ist, ist dieser Authentifikator im Arbeitsspeicher vorhanden.

Die Speicherung von Nur-Text-Anmeldeinformationen im Arbeitsspeicher kann nicht deaktiviert werden, auch nicht, wenn die diese Informationen anfordernden Anmeldeinformationsanbieter deaktiviert sind.

Die gespeicherten Anmelde Informationen sind direkt den Anmelde Sitzungen des Subsystemdienst für die lokale Sicherheitsautorität (LSASS) zugeordnet, die nach dem letzten Neustart gestartet und nicht geschlossen wurden. LSA-Sitzungen mit gespeicherten LSA-Anmeldeinformationen werden beispielsweise erstellt, wenn ein Benutzer eine der folgenden Aktionen ausführt:

-   Meldet sich bei einer lokalen Sitzung oder einer Remotedesktopprotokoll Sitzung (RDP) auf dem Computer an.

-   Ausführen einer Aufgabe mit der Option **RunAs**

-   Ausführen eines aktiven Windows-Diensts auf dem Computer

-   Ausführen einer geplanten Aufgabe oder eines Batchauftrags

-   Ausführen einer Aufgabe auf dem lokalen Computer mithilfe eines Remoteverwaltungstools

In einigen Fällen werden die geheimen Schlüssel der LSA, bei denen es sich um geheime Daten Daten handelt, die nur für System Konto Prozesse zugänglich sind, auf dem Festplattenlaufwerk gespeichert. Einige dieser geheimen Schlüssel sind Anmeldeinformationen, die nach dem Neustart beibehalten werden müssen und verschlüsselt auf dem Festplattenlaufwerk gespeichert werden. Als geheime LSA-Schlüssel gespeicherte Anmeldeinformationen können Folgendes umfassen:

-   Konto Kennwort für das Active Directory Domain Services Konto (AD DS) des Computers

-   Kontokennwörter für auf dem Computer konfigurierte Windows-Dienste

-   Kontokennwörter für konfigurierte geplante Aufgaben

-   Kontokennwörter für IIS-Anwendungspools und -Websites

-   Kenn Wörter für Microsoft-Konten

Das Client Betriebssystem wurde in Windows 8.1 eingeführt und bietet zusätzlichen Schutz für die LSA, um das Lesen von Arbeitsspeicher und Code Injektion durch nicht geschützte Prozesse zu verhindern. Dieser Schutz erhöht die Sicherheit der Anmelde Informationen, die von der LSA gespeichert und verwaltet werden.

Weitere Informationen zu diesen zusätzlichen Schutzmaßnahmen finden Sie unter [Konfigurieren des zusätzlichen LSA-Schutzes](../credentials-protection-and-management/configuring-additional-lsa-protection.md).

## <a name="cached-credentials-and-validation"></a><a name="BKMK_CachedCredentialsAndValidation"></a>Zwischengespeicherte Anmelde Informationen und Validierung
Validierungs Mechanismen basieren auf der Präsentation von Anmelde Informationen zum Zeitpunkt der Anmeldung. Wenn der Computer jedoch von einem Domänen Controller getrennt ist und der Benutzer Domänen Anmelde Informationen präsentiert, verwendet Windows den Prozess der zwischengespeicherten Anmelde Informationen im Validierungs Mechanismus.

Jedes Mal, wenn sich ein Benutzer bei einer Domäne anmeldet, speichert Windows die angegebenen Anmelde Informationen zwischen und speichert Sie in der Sicherheitsstruktur in der Registrierung des Betriebssystems.

Mit zwischengespeicherten Anmelde Informationen kann sich der Benutzer bei einem Domänen Mitglied anmelden, ohne dass er mit einem Domänen Controller in dieser Domäne verbunden ist.


## <a name="credential-storage-and-validation"></a><a name="BKMK_CredentialStorageAndValidation"></a>Speicherung und Validierung von Anmelde Informationen
Es ist nicht immer wünschenswert, einen Satz von Anmelde Informationen für den Zugriff auf verschiedene Ressourcen zu verwenden. Beispielsweise kann ein Administrator beim Zugriff auf einen Remote Server anstelle von Benutzer Anmelde Informationen Administratorrechte verwenden. Wenn ein Benutzer auf externe Ressourcen (z. b. ein Bankkonto) zugreift, kann er auch nur Anmelde Informationen verwenden, die sich von den Anmelde Informationen der Domäne unterscheiden. In den folgenden Abschnitten werden die Unterschiede bei der Verwaltung von Anmelde Informationen zwischen aktuellen Versionen von Windows-Betriebssystemen und den Betriebssystemen Windows Vista und Windows XP beschrieben.

### <a name="remote-logon-credential-processes"></a>Remote Anmelde Informationen für Anmelde Informationen
Der Remotedesktopprotokoll (RDP) verwaltet die Anmelde Informationen des Benutzers, der mithilfe des Remotedesktop Clients, der in Windows 8 eingeführt wurde, eine Verbindung mit einem Remote Computer herstellt. Die Anmelde Informationen in Klartext werden an den Zielhost gesendet, auf dem der Host versucht, den Authentifizierungsprozess auszuführen. wenn der Benutzer erfolgreich ist, wird der Benutzer mit den zulässigen Ressourcen verbunden. RDP speichert die Anmelde Informationen nicht auf dem Client, aber die Domänen Anmelde Informationen des Benutzers werden im LSASS gespeichert.

Der eingeschränkte Administrator Modus wurde in Windows Server 2012 R2 und Windows 8.1 eingeführt und bietet zusätzliche Sicherheit für Remote Anmelde Szenarien. Dieser Modus von Remotedesktop bewirkt, dass die Client Anwendung eine Netzwerk Anmeldeaufforderung mit der unidirektionalen NT-Funktion (ntowf) ausführt oder bei der Authentifizierung beim Remote Host ein Kerberos-Dienst Ticket verwendet. Nachdem der Administrator authentifiziert wurde, verfügt der Administrator nicht über die entsprechenden Konto Anmelde Informationen in LSASS, da diese nicht für den Remote Host bereitgestellt wurden. Stattdessen verfügt der Administrator über die Anmelde Informationen des Computer Kontos für die Sitzung. Administrator Anmelde Informationen werden nicht für den Remote Host bereitgestellt, sodass Aktionen als Computer Konto ausgeführt werden. Ressourcen sind auch auf das Computer Konto beschränkt, und der Administrator kann nicht auf Ressourcen mit seinem eigenen Konto zugreifen.

### <a name="automatic-restart-sign-on-credential-process"></a>Automatischer Neustart der Anmelde Informationen für den Anmeldevorgang
Wenn ein Benutzer sich auf einem Windows 8.1 Gerät anmeldet, speichert LSA die Anmelde Informationen des Benutzers in verschlüsseltem Speicher, auf den nur LSASS.exe zugreifen kann. Wenn Windows Update einen automatischen Neustart ohne Benutzer Präsenz initiiert, werden diese Anmelde Informationen verwendet, um die automatische Anmeldung für den Benutzer zu konfigurieren.

Beim Neustart wird der Benutzer automatisch über den Authentifizierungsmechanismus angemeldet, und der Computer wird außerdem zum Schutz der Benutzersitzung gesperrt. Die Sperre wird durch Winlogon initiiert, während die Verwaltung der Anmelde Informationen von LSA erfolgt. Durch automatisches anmelden und Sperren der Sitzung des Benutzers in der-Konsole werden die Anwendungen für den Sperrbildschirm des Benutzers neu gestartet und sind verfügbar.

Weitere Informationen zu ARSO finden Sie [unter Winlogon Automatic Restart Sign-on &#40;ARSO&#41;](winlogon-automatic-restart-sign-on-arso.md).

### <a name="stored-user-names-and-passwords-in-windows-vista-and-windows-xp"></a>Gespeicherte Benutzernamen und Kenn Wörter in Windows Vista und Windows XP
In Windows Server 2008, Windows Server 2003, Windows Vista und Windows XP vereinfachen die **gespeicherten Benutzernamen und Kenn Wörter** in der Systemsteuerung die Verwaltung und Verwendung mehrerer Gruppen von Anmelde Informationen, einschließlich X. 509-Zertifikaten, die mit Smartcards und Windows Live-Anmelde Informationen verwendet werden (jetzt als Microsoft-Konto bezeichnet). Die Anmelde Informationen, die Teil des Benutzerprofils sind, werden bis zum Bedarf gespeichert. Durch diese Aktion kann die Sicherheit auf Ressourcenbasis erhöht werden, indem sichergestellt wird, dass die Sicherheit nicht beeinträchtigt wird, wenn ein Kennwort kompromittiert wird.

Wenn ein Benutzer sich anmeldet und versucht, auf zusätzliche durch Kennwort geschützte Ressourcen wie eine Freigabe auf einem Server zuzugreifen, und wenn die Standard Anmelde Informationen des Benutzers nicht ausreichen, um Zugriff zu erhalten, werden **Gespeicherte Benutzernamen und Kenn Wörter** abgefragt. Wenn Alternative Anmelde Informationen mit den richtigen Anmelde Informationen in **gespeicherten Benutzernamen und Kenn Wörtern**gespeichert wurden, werden diese Anmelde Informationen verwendet, um Zugriff zu erhalten. Andernfalls wird der Benutzer zur Angabe neuer Anmelde Informationen aufgefordert, die dann zur Wiederverwendung gespeichert werden können, entweder später in der Anmelde Sitzung oder während einer nachfolgenden Sitzung.

Es gelten folgende Einschränkungen:

-   Wenn **Gespeicherte Benutzernamen und Kenn Wörter** ungültige oder falsche Anmelde Informationen für eine bestimmte Ressource enthalten, wird der Zugriff auf die Ressource verweigert, und das Dialogfeld **Gespeicherte Benutzernamen und Kenn Wörter** wird nicht angezeigt.

-   In **gespeicherten Benutzernamen und Kenn Wörtern** werden Anmelde Informationen nur für NTLM, Kerberos-Protokoll, Microsoft-Konto (früher Windows Live ID) und Secure Sockets Layer (SSL)-Authentifizierung gespeichert. Einige Versionen von Internet Explorer behalten ihren eigenen Cache für die Standard Authentifizierung bei.

Diese Anmelde Informationen werden in das Verzeichnis "\Dokumente und einstellungen\benutzername\anwendungsdaten\microsoft\benutzername\anwendungsdaten\microsoft\anmelde Informationen" verschlüsselt. Folglich können diese Anmelde Informationen mit dem Benutzer gewechselt werden, wenn die Netzwerk Richtlinie des Benutzers Roamingbenutzerprofile unterstützt. Wenn der Benutzer jedoch Kopien von **gespeicherten Benutzernamen und Kenn Wörtern** auf zwei verschiedenen Computern aufweist und die Anmelde Informationen, die der Ressource auf einem dieser Computer zugeordnet sind, ändert, wird die Änderung nicht an die **gespeicherten Benutzernamen und Kenn Wörter** auf dem zweiten Computer weitergegeben.

### <a name="windows-vault-and-credential-manager"></a>Windows Vault und Credential Manager
Die Anmelde Informationsverwaltung wurde in Windows Server 2008 R2 und Windows 7 als System Steuerungsfunktion eingeführt, um Benutzernamen und Kenn Wörter zu speichern und zu verwalten. Mit Credential Manager können Benutzer Anmelde Informationen speichern, die für andere Systeme und Websites im sicheren Windows-Tresor relevant sind. Einige Versionen von Internet Explorer verwenden dieses Feature für die Authentifizierung bei Websites.

Die Verwaltung der Anmeldeinformationen mithilfe der Anmeldeinformationsverwaltung wird durch den Benutzer auf dem lokalen Computer gesteuert. Benutzer können Anmeldeinformationen von unterstützten Browsern und Windows-Anwendungen speichern, um ihnen das erneute Anmelden bei diesen Ressourcen zu erleichtern. Anmelde Informationen werden in speziellen verschlüsselten Ordnern auf dem Computer unter dem Profil des Benutzers gespeichert. Anwendungen, die dieses Feature unterstützen (durch Verwendung der Credential Manager-APIs), z. b. Webbrowser und apps, können während des Anmeldevorgangs anderen Computern und Websites die richtigen Anmelde Informationen zur Verfügung stellen.

Wenn eine Website, eine Anwendung oder ein anderer Computer die Authentifizierung über NTLM oder das Kerberos-Protokoll anfordert, wird ein Dialogfeld angezeigt, in dem Sie das Kontrollkästchen **Standard Anmelde Informationen aktualisieren** oder **Kennwort speichern** auswählen. Dieses Dialogfeld, in dem Benutzer Anmelde Informationen lokal speichern können, wird von einer Anwendung generiert, die die Anmelde Informationsverwaltung-APIs unterstützt. Wenn der Benutzer das Kontrollkästchen **Kennwort speichern** aktiviert, werden der Benutzername, das Kennwort und zugehörige Informationen für den verwendeten Authentifizierungsdienst von Credential Manager nachverfolgt.

Wenn der Dienst das nächste Mal verwendet wird, werden die Anmelde Informationen, die im Windows-Tresor gespeichert sind, von Anmelde Informationen Manager automatisch bereitgestellt. Werden diese nicht akzeptiert, wird der Benutzer zur Eingabe der richtigen Information für den Zugriff aufgefordert. Wenn der Zugriff mit den neuen Anmelde Informationen gewährt wird, überschreibt die Anmelde Informationsverwaltung die vorherigen Anmelde Informationen mit der neuen Anmelde Information und speichert dann die neuen Anmelde Informationen im Windows-Tresor.

## <a name="security-accounts-manager-database"></a><a name="BKMK_SAM"></a>SAM-Datenbank
Der Security Accounts Manager (Sam) ist eine Datenbank, in der lokale Benutzerkonten und-Gruppen gespeichert werden. Es ist in jedem Windows-Betriebssystem vorhanden. Wenn ein Computer jedoch einer Domäne hinzugefügt wird, verwaltet Active Directory Domänen Konten in Active Directory Domänen.

Beispielsweise werden Client Computer, auf denen ein Windows-Betriebssystem ausgeführt wird, an einer Netzwerk Domäne teilnehmen, indem Sie mit einem Domänen Controller kommunizieren, auch wenn kein Benutzer angemeldet ist. Zum Initiieren der Kommunikation muss der Computer über ein aktives Konto in der Domäne verfügen. Vor dem Akzeptieren der Kommunikation vom Computer wird die Identität des Computers von der LSA auf dem Domänen Controller authentifiziert. Anschließend wird der Sicherheitskontext des Computers genauso wie für einen Human Security Principal erstellt. Dieser Sicherheitskontext definiert die Identität und die Funktionen eines Benutzers oder Diensts auf einem bestimmten Computer, einem Benutzer, einem Dienst oder einem Computer in einem Netzwerk. Das Zugriffs Token, das im Sicherheitskontext enthalten ist, definiert z. b. die Ressourcen (z. b. eine Dateifreigabe oder einen Drucker), auf die zugegriffen werden kann, sowie die Aktionen (z. b. lesen, schreiben oder ändern), die von diesem Prinzipal ausgeführt werden können, einen Benutzer, einen Computer oder einen Dienst für diese Ressource.

Der Sicherheitskontext eines Benutzers oder Computers kann sich von einem Computer zu einem anderen unterscheiden, z. b. wenn sich ein Benutzer an einem Server oder einer anderen Arbeitsstation anmeldet, als die primäre Arbeitsstation des Benutzers. Dies kann auch von einer Sitzung zu einer anderen variieren, z. b. Wenn ein Administrator die Rechte und Berechtigungen des Benutzers ändert. Außerdem ist der Sicherheitskontext in der Regel anders, wenn ein Benutzer oder Computer eigenständig oder in einem Netzwerk oder als Teil einer Active Directory Domäne arbeitet.

## <a name="local-domains-and-trusted-domains"></a><a name="BKMK_LocalDomainsAndTrustedDomains"></a>Lokale Domänen und vertrauenswürdige Domänen
Wenn eine Vertrauensstellung zwischen zwei Domänen vorhanden ist, basieren die Authentifizierungsmechanismen für jede Domäne auf der Gültigkeit der Authentifizierungen aus der anderen Domäne. Vertrauens Stellungen unterstützen den kontrollierten Zugriff auf freigegebene Ressourcen in einer Ressourcen Domäne (die vertrauende Domäne), indem Sie überprüfen, ob eingehende Authentifizierungsanforderungen von einer vertrauenswürdigen Zertifizierungsstelle (der vertrauenswürdigen Domäne) stammen. Auf diese Weise fungieren Vertrauens Stellungen als Bridges, bei denen nur überprüfte Authentifizierungsanforderungen zwischen Domänen übertragen werden können.

Wie eine bestimmte Vertrauensstellung Authentifizierungsanforderungen übergibt, hängt von der Konfiguration ab. Vertrauens Stellungen können unidirektional sein, indem der Zugriff von der vertrauenswürdigen Domäne auf Ressourcen in der vertrauenden Domäne bereitgestellt wird (oder bidirektional), indem der Zugriff von jeder Domäne auf Ressourcen in der anderen Domäne gewährt wird. Vertrauens Stellungen sind auch nicht transitiv. in diesem Fall besteht nur eine Vertrauensstellung zwischen den beiden vertrauenswürdigen Partner Domänen oder transitiv. in diesem Fall wird eine Vertrauensstellung automatisch auf alle anderen Domänen ausgedehnt, denen beide Partner vertraut sind.

Informationen zu Domänen-und Gesamtstruktur-Vertrauens Stellungen hinsichtlich der Authentifizierung finden Sie unter [Delegierte Authentifizierung und Vertrauens](https://technet.microsoft.com/library/dn169022.aspx)Stellungen.

## <a name="certificates-in-windows-authentication"></a><a name="BKMK_CertificatesInWindowsAuthentication"></a>Zertifikate in der Windows-Authentifizierung
Bei einer Public Key-Infrastruktur (PKI) handelt es sich um eine Kombination aus Software, Verschlüsselungstechnologien, Prozessen und Diensten, mit deren Hilfe die Kommunikation und Geschäftstransaktionen einer Organisation gesichert werden können. Die Fähigkeit einer PKI zum Sichern von Kommunikation und Geschäftstransaktionen basiert auf dem Austausch digitaler Zertifikate zwischen authentifizierten Benutzern und vertrauenswürdigen Ressourcen.

Ein digitales Zertifikat ist ein elektronisches Dokument, das Informationen über die Entität enthält, zu der es gehört, die von ihm ausgegebene Entität, eine eindeutige Seriennummer oder andere eindeutige Identifikations-, Ausstellungs-und Ablaufdaten sowie einen digitalen Fingerabdruck.

Die Authentifizierung ist der Prozess, bei dem ermittelt wird, ob ein Remote Host vertrauenswürdig ist. Um seine Vertrauenswürdigkeit einzurichten, muss der Remote Host ein akzeptables Authentifizierungszertifikat bereitstellen.

Remote Hosts richten ihre Vertrauenswürdigkeit ein, indem Sie ein Zertifikat von einer Zertifizierungsstelle (Certification Authority, ca) erhalten. Die Zertifizierungsstelle kann wiederum über eine Zertifizierung von einer höheren Zertifizierungsstelle verfügen, die eine Vertrauenskette erstellt. Um zu ermitteln, ob ein Zertifikat vertrauenswürdig ist, muss eine Anwendung die Identität der Stamm Zertifizierungsstelle ermitteln und dann ermitteln, ob Sie vertrauenswürdig ist.

Ebenso muss der Remote Host oder der lokale Computer bestimmen, ob das vom Benutzer oder der Anwendung vorgelegte Zertifikat authentisch ist. Das Zertifikat, das vom Benutzer über die LSA und SSPI vorgelegt wird, wird auf dem lokalen Computer für die lokale Anmeldung, im Netzwerk oder in der Domäne über die Zertifikat Speicher in Active Directory ausgewertet.

Um ein Zertifikat zu erhalten, werden die Authentifizierungsdaten durch Hash Algorithmen, wie z. b. Secure-Hash-Algorithmus 1 (SHA1), weitergeleitet, um einen Nachrichten Digest zu erhalten. Der Nachrichten Digest wird dann mithilfe des privaten Schlüssels des Absenders digital signiert, um nachzuweisen, dass der Nachrichten Digest vom Absender erstellt wurde.

> [!NOTE]
> SHA1 ist die Standardeinstellung in Windows 7 und Windows Vista, wurde aber in Windows 8 in SHA2 geändert.

**Authentifizierung mit Smartcards**

Die Smartcard-Technologie ist ein Beispiel für eine Zertifikat basierte Authentifizierung. Die Anmeldung bei einem Netzwerk mit einer Smartcard bietet eine starke Form der Authentifizierung, da Sie eine kryptografiebasierte Identifikation und einen Nachweis des Besitzes verwendet, wenn ein Benutzer bei einer Domäne authentifiziert wird. Active Directory Zertifikat Dienste (AD CS) bieten die kryptografiebasierte Identifikation durch die Ausstellung eines Anmelde Zertifikats für jede Smartcard.

Informationen zur Smartcardauthentifizierung finden Sie in der [technischen Referenz für die Windows-Smartcard](https://technet.microsoft.com/library/ff404297.aspx).

Die Technologie für virtuelle Smartcards wurde in Windows 8 eingeführt. Er speichert das Zertifikat der Smartcard auf dem PC und schützt es dann mithilfe des Sicherheitstokendiensts für den Geräte Manipulations Trusted Platform Module (TPM). Auf diese Weise wird der PC tatsächlich zur Smartcard, die die PIN des Benutzers erhalten muss, damit Sie authentifiziert werden kann.

**Remote-und drahtlose Authentifizierung**

Die Authentifizierung von Remote-und Drahtlos Netzwerken ist eine andere Technologie, die Zertifikate für die Authentifizierung verwendet. Der Internet Authentifizierungsdienst (IAS) und die virtuellen privaten Netzwerkserver verwenden das Extensible Authentication Protocol-Transport Level Security (EAP-TLS), PEAP (Protected Extensible Authentication Protocol) oder IPSec (Internet Protocol Security), um eine Zertifikat basierte Authentifizierung für viele Arten von Netzwerk Zugriff durchzuführen, einschließlich VPN (virtuelles privates Netzwerk) und Drahtlos Verbindungen.

Informationen zur Zertifikat basierten Authentifizierung im Netzwerk finden Sie unter [Netzwerk Zugriffs Authentifizierung und-Zertifikate](https://technet.microsoft.com/library/cc759575(WS.10).aspx).

## <a name="see-also"></a><a name="BKMK_SeeAlso"></a>Siehe auch
[Windows-Authentifizierungskonzepte](https://docs.microsoft.com/windows-server/security/windows-authentication/windows-authentication-concepts)


