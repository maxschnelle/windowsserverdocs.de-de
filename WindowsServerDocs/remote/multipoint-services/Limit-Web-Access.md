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
ms.openlocfilehash: 9f3524261e8e93439ff48a3e6666fa7680a76a29
ms.sourcegitcommit: ccec91c1d32a978159f9b8bb5e39ead5805c26c4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/19/2019
ms.locfileid: "71143737"
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
  
   Wenn Sie eine Website hinzufügen möchten, die nicht von Benutzern besucht werden soll, klicken Sie auf **nur diese Websites zulassen**, geben Sie die Webadresse ein, die Sie nicht besuchen möchten, und klicken Sie dann auf **Hinzufügen**.  
  
   > [!NOTE]
   > Wenn Sie z. b. "contoso.com" eingeben, können Sie Websites, die relativ zu www.contoso.com sind (\.z. b. www NewPage.contoso.com), zulassen oder blockieren. Durch die Eingabe von "Configuration Manager" werden alle standortbezogenen Websites (einschließlich contoso.com, contoso.uk usw.) entweder zugelassen oder beschränkt.  
  
3. Zum Entfernen einer Webadresse aus der Liste der zulässigen oder nicht zulässigen Websites wählen Sie die Webadresse aus und klicken dann auf **Entfernen**.  
  
## <a name="see-also"></a>Siehe auch  
[Verwalten von Benutzer Desktops](manage-user-desktops-using-multipoint-dashboard.md)  
