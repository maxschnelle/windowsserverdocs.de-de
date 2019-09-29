---
title: 'AD FS Problembehandlung: Anspruchs Regeln'
description: In diesem Dokument wird beschrieben, wie Sie eine Problembehandlung für die Anspruchs Regel Syntax mit AD FS
author: billmath
ms.author: billmath
manager: mtillman
ms.date: 03/01/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d0146ba7cfc736f4d37ca66d58d624cc2f7f9a23
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366281"
---
# <a name="ad-fs-troubleshooting---claims-rules-syntax"></a>AD FS Problembehandlung: Syntax von Anspruchs Regeln
Ein Anspruch ist eine-Anweisung, die ein Subjekt über sich selbst oder einen anderen Betreff trifft.  Ansprüche werden von einer vertrauenden Seite ausgegeben, und Sie erhalten einen oder mehrere Werte und werden dann in Sicherheits Token verpackt, die vom AD FS Server ausgestellt werden.  In diesem Artikel werden die Anspruchs Syntax und die Erstellung behandelt.  Weitere Informationen zur Anspruchs Ausstellung finden Sie unter [AD FS Problembehandlung: Anspruchs Ausstellung](ad-fs-tshoot-claims-issuance.md).

>[!NOTE]  
>Sie können [claimsxray](https://adfshelp.microsoft.com/ClaimsXray/TokenRequest) auf der [ADFS-Hilfe](https://adfshelp.microsoft.com) Website verwenden, um die Behandlung von Anspruchs Problemen zu unterstützen.   

## <a name="how-claim-rules-are-processed"></a>Verarbeiten von Anspruchsregeln
Anspruchs Regeln werden mithilfe der Anspruchs- [Engine](../../ad-fs/technical-reference/The-Role-of-the-Claims-Engine.md)über die Anspruchs [Pipeline](../../ad-fs/technical-reference/The-Role-of-the-Claims-Pipeline.md) verarbeitet. Das Anspruchsmodul ist eine logische Komponente des Verbunddiensts, die den Satz der von einem Benutzer gesendeten eingehenden Ansprüche untersucht und anschließend in Abhängigkeit von der Logik in jeder Regel einen Ausgabeanspruchssatz erzeugt.

## <a name="how-to-create-a-claim-rule"></a>Erstellen einer Anspruchsregel
Anspruchsregeln werden separat für jede Verbund-Vertrauensstellungsbeziehung innerhalb des Verbunddiensts erstellt und werden nicht von mehreren Vertrauensstellungen gemeinsam verwendet. Sie können entweder eine Regel aus einer [Anspruchs Regel Vorlage](../../ad-fs/technical-reference/determine-the-type-of-claim-rule-template-to-use.md)erstellen, von Grund auf neu starten, indem Sie die Regel mithilfe der [Anspruchs Regel Sprache](../../ad-fs/technical-reference/when-to-use-a-custom-claim-rule.md) erstellen oder eine Regel mithilfe von Windows PowerShell anpassen.

## <a name="understanding-the-components-of-the-claim-rule-language"></a>Grundlegendes zu den Komponenten der Anspruchsregelsprache
Die Anspruchs Regel Sprache besteht aus den folgenden Komponenten, getrennt durch den Operator "= >":

- Eine Bedingung, die verwendet wird, um Eingabe Ansprüche zu überprüfen und zu bestimmen, ob die Ausstellungs Anweisung der Regel ausgeführt werden soll.  Sie stellt einen logischen Ausdruck dar, der mit true ausgewertet werden muss, um den Hauptteil der Regel auszuführen.

- Eine Ausstellungsanweisung

Beispiel:

```c:[type == "Name", value == "domain user"] => issue(type = "Role", value = "employee");``` 

Der folgende Anspruch hat Folgendes:
- Condition-`c:[type == "Name", value == "domain user"] `: wertet den Eingabe Anspruch aus, ob der Name des Windows-Kontos ein Domänen Benutzer ist.
- Ausstellung-`issue(type = "Role", value = "employee")`: Wenn die Bedingung true ist, wird dem Eingabe Anspruch mit der Rolle Employee ein neuer Anspruch hinzugefügt.

Weitere Informationen zu Ansprüchen und zur Syntax finden Sie in der [Rolle der Anspruchs Regel Sprache](../../ad-fs/technical-reference/the-role-of-the-claim-rule-language.md).

## <a name="claims-rule-editor"></a>Anspruchs Regel-Editor
Die Syntax Überprüfung wird vom Anspruchs Regel-Editor ausgeführt, nachdem Sie den Anspruch abgeschlossen haben, und klicken Sie auf **OK**.  Wenn Sie also die falsche Syntax haben, werden Sie vom Editor informiert.

![Claims](media/ad-fs-tshoot-claims/claims1.png)

## <a name="event-logs"></a>Ereignisprotokolle
Wenn Sie versuchen, einen Anspruch mithilfe der Protokolle zu beheben, empfiehlt es sich, nach der Anspruchs Ausgabe zu suchen.  Sie können nach 1000-und 1001-Ereignissen im Ereignisprotokoll suchen.

![Claims](media/ad-fs-tshoot-claims/claims2.png)

## <a name="creating-a-sample-application"></a>Erstellen einer Beispielanwendung
Sie können auch eine Beispielanwendung erstellen, die ihre Ansprüche widerspiegelt.  Beispielsweise können Sie eine Beispielanwendung verwenden und eine vertrauende Seite erstellen, die den gleichen Anspruch hat, zu dem Sie versuchen, Probleme zu beheben, und feststellen, ob die APP Probleme mit diesem Anspruch hat.

![Claims](media/ad-fs-tshoot-claims/claim4.png)

Eine gute Beispiel-Web-App finden Sie hier.  Diese APP ist eine einfache Web-App, die die Ansprüche zurückgibt, die Sie von der vertrauenden Seite empfängt.  Um dies zu verwenden, müssen Sie die Web. config-app wie folgt bearbeiten:
- Ändern von https://app1.contoso.com/sampapp in die URL, die Sie zum Hosting von sampapp verwenden
- alle Instanzen von STS.contoso.com so ändern, dass Sie AD FS Verbund Servers verweisen
- Ersetzen des Fingerabdrucks durch Ihren Fingerabdruck

![Claims](media/ad-fs-tshoot-claims/claims3.png)

Der folgende [Blog Artikel](https://blogs.technet.microsoft.com/tangent_thoughts/2015/02/20/install-and-configure-a-simple-net-4-5-sample-federated-application-samapp/) enthält hervorragende, ausführliche Anweisungen zum Einrichten dieser Vorgehensweisen.

## <a name="next-steps"></a>Nächste Schritte

- [Behandeln von AD FS-Problemen](ad-fs-tshoot-overview.md)