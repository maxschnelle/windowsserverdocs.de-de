---
ms.assetid: 8b15d44e-e4e6-4510-aa91-cc7ec7161b0a
title: Rolle der Anspruchs-Engine
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.openlocfilehash: f7f33dc2931856aaf0e430aa3a65d03d30038325
ms.sourcegitcommit: dfa48f77b751dbc34409aced628eb2f17c912f08
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/07/2020
ms.locfileid: "87937865"
---
# <a name="the-role-of-the-claims-engine"></a>Rolle der Anspruchs-Engine
Auf der höchsten Ebene ist das Anspruchs Modul in Active Directory-Verbunddienste (AD FS) \( AD FS \) ein Regel \- basiertes Modul, das für die Verarbeitung und Verarbeitung von Anspruchs Anforderungen für die Verbunddienst reserviert ist. Die Anspruchs-Engine ist die einzige Komponente im Verbunddienst, die für die Ausführung der einzelnen Regelsätze für alle verbundenen Vertrauensstellungen, die Sie konfiguriert haben, und die Weitergabe des Ausgabeergebnisses an die Anspruchspipeline verantwortlich ist.

Obwohl es sich bei der Anspruchs Pipeline um ein eher logisches Konzept des End- \- to- \- End-Prozesses für den Fluss von Ansprüchen handelt, sind Anspruchs Regeln ein tatsächliches administratives Element, mit dem Sie den Fluss von Ansprüchen während des Ausführungsprozesses der Anspruchs Regeln anpassen können. Weitere Informationen zu den Pipelineprozessen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).

Wie in der folgenden Abbildung dargestellt, wird das Akzeptieren eingehender Anspruchs \( Akzeptanz Regeln \) , das Autorisieren von Anspruchs Anforderern \( von Autorisierungs Regeln \) und das Ausgeben von ausgehenden Anspruchs Ausstellungs \( Regeln \) durch Anspruchs Regeln über alle Verbund Vertrauens Stellungen in Ihrer Organisation durch die Anspruchs-Engine durchgeführt.

![Rollen AD FS](media/adfs2_enginepipeline.gif)

## <a name="claim-rules-execution-process"></a>Ausführung von Anspruchsregeln
Wenn Sie eine Anspruchs Anbieter-Vertrauensstellung oder eine Vertrauensstellung der vertrauenden Seite in Ihrer Organisation mit Anspruchs Regeln konfigurieren, fungieren die Anspruchs Regelsätze \( \) für diese Vertrauensstellung als Gatekeeper für eingehende Ansprüche, indem Sie die Anspruchs-Engine aufrufen, um die erforderliche Logik in den Anspruchs Regeln anzuwenden, um zu bestimmen, ob Ansprüche ausgegeben werden und welche Ansprüche ausgegeben werden.

Im folgenden Abschnitt werden die Schritte beschrieben, die die Engine während des Ausführungsflusses für Anspruchsregeln ausführt. Alle unten aufgeführten Schritte treten in sämtlichen Phasen auf, die im Ablauf der Anspruchspipeline beschrieben sind. Diese Schritte umfassen:

-   Schritt 1: Initialisierung

-   Schritt 2: Ausführung

-   Schritt 3: Ausführungsergebnis

Weitere Informationen zu den Pipelineprozessen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).

### <a name="step-1--initialization"></a>Schritt 1: Initialisierung
Im ersten Schritt des Ausführungsprozesses für Anspruchsregeln akzeptiert die Anspruchs-Engine eingehende Ansprüche, indem es diese zunächst dem *Eingangsanspruchssatz* hinzufügt. Ein Eingangsanspruchssatz entspricht dem Cache im Arbeitsspeicher, in dem Daten nur so lange temporär gespeichert werden, bis der entsprechende Prozess die erforderlichen Daten abruft. Der Eingangsanspruchssatz wird nach Abschluss der Regelausführung verworfen.

#### <a name="adding-a-claim-to-the-input-claim-set-for-a-rule-set"></a>Hinzufügen von Ansprüchen zum Eingangsanspruchssatz für einen Regelsatz
Der Eingangsanspruchssatz wird von der Anspruchs-Engine erstellt, wenn dieses Anspruchsdaten temporär im Arbeitsspeicher speichern muss, während es die Logik eines Anspruchsregelsatzes verarbeitet. Die Anspruchs-Engine kopiert alle eingehenden Ansprüche in den Eingangsanspruchssatz, aus dem sie durch die erste Regel im Regelsatz abgerufen werden können.

Die Anspruchs-Engine in der Abbildung unten liest z.B. die Ansprüche A und B aus den eingehenden Ansprüchen und kopiert sie in den Eingangsanspruchssatz. Wenn sie im Eingangsanspruchssatz sind, ruft die Anspruchs-Engine die Ansprüche A und B als Eingabe als Eingabe für die Logik in der ersten Regel des Anspruchsregelsatzes ab und verarbeitet sie.

![Rollen AD FS](media/adfs2_context1.gif)

Alle Regeln im Anspruchsregelsatz nutzen denselben Eingangsanspruchssatz. Jede Regel in diesem Satz kann dem freigegebenen Eingangsanspruchssatz etwas hinzufügen und damit alle nachfolgenden Regeln im Satz beeinflussen.

### <a name="step-2--execution"></a>Schritt 2: Ausführung
In diesem Schritt des Anspruchsregelprozesses werden die Anspruchsregeln verarbeitet, indem die Anspruchs-Engine nacheinander alle Regeln in einem bestimmten Regelsatz durchläuft. Jede Regel in einem Regelsatz wird nur einmal ausgeführt und in der Reihenfolge ausgeführt, in der Sie von oben nach unten angezeigt werden, wie im Dialogfeld "Anspruchs Regeln bearbeiten" im Snap-in "AD FS Verwaltung" angezeigt \- . Die Anspruchsregel ganz oben im Regelsatz wird zuerst verarbeitet, und danach werden die nachfolgenden Regeln verarbeitet, bis alle Regeln ausgeführt wurden.

Gemäß der Definition der Anspruchsregelsprache besteht eine Anspruchsregel aus zwei Teilen: Bedingung und Ausstellungsanweisung. Die Anspruchs-Engine verarbeitet zuerst den Bedingungs Teil anhand der Daten im Eingangs Anspruchssatz, um zu bestimmen, ob die in der Regel angegebene Bedingung für die Ansprüche im Eingangs Anspruchssatz true \( ist. die Ansprüche, die der Regel Bedingung entsprechen, werden als übereinstimmende Ansprüche bezeichnet \) . Wenn übereinstimmende Ansprüche gefunden werden, führt die Anspruchs-Engine die Ausstellungsanweisung der Regel für jeden Satz übereinstimmender Ansprüche aus. Die Ausstellungsanweisung der Regel kann eine der folgenden Aufgaben mit den übereinstimmenden Ansprüchen durchführen:

1.  Kopieren eines übereinstimmenden Anspruchs in den Ausgangsanspruchssatz

2.  Umwandeln der Anspruchsfelder und Erstellen eines neuen Anspruchs – entweder nur im Eingangsanspruchssatz oder sowohl im Evaluierungssatz als auch im Ausgangsanspruchssatz

3.  Verwenden Sie die übereinstimmenden Ansprüche \( \) als Schlüssel für die Suche nach weiteren Informationen aus einem Attribut Speicher, um neue Ansprüche \( \) entweder in nur dem Eingangs Anspruchssatz oder in Eingabe-und Ausgangs Anspruchs Sätzen zu erstellen.

#### <a name="adding-a-claim-to-the-output-claim-set-for-a-rule-set"></a>Hinzufügen von Ansprüchen zum Ausgangsanspruchssatz für einen Regelsatz
Der *Ausgangsanspruchssatz* ist ein Speicherort, der anfänglich leer ist. Er ist wichtig, da die Anspruchs-Engine nach Abschluss der Ausführung ausschließlich Ansprüche zurückgibt, die sich im Ausgangsanspruchssatz befinden. Dies bedeutet, dass Ansprüche, die sich lediglich im Eingangsanspruchssatz befinden, aber nicht im Ausgangsanspruchssatz, bei der Berechnung des finalen Satzes von Ausgangsansprüchen ignoriert werden.

#### <a name="adding-a-claim-to-both-claim-sets-for-a-rule-set"></a>Hinzufügen von Ansprüchen zu beiden Anspruchssätzen für einen Regelsatz
Wenn eine Regel verarbeitet wird, werden Ansprüche entweder im Eingangs Anspruchssatz oder sowohl im Eingangs Anspruchssatz als auch im Ausgangs Anspruchssatz hinzugefügt, basierend auf der Anweisung, die in der Ausstellungs Anweisung der Regel verwendet wird. Die Anspruchsregelsprache bezeichnet diese Anweisungen als *Hinzufügen* oder *Ausstellen*.

Bei Verwendung der *Hinzufügen*-Anweisung werden die Ansprüche nur dem Eingangsanspruchssatz hinzugefügt. Die Ansprüche werden ausschließlich für die Ausführung verwendet und danach verworfen. Bei Verwendung der *Ausstellen*-Anweisung werden die Ansprüche dem Eingangs- und dem Ausgangsanspruchssatz hinzugefügt. Nach Abschluss der Ausführung werden die Ansprüche im Ausgangsanspruchssatz zurückgegeben. Weitere Informationen zu diesen Anweisungen finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).

Entspricht der Bedingungsteil einer Regel in einem Regelsatz keinen Ansprüchen im Eingangsanspruchssatz, wird der Ausstellungsanweisungsteil der Regel ignoriert. Es werden daher dann keine Ansprüche dem Eingangs- oder Ausgangsanspruchssatz hinzugefügt. Die folgende Abbildung und die zugehörigen Schritte zeigen, was passiert, wenn die Anspruchs-Engine eine Transformationsregel ausführt:

![Rollen AD FS](media/adfs2_context2.gif)

1.  Eingehende Ansprüche werden dem von der Anspruchs-Engine festgelegten Eingangsanspruchssatz hinzugefügt.

2.  Bei Ausführung der ersten Regel erkennt das Modul die Ansprüche A und B, die zu diesem Zeitpunkt die einzigen Ansprüche im Eingangsanspruchssatz sind, und verarbeitet den Bedingungsteil der Logik von Regel 1.

3.  Da der Anspruch eines Anspruchs im Eingangs Anspruchssatz vorhanden ist, wird die Bedingung der Regel so festgelegt, dass Sie mit \( dem Anspruch a übereinstimmt, \) und ein neuer C-Anspruch wird sowohl dem Eingangs Anspruchssatz als auch dem Ausgangs Anspruchssatz hinzugefügt.

4.  Regel 2 kann nun die Ansprüche A, B und C \( für alle Ansprüche im Eingangs Anspruchssatz \) als Eingabe für die Verarbeitung der Logik verwenden.

Weitere Informationen zur Transformation von Ansprüchen finden Sie unter [When to Use a Transform Claim Rule](When-to-Use-a-Transform-Claim-Rule.md).

### <a name="step-3--execution-result"></a>Schritt 3: Ausführungsergebnis
Die letzte Phase der Ausführung von Anspruchsregelsätzen beginnt, sobald alle Regeln in einem bestimmten Regelsatz ausgeführt wurden und der abschließende Satz von Ansprüchen im Ausgangsanspruchssatz enthalten ist. An diesem Punkt gibt die Anspruchs-Engine den Kontext des Ausgabeanspruchs als Ausgabe der Regelsatzausführung zurück. Ab diesem Punkt übernimmt die Anspruchspipeline und überträgt diese abschließende Ausgabe an die nächste Stufe im Prozess.

## <a name="sending-the-execution-output-to-the-claims-pipeline"></a>Übertragen der Ausgabe der Ausführung an die Anspruchspipeline
Wenn die Anspruchs-Engine einen Regelsatz verarbeitet, besitzt dieser Regelsatz eigene dedizierte Speicherbereiche für den Eingangs- und Ausgangsanspruchssatz. Dies bedeutet, dass sich Eingangs- und Ausgangsanspruchssatz der einzelnen Regelsätze unterscheiden.

Nachdem der gesamte Prozess für die \( Schritte 1, 2 und 3 der Regel festgelegt wurde \) , wird der neu ausgestellte ausgehende Anspruchs \( Inhalt des Ausgangs Anspruchssatzes \) als Eingabe für den nächsten Regelsatz in der Anspruchs Pipeline verwendet. Dadurch können Ansprüche von der Ausgabe des einen Regelsatzes an die Eingabe für einen anderen Regelsatz übertragen werden, wie in der folgenden Abbildung dargestellt.

![Rollen AD FS](media/adfs2_enginecontexts.gif)

> [!NOTE]
> Obwohl der Ausstellungsregelsatz ebenfalls eine wichtige Phase der Pipeline darstellt, wird er in der obigen Abbildung nicht dargestellt, um die Abbildung zu vereinfachen. Eine Darstellung des Ausstellungsregelsatzes und seiner Rolle in der Anspruchspipeline finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).

In diesem Fall wird die Ausgabe der Akzeptanzregeln von der Pipeline verwendet, um den von den Akzeptanzregeln erstellten abschließenden Satz von Ansprüchen an die zweite Phase der Pipeline zu übertragen, in der die Autorisierungsregeln verarbeitet werden. An diesem Punkt würde der gesamte Ausführungsprozess der Anspruchs Regeln ( \( 1, 2 und 3 oben) \) für den Autorisierungs Regel Satz erneut ausgeführt werden. Dieser Vorgang wird fortgesetzt, bis die Ausstellungs Regel \( die letzte Phase in der Pipeline \) abgeschlossen hat.

Sobald die abschließenden ausgehenden Ansprüche für den Ausstellungsregelsatz von der Engine zurückgegeben wurden, werden sie in ein SAML-Token verpackt. Der Verbunddienst sendet das Token dann zurück an den Client.

## <a name="processing-authorization-rules"></a>Verarbeiten von Autorisierungsregeln
Wenn der Anspruchs Regel Satz, der während des Schritts 2 der Anspruchs Regel Ausführung ausgeführt wird, aus Autorisierungs Regeln besteht, \( die über einen anderen Eingabe-und Ausgangs Anspruchssatz als Akzeptanz-oder Ausstellungsregeln verfügen \) , werden diese Autorisierungs Regeln ausgeführt, um zu bestimmen, ob ein tokenanforderer autorisiert ist, ein Sicherheits Token für eine bestimmte vertrauende Seite vom Verbunddienst basierend auf den Ansprüchen der an

Das Ziel von Autorisierungsregeln ist die Ausstellung eines Zulassungs- oder Verweigerungsanspruchs basierend darauf, ob der Benutzer berechtigt ist, ein Token für die angegebene vertrauende Seite abzurufen. Wie in der folgenden Abbildung gezeigt, wird die Ausgabe der Autorisierungs Ausführung von der Pipeline verwendet, um zu bestimmen, ob der Ausstellungs Regel Satz ausgeführt wird oder nicht – basierend auf dem vorhanden sein oder Fehlen des Zulassungs-oder Ablehnungs \/ Anspruchs – die Ausführungs Ausgabe der Autorisierung selbst wird jedoch nicht als Eingabe für den Anspruchs Regelsatz verwendet.

![Rollen AD FS](media/adfs2_authorization.gif)

Weitere Informationen zur Autorisierung von Ansprüchen finden Sie unter [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md).


