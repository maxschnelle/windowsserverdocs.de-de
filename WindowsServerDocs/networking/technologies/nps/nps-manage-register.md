---
title: Registrieren Sie einen NPS-Server in einer Active Directory-Domäne
description: In diesem Thema können Sie um einen Server mit der Netzwerkrichtlinienserver in Windows Server2016 in der Standarddomäne des NPS-Server oder in einer anderen Domäne registrieren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 7ba18f6c994e8b15da3a07a3e37550d5dbff24af
ms.sourcegitcommit: 19d9da87d87c9eefbca7a3443d2b1df486b0b010
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="register-an-nps-server-in-an-active-directory-domain"></a>Registrieren Sie einen NPS-Server in einer Active Directory-Domäne

>Gilt für: Windows Server (Semikolons jährlichen Channel), Windows Server 2016

In diesem Thema können Sie um einen Server mit der Netzwerkrichtlinienserver in Windows Server2016 in der Standarddomäne des NPS-Server oder in einer anderen Domäne registrieren.

## <a name="register-an-nps-server-in-its-default-domain"></a>Registrieren Sie einen NPS-Server in seiner Standarddomäne

Dieses Verfahrens können Sie einen NPS-Server in der Domäne registrieren, in dem der Server Mitglied einer Domäne ist. 

NPS-Server müssen in Active Directory registriert werden, damit sie die Berechtigung, die DFÜ-Eigenschaften von Benutzerkonten während des Autorisierungsprozesses zu lesen. Registrieren eines NPS-Servers den Server Fügt die **RAS- und IAS-Server** Gruppe in Active Directory.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

### <a name="to-register-an-nps-server-in-its-default-domain"></a>So registrieren Sie einen NPS-Server in seiner Standarddomäne


1. Klicken Sie auf dem NPS-Server im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die Netzwerkrichtlinienserver-Konsole wird geöffnet.

2. Mit der rechten Maustaste **NPS (lokal)**, und klicken Sie dann auf **Server in Active Directory registrieren**. Die **Netzwerkrichtlinienserver** Dialogfeld wird geöffnet.

3. In **Netzwerkrichtlinienserver**, klicken Sie auf **OK**, und klicken Sie dann auf **OK** erneut.

## <a name="register-an-nps-server-in-another-domain"></a>Registrieren Sie einen NPS-Server in einer anderen Domäne

Um einen NPS-Server mit der Berechtigung zum Lesen der DFÜ-Eigenschaften von Benutzerkonten in Active Directory zu bieten, muss der NPS-Server in der Domäne registriert werden, in denen die Konten befinden.

Dieses Verfahrens können Sie einen NPS-Server in einer Domäne registrieren, in dem der NPS-Server nicht Mitglied einer Domäne ist.

Mitgliedschaft in **Administratoren**, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um diese Schritteausführen.

### <a name="to-register-an-nps-server-in-another-domain"></a>Registrieren Sie einen NPS-Server in einer anderen Domäne

1. Klicken Sie auf dem Domänencontroller im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und -Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.

2. Navigieren Sie zu der Domäne, die an den NPS-Server zum Lesen von Informationen zum Benutzerkonto in der Konsolenstruktur, und klicken Sie dann auf die **Benutzer** Ordner. 

3. Klicken Sie im Detailbereich mit der rechten Maustaste **RAS- und IAS-Server**, und klicken Sie dann auf **Eigenschaften**. Die **RAS- und IAS-Server-Eigenschaften** Dialogfeld wird geöffnet.

4. In der **RAS- und IAS-Server-Eigenschaften** Dialogfeld, klicken Sie auf die **Mitglieder** Registerkarte, fügen Sie den NPS-Servern, die Sie verwenden möchten, registrieren in der Domäne, und klicken Sie dann auf **OK**.


### <a name="to-register-an-nps-server-in-another-domain-by-using-netsh-commands-for-nps"></a>Registrieren Sie einen NPS-Server in einer anderen Domäne mithilfe von Netsh-Befehle für den NPS

1. Öffnen Sie die Befehlszeile oder Windows PowerShell. 

2. Geben Sie an der Eingabeaufforderung Folgendes ein: **Netsh Nps fügen**&nbsp;*Domäne*&nbsp;*Server*, und drücken Sie dann die EINGABETASTE.

>[!NOTE]
>Im vorstehenden Befehl *Domäne* der DNS-Domänenname der Domäne an, wo Sie die NPS-Server registrieren möchten, und *Server* ist der Name des NPS-Servers.

