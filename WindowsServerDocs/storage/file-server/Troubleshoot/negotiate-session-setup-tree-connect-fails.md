---
title: Fehler beim Aushandeln, beim Einrichten von Sitzungen und bei Strukturverbindungen
description: Erläutert die Problembehandlung bei den Fehlern beim Aushandeln, beim Einrichten der Sitzung und bei der Baum Verbindung.
author: Deland-Han
manager: dcscontentpm
ms.topic: article
ms.author: delhan
ms.date: 12/25/2019
ms.openlocfilehash: 2bad602f934d844074ee96df06bf9234fdbf943f
ms.sourcegitcommit: d5e27c1f2f168a71ae272bebf8f50e1b3ccbcca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2020
ms.locfileid: "86961162"
---
# <a name="negotiate-session-setup-and-tree-connect-failures"></a>Fehler beim Aushandeln, beim Einrichten von Sitzungen und bei Strukturverbindungen

In diesem Artikel wird beschrieben, wie Sie Fehler beheben, die während einer SMB-Aushandlung, einer Sitzungs Einrichtung und einer Struktur Verbindungsanforderung auftreten.

## <a name="negotiate-fails"></a>Aushandlung schlägt fehl

Der SMB-Server empfängt eine SMB-Aushandlungs Anforderung von einem SMB-Client. Der Verbindungs Timeout ist abgelaufen und wird nach 60 Sekunden zurückgesetzt. Nach ungefähr 200 Mikrosekunden kann eine Bestätigungsmeldung angezeigt werden.

Dieses Problem wird häufig durch ein Antivirenprogramm verursacht.

Wenn Sie Windows Server 2008 R2 verwenden, gibt es Hotfixes für dieses Problem. Stellen Sie sicher, dass der SMB-Client und der SMB-Server auf dem neuesten Stand sind.

## <a name="session-setup-fails"></a>Fehler beim Einrichten der Sitzung

Der SMB-Server empfängt eine Anforderung zum Einrichten einer SMB-Sitzung \_ von einem SMB-Client, konnte jedoch nicht Antworten.

Wenn der voll qualifizierte Domänen Name (Fully Qualified Domain Name, FQDN) oder der NetBIOS-Name (Network Basic Input/Output System) des Servers im UNC-Pfad (Universal Naming Convention) angezeigt wird, verwendet Windows Kerberos für die Authentifizierung.

Nach der Aushandlungs Antwort wird versucht, ein Kerberos-Ticket für den CIFS-Dienst Prinzipal Namen (Common Internet File System, SPN) des Servers zu erhalten. Überprüfen Sie den Kerberos-Datenverkehr an TCP-Port 88, um sicherzustellen, dass keine Kerberos-Fehler auftreten, wenn der SMB-Client das Token erhält.

> [!NOTE]
> Die Fehler, die während der Kerberos-Vorauthentifizierung auftreten, sind in Ordnung. Die Fehler, die nach der Kerberos-Vorauthentifizierung auftreten (Instanzen, bei denen die Authentifizierung nicht funktioniert), sind die Fehler, die das SMB-Problem verursacht haben.

Führen Sie außerdem die folgenden Prüfungen durch:

- Überprüfen Sie das sicherheitsblob in der Setup Anforderung für die SMB-Sitzung \_ , um sicherzustellen, dass die richtigen Anmelde Informationen gesendet werden.

- Versuchen Sie, die SMB-Servernamen Härtung zu deaktivieren (**smbservernamehardeninglevel = 0**).

- Stellen Sie sicher, dass der SMB-Server über einen SPN verfügt, wenn der Zugriff über einen CNAME-DNS-Datensatz erfolgt.

- Stellen Sie sicher, dass die SMB-Signatur funktioniert. (Dies ist insbesondere für ältere Geräte von Drittanbietern wichtig.)

## <a name="tree-connect-fails"></a>Fehler bei Struktur Verbindung

Stellen Sie sicher, dass die Anmelde Informationen für das Benutzerkonto über die Berechtigungen Freigabe und NT File System (NTFS) für den Ordner verfügen.

Die Ursache von häufigen Struktur Verbindungsfehlern finden Sie unter [3.3.5.7 empfängt an SMB2 Tree \_ Connect Request](/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87). Im folgenden finden Sie die Lösungen für zwei allgemeine Statuscodes.

\[Ungültiger \_ \_ Netzwerk \_ Name.\]

Stellen Sie sicher, dass die Freigabe auf dem Server vorhanden ist und dass Sie in der SMB-Client Anforderung korrekt geschrieben ist.

\[Status \_ Zugriff \_ verweigert\]

Vergewissern Sie sich, dass der von der Freigabe verwendete Datenträger und Ordner vorhanden sind und darauf zugegriffen werden kann.

Wenn Sie SMBv3 oder höher verwenden, überprüfen Sie, ob für den Server und die Freigabe eine Verschlüsselung erforderlich ist, der Client jedoch keine Verschlüsselung unterstützt. Führen Sie dazu die folgenden Aktionen aus:

- Überprüfen Sie den Server, indem Sie den folgenden Befehl ausführen.

  ```PowerShell
  Get-SmbServerConfiguration | select Encrypt*
  ```

  Wenn "verschlüsseltdata" und "rejectunverschlüsseltedaccess" den Wert "true" haben, muss der Server verschlüsselt werden

- Überprüfen Sie die Freigabe, indem Sie den folgenden Befehl ausführen:

  ```PowerShell
  Get-SmbShare | select name, EncryptData  
  ```

  Wenn "verschlüsseltdata" auf der Freigabe "true" ist und "rejectunverschlüsseltedaccess" auf dem Server "true" ist, wird die Verschlüsselung für die Freigabe benötigt.

Beachten Sie die folgenden Richtlinien bei der Problembehandlung:

- Windows 8, Windows Server 2012 und spätere Versionen von Windows unterstützen die Client seitige Verschlüsselung (SMBv3 und höher).

- Windows 7, Windows Server 2008 R2 und frühere Versionen von Windows unterstützen keine Client seitige Verschlüsselung.

- Die Verschlüsselung wird von Samba und Geräten von Drittanbietern möglicherweise nicht unterstützt. Weitere Informationen finden Sie möglicherweise in der Produktdokumentation.

## <a name="references"></a>References

Weitere Informationen finden Sie in den folgenden Artikeln.

[3.3.5.4 empfängt eine SMB2 Aushandlungs Anforderung](/openspecs/windows_protocols/ms-smb2/b39f253e-4963-40df-8dff-2f9040ebbeb1)

[3.3.5.5 empfängt eine SMB2-Sitzungs \_ Setup Anforderung](/openspecs/windows_protocols/ms-smb2/e545352b-9f2b-4c5e-9350-db46e4f6755e)

[3.3.5.7 empfängt eine SMB2 Tree \_ Connect-Anforderung](/openspecs/windows_protocols/ms-smb2/652e0c14-5014-4470-999d-b174d7b2da87)
