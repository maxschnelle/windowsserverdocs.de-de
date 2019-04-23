---
ms.assetid: af76ddbe-83a2-4a62-9989-873e3bb1c772
title: Rolle „Standorttopologiebesitzer“
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 69443c2fc1af855c7df002e0ac91d43986eff6da
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59832111"
---
# <a name="site-topology-owner-role"></a>Rolle „Standorttopologiebesitzer“

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Administrator, der die Standorttopologie verwaltet, wird als Besitzer der Website-Topologie bezeichnet. Die Standorttopologiebesitzer versteht die Bedingungen des Netzwerks zwischen Standorten und verfügt über die Berechtigung zum Ändern von Eigenschaften in Active Directory Domain Services (AD DS), um Änderungen an der Website-Topologie zu implementieren. Änderungen an der Standorttopologie wirkt sich die Änderung in der Replikationstopologie. Die Standorttopologiebesitzer Aufgaben zählen:  
  
-   Steuern Änderungen an der Website-Topologie, wenn über eine Netzwerkverbindung ändert.  
  
-   Abrufen und Verwalten von Informationen über Netzwerkverbindungen und Router aus der Netzwerkgruppe. Der Besitzer der Website-Topologie muss eine Liste der Subnetzadressen, Subnetzmasken und den Speicherort, zu dem einzelnen gehört, verwalten. Der Besitzer der Website-Topologie müssen Sie zudem alle Probleme bezüglich der netzwerkgeschwindigkeit und der Kapazität verstehen, die Standorttopologie, um die Kosten für standortverknüpfungen effektiv festgelegt zu beeinflussen.  
  
-   Verschieben Sie die Active Directory-Server-Objekte, die zwischen Standorten Domänencontroller darstellt, ändert sich die IP-Adresse des Domänencontrollers auf einem anderen Subnetz in einem anderen Standort, oder das Subnetz selbst mit einem anderen Standort zugewiesen wird. In beiden Fällen muss die Standorttopologiebesitzer manuell die Active Directory-Serverobjekt des Domänencontrollers an den neuen Standort verschieben.  
  


