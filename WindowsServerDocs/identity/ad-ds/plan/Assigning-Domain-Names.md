---
ms.assetid: 73897497-b189-4305-b234-e057ffda163a
title: Zuweisen von Domänennamen
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 357c136f108c6d8e9e2a15dd9449ab61663079e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408991"
---
# <a name="assigning-domain-names"></a>Zuweisen von Domänennamen

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sie müssen jeder Domäne in Ihrem Plan einen Namen zuweisen. Active Directory Domain Services Domänen (AD DS) haben zwei Arten von Namen: Domain Name System (DNS)-Namen und NetBIOS-Namen. Im Allgemeinen sind beide Namen für Endbenutzer sichtbar. Die DNS-Namen Active Directory Domänen umfassen zwei Teile: ein Präfix und ein Suffix. Wenn Sie Domänen Namen erstellen, bestimmen Sie zuerst das DNS-Präfix. Dies ist die erste Bezeichnung im DNS-Namen der Domäne. Das Suffix wird bestimmt, wenn Sie den Namen der Gesamtstruktur-Stamm Domäne auswählen. In der folgenden Tabelle werden die Präfix-Benennungs Regeln für DNS-Namen aufgelistet.  
  
|Regel|Erläuterung|  
|--------|---------------|  
|Wählen Sie ein Präfix aus, das wahrscheinlich nicht mehr veraltet ist.|Vermeiden Sie Namen wie z. b. eine Produktlinie oder ein Betriebssystem, die sich in der Zukunft ändern können. Es wird empfohlen, geografische Namen zu verwenden.|  
|Wählen Sie ein Präfix aus, das nur Internet Standard Zeichen enthält.|A-z, a-z, 0-9 und (-), aber nicht vollständig numerisch.|  
|Fügen Sie im Präfix höchstens 15 Zeichen ein.|Wenn Sie eine Präfix Länge von höchstens 15 Zeichen auswählen, ist der NetBIOS-Name das gleiche wie das Präfix.|  
  
Weitere Informationen finden Sie unter Benennungs Konventionen in Active Directory für Computer, Domänen, Standorte und Organisationseinheiten ([https://go.microsoft.com/fwlink/?LinkId=106629](https://go.microsoft.com/fwlink/?LinkId=106629)).  
  
> [!NOTE]  
>  Obwohl Sie mit Dcpromo.exe in Windows Server 2008 und Windows Server 2003 einen einteiligen DNS-Domänennamen erstellen können, sollten Sie diesen für eine Domäne aus mehreren Gründen nicht verwenden. In Windows Server 2008 R2 können Sie mit Dcpromo.exe einen einteiligen DNS-Domänennamen für eine Domäne nicht erstellen. Weitere Informationen finden Sie unter [https://go.microsoft.com/fwlink/?LinkId=92467.](https://go.microsoft.com/fwlink/?LinkId=92467)   
  
Wenn der aktuelle NetBIOS-Name der Domäne ungeeignet ist, um den Bereich darzustellen, oder die Präfix-Benennungs Regeln nicht erfüllen, wählen Sie ein neues Präfix aus. In diesem Fall unterscheidet sich der NetBIOS-Name der Domäne vom DNS-Präfix der Domäne.  
  
Wählen Sie für jede neu bereitgestellte Domäne ein Präfix aus, das für die Region geeignet ist und die Präfix-Benennungs Regeln erfüllt. Es wird empfohlen, dass der NetBIOS-Name der Domäne mit dem DNS-Präfix identisch ist.  
  
Dokumentieren Sie das DNS-Präfix und die NetBIOS-Namen, die Sie für jede Domäne in der Gesamtstruktur auswählen. Sie können die DNS-und NetBIOS-Namensinformationen dem Arbeitsblatt "Domänen Planung" hinzufügen, das Sie erstellt haben, um den Plan für neue und aktualisierte Domänen zu dokumentieren. Um es zu öffnen, laden Sie Job_Aids_Designing_and_Deploying_Directory_and_Security_Services. zip aus den Auftrags Hilfen für Windows Server 2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)) herunter, und öffnen Sie "Domänen Planung" (DSSLOGI_5. doc).  
  


