---
ms.assetid: 4163cf03-3bff-426c-9844-4cc2d7897d52
title: Zuweisen des DNS für die AD DS-Rolle „Besitzer“
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: e0b4d51014173c8ae33b29452f59fa96ab7538b1
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87959168"
---
# <a name="assigning-the-dns-for-ad-ds-owner-role"></a>Zuweisen des DNS für die AD DS-Rolle „Besitzer“

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der Gesamtstruktur Besitzer weist einen Domain Name System (DNS) für Active Directory Domain Services (AD DS)-Besitzer für die Gesamtstruktur zu. Der DNS für AD DS Besitzer der Gesamtstruktur ist eine Person (oder eine Gruppe von Personen), die für die Überwachen der DNS-Bereitstellung für AD DS Infrastruktur zuständig ist, und um sicherzustellen, dass (falls erforderlich) Domänen Namen bei den entsprechenden Internet Autoritäten registriert sind.

Der DNS für AD DS Besitzer ist für das DNS für AD DS Entwurf für die Gesamtstruktur verantwortlich. Wenn Ihre Organisation derzeit einen DNS-Server Dienst betreibt, arbeitet der DNS-Designer für den vorhandenen DNS-Server Dienst mit dem DNS für AD DS Besitzer, um den DNS-Namen des Gesamtstruktur-Stamm Servers an DNS-Server zu delegieren, die auf Domänen Controllern

Der DNS für AD DS Besitzer für die Gesamtstruktur unterhält auch Kontakt mit der DHCP-Gruppe (Dynamic Host Configuration Protocol) und der DNS-Gruppe der Organisation und koordiniert die Pläne der einzelnen DNS-Besitzer jeder Domäne in der Gesamtstruktur (sofern vorhanden) mit diesen Gruppen. Der DNS-Besitzer der Gesamtstruktur stellt sicher, dass die DHCP-und DNS-Gruppen an der DNS-AD DS Entwurfsprozess beteiligt sind, sodass jede Gruppe den DNS-Entwurfsplan kennt und die Eingabe frühzeitig bereitstellen kann.



