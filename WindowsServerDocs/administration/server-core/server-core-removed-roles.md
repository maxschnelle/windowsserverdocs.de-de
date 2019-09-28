---
title: Rollen, Rollen Dienste und Features, die nicht in Windows Server Server Core enthalten sind
description: Erfahren Sie mehr über die Rollen und Features, die nicht in der Server Core-Installationsoption für Windows Server enthalten sind.
ms.prod: windows-server
ms.mktglfcycl: manage
ms.sitesec: library
author: lizap
ms.localizationpriority: medium
ms.date: 02/23/2018
ms.openlocfilehash: ce8fd0edc426b673f873717a27e6045e3476170f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383365"
---
# <a name="roles-role-services-and-features-not-in-windows-server---server-core"></a>Rollen, Rollen Dienste und Features, die nicht in Windows Server Server Core enthalten sind

> Gilt für: Windows Server 2019, Windows Server 2016 und Windows Server (halbjährlicher Kanal)

Die folgenden Rollen, Rollen Dienste und Features wurden aus der Server Core-Installationsoption von Windows Server entfernt. Anhand dieser Informationen können Sie herausfinden, ob die Server Core-Option für Ihre Umgebung funktioniert.

> [!NOTE]
> Sie können auch eine Liste der Rollen, Rollen Dienste und Features sehen, die [in Server Core enthalten sind](server-core-roles-and-services.md). Es handelt sich um eine sehr große Liste, sodass Sie für optimale Ergebnisse diese Liste nach der jeweiligen Rolle oder dem Feature durchsuchen können, die für Sie von Interesse sind.

## <a name="roles-not-in-server-core"></a>Rollen nicht in Server Core

- Faxserver (**Fax**)
- Multipoint Services (**multipointserverrole**)
- Netzwerk Richtlinien-und Zugriffs Dienste (**npas**)
- Windows-Bereitstellungs Dienste (Windows Deployment Services,**WDS**) *(vor Windows Server Version 1803)*

## <a name="role-services-not-in-server-core"></a>Rollen Dienste nicht in Server Core
Beachten Sie, dass einige Remotedesktop-Rollen Dienste in Server Core (Verbindungs Broker, Lizenzierung, Virtualisierungshost) enthalten sind, andere jedoch nicht (Gateway, RD-Sitzungshost, Webzugriff).

- Druck-und Dokumentdienste \ Server für verteilte Scanvorgänge (**Print-Scan-Server**)
- Druck-und Dokumentdienste \ Internet Druck (**Print-Internet**)
- Remotedesktopdienste \ Remotedesktop Gateway (**RDS-Gateway**)
- Remotedesktopdienste \ Remotedesktop-Sitzungshost (**RDS-RD-Server**)
- Remotedesktopdienste \ Remotedesktop Webzugriff (**RDS-Web-Access**)
- Rollen Dienst-Webserver (IIS) \ Verwaltungs Tools \ IIS-Verwaltungskonsole (**Web-Mgmt-Konsole**)
- Rollen Dienst-Webserver (IIS) \ Verwaltungs Tools \ IIS 6-Verwaltungs Kompatibilität \ IIS 6-Verwaltungskonsole (**Web-lgcy-Mgmt-Console**)
- Windows-Bereitstellungs Dienste \ Bereitstellungs Server (**WDS-Bereitstellung**)
- Windows-Bereitstellungs Dienste \ Transport Server (**WDS-Transport**) *(vor Windows Server-Version 1803)*

## <a name="features-not-in-server-core"></a>Features nicht in Server Core
- Bits (Bits) \ IIS-Server Erweiterung (**BITS-IIS-ext**)
- BitLocker-Netzwerk Entsperrung (**BitLocker-networkunlock**)
- Direkte Wiedergabe (**Direct-Play**)
- Internet Druck Client (**Internet-Print-Client**)
- LPR-Port Monitor (**LPR-Port-Monitor**)
- Message Queuing \ Message Queuing Services \ Multicasting-Unterstützung (**MSMQ-Multicasting**)
- RAS-Verbindungs-Manager-Verwaltungskit (**CMAK**)
- Remote Unterstützung (**Remote**Unterstützung)
- Remoteserver-Verwaltungstools \ Feature-Verwaltungs Tools \ SMTP-Server Tools (**rsat-SMTP**)
- Remoteserver-Verwaltungstools \ Featureverwaltungstools \ BitLocker-Laufwerkverschlüsselung Administration Utilities \ BitLocker-Laufwerkverschlüsselung Tools (**rsat-Feature-Tools-BitLocker-RemoteAdminTool**)
- Remoteserver-Verwaltungstools \ Feature-Verwaltungs Tools \ BITS-Server Erweiterungs Tools (**rsat-BITS-Server**)
- Remoteserver-Verwaltungstools \ Features Verwaltungs Tools \ Netzwerklastenausgleichs **-Tools (RSAT-NLB**)
- Remoteserver-Verwaltungstools \ Features Verwaltungs Tools \ SNMP-Tools (**rsat-SNMP**)
- Remoteserver-Verwaltungstools \ Feature-Verwaltungs Tools \ WINS-Server Tools (**rsat-WINS**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Hyper-v-Verwaltungs Tools \ Hyper-v-GUI-Verwaltungs Tools (**Hyper-v-Tools**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Remotedesktopdienste Tools \ Remotedesktop gatewaytools (**rsat-RDS-Tools**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Remotedesktopdienste Tools \ Remotedesktop gatewaytools (**rsat-RDS-Gateway**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Remotedesktopdienste Tools \ Remotedesktop Lizenzierungs Diagnosetools (**rsat-RDS-Licensing-Diagno-UI**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Remotedesktopdienste Tools \ Remotedesktop Lizenzierungs Tools (**RDS-Licensing-UI**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Windows Server Update Services Tools \ Benutzeroberfläche Verwaltungskonsole (**updateservices-UI**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Active Directory Certificate Services-Tools (**rsat-ADCs**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Active Directory zertifikatdienstetools \ Zertifizierungsstellen-Verwaltungs Tools (**rsat-ADCs-Mgmt**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Active Directory Certificate Services Tools \ Online-Respondertools (**rsat-Online-Responder**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Active Directory Rights Management Services Tools (**rsat-ADRMS**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Faxserver Tools (**rsat-Fax**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Dateidienste Tools (**rsat-File-Services**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Dateidienste Tools \ DFS-Verwaltungs Tools (**rsat-DFS-Mgmt-con**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Dateidienste Tools \ Datei Server Ressourcen-Manager Tools (**rsat-f-Mgmt**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Dateidienste Tools \ Dienste für Netzwerkdatei System-Verwaltungs Tools (**rsat-NFS-admin**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Tools für Netzwerk Richtlinien-und Zugriffs Dienste (**rsat-NPAS**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Druck-und Dokumentdienste Tools (**rsat-Print-Services**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Volumen Aktivierungs Tools (**rsat-VA-Tools**)
- Remoteserver-Verwaltungstools \ Rollen Verwaltungs Tools \ Tools der Windows-Bereitstellungs Dienste (**WDS-Adminpack**)
- Einfache TCP/IP-Dienste (**Simple-tcpip**)
- SMTP-Server (**SMTP-Server**)
- TFTP-Client (**TFTP-Client**)
- WebDAV-Redirector (**WebDAV-Redirector**)
- Windows-Biometrieframework (**biometrische Framework**)
- Windows Defender Features \ GUI für Windows Defender (**Windows-Defender-GUI**)
- Windows Identity Foundation 3,5 (**Windows-Identity-Foundation**)
- Windows PowerShell \ Windows PowerShell ISE (**PowerShell-ISE**)
- Windows-Suchdienst (**Search-Service**)
- Windows-TIFF-IFilter (**Windows-TIFF-IFilter**)
- Drahtloser LAN-Dienst (**Drahtlos Netzwerke**)
- XPS-Viewer (**XPS-Viewer**)
