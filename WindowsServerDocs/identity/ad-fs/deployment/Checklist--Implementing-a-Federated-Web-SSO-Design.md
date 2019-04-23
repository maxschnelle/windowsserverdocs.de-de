---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: 'Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs'
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1122ee3814f656a7229dc2946d7441d525de5ae2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869671"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diese übergeordnete Prüfliste enthält plattformübergreifende\-verweisen auf die Links zu wichtigen Konzepten zum Federated Web Single\-anmelden\-auf \(SSO\) Entwurf für Active Directory Federation Services \(AD FS\). Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen Sie die Aufgaben in der untergeordneten Prüfliste durch, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Federated-Web-Sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie die wichtigen Konzepte zum Federated-Web-SSO-Entwurf aus, und bestimmen Sie die AD FS-Bereitstellungsziele, die Sie verwenden können, um diesen Entwurf auf die Anforderungen Ihrer Organisation anzupassen.|![Federated-Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federated Web SSO Design](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />![Federated-Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Identifizieren der AD FS-Bereitstellungsziele](https://technet.microsoft.com/library/dd807053.aspx)<br /><br />![Federated-Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Bereitstellung](https://technet.microsoft.com/library/dd807083.aspx)|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware, Software, Zertifikat, Domain Name System \(DNS\), Attributspeicher und Clientanforderungen für die Bereitstellung von AD FS in Ihrer Organisation.|![Federated-Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Anhang A: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie wichtige Konzepte zu Ansprüchen, Anspruchsregel, Attributspeicher und die AD FS-Konfigurationsdatenbank vor der Bereitstellung von AD FS in beiden Partnerorganisationen.|![Federated-Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Concepts](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan einen oder mehrere Verbundserver in jeder Partnerorganisation ein. **Hinweis**: Für den Federated-Web-SSO-Entwurf benötigen Sie mindestens einen Verbundserver in der Kontopartnerorganisation und mindestens einen Verbundserver in der Ressourcenpartnerorganisation.|![Federated-Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Das Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|\(Optionale\) zu bestimmen, und zwar unabhängig davon, ob Ihre Organisation einen Verbundserverproxy benötigt. Wenn Ihr Entwurfsplan einen Proxy vorsieht, können Sie eine oder mehrere Verbundserverproxys in jeder Partnerorganisation installieren.|![Federated-Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Das Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|Geben Sie gemäß Ihrem Entwurfsplan Zertifikate frei, konfigurieren Sie Clients und konfigurieren Sie die Vertrauensstellungen in beiden Partnerorganisationen, damit sie über Verbundvertrauensstellung kommunizieren können.|![Federated-Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Konfigurieren der Kontopartnerorganisation](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![Federated-Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Konfigurieren der Ressourcenpartnerorganisation](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![Federated-Web-sso](media/icon_checkboxo.gif)|Wenn Sie ein Administrator in der Ressourcenpartnerorganisation sind, Ansprüche\-Ihre Webbrowseranwendung, Webdienstanwendung oder Microsoft® Office SharePoint® Server-Anwendung mithilfe von WIF und WIF-SDK zu aktivieren.|![Federated-Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![federated web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
