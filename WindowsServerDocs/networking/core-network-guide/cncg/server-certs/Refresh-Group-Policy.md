---
title: Aktualisieren von Gruppenrichtlinien
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X verkabelte und drahtlose Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 83dd48297535aafe30e48fe37010d81b279f4c91
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59863451"
---
# <a name="refresh-group-policy"></a>Aktualisieren von Gruppenrichtlinien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Mithilfe dieses Verfahrens können Sie die Gruppenrichtlinie auf dem lokalen Computer aktualisieren. Wenn ist die Gruppenrichtlinie aktualisiert, wenn der automatischen Registrierung von Zertifikaten konfiguriert und ordnungsgemäß funktioniert, der lokale Computer ist ein Zertifikat von der Zertifizierungsstelle (CA).  
  
> [!NOTE]  
> Die Gruppenrichtlinie wird automatisch aktualisiert, wenn Sie den Domänenmitgliedscomputer neu starten oder ein Benutzer sich an einem Domänenmitgliedscomputer anmeldet. Darüber hinaus wird eine Gruppenrichtlinie in regelmäßigen Abständen aktualisiert. Standardmäßig wird diese regelmäßige Aktualisierung alle 90 Minuten mit einem zufälligen Versatz von bis zu 30 Minuten ausgeführt.  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, damit Sie dieses Verfahren durchführen können.  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>So aktualisieren Sie die Gruppenrichtlinie auf dem lokalen Computer  
  
1.  Auf dem Computer, auf dem Netzwerkrichtlinienserver installiert ist, öffnen Sie Windows PowerShell&reg; mithilfe des Symbols auf der Taskleiste.  
  
2.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **Gpupdate**, und drücken Sie dann die EINGABETASTE.  
  


