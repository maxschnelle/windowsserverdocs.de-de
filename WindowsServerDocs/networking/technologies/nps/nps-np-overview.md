---
title: Netzwerkrichtlinien
description: Dieses Thema bietet eine Übersicht über Netzwerkrichtlinien für Netzwerkrichtlinienserver unter Windows Server 2016, und enthält Links zu weiteren Anleitungen zum NPS.
manager: brianlic
ms.prod: windows-server-threshold
ms.technology: networking
ms.topic: article
ms.assetid: e4a9b134-6d1d-40d7-a49c-5f46d5fdb419
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 60ab80bb6cf26578430b76806405a65a0f596ef2
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59848951"
---
# <a name="network-policies"></a>Netzwerkrichtlinien

>Gilt für: WindowsServer (Halbjährlicher Kanal), WindowsServer 2016

In diesem Thema können einen Überblick über die Netzwerkrichtlinien in NPS.

>[!NOTE]
>Zusätzlich zu diesem Thema steht die folgende Dokumentation zum Netzwerk-Richtlinie.
> - [Access-Berechtigung](nps-np-access.md)
> - [Netzwerkrichtlinien konfigurieren](nps-np-configure.md)

Netzwerkrichtlinien werden Bedingungen, Einschränkungen und Einstellungen, mit denen Sie bestimmen, wer für die Verbindung mit dem Netzwerk und die Umstände, unter denen können oder keine Verbindung, autorisiert ist.

Bei der Verarbeitung von verbindungsanforderungen als Server Remote Authentication Dial-in User Service (RADIUS), führt NPS Authentifizierung und Autorisierung für die verbindungsanforderung an. Während des Authentifizierungsprozesses überprüft NPS die Identität des Benutzers oder der Computer, auf dem eine Verbindung mit dem Netzwerk herstellt. Während des Autorisierungsprozesses bestimmt NPS an, ob der Benutzer oder Computer zulässig ist, auf das Netzwerk zugreifen.

Damit wird dazu, verwendet NPS Netzwerkrichtlinien, die in der NPS-Konsole konfiguriert werden. NPS auch untersucht die Einwähleigenschaften des Benutzerkontos in Active Directory&reg; Domänendienste \(AD DS\) die Autorisierung durch.

## <a name="network-policies---an-ordered-set-of-rules"></a>Netzwerkrichtlinien - einen geordneten Satz von Regeln

Netzwerkrichtlinien können als Regeln angezeigt werden. Jede Regel verfügt über einen Satz von Bedingungen und Einstellungen. NPS vergleicht die Bedingungen der Regel, die die Eigenschaften des Connection-Anforderungen. Wenn eine Übereinstimmung zwischen der Regel und die verbindungsanforderung auftritt, werden die Einstellungen, die in der Regel definierten für die Verbindung angewendet.

Wenn mehrere Netzwerkrichtlinien auf dem Netzwerkrichtlinienserver konfiguriert sind, sind sie einen geordneten Satz von Regeln. NPS überprüft jede verbindungsanforderung anhand der ersten Regel in der Liste aus, und klicken Sie dann die zweite usw., bis eine Übereinstimmung gefunden wird.

Jede Netzwerkrichtlinie verfügt über eine **Richtlinienstatus** festlegen, können Sie aktivieren oder deaktivieren Sie die Richtlinie. Wenn Sie eine Netzwerkrichtlinie deaktivieren, wertet NPS nicht die Richtlinie, bei der Weiterleitung von verbindungsanforderungen zu autorisieren.

>[!NOTE]
>Wenn Sie NPS auswerten eine Netzwerkrichtlinie, bei der Autorisierung für verbindungsanforderungen ausführen möchten, müssen Sie konfigurieren die **Richtlinienstatus** Einstellung wählen Sie die Richtlinie aktiviert, aktivieren Sie das Kontrollkästchen.

## <a name="network-policy-properties"></a>Die Eigenschaften von

Es gibt vier Kategorien von Eigenschaften für jede Netzwerkrichtlinie:

### <a name="overview"></a>Übersicht

 Diese Eigenschaften ermöglichen Ihnen die Angabe, ob die Richtlinie aktiviert ist, gibt an, ob die Richtlinie Zugriff gewährt oder verweigert, und gibt an, ob eine bestimmte Netzwerkverbindungsmethode oder Art von Netzwerkzugriffsserver (NAS), für die Weiterleitung von verbindungsanforderungen erforderlich ist. Übersicht die Übersichtseigenschaften können auch angeben, ob die DFÜ-Eigenschaften von Benutzerkonten in AD DS ignoriert werden. Wenn Sie diese Option auswählen, werden nur die Einstellungen in der Netzwerkrichtlinie von NPS verwendet, um zu bestimmen, ob die Verbindung autorisiert ist.


### <a name="conditions"></a>Bedingungen

 Diese Eigenschaften können Sie die Bedingungen angegeben, die die verbindungsanforderung haben muss, um die Netzwerkrichtlinie entsprechen. Wenn die Bedingungen, die in der Richtlinie konfiguriert die verbindungsanforderung übereinstimmen, werden die Einstellungen, die festgelegt werden, in der Netzwerkrichtlinie für die Verbindung von NPS angewendet. Entspricht z. B. Wenn Sie die NAS-IPv4-Adresse, als Bedingung für die Netzwerkrichtlinie angeben und NPS empfängt eine verbindungsanforderung von einem NAS, die die angegebene IP-Adresse verfügt, die Bedingung in der Richtlinie die verbindungsanforderung. 


### <a name="constraints"></a>Einschränkungen

 Einschränkungen sind zusätzliche Parameter der Netzwerkrichtlinie, die erforderlich sind, entsprechend die verbindungsanforderung. Wenn eine Einschränkung durch die verbindungsanforderung nicht übereinstimmt, lehnt die Anforderung automatisch von NPS ab. Wenn eine Einschränkung nicht überein ist, verweigert NPS im Gegensatz zu der NPS-Antwort an die nicht übereinstimmende Bedingungen in der Netzwerkrichtlinie die verbindungsanforderung ohne zusätzliche Netzwerkrichtlinien auszuwerten.

### <a name="settings"></a>Einstellungen

 Diese Eigenschaften können Sie die Einstellungen angeben, die auf die verbindungsanforderung NPS gilt, wenn alle die netzwerkbedingungen für die Richtlinie für die Richtlinie entsprechen.

Wenn Sie eine neue Netzwerkrichtlinie mit der NPS-Konsole hinzufügen, müssen Sie den Assistenten für neue Netzwerkrichtlinien verwenden. Nachdem Sie eine Netzwerkrichtlinie mithilfe des Assistenten erstellt haben, können Sie die Richtlinie anpassen, durch Doppelklicken auf die Richtlinie in der NPS-Konsole, um die Eigenschaften der Richtlinie zu erhalten.

Beispiele für die Syntax zum Angeben von Mustervergleich Richtlinienattribute Netzwerk, finden Sie unter [Verwenden von regulären Ausdrücken in NPS](nps-crp-reg-expressions.md).

Weitere Informationen zu NPS finden Sie unter [(Network Policy Server, NPS)](nps-top.md).
