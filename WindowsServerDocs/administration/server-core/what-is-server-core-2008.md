---
title: Was ist Server Core 2008?
description: Erfahren Sie mehr über die Server Core-Installationsoption in Windows Server 2008
ms.prod: windows-server-threshold
ms.author: helohr
ms.date: 11/01/2017
ms.topic: article
author: Heidilohr
ms.openlocfilehash: c1ef71dbc589cfdeac63b46d720c4bdd0a44dbaa
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59815401"
---
#<a name="what-is-server-core-2008"></a>Was ist Server Core 2008?
>Gilt für: WindowsServer 2008

>[!NOTE]
>Diese Informationen gelten für Windows Server 2008. Weitere Informationen zu Server Core unter Windows Server, finden Sie unter [Was ist, dass die Server Core-Installation unter Windows Server](https://docs.microsoft.com/windows-server/administration/server-core/what-is-server-core). 

Die Server Core-Option wird eine neue Minimalinstallation-Option, die verfügbar ist, wenn Sie die Standard, Enterprise oder Datacenter Edition von Windows Server 2008 bereitstellen. Server Core bietet Ihnen eine Minimalinstallation von Windows Server 2008, die unterstützt die Installation nur für bestimmte Serverrollen, wie weiter unten in diesem Kapitel beschrieben. Vergleichen Sie dies mit der vollständigen Installationsoption für Windows Server 2008, die unterstützt wird, installieren alle verfügbaren Serverrollen und andere Microsoft oder Drittanbieter-serveranwendungen wie Microsoft Exchange Server oder SAP. 

Bevor wir fortfahren, muss der Ausdruck "Installationsoption" erläutert. Wenn Sie eine Kopie von Windows Server 2008 erwerben, kaufen Sie normalerweise eine Lizenz zur Nutzung von bestimmten Editionen oder die Stock Keeping-Einheiten (SKUs). Tabelle 1: 1 listet die verschiedenen Editionen von Windows Server 2008, die verfügbar sind. Die Tabelle gibt auch an, welche Installationsoptionen (vollständig, Server Core oder beides) für jede Edition verfügbar sind.

**Tabelle 1: 1** Windows Server 2008-Editionen und deren Unterstützung für die Installationsoptionen
| Edition       | Vollständig          | Server Core  |
| ------------- | :-------------: | :------------: |
| Windows Server 2008 Standard (X86- und X64)       | X | X        |
| Windows Server 2008 Enterprise (X86- und X64)       | X | X        |
| Windows Server 2008 Datacenter (X86- und X64)        | X | X       |
| Windows Web Server 2008 (X86- und X64)       | X | X  |
| Windows Server 2008 für Itanium-basierte Systeme       | X |     |
| Windows HPC Server 2008 (nur X64)       | X |   |
| Windows Server 2008 Standard ohne Hyper-V (X86- und X64) | X | X |
| Windows Server 2008 Enterprise ohne Hyper-V (X86- und X64)  | X | X |
| Windows Server 2008 Standard ohne Hyper-V (X86- und X64) | X | X |

Um zu verstehen, was eine "Installationsoption ist", nehmen wir an, dass Sie eine Volumenlizenz erworben haben, in dem Sie eine Kopie von Windows Server 2008 Enterprise Edition installieren können. Beim Einfügen von Ihrem volumenlizenzierte Medieninhalts in einem System und beginnen, wie in Abbildung 1 – 1 dargestellt, während des Installationsvorgangs eine Bildschirme, die Sie sehen, bietet Ihnen die Wahl zwischen verschiedenen Editionen und Installationsoptionen.

![Wählen eine Server Core-Installationsoption installiert](../media/what-is-server-core-2008/FIg1-1.png)

**Abbildung 1-1** eine Server Core-Installationsoption installiert auswählen

In Abbildung 1 – 1, Ihre Volumenlizenzen (oder Product Key für Einzelhandelsmedien) bietet Ihnen zwei Installationsoptionen, Sie zwischen können: die zweite Option (eine vollständige Installation von Windows Server 2008 Enterprise) und die fünfte Option (eine Server Core-Installation von Windows Server 2008 Enterprise), der zweiten Option ausgewählt, die in diesem Beispiel. 

##<a name="full-vs-server-core"></a>Vollständige Visual Studio. Server Core 
Seit den Anfängen der Microsoft Windows-Plattform, Windows Server wurden im Prinzip "Alles" Servern, die alle Arten von Funktionen enthalten, von denen einige möglicherweise nie in Ihrer Netzwerkumgebung Verwendung. Z. B. bei der Installation von Windows Server 2003 auf einem System wurden die Binärdateien für den Routing- und RAS-Dienst (RRAS) auf dem Server installiert, auch wenn Sie keine Notwendigkeit für diesen Dienst mussten (auch wenn immer noch mussten Sie konfigurieren und Aktivieren von RRAS, bevor sie funktionieren würde). Windows Server 2008 verbessert die frühere Versionen durch Installieren der Binärdateien, die von einer Serverrolle nur erforderlich, wenn Sie dieser spezifischen Rolle auf dem Server installieren möchten. Die vollständige Installationsoption von Windows Server 2008 installiert jedoch noch viele Dienste und andere Komponenten, die für ein bestimmtes Einsatzszenario zugängig häufig nicht erforderlich sind. 

Dies ist der Grund, die Microsoft-erstellt eine zweite Installationsoption – Server Core – für Windows Server 2008: um zu vermeiden, alle Dienste und andere Funktionen, die nicht wichtig sind, für die Unterstützung bestimmter Serverrollen häufig verwendet wird. Beispielsweise kein Domain Name System (DNS)-Server nicht unbedingt darauf installiert werden, da Sie aus einem DNS-Server aus Sicherheitsgründen das Web durchsuchen möchten, wäre nicht von Windows Internet Explorer. Und ein DNS-Server nicht einmal eine grafische Benutzeroberfläche (GUI), da Sie fast alle Aspekte von DNS verwalten können entweder über die Befehlszeile mit dem leistungsfähigen Dnscmd.exe-Befehl aus, oder Remote mithilfe der DNS-Microsoft Management Console (MMC)-Snap-in.

Um dies zu vermeiden, Microsoft entschieden, um alles von Windows Server 2008 zu entfernen, die nicht unbedingt für die Ausführung von Core-Netzwerkdienste wie Active Directory Domain Services (AD DS), DNS, Dynamic Host Configuration-Protokoll (DHCP), Datei, und drucken, war und ein Einige andere Serverrollen. Das Ergebnis ist der neue Server Core-Installationsoption, die verwendet werden kann, um einen Server zu erstellen, der nur eine begrenzte Anzahl von Rollen und Features unterstützt. 

##<a name="the-server-core-gui"></a>Der Server Core-GUI
Wenn Sie fertig sind, installieren Server Core zum ersten Mal auf einem System und anmelden, haben Sie für etwas überrascht. Abbildung 1-2 zeigt die Server Core-Benutzeroberfläche nach der ersten Anmeldung an.

![Server Core-Benutzeroberfläche](../media/what-is-server-core-2008/Fig1-2.png)

**Abbildung 1 – 2** Server Core-Benutzeroberfläche

Es gibt keine Desktop! Es ist, also keine Windows-Explorer-Shell, mit dessen Menü "Start", Taskleiste und anderen Features, die Sie anzeigen möchten, verwendet werden können. Sie müssen lediglich eine Eingabeaufforderung, was bedeutet, dass die meisten Aufgaben der Konfiguration einer Server Core-Installations möchten entweder durch Eingabe von Befehlen, die einem an einem bestimmten Zeitpunkt langsam ist, oder mit Skripts und Batchdateien, kann nützlich sein, zu beschleunigen und vereinfachen Ihre Configurati ist auf diese Automatisierung von Aufgaben. Sie können auch einige Aufgaben zur Erstkonfiguration mithilfe von Antwortdateien, bei der Durchführung einer unbeaufsichtigten Installations von Server Core ausführen. 

Konfigurieren und Verwalten von Server Core-Installation können für Administratoren, die mithilfe von Befehlszeilentools wie Netsh.exe, Dfscmd.exe und Dnscmd.exe Experten sind, einfache und sogar unterhaltsam sein. Für diejenigen, die keine Experten sind, jedoch ist nicht alles verloren. Sie können weiterhin die standardmäßigen Windows Server 2008-MMC-Tools verwenden, für die Verwaltung einer Server Core-Installations. Sie müssen lediglich diese auf einem anderen System ausgeführt wird entweder eine vollständige Installation von Windows Server 2008 oder Windows Vista mit Service Pack 1 verwenden. 

Sie erfahren mehr zum Konfigurieren und Verwalten von Server Core-Installationen in Kapitel 3 bis 6 dieses Buchs, beim Verwalten von bestimmten Serverrollen und andere Komponenten spätere Kapitel behandeln. Weitere Informationen zu den verschiedenen Windows-Befehlszeilentools und deren Verwendung, gibt es zwei gute Ressourcen zurate ziehen, um:
* Die Befehlsreferenz-Abschnitt der technischen Bibliothek zu Windows Server 2008) 
* *Die Windows Befehlszeilen Administrator's Pocket Consultant* von William (Microsoft Press, 2008) 

Tabelle 1 – 2 listet die wichtigsten GUI-Anwendungen, zusammen mit ihrer ausführbaren Dateien, die in einer Server Core-Installation verfügbar sind.

**Tabelle 1 – 2** GUI-Anwendungen, die in einer Server Core-Installation verfügbar
| GUI-Anwendung | Ausführbare Datei mit dem Pfad |
| -------------   | -------------       | 
| Eingabeaufforderung | %WINDIR%\System32\Cmd.exe |
| Microsoft-Support-Diagnosetool | %WINDIR%\System32\MSdt.exe |
| Editor | %WINDIR%\System32\Notepad.exe |
| Registrierungs-editor | %WINDIR%\System32\Regedt32.exe |
| Systeminformationen | %WINDIR%\System32\MSinfo32.exe |
| Task-Manager | %WINDIR%\System32\Taskmgr.exe |
| Windows Installer | %WINDIR%\System32\MSiexec.exe |

Das ist eine sehr kurze Liste! Hier ist jetzt eine Liste der Elemente der Benutzeroberfläche, die nicht in Server Core enthalten sind:
* Der Windows-Explorer-desktop-Shell (Explorer.exe) und unterstützenden Funktionen wie z. B. Designs 
* Alle MMC-Konsolen 
* Alle Systemsteuerung-Hilfsprogramme, mit Ausnahme von Regions-und Sprachoptionen ("Intl.cpl") und das Datum und Uhrzeit ("timedate.cpl") 
* Alle Hypertext Markup Language (HTML) Rendering-Engines, einschließlich Internet Explorer und HTML-Hilfe 
* Windows Mail 
* Windows Media Player 
* Die meisten Zubehör wie Paint, Rechner und Wordpad

.NET Framework ist auch nicht in Server Core, was bedeutet, dass es gibt keine Unterstützung für die Ausführung von verwaltetem Code auf einer Server Core-Installation vorhanden. Nur systemeigenen Code – Code geschrieben wurde, mit Windows Application programming Interfaces (APIs), können auf Server Core ausgeführt werden. Zusammenfassend alle GUI-Anwendungen, die auf .NET Framework abhängig sind, oder klicken Sie auf die Explorer.exe nicht Shell unter Server Core ausgeführt. 

>[!NOTE]
>Da Windows PowerShell auf .NET Framework erforderlich ist, wird Sie nicht Windows PowerShell auf Server Core installieren. Sie können jedoch verwalten eine Server Core-Installation Remote mithilfe von Windows PowerShell, sofern Sie nur die PowerShell-WMI-Befehle verwenden.

##<a name="supported-server-roles"></a>Unterstützte Serverrollen 
Server Core-Installation umfasst nur eine begrenzte Anzahl von Serverrollen, die im Vergleich zu einer vollständigen Installation von Windows Server 2008. Tabelle 1 bis 3 vergleicht die Rollen für vollständige Installation und Server Core-Installationen von Windows Server 2008 Enterprise Edition verfügbar sind. 

**Tabelle 1 bis 3** Vergleich von Serverrollen für vollständige Installation und Server Core-Installationen von Windows Server 2008 Enterprise Edition
| Serverrolle  | In der Vollversion verfügbar  | In Server Core verfügbar  |
| ------------- | :-------------: | :------------: |
| Active Directory-Zertifikatdienste (AD CS)  | X |  |
| Active Directory-Domänendienste (AD DS)  | X  | X |
| Active Directory-Verbunddienste (Active Directory Federation Services, AD FS)  | X  |  |
| Active Directory Lightweight Directory Services (ADLDS)  | X  | X |
| Active Directory-Rechteverwaltungsdienste (Active Directory Rights Management Services, AD RMS)  | X  |  |
| Anwendungsserver  | X  |  |
| DHCP-Server  | X  | X |
| DNS-Server  | X  | X |
| Faxserver  | X  |  |
| Dateidienste  | X  | X |
| Hyper-V  | X | X |
| Network Policy and Access Services  | X  |  |
| Druckdienste  | X  | X |
| Streaming Media-Dienste  | X  | X |
| Terminaldienste  | X  |  |
| UDDI-Dienste  | X  |  |
| Webserver (IIS) | X | X |
| Windows-Bereitstellungsdienste  | X |  |

Zwar die Rollen für Server Core verfügbar sind in der Regel unabhängig von der Architektur (X86 oder X64) und die Produktversion aus, gibt es jedoch einige Ausnahmen:
* Die Rolle Hyper-V (Virtualisierung) ist nur verfügbar, wenn Sie Windows Server 2008 mit Hyper-V-Produktmedien erworben (Hyper-V steht nur für X64 Versionen). Wenn Sie nicht über diese Rolle benötigen, können Sie stattdessen Windows Server 2008 ohne Hyper-V-Produktmedien erwerben. 
* Die Rolle "Dateidienste" auf Standard Edition ist auf einem eigenständigen (Distributed File System, DFS)-Stamm und Cross-File Replication (DFS-R) wird nicht unterstützt. 
* Bevor Sie die Streaming-Media Services-Rolle auf Server Core installieren können, müssen Sie aus dem Microsoft Download Center herunterladen und installieren das entsprechende Microsoft eigenständige Updatepaket (MSU-Datei) für Ihr Server Architektur (X86 oder X64).
* Die Rolle Webserver (IIS) wird ASP.NET nicht unterstützt. Dies ist, da .NET Framework unter Server Core, wodurch eingeschränkt, was Sie tun können, mit einem Server Core-Web-Server, nicht unterstützt wird. 

##<a name="supported-optional-features"></a>Unterstützt optionalen features
Server Core-Installation unterstützt auch nur eine begrenzte Teilmenge der verfügbaren Funktionen auf einer vollständigen Installation von Windows Server 2008. Tabelle 1 – 4 vergleicht die Funktionen, die für die vollständige Installation und Server Core-Installationen von Windows Server 2008 Enterprise Edition verfügbar.

**Tabelle 1 – 4** Vergleich der Funktionen für vollständige Installation und Server Core-Installationen von Windows Server 2008 Enterprise Edition

| Feature  | In der Vollversion verfügbar  | In Server Core verfügbar  |
| ------------- | :-------------: | :------------: |
| .NET Framework 3.0-Features  | X  |  |
| BitLocker-Laufwerkverschlüsselung  | X  | X |
| BITS-Servererweiterungen  | X  |  |
| Verbindungs-Manager-Verwaltungskit  | X |  |
| Desktopdarstellung  | X |  |
| Failoverclustering  | X  | X |
| Gruppenrichtlinienverwaltung  | X  |  |
| Internetdruckclient  | X  |  |
| Internet Storage Namenserver  | X  |  |
| LPR-Portüberwachung  | X  |  |
| Message Queuing  | X  |  |
| Multipfad-e/a  | X  | X |
| Netzwerklastenausgleich  | X  | X |
| Peer Name Resolution-Protokoll  | X  |  |
| Verbessertes Audio-/Videostreaming unter Windows  | X |  |
| Remoteunterstützung  | X  |  |
| RDC (Remote Differential Compression) | X  |  |
| Remoteserver-Verwaltungstools  | X  |  |
| Wechselmedien-Manager | X  | X |
| RPC-über-HTTP-Proxy | X  |  |
| Einfache TCP/IP-Dienste  | X  |  |
| SMTP-Server  | X  |  |
| SMNP-Dienste  | X  | X  |
| Speicher-Manager für SANs  | X  |  |
| Subsystem für UNIX-basierte Anwendungen | X | X  |
| Telnet-Client  | X | X  |
| Telnet-Server  | X   |  |
| TFTP-Client  | X   |  |
| Interne Windows-Datenbank  | X  |  |
| Windows PowerShell  | X  |  |
| Aktivierungsdienst für Windows-Produkt  | X   |  |
| Windows Server-Sicherungsfeatures  | X  | X  |
| Windows-Systemressourcen-Manager  | X  |  |
| WINS-Server  | X | X |
| WLAN-Dienst | X  |  |

In diesem Fall sind einige Punkte müssen Sie wissen, zu die Funktionen, die auf Server Core verfügbar:
* Einige Features erfordern möglicherweise besondere Hardware funktionieren ordnungsgemäß (oder überhaupt) auf Server Core. Zu diesen Funktionen gehören die BitLocker-Laufwerkverschlüsselung, Failover-Clusterunterstützung, Multipfad-e/a, Netzwerklastenausgleich und Wechselmedien. 
* Es ist nicht verfügbar in Standard Edition, Failover-Clusterunterstützung.

##<a name="server-core-architecture"></a>Server Core-Architektur
Genauerer Blick auf Server Core, kurz betrachten wir die Architektur von Server Core-Installationen von Windows Server 2008 durch einen Vergleich mit der eine vollständige Installation. Zuerst Denken Sie daran, dass Server Core keine andere Version von Windows Server 2008 jedoch einfach eine Installationsoption, die Sie auswählen können, bei der Installation von Windows Server 2008 auf einem System ist. Dies impliziert Folgendes:
* Der Kernel auf einer Server Core-Installation ist der gleiche finden Sie auf eine vollständige Installation von der gleichen Hardware-Architektur (X86 oder X64) und die Edition. 
* Wenn eine Binärdatei auf einer Server Core-Installation vorhanden ist, hat eine vollständige Installation von die gleiche Hardware-Architektur (X86 oder X64) und die Edition die gleiche Version von dieser bestimmten Binärdatei (mit zwei Ausnahmen, die weiter unten erläutert). 
* Wenn eine bestimmte Einstellung (z. B. eine bestimmte Firewall-Ausnahme oder der Starttyp des einen bestimmten Dienst) eine bestimmte Standardkonfiguration auf einer Server Core-Installation verfügt, wird genau die gleiche Weise auf eine Vollversion des gleichen diese Einstellung konfiguriert werden. Hardware-Architektur (X86 oder X64) "und" Edition ".

Abbildung 1 – 3 zeigt eine vereinfachte Ansicht der Architektur von einer vollständigen Installation und Server Core-Installationen von Windows Server 2008. Die gepunktete Linie gibt die Architektur von Server Core, während das gesamte Diagramm, die Architektur einer vollständigen Installation darstellt an. 

Das Diagramm veranschaulicht die modulare Architektur von Windows Server 2008 mit Server Core, die auf eine Teilmenge der die Kernfunktionen des Betriebssystems erstellt wird. Für die gleiche Hardware-Architektur und die Edition ist jede Datei, die auf eine Neuinstallation von Server Core vorhanden, auch auf eine Vollversion, mit Ausnahme von zwei spezielle Dateien (Scregedit.wsf und Oclist.exe), die nur auf Server Core vorhanden sind. Diese speziellen Dateien enthalten waren auf Server Core, um die erste Konfiguration von einer Server Core-Installation und das Hinzufügen oder Entfernen von Rollen und optionalen Komponenten zu vereinfachen. 

![Die Architekturen von Server Core und die vollständige Installation](../media/what-is-server-core-2008/Fig1-3.png)

**Abbildung 1 – 3** die Architekturen von Server Core und die vollständige Installation

##<a name="driver-support"></a>Treiberunterstützung
Architekturdiagramm von Server Core, dargestellt in Abbildung 1 – 3 ist natürlich vereinfacht. eine Sache, die es nicht angezeigt, ist der Unterschied bei der treiberunterstützung Gerät zwischen Server Core und vollständige Installationen. Eine vollständige Installation von Windows Server 2008 enthält Tausende von in-Box-Treiber für verschiedene Arten von Geräten, die Ihnen ermöglichen, installieren Sie Produkte auf einer Vielzahl von verschiedenen Hardwarekonfigurationen. (Client-Betriebssystemen wie Windows Vista enthalten noch mehr Treiber zur Unterstützung von Geräten, z. B. Digitalkameras und Scanner, die normalerweise nicht mit Servern verwendet werden.) 

Wenn ein neues Gerät verbunden ist (oder im installiert) eine vollständige Installation von Windows Server 2008, das Subsystem Plug & Play (PnP) überprüft zuerst, ob ein in-Box-Treiber für das Gerät vorhanden ist. Wenn ein kompatibler mitgelieferten Treiber gefunden wird, an das Plug & Play-Subsystem automatisch installiert, der Treiber und das Gerät und arbeitet. Auf einer vollständigen Installation von Windows Server 2008 kann eine Popup-Sprechblase angezeigt werden, der angibt, dass der Treiber installiert wurde und das Gerät für die Verwendung bereit ist. 

Auf einer Server Core-Installation ist der Installationsvorgang Treiber identisch (die Plug & Play-Subsystem unter Server Core vorhanden ist) mit beiden Qualifikationen. Server Core enthält zunächst nur eine minimale Anzahl von in-Box-Treibern und nur für die folgenden Arten von Geräten:
* Eine Video-Graphics-Array (VGA) Standardtreiber 
* Treiber für Speichergeräte 
* Treiber für Netzwerkadapter

Beachten Sie, dass für jeden der drei Gerätekategorien, die hier gezeigten, Server Core die gleichen mitgelieferten Treiber enthält, die für eine entsprechende vollständige Installation (für die gleiche Hardwarearchitektur) gefunden werden. 

Auch bei den PnP-Subsystem ein Treibers für ein neues Gerät automatisch installiert wird, dies erfolgt automatisch – keine Popups Sprechblase angezeigt wird. Warum nicht? Da keine grafische Benutzeroberfläche auf Server Core ist ist keine Taskleiste, es gibt also keine Infobereich der Taskleiste auf der Taskleiste! 

Was also können Sie tun, wenn Sie eine Server Core-Installation der Rolle "Druckdienste" hinzu, und Sie einen Drucker installieren möchten? Sie fügen den Druckertreiber manuell hinzu, auf dem Server, Serverkern hat keine in-Box-Druckertreiber.

##<a name="service-footprint"></a>Dienst-Speicherbedarf
Da es sich bei Server Core über eine minimale Installation handelt, hat er einen Geringerer Speicherbedarf Dienst als eine entsprechende vollständige Installation von der gleichen Hardware-Architektur und die Edition. Ungefähr 75 Systemdienste werden z. B. auf einer vollständigen Installation von Windows Server 2008 standardmäßig installiert der ungefähr 50 für den automatischen Start konfiguriert sind. Server Core weist im Gegensatz dazu nur etwa 70 Dienste, die automatisch installiert, standardmäßig und weniger als 40 diese Start auf. 

Tabelle 1 bis 5 werden die Dienste aufgeführt, die auf einer Server Core-Installation mit den Startmodus für standardmäßig installiert sind und Konto, die vom jeweiligen Dienst verwendet.

**Tabelle 1 – 5** Systemdienste, die standardmäßig unter Server Core installiert werden

| Dienstname  | Anzeigename  | Startmodus  | Konto  |
| ------------- | ------------- | ------------ | ------------ |
| AeLookupSvc  | Anwendungskomfort  | Auto | LocalSystem |
| AppMgmt  | Anwendungsverwaltung  | Manual | LocalSystem |
| BFE | Basis-Engine-Filterung  | Auto | LocalService |
| BITS | Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)  | Auto | LocalSystem |
| Browser | Computer-Browser  | Manual | LocalSystem |
| CertPropSvc | Zertifikat-Verteilung  | Manual | LocalSystem |
| COMSysApp  | COM+-Anwendung  | Manual | LocalSystem |
| CryptSvc  | Kryptografische Dienste  | Auto | Netzwerk-Dienst |
| DcomLaunch  | DCOM-Prozess-Startprogramm  | Auto | LocalSystem |
| Dhcp  | DHCP-Client  | Auto | LocalService |
| DnsCache | DNS-Client  | Auto | Netzwerk-Dienst |
| DPS  | Diagnostic Policy-Dienst  | Auto | LocalService |
| Ereignisprotokoll | Windows-Ereignisprotokoll  | Auto | LocalService |
| EventSystem  | COM+-Ereignissystem  | Auto | LocalService |
| FCRegSvc  | Microsoft Fibre Channel-Plattform-Geräteregistrierungsdienst  | Manual | LocalService |
| gpsvc  | Gruppenrichtlinienclient  | Auto | LocalSystem |
| hidserv | Zugriff auf Eingabegeräte  | Manual | LocalSystem |
| hkmsvc  | Integritätsdienst-Schlüssel und Zertifikate verwalten  | Manual | LocalSystem |
| IKEEXT  | IKE- und AuthIP IPsec-Schlüsselerstellungsmodule  | Auto | LocalSystem |
| iphlpsvc  | IP-Hilfsprogramm  | Auto | LocalSystem |
| KeyIso | CNG-Schlüssel-Isolation  | Manual | LocalSystem |
| KtmRm  | KtmRm für Distributed Transaction Coordinator  | Auto | Netzwerk-Dienst |
| LanmanServer  | Server  | Auto | LocalSystem |
| LanmanWorkstation  | Workstatione  | Auto | LocalService |
| lltdsvc  | Zuordnung für Verbindungsschicht-Topologie  | Manual | LocalService |
| lmhosts  | TCP/IP-NetBIOS-Hilfsprogramm  | Auto | LocalService |
| MpsSvc  | Windows-Firewall  | Auto | LocalService |
| MSDTC  | Distributed Transaction Coordinator  | Auto | Netzwerk-Dienst |
| MSiSCSI  | Microsoft iSCSI-Initiator-Dienst  | Manual | LocalSystem |
| MSIServer  | Windows Installer  | Manual | LocalSystem |
| napagent  | Netzwerkzugriffsschutz-Agent  | Manual | Netzwerk-Dienst |
| Netlogon  | Netlogon  | Manual | LocalSystem |
| netprofm  | Netzwerklistendienst  | Auto | LocalService |
| NlaSvc  | Network Location Awareness  | Auto | Netzwerk-Dienst |
| nsi  | Network Store Interface-Dienst  | Auto | LocalService |
| PLA  | Leistungsprotokolle und Warnungen  | Manual | LocalService |
| PlugPlay  | Plug & Play  | Auto | LocalSystem |
| PolicyAgent  | IPsec-Richtlinien-Agent  | Auto | Netzwerk-Dienst |
| ProfSvc  | Benutzerprofildienst  | Auto | LocalSystem |
| ProtectedStorage  | Geschützten Speicher  | Manual | LocalSystem |
| RemoteRegistry  | Remoteregistrierung  | Auto | LocalService |
| RpcSs  | Remoteprozeduraufruf (RPC)  | Auto | Netzwerk-Dienst |
| RSoPProv | Richtlinienergebnissatz-Richtlinienanbieter  | Manual | LocalSystem |
| Sacsvr  | Hilfsprogramm für spezielle Verwaltungskonsole  | Manual | LocalSystem |
| SamSs  | Sicherheitskonten-Manager  | Auto | LocalSystem |
| SCardSvr | Smartcard  | Manual | LocalService |
| Zeitplan | Aufgabenplanung  | Auto | LocalSystem |
| SCPolicySvc | Entfernen des Smartcard-Richtlinie  | Manual | LocalSystem |
| Seclogon | Sekundäre Anmeldung  | Auto | LocalSystem |
| SENS | Benachrichtigungsdienst für Systemereignisse  | Auto | LocalSystem |
| SessionEnv | Terminaldienstekonfiguration  | Manual | LocalSystem |
| slsvc  | Softwarelizenzierung | Auto | Netzwerk-Dienst |
| SNMPTRAP  | SNMP-Trap  | Manual | LocalService |
| swprv  | Microsoft Software Schattenkopieanbieter | Manual | LocalSystem |
| TBS | TPM-Basisdienste  | Manual | LocalService |
| TermService  | Terminaldienste | Auto | Netzwerk-Dienst |
| TrustedInstaller | Windows-Modulinstallation  | Auto | LocalSystem |
| UmRdpService | Anschlussumleitung für Terminaldienst-Redirector  | Manual | LocalSystem |
| vds | Virtuelles Laufwerk  | Manual | LocalSystem |
| VSS | Volumeschattenkopie-Dienst  | Manual | LocalSystem |
| W32Time | Windows-Zeitdienst  | Auto | LocalService |
| WcsPlugInService  | Windows-Farbsystem  | Manual | LocalService |
| WdiServiceHost  | Diagnose-Diensthost  | Manual | LocalService |
| WdiSystemHost  | Diagnosesystem-Host  | Manual | LocalSystem |
| Wecsvc | Windows-Ereignissammlung  | Manual | Netzwerk-Dienst |
| WinHttpAuto-ProxySvc  | WinHTTP-Web Proxy Auto-Discovery-Dienst  | Auto | LocalService |
| Winmgmt | Windows-Verwaltungsinstrumentation | Auto | LocalSystem |
| WinRM  | Windows-Remoteverwaltung (WS-Management) | Auto | Netzwerk-Dienst |
| wmiApSrv  | WMI-Leistungsadapter  | Manual | LocalSystem |
| wuauserv | Windows Update | Auto | LocalSystem |