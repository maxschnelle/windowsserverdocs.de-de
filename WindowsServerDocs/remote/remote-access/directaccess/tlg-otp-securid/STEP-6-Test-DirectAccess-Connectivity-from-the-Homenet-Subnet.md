---
title: Schritt 6 Test DirectAccess-Konnektivität aus dem Subnetz "Homenet"
description: 'Dieses Thema ist Teil der Testumgebungsanleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe3014b8b37fab35532f3ecf833188fda9e8b744
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/31/2019
ms.locfileid: "66446638"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>Schritt 6 Test DirectAccess-Konnektivität aus dem Subnetz "Homenet"

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Die DirectAccess-Bereitstellung Einmalkennwort (OTP) ist jetzt abgeschlossen, und Sie können zum Testen der Konnektivität aus dem Subnetz "Homenet" starten.  
  
### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>So testen Sie OTP-Funktionalität aus dem Subnetz "Homenet" auf "client1"  
  
1. Stellen Sie sicher, dass Sie als angemeldet sind, auf auf CLIENT1 **"user1"** .  
  
2. Auf der **starten** geben**powershell.exe**, mit der rechten Maustaste **Powershell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **ausführen als Administrator**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.  
  
3. Geben Sie in Windows PowerShell-Fenster **Gpupdate/force**, und drücken Sie EINGABETASTE.  
  
4. Trennen Sie CLIENT1 aus dem Subnetz "Corpnet", und verbinden Sie es mit dem Subnetz "Homenet".  
  
5. Klicken Sie auf "client1", öffnen Sie Internet Explorer, und geben Sie in der Adressleiste **https://app1.corp.contoso.com/** und drücken Sie EINGABETASTE. Drücken Sie F5.  
  
   Die Website sollte nicht geöffnet werden.  
  
6. Auf der **starten** geben**RSA**, und klicken Sie auf **RSA SecurID-Token**.  
  
7. Warten Sie, bis das RSA SecurID-Token Einmalkennwort geändert, und klicken Sie dann auf **Kopie**.  
  
8. Klicken Sie im Infobereich auf das Symbol **Netzwerkverbindungen** , um auf die DirectAccess-Medienverwaltung zuzugreifen.  
  
9. Klicken Sie auf **Contoso DirectAccess-Verbindung**, und klicken Sie auf **Weiter**.  
  
10. Drücken Sie Strg + Alt + Entf, und klicken Sie auf die **Einmalkennwort (OTP)** Kachel.  
  
11. Fügen Sie den zuvor kopierten acht Ziffern Tokencode, und klicken Sie auf **OK**. Warten Sie, für die Authentifizierung abzuschließen. Der DirectAccess-Arbeitsplatz-Verbindungsstatus werden **verbunden**.  
  
12. Geben Sie in der Adressleiste in Internet Explorer **https://app1.corp.contoso.com/** und drücken Sie EINGABETASTE. Drücken Sie F5. Die Standard-IIS-Website auf APP1 wird angezeigt.  
  
13. Geben Sie in der Internet Explorer-Adressleiste **https://app2.corp.contoso.com/** und drücken Sie EINGABETASTE. Drücken Sie F5. Die IIS-Standardwebsite wird auf APP2 angezeigt.  
  
14. Auf der **starten** geben<strong>\\\app1\files</strong>, und drücken Sie EINGABETASTE.  
  
15. In der **Dateien** Fenster mit dem freigegebenen Ordner, doppelklicken Sie auf die **Example.txt** Datei. Sehen Sie den Inhalt der Datei "Example.txt" ein.  
  
16. Auf der **starten** geben<strong>\\\app2\files</strong>, und drücken Sie EINGABETASTE.  
  
17. In der **Dateien** Fenster mit dem freigegebenen Ordner, doppelklicken Sie auf die **neue Textdatei.txt** Datei. Sie sehen, dass der Inhalt der Datei neue Textdatei.txt.  
  


