---
title: Erstellen eines Aliaseintrags (CNAME) in DNS für WEB1
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 442ee8b70311eaad3f0b3f263003786b6beab8bc
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813161"
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>Erstellen Sie einen Alias \(CNAME\) Datensätze in DNS für WEB1

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können dieses Verfahren einen kanonischen Aliasnamen hinzufügen \(CNAME\) -Ressourceneintrag für den Webserver zu einer Zone im DNS auf dem Domänencontroller. Mit CNAME-Datensätzen können Sie mehrere Namen zeigen Sie auf einen einzelnen Host, vereinfachen Sie z. B. Hosts, die sowohl eine File Transfer Protocol \(FTP\) Server und einem Webserver auf demselben Computer.   
  
Aus diesem Grund sind Sie kostenlos auf Ihrem Webserver zu verwenden, um die Zertifikatsperrliste hosten \(CRL\) Ihrer Zertifizierungsstelle \(Zertifizierungsstelle\) sowie um zusätzliche Dienste wie z. B. FTP oder Web-Server ausführen.  
  
Wenn Sie dieses Verfahren auszuführen, ersetzen **Aliasnamen** und anderen Variablen mit Werten, die für Ihre Bereitstellung geeignet sind.  
  
Um dieses Verfahren auszuführen, müssen Sie Mitglied werden **Domänen-Admins**.  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>Hinzufügen ein Alias \(CNAME\) zu einer Zone  
  
>[!NOTE]  
>Zum Ausführen dieses Verfahrens mithilfe von Windows PowerShell finden Sie unter [hinzufügen-DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx).  
  
1.  Klicken Sie auf DC1 im Server-Manager auf **Tools** , und klicken Sie dann auf **DNS**. Der DNS-Manager Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie in der Konsolenstruktur auf **Forward-Lookupzonen**, mit der rechten Maustaste in der forward-Lookupzone, in denen Sie möchten die fügen des Alias-Ressourceneintrag, und klicken Sie dann auf **neuer Alias \(CNAME\)** . Die **neuer Ressourcendatensatz** Dialogfeld wird geöffnet.  
  
3.  In **Aliasnamen**, geben Sie den Aliasnamen **Pki**.  
  
4.  Wenn Sie einen Wert für eingeben **Aliasnamen**, wird die **vollständig qualifizierten Domänennamen \(FQDN\)**  automatisch füllt das Dialogfeld. Wenn Sie Ihren Aliasnamen eingeben "Pki" und der Domäne ist ist z. B. "corp.contoso.com", den Wert **pki.corp.contoso.com** wird automatisch für Sie ausgefüllt.  
  
5.  In **vollständig qualifizierten Domänennamen \(FQDN\) Zielhosts**, geben Sie den FQDN Ihres Webservers. Geben Sie beispielsweise, wenn es sich bei Ihrem Webserver WEB1 den Namen und die Domäne "corp.contoso.com", **WEB1.corp.contoso.com**.  
  
6.  Klicken Sie auf **OK** des neuen Eintrags zur Zone hinzufügen.  
  

