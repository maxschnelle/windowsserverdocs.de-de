---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: Konfigurieren von Clientcomputern zum Vertrauen der Kontoverbundserver
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdfb086c8177e72c074ac5b5b1a38aac49c4082c
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886751"
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>Konfigurieren von Clientcomputern zum Vertrauen der Kontoverbundserver

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

So, dass Clientcomputer erfolgreich mithilfe von Active Directory Federation Services verbundanwendungen zugreifen können \(AD FS\), Sie müssen zuerst die Internet Explorer-Einstellungen auf jedem Clientcomputer konfigurieren, sodass der Browser vertraut der Kontoverbundserver. Sie können manuell oder über Gruppenrichtlinien, je nach Bedarf administrative, dazu eines der folgenden Verfahren ausführen.  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Konfigurieren von Internet Explorer-Einstellungen manuell  
Sie können das folgende Verfahren verwenden, jedes Benutzers Internet Explorer-Einstellungen zur Unterstützung von Verbund über AD FS manuell zu konfigurieren. Wenn mehrere Benutzer einen einzelnen Computer verwenden, führen Sie dieses Verfahren mehrmals – einmal für jedes Benutzerprofil.  
  
Um dieses Verfahren auszuführen, melden Sie sich, wie der Benutzer, der auf verbundanwendungen zugreifen werden. Dies ist ein Profil\-Einstellung. Daher erfordert sie, dass Sie diese Einstellung für die einzelnen Profile, die vorhanden ist auf einem bestimmten Computer manuell hinzufügen.  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>So konfigurieren Sie Clientcomputer zum Vertrauen der Kontoverbundserver manuell  
  
1.  Starten Sie Internet Explorer, auf dem Clientcomputer.  
  
2.  Auf der **Tools** Menü klicken Sie auf **Internetoptionen**.  
  
3.  Auf der **Sicherheit** Registerkarte, klicken Sie auf die **lokales Intranet** Symbol, und klicken Sie dann auf **Websites**.  
  
4.  Klicken Sie auf **erweitert**, und klicken Sie in **diese Website zur Zone hinzufügen**, geben Sie das vollständige Domain Name System \(DNS\) Name des der Kontoverbundserver \(z. B. Https :\/\/fs1.fabrikam.com\), und klicken Sie dann auf **hinzufügen**.  
  
5.  Klicken Sie dreimal auf **OK**.  
  
## <a name="configuring-internet-explorer-settings-by-using-grouppolicy"></a>Konfigurieren von Internet Explorer-Einstellungen mithilfe der Gruppenrichtlinie  
Für die meisten Bereitstellungen empfehlen wir, dass Sie Gruppenrichtlinien verwenden, um die entsprechenden Einstellungen für Internet Explorer auf jedem Clientcomputer übertragen.  
  
Mitgliedschaft in **Domänen-Admins** oder **Organisations-Admins**, oder äquivalent, in Active Directory Domain Services \(AD DS\) ist die mindestvoraussetzung, um dieses Verfahren abzuschließen.  Weitere Informationen zur Verwendung der geeigneten Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \(http:\/\/"go.Microsoft.com"\/Fwlink\/? LinkId\=83477\).   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-grouppolicy"></a>Zum Konfigurieren von Clientcomputern für die der Kontoverbundserver Vertrauensstellung mithilfe einer Gruppenrichtlinie  
  
1.  Starten Sie auf einem Domänencontroller in der Gesamtstruktur des der Kontopartnerorganisation der **Gruppenrichtlinienverwaltung** ausrichten\-in.  
  
2.  Suchen Sie das entsprechende Gruppenrichtlinienobjekt \(GPO\)mit der rechten Maustaste\-klicken Sie darauf, und klicken Sie dann auf **bearbeiten**.  
  
3.  Öffnen Sie in der Konsolenstruktur **Benutzerkonfiguration\\Voreinstellungen\\Windows-Einstellungen\\Internet Explorer-Wartung**, und klicken Sie dann auf **Sicherheit**.  
  
4.  Doppelklicken Sie im Detailbereich,\-klicken Sie auf **Sicherheitszonen und Inhaltsfilter**.  
  
5.  Klicken Sie unter **Sicherheitszonen und Datenschutz**, klicken Sie auf **importieren Sie die aktuellen Sicherheitszonen und datenschutzeinstellungen**, und klicken Sie dann auf **Einstellungen ändern**.  
  
6.  Klicken Sie auf **lokales Intranet**, und klicken Sie dann auf **Websites**.  
  
7.  In **diese Website zur Zone hinzufügen**, geben Sie den vollständigen DNS-Namen der Kontoverbundserver \(z. B. Https:\/\/fs1.fabrikam.com\), klicken Sie auf **hinzufügen**, und klicken Sie dann auf **schließen**.  
  
8.  Klicken Sie auf **OK** doppelt so groß wie diese Änderungen an der Gruppenrichtlinie angewendet.  
  
