---
ms.assetid: 6b49cde3-d2cb-4ece-b9b7-dc600e037495
title: 'Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs'
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 165471fd06031a68343a54d019357afee782d082
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359946"
---
# <a name="checklist-implementing-a-federated-web-sso-design"></a>Prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs

Diese übergeordnete Prüfliste enthält Kreuz @ no__t-0reference Links zu wichtigen Konzepten zum Federated Web Single @ no__t-1sign @ no__t-2ON \(sso @ no__t-4 Design für Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-6. Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen Sie die Aufgaben in der untergeordneten Prüfliste durch, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![federated Web SSO @ no__t-1prüfliste: Implementieren eines Federated-Web-SSO-Entwurfs**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte zum Federated-Web-SSO-Entwurf, und legen Sie fest, welche AD FS Bereitstellungs Ziele Sie verwenden können, um diesen Entwurf an die Anforderungen Ihrer Organisation anzupassen.|![federated Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Federated Web SSO Design](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />![federated-Web-SSO,](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[das Ihre AD FS Bereitstellungs Ziele identifiziert](https://technet.microsoft.com/library/dd807053.aspx)<br /><br />![federated-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Bereitstellung](https://technet.microsoft.com/library/dd807083.aspx)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware, die Software, das Zertifikat, Domain Name System \(dns @ no__t-1, den Attribut Speicher und die Client Anforderungen für die Bereitstellung von AD FS in Ihrer Organisation.|![federated Web SSO @ no__t-1Anhang A: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte zu Ansprüchen, Anspruchs Regeln, Attribut speichern und der AD FS Konfigurations Datenbank, bevor Sie AD FS in beiden Partnerorganisationen bereitstellen.|![federated Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Konzepte](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan einen oder mehrere Verbund Server in jeder Partnerorganisation. **Hinweis**: Für den Federated-Web-SSO-Entwurf benötigen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation.|![federated Web SSO @ no__t-1prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|\(optional @ no__t-1 bestimmt, ob Ihre Organisation einen Verbund Server Proxy benötigt. Wenn Ihr Entwurfsplan einen Proxy aufruft, können Sie einen oder mehrere Verbund Server Proxys in jeder Partnerorganisation installieren.|![federated Web SSO @ no__t-1prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Geben Sie gemäß Ihrem Entwurfsplan Zertifikate frei, konfigurieren Sie Clients und konfigurieren Sie die Vertrauensstellungen in beiden Partnerorganisationen, damit sie über Verbundvertrauensstellung kommunizieren können.|![federated Web SSO @ no__t-1prüfliste: Konfigurieren der Konto Partner Organisation @ no__t-0<br /><br />![federated Web SSO @ no__t-1prüfliste: Konfigurieren der Ressourcen Partner Organisation @ no__t-0|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Wenn Sie Administrator in der Ressourcen Partnerorganisation sind, aktivieren Claims @ no__t-0ihre Webbrowser Anwendung, Webdienst Anwendung oder Microsoft® Office SharePoint® Server-Anwendung mithilfe von WIF und dem WIF SDK.|![federated Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![federated Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
