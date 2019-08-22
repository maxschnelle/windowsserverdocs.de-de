---
title: Verwalten von SSL/TLS-Protokollen und Verschlüsselungs Sammlungen für AD FS
description: Häufig gestellte Fragen zu AD FS 2016
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 951e7d74a3370d9863d747e349d7fe701615e225
ms.sourcegitcommit: 2e38b26742f3b16c153170d6f5219c020a8e9383
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/22/2019
ms.locfileid: "69896817"
---
# <a name="managing-ssltls-protocols-and-cipher-suites-for-ad-fs"></a>Verwalten von SSL/TLS-Protokollen und Verschlüsselungs Sammlungen für AD FS
Die folgende Dokumentation enthält Informationen zum Deaktivieren und Aktivieren bestimmter TLS/SSL-Protokolle und Verschlüsselungs Sammlungen, die von verwendet werden AD FS

## <a name="tlsssl-schannel-and-cipher-suites-in-ad-fs"></a>TLS/SSL, SChannel und Chiffre Suites in AD FS

Die Transport Layer Security (TLS) und Secure Sockets Layer (SSL) sind Protokolle, die eine sichere Kommunikation ermöglichen.  Active Directory-Verbunddienste (AD FS) verwendet diese Protokolle für die Kommunikation.  Heute sind mehrere Versionen dieser Protokolle vorhanden.

Schannel ist ein Security Support Provider (SSP), der die standardmäßigen Internetauthentifizierungsprotokolle SSL, TLS und DTLS implementiert. Die Security Support Provider-Schnittstelle (Security Support Provider Interface, SSPI) ist eine API, die von Windows-Systemen verwendet wird, um sicherheitsbezogene Funktionen wie Authentifizierungen durchzuführen. Die SSPI dienst als gemeinsame Schnittstelle für mehrere SSPs (Security Support Providers), einschließlich des Schannel SSP.

Eine Verschlüsselungssammlung ist ein Satz von Kryptografiealgorithmen. Die Schannel SSP-Implementierung der TLS/SSL-Protokolle verwendet Algorithmen aus einer Verschlüsselungs Sammlung zum Erstellen von Schlüsseln und Verschlüsseln von Informationen. Eine Verschlüsselungssammlung gibt einen Algorithmus für jede der folgenden Aufgaben an:

- Schlüsselaustausch
- Massenverschlüsselung
- Nachrichtenauthentifizierung

AD FS verwendet Schannel. dll zum Durchführen der sicheren kommunikationinteraktionen.  Derzeit werden AD FS alle Protokolle und Verschlüsselungs Sammlungen unterstützt, die von Schannel. dll unterstützt werden.

## <a name="managing-the-tlsssl-protocols-and-cipher-suites"></a>Verwalten der TLS/SSL-Protokolle und Verschlüsselungs Sammlungen
> [!IMPORTANT]
> Dieser Abschnitt enthält Schritte, die Ihnen zeigen, wie Sie die Registrierung ändern können. Schwerwiegende Probleme können jedoch auftreten, wenn Sie die Registrierung falsch ändern. Stellen Sie daher sicher, dass Sie diese Schritte sorgfältig ausführen. 
> 
> Beachten Sie, dass das Ändern der Standard Sicherheitseinstellungen für SChannel die Kommunikation zwischen bestimmten Clients und Servern unterbrechen oder verhindern kann.  Dies tritt auf, wenn eine sichere Kommunikation erforderlich ist und Sie nicht über ein Protokoll zum Aushandeln der Kommunikation verfügen.
> 
> Wenn Sie diese Änderungen anwenden, müssen Sie auf alle AD FS Server in der Farm angewendet werden.  Nach dem Anwenden dieser Änderungen ist ein Neustart erforderlich.

Am Tag und dem Alter der Tage wird die Härtung Ihrer Server und das Entfernen älterer oder schwacher Verschlüsselungs Sammlungen für viele Organisationen zu einer wichtigen Priorität.  Software Suites sind verfügbar, mit denen die Server getestet werden und detaillierte Informationen zu diesen Protokollen und Sammlungen bereitgestellt werden.  Um die Konformität zu gewährleisten oder sichere Bewertungen zu erzielen, ist das Entfernen oder deaktivieren schwächer Protokolle oder Verschlüsselungs Sammlungen zu einem muss.  Im restlichen Teil dieses Dokuments finden Sie Anleitungen zum Aktivieren oder Deaktivieren bestimmter Protokolle und Verschlüsselungs Sammlungen.

Die folgenden Registrierungsschlüssel befinden sich am selben Speicherort:  HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols.  Verwenden Sie regedit oder PowerShell, um diese Protokolle und Verschlüsselungs Sammlungen zu aktivieren bzw. zu deaktivieren.

![Registrierungsspeicherort](media/Managing-SSL-Protocols-in-AD-FS/registry.png)

## <a name="enable-and-disable-ssl-20"></a>Aktivieren und Deaktivieren von SSL 2,0
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte, um SSL 2,0 zu aktivieren und zu deaktivieren.

### <a name="enable-ssl-20"></a>Aktivieren von SSL 2,0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "Disabledbydefault" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client] "Disabledbydefault" = DWORD: 00000000 

### <a name="disable-ssl-20"></a>SSL 2,0 deaktivieren
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Server] "Disabledbydefault" = DWORD: 00000001 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0 \ Client] "Disabledbydefault" = DWORD: 00000001

### <a name="using-powershell-to-disable-ssl-20"></a>Verwenden von PowerShell zum Deaktivieren von SSL 2,0

``` powershell
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -Force | Out-Null
    
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
            
New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
            
New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 2.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
Write-Host 'SSL 2.0 has been disabled.'
```

## <a name="enable-and-disable-ssl-30"></a>Aktivieren und Deaktivieren von SSL 3,0
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte, um SSL 3,0 zu aktivieren und zu deaktivieren.

### <a name="enable-ssl-30"></a>Aktivieren von SSL 3.0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "Disabledbydefault" = DWORD: 00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client] "Disabledbydefault" = DWORD: 00000000 

### <a name="disable-ssl-30"></a>SSL 3,0 deaktivieren
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Server] "Disabledbydefault" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0 \ Client] "Disabledbydefault" = DWORD: 00000001 

### <a name="using-powershell-to-disable-ssl-30"></a>Verwenden von PowerShell zum Deaktivieren von SSL 3,0

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\SSL 3.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'SSL 3.0 has been disabled.'
```

## <a name="enable-and-disable-tls-10"></a>Aktivieren und Deaktivieren von TLS 1,0
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte, um TLS 1,0 zu aktivieren und zu deaktivieren.

> [!IMPORTANT]
> Durch das Deaktivieren von TLS 1,0 wird der WAP zum AD FS vertrauenswürdig.  Wenn Sie TLS 1,0 deaktivieren, sollten Sie die starke Authentifizierung für Ihre Anwendungen aktivieren.  Siehe [Aktivieren der starken Authentifizierung](#enabling-strong-authentication-for-net-applications) 



### <a name="enable-tls-10"></a>Aktivieren von TLS 1,0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "Disabledbydefault" = DWORD: 00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client] "Disabledbydefault" = DWORD: 00000000 

### <a name="disable-tls-10"></a>Deaktivieren von TLS 1,0
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Server] "Disabledbydefault" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0 \ Client] "Disabledbydefault" = DWORD: 00000001 

### <a name="using-powershell-to-disable-tls-10"></a>Deaktivieren von TLS 1,0 mithilfe von PowerShell

```powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.0\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.0 has been disabled.'
```


## <a name="enable-and-disable-tls-11"></a>Aktivieren und Deaktivieren von TLS 1,1
Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte, um TLS 1,1 zu aktivieren und zu deaktivieren.

### <a name="enable-tls-11"></a>Aktivieren von TLS 1,1
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "Disabledbydefault" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client] "Disabledbydefault" = DWORD: 00000000

### <a name="disable-tls-11"></a>Deaktivieren von TLS 1,1
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Server] "Disabledbydefault" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1 \ Client] "Disabledbydefault" = DWORD: 00000001 

### <a name="using-powershell-to-disable-tls-11"></a>Deaktivieren von TLS 1,1 mithilfe von PowerShell

``` powershell
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Server' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    
    New-Item 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'Enabled' -value '0' -PropertyType 'DWord' -Force | Out-Null
    
    New-ItemProperty -path 'HKLM:\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.1\Client' -name 'DisabledByDefault' -value 1 -PropertyType 'DWord' -Force | Out-Null
    Write-Host 'TLS 1.1 has been disabled.'
```

## <a name="enable-and-disable-tls-12"></a>Aktivieren und Deaktivieren von TLS 1,2

Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte, um TLS 1,2 zu aktivieren und zu deaktivieren.

### <a name="enable-tls-12"></a>Aktivieren von TLS 1,2
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Server] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Server] "Disabledbydefault" = DWORD: 00000000 
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Client] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Client] "Disabledbydefault" = DWORD: 00000000

### <a name="disable-tls-12"></a>Deaktivieren von TLS 1,2
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Server] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Server] "Disabledbydefault" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Client] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Protocols\TLS 1.2 \ Client] "Disabledbydefault" = DWORD: 00000001

### <a name="using-powershell-to-disable-tls-12"></a>Deaktivieren von TLS 1,2 mithilfe von PowerShell

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

Verwenden Sie die folgenden Registrierungsschlüssel und deren Werte, um RC4 zu aktivieren und zu deaktivieren.  Die Registrierungsschlüssel dieser Verschlüsselungs Sammlung befinden sich hier:

- HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\

![Registrierungsspeicherort](media/Managing-SSL-Protocols-in-AD-FS/cipher.png)



### <a name="enable-rc4"></a>Aktivieren von RC4

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Aktiviert" = DWORD: 00000001
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128] "Aktiviert" = DWORD: 00000001 

### <a name="disable-rc4"></a>RC4 deaktivieren

- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128] "Aktiviert" = DWORD: 00000000
- [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128] "Aktiviert" = DWORD: 00000000
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

## <a name="enabling-or-disabling-additional-cipher-suites"></a>Aktivieren oder deaktivieren zusätzlicher Verschlüsselungs Sammlungen

Sie können bestimmte bestimmte Chiffren deaktivieren, indem Sie Sie aus HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Cryptography\Configuration\Local\SSL\00010002 entfernen. 

![Registrierungsspeicherort](media/Managing-SSL-Protocols-in-AD-FS/suites.png)

Um eine Verschlüsselungs Sammlung zu aktivieren, fügen Sie Ihren Zeichen folgen Wert dem Schlüssel für den funktionsfähigen mehr Zeichen folgen Wert hinzu.  Wenn Sie z. b. TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384_P521 aktivieren möchten, fügen wir es der Zeichenfolge hinzu.

Eine vollständige Liste der unterstützten Verschlüsselungs Sammlungen finden Sie unter Verschlüsselungs Sammlungen [in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx).  Dieses Dokument enthält eine Tabelle mit Suites, die standardmäßig aktiviert sind und die unterstützt, aber nicht standardmäßig aktiviert sind.  Informationen zum Priorisieren der Verschlüsselungs Sammlungen finden Sie unter [Priorisieren von SChannel](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)-Verschlüsselungs Sammlungen.

## <a name="enabling-strong-authentication-for-net-applications"></a>Aktivieren der starken Authentifizierung für .NET-Anwendungen
Die .NET Framework 3.5/4.0/4.5. x-Anwendungen können das Standardprotokoll auf TLS 1,2 umstellen, indem Sie den Registrierungsschlüssel "schutsstrongcrypto" aktivieren.  Dieser Registrierungsschlüssel erzwingt .NET-Anwendungen, TLS 1,2 zu verwenden.

> [!IMPORTANT]
> Für AD FS unter Windows Server 2016 und Windows Server 2012 R2 müssen Sie die .NET Framework 4.0/4.5. x-Taste verwenden:  HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\. NETFramework\v4.0.30319


Verwenden Sie für den .NET Framework 3,5 den folgenden Registrierungsschlüssel:

[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\\. NETFramework\v2.0.50727] "schugstrongcrypto" = DWORD: 00000001

Verwenden Sie für den .NET Framework 4.0/4.5. x den folgenden Registrierungsschlüssel: HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\\. NETFramework\v4.0.30319 "schugstrongcrypto" = DWORD: 00000001

![Strenge Authentifizierung](media/Managing-SSL-Protocols-in-AD-FS/strongauth.png)

```powershell
    
    New-ItemProperty -path 'HKLM:\SOFTWARE\Microsoft\.NetFramework\v4.0.30319' -name 'SchUseStrongCrypto' -value '1' -PropertyType 'DWord' -Force | Out-Null
```

## <a name="additional-information"></a>Zusätzliche Informationen

- [Verschlüsselungs Sammlungen in TLS/SSL (Schannel SSP)](https://msdn.microsoft.com/library/windows/desktop/aa374757.aspx)
- [TLS-Verschlüsselungs Sammlungen in Windows 8.1](https://msdn.microsoft.com/library/windows/desktop/mt767781.aspx)
- [Priorisieren von SChannel-Verschlüsselungs Sammlungen](https://msdn.microsoft.com/library/windows/desktop/bb870930.aspx)
- [Sprechen in Chiffren und anderen rätselhaften Zungen](https://blogs.technet.microsoft.com/askds/2015/12/08/speaking-in-ciphers-and-other-enigmatic-tonguesupdate/)
