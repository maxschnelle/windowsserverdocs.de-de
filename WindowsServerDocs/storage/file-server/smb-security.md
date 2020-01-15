---
title: SMB-Sicherheitsfunktionen
description: Eine Erläuterung der SMB-Verschlüsselungsfunktion in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7b96574dcfc2a4417aa36780d7bd87c2556f61f
ms.sourcegitcommit: 083ff9bed4867604dfe1cb42914550da05093d25
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/14/2020
ms.locfileid: "75950263"
---
# <a name="smb-security-enhancements"></a>SMB-Sicherheitsfunktionen

>Gilt für: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

In diesem Thema werden die SMB-Sicherheitsverbesserungen in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016 erläutert.

## <a name="smb-encryption"></a>SMB-Verschlüsselung

Die SMB-Verschlüsselung bietet eine End-to-End-Verschlüsselung von SMB-Daten und schützt Daten vor dem Auftreten von Ereignissen in nicht vertrauenswürdigen Netzwerken. Sie können die SMB-Verschlüsselung mit minimalem Aufwand bereitstellen, für spezielle Hardware oder Software sind jedoch möglicherweise kleine zusätzliche Kosten erforderlich. Es gelten keine Anforderungen für IPSec (Internet Protocol Security) oder WAN-Accelerators. Die SMB-Verschlüsselung kann auf Freigabe Basis oder für den gesamten Dateiserver konfiguriert und für eine Vielzahl von Szenarios aktiviert werden, in denen Daten über nicht vertrauenswürdige Netzwerke übertragen werden.

>[!NOTE]
>Die SMB-Verschlüsselung deckt nicht die ruhende Sicherheit ab, die in der Regel von BitLocker-Laufwerkverschlüsselung verarbeitet wird.

Die SMB-Verschlüsselung sollte in jedem Szenario berücksichtigt werden, in dem sensible Daten vor man-in-the-Middle-Angriffen geschützt werden müssen. Mögliche Szenarien:

- Die sensiblen Daten eines Information Workers werden mithilfe des SMB-Protokolls verschoben. Die SMB-Verschlüsselung bietet eine End-to-End-Datenschutz-und Integritäts Sicherung zwischen dem Dateiserver und dem Client, unabhängig von den durchsuchenden Netzwerken, z. b. WAN-Verbindungen (Wide Area Network), die von nicht-Microsoft-Anbietern verwaltet werden.
- Mit SMB 3,0 können Dateiserver kontinuierlich verfügbaren Speicher für Server Anwendungen bereitstellen, z. b. SQL Server oder Hyper-V. Das Aktivieren der SMB-Verschlüsselung bietet die Möglichkeit, diese Informationen vor Spionage-Angriffen zu schützen. Die SMB-Verschlüsselung ist einfacher zu verwenden als die dedizierten Hardwarelösungen, die für die meisten Sans (Storage Area Networks) erforderlich sind.

>[!IMPORTANT]
>Beachten Sie, dass im Vergleich zu nicht verschlüsseltem Schutz für die End-to-End-Verschlüsselung ein beachtlicher Leistungs Betriebskosten vorliegt.

## <a name="enable-smb-encryption"></a>Aktivieren der SMB-Verschlüsselung

Sie können die SMB-Verschlüsselung für den gesamten Dateiserver oder nur für bestimmte Dateifreigaben aktivieren. Verwenden Sie eines der folgenden Verfahren, um die SMB-Verschlüsselung zu aktivieren:

### <a name="enable-smb-encryption-with-windows-powershell"></a>Aktivieren der SMB-Verschlüsselung mit Windows PowerShell

1. Geben Sie das folgende Skript auf dem Server ein, um die SMB-Verschlüsselung für eine einzelne Dateifreigabe zu aktivieren:
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. Geben Sie das folgende Skript auf dem Server ein, um die SMB-Verschlüsselung für den gesamten Dateiserver zu aktivieren:
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. Geben Sie das folgende Skript ein, um eine neue SMB-Dateifreigabe mit aktivierter SMB-Verschlüsselung zu erstellen:
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>Aktivieren der SMB-Verschlüsselung mit Server-Manager

1. Öffnen Sie in Server-Manager die **Datei-und Speicherdienste**.
2. Wählen **Sie** Freigaben, um die Verwaltungsseite Freigaben zu öffnen.
3. Klicken Sie mit der rechten Maustaste auf die Freigabe, für die Sie die SMB-Verschlüsselung aktivieren möchten, und wählen Sie dann **Eigenschaften**aus.
4. Wählen Sie auf der Seite **Einstellungen** der Freigabe die Option **Datenzugriff verschlüsseln**aus. Der Remote Dateizugriff auf diese Freigabe ist verschlüsselt.

### <a name="considerations-for-deploying-smb-encryption"></a>Überlegungen zur Bereitstellung von SMB

Wenn die SMB-Verschlüsselung für eine Dateifreigabe oder einen Server aktiviert ist, dürfen standardmäßig nur SMB 3,0-Clients auf die angegebenen Dateifreigaben zugreifen. Dies erzwingt die Absicht des Administrators, die Daten für alle Clients zu schützen, die auf die Freigaben zugreifen. In einigen Fällen möchte ein Administrator jedoch möglicherweise einen unverschlüsselten Zugriff für Clients zulassen, die SMB 3,0 nicht unterstützen (z. b. während eines Übergangszeitraums, wenn gemischte Client Betriebssystem-Versionen verwendet werden). Geben Sie das folgende Skript in Windows PowerShell ein, um unverschlüsselten Zugriff für Clients zuzulassen, die SMB 3,0 nicht unterstützen:

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

Mit der im nächsten Abschnitt beschriebenen sicheren Dialekt Aushandlungs Funktion wird verhindert, dass ein man-in-the-Middle-Angriff eine Verbindung von SMB 3,0 zu SMB 2,0 herabstuft (bei dem unverschlüsselter Zugriff verwendet wird). Es verhindert jedoch nicht das Downgrade auf SMB 1,0, was ebenfalls zu unverschlüsseltem Zugriff führen würde. Um sicherzustellen, dass SMB 3,0-Clients immer SMB-Verschlüsselung für den Zugriff auf verschlüsselte Freigaben verwenden, müssen Sie den SMB 1,0-Server deaktivieren. (Anweisungen hierzu finden Sie im Abschnitt [Deaktivierung von SMB 1,0](#disabling-smb-10).) Wenn die Einstellung **– rejectunverschlüsseltedaccess** an der Standardeinstellung **$true**belassen wird, dürfen nur Verschlüsselungs fähige SMB 3,0-Clients auf die Dateifreigaben zugreifen (SMB 1,0-Clients werden ebenfalls abgelehnt).

>[!NOTE]
>* Die SMB-Verschlüsselung verwendet den Advanced Encryption Standard (AES)-ccm-Algorithmus, um die Daten zu verschlüsseln und zu entschlüsseln. AES-CCM bietet auch eine Überprüfung der Datenintegrität (Signierung) für verschlüsselte Dateifreigaben, unabhängig von den SMB-Signierungs Einstellungen. Wenn Sie SMB-Signaturen ohne Verschlüsselung aktivieren möchten, können Sie diesen Vorgang fortsetzen. Weitere Informationen finden Sie unter [den Grundlagen von SMB-Signaturen](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/).
>* Wenn Sie versuchen, auf die Dateifreigabe oder den Server zuzugreifen, treten möglicherweise Probleme auf, wenn in Ihrer Organisation WAN-Beschleunigungs Geräte (Wide Area Network) verwendet werden.
>* Bei einer Standardkonfiguration (bei der kein unverschlüsselter Zugriff auf verschlüsselte Dateifreigaben zulässig ist) gilt: Wenn Clients, die SMB 3,0 nicht unterstützen, versuchen, auf eine verschlüsselte Dateifreigabe zuzugreifen, wird die Ereignis-ID 1003 im Ereignisprotokoll Microsoft-Windows-Smbserver/Operational protokolliert, und der Client erhält die Fehlermeldung " **Zugriff verweigert** ".
>* Die SMB-Verschlüsselung und die Verschlüsselndes Dateisystem (EFS) im NTFS-Datei System sind nicht miteinander verknüpft, und die SMB-Verschlüsselung erfordert oder ist nicht mit EFS verbunden.
>* Die SMB-Verschlüsselung und die BitLocker-Laufwerkverschlüsselung sind nicht miteinander verknüpft, und die SMB-Verschlüsselung erfordert oder ist nicht erforderlich, wenn BitLocker-Laufwerkverschlüsselung verwendet wird.

## <a name="secure-dialect-negotiation"></a>Sichere Dialekt Aushandlung

SMB 3,0 ist in der Lage, man-in-the-Middle-Angriffe zu erkennen, die versuchen, ein Downgrade des SMB 2,0-oder SMB 3,0-Protokolls oder der Funktionen durchführen, die der Client und der Server aushandeln Wenn ein solcher Angriff vom Client oder Server erkannt wird, wird die Verbindung getrennt, und die Ereignis-ID 1005 wird im Ereignisprotokoll Microsoft-Windows-Smbserver/Operational protokolliert. Die sichere Dialekt Aushandlung kann keine Herabstufungen von SMB 2,0 oder 3,0 auf SMB 1,0 erkennen oder verhindern. Daher wird dringend empfohlen, den SMB 1,0-Server zu deaktivieren, um die vollständigen Funktionen der SMB-Verschlüsselung nutzen zu können. Weitere Informationen finden Sie unter [Deaktivieren von SMB 1,0](#disabling-smb-10).

Mit der im nächsten Abschnitt beschriebenen sicheren Dialekt Aushandlungs Funktion wird verhindert, dass ein man-in-the-Middle-Angriff eine Verbindung von SMB 3 zu SMB 2 herabstuft (bei der unverschlüsselter Zugriff verwendet wird). Es verhindert jedoch nicht das Herabstufen von SMB 1, was ebenfalls zu unverschlüsseltem Zugriff führen würde. Weitere Informationen zu möglichen Problemen mit früheren nicht-Windows-Implementierungen von SMB finden Sie in der [Microsoft Knowledge Base](https://support.microsoft.com/kb/2686098).

## <a name="new-signing-algorithm"></a>Neuer Signatur Algorithmus

SMB 3,0 verwendet einen neueren Verschlüsselungsalgorithmus zum Signieren: Advanced Encryption Standard (AES)-Verschlüsselungscode (Message Authentication Code, CMAC). SMB 2,0 hat den älteren HMAC-SHA256-Verschlüsselungsalgorithmus verwendet. AES-CMAC und AES-CCM können die Datenverschlüsselung auf den meisten modernen CPUs mit AES-Anweisungs Unterstützung erheblich beschleunigen. Weitere Informationen finden Sie unter [den Grundlagen von SMB-Signaturen](https://blogs.technet.microsoft.com/josebda/2010/12/01/the-basics-of-smb-signing-covering-both-smb1-and-smb2/).

## <a name="disabling-smb-10"></a>Deaktivieren von SMB 1,0

Der ältere Computer Browser Dienst und die Features des Remote Verwaltungs Protokolls in SMB 1,0 sind nun getrennt und können entfernt werden. Diese Features sind immer noch standardmäßig aktiviert. Wenn Sie jedoch nicht über ältere SMB-Clients verfügen, z. b. Computer, auf denen Windows Server 2003 oder Windows XP ausgeführt wird, können Sie die SMB 1,0-Features entfernen, um die Sicherheit zu erhöhen und das Patchen zu verringern.

>[!NOTE]
>SMB 2,0 wurde in Windows Server 2008 und Windows Vista eingeführt. Ältere Clients, z. b. Computer, auf denen Windows Server 2003 oder Windows XP ausgeführt wird, unterstützen SMB 2,0 nicht. Daher können Sie nicht auf Dateifreigaben oder Druck Freigaben zugreifen, wenn der SMB 1,0-Server deaktiviert ist. Darüber hinaus können einige nicht-Microsoft-SMB-Clients möglicherweise nicht auf SMB 2,0-Dateifreigaben oder Druck Freigaben zugreifen (z. b. Drucker mit "Scan-to-Share"-Funktionalität).

Bevor Sie mit der Deaktivierung von SMB 1,0 beginnen, müssen Sie herausfinden, ob Ihre SMB-Clients derzeit mit dem Server verbunden sind, auf dem SMB 1,0 ausgeführt wird. Geben Sie hierzu das folgende Cmdlet in Windows PowerShell ein:

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>Sie sollten dieses Skript im Verlauf einer Woche (mehrmals täglich) wiederholt ausführen, um einen Überwachungs Pfad zu erstellen. Sie können dies auch als geplante Aufgabe ausführen.

Um SMB 1,0 zu deaktivieren, geben Sie das folgende Skript in Windows PowerShell ein:

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>Wenn eine SMB-Client Verbindung verweigert wird, weil der Server, auf dem SMB 1,0 ausgeführt wird, deaktiviert wurde, wird Ereignis-ID 1001 im Ereignisprotokoll Microsoft-Windows-Smbserver/Operational protokolliert.

## <a name="more-information"></a>Weitere Informationen

Hier finden Sie einige zusätzliche Ressourcen zu SMB und verwandten Technologien in Windows Server 2012.

- [Server Message Block](file-server-smb-overview.md)
- [Speicher](../storage.md)
- [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](../../failover-clustering/sofs-overview.md)