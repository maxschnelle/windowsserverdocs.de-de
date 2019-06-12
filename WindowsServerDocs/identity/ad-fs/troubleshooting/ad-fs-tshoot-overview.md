---
title: Problembehandlung für AD FS
description: In diesem Dokument wird beschrieben, wie verschiedene Aspekte von AD FS-Problembehandlung
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 6410d510085d1772ca6d8ced47226e00239a1a02
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66443900"
---
# <a name="troubleshooting-ad-fs"></a>Problembehandlung für AD FS
AD FS verfügt über viele bewegliche Teile, viele verschiedene Dinge berührt und hängt von vielen anderen.  Natürlich kann dies zu verschiedenen Problemen führen.  Dieses Dokument soll Ihnen den Einstieg in die Problembehandlung zu erhalten.  In diesem Dokument werden die typischen Bereiche vorgestellt, die Sie sich konzentrieren sollten, wie Sie zum Aktivieren von Funktionen für die zusätzliche Informationen und verschiedene Tools, die zum Erkennen von Problemen verwendet werden können.  

>[!NOTE]
>Weitere Informationen finden Sie [AD FS-Hilfe](http://adfshelp.microsoft.com) die bietet effektive Tools in einem platzieren, erleichtert es Benutzern und Administratoren, die Authentifizierungsprobleme schneller und zu beheben. 


## <a name="what-to-check-first"></a>Was Sie zuerst überprüfen
Bevor Sie die eingehende Problembehandlung beschäftigen, gibt es einige Dinge, die Sie Sie zunächst überprüfen sollten.  Die Überladungen sind:
- **DNS-Konfiguration** -können Sie den Namen des Verbunddiensts beheben?  Dies sollte in beiden des Lastenausgleichs-IP-Adresse oder die IP-Adresse eines der AD FS-Servern in der Farm aufgelöst.  Weitere Informationen finden Sie unter [AD FS-Problembehandlung – DNS-](ad-fs-tshoot-dns.md).
- **AD FS-Endpunkte** -können Sie durchsuchen, um die AD FS-Endpunkte?  Durch Navigieren zu diesem können Sie bestimmen, und zwar unabhängig davon, ob Ihre AD FS-Web-Server auf Anforderungen reagiert.  Wenn Sie diese Datei zugreifen können, wissen Sie, dass AD FS-Anforderungen über 443 problemlos Wartung ist.  Weitere Informationen finden Sie unter [AD FS-Problembehandlung - Endpunkte](ad-fs-tshoot-endpoints.md).
- **IDP-initiierten anmelden** -können Sie sich anmelden und authentifizieren Sie über die Seite Idp-Initiated anmelden?  Sie müssen sicherstellen, dass auf dieser Seite aktiviert wurde, weil sie in der Standardeinstellung deaktiviert ist.  Verwendung `Set-AdfsProperties -EnableIdPInitiatedSignOn $true` auf die Seite zu aktivieren.  Wenn Sie sich anmelden und authentifizieren können wissen Sie, dass AD FS in diesem Bereich arbeitet.  Weitere Informationen finden Sie unter [AD FS-Problembehandlung – SSO](ad-fs-tshoot-initiatedsignon.md).
  ##  <a name="common-troubleshooting-areas"></a>Allgemeine Problembehandlung für Bereiche

|Name|Beschreibung|
|-----|-----|
|[Event-Protokollierung und-Überwachung](ad-fs-tshoot-logging.md)|Verwenden Sie die Windows-Ereignisprotokolle, um hohe und niedrige Ebene Informationen über die Verwaltungs- und Trace-Protokolle anzuzeigen.  Sie können auch verwendet werden, an die sicherheitsüberwachung.|
|[SQL-Konnektivität](ad-fs-tshoot-sql.md)|Informationen zum Testen der Konnektivität zwischen Ihren AD FS-Servern und der Back-End-SQL-Datenbanken|
|[Ausstellung von Ansprüchen](ad-fs-tshoot-claims-issuance.md)|Informationen zu bestimmen, ob AD FS ordnungsgemäß Ansprüche ausstellt.|
|[Loop-Erkennung](ad-fs-tshoot-loop.md)|Informationen zum Bestimmen und verhindert, dass Benutzer hin und her zwischen den Idp und als vertrauende Seite zurückgesendet wird.|
|[Zertifikate](ad-fs-tshoot-certs.md)|Typcial Zertifikatsprobleme, die auftreten können|
|[Fiddler](ad-fs-tshoot-fiddler.md)|Informationen zum Installieren und Verwenden von Fiddler|
|[WS-Verbund mit Fiddler](ad-fs-tshoot-fiddler-ws-fed.md)|Ausführliche Ablaufverfolgung mit Fiddler einen WS-Verbund-Interaktion|
|[Anspruchsregeln](ad-fs-tshoot-claims-rules.md)|Informationen zur Behandlung von Anspruchsregeln und ihrer syntax|
|[Integrierte Windows-Authentifizierung](ad-fs-tshoot-iwa.md)|Informationen zur Problembehandlung für integrierte Authentifizierung.|
|[Azure AD](ad-fs-tshoot-azure.md)|Informationen zur Problembehandlung von AD FS-Interaktion mit Azure AD.|
|[AD FS-Diagnose-Analyzer](ad-fs-diagnostics-analyzer.md)|AD FS-Hilfe Diagnose Analyzer können grundlegende AD FS-Überprüfungen, die mit dem Diagnose-PowerShell-Modul ausführen. 