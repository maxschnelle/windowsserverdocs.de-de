---
ms.assetid: ffb9d63c-ba7c-4ad1-b814-6db67f98c943
title: Rolle der Anspruchspipeline
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5076a686b5d0b9a539f6cad8594aaf84dccc3edb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59887061"
---
>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

# <a name="the-role-of-the-claims-pipeline"></a>Rolle der Anspruchspipeline
Die anspruchspipeline in Active Directory Federation Services \(AD FS\) steht für den Pfad an, die Ansprüche innerhalb des Verbunddiensts ausführen müssen, bevor sie ausgestellt werden können. Der Verbunddienst verwaltet den gesamte End\-zu\-Prozess des anspruchsverlaufs in den verschiedenen Phasen der anspruchspipeline, darunter auch die Verarbeitung von Anspruchsregeln durch die Anspruchsregel-Engine zu beenden.  
  
Weitere Informationen zu Anspruchsregeln finden Sie unter [die Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln durch das Anspruchsregelmodul finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  
Im folgenden Abschnitt wird der vom Verbunddienst verwaltete Prozess ausführlicher beschrieben.  
  
## <a name="claims-pipeline-process"></a>Anspruchspipelineprozess  
Der anspruchspipelineprozess besteht aus drei hohe\-Ebene Phasen. Jede Phase in diesem Prozess initialisiert das Anspruchsregelmodul, um für diese Phase spezifische Anspruchsregeln zu verarbeiten. Diese Phasen umfassen \(in der Reihenfolge ihres Auftretens\):  
  
1.  Akzeptieren von eingehenden Ansprüchen: Diese Phase der Anspruchspipeline wird verwendet, um die eingehenden Ansprüche aus dem Token zu extrahieren und nicht erwartete oder nicht vertrauenswürdige Ansprüche zu entfernen. Nach dem Extrahieren werden die Akzeptanzregeln ausgeführt, aus denen sich der Akzeptanztransformations-Regelsatz für eine Anspruchsanbieter-Vertrauensstellung zusammensetzt. Diese Regeln können verwendet werden, um Ansprüche weiterzuleiten oder neue Ansprüche hinzuzufügen, die dann in den nachfolgenden Phasen der Anspruchspipeline verwendet werden können. Die Ausgabe dieser Phase wird als Eingabe für die zweite und dritte Phase verwendet.  
  
2.  Autorisieren des Anspruchsanforderers: Diese Phase wird vom Anspruchsmodul verwendet, um Zulassungs- oder Verweigerungsansprüche auszustellen. Dies erfolgt in Abhängigkeit davon, ob der Anforderer des Tokens berechtigt ist, ein Token für eine bestimmte vertrauende Seite zu erhalten. Zuvor werden jedoch die Autorisierungsregeln ausgeführt, aus denen sich entweder der Ausstellungsautorisierungs-Regelsatz oder der Delegationsautorisierungs-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt.  
  
3.  Ausstellen von ausgehenden Ansprüchen: Diese Phase wird verwendet, um ausgehende Ansprüche auszustellen und entlang der Pipeline zu senden, wo sie in ein Sicherheitstoken gepackt werden. Zuvor werden jedoch die Ausstellungsregeln ausgeführt, aus denen sich der Ausstellungstransformations-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt. Diese bestimmen, welche Ansprüche als ausgehende Ansprüche ausgestellt werden.  
  
In allen drei oben aufgeführten Phasen werden Anspruchsregeln verarbeitet, jedoch jeweils anhand eines anderen Regelsatzes. Wie oben beschrieben, verfügt jede Phase einen zugeordneten Satz von Regeln basierend auf entweder auf dem Aussteller der eingehenden Ansprüche \(akzeptanzregeln\) oder den Zieldienst für die die Claimincludes ausgestellt werden \(Autorisierung und Regeln für die anspruchsausstellung\).  
  
Ansprüche sind token\-sind aber unabhängig in Sicherheitstoken gekapselt über das Netzwerk zu übertragen. Die Anspruchsregeln werden unabhängig vom Format des eingehenden oder ausgehenden Sicherheitstokens auf Ansprüche angewendet.  
  
Ansprüche, die Regeln enthalten, den Administrator\-definierte Logik, mit dem die Anspruchs-Engine werden die eingehenden Ansprüche akzeptiert, Ansprüche basierend auf der Identität des anforderers autorisiert und Ansprüche ausstellt, durch eine vertrauende Seite erforderlich sind. Letztlich wird durch das Anspruchsmodul bestimmt, welche Ansprüche in das Sicherheitstoken aufgenommen werden, das ausgestellt wird, nachdem der Anspruch die Anspruchspipeline durchlaufen hat.  
  
Wie in der folgenden Abbildung gezeigt wird, wird die anspruchspipeline verantwortlich für das gesamte Ende\-zu\-Ende des Prozesses, der Eigenschaften eines Anspruchs über die verschiedenen Phasen der Pipeline, um die Ausstellung erhalten, die über eine der vertrauenden Seite gesendet werden Vertrauensstellung. Der ausgehende Anspruch in der Abbildung stellt den ausgestellten Anspruch dar.  
  
![AD FS-Rollen](media/adfs2_pipeline.gif)  
  
Obgleich dies in der Abbildung nicht dargestellt ist, erfolgt die tatsächliche Verarbeitung der Regeln in den einzelnen Phasen durch das Anspruchsmodul. Weitere Informationen finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  

