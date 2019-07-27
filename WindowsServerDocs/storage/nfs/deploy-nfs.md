---
title: Network File System bereitstellen
description: Beschreibt, wie das Netzwerkdatei System bereitgestellt wird.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: cc02f0a82b4143b80fc1107a63d234b117502d2d
ms.sourcegitcommit: 6f968368c12b9dd699c197afb3a3d13c2211f85b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/26/2019
ms.locfileid: "68544649"
---
# <a name="deploy-network-file-system"></a>Network File System bereitstellen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Network File System (NFS) stellt eine Dateifreigabe Lösung bereit, mit der Sie Dateien zwischen Computern mit Windows Server-und UNIX-Betriebssystemen mithilfe des NFS-Protokolls übertragen können. In diesem Thema werden die Schritte beschrieben, die Sie zum Bereitstellen von NFS befolgen sollten.

## <a name="whats-new-in-network-file-system"></a>Neues im Netzwerkdatei System

Hier finden Sie eine Änderung für NFS in Windows Server 2012:

- **Unterstützung für NFS-Version 4,1**. Diese Protokollversion umfasst die folgenden Erweiterungen.
  - Die Navigation in Firewalls ist einfacher und verbessert die Barrierefreiheit.
  - Unterstützt das rpcsec\_-GSS-Protokoll, das eine stärkere Sicherheit bietet und Clients und Servern die Aushandlung der Sicherheit ermöglicht.
  - Unterstützt die Datei Semantik von UNIX und Windows.
  - Nutzt Cluster Dateiserver-bereit Stellungen.
  - Unterstützt WAN-freundliche Verbund Prozeduren.

- **NFS-Modul für Windows PowerShell**. Die Verfügbarkeit integrierter NFS-Cmdlets vereinfacht die Automatisierung verschiedener Vorgänge. Die Cmdlet-Namen sind mit anderen Windows PowerShell-Cmdlets konsistent (Verwendung von Verben wie "Get" und "Set"), sodass Benutzer, die mit Windows PowerShell vertraut sind, die Verwendung neuer Cmdlets erleichtern.
- **Verbesserungen der NFS-Verwaltung** Eine neue zentralisierte, auf der Benutzeroberfläche basierende Verwaltungskonsole vereinfacht die Konfiguration und Verwaltung von SMB-und NFS-Freigaben, Kontingenten, Datei Bildschirmen und Klassifizierungen sowie das Verwalten von gruppierten Dateiservern.
- **Verbesserungen der Identitäts Zuordnung**. Neue Benutzeroberflächen Unterstützung und Task basierte Windows PowerShell-Cmdlets zum Konfigurieren der Identitäts Zuordnung, mit deren Hilfe Administratoren schnell eine Identitäts Zuordnungsquelle konfigurieren und dann individuelle zugeordnete Identitäten für Benutzer erstellen können. Durch Verbesserungen können Administratoren auf einfache Weise eine Freigabe für den Zugriff auf mehrere Protokolle über NFS und SMB einrichten.
- **Umstrukturierung des Cluster Ressourcen Modells**. Diese Verbesserung sorgt für Konsistenz zwischen dem Cluster Ressourcenmodell für die Windows NFS-und SMB-Protokollserver und vereinfacht die Verwaltung. Bei NFS-Servern mit vielen Freigaben wird das Ressourcennetzwerk und die Anzahl der erforderlichen WMI-Aufrufe für ein Volume mit einer großen Anzahl von NFS-Freigaben reduziert.
- **Integration in den Resume-Schlüssel-Manager**. Der Schlüssel-Manager für fortsetzen ist eine Komponente, die den Dateiserver-und Dateisystem Status nachverfolgt und es den Windows-SMB-und NFS-Protokoll Servern ermöglicht, ein Failover durchführen, ohne dass Clients oder Server Anwendungen, die Ihre Daten auf dem Diese Verbesserung ist eine wichtige Komponente der Funktion für fortlaufende Verfügbarkeit des Dateiservers, auf dem Windows Server 2012 ausgeführt wird.

## <a name="scenarios-for-using-network-file-system"></a>Szenarien für die Verwendung des Netzwerkdatei Systems

NFS unterstützt eine gemischte Umgebung von Windows-basierten und UNIX-basierten Betriebssystemen. In den folgenden Bereitstellungs Szenarien finden Sie Beispiele für die Bereitstellung eines fortlaufend verfügbaren Windows Server 2012-Dateiservers mithilfe von NFS.

### <a name="provision-file-shares-in-heterogeneous-environments"></a>Bereitstellen von Dateifreigaben in heterogenen Umgebungen

Dieses Szenario gilt für Organisationen mit heterogenen Umgebungen, die sowohl aus Windows als auch aus anderen Betriebssystemen bestehen, z. b. UNIX-oder Linux-basierten Client Computern. In diesem Szenario können Sie den Zugriff auf die gleiche Dateifreigabe über das SMB-und NFS-Protokoll auf dieselbe Dateifreigabe gewähren. Wenn Sie in diesem Szenario einen Windows-Dateiserver bereitstellen, möchten Sie in der Regel die Zusammenarbeit zwischen Benutzern auf Windows-und UNIX-basierten Computern vereinfachen. Wenn eine Dateifreigabe konfiguriert ist, wird Sie sowohl für SMB-als auch für NFS-Protokolle freigegeben, wobei Windows-Benutzer über das SMB-Protokoll auf Ihre Dateien zugreifen und Benutzer auf UNIX-basierten Computern in der Regel über das NFS-Protokoll auf Ihre Dateien zugreifen.

Für dieses Szenario benötigen Sie eine gültige Konfiguration der Identitäts Zuordnung. Windows Server 2012 unterstützt die folgenden Identitäts Mapping-Speicher:

- Mapping-Datei
- Active Directory-Domänendienste (AD DS)
- RFC 2307-kompatible LDAP-Speicher wie z. b. Active Directory Lightweight Directory Services (AD LDS)
- Benutzernamenzuordnung (unm)-Server

### <a name="provision-file-shares-in-unix-based-environments"></a>Bereitstellen von Dateifreigaben in UNIX-basierten Umgebungen

In diesem Szenario werden Windows-Dateiserver in einer vorwiegend UNIX-basierten Umgebung bereitgestellt, um den Zugriff auf NFS-Dateifreigaben für UNIX-basierte Client Computer zu ermöglichen. Eine nicht zugeordnete UUUA-Option (Unix User Access) wurde anfänglich für NFS-Freigaben in Windows Server 2008 R2 implementiert, sodass Windows-Server zum Speichern von NFS-Daten ohne Erstellen einer UNIX-zu-Windows-Konto Zuordnung verwendet werden können. Mit UUUA können Administratoren schnell NFS bereitstellen und bereitstellen, ohne die Konto Zuordnung konfigurieren zu müssen. Wenn Sie für NFS aktiviert ist, erstellt UUUA benutzerdefinierte Sicherheits-IDs (SIDs), die nicht zugeordnete Benutzer darstellen. Zugeordnete Benutzerkonten verwenden standardmäßige Windows-Sicherheits-IDs (SIDs), und nicht zugeordnete Benutzer verwenden benutzerdefinierte NFS-SIDs.

## <a name="system-requirements"></a>Systemanforderungen

Server für NFS kann unter jeder Version von Windows Server 2012 installiert werden. Sie können NFS mit UNIX-basierten Computern verwenden, auf denen ein NFS-Server oder ein NFS-Client ausgeführt wird, wenn diese NFS-Server-und Client Implementierungen eine der folgenden Protokoll Spezifikationen erfüllen:

1. NFS-Version 4,1-Protokollspezifikation (wie in RFC [5661](https://tools.ietf.org/html/rfc5661)definiert)
2. NFS, Version 3, Protokollspezifikation (wie in RFC [1813](https://tools.ietf.org/html/rfc1813)definiert)
3. NFS, Version 2, Protokollspezifikation (wie in RFC [1094](https://tools.ietf.org/html/rfc1094)definiert)

## <a name="deploy-nfs-infrastructure"></a>NFS-Infrastruktur bereitstellen

Sie müssen die folgenden Computer bereitstellen und die Verbindung mit einem LAN (Local Area Network) herstellen:

- Auf einem oder mehreren Computern, auf denen Windows Server 2012 ausgeführt wird, auf dem Sie die beiden Haupt Dienste für NFS-Komponenten installieren: Server für NFS und Client für NFS. Sie können diese Komponenten auf demselben Computer oder auf unterschiedlichen Computern installieren.
- Mindestens ein UNIX-basierter Computer, auf dem NFS-Server und NFS-Client Software ausgeführt werden. Der UNIX-basierte Computer, auf dem der NFS-Server ausgeführt wird, hostet eine NFS-Dateifreigabe oder einen-Export, auf die von einem Computer mit Windows Server 2012 als Client mit Client für NFS zugegriffen wird. Sie können NFS-Server und-Client Software wie gewünscht entweder auf demselben UNIX-basierten Computer oder auf verschiedenen UNIX-basierten Computern installieren.
- Ein Domänen Controller, der auf der Windows Server 2008 R2-Funktionsebene ausgeführt wird. Der Domänen Controller stellt Benutzer Authentifizierungsinformationen und die Zuordnung für die Windows-Umgebung bereit.
- Wenn ein Domänen Controller nicht bereitgestellt wird, können Sie einen Netzwerkinformationsdienst (NIS)-Server verwenden, um Benutzer Authentifizierungsinformationen für die UNIX-Umgebung bereitzustellen. Wenn Sie möchten, können Sie auch Kenn Wort-und Gruppen Dateien verwenden, die auf dem Computer gespeichert sind, auf dem der Benutzernamenzuordnung-Dienst ausgeführt wird.

### <a name="install-network-file-system-on-the-server-with-server-manager"></a>Installieren Sie das Netzwerkdatei System auf dem Server mit Server-Manager

1. Wählen Sie im Assistenten zum Hinzufügen von Rollen und Features unter "Serverrollen" die Option **Datei- und Speicherdienste** , falls diese nicht bereits installiert sind.
2. Wählen Sie unter **Datei-und iSCSI-Dienste**die Option **Datei Server** und **Server für NFS aus**. Wählen Sie **Features hinzufügen** aus, um ausgewählte NFS-Features einzubeziehen.
3. Wählen Sie **Installieren** aus, um die NFS-Komponenten auf dem Server zu installieren.

### <a name="install-network-file-system-on-the-server-with-windows-powershell"></a>Installieren des Netzwerkdatei Systems auf dem Server mit Windows PowerShell

1. Starten Sie Windows PowerShell. Klicken Sie auf der Taskleiste mit der rechten Maustaste auf das PowerShell-Symbol, und wählen Sie dann **Als Administrator ausführen**.
2. Führen Sie die folgenden Windows PowerShell-Befehle aus:

```PowerShell
Import-Module ServerManager
Add-WindowsFeature FS-NFS-Service
Import-Module NFS
```

## <a name="configure-nfs-authentication"></a>Konfigurieren der NFS-Authentifizierung

Bei Verwendung der Protokolle NFS, Version 4,1 und NFS, Version 3,0 haben Sie die folgenden Authentifizierungs-und Sicherheitsoptionen.

- RPCSEC\_-GSS
  - **krb5**. Verwendet das Kerberos 5-Protokoll, um Benutzer zu authentifizieren, bevor Sie Zugriff auf die Dateifreigabe gewähren.
  - **Krb5i**. Verwendet das Kerberos 5-Protokoll für die Authentifizierung bei der Integritäts Überprüfung (Prüfsummen), mit der überprüft wird, ob die Daten nicht geändert wurden.
  - **Krb5p** Verwendet das Kerberos-Protokoll, Version 5, das NFS-Datenverkehr mit Verschlüsselung für den Datenschutz authentifiziert.
- AUTORISIERUNG\_(SYS)

Sie können auch festlegen, dass die Server Autorisierung (auth\_sys) nicht verwendet werden soll. dadurch haben Sie die Möglichkeit, nicht zugeordneten Benutzer Zugriff zu aktivieren. Bei Verwendung des nicht zugeordneten Benutzer Zugriffs können Sie angeben, dass der Zugriff nicht zugeordneter Benutzer mit UID/GID zulässig ist (Standardeinstellung) oder anonymen Zugriff zulässt.

Anweisungen zum Konfigurieren der NFS-Authentifizierung, die im folgenden Abschnitt erläutert werden.

## <a name="create-an-nfs-file-share"></a>Erstellen einer NFS-Dateifreigabe

Sie können eine NFS-Dateifreigabe erstellen, indem Sie entweder Server-Manager oder Windows PowerShell-NFS-Cmdlets verwenden.

### <a name="create-an-nfs-file-share-with-server-manager"></a>Erstellen einer NFS-Dateifreigabe mit Server-Manager

1. Melden Sie sich als Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; beim Server an.
2. Der Server-Manager wird automatisch gestartet. Wenn Sie nicht automatisch gestartet wird, wählen Sie **Start**, geben Sie **ServerManager. exe**ein, und wählen Sie dann **Server-Manager**aus.
3. Wählen Sie auf der linken Seite **Datei-und Speicherdienste**aus, und wählen Sie dann Freigaben **aus.**
4. Wählen Sie **eine Dateifreigabe aus, und starten Sie den Assistenten für neue**Freigaben.
5. Wählen Sie auf der Seite **Profil auswählen** entweder **NFS-Freigabe – schnell** oder **NFS-Freigabe-erweitert**aus, und klicken Sie dann auf **weiter**.
6. Wählen Sie  auf der Seite freigabeort einen Server und ein Volume aus, und klicken Sie auf **weiter**.
7. Geben Sie auf der Seite **Freigabe Name** einen Namen für die neue Freigabe an, und klicken Sie auf **weiter**.
8. Geben Sie auf der Seite **Authentifizierung** die Authentifizierungsmethode an, die Sie für diese Freigabe verwenden möchten.
9. Wählen Sie auf der Seite **Freigabe Berechtigungen** die Option **Hinzufügen**aus, und geben Sie dann den Host, die Clientgruppe oder die Netzwerkgruppe an, der Sie die Berechtigung für die Freigabe erteilen möchten.
10. Konfigurieren Sie unter **Berechtigungen**den Typ der Zugriffs Steuerung, den die Benutzer haben sollen, und wählen Sie **OK**aus.
11. Überprüfen Sie die Konfiguration auf der Seite **Bestätigung** , und wählen Sie **Erstellen** aus, um die NFS-Dateifreigabe zu erstellen.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle

Mit dem folgenden Windows PowerShell-Cmdlet kann auch eine NFS-Dateifreigabe `nfs1` erstellt werden (wobei der Name der `C:\\shares\\nfsfolder` Freigabe und der Dateipfad ist):

```PowerShell
New-NfsShare -name nfs1 -Path C:\shares\nfsfolder
```

### <a name="known-issue"></a>Bekanntes Problem
In der NFS-Version 4,1 können die Dateinamen mit unzulässigen Zeichen erstellt oder kopiert werden. Wenn Sie versuchen, die Dateien mit dem VI-Editor zu öffnen, wird als beschädigt angezeigt. Sie können die Datei nicht aus VI speichern, umbenennen oder verschieben oder Berechtigungen ändern. Vermeiden Sie die Verwendung ungültiger Zeichen.
