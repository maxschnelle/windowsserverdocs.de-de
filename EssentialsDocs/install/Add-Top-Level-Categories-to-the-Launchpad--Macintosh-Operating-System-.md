---
title: Hinzufügen von Kategorien der obersten Ebene zum Launchpad (Macintosh-Betriebssysteme)
description: Beschreibt die Verwendung von Windows Server Essentials
ms.date: 10/03/2016
ms.prod: windows-server
ms.topic: article
ms.assetid: ee2173c3-e464-4001-9f43-6d926a575092
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: c8a15a831a89afc55d20db4e1c1195173d466b3c
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80817513"
---
# <a name="add-top-level-categories-to-the-launchpad-macintosh-operating-system"></a>Hinzufügen von Kategorien der obersten Ebene zum Launchpad (Macintosh-Betriebssysteme)

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

Auf einem Computer mit Macintosh-Betriebssystem können Sie dem Launchpad Kategorien der obersten Ebene hinzufügen. Zum Erstellen eines Launchpad-Add-Ins, das Kategorien der obersten Ebene hinzufügt, können Sie eine Kombination aus Informationen auf dieser Seite und im Thema Gewusst wie: Hinzufügen von Aufgaben und Kategorien zum Launchpad verwenden? im [SDK für Windows Server-Lösungen](https://go.microsoft.com/fwlink/?LinkID=248648).  
  
 Im folgenden Beispiel wird gezeigt, wie Sie Ihren Launchpad-Eintrag als Kategorie der obersten Ebene in der .launchpad-Datei angeben können:  
  
```  
  
<?xml version="1.0" encoding="utf-8" ?>  
<LaunchPad resFile="Localizable">  
   <Category id="Microsoft.Launchpad.HomeCategory" name="SampleAddin"  image="SampleImage01.png">  
      <Task id="Microsoft.Launchpad.SampleAddin.Pictures"   
          name="Pictures"       
           src="smb://%ServerAddress%/Pictures"   
         image="SampleImage02.png"/>  
   </Category>  
</LaunchPad>  
```  
  
 Damit der Eintrag als Kategorie der obersten Ebene zählt, muss das ID-Attribut des Kategorieelements "Microsoft.Launchpad.HomeCategory" lauten.  
  
## <a name="see-also"></a>Weitere Informationen  
 [Erstellen und Anpassen des Abbilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Abbilds für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)