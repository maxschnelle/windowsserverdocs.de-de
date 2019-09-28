---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: Verteilen von Zertifikaten auf Client Computer mithilfe von Gruppenrichtlinie
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1d9692bc099174f15b77e792087f4c7055bf85d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359619"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>Verteilen von Zertifikaten auf Client Computer mithilfe von Gruppenrichtlinie


Sie können das folgende Verfahren verwenden, um die entsprechenden Secure Sockets Layer \(ssl @ no__t-1-Zertifikaten \(oder äquivalente Zertifikate, die mit einem vertrauenswürdigen Stammverzeichnis @ no__t-3 für Konto Verbund Server, Ressourcen Verbund Server und Webserver für jeden Client Computer in der Konto Partner-Gesamtstruktur, indem Sie Gruppenrichtlinie verwenden.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder Organisations- **Admins**oder einer entsprechenden Gruppe in Active Directory Domain Services \(AD DS @ no__t-3 erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/swlink? LinkId\=83477\).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>So verteilen Sie Zertifikate mithilfe von Gruppenrichtlinie auf Client Computer  
  
1.  Starten Sie auf einem Domänen Controller in der Gesamtstruktur der Konto Partnerorganisation das **Gruppenrichtlinie Management** Snap @ no__t-1In.  
  
2.  Suchen Sie ein vorhandenes Gruppenrichtlinie Objekt \(gpo @ no__t-1, oder erstellen Sie ein neues GPO, das die Zertifikat Einstellungen enthält. Stellen Sie sicher, dass das Gruppenrichtlinien Objekt der Domäne, dem Standort oder der Organisationseinheit \(ou @ no__t-1 zugeordnet ist, in der sich die entsprechenden Benutzer-und Computer Konten befinden.  
  
3.  Rechts @ no__t-0klicken Sie auf das GPO, und klicken Sie dann auf **Bearbeiten**.  
  
4.  Öffnen Sie in der Konsolen **Struktur Computer Konfiguration @ no__t-1policies @ no__t-2Windows Settings @ no__t-3security Settings @ no__t-4public Key Policies**, Right @ no__t-5click **Vertrauenswürdige Stamm Zertifizierungs**stellen, und klicken Sie dann auf **importieren.** .  
  
5.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
6.  Geben Sie auf der Seite **zu importierende Datei** den Pfad zu den entsprechenden Zertifikat Dateien \(Ein, z. b. \\ @ no__t-3fs1 @ no__t-4C $ @no__t -5fs1. CER @ no__t-6, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie auf der Seite **Zertifikat Speicher** auf **alle Zertifikate in folgendem Speicher platzieren**, und klicken Sie dann auf **weiter**.  
  
8.  Überprüfen Sie auf der Seite **abschließen des Zertifikat Import-Assistenten** , ob die von Ihnen angegebenen Informationen korrekt sind, und klicken Sie dann auf **Fertig**stellen.  
  
9. Wiederholen Sie die Schritte 2 bis 6, um zusätzliche Zertifikate für jeden der Verbund Server in der Farm hinzuzufügen.  
