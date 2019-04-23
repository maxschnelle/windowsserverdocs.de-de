---
title: SMB-Sicherheitsfunktionen
description: Eine Erläuterung des Features für SMB-Verschlüsselung in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server-threshold
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 831ca8266c3ec18ffb83227dcb2d39b3f953ad1a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838051"
---
# <a name="smb-security-enhancements"></a>SMB-Sicherheitsfunktionen

>Gilt für: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

In diesem Thema wird erläutert, die SMB-sicherheitsverbesserungen in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.

## <a name="smb-encryption"></a>SMB-Verschlüsselung

SMB-Verschlüsselung bietet eine End-to-End-Verschlüsselung von SMB-Daten und schützt Daten vor Lauschangriffen in nicht vertrauenswürdigen Netzwerken. Können Sie SMB-Verschlüsselung mit minimalem Aufwand bereitstellen, jedoch kann es kleine zusätzliche Kosten für spezielle Hardware oder Software erforderlich. Es stellt keine Anforderungen an die internetprotokollsicherheit (IPsec) oder WAN-Beschleuniger. SMB-Verschlüsselung kann auf einer Basis pro Dateifreigabe oder für den gesamten Dateiserver konfiguriert werden, und es kann für eine Vielzahl von Szenarien, in denen Daten auf nicht vertrauenswürdige Netzwerken durchläuft, aktiviert werden.

>[!NOTE]
>SMB-Verschlüsselung deckt nicht die Sicherheit im Ruhezustand, die in der Regel vom BitLocker-Laufwerkverschlüsselung verarbeitet wird.

SMB-Verschlüsselung sollten für jedes Szenario berücksichtigt werden, in denen vertrauliche Daten vor Man-in-the-Middle-Angriffen geschützt werden müssen. Mögliche Szenarien:

- Sensible Daten ein Information-Worker werden verschoben, über das SMB-Protokoll. SMB-Verschlüsselung bietet eine End-to-End-Schutz und Integrität der Zusicherung zwischen dem Dateiserver und dem Client, unabhängig von den Netzwerken, die durchlaufen werden, z. B. Verbindungen wide Area Network (WAN), die von nicht-Microsoft-Anbieter verwaltet werden.
- SMB 3.0 ermöglicht Dateiservern ständig verfügbaren Speicher für serveranwendungen wie SQL Server oder Hyper-V bereitstellen. Aktivieren der SMB-Verschlüsselung bietet die Möglichkeit zum Schutz dieser Informationen vor Spoofingangriffen. SMB-Verschlüsselung ist einfacher, als die dedizierte hardwarelösungen zu verwenden, die für die meisten Storage Area Networks (SANs) erforderlich sind.

>[!IMPORTANT]
>Beachten Sie, dass eine wichtige Leistung betreiben von Kosten mit End-to-End-Verschlüsselungsschutz im Vergleich zu nicht verschlüsselte vorhanden ist.

## <a name="enable-smb-encryption"></a>Aktivieren der SMB-Verschlüsselung

Sie können die SMB-Verschlüsselung für den gesamten Dateiserver oder nur für bestimmte Dateifreigaben aktivieren. Verwenden Sie eines der folgenden Verfahren, um SMB-Verschlüsselung zu aktivieren:

### <a name="enable-smb-encryption-with-windows-powershell"></a>Aktivieren der SMB-Verschlüsselung mit Windows PowerShell

1. Geben Sie das folgende Skript auf dem Server, um SMB-Verschlüsselung für eine einzelne Dateifreigabe zu aktivieren:
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. Geben Sie das folgende Skript auf dem Server, um SMB-Verschlüsselung für den gesamten Dateiserver zu aktivieren:
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. Geben Sie das folgende Skript zum Erstellen einer neuen SMB-Dateifreigabe mit SMB-Verschlüsselung aktiviert:
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>Aktivieren der SMB-Verschlüsselung mit Server-Manager

1. Öffnen Sie im Server-Manager **Datei- und Speicherdienste**.
2. Wählen Sie **Freigaben** der Management-Seite "Freigaben" zu öffnen.
3. Mit der rechten Maustaste in der Freigabe, die Sie auf SMB-Verschlüsselung zu aktivieren, und wählen Sie dann **Eigenschaften**.
4. Auf der **Einstellungen** auf die Freigabe, auf der Seite **Datenzugriff verschlüsseln**. Remote-Datei, die auf diese Freigabe zugegriffen werden verschlüsselt.

### <a name="considerations-for-deploying-smb-encryption"></a>Überlegungen zur Bereitstellung der SMB-Verschlüsselung

Standardmäßig Wenn SMB-Verschlüsselung für eine Dateifreigabe oder Server aktiviert ist nur SMB 3.0-Clients dürfen auf der angegebenen Dateifreigaben zugreifen. Dies erzwingt die Absicht des Administrators Schutz der das für alle Clients, die auf die Freigaben zugreifen. Allerdings kann in einigen Fällen möchte ein Administrator unverschlüsselten Zugriff für Clients zu ermöglichen, die SMB 3.0 (z. B. während eine Übergangsperiode bei gemischten clientbetriebssystemversionen verwendet werden) nicht unterstützt. Um unverschlüsselten Zugriff für Clients zu ermöglichen, die keine SMB 3.0 unterstützen, geben Sie das folgende Skript in Windows PowerShell aus:

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

Die sichere Dialekt Aushandlung-Funktion, die im nächsten Abschnitt beschrieben wird verhindert, dass einen Man-in-the-Middle-Angriff ein Downgrade von einer Verbindungs von SMB 3.0 mit SMB 2.0 (die unverschlüsselte Access verwenden würde). Allerdings verhindert keine Herabstufung auf SMB 1.0, sie dies auch unverschlüsselten Zugriff führen würde. Um zu gewährleisten, dass SMB 3.0-Clients immer SMB-Verschlüsselung verwenden, um die verschlüsselten Freigaben zugreifen, müssen Sie die SMB 1.0-Server deaktivieren. (Anweisungen hierzu finden Sie im Abschnitt [deaktivieren SMB 1.0](#disabling-smb-1.0).) Wenn die **– RejectUnencryptedAccess** Einstellung bleibt die Standardeinstellung von **$true**, nur verschlüsselungsfähiges SMB 3.0-Clients sind zulässig, die Zugriff auf Dateifreigaben (SMB 1.0-Clients werden auch abgelehnt werden).

>[!NOTE]
>* SMB-Verschlüsselung verwendet den Advanced Encryption Standard (AES)-CCM-Algorithmus zum Verschlüsseln und Entschlüsseln der das. AES-CCM bietet auch die Überprüfung der Datenintegrität für verschlüsselten Dateifreigaben, unabhängig von den SMB-Signatur-Einstellungen zu ändern (Anmelden). Wenn Sie SMB-Signaturen ohne Verschlüsselung aktivieren möchten, können Sie weiterhin dazu. Weitere Informationen finden Sie unter [die Grundlagen der SMB-Signaturen](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/).
>* Sie können Probleme auftreten, wenn Sie versuchen, Zugriff auf die Dateifreigabe oder den Server, wenn Ihre Organisation über wide Area Network (WAN) Acceleration Geräte verwendet.
>* Mit einer Standardkonfiguration (wobei es keine unverschlüsselten Zugriff auf verschlüsselten Dateifreigaben zulässig), wenn Clients, die nicht über SMB 3.0 Zugriffsversuch auf einer verschlüsselten Dateifreigabe, Ereignis-ID 1003 unterstützen wird in das Microsoft-Windows-SmbServer/Operational-Ereignisprotokoll protokolliert. , und der Client erhält eine **Zugriffsverweigerung** Fehlermeldung angezeigt.
>* SMB-Verschlüsselung und die Encrypting File System (EFS) im NTFS-Dateisystem werden nicht verknüpfte und SMB-Verschlüsselung nicht erforderlich oder mit EFS abhängig ist.
>* SMB-Verschlüsselung und die BitLocker-Laufwerkverschlüsselung stehen in keinerlei Zusammenhang und SMB-Verschlüsselung nicht erforderlich oder mit BitLocker Drive Encryption abhängig ist.

## <a name="secure-dialect-negotiation"></a>Sichere Dialekt-Aushandlung

SMB 3.0 ist zum Erkennen von Man-in-the-Middle-Angriffe, die versuchen, ein downgrade der SMB 2.0 oder SMB 3.0-Protokoll oder die Funktionen, die der Client und Server handeln kann. Wenn ein solcher Angriff vom Client oder dem Server erkannt wird, wird die Verbindung wird getrennt, und Ereignis-ID 1005 wird im Microsoft-Windows-SmbServer/Operational-Ereignisprotokoll protokolliert. Sichern der Dialekt Aushandlung nicht erkennen oder zu verhindern, dass Downgrades von SMB 2.0 oder 3.0 zu SMB 1.0. Aus diesem Grund und den vollständigen Funktionsumfang von SMB-Verschlüsselung zu nutzen wird dringend empfohlen, dass Sie die SMB 1.0-Server deaktivieren. Weitere Informationen finden Sie unter [deaktivieren SMB 1.0](#disabling-smb-1.0).

Die Möglichkeit der sicheren Dialekt-Aushandlung, die im nächsten Abschnitt beschrieben wird verhindert, dass einen Man-in-the-Middle-Angriff ein Downgrade von einer Verbindungs zwischen smb3 und SMB-2 (die unverschlüsselte Access verwenden würde); Allerdings verhindert nicht Downgrades auf SMB-1, sie dies auch unverschlüsselten Zugriff führen würde. Weitere Informationen zu potenziellen Problemen mit zuvor nicht-Windows-Implementierungen von SMB finden Sie unter den [Microsoft Knowledge Base](http://support.microsoft.com/kb/2686098).

## <a name="new-signing-algorithm"></a>Neue Signaturalgorithmus

SMB 3.0 wird einen neueren Verschlüsselungsalgorithmus für die Signierung verwendet: Advanced Encryption Standard (AES) - Cipher - basierte Hashed Message Authentication Code (CMAC). SMB 2.0 verwendet den älteren HMAC-SHA256-Verschlüsselungsalgorithmus. AES-CMAC und AES-CCM können erheblich datenverschlüsselung für die meisten modernen CPUs beschleunigen, die Unterstützung von AES-Anweisung. Weitere Informationen finden Sie unter [die Grundlagen der SMB-Signaturen](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/).

## <a name="disabling-smb-10"></a>Deaktivieren SMB 1.0

Die älteren computerbrowserdiensts und Remote Administration Protocol-Funktionen in SMB 1.0 sind nun separate und gelöscht werden können. Diese Funktionen sind immer noch standardmäßig aktiviert, aber wenn Sie keine älteren SMB-Clients, z. B. Computer mit Windows Server 2003 oder Windows XP verfügen können, entfernen Sie die SMB 1.0-Features, um den Sicherheitsgrad erhöhen und das Patchen möglicherweise reduziert werden.

>[!NOTE]
>SMB 2.0 wurde in Windows Server 2008 und Windows Vista eingeführt. Ältere Clients wie Computer unter Windows Server 2003 oder Windows XP, unterstützen kein SMB 2.0. und aus diesem Grund, sie werden nicht auf Dateifreigaben zugreifen oder Drucken Freigaben aus, wenn die SMB 1.0-Server deaktiviert ist. Darüber hinaus einige nicht - Microsoft-SMB-Clients möglicherweise nicht auf Dateifreigaben SMB 2.0 zugreifen oder Freigaben (z. B. Drucker mit Funktionen für "Scan-Share") drucken können.

Bevor Sie beginnen, deaktivieren SMB 1.0, müssen Sie herausfinden, ob die SMB-Clients auf den Server mit SMB 1.0 derzeit verbunden sind. Geben Sie zu diesem Zweck das folgende Cmdlet in Windows PowerShell ein:

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>Sie sollten dieses Skript wiederholt ausführen, im Laufe einer Woche (mehrmals täglich), um ein Audit-Trail zu erstellen. Sie können dies auch als geplanten Task ausführen.

Um die SMB 1.0 zu deaktivieren, geben Sie das folgende Skript in Windows PowerShell ein:

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>Wenn eine SMB-Client-Verbindung abgelehnt wird, da der Server mit SMB 1.0 deaktiviert wurde, wird Ereignis-ID 1001 im Microsoft-Windows-SmbServer/Operational-Ereignisprotokoll protokolliert.

## <a name="more-information"></a>Weitere Informationen

Hier sind einige zusätzlichen Ressourcen zu SMB und verwandten Technologien in Windows Server 2012.

- [Server Message Block](file-server-smb-overview.md)
- [Speicher in WindowsServer](../storage.md)
- [Server der Dateiserver mit horizontaler Skalierung für Anwendungsdaten](../../failover-clustering/sofs-overview.md)