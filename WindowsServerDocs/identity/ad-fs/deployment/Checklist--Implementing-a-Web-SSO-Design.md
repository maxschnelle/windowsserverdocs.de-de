---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: "Prüfliste - Implementieren eines Web-SSO-Entwurfs"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 265daf3acb9632aa92f85962abc44a6a9ea8dfed
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="checklist-implementing-a-web-sso-design"></a>Prüfliste: Implementieren eines Web-SSO-Entwurfs

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Diese übergeordnete Prüfliste enthält Cross\-Referenz-Links zu wichtigen Begriffen für das Web Singlethread-Standardparameter auf \(SSO\) Entwurf für Active Directory Federation Services \(AD FS\). Es enthält auch Links zu untergeordneten Prüflisten, die Ihnen bei der Aufgaben, die zum Implementieren dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der Reihenfolge. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, zurück zu diesem Thema, das konzeptuelle Thema überprüfen oder führen Sie die Aufgaben in der untergeordneten Prüfliste, so dass Sie mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Web-SSO-](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Prüfliste: Implementieren eines Web-SSO-Entwurfs**  
  
||Aufgabe|Referenz zu|  
|-|--------|-------------|  
|![Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie wichtiger Konzepte zum Web-SSO-Entwurf und bestimmen Sie, welche AD FS-Bereitstellungsziele, die Sie verwenden können, um diesen Entwurf an die Anforderungen Ihrer Organisation anzupassen. **Hinweis:**|![Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web-SSO-Entwurf](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Identifizieren der AD FS-Bereitstellungsziele](https://technet.microsoft.com/library/dd807053.aspx)|  
|![Web-sso](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware, Software, Zertifikat, Domain Name System \(DNS\), Attributspeicher und Clientanforderungen für die Bereitstellung von AD FS in Ihrer Organisation.|![Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Anhang A: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Web-sso](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan einen oder mehrere Verbundserver im Unternehmensnetzwerk oder im Umkreisnetzwerk. **Hinweis:** der Web-SSO-Entwurf erfordert nur einen Verbundserver erfolgreich funktioniert. Ein einzelnen Verbundserver fungiert in die Ansprüche Anbieter-Rolle und der relying Party-Rolle.|![Web-SSO-](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Checklist: Setting Up a Federation Server](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Web-sso](media/icon_checkboxo.gif)|\(Optional\) bestimmen, ob Ihre Organisation einen Verbundserverproxy im Umkreisnetzwerk benötigt.|![Web-SSO-](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Web-sso](media/icon_checkboxo.gif)|Je nach Ihrem Web-SSO-Entwurfsplan und wie Sie sie verwenden möchten fügen Sie den entsprechenden Attributspeicher, die Vertrauensstellungen der vertrauenden Seite Vertrauensstellungen, Ansprüche, und die Anspruchsregeln für den Verbunddienst.|![Web-SSO-](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[Prüfliste: Konfigurieren der Kontopartnerorganisation](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![Web-sso](media/icon_checkboxo.gif)|Wenn Sie ein Administrator in der Ressourcenpartnerorganisation sind Claims\ aktivieren Ihre Webbrowseranwendung, Webdienstanwendung oder Microsoft® Office SharePoint® Server-Anwendung, die mit dem WIF und WIF-SDK. **Hinweis:**|![Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
