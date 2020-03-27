---
title: Aktualisieren von Gruppenrichtlinien
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server
ms.technology: networking
ms.author: lizross
author: eross-msft
ms.openlocfilehash: b9522909960470d9f5f3e183afbd97ab1b919019
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80318251"
---
# <a name="refresh-group-policy"></a>Aktualisieren von Gruppenrichtlinien

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Mithilfe dieses Verfahrens können Sie die Gruppenrichtlinie auf dem lokalen Computer aktualisieren. Wenn Gruppenrichtlinie aktualisiert wird und die automatische Zertifikat Registrierung konfiguriert ist und ordnungsgemäß funktioniert, wird der lokale Computer von der Zertifizierungsstelle (Certification Authority, ca) automatisch zu einem Zertifikat registriert.  
  
> [!NOTE]  
> Die Gruppenrichtlinie wird automatisch aktualisiert, wenn Sie den Domänenmitgliedscomputer neu starten oder ein Benutzer sich an einem Domänenmitgliedscomputer anmeldet. Außerdem wird Gruppenrichtlinie regelmäßig aktualisiert. Standardmäßig wird diese regelmäßige Aktualisierung alle 90 Minuten mit einem zufälligen Offset von bis zu 30 Minuten ausgeführt.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>So aktualisieren Sie die Gruppenrichtlinie auf dem lokalen Computer  
  
1.  Öffnen Sie auf dem Computer, auf dem NPS installiert ist, Windows PowerShell-&reg;, indem Sie das Symbol auf der Taskleiste verwenden.  
  
2.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **gpupdate**ein, und drücken Sie dann die EINGABETASTE.  
  


