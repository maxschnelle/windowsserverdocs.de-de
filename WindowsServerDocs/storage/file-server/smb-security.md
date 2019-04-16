---
title: SMB-Verbesserungen der Sicherheit
description: Eine Erläuterung des Features in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016 SMB-Verschlüsselung.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 831ca8266c3ec18ffb83227dcb2d39b3f953ad1a
ms.sourcegitcommit: 375e94dc70c76e7aa5679c32f0f4dbc26cf7dd83
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/10/2018
ms.locfileid: "2233526"
---
# <a name="smb-security-enhancements"></a>SMB-Verbesserungen der Sicherheit

>Betrifft: Windows Server 2012 R2, WindowsServer 2012 und WindowsServer 2016

In diesem Thema wird erläutert, die SMB-sicherheitsverbesserungen in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.

## <a name="smb-encryption"></a>SMB-Verschlüsselung

SMB-Verschlüsselung bietet eine End-to-End-Verschlüsselung der SMB-Daten und Daten aus zur Vermeidung von Abhör-Vorkommen in nicht vertrauenswürdigen Netzwerken geschützt. Sie können SMB-Verschlüsselung mit minimalem Aufwand bereitstellen, aber möglicherweise kleine zusätzliche Kosten für spezielle Hardware oder Software erforderlich. Es wurde keine Anforderungen für die internetprotokollsicherheit (IPsec) oder WAN-Beschleuniger. SMB-Verschlüsselung kann für einzelne pro freigeben oder für die gesamte Dateiserver konfiguriert werden, und es kann für eine Vielzahl von Szenarien, in dem Daten nicht vertrauenswürdige Netzwerken durchläuft, aktiviert werden.

>[!NOTE]
>SMB-Verschlüsselung deckt nicht Sicherheit im Ruhezustand, der in der Regel von BitLocker Drive Encryption verwaltet wird.

SMB-Verschlüsselung muss für jedes Szenario berücksichtigt werden, in dem vertrauliche Daten vor Man-in-the-Middle-Angriffen geschützt werden müssen. Gibt die folgenden mögliche Szenarien:

- Ein Information-Worker vertrauliche Daten werden mithilfe des SMB-Protokolls verschoben. SMB-Verschlüsselung bietet eine End-to-End-Datenschutz und Integrität Assurance zwischen dem Dateiserver und dem Client, unabhängig von den Netzwerken durchlaufen, wie etwa wide Area Network (WAN) Verbindungen, die von Anbietern nicht von Microsoft verwaltet werden.
- SMB 3.0 ermöglicht Dateiserver, ständig verfügbaren Speicher für Server-Anwendungen, wie SQL Server oder Hyper-V bereitzustellen. Aktivieren der SMB-Verschlüsselung bietet die Möglichkeit, die betreffenden Informationen vor snooping Angriffen geschützt. SMB-Verschlüsselung ist einfacher zu verwenden als dedizierter Hardware-Lösungen, die für die meisten Storage Area Networks (SANs) erforderlich sind.

>[!IMPORTANT]
>Beachten Sie, dass es ist eine wichtige Leistung Betriebskosten mit alle End-to-End-Verschlüsselung Protection im Vergleich zu nicht verschlüsselt.

## <a name="enable-smb-encryption"></a>Aktivieren der SMB-Verschlüsselung

Sie können SMB-Verschlüsselung für die gesamte Datei-Server oder nur für bestimmte Dateifreigaben aktivieren. Verwenden Sie eine der folgenden Verfahren zum Aktivieren der SMB-Verschlüsselung:

### <a name="enable-smb-encryption-with-windows-powershell"></a>Aktivieren der SMB-Verschlüsselung mit Windows PowerShell

1. Geben Sie das folgende Skript zum Aktivieren der SMB-Verschlüsselung für eine einzelne Dateifreigabe auf dem Server:
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. Geben Sie das folgende Skript auf dem Server, um SMB-Verschlüsselung für die gesamte Datei-Server zu aktivieren:
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. Zum Erstellen einer neuen Dateifreigabe SMB mit SMB-Verschlüsselung aktiviert ist, geben Sie das folgende Skript ein:
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>Aktivieren der SMB-Verschlüsselung mit dem Server-Manager

1. Öffnen Sie im Server-Manager, **Datei und Storage Services**.
2. Wählen Sie **Freigaben** , die Freigaben Management-Seite zu öffnen.
3. Mit der rechten Maustaste der Freigabe, auf der Sie SMB-Verschlüsselung aktivieren möchten, und wählen Sie dann **Eigenschaften**aus.
4. Wählen Sie auf der Seite **Einstellungen** der Freigabe **Verschlüsseln Datenzugriff**ein. Zugriff auf das Verzeichnis Remotedatei wird verschlüsselt.

### <a name="considerations-for-deploying-smb-encryption"></a>Überlegungen für die Bereitstellung von SMB-Verschlüsselung

In der Standardeinstellung bei aktivierter SMB-Verschlüsselung für eine Dateifreigabe oder Server, nur SMB 3.0 Clients dürfen die angegebenen Dateifreigaben zugreifen. Erzwingt die Absicht des Administrators Schützen der Daten für alle Clients, die Freigaben zugreifen. Allerdings kann unter bestimmten Umständen möchte ein Administrator unverschlüsselte Zugriff für Clients zu ermöglichen, die SMB 3.0 (beispielsweise Übergangsphase bei gemischten Betriebssystem Clientversionen verwendet werden) nicht unterstützt. Um unverschlüsselte Zugriff für Clients zu ermöglichen, die keine SMB 3.0 unterstützen, geben Sie in Windows PowerShell das folgende Skript ein:

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

Die sichere Dialekt Aushandlung-Funktion im nächsten Abschnitt beschrieben wird verhindert, dass einen Man-in-the-Middle-Angriff downgraden eine Verbindung von SMB 3.0 mit SMB 2.0 (die unverschlüsselte Zugriff verwenden). Es verhindert keine Herabstufung auf SMB 1.0, jedoch die unverschlüsselte Access auch führen würde. Um sicherzustellen, dass SMB 3.0-Clients immer SMB-Verschlüsselung auf verschlüsselte Freigaben zugreifen verwenden, müssen Sie den Server SMB 1.0 deaktivieren. (Anleitung finden Sie im Abschnitt [Deaktivieren SMB 1.0](#disabling-smb-1.0).) Wenn die Einstellung **RejectUnencryptedAccess –** die Standardeinstellung **$true**bleibt, dürfen nur Verschlüsselung-fähige SMB 3.0 Clients Dateifreigaben zugreifen (SMB 1.0-Clients werden auch abgelehnt).

>[!NOTE]
>* SMB-Verschlüsselung wird der erweiterte Verschlüsselung AES (Standard)-CCM-Algorithmus zum Verschlüsseln und Entschlüsseln der Daten. AES-CCM bietet außerdem die Validierung der Datenintegrität (Anmelden) für verschlüsselte Dateifreigaben, unabhängig von der signierenden SMB-Einstellungen. Wenn Sie ohne Verschlüsselung Signieren SMB aktivieren möchten, können Sie weiterhin dazu. Weitere Informationen finden Sie unter [Der Grundlagen der SMB-Signaturen](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/).
>* Probleme können auftreten, wenn Sie versuchen, den Zugriff auf die Dateifreigabe oder Server, wenn Ihre Organisation wide Area Network (WAN) Acceleration Appliances verwendet.
>* Mit einer Standardkonfiguration (wobei kein unverschlüsselte Zugriff auf verschlüsselte Dateifreigaben zulässig ist), wenn Clients, die keine Unterstützung für SMB 3.0 versucht wird, eine verschlüsselte Dateifreigabe, Ereignis-ID 1003 zuzugreifen, im Ereignisprotokoll von Microsoft-Windows-SmbServer/operationale angemeldet ist , und der Client erhält eine Fehlermeldung **Zugriff verweigert** .
>* SMB-Verschlüsselung und die Encrypting File System (EFS) im NTFS-Dateisystem sind damit nicht zusammenhängenden und SMB-Verschlüsselung nicht erforderlich oder mithilfe von EFS abhängig ist.
>* SMB-Verschlüsselung und die BitLocker Drive Encryption sind damit nicht zusammenhängenden und SMB-Verschlüsselung nicht erforderlich oder mit BitLocker Drive Encryption abhängig ist.

## <a name="secure-dialect-negotiation"></a>Sichere Dialekt Aushandlung

SMB 3.0 kann Man-in-the-Middle-Angriffe, die versuchen, das Protokoll SMB 2.0 oder SMB 3.0 oder die Funktionen, die dem Client und Server verhandeln downgraden erkennen. Wenn vom Client oder Server ein solchen Angriff erkannt wird, wird die Verbindung getrennt und Ereignis-ID 1005 wird im Ereignisprotokoll Microsoft-Windows-SmbServer/operationale protokolliert. Secure Dialekt Aushandlung nicht feststellen oder zu verhindern, dass Downgrades von SMB 2.0 oder 3.0 SMB 1.0. Aus diesem Grund und der volle Funktionsumfang SMB-Verschlüsselung nutzen wird dringend empfohlen, dass Sie den SMB 1.0-Server deaktivieren. Weitere Informationen finden Sie unter [Deaktivieren SMB 1.0](#disabling-smb-1.0).

Die sichere Dialekt Aushandlung-Funktion, die im nächsten Abschnitt beschrieben wird verhindert, dass einen Man-in-the-Middle-Angriff downgraden SMB 3 eine Verbindung mit SMB-2 (die unverschlüsselte Zugriff verwenden). Es verhindert nicht Downgrades SMB-1, jedoch die unverschlüsselte Access auch führen würde. Weitere Informationen zu potenziellen Problemen mit zuvor nicht-Windows Implementierungen von SMB finden Sie im [Microsoft Knowledge Base](http://support.microsoft.com/kb/2686098).

## <a name="new-signing-algorithm"></a>Neue Signaturalgorithmus

SMB 3.0 verwendet einen neueren Verschlüsselungsalgorithmus zum Signieren: Erweiterte Verschlüsselung AES (Standard) - Verschlüsselungsanbieter - basierte Message Authentication Code (CMAC). SMB 2.0 verwendet den älteren HMAC-SHA256-Verschlüsselungsalgorithmus. AES-CMAC und AES-CCM beschleunigen können erheblich Verschlüsselung von Daten auf die meisten modernen CPUs, die AES-Anweisung unterstützen. Weitere Informationen finden Sie unter [Der Grundlagen der SMB-Signaturen](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/).

## <a name="disabling-smb-10"></a>Deaktivieren von SMB 1.0

Die Vorversion Computersuchdienst und Remote Administration Protocol-Features in SMB 1.0 unterscheiden sich jetzt und gelöscht werden können. Diese Funktionen sind weiterhin in der Standardeinstellung aktiviert, aber wenn Sie ältere SMB-Clients wie beispielsweise Computern unter Windows Server 2003 oder Windows XP keine können Sie die SMB 1.0-Features zur Verbesserung der Sicherheit und potenziell reduzieren Patchen entfernen.

>[!NOTE]
>SMB 2.0 wurde in Windows Server 2008 und Windows Vista eingeführt. SMB 2.0 unterstützt ältere Clients wie beispielsweise Computern unter Windows Server 2003 oder Windows XP nicht; und daher, diese werden nicht auf zugreifen Dateifreigaben oder Drucken von Freigaben, bei der Server SMB 1.0 deaktiviertem kann. Darüber hinaus einige nicht - Microsoft SMB-Clients möglicherweise nicht 2.0 SMB-Dateifreigaben zugreifen oder Drucken von Freigaben (beispielsweise Drucker mit "Scan-Freigabe" Funktionalität).

Bevor Sie beginnen, deaktivieren SMB 1.0, müssen Sie ermitteln, ob Ihre SMB-Clients auf den Server mit SMB 1.0 derzeit verbunden sind. Geben Sie hierzu das folgende Cmdlet in Windows PowerShell:

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>Sie sollten dieses Skript im Laufe einer Woche (mehrmals pro Tag) erstellen Sie einen Überwachungspfad wiederholt ausführen. Dies kann auch als geplante Aufgabe ausgeführt werden.

Um SMB 1.0 deaktivieren möchten, geben Sie in Windows PowerShell das folgende Skript aus:

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>Wenn eine SMB-Client-Verbindung verweigert wird, weil der Server mit SMB 1.0 deaktiviert wurde, wird im Ereignisprotokoll Microsoft-Windows-SmbServer/operationale Ereignis-ID 1001 angemeldet sein.

## <a name="more-information"></a>Weitere Informationen

Hier sind einige zusätzlichen Ressourcen über SMB und verwandten Technologien in Windows Server 2012.

- [Server Message Block](file-server-smb-overview.md)
- [Speicher in Windows Server](../storage.md)
- [Horizontale Skalierung Dateiserver für Anwendungsdaten](../../failover-clustering/sofs-overview.md)