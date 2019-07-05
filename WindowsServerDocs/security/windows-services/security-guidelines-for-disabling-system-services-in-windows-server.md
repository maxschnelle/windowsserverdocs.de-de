---
title: Sicherheitsrichtlinien für Systemdienste in Windows Server 2016
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
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2019
ms.locfileid: "66749449"
---
## <a name="guidance-on-disabling-system-services-on-windows-server-2016-with-desktop-experience"></a>Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung

Gilt für: Windows Server 2016

Das Windows-Betriebssystem enthält viele Systemdienste, mit denen wichtige Funktionen bereitgestellt werden. Die Dienste verfügen über unterschiedliche Standardrichtlinien für den Start: einige werden standardmäßig gestartet (automatisch), einige bei Bedarf (manuell) und einige sind standardmäßig deaktiviert und müssen explizit aktiviert werden, bevor sie ausgeführt werden können. Diese Standardeinstellungen wurden für jeden Dienst sorgfältig gewählt, um für typische Kunden eine gute Abstimmung in Bezug auf Leistung, Funktionalität und Sicherheit zu erzielen.

Einige Unternehmenskunden ziehen für ihre Windows-PCs und -Server aber ggf. einen stärker auf Sicherheit ausgerichteten Ansatz vor, bei dem die Angriffsfläche auf das absolute Minimum reduziert ist. Diese Kunden möchten daher alle Dienste vollständig deaktivieren, die in ihren jeweiligen Umgebungen nicht benötigt werden. Für diese Kunden stellt Microsoft® diese Anleitung bereit, die Hinweise dazu enthält, welche Dienste zu diesem Zweck deaktiviert werden können.

Die Anleitung gilt nur für Windows Server 2016 mit Desktopdarstellung (nicht bei Nutzung als Desktopersatz für Endbenutzer). Ab Windows Server 2019 sind diese Richtlinien standardmäßig konfiguriert. Die Dienste des Systems sind jeweils wie folgt kategorisiert:

-   **Deaktivierung empfohlen**: Für sicherheitsorientierte Unternehmen wird die Deaktivierung dieses Diensts und der Verzicht auf die damit verbundenen Funktionen in den meisten Fällen empfohlen (siehe zusätzliche Details unten).
- **Deaktivierung OK**: Dieser Dienst verfügt über Funktionen, die für einige Unternehmen nützlich sind. Er kann von sicherheitsorientierten Unternehmen, die ihn nicht nutzen, problemlos deaktiviert werden.
- **Nicht deaktivieren**: Wenn Dienste dieser Art deaktiviert werden, wirkt sich dies auf grundlegende Funktionen aus, oder es wird verhindert, dass bestimmte Rollen oder Features richtig funktionieren. Daher sollten sie nicht deaktiviert werden.
-  **Kein Hinweis**: Die Auswirkungen der Deaktivierung dieser Dienste wurden noch nicht vollständig evaluiert. Aus diesem Grund sollte die Standardkonfiguration dieser Dienste nicht geändert werden.


Kunden können ihre Windows-PCs und -Server konfigurieren, um ausgewählte Dienste zu deaktivieren, indem sie die Sicherheitsvorlagen in ihren Gruppenrichtlinien oder die PowerShell-Automatisierung verwenden. In einigen Fällen umfasst die Anleitung bestimmte Gruppenrichtlinieneinstellungen, mit denen die Funktionen des Diensts direkt deaktiviert werden. Dies ist eine Alternative zum Deaktivieren des gesamten Diensts.

Microsoft empfiehlt Kunden die Deaktivierung der folgenden Dienste und der jeweiligen geplanten Aufgaben unter Windows Server 2016 mit Desktopdarstellung:

Dienste: 
1. Xbox Live Authentifizierungs-Manager
2. Xbox Live-Spiele speichern

Geplante Aufgaben: 
1. \Microsoft\XblGameSave\XblGameSaveTask
2. \Microsoft\XblGameSave\XblGameSaveTaskLogon

(Du kannst auf die Informationen zu allen Diensten in diesem Artikel auch zugreifen, indem du die angefügte Microsoft Excel-Tabelle anzeigst: [Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung](https://msdnshared.blob.core.windows.net/media/2017/05/Service-management-WS2016.xlsx).)

<br />

### <a name="disabling-services-not-installed-by-default"></a>Deaktivieren von nicht standardmäßig installierten Diensten

Microsoft rät von der Anwendung von Richtlinien zum Deaktivieren von Diensten ab, die nicht standardmäßig installiert werden.
-  Der Dienst wird in der Regel benötigt, wenn das Feature installiert ist. Für das Installieren des Diensts bzw. des Features sind Administratorrechte erforderlich. Lege nicht das Starten des Diensts als unzulässig fest, sondern das Installieren des Features.
-  Durch das Blockieren des Microsoft Windows-Diensts wird nicht verhindert, dass ein Administrator (oder in einigen Fällen auch andere Benutzer) einen ähnlichen Dienst eines Drittanbieters installiert, der unter Umständen mit einem höheren Sicherheitsrisiko verbunden ist.
-  Wenn ein nicht zum Standard gehörender Windows-Dienst (z. B. W3SVC) per Baseline oder Benchmark deaktiviert wird, erweckt dies bei einigen Prüfern den Eindruck, als ob die Technologie (z. B. IIS) grundsätzlich unsicher ist und niemals verwendet werden sollte.
-  Wenn das Feature (und der Dienst) niemals installiert wird, macht dies die Baseline und den Prüfaufwand nur unnötig komplizierter.

<br />
Die beiden folgenden Tabellen enthalten für alle in diesem Dokument aufgeführten Dienste eine Beschreibung der Spalten und Microsoft-Empfehlungen zum Aktivieren und Deaktivieren von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung: 

<br />

### <a name="explanation-of-columns"></a>Beschreibung der Spalten

| | |
|---|---|
|**Dienstbeschreibung**|   Die Beschreibung des Diensts aus „sc.exe qdescription“.|
|**Name** |Schlüsselname (interner Name) des Diensts|
|**Installation** |Immer installiert: Dienst ist für Server Core und Server mit Desktopdarstellung verfügbar  <br /> Nur mit Desktopdarstellung: Dienst ist unter Windows Server 2016 mit Desktopdarstellung verfügbar, aber ***nicht*** für Server Core |
|**Starttyp**  |Starttyp des Diensts unter Windows Server 2016|
|**Empfehlung** |Empfehlung/Hinweis von Microsoft zur Deaktivierung dieses Diensts unter Windows Server 2016 bei einer typischen, gut verwalteten Unternehmensbereitstellung, bei der der Server nicht als Desktopersatz für den Endbenutzer verwendet wird.|
|**Kommentare** |Zusätzliche Beschreibung|

<br />

### <a name="explanation-of-microsoft-recommendations"></a>Beschreibung von Microsoft-Empfehlungen

| | |
|---|---|
|**Nicht deaktivieren** |Dieser Dienst sollte nicht deaktiviert werden.|
|**Deaktivierung OK**| Dieser Dienst kann deaktiviert werden, wenn das von ihm unterstützte Feature nicht verwendet wird.|
|**Bereits deaktiviert**|  Dieser Dienst wird standardmäßig deaktiviert. Die Erzwingung per Richtlinie ist nicht erforderlich.|
|**Deaktivierung empfohlen** |Dieser Dienst sollte auf einem gut verwalteten Unternehmenssystem niemals aktiviert werden.|

<br />

Die folgenden Tabellen enthalten Microsoft-Anleitungen zum Deaktivieren von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung:

<br />

##  <a name="activex-installer-axinstsv"></a>ActiveX-Installationsprogramm (AxInstSV)

| | |
|---|---|
|   **Dienstbeschreibung** |   Ermöglicht die Überprüfung der Benutzerkontensteuerung für die Installation von ActiveX-Steuerelementen über das Internet und die Verwaltung der Installation von ActiveX-Steuerelementen basierend auf Gruppenrichtlinieneinstellungen. Dieser Dienst wird bedarfsgesteuert gestartet, und wenn er deaktiviert ist, verhält sich die Installation von ActiveX-Steuerelementen gemäß den Einstellungen des Standardbrowsers.    |
|   **Dienstname**    |   AxInstSV    |
|   **Installation**    |   Nur mit Desktopdarstellung    |
|   **Starttyp**   |   Manual  |
|   **Empfehlung**  |   Deaktivierung OK   |
|   **Kommentare**    |   Die Deaktivierung ist in Ordnung, wenn das Feature nicht benötigt wird. |


<br />

## <a name="alljoyn-router-service"></a>AllJoyn-Routerdienst   

| | |
|---|---|
|   **Dienstbeschreibung** |   Leitet AllJoyn-Mitteilungen für die lokalen AllJoyn-Clients um. Wenn dieser Dienst angehalten wird, können die AllJoyn-Clients, die nicht über eigene gebündelte Router verfügen, nicht ausgeführt werden. |
|   **Dienstname**    |   AJRouter    |
|   **Installation**    |   Nur mit Desktopdarstellung    |
|   **Starttyp**   |   Manual  |
|   **Empfehlung**  | Kein Hinweis       |
|   **Kommentare**    |       |
| | |

<br />

## <a name="app-readiness"></a>App-Bereitschaft

| | |
|---|---|
**Dienstbeschreibung** |   Bereitet Apps für die Nutzung vor, wenn sich ein Benutzer zum ersten Mal am PC anmeldet und neue Apps hinzugefügt werden.
**Dienstname**    |   AppReadiness
**Installation**    |   Nur mit Desktopdarstellung
**Starttyp**   |   Manual
**Empfehlung**  |   Nicht deaktivieren
**Kommentare**    |   
| | |

<br />

##  <a name="application-identity"></a>Anwendungsidentität

| | |       
|---|---|   
**Dienstbeschreibung** |   Ermittelt und überprüft die Identität einer Anwendung. Wenn dieser Dienst deaktiviert wird, kann AppLocker nicht erzwungen werden.
**Dienstname**    |   AppIDSvc
**Installation**    |   Immer installiert
**Starttyp**   |   Manual
**Empfehlung**  |Kein Hinweis    
**Kommentare**    |   
|||     

<br />

##  <a name="application-information"></a>Anwendungsinformationen 

| | |       
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht das Ausführen von interaktiven Anwendungen mit zusätzlichen Administratorrechten.  Wenn dieser Dienst beendet wird, können Benutzer keine Anwendungen mit den zusätzlichen Administratorrechten mehr starten, die sie für bestimmte Benutzeraufgaben unter Umständen benötigen.
|   **Dienstname**    |   Appinfo
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   Unterstützt die Rechteerweiterung für die Benutzerkontensteuerung auf demselben Desktop
|||     

<br />

##  <a name="application-layer-gateway-service"></a>Gatewaydienst auf Anwendungsebene       

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Stellt Unterstützung für Drittanbieterprotokoll-Plug-Ins für die gemeinsame Nutzung der Internetverbindung bereit.
|   **Dienstname**    |   ALG
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |Kein Hinweis    
|   **Kommentare**    |   
|||     

<br />

##  <a name="application-management"></a>Anwendungsverwaltung      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verarbeitet Installations-, Entfernungs und Enumerationsanforderungen für Software, die über die Gruppenrichtlinie bereitgestellt wird. Wenn der Dienst deaktiviert wird, können Benutzer keine Software mehr installieren, entfernen oder enumerieren, die per Gruppenrichtlinie bereitgestellt wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   AppMgmt
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="appx-deployment-service-appxsvc"></a>AppX-Bereitstellungsdienst (AppXSVC)       

| | |           
|---|---|
|   **Dienstbeschreibung** |   Stellt Infrastrukturunterstützung für die Bereitstellung von Store-Anwendungen bereit. Dieser Dienst wird bedarfsgesteuert gestartet. Wenn er deaktiviert wird, werden Store-Anwendungen nicht für das System bereitgestellt und funktionieren ggf. nicht richtig.
|   **Dienstname**    |   AppXSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="auto-time-zone-updater"></a>Automatische Zeitzonenaktualisierung           

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Legt die Zeitzone des Systems automatisch fest.
|   **Dienstname**    |   tzautoupdate
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

## <a name="background-intelligent-transfer-service"></a>Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Überträgt Dateien im Hintergrund, indem ungenutzte Netzwerkbandbreite verwendet wird. Wenn der Dienst deaktiviert wird, können alle Anwendungen, die von BITS abhängig sind, z. B. Windows Update oder MSN Explorer, Programme und andere Informationen nicht automatisch herunterladen.
|   **Dienstname**    |   BITS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          


## <a name="background-tasks-infrastructure-service"></a>Infrastrukturdienst für Hintergrundaufgaben      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Windows-Infrastrukturdienst, mit dem gesteuert wird, welche Hintergrundaufgaben auf dem System ausgeführt werden können.
|   **Dienstname**    |   BrokerInfrastructure
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="base-filtering-engine"></a>Basisfiltermodul            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Das Basisfiltermodul (Base Filtering Engine, BFE) ist ein Dienst, mit dem Firewall- und IPsec-Richtlinien (Internetprotokollsicherheit) verwaltet werden und die Benutzermodusfilterung implementiert wird. Wenn der BFE-Dienst beendet oder deaktiviert wird, bedeutet dies eine erhebliche Reduzierung der Systemsicherheit. Darüber hinaus führt dies zu unvorhersehbarem Verhalten von IPsec-Verwaltungs- und Firewallanwendungen.
|   **Dienstname**    |   BFE
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="bluetooth-support-service"></a>Bluetooth-Unterstützungsdienst            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Bluetooth-Dienst unterstützt die Ermittlung und Zuordnung von externen Bluetooth-Geräten.  Das Beenden oder Deaktivieren dieses Diensts kann dazu führen, dass bereits installierte Bluetooth-Geräte nicht mehr richtig funktionieren und verhindert wird, dass neue Geräte ermittelt oder zugeordnet werden können.
|   **Dienstname**    |   bthserv
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Die Deaktivierung ist in Ordnung, wenn der Dienst nicht verwendet wird. Ein weiterer Mechanismus für die Deaktivierung: https://technet.microsoft.com/library/dd252791.aspx
|||         

<br />          


## <a name="cdpusersvc"></a>CDPUserSvc           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Benutzerdienst wird für Szenarien mit der Plattform für verbundene Geräte verwendet.
|   **Dienstname**    |   CDPUserSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Benutzerdienstvorlage
|||         

<br />          


##  <a name="certificate-propagation"></a>Zertifikatverteilung     

| | |           
|---|---|
|   **Dienstbeschreibung** |   Kopiert Benutzer- und Stammzertifikate von Smartcards in den Zertifikatspeicher des aktuellen Benutzers, erkennt das Einlegen einer Smartcard in einen Smartcardleser und installiert bei Bedarf den zugehörigen Plug & Play-Minitreiber.
|   **Dienstname**    |   CertPropSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="client-license-service-clipsvc"></a>Clientlizenzdienst (ClipSVC)        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Infrastrukturunterstützung für den Microsoft Store bereit. Dieser Dienst wird bedarfsgesteuert gestartet, und wenn er deaktiviert wird, verhalten sich über den Microsoft Store gekaufte Anwendungen nicht korrekt.
|   **Dienstname**    |   ClipSVC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="cng-key-isolation"></a>CNG-Schlüsselisolation

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der CNG-Schlüsselisolationsdienst wird im LSA-Prozess gehostet. Der Dienst stellt eine Schlüsselprozessisolation für private Schlüssel und zugehörige Kryptografievorgänge gemäß den Anforderungen der allgemeinen Kriterien bereit. Der Dienst speichert und verwendet langlebige Schlüssel in einem sicheren Prozess in Übereinstimmung mit den Anforderungen der allgemeinen Kriterien.
|   **Dienstname**    |   KeyIso
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="com-event-system"></a>COM+-Ereignissystem       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Unterstützt den Systemereignis-Benachrichtigungsdienst (SENS), mit dem Ereignisse automatisch an abonnierende COM-Komponenten verteilt werden. Nach dem Beenden des Diensts wird SENS geschlossen, so dass keine weiteren Anmelde- und Abmeldebenachrichtigungen bereitgestellt werden können. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   EventSystem
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="com-system-application"></a>COM+-Systemanwendung     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet die Komponentenkonfiguration und -überwachung von COM+-basierten Komponenten. Nach dem Beenden des Diensts sind die meisten COM+-basierten Komponenten nicht ordnungsgemäß funktionsfähig. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   COMSysApp
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="computer-browser"></a>Computerbrowser        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Führt eine aktuelle Liste der Computer im Netzwerk und gibt diese an als Browser fungierende Computer weiter. Diese Liste wird nicht aktualisiert oder gewartet, falls der Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   Browser
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

## <a name="connected-devices-platform-service"></a>Plattformdienst für verbundene Geräte       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst wird für verbundene Geräte und Universal Glass-Szenarien verwendet.
|   **Dienstname**    |   CDPSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="connected-user-experiences-and-telemetry"></a>Benutzererfahrung und Telemetrie im verbundenen Modus     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Durch den Dienst für Benutzererfahrung und Telemetrie im verbundenen Modus werden Features aktiviert, die Benutzerfreundlichkeit in Anwendungen und im verbundenen Modus unterstützen. Außerdem verwaltet dieser Dienst die ereignisgesteuerte Sammlung und Übertragung von Diagnose- und Nutzungsdaten (die zur Verbesserung der Benutzerfreundlichkeit und Qualität der Windows-Plattform eingesetzt werden). Dazu müssen die Diagnose- und Nutzungseinstellungen in der Datenschutzoption unter „Feedback und Diagnose“ aktiviert sein.
|   **Dienstname**    |   DiagTrack
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="contact-data"></a>Kontaktdaten        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Indiziert Kontaktdaten für die schnelle Kontaktsuche. Wenn du diesen Dienst beendest oder deaktivierst, können Kontakte in den Suchergebnissen fehlen.
|   **Dienstname**    |   PimIndexMaintenanceSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Benutzerdienstvorlage
|||         

<br />          

## <a name="coremessaging"></a>CoreMessaging            

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Verwaltet die Kommunikation zwischen Systemkomponenten.
|   **Dienstname**    |   CoreMessagingRegistrar
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="credential-manager"></a>Anmeldeinformationsverwaltung           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die sichere Speicherung und den Abruf von Anmeldeinformationen für Benutzer, Anwendungen und Sicherheitspakete.
|   **Dienstname**    |   VaultSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="cryptographic-services"></a>Kryptografiedienste           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt drei Verwaltungsdienste bereit: den Katalogdatenbankendienst, der die Signaturen von Windows-Dateien bestätigt und die Installation neuer Programme ermöglicht, den geschützten Stammdienst, der diesem Computer vertrauenswürdige Zertifikate von Stammzertifizierungsstellen hinzufügt und diese vom Computer entfernt, und den automatischen Aktualisierungsdienst für die Stammzertifizierung, der Stammzertifikate vom Windows Update abruft und Szenarien wie SSL aktiviert. Wird dieser Dienst beendet, funktionieren diese Verwaltungsdienste nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   CryptSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="data-sharing-service"></a>Datenfreigabedienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dient als Datenbroker zwischen Anwendungen.
|   **Dienstname**    |   DsSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="datacollectionpublishingservice"></a>DataCollectionPublishingService          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst für die Erfassung und Veröffentlichung von Daten (Data Collection and Publishing, DCP) unterstützt Erstanbieter-Apps zum Hochladen von Daten in die Cloud.
|   **Dienstname**    |   DcpSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="dcom-server-process-launcher"></a>DCOM-Server-Prozessstart         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst DCOMLAUNCH startet COM- und DCOM-Server als Reaktion auf Objektaktivierungsanforderungen. Wenn dieser Dienst beendet oder deaktiviert wird, funktionieren Programme, für die COM oder DCOM genutzt wird, nicht richtig. Wir empfehlen dir dringend, den Dienst DCOMLAUNCH auszuführen.
|   **Dienstname**    |   DcomLaunch
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |Kein Hinweis    
|   **Kommentare**    |   
|||         

<br />

##  <a name="device-association-service"></a>Gerätezuordnungsdienst      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Kopplung zwischen dem System und verkabelten Geräten oder Drahtlosgeräten.
|   **Dienstname**    |   DeviceAssociationService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />

##  <a name="device-install-service"></a>Geräteinstallationsdienst

| | |
|---|---|
|   **Dienstbeschreibung** |   Ermöglicht einem Computer die Erkennung und Anpassung an Hardwareänderungen mit nur wenigen oder ganz ohne Benutzereingaben. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems.
|   **Dienstname**    |   DeviceInstall
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis
|   **Kommentare**    |
|||

<br />          

##  <a name="device-management-enrollment-service"></a>Registrierungsdienst für die Geräteverwaltung        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Führt Aktivitäten der Geräteregistrierung für die Geräteverwaltung durch.
|   **Dienstname**    |   DmEnrollmentSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="device-setup-manager"></a>Geräteinstallations-Manager         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Erkennung, den Download und die Installation von gerätebezogener Software. Wenn dieser Dienst deaktiviert wird, werden die Geräte ggf. mit veralteter Software konfiguriert und funktionieren unter Umständen nicht richtig.
|   **Dienstname**    |   DsmSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="devquery-background-discovery-broker"></a>Broker für DevQuery-Hintergrundermittlung         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Ermöglicht Apps die Ermittlung von Geräten per Hintergrundaufgabe.
|   **Dienstname**    |   DevQueryBroker
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="dhcp-client"></a>DHCP-Client          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Registriert und aktualisiert IP-Adressen und DNS-Einträge für diesen Computer. Wenn dieser Dienst beendet wird, empfängt der Computer keine dynamischen IP-Adressen und DNS-Updates mehr. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   Dhcp
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="diagnostic-policy-service"></a>Diagnoserichtliniendienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Diagnoserichtliniendienst ermöglicht die Problemerkennung, Problembehandlung und Lösung für Windows-Komponenten.  Wenn dieser Dienst beendet wird, funktioniert die Diagnose nicht mehr.
|   **Dienstname**    |   DPS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="diagnostic-service-host"></a>Diagnosediensthost     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Diagnosediensthost wird vom Diagnoserichtliniendienst als Host für Diagnosen verwendet, die im Kontext eines lokalen Diensts ausgeführt werden müssen.  Wird dieser Dienst beendet, funktionieren alle davon abhängigen Diagnosen nicht mehr ordnungsgemäß.
|   **Dienstname**    |   WdiServiceHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="diagnostic-system-host"></a>Diagnosesystemhost           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Diagnosesystemhost wird vom Diagnoserichtliniendienst verwendet, um Diagnosen zu hosten, die für einen lokalen Dienst durchgeführt werden müssen.  Wird dieser Dienst beendet, funktionieren alle davon abhängigen Diagnosen nicht mehr ordnungsgemäß.
|   **Dienstname**    |   WdiSystemHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="distributed-link-tracking-client"></a>Überwachung verteilter Verknüpfungen (Client)            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet die Links zwischen NTFS-Dateien auf einem Computer oder für die Computer eines Netzwerks.
|   **Dienstname**    |   TrkWks
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="distributed-transaction-coordinator"></a>Distributed Transaction Coordinator     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Koordiniert Transaktionen, die sich über mindestens zwei Ressourcenverwaltungen wie Datenbanken, Nachrichtenwarteschlangen oder Dateisysteme erstrecken. Wenn der Dienst beendet ist, treten bei diesen Transaktionen Fehler auf. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   MSDTC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />  

##  <a name="dmwappushsvc"></a>dmwappushsvc        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   WAP Push-Nachrichtenroutingdienst
|   **Dienstname**    |   dmwappushservice
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Dieser Dienst wird auf Clientgeräten für Intune, MDM und ähnlichen Verwaltungstechnologien sowie für einheitliche Schreibfilter benötigt. Für Server ist der Dienst nicht erforderlich.
|||         

<br />      

##  <a name="dns-client"></a>DNS-Client      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der DNS-Clientdienst (dnscache) wird zum Zwischenspeichern von DNS-Namen (Domain Name System) verwendet und registriert den vollständigen Computernamen für diesen Computer. Wenn der Dienst angehalten wird, werden DNS-Namen weiterhin aufgelöst. Die Ergebnisse von DNS-Namensabfragen werden jedoch nicht zwischengespeichert, und der Name des Computers wird nicht registriert. Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden.
|   **Dienstname**    |   Dnscache
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="downloaded-maps-manager"></a>Manager für heruntergeladene Karten     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Windows-Dienst für den Anwendungszugriff auf heruntergeladene Karten. Dieser Dienst wird bedarfsgesteuert je nach der Anwendung gestartet, die auf heruntergeladene Karten zugreift. Wenn der Dienst deaktiviert wird, können Apps nicht auf Karten zugreifen.
|   **Dienstname**    |   MapsBroker
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Wenn der Dienst deaktiviert wird, funktionieren Apps nicht mehr, die den Dienst benötigen. Die Aktivierung ist kein Problem, wenn der Dienst von Apps nicht benötigt wird.
|||         

<br />          

## <a name="embedded-mode"></a>Eingebetteter Modus            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst „Eingebetteter Modus“ ermöglicht Szenarien, die sich auf Hintergrundanwendungen beziehen.  Wenn dieser Dienst deaktiviert wird, wird die Aktivierung von Hintergrundanwendungen verhindert.
|   **Dienstname**    |   embeddedmode
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="encrypting-file-system-efs"></a>Verschlüsselndes Dateisystem (EFS)

| | |                   
|---|---|           
|   **Dienstbeschreibung** | Eine wichtige Dateiverschlüsselungstechnologie zum Speichern verschlüsselter Dateien auf Volumes mit dem Dateisystem NTFS. Wenn dieser Dienst beendet oder deaktiviert wird, können Anwendungen nicht mehr auf verschlüsselte Dateien zugreifen.            
|   **Dienstname**  |  EFS            
|   **Installation**  |  Immer installiert           
|   **Starttyp**   |  Manual           
|   **Empfehlung**  | Kein Hinweis           
|   **Kommentare**   |
|||                 

<br />  

## <a name="enterprise-app-management-service"></a>Verwaltungsdienst für Unternehmens-Apps            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Verwaltung von Unternehmensanwendungen.
|   **Dienstname**    |   EntAppSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="extensible-authentication-protocol"></a>Extensible Authentication-Protokoll           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der EAP-Dienst (Extensible Authentication Protocol) stellt in folgenden Szenarios eine Netzwerkauthentifizierung bereit: 802.1X (verkabelt und drahtlos), VPN und NAP (Network Access Protection).  EAP stellt darüber hinaus APIs (Application Programming Interface, Anwendungsprogrammierschnittstelle) bereit, die von Netzwerkzugriffclients, einschließlich Drahtlosclients und VPN-Clients, beim Authentifizierungsvorgang verwendet werden.  Wenn du diesen Dienst deaktivierst, kann dieser Computer nicht mehr auf Netzwerke zugreifen, die eine EAP-Authentifizierung verwenden.
|   **Dienstname**    |   EapHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="function-discovery-provider-host"></a>Funktionssuchanbieter-Host         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der FDPHOST-Dienst dient zum Hosten der Netzwerkerkennungsanbieter für die Funktionssuche (Function Discovery, FD). Von diesen FD-Anbietern werden Netzwerkerkennungsdienste für das Simple Services Discovery-Protokoll (SSDP) und das Web Services – Discovery (WS-D)-Protokoll bereitgestellt. Durch das Beenden oder Deaktivieren des FDPHOST-Diensts wird bei Verwendung von FD die Netzwerkerkennung für diese Protokolle deaktiviert. Ist dieser Dienst nicht verfügbar, können mit Netzwerkdiensten, von denen FD und diese Erkennungsprotokolle verwendet werden, keine Netzwerkgeräte oder -ressourcen gesucht werden.
|   **Dienstname**    |   fdPHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="function-discovery-resource-publication"></a>Funktionssuche-Ressourcenveröffentlichung      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Veröffentlicht diesen Computer und die daran angeschlossenen Ressourcen, damit sie über das Netzwerk gesucht werden können.  Wenn dieser Dienst beendet wird, werden die Netzwerkressourcen nicht mehr veröffentlicht, damit sie von anderen Computern im Netzwerk gesucht werden können.
|   **Dienstname**    |   FDResPub
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="geolocation-service"></a>Geolocation-Dienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst überwacht den aktuellen Standort des Systems und verwaltet Geofences (geografische Standorte mit zugeordneten Ereignissen).  Wenn du diesen Dienst deaktivierst, sind Anwendungen nicht in der Lage, Benachrichtigungen zu Geolocations oder Geofences zu nutzen oder zu empfangen.
|   **Dienstname**    |   lfsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Wenn der Dienst deaktiviert wird, funktionieren Apps nicht mehr, die den Dienst benötigen. Die Aktivierung ist kein Problem, wenn der Dienst von Apps nicht benötigt wird.
|||         

<br />          

##  <a name="group-policy-client"></a>Gruppenrichtlinienclient     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Dienst ist für das Anwenden von Einstellungen verantwortlich, die über die Gruppenrichtlinienkomponente durch Administratoren für den Computer und die Benutzer konfiguriert wurden. Wenn der Dienst deaktiviert wird, werden die Einstellungen nicht angewendet. Somit können Anwendungen und Komponenten nicht über die Gruppenrichtlinie verwaltet werden. Von der Gruppenrichtlinienkomponente abhängige Komponenten oder Anwendungen funktionieren zudem ggf. nicht, wenn der Dienst deaktiviert wird.
|   **Dienstname**    |   gpsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          


## <a name="human-interface-device-service"></a>Eingabegerätedienst           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktiviert und unterstützt die Verwendung von Abkürzungstasten auf Tastaturen, Fernbedienungen und anderen Multimediageräten. Wir empfehlen dir, diesen Dienst auszuführen.
|   **Dienstname**    |   hidserv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="hv-host-service"></a>HV-Hostdienst     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt eine Schnittstelle für den Hyper-V-Hypervisor bereit, um für das Hostbetriebssystem Leistungsindikatoren pro Partition verfügbar zu machen.
|   **Dienstname**    |   HvHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Leistungsoptimierungen für Gast-VMs. Wird heutzutage meist nicht mehr verwendet (mit Ausnahme von explizit aufgefüllten VMs), aber der Dienst wird für Application Guard eingesetzt.
|||         

<br />          

## <a name="hyper-v-data-exchange-service"></a>Hyper-V-Datenaustauschdienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt einen Mechanismus zum Austauschen von Daten zwischen dem virtuellen Computer und dem Betriebssystem bereit, das auf dem physischen Computer ausgeführt wird.
|   **Dienstname**    |   vmickvpexchange
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />      

## <a name="hyper-v-guest-service-interface"></a>Hyper-V-Gastdienstschnittstelle          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt eine Schnittstelle für den Hyper-V-Host für die Interaktion mit bestimmten Diensten bereit, die auf dem virtuellen Computer ausgeführt werden.
|   **Dienstname**    |   vmicguestinterface
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />  

## <a name="hyper-v-guest-shutdown-service"></a>Hyper-V-Dienst zum Herunterfahren des Gasts           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt einen Mechanismus zum Herunterfahren des Betriebssystems dieses virtuellen Computers über die Verwaltungsschnittstellen auf dem physischen Computer bereit.
|   **Dienstname**    |   vmicshutdown
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />

## <a name="hyper-v-heartbeat-service"></a>Hyper-V Taktdienst
| | |
|---|---|
|   **Dienstbeschreibung** |   Überwacht den Zustand dieses virtuellen Computers, indem in regelmäßigen Abständen ein Heartbeat gemeldet wird. Mit diesem Dienst kannst du ausgeführte virtuelle Computer identifizieren, die nicht mehr reagieren.
|   **Dienstname**    |   vmicheartbeat
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||

<br />          

## <a name="hyper-v-powershell-direct-service"></a>Hyper-V-Dienst PowerShell Direct            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt einen Mechanismus bereit, um einen virtuellen Computer mit PowerShell über eine VM-Sitzung ohne virtuelles Netzwerk zu verwalten.
|   **Dienstname**    |   vmicvmsession
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />          

## <a name="hyper-v-remote-desktop-virtualization-service"></a>Hyper-V-Remotedesktopvirtualisierungsdienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt eine Plattform für die Kommunikation zwischen dem virtuellen Computer und dem Betriebssystem bereit, das auf dem physischen Computer ausgeführt wird.
|   **Dienstname**    |   vmicrdv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />          

## <a name="hyper-v-time-synchronization-service"></a>Hyper-V-Zeitsynchronisierungsdienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Synchronisiert die Systemzeit dieses virtuellen Computers mit der Systemzeit des physischen Computers.
|   **Dienstname**    |   vmictimesync
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />          

## <a name="hyper-v-volume-shadow-copy-requestor"></a>Hyper-V-Volumeschattenkopie-Anforderer         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Koordiniert die Kommunikation, die erforderlich ist, damit der Volumeschattenkopie-Dienst zum Sichern von Anwendungen und Daten auf diesem virtuellen Computer basierend auf dem Betriebssystem des physischen Computers verwendet werden kann.
|   **Dienstname**    |   vmicvss
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Siehe „HvHost“.
|||         

<br />          

## <a name="ike-and-authip-ipsec-keying-modules"></a>IKE- und AuthIP IPsec-Schlüsselerstellungsmodule          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Die IKEEXT-Diensthosts der Schlüsselerstellungsmodule für IKE (Internet Key Exchange) und Auth-IP (Authenticated Internet Protocol). Diese Schlüsselerstellungsmodule werden für die Authentifizierung und den Schlüsselaustausch in Internet Protocol Security (IPsec) verwendet. Wenn du den IKEEXT-Dienst anhältst oder deaktivierst, wird der IKE/AuthIP-Schlüsselaustausch mit Peercomputern deaktiviert. IPsec ist im Allgemeinen für die Verwendung von IKE/AuthIP konfiguriert, und das Anhalten oder Deaktivieren des IKEEXT-Diensts kann zu einem IPsec-Fehler führen und die Sicherheit des Systems gefährden. Wir empfehlen dir dringend, den Dienst IKEEXT auszuführen.
|   **Dienstname**    |   IKEEXT
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |    
|||         

<br />          

## <a name="interactive-services-detection"></a>Erkennung interaktiver Dienste           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Aktiviert die Benutzerbenachrichtigung von Benutzereingaben für interaktive Dienste. Dies ermöglicht den Zugriff auf von interaktiven Diensten erstellte Dialogfelder, wenn diese angezeigt werden. Wenn dieser Dienst beendet wird, funktionieren Benachrichtigungen über neue interaktive Dienstdialogfelder nicht mehr, und der Zugriff auf Dialogfelder von interaktiven Diensten ist eventuell nicht möglich. Wenn dieser Dienst deaktiviert wird, funktionieren weder die Benachrichtigung über noch der Zugriff auf neue interaktive Dienstdialogfelder.
|   **Dienstname**    |   UI0Detect
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />  

## <a name="internet-connection-sharing-ics"></a>Gemeinsame Nutzung der Internetverbindung            

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Stellt die Dienste für die Netzwerkadressenübersetzung, Adressierung, Namensauflösung bzw. Verhinderung von Eindringversuchen für ein Heimnetzwerk oder ein Netzwerk eines kleinen Büros bereit.
|   **Dienstname**    |   SharedAccess
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Ist für Clients erforderlich, die als WLAN-Hotspots genutzt werden, und außerdem an beiden Enden einer Miracast-Projektion. Die gemeinsame Nutzung der Internetverbindung kann mit der GPO-Einstellung „Verwendung der gemeinsam genutzten Internetverbindung im eigenen DNS-Domänennetzwerk nicht zulassen“ blockiert werden.
|||         

<br />          

## <a name="ip-helper"></a>IP-Hilfsprogramm            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt Tunnelkonnektivität mithilfe von IPv6-Übergangstechnologien (IP6-zu-IP4, ISATAP, Portproxy und Teredo) und IP-HTTPS bereit. Wenn der Dienst beendet wird, verfügt der Computer nicht über die durch diese Technologien ermöglichten Konnektivitätsvorteile.
|   **Dienstname**    |   iphlpsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          


##  <a name="ipsec-policy-agent"></a>IPsec-Richtlinien-Agent      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   IPsec (Internetprotokollsicherheit) unterstützt die Peerauthentifizierung auf Netzwerkebene, die Datenursprungsauthentifizierung, die Datenintegrität, die Datenvertraulichkeit (Verschlüsselung) und den Replay-Schutz.  Dieser Dienst erzwingt IPsec-Richtlinien, die mit dem Snap-In „IP-Sicherheitsrichtlinien“ oder dem Befehlszeilentool „netsh ipsec“ erstellt wurden.  Wenn du diesen Dienst beendest, treten unter Umständen Probleme mit der Netzwerkkonnektivität auf, falls es für deine Richtlinie erforderlich ist, dass für Verbindungen IPsec genutzt wird.  Darüber hinaus ist die Remoteverwaltung der Windows-Firewall nicht verfügbar, wenn dieser Dienst beendet wird.
|   **Dienstname**    |   PolicyAgent
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />

##  <a name="kdc-proxy-server-service-kps"></a>KDC-Proxyserverdienst (KPS)      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der KDC-Proxyserverdienst wird auf Edgeservern ausgeführt, um als Proxy für Kerberos-Protokollnachrichten für Domänencontroller im Unternehmensnetzwerk zu fungieren.
|   **Dienstname**    |   KPSSVC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis    
|   **Kommentare**    |   
|||         

<br />          

## <a name="ktmrm-for-distributed-transaction-coordinator"></a>KtmRm für Distributed Transaction Coordinator            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Koordiniert Transaktionen zwischen dem Distributed Transaction Coordinator (MSDTC) und dem Kerneltransaktions-Manager (KTM). Wir empfehlen dir, diesen Dienst zu beenden, falls er nicht benötigt wird. Falls der Dienst benötigt wird, wird er sowohl vom MSDTC als auch vom KTM automatisch gestartet. Wenn dieser Dienst deaktiviert ist, tritt für alle MSDTC-Transaktionen, die mit einem Kernelressourcen-Manager interagieren, ein Fehler auf. Alle Dienste, die explizit davon abhängen, können nicht gestartet werden.
|   **Dienstname**    |   KtmRm
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />

##  <a name="link-layer-topology-discovery-mapper"></a>Verbindungsschicht-Topologieerkennungs-Zuordnungsprogramm        

| | |       
|---|---|       
|   **Dienstbeschreibung** |   Erstellt eine Netzwerkübersicht mit Computer- und Gerätetopologieinformationen (d. h. Konnektivitätsinformationen) sowie Metadaten, die jeden PC und jedes Gerät beschreiben.  Wenn dieser Dienst deaktiviert wird, funktioniert die Netzwerkübersicht nicht richtig.
|   **Dienstname**    |   lltdsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Kann deaktiviert werden, wenn keine Abhängigkeiten von der Netzwerkübersicht bestehen.
|||         

<br />

## <a name="local-session-manager"></a>Lokaler Sitzungs-Manager                    

| | |                   
|---|---|   
|   **Dienstbeschreibung** |   Windows-Kerndienst, der lokale Benutzersitzungen verwaltet. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems.    
|   **Dienstname**    |   LSM |
|   **Installation**    |   Immer installiert    |
|   **Starttyp**   |   Automatisch   |
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||                 

<br />                  

## <a name="microsoft-r-diagnostics-hub-standard-collector"></a>Standardsammlungsdienst des Microsoft(R)-Diagnose-Hubs         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Windows-Kerndienst, der lokale Benutzersitzungen verwaltet. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems.
|   **Dienstname**    |   LSM
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />

## <a name="microsoft-account-sign-in-assistant"></a>Anmelde-Assistent für Microsoft-Konten
| | |
|---|---|
|   **Dienstbeschreibung** |   Ermöglicht die Benutzeranmeldung über die Identitätsdienste des Microsoft-Kontos. Wenn dieser Dienst beendet wird, können sich Benutzer nicht mehr mit ihrem Microsoft-Konto am Computer anmelden.
|   **Dienstname**    |   wlidsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Microsoft-Konten sind unter Windows Server nicht verfügbar.
|||

<br />          

##  <a name="microsoft-app-v-client"></a>Microsoft App-V Client      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dient zum Verwalten von App-V-Benutzern und virtuellen Anwendungen.
|   **Dienstname**    |   AppVClient
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

## <a name="microsoft-iscsi-initiator-service"></a>Microsoft iSCSI-Initiator-Dienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dient zum Verwalten von iSCSI-Sitzungen (Internet SCSI) von diesem Computer zu iSCSI-Remotezielgeräten. Wenn dieser Dienst beendet wird, kann sich dieser Computer nicht an iSCSI-Zielen anmelden und nicht darauf zugreifen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   MSiSCSI
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Unsere Diagnosedaten deuten darauf hin, dass dieser Dienst auf Clients und auf Servern genutzt wird. Die Deaktivierung hat keinerlei Vorteile.
|||         

<br />          

## <a name="microsoft-passport"></a>Microsoft Passport           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht eine Prozessisolation für Kryptografieschlüssel, die zum Authentifizieren der zugeordneten Identitätsanbieter eines Benutzers verwendet werden. Wenn dieser Dienst deaktiviert wird, ist die gesamte Anwendung und Verwaltung dieser Schlüssel nicht verfügbar. Dies gilt auch für die Computeranmeldung und einmaliges Anmelden für Apps und Websites. Dieser Dienst wird automatisch gestartet und beendet. Wir empfehlen dir, diesen Dienst nicht neu zu konfigurieren.
|   **Dienstname**    |   NgcSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Wird für PIN/Hello-Anmeldungen benötigt, die auf dem Server nicht unterstützt werden.
|||         

<br />          

## <a name="microsoft-passport-container"></a>Microsoft Passport-Container         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet lokale Benutzeridentitätsschlüssel, um Benutzer für Identitätsanbieter und virtuelle TPM-Smartcards zu authentifizieren. Wenn dieser Dienst deaktiviert wird, kann nicht auf lokale Benutzeridentitätsschlüssel und virtuelle TPM-Smartcards zugegriffen werden. Wir empfehlen dir, diesen Dienst nicht neu zu konfigurieren.
|   **Dienstname**    |   NgcCtnrSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="microsoft-software-shadow-copy-provider"></a>Microsoft-Softwareschattenkopie-Anbieter          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet softwarebasierte Volumeschattenkopien des Volumeschattenkopie-Diensts. Softwarebasierte Volumeschattenkopien können nicht verwaltet werden, wenn dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   swprv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="microsoft-storage-spaces-smp"></a>Microsoft-SMP für Speicherplätze         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Hostdienst für den Microsoft-Verwaltungsanbieter für Speicherplätze. Wird dieser Dienst beendet oder deaktiviert, ist die Verwaltung von Speicherplätzen nicht mehr möglich.
|   **Dienstname**    |   smphost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Für APIs für die Speicherverwaltung tritt ohne diesen Dienst ein Fehler auf. Beispiel: "Get-WmiObject -class MSFT_Disk -Namespace Root\Microsoft\Windows\Storage".
|||         

<br />          

## <a name="nettcp-port-sharing-service"></a>Net.Tcp-Portfreigabedienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Freigabe von TCP-Ports über das net.tcp-Protokoll.
|   **Dienstname**    |   NetTcpPortSharing
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

## <a name="netlogon"></a>Netlogon         

| | |           
|---|---|           
|   **Dienstbeschreibung** |   Dient zum Verwalten eines sicheren Kanals zwischen diesem Computer und dem Domänencontroller für die Authentifizierung von Benutzern und Diensten. Wenn dieser Dienst angehalten wird, kann der Computer Benutzer und Dienste möglicherweise nicht authentifizieren, und der Domänencontroller kann keine DNS-Datensätze registrieren. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   Netlogon
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="network-connection-broker"></a>Netzwerkverbindungsbroker            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Fungiert als Broker für Verbindungen, über die Microsoft Store-Apps Benachrichtigungen über das Internet empfangen können.
|   **Dienstname**    |   NcbService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

##  <a name="network-connections"></a>Netzwerkverbindungen         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet Objekte im Ordner „Netzwerk- und Wählverbindungen“, in dem LAN- und Remoteverbindungen angezeigt werden.
|   **Dienstname**    |   Netman
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="network-connectivity-assistant"></a>Netzwerkkonnektivitäts-Assistent      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt die Benachrichtigung zum DirectAccess-Status für Komponenten der Benutzeroberfläche bereit.
|   **Dienstname**    |   NcaSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />  

##  <a name="network-list-service"></a>Netzwerklistendienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Identifiziert die Netzwerke, mit denen der Computer eine Verbindung hergestellt hat, sammelt und speichert Eigenschaften für diese Netzwerke und benachrichtigt Anwendungen, wenn sich diese Eigenschaften ändern.
|   **Dienstname**    |   netprofm
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="network-location-awareness"></a>NLA (Network Location Awareness)           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Sammelt und speichert Konfigurationsinformationen für das Netzwerk und benachrichtigt Programme, wenn diese Informationen geändert werden. Wenn dieser Dienst beendet wird, sind die Konfigurationsinformationen möglicherweise nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   NlaSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="network-setup-service"></a>Netzwerkeinrichtungsdienst       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Netzwerkeinrichtungsdienst verwaltet die Installation von Netzwerktreibern und ermöglicht die Konfiguration von Netzwerkeinstellungen auf unterer Ebene.  Wenn der Dienst beendet wird, werden aktuell ausgeführte Treiberinstallationen unter Umständen abgebrochen.
|   **Dienstname**    |   NetSetupSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="network-store-interface-service"></a>Netzwerkspeicher-Schnittstellendienst      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst stellt Netzwerkbenachrichtigungen (z. B. beim Hinzufügen/Löschen von Schnittstellen) für Benutzermodusclients bereit. Wenn du diesen Dienst beendest, wird die Netzwerkkonnektivität getrennt. Wenn dieser Dienst deaktiviert wird, können andere Dienste, die von diesem Dienst ausschließlich abhängig sind, nicht mehr gestartet werden.
|   **Dienstname**    |   nsi
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="offline-files"></a>Offlinedateien            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Der Offlinedateiendienst führt Wartungsaktivitäten am Cache für Offlinedateien aus, reagiert auf Benutzeranmelde- und -abmeldeereignisse, implementiert die internen Komponenten der öffentlichen API, leitet interessante Ereignisse an Empfänger weiter, die an Offlineaktivitäten interessiert sind, und ändert den Cachestatus.
|   **Dienstname**    |   CscService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

## <a name="optimize-drives"></a>Laufwerke optimieren          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Unterstützt den Computer bei einer effizienteren Ausführung durch das Optimieren von Dateien auf Speicherlaufwerken.
|   **Dienstname**    |   defragsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />

## <a name="performance-counter-dll-host"></a>Leistungsindikator-DLL-Host         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht Remotebenutzern und 64-Bit-Prozessen die Abfrage von Leistungsindikatoren, die von 32-Bit-DLLs bereitgestellt werden. Wenn dieser Dienst beendet wird, können nur lokale Benutzer und 32-Bit-Prozesse die von den 32-Bit-DLLs bereitgestellten Leistungsindikatoren abfragen.
|   **Dienstname**    |   PerfHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis    
|   **Kommentare**    |   
|||         

<br />          

## <a name="performance-logs--alerts"></a>Leistungsprotokolle und -warnungen            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   „Leistungsprotokolle und -warnungen“ sammelt Leistungsdaten von lokalen oder Remotecomputern basierend auf vorkonfigurierten Zeitplanparametern und schreibt die Daten dann in ein Protokoll oder löst eine Warnung aus. Wenn dieser Dienst beendet wird, werden keine Leistungsinformationen erfasst. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   pla
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="phone-service"></a>Telefondienst       

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet den Telefoniestatus des Geräts.
|   **Dienstname**    |   PhoneSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Wird von modernen VoIP-Apps verwendet.
|||         

<br />          

##      <a name="plug-and-play"></a>Plug & Play       

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht einem Computer die Erkennung und Anpassung an Hardwareänderungen mit nur wenigen oder ganz ohne Benutzereingaben. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems.
|   **Dienstname**    |   PlugPlay
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="portable-device-enumerator-service"></a>Enumeratordienst für tragbare Geräte           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Erzwingt Gruppenrichtlinien für Wechsel-Massenspeichergeräte. Ermöglicht Anwendungen wie Windows Media Player und dem Bildimport-Assistenten, Inhalte unter Verwendung von Wechsel-Massenspeichergeräten zu übertragen und zu synchronisieren.
|   **Dienstname**    |   WPDBusEnum
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="power"></a>Stromversorgung            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet die Energierichtlinie und die Zustellung der Energierichtlinienbenachrichtigung.
|   **Dienstname**    |   Stromversorgung
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="print-spooler"></a>Druckspooler:            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst spoolt Druckaufträge und verarbeitet Interaktionen mit dem Drucker.  Wenn du diesen Dienst ausschaltest, kannst du weder drucken noch Drucker anzeigen.
|   **Dienstname**    |   Spooler
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Kann deaktiviert werden, wenn es sich nicht um einen Druckerserver oder einen Domänencontroller handelt.
|   **Kommentare**    |   Auf einem Domänencontroller wird dem Spoolerdienst bei Installation der Domänencontroller-Rolle ein Thread hinzugefügt, der für die Durchführung der Druckbereinigung zuständig ist. Hiermit werden die veralteten Objekte der Druckwarteschlange aus Active Directory entfernt.  Wenn der Spoolerdienst nicht auf mindestens einem DC auf jeder Site ausgeführt wird, kann AD keine alten Warteschlangen entfernen, die nicht mehr vorhanden sind. https://blogs.technet.microsoft.com/askperf/2008/11/18/disabling-unnecessary-services-a-word-to-the-wise/
|||         

<br />          

##  <a name="printer-extensions-and-notifications"></a>Druckererweiterungen und Benachrichtigungen        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Mit diesem Dienst werden benutzerdefinierte Druckerdialogfelder geöffnet und Benachrichtigungen von einem Remotedruckerserver oder Drucker verarbeitet. Wenn du diesen Dienst deaktivierst, werden keine Druckererweiterungen oder Benachrichtigungen angezeigt.
|   **Dienstname**    |   PrintNotify
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Kann deaktiviert werden, wenn es sich nicht um einen Druckerserver handelt.
|   **Kommentare**    |   
|||         

<br />          

##  <a name="problem-reports-and-solutions-control-panel-support"></a>Unterstützung in der Systemsteuerung unter Lösungen für Probleme     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst bietet Unterstützung für das Anzeigen, Senden und Löschen von Problemberichten auf Systemebene für das Applet „Lösungen für Probleme“ in der Systemsteuerung.
|   **Dienstname**    |   wercplsupport
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="program-compatibility-assistant-service"></a>Programmkompatibilitäts-Assistent-Dienst     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst bietet Unterstützung für den Programmkompatibilitäts-Assistenten (Program Compatibility Assistant, PCA).  Mit dem PCA werden die vom Benutzer installierten und ausgeführten Programme überwacht. Wenn dieser Dienst beendet wird, wird der PCA nicht ordnungsgemäß ausgeführt.
|   **Dienstname**    |   PcaSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

##  <a name="quality-windows-audio-video-experience"></a>Verbessertes Audio-/Videostreaming unter Windows      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Windows-Dienst für verbessertes Audio/Video-Streaming (qWave) ist eine Netzwerkplattform für Audio/Video-Streaminganwendungen (AV) in privaten IP-Netzwerken. qWave verbessert die AV-Streamingleistung und -zuverlässigkeit, indem Netzwerk-QoS (Quality-of-Service) für AV-Anwendungen sichergestellt wird. Es werden Mechanismen für Zugangssteuerung, Laufzeitüberwachung und -erzwingung, Anwendungsfeedback sowie Verkehrspriorisierung bereitgestellt.
|   **Dienstname**    |   QWAVE
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Clientseitiger QoS-Dienst
|||         

<br />          

##      <a name="radio-management-service"></a>Funkverwaltungsdienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dienst für Funkverwaltung und Flugzeugmodus
|   **Dienstname**    |   RmSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-access-auto-connection-manager"></a>Verwaltung für automatische RAS-Verbindung            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Erstellt eine Verbindung mit einem Remotenetzwerk, wenn ein Programm auf einen Remote-DNS- oder -NetBIOS-Namen (bzw. eine Adresse) verweist.
|   **Dienstname**    |   RasAuto
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-access-connection-manager"></a>RAS-Verbindungs-Manager         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet Einwähl- und VPN-Verbindungen zwischen diesem Computer und dem Internet oder anderen Remotenetzwerken. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   RasMan
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-desktop-configuration"></a>Remotedesktopkonfiguration         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Remotedesktop-Konfigurationsdienst (Remote Desktop Configuration Service, RDCS) ist für alle Konfigurations- und Sitzungsverwaltungsaktivitäten im Zusammenhang mit den Remotedesktopdiensten und Remotedesktop zuständig, die den SYSTEM-Kontext erfordern. Dazu gehören die sitzungsspezifischen temporären Ordner, Remotedesktopthemen und Remotedesktopzertifikate.
|   **Dienstname**    |   SessionEnv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="remote-desktop-services"></a>Remotedesktopdienste          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht Benutzern das Herstellen einer interaktiven Verbindung mit einem Remotecomputer. Remotedesktop und Remotedesktop-Hostserver können nur zusammen mit diesem Dienst verwendet werden.  Wenn du die Remoteverwendung dieses Computers verhindern möchtest, muss du die Kontrollkästchen auf der Registerkarte „Remote“ in den Systemsteuerungsoptionen deaktivieren.
|   **Dienstname**    |   TermService
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   
|||         

<br />          

##  <a name="remote-desktop-services-usermode-port-redirector"></a>Anschlussumleitung für Remotedesktopdienst im Benutzermodus        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht die Umleitung von Druckern, Laufwerken und Anschlüssen für RDP-Verbindungen.
|   **Dienstname**    |   UmRdpService
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Unterstützt Umleitungen auf der Serverseite der Verbindung.
|||         

<br />          

## <a name="remote-procedure-call-rpc"></a>Remoteprozeduraufruf (RPC)          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der RPCSS-Dienst wird als Dienststeuerungs-Manager für COM- und DCOM-Server verwendet. Von ihm werden Objektaktivierungsanforderungen, Objektexporterauflösungen und die verteilte Garbage Collection für COM- und DCOM-Server ausgeführt. Wenn dieser Dienst beendet oder deaktiviert wird, werden Programme, für die COM oder DCOM verwendet wird, nicht ordnungsgemäß ausgeführt. Wir empfehlen dir dringend, den RPCSS-Dienst auszuführen.
|   **Dienstname**    |   RpcSs
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="remote-procedure-call-rpc-locator"></a>RPC-Locator             

| | |               
|---|---|   
|   **Dienstbeschreibung** |   Unter Windows 2003 und früheren Windows-Versionen wird mit dem RPC-Locatordienst (Remote Procedure Call) die RPC-Namensdienstdatenbank verwaltet. Unter Windows Vista und höheren Windows-Versionen stellt dieser Dienst keine Funktionalität bereit und ist nur für Zwecke der Anwendungskompatibilität vorhanden.   |
|   **Dienstname**    |   RpcLocator  |
|   **Installation**    |   Nur mit Desktopdarstellung    |
|   **Starttyp**   |   Manual  |
|   **Empfehlung**  | Kein Hinweis   |
|   **Kommentare**    |       |
|||             

<br />              

## <a name="remote-registry"></a>Remoteregistrierung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht es Remotebenutzern, Registrierungseinstellungen dieses Computers zu verändern. Wenn dieser Dienst beendet wird, kann die Registrierung nur von lokalen Benutzern dieses Computers verändert werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   RemoteRegistry
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   
|||         

<br />          

##  <a name="resultant-set-of-policy-provider"></a>Richtlinienergebnissatzanbieter            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt einen Netzwerkdienst bereit, der Anforderungen zum Simulieren der Anwendung von Gruppenrichtlinieneinstellungen auf einen Zielbenutzer oder -computer in verschiedenen Situationen verarbeitet und einen sich daraus ergebenden Satz von Richtlinieneinstellungen berechnet.
|   **Dienstname**    |   RSoPProv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |Kein Hinweis    
|   **Kommentare**    |   
|||         

<br />          

## <a name="routing-and-remote-access"></a>Routing und RAS            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Routingdienste in LAN- und WAN-Netzwerkumgebungen.
|   **Dienstname**    |   RemoteAccess
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   Bereits deaktiviert
|||         

<br />          

## <a name="rpc-endpoint-mapper"></a>RPC-Endpunktzuordnung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Löst RPC-Schnittstellen-IDs für den Transport von Endpunkten auf. Wenn dieser Dienst angehalten oder deaktiviert wird, können Programme, für die Remoteprozeduraufruf-Dienste (Remote Procedure Call, RPC) verwendet werden, nicht ordnungsgemäß ausgeführt werden.
|   **Dienstname**    |   RpcEptMapper
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="secondary-logon"></a>Sekundäre Anmeldung     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktiviert das Starten von Prozessen mit verschiedenen Anmeldeinformationen. Wenn dieser Dienst beendet wird, ist dieser Typ von Anmeldezugriff nicht mehr verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   seclogon
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="secure-socket-tunneling-protocol-service"></a>SSTP-Dienst            

| | |               
|---|---|       
|   **Dienstbeschreibung** |   Unterstützt SSTP (Secure Socket Tunneling-Protokoll), um über VPN eine Verbindung mit Remotecomputern herzustellen. Wenn dieser Dienst deaktiviert ist, können Benutzer SSTP nicht für den Zugriff auf Remoteserver verwenden.    |
|   **Dienstname**    |   SstpSvc |
|   **Installation**    |   Immer installiert    |
|   **Starttyp**   |   Manual  |
|   **Empfehlung**  |   Nicht deaktivieren  |
|   **Kommentare**    |   Wenn der Dienst deaktiviert wird, treten RRAS-Fehler auf.   |
|||             

<br />              

## <a name="security-accounts-manager"></a>Sicherheitskonto-Manager            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Durch den Start dieses Diensts wird anderen Diensten signalisiert, dass die Sicherheitskontenverwaltung (SAM) bereit ist, Anforderungen anzunehmen.  Wenn du diesen Dienst deaktivierst, wird verhindert, dass andere Dienste im System benachrichtigt werden, wenn die Sicherheitskontenverwaltung bereit ist. Dies kann wiederum dazu führen, dass diese Dienste nicht korrekt gestartet werden. Dieser Dienst sollte nicht deaktiviert werden.
|   **Dienstname**    |   SamSs
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Nicht deaktivieren
|   **Kommentare**    |   
|||         

<br />          

## <a name="sensor-data-service"></a>Sensordatendienst  

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Liefert Daten von verschiedenen Sensoren.
|   **Dienstname**    |   SensorDataService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />  

## <a name="sensor-monitoring-service"></a>Sensorüberwachungsdienst            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Überwacht verschiedene Sensoren, um Daten verfügbar zu machen und eine Anpassung an den System- und Benutzerstatus vorzunehmen.  Wird dieser Dienst beendet oder deaktiviert, wird die Anzeigehelligkeit nicht an die Lichtbedingungen der Umgebung angepasst. Das Beenden des Diensts kann auch andere Systemfeatures betreffen.
|   **Dienstname**    |   SensrSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br /><br/>
## <a name="sensor-servicebr--br------br---strongservice-descriptionstrong----a-service-for-sensors-that-manages-different-sensors39-functionality-manages-simple-device-orientation-sdo-and-history-for-sensors-loads-the-sdo-sensor-that-reports-device-orientation-changes--if-this-service-is-stopped-or-disabled-the-sdo-sensor-will-not-be-loaded-and-so-auto-rotation-will-not-occur-history-collection-from-sensors-will-also-be-stopped"></a>Sensordienst<br/>| | |<br/>|---|---|<br/>|   <strong>Dienstbeschreibung</strong> |   Ein Sensordienst, der verschiedene Sensorfunktionen verwaltet. Er verwaltet SDO (Simple Device Orientation) und den Verlauf für Sensoren und lädt den SDO-Sensor, der Änderungen der Geräteausrichtung meldet.  Wenn der Dienst beendet oder deaktiviert wird, wird der SDO-Sensor nicht geladen, und es findet keine automatische Drehung statt. Die Sammlung von Verlaufsdaten von den Sensoren wird ebenfalls beendet.
|   <strong>Dienstname</strong>    |   SensorService |   <strong>Installation</strong>    |   Nur mit Desktopdarstellung |   <strong>Starttyp</strong>   |   Manuell |   <strong>Empfehlung</strong>  |   Deaktivierung OK |   <strong>Kommentare</strong>    |<br/>|||<br/>
<br />          

## <a name="server"></a>Server           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Unterstützt Datei-, Drucker- und Named-Piped-Freigabe für diesen Computer über das Netzwerk. Diese Funktionen sind nicht mehr verfügbar, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   LanmanServer
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Wird für die Remoteverwaltung, IPC$ und SMB-Dateifreigabe benötigt.
|||         

<br />          

## <a name="shell-hardware-detection"></a>Shellhardwareerkennung             

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Zeigt Meldungen für Hardwareereignisse für automatische Wiedergabe an.
|   **Dienstname**    |   ShellHWDetection
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="smart-card"></a>Smartcard           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet den Zugriff auf Smartcards, die von diesem Computer gelesen werden. Wenn dieser Dienst beendet wird, kann der Computer keine Smartcards mehr lesen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   SCardSvr
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

## <a name="smart-card-device-enumeration-service"></a>Smartcard-Geräteaufzählungsdienst                    

| | |               
|---|---|       
|   **Dienstbeschreibung** |   Erstellt Softwaregeräteknoten für alle Smartcardleser, die einer bestimmten Sitzung zur Verfügung stehen. Wird dieser Dienst deaktiviert, können von WinRT-APIs keine Smartcardleser aufgezählt werden.   |
|   **Dienstname**    |   ScDeviceEnum    |
|   **Installation**    |   Immer installiert    |
|   **Starttyp**   |   Manual  |
|   **Empfehlung**  |   Deaktivierung OK   |
|   **Kommentare**    |   Wird fast ausschließlich für WinRT-Apps benötigt.    |
|||             

<br />              

## <a name="smart-card-removal-policy"></a>Richtlinie zum Entfernen der Smartcard        

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Lässt eine Konfiguration des Systems zu, bei der der Benutzerdesktop beim Entfernen der Smartcard gesperrt wird.
|   **Dienstname**    |   SCPolicySvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="snmp-trap"></a>SNMP-Trap            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Empfängt Trap-Nachrichten, die von lokalen oder Remote-SNMP-Agents generiert wurden, und leitet die Nachrichten an SNMP-Verwaltungsprogramme weiter, die auf diesem Computer ausgeführt werden. SNMP-basierte Programme auf diesem Computer empfangen keine SNMP-Trap-Nachrichten, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   SNMPTRAP
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="software-protection"></a>Softwareschutz             

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Aktiviert das Herunterladen, die Installation und die Durchsetzung digitaler Lizenzen für Windows und Windows-Anwendungen. Wenn der Dienst deaktiviert wird, werden das Betriebssystem und lizenzierte Anwendungen in einem Benachrichtigungsmodus ausgeführt. Es wird dringend empfohlen, den Softwareschutzdienst nicht zu deaktivieren.
|   **Dienstname**    |   sppsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="special-administration-console-helper"></a>Hilfsprogramm für spezielle Verwaltungskonsole        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht Administratoren über die Notverwaltungsdienste (Emergency Management Services, EMS) den Remotezugriff auf eine Eingabeaufforderung.
|   **Dienstname**    |   sacsvr
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="spot-verifier"></a>Echtzeit-Datenträgerprüfung            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Überprüft mögliche Beschädigungen des Dateisystems.
|   **Dienstname**    |   svsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="ssdp-discovery"></a>SSDP-Suche           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Sucht nach Netzwerkgeräten und -diensten, die das SSDP-Suchprotokoll verwenden, z. B. UPnP-Geräte. Kündigt zudem SSDP-Geräte und -dienste an, die auf dem lokalen Computer ausgeführt werden. Wenn dieser Dienst beendet wird, werden SSDP-basierte Geräte nicht entdeckt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   SSDPSRV
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="state-repository-service"></a>StateRepository-Dienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet die erforderliche Infrastrukturunterstützung für das Anwendungsmodell.
|   **Dienstname**    |   StateRepository
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="still-image-acquisition-events"></a>Ereignisse zum Abrufen von Standbildern

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Startet Anwendungen im Zusammenhang mit Ereignissen zum Abrufen von Standbildern.
|   **Dienstname**    |   WiaRpc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />  

## <a name="storage-service"></a>Speicherdienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt Unterstützungsdienste für Speichereinstellungen und externe Speichererweiterung bereit.
|   **Dienstname**    |   StorSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="storage-tiers-management"></a>Storage Tiers Management        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Optimiert die Verteilung der Daten auf den Speicherstufen für alle mehrstufigen Speicherplätze im System.
|   **Dienstname**    |   TieringEngineService
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="superfetch"></a>Superfetch          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet und verbessert die Systemleistung im Zeitablauf.
|   **Dienstname**    |   SysMain
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="sync-host"></a>Synchronisierungshost            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst synchronisiert E-Mail-, Kontakt-, Kalender- und verschiedene andere Benutzerdaten. Wenn dieser Dienst nicht ausgeführt wird, funktionieren E-Mail-Programme und andere Anwendungen, die von dieser Funktionalität abhängig sind, nicht ordnungsgemäß.
|   **Dienstname**    |   OneSyncSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Benutzerdienstvorlage
|||         

<br />          

## <a name="system-event-notification-service"></a>Benachrichtigungsdienst für Systemereignisse            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Überwacht Systemereignisse und benachrichtigt Abonnenten des COM+-Ereignissystems bei diesen Ereignissen.
|   **Dienstname**    |   SENS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="system-events-broker"></a>Systemereignissebroker             

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Koordiniert die Ausführung der Hintergrundvorgänge für WinRT-Anwendungen. Wird dieser Dienst beendet oder deaktiviert, werden die Hintergrundvorgänge unter Umständen nicht ausgelöst.
|   **Dienstname**    |   SystemEventsBroker
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   In der Beschreibung wird nur die Nutzung für WinRT-Apps erwähnt, aber der Dienst wird auch für die Aufgabenplanung, den Brokerinfrastrukturdienst und andere interne Komponenten benötigt.
|||         

<br />          

## <a name="task-scheduler"></a>Aufgabenplanung           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht es einem Benutzer, automatische Aufgaben auf diesem Computer zu konfigurieren und zu planen. Der Dienst hostet auch mehrere kritische Aufgaben für das Windows-System. Wenn dieser Dienst beendet oder deaktiviert wird, werden diese Vorgänge nicht zu den geplanten Zeiten ausgeführt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   Zeitplan
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="tcpip-netbios-helper"></a>TCP/IP-NetBIOS-Hilfsdienst            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Unterstützung für den NetBIOS-über-TCP/IP-Dienst (NetBT) und die NetBIOS-Namensauflösung für Clients im Netzwerk, sodass Benutzer Daten gemeinsam nutzen, drucken und sich am Netzwerk anmelden können. Diese Funktionen sind nicht mehr verfügbar, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   lmhosts
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="telephony"></a>Telephony           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet Telefonie-API-Unterstützung (TAPI) für Programme, die lokale und über das LAN auf Servern (die diesen Dienst ebenfalls ausführen) angebundene Telefoniegeräte steuern.
|   **Dienstname**    |   TapiSrv
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Wenn der Dienst deaktiviert wird, treten RRAS-Fehler auf.
|||         

<br />          

## <a name="themes"></a>Designs           

| | |           
|---|---|
|   **Dienstbeschreibung** |   Stellt die Designverwaltung zur Verfügung.
|   **Dienstname**    |   Designs
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Es können keine Designs für Barrierefreiheit festgelegt werden, wenn dieser Dienst deaktiviert ist.
|||         

<br />  

## <a name="tile-data-model-server"></a>Kacheldaten-Modellserver           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Kachelserver zur Kachelaktualisierung.
|   **Dienstname**    |   tiledatamodelsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Wenn dieser Dienst deaktiviert wird, tritt für das Startmenü ein Fehler auf.
|||         

<br />          

##  <a name="time-broker"></a>Zeitbroker     

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Koordiniert die Ausführung der Hintergrundvorgänge für WinRT-Anwendungen. Wird dieser Dienst beendet oder deaktiviert, werden die Hintergrundvorgänge unter Umständen nicht ausgelöst.
|   **Dienstname**    |   TimeBrokerSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   In der Beschreibung wird nur die Nutzung für WinRT-Apps erwähnt, aber der Dienst wird auch für die Aufgabenplanung, den Brokerinfrastrukturdienst und andere interne Komponenten benötigt.
|||         

<br />          

## <a name="touch-keyboard-and-handwriting-panel-service"></a>Dienst für Bildschirmtastatur und Schreibbereich         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Aktiviert die Stift- und Freihandfunktionalität der Bildschirmtastatur und des Schreibbereichs.
|   **Dienstname**    |   TabletInputService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="update-orchestrator-service-for-windows-update"></a>Update Orchestrator Service für Windows Update           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet Windows-Updates. Wenn der Dienst beendet wird, können auf deinen Geräten keine aktuellen Updates heruntergeladen und installiert werden.
|   **Dienstname**    |   UsoSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   In v1607 hat die Dienstbeschreibung gefehlt. Dieser Dienst wird für Windows Update (inkl. WSUS) benötigt.
|||         

<br />          

## <a name="upnp-device-host"></a>UPnP-Gerätehost         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht es, dass UPnP-Geräte auf diesem Computer gehostet werden können. Wenn dieser Dienst beendet wird, sind alle gehosteten UPnP-Geräte nicht mehr betriebsbereit, und es können keine weiteren gehosteten Geräte hinzugefügt werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   upnphost
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="user-access-logging-service"></a>Dienst für die Benutzerzugriffsprotokollierung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Mithilfe dieses Diensts werden eindeutige Clientzugriffsanforderungen in Form von IP-Adressen und Benutzernamen von auf dem lokalen Server installierten Produkten und Rollen protokolliert. Diese Informationen können über PowerShell von Administratoren abgefragt werden, die den Clientbedarf an Serversoftware für die Offlineverwaltung von Clientzugriffslizenzen (Client Access License, CAL) berechnen müssen. Wenn der Dienst deaktiviert wird, werden Clientanforderungen nicht protokolliert und sind daher nicht über PowerShell-Abfragen abrufbar. Wird der Dienst beendet, so beeinflusst dies nicht die Abfrage von Verlaufsdaten. (Schritte zum Löschen von Verlaufsdaten findest du in der begleitenden Dokumentation.) Der lokale Systemadministrator muss in den Windows Server-Lizenzbedingungen die Anzahl von Clientzugriffslizenzen festlegen, die für eine ordnungsgemäße Lizenzierung der Serversoftware erforderlich ist. Die Verwendung des UAL-Diensts und der UAL-Daten entbinden nicht von dieser Verpflichtung.
|   **Dienstname**    |   UALSVC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="user-data-access"></a>Benutzerdatenzugriff        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht Apps den Zugriff auf strukturierte Benutzerdaten, z. B. Kontaktinformationen, Kalender, Nachrichten und andere Inhalte. Wenn du diesen Dienst beendest oder deaktivierst, funktionieren Apps, die diese Daten verwenden, möglicherweise nicht ordnungsgemäß.
|   **Dienstname**    |   UserDataSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Benutzerdienstvorlage
|||         

<br />          

## <a name="user-data-storage"></a>Benutzerdatenspeicher            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verarbeitet die Speicherung strukturierter Benutzerdaten, z. B. Kontaktinformationen, Kalender, Nachrichten und andere Inhalte. Wenn du diesen Dienst beendest oder deaktivierst, funktionieren Apps, die diese Daten verwenden, möglicherweise nicht ordnungsgemäß.
|   **Dienstname**    |   UnistoreSvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Benutzerdienstvorlage
|||         

<br />          

## <a name="user-experience-virtualization-service"></a>User Experience Virtualization-Dienst           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt Unterstützung für das Roaming von Anwendungen und Betriebssystemeinstellungen bereit.
|   **Dienstname**    |   UevAgentService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

##  <a name="user-manager"></a>Benutzer-Manager        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Benutzer-Manager stellt die Laufzeitkomponenten bereit, die für Interaktionen mit mehreren Benutzern erforderlich sind.  Wenn dieser Dienst beendet wird, funktionieren einige Anwendungen möglicherweise nicht korrekt.
|   **Dienstname**    |   UserManager
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="user-profile-service"></a>Benutzerprofildienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst ist für das Laden und Entladen von Benutzerprofilen verantwortlich. Wenn dieser Dienst beendet oder deaktiviert ist, können Benutzer sich nicht mehr an- oder abmelden. Zudem können Probleme beim Abrufen von Benutzerdaten für Apps auftreten, und Komponenten, die für den Empfang von Profilereignisbenachrichtigungen registriert sind, erhalten keine Benachrichtigungen.
|   **Dienstname**    |   ProfSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="virtual-disk"></a>Virtueller Datenträger             

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Verwaltungsdienste für Datenträger, Volumes, Dateisysteme und Speicherarrays bereit.
|   **Dienstname**    |   vds
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Kein Hinweis
|   **Kommentare**    |   
|||         

<br />          

## <a name="volume-shadow-copy"></a>Volumeschattenkopie           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Verwaltet und implementiert Volumeschattenkopien, die zu Sicherungs- und anderen Zwecken verwendet werden. Wenn dieser Dienst beendet wird, sind keine Schattenkopien für Sicherungen verfügbar, und die Sicherung kann eventuell fehlschlagen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   VSS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Kein Hinweis
|   **Kommentare**    |   
|||         

<br />          

##  <a name="walletservice"></a>WalletService           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Von Clients der Funktion „Brieftasche“ verwendete Hostobjekte.
|   **Dienstname**    |   WalletService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-audio"></a>Windows-Audio            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Verwaltet Audioinhalte für Windows-basierte Programme.  Wenn dieser Dienst beendet wird, funktionieren Audiogeräte und -effekte nicht ordnungsgemäß.  Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden.
|   **Dienstname**    |   Audiosrv
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-audio-endpoint-builder"></a>Windows-Audio-Endpunkterstellung           

| | |           
|---|---|
|   **Dienstbeschreibung** |   Verwaltet Audiogeräte für den Windows-Audiodienst.  Wenn dieser Dienst beendet wird, funktionieren Audiogeräte und -effekte nicht ordnungsgemäß.  Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden.
|   **Dienstname**    |   AudioEndpointBuilder
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-biometric-service"></a>Windows-Biometriedienst            

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Mit dem Windows-Biometriedienst können in Clientanwendungen biometrische Daten erfasst, verglichen, geändert und gespeichert werden, ohne dass ein direkter Zugriff auf biometrische Hardware oder Proben erfolgt. Der Dienst wird in einem privilegierten SVCHOST-Prozess gehostet.
|   **Dienstname**    |   WbioSrvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-camera-frame-server"></a>Windows-Kamera-FrameServer         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht mehreren Clients den Zugriff auf Videoframes von Kameras.
|   **Dienstname**    |   FrameServer
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-connection-manager"></a>Windows-Verbindungs-Manager           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Anhand der aktuell auf dem PC verfügbaren Netzwerkkonnektivitätsoptionen wird die Verbindung automatisch hergestellt oder getrennt. Zudem kann die Netzwerkkonnektivität mithilfe von Gruppenrichtlinieneinstellungen verwaltet werden.
|   **Dienstname**    |   Wcmsvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-defender-network-inspection-service"></a>Windows Defender-Netzwerkinspektionsdienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Schützt gegen Eindringversuche bei bekannten und neu erkannten Sicherheitsrisiken von Netzwerkprotokollen.
|   **Dienstname**    |   WdNisSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis    
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-defender-service"></a>Windows Defender-Dienst         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Schützt Benutzer vor Schadsoftware und weiterer potenziell unerwünschter Software.
|   **Dienstname**    |   WinDefend
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-driver-foundation---user-mode-driver-framework"></a>Windows Driver Foundation – Benutzermodus-Treiberframework           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Erstellt und verwaltet Benutzermodus-Treiberprozesse. Der Dienst kann nicht beendet werden.
|   **Dienstname**    |   wudfsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-encryption-provider-host-service"></a>Hostdienst für Windows Encryption Provider     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Der Hostdienst für Windows Encryption Provider vermittelt Verschlüsselungsfunktionen von Drittanbieter-Verschlüsselungsanbietern an Prozesse, die EAS-Richtlinien bewerten und anwenden müssen. Wenn dieser Dienst beendet wird, sind die EAS-Kompatibilitätsüberprüfungen gefährdet, die von den verbundenen E-Mail-Konten eingerichtet wurden.
|   **Dienstname**    |   WEPHOSTSVC
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-error-reporting-service"></a>Windows-Fehlerberichterstattungsdienst          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Berichterstattung von Fehlern bei nicht mehr funktionierenden und reagierenden Programmen und das Angeben von Lösungen. Ermöglicht außerdem das Generieren von Protokollen für Diagnose- und Reparaturdienste. Wenn dieser Dienst beendet wird, funktioniert die Fehlerberichterstattung möglicherweise nicht ordnungsgemäß, und die Ergebnisse von Diagnosediensten und Reparaturen werden möglicherweise nicht angezeigt.
|   **Dienstname**    |   WerSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Erfasst und sendet Daten zu Abstürzen und zum Hängen, die sowohl von MS als auch von Dritten (ISVs/IHVs) genutzt werden. Die Daten werden zum Diagnostizieren von Fehlern verwendet, die zu Abstürzen führen können. Dies können auch Sicherheitsfehler sein. Wird auch für die Fehlerberichterstattung in Unternehmen benötigt.
|||         

<br />          

## <a name="windows-event-collector"></a>Windows-Ereignissammlung          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst verwaltet permanente Abonnements für Ereignisse von Remotequellen, die das WS-Verwaltungsprotokoll unterstützen. Hierzu gehören Windows Vista-Ereignisprotokolle sowie Hardware- und IPMI-fähige Ereignisquellen. Der Dienst speichert weitergeleitete Ereignisse in einem lokalen Ereignisprotokoll. Falls dieser Dienst beendet oder deaktiviert wird, können Ereignisabonnements nicht erstellt und weitergeleitete Ereignisse nicht angenommen werden.
|   **Dienstname**    |   Wecsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Erfasst ETW-Ereignisse (z. B. Sicherheitsereignisse) für Verwaltungs- und Diagnosezwecke.  Von diesem Dienst sind viele Features und Drittanbietertools abhängig, z. B. Tools für die Sicherheitsüberwachung.
|||         

<br />          

## <a name="windows-event-log"></a>Windows-Ereignisprotokoll            

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Dieser Dienst verwaltet Ereignisse und Ereignisprotokolle. Er unterstützt die Protokollierung, die Abfrage und das Abonnement von Ereignissen sowie die Archivierung von Ereignisprotokollen und die Verwaltung von Ereignismetadaten. Er kann Ereignisse im XML- und Nur-Text-Format anzeigen. Durch das Beenden dieses Diensts können die Sicherheit und Zuverlässigkeit des Systems beeinträchtigt werden.
|   **Dienstname**    |   EventLog
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-firewall"></a>Windows-Firewall         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Die Windows-Firewall trägt zum Schutz des Computers bei, indem der Zugriff durch nicht autorisierte Benutzer auf den Computer über das Internet bzw. ein Netzwerk verhindert wird.
|   **Dienstname**    |   MpsSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-font-cache-service"></a>Windows-Dienst für Schriftartencache      

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Optimiert die Leistung von Anwendungen durch das Speichern häufig verwendeter Schriftartendaten. Dieser Dienst wird von Anwendungen gestartet, wenn er nicht bereits ausgeführt wird. Er kann deaktiviert werden, aber dadurch wird die Leistung von Anwendungen herabgesetzt.
|   **Dienstname**    |   FontCache
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-image-acquisition-wia"></a>Windows-Bilderfassung (WIA)          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Bilderfassungsdienste für Scanner und Kameras zur Verfügung.
|   **Dienstname**    |   stisvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-insider-service"></a>Windows-Insider-Dienst     

| | |           
|---|---|   
|   **Dienstbeschreibung** |   wisvc
|   **Dienstname**    |   wisvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Für Server wird das Test-Flighting nicht unterstützt, sodass darauf kein Vorgang durchgeführt wird. Das Feature kann auch per Gruppenrichtlinie deaktiviert werden.
|||         

<br />          

##  <a name="windows-installer"></a>Windows Installer       

| | |           
|---|---|
|   **Dienstbeschreibung** |   Fügt Anwendungen, die als Windows Installer-Paket (*.msi, *.msp) angeboten werden, hinzu bzw. ändert oder entfernt sie. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   msiserver
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-license-manager-service"></a>Windows-Lizenz-Manager-Dienst          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Infrastrukturunterstützung für den Microsoft Store bereit.  Der Dienst wird bei Bedarf gestartet, und bei einer Deaktivierung verhalten sich im Windows Store erworbene Inhalte nicht ordnungsgemäß.
|   **Dienstname**    |   LicenseManager
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-management-instrumentation"></a>Windows-Verwaltungsinstrumentation       

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Bietet eine standardmäßige Schnittstelle und ein Objektmodell zum Zugreifen auf Verwaltungsinformationen über das Betriebssystem, Geräte, Anwendungen und Dienste. Die meiste Windows-basierte Software kann nicht ordnungsgemäß ausgeführt werden, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   Winmgmt
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-mobile-hotspot-service"></a>Windows-Dienst für mobile Hotspots          

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Ermöglicht die Freigabe einer Datenverbindung für ein anderes Gerät.
|   **Dienstname**    |   icssvc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-modules-installer"></a>Windows Modules Installer        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Ermöglicht das Installieren, Ändern und Entfernen von Windows-Updates und optionalen Komponenten. Wenn dieser Dienst deaktiviert ist, können beim Installieren oder Deinstallieren von Windows-Updates auf diesem Computer Fehler auftreten.
|   **Dienstname**    |   TrustedInstaller
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-push-notifications-system-service"></a>Windows-Pushbenachrichtigungssystemdienst            

| | |           
|---|---|
|   **Dienstbeschreibung** |   Der Dienst wird in Sitzung 0 ausgeführt und hostet die Benachrichtigungsplattform und den Verbindungsanbieter, der die Verbindung zwischen Gerät und WNS-Server behandelt.
|   **Dienstname**    |   WpnService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Wird für Live-Kacheln und andere Features benötigt.
|||         

<br />      

## <a name="windows-push-notifications-user-service"></a>Windows-Pushbenachrichtigungs-Benutzerdienst          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst hostet die Windows-Benachrichtigungsplattform, die lokale Benachrichtigungen und Pushbenachrichtigungen unterstützt. Unterstützt werden Kachel-, Popup- und unformatierte Benachrichtigungen.
|   **Dienstname**    |   WpnUserService
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung OK
|   **Kommentare**    |   Benutzerdienstvorlage
|||         

<br />

## <a name="windows-remote-management-ws-management"></a>Windows-Remoteverwaltung (WS-Verwaltung)
| | |
|---|---|
|   **Dienstbeschreibung** |   Mit dem Windows-Remoteverwaltungsdienst (WinRM) wird das WS-Verwaltungsprotokoll für die Remoteverwaltung implementiert. Die WS-Verwaltung stellt ein Standard-Webdienst-Protokoll dar, das für die Remote-Software- und Hardware-Verwaltung verwendet wird. Der WinRM-Dienst durchsucht das Netzwerk nach WS-Verwaltungsanforderungen und verarbeitet diese. Der WinRM-Dienst muss mit einem „Listener“ unter Verwendung des Befehlszeilenprogramms winrm.cmd oder über die Gruppenrichtlinie konfiguriert werden, um im Netzwerk „lauschen“ zu können. Der WinRM-Dienst stellt einen Zugriff auf WMI-Daten bereit und ermöglicht eine Ereignissammlung. Die Ereignissammlung und das Abonnieren von Ereignissen machen es erforderlich, dass der Dienst ausgeführt wird. WinRM-Nachrichten verwenden HTTP oder HTTPS als Transporte. Der WinRM-Dienst ist nicht von IIS abhängig, er wird jedoch vorkonfiguriert, um auf demselben Computer einen Port mit IIS zu teilen.  Der WinRM-Dienst reserviert das URL-Präfix „/wsman“. Um Konflikten mit IIS vorzubeugen, sollten Administratoren sicherstellen, dass keine auf IIS gehostete Website das URL-Präfix „/wsman“ verwendet.
|   **Dienstname**    |   WinRM
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Wird für die Remoteverwaltung benötigt.
|||

<br />          

##  <a name="windows-search"></a>Windows Search      

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Stellt Inhaltsindizierung, Eigenschaftenzwischenspeicherung und Suchergebnisse für Dateien, E-Mails und andere Inhalte bereit.
|   **Dienstname**    |   WSearch
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         

<br />          

##  <a name="windows-time"></a>Windows-Zeitdienst        

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Behält Datums- und Zeitsynchronisation auf allen Clients und Servern im Netzwerk bei. Wenn dieser Dienst beendet wurde, sind Zeit- und Datumssynchronisierung nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   W32Time
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis
|   **Kommentare**    |   
|||         

<br />          

## <a name="windows-update"></a>Windows Update           

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Erkennung, Download und Installation von Updates für Windows und andere Programme. Wenn der Dienst deaktiviert ist, können „Windows Update“ bzw. das Feature „Automatische Updates“ nicht verwendet werden. Außerdem können Programme dann die Windows Update-Agent-Anwendungsprogrammierschnittstelle (WUA API) nicht verwenden.
|   **Dienstname**    |   wuauserv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="winhttp-web-proxy-auto-discovery-service"></a>WinHTTP-Web Proxy Auto-Discovery-Dienst         

| | |           
|---|---|   
|   **Dienstbeschreibung** |   WinHTTP implementiert den HTTP-Clientstapel und bietet Entwicklern eine Win32-API und COM-Automatisierungskomponente zum Senden von HTTP-Anforderungen und zum Empfangen von Antworten. Außerdem unterstützt WinHTTP die automatische Erkennung von Proxykonfigurationen über die entsprechende Implementierung des WPAD-Protokolls (Web Proxy Auto-Discovery).
|   **Dienstname**    |   WinHttpAutoProxySvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Nicht deaktivieren
|   **Kommentare**    |   Alle Elemente, die den Netzwerkstapel nutzen, können über eine funktionale Abhängigkeit von diesem Dienst verfügen. Er wird von vielen Organisationen genutzt, um das Routing von HTTP-Proxys für interne Netzwerke zu konfigurieren.  Ohne diesen Dienst tritt für alle HTTP-Internetverbindungen mit internem Ursprung ein Fehler auf.
|||         

<br />          

## <a name="wired-autoconfig"></a>Automatische Konfiguration (verkabelt)         

| | |           
|---|---|       
|   **Dienstbeschreibung** |   Mit dem Dienst für die automatische Konfiguration von Kabelnetzwerken (DOT3SVC) wird eine IEEE 802.1X-Authentifizierung an Ethernet-Schnittstellen ausgeführt. Wenn bei der aktuellen verkabelten Netzwerkbereitstellung die 802.1X-Authentifizierung erzwungen wird, muss der DOT3SVC-Dienst so konfiguriert werden, dass eine Konnektivität auf der 2. Schicht hergestellt bzw. Zugriff auf Netzwerkressourcen ermöglicht wird. Der DOT3SVC-Dienst wirkt sich nicht auf Kabelnetzwerke aus, bei denen die 802.1X-Authentifizierung nicht erzwungen wird.
|   **Dienstname**    |   dot3svc
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis   
|   **Kommentare**    |   
|||         

<br />          

## <a name="wmi-performance-adapter"></a>WMI-Leistungsadapter          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Bietet Leistungsbibliotheksinformationen der Windows-Verwaltungsinstrumentationsanbieter für Clients im Netzwerk. Dieser Dienst wird nur ausgeführt, wenn das Leistungsdaten-Hilfsprogramm aktiviert ist.
|   **Dienstname**    |   wmiApSrv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manual
|   **Empfehlung**  | Kein Hinweis       
|   **Kommentare**    |   
|||         

<br />          

## <a name="workstation"></a>Arbeitsstation          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Erstellt und wartet Clientnetzwerkverbindungen mit Remoteservern unter Verwendung des SMB-Protokolls. Diese Verbindungen sind nicht mehr verfügbar, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden.
|   **Dienstname**    |   LanmanWorkstation
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Kein Hinweis       
|   **Kommentare**    |   
|||         

<br />

## <a name="xbox-live-auth-manager"></a>Xbox Live Authentifizierungs-Manager           

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Stellt Authentifizierungs- und Autorisierungsservices für Xbox Live bereit. Wenn dieser Dienst beendet wird, funktionieren einige Anwendungen möglicherweise nicht korrekt.
|   **Dienstname**    |   XblAuthManager
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung empfohlen
|   **Kommentare**    |   
|||         

<br />          

## <a name="xbox-live-game-save"></a>Xbox Live-Spiele speichern          

| | |           
|---|---|   
|   **Dienstbeschreibung** |   Dieser Dienst synchronisiert für Xbox Live-Spiele gespeicherte Daten.  Wenn der Dienst beendet wird, werden die gespeicherten Spieldaten für Xbox Live nicht hochgeladen bzw. heruntergeladen.
|   **Dienstname**    |   XblGameSave
|   **Installation**    |   Nur mit Desktopdarstellung
|   **Starttyp**   |   Manual
|   **Empfehlung**  |   Deaktivierung empfohlen
|   **Kommentare**    |   Dieser Dienst synchronisiert für Xbox Live-Spiele gespeicherte Daten.  Wenn der Dienst beendet wird, werden die gespeicherten Spieldaten für Xbox Live nicht hochgeladen bzw. heruntergeladen.
|||         

<br /> 
<br /> 

