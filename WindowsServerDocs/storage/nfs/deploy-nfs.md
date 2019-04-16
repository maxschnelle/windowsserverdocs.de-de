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
ms.sourcegitcommit: fcc26ec5a2cc73b59c5752377b39c070d288655e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2018
ms.locfileid: "8976686"
---
# Network File System bereitstellen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, WindowsServer 2012

Network File System (NFS) stellt eine dateifreigabelösung, die Sie Dateien zwischen Computern unter Windows Server und UNIX-Betriebssystemen mithilfe des Protokolls NFS übertragen können. In diesem Thema wird beschrieben, die Schritte, die Sie ausführen müssen, um NFS bereitzustellen.

## Was ist neu in Network File System

Hier sehen Sie, was für NFS in Windows Server 2012 geändert wird:

- **Unterstützung für NFS Version 4.1**. Dieses Protokoll, Version enthalten die folgenden Verbesserungen.
  - Navigieren Firewalls ist einfacher, Verbesserung der Barrierefreiheit.
  - Unterstützt das RPCSEC\_GSS-Protokoll, bietet höhere Sicherheit und ermöglicht Clients und Servern, die Sicherheit auszuhandeln.
  - Unterstützt UNIX und Windows-Datei-Semantik.
  - Nutzt die Vorteile der Bereitstellung von gruppierten Datei-Server.
  - Unterstützt die WAN-freundliche zusammengesetzte Verfahren.

- **NFS-Modul für Windows PowerShell**. Die Verfügbarkeit von integrierten Cmdlets für NFS erleichtert die zahlreichen Vorgänge zu automatisieren. Die Cmdlet-Namen sind mit anderen Windows PowerShell-Cmdlets (mit Verben wie "Get" und "Set"), und vereinfacht für Benutzer mit Windows PowerShell Hinweise zur Verwendung der neuen Cmdlets vertraut.
- **NFS Management Verbesserungen**. Eine neue zentrale UI-basierte Management-Konsole vereinfacht die Konfiguration und Verwaltung von SMB und NFS Freigaben, Kontingente, dateiprüfungen und Einstufung, zusätzlich zur Verwaltung von gruppierten Dateiserver.
- **Verbesserungen Identität zuordnen**. Neue UI-Unterstützung und Task-basierte Windows PowerShell-Cmdlets zum Konfigurieren der Zuordnung ermöglicht Administratoren eine Identität Zuordnungsquelle schnell zu konfigurieren, und erstellen Sie einzelne zugeordnete Identitäten für Benutzer. Verbesserungen erleichtern Administratoren über NFS und SMB-Freigabe für den Zugriff über mehrere Protokolle einrichten.
- Das **Modell der Cluster-Ressourcen neu zu strukturieren**. Diese Verbesserung sorgt dafür, dass aus Gründen der Konsistenz zwischen dem Cluster-Ressource-Modell für die Windows-NFS und SMB-Protokoll-Server und vereinfacht die Verwaltung. Für NFS-Servern, die viele Aktien haben, ein Failover im Netzwerk Ressource und die Anzahl der WMI-Aufrufe erforderlich, ein Volume mit, die eine große Anzahl von NFS-Freigaben verringert werden.
- **Integration mit Resume-Schlüssel-Manager**. Fortsetzen Schlüssel-Manager ist eine Komponente, die verfolgt Dateiserver und Dateisystem und ermöglicht es Ihnen die Windows-SMB- und NFS Protokollserver Failover ohne Unterbrechung des Clients oder serveranwendungen, die ihre Daten auf dem Dateiserver zu speichern. Diese Verbesserung ist eine wichtige Komponente der Funktion kontinuierlicher Verfügbarkeit des Dateiservers mit Windows Server 2012.

## Szenarien für die Verwendung von Network File System

NFS unterstützt eine gemischte Umgebung von Windows-basierten und UNIX-basierten Betriebssystemen. Die folgenden Szenarien für die Bereitstellung sind Beispiele für wie Sie einen ständig verfügbaren Windows Server 2012-Dateiserver mit NFS bereitstellen können.

### Bereitstellen von Dateifreigaben in über heterogene Umgebungen

Dieses Szenario gilt für Unternehmen, die über heterogene Umgebungen, die von Windows und andere Betriebssysteme, z. B. UNIX oder Linux-basierten Client bestehen Computer. Bei diesem Szenario können Sie über die SMB- und die NFS Multi-Protokoll-Zugriff auf die gleiche Dateifreigabe bereitstellen. In der Regel, wenn Sie einen Windows-Dateiserver in diesem Szenario bereitstellen, möchten Sie Zusammenarbeit zwischen Benutzern unter Windows und UNIX-Computer zu erleichtern. Wenn eine Dateifreigabe konfiguriert ist, wird der gemeinsam mit Windows-Benutzer, die Zugriff auf ihre Dateien über das SMB-Protokoll mit der SMB und die NFS Protokolle verwendet, und Benutzer auf UNIX-Computern zugreifen ihre Dateien in der Regel über das NFS-Protokoll.

In diesem Szenario müssen Sie eine gültige Identität Zuordnung Source-Konfiguration. Windows Server 2012 unterstützt die folgenden Identität Zuordnung speichern:

- Zuordnungsdatei
- Active Directory-Domänendienste (AD DS)
- RFC 2307-kompatiblen LDAP speichert, z. B. Active Directory Lightweight Directory Services (ADLDS)
- Benutzer Namen Zuordnung (UNM) server

### Bereitstellen von Dateifreigaben in UNIX-basierten Umgebungen

In diesem Szenario werden Windows Server in einer Umgebung vorwiegend UNIX-basierte, um auf Dateifreigaben NFS für UNIX-Clientcomputern bereitgestellt. Eine Option nicht zugeordnete UNIX Benutzer Zugriff (UUUA) wurde anfänglich für NFS-Freigaben in Windows Server 2008 R2 implementiert, sodass Windows Server können, zum Speichern von NFS Daten verwendet werden ohne Erstellen UNIX-Windows-Zuordnung zu berücksichtigen. UUUA kann Administratoren schnell bereitstellen und Bereitstellen von NFS ohne Konto-Zuordnung zu konfigurieren. Wenn für NFS aktiviert wird, erstellt UUUA benutzerdefinierte Sicherheits-IDs (SIDs) auf nicht zugeordnete Benutzer darstellen. Zugeordnete Benutzerkonten standardmäßigen Windows-Sicherheits-IDs (SIDs), und nicht zugeordnete Benutzer benutzerdefinierte NFS SIDs.

## Systemanforderungen

Server für NFS kann auf eine beliebige Version von Windows Server 2012 installiert werden. Sie können NFS mit UNIX-Computer verwenden, die einen NFS-Server oder NFS-Client ausgeführt werden, wenn diese NFS-Server und Client-Implementierungen entsprechen mit einer der folgenden Protokollspezifikationen:

1. NFS 4.1 Protokoll Versionsspezifikation (wie in RFC [5661](https://tools.ietf.org/html/rfc5661)definiert)
2. NFS Version 3-Protokollspezifikation (wie in RFC [1813](https://tools.ietf.org/html/rfc1813)definiert)
3. Version 2-Protokoll-Spezifikation NFS (wie in RFC [1094](https://tools.ietf.org/html/rfc1094)definiert)

## Bereitstellen von NFS-Infrastruktur

Sie müssen die folgenden Computer bereitstellen, und verbinden Sie sie auf einem lokalen Netzwerk (LAN):

- Ein oder mehrere Computer unter Windows Server 2012 auf dem Sie die beiden wichtigsten Dienste für NFS-Komponenten installieren: Server für NFS und Client für NFS. Sie können diese Komponenten auf dem gleichen Computer oder auf verschiedenen Computern installieren.
- Eine oder mehrere UNIX-Computer, die Server für NFS und NFS-Client-Software ausgeführt werden. Die UNIX-basierten Computer mit Server für NFS hostet eine Dateifreigabe NFS oder exportieren, die von einem Computer zugegriffen werden kann, die Windows Server 2012 als Client über Client für NFS ausgeführt wird. Sie können entweder in demselben UNIX-basierten Computer oder auf verschiedenen UNIX-Computer nach Bedarf NFS-Server und Client-Software installieren.
- Ein Domänencontroller, die auf die Funktionsebene von Windows Server 2008 R2 ausgeführt wird. Der Domänencontroller enthält Informationen zur Benutzerauthentifizierung und die Zuordnung für die Windows-Umgebung.
- Wenn ein Domänencontroller nicht bereitgestellt wird, können Sie einen Server Network Information Service (NIS) verwenden, um Informationen zur Benutzerauthentifizierung für die UNIX-Umgebung bereitzustellen. Oder, falls gewünscht, können Sie Kennwort und Gruppe von Dateien, die auf dem Computer gespeichert sind, die der Benutzer Name Mapping-Dienst ausgeführt wird.

### Installieren Sie Network File System, auf dem Server mit Server-Manager

1. Wählen Sie aus dem Hinzufügen von Rollen und Features-Assistenten unter Serverrollen **Datei- und Speicherdienste** , wenn es nicht bereits installiert ist.
2. Unter **Datei- und iSCSI-Dienste**, **Dateiserver** und **Server für NFS**auszuwählen. Wählen Sie **Features hinzufügen** zum ausgewählten NFS umfasst.
3. Wählen Sie die Installation die NFS-Komponenten auf dem Server **Installieren** .

### Installieren Sie Network File System, auf dem Server mit Windows PowerShell

1. Starten Sie Windows PowerShell. Mit der rechten Maustaste in des PowerShell-Symbols auf der Taskleiste, und wählen Sie **als Administrator ausführen**.
2. Führen Sie die folgenden Windows PowerShell-Befehle aus:

```PowerShell
Import-Module ServerManager
Add-WindowsFeature FS-NFS-Service
Import-Module NFS
```

## Konfigurieren der Authentifizierung für NFS

Wenn Sie die NFS Version 4.1 und NFS Version 3.0 zu verwenden, müssen Sie die folgenden Optionen für die Authentifizierung und Sicherheit.

- RPCSEC\_GSS
  - **Krb5**. Verwendet das Kerberos 5-Protokoll zum Authentifizieren von Benutzern vor dem Zugriff auf die Dateifreigabe.
  - **Krb5i**. Verwendet Kerberos 5-Protokoll zum Authentifizieren von mit Integrität überprüfen (Prüfsummen), die überprüft, dass die Daten nicht geändert wurde.
  - **Krb5p** Wird verwendet, Kerberos-Version 5-Protokoll, das NFS Datenverkehr mit Verschlüsselung für Datenschutz authentifiziert.
- AUTH\_SYS

Sie können auch auswählen, nicht auf Server-Autorisierung (AUTH\_SYS), bietet die Möglichkeit, nicht zugeordnete den Benutzerzugriff zu ermöglichen. Wenn Sie nicht zugeordnete Benutzer den Zugriff zu verwenden, Sie können angeben, nicht zugeordnete Benutzerzugriff von Benutzer-ID / Gruppen-ID, die ist die Standardeinstellung oder anonymen Zugriff erlauben.

Anweisungen zum Konfigurieren von NFS-Authentifizierung auf im folgenden Abschnitt erläutert.

## Erstellen Sie eine Dateifreigabe für NFS

Sie können eine NFS Dateifreigabe mit Server-Manager oder NFS von Windows PowerShell-Cmdlets erstellen.

### Erstellen Sie eine Dateifreigabe NFS mit Server-Manager

1. Melden Sie sich als Mitglied der lokalen Gruppe Administratoren auf dem Server.
2. Server-Manager wird automatisch gestartet. Wenn es nicht automatisch gestartet wird, wählen Sie **Starten**, geben Sie **servermanager.exe**, und wählen Sie dann die **Server-Manager**.
3. Klicken Sie auf der linken Seite Wählen Sie **Datei- und Speicherdienste**, und wählen Sie dann die **Freigaben**.
4. Wählen Sie **zum Erstellen einer Dateifreigabe Starten des Assistenten für neue Teilen**.
5. Wählen Sie auf der Seite **Profil auswählen** **NFS-Freigabe – schnell** oder **NFS-Freigabe - Advanced**, und wählen Sie dann **Weiter**.
6. Klicken Sie auf der Seite **Freigabe** wählen Sie eines Servers und ein Volume aus, und wählen Sie **Weiter**.
7. Klicken Sie auf der Seite **Name Teilen** Geben Sie einen Namen für die neue Bereitstellungsfreigabe, und wählen Sie **Weiter**.
8. Geben Sie auf der Seite der **Authentifizierung** die Authentifizierungsmethode, die Sie für diese Freigabe verwenden möchten.
9. Wählen Sie auf der Seite **Freigabeberechtigungen** **Hinzufügen**, und geben Sie dann den Host, Clientgruppe oder Netgroup Berechtigung für die Freigabe werden soll.
10. Konfigurieren Sie in den **Berechtigungen**, welche Art von Zugriffssteuerung, die die Benutzer haben sollen, und klicken Sie auf **OK**.
11. Klicken Sie auf **der Bestätigungsseite** überprüfen Sie die Konfiguration, und wählen Sie **Erstellen** , um die NFS-Dateifreigabe zu erstellen.

### Entsprechende Windows PowerShell-Befehle

Die folgenden Windows PowerShell-Cmdlet kann auch eine Dateifreigabe NFS erstellen (, in denen `nfs1` ist der Name der Freigabe und `C:\\shares\\nfsfolder` ist der Pfad):

```PowerShell
New-NfsShare -name nfs1 -Path C:\shares\nfsfolder
```

### Bekanntes Problem
NFS Version 4.1 ermöglicht die Dateinamen werden erstellt oder ungültige Zeichen mit kopiert. Wenn Sie versuchen, die Dateien mit vi-Editor öffnen, wird als fehlerhaft angezeigt. Nicht speichern Sie die Datei von vi, umbenennen, verschieben oder Berechtigungen ändern. Vermeiden Sie ungültiges Zeichen.
