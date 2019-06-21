---
title: Verwalten von SSL/TLS-Protokolle und Verschlüsselungssammlungen für AD FS
description: Häufig gestellte Fragen für AD FS 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: c1153cd81185dcfe83d291161a85481e5a7d0700
ms.sourcegitcommit: afb0602767de64a76aaf9ce6a60d2f0e78efb78b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/20/2019
ms.locfileid: "67280547"
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>Verwalten von SSL/TLS-Protokolle und Verschlüsselungssammlungen für AD FS
Die folgende Dokumentation enthält Informationen zum Deaktivieren und aktivieren bestimmte Protokolle TLS/SSL-Verschlüsselungssammlungen, die von AD FS verwendet werden

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>TLS/SSL, SChannel und Verschlüsselungssammlungen in AD FS

Die Transport Layer Security (TLS) und Secure Sockets Layer (SSL) sind Protokolle, die für die sichere Kommunikation bieten.  Active Directory-Verbunddienste werden diese Protokolle für die Kommunikation verwendet.  Heute existieren mehrere Versionen dieser Protokolle.

Schannel ist ein Security Support Provider (SSP), der die standardmäßigen Internetauthentifizierungsprotokolle SSL, TLS und DTLS implementiert. Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI dienst als gemeinsame Schnittstelle für mehrere SSPs (Security Support Providers), einschließlich des Schannel SSP.

Eine Verschlüsselungssammlung ist ein Satz von Kryptografiealgorithmen. Der Schannel-SSP-Implementierung der TLS/SSL-Protokolle verwenden Algorithmen einer Verschlüsselungssammlung zum Erstellen von Schlüsseln und Verschlüsseln von Informationen. Eine Verschlüsselungssammlung gibt einen Algorithmus für jede der folgenden Aufgaben an:

- Schlüsselaustausch
- Massenverschlüsselung
- Nachrichtenauthentifizierung

AD FS verwendet "Schannel.dll", um die sichere Kommunikation Interaktionen durchzuführen.  Derzeit unterstützt AD FS mit allen Protokollen und Verschlüsselungssammlungen, die von "Schannel.dll" unterstützt werden.

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>Verwalten des TLS/SSL-Protokollen und Verschlüsselungssammlungen
> [!IMPORTANT]
> Dieser Abschnitt enthält Schritte, die Sie, wie Sie die Registrierung ändern können. Allerdings können schwerwiegende Probleme auftreten, wenn Sie die Registrierung falsch ändern. Stellen Sie daher sicher, dass Sie die folgenden Schritte sorgfältig ausführen. 
> 
> Denken Sie daran, ändern die standardsicherheitseinstellungen für SCHANNEL konnte unterbrechen oder zu verhindern, dass Kommunikation zwischen bestimmten Clients und Servern.  Dies geschieht, wenn die sicherer Kommunikation ist erforderlich, und sie verfügen nicht über ein Protokoll zum Aushandeln der Kommunikation mit.
> 
> Wenn Sie diese Änderungen anwenden, müssen sie für alle AD FS-Server in der Farm angewendet werden.  Nach dem Übernehmen dieser Änderungen ist ein Neustart erforderlich.

In den heutigen Tag und Alter, Absichern Ihrer Server und ältere entfernt oder schwache Verschlüsselungssammlungen wird eine hohe Priorität für die meisten Organisationen immer.  Software-Suites sind verfügbar, die Ihre Server zu testen und bieten ausführliche Informationen zu diesen Protokollen und Testsammlungen.  Um einhalten oder sicheren Bewertungen zu erreichen, ist das Entfernen oder deaktivieren schwächere Protokolle oder Verschlüsselungssammlungen unverzichtbar geworden.  Im weiteren Verlauf dieses Dokuments bieten Anweisungen zum Aktivieren oder Deaktivieren bestimmter Protokolle und Verschlüsselungssammlungen.

Die folgenden Registrierungsschlüssel befinden sich am gleichen Speicherort:  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols.  Verwenden Sie "regedit" oder PowerShell, und aktivieren oder deaktivieren Sie diese Protokolle Verschlüsselungssammlungen.

![Registrierungsspeicherort](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>Aktivieren und Deaktivieren von SSL 2.0
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte zum Aktivieren und Deaktivieren von SSL 2.0.

### <a name="enable-ssl-20"></a>Aktivieren von SSL 2.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "DisabledByDefault" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "DisabledByDefault" = DWORD: 00000000 

### <a name="disable-ssl-20"></a>Deaktivieren von SSL 2.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SL 2.0\Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server] "DisabledByDefault" = DWORD: 00000001 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client] "DisabledByDefault" = DWORD: 00000001

### <a name="using-powershell-to-disable-ssl-20"></a>Verwenden von PowerShell zum Deaktivieren von SSL 2.0

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>Aktivieren und Deaktivieren von SSL 3.0
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte zum Aktivieren und Deaktivieren von SSL 3.0.

### <a name="enable-ssl-30"></a>Aktivieren von SSL 3.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "DisabledByDefault" = DWORD: 00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "DisabledByDefault" = DWORD: 00000000 

### <a name="disable-ssl-30"></a>Deaktivieren von SSL 3.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server] "DisabledByDefault" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client] "DisabledByDefault" = DWORD: 00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>Verwenden von PowerShell zum Deaktivieren von SSL 3.0

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>Aktivieren und Deaktivieren von TLS 1.0
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte zum Aktivieren und Deaktivieren von TLS 1.0.

> [!IMPORTANT]
> Deaktivierung von TLS 1.0, wird das WAP zu AD FS-Vertrauensstellung aufheben.  Wenn Sie TLS 1.0 zu deaktivieren, sollten Sie starke Authentifizierung für Ihre Anwendungen aktivieren.  Finden Sie unter [strenge Authentifizierung](#enabling-strong-authentication-for-net-applications) 



### <a name="enable-tls-10"></a>Aktivieren von TLS 1.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "Enabled"=dword:00000001
- [1. 0\server HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000000 
- [1. 0\Client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "Aktiviert" = DWORD: 00000001
- [1. 0\Client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000000 

### <a name="disable-tls-10"></a>Deaktivieren von TLS 1.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server] "Enabled"=dword:00000000
- [1. 0\server HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000001
- [1. 0\Client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "Aktiviert" = DWORD: 00000000
- [1. 0\Client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000001 

### <a name="using-powershell-to-disable-tls-10"></a>Verwenden von PowerShell zum Deaktivieren von TLS 1.0

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>Aktivieren und Deaktivieren von TLS 1.1
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte zum Aktivieren und Deaktivieren von TLS 1.1.

### <a name="enable-tls-11"></a>Aktivieren von TLS 1.1
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "DisabledByDefault" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "DisabledByDefault" = DWORD: 00000000

### <a name="disable-tls-11"></a>Deaktivieren von TLS 1.1
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server] "DisabledByDefault" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client] "DisabledByDefault" = DWORD: 00000001 

### <a name="using-powershell-to-disable-tls-11"></a>Verwenden von PowerShell zum Deaktivieren von TLS 1.1

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>Aktivieren und Deaktivieren von TLS 1.2

Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte zum Aktivieren und Deaktivieren von TLS 1.2.

### <a name="enable-tls-12"></a>Aktivieren von TLS 1.2
- [1. 2\server HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "Aktiviert" = DWORD: 00000001
- [1. 2\server HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000000 
- [1. 2\client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "Aktiviert" = DWORD: 00000001
- [1. 2\client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000000

### <a name="disable-tls-12"></a>Deaktivieren von TLS 1.2
- [1. 2\server HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "Aktiviert" = DWORD: 00000000
- [1. 2\server HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000001
- [1. 2\client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "Aktiviert" = DWORD: 00000000
- [1. 2\client HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS] "DisabledByDefault" = DWORD: 00000001

### <a name="using-powershell-to-disable-tls-12"></a>Verwenden von PowerShell zum Deaktivieren von TLS 1.2

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.2 has been disabled.'
```

## <a name="enable-and-disable-rc4"></a>Aktivieren und Deaktivieren von RC4 

Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte zum Aktivieren und Deaktivieren von RC4.  Diese Verschlüsselungssammlung Registrierungsschlüssel befinden sich hier:

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![Registrierungsspeicherort](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>Aktivieren von RC4

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled"=dword:00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Aktiviert" = DWORD: 00000001 

### <a name="disable-rc4"></a>Deaktivieren von RC4

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Enabled"=dword:00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Aktiviert" = DWORD: 00000000 

### <a name="using-powershell"></a>Mithilfe der PowerShell

```powershell
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    ([Microsoft.Win32.RegistryKey]::OpenRemoteBaseKey([Microsoft.Win32.RegistryHive]::LocalMachine,$env:COMPUTERNAME)).CreateSubKey('SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128') 
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="enabling-or-disabling-additional-cipher-suites"></a>Aktivieren oder Deaktivieren von zusätzlichen Verschlüsselungssammlungen

Sie können bestimmte bestimmten Verschlüsselungen deaktivieren aus HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\00010002 löschen 

![Registrierungsspeicherort](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

Um eine Verschlüsselungssammlung zu aktivieren, fügen Sie der Zeichenfolgenwert, der Wert der mehrteiligen Zeichenfolge Funktionsschlüssel hinzu.  Z. B., wenn wir TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521 aktivieren möchten würde dann wir es in die Zeichenfolge hinzufügen.

Eine vollständige Liste der unterstützten Cipher Suites finden Sie unter [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx).  Dieses Dokument enthält eine Tabelle mit Sammlungen, die aktiviert sind, standardmäßig und solche, die unterstützt werden, aber nicht standardmäßig aktiviert.  Priorisieren die Verschlüsselungssammlungen finden Sie unter [Priorisieren von Schannel Cipher Suites](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx).

## <a name="enabling-strong-authentication-for-net-applications"></a>Aktivieren strenge Authentifizierung für .NET-Anwendungen
Die .NET Framework-3.5/4.0/4.5.x-Anwendungen können das Standardprotokoll aktivieren den Registrierungsschlüssel SchUseStrongCrypto auf TLS 1.2 wechseln.  Dieser Registrierungsschlüssel wird für die Verwendung von TLS 1.2 .NET Anwendungen erzwungen.

> [!IMPORTANT]
> Für AD FS unter Windows Server 2016 und Windows Server 2012 R2 müssen Sie den .NET Framework 4.0/4.5.x-Schlüssel verwenden:  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319


Verwenden Sie für .NET Framework 3.5 den folgenden Registrierungsschlüssel:

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\.NETFramework\v2.0.50727] "SchUseStrongCrypto"=dword:00000001

Für .NET Framework 4.0/4.5.x, verwenden Sie den folgenden Registrierungsschlüssel: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\.NETFramework\v4.0.30319 "SchUseStrongCrypto"=dword:00000001

![Strenge Authentifizierung](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>Weitere Informationen

- [Verschlüsselungssammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)
- [TLS-Verschlüsselungssammlungen in Windows 8.1](https://msdn.microsoft.com/library/windows/desktop/mt767781.aspx)
- [Priorisieren von Schannel-Cipher-Suites](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)
- [Verschlüsselung und der andere rätselhaften Zunge sprechende](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
