---
redirect_url: /windows-server/windows-server
ms.openlocfilehash: 6f6e0d21fdf43ce3cf9f713d5731cfea5bb069de
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59812271"
---
# <a name="windows-server-2016"></a>Windows Server 2016

Diese Bibliothek enthält Informationen für IT-Spezialisten für die Bewertung, Planung, Bereitstellung, Sicherung und das Verwalten von Windows Server 2016.

> [!Note] 
> Die nächste Version von Windows Server wird geändert. Finden Sie Detail zu den Neuigkeiten in der [Übersicht: Windows Server, Semi-Annual Channel](./get-started/semi-annual-channel-overview.md). 

[![Windows Server 2016-Übersichtsvideo](media/front-page-video.png)](https://www.youtube-nocookie.com/embed/V8oF0JpDzaM)

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/what-s-new-in-windows-server-2016">
        <img height=145 src="media/whats-new-highlight.png" alt="What's new icon" title="Neuerungen in Windows Server 16"/></a>
        <br/>Neuigkeiten:
    </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/get-started/server-basics">
        <img height=145 src="media/1-getstarted.png" alt="get started icon" title="Erste Schritte mit Windows Server 16" /></a>
      <br/>Erste Schritte </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/administration/index">
        <img height=145 src="media/8-management.png" alt="administer icon" title="Verwalten von Windows Server" /></a>
      <br/>Verwalten </td>
    <td align='center' style="width:25%; border:0;">
      <a href="/windows-server/failover-clustering/failover-clustering-overview">
        <img height=145 src="media/3-failover.png" alt="Failover clustering icon" title="Windows Server-Failoverclusterunterstützung" /></a>
      <br/>Failoverclustering </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/identity/identity-and-access">
        <img height=145 src="media/4-identity.png" alt="Identity and access icon" title="Windows Server: Identität und Zugriff" /></a>
      <br>Identität und Zugriff </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/networking/networking">
        <img height=145 src="media/6-networking.png" alt="Networking icon" title="Windows Server-Netzwerke" />
        </a>
      <br/>Netzwerk </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/remote/index">
        <img height=145 src="media/remote.png" alt="remote icon" title="Remotezugriff und Serververwaltung" />
        </a>
      <br/>Remotezugriff </td>
    <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/security/security-and-assurance">
        <img height=145 src="media/5-security.png" alt="Security icon" title="Sicherheit und Zusicherungen in Windows Server" />
      </a>
      <br/>Sicherheit und Zusicherungen </td>
  </tr>
  <tr style="text-align:center;">
    <td align='center' style="width:25%; border:0;">&nbsp;</td>
    <td align='center' style="width:25%; border:0;"><br>
      <a href="/windows-server/storage/storage">
        <img height=145 src="media/7-storage.png" alt="Storage icon" title="Windows Server-Speicher" />
      </a>
      <br/>Speicher </td>
   <td align='center' style="width:25%; border:0;"><br/>
      <a href="/windows-server/virtualization/virtualization">
        <img height=145 src="media/virtualization.png" alt="virtualization icon" title="Windows Server-Virtualisierung" /></a>
      <br/>Virtualisierung </td>
    <td align='center' style="width:25%; border:0;">&nbsp; </td>
  </tr>
</table>

<br/>

> [!Note] 
> Um in Windows Server 2016 verfügbare neue Features und Funktionen aus erster Hand auszuprobieren, können Sie unter [Windows Server Evaluierungsversionen](https://www.microsoft.com/evalcenter/evaluate-windows-server-2016) eine Evaluierungsversion herunterladen. 


## <a name="windows-server-2016-editions"></a>Windows Server 2016-Editionen

Windows Server 2016 ist unter Standard Edition, Datacenter Edition und Essentials Edition verfügbar. Windows Server 2016 Datacenter umfasst unbegrenzte Virtualisierungsrechte sowie neue Funktionen zum Erstellen eines softwaredefinierten Rechenzentrums. Windows Server 2016 Standard bietet Funktionen auf Unternehmensebene mit eingeschränkten Virtualisierungsrechten. Windows Server Essentials ist ein idealer erster Server mit Cloudverbindung. Dieser verfügt über seine eigene [umfassende Dokumentation](https://go.microsoft.com/fwlink/?LinkID=827171). Der Fokus des Inhalts hier liegt auf Standard Edition und Datacenter Edition. In der folgenden Tabelle sind die Hauptunterschiede zwischen Standard Edition und Datacenter Edition kurz zusammengefasst:

|Feature|Datacenter|Standard|  
|-------------------|----------|-----------------------|  
|Hauptfunktionen von Windows Server| ja| ja|
|Betriebssystemumgebungen (operating system environments, OSEs)/Hyper-V-Container|unbegrenzt|   2|
|Windows Server-Container|unbegrenzt|   unbegrenzt|
|Host-Überwachungsdienst| ja| ja|
|Nano Server-Installationsoption| ja| ja|
|Speicherfunktionen einschließlich Direkte Speicherplätze und Speicherreplikat| ja| nein|
|Abgeschirmte virtuelle Computer| ja| nein|
|Software-Defined Networking-Infrastruktur (Netzwerkcontroller, Softwarelastenausgleich und mehrinstanzenfähiges Gateway)| ja| nein|

Weitere Informationen finden Sie unter [Preise und Lizenzierung für Windows Server 2016](https://www.microsoft.com/en-us/cloud-platform/windows-server-pricing) und [Vergleichen von Funktionen in Windows Server-Versionen](https://www.microsoft.com/en-us/cloud-platform/windows-server-comparison).

## <a name="installation-options"></a>Installationsoptions

*Sowohl Standard Edition als auch Datacenter Edition bieten drei Installationsoptionen:

- **Server Core:** Diese Option reduziert den auf dem Datenträger erforderlichen Festplattenspeicher, die potenzielle Angriffsfläche und insbesondere die Wartungsanforderungen. Dies ist die **empfohlene** Option, sofern Sie keinen besonderen Bedarf an zusätzlichen Benutzeroberflächenelementen und grafischen Verwaltungstools haben.
- **Server mit Desktopdarstellung:** Mit dieser Option werden die Standardbenutzeroberfläche und alle Tools installiert, einschließlich Kundenerfahrungsfeatures, die in Windows Server 2012 R2 eine separate Installation erforderten. Serverrollen und Features werden mit dem Server-Manager oder anderen Methoden installiert.
- **Nano Server:** Dabei handelt es sich um ein remote verwaltetes Serverbetriebssystem, das für private Clouds und Rechenzentren optimiert ist. Das Betriebssystem ähnelt Windows Server im Modus Server Core, ist aber deutlich kleiner, bietet keine Möglichkeit zur lokalen Anmeldung, und unterstützt ausschließlich 64-Bit-Anwendungen, Tools und Agents. Es beansprucht weit weniger Speicherplatz, wird erheblich schneller eingerichtet und erfordert wesentlich weniger Updates und Neustarts als die anderen Optionen.

>[!Note]
> Im Gegensatz zu einigen früheren Versionen von Windows Server ist eine Konvertierung zwischen Server Core und Servern mit Desktopdarstellung nach der Installation nicht möglich. Wenn Sie beispielsweise Server Core installieren und später Server mit Desktopdarstellung verwenden möchten (und umgekehrt), sollten Sie eine Neuinstallation vornehmen.


Nun, da Sie wissen, welche Edition und welche Installationsoption für Sie geeignet ist, klicken Sie auf eine der nachstehenden Optionen, um mit Windows Server 2016 zu beginnen.
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:33%; border:0;">
      <a  href="/windows-server/get-started/getting-started-with-nano-server"> <img width="175" src="media/nano.png" alt="Icon representing Nano server" title="Nano Server - Geringstes Gewicht" /><br/>Nano Server - <br/>Geringste Gewicht</a>
    </td>
    <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-core"> <img width="175" src="media/servercore.png" alt="Icon representing the Server Core installation" title="Server Core - Empfohlen" /><br/>Server Core - <br/>Empfohlen</a></td>
   <td align='center' style="width:33%; border:0;"><a href="/windows-server/get-started/getting-started-with-server-with-desktop-experience"><img width="175" src="media/desktop.png" alt="Icon representing the full desktop experience installation option for Windows Server" title="Desktopdarstellung - Umfassende Benutzererfahrung" /><br/>Desktopdarstellung - <br/>Komplette-Schnittstelle</a></td>
  </tr>
</table>

## <a name="windows-server-software-defined-datacenter-sddc"></a>Windows Server-Software-Defined Datacenter (SDDC)

Virtualisierte Speicher-, Netzwerk-, Sicherheits- und Management-Technologien sind die Bausteine von Windows Server Software-Defined Datacenter (SDDC).
<br/>
<br/>

<table border="0" width="100%" align='center'>
  <tr style="text-align:center;">
    <td align='center' style="width:10%; border:0;"></td>
    <td align='center' style="width:50%; border:0;"><a href="/windows-server/sddc"><img width="400" src="media/sddc/WS16-heading.png" alt="Icon representing SDDC" title="Windows Server-Software-Defined Datacenter (SDDC)" /><br/>Windows Server Software-Defined Datacenter (SDDC)</a></td>
    <td align='center' style="width:10%; border:0;"></td>
  </tr>
</table>
