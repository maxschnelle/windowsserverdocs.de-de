---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: "Zuweisen des DNS für AD DS-Rolle"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: e393cbf32aa5a13ff22044eabb8c575508baaf79
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>Zuweisen des DNS für AD DS-Rolle

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Der Gesamtstrukturbesitzer weist eine DNS Domain Name System () für Active Directory-Domänendienste (AD DS) Besitzer für die Gesamtstruktur. Das DNS für AD DS-Besitzer der Gesamtstruktur ist eine Person (oder eine Gruppe von Personen), wer ist verantwortlich für die Überwachung der Bereitstellung von DNS für AD DS-Infrastruktur und dafür sorgen, dass (falls erforderlich) werden mit den zuständigen Domänennamen registriert.  
  
Das DNS für AD DS-Besitzer ist verantwortlich für das DNS für AD DS-Entwurf für die Gesamtstruktur. Wenn Ihre Organisation derzeit einen DNS-Serverdienst ausgeführt wird, funktioniert der DNS-Designer für die vorhandenen DNS-Server-Dienst mit dem DNS für die AD DS-Besitzer der Gesamtstruktur Stamm-DNS-Name auf DNS-Server auf Domänencontrollern zu delegieren.  
  
Das DNS für AD DS-Besitzer für die Gesamtstruktur auch Kontakt mit dem Dynamic Host Configuration-Protokoll (DHCP)-Gruppe und die DNS-Gruppe der Organisation verwaltet und koordiniert die Pläne des den einzelnen DNS-Besitzer jeder Domäne in der Gesamtstruktur (falls vorhanden) mit diesen Gruppen. Der DNS-Besitzer für die Gesamtstruktur wird sichergestellt, dass die DHCP- und DNS-Gruppen so, dass jede Gruppe von DNS-Entwurfsplan und früh Eingaben kann im DNS für die AD DS-Entwurfsprozesses beteiligt sind.  
  


