---
title: Sicherheitsrichtlinien für die Systemdienste in Windows Server 2016
description: Sicherheitsrichtlinien für das Deaktivieren von Diensten in Windows Server 2016 mit Desktopdarstellung
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 11/26/2018
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
author: nirb
ms.author: nirb
ms.openlocfilehash: 1a9496a121fc45df0b788ea56d50db922fd24536
ms.sourcegitcommit: 0948a1abff1c1be506216eeb51ffc6f752a9fe7e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2019
ms.locfileid: "66749449"
---
## <a name="guidance-on-disabling-system-services-on-windows-server-2016-with-desktop-experience"></a>Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung

Gilt für: Windows Server 2016

Das Windows-Betriebssystem enthält viele Systemdienste, die wichtige Funktionen bereitstellen. Dienste weisen verschiedene Start-Standardrichtlinien: Einige sind standardmäßig gestartet (automatisch), einige bei Bedarf (manuell), und einige sind standardmäßig deaktiviert und muss explizit aktiviert werden, bevor sie ausgeführt werden können. Diese Standardwerte wurden sorgfältig ausgewählt, für jeden Dienst, um Leistung, Funktionalität und Sicherheit für die typischen Kunden auszugleichen.

Allerdings einige Enterprise-Kunden bevorzugt einen Ausgleich mehr sicherheitsorientierte für ihre Windows-PCs und Servern, eine, die ihrer Angriffe reduziert Oberfläche, auf das absolute Minimum und möchten daher alle Dienste vollständig zu deaktivieren, die nicht in ihre spezifischen benötigt werden Umgebungen. Für Kunden stellt Microsoft® bereit, die zugehörige Anweisungen im Hinblick auf die Dienste für diesen Zweck deaktiviert werden können.

Die Anleitung ist nur für Windows Server 2016 mit Desktopdarstellung (es sei denn, die als Ersatz für desktop für Endbenutzer verwendet wird). Ab Windows Server-2019, werden diese Richtlinien standardmäßig konfiguriert. Jeder Dienst im System ist wie folgt kategorisiert:

-   **Sollten deaktivieren:** Eine sicherheitsorientierte Unternehmen wird in den meisten Fällen deaktivieren Sie diesen Dienst und seine Funktionalität verzichten möchten (Weitere Informationen siehe unten).
- **OK, um Sie zu deaktivieren:** Dieser Dienst bietet Funktionen, die hilfreich, einige jedoch nicht alle Unternehmen und sicherheitsorientierte Unternehmen, die sie nicht verwenden, sicher deaktivieren.
- **Deaktivieren Sie nicht:** Das Deaktivieren dieses Diensts wird die Auswirkungen auf die wesentlichen Funktionen oder verhindern, dass bestimmte Rollen oder Features ordnungsgemäß funktioniert. Es sollte daher nicht deaktiviert werden.
-  **(Keine Anleitung):** Die Auswirkungen der Deaktivierung dieser Dienste wurde nicht vollständig ausgewertet. Aus diesem Grund sollte die Standardkonfiguration dieser Dienste nicht geändert werden.


Kunden können ihre Windows-PCs und Servern, um die ausgewählten Dienste mithilfe der Vorlage für die Sicherheit in die Gruppenrichtlinien oder PowerShell-Automatisierung deaktivieren konfigurieren. In einigen Fällen enthält die Anleitung spezifische gruppenrichtlinieneinstellungen, die der integritätsdienstfunktionalität direkt als Alternative zum Deaktivieren des Diensts selbst deaktivieren.

Microsoft empfiehlt, dass Kunden die folgenden Dienste und die jeweiligen geplante Aufgaben unter Windows Server 2016 mit Desktopdarstellung deaktivieren:

Dienste: 
1. Xbox Live Auth Manager
2. Xbox Live-Spiel speichern

Geplante Aufgaben: 
1. \Microsoft\XblGameSave\XblGameSaveTask
2. \Microsoft\XblGameSave\XblGameSaveTaskLogon

(Sie können auch die Informationen für alle Dienste, die anhand der angefügten Microsoft Excel-Arbeitsblatt in diesem Artikel beschriebene zugreifen: [Anleitungen zur Deaktivierung von Systemdiensten unter WindowsServer 2016 mit Desktopdarstellung](https://msdnshared.blob.core.windows.net/media/2017/05/Service-management-WS2016.xlsx))

<br />

### <a name="disabling-services-not-installed-by-default"></a>Deaktivieren von Diensten, die nicht standardmäßig installiert

Microsoft empfiehlt für die Anwendung von Richtlinien für Dienste deaktivieren, die nicht standardmäßig installiert werden.
-  Der Dienst ist in der Regel erforderlich, wenn das Feature installiert ist. Der Dienst oder das Feature installieren, sind Administratorrechte erforderlich. Lehnen Sie die Installation von Features, nicht der Start des Diensts.
-  Der Microsoft Windows-Dienst blockiert beenden kein Administrator (oder ohne Administratorrechte in einigen Fällen) installieren Sie eine ähnliche Drittanbieter-Entsprechung, vielleicht eine mit der ein höheres Sicherheitsrisiko.
-  Eine Baseline oder einen Vergleichstest, die einen nicht standardmäßigen Windows-Dienst (z. B. W3SVC) deaktiviert werden einige Prüfer die falsche Eindruck entstehen, dass die Technologie (z. B. IIS) grundsätzlich unsicher und nie verwendet werden sollte.
-  Wenn das Feature (und Dienst) nicht installiert ist, fügt diese nur unnötige Bulk, und der Baseline und für die Überprüfung der Arbeit.

<br />
Für alle Systemdienste, die in diesem Dokument aufgeführten bieten die zwei Tabellen, die führen Sie eine Erläuterung der Spalten und Empfehlungen von Microsoft zum Aktivieren und Deaktivieren der Systemdienste in Windows Server 2016 mit Desktopdarstellung: 

<br />

### <a name="explanation-of-columns"></a>Erläuterung von Spalten

| | |
|---|---|
|**Dienstbeschreibung**|   Die Beschreibung des Dienstes, von sc.exe Qdescription.|
|**Name** |Schlüssel der Name des Diensts (intern)|
|**Installation** |Immer installiert: Dienst wird auf Server Core und Server mit Desktopdarstellung  <br /> Nur mit Desktopdarstellung: Dienst ist unter Windows Server 2016 mit Desktopdarstellung, aber ***nicht*** unter Server Core |
|**StartType**  |Starttyp des Diensts unter Windows Server 2016|
|**Empfehlung** |Microsoft-Empfehlung/Tipps zur das Deaktivieren dieses Diensts unter Windows Server 2016 in einer typischen und gut verwalteten Enterprise-Bereitstellung und, in dem der Server nicht als eine durch den Endbenutzer-desktop-Ersatz verwendet wird.|
|**Kommentare** |Zusätzliche erläuterungen|

<br />

### <a name="explanation-of-microsoft-recommendations"></a>Erläuterung der Empfehlungen von Microsoft

| | |
|---|---|
|**Deaktivieren Sie nicht** |Dieser Dienst sollte nicht deaktiviert werden|
|**OK, um deaktivieren**| Dieser Dienst kann deaktiviert werden, wenn die Funktion, die sie unterstützt nicht verwendet wird.|
|**Wurde bereits deaktiviert.**|  Dieser Dienst ist standardmäßig deaktiviert. keine Notwendigkeit, mit der Richtlinie zu erzwingen.|
|**Sollte deaktiviert werden** |Dieser Dienst sollte nie auf einem ordnungsgemäß verwalteten Enterprise-System aktiviert werden.|

<br />

In den folgenden Tabellen bieten Microsoft-Anleitung zum Deaktivieren der Systemdienste unter Windows Server 2016 mit Desktopdarstellung:

<br />

##  <a name="activex-installer-axinstsv"></a>ActiveX-Installationsprogramm (AxInstSV)

| | |
|---|---|
|   **Dienstbeschreibung** |   User Account Control-Überprüfung für die Installation von ActiveX-Steuerelemente aus dem Internet ermöglicht und Verwaltung von ActiveX-Steuerelement-Installation anhand der Gruppenrichtlinien-Einstellungen. Dieser Dienst wird bedarfsgesteuert gestartet und wenn die Installation von ActiveX-Steuerelemente deaktiviert wird, verhalten sich entsprechend Browser Standardeinstellungen.    |
|   **Name des Diensts**    |   AxInstSV    |
|   **Installation**    |   Nur mit Desktopdarstellung    |
|   **StartType**   |   Manuell  |
|   **Empfehlung**  |   OK, um deaktivieren   |
|   **Kommentare**    |   OK, deaktivieren, wenn die Funktion nicht erforderlich |


<br />

## <a name="alljoyn-router-service"></a>AllJoyn Router Service   

| | |
|---|---|
|   **Dienstbeschreibung** |   Dass AllJoyn-Nachrichten weiterleitet für die lokalen AllJoyn-Clients. Wenn dieser Dienst beendet wird werden die AllJoyn-Clients, die keine eigene gebündelte Router kann nicht ausgeführt werden. |
|   **Name des Diensts**    |   AJRouter    |
|   **Installation**    |   Nur mit Desktopdarstellung    |
|   **StartType**   |   Manuell  |
|   **Empfehlung**  | Keine allgemeinen Vorgaben       |
|   **Kommentare**    |       |
| | |

<br />

## <a name="app-readiness"></a>App-Bereitschaft

| | |
|---|---|
**Dienstbeschreibung** |   Ruft die apps zur Verwendung beim erstmaligen eines Benutzers anmelden auf diesen PC und beim Hinzufügen neuer apps bereit.
**Name des Diensts**    |   AppReadiness
**Installation**    |   Nur mit Desktopdarstellung
**StartType**   |   Manuell
**Empfehlung**  |   Deaktivieren Sie nicht
**Kommentare**    |   
| | |

<br />

##  <a name="application-identity"></a>Anwendungsidentität

| | |       
|---|---|   
**Dienstbeschreibung** |   Bestimmt, und überprüft die Identität einer Anwendung. Das Deaktivieren dieses Diensts wird verhindert, dass AppLocker erzwungen wird.
**Name des Diensts**    |   AppIDSvc
**Installation**    |   Immer installiert
**StartType**   |   Manuell
**Empfehlung**  |Keine allgemeinen Vorgaben    
**Kommentare**    |   
|||     

<br />

##  <a name="application-information"></a>Anwendungsinformationen 

| | |       
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht das Ausführen von interaktiven Anwendungen mit zusätzlichen administrativen Berechtigungen.  Wenn dieser Dienst beendet wird, können Benutzer keine Anwendungen mit den zusätzlichen administrativen Berechtigungen starten, auf die gewünschten Benutzer Aufgaben erforderlich sind.
|   **Name des Diensts**    |   Appinfo
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   Unterstützt die gleichen Desktop UAC-rechteerweiterung
|||     

<br />

##  <a name="application-layer-gateway-service"></a>Gatewaydienst auf Anwendungsebene       

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Bietet Unterstützung für Protokoll von Drittanbieter-Plug-ins für die gemeinsame Nutzung der Internetverbindung
|   **Name des Diensts**    |   ALG
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |Keine allgemeinen Vorgaben    
|   **Kommentare**    |   
|||     

<br />

##  <a name="application-management"></a>Anwendungsverwaltung      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verarbeitet die Installation sowie die Entfernung und Enumeration Anforderungen für Software, die über Gruppenrichtlinien bereitgestellt. Wenn der Dienst deaktiviert ist, werden Benutzer nicht installieren, entfernen oder Auflisten von Software, die über Gruppenrichtlinien bereitgestellt. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   AppMgmt
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="appx-deployment-service-appxsvc"></a>AppX-Bereitstellungsdienst (AppXSVC)       

| | |           
|---|---|
|   **Dienstbeschreibung** |   Bietet infrastrukturunterstützung für die Bereitstellung von Store-Anwendungen. Dieser Dienst bedarfsgesteuert gestartet wurde und deaktivierte Store-Anwendungen nicht für das System bereitgestellt werden werden und möglicherweise nicht funktionieren ordnungsgemäß.
|   **Name des Diensts**    |   AppXSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="auto-time-zone-updater"></a>Automatische Zeitzone Updater           

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Legt die Zeitzone des Systems automatisch fest.
|   **Name des Diensts**    |   tzautoupdate
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

## <a name="background-intelligent-transfer-service"></a>Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Überträgt Dateien im Hintergrund im Leerlauf befindliche Netzwerkbandbreite. Wenn der Dienst deaktiviert ist, klicken Sie dann werden alle Anwendungen, die von BITS, beispielsweise Windows Update oder MSN Explorer abhängen kann nicht automatisch heruntergeladen werden Programme und andere Informationen.
|   **Name des Diensts**    |   BITS
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          


## <a name="background-tasks-infrastructure-service"></a>Infrastruktur von Hintergrunddienst-Aufgaben      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Windows-Infrastruktur-Dienst, der steuert, welche Aufgaben im Hintergrund kann auf dem System ausgeführt.
|   **Name des Diensts**    |   BrokerInfrastructure
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="base-filtering-engine"></a>Basis-Engine-Filterung            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Die Base Filtering Engine (BFE) ist ein Dienst, der verwaltet die Firewall und Richtlinien für Internet Protocol Security (IPsec) und Benutzer Modus Filtern implementiert. Der BFE-Dienst anhalten oder deaktivieren reduziert der Sicherheit des Systems. Dies führt auch zu einem unvorhersehbaren Verhalten in IPSec-Management und Firewall-Anwendungen.
|   **Name des Diensts**    |   BFE
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="bluetooth-support-service"></a>Unterstützung für Bluetooth-Dienst            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Bluetooth-Dienst unterstützt die Erkennung und Zuordnung von externen Bluetooth-Geräten.  Beenden oder das Deaktivieren dieses Diensts möglicherweise bereits installierte Bluetooth-Geräten nicht ordnungsgemäß ausgeführt werden und verhindern, dass neue Geräte erkannt oder verknüpft ist.
|   **Name des Diensts**    |   bthserv
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   OK, deaktivieren, wenn Sie nicht verwendet. Einen anderen Mechanismus für das deaktivieren: https://technet.microsoft.com/library/dd252791.aspx
|||         

<br />          


## <a name="cdpusersvc"></a>CDPUserSvc           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Benutzerdienst wird für Connected Devices Platform-Szenarien verwendet werden.
|   **Name des Diensts**    |   CDPUserSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Vorlage "Benutzer"-Dienst
|||         

<br />          


##  <a name="certificate-propagation"></a>Zertifikat-Verteilung     

| | |           
|---|---|
|   **Dienstbeschreibung** |   Benutzerzertifikate und Stammzertifikate von Smartcards in Zertifikatspeicher des aktuellen Benutzers kopiert, erkennt, wenn eine Smartcard in einen Smartcardleser eingelegt wird, und bei Bedarf, die Smartcard-Minitreiber Plug & Play installiert.
|   **Name des Diensts**    |   CertPropSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="client-license-service-clipsvc"></a>Client-Lizenzdienst (ClipSVC)        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet infrastrukturunterstützung für den Microsoft Store an. Dieser Dienst wird bedarfsgesteuert gestartet und wenn deaktivierte Anwendungen gekauft mithilfe von Microsoft Store wird nicht mehr ordnungsgemäß funktionieren.
|   **Name des Diensts**    |   ClipSVC
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="cng-key-isolation"></a>CNG-Schlüssel-Isolation

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Die CNG-Schlüsselisolationsdienst wird im LSA-Prozess gehostet. Der Dienst bietet schlüsseländerung Isolierung zur Einschränkung des privaten Schlüssel und die zugehörigen kryptografische Vorgänge wie die Common Criteria erforderlich. Der Dienst speichert und langlebige Schlüssel in ein sicheres Verfahren, die Einhaltung der Common Criteria-Anforderungen verwendet.
|   **Name des Diensts**    |   KeyIso
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="com-event-system"></a>COM+-Ereignissystem       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Unterstützt System Event Notification Service (SENS), die automatische Verteilung von Ereignissen zum Abonnieren von Component Object Model (COM) Komponenten bereitstellt. Wenn der Dienst beendet wird, wird SENS geschlossen, und ist nicht möglich, an- und Abmeldung Benachrichtigungen bereitzustellen. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   EventSystem
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="com-system-application"></a>COM+-Anwendung     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet die Konfiguration und Überwachung von Component Object Model (COM)-basierten Komponenten. Wenn der Dienst wird beendet, die meisten COM+-basierte Komponenten nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   COMSysApp
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="computer-browser"></a>Computer-Browser        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Enthält eine aktualisierte Liste der Computer im Netzwerk, und sendet diese Liste auf Computern, die als Browser. Wenn dieser Dienst beendet wird, wird diese Liste nicht aktualisiert oder verwaltet werden. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   Browser
|   **Installation**    |   Immer installiert
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

## <a name="connected-devices-platform-service"></a>Plattform-Dienst für verbundene Geräte       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst wird für Szenarien mit verbundenen Geräten und universelle Glass verwendet.
|   **Name des Diensts**    |   CDPSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="connected-user-experiences-and-telemetry"></a>Verbundene Benutzererfahrung und Telemetrie     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der verbundene Benutzererfahrung und Telemetrie-Dienst ermöglicht Funktionen, die in der Anwendung verbundenen Benutzerfunktionalität zu unterstützen. Dieser Dienst darüber hinaus verwaltet, die das ereignisgesteuerte Sammlung und Übermittlung von Diagnose- und Nutzungsdaten Informationen (zur Verbesserung der benutzerfreundlichkeit und Qualität der Windows-Plattform) bei der Diagnose und Nutzung von datenschutzeinstellungen für Option unter aktiviert sind Feedback und Diagnose.
|   **Name des Diensts**    |   DiagTrack
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="contact-data"></a>Wenden Sie sich an Daten        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Indizes erhalten Sie Daten schnell Kontakt suchen. Wenn Sie beenden oder deaktivieren Sie diesen Dienst, aus den Suchergebnissen fehlen möglicherweise Kontakte.
|   **Name des Diensts**    |   PimIndexMaintenanceSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Vorlage "Benutzer"-Dienst
|||         

<br />          

## <a name="coremessaging"></a>CoreMessaging            

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Verwaltet die Kommunikation zwischen Komponenten des Informationssystems.
|   **Name des Diensts**    |   CoreMessagingRegistrar
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="credential-manager"></a>Anmeldeinformationsverwaltung           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt sicher speichern und Abrufen von Anmeldeinformationen für Benutzer, Anwendungen und Sicherheitspakete der Dienst bereit.
|   **Name des Diensts**    |   VaultSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="cryptographic-services"></a>Kryptografische Dienste           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt drei Management-Dienste bereit: Katalogsichten von Datenbank-Dienst, der bestätigt der Signatures von Windows-Dateien, und neue Programme installiert werden können; Root-Dienst, der hinzugefügt und entfernt Zertifikate für vertrauenswürdige Stammzertifikate von Zertifizierungsstellen auf diesem Computer wird geschützt. und automatische Root Certificate Updatedienst, der Stammzertifikate von Windows-Update abgerufen, und ermöglichen Szenarien wie SSL. Wenn dieser Dienst beendet wird, werden diese Management-Dienste möglicherweise nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   CryptSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="data-sharing-service"></a>Datendienst-Freigabe         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt Daten Vermittlung zwischen Anwendungen.
|   **Name des Diensts**    |   DsSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="datacollectionpublishingservice"></a>DataCollectionPublishingService          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der DCP (Datensammlung und das Veröffentlichen)-Dienst unterstützt die Erstanbieter-apps zum Hochladen von Daten in die cloud.
|   **Name des Diensts**    |   DcpSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="dcom-server-process-launcher"></a>DCOM-Prozess-Startprogramm         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der DCOMLAUNCH-Dienst wird gestartet, COM- und DCOM-Server als Antwort auf aktivierungsanforderungen Objekt. Wenn dieser Dienst beendet oder deaktiviert ist, werden mithilfe von COM, oder DCOM Programme nicht ordnungsgemäß. Es wird dringend empfohlen, dass der DCOMLAUNCH-Dienst ausgeführt werden.
|   **Name des Diensts**    |   DcomLaunch
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  |Keine allgemeinen Vorgaben    
|   **Kommentare**    |   
|||         

<br />

##  <a name="device-association-service"></a>Gerätezuordnungsdienst      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktiviert die Kopplung zwischen dem System und verkabelten oder drahtlosen Geräte.
|   **Name des Diensts**    |   DeviceAssociationService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />

##  <a name="device-install-service"></a>Gerät installieren von Service

| | |
|---|---|
|   **Dienstbeschreibung** |   Ermöglicht es einem Computer zu erkennen und übernehmen auf hardwareänderungen, mit nur wenig oder keine Benutzereingaben aus. Beenden oder das Deaktivieren dieses Diensts führt zur Instabilität des Systems.
|   **Name des Diensts**    |   DeviceInstall
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben
|   **Kommentare**    |
|||

<br />          

##  <a name="device-management-enrollment-service"></a>Registrierungsdienst für Netzwerkgeräte Management        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Führt Aktivitäten der Registrierung für die Geräteverwaltung
|   **Name des Diensts**    |   DmEnrollmentSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="device-setup-manager"></a>Setup-Geräte-Manager         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Erkennung, Download und Installation von Software im Zusammenhang mit dem Gerät. Wenn dieser Dienst deaktiviert ist, werden Geräte mit veralteter Software konfiguriert werden können, und möglicherweise nicht ordnungsgemäß ausgeführt.
|   **Name des Diensts**    |   DsmSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="devquery-background-discovery-broker"></a>Die Ermittlung Broker DevQuery-Hintergrund         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Ermöglicht apps, Geräte mit einem Task Rasterlinie ermitteln
|   **Name des Diensts**    |   DevQueryBroker
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="dhcp-client"></a>DHCP-Client          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Registriert und aktualisiert IP-Adressen und DNS-Einträge für diesen Computer. Wenn dieser Dienst beendet wird, erhalten diese Computer keine dynamische IP-Adressen und DNS-Updates. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   Dhcp
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="diagnostic-policy-service"></a>Diagnostic Policy-Dienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Den Diagnoserichtliniendienst ermöglicht problemerkennung, Problembehandlung und Lösung für das Windows-Komponenten.  Wenn dieser Dienst beendet wird, wird die Diagnose nicht mehr funktionieren.
|   **Name des Diensts**    |   DPS
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="diagnostic-service-host"></a>Diagnose-Diensthost     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Die Diagnose-Diensthost wird von den Diagnoserichtliniendienst für die Host-Diagnose verwendet, die in einem Kontext lokaler Dienst ausgeführt werden müssen.  Wenn dieser Dienst beendet wird, werden Diagnoseinformationen, die davon abhängen, nicht mehr funktionieren.
|   **Name des Diensts**    |   WdiServiceHost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="diagnostic-system-host"></a>Diagnosesystem-Host           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Diagnose Systemhost wird von den Diagnoserichtliniendienst für die Host-Diagnose verwendet, die in einem lokalen System-Kontext ausgeführt werden müssen.  Wenn dieser Dienst beendet wird, werden Diagnoseinformationen, die davon abhängen, nicht mehr funktionieren.
|   **Name des Diensts**    |   WdiSystemHost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="distributed-link-tracking-client"></a>DLT-Client            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet die Links zwischen den NTFS-Dateien auf einem Computer oder auf Computern in einem Netzwerk.
|   **Name des Diensts**    |   TrkWks
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="distributed-transaction-coordinator"></a>Distributed Transaction Coordinator     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Koordiniert Transaktionen, die mehrere Ressourcen-Manager, z. B. Datenbanken, Nachrichtenwarteschlangen und Dateisysteme umfassen. Wenn dieser Dienst beendet wird, schlägt diese Transaktionen fehl. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   MSDTC
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />  

##  <a name="dmwappushsvc"></a>dmwappushsvc        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   WAP Push-Nachricht-Routingdienst
|   **Name des Diensts**    |   dmwappushservice
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Der Dienst für Intune, Verwaltung mobiler Geräte und ähnliche Technologien und für Unified Write Filter, die auf Clientgeräten erforderlich. Für Server erforderlich nicht.
|||         

<br />      

##  <a name="dns-client"></a>DNS-Client      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der DNS-Clientdienst (dnscache) wird zum Zwischenspeichern von DNS-Namen (Domain Name System) verwendet und registriert den vollständigen Computernamen für diesen Computer. Wenn der Dienst angehalten wird, werden DNS-Namen weiterhin aufgelöst. Allerdings werden die Ergebnisse der DNS-Namensabfragen nicht zwischengespeichert werden, und der Name des Computers wird nicht registriert werden. Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden.
|   **Name des Diensts**    |   DnsCache
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="downloaded-maps-manager"></a>Heruntergeladene Maps-Manager     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Windows-Dienst für die Anwendung den Zugriff auf die heruntergeladene Zuordnungen. Dieser Dienst wird bei Bedarf gestartet von Anwendung den Zugriff auf Karten heruntergeladen. Das Deaktivieren dieses Diensts wird verhindert, dass apps den Zugriff auf Karten.
|   **Name des Diensts**    |   MapsBroker
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Deaktivieren Seitenumbrüche apps, die auf den Dienst basieren; OK, um Wenn deaktivieren, apps, die sich nicht darauf verlassen.
|||         

<br />          

## <a name="embedded-mode"></a>Eingebetteten Modus            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst eingebetteten Modus ermöglicht Szenarien, die im Zusammenhang mit Hintergrundanwendungen.  Das Deaktivieren dieses Diensts verhindert, dass Programme im Hintergrund aus aktiviert wird.
|   **Name des Diensts**    |   embeddedmode
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="encrypting-file-system-efs"></a>Verschlüsselndes Dateisystem (EFS)

| | |                   
|---|---|           
|   **Dienstbeschreibung** | Bietet die Kern-dateiverschlüsselungstechnologie zum Speichern von verschlüsselter Dateien auf NTFS-Dateisystemvolumes verwendet. Wenn dieser Dienst beendet oder deaktiviert wird, werden Anwendungen kann nicht auf verschlüsselte Dateien zuzugreifen.            
|   **Name des Diensts**  |  EFS            
|   **Installation**  |  Immer installiert           
|   **StartType**   |  Manuell           
|   **Empfehlung**  | Keine allgemeinen Vorgaben           
|   **Kommentare**   |
|||                 

<br />  

## <a name="enterprise-app-management-service"></a>Enterprise-App-Management-Dienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Verwaltung von unternehmensanwendungen.
|   **Name des Diensts**    |   EntAppSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="extensible-authentication-protocol"></a>Extensible Authentication-Protokoll           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Extensible Authentication Protocol (EAP)-Dienst bietet die Netzwerkauthentifizierung in einem solchen Szenario 802.1 x verkabelt und drahtlos, VPN- und (Network Access Protection, NAP).  EAP bietet auch die Anwendungsprogrammierschnittstellen (APIs), die durch die Clients, drahtlosen und VPN-Clients, einschließlich der während des Authentifizierungsprozesses Zugriff verwendet werden.  Wenn Sie diesen Dienst deaktivieren, wird verhindert, dass dieser Computer den Zugriff auf Netzwerke, die EAP-Authentifizierung erforderlich ist.
|   **Name des Diensts**    |   EapHost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="function-discovery-provider-host"></a>Funktionssuchanbieter-Host         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der FDPHOST-Dienst hostet die Netzwerkanbieter Ermittlung Function Discovery (FD). Diese Anbieter FD Geben Sie Netzwerk-Ermittlung für einfache Services Discovery-Protokoll (SSDP) und Webdienste - Discovery (WS-D)-Protokolls. Anhalten oder Deaktivieren des FDPHOST-Diensts wird die Netzwerkermittlung für diese Protokolle deaktiviert, wenn FD verwenden. Wenn dieser Dienst nicht verfügbar ist, werden Netzwerkgeräte oder Ressourcen kann nicht gefunden Netzwerkdienste FD verwenden und auf diese Protokolle für die Ermittlung zu verlassen.
|   **Name des Diensts**    |   fdPHost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="function-discovery-resource-publication"></a>Funktionssuche-Ressourcenveröffentlichung      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Veröffentlicht diesen Computer und Ressourcen, die an den Computer angeschlossen werden, damit diese über das Netzwerk gefunden werden können.  Wenn dieser Dienst beendet wird, Netzwerkressourcen nicht mehr veröffentlicht werden, und sie werden nicht von anderen Computern im Netzwerk ermittelt werden.
|   **Name des Diensts**    |   FDResPub
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="geolocation-service"></a>Geolocation-Dienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst überwacht den aktuellen Speicherort des Systems und Geofences (einen geografischen Standort mit zugeordneten Ereignissen) verwaltet.  Wenn Sie diesen Dienst deaktivieren, werden Anwendungen nicht verwenden oder Empfangen von Benachrichtigungen für Geolocation oder Geofences.
|   **Name des Diensts**    |   lfsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Deaktivieren Seitenumbrüche apps, die auf den Dienst basieren; OK, um Wenn deaktivieren, apps, die sich nicht darauf verlassen.
|||         

<br />          

##  <a name="group-policy-client"></a>Gruppenrichtlinienclient     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst ist verantwortlich für die Anwendung von Einstellungen, die von Administratoren für den Computer und Benutzer über die Gruppenrichtlinien-Komponente konfiguriert. Wenn der Dienst deaktiviert ist, werden die Einstellungen nicht angewendet, und Anwendungen und Komponenten werden nicht über eine Gruppenrichtlinie verwaltet werden. Alle Komponenten oder Anwendungen, die von der Gruppenrichtlinienkomponente abhängig sind möglicherweise nicht mehr funktionsfähig, wenn der Dienst deaktiviert ist.
|   **Name des Diensts**    |   gpsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          


## <a name="human-interface-device-service"></a>Eingabegerätedienst           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktiviert und die Verwendung von Abkürzungstasten auf Tastaturen, Fernbedienungen und andere Multimediageräte verwaltet. Es wird empfohlen, zu diesem Dienst ausgeführt wird.
|   **Name des Diensts**    |   hidserv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="hv-host-service"></a>HV-Hostdienst     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt eine Schnittstelle für den Hyper-V-Hypervisor Leistungsindikatoren pro Partition, für das Hostbetriebssystem bereitstellen.
|   **Name des Diensts**    |   HvHost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Leistung Enhancers für Gast-VMs. Nicht verwendete heute mit Ausnahme von explizit VMs aufgefüllt, jedoch verwendet werden, in der Application Guard
|||         

<br />          

## <a name="hyper-v-data-exchange-service"></a>Hyper-V-Datenaustauschdienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt einen Mechanismus zum Austauschen von Daten zwischen dem virtuellen Computer und dem Betriebssystem bereit, das auf dem physischen Computer ausgeführt wird.
|   **Name des Diensts**    |   vmickvpexchange
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />      

## <a name="hyper-v-guest-service-interface"></a>Hyper-V-Gastdienstschnittstelle          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt eine Schnittstelle für den Hyper-V-Host für die Interaktion mit bestimmten Diensten, die auf dem virtuellen Computer ausgeführt wird.
|   **Name des Diensts**    |   vmicguestinterface
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />  

## <a name="hyper-v-guest-shutdown-service"></a>Hyper-V-Dienst zum Herunterfahren des Gasts           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt einen Mechanismus zum Herunterfahren des Betriebssystems des virtuellen Computers über die Verwaltungsschnittstellen auf dem physischen Computer.
|   **Name des Diensts**    |   vmicshutdown
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />

## <a name="hyper-v-heartbeat-service"></a>Hyper-V Taktdienst
| | |
|---|---|
|   **Dienstbeschreibung** |   Überwacht den Zustand dieser virtuellen Maschine von einem Takt in regelmäßigen Abständen reporting. Dieser Dienst ermöglicht Ihnen die ausgeführten virtuellen Computer zu identifizieren, die keine Reaktion mehr.
|   **Name des Diensts**    |   vmicheartbeat
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||

<br />          

## <a name="hyper-v-powershell-direct-service"></a>Hyper-V-Dienst PowerShell Direct            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt einen Mechanismus zum Verwalten des virtuellen Computers mit PowerShell über VM-Sitzungen ohne ein virtuelles Netzwerk bereit.
|   **Name des Diensts**    |   vmicvmsession
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />          

## <a name="hyper-v-remote-desktop-virtualization-service"></a>Hyper-V-Remotedesktopvirtualisierungsdienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet eine Plattform für die Kommunikation zwischen den virtuellen Computer und das Betriebssystem auf dem physischen Computer ausgeführt wird.
|   **Name des Diensts**    |   vmicrdv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />          

## <a name="hyper-v-time-synchronization-service"></a>Hyper-V-Zeitsynchronisierungsdienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Synchronisiert die Systemzeit dieses virtuellen Computers mit der Systemzeit des physischen Computers.
|   **Name des Diensts**    |   vmictimesync
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />          

## <a name="hyper-v-volume-shadow-copy-requestor"></a>Hyper-V-Volumeschattenkopie-Anforderer         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Koordiniert die Kommunikation, die erforderlich sind, um die Volumeschattenkopie-Dienst zu verwenden, um Anwendungen und Daten auf diesem virtuellen Computer aus dem Betriebssystem auf dem physischen Computer sichern.
|   **Name des Diensts**    |   vmicvss
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Finden Sie unter HvHost
|||         

<br />          

## <a name="ike-and-authip-ipsec-keying-modules"></a>IKE- und AuthIP IPsec-Schlüsselerstellungsmodule          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Die IKEEXT-Diensthosts der Internetinformationsdienste (Internet Key Exchange, IKE) und Internet AuthIP (Authenticated Protocol) Schlüsselerstellungsmodule. Diese Schlüsselerstellungsmodule werden im Internet Protocol Security (IPsec) für die Authentifizierung und den Schlüsselaustausch verwendet. Die IKEEXT-Dienst anhalten oder deaktivieren wird IKE- und AuthIP Schlüsselaustausch mit Peercomputern deaktiviert. IPsec ist in der Regel für die Verwendung von IKE- oder AuthIP konfiguriert; aus diesem Grund die IKEEXT-Dienst anhalten oder Deaktivieren einer IPsec-Fehler unter Umständen, und möglicherweise die Sicherheit des Systems beeinträchtigen. Es wird dringend empfohlen, dass der IKEEXT-Dienst ausgeführt werden.
|   **Name des Diensts**    |   IKEEXT
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |    
|||         

<br />          

## <a name="interactive-services-detection"></a>Erkennung interaktiver Dienste           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Aktiviert die benutzerbenachrichtigung von Benutzereingaben für interaktive Dienste, die ermöglicht den Zugriff auf Dialogfelder, die von interaktiver Dienste erstellt werden, wenn diese angezeigt werden. Wenn dieser Dienst beendet wird, Benachrichtigungen über neue Dialogfelder werden nicht mehr funktionieren und gibt es möglicherweise nicht den Zugriff auf Dialogfelder. Wenn dieser Dienst deaktiviert ist, werden Benachrichtigungen der und Zugriff auf neue Dialogfelder nicht mehr funktionieren.
|   **Name des Diensts**    |   UI0Detect
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />  

## <a name="internet-connection-sharing-ics"></a>Gemeinsame Nutzung der Internetverbindung            

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Stellt die Netzwerkadressübersetzung, Adressierung, Name Auflösung oder der Intrusion Prevention-Dienst für ein Heim-oder Büronetzwerken Netzwerk bereit.
|   **Name des Diensts**    |   SharedAccess
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Erforderlich für Clients, die als WLAN-Hotspots und auch an beiden Enden der Miracast-Projektion verwendet. Gemeinsam genutzter Internetverbindung können blockiert werden, mit der GPO-Einstellung, die "Verbieten die Verwendung eines Internet Connection Sharing in Ihrem DNS-Domäne-Netzwerk"
|||         

<br />          

## <a name="ip-helper"></a>IP-Hilfsprogramm            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt tunnelkonnektivität mithilfe von IPv6-übergangstechnologien (6to4, ISATAP, Port-Proxy und Teredo) und IP-HTTPS bereit. Wenn dieser Dienst beendet wird, wird der Computer nicht die Vorteile für verbesserte Konnektivität verfügen, die diese Technologien bieten.
|   **Name des Diensts**    |   iphlpsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          


##  <a name="ipsec-policy-agent"></a>IPsec-Richtlinien-Agent      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Unterstützt die Internet Protocol Security (IPsec) Peer-Authentifizierung, die Datenursprungsauthentifizierung, Datenintegrität, Vertraulichkeit (Verschlüsselung), der Daten auf Netzwerkebene und replay-Schutz.  Dieser Dienst setzt die IPsec-Richtlinien, die über das IP-Sicherheitsrichtlinien-Snap-in oder des Befehlszeilentools "Netsh Ipsec" erstellt.  Wenn Sie diesen Dienst beenden, können Verbindungsprobleme auftreten, wenn Ihre Richtlinie erfordert, dass Verbindungen über IPsec verwenden.  Darüber hinaus ist die Remoteverwaltung von Windows-Firewall nicht verfügbar, wenn dieser Dienst beendet wird.
|   **Name des Diensts**    |   PolicyAgent
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />

##  <a name="kdc-proxy-server-service-kps"></a>KDC-proxyserverdienst (KPS)      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   KDC-proxyserverdienst führt auf Edgeservern an Kerberos-Proxy-Protokollnachrichten auf Domänencontrollern mit dem Unternehmensnetzwerk verbunden.
|   **Name des Diensts**    |   KPSSVC
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben    
|   **Kommentare**    |   
|||         

<br />          

## <a name="ktmrm-for-distributed-transaction-coordinator"></a>KtmRm für Distributed Transaction Coordinator            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Koordiniert Transaktionen zwischen der Distributed Transaction Coordinator (MSDTC) und den Kerneltransaktions-Manager (KTM). Wenn es nicht erforderlich ist, empfiehlt es sich, dass dieses Diensts bleiben beendet. Wenn es erforderlich ist, werden sowohl MSDTC und KTM dieser Dienst automatisch gestartet. Wenn dieser Dienst deaktiviert ist, wird MSDTC-Transaktion, die Interaktion mit einem Kernel-Ressourcen-Manager und alle Dienste, die explizit davon abhängen schlägt fehl, um zu starten.
|   **Name des Diensts**    |   KtmRm
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />

##  <a name="link-layer-topology-discovery-mapper"></a>Zuordnung für Verbindungsschicht-Topologie        

| | |       
|---|---|       
|   **Dienstbeschreibung** |   Erstellt eine Netzwerkübersicht, bestehend aus PC und Geräte Topologieinformationen (Verbindung) und Metadaten zur Beschreibung jeder PC und Geräte an.  Wenn dieser Dienst deaktiviert ist, wird die Netzwerk-Zuordnung nicht mehr ordnungsgemäß.
|   **Name des Diensts**    |   lltdsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   OK, wenn keine Abhängigkeiten von Netzwerk-Zuordnung deaktivieren
|||         

<br />

## <a name="local-session-manager"></a>Lokaler Sitzungs-Manager                    

| | |                   
|---|---|   
|   **Dienstbeschreibung** |   Core Windows-Dienst, der lokale benutzersitzungen verwaltet. Beenden oder das Deaktivieren dieses Diensts führt zur Instabilität des Systems.    
|   **Name des Diensts**    |   LSM |
|   **Installation**    |   Immer installiert    |
|   **StartType**   |   Automatic   |
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||                 

<br />                  

## <a name="microsoft-r-diagnostics-hub-standard-collector"></a>Microsoft (R)-Diagnose-Hub-Standard-Auflister         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Core Windows-Dienst, der lokale benutzersitzungen verwaltet. Beenden oder das Deaktivieren dieses Diensts führt zur Instabilität des Systems.
|   **Name des Diensts**    |   LSM
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />

## <a name="microsoft-account-sign-in-assistant"></a>Microsoft-Konto-Anmeldeassistent
| | |
|---|---|
|   **Dienstbeschreibung** |   Ermöglicht der Benutzeranmeldung durch Identitätsdienste für Microsoft-Konto. Wenn dieser Dienst beendet wird, werden Benutzer nicht auf dem Computer mit ihrem Microsoft-Konto anmelden.
|   **Name des Diensts**    |   wlidsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Microsoft-Accounts werden n/v unter Windows Server
|||

<br />          

##  <a name="microsoft-app-v-client"></a>Microsoft App-V-Client      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet die App-V-Benutzer und virtuelle Anwendungen
|   **Name des Diensts**    |   AppVClient
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

## <a name="microsoft-iscsi-initiator-service"></a>Microsoft iSCSI-Initiator-Dienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet Internet SCSI (iSCSI)-Sitzungen auf diesem Computer auf remote-iSCSI-Zielgeräte an. Wenn dieser Dienst beendet wird, wird diesem Computer nicht anmelden oder auf dem iSCSI-Ziele zugreifen können. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   MSiSCSI
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Unsere Diagnosen deuten darauf hin, dass dies sowohl Client als auch Server verwendet wird. Keine Deaktivierung dieser Vorteil.
|||         

<br />          

## <a name="microsoft-passport"></a>Microsoft Passport           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Prozessisolation für kryptografische Schlüssel verwendet, um die zugehörigen Identitätsanbieter eines Benutzers zu authentifizieren. Wenn dieser Dienst deaktiviert ist, werden alle verwendet und die Verwaltung dieser Schlüssel nicht verfügbar ist, darunter Computer anmelden und einmaligem Anmelden auf für apps und Websites. Dieser Dienst wird gestartet und automatisch beendet. Es wird empfohlen, dass Sie diesen Dienst nicht neu konfigurieren.
|   **Name des Diensts**    |   NgcSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Nach der PIN/Hello-Anmeldungen, die auf dem Server nicht unterstützt werden
|||         

<br />          

## <a name="microsoft-passport-container"></a>Microsoft Passport-Container         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet lokaler Benutzer Identitätsschlüssel verwendet, um Benutzer von Identitätsanbietern als auch virtuellen TPM-Smartcards authentifizieren. Wenn dieser Dienst deaktiviert ist, kann Identitätsschlüssel für lokale Benutzer und virtuellen TPM-Smartcards nicht zugegriffen werden. Es wird empfohlen, dass Sie diesen Dienst nicht neu konfigurieren.
|   **Name des Diensts**    |   NgcCtnrSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="microsoft-software-shadow-copy-provider"></a>Microsoft Software Schattenkopieanbieter          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet die Softwarebasierte Volumeschattenkopien vom Volumeschattenkopie-Dienst. Wenn dieser Dienst beendet wird, können keine softwarebasierten Volumeschattenkopien verwaltet werden. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   swprv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="microsoft-storage-spaces-smp"></a>Microsoft-Speicherplätze SMP         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Hostdienst für Anbieter für die Microsoft-Speicherplätze. Wenn dieser Dienst beendet oder deaktiviert ist, können keine Speicherplätze verwaltet werden.
|   **Name des Diensts**    |   smphost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Speicher-Management werden APIs ohne diesen Dienst fehl. Beispiel: "Get-WmiObject -class MSFT_Disk -Namespace Root\Microsoft\Windows\Storage".
|||         

<br />          

## <a name="nettcp-port-sharing-service"></a>Net.Tcp-Portfreigabedienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet die Möglichkeit zur Freigabe von TCP-Ports über das net.tcp-Protokoll.
|   **Name des Diensts**    |   NetTcpPortSharing
|   **Installation**    |   Immer installiert
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

## <a name="netlogon"></a>Netlogon         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Verwaltet einen sicheren Kanal zwischen diesem Computer und dem Domänencontroller zum Authentifizieren von Benutzern und Diensten. Wenn dieser Dienst beendet wird, der Computer möglicherweise nicht authentifizieren von Benutzern und Diensten und der Domänencontroller können nicht registriert werden DNS-Einträge. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   Netlogon
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="network-connection-broker"></a>Netzwerk-Verbindungsbroker            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Broker-Verbindungen, die Microsoft Store-Apps zum Empfangen von Benachrichtigungen über das Internet zu ermöglichen.
|   **Name des Diensts**    |   NcbService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

##  <a name="network-connections"></a>Netzwerkverbindungen         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet von Objekten im Netzwerk und DFÜ-Verbindungen Ordner, in dem Sie sowohl lokale Netzwerk Verbindungen und Remoteverbindungen anzeigen können.
|   **Name des Diensts**    |   NETMAN
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="network-connectivity-assistant"></a>Netzwerkkonnektivitäts-Assistent      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Enthält die DirectAccess-Benachrichtigung für UI-Komponenten
|   **Name des Diensts**    |   NcaSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />  

##  <a name="network-list-service"></a>Netzwerklistendienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Identifiziert die Netzwerke, der Computer hat eine Verbindung hergestellt, erfasst und speichert Eigenschaften für diese Netzwerke und meldet Anwendungen, wenn diese Eigenschaften zu ändern.
|   **Name des Diensts**    |   netprofm
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="network-location-awareness"></a>Network Location Awareness           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Sammelt und speichert die Konfigurationsinformationen für das Netzwerk und Programme benachrichtigt, wenn diese Informationen geändert wird. Wenn dieser Dienst beendet wird, kann die Konfigurationsinformationen nicht verfügbar sein. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   NlaSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="network-setup-service"></a>Einrichten des Netzwerk-Diensts       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Setup-Netzwerkdienst verwaltet die Installation der Netzwerktreiber und ermöglicht die Konfiguration von Netzwerkeinstellungen auf niedriger Ebene.  Wenn dieser Dienst beendet wird, wird möglicherweise alle Treiberinstallationen, die in Bearbeitung sind abgebrochen werden.
|   **Name des Diensts**    |   NetSetupSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="network-store-interface-service"></a>Network Store Interface-Dienst      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst bietet Netzwerk-Benachrichtigungen (z. B. Schnittstelle hinzufügen/löschen usw.) auf Clients im Modus für Benutzer. Beim Beenden dieses Diensts wird zum Verlust der Netzwerkkonnektivität. Wenn dieser Dienst deaktiviert ist, werden alle anderen Dienste, die explizit von diesem Dienst abhängen nicht gestartet.
|   **Name des Diensts**    |   nsi
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="offline-files"></a>Offlinedateien            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Die Offlinedateien-Dienst ausführt Wartungsarbeiten an der Offlinedateien-Cache auf Benutzerereignisse an- und Abmeldung, reagiert die Interna der öffentlichen API implementiert und sendet, die relevante Ereignisse, die daran interessiert, Offlinedateien Aktivitäten und Änderungen in den Zustand des Cache.
|   **Name des Diensts**    |   CscService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

## <a name="optimize-drives"></a>Optimieren von Laufwerken          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Können den Computer, die durch das Optimieren von Dateien auf Speichergeräten effizienter ausgeführt.
|   **Name des Diensts**    |   defragsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />

## <a name="performance-counter-dll-host"></a>Leistung-Leistungsindikator-DLL-Host         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht Remotebenutzern und 64-Bit-Prozessen, zum Abfragen von Leistungsindikatoren, die von 32-Bit-DLLs bereitgestellt. Wenn dieser Dienst beendet wird, werden nur lokale Benutzer und 32-Bit-Prozesse können Abfragen von Leistungsindikatoren, die von 32-Bit-DLLs bereitgestellt.
|   **Name des Diensts**    |   PerfHost
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben    
|   **Kommentare**    |   
|||         

<br />          

## <a name="performance-logs--alerts"></a>Leistungsprotokolle und Warnungen            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Leistungsprotokolle und Warnungen erfasst Daten von lokalen Computern oder Remotecomputern auf der Grundlage vorkonfigurierter Zeitplanparameter, klicken Sie dann schreibt die Daten in ein Protokoll oder löst eine Warnung aus. Wenn dieser Dienst beendet wird, werden keine Informationen gesammelt. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   PLA
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="phone-service"></a>Telefondienst       

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet die Telefonie-Zustand auf dem Gerät
|   **Name des Diensts**    |   PhoneSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Ein, die moderne VoIP-apps
|||         

<br />          

##      <a name="plug-and-play"></a>Plug & Play       

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht es einem Computer zu erkennen und übernehmen auf hardwareänderungen, mit nur wenig oder keine Benutzereingaben aus. Beenden oder das Deaktivieren dieses Diensts führt zur Instabilität des Systems.
|   **Name des Diensts**    |   PlugPlay
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="portable-device-enumerator-service"></a>Tragbare Geräte Enumerator-Dienst           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Erzwingt die Gruppenrichtlinie für Massenspeicher-Wechselmedien. Ermöglicht es Anwendungen, wie z. B. Windows Media Player und Image Tabellenimport-Assistenten zum übertragen und Synchronisieren von Inhalt mithilfe von Wechselmedien Massenspeicher.
|   **Name des Diensts**    |   WPDBusEnum
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="power"></a>Stromversorgung            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet Energierichtlinie und Benachrichtigungsübermittlung für Power-Richtlinie.
|   **Name des Diensts**    |   Stromversorgung
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="print-spooler"></a>Druckspooler:            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst spoolt Druckaufträge und Interaktion mit dem Drucker behandelt.  Wenn Sie diesen Dienst deaktivieren, ist Sie nicht drucken oder finden Sie unter Ihrer Drucker.
|   **Name des Diensts**    |   Spooler
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, wenn kein Druckserver oder auf einem Domänencontroller deaktiviert
|   **Kommentare**    |   Auf einem Domänencontroller fügt die Installation der DC-Rolle einen Thread für den Warteschlangendienst auf, der für die print-Bereinigung – Entfernen der veralteten Druckwarteschlange-Objekte aus Active Directory zuständig ist.  Wenn es sich bei der Spoolerdienst auf mindestens einem Domänencontroller an jedem Standort nicht ausgeführt wird, verfügt AD keine Möglichkeit, alte Warteschlangen zu entfernen, die nicht mehr vorhanden sind. https://blogs.technet.microsoft.com/askperf/2008/11/18/disabling-unnecessary-services-a-word-to-the-wise/
|||         

<br />          

##  <a name="printer-extensions-and-notifications"></a>Erweiterungen der Drucker und Benachrichtigungen        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst benutzerdefinierte Drucker Dialogfelder geöffnet, und verarbeitet Benachrichtigungen von einem Remotedruckerserver oder einen Drucker. Wenn Sie diesen Dienst deaktivieren, wird nicht Sie Drucker Erweiterungen oder Benachrichtigungen zu sehen sein.
|   **Name des Diensts**    |   PrintNotify
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um Sie zu deaktivieren, wenn keinem Druckerserver
|   **Kommentare**    |   
|||         

<br />          

##  <a name="problem-reports-and-solutions-control-panel-support"></a>Problemberichte und -Lösungen Control Panel-Unterstützung     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst bietet Unterstützung für anzeigen, senden und Löschen von Problemberichten mit auf Systemebene für die Systemsteuerung für Problemberichte und-Lösungen an.
|   **Name des Diensts**    |   wercplsupport
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="program-compatibility-assistant-service"></a>Programm-Assistenten Kompatibilitätsdienst     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst bietet Unterstützung für die Program Compatibility Assistant (PCA).  Der PCA überwacht Programme installiert und vom Benutzer ausgeführt und erkennt bekannte Kompatibilitätsprobleme. Wenn dieser Dienst beendet wird, wird der PCA nicht ordnungsgemäß.
|   **Name des Diensts**    |   PcaSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

##  <a name="quality-windows-audio-video-experience"></a>Verbessertes Audio-/Videostreaming unter Windows      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Quality Windows Audio/Video-Streaming (qWave) ist eine Netzwerkplattform für Audio Video (AV) streaming von Anwendungen im privaten IP-Netzwerken. qWave verbessert AV-streaming-Leistung und Zuverlässigkeit Leuchten Netzwerk Quality-of-Service (QoS) für AV-Anwendungen. Es bietet es sich um Mechanismen zur Zugangskontrolle, Zeit zu überwachen und erzwingen, anwendungsfeedback und Priorisierung von Datenverkehr ausführen.
|   **Name des Diensts**    |   QWAVE
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Die clientseitige QoS-Dienst
|||         

<br />          

##      <a name="radio-management-service"></a>Radio-Management-Dienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltung des Senders und Flugzeug-Modus-Dienst
|   **Name des Diensts**    |   RmSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-access-auto-connection-manager"></a>Remote Access automatisch Verbindungs-Manager            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Erstellt eine Verbindung mit einem Remotenetzwerk, wenn ein Programm auf einem remote-DNS oder NetBIOS-Name oder Adresse verweist auf.
|   **Name des Diensts**    |   RasAuto
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-access-connection-manager"></a>RAS-Verbindungsverwaltung         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet von DFÜ- und virtuelle private Netzwerkverbindungen (VPN) auf diesem Computer mit dem Internet oder anderen remote-Netzwerke. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   RasMan
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-desktop-configuration"></a>Remotedesktopkonfiguration         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Konfiguration des Remotedesktop-Remotedienst (Centers oder RDCS) ist verantwortlich für alle von Remote Desktop Services und Remotedesktop verwandte Aktivitäten zur Konfiguration und Sitzung Wartung, die SYSTEM-Kontext erfordern. Dazu gehören die temporären Ordner für die Sitzung, RD-Designs und RD-Zertifikate.
|   **Name des Diensts**    |   SessionEnv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-desktop-services"></a>Remotedesktopdienste          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht Benutzern, interaktiv mit einem Remotecomputer herzustellen. Remotedesktop und Remote Desktop Session Host-Server müssen Sie diesem Dienst abhängig.  Deaktivieren Sie die Kontrollkästchen auf der Registerkarte "Remote" des Systemsteuerungselements das System-Eigenschaften, um zu verhindern, dass die Remoteverwendung von diesem Computer.
|   **Name des Diensts**    |   TermService
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         

<br />          

##  <a name="remote-desktop-services-usermode-port-redirector"></a>Remote Desktop Anschlussumleitung für Terminaldienst-Redirector        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht die Umleitung von Druckern/Laufwerke/Ports für RDP-Verbindungen
|   **Name des Diensts**    |   UmRdpService
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Unterstützt die umleitungen der Verbindung auf dem Server.
|||         

<br />          

## <a name="remote-procedure-call-rpc"></a>Remoteprozeduraufruf (RPC)          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   RPCSS-Diensts wird der Dienststeuerungs-Manager für COM- und DCOM-Server. Es führt Aktivierungen objektanforderungen, Objekt Exporter-Tool-Lösungen und verteilte Garbagecollection für COM- und DCOM-Server. Wenn dieser Dienst beendet oder deaktiviert ist, werden mithilfe von COM, oder DCOM Programme nicht ordnungsgemäß. Es wird dringend empfohlen, dass der RPCSS-Dienst ausgeführt werden.
|   **Name des Diensts**    |   RpcSs
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="remote-procedure-call-rpc-locator"></a>Locator der Remoteprozeduraufruf-Remoteprozeduraufruf (RPC)             

| | |               
|---|---|   
|   **Dienstbeschreibung** |   In Windows 2003 und früheren Versionen von Windows verwaltet der (Remote Procedure Call, RPC) Locator-Dienst die RPC-Name-Dienstdatenbank. In Windows Vista und höheren Versionen von Windows wird dieser Dienst bietet alle Funktionen keine und für die Anwendungskompatibilität vorhanden ist.   |
|   **Name des Diensts**    |   RpcLocator  |
|   **Installation**    |   Nur mit Desktopdarstellung    |
|   **StartType**   |   Manuell  |
|   **Empfehlung**  | Keine allgemeinen Vorgaben   |
|   **Kommentare**    |       |
|||             

<br />              

## <a name="remote-registry"></a>Remoteregistrierung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht Remotebenutzern registrierungseinstellungen auf diesem Computer zu ändern. Wenn dieser Dienst beendet wird, kann die Registrierung nur von Benutzern auf diesem Computer geändert werden. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   RemoteRegistry
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         

<br />          

##  <a name="resultant-set-of-policy-provider"></a>Richtlinienergebnissatz-Richtlinienanbieter            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt einen Netzwerkdienst, der verarbeitet die Anforderungen an die Anwendung von gruppenrichtlinieneinstellungen für einen Zielbenutzer oder Computer in verschiedenen Situationen zu simulieren und die Einstellungen des Richtlinienergebnissatzes berechnet.
|   **Name des Diensts**    |   RSoPProv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |Keine allgemeinen Vorgaben    
|   **Kommentare**    |   
|||         

<br />          

## <a name="routing-and-remote-access"></a>Routing und RAS            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Routingdienste für Unternehmen im LAN und WAN-netzwerkumgebungen.
|   **Name des Diensts**    |   RemoteAccess
|   **Installation**    |   Immer installiert
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   Wurde bereits deaktiviert.
|||         

<br />          

## <a name="rpc-endpoint-mapper"></a>RPC-Endpunktzuordnung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   RPC-Schnittstellen-IDs in Transport-Endpunkte aufgelöst. Wenn dieser Dienst beendet oder deaktiviert ist, werden Programme, die mithilfe von (Remoteprozeduraufruf) Services möglicherweise nicht ordnungsgemäß.
|   **Name des Diensts**    |   RpcEptMapper
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="secondary-logon"></a>Sekundäre Anmeldung     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht das Starten von Prozessen unter alternativen Anmeldeinformationen. Wenn dieser Dienst beendet wird, werden diese Art der Anmeldung nicht verfügbar. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   Seclogon
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="secure-socket-tunneling-protocol-service"></a>Secure Socket Tunneling Protokolldienst            

| | |               
|---|---|       
|   **Dienstbeschreibung** |   Bietet Unterstützung für das Secure Socket Tunneling Protocol (SSTP) eine Verbindung mit Remotecomputern über ein VPN herstellen. Wenn dieser Dienst deaktiviert ist, werden Benutzer nicht mit SSTP auf Remoteservern zugreifen können.    |
|   **Name des Diensts**    |   SstpSvc |
|   **Installation**    |   Immer installiert    |
|   **StartType**   |   Manuell  |
|   **Empfehlung**  |   Deaktivieren Sie nicht  |
|   **Kommentare**    |   Deaktivieren Seitenumbrüche RRAS   |
|||             

<br />              

## <a name="security-accounts-manager"></a>Sicherheitskonten-Manager            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Start dieses Diensts signalisiert andere Dienste, dass der Security Accounts Manager (SAM) zum Akzeptieren von Anforderungen bereit ist.  Das Deaktivieren dieses Diensts verhindert, dass andere Dienste im System benachrichtigt wird, wenn der SAM bereit ist, der möglicherweise wiederum dazu führen, dass diese Dienste nicht ordnungsgemäß gestartet. Dieser Dienst sollte nicht deaktiviert werden.
|   **Name des Diensts**    |   SamSs
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         

<br />          

## <a name="sensor-data-service"></a>Sensor-Datendienst  

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Daten über eine Vielzahl von Sensoren
|   **Name des Diensts**    |   SensorDataService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />  

## <a name="sensor-monitoring-service"></a>Sensor-Überwachungsdienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Überwacht die verschiedenen Sensoren aus, um die Daten verfügbar machen, und passen Sie System- und Status.  Wenn dieser Dienst beendet oder deaktiviert ist, wird die anzeigehelligkeit nicht an Lichtverhältnissen anpassen. Beim Beenden dieses Diensts beeinträchtigen andere Systemfunktionen und Features ebenfalls.
|   **Name des Diensts**    |   SensrSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br /><br/>
## <a name="sensor-servicebr--br------br---strongservice-descriptionstrong----a-service-for-sensors-that-manages-different-sensors39-functionality-manages-simple-device-orientation-sdo-and-history-for-sensors-loads-the-sdo-sensor-that-reports-device-orientation-changes--if-this-service-is-stopped-or-disabled-the-sdo-sensor-will-not-be-loaded-and-so-auto-rotation-will-not-occur-history-collection-from-sensors-will-also-be-stopped"></a>Sensor-Dienst<br/>| | |<br/>|---|---|<br/>|   <strong>Dienstbeschreibung</strong> |   Ein Dienst für Sensoren, der verschiedene Sensoren verwaltet&#39; Funktionalität. Verwaltet die einfache Device Orientation (SDO) und den Verlauf für Sensoren. Lädt die SDO-Sensor, der Änderungen der bildschirmausrichtung Gerät meldet.  Wenn dieser Dienst beendet oder deaktiviert ist, der SDO Sensor wird nicht geladen werden und automatische Rotation erfolgt also keine. Verlauf der Sammlung von Sensoren wird auch beendet werden.
|   <strong>Name des Diensts</strong> |   SensorService |   <strong>Installation</strong> |   Nur mit Desktopdarstellung |   <strong>StartType</strong> |   Manuelle |   <strong>Empfehlung</strong> |   OK, um Sie zu deaktivieren |   <strong>Kommentare</strong>    |<br/>|||<br/>
<br />          

## <a name="server"></a>Server           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Unterstützt die Datei-, Druck- und named Pipes über das Netzwerk für diesen Computer freigeben. Wenn dieser Dienst beendet wird, werden diese Funktionen nicht verfügbar. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   LanmanServer
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Erforderlich für die Remoteverwaltung IPC$, SMB-Dateifreigabe
|||         

<br />          

## <a name="shell-hardware-detection"></a>Shellhardwareerkennung             

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt Benachrichtigungen für die automatische Wiedergabe Hardwareereignisse bereit.
|   **Name des Diensts**    |   ShellHWDetection
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="smart-card"></a>Smartcard           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet den Zugriff auf Smartcards, die von diesem Computer gelesen. Wenn dieser Dienst beendet wird, werden dieser Computer kann nicht gelesen werden Smartcards. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   SCardSvr
|   **Installation**    |   Immer installiert
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

## <a name="smart-card-device-enumeration-service"></a>Smartcard-Gerätedienst-Enumeration                    

| | |               
|---|---|       
|   **Dienstbeschreibung** |   Software-Device-Knoten erstellt für alle Smartcard-Lesern zugegriffen werden kann, um eine bestimmte Sitzung. Wenn dieser Dienst deaktiviert ist, werden WinRT-APIs nicht zum Auflisten von Smartcard-Lesern können.   |
|   **Name des Diensts**    |   ScDeviceEnum    |
|   **Installation**    |   Immer installiert    |
|   **StartType**   |   Manuell  |
|   **Empfehlung**  |   OK, um deaktivieren   |
|   **Kommentare**    |   Fast ausschließlich für WinRT-apps erforderlich sind    |
|||             

<br />              

## <a name="smart-card-removal-policy"></a>Entfernen des Smartcard-Richtlinie        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Lässt das System konfiguriert werden, um dem Desktop des Benutzers beim Entfernen der Smartcard sperren.
|   **Name des Diensts**    |   SCPolicySvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="snmp-trap"></a>SNMP-Trap            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Empfängt die Trap-Nachrichten von lokalen oder Remotecomputer Simple Network Management Protocol (SNMP)-Agents generiert und leitet die Nachrichten auf SNMP-Management-Programme, die auf diesem Computer ausgeführt. Wenn dieser Dienst beendet wird, erhalten die SNMP-basierte Programme auf diesem Computer keine SNMP-Trap-Nachrichten. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   SNMPTRAP
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="software-protection"></a>Softwareschutz             

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktiviert den Download, Installation und Erzwingung von Lizenzen für digitale für Windows und Windows Anwendungen. Wenn der Dienst deaktiviert ist, können das Betriebssystem und lizenzierte Anwendungen in einem Benachrichtigungsmodus ausgeführt. Es wird dringend empfohlen, nicht des softwareschutzdienstes zu deaktivieren.
|   **Name des Diensts**    |   sppsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="special-administration-console-helper"></a>Hilfsprogramm für spezielle Verwaltungskonsole        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht es Administratoren, die für den Remotezugriff von einer Eingabeaufforderung mithilfe von EMS.
|   **Name des Diensts**    |   Sacsvr
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="spot-verifier"></a>Spot-Verifier            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Potenzielle dateisystembeschädigungen wird überprüft.
|   **Name des Diensts**    |   svsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="ssdp-discovery"></a>Ermittlung von SSDP           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermittelt, vernetzten Geräten und Diensten, die die SSDP Discovery-Protokolls, z. B. UPnP-Geräte zu verwenden. Kündigt auch, SSDP-Geräte und Dienste, die auf dem lokalen Computer ausgeführt wird. Wenn dieser Dienst beendet wird, werden die SSDP-basierte Geräte nicht ermittelt werden. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   SSDPSRV
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="state-repository-service"></a>Status der Repository-Dienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt die erforderliche Infrastruktur zur Unterstützung für das Anwendungsmodell bereit.
|   **Name des Diensts**    |   StateRepository
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="still-image-acquisition-events"></a>Weiterhin Image Acquisition-Ereignisse

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Startet die Anwendungen weiterhin Image Käufen zugeordnet.
|   **Name des Diensts**    |   WiaRpc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />  

## <a name="storage-service"></a>Storage-Dienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktivieren von Diensten für speichereinstellungen und externen Speicher-Erweiterung bietet
|   **Name des Diensts**    |   StorSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="storage-tiers-management"></a>Storage Tiers Management        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Optimiert die Platzierung von Daten in die Speicherebenen für alle mehrstufigen Speicherplätzen in das System an.
|   **Name des Diensts**    |   TieringEngineService
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="superfetch"></a>SuperFetch          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet und verbessert die Leistung des Systems im Laufe der Zeit.
|   **Name des Diensts**    |   SysMain
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="sync-host"></a>Synchronisierungshost            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst synchronisiert, e-Mail, Kontakte, Kalender und verschiedene andere Benutzerdaten. E-Mail und andere Anwendungen, die diese Funktionalität hängt funktioniert nicht ordnungsgemäß, wenn dieser Dienst nicht ausgeführt wird.
|   **Name des Diensts**    |   OneSyncSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Vorlage "Benutzer"-Dienst
|||         

<br />          

## <a name="system-event-notification-service"></a>Benachrichtigungsdienst für Systemereignisse            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Systemereignisse überwacht, und benachrichtigt Abonnenten von COM+-Ereignissystem dieser Ereignisse.
|   **Name des Diensts**    |   SENS
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="system-events-broker"></a>System-Ereignisse-Broker             

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Koordiniert die Ausführung von Hintergrundaufgaben für WinRT-Anwendung. Wenn dieser Dienst beendet oder deaktiviert ist, kann keine Verarbeitung im Hintergrund ausgelöst werden.
|   **Name des Diensts**    |   SystemEventsBroker
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Trotz der Tatsache, die die Beschreibung impliziert, dass es nur für WinRT-apps ist, ist es für die aufgabenplanung, Broker-Infrastruktur-Dienst und anderen internen Komponenten erforderlich.
|||         

<br />          

## <a name="task-scheduler"></a>Aufgabenplanung           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht Benutzern das Konfigurieren und planen automatisierte Aufgaben auf diesem Computer. Der Dienst enthält außerdem mehrere Windows-System – wichtige Aufgaben. Wenn dieser Dienst beendet oder deaktiviert ist, diese Aufgaben werden nicht ausgeführt werden zu den geplanten Zeiten. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   Zeitplan
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="tcpip-netbios-helper"></a>TCP/IP-NetBIOS-Hilfsprogramm            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Unterstützung für die NetBIOS über TCP/IP (NetBT)-Dienst und den NetBIOS-namensauflösung für Clients im Netzwerk aus diesem Grund ermöglicht Benutzern zum Freigeben von Dateien, drucken, und melden Sie sich mit dem Netzwerk. Wenn dieser Dienst beendet wird, können diese Funktionen nicht verfügbar sein. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   lmhosts
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="telephony"></a>Telephony           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet Telefonie-API (TAPI)-Unterstützung für Programme, die Steuerung von Telefoniegeräten, auf dem lokalen Computer und über das LAN auf Servern, auf denen auch den Dienst ausgeführt wird.
|   **Name des Diensts**    |   TapiSrv
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Deaktivieren Seitenumbrüche RRAS
|||         

<br />          

## <a name="themes"></a>Designs           

| | |           
|---|---|
|   **Dienstbeschreibung** |   Enthält, Designverwaltung des Benutzererlebnisses.
|   **Name des Diensts**    |   Designs
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Barrierefreiheit-Designs kann nicht festgelegt werden, wenn dieser Dienst deaktiviert ist
|||         

<br />  

## <a name="tile-data-model-server"></a>Kachel "Data Model-server           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Kachelserver für kachelaktualisierungen.
|   **Name des Diensts**    |   tiledatamodelsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Starten Sie Menü unterbrochen, wenn dieser Dienst deaktiviert ist
|||         

<br />          

##  <a name="time-broker"></a>Time-Broker     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Koordiniert die Ausführung von Hintergrundaufgaben für WinRT-Anwendung. Wenn dieser Dienst beendet oder deaktiviert ist, kann keine Verarbeitung im Hintergrund ausgelöst werden.
|   **Name des Diensts**    |   TimeBrokerSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Trotz der Tatsache, die die Beschreibung impliziert, dass es nur für WinRT-apps ist, ist es für die aufgabenplanung, Broker-Infrastruktur-Dienst und anderen internen Komponenten erforderlich.
|||         

<br />          

## <a name="touch-keyboard-and-handwriting-panel-service"></a>Touch, Tastatur und Handschrift-Bereich-Dienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht das Handschrifterkennungs-Bereich und tippen Sie auf der Tastatur Stift- und Handschrifteingaben-Funktionen
|   **Name des Diensts**    |   TabletInputService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="update-orchestrator-service-for-windows-update"></a>Orchestrator-Dienst für Windows Update aktualisieren           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet die Windows-Updates. Wenn beendet, werden Ihre Geräte werden nicht zum Herunterladen und installieren die neuesten Updates.
|   **Name des Diensts**    |   UsoSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Beschreibung des Diensts konnte nicht in der v1607; Windows Update (inkl. WSUS), die diesem Dienst abhängig ist.
|||         

<br />          

## <a name="upnp-device-host"></a>Host UPnP-Geräte         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht das UPnP-Geräte, die auf diesem Computer gehostet werden. Wenn dieser Dienst beendet wird, alle gehosteten UPnP-Geräte werden nicht mehr funktioniert, und keine zusätzlichen gehosteten Geräte hinzugefügt werden können. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   upnphost
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="user-access-logging-service"></a>Dienst für die Benutzerzugriffsprotokollierung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst protokolliert eindeutigen Clientanforderungen, in Form von IP-Adressen und Namen, der installierten Produkte und Rollen auf dem lokalen Server. Diese Informationen kann, über Powershell: Administratoren müssen Clients bei Bedarf von Server-Software für die Verwaltung von offline (Client Access License, CAL) quantifizieren abgefragt werden. Wenn der Dienst deaktiviert ist, Clientanforderungen werden nicht protokolliert, und werden nicht über Powershell Abfragen abgerufen werden. Beenden des Diensts wirkt sich nicht auf das Abfragen von Verlaufsdaten (Siehe unterstützende Dokumentation für die Schritte zum Löschen von Verlaufsdaten) aus. Der lokalen Systemadministrator muss wenden Sie sich an, auffordern, Windows Server-Lizenzbedingungen zum Ermitteln von der Anzahl der Clientzugriffslizenzen, die für die Serversoftware ordnungsgemäß lizenziert werden erforderlich sind; die Benutzerzugriffsprotokollierung-Dienst verwenden und Daten ändert sich nicht auf diese Verpflichtung.
|   **Name des Diensts**    |   UALSVC
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="user-data-access"></a>Datenzugriff für Benutzer        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet apps Zugriff auf strukturierte Benutzerdaten, einschließlich von Kontaktinformationen, Kalender, Nachrichten und andere Inhalte an. Wenn Sie beenden oder deaktivieren Sie diesen Dienst, können apps, die diese Daten verwenden, nicht ordnungsgemäß.
|   **Name des Diensts**    |   UserDataSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Vorlage "Benutzer"-Dienst
|||         

<br />          

## <a name="user-data-storage"></a>Speicherung von            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verarbeitet die Speicherung von strukturierten Benutzerdaten, einschließlich von Kontaktinformationen, Kalender, Meldungen und anderen Inhalten. Wenn Sie beenden oder deaktivieren Sie diesen Dienst, können apps, die diese Daten verwenden, nicht ordnungsgemäß.
|   **Name des Diensts**    |   UnistoreSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Vorlage "Benutzer"-Dienst
|||         

<br />          

## <a name="user-experience-virtualization-service"></a>User Experience Virtualization-Dienst           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet Unterstützung für Anwendungs- und betriebssystemeinstellungen roaming
|   **Name des Diensts**    |   UevAgentService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

##  <a name="user-manager"></a>Benutzer-Manager        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Benutzer-Manager stellt die Runtime-Komponenten, die für mehrere Benutzer Interaktion erforderlich sind.  Wenn dieser Dienst beendet wird, können einige Anwendungen möglicherweise nicht ordnungsgemäß.
|   **Name des Diensts**    |   UserManager
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="user-profile-service"></a>Benutzerprofildienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst ist verantwortlich für das Laden und Entladen von Benutzerprofilen. Wenn dieser Dienst beendet oder deaktiviert ist, Benutzer werden nicht mehr in der Lage, sich erfolgreich angemeldet haben, oder melden Sie sich ab, apps treten möglicherweise Probleme, die auf Daten des Benutzers abrufen und Komponenten, die den Empfang von Benachrichtigungen des Arbeitsprofils-Ereignis registriert wird nicht empfangen.
|   **Name des Diensts**    |   ProfSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="virtual-disk"></a>Virtuelles Laufwerk             

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Verwaltungsdienste für Datenträger, Volumes, Dateisysteme und Speicherarrays.
|   **Name des Diensts**    |   vds
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Keine allgemeinen Vorgaben
|   **Kommentare**    |   
|||         

<br />          

## <a name="volume-shadow-copy"></a>Volumeschattenkopie-Dienst           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet und implementiert Volumeschattenkopien für Sicherung und andere Zwecke verwendet. Wenn dieser Dienst beendet wird, Schattenkopien sind nicht verfügbar, für die Sicherung und die Sicherung fehlschlagen. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   VSS
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Keine allgemeinen Vorgaben
|   **Kommentare**    |   
|||         

<br />          

##  <a name="walletservice"></a>WalletService           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Hosts-Objekte, die von Clients der Hülle der verwendet wird
|   **Name des Diensts**    |   WalletService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-audio"></a>Windows Audio            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Audio für Windows-basierten Programmen wird verwaltet.  Wenn dieser Dienst beendet wird, werden Audio- und Effekte möglicherweise nicht ordnungsgemäß.  Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind nicht gestartet
|   **Name des Diensts**    |   Audiosrv
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-audio-endpoint-builder"></a>Windows Audio Endpoint Builder           

| | |           
|---|---|
|   **Dienstbeschreibung** |   Verwaltet Audiogeräte für den Windows-Audio-Dienst.  Wenn dieser Dienst beendet wird, werden Audio- und Effekte möglicherweise nicht ordnungsgemäß.  Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind nicht gestartet
|   **Name des Diensts**    |   AudioEndpointBuilder
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-biometric-service"></a>Windows-Biometriedienst            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Windows-biometriedienst bietet Clientanwendungen die Möglichkeit, zu erfassen, verglichen werden soll, bearbeiten und Speichern von biometrischen Daten ohne direkten Zugriff auf biometrische Hardware oder nur Beispiele. Der Dienst wird in einem privilegierten SVCHOST-Prozess gehostet.
|   **Name des Diensts**    |   WbioSrvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-camera-frame-server"></a>Windows-Kamera-Frame-Server         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht er mehreren Clients Videoframes Kamerageräte auf.
|   **Name des Diensts**    |   FrameServer
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-connection-manager"></a>Windows-Verbindungs-Manager           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Wird automatisch eine Verbindung herstellen/trennen Entscheidungen basierend auf die Konnektivität-Netzwerkoptionen, die derzeit für den PC zur Verfügung und ermöglicht die Verwaltung der Netzwerkverbindungen, die basierend auf einer Gruppenrichtlinie Einstellungen.
|   **Name des Diensts**    |   Wcmsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-defender-network-inspection-service"></a>Windows Defender-Netzwerkinspektionsdienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Hilft beim gegen Eindringversuche für bekannte und neu entdeckte Sicherheitslücken in Netzwerkprotokollen
|   **Name des Diensts**    |   WdNisSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben    
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-defender-service"></a>Windows Defender-Dienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Benutzer schützen vor Malware und andere potenziell unerwünschte software
|   **Name des Diensts**    |   WinDefend
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-driver-foundation---user-mode-driver-framework"></a>Windows-Treiber-Foundation - Benutzermodus-Treiberframework           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Erstellt und verwaltet die Benutzermodus-Treiber. Dieser Dienst kann nicht beendet werden.
|   **Name des Diensts**    |   wudfsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-encryption-provider-host-service"></a>Windows-Verschlüsselung-Anbieterdienst für Host     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Windows-Verschlüsselung-Anbieter-Hostdienst Broker die verschlüsselungsbezogenen Funktionen von Drittanbieter-Kryptografieanbietern für Prozesse, die zum Auswerten und EAS-Richtlinien anwenden müssen. Beendet wird werden Überprüfungen der EAS-Konformität gefährdet werden, die von verbundenen e-Mail-Konten eingerichtet wurden
|   **Name des Diensts**    |   WEPHOSTSVC
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-error-reporting-service"></a>Windows-Fehlerberichterstattungsdienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht Fehler gemeldet werden, wenn Programme arbeiten oder reagiert nicht mehr und vorhandene Lösungen bereitgestellt werden. Ermöglicht auch die Protokolle für Diagnose generiert werden soll, und reparieren Sie die Dienste. Wenn dieser Dienst beendet wird, Fehlerberichterstattung funktionieren möglicherweise nicht korrekt und Diagnosedienste repariert und dessen Ergebnisse möglicherweise nicht angezeigt.
|   **Name des Diensts**    |   WerSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Sammelt und sendet abstürzen/Stillständen-Daten, die sowohl MS als auch von Drittanbietern ISVs/IHVs verwendet wird. Die Daten werden zum Diagnostizieren von Fehlern Abstürze auslösen, Sicherheitsfehler enthalten kann. Auch erforderlich für die Fehlerberichterstattung im Unternehmen.
|||         

<br />          

## <a name="windows-event-collector"></a>Windows-Ereignissammlung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst verwaltet permanente Abonnements von Ereignissen aus Remotequellen, die WS-Management-Protokoll unterstützen. Dies umfasst Windows Vista-Ereignisprotokolle, Hardware und IPMI-fähigen Ereignisquellen. Der Dienst speichert weitergeleitete Ereignisse in ein lokales Ereignisprotokoll. Wenn dieser Dienst beendet oder deaktiviert ist Event-Abonnements können nicht erstellt werden, und weitergeleitete Ereignisse nicht zulässig.
|   **Name des Diensts**    |   Wecsvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Erfasst ETW-Ereignisse (z. B. sicherheitsrelevanten Ereignissen), für die Verwaltbarkeit sowie Diagnose.  Viele der Funktionen und Tools von Drittanbietern erforderlich ist, einschließlich Security Audit-tools
|||         

<br />          

## <a name="windows-event-log"></a>Windows-Ereignisprotokoll            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst verwaltet, Ereignisse und Ereignisprotokolle. Protokollieren von Ereignissen, Ereignisse abonnieren von Ereignissen, Ereignisprotokollen Archivierung und Verwalten von Ereignismetadaten Abfragen unterstützt. Sie können Ereignisse im sowohl XML- und nur-Text-Format angezeigt. Beim Beenden dieses Diensts kann die Sicherheit und Zuverlässigkeit des Systems beeinträchtigt werden.
|   **Name des Diensts**    |   EventLog
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-firewall"></a>Windows-Firewall         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Windows-Firewall hilft dabei, Ihren Computer zu schützen, indem durch verhindert, dass nicht autorisierte Benutzer Zugriff auf Ihren Computer über das Internet oder einem Netzwerk.
|   **Name des Diensts**    |   MpsSvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-font-cache-service"></a>Windows-Schriftartencache      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Optimiert die Leistung von Anwendungen durch das Zwischenspeichern von häufig verwendeten Schriftartdaten. Anwendungen, werden dieser Dienst gestartet, wenn er nicht bereits ausgeführt wird. Es kann deaktiviert werden, obwohl dies die Leistung der Anwendung beeinträchtigen wird.
|   **Name des Diensts**    |   FontCache
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-image-acquisition-wia"></a>Windows Image Acquisition (WIA)          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Image Acquisition-Dienste für Scanner und Kameras
|   **Name des Diensts**    |   stisvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-insider-service"></a>Windows-Insider-Dienst     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   wisvc
|   **Name des Diensts**    |   wisvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Server unterstützt keine Test-flighting, daher wird keine Aktion auf dem Server. Funktion kann auch über Gruppenrichtlinien deaktiviert werden.
|||         

<br />          

##  <a name="windows-installer"></a>Windows Installer       

| | |           
|---|---|
|   **Dienstbeschreibung** |   Hinzugefügt, geändert und entfernt Anwendungen, die als Windows Installer (*.msi, *.msp)-Paket bereitgestellt. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   MSIServer
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-license-manager-service"></a>Windows-Lizenz-Manager-Dienst          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet infrastrukturunterstützung für den Microsoft Store an.  Dieser Dienst wird bedarfsgesteuert gestartet und wenn Inhalt über den Microsoft Store erworben wurden klicken Sie dann deaktiviert, funktionieren nicht ordnungsgemäß.
|   **Name des Diensts**    |   LicenseManager
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-management-instrumentation"></a>Windows-Verwaltungsinstrumentation       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet eine allgemeine Schnittstelle und-Objektmodell auf Management-Informationen zu Betriebssystem, Geräte, Anwendungen und Dienste zugreifen. Wenn dieser Dienst beendet wird, werden die meisten Windows-basierter Software nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   Winmgmt
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-mobile-hotspot-service"></a>Windows Mobile-Hotspot-Dienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet die Möglichkeit, eine Datenverbindung mit einem anderen Gerät freizugeben.
|   **Name des Diensts**    |   icssvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-modules-installer"></a>Windows-Modulinstallation        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Können die Installation, Änderung und Entfernen von Windows-Updates und optionalen Komponenten. Wenn dieser Dienst deaktiviert ist, installieren Sie oder deinstallieren Sie der Windows-Updates für diesen Computer fehlschlagen.
|   **Name des Diensts**    |   TrustedInstaller
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-push-notifications-system-service"></a>Windows-Push-Benachrichtigungen-Systemdienst            

| | |           
|---|---|
|   **Dienstbeschreibung** |   Dieser Dienst wird in Sitzung 0 ausgeführt und hostet den Benachrichtigungsanbieters-Plattform und die Verbindung, der Verbindung zwischen dem Gerät und WNS-Server verarbeitet.
|   **Name des Diensts**    |   WpnService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Automatic
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Für live-Kacheln und anderen Funktionen erforderlich sind
|||         

<br />      

## <a name="windows-push-notifications-user-service"></a>Windows Push Benachrichtigungsdienst-Benutzer          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst hostet die Plattform für Windows bietet Unterstützung für lokale und Pushbenachrichtigungen. Unterstützte Benachrichtigungen sind Kachel, Toast und Rohdaten.
|   **Name des Diensts**    |   WpnUserService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   OK, um deaktivieren
|   **Kommentare**    |   Vorlage "Benutzer"-Dienst
|||         

<br />

## <a name="windows-remote-management-ws-management"></a>Windows-Remoteverwaltung (WS-Management)
| | |
|---|---|
|   **Dienstbeschreibung** |   Mit dem Windows-Remoteverwaltungsdienst (WinRM) wird das WS-Verwaltungsprotokoll für die Remoteverwaltung implementiert. Die WS-Verwaltung stellt ein Standard-Webdienst-Protokoll dar, das für die Remote-Software- und Hardware-Verwaltung verwendet wird. Der WinRM-Dienst durchsucht das Netzwerk nach WS-Verwaltungsanforderungen und verarbeitet diese. Der WinRM-Dienst muss mit einem „Listener“ unter Verwendung des Befehlszeilenprogramms winrm.cmd oder über die Gruppenrichtlinie konfiguriert werden, um im Netzwerk „lauschen“ zu können. Der WinRM-Dienst stellt einen Zugriff auf WMI-Daten bereit und ermöglicht eine Ereignissammlung. Die Ereignissammlung und das Abonnieren von Ereignissen machen es erforderlich, dass der Dienst ausgeführt wird. WinRM-Nachrichten verwenden HTTP oder HTTPS als Transporte. Der WinRM-Dienst ist nicht von IIS abhängig, er wird jedoch vorkonfiguriert, um auf demselben Computer einen Port mit IIS zu teilen.  Der WinRM-Dienst reserviert das URL-Präfix „/wsman“. Um Konflikten mit IIS vorzubeugen, sollten Administratoren sicherstellen, dass keine auf IIS gehostete Website das URL-Präfix „/wsman“ verwendet.
|   **Name des Diensts**    |   WinRM
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Für die Remoteverwaltung erforderlich
|||

<br />          

##  <a name="windows-search"></a>Windows Search      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet inhaltsindizierung Zwischenspeichern von Eigenschaften und Suchergebnisse für Dateien, E-mail und andere Inhalte an.
|   **Name des Diensts**    |   WSearch
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Disabled
|   **Empfehlung**  |   Wurde bereits deaktiviert.
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-time"></a>Windows-Zeitdienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet Synchronisierung von Datum und Uhrzeit auf allen Clients und Servern im Netzwerk. Wenn dieser Dienst beendet wird, werden Datums-, Zeit- und datumssynchronisierung nicht verfügbar. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   W32Time
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-update"></a>Windows Update           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Erkennung, Download und Installation von Updates für Windows und andere Programme. Wenn dieser Dienst deaktiviert ist, Benutzer dieses Computers mit Windows Update oder die Funktion zum automatischen Aktualisieren nicht möglich, und Programme werden nicht in der Windows Update Agent (WUA) API verwenden können.
|   **Name des Diensts**    |   wuauserv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="winhttp-web-proxy-auto-discovery-service"></a>WinHTTP-Web Proxy Auto-Discovery-Dienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   WinHTTP die Client-HTTP-Stapel implementiert und bietet Entwicklern eine Win32-API und COM-Automatisierung-Komponente für HTTP-Anforderungen senden und Empfangen von Antworten. Darüber hinaus bietet WinHTTP Unterstützung für die automatische Ermittlung von Proxy-Konfiguration über die Implementierung des Protokolls (Web Proxy Auto-Discovery, WPAD).
|   **Name des Diensts**    |   WinHttpAutoProxySvc
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Alle Elemente, die den Netzwerkstapel verwendet haben ein funktionales abhängigkeitsprofil für diesen Dienst. Viele Organisationen nutzen auf diese Option, um ihre interne Netzwerke HTTP-Proxy routing konfigurieren.  Ohne diese werden intern, stammen von HTTP-Verbindungen mit dem Internet ausfallen.
|||         

<br />          

## <a name="wired-autoconfig"></a>Wired AutoConfig         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst für automatische Konfiguration von Kabelnetzwerken (DOT3SVC) ist verantwortlich für die Durchführung der IEEE 802.1X-Authentifizierung auf Ethernet-Schnittstellen. Wenn die aktuelle Bereitstellung des verkabelten Netzwerk 802.1 X Authentifizierung erzwingt, sollte die DOT3SVC-Dienst konfiguriert werden, führen Sie für die Einrichtung einer Layer 2-Konnektivität "und/oder" Bereitstellung des Zugriffs auf Netzwerkressourcen. Verdrahtete Netzwerken, die keine 802.1X-Authentifizierung erzwingen, sind nicht betroffen, durch den DOT3SVC-Dienst.
|   **Name des Diensts**    |   dot3svc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben   
|   **Kommentare**    |   
|||         

<br />          

## <a name="wmi-performance-adapter"></a>WMI-Leistungsadapter          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Leistungsinformationen für die Bibliothek von Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI)-Anbietern für Clients im Netzwerk bereit. Dieser Dienst wird nur ausgeführt, wenn Performance Data Helper aktiviert ist.
|   **Name des Diensts**    |   wmiApSrv
|   **Installation**    |   Immer installiert
|   **StartType**   |   Manuell
|   **Empfehlung**  | Keine allgemeinen Vorgaben       
|   **Kommentare**    |   
|||         

<br />          

## <a name="workstation"></a>Arbeitsstation          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Erstellt und verwaltet Clientnetzwerkverbindungen zu Remoteservern mithilfe des SMB-Protokolls. Wenn dieser Dienst beendet wird, werden diese Verbindungen nicht verfügbar. Wenn dieser Dienst deaktiviert ist, werden alle Dienste, die explizit davon abhängig sind möglicherweise nicht gestartet werden.
|   **Name des Diensts**    |   LanmanWorkstation
|   **Installation**    |   Immer installiert
|   **StartType**   |   Automatic
|   **Empfehlung**  | Keine allgemeinen Vorgaben       
|   **Kommentare**    |   
|||         

<br />

## <a name="xbox-live-auth-manager"></a>Xbox Live Auth Manager           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Authentifizierung und Autorisierung Dienste für die Interaktion mit Xbox Live. Wenn dieser Dienst beendet wird, können einige Anwendungen möglicherweise nicht ordnungsgemäß.
|   **Name des Diensts**    |   XblAuthManager
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Sollte deaktiviert werden
|   **Kommentare**    |   
|||         

<br />          

## <a name="xbox-live-game-save"></a>Xbox Live-Spiel speichern          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst wird synchronisiert speichern Sie Daten speichern aktiviert Spiele für Xbox Live.  Wenn dieser Dienst beendet wird, wird nicht Spiel Daten speichern, zum Hochladen oder Herunterladen von Xbox Live.
|   **Name des Diensts**    |   XblGameSave
|   **Installation**    |   Nur mit Desktopdarstellung
|   **StartType**   |   Manuell
|   **Empfehlung**  |   Sollte deaktiviert werden
|   **Kommentare**    |   Dieser Dienst wird synchronisiert speichern Sie Daten speichern aktiviert Spiele für Xbox Live.  Wenn dieser Dienst beendet wird, wird nicht Spiel Daten speichern, zum Hochladen oder Herunterladen von Xbox Live.
|||         

<br /> 
<br /> 

