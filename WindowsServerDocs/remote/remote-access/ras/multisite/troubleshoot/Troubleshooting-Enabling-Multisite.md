---
title: Behandeln von Problemen beim Aktivieren der Funktionen für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs bereitstellen mehrere RAS-Server in einer Bereitstellung für mehrere Standorte in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 570c81d6-c4f4-464c-bee9-0acbd4993584
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7fafc2e95f30a3956a1e2fdfcdf2f368a1798d28
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280961"
---
# <a name="troubleshooting-enabling-multisite"></a>Behandeln von Problemen beim Aktivieren der Funktionen für mehrere Standorte

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Dieses Thema enthält Informationen zum Beheben von Problemen mit dem Befehl `Enable-DAMultisite`. Um sicherzustellen, dass sich der angezeigte Fehler auf das Aktivieren der Funktionen für mehrere Standorte bezieht, prüfen Sie, ob im Windows-Ereignisprotokoll die Ereignis-ID 10051 aufgeführt wird.  
  
## <a name="user-connectivity-issues"></a>Benutzerkonnektivitätsprobleme  
Bei Benutzern treten möglicherweise Konnektivitätsprobleme auf, wenn Sie die Funktionen für mehrere Standorte aktivieren, aber die Konfiguration nicht richtig ist.  
  
**Ursache**  
  
Windows 10 und Windows 8-Clientcomputer können in einer Bereitstellung für mehrere Standorte zwischen verschiedenen Einstiegspunkten wechseln.  Windows 7-Clientcomputer müssen in der Bereitstellung für mehrere Standorte einem bestimmten Einstiegspunkt zugewiesen sein. Falls sich Clientcomputer nicht in der richtigen Sicherheitsgruppe befinden, erhalten sie möglicherweise die falschen Gruppenrichtlinieneinstellungen.  
  
**Lösung**  
  
DirectAccess erfordert mindestens eine Sicherheitsgruppe für alle Windows 10- und Windows 8-Clientcomputer; Verwendung einer Sicherheitsgruppe für alle Windows 10 und Windows 8-Computer pro Domäne empfohlen. DirectAccess erfordert darüber hinaus eine Sicherheitsgruppe für Windows 7-Clientcomputer für jeden Einstiegspunkt. Jeder Clientcomputer sollte nur in eine Sicherheitsgruppe aufgenommen werden. Daher stellen Sie sicher, dass die Sicherheitsgruppen für Windows 10 und Windows 8-Clients enthalten nur Computer mit Windows 10 oder Windows 8 und, die jedem Clientcomputer Windows 7 gehört zu einer dedizierten Sicherheitsgruppe für den relevanten Einstiegspunkt und dass keine Windows 10 oder Windows 8-Clients die Windows 7-Sicherheitsgruppen angehören.  
  
Konfigurieren Sie die Windows 8-Sicherheitsgruppen für die **Gruppen auswählen** auf der Seite die **DirectAccess-Clientsetup** Assistenten. Konfigurieren von Windows 7-Sicherheitsgruppen für die **Clientunterstützung** auf der Seite die **Aktivieren der Bereitstellung für mehrere Standorte** -Assistenten oder auf die **Clientunterstützung** auf der Seite die  **Fügen Sie einen Einstiegspunkt** Assistenten.  
  
## <a name="kerberos-proxy-authentication"></a>Kerberos-Proxyauthentifizierung  
**Fehler**. Kerberos-Proxyauthentifizierung wird in einer Bereitstellung für mehrere Standorte nicht unterstützt. Sie müssen die Verwendung von Computerzertifikaten für IPsec-Benutzerauthentifizierung aktivieren.  
  
**Ursache**  
  
Die Computerzertifikatauthentifizierung muss vor dem Aktivieren der Funktionen für mehrere Standorte aktiviert werden.  
  
**Lösung**  
  
So konfigurieren Sie die Computerzertifikatauthentifizierung:  
  
1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 2 **RAS-Server** auf **Bearbeiten**.  
  
2.  Aktivieren Sie im **Setup-Assistenten für den RAS-Server** auf der Seite **Authentifizierung** das Kontrollkästchen **Computerzertifikate verwenden**, und wählen Sie die Stamm- oder Zwischenzertifizierungsstelle aus, von der Zertifikate in Ihrer Bereitstellung ausgestellt werden.  
  
Verwenden Sie zum Aktivieren der Computerzertifikatauthentifizierung mithilfe von Windows PowerShell die `Set-DAServer` Cmdlet, und geben Sie die *IPsecRootCertificate* Parameter.  
  
## <a name="ip-https-certificates"></a>IP-HTTPS-Zertifikate  
**Fehler**. Der DirectAccess-Server wird ein selbstsigniertes Zertifikat für IP-HTTPS verwendet. Konfigurieren Sie IP-HTTPS für die Verwendung eines signierten Zertifikats von einer bekannten Zertifizierungsstelle.  
  
**Ursache**  
  
Das IP-HTTPS-Zertifikat ist selbstsigniert. Sie können keine selbstsignierten Zertifikate in einer Bereitstellung für mehrere Standorte verwenden.  
  
**Lösung**  
  
So wählen Sie ein IP-HTTPS-Zertifikat aus:  
  
1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 2 **RAS-Server** auf **Bearbeiten**.  
  
2.  Stellen Sie sicher, dass im **Setup-Assistenten für den RAS-Server** auf der Seite **Netzwerkadapter** unter **Wählen Sie das Zertifikat aus, mit dem IP-HTTPS-Verbindungen authentifiziert werden:** das Kontrollkästchen **Selbstsigniertes Zertifikat verwenden, das von DirectAccess automatisch erstellt wurde** deaktiviert ist, und klicken Sie auf **Durchsuchen**, um ein von einer vertrauenswürdigen Zertifizierungsstelle ausgestelltes Zertifikat auszuwählen.  
  
## <a name="network-location-server"></a>Netzwerkadressenserver  
  
-   **Problem 1**  
  
    **Fehler**. DirectAccess für die Verwendung ein selbstsigniertes Zertifikats für den Netzwerkadressenserver konfiguriert. Konfigurieren Sie den Netzwerkadressenserver für die Verwendung eines signierten Zertifikats von einer Zertifizierungsstelle.  
  
    **Ursache**  
  
    Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt und verwendet ein selbstsigniertes Zertifikat. Sie können keine selbstsignierten Zertifikate in einer Bereitstellung für mehrere Standorte verwenden.  
  
    **Lösung**  
  
    So wählen Sie ein Netzwerkadressenserver-Zertifikat aus:  
  
    1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 3 **Infrastrukturserver** auf **Bearbeiten**.  
  
    2.  Stellen Sie sicher, dass im **Assistenten zum Einrichten** des Infrastrukturservers auf der Seite **Netzwerkadressenserver** unter **Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt.** das Kontrollkästchen **Selbstsigniertes Zertifikat verwenden** deaktiviert ist, und klicken Sie auf **Durchsuchen**, um ein von einer Unternehmenszertifizierungsstelle ausgestelltes Zertifikat auszuwählen.  
  
-   **Problem 2**  
  
    **Fehler**. Zum Bereitstellen eines Clusters mit Netzwerklastenausgleich oder Bereitstellung für mehrere Standorte, rufen Sie ein Zertifikat für den Netzwerkadressenserver mit einem Antragstellernamen an, der von den internen Namen der RAS-Servers unterscheidet.  
  
    **Ursache**  
  
    Der Antragstellername des für die Netzwerkadressenserver-Website verwendeten Zertifikats stimmt mit dem internen Namen des RAS-Servers überein. Dadurch werden Probleme bei der Namensauflösung verursacht.  
  
    **Lösung**  
  
    Fordern Sie ein Zertifikat mit einem Antragstellernamen an, der sich vom internen Namen des RAS-Servers unterscheidet.  
  
    So konfigurieren Sie den Netzwerkadressenserver:  
  
    1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 3 **Infrastrukturserver** auf **Bearbeiten**.  
  
    2.  Klicken Sie im **Assistenten zum Einrichten** des Infrastrukturservers auf der Seite **Netzwerkadressenserver** unter **Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt.** auf **Durchsuchen**, um das zuvor abgerufene Zertifikat auszuwählen. Das Zertifikat muss einen Antragstellernamen enthalten, der sich vom internen Namen des RAS-Servers unterscheidet.  
  
## <a name="windows-7-client-computers"></a>Windows 7-Clientcomputer  
**Empfangene Warnung**. Wenn Sie für mehrere Standorte aktivieren, müssen für DirectAccess-Clients konfigurierten Sicherheitsgruppen keine Windows 7-Computer enthalten. Wählen Sie eine Sicherheitsgruppe aus, die die Clients für die einzelnen Einstiegspunkte enthält, damit Clientcomputer mit Windows 7 in einer Bereitstellung mit mehreren Standorten unterstützt werden.  
  
**Ursache**  
  
In der vorhandenen DirectAccess-Bereitstellung wurde Unterstützung für Windows 7-Clients aktiviert.  
  
**Lösung**  
  
DirectAccess erfordert mindestens eine Sicherheitsgruppe für alle Windows 8-Clientcomputer und eine Sicherheitsgruppe für Windows 7-Clientcomputer für jeden Einstiegspunkt. Jeder Clientcomputer sollte nur in eine Sicherheitsgruppe aufgenommen werden. Aus diesem Grund sollten Sie sicherstellen, dass die Sicherheitsgruppe für Windows 8-Clients nur Computer mit Windows 8 enthält, und jede Windows 7-Clientcomputer zu einer dedizierten Sicherheitsgruppe für den relevanten Einstiegspunkt und gehört, kein Windows 8-Clients die Windows 7-Sicherheitsgruppen angehören.  
  
## <a name="active-directory-site"></a>Active Directory-Standort  
**Fehler**. Der Server < Servername > ist nicht in der Active Directory-Standort zugeordnet.  
  
**Ursache**  
  
Von DirectAccess konnte der Active Directory-Standort nicht ermittelt werden. In der Konsole für Active Directory-Standorte und -Dienste können Sie die verschiedenen Subnetze für Ihr Netzwerk konfigurieren und die einzelnen Subnetze dem relevanten Active Directory-Standort zuweisen. Dieser Fehler kann auftreten, wenn die IP-Adresse des RAS-Servers zu keinem der Subnetze gehört oder wenn das Subnetz, zu dem die IP-Adresse gehört, keinem Active Directory-Standort zugeordnet ist.  
  
**Lösung**  
  
Überprüfen Sie, ob dies das Problem ist, indem Sie den Befehl `nltest /dsgetsite` auf dem RAS-Server ausführen. Ist dies das Problem, wird vom Befehl ERROR_NO_SITENAME zurückgegeben. Stellen Sie zum Beheben des Problems sicher, dass auf dem Domänencontroller ein Subnetz vorhanden ist, das die interne Server-IP-Adresse enthält und einem Active Directory-Standort zugeordnet ist.  
  
## <a name="SaveGPOSettings"></a>Server-GPO-Einstellungen werden gespeichert.  
**Fehler**. Fehler beim Speichern der Remotezugriffseinstellungen GPO < GPO_name >.  
  
**Ursache**  
  
Änderungen an den Server-Gruppenrichtlinienobjekt konnten nicht gespeichert werden, entweder aufgrund von Konnektivitätsproblemen oder bei eine freigabeverletzung der Datei registry.pol wird z. B. ein anderer Benutzer hat die Datei gesperrt.  
  
**Lösung**  
  
Stellen Sie sicher, dass Konnektivität zwischen dem RAS-Server und dem Domänencontroller besteht. Besteht Konnektivität, überprüfen Sie auf dem Domänencontroller, ob die Datei %%amp;quot;registry.pol%%amp;quot; durch einen anderen Benutzer gesperrt ist, und beenden Sie ggf. diese Benutzersitzung, um die Datei zu entsperren.  
  
## <a name="InternalServerError"></a>Interner Fehler ist aufgetreten  
**Fehler**. Interner Fehler.  
  
**Ursache**  
  
Dieser Fehler wird möglicherweise durch eine unerwartete Konfiguration der Einstiegspunkttabelle im Client-Gruppenrichtlinienobjekt verursacht. Dies kann passieren, wenn der Administrator DirectAccess-Client-Cmdlets zum Bearbeiten der Einstiegspunkttabelle im Client-Gruppenrichtlinienobjekt verwendet.  
  
**Lösung**  
  
Überprüfen Sie die Konfiguration der Einstiegspunkttabelle in allen Client-Gruppenrichtlinienobjekten, und beheben Sie alle Inkonsistenzen in der Konfiguration für mehrere Standorte zwischen den verschiedenen Instanzen der Client-Gruppenrichtlinienobjekte und der DirectAccess-Konfiguration. Verwenden Sie das `Get-DaEntryPointTableItem`-Cmdlet mit dem Namen des Client-Gruppenrichtlinienobjekts, um die Einstiegspunkttabelle für den Client abzurufen. Verwenden Sie das `Get-NetIPHttpsConfiguration`-Cmdlet, um alle IP-HTTPS-Profile für alle Einstiegspunkte abzurufen.  
  
Weitere Informationen finden Sie unter [DirectAccess-Client-Cmdlets in Windows PowerShell](https://technet.microsoft.com/library/hh848426).  
  


