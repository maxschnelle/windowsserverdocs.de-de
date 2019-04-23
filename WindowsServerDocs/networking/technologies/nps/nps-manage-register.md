---
title: Registrieren eines Netzwerkrichtlinienservers in einer Active Directory-Domäne
description: Sie können in diesem Thema verwenden, um einen Server Network Policy Server in Windows Server 2016 in der NPS-Standarddomäne oder in einer anderen Domäne zu registrieren.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: 2de954fd-a7d8-4cc6-85b1-b0c3c06f788f
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 4a289ec519e5107576becf2905cd881cf9def190
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59877651"
---
# <a name="register-an-nps-in-an-active-directory-domain"></a>Registrieren eines Netzwerkrichtlinienservers in einer Active Directory-Domäne

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

Sie können in diesem Thema verwenden, um einen Server Network Policy Server in Windows Server 2016 in der NPS-Standarddomäne oder in einer anderen Domäne zu registrieren.

## <a name="register-an-nps-in-its-default-domain"></a>Registrieren Sie einen NPS in seiner Standarddomäne

Sie können dieses Verfahren verwenden, ein NPS in der Domäne registrieren, in dem der Server Mitglied einer Domäne ist. 

NPSs müssen in Active Directory registriert werden, damit sie die Berechtigung zum Lesen der DFÜ-Eigenschaften von Benutzerkonten während des Autorisierungsprozesses haben. Registrieren einen NPS, fügt den Server die **RAS- und IAS-Server** Gruppe in Active Directory.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

### <a name="to-register-an-nps-in-its-default-domain"></a>So registrieren Sie einen Netzwerkrichtlinienserver in der Standarddomäne


1. Klicken Sie auf den NPS, im Server-Manager auf **Tools**, und klicken Sie dann auf **Netzwerkrichtlinienserver**. Die Netzwerkrichtlinienserver-Konsole wird geöffnet.

2. Mit der rechten Maustaste **NPS (lokal)**, und klicken Sie dann auf **Server in Active Directory registrieren**. Das Dialogfeld **Netzwerkrichtlinienserver** wird geöffnet.

3. Klicken Sie im Dialogfeld **Netzwerkrichtlinienserver** auf **OK**, und klicken Sie erneut auf **OK**.

## <a name="register-an-nps-in-another-domain"></a>Registrieren Sie einen NPS in einer anderen Domäne

Um ein NPS mit der Berechtigung zum Lesen der DFÜ-Eigenschaften von Benutzerkonten in Active Directory bereitzustellen, muss der NPS in der Domäne registriert werden, in denen die Konten befinden.

Sie können dieses Verfahren verwenden, ein NPS in eine Domäne registrieren, in dem der NPS nicht Mitglied einer Domäne ist.

Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe sein, um diese Verfahren ausführen zu können.

### <a name="to-register-an-nps-in-another-domain"></a>Um ein NPS in einer anderen Domäne zu registrieren.

1. Klicken Sie auf dem Domänencontroller im Server-Manager auf **Tools**, und klicken Sie dann auf **Active Directory-Benutzer und-Computer**. Die Konsole Active Directory-Benutzer und -Computer wird geöffnet.

2. In der Konsolenstruktur, navigieren Sie zu der Domäne, in dem der NPS zum Lesen von Informationen für das Benutzerkonto angezeigt werden sollen, und klicken Sie dann auf die **Benutzer** Ordner. 

3. Klicken Sie im Detailbereich mit der Maustaste **RAS- und IAS-Server**, und klicken Sie dann auf **Eigenschaften**. Die **RAS- und IAS-Server-Eigenschaften** Dialogfeld wird geöffnet.

4. In der **RAS- und IAS-Server-Eigenschaften** Dialogfeld klicken Sie auf die **Mitglieder** Registerkarte, die jede der NPSs, die Sie verwenden möchten, in der Domäne registrieren, und klicken Sie dann auf Hinzufügen, **OK**.


### <a name="to-register-an-nps-in-another-domain-by-using-netsh-commands-for-nps"></a>Ein NPS in einer anderen Domäne zu registrieren, indem Sie mithilfe von Netsh-Befehle für Netzwerkrichtlinienserver

1. Öffnen Sie die Eingabeaufforderung oder ein Windows PowerShell. 

2. Geben Sie an der Eingabeaufforderung Folgendes ein: **Netsh Nps hinzufügen Registeredserver** &nbsp; *Domäne* &nbsp; *Server*, und drücken Sie dann die EINGABETASTE.

>[!NOTE]
>Im obigen Befehl *Domäne* ist der DNS-Domänenname der Domäne, in dem Sie den NPS, registrieren möchten, und *Server* ist der Name des Computers NPS.

