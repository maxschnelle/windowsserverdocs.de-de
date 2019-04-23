---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: Verteilen Sie Zertifikate auf den Clientcomputern mithilfe einer Gruppenrichtlinie
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d3a7e05e4d16565b17b69de254e353df749bbc3a
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59839231"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>Verteilen Sie Zertifikate auf den Clientcomputern mithilfe einer Gruppenrichtlinie

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


Sie können das folgende Verfahren mithilfe von Push übertragen Sie die entsprechenden Secure Sockets Layer \(SSL\) Zertifikate \(oder die entsprechenden Zertifikate einer vertrauenswürdigen Stammzertifizierungsstelle\) für kontoverbundservern, Ressourcenverbundserver und Webservern auf jedem Clientcomputer in der Kontopartner-Gesamtstruktur mithilfe der Gruppenrichtlinie.  
  
Mitgliedschaft in **Domänen-Admins** oder **Organisations-Admins**, oder äquivalent, in Active Directory Domain Services \(AD DS\) ist die mindestvoraussetzung, um dieses Verfahren abzuschließen.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>Zum Verteilen von Zertifikaten auf Clientcomputern mithilfe einer Gruppenrichtlinie  
  
1.  Starten Sie auf einem Domänencontroller in der Gesamtstruktur des der Kontopartnerorganisation der **Gruppenrichtlinienverwaltung** ausrichten\-in.  
  
2.  Suchen eines vorhandenen Gruppenrichtlinienobjekts \(GPO\) , oder erstellen ein neues Gruppenrichtlinienobjekts für die zertifikateinstellungen enthalten. Stellen Sie sicher, dass das Gruppenrichtlinienobjekt mit der Domäne, Site oder Organisationseinheit verknüpft ist \(Organisationseinheit\) , in der entsprechenden Benutzer- und Computerkonten gespeichert sind.  
  
3.  Rechts\-klicken Sie auf das Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**.  
  
4.  Öffnen Sie in der Konsolenstruktur **Computerkonfiguration\\Richtlinien\\Windows-Einstellungen\\Sicherheitseinstellungen\\Richtlinien öffentlicher Schlüssel**mit der rechten Maustaste\-klicken Sie auf **Trusted Root Certification Authorities**, und klicken Sie dann auf **Import**.  
  
5.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
6.  Auf der **zu importierende Datei** geben den Pfad zu der entsprechenden Zertifikatdateien \(z. B. \\ \\fs1\\c$\\fs1.cer\), und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Certificate Store** auf **alle Zertifikate in folgendem Speicher speichern**, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Abschließen des Zertifikatimport-Assistenten** Seite stellen Sie sicher, dass die angegebenen Informationen korrekt sind, und klicken Sie dann auf **Fertig stellen**.  
  
9. Wiederholen Sie Schritte 2 bis 6, um zusätzliche Zertifikate für jeden Verbundserver in der Farm hinzuzufügen.  
