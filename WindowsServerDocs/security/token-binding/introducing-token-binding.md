---
title: "Einführung in die Token-Bindung"
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 2a0bb8c75fe3ca7f7befe0bd67eb3d363a5ad7a9
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="introducing-token-binding"></a>Einführung in die Token-Bindung

>Gilt für: Windows Server 2016 und Windows10

Das Token Binding-Protokoll ermöglicht Anwendungen und Dienste, binden Sie die Sicherheitstoken kryptografisch der TLS-Ebene zu entschärfen von token Diebstahl und replay-Angriffen. Die langlebigen, eindeutig identifizierbaren TLS [RFC5246] Bindungen können mehrere TLS-Sitzungen und Verbindungen umfassen.

Unterstützung für Version:

- Windows 10, Version 1507 – standardmäßig deaktiviert
    - Token-Binding-Protokoll hinzugefügt [[Entwurf-Ietf-Tokbind-Protokoll-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet & HTTP. SYS-Unterstützung für token-Bindung über HTTP [[Entwurf-Ietf-Tokbind-Https-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10, Version 1511 und 1607 und Windows Server 2016 – auf standardmäßig
    - Token-Binding-Protokoll aktualisiert [[Entwurf-Ietf-Tokbind-Protokoll-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - TLS-Erweiterung für token Bindung Aushandlung hinzugefügt [[Entwurf-Popov-Tokbind-Aushandlung-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet & HTTP. SYS-Unterstützung für token-Bindung über HTTP aktualisiert [[Entwurf Ietf-Tokbind-Https-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows10, Version 1507 mit Wartung Update [KB4034668](https://support.microsoft.com/kb/KB4034668), Windows10, Version 1511 mit Wartung Update [KB4034660](https://support.microsoft.com/kb/KB4034660), Windows10, Version 1607 und Windows Server2016 mit Wartung Update [KB4034658](https://support.microsoft.com/kb/KB4034658) Token Binding-Protokollversion 0,10 – auf standardmäßig unterstützt
    - Token-Binding-Protokoll aktualisiert [[Entwurf-Ietf-Tokbind-Protokoll-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - TLS-Erweiterung für token Bindung Aushandlung hinzugefügt [[Entwurf-Ietf-Tokbind-Aushandlung-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP. SYS-Unterstützung für token-Bindung über HTTP aktualisiert [[Entwurf-Ietf-Tokbind-Https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10 unterstützt Version 1703 Token Binding-Protokollversion 0,10 – auf standardmäßig
    - Token-Binding-Protokoll aktualisiert [[Entwurf-Ietf-Tokbind-Protokoll-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - TLS-Erweiterung für token Bindung Aushandlung hinzugefügt [[Entwurf-Ietf-Tokbind-Aushandlung-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet & HTTP. SYS-Unterstützung für token-Bindung über HTTP aktualisiert [[Entwurf-Ietf-Tokbind-Https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - Windows-Geräte mit auf Virtualisierung basierende Sicherheit aktiviert werden die Bindung token-Schlüssel in einer geschützten Umgebung beibehalten, die vom Betriebssystem isoliert ist

Informationen zur Unterstützung von ASP .NET finden Sie unter der [.NET Framework-Referenzquelle](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170). 

Informationen zu .NET Framework finden Sie unter den folgenden Themen:

- [Netzwerkerweiterungen](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding-Klasse](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
