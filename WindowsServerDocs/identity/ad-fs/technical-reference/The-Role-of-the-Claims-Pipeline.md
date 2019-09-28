---
ms.assetid: ffb9d63c-ba7c-4ad1-b814-6db67f98c943
title: Rolle der Anspruchspipeline
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 6aafa37b06599f4114cf076e87415fece128fb05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407337"
---
# <a name="the-role-of-the-claims-pipeline"></a>Rolle der Anspruchspipeline
Die Anspruchs Pipeline in Active Directory-Verbunddienste (AD FS) \(AD FS\) stellt den Pfad dar, den Ansprüche durch die Verbunddienst befolgen müssen, bevor Sie ausgestellt werden können. Der Verbunddienst verwaltet den gesamten End\--\-to-End-Prozess der eingehenden Ansprüche durch die verschiedenen Phasen der Anspruchs Pipeline, die auch die Verarbeitung von Anspruchs Regeln durch die Anspruchs Regel-Engine beinhalten.  
  
Weitere Informationen zu Anspruchs Regeln finden Sie [unter der Rolle von Anspruchs Regeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln durch das Anspruchsregelmodul finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  
Im folgenden Abschnitt wird der vom Verbunddienst verwaltete Prozess ausführlicher beschrieben.  
  
## <a name="claims-pipeline-process"></a>Anspruchspipelineprozess  
Der Anspruchs Pipeline Prozess besteht aus drei Ebenen\-auf hoher Ebene. Jede Phase in diesem Prozess initialisiert das Anspruchsregelmodul, um für diese Phase spezifische Anspruchsregeln zu verarbeiten. Diese Phasen umfassen \(die Reihenfolge, in der\)Sie auftreten:  
  
1.  Akzeptieren von eingehenden Ansprüchen: Diese Phase der Anspruchspipeline wird verwendet, um die eingehenden Ansprüche aus dem Token zu extrahieren und nicht erwartete oder nicht vertrauenswürdige Ansprüche zu entfernen. Nach dem Extrahieren werden die Akzeptanzregeln ausgeführt, aus denen sich der Akzeptanztransformations-Regelsatz für eine Anspruchsanbieter-Vertrauensstellung zusammensetzt. Diese Regeln können verwendet werden, um Ansprüche weiterzuleiten oder neue Ansprüche hinzuzufügen, die dann in den nachfolgenden Phasen der Anspruchspipeline verwendet werden können. Die Ausgabe dieser Phase wird als Eingabe für die zweite und dritte Phase verwendet.  
  
2.  Autorisieren des Anspruchsanforderers: Diese Phase wird vom Anspruchsmodul verwendet, um Zulassungs- oder Verweigerungsansprüche auszustellen. Dies erfolgt in Abhängigkeit davon, ob der Anforderer des Tokens berechtigt ist, ein Token für eine bestimmte vertrauende Seite zu erhalten. Zuvor werden jedoch die Autorisierungsregeln ausgeführt, aus denen sich entweder der Ausstellungsautorisierungs-Regelsatz oder der Delegationsautorisierungs-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt.  
  
3.  Ausstellen von ausgehenden Ansprüchen: Diese Phase wird verwendet, um ausgehende Ansprüche auszustellen und entlang der Pipeline zu senden, wo sie in ein Sicherheitstoken gepackt werden. Zuvor werden jedoch die Ausstellungsregeln ausgeführt, aus denen sich der Ausstellungstransformations-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt. Diese bestimmen, welche Ansprüche als ausgehende Ansprüche ausgestellt werden.  
  
In allen drei oben aufgeführten Phasen werden Anspruchsregeln verarbeitet, jedoch jeweils anhand eines anderen Regelsatzes. Wie oben beschrieben, verfügt jede Stufe über einen zugeordneten Regelsatz, der entweder auf dem Aussteller der Eingeh \(enden Ansprüche die\) Akzeptanz Regeln oder den Ziel Dienst basiert, für die die claimincludes-Autorisierung ausgestellt \(wird. Ausstellungsregeln\).  
  
Ansprüche sind tokenagnostisch\-, werden jedoch in Sicherheits Token gekapselt über das Netzwerk übertragen. Die Anspruchsregeln werden unabhängig vom Format des eingehenden oder ausgehenden Sicherheitstokens auf Ansprüche angewendet.  
  
Anspruchs Regeln enthalten die vom\-Administrator definierte Logik, mit der die Anspruchs-Engine eingehende Ansprüche akzeptiert, Ansprüche basierend auf der Identität des Anforderers autorisieren und Ansprüche ausgeben kann, die von einer vertrauenden Seite benötigt werden. Letztlich wird durch das Anspruchsmodul bestimmt, welche Ansprüche in das Sicherheitstoken aufgenommen werden, das ausgestellt wird, nachdem der Anspruch die Anspruchspipeline durchlaufen hat.  
  
Wie in der folgenden Abbildung gezeigt, ist die Anspruchs Pipeline für den gesamten End\--to\--End-Prozess des Flusses eines Anspruchs über die verschiedenen Pipeline Stufen zuständig, um einen ausgestellten Anspruch zu erhalten, der über einen abhängigen Vertrauensstellung der Partei. Der ausgehende Anspruch in der Abbildung stellt den ausgestellten Anspruch dar.  
  
![Rollen AD FS](media/adfs2_pipeline.gif)  
  
Obgleich dies in der Abbildung nicht dargestellt ist, erfolgt die tatsächliche Verarbeitung der Regeln in den einzelnen Phasen durch das Anspruchsmodul. Weitere Informationen finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  

