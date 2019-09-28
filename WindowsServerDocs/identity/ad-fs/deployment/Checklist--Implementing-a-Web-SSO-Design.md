---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: 'Prüfliste: Implementieren eines Web-SSO-Entwurfs'
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8488e0c9195930374aacd959e72d0eff34142ca7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408461"
---
# <a name="checklist-implementing-a-web-sso-design"></a>Prüfliste: Implementieren eines Web-SSO-Entwurfs

Diese übergeordnete Prüfliste enthält Kreuz @ no__t-0reference Links zu wichtigen Konzepten zum Web Single @ no__t-1sign @ no__t-2ON \(sso @ no__t-4 Design for Active Directory-Verbunddienste (AD FS) \(AD FS @ no__t-6. Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen die Aufgaben in der untergeordneten Prüfliste ab, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![web-SSO @ no__t-1prüfliste: Implementieren eines Web-SSO-Entwurfs**  
  
||Aufgabe|Referenz|  
|-|--------|-------------|  
|![Web-SSO](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte zum Web-SSO-Entwurf, und legen Sie fest, welche AD FS Bereitstellungs Ziele Sie verwenden können, um diesen Entwurf an die Anforderungen Ihrer Organisation anzupassen. **Hinweis**:|![web SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Web-SSO-Entwurf](https://technet.microsoft.com/library/dd807033.aspx)<br /><br />![web-SSO,](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[das Ihre AD FS Bereitstellungs Ziele identifiziert](https://technet.microsoft.com/library/dd807053.aspx)|  
|![Web-SSO](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware, die Software, das Zertifikat, Domain Name System \(dns @ no__t-1, den Attribut Speicher und die Client Anforderungen für die Bereitstellung von AD FS in Ihrer Organisation.|![web SSO @ no__t-1Anhang A: Überprüfen der AD FS-Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Web-SSO](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan mindestens einen Verbund Server im Unternehmensnetzwerk oder im Umkreis Netzwerk. **Hinweis**: Der Web-SSO-Entwurf erfordert, dass nur ein Verbund Server erfolgreich funktioniert. Ein einzelner Verbund Server agiert sowohl in der Rolle des Anspruchs Anbieters als auch in der Rolle der vertrauenden Seite.|![web-SSO @ no__t-1prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Web-SSO](media/icon_checkboxo.gif)|\(optional @ no__t-1 bestimmt, ob Ihre Organisation einen Verbund Server Proxy im Umkreis Netzwerk benötigt.|![web-SSO @ no__t-1prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Web-SSO](media/icon_checkboxo.gif)|Je nach Web-SSO-Entwurfsplan und der vorgesehenen Verwendung fügen Sie den entsprechenden Attributspeicher, die Vertrauensstellungen der vertrauenden Seite, die Ansprüche und die Anspruchsregeln für den Verbunddienst hinzu.|![web-SSO @ no__t-1prüfliste: Konfigurieren der Konto Partner Organisation @ no__t-0|  
|![Web-SSO](media/icon_checkboxo.gif)|Wenn Sie Administrator in der Ressourcen Partnerorganisation sind, aktivieren Claims @ no__t-0ihre Webbrowser Anwendung, Webdienst Anwendung oder Microsoft® Office SharePoint® Server-Anwendung mithilfe von WIF und dem WIF SDK. **Hinweis**:|![web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<br /><br />![web SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
