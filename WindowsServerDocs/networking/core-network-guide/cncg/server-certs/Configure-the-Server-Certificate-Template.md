---
title: Konfigurieren der Serverzertifikatvorlage
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 8ff610e2-43ca-407f-a828-06d9366e02f0
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 35d5875c78dcd92f3b40b919568dabcf0d45d673
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356756"
---
# <a name="configure-the-server-certificate-template"></a>Konfigurieren der Serverzertifikatvorlage

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Mithilfe dieses Verfahrens können Sie die Zertifikat Vorlage konfigurieren, die Active Directory @ no__t-0-Zertifikat Dienste (AD CS) als Grundlage für Server Zertifikate verwendet, die bei Servern in Ihrem Netzwerk registriert sind.  
  
Beim Konfigurieren dieser Vorlage können Sie die Server Active Directory Gruppe angeben, die automatisch ein Serverzertifikat von AD CS erhalten soll.   
  
Das folgende Verfahren enthält Anweisungen zum Konfigurieren der Vorlage zum Ausstellen von Zertifikaten für alle der folgenden Server Typen:  
  
- Server, auf denen der RAS-Dienst ausgeführt wird, einschließlich der RAS-Gatewayserver, die Mitglieder der Gruppe " **RAS-und IAS-Server** " sind.  
- Server, auf denen der Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird, die Mitglieder der Gruppe " **RAS-und IAS-Server** " sind.  
  
Für dieses Verfahren sind mindestens die Mitgliedschaften in den Gruppen **Organisations-Admins** und **Domänen-Admins** der Stammdomäne erforderlich.  
  
### <a name="to-configure-the-certificate-template"></a>So konfigurieren Sie die Zertifikatvorlage  
  
1.  Klicken Sie auf CA1 in Server-Manager auf **Extras, und klicken Sie dann**auf **Zertifizierungs**Stelle. Die Microsoft Management Console (MMC) der Zertifizierungsstelle wird geöffnet.  
  
2.  Doppelklicken Sie in der MMC auf den Zertifizierungsstellen Namen, klicken Sie mit der rechten Maustaste auf **Zertifikat Vorlagen**, und klicken Sie dann auf **Verwalten**.  
  
3.  Die Konsole Zertifikat Vorlagen wird geöffnet. Alle Zertifikat Vorlagen werden im Bereich Details angezeigt.  
  
4.  Klicken Sie im Detailbereich auf die Vorlage **RAS-und IAS-Server** .  
  
5.  Klicken Sie auf das Menü **Aktion** , und klicken Sie dann auf **Doppelte Vorlage**. Das Dialogfeld Vorlagen **Eigenschaften** wird geöffnet.  
  
6.  Klicken Sie auf die Registerkarte **Sicherheit**.   
  
7.  Klicken Sie auf der Registerkarte **Sicherheit** unter **Gruppen-oder Benutzernamen**auf **RAS-und IAS-Server**.  
  
8.  Stellen Sie in **Berechtigungen für RAS-und IAS-Server**unter **zulassen**sicher, dass **registrieren** ausgewählt ist, und aktivieren Sie dann das Kontrollkästchen **Automatische** Registrierung. Klicken Sie auf **OK**, und schließen Sie die Zertifikat Vorlagen-MMC.  
  
9.  Klicken Sie in der MMC der Zertifizierungsstelle auf **Zertifikat Vorlagen**. Zeigen Sie im Menü **Aktion** auf **neu**, und klicken Sie dann auf Auszustellende **Zertifikat Vorlage**. Das Dialogfeld **Zertifikatvorlagen aktivieren** wird geöffnet.  
  
10. Klicken Sie in **Zertifikat Vorlagen aktivieren**auf den Namen der soeben konfigurierten Zertifikat Vorlage, und klicken Sie dann auf **OK**. Wenn Sie z. b. den Namen der Standard Zertifikat Vorlage nicht geändert haben, klicken Sie auf **Kopieren von RAS-und IAS-Server**, und klicken Sie dann auf **OK**.  
  


