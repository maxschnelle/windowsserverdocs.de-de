---
ms.assetid: 155abe09-6360-4913-8dd9-7392d71ea4e6
title: "Konfigurieren eines Computers für die Problembehandlung"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 915b8d1133b3bee050f5eedce9e7ac445f833048
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/12/2017
---
# <a name="configuring-a-computer-for-troubleshooting"></a>Konfigurieren eines Computers für die Problembehandlung

>Gilt für: Windows Server2016, Windows Server2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd">
  <introduction>
    <para>Erweiterte Problembehandlung zu identifizieren und beheben Sie Probleme bei der Active Directory verwenden, konfigurieren Sie Ihre Computer für die Problembehandlung. Sie sollten auch Grundkenntnisse verfügen <token>Nextref_longhorincludes > Problembehandlung Konzepte, Verfahren und Tools. </para>
    <para>Informationen zum Überwachen von Tools für Windows Server2008 finden Sie unter der Step-by-Step-Handbuch für die Leistungs- und Zuverlässigkeitsüberwachung in Windows Server2008 (<externalLink><linkText>https://go.microsoft.com/fwlink/?LinkId=123737</linkText><linkUri>https://go.microsoft.com/fwlink/?LinkId=123737</linkUri></externalLink>).</para>
  </introduction>
  <section>
    <title>Konfigurationsaufgaben für die Problembehandlung</title>
    <content>
      <para>Um den Computer für die Problembehandlung bei Active Directory-Domänendienste (AD DS) zu konfigurieren, führen Sie die folgenden Aufgaben:</para>
      <para>
        <link xlink:href="#BKMK_2">installieren Sie Remoteserver-Verwaltungstools für AD DS</link>
      </para>
      <para>
        <link xlink:href="#BKMK_3">konfigurieren Zuverlässigkeits- und Leistungsüberwachung</link>
      </para>
      <para>
        <link xlink:href="#BKMK_4">Protokolliergrad festlegen</link>
      </para>
    </content>
    <sections>
      <section address="BKMK_2">
        <title>Installieren Sie Remoteserver-Verwaltungstools für AD DS</title>
        <content>
          <para>Bei der Installation von AD DS auf einen Domänencontroller erstellen, werden die Verwaltungsprogramme, die Sie verwenden, um das Verwalten von AD DS automatisch installiert. Wenn Sie Domänencontroller remote von einem Computer verwalten, die nicht auf einem Domänencontroller ist möchten, können Sie die Verwaltung installieren, auf einem Mitgliedsserver, auf denen ausgeführt wird <token>Nextref_longhorincludes > oder auf einem Computer, auf denen Windows Vista mit Service Pack 1 (SP1) ausgeführt wird. Auf Mitgliedsservern, die ausgeführt werden <token>Nextref_longhorincludes >, Sie mithilfe der Remoteserver-Verwaltungstools (RSAT)-Funktion in Server-Manager, Active Directory Domain Services-Tools zu installieren. Remoteserver-Verwaltungstools ersetzt die Windows-Supporttools in Windows Server 2003. Sie können auch Active Directory Domain Services-Tools auf einem Computer mit Windows Vista mit Service Pack 1 (SP1) installieren, laden Sie die Tools auf dem Computer.</para>
          <para>Finden Sie Informationen zum Installieren der Remoteserver-Verwaltungstools, <link xlink:href="610ba7d9-51b5-4e14-9232-0510a9091aba">Installieren von Remoteserver-Verwaltungstools für AD DS</link>.</para>
        </content>
      </section>
      <section address="BKMK_3">
        <title>Konfigurieren der Zuverlässigkeits- und Leistungsüberwachung</title>
        <content>
          <para>Windows Server 2008 umfasst die Windows-Zuverlässigkeits- und Leistungsüberwachung, d. h. ein Microsoft Management Console (MMC)-Snap-in, das die Funktionen von vorherigen eigenständige Tools, z. B. Leistungsprotokolle und Warnungen, Server Performance Advisor und Systemmonitor kombiniert. Dieses Snap-In bietet eine grafische Benutzeroberfläche (GUI) zum Anpassen von Datensammlersätze und Ereignisablaufverfolgungssitzungen. </para>
          <para>Zuverlässigkeits- und Leistungsüberwachung enthält auch Zuverlässigkeitsüberwachung, ein MMC-Snap-in, die Änderungen am System verfolgt und vergleicht diese Änderungen in die Systemstabilität, deren Beziehung grafisch bereitstellen. </para>
        </content>
      </section>
      <section address="BKMK_4">
        <title>Legen Sie die Protokollierungsstufen</title>
        <content>
          <para>Wenn die Informationen, die Sie in das Verzeichnisdienst-Protokoll in der Ereignisanzeige erhalten für die Problembehandlung bei nicht ausreicht, erhöhen Sie die Protokollierungsstufen mit den entsprechenden Registrierungseintrag in <embeddedLabel>HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics</embeddedLabel>. </para>
          <para>Standardmäßig die Protokollierungsstufen für alle Einträge festgelegt <embeddedLabel>0</embeddedLabel>, das Mindestmaß an Informationen bereitstellt. Ist die höchste Protokollierungsstufe <embeddedLabel>5</embeddedLabel>. Für einen Eintrag im Klaren bewirkt, dass zusätzliche Ereignisse im Verzeichnisdienst-Ereignisprotokoll protokolliert werden. </para>
          <para>Können das folgende Verfahren ändern Sie die Protokollierungsstufe für eine Diagnose Eintrag. </para>
          <alert class="caution">
            <para>Es wird empfohlen, dass Sie nicht direkt die Registrierung bearbeiten, sofern es keine andere Alternative. Änderungen an der Registrierung werden durch den Registrierungs-Editor oder durch Windows nicht überprüft, bevor sie angewendet werden, daher können falsche Werte gespeichert werden. Dies kann nicht behebbaren Fehlern im System führen. Verwenden Sie nach Möglichkeit Gruppenrichtlinien oder anderen Windows-Tools, z. B. MMC-Snap-ins zum Ausführen von Aufgaben, anstatt die direkte Bearbeitung der Registrierung. Wenn Sie die Registrierung bearbeiten müssen, verwenden Sie äußerst vorsichtig vor. </para>
          </alert>
          <para>
            <embeddedLabel>Anforderungen</embeddedLabel>
          </para>
          <list class="bullet">
            <listItem>
              <para>Mitglied der Gruppe <embeddedLabel>Domänen-Admins</embeddedLabel>, oder einer gleichwertigen Gruppe ist mindestens erforderlich, um dieses Verfahren ausführen. <token>review_detailincludes></para>
            </listItem>
            <listItem>
              <para>Tools: Regedit.exe</para>
            </listItem>
          </list>
          <procedure>
            <title>So ändern Sie die Protokollierungsstufe für einen diagnostic</title>
            <steps class="ordered">
              <step>
                <content>
                  <para>Klicken Sie auf <ui>Starten</ui>, klicken Sie auf <ui>Ausführen</ui>, typ <userInput>regedit</userInput>, und klicken Sie dann auf <ui>OK</ui>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Navigieren Sie zu den Eintrag für die Protokollierung sollen <embeddedLabel>HKEY_LOCAL_MACHINESYSTEMCurrentControlSetServicesNTDSDiagnostics</embeddedLabel>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>Doppelklicken Sie auf den Eintrag im <embeddedLabel>Base</embeddedLabel>, klicken Sie auf <embeddedLabel>Dezimal</embeddedLabel>.</para>
                </content>
              </step>
              <step>
                <content>
                  <para>In <embeddedLabel>Wert</embeddedLabel>, geben Sie eine ganze Zahl zwischen <embeddedLabel>0</embeddedLabel> über <embeddedLabel>5</embeddedLabel>, und klicken Sie dann auf <ui>OK</ui>.</para>
                </content>
              </step>
            </steps>
          </procedure>
        </content>
      </section>
    </sections>
  </section>
  <relatedTopics />
</developerConceptualDocument>


