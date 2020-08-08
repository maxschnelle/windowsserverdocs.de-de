---
title: Behandeln von Problemen beim Aktivieren der Funktionen für mehrere Standorte
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.topic: article
ms.assetid: 570c81d6-c4f4-464c-bee9-0acbd4993584
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 97e33b08d84b4e1aa4a5cb17aca331456e0402d2
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87958488"
---
# <a name="troubleshooting-enabling-multisite"></a>Behandeln von Problemen beim Aktivieren der Funktionen für mehrere Standorte

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält Informationen zum Beheben von Problemen mit dem Befehl `Enable-DAMultisite`. Um sicherzustellen, dass sich der angezeigte Fehler auf das Aktivieren der Funktionen für mehrere Standorte bezieht, prüfen Sie, ob im Windows-Ereignisprotokoll die Ereignis-ID 10051 aufgeführt wird.

## <a name="user-connectivity-issues"></a>Benutzerkonnektivitätsprobleme
Bei Benutzern treten möglicherweise Konnektivitätsprobleme auf, wenn Sie die Funktionen für mehrere Standorte aktivieren, aber die Konfiguration nicht richtig ist.

**Ursache**

Bei einer Bereitstellung mit mehreren Standorten können Windows 10-und Windows 8-Client Computer zwischen verschiedenen Einstiegspunkten wechseln.  Windows 7-Client Computer müssen einem bestimmten Einstiegspunkt in der Bereitstellung für mehrere Standorte zugeordnet werden. Falls sich Clientcomputer nicht in der richtigen Sicherheitsgruppe befinden, erhalten sie möglicherweise die falschen Gruppenrichtlinieneinstellungen.

**Lösung**

DirectAccess erfordert mindestens eine Sicherheitsgruppe für alle Windows 10-und Windows 8-Client Computer. Es wird empfohlen, eine Sicherheitsgruppe für alle Windows 10-und Windows 8-Computer pro Domäne zu verwenden. DirectAccess erfordert auch eine Sicherheitsgruppe für Windows 7-Client Computer für jeden Einstiegspunkt. Jeder Clientcomputer sollte nur in eine Sicherheitsgruppe aufgenommen werden. Daher sollten Sie sicherstellen, dass die Sicherheitsgruppen für Windows 10-und Windows 8-Clients nur Computer enthalten, auf denen Windows 10 oder Windows 8 ausgeführt wird, und dass jeder Windows 7-Client Computer zu einer einzelnen dedizierten Sicherheitsgruppe für den relevanten Einstiegspunkt gehört und dass keine Windows 10-oder Windows 8-Clients zu den Windows 7-Sicherheitsgruppen gehören.

Konfigurieren Sie die Windows 8-Sicherheitsgruppen auf der Seite **Gruppen auswählen** des Setup-Assistenten für den **DirectAccess-Client** . Konfigurieren Sie Windows 7-Sicherheitsgruppen auf der Seite **Client Unterstützung** des Assistenten zum **Aktivieren der Bereitstellung für mehrere Standorte** oder auf der Seite **Client Unterstützung** des Assistenten zum **Hinzufügen von Einstiegspunkten** .

## <a name="kerberos-proxy-authentication"></a>Kerberos-Proxyauthentifizierung
Der **Fehler wurde empfangen**. Die Kerberos-Proxy Authentifizierung wird in einer Bereitstellung mit mehreren Standorten nicht unterstützt. Sie müssen die Verwendung von Computerzertifikaten für IPsec-Benutzerauthentifizierung aktivieren.

**Ursache**

Die Computerzertifikatauthentifizierung muss vor dem Aktivieren der Funktionen für mehrere Standorte aktiviert werden.

**Lösung**

So konfigurieren Sie die Computerzertifikatauthentifizierung:

1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 2 **RAS-Server** auf **Bearbeiten**.

2.  Aktivieren Sie im Setup-Assistenten für den RAS-Server**** auf der Seite **Authentifizierung** das Kontrollkästchen **Computerzertifikate verwenden**, und wählen Sie die Stamm- oder Zwischenzertifizierungsstelle aus, von der Zertifikate in Ihrer Bereitstellung ausgestellt werden.

Verwenden Sie zum Aktivieren der Computer Zertifikat Authentifizierung mithilfe von Windows PowerShell das `Set-DAServer` Cmdlet, und geben Sie den Parameter *ipccrootcertificate* an.

## <a name="ip-https-certificates"></a>IP-HTTPS-Zertifikate
Der **Fehler wurde empfangen**. Der DirectAccess-Server verwendet ein selbst signiertes IP-HTTPS-Zertifikat. Konfigurieren Sie IP-HTTPS für die Verwendung eines signierten Zertifikats von einer bekannten Zertifizierungsstelle.

**Ursache**

Das IP-HTTPS-Zertifikat ist selbstsigniert. Sie können keine selbstsignierten Zertifikate in einer Bereitstellung für mehrere Standorte verwenden.

**Lösung**

So wählen Sie ein IP-HTTPS-Zertifikat aus:

1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 2 **RAS-Server** auf **Bearbeiten**.

2.  Stellen Sie sicher, dass im Setup-Assistenten für den RAS-Server **** auf der Seite **Netzwerkadapter** unter **Wählen Sie das Zertifikat aus, mit dem IP-HTTPS-Verbindungen authentifiziert werden:** das Kontrollkästchen **Selbstsigniertes Zertifikat verwenden, das von DirectAccess automatisch erstellt wurde** deaktiviert ist, und klicken Sie auf **Durchsuchen**, um ein von einer vertrauenswürdigen Zertifizierungsstelle ausgestelltes Zertifikat auszuwählen.

## <a name="network-location-server"></a>Netzwerkadressenserver

-   **Problem 1:**

    Der **Fehler wurde empfangen**. DirectAccess ist für die Verwendung eines selbst signierten Zertifikats für den Netzwerkadressen Server konfiguriert. Konfigurieren Sie den Netzwerkadressenserver für die Verwendung eines signierten Zertifikats von einer Zertifizierungsstelle.

    **Ursache**

    Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt und verwendet ein selbstsigniertes Zertifikat. Sie können keine selbstsignierten Zertifikate in einer Bereitstellung für mehrere Standorte verwenden.

    **Lösung**

    So wählen Sie ein Netzwerkadressenserver-Zertifikat aus:

    1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 3 **Infrastrukturserver** auf **Bearbeiten**.

    2.  Stellen Sie sicher, dass im **** Assistenten zum Einrichten des Infrastrukturservers auf der Seite **Netzwerkadressenserver** unter **Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt.** das Kontrollkästchen **Selbstsigniertes Zertifikat verwenden** deaktiviert ist, und klicken Sie auf **Durchsuchen**, um ein von einer Unternehmenszertifizierungsstelle ausgestelltes Zertifikat auszuwählen.

-   **Problem 2:**

    Der **Fehler wurde empfangen**. Zum Bereitstellen eines Clusters mit Netzwerk Lastenausgleich oder einer Bereitstellung mit mehreren Standorten müssen Sie ein Zertifikat für den Netzwerkadressen Server mit einem Antragsteller Namen abrufen, der sich vom internen Namen des RAS-Servers unterscheidet.

    **Ursache**

    Der Antragstellername des für die Netzwerkadressenserver-Website verwendeten Zertifikats stimmt mit dem internen Namen des RAS-Servers überein. Dadurch werden Probleme bei der Namensauflösung verursacht.

    **Lösung**

    Fordern Sie ein Zertifikat mit einem Antragstellernamen an, der sich vom internen Namen des RAS-Servers unterscheidet.

    So konfigurieren Sie den Netzwerkadressenserver:

    1.  Klicken Sie in der Remotezugriffs-Verwaltungskonsole im Detailbereich in Schritt 3 **Infrastrukturserver** auf **Bearbeiten**.

    2.  Klicken Sie im **** Assistenten zum Einrichten des Infrastrukturservers auf der Seite **Netzwerkadressenserver** unter **Der Netzwerkadressenserver wird auf dem RAS-Server bereitgestellt.** auf **Durchsuchen**, um das zuvor abgerufene Zertifikat auszuwählen. Das Zertifikat muss einen Antragstellernamen enthalten, der sich vom internen Namen des RAS-Servers unterscheidet.

## <a name="windows-7-client-computers"></a>Windows 7-Clientcomputer
Die **Warnung wurde empfangen**. Beim Aktivieren von Multisite dürfen die für DirectAccess-Clients konfigurierten Sicherheitsgruppen keine Windows 7-Computer enthalten. Wählen Sie eine Sicherheitsgruppe aus, die die Clients für die einzelnen Einstiegspunkte enthält, damit Clientcomputer mit Windows 7 in einer Bereitstellung mit mehreren Standorten unterstützt werden.

**Ursache**

In der vorhandenen DirectAccess-Bereitstellung wurde die Windows 7-Client Unterstützung aktiviert.

**Lösung**

DirectAccess erfordert mindestens eine Sicherheitsgruppe für alle Windows 8-Client Computer und eine Sicherheitsgruppe für Windows 7-Client Computer für jeden Einstiegspunkt. Jeder Clientcomputer sollte nur in eine Sicherheitsgruppe aufgenommen werden. Daher sollten Sie sicherstellen, dass die Sicherheitsgruppe für Windows 8-Clients nur Computer enthält, auf denen Windows 8 ausgeführt wird, und dass jeder Windows 7-Client Computer zu einer einzelnen dedizierten Sicherheitsgruppe für den relevanten Einstiegspunkt gehört und dass keine Windows 8-Clients zu den Windows 7-Sicherheitsgruppen gehören.

## <a name="active-directory-site"></a>Active Directory-Standort
Der **Fehler wurde empfangen**. Der Server <server_name> ist keinem Active Directory Standort zugeordnet.

**Ursache**

Von DirectAccess konnte der Active Directory-Standort nicht ermittelt werden. In der Konsole für Active Directory-Standorte und -Dienste können Sie die verschiedenen Subnetze für Ihr Netzwerk konfigurieren und die einzelnen Subnetze dem relevanten Active Directory-Standort zuweisen. Dieser Fehler kann auftreten, wenn die IP-Adresse des RAS-Servers zu keinem der Subnetze gehört oder wenn das Subnetz, zu dem die IP-Adresse gehört, keinem Active Directory-Standort zugeordnet ist.

**Lösung**

Überprüfen Sie, ob dies das Problem ist, indem Sie den Befehl `nltest /dsgetsite` auf dem RAS-Server ausführen. Ist dies das Problem, wird vom Befehl ERROR_NO_SITENAME zurückgegeben. Stellen Sie zum Beheben des Problems sicher, dass auf dem Domänencontroller ein Subnetz vorhanden ist, das die interne Server-IP-Adresse enthält und einem Active Directory-Standort zugeordnet ist.

## <a name="saving-server-gpo-settings"></a><a name="SaveGPOSettings"></a>Speichern der Server-GPO-Einstellungen
Der **Fehler wurde empfangen**. Fehler beim Speichern der Remote Zugriffs Einstellungen auf dem GPO-<GPO_name>.

**Ursache**

Änderungen am Server-GPO konnten aufgrund von Konnektivitätsproblemen oder einer Freigabe Verletzung in der Datei "Registry. Pol" nicht gespeichert werden, z. b. Wenn ein anderer Benutzer die Datei gesperrt hat.

**Lösung**

Stellen Sie sicher, dass Konnektivität zwischen dem RAS-Server und dem Domänencontroller besteht. Besteht Konnektivität, überprüfen Sie auf dem Domänencontroller, ob die Datei %%amp;quot;registry.pol%%amp;quot; durch einen anderen Benutzer gesperrt ist, und beenden Sie ggf. diese Benutzersitzung, um die Datei zu entsperren.

## <a name="internal-error-occurred"></a><a name="InternalServerError"></a>Interner Fehler
Der **Fehler wurde empfangen**. Interner Fehler.

**Ursache**

Dieser Fehler wird möglicherweise durch eine unerwartete Konfiguration der Einstiegspunkttabelle im Client-Gruppenrichtlinienobjekt verursacht. Dies kann passieren, wenn der Administrator DirectAccess-Client-Cmdlets zum Bearbeiten der Einstiegspunkttabelle im Client-Gruppenrichtlinienobjekt verwendet.

**Lösung**

Überprüfen Sie die Konfiguration der Einstiegspunkttabelle in allen Client-Gruppenrichtlinienobjekten, und beheben Sie alle Inkonsistenzen in der Konfiguration für mehrere Standorte zwischen den verschiedenen Instanzen der Client-Gruppenrichtlinienobjekte und der DirectAccess-Konfiguration. Verwenden Sie das `Get-DaEntryPointTableItem`-Cmdlet mit dem Namen des Client-Gruppenrichtlinienobjekts, um die Einstiegspunkttabelle für den Client abzurufen. Verwenden Sie das `Get-NetIPHttpsConfiguration`-Cmdlet, um alle IP-HTTPS-Profile für alle Einstiegspunkte abzurufen.

Weitere Informationen finden Sie unter [DirectAccess-Client-Cmdlets in Windows PowerShell](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj591658(v=ws.11)).

