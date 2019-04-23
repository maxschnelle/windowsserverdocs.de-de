---
title: Network File System bereitstellen
description: Beschreibt, wie Sie Network File System bereitstellen.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2f3671283720d515cd3e3e609d98e02343c15892
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59860771"
---
# <a name="deploy-network-file-system"></a>Network File System bereitstellen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Network File System (NFS) stellt eine dateifreigabelösung mit der Sie die Dateien zwischen PCs unter Windows Server und UNIX-Betriebssystemen, die über das NFS-Protokoll übertragen können. In diesem Thema beschreiben die Schritte, die Sie befolgen sollten, um NFS bereitzustellen.

## <a name="whats-new-in-network-file-system"></a>Neuerungen in Network File System

Hier ist, was für NFS unter Windows Server 2012 geändert wird:

- **Unterstützung für NFS-Version 4.1**. Diese Protokollversion enthält die folgenden Verbesserungen.
  - Navigieren in Firewalls ist einfacher, optimieren behindertengerechter Software.
  - Unterstützt die RPCSEC\_GSS-Protokoll, stärker integrierte Sicherheit bereitstellen und ermöglicht Clients und Servern, zum Aushandeln der Sicherheit.
  - Unterstützt die Semantik für UNIX und Windows-Datei.
  - Nutzt die Vorteile der Bereitstellung von gruppierten Dateiservern-Server.
  - WAN-freundlicher zusammengesetzte Prozeduren unterstützt.

- **NFS-Modul für Windows PowerShell**. Die Verfügbarkeit von integrierten NFS-Cmdlets erleichtert die Automatisierung verschiedener Vorgänge. Die Cmdlet-Namen sind konsistent mit anderen Windows PowerShell-Cmdlets (mit Verben wie "Get" und "Set"), erleichtert Ihnen die für Benutzer mit Windows PowerShell zu erfahren, wie Sie die neuen Cmdlets vertraut sind.
- **Verbesserungen bei NFS**. Eine neue Konsole für die zentrale Verwaltung der UI-basierten vereinfacht die Konfiguration und Verwaltung von SMB und NFS-Freigaben, Kontingente, dateiprüfungen und Klassifizierung zusätzlich zum Verwalten von gruppierten Dateiservern.
- **Zuordnen von Verbesserungen der Identität**. Neue Benutzeroberflächenautomatisierungs-Unterstützung und aufgabenbasierte von Microsoft Windows PowerShell-Cmdlets für die Konfiguration der identitätszuordnung, dadurch können Administratoren eine Quelle für identitätszuordnung schnell zu konfigurieren, und erstellen Sie einzelne zugeordnete Identitäten für Benutzer. Verbesserungen erleichtern es Administratoren, die zum Einrichten einer Freigabe für den Multi-Protocol-Zugriff über SMB und NFS.
- **Cluster-Resource Model Umstrukturierung**. Diese Verbesserung sorgt für Konsistenz zwischen dem Cluster-Resource-Modell für die Windows-NFS und SMB-Protokoll-Server und vereinfacht die Verwaltung. Für die NFS-Servern, die viele Freigaben aufweisen, das Failover im Netzwerk der Ressource und die Anzahl der WMI-Aufrufe, die erforderlich sind, ein Volume enthält, die eine große Anzahl von NFS-Freigaben reduziert werden.
- **Integration in fortsetzen Schlüssel Manager**. Der fortsetzen-Schlüssel-Manager ist eine Komponente, die verfolgt nach, Dateiserver und Dateisystem und die Windows SMB und NFS-Protokoll-Server für das Failover ohne Unterbrechung der Clients oder serveranwendungen, die ihre Daten auf dem Dateiserver speichern kann. Diese Verbesserung ist eine wichtige Komponente der Funktion fortlaufende Verfügbarkeit des Dateiservers mit Windows Server 2012 ausgeführt wird.

## <a name="scenarios-for-using-network-file-system"></a>Szenarien für die Verwendung von Network File System

NFS unterstützt eine gemischte Umgebung mit Windows-basierten und UNIX-basierten Betriebssystemen. Die folgenden Bereitstellungsszenarien sind Beispiele für wie Sie einen fortlaufend verfügbaren Dateiserver für Windows Server 2012 verwenden Sie stattdessen NFS bereitstellen können.

### <a name="provision-file-shares-in-heterogeneous-environments"></a>Bereitstellen von Dateifreigaben in heterogenen Umgebungen

Dieses Szenario gilt für Organisationen mit heterogenen Umgebungen, die von Windows und andere Betriebssysteme, wie z. B. UNIX- oder Linux-basierten Client bestehen aus Computern. In diesem Szenario können Sie über die sowohl von SMB- und NFS-Protokolle Multiprotokoll-Zugriff auf die gleiche Dateifreigabe bereitstellen. Wenn Sie einen Windows-Dateiserver in diesem Szenario bereitstellen, möchten Sie in der Regel zur Erleichterung der Zusammenarbeit zwischen Benutzern auf Windows und UNIX-basierte Computer. Wenn eine Dateifreigabe konfiguriert ist, sie sowohl die SMB- und NFS-Protokolle, für den Zugriff auf ihre Dateien über das SMB-Protokoll, Windows-Benutzer freigegeben ist, und auf UNIX-basierten Computern in der Regel Benutzerzugriff auf ihre Dateien über das NFS-Protokoll.

In diesem Szenario müssen Sie eine gültige Identität Zuordnungskonfiguration-Quelle verfügen. Windows Server 2012 unterstützt die folgenden Identitätsspeicher für die Zuordnung an:

- Zuordnungsdatei
- Active Directory-Domänendienste (AD DS)
- RFC 2307-kompatible LDAP speichert, z. B. Active Directory Lightweight Directory Services (AD LDS)
- Server des Benutzers-Namen zuordnen (UNM)

### <a name="provision-file-shares-in-unix-based-environments"></a>Bereitstellen von Dateifreigaben in UNIX-Umgebungen

In diesem Szenario werden die Windows-Dateiserver in einer hauptsächlich auf UNIX basierende Umgebung für UNIX-basierten Clientcomputer, auf den Zugriff auf die NFS-Dateifreigaben zu bereitgestellt. Eine Option für nicht zugeordnete UNIX User Access (UUUA) wurde ursprünglich für NFS-Freigaben in Windows Server 2008 R2 implementiert, damit, dass Windows Server können, zum Speichern von NFS-Daten verwendet werden ohne Erstellung von UNIX zu Windows Zuordnung berücksichtigen. UUUA kann Administratoren die schnelle Bereitstellung und Bereitstellen von NFS ohne kontozuordnung konfigurieren zu müssen. Wenn für NFS aktiviert wird, erstellt UUUA benutzerdefinierte Sicherheits-IDs (SIDs), um nicht zugeordnete Benutzer darzustellen. Zugeordnete Benutzerkonten verwenden die standardmäßigen Windows-Sicherheits-IDs (SIDs), und nicht zugeordneten Benutzer verwenden benutzerdefinierte NFS-SIDs.

## <a name="system-requirements"></a>Systemanforderungen

Server für NFS kann unter jeder Version von Windows Server 2012 installiert werden. Sie können NFS mit UNIX-basierten Computern verwenden, die ein NFS-Server oder NFS-Client ausgeführt werden, wenn dieser NFS-Server und Client-Implementierungen entsprechen mit einem der folgenden Protokollspezifikationen:

1. NFS-Version 4.1-Protokollspezifikation (gemäß RFC [5661](https://tools.ietf.org/html/rfc5661))
2. NFS-Version 3-Protokollspezifikation (gemäß RFC [1813](https://tools.ietf.org/html/rfc1813))
3. NFS Version 2 Protocol Specification (gemäß RFC [1094](https://tools.ietf.org/html/rfc1094))

## <a name="deploy-nfs-infrastructure"></a>Bereitstellen der NFS-Infrastruktur

Sie müssen die folgenden Computer bereitstellen, und verbinden Sie sie in einem lokalen Netzwerk (LAN):

- Eine oder mehrere Computer unter Windows Server 2012 auf dem Sie die beiden wichtigsten Dienste für NFS-Komponenten installieren möchten: Server für NFS- und Client für NFS. Sie können diese Komponenten auf demselben Computer oder auf verschiedenen Computern installieren.
- Eine oder mehrere UNIX-basierten Computern, die NFS-Server und NFS-Client-Software ausgeführt werden. Der UNIX-basierte Computer, der NFS-Server ausgeführt wird, hostet einen NFS-Dateifreigabe oder den Export, das von einem Computer zugegriffen werden kann, auf denen Windows Server 2012 als mit der-Client für NFS-Client ausgeführt wird. Sie können entweder in der gleichen UNIX-basierte Computer oder auf andere UNIX-basierten Computern wie gewünscht NFS-Server und Client-Software installieren.
- Ein Domänencontroller, auf der Funktionsebene von Windows Server 2008 R2 ausgeführt wird. Der Domänencontroller bietet Informationen zur Benutzerauthentifizierung und -Zuordnungen für die Windows-Umgebung.
- Wenn ein Domänencontroller nicht bereitgestellt wird, können Sie einen Server (Network Information Service, NIS), um Informationen zur Benutzerauthentifizierung für die UNIX-Umgebung bereitzustellen. Oder, falls gewünscht, können Sie von Kennwörtern und Gruppen-Dateien, die auf dem Computer gespeichert sind, die der User Name Mapping-Dienst ausgeführt wird.

### <a name="install-network-file-system-on-the-server-with-server-manager"></a>Installieren Sie Network File System, auf dem Server mit Server-Manager

1. Wählen Sie im Assistenten zum Hinzufügen von Rollen und Features unter "Serverrollen" die Option **Datei- und Speicherdienste** , falls diese nicht bereits installiert sind.
2. Klicken Sie unter **Datei- und iSCSI-Dienste**Option **Dateiserver** und **Server für NFS**. Wählen Sie **Features hinzufügen** ausgewählte NFS-Funktionen einschließen.
3. Wählen Sie **installieren** auf die NFS-Komponenten auf dem Server zu installieren.

### <a name="install-network-file-system-on-the-server-with-windows-powershell"></a>Installieren Sie Network File System, auf dem Server mit Windows PowerShell

1. Starten Sie Windows PowerShell. Klicken Sie auf der Taskleiste mit der rechten Maustaste auf das PowerShell-Symbol, und wählen Sie dann **Als Administrator ausführen**.
2. Führen Sie die folgenden Windows PowerShell-Befehle aus:

```PowerShell
Import-Module ServerManager
Add-WindowsFeature FS-NFS-Service
Import-Module NFS
```

## <a name="configure-nfs-authentication"></a>Konfigurieren der NFS-Authentifizierung

Wenn Sie die NFS-Version 4.1 und NFS-Version 3.0-Protokolle verwenden, müssen Sie die folgenden Optionen für Authentifizierung und Sicherheit.

- RPCSEC\_GSS
  - **krb5**. Verwendet das Kerberos V5-Protokoll zum Authentifizieren von Benutzern vor dem Gewähren des Zugriffs auf die Dateifreigabe.
  - **Krb5i**. Kerberos V5-Protokoll verwendet, für die Authentifizierung mit integritätsprüfung (Prüfsummen), die überprüft, ob die Daten nicht geändert wurde.
  - **Krb5p** verwendet das Kerberos V5-Protokoll, das Authentifizierung von NFS-Datenverkehr mit Verschlüsselung für den Datenschutz.
- AUTH\_SYS

Sie können auch auswählen, nicht zu Server-Autorisierung verwenden (AUTH\_SYS), die Ihnen die Möglichkeit, die nicht zugeordneten Benutzer den Zugriff zu ermöglichen. Bei Verwendung des Zugriffs von nicht zugeordneten Benutzer können Sie angeben, dass die nicht zugeordneten Benutzer Zugriff per UID / GID, der die Standardeinstellung ist, oder anonymen Zugriff zulassen.

Anweisungen zum Konfigurieren von NFS-Authentifizierung auf, die in der folgende Abschnitt erläutert wurde.

## <a name="create-an-nfs-file-share"></a>Erstellen einer Dateifreigabe für NFS

Sie können eine NFS-Dateifreigabe mithilfe von Server-Manager oder Windows PowerShell-NFS-Cmdlets erstellen.

### <a name="create-an-nfs-file-share-with-server-manager"></a>Erstellen einer NFS-Dateifreigabe mit Server-Manager

1. Melden Sie sich als Mitglied der lokalen Gruppe %%amp;quot;Administratoren%%amp;quot; beim Server an.
2. Der Server-Manager wird automatisch gestartet. Wenn sie nicht automatisch gestartet wird, wählen Sie **starten**, Typ **servermanager.exe**, und wählen Sie dann **Server-Manager**.
3. Wählen Sie auf der linken Seite **Datei- und Speicherdienste**, und wählen Sie dann **Freigaben**.
4. Wählen Sie **um eine Dateifreigabe zu erstellen, starten Sie den Assistenten für neue Serverfreigaben**.
5. Auf der **Profil auswählen** Seite, wählen Sie entweder **NFS-Freigabe – schnell** oder **NFS-Freigabe – erweitert**, und wählen Sie dann **Weiter**.
6. Auf der **Freigabeort** Seite, wählen Sie einen Server und ein Volume aus, und wählen **Weiter**.
7. Auf der **Freigabename** Seite aus, geben Sie einen Namen für die neue Freigabe, und wählen **Weiter**.
8. Auf der **Authentifizierung** Seite, geben Sie die Authentifizierungsmethode, die Sie für diese Freigabe verwenden möchten.
9. Auf der **Empfängern** Seite **hinzufügen**, und geben Sie dann den Host, Clientgruppe oder Netzgruppe, die Sie Berechtigungen für die Freigabe gewähren möchten.
10. In **Berechtigungen**, konfigurieren Sie den Typ der Zugriffssteuerung, die die Benutzer besitzen, und wählen Sie **OK**.
11. Auf der **Bestätigung** Seite, überprüfen Sie Ihre Konfiguration, und wählen **erstellen** die NFS-Dateifreigabe zu erstellen.

### <a name="windows-powershell-equivalent-commands"></a>Gleichwertige Windows PowerShell-Befehle

Das folgende Windows PowerShell-Cmdlet kann auch eine NFS-Freigabe-Datei erstellen (wobei `nfs1` ist der Name der Freigabe und `C:\\shares\\nfsfolder` ist der Dateipfad):

```PowerShell
New-NfsShare -name nfs1 -Path C:\shares\nfsfolder
```

### <a name="known-issue"></a>Bekanntes Problem
NFS-Version 4.1 können Sie die Dateinamen werden erstellt oder kopiert haben, verwenden ungültige Zeichen. Wenn Sie versuchen, die Dateien mit vi-Editor zu öffnen, wird als beschädigt angezeigt. Nicht speichern Sie die Datei von vi, umbenannt, verschieben oder Ändern von Berechtigungen. Vermeiden Sie ungültiges Zeichen.
