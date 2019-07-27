---
title: Einschränken des Webzugriffs
description: Erfahren Sie, wie Sie den Benutzer Zugriff auf das Internet in Multipoint Services einschränken.
ms.custom: na
ms.date: 07/08/2016
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 044f2fd5-5b87-42bb-ba0d-c06516ac48c8
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: cb91914608110d26ff2db8eff1cd28d26d04669b
ms.sourcegitcommit: 9f955be34c641b58ae8b3000768caa46ad535d43
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/27/2019
ms.locfileid: "68590352"
---
# <a name="limit-web-access"></a>Einschränken des Webzugriffs
Zusätzlich zur Überwachung von Benutzeraktivitäten auf einzelnen Desktops können Sie als Administrator den Benutzer Zugriff auf bestimmte Websites einschränken, indem Sie zulässige Websites und Websites angeben, für die Sie den Benutzer Zugriff blockieren möchten.  
  
## <a name="to-limit-web-access-on-a-station"></a>So schränken Sie den Webzugriff auf einer Station ein  
  
1. Klicken Sie im Multipoint-Dashboard auf der Registerkarte **webbeschränkung** auf **Konfigurieren**. Die Seite **Webeinschränkung konfigurieren** wird geöffnet. Die Websites, auf die der Benutzer zugreifen kann, sind aufgelistet.  
  
2. Klicken Sie auf das Miniaturbild der Benutzerstation, auf der Sie den Webzugriff einschränken möchten.  
  
3. Klicken Sie unter **Ausgewählte Aufgaben für Elemente** auf **Webzugriff auf dieser Station einschränken**. Die Seite **Webeinschränkung konfigurieren** wird geöffnet. Die Websites, auf die der Benutzer zugreifen kann, sind aufgelistet.  
  
4. Geben Sie zum Hinzufügen einer zulässigen Website die Webadresse ein, und klicken Sie dann auf **Hinzuzufügen**.  
  
   > [!NOTE]
   > Wenn Sie z. b. "contoso.com" eingeben, werden Websites, die relativ\.zu www contoso.com sind (z\.. b. www NewPage.contoso.com), zugelassen oder blockiert. Durch die Eingabe von "Configuration Manager" werden alle standortbezogenen Websites (einschließlich contoso.com, contoso.uk usw.) entweder zugelassen oder beschränkt.  
  
5. Zum Entfernen einer Webadresse aus der Liste der zulässigen Websites klicken Sie auf die Webadresse, zu der Sie den Zugang entfernen möchten, und klicken Sie dann auf **Entfernen**.  
  
## <a name="to-limit-web-access-on-all-stations"></a>So schränken Sie den Webzugriff auf allen Stationen ein  
  
1. Klicken Sie im Multipoint-Dashboard auf der Registerkarte **webbegrenzung** auf das\-Dropdown Menü Start, und klicken Sie dann **auf Webzugriff auf allen Desktops begrenzen**.  
  
   Die Seite **Webeinschränkung konfigurieren** wird geöffnet. Die Websites, auf die der Benutzer zugreifen kann, sind aufgelistet. Führen Sie eines der folgenden Verfahren aus:  
  
2. Klicken Sie zum Hinzufügen einer zulässigen Website auf **Nur diese Websites zulassen**, geben Sie die Webadresse ein, und klicken Sie dann auf **Hinzufügen**.  
  
   Klicken Sie zum Hinzufügen einer Website, die die Benutzer nicht besuchen sollen, auf **Nur diese Websites nicht zulassen**, geben Sie die entsprechende Webadresse ein, und klicken Sie dann auf **Hinzufügen**.  
  
   > [!NOTE]
   > Wenn Sie z. b. "contoso.com" eingeben, können Sie Websites, die relativ zu www.contoso.com sind (z. b. www.NewPage.contoso.com), zulassen oder blockieren. Durch die Eingabe von "Configuration Manager" werden alle standortbezogenen Websites (einschließlich contoso.com, contoso.uk usw.) entweder zugelassen oder beschränkt.  
  
3. Zum Entfernen einer Webadresse aus der Liste der zulässigen oder nicht zulässigen Websites wählen Sie die Webadresse aus und klicken dann auf **Entfernen**.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Benutzer Desktops](manage-user-desktops-using-multipoint-dashboard.md)  
