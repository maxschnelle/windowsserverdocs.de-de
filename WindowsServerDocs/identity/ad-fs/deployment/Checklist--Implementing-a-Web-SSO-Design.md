---
ms.assetid: 30657638-5709-48c5-87aa-98f688e07b4c
title: 'Prüfliste: Implementieren eines Web-SSO-Entwurfs'
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 298233eb20bd54e3e07eb87e029211502142b215
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855213"
---
# <a name="checklist-implementing-a-web-sso-design"></a>Checkliste: Implementieren eines Web-SSO-Entwurfs

Diese übergeordnete Prüfliste enthält quer\-Referenz Links zu wichtigen Konzepten zum Web Single\-Sign\-on \(SSO\) Design for Active Directory-Verbunddienste (AD FS) \(AD FS\). Sie enthält außerdem Links zu untergeordneten Prüflisten, die Sie beim Abschließen der Aufgaben unterstützen, die für die Implementierung dieses Entwurfs erforderlich sind.  
  
> [!NOTE]  
> Führen Sie die Aufgaben in dieser Prüfliste in der angegebenen Reihenfolge aus. Wenn ein Link auf ein grundlegendes Thema oder eine untergeordnete Prüfliste verweist, kehren Sie nach der Durchsicht des grundlegenden Themas zu diesem Thema zurück oder schließen die Aufgaben in der untergeordneten Prüfliste ab, damit Sie dann mit den übrigen Aufgaben in dieser Prüfliste fortfahren können.  
  
![Web-SSO-](media/2b05dce3-938f-4168-9b8f-1f4398cbdb9b.gif)**Checkliste: Implementieren eines Web-SSO-Entwurfs**  
  
||Aufgabe|Verweis|  
|-|--------|-------------|  
|![Web-SSO](media/icon_checkboxo.gif)|Informieren Sie sich über wichtige Konzepte zum Web-SSO-Entwurf, und legen Sie fest, welche AD FS Bereitstellungs Ziele Sie verwenden können, um diesen Entwurf an die Anforderungen Ihrer Organisation anzupassen. **Hinweis:**|Web-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[SSO-Entwurf](https://technet.microsoft.com/library/dd807033.aspx) für ![Web-SSO<p>![Web-SSO,](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[das Ihre AD FS Bereitstellungs Ziele identifiziert](https://technet.microsoft.com/library/dd807053.aspx)|  
|![Web-SSO](media/icon_checkboxo.gif)|Überprüfen Sie die Hardware-, Software-, Zertifikat-, Domain Name System \(DNS-\), den Attribut Speicher und die Client Anforderungen für die Bereitstellung AD FS in Ihrer Organisation.|![Web-SSO-](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Anhang A: Überprüfen der AD FS Anforderungen](https://technet.microsoft.com/library/ff678034.aspx)|  
|![Web-SSO](media/icon_checkboxo.gif)|Installieren Sie gemäß Ihrem Entwurfsplan mindestens einen Verbund Server im Unternehmensnetzwerk oder im Umkreis Netzwerk. **Hinweis:** Der Web-SSO-Entwurf erfordert, dass nur ein Verbund Server erfolgreich funktioniert. Ein einzelner Verbund Server agiert sowohl in der Rolle des Anspruchs Anbieters als auch in der Rolle der vertrauenden Seite.|![Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Einrichten eines Verbund Servers](Checklist--Setting-Up-a-Federation-Server.md)|  
|![Web-SSO](media/icon_checkboxo.gif)|\(optional\) bestimmen, ob Ihre Organisation einen Verbund Server Proxy im Umkreis Netzwerk benötigt.|![Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Einrichten eines Verbund Server Proxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)|  
|![Web-SSO](media/icon_checkboxo.gif)|Je nach Web-SSO-Entwurfsplan und der vorgesehenen Verwendung fügen Sie den entsprechenden Attributspeicher, die Vertrauensstellungen der vertrauenden Seite, die Ansprüche und die Anspruchsregeln für den Verbunddienst hinzu.|![Web-SSO-Prüfliste](media/bc6cea1a-1c6c-4124-8c8f-1df5adfe8c88.gif)[: Konfigurieren der Konto Partner Organisation](Checklist--Configuring-the-Account-Partner-Organization.md)|  
|![Web-SSO](media/icon_checkboxo.gif)|Wenn Sie ein Administrator in der Ressourcen Partnerorganisation sind, können Ansprüche\-ihre Webbrowser Anwendung, Webdienst Anwendung oder Microsoft&reg; Office SharePoint&reg; Server-Anwendung mithilfe von WIF und dem WIF SDK aktivieren. **Hinweis:**|![Web-SSO von](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266)<p>![Web-SSO](media/faa393df-4856-4431-9eda-4f4e5be72a90.gif)[Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266)| 
