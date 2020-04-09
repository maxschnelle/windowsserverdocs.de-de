---
title: Schritt 6 Testen der DirectAccess-Konnektivität aus dem homenet-Subnetz
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.prod: windows-server
ms.technology: networking-da
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: dbbaae146a0101decfc62d950b98c1af10fb39b2
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80814405"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>Schritt 6 Testen der DirectAccess-Konnektivität aus dem homenet-Subnetz

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Die Bereitstellung des einmaligen Kennworts für DirectAccess ist jetzt fertiggestellt, und Sie können damit beginnen, die Konnektivität aus dem homenet-Subnetz zu testen.  
  
### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>So testen Sie die OTP-Funktionalität aus dem homenet-Subnetz auf CLIENT1  
  
1. Stellen Sie auf CLIENT1 sicher, dass Sie als **User1**angemeldet sind.  
  
2. Geben Sie auf dem **Start** Bildschirm**PowerShell. exe**ein, klicken Sie mit der rechten Maustaste auf **PowerShell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass die angezeigte Aktion ausgeführt werden soll, und klicken Sie anschließend auf **Ja**.  
  
3. Geben Sie im Windows PowerShell-Fenster **gpupdate/force**ein, und drücken Sie die EINGABETASTE.  
  
4. Entfernen Sie CLIENT1 aus dem Corpnet-Subnetz, und verbinden Sie es mit dem homenet-Subnetz.  
  
5. Öffnen Sie auf CLIENT1 Internet Explorer, geben Sie in der Adressleiste **https://app1.corp.contoso.com/** ein, und drücken Sie die EINGABETASTE. Drücken Sie F5.  
  
   Die Site sollte nicht geöffnet werden.  
  
6. Geben Sie auf dem **Start** Bildschirm**RSA**ein, und klicken Sie auf **RSA SecurID Token**.  
  
7. Warten Sie, bis der RSA SecurID-Token das einmalige Kennwort ändert, und klicken Sie dann auf **Kopieren**.  
  
8. Klicken Sie im Infobereich auf das Symbol **Netzwerkverbindungen** , um auf die DirectAccess-Medienverwaltung zuzugreifen.  
  
9. Klicken Sie auf die **DirectAccess-Verbindung**von Configuration Manager, und klicken Sie auf **weiter**.  
  
10. Drücken Sie STRG + ALT + ENTF, und klicken Sie auf die Kachel **einmal Kennwort (OTP)** .  
  
11. Fügen Sie die zuvor kopierte achtstellige Ziffer in den Code ein, und klicken Sie auf **OK**. Warten Sie, bis die Authentifizierung fertiggestellt ist. Der Status der DirectAccess-Arbeitsplatz Verbindung wird nun **verbunden**.  
  
12. Geben Sie in Internet Explorer in der Adressleiste **https://app1.corp.contoso.com/** ein, und drücken Sie die EINGABETASTE. Drücken Sie F5. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
13. Geben Sie in der Internet Explorer-Adressleiste **https://app2.corp.contoso.com/** ein, und drücken Sie die EINGABETASTE. Drücken Sie F5. Die IIS-Standard Website wird auf APP2 angezeigt.  
  
14. Geben Sie auf dem **Start** Bildschirm<strong>\\\app1\files</strong>ein, und drücken Sie die EINGABETASTE.  
  
15. Doppelklicken Sie im Fenster freigegebene Ordner **Dateien** auf die Datei " **example. txt** ". Der Inhalt der Datei "example. txt" wird angezeigt.  
  
16. Geben Sie auf dem **Start** Bildschirm<strong>\\\app2\files</strong>ein, und drücken Sie die EINGABETASTE.  
  
17. Doppelklicken Sie im Fenster "freigegebene Ordner **Dateien** " auf die **neue Textdatei "Document. txt** ". Der Inhalt der neuen Datei "Text Document. txt" wird angezeigt.  
  


