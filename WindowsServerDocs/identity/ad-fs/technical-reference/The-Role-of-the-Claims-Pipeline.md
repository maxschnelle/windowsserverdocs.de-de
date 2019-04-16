---
ms.assetid: ffb9d63c-ba7c-4ad1-b814-6db67f98c943
title: Die Rolle der Anspruchspipeline
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 5076a686b5d0b9a539f6cad8594aaf84dccc3edb
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2017
---
>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

# <a name="the-role-of-the-claims-pipeline"></a>Die Rolle der Anspruchspipeline
Die anspruchspipeline in Active Directory Federation Services \(AD FS\) stellt den Pfad, den Ansprüche innerhalb des Verbunddiensts durchlaufen müssen, bevor sie ausgestellt werden können. Der Verbunddienst verwaltet den gesamten zur Implementierung-zu-Ende-Prozess des anspruchsverlaufs in den verschiedenen Phasen der anspruchspipeline, darunter auch die Verarbeitung von Anspruchsregeln durch das anspruchsregelmodul.  
  
Weitere Informationen zu Anspruchsregeln finden Sie unter [der Rolle der Anspruchsregeln](The-Role-of-Claim-Rules.md). Weitere Informationen zur Verarbeitung von Regeln durch des anspruchsregelmodul finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  
Im folgenden Abschnittwird den Prozess, den den Verbunddienst genauer überwacht.  
  
## <a name="claims-pipeline-process"></a>Anspruchspipelineprozess  
Der anspruchspipelineprozess besteht aus drei allgemeine Phasen. Jede Phase in diesem Prozess initialisiert das anspruchsregelmodul Anspruchsregeln zu verarbeiten, die für diese Phase spezifisch sind. Diese Phasen umfassen \ (in der Reihenfolge, dass Occur\):  
  
1.  Akzeptieren von eingehenden Ansprüchen: Diese Phase der anspruchspipeline wird verwendet, um die eingehenden Ansprüche aus dem Token zu extrahieren und beseitigen Ansprüche, die nicht erwartete oder nicht vertrauenswürdig sind. Nach dem Extrahieren werden festgelegt, aus denen die Annahme transformationsregel, akzeptanzregeln für eine Anspruchsanbieter-Vertrauensstellung ausgeführt werden. Diese Regeln können verwendet werden, um Ansprüche weiterzuleiten oder Hinzufügen neuer Ansprüche, die dann in den nachfolgenden Phasen der anspruchspipeline verwendet werden können. Die Ausgabe dieser Phase wird als Eingabe für die zweite und dritte Phase verwendet.  
  
2.  Autorisieren des anspruchsanforderers: Diese Phase wird vom anspruchsmodul verwendet, um Zulassungs- oder verweigerungsansprüche auf, ob der anforderer des Tokens zum Abrufen eines Token für eine bestimmte vertrauende oder nicht zulässig ist. Aber damit dies durchgeführt werden kann, legen Sie die Autorisierungsregeln, die entweder der ausstellungsautorisierungs-Regelsatz bilden oder der delegationsautorisierungs-Regelsatz für eine Vertrauensstellung der vertrauenden Seite ausgeführt.  
  
3.  Ausstellen von ausgehenden Ansprüchen: Diese Phase wird verwendet, um ausgehende Ansprüche auszustellen und senden Sie sie an die Pipeline, werden sie in ein Sicherheitstoken gepackt werden. Allerdings zuvor die von ausstellungsregeln, die sich der ausstellungstransformations-Regelsatz für eine Vertrauensstellung der vertrauenden Seite zusammensetzt ausgeführt werden, bestimmen, welche Ansprüche als ausgehende Ansprüche ausgegeben werden.  
  
Alle drei oben aufgeführten Phasen Anspruchsregeln verarbeitet, jedoch einen anderen Satz von Regeln. Wie oben beschrieben, hat jeder Phase einen verknüpften Satz von Regeln auf Grundlage der entweder auf dem Aussteller der eingehenden Ansprüche \(the acceptance rules\) oder den Zieldienst für die die Claimincludes ausgestellt werden \ (Rules\ Autorisierungs- und ausstellungsregeln).  
  
Ansprüche Token\ agnostisch sind jedoch in Sicherheitstoken gekapselt über das Netzwerk übertragen werden. Die Anspruchsregeln, die über Ansprüche unabhängig vom Format des eingehenden oder ausgehenden Sicherheitstokens betrieben werden.  
  
Ansprüche, dass die Regeln für die Administrator\ definierte Logik enthalten, mit der das anspruchsmodul werden die eingehenden Ansprüche akzeptiert, Ansprüche basierend auf der Identität des anforderers autorisiert und Ansprüche ausstellt, die, werden durch eine vertrauende Seite benötigt. Letztlich wird das anspruchsmodul bestimmt, welche Ansprüche in das Sicherheitstoken aufgenommen werden, das ausgestellt wird, nachdem der Anspruch in der anspruchspipeline durchlaufen hat.  
  
Wie in der folgenden Abbildunggezeigt, ist die anspruchspipeline verantwortlich für den gesamten zur Implementierung-zu-Ende-Prozess an einen Anspruch in den verschiedenen Pipelinephasen zur Ausstellung Beendigung, die über eine Vertrauensstellung der vertrauenden Seite gesendet wird. Der ausgehende Anspruch in der Abbildungstellt den ausgestellten Anspruch dar.  
  
![AD FS-Rollen](media/adfs2_pipeline.gif)  
  
Obwohl es in der Abbildungnicht dargestellt wird, wird das anspruchsmodul, das die tatsächliche Verarbeitung der Regeln in jeder Phase führt. Weitere Informationen finden Sie unter [The Role of the Claims Engine](The-Role-of-the-Claims-Engine.md).  
  

