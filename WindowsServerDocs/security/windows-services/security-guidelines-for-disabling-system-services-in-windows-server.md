---
title: Sicherheitsrichtlinien für Systemdienste in Windows Server2016
description: Sicherheitsrichtlinien für das Deaktivieren von Diensten in Windows Server2016 mit Desktopdarstellung
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: techgroup-security
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 5/22/2017
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
author: nirb
ms.author: nirb
ms.openlocfilehash: 8f60d5095a3e4cebdffba5d3c02c69bc06326b3a
ms.sourcegitcommit: 68952ac7a29d0e2f07023958ad949fecc1b783b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/30/2018
---
## <a name="guidance-on-disabling-system-services-on-windows-server-2016-with-desktop-experience"></a>Anleitung zum Deaktivieren der System-Dienste unter Windows Server2016 mit Desktopdarstellung

Gilt für: Windows Server 2016

Windows-Betriebssystem umfasst viele Systemdiensten, die wichtige Funktionen bereit. Unterschiedliche Dienste haben unterschiedliche Start Standardrichtlinien: Einige sind standardmäßig gestartet (automatisch), einige bei Bedarf (manuell), und einige sind standardmäßig deaktiviert und muss explizit aktiviert werden, bevor sie ausgeführt werden können. Diese Standardeinstellungen wurden sorgfältig für jeden Dienst zum Abstimmen von Leistung, Funktionalität und Sicherheit für typische Kunden ausgewählt.

Möglicherweise einige Enterprise-Kunden bevorzugen jedoch ein Gleichgewicht Sicherheit gezielter für ihre Windows-PCs und Server, verringert die Angriffsfläche auf das absolute Minimum und können daher vollständig deaktivieren Sie alle Dienste, die nicht in ihrer spezifischen Umgebung erforderlich sind. Für diese Kunden bietet Microsoft® die zugehörige Richtlinien in Bezug auf die Dienste für diesen Zweck deaktiviert werden können.

Die Anleitung ist für Windows Server2016 mit Desktopdarstellung (es sei denn, die als Ersatz für Desktop für Endbenutzer verwendet wird). Jeder Dienst auf dem System ist wie folgt kategorisiert:

-   **Deaktivieren:** ein Unternehmen Security-orientierten wird wahrscheinlich lieber deaktivieren Sie diesen Dienst und auf seine Funktionalität (Weitere Informationen siehe unten).
- **OK, um deaktivieren:** dieser Dienst bietet Funktionen, die für einige, aber nicht alle Unternehmen sinnvoll ist und Sicherheit ausgerichteten Unternehmen, die sie nicht verwenden können problemlos deaktivieren.
- **Deaktivieren Sie nicht:** Deaktivieren dieses Diensts werden grundlegende Funktionen auswirken oder verhindern, dass bestimmte Rollen oder Features nicht ordnungsgemäß funktioniert. Sie sollten daher nicht deaktiviert werden.
-  **(Keine Hinweise):** die Auswirkung der Deaktivierung dieser Dienste nicht vollständig ausgewertet. Daher sollte die Standardkonfiguration dieser Dienste nicht geändert werden.


Kunden können ihre Windows-PCs und Servern, um ausgewählte Dienste mithilfe von Sicherheitsvorlagen in ihren Gruppenrichtlinien oder PowerShell-Automatisierung deaktivieren konfigurieren. In einigen Fällen enthält die Richtlinien spezifische Gruppenrichtlinieneinstellungen, die den Dienst Funktionen direkt als Alternative zur Deaktivierung des Diensts selbst zu deaktivieren.

Microsoft empfiehlt, dass Kunden die folgenden Dienste und ihre jeweiligen geplanten Aufgaben unter Windows Server2016 mit Desktopdarstellung deaktivieren:

Dienste: 
1. Xbox Live Auth-Manager
2. Xbox Live-Spiel speichern

Geplante Aufgaben: 
1. \Microsoft\XblGameSave\XblGameSaveTask
2. \Microsoft\XblGameSave\XblGameSaveTaskLogon

(Sie können auch die Informationen auf alle Dienste, die durch das Anzeigen von angefügten Microsoft Excel-Tabelle in diesem Artikel angegebene zugreifen: [Anleitung zum Deaktivieren der System-Dienste unter Windows Server2016 mit Desktopdarstellung](https://msdnshared.blob.core.windows.net/media/2017/05/Service-management-WS2016.xlsx))

<br />

### <a name="disabling-services-not-installed-by-default"></a>Deaktivieren von Diensten, die nicht standardmäßig installiert

Microsoft empfiehlt, Anwenden von Richtlinien so deaktivieren Sie Dienste, die nicht standardmäßig installiert sind.
-  Der Dienst ist in der Regel erforderlich, wenn das Feature installiert ist. Der Dienst oder das Feature installieren, sind Administratorrechte erforderlich. Die Featureinstallation, nicht Dienststart nicht zulassen.
-  Der Microsoft-Windows-Dienst blockiert beenden kein Administrator (oder ohne Administratorrechte in einigen Fällen) installiert eine ähnliche Drittanbieter-Entsprechung, z.B. eins mit ein höheres Sicherheitsrisiko.
-  Eine geplante oder Benchmarks, die nicht standardmäßigen Windows-Dienst (z.B. W3SVC) deaktiviert werden einige Prüfer den Garantie-Eindruck zu vermitteln, dass die Technologie (z.B. IIS) grundsätzlich unsicher ist und nicht verwendet werden sollte.
-  Wenn das Feature (und Service) nicht installiert ist, fügt diese nur unnötige Bulk der grundlegenden und Überprüfung der Arbeit.

<br />
Für alle Systemdienste, die in diesem Dokument aufgeführten bieten die beiden Tabellen, die folgen eine Erläuterung der Spalten und Empfehlungen von Microsoft für die Aktivierung und Deaktivierung von Systemdiensten in Windows Server2016 mit Desktopdarstellung: 
 
<br />

### <a name="explanation-of-columns"></a>Erläuterung der Spalten

| | |
|---|---|
|**Beschreibung**|   Die Beschreibung des Dienstes, von sc.exe Qdescription.|
|**Name** |Schlüsselname (interne) des Diensts|
|**Installation** |Immer installiert: Dienst wird auf Server Core und Server mit Desktopdarstellung  <br /> Nur auf Datacenter Edition: Dienst ist in Server2016 mit Desktopdarstellung, aber ***nicht*** auf Server Core-Installationen |
|**Starttyp**  |Dienststarttyp unter Windows Server2016|
|**Empfehlung** |Microsoft Empfehlung/Ratschläge Deaktivieren dieses Diensts unter Windows Server2016 in einer normalen, gut verwaltete Enterprise-Bereitstellung und, in dem der Server nicht als Ersatz Desktop Endbenutzer verwendet wird.|
|**Kommentare** |Weitere Erläuterung|

<br />

### <a name="explanation-of-microsoft-recommendations"></a>Erläuterung der Empfehlungen von Microsoft

| | |
|---|---|
|**Deaktivieren Sie nicht** |Dieser Dienst sollte nicht deaktiviert werden|
|**So deaktivieren Sie OK**| Dieser Dienst kann deaktiviert werden, wenn die Funktion, die sie unterstützt nicht verwendet wird.|
|**Bereits deaktiviert**|  Dieser Dienst wird standardmäßig deaktiviert. nicht erforderlich, mit der Richtlinie zu erzwingen.|
|**Sollte deaktiviert werden** |Dieser Dienst sollte nie auf einem verwalteten Enterprise-System aktiviert werden.|

<br />

In den folgenden Tabellen bieten Microsoft-Anleitung zum Deaktivieren der System-Dienste unter Windows Server2016 mit Desktopdarstellung:

<br />

##  <a name="activex-installer-axinstsv"></a>ActiveX Installer (AxInstSV)

| | |
|---|---|
|   **Beschreibung** |   Benutzerkontensteuerung-Überprüfung für die Installation des ActiveX-Steuerelemente enthält, aus dem Internet und ermöglicht die Verwaltung der Installation von ActiveX-Steuerelementen basierend auf einer Gruppenrichtlinie Einstellungen. Dieser Dienst bei Bedarf gestartet wird und wenn die Installation von ActiveX-Steuerelemente deaktiviert verhält sich je nach Browser Standardeinstellungen.    |
|   **Dienstname**    |   AxInstSV    |
|   **Installation**    |   Nur auf Datacenter Edition  |
|   **Starttyp**   |   Manuell  |
|   **Empfehlung**  |   So deaktivieren Sie OK   |
|   **Kommentare**    |   OK, Sie deaktivieren, wenn die Funktion nicht erforderlich |


<br />

## <a name="alljoyn-router-service"></a>AllJoyn-Router-Dienst   
| | |
|---|---|
|   **Beschreibung** |   AllJoyn-Nachrichten weitergeleitet für die lokale AllJoyn-Clients. Wenn dieser Dienst beendet wird werden nicht ausgeführt AllJoyn-Clients, die ihre eigenen gebündelte Router nicht vorhanden sind. |
|   **Dienstname**    |   AJRouter    |
|   **Installation**    |   Nur auf Datacenter Edition  |
|   **Starttyp**   |   Manuell  |
|   **Empfehlung**  | Keine Hinweise       |
|   **Kommentare**    |       |
| | |

<br />

## <a name="app-readiness"></a>App-Bereitschaft
| | |
|---|---|
**Beschreibung** |   Ruft Apps für die Verwendung ein Benutzers auf diesem PC und meldet sich beim Hinzufügen neuer Apps zum ersten Mal bereit.
**Dienstname**    |   AppReadiness
**Installation**    |   Nur auf Datacenter Edition
**Starttyp**   |   Manuell
**Empfehlung**  |   Deaktivieren Sie nicht
**Kommentare**    |   
| | |

<br />

##  <a name="application-identity"></a>-Identität
| | |       
|---|---|   
**Beschreibung** |   Bestimmt und überprüft die Identität einer Anwendung. Wenn dieser Dienst deaktiviert wird verhindert, dass AppLocker erzwungen wird.
**Dienstname**    |   AppIDSvc
**Installation**    |   Immer installiert
**Starttyp**   |   Manuell
**Empfehlung**  |Keine Hinweise    
**Kommentare**    |   
|||     

<br />

##  <a name="application-information"></a>Informationen zur Anwendung 
| | |       
|---|---|   
|   **Beschreibung** |   Ermöglicht das Ausführen von interaktiven Anwendungen mit zusätzlichen Administratorrechte.  Wenn dieser Dienst beendet wird, können Benutzer keine Anwendungen mit zusätzlichen Administratorrechte starten sie zum gewünschten Benutzer Aufgaben erfordern.
|   **Dienstname**    |   AppInfo
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   Unterstützt von UAC denselben Desktop für erhöhte Rechte
|||     

<br />

##  <a name="application-layer-gateway-service"></a>Gatewaydienst auf Anwendungsebene       
| | |           
|---|---|           
|   **Beschreibung** |   Bietet Unterstützung für Drittanbieter-Protokoll-Plug-Ins für die gemeinsame Nutzung der Internetverbindung
|   **Dienstname**    |   ALGORITHMUS
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |Keine Hinweise    
|   **Kommentare**    |   
|||     

<br />

##  <a name="application-management"></a>Application Management      
| | |           
|---|---|       
|   **Beschreibung** |   Installation, Deinstallation und Enumeration Anforderungen für Software, die über die Gruppenrichtlinie bereitgestellt wird verarbeitet. Wenn der Dienst deaktiviert ist, können sich Benutzer nur installieren, entfernen oder Aufzählen von Software mithilfe von Gruppenrichtlinien bereitgestellt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   AppMgmt
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="appx-deployment-service-appxsvc"></a>AppX-Bereitstellungsdienst (AppXSVC)       
| | |           
|---|---|
|   **Beschreibung** |   Bietet Unterstützung für die Bereitstellung von Store-Apps. Dieser Dienst bei Bedarf gestartet wird und wenn deaktiviert Store-Apps nicht auf dem System bereitgestellt werden werden, und möglicherweise nicht ordnungsgemäß.
|   **Dienstname**    |   AppXSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="auto-time-zone-updater"></a>Automatische Zeitzone Updater           
| | |           
|---|---|           
|   **Beschreibung** |   Legt die Zeitzone des Systems automatisch fest.
|   **Dienstname**    |   tzautoupdate
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="background-intelligent-transfer-service"></a>Background Intelligent Transfer Service          
| | |           
|---|---|   
|   **Beschreibung** |   Übertragen von Dateien im Hintergrund verwenden die inaktive Netzwerkbandbreite. Wenn der Dienst deaktiviert ist, klicken Sie dann wird alle Anwendungen, die von BITS, z.B. Windows Update oder MSN Explorer abhängig sind Programme und andere Informationen automatisch heruntergeladen.
|   **Dienstname**    |   BITS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          


## <a name="background-tasks-infrastructure-service"></a>Hintergrund Aufgaben-Infrastruktur-Dienst      
| | |           
|---|---|   
|   **Beschreibung** |   Windows-Infrastruktur-Dienst, die steuert, welche Hintergrundaufgaben kann auf dem System ausgeführt werden.
|   **Dienstname**    |   BrokerInfrastructure
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="base-filtering-engine"></a>Filter-Engine Base            
| | |           
|---|---|       
|   **Beschreibung** |   Der Base Filterung Engine (BFE) ist ein Dienst, der Firewall und Richtlinien Internet Protocol Security (IPsec) verwaltet, und Filtern von Benutzer Modus implementiert. Die BFE-Dienst anhalten oder deaktivieren reduziert der Sicherheit des Systems. Es führt auch zu unvorhersehbaren Verhalten in IPsec-Verwaltung und Firewall-Apps.
|   **Dienstname**    |   BFE
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="bluetooth-support-service"></a>Unterstützung für Bluetooth-Dienst            
| | |           
|---|---|   
|   **Beschreibung** |   Die Bluetooth-Dienst unterstützt die Erkennung und Zuordnung der Remote-Bluetooth-Geräte.  Anhalten oder Deaktivieren dieser Dienst möglicherweise bereits installierten Bluetooth-Geräte können nicht ordnungsgemäß und verhindern, dass neue Geräte erkannt oder verknüpft ist.
|   **Dienstname**    |   bthserv
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   OK deaktivieren, wenn Sie nicht verwendet. Ein weiterer Mechanismus für deaktivieren:https://technet.microsoft.com/en-us/library/dd252791.aspx
|||         
            
<br />          


## <a name="cdpusersvc"></a>CDPUserSvc           
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Benutzerdienst wird für Szenarien mit verbundenen Geräten Plattform verwendet.
|   **Dienstname**    |   CDPUserSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Benutzer-Dienstvorlage
|||         
            
<br />          


##  <a name="certificate-propagation"></a>Zertifikat-Verteilung     
| | |           
|---|---|
|   **Beschreibung** |   Zertifikate und Stammzertifikate von Smartcards in den Zertifikatspeicher des aktuellen Benutzers kopiert, erkennt, wenn eine Smartcard in einen Smartcardleser eingelegt wird, und bei Bedarf, die Smartcard-Plug & Play-Minitreiber installiert.
|   **Dienstname**    |   CertPropSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="client-license-service-clipsvc"></a>Lizenz Clientdienst (ClipSVC)        
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Unterstützung der Infrastruktur für den Microsoft Store. Dieser Dienst wird bei Bedarf gestartet, und wenn deaktivierte Anwendungen erworben haben mit Microsoft Store wird nicht mehr ordnungsgemäß funktionieren.
|   **Dienstname**    |   ClipSVC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="cng-key-isolation"></a>CNG wichtige Isolation
| | |           
|---|---|   
|   **Beschreibung** |   CNG-Schlüsselisolationsdienst wird in der LSA-Prozess gehostet. Der Dienst bietet wichtige Prozesse isoliert aus, um den privaten Schlüssel und die zugeordneten kryptografischen Vorgänge gemäß Common Criteria. Der Dienst gespeichert und langlebige Schlüssel in einem sicheren Prozess Einhaltung Common Criteria-Anforderungen verwendet.
|   **Dienstname**    |   KeyIso
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="com-event-system"></a>COM+-Ereignissystem       
| | |           
|---|---|       
|   **Beschreibung** |   Unterstützt System Event Notification Service (SENS), die automatische Verteilung von Ereignissen zum Abonnieren von Component Object Model (COM)-Komponenten bereitstellt. Wenn der Dienst beendet wird, SENS geschlossen, und ist nicht in der Lage, an- und Abmelden Benachrichtigungen bereitzustellen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   EventSystem
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="com-system-application"></a>COM+-Anwendung     
| | |           
|---|---|       
|   **Beschreibung** |   Verwaltet die Konfiguration und Überwachung von Component Object Model (COM)-basierten Komponenten. Wenn der Dienst beendet wird, die meisten COM+-basierte Komponenten nicht ordnungsgemäß funktionieren. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   COMSysApp
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="computer-browser"></a>Computer-Browser        
| | |           
|---|---|       
|   **Beschreibung** |   Führt eine aktualisierte Liste der Computer im Netzwerk und stellt diese Liste Computer, die als Browser zur Verfügung. Wenn dieser Dienst beendet wird, wird diese Liste nicht aktualisiert oder verwaltet werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   Browser
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="connected-devices-platform-service"></a>Verbundene Geräte Platform-Dienst       
| | |           
|---|---|       
|   **Beschreibung** |   Dieser Dienst wird für verbundene Geräte und universelle Glass-Szenarien verwendet werden.
|   **Dienstname**    |   CDPSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="connected-user-experiences-and-telemetry"></a>Connected User Experiences and Telemetry     
| | |           
|---|---|       
|   **Beschreibung** |   Der Benutzererlebnis verbunden und Telemetrie-Dienst ermöglicht Features, die in der Anwendung und verbundenen Benutzeroberflächen zu unterstützen. Darüber hinaus dieser Dienst verwaltet, die ereignisgesteuerten Erfassung und Übermittlung von Diagnose- und Nutzungsdaten Informationen (zur Verbesserung der Benutzerfreundlichkeit und Qualität der Windows-Plattform) bei der Diagnose und die Nutzung Option Datenschutzeinstellungen unter Feedback und Diagnose aktiviert werden.
|   **Dienstname**    |   DiagTrack
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="contact-data"></a>Wenden Sie sich an Daten        
| | |           
|---|---|       
|   **Beschreibung** |   Indizes erhalten Daten Sie schnell Kontakt zu suchen. Wenn Sie beenden oder deaktivieren Sie diesen Dienst, können Kontakte aus den Suchergebnissen nicht vorhanden sein.
|   **Dienstname**    |   PimIndexMaintenanceSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Benutzer-Dienstvorlage
|||         
            
<br />          

## <a name="coremessaging"></a>CoreMessaging            
| | |           
|---|---|           
|   **Beschreibung** |   Kommunikation zwischen Komponenten verwaltet.
|   **Dienstname**    |   CoreMessagingRegistrar
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="credential-manager"></a>Die Anmeldeinformationsverwaltung           
| | |           
|---|---|       
|   **Beschreibung** |   Bietet sichere Speichern und Abrufen von Anmeldeinformationen für Benutzer, Anwendungen und Sicherheitspaketen.
|   **Dienstname**    |   VaultSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="cryptographic-services"></a>Kryptografiedienste           
| | |           
|---|---|       
|   **Beschreibung** |   Bietet drei Management Services: Katalog-Datenbank-Dienst, der bestätigt die Signaturen von Windows-Dateien und können neue Programme installiert werden. Stamm-Dienst, der hinzugefügt und entfernt vertrauenswürdige Stammzertifizierungsstellen-Zertifikate von diesem Computer wird geschützt. und automatische Stammzertifizierungsstellen-Zertifikat Update-Dienst die Stammzertifikate von Windows Update abgerufen und ermöglichen Szenarien wie z.B. SSL. Wenn dieser Dienst beendet wird, werden diese Verwaltungsdienste nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   Den Kryptografiedienst erneut
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="data-sharing-service"></a>Gemeinsame Nutzung der Daten         
| | |           
|---|---|       
|   **Beschreibung** |   Enthält die Daten zwischen den Clientanwendungen weitergeben.
|   **Dienstname**    |   DsSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="datacollectionpublishingservice"></a>DataCollectionPublishingService          
| | |           
|---|---|       
|   **Beschreibung** |   Das DCP (Datensammlung und Veröffentlichung)-Dienst unterstützt Erstanbieter-Apps zum Hochladen von Daten in die Cloud.
|   **Dienstname**    |   DcpSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="dcom-server-process-launcher"></a>DCOM-Serverprozess-Startprogramm         
| | |           
|---|---|       
|   **Beschreibung** |   Der Dienst DCOMLAUNCH startet COM- und DCOM-Server als Antwort auf aktivierungsanforderungen Objekt. Wenn dieser Dienst beendet oder deaktiviert ist, funktioniert mit COM oder DCOM Programme nicht ordnungsgemäß. Es wird dringend empfohlen, dass der DCOMLAUNCH-Dienst ausgeführt werden.
|   **Dienstname**    |   DcomLaunch
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |Keine Hinweise    
|   **Kommentare**    |   
|||         
            
<br />

##  <a name="device-association-service"></a>Gerätezuordnungsdienst      
| | |           
|---|---|       
|   **Beschreibung** |   Aktiviert die Kopplung zwischen dem System und verkabelten oder drahtlosen Geräten.
|   **Dienstname**    |   DeviceAssociationService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          
        
##  <a name="device-install-service"></a>Geräte-Installationsdienst      
| | |           
|---|---|       
|   **Beschreibung** |   Ermöglicht es einem Computer zu erkennen und mit minimaler oder ohne Benutzereingabe hardwareänderungen übernehmen. Anhalten oder Deaktivieren dieses Diensts führt Instabilität des Systems.
|   **Dienstname**    |   DeviceInstall
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="device-management-enrollment-service"></a>Registrierungsdienst für Netzwerkgeräte Management        
| | |           
|---|---|       
|   **Beschreibung** |   Führt Registrierungsaktivitäten Gerät für die Geräteverwaltung
|   **Dienstname**    |   DmEnrollmentSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="device-setup-manager"></a>Geräte-Setup-Manager         
| | |           
|---|---|       
|   **Beschreibung** |   Ermöglicht die Erkennung, Download und Installation von Software im Zusammenhang mit dem Gerät. Wenn dieser Dienst deaktiviert ist, werden Geräte mit veralteten Software konfiguriert werden können, und funktioniert möglicherweise nicht ordnungsgemäß.
|   **Dienstname**    |   DsmSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="devquery-background-discovery-broker"></a>DevQuery Hintergrund Discovery-Broker         
| | |           
|---|---|           
|   **Beschreibung** |   Ermöglicht Apps auf Geräten mit einer Aufgabe Rasterlinie ermitteln
|   **Dienstname**    |   DevQueryBroker
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="dhcp-client"></a>DHCP-Client          
| | |           
|---|---|       
|   **Beschreibung** |   Registriert und IP-Adressen und DNS-Einträge für diesen Computer aktualisiert. Wenn dieser Dienst beendet wird, erhält dieser Computer keine dynamische IP-Adressen und DNS-Updates. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   DHCP
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="diagnostic-policy-service"></a>Diagnostic Policy Service            
| | |           
|---|---|       
|   **Beschreibung** |   Die Richtlinie Diagnosedienst ermöglicht Problemerkennung, Problembehandlung und Auflösung für Windows-Komponenten.  Wenn dieser Dienst beendet wird, wird die Diagnose nicht mehr funktionieren.
|   **Dienstname**    |   DPS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="diagnostic-service-host"></a>Diagnose-Diensthost     
| | |           
|---|---|       
|   **Beschreibung** |   Der Diagnose-Dienst-Host wird durch den Diagnosedienst-Richtlinie für die Host-Diagnose verwendet, müssen in einem lokalen Dienst-Kontext ausgeführt.  Wenn dieser Dienst beendet wird, wird Diagnose, die davon abhängen, nicht mehr funktionieren.
|   **Dienstname**    |   WdiServiceHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="diagnostic-system-host"></a>Diagnose Systemhost           
| | |           
|---|---|       
|   **Beschreibung** |   Die Diagnose System-Host wird von den Diagnosedienst-Richtlinie für die Host-Diagnose verwendet, die im lokalen Systemkontext ausgeführt werden müssen.  Wenn dieser Dienst beendet wird, wird Diagnose, die davon abhängen, nicht mehr funktionieren.
|   **Dienstname**    |   WdiSystemHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="distributed-link-tracking-client"></a>Distributed Link Tracking-Client            
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet Links zwischen NTFS-Dateien auf einem Computer oder auf Computern in einem Netzwerk.
|   **Dienstname**    |   TrkWks
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="distributed-transaction-coordinator"></a>Distributed Transaction Coordinator     
| | |           
|---|---|   
|   **Beschreibung** |   Koordiniert Transaktionen, die mehrere Ressourcen-Manager wie Datenbanken, Nachrichtenwarteschlangen und Dateisysteme umfassen. Wenn dieser Dienst beendet wird, schlägt diese Transaktionen fehl. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   MSDTC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />  

##  <a name="dmwappushsvc"></a>dmwappushsvc        
| | |           
|---|---|       
|   **Beschreibung** |   WAP-Nachricht Push Routingdienst
|   **Dienstname**    |   dmwappushservice
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Dienst auf Client-Geräte erforderlich sind, Intune, MDM und ähnliche Technologien zur Verwaltung und Unified Write Filter. Für Server erforderlich nicht.
|||         
            
<br />      

##  <a name="dns-client"></a>DNS-Client      
| | |           
|---|---|       
|   **Beschreibung** |   Der DNS-Clientdienst (Dnscache) speichert Domain Name System (DNS-Namen) und registriert den vollständigen Computernamen für diesen Computer. Wenn der Dienst angehalten wird, werden DNS-Namen weiterhin aufgelöst werden. Allerdings werden die Ergebnisse der DNS-Namensabfragen nicht zwischengespeichert, und den Namen des Computers wird nicht registriert werden. Wenn der Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   DnsCache
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="downloaded-maps-manager"></a>Heruntergeladene Karten-Manager     
| | |           
|---|---|   
|   **Beschreibung** |   Windows-Dienst für die Anwendungszugriff auf die heruntergeladene Karten. Dieser Dienst wird bei Bedarf gestartet von Anwendung den Zugriff auf heruntergeladene Karten. Wenn dieser Dienst deaktiviert wird verhindert, dass Apps auf die kartenanwendung.
|   **Dienstname**    |   MapsBroker
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Deaktivieren Pausen Apps, die auf den Dienst abhängig sind; OK, um deaktivieren, wenn Apps nicht darauf verlassen
|||         
            
<br />          

## <a name="embedded-mode"></a>Eingebetteten Modus            
| | |           
|---|---|       
|   **Beschreibung** |   Der eingebetteten Modus-Dienst ermöglicht Szenarien im Zusammenhang mit Hintergrund-Apps.  Deaktivieren dieses Diensts verhindert, dass Programme im Hintergrund aktiviert wurden.
|   **Dienstname**    |   embeddedmode
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="encrypting-file-system-efs"></a>Das verschlüsselnde Dateisystem (EFS)
| | |                   
|---|---|           
|   **Beschreibung** | Enthält die wichtigsten dateiverschlüsselungstechnologie zum Speichern verschlüsselter Dateien auf NTFS-Datenträger. Wenn dieser Dienst beendet oder deaktiviert ist, werden Anwendungen nicht auf verschlüsselte Dateien zugreifen.            
|   **Dienstname**  |  EFS            
|   **Installation**  |  Immer installiert           
|   **Starttyp**   |  Manuell           
|   **Empfehlung**  | Keine Hinweise           
|   **Kommentare**   |
|||                 
                            
<br />  

## <a name="enterprise-app-management-service"></a>Unternehmens-App-Verwaltungsdienst            
| | |           
|---|---|       
|   **Beschreibung** |   Ermöglicht die Verwaltung der Enterprise-Anwendung.
|   **Dienstname**    |   EntAppSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="extensible-authentication-protocol"></a>Extensible Authentication-Protokoll           
| | |           
|---|---|   
|   **Beschreibung** |   Das Extensible Authentication Protocol (EAP)-Dienst bietet Netzwerkauthentifizierung in Szenarien wie 802,1 x kabelgebundenen und drahtlosen und VPN (Network Access Protection, NAP).  EAP bietet auch Anwendungsprogrammierschnittstellen (APIs), die auf Clients, einschließlich WLAN und VPN-Clients, während der Authentifizierung verwendet werden.  Wenn Sie diesen Dienst deaktivieren, wird verhindert, dass dieser Computer Zugriff auf Netzwerke, die EAP-Authentifizierung erforderlich ist.
|   **Dienstname**    |   EapHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="function-discovery-provider-host"></a>Funktionssuchanbieter-Host         
| | |           
|---|---|       
|   **Beschreibung** |   Der FDPHOST-Dienst hostet Netzwerkanbieter Ermittlung Funktion Discovery (FD). Diese Anbieter FD angeben Ermittlung Netzwerkdienste für die einfache Dienste Discovery Protocol (SSDP) und Web Services - Suchprotokoll (WS-D). Der FDPHOST-Dienst anhalten oder deaktivieren wird die Netzwerkermittlung für diese Protokolle deaktiviert, wenn FD verwenden. Wenn dieser Dienst nicht verfügbar ist, werden Netzwerkdienste FD verwenden und auf diesen Discovery-Protokollen Netzwerkgeräte oder Ressourcen kann nicht gefunden werden.
|   **Dienstname**    |   fdPHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="function-discovery-resource-publication"></a>Funktionssuche-Ressourcenveröffentlichung      
| | |           
|---|---|       
|   **Beschreibung** |   Veröffentlicht diesen Computer und Ressourcen, die an den Computer angeschlossen werden, damit sie über das Netzwerk erkannt werden können.  Wenn dieser Dienst beendet wird, Netzwerkressourcen nicht mehr veröffentlicht werden und wird nicht von anderen Computern im Netzwerk ermittelt werden.
|   **Dienstname**    |   FDResPub
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="geolocation-service"></a>GeoLocation-Dienst          
| | |           
|---|---|       
|   **Beschreibung** |   Dieser Dienst überwacht die aktuelle Position des Systems und Geofence (einen geografischen Ort mit zugeordneten Ereignissen) verwaltet.  Wenn Sie diesen Dienst deaktivieren, werden Anwendungen nicht verwenden oder Benachrichtigungen für Geolocation oder Geofence-Bereiche.
|   **Dienstname**    |   lfsvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Deaktivieren Pausen Apps, die auf den Dienst abhängig sind; OK, um deaktivieren, wenn Apps nicht darauf verlassen
|||         
            
<br />          

##  <a name="group-policy-client"></a>Gruppenrichtlinienclient     
| | |           
|---|---|       
|   **Beschreibung** |   Der Dienst ist verantwortlich für die Anwendung von Administratoren für den Computer und Benutzer über die Gruppenrichtlinienkomponente konfigurierten Einstellungen. Wenn der Dienst deaktiviert ist, werden die Einstellungen nicht angewendet und Anwendungen und Komponenten werden nicht über eine Gruppenrichtlinie verwaltbare. Alle Komponenten oder Anwendungen, die abhängig von der Gruppenrichtlinienkomponente möglicherweise nicht funktionieren, wenn der Dienst deaktiviert ist.
|   **Dienstname**    |   gpsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          


## <a name="human-interface-device-service"></a>Eingabegerätedienst           
| | |           
|---|---|       
|   **Beschreibung** |   Aktiviert und verwaltet die Verwendung von Abkürzungstasten auf Tastaturen, Fernbedienungen und andere Multimedia-Geräte. Es wird empfohlen, dass stets dieser Dienst wird ausgeführt.
|   **Dienstname**    |   HidServ
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="hv-host-service"></a>HV Hostdienst     
| | |           
|---|---|   
|   **Beschreibung** |   Stellt eine Schnittstelle für den Hyper-V-Hypervisor-Partition Leistungsindikatoren für das Hostbetriebssystem bereitstellen.
|   **Dienstname**    |   HvHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Leistung Enhancers für Gast-VMs. Mit Ausnahme von nicht verwendeten heute explizit VMs aufgefüllt, aber in Application Guard verwendet wird
|||         
            
<br />          

## <a name="hyper-v-data-exchange-service"></a>Hyper-V-Datenaustauschdienst        
| | |           
|---|---|   
|   **Beschreibung** |   Bietet einen Mechanismus zum Austauschen von Daten zwischen den virtuellen Computer und das Betriebssystem auf dem physischen Computer ausgeführt wird.
|   **Dienstname**    |   vmickvpexchange
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />      

## <a name="hyper-v-guest-service-interface"></a>Hyper-V-Gastdienstschnittstelle          
| | |           
|---|---|   
|   **Beschreibung** |   Stellt eine Schnittstelle für den Hyper-V-Host für die Interaktion mit bestimmten Diensten, die auf dem virtuellen Computer ausgeführt wird.
|   **Dienstname**    |   vmicguestinterface
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />  

## <a name="hyper-v-guest-shutdown-service"></a>Hyper-V-Gastcomputers Shutdown Service           
| | |           
|---|---|       
|   **Beschreibung** |   Bietet einen Mechanismus zum Herunterfahren des Betriebssystems dieses virtuellen Computers über die Verwaltungsschnittstellen auf dem physischen Computer.
|   **Dienstname**    |   vmicshutdown
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />          
    
## <a name="hyper-v-heartbeat-service"></a>Hyper-V Taktdienst            
| | |           
|---|---|           
|   **Beschreibung** |   Überwacht den Zustand der virtuellen Computer einen Takt in regelmäßigen Abständen melden. Dieser Dienst ermöglicht Ihnen die ausgeführten virtuellen Computer zu identifizieren, die nicht mehr reagiert.
|   **Dienstname**    |   vmicheartbeat
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />          

## <a name="hyper-v-powershell-direct-service"></a>Hyper-V-PowerShell Direct-Dienst            
| | |           
|---|---|       
|   **Beschreibung** |   Bietet einen Mechanismus zum Verwalten des virtuellen Computers mit PowerShell über VM-Sitzung ohne virtuelles Netzwerk.
|   **Dienstname**    |   vmicvmsession
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />          

## <a name="hyper-v-remote-desktop-virtualization-service"></a>Hyper-V-Remotedesktopvirtualisierungsdienst            
| | |           
|---|---|       
|   **Beschreibung** |   Bietet eine Plattform für die Kommunikation zwischen dem virtuellen Computer und das Betriebssystem auf dem physischen Computer ausgeführt wird.
|   **Dienstname**    |   vmicrdv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />          

## <a name="hyper-v-time-synchronization-service"></a>Hyper-V-Zeitsynchronisierungsdienst         
| | |           
|---|---|       
|   **Beschreibung** |   Synchronisiert die Systemzeit dieses virtuellen Computers mit der Systemzeit des physischen Computers.
|   **Dienstname**    |   vmictimesync
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />          

## <a name="hyper-v-volume-shadow-copy-requestor"></a>Hyper-V-Volumeschattenkopie-Anforderer         
| | |           
|---|---|           
|   **Beschreibung** |   Koordiniert die Kommunikationen, die erforderlich sind, um die Volumeschattenkopie-Dienst zu verwenden, um Apps und Daten auf diesem virtuellen Computer aus dem Betriebssystem auf dem physischen Computer sichern.
|   **Dienstname**    |   vmicvss
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Weitere Informationen finden Sie unter HvHost
|||         
            
<br />          

## <a name="ike-and-authip-ipsec-keying-modules"></a>IKE- und AuthIP IPsec-Schlüsselerstellungsmodule          
| | |           
|---|---|       
|   **Beschreibung** |   Die IKEEXT-Diensthosts der Internetinformationsdienste (Internet Key Exchange, IKE) und Authenticated Internet Protocol (AuthIP) Schlüsselerstellungsmodule. Diese Schlüsselerstellungsmodule werden für die Authentifizierung und Schlüsselaustausch in Internet Protocol Security (IPsec) verwendet. Die IKEEXT-Dienst anhalten oder deaktivieren, werden IKE- und AuthIP Schlüsselaustausch mit Peercomputern deaktiviert. IPsec ist in der Regel so konfiguriert, dass IKE oder AuthIP verwenden. Daher wird die IKEEXT-Dienst anhalten oder deaktivieren kann dazu führen, dass Fehler bei der IPsec- und die Sicherheit des Systems gefährden kann. Es wird dringend empfohlen, dass der IKEEXT-Dienst ausgeführt werden.
|   **Dienstname**    |   IKEEXT
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |    
|||         
            
<br />          

## <a name="interactive-services-detection"></a>Erkennung interaktiver Dienste           
| | |           
|---|---|   
|   **Beschreibung** |   Aktiviert die benutzerbenachrichtigung von Benutzereingaben für interaktive Dienste, die ermöglicht den Zugriff auf die Dialogfelder von interaktiver Dienste erstellt, wenn sie angezeigt werden. Wenn dieser Dienst beendet wird, Benachrichtigungen über neue Dialogfelder funktioniert nicht mehr, und es möglicherweise nicht den Zugriff auf Dialogfelder. Wenn dieser Dienst deaktiviert ist, funktionieren Benachrichtigungen und den Zugriff auf neue Dialogfelder nicht mehr.
|   **Dienstname**    |   UI0Detect
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />  

## <a name="internet-connection-sharing-ics"></a>ICS (ICS)            
| | |           
|---|---|           
|   **Beschreibung** |   Enthält die Netzwerkadressübersetzung, adressieren, Auflösung und/oder Erkennen von Eindringlingen Prevention-Dienste für eines Heimnetzwerks oder eines kleinen Büronetzwerks.
|   **Dienstname**    |   SharedAccess
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Erforderlich für Clients, die als WLAN-Hotspots sowie an beiden Enden des Miracast-Projektion. ICS mit GPO-Einstellung blockiert werden können, "Nicht mit Internet Connection Sharing auf dem DNS-Domänennetzwerk zulassen"
|||         
            
<br />          

## <a name="ip-helper"></a>IP-Hilfsdienst            
| | |           
|---|---|       
|   **Beschreibung** |   Stellt tunnelkonnektivität mithilfe von IPv6-übergangstechnologien (6to4 ISATAP-Port-Proxy und Teredo) und IP-HTTPS bereit. Wenn dieser Dienst beendet wird, wird der Computer nicht die Erweiterte Konnektivität Vorteile mit sich bringen, die diese Technologien bieten.
|   **Dienstname**    |   iphlpsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          


##  <a name="ipsec-policy-agent"></a>IPsec-Richtlinien-Agent      
| | |           
|---|---|       
|   **Beschreibung** |   Internet Protocol Security (IPsec) unterstützt die Netzwerk-Peerauthentifizierung auf Netzwerkebene, die Datenursprungsauthentifizierung, Datenintegrität, Datenvertraulichkeit (Verschlüsselung) und Replay-Schutz.  Dieser Dienst erzwingt die IPsec-Richtlinien, die über die IP-Sicherheitsrichtlinien-Snap-In oder des Befehlszeilentools "Netsh Ipsec" erstellt.  Wenn dieser Dienst beendet wird, können Probleme mit der Netzwerkkonnektivität auftreten, wenn Ihre Richtlinie erfordert, dass Verbindungen IPsec verwenden.  Außerdem ist die Remoteverwaltung von Windows-Firewall nicht verfügbar, wenn dieser Dienst beendet wird.
|   **Dienstname**    |   Richtlinien-Agent
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />

##  <a name="kdc-proxy-server-service-kps"></a>KDC-Proxyserver-Dienst (KPS)      
| | |           
|---|---|       
|   **Beschreibung** |   KDC-Proxyserver-Dienst wird auf Edge-Servern mit Kerberos-Proxy ausgeführt Protokollnachrichten auf Domänencontroller im Unternehmensnetzwerk.
|   **Dienstname**    |   KPSSVC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise    
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="ktmrm-for-distributed-transaction-coordinator"></a>KtmRm für Distributed Transaction Coordinator            
| | |           
|---|---|       
|   **Beschreibung** |   Koordiniert Transaktionen zwischen dem Distributed Transaction Coordinator (MSDTC) und die Kerneltransaktions-Manager (KTM). Wenn es nicht erforderlich ist, empfiehlt es sich, dass dieser Dienst bleiben beendet wurde. Wenn es erforderlich ist, wird MSDTC und KTM dieser Dienst automatisch gestartet. Wenn dieser Dienst deaktiviert ist, wird Interaktion mit einem Kernel-Ressourcen-Manager MS DTC-Transaktion fehl, und alle Dienste, die explizit davon abhängen können nicht gestartet.
|   **Dienstname**    |   KtmRm
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />

##  <a name="link-layer-topology-discovery-mapper"></a>Link-Layer-Topologie-Ermittlungszuordnung.        
| | |       
|---|---|       
|   **Beschreibung** |   Erstellt eine Netzwerkübersicht bestehend aus PC und Geräteinformationen Topologie (Connectivity) und Metadaten, die jeden PC und Geräte beschreiben.  Wenn dieser Dienst deaktiviert ist, wird der Netzwerk-Karte nicht ordnungsgemäß.
|   **Dienstname**    |   lltdsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   OK, wenn keine Abhängigkeiten von Netzwerk-Karte deaktivieren
|||         
            
<br />

## <a name="local-session-manager"></a>Lokale Sitzungs-Managers                    
| | |                   
|---|---|   
|   **Beschreibung** |   Core Windows-Dienst, der lokalen Benutzersitzungen verwaltet. Anhalten oder Deaktivieren dieses Diensts führt Instabilität des Systems.    
|   **Dienstname**    |   LSM |
|   **Installation**    |   Immer installiert    |
|   **Starttyp**   |   Automatisch   |
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||                 
                    
<br />                  

## <a name="microsoft-r-diagnostics-hub-standard-collector"></a>Microsoft (R) Diagnose-Hub-Standard-Sammlung         
| | |           
|---|---|           
|   **Beschreibung** |   Core Windows-Dienst, der lokalen Benutzersitzungen verwaltet. Anhalten oder Deaktivieren dieses Diensts führt Instabilität des Systems.
|   **Dienstname**    |   LSM
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          
            
## <a name="microsoft-account-sign-in-assistant"></a>Microsoft-Konto-Assistenten          
| | |           
|---|---|       
|   **Beschreibung** |   Benutzer melden Sie sich über Microsoft-Konto Identitätsdienste ermöglicht. Wenn dieser Dienst beendet wird, werden Benutzer nicht auf dem Computer mit ihrem Microsoft-Konto anmelden.
|   **Dienstname**    |   wlidsvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Microsoft Accounts sind nicht für Windows Server
|||         
            
<br />          

##  <a name="microsoft-app-v-client"></a>Microsoft App-V-Client      
| | |           
|---|---|       
|   **Beschreibung** |   Zur Verwaltung von App-V-Benutzer und virtuelle Anwendungen
|   **Dienstname**    |   AppVClient
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="microsoft-iscsi-initiator-service"></a>Microsoft iSCSI-Initiator-Dienst            
| | |           
|---|---|       
|   **Beschreibung** |   Verwaltet Internet SCSI (iSCSI)-Sitzungen von diesem Computer auf Remote-iSCSI-Zielgeräte. Wenn dieser Dienst beendet wird, wird diesem Computer werden nicht anmelden oder Zugriff auf iSCSI-Ziele. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   MSiSCSI
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Unsere Diagnosedaten weist darauf hin, dass dieser Client als auch Server verwendet wird. Keinen Vorteil dieser deaktivieren.
|||         
            
<br />          

## <a name="microsoft-passport"></a>Microsoft Passport           
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Prozessisolation für kryptografische Schlüssel zum Authentifizieren des Benutzers zugeordnete Identitätsanbietern verwendet. Wenn dieser Dienst deaktiviert ist, werden alle verwendet und die Verwaltung dieser Schlüssel, nicht verfügbar, beispielsweise Computer anmelden und Single-Sign-in für Apps und Websites. Dieser Dienst wird gestartet und automatisch beendet. Es wird empfohlen, dass Sie diesen Dienst nicht neu konfigurieren.
|   **Dienstname**    |   NgcSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Erforderlich für die PIN/Hello Anmeldungen, die auf dem Server nicht unterstützt werden
|||         
            
<br />          

## <a name="microsoft-passport-container"></a>Microsoft Passport-Container         
| | |           
|---|---|       
|   **Beschreibung** |   Verwaltet lokale Benutzer Identitätsschlüssel zum Authentifizieren des Benutzers Identitätsanbietern als auch für virtuelle Smartcards TPM verwendet. Wenn dieser Dienst deaktiviert ist, werden lokale Identität Benutzerschlüssel und virtuelle Smartcards TPM nicht zugegriffen werden. Es wird empfohlen, dass Sie diesen Dienst nicht neu konfigurieren.
|   **Dienstname**    |   NgcCtnrSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="microsoft-software-shadow-copy-provider"></a>Schattenkopieanbieter für Microsoft-Software          
| | |           
|---|---|       
|   **Beschreibung** |   Verwaltet Softwarebasierte Volumeschattenkopien vom Volumeschattenkopie-Dienst. Wenn dieser Dienst beendet wird, können Softwarebasierte Volumeschattenkopien verwaltet werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   SWPRV
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="microsoft-storage-spaces-smp"></a>Microsoft-Speicherplätze SMP         
| | |           
|---|---|       
|   **Beschreibung** |   Hostdienst für den Microsoft Storage Spaces Management Provider. Wenn dieser Dienst beendet oder deaktiviert ist, kann mithilfe von Speicherplätzen verwaltet werden.
|   **Dienstname**    |   smphost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Speicherverwaltung fehl APIs ohne diesen Dienst. Beispiel: "Get-WmiObject-Klasse MSFT_Disk - Namespace Root\Microsoft\Windows\Storage".
|||         
            
<br />          

## <a name="nettcp-port-sharing-service"></a>Gemeinsame Nutzung der Net.Tcp Port         
| | |           
|---|---|       
|   **Beschreibung** |   Bietet die Möglichkeit zur Freigabe von TCP-Ports über das net.tcp-Protokoll.
|   **Dienstname**    |   NetTcpPortSharing
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="netlogon"></a>Anmeldedienst         
| | |           
|---|---|           
|   **Beschreibung** |   Verwaltet einen sicheren Kanal zwischen diesem Computer und dem Domänencontroller für die Authentifizierung von Benutzern und Diensten. Wenn dieser Dienst beendet wird, wird der Computer möglicherweise nicht authentifizieren von Benutzern und Dienste und der Domänencontroller können keine DNS-Datensätze registrieren. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   Anmeldedienst
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="network-connection-broker"></a>Network Connection Broker            
| | |           
|---|---|       
|   **Beschreibung** |   Broker-Verbindungen, mit die Microsoft Store-Apps Benachrichtigungen aus dem Internet empfangen können.
|   **Dienstname**    |   NcbService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="network-connections"></a>Netzwerkverbindungen         
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet von Objekten im Ordner "Netzwerk- und DFÜ-Verbindungen", in dem Sie Local Area Network und Remoteverbindungen anzeigen können.
|   **Dienstname**    |   NETMAN
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="network-connectivity-assistant"></a>Network Connectivity Assistant      
| | |           
|---|---|       
|   **Beschreibung** |   Bietet DirectAccess Benachrichtigung über den UI-Komponenten
|   **Dienstname**    |   NcaSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />  

##  <a name="network-list-service"></a>Netzwerkdienst-Liste        
| | |           
|---|---|   
|   **Beschreibung** |   Identifiziert die Netzwerke, zu denen der Computer hat eine Verbindung hergestellt, erfasst und speichert Eigenschaften für diese Netzwerke und Anwendungen benachrichtigt, wenn diese Eigenschaften geändert.
|   **Dienstname**    |   netprofm
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="network-location-awareness"></a>Network Location Awareness           
| | |           
|---|---|       
|   **Beschreibung** |   Sammelt und speichert die Konfigurationsinformationen für das Netzwerk und benachrichtigt Programme, wenn diese Informationen geändert werden. Konfigurationsinformationen sind möglicherweise nicht verfügbar, wenn dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   NlaSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="network-setup-service"></a>Netzwerkdienst-Setup       
| | |           
|---|---|       
|   **Beschreibung** |   Der Setup-Netzwerkdienst verwaltet die Installation von Netzwerktreiber und ermöglicht die Konfiguration der Low-Level-Einstellungen.  Wenn dieser Dienst beendet wird, können Installation der Treiber, die in Bearbeitung sind storniert werden.
|   **Dienstname**    |   NetSetupSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="network-store-interface-service"></a>Netzwerk-Schnittstelle Speicherdienst      
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst bietet netzwerkbenachrichtigungen (z.B. Schnittstelle hinzufügen/löschen usw.) auf Clients für Benutzer im Modus. Dieser Dienst beendet wird einen Verlust der Netzwerkkonnektivität. Wenn dieser Dienst deaktiviert ist, werden alle anderen Dienste, die explizit von diesem Dienst abhängig sind nicht gestartet.
|   **Dienstname**    |   NSI
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="offline-files"></a>Offlinedateien            
| | |           
|---|---|       
|   **Beschreibung** |   Der Offlinedateien-Dienst auf den Cache für Offlinedateien, Wartungsaktivitäten führt auf Benutzer an- und Abmelden Ereignisse reagiert, internen die öffentliche API implementiert und verteilt interessante Ereignisse an Offlinedateien Aktivitäten und Änderungen im Cache Zustand möchten.
|   **Dienstname**    |   CscService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="optimize-drives"></a>Optimieren Sie Laufwerke          
| | |           
|---|---|   
|   **Beschreibung** |   Können den Computer durch Optimieren der Dateien auf Speichergeräten effizienter ausgeführt.
|   **Dienstname**    |   defragsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />

## <a name="performance-counter-dll-host"></a>Leistung Leistungsindikator-DLL-Host         
| | |           
|---|---|       
|   **Beschreibung** |   Ermöglicht Remotebenutzern und 64-Bit-Prozesse zum Abfragen von Leistungsindikatoren von 32-Bit-DLLs bereitgestellt. Wenn dieser Dienst beendet wird, werden kann von 32-Bit-DLLs verfügbaren Leistungsindikatoren Abfragen nur lokale Benutzer und 32-Bit-Prozesse.
|   **Dienstname**    |   PerfHost
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise    
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="performance-logs--alerts"></a>Leistungsprotokolle und Warnungen            
| | |           
|---|---|   
|   **Beschreibung** |   Leistungsprotokolle und Warnungen sammelt Leistungsdaten von lokalen Computern oder Remotecomputern basierend auf vorkonfigurierten Zeitplan dann schreibt die Daten in einem Protokoll oder wird eine Warnung ausgelöst. Wenn dieser Dienst beendet wird, werden die Performance-Daten nicht gesammelt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   PLA
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="phone-service"></a>Telefon       
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet den Zustand Telefonie auf dem Gerät
|   **Dienstname**    |   PhoneSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Von modernen VoIP-Apps verwendet werden
|||         
            
<br />          

##      <a name="plug-and-play"></a>Plug & Play       
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht es einem Computer zu erkennen und mit minimaler oder ohne Benutzereingabe hardwareänderungen übernehmen. Anhalten oder Deaktivieren dieses Diensts führt Instabilität des Systems.
|   **Dienstname**    |   PlugPlay
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="portable-device-enumerator-service"></a>Tragbares Gerät Enumerator Service           
| | |           
|---|---|       
|   **Beschreibung** |   Erzwingt die Gruppenrichtlinie für Wechseldatenträger Massenspeichergeräte. Ermöglicht es Anwendungen, z.B. Windows Media Player und Assistenten zum Importieren von Images, zum übertragen und synchronisieren Sie Inhalt mithilfe von Wechselmedien Massenspeichergeräte.
|   **Dienstname**    |   WPDBusEnum
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="power"></a>Ein/aus            
| | |           
|---|---|       
|   **Beschreibung** |   Energierichtlinien und Benachrichtigungsübermittlung für Ein/Aus-Richtlinie verwaltet.
|   **Dienstname**    |   Ein/aus
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="print-spooler"></a>Druckspooler neu.            
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst spoolt Druckaufträge und Interaktion mit dem Drucker behandelt.  Wenn Sie diesen Dienst deaktivieren, wird Sie nicht drucken oder Ihr Drucker.
|   **Dienstname**    |   Spooler
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   OK, um deaktivieren, wenn kein Druckserver oder einem Domänencontroller
|   **Kommentare**    |   Die Installation von Domänencontrollern wird der Spooler-Dienst, der für die Ausführung von drucken Archivs – entfernen die Druckwarteschlange veraltete Objekte aus Active Directory zuständig ist auf einem Domänencontroller einen Thread hinzugefügt.  Wenn der Druckerwarteschlangendienst nicht mindestens ein Domänencontroller an jedem Standort ausgeführt wird, hat die Anzeige keine Möglichkeit zum alte Warteschlangen zu entfernen, die nicht mehr vorhanden sind. https://blogs.technet.microsoft.com/askperf/2008/11/18/disabling-unnecessary-services-a-word-to-the-wise/
|||         
            
<br />          

##  <a name="printer-extensions-and-notifications"></a>Drucker-Erweiterungen und Benachrichtigungen        
| | |           
|---|---|       
|   **Beschreibung** |   Dieser Dienst benutzerdefinierte Drucker Dialogfelder geöffnet und Benachrichtigungen über einen Remotedruckerserver oder einem Drucker behandelt. Wenn Sie diesen Dienst deaktivieren, werden nicht Drucker Erweiterungen oder Benachrichtigungen angezeigt.
|   **Dienstname**    |   PrintNotify
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   OK, um Sie zu deaktivieren, wenn keinem Druckerserver
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="problem-reports-and-solutions-control-panel-support"></a>Problemberichte und -Lösungen Systemsteuerung Unterstützung     
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst bietet Unterstützung für anzeigen, senden und Löschen von auf Systemebene Problemberichte für Problemberichte und -Lösungen-Systemsteuerung.
|   **Dienstname**    |   wercplsupport
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="program-compatibility-assistant-service"></a>Programm Kompatibilität Dienst-Assistent     
| | |           
|---|---|       
|   **Beschreibung** |   Dieser Dienst bietet Unterstützung für das Programm Compatibility-Assistenten (PCA).  PCA installieren und ausführen, indem Sie den Benutzer überwacht und bekannte Kompatibilitätsprobleme erkannt. Wenn dieser Dienst beendet wird, wird der PCA nicht ordnungsgemäß.
|   **Dienstname**    |   PcaSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="quality-windows-audio-video-experience"></a>Verbessertes Windows Audio Video-Streaming      
| | |           
|---|---|   
|   **Beschreibung** |   Verbessertes Windows-Audio-Video-Streaming (qWave) ist eine Netzwerkplattform für Audio Video (AV) Streaming von Anwendungen im privaten IP-Netzwerken. qWave verbessert AV-Streaming-Leistung und Zuverlässigkeit von Netzwerk Quality-of-Service (QoS) für AV-Anwendungen sichergestellt. Es bietet Mechanismen für die Zulassung Steuerelement Zeit Überwachung und Erzwingung, Anwendung Feedback und Priorisierung von Datenverkehr ausgeführt werden.
|   **Dienstname**    |   QWAVE
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Clientseitige QoS-Dienst
|||         
            
<br />          

##      <a name="radio-management-service"></a>Radio-Verwaltungsdienst        
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltung des Senders und Flugzeugmodus-Modus-Dienst
|   **Dienstname**    |   RmSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="remote-access-auto-connection-manager"></a>Verwaltung für automatische RAS-Verbindung            
| | |           
|---|---|   
|   **Beschreibung** |   Erstellt eine Verbindung mit einem Remotenetzwerk, wenn ein Programm eine remote DNS- oder NetBIOS-Namen oder die Adresse verweist.
|   **Dienstname**    |   RasAuto
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="remote-access-connection-manager"></a>RAS-Verbindungs-Manager         
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet DFÜ-Verbindung und virtuelle private Netzwerk (VPN) Verbindungen von diesem Computer mit dem Internet oder anderen Remote-Netzwerken. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   RasMan
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="remote-desktop-configuration"></a>Remotedesktopkonfiguration         
| | |           
|---|---|   
|   **Beschreibung** |   Konfiguration des Remotedesktop-Remotedienst (Centers oder RDCS) ist verantwortlich für alle Remote Desktop Services und Remotedesktop Konfiguration und die Sitzung Wartungsaktivitäten, die SYSTEM-Kontext erfordern. Dazu gehören temporäre Ordner für die Sitzung, RD-Designs und RD-Zertifikate.
|   **Dienstname**    |   SessionEnv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="remote-desktop-services"></a>Remote Desktop Services          
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht Benutzern, interaktiv mit einem Remotecomputer herstellen. Remotedesktop und Remotedesktop-Sitzungshostserver müssen Sie diesem Dienst abhängig.  Deaktivieren Sie die Kontrollkästchen auf der Registerkarte Remote das Systemsteuerungselement für System-Eigenschaften, um zu verhindern, dass die Remoteverwendung von diesem Computer.
|   **Dienstname**    |   TermService
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="remote-desktop-services-usermode-port-redirector"></a>Anschlussumleitung für Remote Desktop Services-Redirector        
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht die Umleitung von Druckern/Laufwerke/Ports für RDP-Verbindungen
|   **Dienstname**    |   UmRdpService
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Unterstützt die Umleitung der Verbindung auf dem Server.
|||         
            
<br />          

## <a name="remote-procedure-call-rpc"></a>Remoteprozeduraufruf (RPC)          
| | |           
|---|---|   
|   **Beschreibung** |   Der RPCSS-Dienst ist der Dienststeuerungs-Manager für COM- und DCOM-Server. Objekt Aktivierungen Anfragen, Objekt Exporter Auflösungen und verteilte Garbagecollection durchgeführt für COM- und DCOM-Server. Wenn dieser Dienst beendet oder deaktiviert ist, funktioniert mit COM oder DCOM Programme nicht ordnungsgemäß. Es wird dringend empfohlen, dass der RPCSS-Dienst ausgeführt werden.
|   **Dienstname**    |   RpcSs
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="remote-procedure-call-rpc-locator"></a>Remote Procedure Call (RPC) Locator             
| | |               
|---|---|   
|   **Beschreibung** |   In Windows2003 und früheren Versionen von Windows verwaltet (Remote Procedure Call, RPC)-Locator-Dienst die RPC-Namen-Datenbank. In Windows Vista und höheren Versionen von Windows wird dieser Dienst bietet keine Funktionen und Anwendungskompatibilität vorhanden ist.   |
|   **Dienstname**    |   RpcLocator  |
|   **Installation**    |   Nur auf Datacenter Edition  |
|   **Starttyp**   |   Manuell  |
|   **Empfehlung**  | Keine Hinweise   |
|   **Kommentare**    |       |
|||             
                
<br />              

## <a name="remote-registry"></a>Remote-Registrierung          
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht Remotebenutzern Registrierungseinstellungen auf diesem Computer zu ändern. Wenn dieser Dienst beendet wird, kann die Registrierung nur von Benutzern auf diesem Computer geändert werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   RemoteRegistry
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="resultant-set-of-policy-provider"></a>Anbieter des Richtlinienergebnissatzes            
| | |           
|---|---|       
|   **Beschreibung** |   Bietet einen Netzwerkdienst, der verarbeitet Anforderungen zum Simulieren der Anwendung der Gruppenrichtlinie für eine Zielbenutzer oder Computer in verschiedenen Situationen und die Einstellungen des Richtlinienergebnissatzes berechnet.
|   **Dienstname**    |   RSoPProv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |Keine Hinweise    
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="routing-and-remote-access"></a>Routing und Remotezugriff            
| | |           
|---|---|   
|   **Beschreibung** |   Angebote Routingdienste für Unternehmen in LAN und WAN-Umgebungen.
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
|   **Beschreibung** |   RPC-Schnittstellen-IDs in Endpunkte aufgelöst. Wenn dieser Dienst beendet oder deaktiviert ist, werden Programme, die mit Diensten (Remote Procedure Call, RPC) nicht ordnungsgemäß.
|   **Dienstname**    |   RpcEptMapper
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="secondary-logon"></a>Sekundäre Anmeldung     
| | |           
|---|---|       
|   **Beschreibung** |   Aktiviert das Starten von Prozessen mit unterschiedlichen Anmeldeinformationen. Wenn dieser Dienst beendet wird, wird diese Art der Anmeldung nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   Seclogon
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="secure-socket-tunneling-protocol-service"></a>Secure Socket Tunneling Protokolldienst            
| | |               
|---|---|       
|   **Beschreibung** |   Bietet Unterstützung für den SSTP Secure Socket Tunneling-Protokoll () für die Verbindung mit Remotecomputern über VPN. Wenn dieser Dienst deaktiviert ist, werden Benutzer nicht SSTP zu verwenden, um die RAS-Server zugreifen können.    |
|   **Dienstname**    |   SstpSvc |
|   **Installation**    |   Immer installiert    |
|   **Starttyp**   |   Manuell  |
|   **Empfehlung**  |   Deaktivieren Sie nicht  |
|   **Kommentare**    |   Deaktivieren Pausen RRAS   |
|||             
                
<br />              

## <a name="security-accounts-manager"></a>Sicherheitskonten-Manager            
| | |           
|---|---|       
|   **Beschreibung** |   Der Start dieses Diensts signalisiert andere Dienste, dass die Sicherheitskontenverwaltung (SAM) Anforderungen akzeptiert werden kann.  Deaktivieren dieses Diensts verhindert, dass andere Dienste im System benachrichtigt wird, wenn das SAM bereit ist, das kann wiederum dazu führen, dass diese Dienste nicht ordnungsgemäß gestartet. Dieser Dienst sollte nicht deaktiviert werden.
|   **Dienstname**    |   SamSs
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Deaktivieren Sie nicht
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="sensor-data-service"></a>Sensor-Datendienst  
| | |           
|---|---|   
|   **Beschreibung** |   Liefert Daten aus einer Vielzahl von Sensoren
|   **Dienstname**    |   SensorDataService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />  

## <a name="sensor-monitoring-service"></a>Sensor-Überwachungsdienst            
| | |           
|---|---|       
|   **Beschreibung** |   Überwacht die verschiedenen Sensoren, um Daten und Anpassung an System- und Status.  Wenn dieser Dienst beendet oder deaktiviert ist, wird die bildschirmhelligkeit nicht an die Lichtverhältnisse anpassen. Wenn dieser Dienst beendet beeinträchtigen anderen Systemfunktionen und Features ebenfalls.
|   **Dienstname**    |   SensrSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          
        
## <a name="sensor-service"></a>Sensor-Dienst           
| | |           
|---|---|       
|   **Beschreibung** |   Ein Dienst für Sensoren, der Funktionen verschiedener Sensoren verwaltet. Einfache Gerät Ausrichtung (SDO) und den Verlauf verwaltet für Sensoren. Lädt den SDO-Sensor, der meldet Änderungen an der Geräteausrichtung.  Wenn dieser Dienst beendet oder deaktiviert ist, der SDO-Sensor wird nicht geladen werden und daher automatische Drehung wird nicht ausgeführt. Verlauf Sammlung von Sensoren wird auch beendet werden.
|   **Dienstname**    |   SensorService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="server"></a>Server           
| | |           
|---|---|   
|   **Beschreibung** |   Unterstützt die Datei, Drucken und named Pipes über das Netzwerk für diesen Computer freigeben. Wenn dieser Dienst beendet wird, werden diese Funktionen nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   LanmanServer
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Erforderlich für die Remoteverwaltung, IPC$, SMB-Dateifreigabe
|||         
            
<br />          

## <a name="shell-hardware-detection"></a>Shellhardwareerkennung             
| | |           
|---|---|       
|   **Beschreibung** |   Für die automatische Wiedergabe Hardwareereignisse bietet.
|   **Dienstname**    |   ShellHWDetection
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="smart-card"></a>Smartcard           
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet den Zugriff auf Smartcards, die von diesem Computer gelesen. Wenn dieser Dienst beendet wird, wird dieser Computer kann nicht gelesen werden Smartcards sein. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   SCardSvr
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="smart-card-device-enumeration-service"></a>Smartcard-Dienst zum Enumeration                    
| | |               
|---|---|       
|   **Beschreibung** |   Software-Geräteknoten erstellt für alle Smartcard-Leser für eine bestimmte Sitzung. Wenn dieser Dienst deaktiviert ist, werden WinRT-APIs nicht Smartcardleser aufgelistet werden können.   |
|   **Dienstname**    |   ScDeviceEnum    |
|   **Installation**    |   Immer installiert    |
|   **Starttyp**   |   Manuell  |
|   **Empfehlung**  |   So deaktivieren Sie OK   |
|   **Kommentare**    |   Fast ausschließlich für WinRT-Apps erforderlich sind    |
|||             
                
<br />              

## <a name="smart-card-removal-policy"></a>Richtlinie für Smartcard zum Entfernen        
| | |           
|---|---|       
|   **Beschreibung** |   Kann das System so konfiguriert werden, dass den Desktop des Benutzers beim Entfernen der Smartcard gesperrt.
|   **Dienstname**    |   SCPolicySvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="snmp-trap"></a>SNMP-Trap            
| | |           
|---|---|       
|   **Beschreibung** |   Empfängt Trap-Nachrichten, die von lokalen oder Remotecomputer Simple Network Management Protocol (SNMP)-Agenten generiert wurden, und leitet die Nachricht an SNMP-Verwaltungsprogramme auf diesem Computer. Wenn dieser Dienst beendet wird, erhält der SNMP-basierte Programme auf diesem Computer keine SNMP-Trap-Nachrichten. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   SNMPTRAP
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="software-protection"></a>Softwareschutz             
| | |           
|---|---|       
|   **Beschreibung** |   Aktiviert den Download, Installation und Erzwingung von Lizenzen für digitale für Windows und Windows Anwendungen. Wenn der Dienst deaktiviert ist, können des Betriebssystems und lizenzierte Anwendung in einem Benachrichtigungsmodus ausgeführt. Es wird dringend empfohlen, dass Sie nicht den Schutz deaktivieren.
|   **Dienstname**    |   sppsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="special-administration-console-helper"></a>Hilfsprogramm für spezielle Verwaltungskonsole        
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht es Administratoren, die den Remotezugriff auf einer Befehlszeile mithilfe von Emergency Management Services.
|   **Dienstname**    |   Sacsvr
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="spot-verifier"></a>Volltonfarben Verifier            
| | |           
|---|---|   
|   **Beschreibung** |   Überprüft, potenzielle Beschädigungen am Dateisystem der Datei.
|   **Dienstname**    |   svsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="ssdp-discovery"></a>SSDP-Suche           
| | |           
|---|---|   
|   **Beschreibung** |   Ermittelt Netzwerkgeräte und Dienste, die das SSDP Discovery-Protokoll, z.B. UPnP-Geräten verwenden. Kündigt zudem SSDP-Geräte und Dienste, die auf dem lokalen Computer ausgeführt. Wenn dieser Dienst beendet wird, werden SSDP-basierte Geräte nicht ermittelt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   SSDPSRV
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="state-repository-service"></a>Status-Repository-Dienst         
| | |           
|---|---|   
|   **Beschreibung** |   Erforderliche Infrastruktur unterstützt das Anwendungsmodell.
|   **Dienstname**    |   StateRepository
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="still-image-acquisition-events"></a>Weiterhin Image Acquisition Ereignisse
| | |           
|---|---|   
|   **Beschreibung** |   Startet die Anwendung weiterhin Image Acquisition Ereignissen zugeordnet.
|   **Dienstname**    |   WiaRpc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />  

## <a name="storage-service"></a>Service für Speicher          
| | |           
|---|---|       
|   **Beschreibung** |   Aktivieren von Diensten für Einstellungen und externen Speicher-Erweiterung enthält
|   **Dienstname**    |   StorSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="storage-tiers-management"></a>Storage Tiers Management        
| | |           
|---|---|   
|   **Beschreibung** |   Optimiert die Platzierung von Daten in Speicherebenen auf alle mehrstufigen Speicherplätzen im System.
|   **Dienstname**    |   TieringEngineService
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="superfetch"></a>SuperFetch          
| | |           
|---|---|       
|   **Beschreibung** |   Verwaltet und verbessert die Systemleistung.
|   **Dienstname**    |   SysMain
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="sync-host"></a>Sync-Host            
| | |           
|---|---|       
|   **Beschreibung** |   Der Dienst synchronisiert E-Mails, Kontakte, Kalender und verschiedenen anderen Benutzerdaten. E-Mail-Nachrichten und andere Anwendungen, die auf diese Funktion funktioniert nicht ordnungsgemäß, wenn dieser Dienst nicht ausgeführt wird.
|   **Dienstname**    |   OneSyncSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Benutzer-Dienstvorlage
|||         
            
<br />          

## <a name="system-event-notification-service"></a>Benachrichtigungsdienst für Systemereignisse            
| | |           
|---|---|       
|   **Beschreibung** |   Systemereignisse überwacht und Abonnenten von COM+-Ereignissystem dieser Ereignisse benachrichtigt.
|   **Dienstname**    |   SENS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="system-events-broker"></a>System-Ereignisse Broker             
| | |           
|---|---|       
|   **Beschreibung** |   Koordiniert die Ausführung von Hintergrundarbeit für WinRT-Anwendung. Wenn dieser Dienst beendet oder deaktiviert ist, kann keine Hintergrundaufgaben ausgelöst werden.
|   **Dienstname**    |   SystemEventsBroker
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Trotz der Tatsache, die die Beschreibung impliziert, dass er nur für WinRT-Apps ist, ist es für den Taskplaner, Broker-Infrastruktur-Dienst und andere internen Komponenten erforderlich.
|||         
            
<br />          

## <a name="task-scheduler"></a>Die Aufgabenplanung           
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht einem Benutzer zu konfigurieren und planen automatisierte Aufgaben auf diesem Computer. Der Dienst hostet außerdem mehrere Windows-System-wichtigen Aufgaben. Wenn dieser Dienst beendet oder deaktiviert ist, wird diese Aufgaben nicht ausgeführt zu den geplanten Zeiten. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   Zeitplan
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="tcpip-netbios-helper"></a>TCP/IP-NetBIOS-Hilfsprogramm            
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Unterstützung für die NetBIOS über TCP/IP (NetBT)-Dienst und NetBIOS-Namensauflösung für Clients im Netzwerk daher zum Freigeben von Dateien, das es Benutzern zu drucken, und melden Sie sich mit dem Netzwerk. Wenn dieser Dienst beendet wird, können diese Funktionen nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   LMHOSTS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="telephony"></a>Telefonie           
| | |           
|---|---|       
|   **Beschreibung** |   Bietet Telefonie-API (TAPI)-Unterstützung für Programme, die steuern, Telefoniegeräte auf dem lokalen Computer und über das LAN auf Servern, auf denen auch den Dienst ausgeführt wird.
|   **Dienstname**    |   TapiSrv
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Deaktivieren Pausen RRAS
|||         
            
<br />          

## <a name="themes"></a>Designs           
| | |           
|---|---|
|   **Beschreibung** |   Stellt die Designverwaltung bereit.
|   **Dienstname**    |   Designs
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Eingabehilfen-Designs kann nicht festgelegt werden, wenn der Dienst deaktiviert ist
|||         
            
<br />  

## <a name="tile-data-model-server"></a>Kachel Datenserver Modell           
| | |           
|---|---|   
|   **Beschreibung** |   Kachel Server für die Kachelupdates.
|   **Dienstname**    |   tiledatamodelsvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Starten Sie Menü Pausen, wenn der Dienst deaktiviert ist
|||         
            
<br />          

##  <a name="time-broker"></a>Zeit Broker     
| | |           
|---|---|       
|   **Beschreibung** |   Koordiniert die Ausführung von Hintergrundarbeit für WinRT-Anwendung. Wenn dieser Dienst beendet oder deaktiviert ist, kann keine Hintergrundaufgaben ausgelöst werden.
|   **Dienstname**    |   TimeBrokerSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Trotz der Tatsache, die die Beschreibung impliziert, dass er nur für WinRT-Apps ist, ist es für den Taskplaner, Broker-Infrastruktur-Dienst und andere internen Komponenten erforderlich.
|||         
            
<br />          

## <a name="touch-keyboard-and-handwriting-panel-service"></a>Bildschirmtastatur und Schreibbereich Panel-Dienst         
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht die Bildschirmtastatur und Schreibbereich Pen und Ink-Funktionen
|   **Dienstname**    |   TabletInputService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="update-orchestrator-service-for-windows-update"></a>Orchestrator-Aktualisierungsdienst für Windows Update           
| | |           
|---|---|       
|   **Beschreibung** |   Windows verwaltet. Wenn beendet, werden Ihre Geräte werden nicht zum Herunterladen und Installieren der neuesten Updates.
|   **Dienstname**    |   UsoSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Beschreibung des Dienstes war nicht in der v1607. Windows Update (inkl. WSUS), die diesem Dienst abhängig ist.
|||         
            
<br />          

## <a name="upnp-device-host"></a>UPnP-Gerätehost         
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht das UPnP-Geräten auf diesem Computer gehostet werden. Wenn dieser Dienst beendet wird, gehosteten UPnP-Geräten werden nicht mehr funktioniert, und keine weiteren gehosteten Geräte hinzugefügt werden können. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   UPnPHost
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="user-access-logging-service"></a>Dienst für die Benutzerzugriffsprotokollierung          
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst protokolliert eindeutigen Clientanforderungen, in Form von IP-Adressen und Namen, der installierten Produkte und Rollen auf dem lokalen Server. Diese Informationen kann, über PowerShell zu quantifizieren Client bei Bedarf von Server-Software für die Verwaltung der offline (Client Access License, CAL) abgefragt werden kann. Wenn der Dienst deaktiviert ist, wird Clientanforderungen werden nicht protokolliert werden und werden nicht über PowerShell Abfragen aufgerufen werden. Beenden des Diensts wirkt sich nicht auf das Abfragen von Verlaufsdaten (Siehe unterstützende Dokumentation für die Schrittezum Löschen von Verlaufsdaten) aus. Der lokale Systemadministrator muss wenden Sie sich an, seinem, Windows Server-Lizenzbedingungen zum Bestimmen der Anzahl der Clientzugriffslizenzen, die für den Server-Software ordnungsgemäß lizenziert werden erforderlich sind; die UAL-Dienst verwenden und diese Verpflichtung Daten nicht geändert.
|   **Dienstname**    |   UALSVC
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="user-data-access"></a>Datenzugriff für Benutzer        
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht Apps den Zugriff auf Daten strukturierte Benutzers, einschließlich Kontaktinformationen, Kalender, Nachrichten und andere Inhalte. Wenn Sie beenden oder deaktivieren Sie diesen Dienst, möglicherweise Apps, die diese Daten nicht ordnungsgemäß.
|   **Dienstname**    |   UserDataSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Benutzer-Dienstvorlage
|||         
            
<br />          

## <a name="user-data-storage"></a>Speicherung von Daten            
| | |           
|---|---|       
|   **Beschreibung** |   Behandelt die Speicherung von strukturierten Benutzerdaten, einschließlich Kontaktinformationen, Kalender, Nachrichten und andere Inhalte. Wenn Sie beenden oder deaktivieren Sie diesen Dienst, möglicherweise Apps, die diese Daten nicht ordnungsgemäß.
|   **Dienstname**    |   UnistoreSvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Benutzer-Dienstvorlage
|||         
            
<br />          

## <a name="user-experience-virtualization-service"></a>User Experience Virtualization Service           
| | |           
|---|---|       
|   **Beschreibung** |   Bietet Unterstützung für die Anwendung und Betriebssystem-Einstellungen, die Roaming
|   **Dienstname**    |   UevAgentService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="user-manager"></a>Benutzer-Manager        
| | |           
|---|---|   
|   **Beschreibung** |   Benutzer-Manager bietet die Runtime-Komponenten, die für die Benutzerinteraktion mit mehreren erforderlich.  Wenn dieser Dienst beendet wird, können einige Programme möglicherweise nicht ordnungsgemäß.
|   **Dienstname**    |   UserManager
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="user-profile-service"></a>User Profile Service         
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst ist verantwortlich für das Laden und Entladen von Benutzerprofilen. Wenn dieser Dienst beendet oder deaktiviert ist, Benutzer werden nicht mehr in der Lage, sich erfolgreich angemeldet haben, oder melden Sie sich ab, Apps möglicherweise Probleme, die auf Daten des Benutzers abrufen und Komponenten registriert, um den Empfang von ereignisbenachrichtigungen Profil wird nicht empfangen werden.
|   **Dienstname**    |   ProfSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="virtual-disk"></a>Virtuelles Laufwerk             
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Verwaltungsdienste für Datenträger, Volumes, Dateisystemen und Speicherarrays.
|   **Dienstname**    |   VDS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Keine Hinweise
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="volume-shadow-copy"></a>Volumeschattenkopie-Dienst           
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet und implementiert Volumeschattenkopien, die für die Sicherung und andere Zwecke verwendet. Wenn dieser Dienst beendet wird, Schattenkopien stehen nicht für die Sicherung und die Sicherung schlägt möglicherweise fehl. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   VSS
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Keine Hinweise
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="walletservice"></a>WalletService           
| | |           
|---|---|   
|   **Beschreibung** |   Hosts-Objekte, die von Clients von der Brieftasche verwendet werden.
|   **Dienstname**    |   WalletService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-audio"></a>Windows-Audio            
| | |           
|---|---|       
|   **Beschreibung** |   Verwaltet Audio für Windows-Programme.  Wenn dieser Dienst beendet wird, funktioniert Audiogeräte und -Effekte nicht ordnungsgemäß.  Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht gestartet
|   **Dienstname**    |   AudioSrv
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-audio-endpoint-builder"></a>Windows-Audio-Endpunkt-Generator           
| | |           
|---|---|
|   **Beschreibung** |   Verwaltet Audiogeräte für den Windows-Audio-Dienst.  Wenn dieser Dienst beendet wird, funktioniert Audiogeräte und -Effekte nicht ordnungsgemäß.  Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht gestartet
|   **Dienstname**    |   AudioEndpointBuilder
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-biometric-service"></a>Windows-Biometriediensts            
| | |           
|---|---|   
|   **Beschreibung** |   Der Windows-biometriedienst ermöglicht Clientanwendungen zu erfassen, vergleichen, bearbeiten und Speichern von biometrischen Daten ohne direkten Zugriff auf biometrische Hardware oder Beispiele. Der Dienst wird in einem privilegierten SVCHOST-Prozess gehostet.
|   **Dienstname**    |   WbioSrvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="windows-camera-frame-server"></a>Windows-Kamera-Frame-Server         
| | |           
|---|---|       
|   **Beschreibung** |   Können mehrere Clients auf Videoframes Kamerageräte zugreifen.
|   **Dienstname**    |   FrameServer
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-connection-manager"></a>Windows-Verbindungs-Manager           
| | |           
|---|---|   
|   **Beschreibung** |   Stellt automatisch eine Verbindung herstellen/trennen Entscheidungen basierend auf den Optionen für die Netzwerkkonnektivität mit dem PC derzeit verfügbar und ermöglicht die Verwaltung der Netzwerkkonnektivität, die auf Gruppenrichtlinien basiert.
|   **Dienstname**    |   Wcmsvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-defender-network-inspection-service"></a>Windows Defender-Netzwerkinspektionsdienst          
| | |           
|---|---|       
|   **Beschreibung** |   Schützt vor Zugriffsversuche auf bekannte und neu entdeckte Sicherheitslücken in Netzwerkprotokolle
|   **Dienstname**    |   WdNisSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise    
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-defender-service"></a>Windows Defender-Dienst         
| | |           
|---|---|       
|   **Beschreibung** |   Schützt Benutzer vor Schadsoftware und anderer potenziell unerwünschter Software
|   **Dienstname**    |   WinDefend
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-driver-foundation---user-mode-driver-framework"></a>Windows-Treiber-Foundation - User-Mode Driver Framework           
| | |           
|---|---|   
|   **Beschreibung** |   Erstellt und verwaltet Benutzermodusprozesse Treiber. Dieser Dienst kann nicht beendet werden.
|   **Dienstname**    |   wudfsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-encryption-provider-host-service"></a>Windows-Verschlüsselung Provider-Host-Dienst     
| | |           
|---|---|   
|   **Beschreibung** |   Windows-Verschlüsselung Provider Host Service Broker-Verschlüsselung im Zusammenhang mit Funktionen von Drittanbietern Verschlüsselung auf Prozesse, die zum Bewerten und EAS-Richtlinien gelten. Beenden Dies wird EAS Konformität überprüft gefährdet, die mit den verbundenen E-Mail-Konten eingerichtet wurden
|   **Dienstname**    |   WEPHOSTSVC
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-error-reporting-service"></a>Windows-Fehlerberichterstattungsdienst          
| | |           
|---|---|       
|   **Beschreibung** |   Können Fehler gemeldet werden soll, wenn Programme nicht mehr funktioniert oder reagiert, und vorhandene Lösungen übermittelt werden. Darüber hinaus können Protokolle für die Diagnose generiert werden und Dienste reparieren. Wenn dieser Dienst beendet wird, Fehlerberichterstattung unter Umständen nicht ordnungsgemäß, und Ergebnisse der Diagnose-Services und Reparaturen möglicherweise nicht angezeigt.
|   **Dienstname**    |   WerSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Sammelt und sendet die Daten der Absturz/hängen von Microsoft und von Drittanbietern ISVs/IHVs verwendet wird. Die Daten werden zur Diagnose von Fehlern Absturz auslösen, z.B. Sicherheitsfehler verwendet. Auch erforderlich für Firmen-Fehlerberichterstattung
|||         
            
<br />          

## <a name="windows-event-collector"></a>Windows-Ereignissammlung          
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst verwaltet die permanente Abonnements von Ereignissen aus Remotequellen, die WS-Management-Protokoll unterstützen. Dazu gehören Windows Vista-Ereignisprotokolle, Hardware und IPMI-fähigen Ereignisquellen. Der Dienst Stores weitergeleitet Ereignisse in einem lokalen Ereignisprotokoll. Wenn dieser Dienst beendet oder deaktiviert ist Ereignisabonnements können nicht erstellt werden, und weitergeleitete Ereignisse können nicht angenommen werden.
|   **Dienstname**    |   Wecsvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Verwaltbarkeit, Diagnose erfasst ETW-Ereignisse (einschließlich Sicherheitsereignisse).  Viele der Features und Tools von Drittanbietern abhängig, einschließlich Sicherheitstools überwachen
|||         
            
<br />          

## <a name="windows-event-log"></a>Windows-Ereignisprotokoll            
| | |           
|---|---|       
|   **Beschreibung** |   Dieser Dienst verwaltet Ereignisse und Ereignisprotokolle. Protokollieren von Ereignissen, Abfrage und Abonnieren von Ereignissen, Archivierung von Ereignisprotokollen und Verwaltung von Ereignismetadaten unterstützt. Sie können Ereignisse in XML und Nur-Text-Format anzeigen. Beenden Sie den Dienst kann die Sicherheit und Zuverlässigkeit des Systems beeinträchtigen.
|   **Dienstname**    |   EventLog
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-firewall"></a>Windows-Firewall         
| | |           
|---|---|   
|   **Beschreibung** |   Windows-Firewall schützt Ihren Computer durch die verhindert, dass nicht autorisierte Benutzer Zugriff auf den Computer über das Internet oder einem Netzwerk.
|   **Dienstname**    |   MpsSvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="windows-font-cache-service"></a>Windows-Schriftart-Cache-Dienst      
| | |           
|---|---|   
|   **Beschreibung** |   Optimiert die Leistung der Anwendung durch das Zwischenspeichern von häufig verwendeten Schriftartdaten. Anwendungen werden dieser Dienst gestartet, wenn er nicht bereits ausgeführt wird. Sie können deaktiviert werden, obwohl dies die Leistung der Anwendung beeinträchtigen kann.
|   **Dienstname**    |   FontCache
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-image-acquisition-wia"></a>Windows Image Acquisition (WIA)          
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Image Acquisition Dienste für Scanner und Kameras
|   **Dienstname**    |   stisvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="windows-insider-service"></a>Windows-Insider-Dienst     
| | |           
|---|---|   
|   **Beschreibung** |   wisvc
|   **Dienstname**    |   wisvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Server unterstützt keine Test-Flighting, daher es No-Op auf Server ist. Feature kann auch über GP deaktiviert werden.
|||         
            
<br />          

##  <a name="windows-installer"></a>Windows Installer       
| | |           
|---|---|
|   **Beschreibung** |   Hinzugefügt, geändert und entfernt Anwendungen, die als Windows Installer (MSI,.msp)-Paket bereitgestellt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   MSIServer
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-license-manager-service"></a>Windows-Lizenz-Manager-Dienst          
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Unterstützung der Infrastruktur für den Microsoft Store.  Dieser Dienst wird bei Bedarf gestartet, und klicken Sie dann im Microsoft Store erworbene deaktiviert nicht ordnungsgemäß funktionieren.
|   **Dienstname**    |   LicenseManager
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-management-instrumentation"></a>Windows-Verwaltungsinstrumentation       
| | |           
|---|---|       
|   **Beschreibung** |   Stellt eine allgemeine Schnittstelle oder ein Objekt Management-Informationen zum Betriebssystem, Geräte, Anwendungen und Dienste zugreifen. Wenn dieser Dienst beendet wird, werden die meisten Windows-basierter Software nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   WinMgmt
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="windows-mobile-hotspot-service"></a>Windows Mobile Hotspot-Dienst          
| | |           
|---|---|       
|   **Beschreibung** |   Bietet die Möglichkeit, eine Mobilfunkverbindung für andere Geräte freigeben.
|   **Dienstname**    |   icssvc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-modules-installer"></a>Windows-Module-Installer        
| | |           
|---|---|   
|   **Beschreibung** |   Ermöglicht die Installation, Änderung und Entfernung von Windows-Updates und optionalen Komponenten. Wenn dieser Dienst deaktiviert ist, installieren oder Deinstallieren von Windows-Updates für diesen Computer bei.
|   **Dienstname**    |   TrustedInstaller
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-push-notifications-system-service"></a>Windows Push Notifications-Dienst            
| | |           
|---|---|
|   **Beschreibung** |   Dieser Dienst in Sitzung 0 und den Benachrichtigung Plattform und Verbindung-Anbieter, der behandelt die Verbindung zwischen dem Gerät und den WNS-Server hostet.
|   **Dienstname**    |   WpnService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Erforderlich für Live-Kacheln und andere Features
|||         
            
<br />      

## <a name="windows-push-notifications-user-service"></a>Windows Push Notifications User Service          
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst hostet Windows-Benachrichtigungsplattform die Unterstützung von lokalen bereitstellt und Pushbenachrichtigungen. Unterstützte Benachrichtigungen sind Kachel-, Popup- und unformatierte.
|   **Dienstname**    |   WpnUserService
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   So deaktivieren Sie OK
|   **Kommentare**    |   Benutzer-Dienstvorlage
|||         
            
<br />          
    
## <a name="windows-remote-management-ws-management"></a>Windows Remote Management (WS-Management)            
| | |           
|---|---|   
|   **Beschreibung** |   Windows-Remoteverwaltung (WinRM)-Dienst implementiert das WS-Verwaltungsprotokoll für die Remoteverwaltung. WS-Verwaltung ist ein standardmäßiges Webdienstprotokoll für die Remoteverwaltung für Software und Hardware. Der WinRM-Dienst für WS-Management-Anforderungen im Netzwerk überwacht und verarbeitet diese. Der WinRM Service muss mit einem Listener mithilfe des Befehlszeilenprogramms winrm.cmd oder über Gruppenrichtlinien konfiguriert werden, in der Reihenfolge dafür, über das Netzwerk zu überwachen. Der WinRM-Dienst ermöglicht den Zugriff auf WMI-Daten und ermöglicht eine Ereignissammlung. Ereignissammlung und das Abonnement von Ereignissen erforderlich, dass der Dienst ausgeführt wird. WinRM-Nachrichten verwenden HTTP und HTTPS als Transporte. Der WinRM-Dienst ist nicht von IIS abhängig ist jedoch vorkonfiguriert einen Port mit IIS auf demselben Computer freigeben.  Der WinRM-Dienst reserviert das /wsman URL-Präfix. Zur Vermeidung von Konflikten mit IIS Administratoren sollten stellen Sie sicher, dass keine Websites in IIS gehostete verwenden die /wsman URL-Präfix.
|   **Dienstname**    |   WinRM
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Erforderlich für die Remoteverwaltung
|||         
            
<br />          

##  <a name="windows-search"></a>Windows-Suche      
| | |           
|---|---|       
|   **Beschreibung** |   Stellt Inhaltsindex, Zwischenspeichern von Eigenschaften und Suchergebnisse für Dateien, E-Mail und andere Inhalte bereit.
|   **Dienstname**    |   WSearch
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Deaktiviert
|   **Empfehlung**  |   Bereits deaktiviert
|   **Kommentare**    |   
|||         
            
<br />          

##  <a name="windows-time"></a>Windows-Zeitdienst        
| | |           
|---|---|   
|   **Beschreibung** |   Verwaltet die Datums- und uhrzeitsynchronisierung auf allen Clients und Servern im Netzwerk. Wenn dieser Dienst beendet wird, werden Datums- und uhrzeitsynchronisierung nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   W32Time
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="windows-update"></a>Windows Update           
| | |           
|---|---|       
|   **Beschreibung** |   Ermöglicht die Erkennung, Download und Installation von Updates für Windows und anderen Programmen. Wenn dieser Dienst deaktiviert ist, Benutzer dieses Computers nicht mithilfe von Windows Update oder die Funktion zum automatischen Aktualisieren und Programme werden nicht in der Windows Update-Agent (WUA) API verwenden können.
|   **Dienstname**    |   wuauserv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="winhttp-web-proxy-auto-discovery-service"></a>WinHTTP-Web Proxy Auto-Discovery-Dienst         
| | |           
|---|---|   
|   **Beschreibung** |   WinHTTP implementiert die Client-HTTP-Protokollstapel, und bietet Entwicklern eine Win32-API und die Automatisierung der COM+-Komponente von Antworten zu sendenden HTTP-Anforderungen. WinHTTP bietet darüber hinaus Unterstützung für den automatischen Proxy-Konfiguration über die entsprechende Implementierung des Protokolls Web Proxy Auto-Discovery (WPAD) erkennen.
|   **Dienstname**    |   WinHttpAutoProxySvc
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Deaktivieren Sie nicht
|   **Kommentare**    |   Alle Elemente, die den Netzwerkstapel wird verwendet, kann dieser Dienst funktionsfähig abhängig sind. Viele Organisationen verwenden diese Option, um ihre interne Netzwerke HTTP-Proxy-Routing zu konfigurieren.  Ohne diese tritt intern mit Ursprung HTTP-Verbindungen mit dem Internet alle ein.
|||         
            
<br />          

## <a name="wired-autoconfig"></a>(Verkabelt)         
| | |           
|---|---|       
|   **Beschreibung** |   Der Konfiguration verkabelter Netzwerke (DOT3SVC) ist verantwortlich für die Durchführung von IEEE 802.1 X-Authentifizierung auf Ethernet-Schnittstellen. Wenn die aktuelle Kabelnetzwerk Bereitstellung 802. 1 X-Authentifizierung erzwingt, sollte der Dienst DOT3SVC führen Sie für die Einrichtung einer Ebene-2-Konnektivität bzw. die Bereitstellung des Zugriffs auf Netzwerkressourcen konfiguriert werden. Verkabelte Netzwerke, die nicht 802. 1 X-Authentifizierung erzwingen werden vom Dienst DOT3SVC nicht beeinflusst.
|   **Dienstname**    |   dot3svc
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise   
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="wmi-performance-adapter"></a>WMI-Leistungsadapter          
| | |           
|---|---|   
|   **Beschreibung** |   Informationen bereit von Windows-Verwaltungsinstrumentation (Windows Management Instrumentation, WMI)-Anbietern für Clients im Netzwerk. Dieser Dienst wird nur ausgeführt, wenn Leistungsdaten-Hilfsprogramm aktiviert wird.
|   **Dienstname**    |   wmiApSrv
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Manuell
|   **Empfehlung**  | Keine Hinweise       
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="workstation"></a>Arbeitsstation          
| | |           
|---|---|   
|   **Beschreibung** |   Erstellt und verwaltet Clientnetzwerkverbindungen zu Remoteservern mithilfe des SMB-Protokolls. Wenn dieser Dienst beendet wird, werden diese Verbindungen nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die abhängigen nicht starten.
|   **Dienstname**    |   "LanmanWorkstation"
|   **Installation**    |   Immer installiert
|   **Starttyp**   |   Automatisch
|   **Empfehlung**  | Keine Hinweise       
|   **Kommentare**    |   
|||         
            
<br />

## <a name="xbox-live-auth-manager"></a>Xbox Live Auth-Manager           
| | |           
|---|---|   
|   **Beschreibung** |   Bietet Authentifizierung und Autorisierung Dienste für die Interaktion mit Xbox Live. Wenn dieser Dienst beendet wird, können einige Programme möglicherweise nicht ordnungsgemäß.
|   **Dienstname**    |   XblAuthManager
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Sollte deaktiviert werden
|   **Kommentare**    |   
|||         
            
<br />          

## <a name="xbox-live-game-save"></a>Xbox Live-Spiel speichern          
| | |           
|---|---|   
|   **Beschreibung** |   Dieser Dienst synchronisiert speichern aktiviert Spiele Daten für Xbox Live.  Wenn dieser Dienst beendet wird, Spiel gespeicherten Daten nicht zum Hochladen oder Herunterladen von Xbox Live.
|   **Dienstname**    |   XblGameSave
|   **Installation**    |   Nur auf Datacenter Edition
|   **Starttyp**   |   Manuell
|   **Empfehlung**  |   Sollte deaktiviert werden
|   **Kommentare**    |   Dieser Dienst synchronisiert speichern aktiviert Spiele Daten für Xbox Live.  Wenn dieser Dienst beendet wird, Spiel gespeicherten Daten nicht zum Hochladen oder Herunterladen von Xbox Live.
|||         
                
<br /> 
<br /> 

