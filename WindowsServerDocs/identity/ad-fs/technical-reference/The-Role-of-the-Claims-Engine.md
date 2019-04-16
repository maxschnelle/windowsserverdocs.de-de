---
ms.assetid: 8b15d44e-e4e6-4510-aa91-cc7ec7161b0a
title: Die Rolle des Anspruchsmoduls
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 930b6f8034f17d8902104419042f944b82e90b4f
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-the-claims-engine"></a>Die Rolle des Anspruchsmoduls
Auf der höchsten Ebene ist das anspruchsmodul in Active Directory Federation Services \(AD FS\) eine Rule\-Modul, das für die Bereitstellung und Verarbeitung von anspruchsanforderungen für den Verbunddienst vorgesehen ist. Das anspruchsmodul ist die einzige Komponente im Verbunddienst, der für die Ausführung der einzelnen Regelsätze für alle verbundenen Vertrauensstellungen, die Sie konfiguriert haben und die Übergabe des Ausgabeergebnisses an die anspruchspipeline verantwortlich ist.  
  
Während die anspruchspipeline um ein eher logisches Konzept des ist angeblich der zur Implementierung-zu-Ende-Prozess für den anspruchsverlauf handelt, Anspruchsregeln ein tatsächliches administratives Element handelt, das Sie verwenden können, um den anspruchsverlauf während der Ausführungsprozess der Anspruchsregeln anpassen. Weitere Informationen zu den pipelineprozessen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
In der folgenden Abbildung, das Act Annahme von eingehenden Ansprüchen \(acceptance rules\), siehe Ansprüche autorisieren \(authorization rules\) anfordern und Ausstellen von ausgehenden Ansprüchen, dass durch das anspruchsmodul \(issuance rules\) Anspruchsregeln für alle verbundenen Vertrauensstellungen in Ihrer Organisation ausgeführt wird.  
  
![AD FS-Rollen](media/adfs2_enginepipeline.gif)  
  
## <a name="claim-rules-execution-process"></a>Anspruchsregeln  
Beim Konfigurieren einer Anspruchsanbieter-Vertrauensstellung oder vertrauende Vertrauen in Ihrer Organisation mit Anspruchsregeln, die Anspruch Regel set\(s\) für Act Vertrauensstellung als Gatekeeper für eingehende Ansprüche durch das anspruchsmodul, um die erforderliche Logik in den Anspruchsregeln, um zu bestimmen, ob alle Ansprüche ausgeben und welche Ansprüche auszugeben aufrufen.  
  
Im folgende Abschnittwerden die Schrittebeschrieben, die vom Modul während der anspruchsverlauf in der Ausführungsprozess der Anspruchsregeln auftreten. Alle Schrittetritt auf, wie im folgenden beschrieben für jede Phase, in der anspruchspipelineprozess beschrieben. Diese Schritteumfassen:  
  
-   Schritt1: Initialisierung  
  
-   Schritt2: Ausführung  
  
-   Schritt3: Ausführungsergebnis  
  
Weitere Informationen zu den pipelineprozessen finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
### <a name="step-1--initialization"></a>Schritt1: Initialisierung  
Im ersten Schrittdes der Ausführungsprozess der Anspruchsregeln akzeptiert das anspruchsmodul eingehende Ansprüche, indem Sie sie zum ersten Hinzufügen der *eingangsanspruchssatz*. Ein eingangsanspruchssatz entspricht dem Cache im Arbeitsspeicher, der verwendet wird, um Daten temporär zu speichern, nur so lange ein Prozess erforderlichen Daten, die für den Abruf zur Verfügung gestellt erfordert. Der eingangsanspruchssatz Daten werden nach der regelausführung verworfen.  
  
#### <a name="adding-a-claim-to-the-input-claim-set-for-a-rule-set"></a>Hinzufügen von Ansprüchen zum eingangsanspruchssatz für einen Regelsatz  
Der eingangsanspruchssatz wird vom anspruchsmodul erstellt, wenn Anspruchsdaten temporär im Speicher zu speichern, während es die Logik, die ein anspruchsregelsatz zugeordneten verarbeitet werden muss. Das anspruchsmodul kopiert alle eingehenden Ansprüche in den eingangsanspruchssatz, in dem sie durch die erste Regel im Regelsatz abgerufen werden können.  
  
Beispielsweise liest das anspruchsmodul in der folgenden Abbildung, die Ansprüche A und B aus den eingehenden Ansprüchen und kopiert sie in den eingangsanspruchssatz. Nachdem sie in den eingangsanspruchssatz sind, wird das anspruchsmodul abgerufen und Ansprüche A und B als Eingabe für die Logik in der ersten Regel in der anspruchsregelsatzes verarbeitet.  
  
![AD FS-Rollen](media/adfs2_context1.gif)  
  
Alle Regeln in ein anspruchsregelsatz Teilen denselben eingangsanspruchssatz. Jede Regel in diesem Satz kann dem freigegebenen eingangsanspruchssatz, damit alle nachfolgende Regeln im Satz beeinflussen hinzufügen.  
  
### <a name="step-2--execution"></a>Schritt2: Ausführung  
In diesem Schrittdes Prozesses Anspruch Regeln werden Anspruchsregeln verarbeitet, wenn das anspruchsmodul chronologisch alle Regeln in einem bestimmten Regelsatz zu einem Zeitpunkt Schritte. Jede Regel innerhalb eines Regelsatzes wird nur einmal ausgeführt und wird ausgeführt, in der Reihenfolge von oben nach unten werden wie in dem Dialogfeld "Anspruchsregeln bearbeiten" in AD FS-Verwaltungs-Snap-In angezeigt. Die Anspruchsregel ein, die am oberen Rand der Regel festgelegt wird zuerst verarbeitet wird, und klicken Sie dann die nachfolgenden Regeln verarbeitet, bis alle Regeln ausgeführt wurden.  
  
Gemäß der Definition in der anspruchsregelsprache besteht eine Anspruchsregel aus zwei Teilen: Bedingung und ausstellungsanweisung. Das Ansprüche Modul zuerst verarbeitet der Bedingungsteil anhand der Daten in der Eingabe ausgangsanspruchssatz zu bestimmen, ob die in der Regel angegebene Bedingung für die Ansprüche in der Eingabe zutrifft ausgangsanspruchssatz \ (die Ansprüche, die der Regelbedingung entsprechen, werden als eine übereinstimmende Claims\ bezeichnet). Wenn übereinstimmende Ansprüche gefunden werden, führt das anspruchsmodul die ausstellungsanweisung der Regel für jeden Satz übereinstimmender Ansprüche aus. Die ausstellungsanweisung der Regel kann die folgenden Aufgaben mit den übereinstimmenden Ansprüchen durchführen:  
  
1.  Kopieren eines übereinstimmenden Anspruchs in den ausgabeanspruchssatz kopiert  
  
2.  Umwandeln der anspruchsfelder und erstellen Sie eine neue Anforderung entweder nur dem eingangsanspruchssatz oder ausgangsanspruchssatz in Auswertung und Ausgabe.  
  
3.  Verwenden Sie die übereinstimmenden claim\(s\) als Schlüssel zum Suchen nach Informationen in einem Attributspeicher erstellen neue claim\(s\) entweder nur dem eingangsanspruchssatz oder ausgangsanspruchssatz in ein- und Ausgabe.  
  
#### <a name="adding-a-claim-to-the-output-claim-set-for-a-rule-set"></a>Hinzufügen von Ansprüchen zum ausgangsanspruchssatz für einen Regelsatz  
Die *ausgangsanspruchssatz* ist ein Speicherort im Arbeitsspeicher, die anfänglich leer ist wichtig, da das anspruchsmodul nur Ansprüche, die sich im ausgangsanspruchssatz zurück nach Abschluss der Ausführung befinden. Das bedeutet, die Ansprüche, die nur im eingangsanspruchssatz befinden sich festgelegt und nicht in den ausgabeanspruchssatz kopiert werden bei der Zeit für die Berechnung der abschließende Satz von ausgehenden Ansprüchen ignoriert.  
  
#### <a name="adding-a-claim-to-both-claim-sets-for-a-rule-set"></a>Hinzufügen von Ansprüchen zu beiden Anspruchssätzen für einen Regelsatz  
Wie eine Regel verarbeitet wird, werden Ansprüche entweder in der Eingabe hinzugefügt oder beiden eingabeanspruchssatz als auch je nach Anweisung, die in der Regel ausstellungsanweisung verwendet wird. Die anspruchsregelsprache bezeichnet diese Anweisungen als *hinzufügen* oder *Problem*.  
  
Wenn die *hinzufügen* Anweisung verwendet wird, werden die Ansprüche nur dem eingangsanspruchssatz hinzugefügt und die Ansprüche ist nur für die Zwecke der Ausführung vorhanden und wird nicht mehr vorhanden sind, nach Abschluss der Ausführung. Wenn die *Problem* -Anweisung verwendet, die Ansprüche im eingangsanspruchssatz und dem ausgangsanspruchssatz hinzugefügt, und die Ansprüche im ausgangsanspruchssatz nach Abschluss der Ausführung zurückgegeben. Weitere Informationen zu diesen Anweisungen finden Sie unter [The Role of the Claim Rule Language](The-Role-of-the-Claim-Rule-Language.md).  
  
Entspricht der Bedingungsteil einer Regel in einem Regelsatz keine Ansprüche im eingangsanspruchssatz, wird der ausstellungsanweisungsteil der Regel ignoriert, und daher keine Ansprüche entweder den ausgabeanspruchssatz kopiert oder dem eingabeanspruchssatz hinzugefügt werden. Die folgende Abbildungund die entsprechenden Schrittezeigen, was passiert, wenn das anspruchsmodul eine transformationsregel ausführt:  
  
![AD FS-Rollen](media/adfs2_context2.gif)  
  
1.  Eingehende Ansprüche werden die vom anspruchsmodul festgelegten eingangsanspruchssatz hinzugefügt.  
  
2.  Wenn die erste Regel ausgeführt wird, die Ansprüche A und B, die zu diesem Zeitpunkt die einzigen Ansprüche im eingabeanspruchssatz sind, erkennt und verarbeitet den Bedingungsteil der Logik in der Regel 1 wird.  
  
3.  Da der Anspruch A im eingangsanspruchssatz vorhanden ist, wird die Bedingung der Regel um wahr zu sein bestimmt \ (Übereinstimmung mit Anspruch a) und ein neuer C#-Anspruch wird sowohl dem Eingangs- und dem ausgangsanspruchssatz hinzugefügt.  
  
4.  Regel 2 können jetzt die Ansprüche A, B und C \ (alle Ansprüche im Anspruch Set) als Eingabe für die Verarbeitung der Logik.  
  
Weitere Informationen zur Transformation von Ansprüchen finden Sie unter [a Transform Claim Rule verwenden](When-to-Use-a-Transform-Claim-Rule.md).  
  
### <a name="step-3--execution-result"></a>Schritt3: Ausführungsergebnis  
Die Endphase des Anspruchs regelsatzausführung beginnt, sobald alle Regeln in einem bestimmten Regelsatz ausgeführt wurden und der abschließende Satz von Ansprüchen im ausgangsanspruchssatz vorhanden ist. An diesem Punkt gibt das anspruchsmodul den Kontext des ausgangsanspruchssatz als Ausgabe der regelsatzausführung zurück. Ab diesem Punkt ist die anspruchspipeline, über die und überträgt diese abschließende Ausgabe an die nächste Stufe im Prozess.  
  
## <a name="sending-the-execution-output-to-the-claims-pipeline"></a>Senden die Ausgabe an die anspruchspipeline  
Wenn das anspruchsmodul Prozesse festgelegt eine Regel, dass Regelsatz eigene dedizierte Speicherbereiche für den Eingangs- und ausgangsanspruchssatz. Dies bedeutet, dass der Eingangs- und ausgangsanspruchssatz Sätze von einem Regelsatz verwendet werden getrennt von der Eingabe und ausgangsanspruchssatz in einen anderen Regelsatz verwendet.  
  
Nach dem Ausführen des gesamten Prozess für einen bestimmten Regelsatz \ (die Schritte1, 2 und 3\), die neu ausgestellten ausgehenden Ansprüche \ (Inhalt von der Ausgabe Anspruch Set) als Eingabe für den nächsten Regelsatz in der anspruchspipeline verwendet werden. Dadurch können Ansprüche aus der Ausgabe des einen Regelsatzes an die Eingabe für einen anderen Regelsatz übertragen werden, wie in der folgenden Abbildungdargestellt.  
  
![AD FS-Rollen](media/adfs2_enginecontexts.gif)  
  
> [!NOTE]  
> Obwohl der ausstellungsregelsatz ebenfalls eine wichtige Phase der Pipeline ist, wird Sie von die obigen Abbildungnicht nur zum Zweck der Vereinfachung der Abbildunggezeigt. Eine Darstellung des ausstellungsregelsatzes und wie sie in der anspruchspipeline passt, finden Sie unter [The Role of the Claims Pipeline](The-Role-of-the-Claims-Pipeline.md).  
  
In diesem Fall wird die Ausgabe der akzeptanzregeln von der Pipeline verwendet, übertragen Sie die endgültige Gruppe von Ansprüchen von den akzeptanzregeln an die zweite Phase der Pipeline die Verarbeitung von Autorisierungsregeln ist. Zu diesem Zeitpunkt die gesamte Ausführungsprozess der Anspruch \ (Schritte1, 2 und 3 Above\) würde für den autorisierungsregelsatz erneut ausgeführt. Dieser Zyklus wird fortgesetzt, bis die Ausstellung Regelsatz \ (der letzte Schrittin der Pipeline\) abgeschlossen wurde.  
  
Sobald die abschließenden ausgehenden Ansprüche aus dem Modul für den ausstellungsregelsatz zurückgegeben wurden, sie werden in ein SAML-Token verpackt werden, und der Verbunddienst sendet das Token dann zurück an den Client.  
  
## <a name="processing-authorization-rules"></a>Verarbeiten von Autorisierungsregeln  
Wenn der anspruchsregelsatz, die in Schritt2 des der Ausführungsprozess der Anspruchsregeln ausgeführt wird von Autorisierungsregeln besteht \ (die anderen Eingangs- und legt als die Akzeptanz- und ausstellungsregeln Rules\ Anspruch Ausgabe haben), und klicken Sie dann diese Autorisierungsregeln ausgeführt werden, um festzustellen, ob der anforderer des Tokens autorisiert ist, um ein Sicherheitstoken für eine bestimmte vertrauende Seite vom Verbunddienst Ansprüche des anforderers-basierte zu erhalten.  
  
Das Ziel von Autorisierungsregeln ist Zulassungs- oder verweigerungsanspruchs basierend darauf, ob der Benutzer berechtigt ist, ein Token für eine bestimmte vertrauende Seite abzurufen ist. Wie in der folgenden Abbildunggezeigt, die Ausgabe der Autorisierung wird verwendet von der Pipeline um zu bestimmen, ob der ausstellungsregelsatz oder nicht ausgeführt wird – basierend auf dem Vorhandensein oder fehlen die And\ zulassen / oder verweigerungsanspruchs – aber Ausgabe der Autorisierung selbst wird nicht als Eingabe für den anspruchsregelsatz verwendet.  
  
![AD FS-Rollen](media/adfs2_authorization.gif)  
  
Weitere Informationen zur Autorisierung von Ansprüchen finden Sie unter [Wann sollte eine Autorisierungsanspruchsregel verwendet](When-to-Use-an-Authorization-Claim-Rule.md).  
  

