---
ms.assetid: ac6604b0-7459-4ff3-af1c-4936897f5d14
title: Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 2504208210c03193451d19478f3bc8c98ec98f23
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
# <a name="delegating-administration-of-default-containers-and-ous"></a>Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Alle Active Directory-Domäne enthält eine Reihe von Container und Organisationseinheiten (OUs), die während der Installation von Active Directory-Domänendienste (AD DS) erstellt werden. Dazu zählen folgende:  
  
-   Domänencontainer, die als Stammcontainer für die Hierarchie dient  
  
-   Integrierte-Container, der die Standardinstallation Konten enthält  
  
-   Container "Benutzer", wird der Standardspeicherort für neue Benutzerkonten und Gruppen in der Domäne erstellt.  
  
-   Container für Computer, die ist der Standardspeicherort für neue Computerkonten in der Domäne erstellt.  
  
-   Domänencontroller-Organisationseinheit, wird der Standardspeicherort für die Computerkonten für Domain Controller-Computerkonten  
  
Der Gesamtstrukturbesitzer steuert diese Standardcontainern und Organisationseinheiten.  
  
## <a name="domain-container"></a>Domänencontainer  
Der Domänencontainer ist der Stammcontainer der Hierarchie von einer Domäne. Änderungen an den Richtlinien oder der Zugriffssteuerungsliste (ACL) für diesen Container können potenziell domänenweite Auswirkungen haben. Führen Sie keine Delegieren der Verwaltung dieser Container; Es muss von den Dienstadministratoren gesteuert werden.  
  
## <a name="users-and-computers-containers"></a>Benutzer und-Computer Container  
Wenn Sie ein direktes Domänenupgrade von Windows Server 2003 auf Windows Server 2008 ausführen, werden vorhandene Benutzer und -Computer automatisch in den Benutzern und dem Container platziert. Wenn Sie erstellen sind eine neue Active Directory-Domäne, die Benutzer und Computer Container Speicherorte standardmäßig für alle neuen Benutzerkonten und Computerkonten für kein Domänencontroller in der Domäne.  
  
> [!IMPORTANT]  
> Wenn Sie die Kontrolle über Benutzer oder Computer müssen, ändern die Standardeinstellungen für die Benutzer und Computer nicht Container. Stattdessen erstellen Sie neue Organisationseinheiten (bei Bedarf), und verschieben Sie die Benutzer- und Computerobjekte aus ihren Standardcontainer und in neuen Organisationseinheiten. Delegieren der Steuerung der neuen Organisationseinheiten nach Bedarf. Es wird empfohlen, dass Sie nicht ändern, die den Standardcontainer steuert.  
  
Sie können auch gruppenrichtlinieneinstellungen auf die Standardbenutzer und Computer anwenden Container. Zum Anwenden der Gruppenrichtlinie für Benutzer und Computer, erstellen Sie eine neue Organisationseinheit, und verschieben Sie die Benutzer- und Computerobjekte in diesen Organisationseinheiten. Die Gruppenrichtlinien-Einstellungen für die neuen Organisationseinheiten angewendet.  
  
Optional können Sie die Erstellung von Objekten umleiten, die in den Standardcontainern in Containern Ihrer Wahl platziert werden platziert werden.  
  
## <a name="well-known-users-and-groups-and-built-in-accounts"></a>Bekannte Benutzer, Gruppen und Konten  
Standardmäßig werden mehrere bekannten Benutzer, Gruppen und Konten in einer neuen Domäne erstellt. Es wird empfohlen, dass die Verwaltung dieser Konten unter der Kontrolle von der Dienstadministratoren wird. Delegieren Sie die Verwaltung dieser Konten nicht um eine Person, die ein Dienstadministrator nicht ist. Die folgende Tabelle enthält die bekannten Benutzer und Gruppen und die integrierten Konten, die unter der Kontrolle von den Dienstadministratoren bleiben müssen.  
  
|Bekannte Benutzer und Gruppen|Integrierte Konten|  
|--------------------------------|----------------------|  
|Zertifikatherausgeber<br /><br />Domänencontroller<br /><br />Gruppenrichtlinienersteller-Besitzer<br /><br />KRBTGT<br /><br />Domänen-Gäste<br /><br />Administrator<br /><br />Domänen-Admins<br /><br />Schema-Admins (nur für Gesamtstruktur-Stammdomäne)<br /><br />Organisations-Admins (nur für Gesamtstruktur-Stammdomäne)<br /><br />Domänen-Benutzer|Administrator<br /><br />Gastbetriebssystem<br /><br />Gäste<br /><br />Konten-Operatoren<br /><br />Administratoren<br /><br />Sicherungs-Operatoren<br /><br />Erstellungen eingehender Gesamtstruktur Vertrauensstellung<br /><br />Druck-Operatoren<br /><br />Prä-Windows 2000 kompatibler Zugriff<br /><br />Server-Operatoren<br /><br />Benutzer|  
  
## <a name="domain-controller-ou"></a>Domänencontroller-Organisationseinheit  
Wenn Domänencontroller der Domäne hinzugefügt werden, werden ihre Computerobjekte automatisch mit der Domänencontroller-Organisationseinheit hinzugefügt. Diese Organisationseinheit verfügt über eine Reihe von Richtlinien angewendet wurden. Um sicherzustellen, dass diese Richtlinien gleichmäßig auf alle Domänencontroller angewendet werden, empfehlen wir, dass Sie nicht die Computerobjekte Domänencontroller aus dieser Organisationseinheit verschieben. Fehler, um die Standardrichtlinien gelten kann dazu führen, dass Domänencontroller nicht ordnungsgemäß ausgeführt.  
  
In der Standardeinstellung steuern die Administratoren dieser Organisationseinheit. Delegieren Sie die Kontrolle über diese Organisationseinheit nicht für Personen als die Dienstadministratoren.  
  


