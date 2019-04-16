---
title: Aktualisieren von Gruppenrichtlinien
description: In diesem Thema ist Teil des Handbuchs Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundenen und drahtlosen Bereitstellungen
manager: brianlic
ms.topic: article
ms.assetid: 65b36794-bb09-4c1b-a2e7-8fc780893d97
ms.prod: windows-server-threshold
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4d9f5d38199f8cf3c0ffe46df4cd975cd9c56ff6
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="refresh-group-policy"></a>Aktualisieren von Gruppenrichtlinien

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

Dieses Verfahrens können Sie Gruppenrichtlinien auf dem lokalen Computer manuell aktualisieren. Wenn Gruppenrichtlinien aktualisiert automatische Registrierung von Zertifikaten konfiguriert ist und ordnungsgemäß funktioniert, ist des lokalen Computers automatisch registrierte ein Zertifikat von der Zertifizierungsstelle (CA).  
  
> [!NOTE]  
> Gruppenrichtlinien werden automatisch aktualisiert, wenn Sie den Domänenmitgliedscomputer neu starten, oder wenn ein Benutzer an einem Domänenmitgliedscomputer anmeldet. Darüber hinaus wird der Gruppenrichtlinie in regelmäßigen Abständen aktualisiert. Standardmäßig ist dieser regelmäßige Aktualisierung alle 90Minuten mit einem zufälligen Versatz von bis zu 30Minuten ausgeführt.  
  
Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen.  
  
### <a name="to-refresh-group-policy-on-the-local-computer"></a>So aktualisieren Sie Gruppenrichtlinien auf dem lokalen Computer  
  
1.  Auf dem Computer, auf dem Netzwerkrichtlinienserver installiert ist, öffnen Sie Windows PowerShell&reg; mithilfe des Symbols auf der Taskleiste.  
  
2.  Geben Sie an der Windows PowerShell-Eingabeaufforderung **Gpupdate**, und drücken Sie dann die EINGABETASTE.  
  


