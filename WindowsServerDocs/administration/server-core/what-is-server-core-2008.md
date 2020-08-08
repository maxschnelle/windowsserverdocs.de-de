---
title: Was ist Server Core 2008?
description: Weitere Informationen zur Server Core-Installationsoption in Windows Server 2008
ms.author: helohr
ms.date: 11/01/2017
ms.topic: article
author: heidilohr
ms.openlocfilehash: fb3e0b60787cb12c3401a14a54aebf4809c61b45
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87993227"
---
# <a name="what-is-server-core-2008"></a>Was ist Server Core 2008?
>Gilt für: Windows Server 2008

>[!NOTE]
>Diese Informationen gelten für Windows Server 2008. Weitere Informationen zu Server Core in Windows Server finden Sie unter [Was ist die Server Core-Installation in Windows Server](./what-is-server-core.md).

Bei der Server Core-Option handelt es sich um eine neue minimale Installationsoption, die verfügbar ist, wenn Sie die Standard Edition, Enterprise oder Datacenter Edition von Windows Server 2008 bereitstellen. Server Core bietet eine minimale Installation von Windows Server 2008, die die Installation bestimmter Server Rollen unterstützt, wie weiter unten in diesem Kapitel beschrieben. Vergleichen Sie dies mit der vollständigen Installationsoption für Windows Server 2008, die die Installation aller verfügbaren Server Rollen sowie anderer Microsoft-oder Drittanbieter-Server Anwendungen wie Microsoft Exchange Server oder SAP unterstützt.

Bevor wir fortfahren, muss der Begriff "Installationsoption" erläutert werden. Wenn Sie eine Kopie von Windows Server 2008 erwerben, erwerben Sie normalerweise eine Lizenz zur Verwendung bestimmter Editionen oder Stock-Keeping Units (SKUs). In Tabelle 1-1 sind die verschiedenen verfügbaren Editionen von Windows Server 2008 aufgeführt. Die Tabelle gibt auch an, welche Installationsoptionen (Full, Server Core oder beides) für jede Edition verfügbar sind.

**Tabelle 1-1** Windows Server 2008-Editionen und deren Unterstützung für Installationsoptionen

| Edition       | Vollständig          | Server Core  |
| ------------- | :-------------: | :------------: |
| Windows Server 2008 Standard (x86 und x64)       | X | X        |
| Windows Server 2008 Enterprise (x86 und x64)       | X | X        |
| Windows Server 2008 Datacenter (x86 und x64)        | X | X       |
| Windows-Webserver 2008 (x86 und x64)       | X | X  |
| Windows Server 2008 für Itanium-basierte Systeme       | X |     |
| Windows HPC Server 2008 (nur x64)       | X |   |
| Windows Server 2008 Standard ohne Hyper-V (x86 und x64) | X | X |
| Windows Server 2008 Enterprise ohne Hyper-V (x86 und x64)  | X | X |
| Windows Server 2008 Standard ohne Hyper-V (x86 und x64) | X | X |

Um zu verstehen, was eine "Installationsoption" ist, nehmen wir an, dass Sie eine Volumenlizenz erworben haben, mit der Sie eine Kopie von Windows Server 2008 Enterprise Edition installieren können. Wenn Sie Ihre Volumen lizenzierten Medien in ein System einfügen und den Installationsvorgang starten, können Sie auf einem der angezeigten Bildschirme, wie in Abbildung 1-1 dargestellt, Editionen und Installationsoptionen auswählen.

![Auswählen einer Server Core-Installationsoption für die Installation](../media/what-is-server-core-2008/FIg1-1.png)

**Abbildung 1-1** Auswählen einer Server Core-Installationsoption für die Installation

In Abbildung 1-1 bietet Ihre Volumenlizenz (oder Product Key für Einzelhandels Medien) zwei Installationsoptionen, zwischen denen Sie wählen können: die zweite Option (eine vollständige Installation von Windows Server 2008 Enterprise) und die fünfte Option (eine Server Core-Installation von Windows Server 2008 Enterprise) mit der in diesem Beispiel ausgewählten.

## <a name="full-vs-server-core"></a>Vollständig im Vergleich zu Server Core
Seit den frühen Tagen der Microsoft Windows-Plattform waren Windows-Server im wesentlichen "alles"-Server, die alle Arten von Features enthielt, von denen Sie in Ihrer Netzwerkumgebung möglicherweise nie tatsächlich verwendet werden. Wenn Sie z. b. Windows Server 2003 auf einem System installiert haben, wurden die Binärdateien für den Routing-und RAS-Dienst (RRAS) auf dem Server installiert, auch wenn Sie diesen Dienst nicht benötigen (obwohl Sie weiterhin RRAS konfigurieren müssen, bevor dies funktioniert). Windows Server 2008 verbessert frühere Versionen, indem die von einer Server Rolle benötigten Binärdateien nur installiert werden, wenn Sie diese Rolle auf dem Server installieren. Bei der vollständigen Installation von Windows Server 2008 werden jedoch weiterhin viele Dienste und andere Komponenten installiert, die für ein bestimmtes Verwendungs Szenario häufig nicht benötigt werden.

Dies ist der Grund, warum Microsoft eine zweite Installationsoption – Server Core – für Windows Server 2008 erstellt hat:, um Dienste und andere Features zu eliminieren, die für die Unterstützung bestimmter häufig verwendeter Server Rollen nicht von wesentlicher Bedeutung sind. Beispielsweise muss auf einem Domain Name System (DNS)-Server nicht Windows Internet Explorer installiert sein, da Sie aus Sicherheitsgründen nicht das Web von einem DNS-Server durchsuchen möchten. Und ein DNS-Server benötigt nicht einmal eine grafische Benutzeroberfläche (GUI), da Sie praktisch alle DNS-Aspekte über die Befehlszeile verwalten können, indem Sie den leistungsfähigen Dnscmd.exe Befehl verwenden, oder Sie verwenden das DNS Microsoft Management Console (MMC)-Snap-in.

Um dies zu vermeiden, entschied sich Microsoft, alles aus Windows Server 2008 zu entfernen, das nicht unbedingt für die Ausführung von Kern Netzwerkdiensten wie Active Directory Domain Services (AD DS), DNS, DHCP (Dynamic Host Configuration Protocol), Datei-und Druckfunktionen und einigen anderen Server Rollen erforderlich war. Das Ergebnis ist die neue Server Core-Installationsoption, die zum Erstellen eines Servers verwendet werden kann, der nur eine begrenzte Anzahl von Rollen und Features unterstützt.

## <a name="the-server-core-gui"></a>Die Server Core-GUI
Wenn Sie die Installation von Server Core auf einem System abgeschlossen haben und sich zum ersten Mal anmelden, sind Sie etwas überraschend. In Abbildung 1-2 wird die Server Core-Benutzeroberfläche nach der ersten Anmeldung angezeigt.

![Server Core-Benutzeroberfläche](../media/what-is-server-core-2008/Fig1-2.png)

**Abbildung 1-2** Server Core-Benutzeroberfläche

Es gibt keinen Desktop! Das heißt, es gibt keine Windows-Explorer-Shell, mit dem Startmenü, der Taskleiste und den anderen Features, die Sie möglicherweise verwenden. Sie verfügen lediglich über eine Eingabeaufforderung. Dies bedeutet, dass Sie den größten Teil der Konfiguration einer Server Core-Installation durchführen müssen, indem Sie nacheinander Befehle einzeln eingeben. Dies ist langsam oder mithilfe von Skripts und Batch Dateien, die Ihnen helfen können, ihre Konfigurationsaufgaben zu beschleunigen und zu vereinfachen, indem Sie Sie automatisieren. Sie können auch einige erst Konfigurationsaufgaben mithilfe von Antwort Dateien ausführen, wenn Sie eine unbeaufsichtigte Installation von Server Core durchführen.

Administratoren, die über Befehlszeilen Tools wie Netsh.exe, Dfscmd.exe und Dnscmd.exe verfügen, sind die Konfiguration und Verwaltung einer Server Core-Installation einfach und sogar unterhaltsam. Personen, die keine Experten sind, gehen jedoch nicht verloren. Sie können weiterhin die standardmäßigen Windows Server 2008-MMC-Tools für die Verwaltung einer Server Core-Installation verwenden. Sie müssen Sie nur auf einem anderen System verwenden, auf dem entweder eine vollständige Installation von Windows Server 2008 oder Windows Vista mit Service Pack 1 ausgeführt wird.

Weitere Informationen zum Konfigurieren und Verwalten einer Server Core-Installation finden Sie in Kapitel 3 bis 6 dieses Buchs, während in späteren Kapiteln die Verwaltung bestimmter Server Rollen und anderer Komponenten behandelt wird. Weitere Informationen zu den verschiedenen Windows-Befehlszeilen Tools und deren Verwendung finden Sie in den folgenden zwei guten Ressourcen:
* Der Befehlsreferenz Abschnitt der technischen Bibliothek zu Windows Server 2008 ()
* *Der Windows-Befehlszeilen Administrator (Pocket Consultant* ) von William R. Stanek (Microsoft Press, 2008)

In Tabelle 1-2 sind die Haupt-GUI-Anwendungen sowie die ausführbaren Dateien aufgeführt, die in einer Server Core-Installation verfügbar sind.

**Tabelle 1-2** In einer Server Core-Installation verfügbare GUI-Anwendungen

| GUI-Anwendung | Ausführbare Datei mit Pfad |
| -------------   | -------------       |
| Eingabeaufforderung | % WINDIR% \System32\Cmd.exe |
| Diagnose Tool für Microsoft-Support | % WINDIR% \System32\MSdt.exe |
| Editor | % WINDIR% \System32\Notepad.exe |
| Registrierungs-Editor | % WINDIR% \System32\Regedt32.exe |
| Systeminformationen | % WINDIR% \System32\MSinfo32.exe |
| Task-Manager | % WINDIR% \System32\Taskmgr.exe |
| Windows Installer | % WINDIR% \System32\MSiexec.exe |

Das ist eine ziemlich kurze Liste. Im folgenden finden Sie eine Liste der Benutzeroberflächen Elemente, die nicht in Server Core enthalten sind:
* Windows Explorer Desktop Shell (Explorer.exe) und alle unterstützenden Features, wie z. b. Designs
* Alle MMC-Konsolen
* Alle System Steuerungsprogramme, mit Ausnahme von Regions-und Sprachoptionen (Intl.cpl) und Datum und Uhrzeit (Timedate.cpl)
* Alle Hypertext Markup Language (HTML) Rendering-Engines, einschließlich Internet Explorer und HTML-Hilfe
* Windows Mail
* Windows Media Player
* Die meisten Zubehör, wie z. b. Paint, Calculator und WordPad

Der .NET Framework ist auch nicht in Server Core vorhanden. Dies bedeutet, dass es keine Unterstützung für die Ausführung von verwaltetem Code auf einer Server Core-Installation gibt. Nur System eigener Code – Code, der mithilfe von Windows-APIs (Application Programming Interfaces) geschrieben wurde – kann auf Server Core ausgeführt werden. Zusammenfassend lässt sich sagen, dass alle GUI-Anwendungen, die entweder vom .NET Framework oder von der Explorer.exe Shell abhängen, nicht auf Server Core ausgeführt werden.

>[!NOTE]
>Da für Windows PowerShell das .NET Framework erforderlich ist, können Sie Windows PowerShell nicht auf Server Core installieren. Sie können eine Server Core-Installation jedoch Remote mithilfe von Windows PowerShell verwalten, solange Sie nur PowerShell-WMI-Befehle verwenden.

## <a name="supported-server-roles"></a>Unterstützte Server Rollen
Eine Server Core-Installation umfasst nur eine begrenzte Anzahl von Server Rollen im Vergleich zu einer vollständigen Installation von Windows Server 2008. In Tabelle 1-3 werden die verfügbaren Rollen für vollständige und Server Core-Installationen von Windows Server 2008 Enterprise Edition verglichen.

**Tabelle 1-3** Vergleich der Server Rollen für vollständige und Server Core-Installationen von Windows Server 2008 Enterprise Edition

| Serverrolle  | In vollständiger Installation verfügbar  | Verfügbar in Server Core  |
| ------------- | :-------------: | :------------: |
| Active Directory-Zertifikatdienste (AD CS)  | X |  |
| Active Directory Domain Services (AD DS)  | X  | X |
| Active Directory-Verbunddienste (Active Directory Federation Services, AD FS)  | X  |  |
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

Die Rollen, die für Server Core verfügbar sind, sind in der Regel unabhängig von der Architektur (x86 oder x64) und der Produkt Edition gleich. es gibt jedoch einige Ausnahmen:
* Die Rolle "Hyper-v (Virtualization)" ist nur verfügbar, wenn Sie Windows Server 2008 mit Hyper-v-Produktmedien erworben haben (Hyper-v ist nur für x64-Versionen verfügbar). Wenn Sie diese Rolle nicht benötigen, können Sie stattdessen Windows Server 2008 ohne Hyper-V-Produktmedien erwerben.
* Die Rolle "Dateidienste" in der Standard Edition ist auf einen DFS-Stamm (Standalone verteiltes Dateisystem) beschränkt und unterstützt keine Datei übergreifende Replikation (DFS-R).
* Bevor Sie die Streaming Media Services-Rolle auf Server Core installieren können, müssen Sie das entsprechende Microsoft Update eigenständige Paket (MSU-Datei) für die Architektur Ihres Servers (x86 oder x64) aus dem Microsoft Download Center herunterladen und installieren.
* Die Rolle "Webserver (IIS)" unterstützt ASP.net nicht. Dies liegt daran, dass die .NET Framework auf Server Core nicht unterstützt wird, was die Möglichkeiten eines Server Core-Webservers einschränkt.

## <a name="supported-optional-features"></a>Unterstützte optionale Funktionen
Eine Server Core-Installation unterstützt auch nur eine begrenzte Teilmenge der Features, die bei einer vollständigen Installation von Windows Server 2008 verfügbar sind. In Tabelle 1-4 werden die verfügbaren Funktionen für vollständige und Server Core-Installationen von Windows Server 2008 Enterprise Edition verglichen.

**Tabelle 1-4** Vergleich der Features für vollständige und Server Core-Installationen von Windows Server 2008 Enterprise Edition

| Feature  | In vollständiger Installation verfügbar  | Verfügbar in Server Core  |
| ------------- | :-------------: | :------------: |
| .NET Framework 3.0-Funktionen  | X  |  |
| BitLocker-Laufwerkverschlüsselung  | X  | X |
| BITS-Server Erweiterungen  | X  |  |
| Verbindungs-Manager-Verwaltungskit  | X |  |
| Desktopdarstellung  | X |  |
| Failoverclustering  | X  | X |
| Gruppenrichtlinienverwaltung  | X  |  |
| Internetdruckclient  | X  |  |
| Internet Storage Name Server  | X  |  |
| LPR-Portüberwachung  | X  |  |
| Message Queuing  | X  |  |
| Multipfad-E/A  | X  | X |
| Netzwerklastenausgleich  | X  | X |
| Peer Name Resolution-Protokoll  | X  |  |
| Verbessertes Windows-Audio-/Video-Streaming  | X |  |
| Remoteunterstützung  | X  |  |
| Remotedifferenzialkomprimierung | X  |  |
| Remoteserver-Verwaltungstools  | X  |  |
| Wechsel Speicher-Manager | X  | X |
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
| Windows PowerShell  | X  |  |
| Windows-Produkt Aktivierungs Dienst  | X   |  |
| Windows Server-Sicherung Features  | X  | X  |
| Windows-Systemressourcen-Manager  | X  |  |
| WINS-Server  | X | X |
| WLAN-Dienst | X  |  |

Auch hier gibt es einige Punkte, die Sie über die auf Server Core verfügbaren Features wissen müssen:
* Einige Features erfordern möglicherweise spezielle Hardware, damit Sie (oder überhaupt) auf Server Core ordnungsgemäß funktioniert. Zu diesen Features gehören BitLocker-Laufwerkverschlüsselung, Failoverclustering, Multipfad-e/a, Netzwerk Lastenausgleich und Wechselmedien.
* Failoverclustering ist in der Standard Edition nicht verfügbar.

## <a name="server-core-architecture"></a>Server Core-Architektur
Sehen wir uns die Architektur einer Server Core-Installation von Windows Server 2008 genauer an, indem wir Sie mit der einer vollständigen Installation vergleichen. Denken Sie zunächst daran, dass es sich bei Server Core nicht um eine andere Version von Windows Server 2008, sondern lediglich um eine Installationsoption handelt, die Sie bei der Installation von Windows Server 2008 auf einem System auswählen können. Dies impliziert Folgendes:
* Der Kernel einer Server Core-Installation ist derselbe, der bei einer vollständigen Installation derselben Hardwarearchitektur (x86 oder x64) und Edition gefunden wurde.
* Wenn eine Binärdatei in einer Server Core-Installation vorhanden ist, hat eine vollständige Installation der gleichen Hardwarearchitektur (x86 oder x64) und Edition dieselbe Version dieser speziellen Binärdatei (mit zwei Ausnahmen, die später besprochen werden).
* Wenn eine bestimmte Einstellung (z. b. eine bestimmte Firewallausnahme oder der Starttyp eines bestimmten dienstantetyps) eine bestimmte Standardkonfiguration für eine Server Core-Installation aufweist, wird diese Einstellung in einer vollständigen Installation derselben Hardwarearchitektur (x86 oder x64) und Edition exakt auf die gleiche Weise konfiguriert.

In Abbildung 1-3 wird eine vereinfachte Ansicht der Architektur einer vollständigen Installation und einer Server Core-Installation von Windows Server 2008 veranschaulicht. Die gepunktete Linie zeigt die Architektur von Server Core an, während das gesamte Diagramm die Architektur einer vollständigen Installation darstellt.

Das Diagramm veranschaulicht die modulare Architektur von Windows Server 2008, wobei Server Core auf einer Teilmenge der wichtigsten Betriebssystem Features erstellt wird. Bei der gleichen Hardwarearchitektur und Edition ist jede Datei, die auf einer Neuinstallation von Server Core vorhanden ist, auch in einer vollständigen Installation vorhanden, mit Ausnahme zweier spezieller Dateien (scregedit. wsf und Oclist.exe), die nur auf Server Core vorhanden sind. Diese speziellen Dateien waren in Server Core enthalten, um die Erstkonfiguration einer Server Core-Installation und das Hinzufügen oder Entfernen von Rollen und optionalen Komponenten zu vereinfachen.

![Die Architekturen von Server Core-und vollständigen Installationen](../media/what-is-server-core-2008/Fig1-3.png)

**Abbildung 1-3** Die Architekturen von Server Core-und vollständigen Installationen

## <a name="driver-support"></a>Treiberunterstützung
Das Architektur Diagramm von Server Core, das in Abbildung 1-3 dargestellt wird, ist offensichtlich vereinfacht. der Unterschied bei der Gerätetreiber Unterstützung zwischen Server Core-und vollständigen Installationen ist nicht zu sehen. Eine vollständige Installation von Windows Server 2008 enthält Tausende von in-Box-Treibern für verschiedene Gerätetypen, mit denen Sie Produkte auf einer Vielzahl verschiedener Hardware Konfigurationen installieren können. (Client Betriebssysteme wie Windows Vista enthalten noch mehr Treiber zur Unterstützung von Geräten, wie z. b. digitale Kameras und Scanner, die normalerweise nicht mit Servern verwendet werden.)

Wenn ein neues Gerät mit einer vollständigen Installation von Windows Server 2008 verbunden ist (oder darin installiert ist), überprüft das Plug & Play (PNP)-Subsystem zunächst, ob ein in-Box-Treiber für das Gerät vorhanden ist. Wenn ein kompatibler in-Box-Treiber gefunden wird, installiert das PNP-Subsystem automatisch den Treiber, und das Gerät wird dann betrieben. Bei einer vollständigen Installation von Windows Server 2008 wird möglicherweise eine Benachrichtigung über eine Sprechblase angezeigt, die anzeigt, dass der Treiber installiert wurde und das Gerät einsatzbereit ist.

Bei einer Server Core-Installation ist der Treiber Installationsvorgang identisch (das PNP-Subsystem ist auf Server Core vorhanden) und hat zwei Qualifikationen. Zuerst umfasst Server Core nur eine minimale Anzahl von in-Box-Treibern und nur für die folgenden Gerätetypen:
* Ein standardmäßiger Video Grafik Array-Videotreiber (VGA)
* Treiber für Speichergeräte
* Treiber für Netzwerkadapter

Beachten Sie, dass für jede der drei hier gezeigten Gerätekategorien Server Core dieselben in-Box-Treiber enthält, die in einer entsprechenden vollständigen Installation (für die gleiche Hardwarearchitektur) gefunden werden.

Wenn das PNP-Subsystem automatisch einen Treiber für ein neues Gerät installiert, erfolgt dies automatisch – es wird keine Benachrichtigung über eine Sprechblase angezeigt. Warum nicht? Da keine GUI auf Server Core vorhanden ist, gibt es keine Taskleiste, sodass auf der Taskleiste kein Benachrichtigungsbereich vorhanden ist.

Was tun Sie also, wenn Sie die Rolle "Druckdienste" zu einer Server Core-Installation hinzufügen und einen Drucker installieren möchten? Der Druckertreiber wird dem Server manuell hinzugefügt – Server Core verfügt über keine in-Box-Drucktreiber.

## <a name="service-footprint"></a>Dienst Bedarf
Da Server Core eine minimale Installation ist, verfügt sie über einen geringeren Systemdienst-Speicherbedarf als eine entsprechende vollständige Installation derselben Hardwarearchitektur und Edition. Beispielsweise werden ungefähr 75 Systemdienste standardmäßig bei einer vollständigen Installation von Windows Server 2008 installiert, von denen ungefähr 50 für den automatischen Start konfiguriert sind. Im Gegensatz dazu sind bei Server Core standardmäßig nur 70 Dienste installiert, und weniger als 40 davon werden automatisch gestartet.

In Tabelle 1-5 werden die Dienste aufgelistet, die standardmäßig in einer Server Core-Installation installiert werden, wobei der Start Modus für und das von den einzelnen Diensten verwendete Konto verwendet wird.

**Tabelle 1-5** Standardmäßig installierte System Dienste auf Server Core

| Dienstname  | `Display name`  | Start Modus  | Konto  |
| ------------- | ------------- | ------------ | ------------ |
| Aelookupsvc  | Anwendungserfahrung  | Automatisch | LocalSystem |
| AppMgmt  | Anwendungsverwaltung  | Manuell | LocalSystem |
| BFE | Basisfiltermodul  | Automatisch | LocalService |
| BITS | Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)  | Automatisch | LocalSystem |
| Browser | Computerbrowser  | Manuell | LocalSystem |
| CertPropSvc | Zertifikatverteilung  | Manuell | LocalSystem |
| COMSysApp  | COM+-Systemanwendung  | Manuell | LocalSystem |
| CryptSvc  | Kryptografische Dienste  | Automatisch | Netzwerkdienst |
| DcomLaunch  | DCOM-Server-Prozessstart  | Automatisch | LocalSystem |
| Dhcp  | DHCP-Client  | Automatisch | LocalService |
| Dnscache | DNS-Client  | Automatisch | Netzwerkdienst |
| DPS  | Diagnoserichtliniendienst  | Automatisch | LocalService |
| EventLog | Windows-Ereignisprotokoll  | Automatisch | LocalService |
| EventSystem  | COM+-Ereignissystem  | Automatisch | LocalService |
| "F"  | Registrierungsdienst für Microsoft Fibre Channel-Plattform  | Manuell | LocalService |
| gpsvc  | Gruppenrichtlinienclient  | Automatisch | LocalSystem |
| hidserv | Eingabegeräte Zugriff  | Manuell | LocalSystem |
| hkmsvc  | Integritäts Schlüssel und Zertifikat Verwaltung  | Manuell | LocalSystem |
| IKEEXT  | IKE- und AuthIP IPsec-Schlüsselerstellungsmodule  | Automatisch | LocalSystem |
| iphlpsvc  | IP-Hilfsprogramm  | Automatisch | LocalSystem |
| KeyIso | CNG-Schlüsselisolation  | Manuell | LocalSystem |
| KtmRm  | KtmRm für Distributed Transaction Coordinator  | Automatisch | Netzwerkdienst |
| LanmanServer  | Server  | Automatisch | LocalSystem |
| LanmanWorkstation  | Workstatione  | Automatisch | LocalService |
| lltdsvc  | Verbindungsschicht-Topologieerkennungs-Zuordnungsprogramm  | Manuell | LocalService |
| lmhosts  | TCP/IP-NetBIOS-Hilfsdienst  | Automatisch | LocalService |
| MpsSvc  | Windows-Firewall  | Automatisch | LocalService |
| MSDTC  | Distributed Transaction Coordinator  | Automatisch | Netzwerkdienst |
| MSiSCSI  | Microsoft iSCSI-Initiator-Dienst  | Manuell | LocalSystem |
| msiserver  | Windows Installer  | Manuell | LocalSystem |
| NAPAgent  | Netzwerkzugriffsschutz-Agent  | Manuell | Netzwerkdienst |
| Netlogon  | Netlogon  | Manuell | LocalSystem |
| netprofm  | Netzwerklistendienst  | Automatisch | LocalService |
| NlaSvc  | NLA (Network Location Awareness)  | Automatisch | Netzwerkdienst |
| nsi  | Netzwerkspeicher-Schnittstellendienst  | Automatisch | LocalService |
| pla  | Leistungsprotokolle und -warnungen  | Manuell | LocalService |
| PlugPlay  | Plug & Play  | Automatisch | LocalSystem |
| PolicyAgent  | IPsec-Richtlinien-Agent  | Automatisch | Netzwerkdienst |
| ProfSvc  | Benutzerprofildienst  | Automatisch | LocalSystem |
| ProtectedStorage  | Geschützter Speicher  | Manuell | LocalSystem |
| RemoteRegistry  | Remoteregistrierung  | Automatisch | LocalService |
| RpcSs  | Remoteprozeduraufruf (RPC)  | Automatisch | Netzwerkdienst |
| RSoPProv | Richtlinienergebnissatzanbieter  | Manuell | LocalSystem |
| sacsvr  | Hilfsprogramm für spezielle Verwaltungskonsole  | Manuell | LocalSystem |
| SamSs  | Sicherheitskonto-Manager  | Automatisch | LocalSystem |
| SCardSvr | Smartcard  | Manuell | LocalService |
| Zeitplan | Aufgabenplanung  | Automatisch | LocalSystem |
| SCPolicySvc | Richtlinie zum Entfernen der Smartcard  | Manuell | LocalSystem |
| seclogon | Sekundäre Anmeldung  | Automatisch | LocalSystem |
| SENS | Benachrichtigungsdienst für Systemereignisse  | Automatisch | LocalSystem |
| SessionEnv | Terminaldienstekonfiguration  | Manuell | LocalSystem |
| SLsvc  | Softwarelizenzierung | Automatisch | Netzwerkdienst |
| SNMPTRAP  | SNMP-Trap  | Manuell | LocalService |
| swprv  | Microsoft-Softwareschattenkopie-Anbieter | Manuell | LocalSystem |
| TB | TPM-Basisdienste  | Manuell | LocalService |
| TermService  | Terminaldienste | Automatisch | Netzwerkdienst |
| TrustedInstaller | Windows Modules Installer  | Automatisch | LocalSystem |
| UmRdpService | Terminal Dienste-portredirector für usermode  | Manuell | LocalSystem |
| vds | Virtueller Datenträger  | Manuell | LocalSystem |
| VSS | Volumeschattenkopie  | Manuell | LocalSystem |
| W32Time | Windows-Zeitdienst  | Automatisch | LocalService |
| WcsPlugInService  | Windows-Farb System  | Manuell | LocalService |
| WdiServiceHost  | Diagnosediensthost  | Manuell | LocalService |
| WdiSystemHost  | Diagnosesystemhost  | Manuell | LocalSystem |
| Wecsvc | Windows-Ereignissammlung  | Manuell | Netzwerkdienst |
| Winhttpauto-proxysvc  | WinHTTP-Web Proxy Auto-Discovery-Dienst  | Automatisch | LocalService |
| Winmgmt | Windows-Verwaltungsinstrumentation | Automatisch | LocalSystem |
| WinRM  | Windows-Remoteverwaltung (WS-Verwaltung) | Automatisch | Netzwerkdienst |
| wmiApSrv  | WMI-Leistungsadapter  | Manuell | LocalSystem |
| wuauserv | Windows-Update | Automatisch | LocalSystem |