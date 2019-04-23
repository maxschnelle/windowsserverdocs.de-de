---
ms.assetid: ac6604b0-7459-4ff3-af1c-4936897f5d14
title: Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 9d482854fd82b4bf0d0e61315d36e6222470ca55
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59830891"
---
# <a name="delegating-administration-of-default-containers-and-ous"></a>Delegieren der Verwaltung von Standardcontainern und Organisationseinheiten

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Alle Active Directory-Domäne enthält einen Standardsatz von Container und Organisationseinheiten (OUs), die während der Installation von Active Directory Domain Services (AD DS) erstellt werden. Beispiele:  
  
-   Domain-Container, der dient als Stammcontainer für die Hierarchie  
  
-   Integrierten Container, die standardmäßig Dienstadministratorkonten enthält.  
  
-   Container "Benutzer", die am Standardort für neue Benutzerkonten und Gruppen ist in der Domäne erstellt.  
  
-   Computercontainer der Standardspeicherort für die neue Computerkonten ist in der Domäne erstellt.  
  
-   Domänencontroller-Organisationseinheit, die ist der Standardspeicherort für die Computerkonten für Domänenkonten Controller-computer  
  
Der Gesamtstrukturbesitzer steuert diese Standardcontainern und Organisationseinheiten.  
  
## <a name="domain-container"></a>Domänencontainer  
Der Domänencontainer wird der Stammcontainer der Hierarchie von einer Domäne. Änderungen an die Richtlinien oder die Zugriffssteuerungsliste (ACL) für diesen Container können potenziell die domänenweite-auswirken. Delegieren Sie die Kontrolle über diesen Container nicht; Es muss von den Dienstadministratoren gesteuert werden.  
  
## <a name="users-and-computers-containers"></a>Benutzer und-Computer Container  
Wenn Sie eine direkte domänenaktualisierung von Windows Server 2003 auf Windows Server 2008 ausführen, werden vorhandene Benutzer und Computer automatisch in die Benutzer und die Computercontainer platziert. Bei der Erstellung sind einer neuen Active Directory-Domäne, die Benutzer und Computer Container Speicherorte standardmäßig für alle neuen Benutzerkonten und Computerkonten für nicht-Domänencontroller in der Domäne.  
  
> [!IMPORTANT]  
> Wenn Sie die Kontrolle über die Benutzer oder Computer delegieren möchten, ändern die Standardeinstellungen für die Benutzer und Computer nicht Container. Stattdessen erstellen Sie neue Organisationseinheiten, die (bei Bedarf), und verschieben Sie die Benutzer- und Computerobjekte aus ihrer Standardcontainern und in den neuen Organisationseinheiten. Delegieren der Steuerung der neuen Organisationseinheiten nach Bedarf. Es wird empfohlen, dass Sie nicht ändern, die die Standardcontainern steuert.  
  
Darüber hinaus können Sie die gruppenrichtlinieneinstellungen auf den Standardbenutzer und-Computer anwenden Container. Zum Anwenden der Gruppenrichtlinie für Benutzer und Computer erstellen Sie neue Organisationseinheiten, und verschieben Sie die Benutzer- und Computerobjekte in Organisationseinheiten. Gelten Sie die Gruppenrichtlinien-Einstellungen für den neuen Organisationseinheiten.  
  
Optional können Sie die Erstellung von Objekten umleiten, die in den Standardcontainern in Container Ihrer Wahl platziert wird, platziert werden.  
  
## <a name="well-known-users-and-groups-and-built-in-accounts"></a>Well-Known-Benutzer und Gruppen sowie integrierte Konten  
Standardmäßig werden verschiedene bekannte Benutzer, Gruppen und integrierte Konten in einer neuen Domäne erstellt. Es wird empfohlen, dass die Verwaltung dieser Konten unter der Kontrolle über die Dienstadministratoren bleibt. Delegieren Sie die Verwaltung dieser Konten nicht auf eine Person, die ein Dienstadministrator nicht ist. Die folgende Tabelle enthält die bekannten Benutzer, Gruppen und integrierte Konten, die unter der Kontrolle über die Dienstadministratoren bleiben müssen.  
  
|Well-Known-Benutzer und Gruppen|Integrierte Konten|  
|--------------------------------|----------------------|  
|Zertifikatherausgeber<br /><br />Domänencontroller<br /><br />Gruppenrichtlinienersteller-Besitzer<br /><br />KRBTGT<br /><br />Domänen-Gäste<br /><br />Administrator<br /><br />Domänen-Admins<br /><br />Schema-Admins (nur für Gesamtstruktur-Stammdomäne)<br /><br />Organisations-Admins (nur für Gesamtstruktur-Stammdomäne)<br /><br />Domänenbenutzer|Administrator<br /><br />Gast<br /><br />Gäste<br /><br />Konten-Operatoren<br /><br />Administratoren<br /><br />Sicherungsoperatoren<br /><br />Eingehende Gesamtstruktur-Vertrauensstellung<br /><br />Druck-Operatoren<br /><br />Prä-Windows 2000 kompatibler Zugriff<br /><br />Server-Operatoren<br /><br />Benutzer|  
  
## <a name="domain-controller-ou"></a>Domänencontroller-Organisationseinheit  
Wenn Domänencontroller mit der Domäne hinzugefügt werden, werden ihre Computerobjekte automatisch mit der Domänencontroller-Organisationseinheit hinzugefügt. Diese Organisationseinheit verfügt über eine Reihe von Richtlinien, die angewendet werden. Um sicherzustellen, dass diese Richtlinien gleichmäßig auf alle Domänencontroller angewendet werden, empfehlen wir, dass Sie nicht die Computerobjekte der Domänencontroller aus dieser Organisationseinheit verschieben. Fehler beim Anwenden der Standardrichtlinien für kann dazu führen, dass einen Domänencontroller nicht ordnungsgemäß funktioniert.  
  
In der Standardeinstellung steuern die Dienstadministratoren dieser Organisationseinheit an. Delegieren Sie die Kontrolle über diese Organisationseinheit nicht zu anderen Personen als die Dienstadministratoren.  
  


