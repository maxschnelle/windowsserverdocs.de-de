---
ms.assetid: cf32926a-2083-408b-a264-2cad179ed18a
title: Verteilen von Zertifikaten auf Client Computer mithilfe von Gruppenrichtlinie
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c0e1ab21faa42789bee20c7b8945284aba068310
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80855443"
---
# <a name="distribute-certificates-to-client-computers-by-using-group-policy"></a>Verteilen von Zertifikaten auf Client Computer mithilfe von Gruppenrichtlinie


Mithilfe des folgenden Verfahrens können Sie die entsprechenden Secure Sockets Layer \(SSL-\) Zertifikate \(oder äquivalente Zertifikate, die mit einem vertrauenswürdigen Stamm\) für Konto Verbund Server, Ressourcen Verbund Server und Webserver verkettet sind, mithilfe von Gruppenrichtlinie an jeden Client Computer in der Konto Partner-Gesamtstruktur übertragen.  
  
Zum Ausführen dieses Verfahrens ist mindestens die Mitgliedschaft in **Domänen-Admins** oder Organisations- **Admins**oder einer entsprechenden Gruppe in Active Directory Domain Services \(AD DS\) erforderlich.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/go.Microsoft.com\/\/. LinkId\=83477\).   
  
### <a name="to-distribute-certificates-to-client-computers-by-using-group-policy"></a>So verteilen Sie Zertifikate mithilfe von Gruppenrichtlinie auf Client Computer  
  
1.  Starten Sie auf einem Domänen Controller in der Gesamtstruktur der Konto Partnerorganisation das Snap\-**Gruppenrichtlinie-Verwaltung** in.  
  
2.  Suchen Sie ein vorhandenes Gruppenrichtlinie Objekt \(GPO\) oder erstellen Sie ein neues GPO, das die Zertifikat Einstellungen enthält. Stellen Sie sicher, dass das Gruppenrichtlinien Objekt der Domäne, dem Standort oder der Organisationseinheit \(OE\) zugeordnet ist, in der sich die entsprechenden Benutzer-und Computer Konten befinden.  
  
3.  Klicken Sie mit der rechten\-auf das GPO, und klicken Sie dann auf **Bearbeiten**.  
  
4.  Öffnen Sie in der Konsolen **Struktur Computer Konfiguration\\Richtlinien\\Windows-Einstellungen\\Sicherheitseinstellungen\\Public Key Policies**, klicken Sie mit der rechten\-klicken Sie auf **Vertrauenswürdige Stamm Zertifizierungs**stellen, und klicken Sie dann auf **importieren**.  
  
5.  Klicken Sie auf der Seite **Willkommen** auf **Weiter**.  
  
6.  Geben Sie auf der Seite **zu importierende Datei** den Pfad zu den entsprechenden Zertifikat Dateien \(z. b. \\\\FS1\\c $\\FS1. CER\)ein, und klicken Sie dann auf **weiter**.  
  
7.  Klicken Sie auf der Seite **Zertifikat Speicher** auf **alle Zertifikate in folgendem Speicher platzieren**, und klicken Sie dann auf **weiter**.  
  
8.  Überprüfen Sie auf der Seite **abschließen des Zertifikat Import-Assistenten** , ob die von Ihnen angegebenen Informationen korrekt sind, und klicken Sie dann auf **Fertig**stellen.  
  
9. Wiederholen Sie die Schritte 2 bis 6, um zusätzliche Zertifikate für jeden der Verbund Server in der Farm hinzuzufügen.  
