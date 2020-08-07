---
title: Schritt 6 Testen der DirectAccess-Konnektivität aus dem homenet-Subnetz
description: 'Dieses Thema ist Teil der Test Umgebungs Anleitung: veranschaulichen von DirectAccess mit OTP-Authentifizierung und RSA SecurID für Windows Server 2016'
manager: brianlic
ms.topic: article
ms.assetid: b9b77cfd-8dd4-476b-a118-f3d6bf59e7b1
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 8bad40c6bb7a01d578f2cdb7a61090b1624046d8
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87971677"
---
# <a name="step-6-test-directaccess-connectivity-from-the-homenet-subnet"></a>Schritt 6 Testen der DirectAccess-Konnektivität aus dem homenet-Subnetz

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Die Bereitstellung des einmaligen Kennworts für DirectAccess ist jetzt fertiggestellt, und Sie können damit beginnen, die Konnektivität aus dem homenet-Subnetz zu testen.

### <a name="to-test-otp-functionality-from-the-homenet-subnet-on-client1"></a>So testen Sie die OTP-Funktionalität aus dem homenet-Subnetz auf CLIENT1

1. Stellen Sie auf CLIENT1 sicher, dass Sie als **User1**angemeldet sind.

2. Geben Sie auf dem **Start** Bildschirm**powershell.exe**ein, klicken Sie mit der rechten Maustaste auf **PowerShell**, klicken Sie auf **erweitert**, und klicken Sie dann auf **als Administrator ausführen**. Falls das Dialogfeld **Benutzerkontensteuerung** angezeigt wird, bestätigen Sie, dass Sie die angezeigte Aktion wünschen, und klicken Sie anschließend auf **Ja**.

3. Geben Sie im Windows PowerShell-Fenster **gpupdate/force**ein, und drücken Sie die EINGABETASTE.

4. Entfernen Sie CLIENT1 aus dem Corpnet-Subnetz, und verbinden Sie es mit dem homenet-Subnetz.

5. Öffnen Sie auf CLIENT1 Internet Explorer, geben Sie in der Adressleiste ein, **https://app1.corp.contoso.com/** und drücken Sie die EINGABETASTE. Drücken Sie F5.

   Die Site sollte nicht geöffnet werden.

6. Geben Sie auf dem **Start** Bildschirm**RSA**ein, und klicken Sie auf **RSA SecurID Token**.

7. Warten Sie, bis der RSA SecurID-Token das einmalige Kennwort ändert, und klicken Sie dann auf **Kopieren**.

8. Klicken Sie auf die**Netzwerkverbindungen**-Symbol im Infobereich angezeigt, DA Medien-Manager zugreifen.

9. Klicken Sie auf die **DirectAccess-Verbindung**von Configuration Manager, und klicken Sie auf **weiter**.

10. Drücken Sie STRG + ALT + ENTF, und klicken Sie auf die Kachel **einmal Kennwort (OTP)** .

11. Fügen Sie die zuvor kopierte achtstellige Ziffer in den Code ein, und klicken Sie auf **OK**. Warten Sie, bis die Authentifizierung fertiggestellt ist. Der Status der DirectAccess-Arbeitsplatz Verbindung wird nun **verbunden**.

12. Geben Sie in Internet Explorer in der Adressleiste ein, **https://app1.corp.contoso.com/** und drücken Sie die EINGABETASTE. Drücken Sie F5. Die Standard-IIS-Website auf APP1 wird angezeigt.

13. Geben Sie in der Internet Explorer-Adressleiste ein, **https://app2.corp.contoso.com/** und drücken Sie die EINGABETASTE. Drücken Sie F5. Die IIS-Standard Website wird auf APP2 angezeigt.

14. Geben Sie auf dem **Start** Bildschirm<strong> \\ \app1\files</strong>ein, und drücken Sie die EINGABETASTE.

15. Doppelklicken Sie im Fenster freigegebene Ordner **Dateien** auf die **Example.txt** Datei. Der Inhalt der Example.txt Datei wird angezeigt.

16. Geben Sie auf dem **Start** Bildschirm<strong> \\ \app2\files</strong>ein, und drücken Sie die EINGABETASTE.

17. Doppelklicken Sie im Fenster freigegebene Ordner **Dateien** auf den **neuen Text #b0** Datei. Der Inhalt der neuen Text Document.txt Datei wird angezeigt.



