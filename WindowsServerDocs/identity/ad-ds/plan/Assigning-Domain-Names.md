---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: Zuweisen von Domänennamen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: ba5a7ee8b7d9728c48e2798853aab8d55047e86f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59866561"
---
# <a name="assigning-domain-names"></a>Zuweisen von Domänennamen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie müssen einen Namen und jeder Domäne in Ihrem Plan zuweisen. Active Directory-Domänendienste (AD DS)-Domänen haben zwei Typen von Namen: Namen von Domain Name System (DNS) und NetBIOS-Namen. Beide Namen sind im Allgemeinen für Endbenutzer sichtbar. Die DNS-Namen des Active Directory-Domänen gehören zwei Komponenten: ein Präfix und Suffix. Beim Erstellen von Domänennamen ermitteln Sie zunächst das DNS-Präfix. Dies ist die erste Bezeichnung im DNS-Namen der Domäne. Wenn Sie den Namen der Stammdomäne der Gesamtstruktur auswählen, wird das Suffix bestimmt. Die folgende Tabelle enthält die Präfix-Benennungsregeln für DNS-Namen.  
  
|Regel|Erläuterung|  
|--------|---------------|  
|Wählen Sie ein Präfix, das nicht wahrscheinlich veraltet ist.|Vermeiden Sie Namen, z. B. eine Produktlinie oder das Betriebssystem, das in der Zukunft ändern kann. Es wird empfohlen, mithilfe von geografischen Namen.|  
|Wählen Sie ein Präfix, das Internet nur standardmäßige Zeichen enthält.|A-Z, a – Z, 0-9 und (-), aber nicht vollständig numerische.|  
|15 Zeichen enthalten oder weniger in das Präfix.|Bei Auswahl eine Präfixlänge von höchstens 15 Zeichen ist der NetBIOS-Name identisch mit dem Präfix.|  
  
Weitere Informationen finden Sie in der Namenskonventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629)).  
  
> [!NOTE]  
>  Obwohl Sie mit Dcpromo.exe in Windows Server 2008 und Windows Server 2003 einen einteiligen DNS-Domänennamen erstellen können, sollten Sie diesen für eine Domäne aus mehreren Gründen nicht verwenden. In Windows Server 2008 R2 können Sie mit Dcpromo.exe einen einteiligen DNS-Domänennamen für eine Domäne nicht erstellen. Weitere Informationen finden Sie unter [ https://go.microsoft.com/fwlink/?LinkId=92467.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
Wenn die aktuelle NetBIOS-Namen der Domäne nicht zulässig ist, der die Region darstellt oder nicht die Präfix-Benennungsregeln entsprechen, wählen Sie ein neues Präfix. In diesem Fall unterscheidet sich der NetBIOS-Name der Domäne aus dem DNS-Präfix der Domäne.  
  
Wählen Sie für jede neue Domäne, die Sie bereitstellen ein Präfix, für die Region geeignet ist und die Präfix-Benennungsregeln entspricht. Es wird empfohlen, der NetBIOS-Namen der Domäne, die das DNS-Präfix identisch sein.  
  
Dokumentieren Sie den DNS-Präfix und der NetBIOS-Namen, die Sie für jede Domäne in der Gesamtstruktur auswählen. Sie können die Informationen für DNS- und NetBIOS-Namen in das Arbeitsblatt "Planen der Domäne" hinzufügen, die Sie erstellt haben, um Ihren Plan für neue und aktualisierte Domänen zu dokumentieren. Laden Sie zum Öffnen von Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunter ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), und öffnen Sie "Domäne" Planning"(DSSLOGI_5.doc).  
  


