---
title: Problembehandlung für AD FS
description: In diesem Dokument wird beschrieben, wie verschiedene Aspekte von AD FS behandelt werden.
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 01/12/2018
ms.topic: article
ms.openlocfilehash: ba18341448720403f1572ee485ec33bec84b4324
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87953069"
---
# <a name="troubleshooting-ad-fs"></a>Problembehandlung für AD FS
AD FS eine Menge beweglicher Teile hat, werden viele verschiedene Dinge behandelt, und es gibt viele verschiedene Abhängigkeiten.  Naturgemäß kann dies zu diversen Problemen führen.  Dieses Dokument soll Ihnen den Einstieg in die Behebung dieser Probleme erleichtern.  In diesem Dokument werden die typischen Bereiche vorgestellt, auf die Sie sich konzentrieren sollten, das Aktivieren von Features für zusätzliche Informationen und verschiedene Tools, die zum Nachverfolgen von Problemen verwendet werden können.

>[!NOTE]
>Weitere Informationen finden Sie in der [ADFS-Hilfe](https://adfshelp.microsoft.com) , die effektive Tools an einem Ort bereitstellt, die es Benutzern und Administratoren erleichtern, Authentifizierungs Probleme schneller zu lösen.


## <a name="what-to-check-first"></a>Was zuerst überprüft werden muss
Bevor Sie sich mit der detaillierten Problembehandlung befassen, sollten Sie zunächst einige Punkte überprüfen.  Sie lauten wie folgt:
- **DNS-Konfiguration** : können Sie den Namen des Verbund Dienstanbieter auflösen?  Dies sollte entweder in die IP-Adresse des Load Balancers oder die IP-Adresse eines der AD FS Server in der Farm aufgelöst werden.  Weitere Informationen finden Sie unter [AD FS Problembehandlung: DNS](ad-fs-tshoot-dns.md).
- **AD FS Endpunkte** : können Sie zu den AD FS Endpunkten navigieren?  Durch das Durchsuchen können Sie feststellen, ob Ihr AD FS Webserver auf Anforderungen antwortet.  Wenn Sie diese Datei erhalten, wissen Sie, dass AD FS Anforderungen genau über 443 verarbeitet.  Weitere Informationen finden Sie unter [AD FS Problembehandlung-Endpunkte](ad-fs-tshoot-endpoints.md).
- **IDP-initiierte Anmeldung** : können Sie sich über die IDP-initiierte Anmeldeseite anmelden und authentifizieren?  Sie müssen sicherstellen, dass diese Seite aktiviert wurde, da Sie standardmäßig deaktiviert ist.  Verwenden `Set-AdfsProperties -EnableIdPInitiatedSignOn $true` Sie, um die Seite zu aktivieren.  Wenn Sie sich anmelden und authentifizieren können, wissen Sie, dass AD FS in diesem Bereich funktioniert.  Weitere Informationen finden Sie unter [AD FS Troubleshooting-SignOn](ad-fs-tshoot-initiatedsignon.md).
  ##  <a name="common-troubleshooting-areas"></a>Allgemeine Problem Behandlungsbereiche

|Name|BESCHREIBUNG|
|-----|-----|
|[Ereignisprotokollierung und-Überwachung](ad-fs-tshoot-logging.md)|Verwenden Sie die Windows-Ereignisprotokolle, um allgemeine Informationen über die Administrator-und Ablauf Verfolgungs Protokolle anzuzeigen.  Sie kann auch verwendet werden, um die Sicherheitsüberwachung anzuzeigen.|
|[SQL-Konnektivität](ad-fs-tshoot-sql.md)|Informationen zum Testen der Konnektivität zwischen ihren AD FS Servern und den SQL-Back-End-Datenbanken|
|[Anspruchs Ausstellung](ad-fs-tshoot-claims-issuance.md)|Informationen zum bestimmen, ob AD FS Ansprüche ordnungsgemäß ausgibt.|
|[Schleifen Erkennung](ad-fs-tshoot-loop.md)|Informationen zum bestimmen und verhindern, dass Benutzer zwischen dem IDP und einem RP hin-und hergewechselt werden.|
|[Zertifikate](ad-fs-tshoot-certs.md)|Probleme mit typzertifikaten, die auftreten können|
|[Fiddler](ad-fs-tshoot-fiddler.md)|Informationen zum Installieren und Verwenden von "fddler"|
|[WS-Verbund mit "fddler"](ad-fs-tshoot-fiddler-ws-fed.md)|Ausführliche Ablauf Verfolgung einer WS-Verbund-Interaktion|
|[Anspruchs Regeln](ad-fs-tshoot-claims-rules.md)|Informationen zur Problembehandlung von Anspruchs Regeln und deren Syntax|
|[Integrierte Windows-Authentifizierung](ad-fs-tshoot-iwa.md)|Informationen zur Problembehandlung bei der integrierten Authentifizierung.|
|[Azure AD](ad-fs-tshoot-azure.md)|Informationen zur Problembehandlung AD FS Interaktion mit Azure AD.|
|[AD FS Diagnostics Analyzer](ad-fs-diagnostics-analyzer.md)|AD FS Help Diagnostics Analyzer kann bei der Ausführung grundlegender AD FS Prüfungen mithilfe des Diagnose-PowerShell-Moduls helfen.