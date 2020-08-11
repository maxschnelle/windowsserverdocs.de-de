---
title: Sicherheitsrichtlinien für Systemdienste in Windows Server 2016
description: Sicherheitsrichtlinien für das Deaktivieren von Diensten in Windows Server 2016 mit Desktopdarstellung
ms.topic: article
ms.date: 11/26/2018
ms.assetid: b886b2fd-3567-4f0a-8aa3-4ba7923d2d21
author: nirb
ms.author: nirb
ms.openlocfilehash: 5cbe96f86d1e9b54c5f0ea455f82f9c6a4a461f3
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87950795"
---
# <a name="guidance-on-disabling-system-services-on-windows-server-2016-with-desktop-experience"></a>Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung

Gilt für: Windows Server 2016

Das Windows-Betriebssystem enthält viele Systemdienste, mit denen wichtige Funktionen bereitgestellt werden. Die Dienste verfügen über unterschiedliche Standardrichtlinien für den Start: einige werden standardmäßig gestartet (automatisch), einige bei Bedarf (manuell) und einige sind standardmäßig deaktiviert und müssen explizit aktiviert werden, bevor sie ausgeführt werden können. Diese Standardeinstellungen wurden für jeden Dienst sorgfältig gewählt, um für typische Kunden eine gute Abstimmung in Bezug auf Leistung, Funktionalität und Sicherheit zu erzielen.

Einige Unternehmenskunden ziehen für ihre Windows-PCs und -Server aber ggf. einen stärker auf Sicherheit ausgerichteten Ansatz vor, bei dem die Angriffsfläche auf das absolute Minimum reduziert ist. Diese Kunden möchten daher alle Dienste vollständig deaktivieren, die in ihren jeweiligen Umgebungen nicht benötigt werden. Für diese Kunden stellt Microsoft&reg; diese Anleitung bereit, die Hinweise dazu enthält, welche Dienste zu diesem Zweck deaktiviert werden können.

Die Anleitung gilt nur für Windows Server 2016 mit Desktopdarstellung (nicht bei Nutzung als Desktopersatz für Endbenutzer). Ab Windows Server 2019 sind diese Richtlinien standardmäßig konfiguriert. Die Dienste des Systems sind jeweils wie folgt kategorisiert:

- **Deaktivierung empfohlen**: Für sicherheitsorientierte Unternehmen wird die Deaktivierung dieses Diensts und der Verzicht auf die damit verbundenen Funktionen in den meisten Fällen empfohlen (siehe zusätzliche Details unten).
- **Deaktivierung OK**: Dieser Dienst verfügt über Funktionen, die für einige Unternehmen nützlich sind. Er kann von sicherheitsorientierten Unternehmen, die ihn nicht nutzen, problemlos deaktiviert werden.
- **Nicht deaktivieren**: Wenn Dienste dieser Art deaktiviert werden, wirkt sich dies auf grundlegende Funktionen aus, oder es wird verhindert, dass bestimmte Rollen oder Features richtig funktionieren. Daher sollten sie nicht deaktiviert werden.
- **Kein Hinweis**: Die Auswirkungen der Deaktivierung dieser Dienste wurden noch nicht vollständig evaluiert. Aus diesem Grund sollte die Standardkonfiguration dieser Dienste nicht geändert werden.

Kunden können ihre Windows-PCs und -Server konfigurieren, um ausgewählte Dienste zu deaktivieren, indem sie die Sicherheitsvorlagen in ihren Gruppenrichtlinien oder die PowerShell-Automatisierung verwenden. In einigen Fällen umfasst die Anleitung bestimmte Gruppenrichtlinieneinstellungen, mit denen die Funktionen des Diensts direkt deaktiviert werden. Dies ist eine Alternative zum Deaktivieren des gesamten Diensts.

Microsoft empfiehlt Kunden die Deaktivierung der folgenden Dienste und der jeweiligen geplanten Aufgaben unter Windows Server 2016 mit Desktopdarstellung:

Dienste:
1. Xbox Live Authentifizierungs-Manager
2. Xbox Live-Spiele speichern

Geplante Aufgaben:
1. \Microsoft\XblGameSave\XblGameSaveTask
2. \Microsoft\XblGameSave\XblGameSaveTaskLogon

Sie können auf die Informationen zu allen Diensten in diesem Artikel auch zugreifen, indem Sie die angefügte Microsoft Excel-Tabelle anzeigen: [Anleitungen zur Deaktivierung von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung](https://msdnshared.blob.core.windows.net/media/2017/05/Service-management-WS2016.xlsx).)

### <a name="disabling-services-not-installed-by-default"></a>Deaktivieren von nicht standardmäßig installierten Diensten

Microsoft rät von der Anwendung von Richtlinien zum Deaktivieren von Diensten ab, die nicht standardmäßig installiert werden.
- Der Dienst wird in der Regel benötigt, wenn das Feature installiert ist. Für das Installieren des Diensts bzw. des Features sind Administratorrechte erforderlich. Lege nicht das Starten des Diensts als unzulässig fest, sondern das Installieren des Features.
- Durch das Blockieren des Microsoft Windows-Diensts wird nicht verhindert, dass ein Administrator (oder in einigen Fällen auch andere Benutzer) einen ähnlichen Dienst eines Drittanbieters installiert, der unter Umständen mit einem höheren Sicherheitsrisiko verbunden ist.
- Wenn ein nicht zum Standard gehörender Windows-Dienst (z. B. W3SVC) per Baseline oder Benchmark deaktiviert wird, erweckt dies bei einigen Prüfern den Eindruck, als ob die Technologie (z. B. IIS) grundsätzlich unsicher ist und niemals verwendet werden sollte.
- Wenn das Feature (und der Dienst) niemals installiert wird, macht dies die Baseline und den Prüfaufwand nur unnötig komplizierter.

Die beiden folgenden Tabellen enthalten für alle in diesem Dokument aufgeführten Dienste eine Beschreibung der Spalten und Microsoft-Empfehlungen zum Aktivieren und Deaktivieren von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung:

### <a name="explanation-of-columns"></a>Beschreibung der Spalten

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Schlüsselname (interner Name) des Diensts |
| **Beschreibung** | Die Beschreibung des Diensts aus „sc.exe qdescription“. |
| **Installation** | *Immer installiert*: Dienst ist unter Windows Server 2016 Core und Windows Server 2016 mit Desktopdarstellung installiert. *Nur mit Desktopdarstellung*: Dienst ist unter Windows Server 2016 mit Desktopdarstellung, aber ***nicht*** unter Server Core installiert. |
| **Starttyp** | Starttyp des Diensts unter Windows Server 2016 |
| **Empfehlung** | Empfehlung/Hinweis von Microsoft zur Deaktivierung dieses Diensts unter Windows Server 2016 bei einer typischen, gut verwalteten Unternehmensbereitstellung, bei der der Server nicht als Desktopersatz für den Endbenutzer verwendet wird. |
| **Kommentare** | Zusätzliche Beschreibung |

### <a name="explanation-of-microsoft-recommendations"></a>Beschreibung von Microsoft-Empfehlungen

| Name | BESCHREIBUNG |
|--|--|
| **Nicht deaktivieren** | Dieser Dienst sollte nicht deaktiviert werden. |
| **Deaktivierung OK** | Dieser Dienst kann deaktiviert werden, wenn das von ihm unterstützte Feature nicht verwendet wird. |
| **Bereits deaktiviert** | Dieser Dienst wird standardmäßig deaktiviert. Die Erzwingung per Richtlinie ist nicht erforderlich. |
| **Deaktivierung empfohlen** | Dieser Dienst sollte auf einem gut verwalteten Unternehmenssystem niemals aktiviert werden. |

Die folgenden Tabellen enthalten Microsoft-Anleitungen zum Deaktivieren von Systemdiensten unter Windows Server 2016 mit Desktopdarstellung:


## <a name="activex-installer-axinstsv"></a>ActiveX-Installationsprogramm (AxInstSV)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AxInstSV |
| **Beschreibung** | Ermöglicht die Überprüfung der Benutzerkontensteuerung für die Installation von ActiveX-Steuerelementen über das Internet und die Verwaltung der Installation von ActiveX-Steuerelementen basierend auf Gruppenrichtlinieneinstellungen. Dieser Dienst wird bedarfsgesteuert gestartet, und wenn er deaktiviert ist, verhält sich die Installation von ActiveX-Steuerelementen gemäß den Einstellungen des Standardbrowsers. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Die Deaktivierung ist in Ordnung, wenn das Feature nicht benötigt wird. |

## <a name="alljoyn-router-service"></a>AllJoyn-Routerdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AJRouter |
| **Beschreibung** | Leitet AllJoyn-Mitteilungen für die lokalen AllJoyn-Clients um. Wenn dieser Dienst angehalten wird, können die AllJoyn-Clients, die nicht über eigene gebündelte Router verfügen, nicht ausgeführt werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="app-readiness"></a>App-Bereitschaft

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AppReadiness |
| **Beschreibung** | Bereitet Apps für die Nutzung vor, wenn sich ein Benutzer zum ersten Mal am PC anmeldet und neue Apps hinzugefügt werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Keine |

## <a name="application-identity"></a>Anwendungsidentität

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AppIDSvc |
| **Beschreibung** | Ermittelt und überprüft die Identität einer Anwendung. Wenn dieser Dienst deaktiviert wird, kann AppLocker nicht erzwungen werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="application-information"></a>Anwendungsinformationen

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Appinfo |
| **Beschreibung** | Ermöglicht das Ausführen von interaktiven Anwendungen mit zusätzlichen Administratorrechten. Wenn dieser Dienst beendet wird, können Benutzer keine Anwendungen mit den zusätzlichen Administratorrechten mehr starten, die sie für bestimmte Benutzeraufgaben unter Umständen benötigen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Unterstützt die Rechteerweiterung für die Benutzerkontensteuerung auf demselben Desktop |

## <a name="application-layer-gateway-service"></a>Gatewaydienst auf Anwendungsebene

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | ALG |
| **Beschreibung** | Stellt Unterstützung für Drittanbieterprotokoll-Plug-Ins für die gemeinsame Nutzung der Internetverbindung bereit. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="application-management"></a>Anwendungsverwaltung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AppMgmt |
| **Beschreibung** | Verarbeitet Installations-, Entfernungs und Enumerationsanforderungen für Software, die über die Gruppenrichtlinie bereitgestellt wird. Wenn der Dienst deaktiviert wird, können Benutzer keine Software mehr installieren, entfernen oder enumerieren, die per Gruppenrichtlinie bereitgestellt wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="appx-deployment-service-appxsvc"></a>AppX-Bereitstellungsdienst (AppXSVC)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AppXSvc |
| **Beschreibung** | Stellt Infrastrukturunterstützung für die Bereitstellung von Store-Anwendungen bereit. Dieser Dienst wird bedarfsgesteuert gestartet. Wenn er deaktiviert wird, werden Store-Anwendungen nicht für das System bereitgestellt und funktionieren ggf. nicht richtig. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="auto-time-zone-updater"></a>Automatische Zeitzonenaktualisierung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | tzautoupdate |
| **Beschreibung** | Legt die Zeitzone des Systems automatisch fest. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |

## <a name="background-intelligent-transfer-service"></a>Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | BITS |
| **Beschreibung** | Überträgt Dateien im Hintergrund, indem ungenutzte Netzwerkbandbreite verwendet wird. Wenn der Dienst deaktiviert wird, können alle Anwendungen, die von BITS abhängig sind, z. B. Windows Update oder MSN Explorer, Programme und andere Informationen nicht automatisch herunterladen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="background-tasks-infrastructure-service"></a>Infrastrukturdienst für Hintergrundaufgaben

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | BrokerInfrastructure |
| **Beschreibung** | Windows-Infrastrukturdienst, mit dem gesteuert wird, welche Hintergrundaufgaben auf dem System ausgeführt werden können. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="base-filtering-engine"></a>Basisfiltermodul

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | BFE |
| **Beschreibung** | Das Basisfiltermodul (Base Filtering Engine, BFE) ist ein Dienst, mit dem Firewall- und IPsec-Richtlinien (Internetprotokollsicherheit) verwaltet werden und die Benutzermodusfilterung implementiert wird. Wenn der BFE-Dienst beendet oder deaktiviert wird, bedeutet dies eine erhebliche Reduzierung der Systemsicherheit. Darüber hinaus führt dies zu unvorhersehbarem Verhalten von IPsec-Verwaltungs- und Firewallanwendungen. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="bluetooth-support-service"></a>Bluetooth-Unterstützungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | bthserv |
| **Beschreibung** | Der Bluetooth-Dienst unterstützt die Ermittlung und Zuordnung von externen Bluetooth-Geräten. Das Beenden oder Deaktivieren dieses Diensts kann dazu führen, dass bereits installierte Bluetooth-Geräte nicht mehr richtig funktionieren und verhindert wird, dass neue Geräte ermittelt oder zugeordnet werden können. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Die Deaktivierung ist in Ordnung, wenn der Dienst nicht verwendet wird. Ein weiterer Mechanismus für die Deaktivierung: [Deaktivieren von Bluetooth und Infrarot-Übertragung](/previous-versions/tn-archive/dd252791(v=technet.10)) |

## <a name="cdpusersvc"></a>CDPUserSvc

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | CDPUserSvc |
| **Beschreibung** | Dieser Benutzerdienst wird für Szenarien mit der Plattform für verbundene Geräte verwendet. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Benutzerdienstvorlage |

## <a name="certificate-propagation"></a>Zertifikatverteilung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | CertPropSvc |
| **Beschreibung** | Kopiert Benutzer- und Stammzertifikate von Smartcards in den Zertifikatspeicher des aktuellen Benutzers, erkennt das Einlegen einer Smartcard in einen Smartcardleser und installiert bei Bedarf den zugehörigen Plug & Play-Minitreiber. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="client-license-service-clipsvc"></a>Clientlizenzdienst (ClipSVC)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | ClipSVC |
| **Beschreibung** | Stellt Infrastrukturunterstützung für den Microsoft Store bereit. Dieser Dienst wird bedarfsgesteuert gestartet, und wenn er deaktiviert wird, verhalten sich über den Microsoft Store gekaufte Anwendungen nicht korrekt. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="cng-key-isolation"></a>CNG-Schlüsselisolation

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | KeyIso
| **Beschreibung** | Der CNG-Schlüsselisolationsdienst wird im LSA-Prozess gehostet. Der Dienst stellt eine Schlüsselprozessisolation für private Schlüssel und zugehörige Kryptografievorgänge gemäß den Anforderungen der allgemeinen Kriterien bereit. Der Dienst speichert und verwendet langlebige Schlüssel in einem sicheren Prozess in Übereinstimmung mit den Anforderungen der allgemeinen Kriterien.
| **Installation** | Immer installiert
| **Starttyp** | Manuell
| **Empfehlung** | Kein Hinweis
| **Kommentare** | Keine |

## <a name="com-event-system"></a>COM+-Ereignissystem

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | EventSystem |
| **Beschreibung** | Unterstützt den Systemereignis-Benachrichtigungsdienst (SENS), mit dem Ereignisse automatisch an abonnierende COM-Komponenten verteilt werden. Nach dem Beenden des Diensts wird SENS geschlossen, so dass keine weiteren Anmelde- und Abmeldebenachrichtigungen bereitgestellt werden können. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="com-system-application"></a>COM+-Systemanwendung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | COMSysApp |
| **Beschreibung** | Verwaltet die Komponentenkonfiguration und -überwachung von COM+-basierten Komponenten. Nach dem Beenden des Diensts sind die meisten COM+-basierten Komponenten nicht ordnungsgemäß funktionsfähig. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="computer-browser"></a>Computerbrowser

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Browser |
| **Beschreibung** | Führt eine aktuelle Liste der Computer im Netzwerk und gibt diese an als Browser fungierende Computer weiter. Diese Liste wird nicht aktualisiert oder gewartet, falls der Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |

## <a name="connected-devices-platform-service"></a>Plattformdienst für verbundene Geräte

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | CDPSvc |
| **Beschreibung** | Dieser Dienst wird für verbundene Geräte und Universal Glass-Szenarien verwendet. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="connected-user-experiences-and-telemetry"></a>Benutzererfahrung und Telemetrie im verbundenen Modus

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DiagTrack |
| **Beschreibung** | Durch den Dienst für Benutzererfahrung und Telemetrie im verbundenen Modus werden Features aktiviert, die Benutzerfreundlichkeit in Anwendungen und im verbundenen Modus unterstützen. Außerdem verwaltet dieser Dienst die ereignisgesteuerte Sammlung und Übertragung von Diagnose- und Nutzungsdaten (die zur Verbesserung der Benutzerfreundlichkeit und Qualität der Windows-Plattform eingesetzt werden). Dazu müssen die Diagnose- und Nutzungseinstellungen in der Datenschutzoption unter „Feedback und Diagnose“ aktiviert sein. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="contact-data"></a>Kontaktdaten

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PimIndexMaintenanceSvc |
| **Beschreibung** | Indiziert Kontaktdaten für die schnelle Kontaktsuche. Wenn du diesen Dienst beendest oder deaktivierst, können Kontakte in den Suchergebnissen fehlen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Benutzerdienstvorlage |

## <a name="coremessaging"></a>CoreMessaging

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | CoreMessagingRegistrar |
| **Beschreibung** | Verwaltet die Kommunikation zwischen Systemkomponenten. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="credential-manager"></a>Anmeldeinformationsverwaltung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | VaultSvc |
| **Beschreibung** | Ermöglicht die sichere Speicherung und den Abruf von Anmeldeinformationen für Benutzer, Anwendungen und Sicherheitspakete. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="cryptographic-services"></a>Kryptografische Dienste

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | CryptSvc |
| **Beschreibung** | Stellt drei Verwaltungsdienste bereit: den Katalogdatenbankendienst, der die Signaturen von Windows-Dateien bestätigt und die Installation neuer Programme ermöglicht, den geschützten Stammdienst, der diesem Computer vertrauenswürdige Zertifikate von Stammzertifizierungsstellen hinzufügt und diese vom Computer entfernt, und den automatischen Aktualisierungsdienst für die Stammzertifizierung, der Stammzertifikate vom Windows Update abruft und Szenarien wie SSL aktiviert. Wird dieser Dienst beendet, funktionieren diese Verwaltungsdienste nicht ordnungsgemäß. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="data-sharing-service"></a>Datenfreigabedienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DsSvc |
| **Beschreibung** | Dient als Datenbroker zwischen Anwendungen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="datacollectionpublishingservice"></a>DataCollectionPublishingService

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DcpSvc |
| **Beschreibung** | Der Dienst für die Erfassung und Veröffentlichung von Daten (Data Collection and Publishing, DCP) unterstützt Erstanbieter-Apps zum Hochladen von Daten in die Cloud. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="dcom-server-process-launcher"></a>DCOM-Server-Prozessstart

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DcomLaunch |
| **Beschreibung** | Der Dienst DCOMLAUNCH startet COM- und DCOM-Server als Reaktion auf Objektaktivierungsanforderungen. Wenn dieser Dienst beendet oder deaktiviert wird, funktionieren Programme, für die COM oder DCOM genutzt wird, nicht richtig. Wir empfehlen dir dringend, den Dienst DCOMLAUNCH auszuführen. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="device-association-service"></a>Gerätezuordnungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DeviceAssociationService |
| **Beschreibung** | Ermöglicht die Kopplung zwischen dem System und verkabelten Geräten oder Drahtlosgeräten. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="device-install-service"></a>Geräteinstallationsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DeviceInstall |
| **Beschreibung** | Ermöglicht einem Computer die Erkennung und Anpassung an Hardwareänderungen mit nur wenigen oder ganz ohne Benutzereingaben. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="device-management-enrollment-service"></a>Registrierungsdienst für die Geräteverwaltung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DmEnrollmentSvc |
| **Beschreibung** | Führt Aktivitäten der Geräteregistrierung für die Geräteverwaltung durch. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="device-setup-manager"></a>Geräteinstallations-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DsmSvc |
| **Beschreibung** | Ermöglicht die Erkennung, den Download und die Installation von gerätebezogener Software. Wenn dieser Dienst deaktiviert wird, werden die Geräte ggf. mit veralteter Software konfiguriert und funktionieren unter Umständen nicht richtig. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="devquery-background-discovery-broker"></a>Broker für DevQuery-Hintergrundermittlung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DevQueryBroker |
| **Beschreibung** | Ermöglicht Apps die Ermittlung von Geräten per Hintergrundaufgabe. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="dhcp-client"></a>DHCP-Client

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Dhcp |
| **Beschreibung** | Registriert und aktualisiert IP-Adressen und DNS-Einträge für diesen Computer. Wenn dieser Dienst beendet wird, empfängt der Computer keine dynamischen IP-Adressen und DNS-Updates mehr. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="diagnostic-policy-service"></a>Diagnoserichtliniendienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | DPS |
| **Beschreibung** | Der Diagnoserichtliniendienst ermöglicht die Problemerkennung, Problembehandlung und Lösung für Windows-Komponenten. Wenn dieser Dienst beendet wird, funktioniert die Diagnose nicht mehr. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="diagnostic-service-host"></a>Diagnosediensthost

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WdiServiceHost |
| **Beschreibung** | Der Diagnosediensthost wird vom Diagnoserichtliniendienst als Host für Diagnosen verwendet, die im Kontext eines lokalen Diensts ausgeführt werden müssen. Wird dieser Dienst beendet, funktionieren alle davon abhängigen Diagnosen nicht mehr ordnungsgemäß. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="diagnostic-system-host"></a>Diagnosesystemhost

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WdiSystemHost |
| **Beschreibung** | Der Diagnosesystemhost wird vom Diagnoserichtliniendienst verwendet, um Diagnosen zu hosten, die für einen lokalen Dienst durchgeführt werden müssen. Wird dieser Dienst beendet, funktionieren alle davon abhängigen Diagnosen nicht mehr ordnungsgemäß. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="distributed-link-tracking-client"></a>Überwachung verteilter Verknüpfungen (Client)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TrkWks |
| **Beschreibung** | Verwaltet die Links zwischen NTFS-Dateien auf einem Computer oder für die Computer eines Netzwerks. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="distributed-transaction-coordinator"></a>Distributed Transaction Coordinator

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | MSDTC |
| **Beschreibung** | Koordiniert Transaktionen, die sich über mindestens zwei Ressourcenverwaltungen wie Datenbanken, Nachrichtenwarteschlangen oder Dateisysteme erstrecken. Wenn der Dienst beendet ist, treten bei diesen Transaktionen Fehler auf. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="dmwappushsvc"></a>dmwappushsvc

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | dmwappushservice |
| **Beschreibung** | WAP Push-Nachrichtenroutingdienst |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Dieser Dienst wird auf Clientgeräten für Intune, MDM und ähnlichen Verwaltungstechnologien sowie für einheitliche Schreibfilter benötigt. Für Server ist der Dienst nicht erforderlich. |

## <a name="dns-client"></a>DNS-Client

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Dnscache |
| **Beschreibung** | Der DNS-Clientdienst (dnscache) wird zum Zwischenspeichern von DNS-Namen (Domain Name System) verwendet und registriert den vollständigen Computernamen für diesen Computer. Wenn der Dienst angehalten wird, werden DNS-Namen weiterhin aufgelöst. Die Ergebnisse von DNS-Namensabfragen werden jedoch nicht zwischengespeichert, und der Name des Computers wird nicht registriert. Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="downloaded-maps-manager"></a>Manager für heruntergeladene Karten

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | MapsBroker |
| **Beschreibung** | Windows-Dienst für den Anwendungszugriff auf heruntergeladene Karten. Dieser Dienst wird bedarfsgesteuert je nach der Anwendung gestartet, die auf heruntergeladene Karten zugreift. Wenn der Dienst deaktiviert wird, können Apps nicht auf Karten zugreifen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Wenn der Dienst deaktiviert wird, funktionieren Apps nicht mehr, die den Dienst benötigen. Die Aktivierung ist kein Problem, wenn der Dienst von Apps nicht benötigt wird. |

## <a name="embedded-mode"></a>Eingebetteter Modus

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | embeddedmode |
| **Beschreibung** | Der Dienst „Eingebetteter Modus“ ermöglicht Szenarien, die sich auf Hintergrundanwendungen beziehen. Wenn dieser Dienst deaktiviert wird, wird die Aktivierung von Hintergrundanwendungen verhindert. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="encrypting-file-system-efs"></a>Verschlüsselndes Dateisystem (EFS)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | EFS |
| **Beschreibung** | Eine wichtige Dateiverschlüsselungstechnologie zum Speichern verschlüsselter Dateien auf Volumes mit dem Dateisystem NTFS. Wenn dieser Dienst beendet oder deaktiviert wird, können Anwendungen nicht mehr auf verschlüsselte Dateien zugreifen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |

## <a name="enterprise-app-management-service"></a>Verwaltungsdienst für Unternehmens-Apps

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | EntAppSvc |
| **Beschreibung** | Ermöglicht die Verwaltung von Unternehmensanwendungen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="extensible-authentication-protocol"></a>Extensible Authentication-Protokoll

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | EapHost |
| **Beschreibung** | Der EAP-Dienst (Extensible Authentication Protocol) stellt in folgenden Szenarios eine Netzwerkauthentifizierung bereit: 802.1X (verkabelt und drahtlos), VPN und NAP (Network Access Protection). EAP stellt darüber hinaus APIs (Application Programming Interface, Anwendungsprogrammierschnittstelle) bereit, die von Netzwerkzugriffclients, einschließlich Drahtlosclients und VPN-Clients, beim Authentifizierungsvorgang verwendet werden. Wenn du diesen Dienst deaktivierst, kann dieser Computer nicht mehr auf Netzwerke zugreifen, die eine EAP-Authentifizierung verwenden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="function-discovery-provider-host"></a>Funktionssuchanbieter-Host

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | fdPHost |
| **Beschreibung** | Der FDPHOST-Dienst dient zum Hosten der Netzwerkerkennungsanbieter für die Funktionssuche (Function Discovery, FD). Von diesen FD-Anbietern werden Netzwerkerkennungsdienste für das Simple Services Discovery-Protokoll (SSDP) und das Web Services – Discovery (WS-D)-Protokoll bereitgestellt. Durch das Beenden oder Deaktivieren des FDPHOST-Diensts wird bei Verwendung von FD die Netzwerkerkennung für diese Protokolle deaktiviert. Ist dieser Dienst nicht verfügbar, können mit Netzwerkdiensten, von denen FD und diese Erkennungsprotokolle verwendet werden, keine Netzwerkgeräte oder -ressourcen gesucht werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="function-discovery-resource-publication"></a>Funktionssuche-Ressourcenveröffentlichung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | FDResPub |
| **Beschreibung** | Veröffentlicht diesen Computer und die daran angeschlossenen Ressourcen, damit sie über das Netzwerk gesucht werden können. Wenn dieser Dienst beendet wird, werden die Netzwerkressourcen nicht mehr veröffentlicht, damit sie von anderen Computern im Netzwerk gesucht werden können. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="geolocation-service"></a>Geolocation-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | lfsvc |
| **Beschreibung** | Dieser Dienst überwacht den aktuellen Standort des Systems und verwaltet Geofences (geografische Standorte mit zugeordneten Ereignissen). Wenn du diesen Dienst deaktivierst, sind Anwendungen nicht in der Lage, Benachrichtigungen zu Geolocations oder Geofences zu nutzen oder zu empfangen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Wenn der Dienst deaktiviert wird, funktionieren Apps nicht mehr, die den Dienst benötigen. Die Aktivierung ist kein Problem, wenn der Dienst von Apps nicht benötigt wird. |



## <a name="group-policy-client"></a>Gruppenrichtlinienclient

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | gpsvc |
| **Beschreibung** | Der Dienst ist für das Anwenden von Einstellungen verantwortlich, die über die Gruppenrichtlinienkomponente durch Administratoren für den Computer und die Benutzer konfiguriert wurden. Wenn der Dienst deaktiviert wird, werden die Einstellungen nicht angewendet. Somit können Anwendungen und Komponenten nicht über die Gruppenrichtlinie verwaltet werden. Von der Gruppenrichtlinienkomponente abhängige Komponenten oder Anwendungen funktionieren zudem ggf. nicht, wenn der Dienst deaktiviert wird. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="human-interface-device-service"></a>Eingabegerätedienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | hidserv |
| **Beschreibung** | Aktiviert und unterstützt die Verwendung von Abkürzungstasten auf Tastaturen, Fernbedienungen und anderen Multimediageräten. Wir empfehlen dir, diesen Dienst auszuführen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="hv-host-service"></a>HV-Hostdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | HvHost |
| **Beschreibung** | Stellt eine Schnittstelle für den Hyper-V-Hypervisor bereit, um für das Hostbetriebssystem Leistungsindikatoren pro Partition verfügbar zu machen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Leistungsoptimierungen für Gast-VMs. Wird heutzutage meist nicht mehr verwendet (mit Ausnahme von explizit aufgefüllten VMs), aber der Dienst wird für Application Guard eingesetzt. |



## <a name="hyper-v-data-exchange-service"></a>Hyper-V-Datenaustauschdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmickvpexchange |
| **Beschreibung** | Stellt einen Mechanismus zum Austauschen von Daten zwischen dem virtuellen Computer und dem Betriebssystem bereit, das auf dem physischen Computer ausgeführt wird. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-guest-service-interface"></a>Hyper-V-Gastdienstschnittstelle

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmicguestinterface |
| **Beschreibung** | Stellt eine Schnittstelle für den Hyper-V-Host für die Interaktion mit bestimmten Diensten bereit, die auf dem virtuellen Computer ausgeführt werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-guest-shutdown-service"></a>Hyper-V-Dienst zum Herunterfahren des Gasts

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmicshutdown |
| **Beschreibung** | Stellt einen Mechanismus zum Herunterfahren des Betriebssystems dieses virtuellen Computers über die Verwaltungsschnittstellen auf dem physischen Computer bereit. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-heartbeat-service"></a>Hyper-V Taktdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmicheartbeat |
| **Beschreibung** | Überwacht den Zustand dieses virtuellen Computers, indem in regelmäßigen Abständen ein Heartbeat gemeldet wird. Mit diesem Dienst kannst du ausgeführte virtuelle Computer identifizieren, die nicht mehr reagieren. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-powershell-direct-service"></a>Hyper-V-Dienst PowerShell Direct

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmicvmsession |
| **Beschreibung** | Stellt einen Mechanismus bereit, um einen virtuellen Computer mit PowerShell über eine VM-Sitzung ohne virtuelles Netzwerk zu verwalten. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-remote-desktop-virtualization-service"></a>Hyper-V-Remotedesktopvirtualisierungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmicrdv |
| **Beschreibung** | Stellt eine Plattform für die Kommunikation zwischen dem virtuellen Computer und dem Betriebssystem bereit, das auf dem physischen Computer ausgeführt wird. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-time-synchronization-service"></a>Hyper-V-Zeitsynchronisierungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmictimesync |
| **Beschreibung** | Synchronisiert die Systemzeit dieses virtuellen Computers mit der Systemzeit des physischen Computers. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="hyper-v-volume-shadow-copy-requestor"></a>Hyper-V-Volumeschattenkopie-Anforderer

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vmicvss |
| **Beschreibung** | Koordiniert die Kommunikation, die erforderlich ist, damit der Volumeschattenkopie-Dienst zum Sichern von Anwendungen und Daten auf diesem virtuellen Computer basierend auf dem Betriebssystem des physischen Computers verwendet werden kann. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Siehe „HvHost“. |



## <a name="ike-and-authip-ipsec-keying-modules"></a>IKE- und AuthIP IPsec-Schlüsselerstellungsmodule

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | IKEEXT |
| **Beschreibung** | Die IKEEXT-Diensthosts der Schlüsselerstellungsmodule für IKE (Internet Key Exchange) und Auth-IP (Authenticated Internet Protocol). Diese Schlüsselerstellungsmodule werden für die Authentifizierung und den Schlüsselaustausch in Internet Protocol Security (IPsec) verwendet. Wenn du den IKEEXT-Dienst anhältst oder deaktivierst, wird der IKE/AuthIP-Schlüsselaustausch mit Peercomputern deaktiviert. IPsec ist im Allgemeinen für die Verwendung von IKE/AuthIP konfiguriert, und das Anhalten oder Deaktivieren des IKEEXT-Diensts kann zu einem IPsec-Fehler führen und die Sicherheit des Systems gefährden. Wir empfehlen dir dringend, den Dienst IKEEXT auszuführen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="interactive-services-detection"></a>Erkennung interaktiver Dienste

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UI0Detect |
| **Beschreibung** | Aktiviert die Benutzerbenachrichtigung von Benutzereingaben für interaktive Dienste. Dies ermöglicht den Zugriff auf von interaktiven Diensten erstellte Dialogfelder, wenn diese angezeigt werden. Wenn dieser Dienst beendet wird, funktionieren Benachrichtigungen über neue interaktive Dienstdialogfelder nicht mehr, und der Zugriff auf Dialogfelder von interaktiven Diensten ist eventuell nicht möglich. Wenn dieser Dienst deaktiviert wird, funktionieren weder die Benachrichtigung über noch der Zugriff auf neue interaktive Dienstdialogfelder. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="internet-connection-sharing-ics"></a>Gemeinsame Nutzung der Internetverbindung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SharedAccess |
| **Beschreibung** | Stellt die Dienste für die Netzwerkadressenübersetzung, Adressierung, Namensauflösung bzw. Verhinderung von Eindringversuchen für ein Heimnetzwerk oder ein Netzwerk eines kleinen Büros bereit. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Ist für Clients erforderlich, die als WLAN-Hotspots genutzt werden, und außerdem an beiden Enden einer Miracast-Projektion. Die gemeinsame Nutzung der Internetverbindung kann mit der GPO-Einstellung „Verwendung der gemeinsam genutzten Internetverbindung im eigenen DNS-Domänennetzwerk nicht zulassen“ blockiert werden. |



## <a name="ip-helper"></a>IP-Hilfsprogramm

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | iphlpsvc |
| **Beschreibung** | Stellt Tunnelkonnektivität mithilfe von IPv6-Übergangstechnologien (IP6-zu-IP4, ISATAP, Portproxy und Teredo) und IP-HTTPS bereit. Wenn der Dienst beendet wird, verfügt der Computer nicht über die durch diese Technologien ermöglichten Konnektivitätsvorteile. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="ipsec-policy-agent"></a>IPsec-Richtlinien-Agent

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PolicyAgent |
| **Beschreibung** | IPsec (Internetprotokollsicherheit) unterstützt die Peerauthentifizierung auf Netzwerkebene, die Datenursprungsauthentifizierung, die Datenintegrität, die Datenvertraulichkeit (Verschlüsselung) und den Replay-Schutz. Dieser Dienst erzwingt IPsec-Richtlinien, die mit dem Snap-In „IP-Sicherheitsrichtlinien“ oder dem Befehlszeilentool „netsh ipsec“ erstellt wurden. Wenn du diesen Dienst beendest, treten unter Umständen Probleme mit der Netzwerkkonnektivität auf, falls es für deine Richtlinie erforderlich ist, dass für Verbindungen IPsec genutzt wird. Darüber hinaus ist die Remoteverwaltung der Windows-Firewall nicht verfügbar, wenn dieser Dienst beendet wird. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="kdc-proxy-server-service-kps"></a>KDC-Proxyserverdienst (KPS)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | KPSSVC |
| **Beschreibung** | Der KDC-Proxyserverdienst wird auf Edgeservern ausgeführt, um als Proxy für Kerberos-Protokollnachrichten für Domänencontroller im Unternehmensnetzwerk zu fungieren. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="ktmrm-for-distributed-transaction-coordinator"></a>KtmRm für Distributed Transaction Coordinator

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | KtmRm |
| **Beschreibung** | Koordiniert Transaktionen zwischen dem Distributed Transaction Coordinator (MSDTC) und dem Kerneltransaktions-Manager (KTM). Wir empfehlen dir, diesen Dienst zu beenden, falls er nicht benötigt wird. Falls der Dienst benötigt wird, wird er sowohl vom MSDTC als auch vom KTM automatisch gestartet. Wenn dieser Dienst deaktiviert ist, tritt für alle MSDTC-Transaktionen, die mit einem Kernelressourcen-Manager interagieren, ein Fehler auf. Alle Dienste, die explizit davon abhängen, können nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="link-layer-topology-discovery-mapper"></a>Verbindungsschicht-Topologieerkennungs-Zuordnungsprogramm

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | lltdsvc |
| **Beschreibung** | Erstellt eine Netzwerkübersicht mit Computer- und Gerätetopologieinformationen (d. h. Konnektivitätsinformationen) sowie Metadaten, die jeden PC und jedes Gerät beschreiben. Wenn dieser Dienst deaktiviert wird, funktioniert die Netzwerkübersicht nicht richtig. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Kann deaktiviert werden, wenn keine Abhängigkeiten von der Netzwerkübersicht bestehen. |



## <a name="local-session-manager"></a>Lokaler Sitzungs-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | LSM |
| **Beschreibung** | Windows-Kerndienst, der lokale Benutzersitzungen verwaltet. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="microsoft-r-diagnostics-hub-standard-collector"></a>Standardsammlungsdienst des Microsoft(R)-Diagnose-Hubs

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | diagnosticshub.standardcollector.service |
| **Beschreibung** | Standardsammlungsdienst des Diagnose-Hubs. Bei der Ausführung sammelt dieser Dienst ETW-Echtzeitereignisse und verarbeitet sie. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="microsoft-account-sign-in-assistant"></a>Anmelde-Assistent für Microsoft-Konten

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | wlidsvc |
| **Beschreibung** | Ermöglicht die Benutzeranmeldung über die Identitätsdienste des Microsoft-Kontos. Wenn dieser Dienst beendet wird, können sich Benutzer nicht mehr mit ihrem Microsoft-Konto am Computer anmelden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Microsoft-Konten sind unter Windows Server nicht verfügbar. |



## <a name="microsoft-app-v-client"></a>Microsoft App-V Client

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AppVClient |
| **Beschreibung** | Dient zum Verwalten von App-V-Benutzern und virtuellen Anwendungen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |



## <a name="microsoft-iscsi-initiator-service"></a>Microsoft iSCSI-Initiator-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | MSiSCSI |
| **Beschreibung** | Dient zum Verwalten von iSCSI-Sitzungen (Internet SCSI) von diesem Computer zu iSCSI-Remotezielgeräten. Wenn dieser Dienst beendet wird, kann sich dieser Computer nicht an iSCSI-Zielen anmelden und nicht darauf zugreifen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Unsere Diagnosedaten deuten darauf hin, dass dieser Dienst auf Clients und auf Servern genutzt wird. Die Deaktivierung hat keinerlei Vorteile. |



## <a name="microsoft-passport"></a>Microsoft Passport

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NgcSvc |
| **Beschreibung** | Ermöglicht eine Prozessisolation für Kryptografieschlüssel, die zum Authentifizieren der zugeordneten Identitätsanbieter eines Benutzers verwendet werden. Wenn dieser Dienst deaktiviert wird, ist die gesamte Anwendung und Verwaltung dieser Schlüssel nicht verfügbar. Dies gilt auch für die Computeranmeldung und einmaliges Anmelden für Apps und Websites. Dieser Dienst wird automatisch gestartet und beendet. Wir empfehlen dir, diesen Dienst nicht neu zu konfigurieren. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Wird für PIN/Hello-Anmeldungen benötigt, die auf dem Server nicht unterstützt werden. |



## <a name="microsoft-passport-container"></a>Microsoft Passport-Container

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NgcCtnrSvc |
| **Beschreibung** | Verwaltet lokale Benutzeridentitätsschlüssel, um Benutzer für Identitätsanbieter und virtuelle TPM-Smartcards zu authentifizieren. Wenn dieser Dienst deaktiviert wird, kann nicht auf lokale Benutzeridentitätsschlüssel und virtuelle TPM-Smartcards zugegriffen werden. Wir empfehlen dir, diesen Dienst nicht neu zu konfigurieren. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="microsoft-software-shadow-copy-provider"></a>Microsoft-Softwareschattenkopie-Anbieter

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | swprv |
| **Beschreibung** | Verwaltet softwarebasierte Volumeschattenkopien des Volumeschattenkopie-Diensts. Softwarebasierte Volumeschattenkopien können nicht verwaltet werden, wenn dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="microsoft-storage-spaces-smp"></a>Microsoft-SMP für Speicherplätze

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | smphost |
| **Beschreibung** | Hostdienst für den Microsoft-Verwaltungsanbieter für Speicherplätze. Wird dieser Dienst beendet oder deaktiviert, ist die Verwaltung von Speicherplätzen nicht mehr möglich. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Für APIs für die Speicherverwaltung tritt ohne diesen Dienst ein Fehler auf. Beispiel: "Get-WmiObject -class MSFT_Disk -Namespace Root\Microsoft\Windows\Storage". |



## <a name="nettcp-port-sharing-service"></a>Net.Tcp-Portfreigabedienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NetTcpPortSharing |
| **Beschreibung** | Ermöglicht die Freigabe von TCP-Ports über das net.tcp-Protokoll. |
| **Installation** | Immer installiert |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |



## <a name="netlogon"></a>Netlogon

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Netlogon |
| **Beschreibung** | Dient zum Verwalten eines sicheren Kanals zwischen diesem Computer und dem Domänencontroller für die Authentifizierung von Benutzern und Diensten. Wenn dieser Dienst angehalten wird, kann der Computer Benutzer und Dienste möglicherweise nicht authentifizieren, und der Domänencontroller kann keine DNS-Datensätze registrieren. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="network-connection-broker"></a>Netzwerkverbindungsbroker

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NcbService |
| **Beschreibung** | Fungiert als Broker für Verbindungen, über die Microsoft Store-Apps Benachrichtigungen über das Internet empfangen können. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="network-connections"></a>Netzwerkverbindungen

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Netman |
| **Beschreibung** | Verwaltet Objekte im Ordner „Netzwerk- und Wählverbindungen“, in dem LAN- und Remoteverbindungen angezeigt werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="network-connectivity-assistant"></a>Netzwerkkonnektivitäts-Assistent

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NcaSvc |
| **Beschreibung** | Stellt die Benachrichtigung zum DirectAccess-Status für Komponenten der Benutzeroberfläche bereit. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="network-list-service"></a>Netzwerklistendienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | netprofm |
| **Beschreibung** | Identifiziert die Netzwerke, mit denen der Computer eine Verbindung hergestellt hat, sammelt und speichert Eigenschaften für diese Netzwerke und benachrichtigt Anwendungen, wenn sich diese Eigenschaften ändern. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="network-location-awareness"></a>NLA (Network Location Awareness)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NlaSvc |
| **Beschreibung** | Sammelt und speichert Konfigurationsinformationen für das Netzwerk und benachrichtigt Programme, wenn diese Informationen geändert werden. Wenn dieser Dienst beendet wird, sind die Konfigurationsinformationen möglicherweise nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="network-setup-service"></a>Netzwerkeinrichtungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | NetSetupSvc |
| **Beschreibung** | Der Netzwerkeinrichtungsdienst verwaltet die Installation von Netzwerktreibern und ermöglicht die Konfiguration von Netzwerkeinstellungen auf unterer Ebene. Wenn der Dienst beendet wird, werden aktuell ausgeführte Treiberinstallationen unter Umständen abgebrochen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="network-store-interface-service"></a>Netzwerkspeicher-Schnittstellendienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | nsi |
| **Beschreibung** | Dieser Dienst stellt Netzwerkbenachrichtigungen (z. B. beim Hinzufügen/Löschen von Schnittstellen) für Benutzermodusclients bereit. Wenn du diesen Dienst beendest, wird die Netzwerkkonnektivität getrennt. Wenn dieser Dienst deaktiviert wird, können andere Dienste, die von diesem Dienst ausschließlich abhängig sind, nicht mehr gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="offline-files"></a>Offlinedateien

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | CscService |
| **Beschreibung** | Der Offlinedateiendienst führt Wartungsaktivitäten am Cache für Offlinedateien aus, reagiert auf Benutzeranmelde- und -abmeldeereignisse, implementiert die internen Komponenten der öffentlichen API, leitet interessante Ereignisse an Empfänger weiter, die an Offlineaktivitäten interessiert sind, und ändert den Cachestatus. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |



## <a name="optimize-drives"></a>Laufwerke optimieren

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | defragsvc |
| **Beschreibung** | Unterstützt den Computer bei einer effizienteren Ausführung durch das Optimieren von Dateien auf Speicherlaufwerken. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="performance-counter-dll-host"></a>Leistungsindikator-DLL-Host

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PerfHost |
| **Beschreibung** | Ermöglicht Remotebenutzern und 64-Bit-Prozessen die Abfrage von Leistungsindikatoren, die von 32-Bit-DLLs bereitgestellt werden. Wenn dieser Dienst beendet wird, können nur lokale Benutzer und 32-Bit-Prozesse die von den 32-Bit-DLLs bereitgestellten Leistungsindikatoren abfragen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="performance-logs--alerts"></a>Leistungsprotokolle und -warnungen

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | pla |
| **Beschreibung** | „Leistungsprotokolle und -warnungen“ sammelt Leistungsdaten von lokalen oder Remotecomputern basierend auf vorkonfigurierten Zeitplanparametern und schreibt die Daten dann in ein Protokoll oder löst eine Warnung aus. Wenn dieser Dienst beendet wird, werden keine Leistungsinformationen erfasst. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="phone-service"></a>Telefondienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PhoneSvc |
| **Beschreibung** | Verwaltet den Telefoniestatus des Geräts. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Wird von modernen VoIP-Apps verwendet. |



## <a name="plug-and-play"></a>Plug & Play

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PlugPlay |
| **Beschreibung** | Ermöglicht einem Computer die Erkennung und Anpassung an Hardwareänderungen mit nur wenigen oder ganz ohne Benutzereingaben. Das Beenden oder Deaktivieren dieses Diensts führt zu Instabilität des Systems. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="portable-device-enumerator-service"></a>Enumeratordienst für tragbare Geräte

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WPDBusEnum |
| **Beschreibung** | Erzwingt Gruppenrichtlinien für Wechsel-Massenspeichergeräte. Ermöglicht Anwendungen wie Windows Media Player und dem Bildimport-Assistenten, Inhalte unter Verwendung von Wechsel-Massenspeichergeräten zu übertragen und zu synchronisieren. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="power"></a>Stromversorgung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Leistung |
| **Beschreibung** | Verwaltet die Energierichtlinie und die Zustellung der Energierichtlinienbenachrichtigung. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="print-spooler"></a>Druckspooler

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Spooler |
| **Beschreibung** | Dieser Dienst spoolt Druckaufträge und verarbeitet Interaktionen mit dem Drucker. Wenn du diesen Dienst ausschaltest, kannst du weder drucken noch Drucker anzeigen. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kann deaktiviert werden, wenn es sich nicht um einen Druckerserver oder einen Domänencontroller handelt. |
| **Kommentare** | Auf einem Domänencontroller wird dem Spoolerdienst bei Installation der Domänencontroller-Rolle ein Thread hinzugefügt, der für die Durchführung der Druckbereinigung zuständig ist. Hiermit werden die veralteten Objekte der Druckwarteschlange aus Active Directory entfernt. Wenn der Spoolerdienst nicht auf mindestens einem DC auf jeder Site ausgeführt wird, kann AD keine alten Warteschlangen entfernen, die nicht mehr vorhanden sind. [Blog „Ask the Performance Team“](https://techcommunity.microsoft.com/t5/ask-the-performance-team/bg-p/AskPerf). |



## <a name="printer-extensions-and-notifications"></a>Druckererweiterungen und Benachrichtigungen

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PrintNotify |
| **Beschreibung** | Mit diesem Dienst werden benutzerdefinierte Druckerdialogfelder geöffnet und Benachrichtigungen von einem Remotedruckerserver oder Drucker verarbeitet. Wenn du diesen Dienst deaktivierst, werden keine Druckererweiterungen oder Benachrichtigungen angezeigt. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kann deaktiviert werden, wenn es sich nicht um einen Druckerserver handelt. |
| **Kommentare** | Keine |



## <a name="problem-reports-and-solutions-control-panel-support"></a>Unterstützung in der Systemsteuerung unter Lösungen für Probleme

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | wercplsupport |
| **Beschreibung** | Dieser Dienst bietet Unterstützung für das Anzeigen, Senden und Löschen von Problemberichten auf Systemebene für das Applet „Lösungen für Probleme“ in der Systemsteuerung. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="program-compatibility-assistant-service"></a>Programmkompatibilitäts-Assistent-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | PcaSvc |
| **Beschreibung** | Dieser Dienst bietet Unterstützung für den Programmkompatibilitäts-Assistenten (Program Compatibility Assistant, PCA). Mit dem PCA werden die vom Benutzer installierten und ausgeführten Programme überwacht. Wenn dieser Dienst beendet wird, wird der PCA nicht ordnungsgemäß ausgeführt. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="quality-windows-audio-video-experience"></a>Verbessertes Windows-Audio-/Video-Streaming

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | QWAVE |
| **Beschreibung** | Der Windows-Dienst für verbessertes Audio/Video-Streaming (qWave) ist eine Netzwerkplattform für Audio/Video-Streaminganwendungen (AV) in privaten IP-Netzwerken. qWave verbessert die AV-Streamingleistung und -zuverlässigkeit, indem Netzwerk-QoS (Quality-of-Service) für AV-Anwendungen sichergestellt wird. Es werden Mechanismen für Zugangssteuerung, Laufzeitüberwachung und -erzwingung, Anwendungsfeedback sowie Verkehrspriorisierung bereitgestellt. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Clientseitiger QoS-Dienst |



## <a name="radio-management-service"></a>Funkverwaltungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RmSvc |
| **Beschreibung** | Dienst für Funkverwaltung und Flugzeugmodus |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="remote-access-auto-connection-manager"></a>Verwaltung für automatische RAS-Verbindung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RasAuto |
| **Beschreibung** | Erstellt eine Verbindung mit einem Remotenetzwerk, wenn ein Programm auf einen Remote-DNS- oder -NetBIOS-Namen (bzw. eine Adresse) verweist. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="remote-access-connection-manager"></a>RAS-Verbindungs-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RasMan |
| **Beschreibung** | Verwaltet Einwähl- und VPN-Verbindungen zwischen diesem Computer und dem Internet oder anderen Remotenetzwerken. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="remote-desktop-configuration"></a>Remotedesktopkonfiguration

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SessionEnv |
| **Beschreibung** | Der Remotedesktop-Konfigurationsdienst (Remote Desktop Configuration Service, RDCS) ist für alle Konfigurations- und Sitzungsverwaltungsaktivitäten im Zusammenhang mit den Remotedesktopdiensten und Remotedesktop zuständig, die den SYSTEM-Kontext erfordern. Dazu gehören die sitzungsspezifischen temporären Ordner, Remotedesktopthemen und Remotedesktopzertifikate. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Keine |



## <a name="remote-desktop-services"></a>Remotedesktopdienste

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TermService |
| **Beschreibung** | Ermöglicht Benutzern das Herstellen einer interaktiven Verbindung mit einem Remotecomputer. Remotedesktop und Remotedesktop-Hostserver können nur zusammen mit diesem Dienst verwendet werden. Wenn du die Remoteverwendung dieses Computers verhindern möchtest, muss du die Kontrollkästchen auf der Registerkarte „Remote“ in den Systemsteuerungsoptionen deaktivieren. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Keine |



## <a name="remote-desktop-services-usermode-port-redirector"></a>Anschlussumleitung für Remotedesktopdienst im Benutzermodus

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UmRdpService |
| **Beschreibung** | Ermöglicht die Umleitung von Druckern, Laufwerken und Anschlüssen für RDP-Verbindungen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Unterstützt Umleitungen auf der Serverseite der Verbindung. |



## <a name="remote-procedure-call-rpc"></a>Remoteprozeduraufruf (RPC)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RpcSs |
| **Beschreibung** | Der RPCSS-Dienst wird als Dienststeuerungs-Manager für COM- und DCOM-Server verwendet. Von ihm werden Objektaktivierungsanforderungen, Objektexporterauflösungen und die verteilte Garbage Collection für COM- und DCOM-Server ausgeführt. Wenn dieser Dienst beendet oder deaktiviert wird, werden Programme, für die COM oder DCOM verwendet wird, nicht ordnungsgemäß ausgeführt. Wir empfehlen dir dringend, den RPCSS-Dienst auszuführen. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="remote-procedure-call-rpc-locator"></a>RPC-Locator

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RpcLocator |
| **Beschreibung** | Unter Windows 2003 und früheren Windows-Versionen wird mit dem RPC-Locatordienst (Remote Procedure Call) die RPC-Namensdienstdatenbank verwaltet. Unter Windows Vista und höheren Windows-Versionen stellt dieser Dienst keine Funktionalität bereit und ist nur für Zwecke der Anwendungskompatibilität vorhanden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="remote-registry"></a>Remoteregistrierung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RemoteRegistry |
| **Beschreibung** | Ermöglicht es Remotebenutzern, Registrierungseinstellungen dieses Computers zu verändern. Wenn dieser Dienst beendet wird, kann die Registrierung nur von lokalen Benutzern dieses Computers verändert werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Keine |



## <a name="resultant-set-of-policy-provider"></a>Richtlinienergebnissatzanbieter

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RSoPProv |
| **Beschreibung** | Stellt einen Netzwerkdienst bereit, der Anforderungen zum Simulieren der Anwendung von Gruppenrichtlinieneinstellungen auf einen Zielbenutzer oder -computer in verschiedenen Situationen verarbeitet und einen sich daraus ergebenden Satz von Richtlinieneinstellungen berechnet. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="routing-and-remote-access"></a>Routing und RAS

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RemoteAccess |
| **Beschreibung** | Bietet Routingdienste in LAN- und WAN-Netzwerkumgebungen. |
| **Installation** | Immer installiert |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Bereits deaktiviert |



## <a name="rpc-endpoint-mapper"></a>RPC-Endpunktzuordnung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | RpcEptMapper |
| **Beschreibung** | Löst RPC-Schnittstellen-IDs für den Transport von Endpunkten auf. Wenn dieser Dienst angehalten oder deaktiviert wird, können Programme, für die Remoteprozeduraufruf-Dienste (Remote Procedure Call, RPC) verwendet werden, nicht ordnungsgemäß ausgeführt werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="secondary-logon"></a>Sekundäre Anmeldung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | seclogon |
| **Beschreibung** | Aktiviert das Starten von Prozessen mit verschiedenen Anmeldeinformationen. Wenn dieser Dienst beendet wird, ist dieser Typ von Anmeldezugriff nicht mehr verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="secure-socket-tunneling-protocol-service"></a>SSTP-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SstpSvc |
| **Beschreibung** | Unterstützt SSTP (Secure Socket Tunneling-Protokoll), um über VPN eine Verbindung mit Remotecomputern herzustellen. Wenn dieser Dienst deaktiviert ist, können Benutzer SSTP nicht für den Zugriff auf Remoteserver verwenden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Wenn der Dienst deaktiviert wird, treten RRAS-Fehler auf. |



## <a name="security-accounts-manager"></a>Sicherheitskonto-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SamSs |
| **Beschreibung** | Durch den Start dieses Diensts wird anderen Diensten signalisiert, dass die Sicherheitskontenverwaltung (SAM) bereit ist, Anforderungen anzunehmen. Wenn du diesen Dienst deaktivierst, wird verhindert, dass andere Dienste im System benachrichtigt werden, wenn die Sicherheitskontenverwaltung bereit ist. Dies kann wiederum dazu führen, dass diese Dienste nicht korrekt gestartet werden. Dieser Dienst sollte nicht deaktiviert werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Keine |



## <a name="sensor-data-service"></a>Sensordatendienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SensorDataService |
| **Beschreibung** | Liefert Daten von verschiedenen Sensoren. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="sensor-monitoring-service"></a>Sensorüberwachungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SensrSvc |
| **Beschreibung** | Überwacht verschiedene Sensoren, um Daten verfügbar zu machen und eine Anpassung an den System- und Benutzerstatus vorzunehmen. Wird dieser Dienst beendet oder deaktiviert, wird die Anzeigehelligkeit nicht an die Lichtbedingungen der Umgebung angepasst. Das Beenden des Diensts kann auch andere Systemfeatures betreffen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |


## <a name="sensor-service"></a>Sensordienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SensorService |
| **Beschreibung** | Ein Sensordienst, der die Funktionen verschiedener Sensoren verwaltet. Er verwaltet SDO (Simple Device Orientation) und den Verlauf für Sensoren und lädt den SDO-Sensor, der Änderungen der Geräteausrichtung meldet. Wenn der Dienst beendet oder deaktiviert wird, wird der SDO-Sensor nicht geladen, und es findet keine automatische Drehung statt. Die Sammlung von Verlaufsdaten von den Sensoren wird ebenfalls beendet. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |


## <a name="server"></a>Server

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | LanmanServer |
| **Beschreibung** | Unterstützt Datei-, Drucker- und Named-Piped-Freigabe für diesen Computer über das Netzwerk. Diese Funktionen sind nicht mehr verfügbar, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Wird für die Remoteverwaltung, IPC$ und SMB-Dateifreigabe benötigt. |



## <a name="shell-hardware-detection"></a>Shellhardwareerkennung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | ShellHWDetection |
| **Beschreibung** | Zeigt Meldungen für Hardwareereignisse für automatische Wiedergabe an. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="smart-card"></a>Smartcard

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SCardSvr |
| **Beschreibung** | Verwaltet den Zugriff auf Smartcards, die von diesem Computer gelesen werden. Wenn dieser Dienst beendet wird, kann der Computer keine Smartcards mehr lesen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |



## <a name="smart-card-device-enumeration-service"></a>Smartcard-Geräteaufzählungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | ScDeviceEnum |
| **Beschreibung** | Erstellt Softwaregeräteknoten für alle Smartcardleser, die einer bestimmten Sitzung zur Verfügung stehen. Wird dieser Dienst deaktiviert, können von WinRT-APIs keine Smartcardleser aufgezählt werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Wird fast ausschließlich für WinRT-Apps benötigt. |



## <a name="smart-card-removal-policy"></a>Richtlinie zum Entfernen der Smartcard

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SCPolicySvc |
| **Beschreibung** | Lässt eine Konfiguration des Systems zu, bei der der Benutzerdesktop beim Entfernen der Smartcard gesperrt wird. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="snmp-trap"></a>SNMP-Trap

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SNMPTRAP |
| **Beschreibung** | Empfängt Trap-Nachrichten, die von lokalen oder Remote-SNMP-Agents generiert wurden, und leitet die Nachrichten an SNMP-Verwaltungsprogramme weiter, die auf diesem Computer ausgeführt werden. SNMP-basierte Programme auf diesem Computer empfangen keine SNMP-Trap-Nachrichten, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="software-protection"></a>Softwareschutz

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | sppsvc |
| **Beschreibung** | Aktiviert das Herunterladen, die Installation und die Durchsetzung digitaler Lizenzen für Windows und Windows-Anwendungen. Wenn der Dienst deaktiviert wird, werden das Betriebssystem und lizenzierte Anwendungen in einem Benachrichtigungsmodus ausgeführt. Es wird dringend empfohlen, den Softwareschutzdienst nicht zu deaktivieren. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="special-administration-console-helper"></a>Hilfsprogramm für spezielle Verwaltungskonsole

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | sacsvr |
| **Beschreibung** | Ermöglicht Administratoren über die Notverwaltungsdienste (Emergency Management Services, EMS) den Remotezugriff auf eine Eingabeaufforderung. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="spot-verifier"></a>Echtzeit-Datenträgerprüfung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | svsvc |
| **Beschreibung** | Überprüft mögliche Beschädigungen des Dateisystems. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="ssdp-discovery"></a>SSDP-Suche

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SSDPSRV |
| **Beschreibung** | Sucht nach Netzwerkgeräten und -diensten, die das SSDP-Suchprotokoll verwenden, z. B. UPnP-Geräte. Kündigt zudem SSDP-Geräte und -dienste an, die auf dem lokalen Computer ausgeführt werden. Wenn dieser Dienst beendet wird, werden SSDP-basierte Geräte nicht entdeckt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="state-repository-service"></a>StateRepository-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | StateRepository |
| **Beschreibung** | Bietet die erforderliche Infrastrukturunterstützung für das Anwendungsmodell. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="still-image-acquisition-events"></a>Ereignisse zum Abrufen von Standbildern

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WiaRpc |
| **Beschreibung** | Startet Anwendungen im Zusammenhang mit Ereignissen zum Abrufen von Standbildern. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="storage-service"></a>Speicherdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | StorSvc |
| **Beschreibung** | Stellt Unterstützungsdienste für Speichereinstellungen und externe Speichererweiterung bereit. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="storage-tiers-management"></a>Storage Tiers Management

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TieringEngineService |
| **Beschreibung** | Optimiert die Verteilung der Daten auf den Speicherstufen für alle mehrstufigen Speicherplätze im System. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="superfetch"></a>Superfetch

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SysMain |
| **Beschreibung** | Verwaltet und verbessert die Systemleistung im Zeitablauf. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="sync-host"></a>Synchronisierungshost

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | OneSyncSvc |
| **Beschreibung** | Dieser Dienst synchronisiert E-Mail-, Kontakt-, Kalender- und verschiedene andere Benutzerdaten. Wenn dieser Dienst nicht ausgeführt wird, funktionieren E-Mail-Programme und andere Anwendungen, die von dieser Funktionalität abhängig sind, nicht ordnungsgemäß. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Benutzerdienstvorlage |



## <a name="system-event-notification-service"></a>Benachrichtigungsdienst für Systemereignisse

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SENS |
| **Beschreibung** | Überwacht Systemereignisse und benachrichtigt Abonnenten des COM+-Ereignissystems bei diesen Ereignissen. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="system-events-broker"></a>Systemereignissebroker

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | SystemEventsBroker |
| **Beschreibung** | Koordiniert die Ausführung der Hintergrundvorgänge für WinRT-Anwendungen. Wird dieser Dienst beendet oder deaktiviert, werden die Hintergrundvorgänge unter Umständen nicht ausgelöst. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | In der Beschreibung wird nur die Nutzung für WinRT-Apps erwähnt, aber der Dienst wird auch für die Aufgabenplanung, den Brokerinfrastrukturdienst und andere interne Komponenten benötigt. |



## <a name="task-scheduler"></a>Aufgabenplanung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Zeitplan |
| **Beschreibung** | Ermöglicht es einem Benutzer, automatische Aufgaben auf diesem Computer zu konfigurieren und zu planen. Der Dienst hostet auch mehrere kritische Aufgaben für das Windows-System. Wenn dieser Dienst beendet oder deaktiviert wird, werden diese Vorgänge nicht zu den geplanten Zeiten ausgeführt. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="tcpip-netbios-helper"></a>TCP/IP-NetBIOS-Hilfsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | lmhosts |
| **Beschreibung** | Bietet Unterstützung für den NetBIOS-über-TCP/IP-Dienst (NetBT) und die NetBIOS-Namensauflösung für Clients im Netzwerk, sodass Benutzer Daten gemeinsam nutzen, drucken und sich am Netzwerk anmelden können. Diese Funktionen sind nicht mehr verfügbar, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="telephony"></a>Telephony

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TapiSrv |
| **Beschreibung** | Bietet Telefonie-API-Unterstützung (TAPI) für Programme, die lokale und über das LAN auf Servern (die diesen Dienst ebenfalls ausführen) angebundene Telefoniegeräte steuern. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Wenn der Dienst deaktiviert wird, treten RRAS-Fehler auf. |



## <a name="themes"></a>Designs

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Designs |
| **Beschreibung** | Stellt die Designverwaltung zur Verfügung. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Es können keine Designs für Barrierefreiheit festgelegt werden, wenn dieser Dienst deaktiviert ist. |



## <a name="tile-data-model-server"></a>Kacheldaten-Modellserver

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | tiledatamodelsvc |
| **Beschreibung** | Kachelserver zur Kachelaktualisierung. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Wenn dieser Dienst deaktiviert wird, tritt für das Startmenü ein Fehler auf. |



## <a name="time-broker"></a>Zeitbroker

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TimeBrokerSvc |
| **Beschreibung** | Koordiniert die Ausführung der Hintergrundvorgänge für WinRT-Anwendungen. Wird dieser Dienst beendet oder deaktiviert, werden die Hintergrundvorgänge unter Umständen nicht ausgelöst. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | In der Beschreibung wird nur die Nutzung für WinRT-Apps erwähnt, aber der Dienst wird auch für die Aufgabenplanung, den Brokerinfrastrukturdienst und andere interne Komponenten benötigt. |



## <a name="touch-keyboard-and-handwriting-panel-service"></a>Dienst für Bildschirmtastatur und Schreibbereich

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TabletInputService |
| **Beschreibung** | Aktiviert die Stift- und Freihandfunktionalität der Bildschirmtastatur und des Schreibbereichs. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="update-orchestrator-service-for-windows-update"></a>Update Orchestrator Service für Windows Update

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UsoSvc |
| **Beschreibung** | Verwaltet Windows-Updates. Wenn der Dienst beendet wird, können auf deinen Geräten keine aktuellen Updates heruntergeladen und installiert werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | In v1607 hat die Dienstbeschreibung gefehlt. Dieser Dienst wird für Windows Update (inkl. WSUS) benötigt. |



## <a name="upnp-device-host"></a>UPnP-Gerätehost

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | upnphost |
| **Beschreibung** | Ermöglicht es, dass UPnP-Geräte auf diesem Computer gehostet werden können. Wenn dieser Dienst beendet wird, sind alle gehosteten UPnP-Geräte nicht mehr betriebsbereit, und es können keine weiteren gehosteten Geräte hinzugefügt werden. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="user-access-logging-service"></a>Dienst für die Benutzerzugriffsprotokollierung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UALSVC |
| **Beschreibung** | Mithilfe dieses Diensts werden eindeutige Clientzugriffsanforderungen in Form von IP-Adressen und Benutzernamen von auf dem lokalen Server installierten Produkten und Rollen protokolliert. Diese Informationen können über PowerShell von Administratoren abgefragt werden, die den Clientbedarf an Serversoftware für die Offlineverwaltung von Clientzugriffslizenzen (Client Access License, CAL) berechnen müssen. Wenn der Dienst deaktiviert wird, werden Clientanforderungen nicht protokolliert und sind daher nicht über PowerShell-Abfragen abrufbar. Wird der Dienst beendet, so beeinflusst dies nicht die Abfrage von Verlaufsdaten. (Schritte zum Löschen von Verlaufsdaten findest du in der begleitenden Dokumentation.) Der lokale Systemadministrator muss in den Windows Server-Lizenzbedingungen die Anzahl von Clientzugriffslizenzen festlegen, die für eine ordnungsgemäße Lizenzierung der Serversoftware erforderlich ist. Die Verwendung des UAL-Diensts und der UAL-Daten entbinden nicht von dieser Verpflichtung. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="user-data-access"></a>Benutzerdatenzugriff

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UserDataSvc |
| **Beschreibung** | Ermöglicht Apps den Zugriff auf strukturierte Benutzerdaten, z. B. Kontaktinformationen, Kalender, Nachrichten und andere Inhalte. Wenn du diesen Dienst beendest oder deaktivierst, funktionieren Apps, die diese Daten verwenden, möglicherweise nicht ordnungsgemäß. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Benutzerdienstvorlage |



## <a name="user-data-storage"></a>Benutzerdatenspeicher

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UnistoreSvc |
| **Beschreibung** | Verarbeitet die Speicherung strukturierter Benutzerdaten, z. B. Kontaktinformationen, Kalender, Nachrichten und andere Inhalte. Wenn du diesen Dienst beendest oder deaktivierst, funktionieren Apps, die diese Daten verwenden, möglicherweise nicht ordnungsgemäß. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Benutzerdienstvorlage |



## <a name="user-experience-virtualization-service"></a>User Experience Virtualization-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UevAgentService |
| **Beschreibung** | Stellt Unterstützung für das Roaming von Anwendungen und Betriebssystemeinstellungen bereit. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |



## <a name="user-manager"></a>Benutzer-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | UserManager |
| **Beschreibung** | Der Benutzer-Manager stellt die Laufzeitkomponenten bereit, die für Interaktionen mit mehreren Benutzern erforderlich sind. Wenn dieser Dienst beendet wird, funktionieren einige Anwendungen möglicherweise nicht korrekt. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="user-profile-service"></a>Benutzerprofildienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | ProfSvc |
| **Beschreibung** | Dieser Dienst ist für das Laden und Entladen von Benutzerprofilen verantwortlich. Wenn dieser Dienst beendet oder deaktiviert ist, können Benutzer sich nicht mehr an- oder abmelden. Zudem können Probleme beim Abrufen von Benutzerdaten für Apps auftreten, und Komponenten, die für den Empfang von Profilereignisbenachrichtigungen registriert sind, erhalten keine Benachrichtigungen. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="virtual-disk"></a>Virtueller Datenträger

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | vds |
| **Beschreibung** | Stellt Verwaltungsdienste für Datenträger, Volumes, Dateisysteme und Speicherarrays bereit. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="volume-shadow-copy"></a>Volumeschattenkopie

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | VSS |
| **Beschreibung** | Verwaltet und implementiert Volumeschattenkopien, die zu Sicherungs- und anderen Zwecken verwendet werden. Wenn dieser Dienst beendet wird, sind keine Schattenkopien für Sicherungen verfügbar, und die Sicherung kann eventuell fehlschlagen. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="walletservice"></a>WalletService

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WalletService |
| **Beschreibung** | Von Clients der Funktion „Brieftasche“ verwendete Hostobjekte. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="windows-audio"></a>Windows-Audio

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Audiosrv |
| **Beschreibung** | Verwaltet Audioinhalte für Windows-basierte Programme. Wenn dieser Dienst beendet wird, funktionieren Audiogeräte und -effekte nicht ordnungsgemäß. Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="windows-audio-endpoint-builder"></a>Windows-Audio-Endpunkterstellung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | AudioEndpointBuilder |
| **Beschreibung** | Verwaltet Audiogeräte für den Windows-Audiodienst. Wenn dieser Dienst beendet wird, funktionieren Audiogeräte und -effekte nicht ordnungsgemäß. Wenn der Dienst deaktiviert wird, können Dienste, die explizit von diesem Dienst abhängig sind, nicht gestartet werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="windows-biometric-service"></a>Windows-Biometriedienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WbioSrvc |
| **Beschreibung** | Mit dem Windows-Biometriedienst können in Clientanwendungen biometrische Daten erfasst, verglichen, geändert und gespeichert werden, ohne dass ein direkter Zugriff auf biometrische Hardware oder Proben erfolgt. Der Dienst wird in einem privilegierten SVCHOST-Prozess gehostet. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-camera-frame-server"></a>Windows-Kamera-FrameServer

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | FrameServer |
| **Beschreibung** | Ermöglicht mehreren Clients den Zugriff auf Videoframes von Kameras. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="windows-connection-manager"></a>Windows-Verbindungs-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Wcmsvc |
| **Beschreibung** | Anhand der aktuell auf dem PC verfügbaren Netzwerkkonnektivitätsoptionen wird die Verbindung automatisch hergestellt oder getrennt. Zudem kann die Netzwerkkonnektivität mithilfe von Gruppenrichtlinieneinstellungen verwaltet werden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-defender-network-inspection-service"></a>Windows Defender-Netzwerkinspektionsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WdNisSvc |
| **Beschreibung** | Schützt gegen Eindringversuche bei bekannten und neu erkannten Sicherheitsrisiken von Netzwerkprotokollen. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-defender-service"></a>Windows Defender-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WinDefend |
| **Beschreibung** | Schützt Benutzer vor Schadsoftware und weiterer potenziell unerwünschter Software. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-driver-foundation---user-mode-driver-framework"></a>Windows Driver Foundation – Benutzermodus-Treiberframework

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | wudfsvc |
| **Beschreibung** | Erstellt und verwaltet Benutzermodus-Treiberprozesse. Der Dienst kann nicht beendet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-encryption-provider-host-service"></a>Hostdienst für Windows Encryption Provider

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WEPHOSTSVC |
| **Beschreibung** | Der Hostdienst für Windows Encryption Provider vermittelt Verschlüsselungsfunktionen von Drittanbieter-Verschlüsselungsanbietern an Prozesse, die EAS-Richtlinien bewerten und anwenden müssen. Wenn dieser Dienst beendet wird, sind die EAS-Kompatibilitätsüberprüfungen gefährdet, die von den verbundenen E-Mail-Konten eingerichtet wurden. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-error-reporting-service"></a>Windows-Fehlerberichterstattungsdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WerSvc |
| **Beschreibung** | Ermöglicht die Berichterstattung von Fehlern bei nicht mehr funktionierenden und reagierenden Programmen und das Angeben von Lösungen. Ermöglicht außerdem das Generieren von Protokollen für Diagnose- und Reparaturdienste. Wenn dieser Dienst beendet wird, funktioniert die Fehlerberichterstattung möglicherweise nicht ordnungsgemäß, und die Ergebnisse von Diagnosediensten und Reparaturen werden möglicherweise nicht angezeigt. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Erfasst und sendet Daten zu Abstürzen und zum Hängen, die sowohl von MS als auch von Dritten (ISVs/IHVs) genutzt werden. Die Daten werden zum Diagnostizieren von Fehlern verwendet, die zu Abstürzen führen können. Dies können auch Sicherheitsfehler sein. Wird auch für die Fehlerberichterstattung in Unternehmen benötigt. |



## <a name="windows-event-collector"></a>Windows-Ereignissammlung

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Wecsvc |
| **Beschreibung** | Dieser Dienst verwaltet permanente Abonnements für Ereignisse von Remotequellen, die das WS-Verwaltungsprotokoll unterstützen. Hierzu gehören Windows Vista-Ereignisprotokolle sowie Hardware- und IPMI-fähige Ereignisquellen. Der Dienst speichert weitergeleitete Ereignisse in einem lokalen Ereignisprotokoll. Falls dieser Dienst beendet oder deaktiviert wird, können Ereignisabonnements nicht erstellt und weitergeleitete Ereignisse nicht angenommen werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Erfasst ETW-Ereignisse (z. B. Sicherheitsereignisse) für Verwaltungs- und Diagnosezwecke. Von diesem Dienst sind viele Features und Drittanbietertools abhängig, z. B. Tools für die Sicherheitsüberwachung. |



## <a name="windows-event-log"></a>Windows-Ereignisprotokoll

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | EventLog |
| **Beschreibung** | Dieser Dienst verwaltet Ereignisse und Ereignisprotokolle. Er unterstützt die Protokollierung, die Abfrage und das Abonnement von Ereignissen sowie die Archivierung von Ereignisprotokollen und die Verwaltung von Ereignismetadaten. Er kann Ereignisse im XML- und Nur-Text-Format anzeigen. Durch das Beenden dieses Diensts können die Sicherheit und Zuverlässigkeit des Systems beeinträchtigt werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-firewall"></a>Windows-Firewall

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | MpsSvc |
| **Beschreibung** | Die Windows-Firewall trägt zum Schutz des Computers bei, indem der Zugriff durch nicht autorisierte Benutzer auf den Computer über das Internet bzw. ein Netzwerk verhindert wird. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-font-cache-service"></a>Windows-Dienst für Schriftartencache

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | FontCache |
| **Beschreibung** | Optimiert die Leistung von Anwendungen durch das Speichern häufig verwendeter Schriftartendaten. Dieser Dienst wird von Anwendungen gestartet, wenn er nicht bereits ausgeführt wird. Er kann deaktiviert werden, aber dadurch wird die Leistung von Anwendungen herabgesetzt. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-image-acquisition-wia"></a>Windows-Bilderfassung (WIA)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | stisvc |
| **Beschreibung** | Stellt Bilderfassungsdienste für Scanner und Kameras zur Verfügung. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="windows-insider-service"></a>Windows-Insider-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | wisvc |
| **Beschreibung** | wisvc |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Für Server wird das Test-Flighting nicht unterstützt, sodass darauf kein Vorgang durchgeführt wird. Das Feature kann auch per Gruppenrichtlinie deaktiviert werden. |



## <a name="windows-installer"></a>Windows Installer

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | msiserver |
| **Beschreibung** | Fügt Anwendungen, die als Windows Installer-Paket (*.msi, *.msp) angeboten werden, hinzu bzw. ändert oder entfernt sie. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-license-manager-service"></a>Windows-Lizenz-Manager-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | LicenseManager |
| **Beschreibung** | Stellt Infrastrukturunterstützung für den Microsoft Store bereit. Der Dienst wird bei Bedarf gestartet, und bei einer Deaktivierung verhalten sich im Windows Store erworbene Inhalte nicht ordnungsgemäß. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-management-instrumentation"></a>Windows-Verwaltungsinstrumentation

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | Winmgmt |
| **Beschreibung** | Bietet eine standardmäßige Schnittstelle und ein Objektmodell zum Zugreifen auf Verwaltungsinformationen über das Betriebssystem, Geräte, Anwendungen und Dienste. Die meiste Windows-basierte Software kann nicht ordnungsgemäß ausgeführt werden, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-mobile-hotspot-service"></a>Windows-Dienst für mobile Hotspots

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | icssvc |
| **Beschreibung** | Ermöglicht die Freigabe einer Datenverbindung für ein anderes Gerät. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Keine |



## <a name="windows-modules-installer"></a>Windows Modules Installer

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | TrustedInstaller |
| **Beschreibung** | Ermöglicht das Installieren, Ändern und Entfernen von Windows-Updates und optionalen Komponenten. Wenn dieser Dienst deaktiviert ist, können beim Installieren oder Deinstallieren von Windows-Updates auf diesem Computer Fehler auftreten. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-push-notifications-system-service"></a>Windows-Pushbenachrichtigungssystemdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WpnService |
| **Beschreibung** | Der Dienst wird in Sitzung 0 ausgeführt und hostet die Benachrichtigungsplattform und den Verbindungsanbieter, der die Verbindung zwischen Gerät und WNS-Server behandelt. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Automatisch |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Wird für Live-Kacheln und andere Features benötigt. |



## <a name="windows-push-notifications-user-service"></a>Windows-Pushbenachrichtigungs-Benutzerdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WpnUserService |
| **Beschreibung** | Dieser Dienst hostet die Windows-Benachrichtigungsplattform, die lokale Benachrichtigungen und Pushbenachrichtigungen unterstützt. Unterstützt werden Kachel-, Popup- und unformatierte Benachrichtigungen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung OK |
| **Kommentare** | Benutzerdienstvorlage |



## <a name="windows-remote-management-ws-management"></a>Windows-Remoteverwaltung (WS-Verwaltung)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WinRM |
| **Beschreibung** | Mit dem Windows-Remoteverwaltungsdienst (WinRM) wird das WS-Verwaltungsprotokoll für die Remoteverwaltung implementiert. Die WS-Verwaltung stellt ein Standard-Webdienst-Protokoll dar, das für die Remote-Software- und Hardware-Verwaltung verwendet wird. Der WinRM-Dienst durchsucht das Netzwerk nach WS-Verwaltungsanforderungen und verarbeitet diese. Der WinRM-Dienst muss mit einem „Listener“ unter Verwendung des Befehlszeilenprogramms winrm.cmd oder über die Gruppenrichtlinie konfiguriert werden, um im Netzwerk „lauschen“ zu können. Der WinRM-Dienst stellt einen Zugriff auf WMI-Daten bereit und ermöglicht eine Ereignissammlung. Die Ereignissammlung und das Abonnieren von Ereignissen machen es erforderlich, dass der Dienst ausgeführt wird. WinRM-Nachrichten verwenden HTTP oder HTTPS als Transporte. Der WinRM-Dienst ist nicht von IIS abhängig, er wird jedoch vorkonfiguriert, um auf demselben Computer einen Port mit IIS zu teilen. Der WinRM-Dienst reserviert das URL-Präfix „/wsman“. Um Konflikten mit IIS vorzubeugen, sollten Administratoren sicherstellen, dass keine auf IIS gehostete Website das URL-Präfix „/wsman“ verwendet. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Wird für die Remoteverwaltung benötigt. |



## <a name="windows-search"></a>Windows Search

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WSearch |
| **Beschreibung** | Stellt Inhaltsindizierung, Eigenschaftenzwischenspeicherung und Suchergebnisse für Dateien, E-Mails und andere Inhalte bereit. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Deaktiviert |
| **Empfehlung** | Bereits deaktiviert |
| **Kommentare** | Keine |



## <a name="windows-time"></a>Windows-Zeitdienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | W32Time |
| **Beschreibung** | Behält Datums- und Zeitsynchronisation auf allen Clients und Servern im Netzwerk bei. Wenn dieser Dienst beendet wurde, sind Zeit- und Datumssynchronisierung nicht verfügbar. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="windows-update"></a>Windows-Update

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | wuauserv |
| **Beschreibung** | Erkennung, Download und Installation von Updates für Windows und andere Programme. Wenn der Dienst deaktiviert ist, können „Windows Update“ bzw. das Feature „Automatische Updates“ nicht verwendet werden. Außerdem können Programme dann die Windows Update-Agent-Anwendungsprogrammierschnittstelle (WUA API) nicht verwenden. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="winhttp-web-proxy-auto-discovery-service"></a>WinHTTP-Web Proxy Auto-Discovery-Dienst

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | WinHttpAutoProxySvc |
| **Beschreibung** | WinHTTP implementiert den HTTP-Clientstapel und bietet Entwicklern eine Win32-API und COM-Automatisierungskomponente zum Senden von HTTP-Anforderungen und zum Empfangen von Antworten. Außerdem unterstützt WinHTTP die automatische Erkennung von Proxykonfigurationen über die entsprechende Implementierung des WPAD-Protokolls (Web Proxy Auto-Discovery). |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Nicht deaktivieren |
| **Kommentare** | Alle Elemente, die den Netzwerkstapel nutzen, können über eine funktionale Abhängigkeit von diesem Dienst verfügen. Er wird von vielen Organisationen genutzt, um das Routing von HTTP-Proxys für interne Netzwerke zu konfigurieren. Ohne diesen Dienst tritt für alle HTTP-Internetverbindungen mit internem Ursprung ein Fehler auf. |



## <a name="wired-autoconfig"></a>Automatische Konfiguration (verkabelt)

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | dot3svc |
| **Beschreibung** | Mit dem Dienst für die automatische Konfiguration von Kabelnetzwerken (DOT3SVC) wird eine IEEE 802.1X-Authentifizierung an Ethernet-Schnittstellen ausgeführt. Wenn bei der aktuellen verkabelten Netzwerkbereitstellung die 802.1X-Authentifizierung erzwungen wird, muss der DOT3SVC-Dienst so konfiguriert werden, dass eine Konnektivität auf der 2. Schicht hergestellt bzw. Zugriff auf Netzwerkressourcen ermöglicht wird. Der DOT3SVC-Dienst wirkt sich nicht auf Kabelnetzwerke aus, bei denen die 802.1X-Authentifizierung nicht erzwungen wird. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="wmi-performance-adapter"></a>WMI-Leistungsadapter

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | wmiApSrv |
| **Beschreibung** | Bietet Leistungsbibliotheksinformationen der Windows-Verwaltungsinstrumentationsanbieter für Clients im Netzwerk. Dieser Dienst wird nur ausgeführt, wenn das Leistungsdaten-Hilfsprogramm aktiviert ist. |
| **Installation** | Immer installiert |
| **Starttyp** | Manuell |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="workstation"></a>Arbeitsstation

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | LanmanWorkstation |
| **Beschreibung** | Erstellt und wartet Clientnetzwerkverbindungen mit Remoteservern unter Verwendung des SMB-Protokolls. Diese Verbindungen sind nicht mehr verfügbar, falls dieser Dienst beendet wird. Wenn dieser Dienst deaktiviert ist, können alle Dienste, die explizit davon abhängen, nicht gestartet werden. |
| **Installation** | Immer installiert |
| **Starttyp** | Automatisch |
| **Empfehlung** | Kein Hinweis |
| **Kommentare** | Keine |



## <a name="xbox-live-auth-manager"></a>Xbox Live Authentifizierungs-Manager

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | XblAuthManager |
| **Beschreibung** | Stellt Authentifizierungs- und Autorisierungsservices für Xbox Live bereit. Wenn dieser Dienst beendet wird, funktionieren einige Anwendungen möglicherweise nicht korrekt. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung empfohlen |
| **Kommentare** | Keine |



## <a name="xbox-live-game-save"></a>Xbox Live-Spiele speichern

| Name | BESCHREIBUNG |
|--|--|
| **Dienstname** | XblGameSave |
| **Beschreibung** | Dieser Dienst synchronisiert für Xbox Live-Spiele gespeicherte Daten. Wenn der Dienst beendet wird, werden die gespeicherten Spieldaten für Xbox Live nicht hochgeladen bzw. heruntergeladen. |
| **Installation** | Nur mit Desktopdarstellung |
| **Starttyp** | Manuell |
| **Empfehlung** | Deaktivierung empfohlen |
| **Kommentare** | Dieser Dienst synchronisiert für Xbox Live-Spiele gespeicherte Daten. Wenn der Dienst beendet wird, werden die gespeicherten Spieldaten für Xbox Live nicht hochgeladen bzw. heruntergeladen. |
