---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: Zuweisen des DNS für die AD DS-Rolle „Besitzer“
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: dde9ed6035b30ba5b5b96b7132d25a1f8a1c0b8c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59884021"
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>Zuweisen des DNS für die AD DS-Rolle „Besitzer“

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Gesamtstrukturbesitzer weist eines DNS Domain Name System () für den Besitzer der Active Directory Domain Services (AD DS) für die Gesamtstruktur. Das DNS für AD DS-Besitzer der Gesamtstruktur ist eine Person (oder eine Gruppe von Personen), wer ist verantwortlich für die Überwachung der Bereitstellung von DNS für AD DS-Infrastruktur und sicherstellen, dass (falls erforderlich) werden mit den zuständigen Domänennamen registriert.  
  
Das DNS für AD DS-Besitzer ist verantwortlich für das DNS für AD DS-Entwurf für die Gesamtstruktur. Wenn Ihre Organisation derzeit einen DNS-Serverdienst ausgeführt wird, funktioniert der DNS-Designer für den vorhandenen DNS-Server-Dienst, durch den DNS-Besitzer von AD DS delegieren Stammnamen der Gesamtstruktur-DNS-an DNS-Server auf einem Domänencontroller ausgeführt wird.  
  
Das DNS für AD DS-Besitzer für die Gesamtstruktur auch Kontakt mit dem Dynamic Host Configuration Protocol (DHCP) und die DNS-Gruppe der Organisation verwaltet und koordiniert die Pläne der einzelnen DNS-Besitzer jeder Domäne in der Gesamtstruktur (sofern vorhanden), diese Gruppen. Der DNS-Besitzer für die Gesamtstruktur wird sichergestellt, dass die DHCP- und DNS-Gruppen im DNS für AD DS-Entwurfsprozesses beteiligt sind, so, dass jede Gruppe die DNS-Entwurfsplan beachtet und Bereitstellen von Eingaben frühzeitig kann.  
  


