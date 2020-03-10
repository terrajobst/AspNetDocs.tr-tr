---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Parolanın gücünü test etme (VB) | Microsoft Docs
author: wenz
description: Parolaların neredeyse her yerde olması gerekir; böylece yavaş kullanıcılar, kolayca kesintiye uğramaları kolay olan basit parolalar seçlidirler. ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627304"
---
# <a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="74228-104">Bir Parolanın Güçlülüğünü Test Etme (VB)</span><span class="sxs-lookup"><span data-stu-id="74228-104">Testing the Strength of a Password (VB)</span></span>

<span data-ttu-id="74228-105">[Hristia WENZ](https://github.com/wenz) tarafından</span><span class="sxs-lookup"><span data-stu-id="74228-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="74228-106">[Kodu indirin](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) veya [PDF 'yi indirin](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="74228-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="74228-107">Parolaların neredeyse her yerde olması gerekir; böylece yavaş kullanıcılar, kolayca kesintiye uğramaları kolay olan basit parolalar seçlidirler.</span><span class="sxs-lookup"><span data-stu-id="74228-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="74228-108">ASP.NET AJAX denetim araç setinde Passwordkuvveti denetimi bir parolanın ne kadar iyi olduğunu denetleyebilir.</span><span class="sxs-lookup"><span data-stu-id="74228-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="74228-109">Genel bakış</span><span class="sxs-lookup"><span data-stu-id="74228-109">Overview</span></span>

<span data-ttu-id="74228-110">Parolaların neredeyse her yerde olması gerekir; böylece yavaş kullanıcılar, kolayca kesintiye uğramaları kolay olan basit parolalar seçlidirler.</span><span class="sxs-lookup"><span data-stu-id="74228-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="74228-111">ASP.NET AJAX denetim araç setinde `PasswordStrength` denetimi bir parolanın ne kadar iyi olduğunu denetleyebilir.</span><span class="sxs-lookup"><span data-stu-id="74228-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="74228-112">Adımlar</span><span class="sxs-lookup"><span data-stu-id="74228-112">Steps</span></span>

<span data-ttu-id="74228-113">`PasswordStrength` denetimi bir metin kutusunu genişletir ve içindeki parolanın yeterince iyi olup olmadığını denetler.</span><span class="sxs-lookup"><span data-stu-id="74228-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="74228-114">Öznitelikler aracılığıyla çok sayıda seçenek sunar; Bunlardan bazıları şunlardır:</span><span class="sxs-lookup"><span data-stu-id="74228-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="74228-115">Parolada gereken en az sayısal karakter sayısı `MinimumNumericCharacters`</span><span class="sxs-lookup"><span data-stu-id="74228-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="74228-116">Parolada gereken en az sayıda simge karakteri (harf ve rakam değil) `MinimumSymbolCharacters`</span><span class="sxs-lookup"><span data-stu-id="74228-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="74228-117">en az parola uzunluğu `PreferredPasswordLength`</span><span class="sxs-lookup"><span data-stu-id="74228-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="74228-118">parolanın hem büyük hem de küçük harf karakter kullanması gerekip gerekmediğini `RequiresUpperAndLowerCaseCharacters`</span><span class="sxs-lookup"><span data-stu-id="74228-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="74228-119">`StrengthIndicatorType`, metin (değer `"Text"`) veya bir tür ilerleme çubuğu (değer `"BarIndicator"`) olarak parolanın gücünü sunma bilgilerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="74228-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="74228-120">`DisplayPosition` özniteliğinde, bilgilerin nerede göründüğünü yapılandırırsınız.</span><span class="sxs-lookup"><span data-stu-id="74228-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="74228-121">Burada, ASP.NET AJAX `ScriptManager` denetimi, `PasswordStrength` denetimi ve kurs, kullanıcının bir parola girebileceği bir metin kutusu gibi bir örnek verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="74228-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="74228-122">Tanıtım için ikinci form alanı, bir parola alanı değil normal metin alanıdır ve bu sayede, yazarken geliştirme sırasında bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="74228-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="74228-123">Sayfayı çalıştırın ve dışarıda yazın: yalnızca küçük harfler, büyük harfler, rakamlar ve semboller girdikten sonra parola ayırıcı olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="74228-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="74228-124">[parolayı artık (oldukça) iyi ![](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="74228-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="74228-125">Artık parola (oldukça) iyi ([tam boyutlu görüntüyü görüntülemek Için tıklatın](testing-the-strength-of-a-password-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="74228-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="74228-126">Öncekini</span><span class="sxs-lookup"><span data-stu-id="74228-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)
