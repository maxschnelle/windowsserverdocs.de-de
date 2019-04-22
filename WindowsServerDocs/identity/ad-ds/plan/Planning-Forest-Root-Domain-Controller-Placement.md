---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 57eafcc884a827d98c249e2da0c0af6888abc5b9
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59823641"
---
# <a name="planning-forest-root-domain-controller-placement"></a>Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Domänencontrollern im Gesamtstrukturstamm sind erforderlich, Sie Vertrauenspfaden für Clients zu erstellen, benötigen Zugriff auf Ressourcen in anderen Domänen als ihre eigenen. Platzieren Sie Domänencontrollern im Gesamtstrukturstamm an Hubstandorten und an Standorten, die Rechenzentren zu hosten. Wenn Benutzer in einem bestimmten Standort Zugriff auf Ressourcen von anderen Domänen in demselben Speicherort benötigen, und die netzwerkverfügbarkeit zwischen dem Datencenter und der Standort des Benutzers nicht zuverlässig ist, Sie können eine Stammdomänencontroller der Gesamtstruktur am Speicherort hinzufügen oder Erstellen einer vertrauensstellungsabkürzung zwischen den beiden Domänen. Es ist kosteneffizienter, eine vertrauensstellungsabkürzung zwischen den Domänen erstellen, es sei denn, Sie auch aus anderen Gründen eine Stammdomänencontroller der Gesamtstruktur an dieser Stelle zu platzieren.  
  
Verknüpfte Vertrauensstellungen Hilfe, um authentifizierungsanforderungen, die von Benutzern in beiden Domänen zu optimieren. Weitere Informationen zu Verknüpfungsvertrauensstellungen zwischen Domänen, finden Sie im Artikel [Kenntnisse beim Erstellen einer Verknüpfung Vertrauensstellung](https://go.microsoft.com/fwlink/?LinkId=107061).  
  
Ein Arbeitsblatt, das Sie beim Dokumentieren Ihrer Platzierung der Stammdomänencontroller der Gesamtstruktur zu unterstützen, finden Sie unter [Auftrag Hilfsmittel für Windows Server 2003 Deployment Kit](https://go.microsoft.com/fwlink/?LinkID=102558), Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip herunterladen , und öffnen Sie "Domänencontrollerkapazität" (DSSTOPO_4.doc).  
  
Sie benötigen, um auf diese Informationen verweisen, bei der Erstellung von Gesamtstruktur-Stammdomäne. Weitere Informationen zum Bereitstellen der Stammdomäne der Gesamtstruktur finden Sie unter [Bereitstellen einer Windows Server 2008-Gesamtstruktur-Stammdomäne](https://technet.microsoft.com/library/cc731174.aspx).  
