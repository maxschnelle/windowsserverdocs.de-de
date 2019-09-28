---
title: Erstellen eines Aliaseintrags (CNAME) in DNS für WEB1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 77b8e464d2d8fab8803477e59826c3e715c0a6d2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406301"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>Erstellen Sie einen Alias \(cname @ no__t-1-Datensatz in DNS für WEB1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie einen kanonischen Alias Namen \(cname @ no__t-1-Ressourcen Daten Satz für Ihren Webserver zu einer Zone im DNS auf Ihrem Domänen Controller hinzufügen. Mit CNAME-Datensätzen können Sie mehr als einen Namen verwenden, um auf einen einzelnen Host zu verweisen. Dies vereinfacht das Hosten eines Dateiübertragungsprotokoll \(ftp @ no__t-1-Servers und eines Webservers auf dem gleichen Computer.   
  
Aus diesem Grund können Sie Ihren Webserver verwenden, um die Zertifikat Sperr Liste \(crl @ no__t-1 für Ihre Zertifizierungsstelle \(CA @ no__t-3 zu hosten und zusätzliche Dienste wie FTP oder Webserver auszuführen.  
  
Ersetzen Sie beim Ausführen dieses Verfahrens **Alias Namen** und andere Variablen durch Werte, die für Ihre Bereitstellung geeignet sind.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe " **Domänen-Admins**" sein.  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>So fügen Sie einer Zone einen Alias \(cname @ no__t-1-Ressourcen Daten Satz hinzu  
  
>[!NOTE]  
>Informationen dazu, wie Sie dieses Verfahren mithilfe von Windows PowerShell ausführen, finden [Sie unter Add-dnsserverresourcerecordcname](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx).  
  
1.  Klicken Sie auf DC1 in **Server-Manager auf Extras und dann** auf **DNS**. Der DNS-Manager Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie in der Konsolen Struktur auf **Forward-Lookupzonen**, klicken Sie mit der rechten Maustaste auf die Forward-Lookupzone, in der Sie den Alias Ressourcen Daten Satz hinzufügen möchten, und klicken Sie dann auf **Neuer Alias \(cname @ no__t-3**. Das Dialogfeld **neuer Ressourcen Daten Satz** wird geöffnet.  
  
3.  Geben Sie unter **Alias Name**den Aliasnamen **PKI**ein.  
  
4.  Wenn Sie einen Wert für **Alias Name**eingeben, wird im Dialogfeld der **voll qualifizierte Domänen Name \(fqdn @ no__t-3** automatisch ausgefüllt. Wenn Ihr Alias Name beispielsweise "PKI" lautet und Ihre Domäne corp.contoso.com ist, wird der Wert **PKI.Corp.contoso.com** automatisch für Sie ausgefüllt.  
  
5.  Geben Sie unter **voll qualifizierter Domänen Name \(fqdn @ no__t-2 für Zielhost den voll qualifizierten Domänen Namen**(FQDN) des Webservers ein. Wenn Ihr Webserver z. b. den Namen WEB1 und Ihre Domäne corp.contoso.com lautet, geben Sie **WEB1.Corp.contoso.com**ein.  
  
6.  Klicken Sie auf **OK** , um der Zone den neuen Datensatz hinzuzufügen.  
  

