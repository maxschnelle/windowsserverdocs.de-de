---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: "Zuweisen von Domänennamen"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 0d5ec9b76798f21503f650527a7961cff0b592b4
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="assigning-domain-names"></a>Zuweisen von Domänennamen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Sie müssen jede Domäne in Ihrem Plan einen Namen zuweisen. Active Directory-Domänendienste (AD DS)-Domänen sind zwei Arten von Namen: Domain Name System (DNS) und NetBIOS-Namen. Beide Namen sind im Allgemeinen für Endbenutzer sichtbar. Die DNS-Namen der Active Directory-Domänen gehören zwei Teile, ein Präfix und ein Suffix. Beim Erstellen von Domänennamen, ermitteln Sie zunächst das DNS-Präfix. Dies ist die Bezeichnung des ersten in den DNS-Namen der Domäne. Wenn Sie den Namen der Stammdomäne der Gesamtstruktur auswählen, wird das Suffix bestimmt. Die folgende Tabelle enthält das Präfix Benennungsregeln für DNS-Namen.  
  
|Regel|Erläuterung|  
|--------|---------------|  
|Wählen Sie ein Präfix, das nicht wahrscheinlich veraltet ist.|Vermeiden Sie Namen, z. B. einer Produktfamilie oder das Betriebssystem, die in der Zukunft ändern kann. Wir empfehlen die Verwendung von geografischer Namen.|  
|Wählen Sie ein Präfix, das nur Internet standard Zeichen enthält.|A-Z, a-Z, 0-9 und (-), aber nicht vollständig numerischen.|  
|Mehr als 15 Zeichen enthalten oder weniger in das Präfix.|Wenn Sie eine Präfixlänge von höchstens 15 Zeichen auswählen, wird der NetBIOS-Name identisch mit dem Präfix.|  
  
Weitere Informationen finden Sie unter Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629)).  
  
> [!NOTE]  
>  Obwohl Dcpromo.exe in Windows Server 2008 und Windows Server 2003 einen einteiligen DNS-Domänennamen erstellen können, sollten Sie einen einteiligen DNS-Namen für eine Domäne nicht mehreren Gründen verwenden. In Windows Server 2008 R2 lässt Dcpromo.exe nicht um einen einteiligen DNS-Namen für eine Domäne erstellen. Weitere Informationen finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=92467.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
Wenn Sie der aktuelle NetBIOS-Namen der Domäne ist zum Darstellen der Region ungeeignet oder nicht das Präfix Benennungsregeln erfüllen, wählen Sie ein neues Präfix. In diesem Fall unterscheidet sich der NetBIOS-Name der Domäne aus dem DNS-Präfix der Domäne.  
  
Wählen Sie für jede neue Domäne, die Sie bereitstellen, ein Präfix, das eignet sich für die Region und Präfix Benennungsregeln erfüllt. Wir empfehlen, der NetBIOS-Namen der Domäne der DNS-Präfix identisch sein.  
  
Dokumentieren Sie den DNS-Präfix und den NetBIOS-Namen, die Sie für jede Domäne in der Gesamtstruktur auswählen. Sie können die Informationen zu DNS und NetBIOS-Namen in das Arbeitsblatt "Planen der Domäne" hinzufügen, die Sie erstellt haben, um die Planung der neuen und aktualisierten Domänen zu dokumentieren. Um es zu öffnen, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip vom Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie "Domäne" Planning"(DSSLOGI_5.doc).  
  


