---
ms.assetid: 4ae26970-e42e-4e69-887a-b16d2f8d0695
title: Konfigurieren Sie Clientcomputer dem Kontoverbundserver vertrauen
description: 
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: bdfb086c8177e72c074ac5b5b1a38aac49c4082c
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configure-client-computers-to-trust-the-account-federation-server"></a>Konfigurieren Sie Clientcomputer dem Kontoverbundserver vertrauen

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012

So, dass Clientcomputer erfolgreich mit Active Directory Federation Services \(AD FS\) verbundanwendungen zugreifen können, müssen Sie die Internet Explorer-Einstellungen, damit der Browser der Kontoverbundserver Vertrauensstellungen zunächst auf jedem Clientcomputer konfigurieren. Sie hierzu manuell oder über Gruppenrichtlinien, je nach Wunsch administrative eines der folgenden Verfahren abschließen.  
  
## <a name="configuring-internet-explorer-settings-manually"></a>Konfigurieren von Internet Explorer-Einstellungen manuell  
Das folgende Verfahren können jeden Benutzer Internet Explorer-Einstellungen zur Unterstützung von Verbundservern über AD FS manuell zu konfigurieren. Wenn mehrere Benutzer auf einen einzelnen Computer verwenden, führen Sie dieses Verfahren mehrmals – einmal für jedes Benutzerprofil.  
  
Melden Sie sich zum Ausführen dieses Verfahrens wie der Benutzer, der auf verbundanwendungen zugreifen. Dies ist eine Profile\-spezifischen Einstellung. Aus diesem Grund müssen Sie diese Einstellung wird für jedes Profil vorhanden ist, die auf einem bestimmten Computer manuell hinzufügen.  
  
#### <a name="to-manually-configure-client-computers-to-trust-the-account-federation-server"></a>So konfigurieren Sie Clientcomputer dem Kontoverbundserver vertrauen manuell  
  
1.  Starten Sie Internet Explorer auf dem Clientcomputer.  
  
2.  Auf der **Tools** Menü klicken Sie auf **Internetoptionen**.  
  
3.  Auf der **Security** auf die **lokales Intranet** Symbol, und klicken Sie dann auf **Sites**.  
  
4.  Klicken Sie auf **erweitert**, und im **diese Website zur Zone hinzufügen**, geben Sie den vollständigen Namen der Domain Name System \(DNS\) von der Kontoverbundserver \ (z. B. https:\/\/fs1.fabrikam.com\), und klicken Sie dann auf **hinzufügen**.  
  
5.  Klicken Sie auf **OK** drei Mal.  
  
## <a name="configuring-internet-explorer-settings-by-using-group-policy"></a>Konfigurieren von Internet Explorer-Einstellungen mithilfe von Gruppenrichtlinien  
Für die meisten Bereitstellungen wird empfohlen, dass Sie eine Gruppenrichtlinie verwenden, um die entsprechenden Einstellungen von Internet Explorer per push auf jedem Client-Computer.  
  
Mitgliedschaft in **Domänen-Admins** oder **Organisations-Admins**, oder entsprechende Berechtigungen in Active Directory-Domänendiensten \(AD DS\) mindestens erforderlich, um dieses Verfahren ausführen.  Weitere Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften unter [lokale und Domänenstandardgruppen](https://go.microsoft.com/fwlink/?LinkId=83477) \ (http:///\/ go.microsoft.com\/Fwlink\ /? LinkId\ = 83477\).   
  
#### <a name="to-configure-client-computers-to-trust-the-account-federation-server-by-using-group-policy"></a>So konfigurieren Sie Clientcomputer dem Kontoverbundserver vertrauen mithilfe von Gruppenrichtlinien  
  
1.  Starten Sie auf einem Domänencontroller in der Gesamtstruktur des der Kontopartnerorganisation der **Gruppenrichtlinienverwaltung** Snap-in.  
  
2.  Suchen Sie das entsprechende Gruppenrichtlinienobjekt \(GPO\), klicken Sie auf, und klicken Sie dann auf **bearbeiten**.  
  
3.  Öffnen Sie in der Konsolenstruktur **Benutzer einstellungen\\dateien Settings\\Internet Explorer-Wartung**, und klicken Sie dann auf **Security**.  
  
4.  Klicken Sie im Detailbereich doppelten Mausklick **Sicherheitszonen und Inhaltsfilter**.  
  
5.  Unter **Sicherheitszonen und Datenschutz**, klicken Sie auf **Importieren der aktuellen Sicherheitszonen und Datenschutz**, und klicken Sie dann auf **Sammlungseinstellungen**.  
  
6.  Klicken Sie auf **lokales Intranet**, und klicken Sie dann auf **Sites**.  
  
7.  In **diese Website zur Zone hinzufügen**, geben Sie den vollständigen DNS-Namen des kontoverbundservers \ (z. B. https:\/\/fs1.fabrikam.com\), klicken Sie auf **hinzufügen**, und klicken Sie dann auf **schließen**.  
  
8.  Klicken Sie auf **OK** zweimal, um diese Änderungen auf der Gruppenrichtlinie anzuwenden.  
  
