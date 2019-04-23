---
title: Einführung in die Bindung von Token
ms.custom: na
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
manager: alanth
author: justinha
ms.technology: security-authentication
ms.date: 11/09/2016
ms.openlocfilehash: 2a0bb8c75fe3ca7f7befe0bd67eb3d363a5ad7a9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884231"
---
# <a name="introducing-token-binding"></a>Einführung in die Bindung von Token

>Gilt für: WindowsServer 2016 und Windows 10

Das Token Binding-Protokoll ermöglicht, Anwendungen und Dienste, um seine Sicherheitstoken kryptografisch der TLS-Ebene zum Verringern der Diebstahl von token und Wiederholungsangriffe zu binden. Die Bindungen für langlebigen, eindeutig identifizierbaren TLS [RFC5246] können mehrere TLS-Sitzungen und Verbindungen umfassen.

Versionsunterstützung:

- Windows 10 Version 1507 – standardmäßig deaktiviert
    - Token-Bindung Protokoll hinzugefügt [[Draft-Ietf-Tokbind-Protokoll-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet und HTTP. SYS-Unterstützung von tokenbindungen über HTTP [[Draft-Ietf-Tokbind-Https-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10-Versionen 1511 und 1607 und Windows Server 2016 – in der Standardeinstellung
    - Token-Bindung Protokoll aktualisiert [[Draft-Ietf-Tokbind-Protokoll-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - TLS-Erweiterungen für die Bindung von token-Aushandlung hinzugefügt [[Draft-Popov-Tokbind-Aushandlung-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet und HTTP. SYS-Unterstützung von tokenbindungen über HTTP aktualisiert [[Draft-Ietf-Tokbind-Https-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10 Version 1507 mit Wartungsupdate [KB4034668](https://support.microsoft.com/kb/KB4034668), Windows 10, Version 1511 mit Wartungsupdate [KB4034660](https://support.microsoft.com/kb/KB4034660), Windows 10, Version 1607 und Windows Server 2016 mit Wartungsupdate [KB4034658](https://support.microsoft.com/kb/KB4034658) Tokenbindungsprotokoll Version 0.10 – auf standardmäßig unterstützt.
    - Token-Bindung Protokoll aktualisiert [[Draft-Ietf-Tokbind-Protokoll-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - TLS-Erweiterungen für die Bindung von token-Aushandlung hinzugefügt [[Draft-Ietf-Tokbind-Aushandlung: 05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet und HTTP. SYS-Unterstützung von tokenbindungen über HTTP aktualisiert [[Draft-Ietf-Tokbind-Https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10 unterstützt Version 1703 Tokenbindungsprotokoll Version 0.10 – standardmäßig für
    - Token-Bindung Protokoll aktualisiert [[Draft-Ietf-Tokbind-Protokoll-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - TLS-Erweiterungen für die Bindung von token-Aushandlung hinzugefügt [[Draft-Ietf-Tokbind-Aushandlung: 05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet und HTTP. SYS-Unterstützung von tokenbindungen über HTTP aktualisiert [[Draft-Ietf-Tokbind-Https-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - Windows-Geräte mit aktivierter virtualisierungsbasierte Sicherheit werden die Bindung von token-Schlüssel in einer geschützten Umgebung beibehalten, die von dem ausgeführten Betriebssystem isoliert ist

Informationen zur Unterstützung von ASP .NET finden Sie unter den [.NET Framework Reference Source](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170). 

Informationen zu .NET Framework finden Sie unter den folgenden Themen:

- [Netzwerkerweiterungen](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.NET TokenBinding-Klasse](https://msdn.microsoft.com/library/system.security.authentication.extendedprotection.tokenbinding.aspx)
