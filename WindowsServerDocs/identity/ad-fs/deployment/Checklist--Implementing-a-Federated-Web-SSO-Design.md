---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: 'Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs'
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: e3c9f94ee1ce1e1fef2429a12fdb77604987fdb8
ms.sourcegitcommit: 3632b72f63fe4e70eea6c2e97f17d54cb49566fd
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2020
ms.locfileid: "87520039"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>Checkliste: Implementieren eines Entwurfs für Federated-Web-SSO

Diese übergeordnete Prüfliste enthält quer \- Verweise zu wichtigen Konzepten des Entwurfs für einmaliges Anmelden mit Verbund-Web- \- \- \( SSO \) für Active Directory-Verbunddienste (AD FS) \( AD FS \) . Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.

> [!NOTE]
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen Sie die Aufgaben in der untergeordneten Prüfliste durch, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.

![Verbund-Web-SSO-Prüfliste](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**: Implementieren eines Verbund Web-SSO-Entwurfs**

|Aufgabe|Verweis|
|--------|-------------|
|Informieren Sie sich über wichtige Konzepte zum Federated-Web-SSO-Entwurf, und legen Sie fest, welche AD FS Bereitstellungs Ziele Sie verwenden können, um diesen Entwurf an die Anforderungen Ihrer Organisation anzupassen.|![](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[WebSSO-Entwurf](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dd807050(v=ws.11)) für Verbund-Web-SSO<p>![Verbund-Web-SSO,](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[das Ihre AD FS Bereitstellungs Ziele identifiziert](../design/identifying-your-ad-fs-deployment-goals.md)<p>![Verbund-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Bereitstellung](../design/planning-your-deployment.md)|
|Überprüfen Sie die Hardware-, Software-, Zertifikat-, Domain Name System \( DNS \) -, Attribut Speicher-und Client Anforderungen für die Bereitstellung von AD FS in Ihrer Organisation.|![Verbund-Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Anhang A: Überprüfen der AD FS Anforderungen](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/ff678034(v=ws.11))|
|Informieren Sie sich über wichtige Konzepte zu Ansprüchen, Anspruchs Regeln, Attribut speichern und der AD FS Konfigurations Datenbank, bevor Sie AD FS in beiden Partnerorganisationen bereitstellen.|![Verbund-Web-SSO-Grundlegendes zu](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Schlüssel AD FS Konzepten](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|
|Installieren Sie gemäß Ihrem Entwurfsplan einen oder mehrere Verbund Server in jeder Partnerorganisation. **Hinweis:** Für den Federated-Web-SSO-Entwurf benötigen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation.|![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)|
|\(Optional \) : Legen Sie fest, ob Ihre Organisation einen Verbund Server Proxy benötigt. Wenn Ihr Entwurfsplan einen Proxy aufruft, können Sie einen oder mehrere Verbund Server Proxys in jeder Partnerorganisation installieren.|![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|
|Geben Sie gemäß Ihrem Entwurfsplan Zertifikate frei, konfigurieren Sie Clients und konfigurieren Sie die Vertrauensstellungen in beiden Partnerorganisationen, damit sie über Verbundvertrauensstellung kommunizieren können.|![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Konfigurieren der Konto Partner Organisation](Checklist--Configuring-the-Account-Partner-Organization.md)<p>![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Konfigurieren der Ressourcen Partner Organisation](Checklist--Configuring-the-Resource-Partner-Organization.md)|
|Wenn Sie Administrator in der Ressourcen Partnerorganisation sind, können Ansprüche \- Ihre Webbrowser Anwendung, Webdienst Anwendung oder Microsoft &reg; Office SharePoint &reg; Server-Anwendung mithilfe von WIF und dem WIF-SDK aktivieren.|![Verbund-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![Verbund-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|
