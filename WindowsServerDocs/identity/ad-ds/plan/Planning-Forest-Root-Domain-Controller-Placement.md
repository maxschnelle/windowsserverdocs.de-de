---
ms.assetid: 2a2f493a-9796-454a-9721-e223b799dfa7
title: "Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 374ce31c61c666302e2b00a8f365c289cb8799f8
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="planning-forest-root-domain-controller-placement"></a>Planen der Platzierung der Stammdomänencontroller der Gesamtstruktur

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Domänencontrollern im Gesamtstrukturstamm sind erforderlich, um Vertrauenspfaden für Clients erstellen, die Zugriff auf Ressourcen in anderen Domänen als eigene benötigen. Platzieren Sie Domänencontrollern im Gesamtstrukturstamm im Hub Speicherorte und an Standorten, die Rechenzentren hosten. Wenn Benutzer in einer bestimmten Position auf Ressourcen aus anderen Domänen am gleichen Speicherort zugreifen müssen, und die Verfügbarkeit des Netzwerks zwischen Rechenzentrum und die Position des Benutzers unzuverlässig ist, können Sie eine Stammdomänencontroller am Speicherort hinzufügen oder Erstellen einer vertrauensstellungsabkürzung zwischen den beiden Domänen. Es ist kosteneffizienter, Erstellen einer vertrauensstellungsabkürzung zwischen den Domänen, es sei denn, Sie aus anderen Gründen ein Stammdomänencontroller an diesem Standort zu platzieren.  
  
Verknüpfte Vertrauensstellungen Hilfe Authentifizierungsanforderungen, die vom Benutzer in beiden Domänen zu optimieren. Weitere Informationen über Verknüpfungsvertrauensstellungen zwischen Domänen finden Sie unter Grundlegendes zu beim Erstellen einer Vertrauensstellungsabkürzung ([https://go.microsoft.com/fwlink/?LinkId=107061](https://go.microsoft.com/fwlink/?LinkId=107061)).  
  
Ein Arbeitsblatt, die Sie dokumentieren Sie Ihre Platzierung der Stammdomänencontroller der Gesamtstruktur unterstützen, finden Sie unter Auftrag Hilfsmittel für Windows Server2003 Deployment Kit ([https://go.microsoft.com/fwlink/?LinkID=102558](https://go.microsoft.com/fwlink/?LinkID=102558)), herunterladen Job_Aids_Designing_and_Deploying_Directory_and_Security_Services.zip, und Öffnen Sie "Domänencontrollerkapazität" (DSSTOPO_4.doc).  
  
Sie müssen auf diese Informationen finden Sie bei der Erstellung der Gesamtstruktur-Stammdomäne. Weitere Informationen zum Bereitstellen von Gesamtstruktur-Stammdomäne, finden Sie unter [Bereitstellen einer Gesamtstruktur-Stammdomäne von Windows Server2008](https://technet.microsoft.com/library/cc731174.aspx).  
  


