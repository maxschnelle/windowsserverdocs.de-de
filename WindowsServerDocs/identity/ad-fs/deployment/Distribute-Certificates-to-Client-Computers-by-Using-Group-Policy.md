---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: Verteilen von Zertifikaten an Clientcomputer mithilfe von Gruppenrichtlinien
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d3a7e05e4d16565b17b69de254e353df749bbc3a
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>Verteilen von Zertifikaten an Clientcomputer mithilfe von Gruppenrichtlinien

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


Sie können das folgende Verfahren verwenden, um nach der entsprechenden Zertifikate für Secure Sockets Layer \(SSL\) Push \ (oder äquivalent zu einer vertrauenswürdigen Root\ Zertifikate) für Konto-Verbundserver, Ressourcenverbundserver und Webserver auf jedem Clientcomputer in der Kontopartner-Gesamtstruktur mithilfe von Gruppenrichtlinien.  
  
Mitgliedschaft in **Domänen-Admins** oder **Organisations-Admins**, oder entsprechende Berechtigungen in Active Directory-Domänendiensten \(AD DS\) mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>Zum Verteilen von Zertifikaten an Clientcomputer mithilfe von Gruppenrichtlinien  
  
1.  Starten Sie auf einem Domänencontroller in der Gesamtstruktur des der Kontopartnerorganisation der **Gruppenrichtlinienverwaltung** Snap-in.  
  
2.  Suchen Sie ein vorhandenes Gruppenrichtlinienobjekt \(GPO\) oder erstellen Sie ein neues Gruppenrichtlinienobjekt, um das Zertifikat enthalten. Stellen Sie sicher, dass das Gruppenrichtlinienobjekt mit der Domäne, Site oder Organisationseinheit verknüpft ist, in denen der entsprechenden Benutzer- und Computerkonten befinden \(OU\).  
  
3.  Mit der rechten Maustaste auf das Gruppenrichtlinienobjekt, und klicken Sie dann auf **bearbeiten**.  
  
4.  Öffnen Sie in der Konsolenstruktur **Configuration\\Policies\\Windows um Settings\\Public Schlüssel Computerrichtlinien**, klicken Sie auf **vertrauenswürdige Stammzertifizierungsstellen**, und klicken Sie dann auf **Import**.  
  
5.  Auf der **Willkommen bei den Zertifikatimport-Assistenten** auf **Weiter**.  
  
6.  Auf der **zu importierende Datei** Geben Sie den Pfad zu der entsprechenden Zertifikatdateien \ (z.B. \\\fs1\\c$\\fs1.cer\), und klicken Sie dann auf **Weiter**.  
  
7.  Auf der **Zertifikatspeicher** auf **alle Zertifikate in folgendem Speicher speichern**, und klicken Sie dann auf **Weiter**.  
  
8.  Auf der **Abschließen des Zertifikatimport-Assistenten** Seite, stellen Sie sicher, dass die angegebenen Informationen korrekt sind, und klicken Sie dann auf **Fertig stellen**.  
  
9. Wiederholen Sie die Schritte2 bis 6, um zusätzliche Zertifikate für jeden Verbundserver in der Farm hinzuzufügen.  
