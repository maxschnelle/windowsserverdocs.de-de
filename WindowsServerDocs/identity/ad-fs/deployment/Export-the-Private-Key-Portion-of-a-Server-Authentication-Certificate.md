---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: "Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats"
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: c968f0702d56b56d0a80459e5cf0c9e658c56741
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>Exportieren des Bereichs der privaten Schlüssel eines Serverauthentifizierungszertifikats

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

Jeder Verbundserver in einer Active Directory Federation Services-Farm \(AD FS\) benötigen Zugriff auf den privaten Schlüssel des Serverzertifikats Authentifizierung. Wenn Sie eine Serverfarm mit Verbundserver oder Webservern implementieren, müssen Sie ein einzelnes Authentifizierungszertifikat verfügen. Dieses Zertifikat muss ausgestellt werden von einer Unternehmenszertifizierungsstelle \(CA\), und sie benötigen einen exportierbaren privaten Schlüssel. Der private Schlüssel, der das Serverauthentifizierungszertifikat muss exportierbar sein, damit es an alle Server in der Farm zur Verfügung gestellt werden kann.  
  
Dasselbe Konzept gilt der Verbund-Proxy Serverfarmen in dem Sinn, dass alle Verbundserverproxys in einer Farm den privaten Schlüssel Teil der gleiche Serverauthentifizierungszertifikat, das gemeinsam genutzt werden müssen.  
  
> [!NOTE]  
> AD FS-Verwaltungs-Snap-in bezeichnet Serverauthentifizierungszertifikate für Verbundserver als dienstkommunikationszertifikate.  
  
Je nachdem, welche Rolle dieser Computer spielen wird, verwenden Sie dieses Verfahren auf dem Verbundservercomputer oder Verbundserverproxy-Computer, auf dem Sie das Serverauthentifizierungszertifikat mit dem privaten Schlüssel installiert. Wenn Sie das Verfahren abgeschlossen haben, können Sie dann dieses Zertifikat auf der Standardwebsite jedes Servers in der Farm importieren. Weitere Informationen finden Sie unter [importieren Sie ein Serverauthentifizierungszertifikat auf der Standardwebsite](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
Mitgliedschaft in **Administratoren**, oder eine entsprechende Berechtigung auf dem lokalen Computer mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>So exportieren Sie die privaten Teil eines serverauthentifizierungszertifikats  
  
1.  Auf der **starten** geben**Internetinformationsdienste \(IIS\) Manager**, und drücken Sie dann die EINGABETASTE.  
  
2.  Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3.  Im mittleren Bereich doppelten Mausklick **Serverzertifikate**.  
  
4.  Im mittleren Bereich mit der rechten Maustaste auf das Zertifikat, das Sie exportieren möchten, und klicken Sie dann auf **exportieren**.  
  
5.  In der **Zertifikat exportieren** Dialogfeld, klicken Sie auf die **...** Schaltfläche.  
  
6.  In **Dateinamen**, Typ **C:\\***Name des Zerttifikats*, und klicken Sie dann auf **öffnen**.  
  
7.  Geben Sie ein Kennwort für das Zertifikat, bestätigen Sie es, und klicken Sie dann auf **OK**.  
  
8.  Überprüfen Sie den Erfolg Ihres Exportvorgangs, indem Sie sicherstellen, dass die angegebene Datei am angegebenen Speicherort erstellt wird.  
  
    > [!IMPORTANT]  
    > So, dass dieses Zertifikat in den lokalen Zertifikatspeicher auf dem neuen Server importiert werden kann, müssen Sie die Datei auf ein physisches Speichermedium übertragen und die Sicherheit während des Transports auf den neuen Server schützen. Es ist äußerst wichtig, um die Sicherheit des privaten Schlüssels zu schützen. Wenn dieser Schlüssel gefährdet ist, die Sicherheit Ihrer gesamten AD FS-Bereitstellung \ (einschließlich der Ressourcen in Ihrer Organisation und in Resource Partner Organizations\) gefährdet ist.  
  
9. Importieren Sie das exportierte Serverauthentifizierungszertifikat in den Zertifikatspeicher auf dem neuen Server vor der Installation des Verbunddiensts. Informationen dazu, wie Sie das Zertifikat importieren, finden Sie unter Importieren eines Serverzertifikats \ ([http:///\/go.microsoft.com\/fwlink\/? LinkId\ = 108283](https://go.microsoft.com/fwlink/?LinkId=108283)\).  
  
## <a name="additional-references"></a>Weitere Verweise  
[Checkliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Checkliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Certificate Requirements for Federation Servers](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Certificate Requirements for Federation Server Proxies](https://technet.microsoft.com/library/dd807054.aspx)  
  

