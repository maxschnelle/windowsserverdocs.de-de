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
# <a name="checklist-implementing-a-federated-web-sso-design"></a>Checkliste: Implementieren eines Entwurfs für Federated-Web-SSO

Diese übergeordnete Prüfliste enthält quer\-Referenz Links zu wichtigen Konzepten der Verbund-Web-\-Sign\-on \(SSO\) Design for Active Directory-Verbunddienste (AD FS) \(AD FS\). Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen Sie die Aufgaben in der untergeordneten Prüfliste durch, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Verbund-Web-SSO-Prüfliste](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**: Implementieren eines Verbund Web SSO-Entwurfs**  
  
||Aufgabe|Verweis|  
|-|--------|-------------|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte zum Federated-Web-SSO-Entwurf, und legen Sie fest, welche AD FS Bereitstellungs Ziele Sie verwenden können, um diesen Entwurf an die Anforderungen Ihrer Organisation anzupassen.|![Verbund Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Verbund Web SSO Design](https://technet.microsoft.com/library/dd807050.aspx)<br /><br />![Verbund-Web-SSO,](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[das Ihre AD FS Bereitstellungs Ziele identifiziert](https://technet.microsoft.com/library/dd807053.aspx)<br /><br />![Verbund-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Planen der Bereitstellung](https://technet.microsoft.com/library/dd807083.aspx)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware-, Software-, Zertifikat-, Domain Name System \(DNS-\), den Attribut Speicher und die Client Anforderungen für die Bereitstellung AD FS in Ihrer Organisation.|![Verbund Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Anhang A: Überprüfen von AD FS Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte zu Ansprüchen, Anspruchs Regeln, Attribut speichern und der AD FS Konfigurations Datenbank, bevor Sie AD FS in beiden Partnerorganisationen bereitstellen.|![Verbund Web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Understanding Key AD FS Konzepte](../../ad-fs/technical-reference/Understanding-Key-AD-FS-Concepts.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan einen oder mehrere Verbund Server in jeder Partnerorganisation. **Hinweis:** Für den Federated-Web-SSO-Entwurf benötigen Sie mindestens einen Verbund Server in der Konto Partnerorganisation und mindestens einen Verbund Server in der Ressourcen Partnerorganisation.|![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|\(optional\) bestimmen, ob Ihre Organisation einen Verbund Server Proxy benötigt. Wenn Ihr Entwurfsplan einen Proxy aufruft, können Sie einen oder mehrere Verbund Server Proxys in jeder Partnerorganisation installieren.|![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Geben Sie gemäß Ihrem Entwurfsplan Zertifikate frei, konfigurieren Sie Clients und konfigurieren Sie die Vertrauensstellungen in beiden Partnerorganisationen, damit sie über Verbundvertrauensstellung kommunizieren können.|![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Konfigurieren der Konto Partner Organisation](Checklist--Configuring-the-Account-Partner-Organization.md)<br /><br />![Verbund-Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Konfigurieren der Ressourcen Partner Organisation](Checklist--Configuring-the-Resource-Partner-Organization.md)|  
|![Verbund-Web-SSO](media/icon_checkboxo.gif)|Wenn Sie ein Administrator in der Ressourcen Partnerorganisation sind, können Ansprüche\-ihre Webbrowser Anwendung, Webdienst Anwendung oder Microsoft® Office SharePoint® Server-Anwendung mithilfe von WIF und dem WIF SDK aktivieren.|![Verbund-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![Verbund-Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)|  
