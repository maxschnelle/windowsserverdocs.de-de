---
title: Einführen der tokenbindung
ms.topic: article
ms.assetid: 4623a48c-cefd-4a27-9173-2af58ac212f2
author: justinha
ms.author: Justinha
ms.date: 11/09/2016
ms.openlocfilehash: 08042ef376587c1e3370c07bf6c77b07f7aedc1f
ms.sourcegitcommit: 7cacfc38982c6006bee4eb756bcda353c4d3dd75
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/14/2020
ms.locfileid: "90078517"
---
# <a name="introducing-token-binding"></a>Einführen der tokenbindung

>Gilt für: Windows Server 2016 und Windows 10

Das tokenbindungsprotokoll ermöglicht Anwendungen und Diensten das kryptografische binden ihrer Sicherheits Token an die TLS-Schicht, um tokendiebstahl und Replay-Angriffe zu verhindern
Die langlebige, eindeutig identifizierbaren TLS-Bindungen [RFC5246] können mehrere TLS-Sitzungen und-Verbindungen umfassen.

Versions Unterstützung:

- Windows 10, Version 1507 – standardmäßig deaktiviert
    - Tokenbindungsprotokoll hinzugefügt [[Draft-IETF-tokbind-Protocol-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - WinInet-& HTTP.SYS Unterstützung der [tokenbindung über http [Draft-IETF-tokbind-HTTPS-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/01/)
- Windows 10, Version 1511 und 1607 und Windows Server 2016 – standardmäßig aktiviert
    - Tokenbindungsprotokoll aktualisiert [[Draft-IETF-tokbind-Protocol-01]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/01/)
    - TLS-Erweiterung für [tokenbindungs-Aushandlung hinzugefügt [Draft-Popov-tokbind-Aushandlung-00]](https://tools.ietf.org/html/draft-popov-tokbind-negotiation-00)
    - WinInet-& HTTP.SYS Unterstützung der [tokenbindung über HTTP aktualisiert [Draft-IETF-tokbind-HTTPS-02]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/02/)
- Windows 10, Version 1507 mit Wartungsupdate [KB4034668](https://support.microsoft.com/kb/KB4034668), Windows 10, Version 1511 mit Wartungsupdate [KB4034660](https://support.microsoft.com/kb/KB4034660), Windows 10, Version 1607 und Windows Server 2016 mit Wartungsupdate [KB4034658](https://support.microsoft.com/kb/KB4034658) Support Token Binding Protocol Version 0,10 – on default
    - Tokenbindungsprotokoll aktualisiert [[Draft-IETF-tokbind-Protocol-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - TLS-Erweiterung für [tokenbindungs-Aushandlung hinzugefügt [Draft-IETF-tokbind-Aushandlung-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet-& HTTP.SYS Unterstützung der [tokenbindung über HTTP aktualisiert [Draft-IETF-tokbind-HTTPS-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
- Windows 10, Version 1703 unterstützt das tokenbindungsprotokoll Version 0,10 – standardmäßig on
    - Tokenbindungsprotokoll aktualisiert [[Draft-IETF-tokbind-Protocol-10]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-protocol/10/)
    - TLS-Erweiterung für [tokenbindungs-Aushandlung hinzugefügt [Draft-IETF-tokbind-Aushandlung-05]](https://tools.ietf.org/html/draft-ietf-tokbind-negotiation-05)
    - WinInet-& HTTP.SYS Unterstützung der [tokenbindung über HTTP aktualisiert [Draft-IETF-tokbind-HTTPS-06]](https://datatracker.ietf.org/doc/draft-ietf-tokbind-https/06/)
    - Bei Windows-Geräten mit aktivierter virtualisierungsbasierter Sicherheit werden die tokenbindungsschlüssel in einer geschützten Umgebung aufbewahrt, die vom laufenden Betriebssystem isoliert ist.

Informationen zur ASP .NET-Unterstützung finden Sie im [.NET Framework Verweis Quelle](https://referencesource.microsoft.com/#System.Web/ITlsTokenBindingInfo.cs,4a5e5668f5c31170).

Weitere Informationen zu .NET Framework finden Sie in den folgenden Themen:

- [Netzwerk Erweiterungen](https://blogs.msdn.microsoft.com/dotnet/2015/11/30/net-framework-4-6-1-is-now-available/#networking)

- [.Net tokenbinding-Klasse](/dotnet/api/system.security.authentication.extendedprotection.tokenbinding?view=netframework-4.8)