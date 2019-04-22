---
ms.assetid: 8b15d44e-e4e6-4510-aa91-cc7ec7161b0a
title: Rolle des Anspruchsmoduls
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 930b6f8034f17d8902104419042f944b82e90b4f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814931"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-the-claims-engine"></a>Rolle des Anspruchsmoduls
Auf der höchsten Ebene, die Anspruchs-engine in Active Directory-Verbunddienste \(AD FS\) ist eine Regel\-Basis-Engine, die für die Bereitstellung und Verarbeitung von anspruchsanforderungen für den Verbunddienst vorgesehen ist. Das Anspruchsmodul ist die einzige Komponente im Verbunddienst, die für die Ausführung der einzelnen Regelsätze für alle verbundenen Vertrauensstellungen, die Sie konfiguriert haben, und die Weitergabe des Ausgabeergebnisses an die Anspruchspipeline verantwortlich ist.  
  
Während der anspruchspipeline mehr ein logisches Konzept des Endes\-zu\-Ende des Prozesses für anspruchsverlaufs, beanspruchen Sie die Regeln sind ein tatsächliches administratives Element, das Sie verwenden können, um den Fluss der Ansprüche während der Ausführungsprozess der Anspruchsregeln anpassen. Weitere Informationen zu den Pipelineprozessen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
Wie in der folgenden Abbildung wird der Vorgang der Annahme von eingehenden Ansprüchen dargestellt \(akzeptanzregeln\), Autorisieren von Ansprüchen anfordernde Personen \(Autorisierungsregeln\) und Ausgeben von ausgehenden Ansprüchen \( Regeln für die anspruchsausstellung\) über Anspruch Regeln für alle verbundenen Vertrauensstellungen in Ihrer Organisation durch die Anspruchs-Engine ausgeführt wird.  
  
![AD FS-Rollen](media/adfs2_enginepipeline.gif)  
  
## <a name="claim-rules-execution-process"></a>Ausführung von Anspruchsregeln  
Wenn Sie eine Anspruchsanbieter-Vertrauensstellung oder Vertrauensstellung der vertrauenden in Ihrer Organisation mit Anspruchsregeln konfigurieren, legen Sie die Anspruchsregel\(s\) für diese Vertrauensstellung fungieren als Gatekeeper für eingehende Ansprüche durch den Aufruf von der Anspruchs-Engine, um die erforderlichen anzuwenden. die Logik in die Anspruchsregeln, um zu bestimmen, ob alle Ansprüche ausgeben und welche Ansprüche auszugeben.  
  
Im folgenden Abschnitt werden die Schritte beschrieben, die das Modul während des Ausführungsflusses für Anspruchsregeln ausführt. Alle unten aufgeführten Schritte treten in sämtlichen Phasen auf, die im Ablauf der Anspruchspipeline beschrieben sind. Diese Schritte umfassen:  
  
-   Schritt 1: Initialisierung  
  
-   Schritt 2: Ausführung  
  
-   Schritt 3: Ausführungsergebnis  
  
Weitere Informationen zu den Pipelineprozessen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
### <a name="step-1--initialization"></a>Schritt 1: Initialisierung  
Im ersten Schritt des Ausführungsprozesses für Anspruchsregeln akzeptiert das Anspruchsmodul eingehende Ansprüche, indem es diese zunächst dem *Eingangsanspruchssatz* hinzufügt. Ein Eingangsanspruchssatz entspricht dem Cache im Arbeitsspeicher, in dem Daten nur so lange temporär gespeichert werden, bis der entsprechende Prozess die erforderlichen Daten abruft. Der Eingangsanspruchssatz wird nach Abschluss der Regelausführung verworfen.  
  
#### <a name="adding-a-claim-to-the-input-claim-set-for-a-rule-set"></a>Hinzufügen von Ansprüchen zum Eingangsanspruchssatz für einen Regelsatz  
Der Eingangsanspruchssatz wird vom Anspruchsmodul erstellt, wenn dieses Anspruchsdaten temporär im Arbeitsspeicher speichern muss, während es die Logik eines Anspruchsregelsatzes verarbeitet. Das Anspruchsmodul kopiert alle eingehenden Ansprüche in den Eingangsanspruchssatz, aus dem sie durch die erste Regel im Regelsatz abgerufen werden können.  
  
Das Anspruchsmodul in der Abbildung unten liest z. B. die Ansprüche A und B aus den eingehenden Ansprüchen und kopiert sie in den Eingangsanspruchssatz. Wenn sie im Eingangsanspruchssatz sind, ruft das Anspruchsmodul die Ansprüche A und B als Eingabe als Eingabe für die Logik in der ersten Regel des Anspruchsregelsatzes ab und verarbeitet sie.  
  
![AD FS-Rollen](media/adfs2_context1.gif)  
  
Alle Regeln im Anspruchsregelsatz nutzen denselben Eingangsanspruchssatz. Jede Regel in diesem Satz kann dem freigegebenen Eingangsanspruchssatz etwas hinzufügen und damit alle nachfolgenden Regeln im Satz beeinflussen.  
  
### <a name="step-2--execution"></a>Schritt 2: Ausführung  
In diesem Schritt des Anspruchsregelprozesses werden die Anspruchsregeln verarbeitet, indem das Anspruchsmodul nacheinander alle Regeln in einem bestimmten Regelsatz durchläuft. Jede Regel innerhalb eines Regelsatzes nur einmal ausgeführt wird, und wird ausgeführt, in der Reihenfolge, in dem sie von oben nach unten angezeigt werden wie angezeigt im Dialogfeld "Anspruchsregeln bearbeiten" im AD FS-Verwaltungs-Snap-\-in. Die Anspruchsregel ganz oben im Regelsatz wird zuerst verarbeitet, und danach werden die nachfolgenden Regeln verarbeitet, bis alle Regeln ausgeführt wurden.  
  
Gemäß der Definition der Anspruchsregelsprache besteht eine Anspruchsregel aus zwei Teilen: Bedingung und Ausstellungsanweisung. Die erste Prozesse Engine Ansprüche der Bedingungsteil anhand der Daten in der Eingabe Anspruchssatz, um zu bestimmen, ob die in der Regel angegebene Bedingung "true" für die Ansprüche in der Eingabe enthält Satz von Ansprüchen \(die Ansprüche, die mit der Regel übereinstimmen. Bedingung, werden als übereinstimmende Ansprüche bezeichnet\). Wenn übereinstimmende Ansprüche gefunden werden, führt das Anspruchsmodul die Ausstellungsanweisung der Regel für jeden Satz übereinstimmender Ansprüche aus. Die Ausstellungsanweisung der Regel kann eine der folgenden Aufgaben mit den übereinstimmenden Ansprüchen durchführen:  
  
1.  Kopieren eines übereinstimmenden Anspruchs in den Ausgangsanspruchssatz  
  
2.  Umwandeln der Anspruchsfelder und Erstellen eines neuen Anspruchs – entweder nur im Eingangsanspruchssatz oder sowohl im Evaluierungssatz als auch im Ausgangsanspruchssatz  
  
3.  Verwenden Sie den übereinstimmenden Anspruch\(s\) als Schlüssel zum Suchen von Informationen aus einem Attributspeicher zum Erstellen des neuen Anspruchs\(s\) entweder nur die Eingabe Satz von Ansprüchen oder sowohl die ein- und Ausgabe Sätze von Ansprüchen.  
  
#### <a name="adding-a-claim-to-the-output-claim-set-for-a-rule-set"></a>Hinzufügen von Ansprüchen zum Ausgangsanspruchssatz für einen Regelsatz  
Der *Ausgangsanspruchssatz* ist ein Speicherort, der anfänglich leer ist. Er ist wichtig, da das Anspruchsmodul nach Abschluss der Ausführung ausschließlich Ansprüche zurückgibt, die sich im Ausgangsanspruchssatz befinden. Dies bedeutet, dass Ansprüche, die sich lediglich im Eingangsanspruchssatz befinden, aber nicht im Ausgangsanspruchssatz, bei der Berechnung des finalen Satzes von Ausgangsansprüchen ignoriert werden.  
  
#### <a name="adding-a-claim-to-both-claim-sets-for-a-rule-set"></a>Hinzufügen von Ansprüchen zu beiden Anspruchssätzen für einen Regelsatz  
Während der Verarbeitung einer Regel werden die Ansprüche je nach Anweisung in der Ausstellungsanweisung der Regel entweder dem Eingangsanspruchssatz oder beiden Anspruchssätzen hinzugefügt. Die Anspruchsregelsprache bezeichnet diese Anweisungen als *Hinzufügen* oder *Ausstellen*.  
  
Bei Verwendung der *Hinzufügen* -Anweisung werden die Ansprüche nur dem Eingangsanspruchssatz hinzugefügt. Die Ansprüche werden ausschließlich für die Ausführung verwendet und danach verworfen. Bei Verwendung der *Ausstellen*-Anweisung werden die Ansprüche dem Eingangs- und dem Ausgangsanspruchssatz hinzugefügt. Nach Abschluss der Ausführung werden die Ansprüche im Ausgangsanspruchssatz zurückgegeben. Weitere Informationen zu diesen Anweisungen finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  
Entspricht der Bedingungsteil einer Regel in einem Regelsatz keinen Ansprüchen im Eingangsanspruchssatz, wird der Ausstellungsanweisungsteil der Regel ignoriert. Es werden daher dann keine Ansprüche dem Eingangs- oder Ausgangsanspruchssatz hinzugefügt. Die folgende Abbildung und die zugehörigen Schritte zeigen, was passiert, wenn das Anspruchsmodul eine Transformationsregel ausführt:  
  
![AD FS-Rollen](media/adfs2_context2.gif)  
  
1.  Eingehende Ansprüche werden dem vom Anspruchsmodul festgelegten Eingangsanspruchssatz hinzugefügt.  
  
2.  Bei Ausführung der ersten Regel erkennt das Modul die Ansprüche A und B, die zu diesem Zeitpunkt die einzigen Ansprüche im Eingangsanspruchssatz sind, und verarbeitet den Bedingungsteil der Logik von Regel 1.  
  
3.  Da sich Anspruch A im eingangsanspruchssatz vorhanden ist, wird die Bedingung der Regel auf "true" werden bestimmt \(Übereinstimmung mit Anspruch A\) und neuer Anspruch C wird Satz von Ansprüchen zu beiden und dem ausgangsanspruchssatz hinzugefügt.  
  
4.  Regel 2 können Sie jetzt die Ansprüche A, B und C \(alle Ansprüche im ausgangsanspruchssatz\) als Eingabe für die Verarbeitung der Logik.  
  
Weitere Informationen zur Transformation von Ansprüchen finden Sie unter [When to Use a Transform Claim Rule](When-to-Use-a-Transform-Claim-Rule.md).  
  
### <a name="step-3--execution-result"></a>Schritt 3: Ausführungsergebnis  
Die letzte Phase der Ausführung von Anspruchsregelsätzen beginnt, sobald alle Regeln in einem bestimmten Regelsatz ausgeführt wurden und der abschließende Satz von Ansprüchen im Ausgangsanspruchssatz enthalten ist. An diesem Punkt gibt das Anspruchsmodul den Kontext des Ausgabeanspruchs als Ausgabe der Regelsatzausführung zurück. Ab diesem Punkt übernimmt die Anspruchspipeline und überträgt diese abschließende Ausgabe an die nächste Stufe im Prozess.  
  
## <a name="sending-the-execution-output-to-the-claims-pipeline"></a>Übertragen der Ausgabe der Ausführung an die Anspruchspipeline  
Wenn das Anspruchsmodul einen Regelsatz verarbeitet, besitzt dieser Regelsatz eigene dedizierte Speicherbereiche für den Eingangs- und Ausgangsanspruchssatz. Dies bedeutet, dass sich Eingangs- und Ausgangsanspruchssatz der einzelnen Regelsätze unterscheiden.  
  
Nach dem Ausführen des gesamten Prozess für einen bestimmten Regelsatz \(Schritte 1, 2 und 3\), wird die neu ausgehende Ansprüche ausgestellt \(Inhalt des Satz von Ansprüchen\) als Eingabe für den nächsten Regelsatz in der anspruchspipeline verwendet werden. Dadurch können Ansprüche von der Ausgabe des einen Regelsatzes an die Eingabe für einen anderen Regelsatz übertragen werden, wie in der folgenden Abbildung dargestellt.  
  
![AD FS-Rollen](media/adfs2_enginecontexts.gif)  
  
> [!NOTE]  
> Obwohl der Ausstellungsregelsatz ebenfalls eine wichtige Phase der Pipeline darstellt, wird er in der obigen Abbildung nicht dargestellt, um die Abbildung zu vereinfachen. Eine Darstellung des Ausstellungsregelsatzes und seiner Rolle in der Anspruchspipeline finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
In diesem Fall wird die Ausgabe der Akzeptanzregeln von der Pipeline verwendet, um den von den Akzeptanzregeln erstellten abschließenden Satz von Ansprüchen an die zweite Phase der Pipeline zu übertragen, in der die Autorisierungsregeln verarbeitet werden. An diesem Punkt die gesamte Ausführungsprozess der Anspruch \(Schritte 1, 2 und 3 oben\) würde für den autorisierungsregelsatz erneut ausgeführt. Dieser Zyklus wird fortgesetzt, bis der ausstellungsautorisierungs-Regelsatz \(der letzte Schritt in der Pipeline\) abgeschlossen wurde.  
  
Sobald die abschließenden ausgehenden Ansprüche für den Ausstellungsregelsatz vom Modul zurückgegeben wurden, werden sie in ein SAML-Token verpackt. Der Verbunddienst sendet das Token dann zurück an den Client.  
  
## <a name="processing-authorization-rules"></a>Verarbeiten von Autorisierungsregeln  
Wenn die Regelsatz von Ansprüchen, die in Schritt 2 des der Ausführungsprozess der Anspruchsregeln ausgeführt wird von Autorisierungsregeln besteht \(die haben eine andere Eingabe- / Ausgabe-Anspruch der Sets als Akzeptanz- und ausstellungsregeln Regeln\), klicken Sie dann die Autorisierungsregeln werden ausgeführt, um zu bestimmen, ob ein anforderer des Tokens autorisiert ist, um ein Sicherheitstoken für eine bestimmte vertrauende Seite über den Verbunddienst basierend auf der anfordernden Person Ansprüchen zu erhalten.  
  
Das Ziel von Autorisierungsregeln ist die Ausstellung eines Zulassungs- oder Verweigerungsanspruchs basierend darauf, ob der Benutzer berechtigt ist, ein Token für die angegebene vertrauende Seite abzurufen. Wie in der folgenden Abbildung dargestellt, die Ausgabe der Autorisierung wird verwendet, von der Pipeline um zu bestimmen, ob der ausstellungsregelsatz oder nicht ausgeführt wird – basierend auf Vorhandensein oder fehlen des Zulassungs- und\/oder verweigerungsanspruchs, aber die Autorisierung die Ausgabe der erweiterungsausführung selbst wird nicht als Eingabe für den anspruchsregelsatz verwendet.  
  
![AD FS-Rollen](media/adfs2_authorization.gif)  
  
Weitere Informationen zur Autorisierung von Ansprüchen finden Sie unter [When to Use an Authorization Claim Rule](When-to-Use-an-Authorization-Claim-Rule.md).  
  

