---
title: Problembehandlung für AD FS - Anspruchsregeln
description: In diesem Dokument wird beschrieben, wie Ansprüche Regelsyntax mit AD FS-Problembehandlung
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 027b2afc9e580253ec820e7e5be14419387ddd44
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837921"
---
# <a name="ad-fs-troubleshooting---claims-rules-syntax"></a>Problembehandlung für AD FS - Anspruchsanbieter-Regeln-Syntax
Ein Anspruch ist eine Anweisung, ein Subjekt macht über sich selbst oder einen anderen Antragsteller.  Ansprüche werden durch eine vertrauende Seite ausgestellt, und sie erhalten Sie einen oder mehrere Werte sind, und klicken Sie dann in Sicherheitstoken, die von AD FS-Servers ausgestellt werden verpackt.  Dieser Artikel befasst sich mit den Ansprüchen Syntax und Erstellung.  Informationen zu Ansprüchen finden Sie unter ausstellungstransformationsregeln [AD FS-Problembehandlung - Ausstellung von Ansprüchen](ad-fs-tshoot-claims-issuance.md).

>[!NOTE]  
>Können Sie [ClaimsXRay](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) auf die [AD FS-Hilfe](https://adfshelp.microsoft.com) Site zur Problembehandlung behauptet Probleme.   

## <a name="how-claim-rules-are-processed"></a>Verarbeiten von Anspruchsregeln
Anspruchsregeln werden verarbeitet, bis die [anspruchspipeline](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md) mithilfe der [Anspruchs-Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md). Das Anspruchsmodul ist eine logische Komponente des Verbunddiensts, die den Satz der von einem Benutzer gesendeten eingehenden Ansprüche untersucht und anschließend in Abhängigkeit von der Logik in jeder Regel einen Ausgabeanspruchssatz erzeugt.

## <a name="how-to-create-a-claim-rule"></a>Erstellen einer Anspruchsregel
Anspruchsregeln werden separat für jede Verbund-Vertrauensstellungsbeziehung innerhalb des Verbunddiensts erstellt und werden nicht von mehreren Vertrauensstellungen gemeinsam verwendet. Sie können entweder erstellen eine Regel an eine [anspruchsregelvorlage](../../ad-fs/technical-reference/determine-the-type-of-claim-rule-template-to-use.md), von Grund auf neu starten, durch das Erstellen der Regel mithilfe der [anspruchsregelsprache](../../ad-fs/technical-reference/when-to-use-a-custom-claim-rule.md) oder verwenden Sie Windows PowerShell, um eine Regel anpassen.

## <a name="understanding-the-components-of-the-claim-rule-language"></a>Grundlegendes zu den Komponenten der Anspruchsregelsprache
Die anspruchsregelsprache besteht aus den folgenden Komponenten, getrennt durch die "= >"-Operator:

- Eine Bedingung: das zum Überprüfen der Eingabeansprüche und zu bestimmen, ob die ausstellungsanweisung der Regel ausgeführt werden soll.  Es stellt einen logischen Ausdruck, der ausgewertet werden kann, muss zum Ausführen der Hauptteil der Regel auf "true".

- Eine Ausstellungsanweisung

Beispiel:

```c:[type == "Name", value == "domain user"] => issue(type = "Role", value = "employee");``` 

Die folgende Anspruch enthält Folgendes:
- Bedingung: `c:[type == "Name", value == "domain user"] ` -wertet den Eingabeanspruch, ob der Windows-Kontoname ein Domänenbenutzer ist
- Ausstellung - `issue(type = "Role", value = "employee")` – Wenn die Bedingung "true" Fügt einen neuen Anspruch, der Eingabeanspruch mit der Rolle des Mitarbeiters.

Weitere Informationen zu Ansprüchen und die Syntax finden Sie unter [die Rolle der Anspruchsregelsprache](../../ad-fs/technical-reference/the-role-of-the-claim-rule-language.md).

## <a name="claims-rule-editor"></a>Ansprüche-Regel-editor
Syntaxüberprüfung erfolgt durch die Regel-Editor für Ansprüche, nachdem Sie den Anspruch abgeschlossen haben, und klicken Sie auf **OK**.  Wenn Sie die falsche Syntax haben wird dann Editor Ihnen mit, lassen.

![Ansprüche](media/ad-fs-tshoot-claims/claims1.png)

## <a name="event-logs"></a>Ereignisprotokolle
Beim Versuch, einen Anspruch, der mithilfe der Protokolle zu behandeln ist der beste Ansatz, um für die Ausgabe von Ansprüchen zu suchen.  Sie können für 1000 und 1001 Ereignisse im Ereignisprotokoll suchen.

![Ansprüche](media/ad-fs-tshoot-claims/claims2.png)

## <a name="creating-a-sample-application"></a>Zum Erstellen einer beispielanwendung
Sie können auch erstellen eine beispielanwendung die wiederholt von Ansprüchen.  Beispielsweise können Sie verwenden eine Beispiel-App und erstellen eine relying Party, die den gleichen Anspruch, den Sie versuchen enthält zu überprüfen, ob die app alle Probleme mit dem Anspruch enthält.

![Ansprüche](media/ad-fs-tshoot-claims/claim4.png)

Hier ist eine gutes Beispiel-Web-app verfügbar.  Diese app ist eine einfache Web-app, die zurück auf die Ansprüche zurückgibt, die von die vertrauende Seite empfangen.  Um dies zu verwenden, müssen Sie zum Bearbeiten der Datei "Web.config"-app durch:
- Ändern der https://app1.contoso.com/sampapp an die URL der verwenden Sie zum Hosten der Sampapp
- Ändern alle Instanzen von "STS.contoso.com", um Sie zu AD FS-Verbundserver verweisen
- Ersetzen den Fingerabdruck durch Ihren Fingerabdruck ein.

![Ansprüche](media/ad-fs-tshoot-claims/claims3.png)

Die folgenden [Blogartikel](https://blogs.technet.microsoft.com/tangent_thoughts/2015/02/20/install-and-configure-a-simple-net-4-5-sample-federated-application-samapp/) verfügt über hervorragende und ausführliche Anweisungen zum einrichten.

## <a name="next-steps"></a>Nächste Schritte

- [AD FS-Problembehandlung](ad-fs-tshoot-overview.md)