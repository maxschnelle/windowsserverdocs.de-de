---
title: SMB-Sicherheitsfunktionen
description: Eine Erläuterung der SMB-Verschlüsselungsfunktion in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016.
ms.prod: windows-server
ms.topic: article
author: JasonGerend
ms.author: jgerend
ms.technology: storage
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9052e9e6a1327b67fd75b07ab2ee6fc56b1190ac
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86962134"
---
# <a name="smb-security-enhancements"></a>SMB-Sicherheitsfunktionen

>Gilt für: Windows Server 2012 R2, Windows Server 2012, Windows Server 2016

In diesem Thema werden die SMB-Verschlüsselungsfunktion in Windows Server 2012 R2, Windows Server 2012 und Windows Server 2016 erläutert.

## <a name="smb-encryption"></a>SMB-Verschlüsselung

SMB-Verschlüsselung sorgt für End-to-End-Verschlüsselung von SMB-Daten und schützt Daten vor Lauschangriffen in nicht vertrauenswürdigen Netzwerken. Sie können SMB-Verschlüsselung mit minimalem Aufwand bereitstellen, für spezielle Hardware oder Software fallen jedoch möglicherweise geringfügige zusätzliche Kosten an. Sie erfordert weder IPsec (Internet Protocol Security) noch WAN-Beschleuniger. SMB-Verschlüsselung kann auf Freigabebasis oder für den gesamten Dateiserver konfiguriert und für eine Vielzahl von Szenarien aktiviert werden, bei denen Daten über nicht vertrauenswürdige Netzwerke übertragen werden.

>[!NOTE]
>SMB-Verschlüsselung bezieht sich nicht auf Daten im Ruhezustand. Diese werden in der Regel von BitLocker-Laufwerkverschlüsselung verarbeitet.

SMB-Verschlüsselung sollte für jedes Szenario in Erwägung gezogen werden, in dem vertrauliche Daten vor Man-in-the-Middle-Angriffen geschützt werden müssen. Mögliche Szenarien:

- Die sensiblen Daten eines Information Workers werden mithilfe des SMB-Protokolls verschoben. SMB-Verschlüsselung bietet eine End-to-End-Datenschutz- und -Integritätssicherung zwischen dem Dateiserver und dem Client, unabhängig von den durchlaufenen Netzwerken, z. B. WAN-Verbindungen (Wide Area Network), die von Nicht-Microsoft-Anbietern verwaltet werden.
- Mit SMB 3.0 können Dateiserver kontinuierlich verfügbaren Speicher für Serveranwendungen bereitstellen, z. B. für SQL Server oder Hyper-V. Das Aktivieren der SMB-Verschlüsselung bietet die Möglichkeit, diese Informationen vor Spionageangriffen zu schützen. SMB-Verschlüsselung ist einfacher zu verwenden als die dedizierten Hardwarelösungen, die für die meisten SANs (Storage Area Networks) erforderlich sind.

>[!IMPORTANT]
>Beachten Sie, dass im Vergleich zu nicht verschlüsseltem Schutz für die End-to-End-Verschlüsselung beachtliche Leistungsbetriebskosten anfallen.

## <a name="enable-smb-encryption"></a>Aktivieren von SMB-Verschlüsselung

Sie können SMB-Verschlüsselung für den gesamten Dateiserver oder nur für bestimmte Dateifreigaben aktivieren. Verwenden Sie zum Aktivieren von SMB-Verschlüsselung eines der folgenden Verfahren:

### <a name="enable-smb-encryption-with-windows-powershell"></a>Aktivieren von SMB-Verschlüsselung mit Windows PowerShell

1. Geben Sie das folgende Skript auf dem Server ein, um SMB-Verschlüsselung für eine einzelne Dateifreigabe zu aktivieren:
    
    ```PowerShell
    Set-SmbShare –Name <sharename> -EncryptData $true
    ```
2. Geben Sie das folgende Skript auf dem Server ein, um SMB-Verschlüsselung für den gesamten Dateiserver zu aktivieren:
    
    ```PowerShell
    Set-SmbServerConfiguration –EncryptData $true
    ```
3. Geben Sie das folgende Skript ein, um eine neue SMB-Dateifreigabe mit aktivierter SMB-Verschlüsselung zu erstellen:
    
    ```PowerShell
    New-SmbShare –Name <sharename> -Path <pathname> –EncryptData $true
    ```

### <a name="enable-smb-encryption-with-server-manager"></a>Aktivieren von SMB-Verschlüsselung mit Server-Manager

1. Öffnen Sie in Server-Manager **Datei- und Speicherdienste**.
2. Wählen Sie **Freigaben** aus, um die Verwaltungsseite „Freigaben“ zu öffnen.
3. Klicken Sie mit der rechten Maustaste auf die Freigabe, für die Sie SMB-Verschlüsselung aktivieren möchten, und wählen Sie dann **Eigenschaften** aus.
4. Wählen Sie auf der Seite **Einstellungen** der Freigabe **Datenzugriff verschlüsseln** aus. Remotedateizugriff auf diese Freigabe wird verschlüsselt.

### <a name="considerations-for-deploying-smb-encryption"></a>Überlegungen zur Bereitstellung von SMB-Verschlüsselung

Wenn SMB-Verschlüsselung für eine Dateifreigabe oder einen Server aktiviert ist, dürfen standardmäßig nur SMB 3.0-Clients auf die angegebenen Dateifreigaben zugreifen. Dies setzt die Absicht des Administrators durch, die Daten für alle Clients zu schützen, die auf die Freigaben zugreifen. In einigen Fällen möchte ein Administrator jedoch möglicherweise einen unverschlüsselten Zugriff für Clients zulassen, die SMB 3.0 nicht unterstützen (z. B. während eines Übergangszeitraums, wenn gemischte Clientbetriebssystemversionen verwendet werden). Geben Sie das folgende Skript in Windows PowerShell ein, um unverschlüsselten Zugriff für Clients zuzulassen, die SMB 3.0 nicht unterstützen:

```PowerShell
Set-SmbServerConfiguration –RejectUnencryptedAccess $false
```

Mit der im nächsten Abschnitt beschriebenen sicheren Dialektaushandlungsfunktion wird verhindert, dass ein Man-in-the-Middle-Angriff eine Verbindung von SMB 3.0 auf SMB 2.0 herabstuft (dann würde unverschlüsselter Zugriff verwendet). Es wird jedoch kein Downgrade auf SMB 1.0 verhindert, was ebenfalls zu unverschlüsseltem Zugriff führen würde. Um sicherzustellen, dass SMB 3.0-Clients immer SMB-Verschlüsselung für den Zugriff auf verschlüsselte Freigaben verwenden, müssen Sie den SMB 1.0-Server deaktivieren. (Anweisungen dazu finden Sie im Abschnitt [Deaktivieren von SMB 1.0](#disabling-smb-10).) Wenn für die Einstellung **–RejectUnencryptedAccess** die Standardeinstellung **$true** beibehalten wird, dürfen nur verschlüsselungsfähige SMB 3.0-Clients auf die Dateifreigaben zugreifen (SMB 1.0-Clients werden ebenfalls abgelehnt).

>[!NOTE]
>* SMB-Verschlüsselung verwendet den AES-CCM-Algorithmus (Advanced Encryption Standard), um die Daten zu verschlüsseln und zu entschlüsseln. AES-CCM bietet auch eine Überprüfung der Datenintegrität (Signierung) für verschlüsselte Dateifreigaben, unabhängig von den SMB-Signierungseinstellungen. Wenn Sie SMB-Signaturen ohne Verschlüsselung aktivieren möchten, können Sie diese weiterhin verwenden. Weitere Informationen finden Sie unter [Grundlagen von SMB-Signaturen](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2).
>* Wenn Sie versuchen, auf die Dateifreigabe oder den Server zuzugreifen, treten möglicherweise Probleme auf, wenn in Ihrer Organisation WAN-Beschleuniger (Wide Area Network) verwendet werden.
>* Mit einer Standardkonfiguration (bei der kein unverschlüsselter Zugriff auf verschlüsselte Dateifreigaben zulässig ist), wird Ereignis-ID 1003 im Ereignisprotokoll „Microsoft-Windows-SmbServer/Operational“ protokolliert, und der Client empfängt eine Fehlermeldung des Typs **Zugriff verweigert**, wenn Clients, die SMB 3.0 nicht unterstützen, versuchen, auf eine verschlüsselte Dateifreigabe zuzugreifen.
>* SMB-Verschlüsselung und das verschlüsselnde Dateisystem (EFS) im NTFS-Dateisystem stehen nicht miteinander in Beziehung, und SMB-Verschlüsselung erfordert nicht die Verwendung von EFS oder hängt davon ab.
>* SMB-Verschlüsselung und die BitLocker-Laufwerkverschlüsselung stehen nicht miteinander in Beziehung, und SMB-Verschlüsselung erfordert nicht die Verwendung von Bitlocker-Laufwerkverschlüsselung oder hängt davon ab.

## <a name="secure-dialect-negotiation"></a>Sichere Dialektaushandlung

SMB 3.0 ist in der Lage, Man-in-the-Middle-Angriffe zu erkennen, die versuchen, ein Downgrade des SMB 2.0- oder SMB 3.0-Protokolls oder der Funktionen durchzuführen, die der Client und der Server aushandeln. Wenn ein solcher Angriff vom Client oder Server erkannt wird, wird die Verbindung getrennt, und die Ereignis-ID 1005 wird im Ereignisprotokoll „Microsoft-Windows-SmbServer/Operational“ protokolliert. Die sichere Dialektaushandlung kann keine Herabstufungen von SMB 2.0 oder 3.0 auf SMB 1.0 erkennen oder verhindern. Daher wird dringend empfohlen, den SMB 1.0-Server zu deaktivieren, um die vollständigen Funktionen von SMB-Verschlüsselung nutzen zu können. Weitere Informationen finden Sie unter [Deaktivieren von SMB 1.0](#disabling-smb-10).

Mit der im nächsten Abschnitt beschriebenen sicheren Dialektaushandlungsfunktion wird verhindert, dass ein Man-in-the-Middle-Angriff eine Verbindung von SMB 3 auf SMB 2 herabstuft (dann würde unverschlüsselter Zugriff verwendet). Es jedoch nicht das Herabstufen auf SMB 1 verhindert, was ebenfalls zu unverschlüsseltem Zugriff führen würde. Weitere Informationen zu möglichen Problemen mit früheren Nicht-Windows-Implementierungen von SMB finden Sie in der [Microsoft Knowledge Base](https://support.microsoft.com/kb/2686098).

## <a name="new-signing-algorithm"></a>Neuer Signaturalgorithmus

SMB 3.0 verwendet einen neueren Verschlüsselungsalgorithmus zum Signieren: AES-CMAC (Advanced Encryption Standard, Cipher-based Message Authentication Code). SMB 2.0 hat den älteren HMAC-SHA256-Verschlüsselungsalgorithmus verwendet. AES-CMAC und AES-CCM können die Datenverschlüsselung mit den meisten modernen CPUs mit AES-Anweisungsunterstützung erheblich beschleunigen. Weitere Informationen finden Sie unter [Grundlagen von SMB-Signaturen](/archive/blogs/josebda/the-basics-of-smb-signing-covering-both-smb1-and-smb2).

## <a name="disabling-smb-10"></a>Deaktivieren von SMB 1.0

Die Features des älteren Computerbrowserdiensts und des Remoteverwaltungsprotokolls in SMB 1.0 wurden nun getrennt und können entfernt werden. Die Features sind immer noch standardmäßig aktiviert. Wenn Sie jedoch keine älteren SMB-Clients wie Computer mit Windows XP oder Windows Server 2003 besitzen, können Sie die SMB 1.0-Features entfernen, um die Sicherheit zu erhöhen und das Patchen möglicherweise zu reduzieren.

>[!NOTE]
>SMB 2.0 wurde in Windows Server 2008 und Windows Vista eingeführt. Ältere Clients, z. B. Computer, auf denen Windows Server 2003 oder Windows XP ausgeführt wird, unterstützen SMB 2.0 nicht. Daher können sie nicht auf Dateifreigaben oder Druckfreigaben zugreifen, wenn der SMB 1.0-Server deaktiviert ist. Darüber hinaus können einige Nicht-Microsoft-SMB-Clients möglicherweise nicht auf SMB 2.0-Dateifreigaben oder -Druckfreigaben zugreifen (z. B. Drucker mit „Scan-to-Share“-Funktionalität).

Bevor Sie mit der Deaktivierung von SMB 1.0 beginnen, müssen Sie herausfinden, ob Ihre SMB-Clients derzeit mit dem Server verbunden sind, auf dem SMB 1.0 ausgeführt wird. Geben Sie zu diesem Zweck das folgende Cmdlet in Windows PowerShell ein:

```PowerShell
Get-SmbSession | Select Dialect,ClientComputerName,ClientUserName | ? Dialect -lt 2
```

>[!NOTE]
>Sie sollten dieses Skript im Verlauf einer Woche wiederholt (mehrmals täglich) ausführen, um einen Überwachungspfad zu erstellen. Sie können dieses Skript auch als geplante Aufgabe ausführen.

Geben Sie zum Deaktivieren von SMB 1.0 das folgende Skript in Windows PowerShell ein:

```PowerShell
Set-SmbServerConfiguration –EnableSMB1Protocol $false
```

>[!NOTE]
>Wenn eine SMB-Clientverbindung verweigert wird, weil der Server, auf dem SMB 1.0 ausgeführt wird, deaktiviert wurde, wird Ereignis-ID 1001 im Ereignisprotokoll „Microsoft-Windows-SmbServer/Operational“ protokolliert.

## <a name="more-information"></a>Weitere Informationen

Dies sind einige zusätzliche Ressourcen zu SMB und verwandten Technologien in Windows Server 2012.

- [Server Message Block](file-server-smb-overview.md)
- [Speicher](../storage.yml)
- [Dateiserver mit horizontaler Skalierung für Anwendungsdaten](../../failover-clustering/sofs-overview.md)
