---
title: Erstellen eines Aliaseintrags (CNAME) in DNS für WEB1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 9a966ab2883e22173ecf3e64e87d2a4b7a9c57d2
ms.sourcegitcommit: 68444968565667f86ee0586ed4c43da4ab24aaed
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87995584"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>Erstellen eines Alias \( CNAME- \) Datensatzes in DNS für WEB1

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mit diesem Verfahren können Sie einen kanonischen Alias namens \( CNAME- \) Ressourcen Daten Satz für Ihren Webserver zu einer Zone im DNS auf Ihrem Domänen Controller hinzufügen. Mit CNAME-Datensätzen können Sie mehr als einen Namen verwenden, um auf einen einzelnen Host zu verweisen. Dies vereinfacht das Hosten sowohl eines Dateiübertragungsprotokoll \( FTP \) -Servers als auch eines Webservers auf dem gleichen Computer.

Aus diesem Grund können Sie Ihren Webserver verwenden, um die Zertifikat Sperr Listen-CRL für die Zertifizierungsstellen-Zertifizierungsstelle zu hosten und \( \) \( \) um zusätzliche Dienste wie FTP oder Webserver auszuführen.

Ersetzen Sie beim Ausführen dieses Verfahrens **Alias Namen** und andere Variablen durch Werte, die für Ihre Bereitstellung geeignet sind.

Um dieses Verfahren auszuführen, müssen Sie Mitglied der Gruppe " **Domänen-Admins**" sein.

## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>So fügen Sie einer Zone einen Alias- \( CNAME- \) Ressourcen Daten Satz hinzu

>[!NOTE]
>Informationen dazu, wie Sie dieses Verfahren mithilfe von Windows PowerShell ausführen, finden [Sie unter Add-dnsserverresourcerecordcname](/powershell/module/dnsserver/add-dnsserverresourcerecordcname?view=winserver2012r2-ps).

1.  Klicken Sie auf DC1 in **Server-Manager auf Extras und dann** auf **DNS**. Der DNS-Manager Microsoft Management Console (MMC) wird geöffnet.

2.  Doppelklicken Sie in der Konsolen Struktur auf **Forward-Lookupzonen**, klicken Sie mit der rechten Maustaste auf die Forward-Lookupzone, in der Sie den Alias Ressourcen Daten Satz hinzufügen möchten, und klicken Sie dann auf **Neuer Alias \( CNAME \) **. Das Dialogfeld **neuer Ressourcen Daten Satz** wird geöffnet.

3.  Geben Sie unter **Alias Name**den Aliasnamen **PKI**ein.

4.  Wenn Sie einen Wert für **Alias Name**eingeben, wird der **voll qualifizierte Domänen Namen- \( FQDN \) ** im Dialogfeld automatisch ausgefüllt. Wenn Ihr Alias Name beispielsweise "PKI" lautet und Ihre Domäne corp.contoso.com ist, wird der Wert **PKI.Corp.contoso.com** automatisch für Sie ausgefüllt.

5.  Geben Sie im **voll qualifizierten Domänen Namen- \( FQDN des \) Zielhosts**den FQDN des Webservers ein. Wenn Ihr Webserver z. b. den Namen WEB1 und Ihre Domäne corp.contoso.com lautet, geben Sie **WEB1.Corp.contoso.com**ein.

6.  Klicken Sie auf **OK** , um der Zone den neuen Datensatz hinzuzufügen.