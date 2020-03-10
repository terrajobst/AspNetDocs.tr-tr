---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
title: Hizmet katmanı ile doğrulama (VB) | Microsoft Docs
author: StephenWalther
description: Doğrulama mantığınızı denetleyici eylemlerinizin dışında ve ayrı bir hizmet katmanında nasıl taşıyacağınızı öğrenin. Bu öğreticide, Stephen Walther nasıl yapılacağını açıklar...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 344bb38e-4965-4c47-bda1-f6d29ae5b83a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 704657ffe6f50eaf3eb0d91d0d334567003ab7f4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542828"
---
# <a name="validating-with-a-service-layer-vb"></a>Hizmet Katmanı ile Doğrulama (VB)

ile [Stephen Walther](https://github.com/StephenWalther)

> Doğrulama mantığınızı denetleyici eylemlerinizin dışında ve ayrı bir hizmet katmanında nasıl taşıyacağınızı öğrenin. Bu öğreticide, Stephen Walther, hizmet katmanınızı denetleyici katmanınızdan yalıtarak sorunları nasıl keskin bir şekilde koruyabileceğinizi açıklar.

Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirme yöntemini açıklıyor. Bu öğreticide, doğrulama mantığınızı denetleyicilerden ve ayrı bir hizmet katmanına taşımayı öğreneceksiniz.

## <a name="separating-concerns"></a>Kaygıları ayırma

Bir ASP.NET MVC uygulaması oluşturduğunuzda, veritabanı mantığınızı denetleyici eylemlerinizin içine yerleştirmemelisiniz. Veritabanınızı ve denetleyici mantığınızı karıştırmak, uygulamanızın zaman içinde bakımını daha zor hale getirir. Öneri, tüm veritabanı mantığınızı ayrı bir depo katmanında yerleştirmesidir.

Örneğin, Listeleme 1, ProductRepository adlı basit bir depo içerir. Ürün deposu, uygulamanın tüm veri erişim kodunu içerir. Liste ayrıca, ürün deposunun uyguladığı ıproductrepository arabirimini de içerir.

**Listeleme 1-Models\productdepotory.exe**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample1.vb)]

Listeleme 2 ' deki denetleyici, dizin () ve Create () eylemleri içinde depo katmanını kullanır. Bu denetleyicinin herhangi bir veritabanı mantığı içermediğini unutmayın. Bir depo katmanı oluşturmak, kaygılara yönelik temiz ayrımı korumanıza olanak sağlar. Denetleyiciler, uygulama akış denetim mantığından sorumludur ve veri erişim mantığıyla depo sorumludur.

**Listeleme 2-Controllers\productcontroller.exe**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample2.vb)]

## <a name="creating-a-service-layer"></a>Hizmet katmanı oluşturma

Bu nedenle, uygulama akış denetim mantığı bir denetleyiciye aittir ve veri erişim mantığı bir depoya aittir. Bu durumda, doğrulama mantığınızı nereye yerleştirmeniz gerekir? Bir seçenek, doğrulama mantığınızı bir *hizmet katmanına*yerleştirmadır.

Bir hizmet katmanı, bir ASP.NET MVC uygulamasındaki bir denetleyici ve depo katmanı arasındaki iletişimi destekleyen ek bir katmandır. Hizmet katmanı iş mantığını içerir. Özellikle, doğrulama mantığını içerir.

Örneğin, kod 3 ' teki ürün hizmeti katmanının bir CreateProduct () yöntemi vardır. CreateProduct () yöntemi, ürünü ürün deposuna geçirmeden önce yeni bir ürünü doğrulamak için ValidateProduct () yöntemini çağırır.

**Listeleme 3-Models\productservice.exe**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample3.vb)]

Ürün denetleyicisi, kod 4 ' te depo katmanı yerine hizmet katmanını kullanmak üzere güncelleştirilmiştir. Denetleyici katmanı hizmet katmanıyla oynanır. Hizmet katmanı, depo katmanıyla konuşur. Her katmanın ayrı bir sorumluluğu vardır.

**Listeleme 4-Controllers\productcontroller.exe**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample4.vb)]

Ürün hizmeti 'nin ürün denetleyicisi oluşturucusunda oluşturulmuş olduğuna dikkat edin. Ürün hizmeti oluşturulduğunda, model durum sözlüğü hizmete geçirilir. Ürün hizmeti, doğrulama hata iletilerini denetleyiciye geri geçirmek için model durumunu kullanır.

## <a name="decoupling-the-service-layer"></a>Hizmet katmanını bağlama

Denetleyiciyi ve hizmet katmanlarını tek bir şekilde yalıtamadı. Denetleyici ve hizmet katmanları, model durumu üzerinden iletişim kurar. Diğer bir deyişle, hizmet katmanının, ASP.NET MVC çerçevesinin belirli bir özelliğine bağımlılığı vardır.

Hizmet katmanını denetleyici katmanımız kadar mümkün olduğunca yalıtmak istiyoruz. Teorik olarak, hizmet katmanını yalnızca bir ASP.NET MVC uygulaması değil, herhangi bir uygulama türüyle kullanabilmelidir. Örneğin, gelecekte uygulamamız için bir WPF ön ucu oluşturmak isteyebilirsiniz. ASP.NET MVC modeli durumundaki bağımlılığı hizmet katmanımızdan kaldırmanın bir yolunu bulduk.

5\. listede, hizmet katmanı artık model durumunu kullanmamasını sağlayacak şekilde güncelleştirilmiştir. Bunun yerine, ıvalidationdictionary arabirimini uygulayan herhangi bir sınıfı kullanır.

**Listeleme 5-Models\productservice,vb (ayrılmış)**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample5.vb)]

Ivalidationdictionary arabirimi, liste 6 ' da tanımlanmıştır. Bu basit arabirim tek bir yönteme ve tek bir özelliğe sahiptir.

**Listeleme 6-Models\IValidationDictionary.cs**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample6.vb)]

ModelStateWrapper sınıfı adlı Listeleme 7 ' deki sınıf ıvalidationdictionary arabirimini uygular. Bir model durum sözlüğünü oluşturucuya geçirerek ModelStateWrapper sınıfının örneğini oluşturabilirsiniz.

**Listeleme 7-Models\ModelStateWrapper.vb**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample7.vb)]

Son olarak, liste 8 ' deki güncelleştirilmiş denetleyici, Oluşturucu içinde hizmet katmanını oluştururken ModelStateWrapper kullanır.

**8-Controllers\productcontroller.exe listeleme**

[!code-vb[Main](validating-with-a-service-layer-vb/samples/sample8.vb)]

Ivalidationdictionary arabirimini ve ModelStateWrapper sınıfını kullanmak, hizmet katmanımızı denetleyici katmanımızdan tamamen yalıtmamızı sağlar. Hizmet katmanı artık model durumuna bağlı değil. Ivalidationdictionary arabirimini uygulayan herhangi bir sınıfı hizmet katmanına geçirebilirsiniz. Örneğin, bir WPF uygulaması, bir basit koleksiyon sınıfıyla ıvalidationdictionary arabirimini uygulayabilir.

## <a name="summary"></a>Özet

Bu öğreticinin amacı, bir ASP.NET MVC uygulamasında doğrulama gerçekleştirmeye yönelik bir yaklaşımı tartışmaktır. Bu öğreticide, tüm doğrulama mantığınızı denetleyicilerden ve ayrı bir hizmet katmanına nasıl taşıyabileceğinizi öğrendiniz. Ayrıca, bir Modelstatesarmalayıcı sınıfı oluşturarak hizmet katmanınızı denetleyici katmanınızdan yalıtmak için de öğrenirsiniz.

> [!div class="step-by-step"]
> [Önceki](validating-with-the-idataerrorinfo-interface-vb.md)
> [İleri](validation-with-the-data-annotation-validators-vb.md)
