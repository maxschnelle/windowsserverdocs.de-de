---
ms.assetid: ffb9d63c-ba7c-4ad1-b814-6db67f98c943
title: Rolle der Anspruchspipeline
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: ab5cfba579313cbe6aa56c84fb59a87e06101f15
ms.sourcegitcommit: b00d7c8968c4adc8f699dbee694afe6ed36bc9de
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/08/2020
ms.locfileid: "80853843"
---
# <a name="the-role-of-the-claims-pipeline"></a>Rolle der Anspruchspipeline
Die Anspruchs Pipeline in Active Directory-Verbunddienste (AD FS) \(AD FS\) den Pfad darstellt, den Ansprüche durch die Verbunddienst befolgen müssen, bevor Sie ausgestellt werden können. Der Verbunddienst verwaltet die gesamte End\-, um den Prozess der eingehenden Ansprüche durch die verschiedenen Phasen der Anspruchs Pipeline zu\-, die auch die Verarbeitung von Anspruchs Regeln durch die Anspruchs Regel-Engine einschließt.  
  
Weitere Informationen zu Anspruchs Regeln finden Sie [unter der Rolle von Anspruchs Regeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln durch das Anspruchsregelmodul finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  
Im folgenden Abschnitt wird der vom Verbunddienst verwaltete Prozess ausführlicher beschrieben.  
  
## <a name="claims-pipeline-process"></a>Anspruchspipelineprozess  
Der Anspruchs Pipeline Prozess besteht aus drei Stufen mit hoher\-Ebene. Jede Phase in diesem Prozess initialisiert das Anspruchsregelmodul, um für diese Phase spezifische Anspruchsregeln zu verarbeiten. Diese Phasen umfassen \(in der Reihenfolge, in der Sie auftreten\):  
  
1.  Akzeptieren von eingehenden Ansprüchen: Diese Phase der Anspruchspipeline wird verwendet, um die eingehenden Ansprüche aus dem Token zu extrahieren und nicht erwartete oder nicht vertrauenswürdige Ansprüche zu entfernen. Nach dem Extrahieren werden die Akzeptanzregeln ausgeführt, aus denen sich der Akzeptanztransformations-Regelsatz für eine Anspruchsanbieter-Vertrauensstellung zusammensetzt. Diese Regeln können verwendet werden, um Ansprüche weiterzuleiten oder neue Ansprüche hinzuzufügen, die dann in den nachfolgenden Phasen der Anspruchspipeline verwendet werden können. Die Ausgabe dieser Phase wird als Eingabe für die zweite und dritte Phase verwendet.  
  
2.  Autorisieren des Anspruchsanforderers: Diese Phase wird vom Anspruchsmodul verwendet, um Zulassungs- oder Verweigerungsansprüche auszustellen. Dies erfolgt in Abhängigkeit davon, ob der Anforderer des Tokens berechtigt ist, ein Token für eine bestimmte vertrauende Seite zu erhalten. Zuvor werden jedoch die Autorisierungsregeln ausgeführt, aus denen sich entweder der Ausstellungsautorisierungs-Regelsatz oder der Delegationsautorisierungs-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt.  
  
3.  Ausstellen von ausgehenden Ansprüchen: Diese Phase wird verwendet, um ausgehende Ansprüche auszustellen und entlang der Pipeline zu senden, wo sie in ein Sicherheitstoken gepackt werden. Zuvor werden jedoch die Ausstellungsregeln ausgeführt, aus denen sich der Ausstellungstransformations-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt. Diese bestimmen, welche Ansprüche als ausgehende Ansprüche ausgestellt werden.  
  
In allen drei oben aufgeführten Phasen werden Anspruchsregeln verarbeitet, jedoch jeweils anhand eines anderen Regelsatzes. Wie oben beschrieben ist jeder Phase ein Regelsatz zugeordnet, der entweder auf dem Aussteller der eingehenden Ansprüche \(den Akzeptanz Regeln\) oder auf dem Ziel Dienst basiert, für den die claimincludes \(Autorisierungs-und Ausstellungsregeln\)ausgegeben werden.  
  
Ansprüche sind Token\-agnostisch, werden jedoch über das Netzwerk übertragen, das in Sicherheits Token gekapselt ist. Die Anspruchsregeln werden unabhängig vom Format des eingehenden oder ausgehenden Sicherheitstokens auf Ansprüche angewendet.  
  
Anspruchs Regeln enthalten die vom Administrator\-definierte Logik, mit der das Anspruchs Modul die eingehenden Ansprüche akzeptiert, Ansprüche basierend auf der Identität des Anforderers autorisiert und Ansprüche ausstellt, die von einer vertrauenden Seite benötigt werden. Letztlich wird durch das Anspruchsmodul bestimmt, welche Ansprüche in das Sicherheitstoken aufgenommen werden, das ausgestellt wird, nachdem der Anspruch die Anspruchspipeline durchlaufen hat.  
  
Wie in der folgenden Abbildung gezeigt, ist die Anspruchs Pipeline dafür verantwortlich, dass die Anspruchs Pipeline\-den Vorgang zum Durchlaufen eines Anspruchs durch die verschiedenen Pipeline Stufen\-, um einen ausgestellten Anspruch zu erhalten, der über eine Vertrauensstellung der vertrauenden Seite gesendet wird. Der ausgehende Anspruch in der Abbildung stellt den ausgestellten Anspruch dar.  
  
![Rollen AD FS](media/adfs2_pipeline.gif)  
  
Obgleich dies in der Abbildung nicht dargestellt ist, erfolgt die tatsächliche Verarbeitung der Regeln in den einzelnen Phasen durch das Anspruchsmodul. Weitere Informationen finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  

