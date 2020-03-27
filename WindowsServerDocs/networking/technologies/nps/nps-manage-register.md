---
title: Registrieren eines Netzwerkrichtlinienservers in einer Active Directory-Domäne
description: Sie können dieses Thema verwenden, um einen Server, auf dem der Netzwerk Richtlinien Server ausgeführt wird, in Windows Server 2016 in der NPS-Standard Domäne oder in einer anderen Domäne zu registrieren.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: lizross
author: eross-msft
ms.openlocfilehash: 63d630250b0b24937a3dfc01bcba7ec63faa3c3e
ms.sourcegitcommit: da7b9bce1eba369bcd156639276f6899714e279f
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/26/2020
ms.locfileid: "80315963"
---
# <a name="register-an-nps-in-an-active-directory-domain"></a>Registrieren eines Netzwerkrichtlinienservers in einer Active Directory-Domäne

>Gilt für: Windows Server (Semi-Annual Channel), Windows Server 2016

Sie können dieses Thema verwenden, um einen Server, auf dem der Netzwerk Richtlinien Server ausgeführt wird, in Windows Server 2016 in der NPS-Standard Domäne oder in einer anderen Domäne zu registrieren.

## <a name="register-an-nps-in-its-default-domain"></a>Registrieren eines NPS in seiner Standard Domäne

Mit diesem Verfahren können Sie einen NPS in der Domäne registrieren, in der der Server ein Domänen Mitglied ist. 

NPSS muss in Active Directory registriert werden, damit Sie über die Berechtigung zum Lesen der Einwähleigenschaften von Benutzerkonten während des Autorisierungs Vorgangs verfügen. Beim Registrieren eines NPS wird der Server der Gruppe " **RAS-und IAS-Server** " in Active Directory hinzugefügt.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

### <a name="to-register-an-nps-in-its-default-domain"></a>So registrieren Sie einen NPS in seiner Standard Domäne


1. Klicken Sie auf dem NPS in Server-Manager auf **Extras, und klicken Sie dann**auf **Netzwerk Richtlinien Server**. Die Netzwerk Richtlinien Server-Konsole wird geöffnet.

2. Klicken Sie mit der rechten Maustaste auf **NPS (lokal)** , und klicken Sie dann **auf Server in Active Directory registrieren**. Das Dialogfeld **Netzwerkrichtlinienserver** wird geöffnet.

3. Klicken Sie im Dialogfeld **Netzwerkrichtlinienserver** auf **OK**, und klicken Sie erneut auf **OK**.

## <a name="register-an-nps-in-another-domain"></a>Registrieren eines NPS in einer anderen Domäne

Zum Bereitstellen eines NPS mit der Berechtigung zum Lesen der DFÜ-Eigenschaften von Benutzerkonten in Active Directory muss der NPS in der Domäne registriert sein, in der sich die Konten befinden.

Mithilfe dieses Verfahrens können Sie ein NPS in einer Domäne registrieren, bei der der NPS kein Domänen Mitglied ist.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

### <a name="to-register-an-nps-in-another-domain"></a>So registrieren Sie einen NPS in einer anderen Domäne

1. Klicken Sie auf dem Domänen Controller in Server-Manager auf **Extras, und klicken Sie dann**auf **Active Directory Benutzer und Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.

2. Navigieren Sie in der Konsolen Struktur zu der Domäne, in der die NPS Benutzerkontoinformationen lesen möchten, und klicken Sie dann auf den Ordner **Benutzer** . 

3. Klicken Sie im Detailfenster mit der rechten Maustaste auf **RAS-und IAS-Server**, und klicken Sie dann auf **Eigenschaften**. Das Dialogfeld **Eigenschaften von RAS-und IAS-Server** wird geöffnet.

4. Klicken Sie im Dialogfeld **Eigenschaften von RAS-und IAS-Server** auf die Registerkarte **Mitglieder** , fügen Sie alle NPSS hinzu, die Sie in der Domäne registrieren möchten, und klicken Sie dann auf **OK**.


### <a name="to-register-an-nps-in-another-domain-by-using-netsh-commands-for-nps"></a>So registrieren Sie einen NPS in einer anderen Domäne mithilfe von Netsh-Befehlen für NPS

1. Öffnen Sie die Eingabeaufforderung oder Windows PowerShell. 

2. Geben Sie Folgendes an der Eingabeaufforderung ein: **netsh NPS add registeredserver** &nbsp;*Domain* &nbsp;*Server*, und drücken Sie dann die EINGABETASTE.

>[!NOTE]
>Im vorherigen Befehl ist *Domäne* der DNS-Domänen Name der Domäne, in der Sie den NPS registrieren möchten, und *Server* ist der Name des NPS-Computers.

