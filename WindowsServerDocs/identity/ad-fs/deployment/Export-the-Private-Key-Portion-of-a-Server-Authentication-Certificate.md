---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: Exportieren des Teils eines privaten Schlüssels aus einem Serverauthentifizierungszertifikat
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 1a7e59dd83ebc9a9eabd5bda1dc598d320f5028d
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66442501"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>Exportieren des Teils eines privaten Schlüssels aus einem Serverauthentifizierungszertifikat

Jedes Verbundservers in einer Active Directory Federation Services \(AD FS\) Farm benötigen Zugriff auf den privaten Schlüssel des serverauthentifizierungszertifikats. Wenn Sie eine Serverfarm mit Verbundserver oder Webservern implementieren, müssen Sie ein einzelnes Authentifizierungszertifikat verfügen. Dieses Zertifikat muss von einer Unternehmenszertifizierungsstelle ausgestellt sein \(Zertifizierungsstelle\), und sie müssen einen exportierbaren privaten Schlüssel. Der private Schlüssel des Serverauthentifizierungszertifikats muss exportierbar sein, damit er für alle Server in der Farm zur Verfügung gestellt werden kann.  
  
Dasselbe Konzept gilt für Verbund-Proxy-Serverfarmen in dem Sinne, dass alle Verbundserverproxys in einer Farm Teil mit den privaten Schlüssel des das gleiche Serverauthentifizierungszertifikat verwenden, müssen zur Verfügung.  
  
> [!NOTE]  
> Die AD FS-Verwaltungs-Snap\-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.  
  
Je nachdem welche Rolle dieser Computer spielen wird, verwenden Sie dieses Verfahren auf dem verbundservercomputer oder Verbundserverproxy-Computer, auf dem Sie das Serverauthentifizierungszertifikat mit dem privaten Schlüssel installiert. Wenn das Verfahren abgeschlossen ist, können Sie dieses Zertifikat dann auf der Standardwebsite jedes Servers in der Farm importieren. Weitere Informationen finden Sie unter [Importieren eines Serverauthentifizierungszertifikats auf die Standardwebsite](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>So exportieren Sie den Bereich mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats  
  
1. Auf der **starten** geben**Internet Information Services \(IIS\) Manager**, und drücken Sie dann die EINGABETASTE.  
  
2. Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3. Doppelklicken Sie im mittleren Bereich\-klicken Sie auf **Serverzertifikate**.  
  
4. Klicken Sie im mittleren Bereich der rechten Maustaste\-klicken Sie auf das Zertifikat, das Sie exportieren möchten, und klicken Sie dann auf **exportieren**.  
  
5. In der **Zertifikat exportieren** Dialogfeld klicken Sie auf die **...** .  
  
6. In **Dateiname**, Typ **C:\\** <em>Name des Zerttifikats</em>, und klicken Sie dann auf **öffnen**.  
  
7. Geben Sie das Kennwort für das Zertifikat ein, bestätigen Sie das Kennwort, und klicken Sie dann auf **OK**.  
  
8. Überprüfen Sie den Erfolg Ihres Exportvorgangs, indem Sie bestätigen, dass die von Ihnen angegebene Daten am angegebenen Standort erstellt wird.  
  
   > [!IMPORTANT]  
   > Damit dieses Zertifikat in den lokalen Zertifikatspeicher auf dem neuen Server importiert werden, müssen Sie die Datei auf ein physisches Speichermedium übertragen und ihre Sicherheit während des Transports auf den neuen Server sichern. Es ist äußerst wichtig, die Sicherheit des privaten Schlüssels zu gewähren. Wenn dieser Schlüssel gefährdet ist, die Sicherheit der gesamten AD FS-Bereitstellung \(das Einschließen von Ressourcen in Ihrer Organisation und in ressourcenpartnerorganisationen\) gefährdet ist.  
  
9. Importieren Sie das exportierte Serverauthentifizierungszertifikat in den Zertifikatspeicher auf dem neuen Server, bevor Sie den Verbunddienst installieren. Informationen dazu, wie Sie das Zertifikat zu importieren, finden Sie unter Importieren eines Serverzertifikats \( [http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=108283](https://go.microsoft.com/fwlink/?LinkId=108283)\).  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Zertifikatanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807054.aspx)  
  

