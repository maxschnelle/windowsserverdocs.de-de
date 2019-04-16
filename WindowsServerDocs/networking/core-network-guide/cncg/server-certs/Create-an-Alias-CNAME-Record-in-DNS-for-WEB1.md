---
title: Erstellen Sie ein Aliaseintrag (CNAME) in DNS für WEB1
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: bfae23f0-ae12-486b-94fe-50a137e141a5
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 65f10efe1cfd2866fb99406bf031197f6268b05b
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="create-an-alias-cname-record-in-dns-for-web1"></a>Erstellen Sie einen Alias \(CNAME\)-Eintrag in DNS für WEB1

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie einen Alias kanonischen Namen \(CNAME\)-Ressourceneintrag für den Webserver einer Zone in DNS auf dem Domänencontroller hinzufügen. CNAME-Datensätze können Sie mehr als einem Namen auf einen einzelnen Host erleichtern soll, z.B. Host einen \(FTP\) File Transfer Protocol-Server und einem Webserver auf demselben Computer zeigen.   
  
Aus diesem Grund werden auf Ihrem Webserver zu verwenden, um die zertifikatsperrung Hosten Ihrer Zertifizierungsstelle \(CRL\) Liste \(CA\) auch als weitere Dienste, z.B. Webserver ausführen.  
  
Wenn Sie dieses Verfahren ausführen, ersetzen Sie **Aliasnamen** und andere Variablen mit Werten, die für Ihre Bereitstellung geeignet sind.  
  
Zum Ausführen dieses Verfahrens müssen Sie Mitglied der sein **Domänen-Admins**.  
  
## <a name="to-add-an-alias-cname-resource-record-to-a-zone"></a>Hinzufügen ein Aliasressourceneintrags \(CNAME\) zu einer Zone  
  
>[!NOTE]  
>Um dieses Verfahren mithilfe von Windows PowerShell finden Sie unter [hinzufügen DnsServerResourceRecordCName](https://technet.microsoft.com/library/jj649894(v=wps.630).aspx).  
  
1.  Klicken Sie auf DC1 im Server-Manager auf **Tools**, und klicken Sie dann auf **DNS**. Der DNS-Manager Microsoft Management Console (MMC) wird geöffnet.  
  
2.  Doppelklicken Sie in der Konsolenstruktur auf **Forward-Lookupzonen**, mit der rechten Maustaste in der Forward-Lookupzone, in dem Sie hinzufügen möchten den Alias-Ressourceneintrag, und klicken Sie dann auf **neuen Alias \(CNAME\)**. Die **neuer Ressourcendatensatz** Dialogfeld wird geöffnet.  
  
3.  In **Aliasnamen**, geben Sie den Aliasnamen **Pki**.  
  
4.  Bei der Eingabe eines Werts für **Aliasnamen**, die **vollqualifizierten Domänennamen \(FQDN\)** Auto-füllt das Dialogfeld. Wenn Ihr Aliasname "Pki" und die Domäne ist z.B. corp.contoso.com, den Wert **pki.corp.contoso.com** wird automatisch für Sie ausgefüllt.  
  
5.  In **vollqualifizierten Domänennamen \(FQDN\) Zielhosts**, geben Sie den FQDN des Webservers. Geben Sie z.B. wenn Webservers WEB1 den Namen und die Domäne corp.contoso.com, **WEB1.corp.contoso.com**.  
  
6.  Klicken Sie auf **OK** den neuen Eintrag zur Zone hinzufügen.  
  

