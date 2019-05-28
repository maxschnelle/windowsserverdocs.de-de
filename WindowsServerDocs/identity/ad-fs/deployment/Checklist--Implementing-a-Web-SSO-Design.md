---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: 'Prüfliste: Implementieren eines Web-SSO-Entwurfs'
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: b2e09addbdc192bc6ce93a4402e6a6e61873ad56
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/24/2019
ms.locfileid: "66192365"
---
# <a name="checklist-implementing-a-web-sso-design"></a>Prüfliste: Implementieren eines Web-SSO-Entwurfs

Diese übergeordnete Prüfliste enthält plattformübergreifende\-verweisen auf die Links zu wichtigen Konzepten zum Web Single\-anmelden\-auf \(SSO\) Entwurf für Active Directory Federation Services \(AD FS \). Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen die Aufgaben in der untergeordneten Prüfliste ab, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Web-Sso](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Implementieren eines Web-SSO-Entwurfs**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie wichtiger Konzepte zum Web-SSO-Entwurf aus, und bestimmen Sie die AD FS-Bereitstellungsziele, die Sie verwenden können, um diesen Entwurf auf die Anforderungen Ihrer Organisation anzupassen. **Hinweis**:|![Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web SSO Design](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Identifizieren der AD FS-Bereitstellungsziele](https://technet.microsoft.com/library/dd807053.aspx)|  
|![Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware, Software, Zertifikat, Domain Name System \(DNS\), Attributspeicher und Clientanforderungen für die Bereitstellung von AD FS in Ihrer Organisation.|![Web-Sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Anhang A: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Web-sso](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan einen oder mehrere Verbundserver im Unternehmensnetzwerk oder im Umkreisnetzwerk. **Hinweis**: Der Web-SSO-Entwurf erfordert nur einen Verbundserver erfolgreich ausgeführt. Ein einzelnen Verbundservers fungiert in der Anbieterrolle Ansprüchen und der vertrauenden Seite parteienrolle.|![Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Web-sso](media/icon_checkboxo.gif)|\(Optionale\) zu bestimmen, und zwar unabhängig davon, ob Ihre Organisation einen Verbundserverproxy im Umkreisnetzwerk benötigt.|![Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Web-sso](media/icon_checkboxo.gif)|Je nach Web-SSO-Entwurfsplan und der vorgesehenen Verwendung fügen Sie den entsprechenden Attributspeicher, die Vertrauensstellungen der vertrauenden Seite, die Ansprüche und die Anspruchsregeln für den Verbunddienst hinzu.|![Web-Sso](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Konfigurieren der Kontopartnerorganisation](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![Web-sso](media/icon_checkboxo.gif)|Wenn Sie ein Administrator in der Ressourcenpartnerorganisation sind, Ansprüche\-Ihre Webbrowseranwendung, Webdienstanwendung oder Microsoft® Office SharePoint® Server-Anwendung mithilfe von WIF und WIF-SDK zu aktivieren. **Hinweis**:|![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![web sso](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
