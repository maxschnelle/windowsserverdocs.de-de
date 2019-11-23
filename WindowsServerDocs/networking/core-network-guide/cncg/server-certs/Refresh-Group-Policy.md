---
title: Aktualisieren von Gruppenrichtlinien
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 88d39f41f61ae7c7f6a1fb84aa99806c4796c8cf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356187"
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
  


