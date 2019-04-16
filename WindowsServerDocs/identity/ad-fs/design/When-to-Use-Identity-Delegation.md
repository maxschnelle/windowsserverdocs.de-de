---
ms.assetid: 6e711a96-9055-4508-b6d4-318d6aa95fd1
title: "Wenn für Identitätsdelegierung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: af227d9e87ddb73f194dd46c8ce45fcdf12a34cf
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="when-to-use-identity-delegation"></a>Wenn für Identitätsdelegierung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012
  
## <a name="what-is-identity-delegation"></a>Was ist identitätsdelegierung?  
Identitätsdelegierung ist ein Feature von Active Directory Federation Services \(AD FS\), die Administrator\ angegebenen Konten Benutzern annehmen können. Das Konto, das die Identität des Benutzers wird aufgerufen, die *Delegieren*. Diese delegierungsmöglichkeit ist für viele verteilte Anwendungen, die für die es gibt eine Reihe von Access Steuerelement überprüft, die ob der nacheinander für jede Anwendung, die Datenbank oder den Dienst in der autorisierungskette für die ursprüngliche Anforderung vorgenommen werden müssen. Viele Praxis Szenarien vorhanden sein muss, in denen eine "front-End"-Webanwendung Daten von einem sicherer "Back-End", z.B. einen Webdienst, der mit einer Microsoft SQL Server-Datenbank verbunden ist abrufen.  
  
Beispielsweise kann eine vorhandene Website Parts\-Anordnung programmgesteuert erweitert werden, so, dass Partner Organisationen ihre eigenen Käufe Verlauf und den Kontostatus einsehen können. Aus Sicherheitsgründen werden alle Finanzdaten der Partner in einer sicheren Datenbank auf einem dedizierten Structured Query Language \(SQL\) Server gespeichert. In diesem Fall hat der Programmcode in der Front\-End-Anwendung keinerlei wissen über die Finanzdaten der Partnerorganisation. Daher müssen sie die Daten abrufen, von einem anderen Computer im Netzwerk, auf dem gehostet \ (in diesem wird) der Webdienst für die Teiledatenbank \(the back end\).  
  
Für diesen Prozess Systemstatusdaten\ Abruf erfolgreich ausgeführt werden kann eine Abfolge von Autorisierungs-, "Hand\ Schütteln" ausführen muss, platzieren Sie zwischen der Anwendung und der Webdienst für die Teiledatenbank wie in der folgenden Abbildungdargestellt.  
  
![identitätsdelegierung](media/adfs2_identitydelegationconcept.gif)  
  
Da die ursprüngliche Anforderung an den Webserver selbst, das in einem ganz anderen Organisation des Benutzers befinden, der versucht vorgenommen wurde, den Web-Server zugreifen, erfüllt das Sicherheitstoken, das zusammen mit der Anforderung gesendet wird nicht den Autorisierungskriterien, die zum Zugreifen auf einem anderen Computer als den Webserver erforderlich. Daher ist die einzige Möglichkeit, dass die ursprüngliche des Benutzers Anforderung durch das Platzieren eines zwischengeschalteten Verbundservers in der Ressourcenpartnerorganisation zur Unterstützung der zugreifenden ein Sicherheitstoken, die über die entsprechenden Zugriffsrechte verfügt.  
  
## <a name="how-does-identity-delegation-work"></a>Wie funktioniert die identitätsdelegierung?  
Web-Apps Anwendungsarchitektur rufen oft Webdienste gemeinsam genutzte Daten und Funktionen für den Zugriff auf. Es ist wichtig für diese Webdienste, die Identität des ursprünglichen Benutzers kennen, damit der Dienst Autorisierungsentscheidungen treffen kann, und eine Überwachung ermöglicht. In diesem Fall stellt die Front\-End-Webanwendung den Benutzer an den Webdienst als Delegat. AD FS ermöglicht dieses Szenario in eigener Regie Active Directory-Konten als ein Benutzer einer vertrauenden fungieren. Ein Szenario mit identitätsdelegierung dar, ist in der folgenden Abbildungdargestellt.  
  
![identitätsdelegierung](media/adfs2_identitydelegationsteps.gif)  
  
1.  Frank versucht, eine Webanwendung in einer anderen Organisation Part\-Anordnung Verlauf zugreifen. Sein Clientcomputer fordert und erhält ein Token von AD FS für die Front\-End-Webanwendung Part\-Anordnung.  
  
2.  Der Clientcomputer sendet eine Anforderung an die Web-Anwendung, einschließlich des in Schritt1, um die Identität des Clients zu beweisen erhaltenen Tokens.  
  
3.  Die Web-Anwendung muss für die Kommunikation mit dem Webdienst zum Abschließen einer Transaktions für den Client. Die Web-Anwendung eine Verbindung mit AD FS, um ein delegierungstoken für die Interaktion mit dem Webdienst zu erhalten. Delegierungstoken sind Sicherheitstoken, die auf einen Delegaten fungieren als Benutzer ausgestellt werden. AD FS gibt ein delegierungstoken mit Ansprüchen bezüglich des Clients, die für den Webdienst vorgesehen.  
  
4.  Die Webanwendung verwendet das Token, das abgerufen wurde, von AD FS in Schritt3, um Zugriff auf den Webdienst, der als Client auftritt. Durch Untersuchen des delegierungstokens, kann der Webdienst erkennen, dass die Anwendung als Client fungiert. Der Webdienst führt seine Autorisierungsrichtlinie protokolliert die Anforderung und gibt die Verlaufsdaten, die ursprünglich von Frank, auf die Webanwendung angefordert wurde und somit an Frank aus.  
  
Für Delegaten können AD FS die Webdienste einschränken, für die die Anwendung ein delegierungstoken anfordern kann. Der Clientcomputer hat keinen Active Directory-Konto für diesen Vorgang verfügen. Schließlich kann wie bereits erwähnt, der Webdienst problemlos die Identität des Delegaten ermitteln, der als der Benutzer fungiert. Dadurch können Webdienste unterschiedliches Verhalten abhängig, ob sie direkt an den Clientcomputer oder über einen Delegaten kommunizieren zeigen.  
  
## <a name="configuring-ad-fs-for-identity-delegation"></a>Konfigurieren von AD FS für die identitätsdelegierung  
Sie können AD FS-Verwaltungs-Snap-In AD FS für die identitätsdelegierung konfigurieren, wenn Sie den datenabrufprozess vereinfachen möchten. Nach der Konfiguration, können AD FS generieren neue Sicherheitstoken, die den Autorisierungskontext enthalten, die der Back\-End-Dienst möglicherweise erforderlich sind, bevor sie den Zugriff für die geschützten Daten ermöglichen kann.  
  
AD FS schränkt nicht ein, welche Benutzeridentitäten angenommen werden können. Nachdem Sie AD FS für die identitätsdelegierung konfigurieren, geschieht Folgendes:  
  
-   Es bestimmt, welche Server delegiert werden können die Berechtigung Token anzufordern, einen Benutzer zu imitieren.  
  
-   Es festgelegt und separat beide Identität Kontext für das Clientkonto, das delegiert wird und der Server, der als Delegat fungiert.  
  
Sie können die identitätsdelegierung konfigurieren, durch Hinzufügen von Autorisierungsregeln zu einer Vertrauensstellung der vertrauenden Seite in AD FS-Verwaltungs-Snap-In. Weitere Informationen hierzu finden Sie unter [Prüfliste: Erstellen von Anspruchsregeln für eine der vertrauenden Seite Vertrauensstellung](../../ad-fs/deployment/Checklist--Creating-Claim-Rules-for-a-Relying-Party-Trust.md).  
  
## <a name="configuring-the-front-end-web-application-for-identity-delegation"></a>Konfigurieren der Front\-End-Web-Anwendung für die identitätsdelegierung  
Entwickler haben mehrere Optionen, die sie verwenden können, die Web Front\-End-Anwendung oder ein Dienst zum Umleiten von Delegierungsanfragen an einen AD FS-Computer entsprechend zu programmieren. Weitere Informationen zum Anpassen von Web-Apps auf die identitätsdelegierung finden Sie unter der [Windows Identity Foundation SDK](https://go.microsoft.com/fwlink/?LinkId=122266).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
