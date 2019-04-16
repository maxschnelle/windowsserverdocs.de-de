---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: Rolle "Standorttopologiebesitzer" der Website-Topologie
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 7c98d313cac28ab07380791a384a87bffacfbda2
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="site-topology-owner-role"></a>Rolle "Standorttopologiebesitzer" der Website-Topologie

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Der Administrator, der die Standorttopologie verwaltet, wird als Besitzer der Website-Topologie bezeichnet. Der Besitzer der Website-Topologie versteht die Garantien in Bezug auf das Netzwerk zwischen den Standorten und verfügt über die Berechtigung zum Ändern der Einstellungen in Active Directory-Domänendienste (AD DS), um Änderungen an der Standorttopologie zu implementieren. Änderungen an der Standorttopologie wirkt sich die Änderung in der Replikationstopologie. Die Topologie des Websitebesitzers folgende Verantwortungsbereiche:  
  
-   Änderungen an der Standorttopologie steuern, wenn die Netzwerkkonnektivität ändert.  
  
-   Anfordern und Verwalten von Informationen zu Netzwerkverbindungen und Router aus der Gruppe "Netzwerk". Der Besitzer der Website-Topologie muss eine Liste von Subnetzadressen, Subnetzmasken und den Speicherort für den einzelnen gehört verwalten. Der Besitzer der Website-Topologie muss auch Probleme zur Geschwindigkeit und Kapazität verstehen, die Standorttopologie effektiv Festlegen der Kosten für standortverknüpfungen auswirken.  
  
-   Verschieben Sie die Active Directory-Server-Objekte, die zwischen Standorten Domänencontroller darstellt, wenn die IP-Adresse des Domänencontrollers in einem anderen Subnetz an einem anderen Standort ändert oder wenn das Subnetz selbst an einen anderen Standort zugewiesen ist. In beiden Fällen muss der Besitzer der Website-Topologie manuell das Active Directory-Serverobjekt des Domänencontrollers an den neuen Standort verschieben.  
  


