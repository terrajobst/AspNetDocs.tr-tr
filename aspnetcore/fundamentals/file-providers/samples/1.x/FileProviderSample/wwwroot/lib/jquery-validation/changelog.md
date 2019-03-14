---
ms.openlocfilehash: b97b3f95a1ecd1e5802794043f848bda83a2f966
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070467"
---
<a name="1160--2016-12-01"></a>1.16.0 / 2016-12-01
==================

## <a name="additional"></a>Ek
  * CifES ve nieES algoritmaları daraltın. #1826 kapatır

## <a name="build"></a>Yapı
  * Küçültülmüş sürüm NPM pakete Ekle
  * En yeni sürümlerine geliştirme bağımlılıkları kabartma

## <a name="core"></a>Çekirdek
  * Düğme türü ile giriş bağlaması ekleyin. #1891 kapatır
  * Jquery3 destekler. #1866 kapatır
  * Değişiklik jQuery diğer adı ' ifade [":"]' için 'expr.pseudos'

## <a name="localisation"></a>Yerelleştirme
  * Urdu çeviri ekleyin. #1873 kapatır.

## <a name="localization"></a>Yerelleştirme
  * Sabit yanlış-için dosya uzantısı az çeviri. Closes #1890.
  * Eksik çeviri pt-BR (#1897 kapatır) eklendi
  * Sabit arabien dili dosyası yazım yanlışı.

## <a name="tests"></a>Testler
  * QUnit 2. 0'ı yükseltin.

## <a name="umd"></a>UMD
  * CommonJS için daha iyi destek.

<a name="1151--2016-07-22"></a>1.15.1 / 2016-07-22
==================

## <a name="additional"></a>Ek
  * Birden çok MIME türü doğrulama Düzelt
  * En az 5 karakter (#1797 kapatır, #1674 düzeltir) IBAN gerektirir
  * Doğru notEqualTo jQuery başvurusu

## <a name="core"></a>Çekirdek
  * Eklenen #1805 için test başarısız oluyor
  * Grup doğrulama 3 ve daha fazla alan düzeltme
  * #1644 ve #1657 (#1800 kapatır) de kullanıma sunulan gerilemeleri Düzelt
  * Kayan nokta doğru bir şekilde işlemek için doğrulama adımı güncelleştirme
  * Bir form olmayan öğede $.fn.rules() çağrılırken hata düzeltme
  * Çağrı `errorPlacement` Doğrulayıcı kapsamında
  * Olayları tek giriş doğrulama için özel durumları burada neden Forms'ta contenteditable öğelerle sorun düzeltildi

## <a name="demo"></a>Tanıtımı
  * Önyükleme ve Semantic UI tanıtımları için index.html bağlantılar ekleme
  * Kullanım `.on()` yerine `.validateDelegate()`

## <a name="localization"></a>Yerelleştirme
  * Eklenen bir Azerice dili

## <a name="tests"></a>Testler
  * Çekme isteği #1760 için eklenen regresyon birim testleri

<a name="1150--2016-02-24"></a>1.15.0 / 2016-02-24
==================

## <a name="all"></a>Tümü
  * Sabit kod stili sorunları

## <a name="core"></a>Çekirdek
  * `resetForm` Ayrıca kaldırmalısınız `valid` öğelerinden sınıfı.
  * Uzak kuralını kullanırken zaten vurgulanmış, unhighlighting alan.
  * Bağlama `blur` yalnızca bir kez olayı `equalTo` kuralı
  * .Rules() üzerinde boş jquery çağrılırken hata düzeltildi ayarlanmış.
  * Hata iletilerini işleme giriş gruplarıyla düzeltin.
  * İçinde TypeError düzeltme `showLabel` kullanırken `groups` ayarları
  * Yöntem adı uzak geçirmek için bir yol ekleme
  * Sonraki alana zaten (düzeltmeler #1508) dolduğunda tetiklemek doğrulama başarısız
  * Sayı & basamak kuralları üzerinden gerekli kuralı önceliklidir
  * Giriş hatası sınıfı gizlenmemiş hata kaldırıldı
  * Uzak doğrulama yanlış hata iletilerini kullanır.
  * Uzak doğrulama ile alanı vurgulama düzeltildi.
  * Sabit `:filled` çoklu seçim öğelerinden Seçicisi.
  * Eklenen belge jQuery.validator.methods referansı
  * Gelen işleme iletiyi `formatAndAdd` için `defaultMessage`
  * Yalnızca olması gerektiği hataları ErrorList içermelidir
  * Dosya adı "C:\fakepath dahil etmeden ayıklayın\"
  * HTML5 adım özniteliği desteği. #1295 giderir
  * "Bekliyor" bekleyen isteklerden sınıfı için destek eklendi
  * Added normalizer (#1602)
  * Çıkış bölme `creditcard` yöntemi
  * Aria-describedby = tasarlanmamış için kullanılmak üzere normal ifade, errorID kaçış
  * Kaçış adları bir hale getirir oluşturulan hata önleme tek tırnak işaretleri
  * API çağrısı atlamak için doğrulama alanın değeri kullanmak yerine, istek seri hale getirilmiş veri nesnesi kullanma
  * ContentEditable etiketleri için destek ekleme

## <a name="additional"></a>Ek
  * BIC: ikinci bir yerde konumun 1-9 arası rakamları izin ver
  * Yöntemi regex için doğru kaçış kabul edin.
  * Büyük küçük harf duyarsız BIC denetle
  * Geçersiz birleşimleri hariç tutmak için doğru postalCodeCA
  * PostalCodeCA yöntem daha esnek yapın

## <a name="localization"></a>Yerelleştirme
  * Makedonya yerelleştirme eklendi.
  * Lehçe (adamwojtkiewicz) içinde eklenen eksik desenini iletinin
  * En düşük/en yüksek ileti sabit Fars çevirisi.
  * Güncelleştirilmiş messages_sk.js
  * Malay çeviri güncelleştir
  * Ek yöntemleri gelen iletileri
  * Pt_BR çeviri geliştirme ve bir yazım yanlışı 'cifES' anahtarı düzeltiyor.

<a name="1140--2015-06-30"></a>1.14.0 / 2015-06-30
==================

## <a name="core"></a>Çekirdek
  * Remove kullanılmayan removeAttrs yöntemi
  * Regex URL'si yöntemi için değiştirin
  * Hatalı url param $.ajax, $.extend tarafından üzerine Kaldır
  * İç içe geçmiş iptal düğmesi düzgün bir şekilde işlemek
  * Girinti Düzelt
  * AttributeRules ve dataRules noramlizer paylaşmak için yeniden düzenleme
  * sayı girişleri için sayı değerini dönüştürmek için dataRules yöntemi
  * Güncelleştirme protokolü göreli URL'ler için izin vermek için url yöntemi
  * Kullanım dışı $.format yer tutucu Kaldır
  * JQuery 1.7 + açık/kapalı kullanın, ekleme yöntemi yok
  * IE8 uyumluluk .indexOf $.inArray için değiştirildi.
  * NaN değerini öznitelikleri tanımsız Opera Mini için tür dönüştürme
  * Kırpma değer gerekli metot içinde Durdur
  * Kullanım: devre dışı öğelerle eşleme için devre dışı Seçici
  * Alan gönderilmesinde engellemek için bazı klavye tuşlarını Dışla
  * Tüm DOM radyo/checkbox öğeler için arama
  * Daha iyi hataları hatalı kural yöntemleri için atar
  * Sabit numarası doğrulama hatası
  * Whatwg spec referansı düzeltin
  * Özel bir giriş kümesini doğrularken odak neplatný prvek
  * Öğe stili özel vurgu yöntemleri kullanılırken Sıfırla
  * Kaçış dolar işareti hata kimliği
  * "Yoksay salt okunur olarak devre dışı alanlar." Geri Al
  * Güncelleştirme bağlantısını Luhn algoritması için açıklama

## <a name="additionals"></a>Additionals
  * Güncelleştirme dateITA adresi saat dilimi verilecek
  * Genişletme yöntemi yalnızca yöntemi dönem için düzeltme
  * Düzeltme kabul dönem yalnızca eşleşecek şekilde yöntemi
  * Tek basamaklı saat izin vermek için güncelleştirme zaman yöntemi
  * Bırakma hatalı test notEqualTo yöntemi
  * NotEqualTo yöntemi ekleme
  * Doğru jQuery başvuru üzerinden kullanın `$`
  * Gereksiz regex onay IBAN yönteminde Kaldır
  * Brezilya CPF numarası

## <a name="localization"></a>Yerelleştirme
  * Güncelleştirme messages_tr.js
  * Update messages_sr_lat.js
  * Perú İspanyolca (ES PE) ekleme
  * Gürcüce (ქართული, ge) ekleme
  * Katalanca çeviri sabit yazım yanlışı
  * Fince (fi) çeviri geliştirin
  * Ermenice (hy_AM) yerel ayar Ekle
  * İtalyanca (,) ile para birimi yöntemi çeviri genişletme
  * Bn_BD yerel ayar Ekle
  * Güncelleştirme zh yerel ayar
  * İtalyanca iletileri sonunda tam Durma Kaldır

<a name="1131--2014-10-14"></a>1.13.1 / 2014-10-14
==================

## <a name="core"></a>Çekirdek
  * AutoCreateRanges değeri olarak 0 izin ver
  * Uygulama ayarı tüm validationTargetFor öğeleri yoksay
  * Min/maks/rangelength yöntemleri değerinde trim yok
  * Kimliği/ad errorsFor seçicide olarak kullanmadan önce kaçış
  * Açıkça varsayılan focusCleanup seçeneği
  * Yanlış regexp describedby = Eşleştiricisi için düzeltme
  * Salt okunur ve bunun yanı sıra devre dışı alanlar yoksay
  * Kimliği kaçış artırmak, mağaza kaçış kodu içinde describedby =
  * İzin verme veya engelleme form gönderme için submitHandler dönüş değerini kullanın

## <a name="additionals"></a>Additionals
  * PostalcodeBR yöntemi ekleme
  * Parametresi bir dize olduğunda, düzeni yöntemi Düzelt


<a name="1130--2014-07-01"></a>1.13.0 / 2014-07-01
==================

## <a name="all"></a>Tümü
* Eklenti UMD sarmalayıcı Ekle

## <a name="core"></a>Çekirdek
* Boş gizli hataları ve hata olmayan aria-describedby = Uy
* DateISO RegExp geliştirin
* Eklenen radyo/click olay temsilci seçmek için onay kutusu
* Aria-describedby = etiketi olmayan öğeler için kullanın.
* Focusin ve focusout keyup radyo/onay kutusu üzerindeki kaydetme
* Normalleştirme rangelength öznitelik değeri için düzeltme
* Güncelleştirme türü ile mücadele etmek elementValue yöntemi = "number" alanlar
* CharAt IE8(?) destek dizeler, dizi gösterimi yerine kullanın

## <a name="localization"></a>Yerelleştirme
* SK çeviri rangelength yönteminin Düzelt
* Fince yöntemleri ekleyin
* Sabit GL numarası doğrulama iletisi
* Sabit ES yöntemi doğrulama iletisi sayısı
* Eklenen Galiçya dili (GM)
* Min ve Maks yöntemleri için sabit Fransızca iletileri

## <a name="additionals"></a>Additionals
* StatesUS yöntemi ekleme
* Düzeltme DST hata ile dağıtılacak dateITA yöntemi
* Farsça tarih yöntemi ekleme
* PostalCodeCA yöntemi ekleme
* PostalcodeIT yöntemi ekleme

<a name="1120--2014-04-01"></a>1.12.0 / 2014-04-01
==================

* ARIA test ekleme ([3d5658e](https://github.com/jzaefferer/jquery-validation/commit/3d5658e9e4825fab27198c256beed86f0bd12577))
* ES AR yerelleştirme iletileri ekleyin. ([7b30beb](https://github.com/jzaefferer/jquery-validation/commit/7b30beb8ebd218c38a55d26a63d529e16035c7a2))
* Eksik nokta ekleyin 'es' ve 'es_AR' iletileri. ([a2a653c](https://github.com/jzaefferer/jquery-validation/commit/a2a653cb68926ca034b4b09d742d275db934d040))
* Endonezya dili (ID) yerelleştirme eklendi ([1d348bd](https://github.com/jzaefferer/jquery-validation/commit/1d348bdcb65807c71da8d0bfc13a97663631cd3a))
* Eklenen belgeleri numaraları doğrulama NBU, NIE ve CIF İspanyolca ([#830](https://github.com/jzaefferer/jquery-validation/issues/830), [317c20f](https://github.com/jzaefferer/jquery-validation/commit/317c20fa9bb772770bb9b70d46c7081d7cfc6545))
* Uzak ajax isteği bağlamı için geçerli form eklendi ([0a18ae6](https://github.com/jzaefferer/jquery-validation/commit/0a18ae65b9b6d877e3d15650a5c2617a9d2b11d5))
* Additionals: Güncelleştirme IBAN yöntemi, sondaki boşluk kesim ([#970](https://github.com/jzaefferer/jquery-validation/issues/970), [347b04a](https://github.com/jzaefferer/jquery-validation/commit/347b04a7d4e798227405246a5de3fc57451d52e1))
* BIC yöntemi: Normal ifade, artırmak {1} her zaman gereksizdir. GH 744 kapatır ([5cad6b4](https://github.com/jzaefferer/jquery-validation/commit/5cad6b493575e8a9a82470d17e0900c881130873))
* Bower: Paket kayıt için Bower.JSON ekleyin ([e86ccb0](https://github.com/jzaefferer/jquery-validation/commit/e86ccb06e301613172d472cf15dd4011ff71b398))
* 'JQuery' jQuery.noConflict ile uyumluluk için dolar başvurularını değiştirir. GH 754 kapatır ([2049afe](https://github.com/jzaefferer/jquery-validation/commit/2049afe46c1be7b3b89b1d9f0690f5bebf4fbf68))
* Çekirdek: Hata listesi girişi için "method" alanını ekleyin ([89a15c7](https://github.com/jzaefferer/jquery-validation/commit/89a15c7a4b17fa2caaf4ff817f09b04c094c3884))
* Çekirdek: Veri msg özniteliği aracılığıyla genel iletileri için destek eklendi ([5bebaa5](https://github.com/jzaefferer/jquery-validation/commit/5bebaa5c55c73f457c0e0181ec4e3b0c409e2a9d))
* Çekirdek: Sıfır değerine sahip öznitelik izin ver (örn min = '0') ([#854](https://github.com/jzaefferer/jquery-validation/issues/854), [9dc0d1d](https://github.com/jzaefferer/jquery-validation/commit/9dc0d1dd946b2c6178991fb16df0223c76162579))
* Çekirdek: Devre dışı bırakma kullanım dışı $.format ([#755](https://github.com/jzaefferer/jquery-validation/issues/755), [bf3b350](https://github.com/jzaefferer/jquery-validation/commit/bf3b3509140ea8ab5d83d3ec58fd9f1d7822efc5))
* Çekirdek: Birden çok hata sınıfları için destek düzeltme ([c1f0baf](https://github.com/jzaefferer/jquery-validation/commit/c1f0baf36c21ca175bbc05fb9345e5b44b094821))
* Çekirdek: Yoksayılan öğelerde olaylarını yoksay ([#700](https://github.com/jzaefferer/jquery-validation/issues/700), [a864211](https://github.com/jzaefferer/jquery-validation/commit/a86421131ea69786ee9e0d23a68a54a7658ccdbf))
* Çekirdek: ElementValue yöntemi geliştirmek ([6c041ed](https://github.com/jzaefferer/jquery-validation/commit/6c041edd21af1425d12d06cdd1e6e32a78263e82))
* Çekirdek: Element() göz ardı tanıtıcı öğeleri düzgün şekilde yapın. ([3f464a8](https://github.com/jzaefferer/jquery-validation/commit/3f464a8da49dbb0e4881ada04165668e4a63cecb))
* Çekirdek: Geçiş W3C HTML5 spec stiline ayrıştırma dataRules ([460fd22](https://github.com/jzaefferer/jquery-validation/commit/460fd22b6c84a74c825ce1fa860c0a9da20b56bb))
* Çekirdek: Tetikleme başarılı olduğunda isteğe bağlı, ancak diğer başarılı doğrulayıcıya sahip ([#851](https://github.com/jzaefferer/jquery-validation/issues/851), [f93e1de](https://github.com/jzaefferer/jquery-validation/commit/f93e1deb48ec8b3a8a54e946a37db2de42d3aa2a))
* Çekirdek: Kullanmak yerine düz öğesi beklemediğiniz kaydırma öğesi yeniden ([03cd4c9](https://github.com/jzaefferer/jquery-validation/commit/03cd4c93069674db5415a0bf174a5870da47e5d2))
* Çekirdek: uzaktan son yürütülen emin olun ([#711](https://github.com/jzaefferer/jquery-validation/issues/711), [ad91b6f](https://github.com/jzaefferer/jquery-validation/commit/ad91b6f388b7fdfb03b74e78554cbab9fd8fca6f))
* Demo: Doğru seçeneği çok bölümlü gösteride kullanın. ([#1025](https://github.com/jzaefferer/jquery-validation/issues/1025), [070edc7](https://github.com/jzaefferer/jquery-validation/commit/070edc7be4de564cb74cfa9ee4e3f40b6b70b76f))
* $/ JQuery kullanım ek yöntemleri düzeltin. Fixes #839 ([#839](https://github.com/jzaefferer/jquery-validation/issues/839), [59bc899](https://github.com/jzaefferer/jquery-validation/commit/59bc899e4586255a4251903712e813c21d25b3e1))
* Çince çevirileri geliştirin ([1a0bfe3](https://github.com/jzaefferer/jquery-validation/commit/1a0bfe32b16f8912ddb57388882aa880fab04ffe))
* İlk ARIA-gerekli uygulama ([bf3cfb2](https://github.com/jzaefferer/jquery-validation/commit/bf3cfb234ede2891d3f7e19df02894797dd7ba5e))
* Yerelleştirme: değişiklik uzantısı değerleri kabul edin. #771 düzeltmeleri, gh 793 kapatır. ([#771](https://github.com/jzaefferer/jquery-validation/issues/771), [12edec6](https://github.com/jzaefferer/jquery-validation/commit/12edec66eb30dc7e86756222d455d49b34016f65))
* İletileri: İzlanda yerelleştirme ekleyin ([dc88575](https://github.com/jzaefferer/jquery-validation/commit/dc885753c8872044b0eaa1713cecd94c19d4c73d))
* İletileri: Eksik nokta 'bg', 'tr' ve 'sr' iletileri ekleyin. ([adbc636](https://github.com/jzaefferer/jquery-validation/commit/adbc6361c377bf6b74c35df9782479b1115fbad7))
* İletileri: Messages_sr_lat.js oluşturun ([f2f9007](https://github.com/jzaefferer/jquery-validation/commit/f2f90076518014d98495c2a9afb9a35d45d184e6))
* İletileri: Messages_tj.js oluşturun ([de830b3](https://github.com/jzaefferer/jquery-validation/commit/de830b3fd8689a7384656c17565ee92c2878d8a5))
* İletileri: Sr_lat çeviri düzeltmek için eksik alanı Ekle ([880ba1c](https://github.com/jzaefferer/jquery-validation/commit/880ba1ca545903a41d8c5332fc4038a7e9a580bd))
* İletileri: Messages_sr.js güncelleştirmesi, eksik alanı düzeltme ([10313f4](https://github.com/jzaefferer/jquery-validation/commit/10313f418c18ea75f385248468c2d3600f136cfb))
* Yöntemleri: Para birimi için ek bir yöntem ekleyin ([1a981b4](https://github.com/jzaefferer/jquery-validation/commit/1a981b440346620964c87ebdd0fa03246348390e))
* Yöntemleri: Akıllı tırnaklar stripHTML'ın noktalama Temizleme için ekleme ([aa0d624](https://github.com/jzaefferer/jquery-validation/commit/aa0d6241c3ea04663edc1e45ed6e6134630bdd2f))
* Yöntemleri: Yaz Mevsimi hataların önlenmesiyle dateITA yöntemi düzeltme ([279b932](https://github.com/jzaefferer/jquery-validation/commit/279b932c1267b7238e6652880b7846ba3bbd2084))
* Yöntemleri: Yerelleştirilmiş Şili kültürü (es-CL) için yöntemleri ([cf36b93](https://github.com/jzaefferer/jquery-validation/commit/cf36b933499e435196d951401221d533a4811810))
* Yöntemleri: HTML5 regex kullanmak için e-posta2 yöntem kaldırma e-postasını güncelleştir ([#828](https://github.com/jzaefferer/jquery-validation/issues/828), [dd162ae](https://github.com/jzaefferer/jquery-validation/commit/dd162ae360639f73edd2dcf7a256710b2f5a4e64))
* Desen yöntemi: HTML5 uygulamaları, bu da içermez beri ayırıcılar kaldırın. ([37992c1](https://github.com/jzaefferer/jquery-validation/commit/37992c1c9e2e0be8b315ccccc2acb74863439d3e))
* Uzunluk denetimi eklemek için kredi kartı Doğrulayıcı kısıtlama. GH 772 kapatır ([f5f47c5](https://github.com/jzaefferer/jquery-validation/commit/f5f47c5c661da5b0c0c6d59d169e82230928a804))
* Messages_ko.js update - gh 715 kapatır ([5da3085](https://github.com/jzaefferer/jquery-validation/commit/5da3085ff02e0e6ecc955a8bfc3bb9a8d220581b))
* Messages_pt_BR.js güncelleştirin. GH 782 kapatır ([4bf813b](https://github.com/jzaefferer/jquery-validation/commit/4bf813b751ce34fac3c04eaa2e80f75da3461124))
* PhonesUK ve mobileUK yeni ön ekleri kabul edecek şekilde güncelleştirin. GH 750 kapatır ([d447b41](https://github.com/jzaefferer/jquery-validation/commit/d447b41b830dee984be21d8281ec7b87a852001d))
* Dokuz basamak posta kodları doğrulayın. GH 726 kapatır ([165005d](https://github.com/jzaefferer/jquery-validation/commit/165005d4b5780e22d13d13189d107940c622a76f))
* phoneUS: N11 dışlamaları ekleyin. GH 861 kapatır ([519bbc6](https://github.com/jzaefferer/jquery-validation/commit/519bbc656bcb26e8aae5166d7b2e000014e0d12a))
* resetForm aria-geçersiz değerleri temizlemek ([4f8a631](https://github.com/jzaefferer/jquery-validation/commit/4f8a631cbe84f496ec66260ada52db2aa0bb3733))
* valid(): Tüm öğeleri denetleyin. Düzeltmeleri - #791 valid() yalnızca ilk (geçersiz) öğeyi doğrular ([#791](https://github.com/jzaefferer/jquery-validation/issues/791), [6f26803](https://github.com/jzaefferer/jquery-validation/commit/6f268031afaf4e155424ee74dd11f6c47fbb8553))

<a name="1111--2013-03-22"></a>1.11.1 / 2013-03-22
==================

  * De aralık yönteminin parametreleri sayılara dönüştürme döndürün. GH 702 kapatır
  * Çoğu PHP kullanımını mockjax işleyicileri ile değiştirin. Bazı tanıtım temizleme de yapmak için yeni girişi maskelenmiş eklentisi için güncelleştirin. Captcha tanıtım PHP'de tutun. #662 giderir
  * Satır içi sütlü tanıtım kodları vurguladığımızdan kaldırın. Kaynağı Görüntüle düzgün çalışır.
  * JQuery oluşturucusuna geçirilmeden önce şablonu içeriğinden kırpmayı boşluk tarafından dinamik toplamlar tanıtım Düzelt
  * Min/Maks doğrulama düzeltin. GH 666 kapatır. #648 giderir
  * 'Bir kural olarak geldiğini ve neden rules("add") güncelleştirilmesini sonra bir özel durum iletileri' düzeltildi. GH 670 kapatır, #624 giderir
  * Korece (ko) yerelleştirme ekleyin. GH 671 kapatır
  * Daha fazla geçersiz postcodes filtrelemek için UK posta kodu yöntemi geliştirdik. #682 kapatır
  * Messages_sv.js güncelleştirin. #683 kapatır
  * Proje Web sitesindeki değişiklik grunt bağlantısı. #684 kapatır
  * Uzak yöntem bir alana uygulanan tüm diğer yöntemler sonra son olarak, çalıştırmak için listede aşağı taşıyın. #679 giderir
  * Plugin.JSON güncelleştirmesi, word 'Doğrula' içermelidir
  * Yazım hatalarını Düzelt
  * JQuery yükleyici yolu kendisinin kullanmak için düzeltildi. İç içe geçmiş düzeltmeleri tanıtımları.
  * PhantomJS 1.8 düğüm Modülü 'phantomjs' yüklendiğinde yararlanması için grunt-contrib-qunit güncelleştir
  * Bir Boole değeri 0 veya 1 yerine dönüş valid() olun. Düzeltmeleri - #109 valid() boolean bir değer döndürmüyor

<a name="1110--2013-02-04"></a>1.11.0 / 2013-02-04
==================

  * Temizleme sayıda olarak kaldırma `min`, `max` ve `range` kuralları. #455 düzeltir. GH 528 kapatır.
  * Önceden var olan etiketler update - düzeltmeleri #430 gh-436 kapatır
  * Düzeltme $. Burada, en az grup ilişkilendirme önlemek için validator.format değiştirir. IE8/9 - bash ile eşleşmiyor. #614 giderir
  * Mımetype regex Düzelt
  * Eklenti bildirimi ekleyin ve yalnızca MIT lisansı üstbilgileri güncelleştirme, (örneğin, jQuery) gereksiz çift lisanslama bırakın.
  * İbranice iletileri: Cümleleri - düzeltmeleri gh-568 sonunda kaldırılan noktalar
  * Fransızca çeviri require_from_group doğrulama için. GH 573 düzeltir.
  * Bir dizi veya dize - #479 düzeltmeleri olacak grupları izin ver
  * Kaldırılan alanları ile birden çok MIME türleri
  * Bazı tarih doğrulamaları, JS söz dizimi hatalarını düzeltin.
  * Meta verileri eklentisi için desteği kaldırabilir, yerine veri kuralı ve veri iletisi-(907467e8 eklendi) özellikleri.
  * Geçerli bir url deseni olarak eklenen sftp
  * Malay Dili (my) yerelleştirme Ekle
  * Güncelleştirme localization/messages_hu.js
  * Focusin/focusout polyfill kaldırın. Jquery.validate interfers IE9 focusin ve focusout olayları ile düzeltmelerini #542 - ekleme
  * Yerelleştirme: Fince çeviri sabit yazım yanlışı
  * Geçersiz simge geçerli yedeklemeyi kullanarak için geçersiz geçerken göstermek için RTM tanıtım Düzelt
  * Ajax çağrısı giriş çok hızlı bir şekilde girilen durumunda yapılan dan engelleyen uzak işlev sabit erken döndürür. Uzak doğrulama her zaman en yeni değerin doğrulama sağlar.
  * #244 düzeltmesini geri al. #521 - hemen metin alanı olduğunda e-posta doğrulama ateşlenir düzeltir.

<a name="1100--2012-09-07"></a>1.10.0 / 2012-09-07
===================

  * Fransızca dizeler nowhitespace, phoneUS phoneUK ve topluluk geri bildirimlerine mobileUK için düzeltildi.
  * Standart ISO_3166 1 göre language_REGION dosyalarını yeniden adlandırın (http://en.wikipedia.org/wiki/ISO_3166-1), Çince (zh) Tayvan için tha dilidir ve bölgedir Tayvan (TW)
  * Normal ifade desenleri, Birleşik Krallık telefon numaraları için özellikle optimize.
  * Her dosya için dil adı ekleme, yeniden adlandırmak için Estonca, Gürcüce, Ukrayna dili ve Çince (standart ISO 639 göre dil kodu http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)
  * Eklenen Hırvatça (ik) yerelleştirme
  * Mevcut Fransızca çevirileri düzenlendi ve Fransızca çevirileri ek yöntemleri için eklenmiştir.
  * Özel hata iletileri veri öznitelikleri belirtmek için değişiklikleri birleştirildi
  * Güncelleştirilmiş UK mobil telefon numarası için normal ifade yeni numaraları. #154 giderir
  * Öğe başarılı çağrı ile test ekleyin. Düzeltmeleri #60
  * Zaman ek yöntemi için sabit normal ifade. #131 giderir
  * resetForm artık eski previousValue form öğeleri üzerinde temizler. #312 giderir
  * Eklenen onay kutusu require_from_group ve değiştirilen require_from_group elementValue kullanmak için test edin. #359 giderir
  * Ayarlamalısınız jQuery 1.5.2+ içinde yanıt sorunlar düzeltildi. #405 giderir
  * Eklenen jQuery Mobile Tanıtımı. #249 giderir
  * Doğruluk findByName deoptimize. Fixes #82 - $.validator.prototype.findByName breaks in IE7
  * Eklenen ABD posta kodu desteği ve test. #90 giderir
  * Değiştirilen lastElement lastActive keyup içinde için sekmesinde veya boş öğesi Doğrulamayı atla. #244 giderir
  * Kaldırılan sayı stripHtml şeridi oluşturma. Düzeltmeleri #2
  * Geçerli uzak doğrulama için geçersiz sabit geçersiz sayısı. Düzeltmeleri #286
  * Tanıtım dizine file_input bağlantı ekleme
  * Eski uzantı yöntemine kabul taşınan ek yöntem, eklenen yeni accept standart tarayıcı mımetype filtreleme işlemek için yöntemi. #287 düzeltir ve #369 yerine geçer
  * Devre dışı bırakır, onfocusout false olarak ayarlandığında olay bulanıklaştıran. Test eklendi.
  * Radyo düğmeleri ve onay kutuları için değer sorun düzeltildi. #363 giderir
  * Eklenen test rangeWords ve sabit bir normal ifade yöntemi sınırları için. #308 giderir
  * Sabit TinyMCE tanıtım ve tanıtım sayfasında bağlantı eklendi. Fixes #382
  * Min/maks değiştirilen yerelleştirme iletisi. #273 giderir
  * Varsayılan boş tür özniteliği ile bu sorunu düzeltmek metin giriş türleri için sahte Seçici eklendi. Testler eklendi ve bazı biçimlendirme test edin. #217 giderir
  * Dinamik toplamlar tanıtım için sabit bir temsilci hata. #51 giderir
  * Alfasayısal doğrulayıcı için yanlış iletisi düzeltildi
  * Gerekli öznitelik yanlış false denetimi kaldırıldı
  * Gerekli öznitelik için html5 olmayan tarayıcıları düzeltin. #301 giderir
  * Eklenen yöntemleri "require_from_group" ve "skip_or_fill_minimum"
  * Doğru ISO kodunu, İsveç dili için kullanır.
  * HTML5 doctype kullanmak üzere güncelleştirilmiş tanıtım HTML dosyaları
  * Önünde sıfır olmadan ondalık Regex sorunu düzeltildi. Eklenen yeni yöntemleri test. Düzeltmeleri #41
  * Yalnızca dize değerleri (çoklu seçim dizi değeri dokunmayın) normalleştirir elementValue yöntem sunar. #116 giderir
  * Dinamik olarak eklenen düğmeleri ve güncelleştirilmiş test çalışması için destek. ValidateDelegate kullanır. Çekme isteği #9 koddan
  * Hatalı çift tırnak işareti içinde test armatürleri Düzelt
  * Üst sınıra dahil, dışarıda değil maxWords yöntemi düzeltin. #284 giderir
  * Alman aralığı Doğrulayıcı iletisinde dilbilgisi hata düzeltildi. #315 giderir
  * Birden çok sınıf adları errorClass seçeneği için sabit işlenmesi. En fazla Lynch'in tarafından test edin. #280 giderir
  * JQuery.format kullanım düzeltmek için $ olmalıdır. validator.format. #329 giderir
  * 'Tüm' UK telefon numaraları ve UK postcodes yöntemleri
  * Desen yöntemi: Dize param RegExp için dönüştürün. #223 düzeltmeleri sorunu
  * Alman yerelleştirme dosyasında dilbilgisi hata
  * İletiler için eklenen Estonca yerelleştirme
  * Araç İpucu themerollered tanıtım işleme geliştirin
  * Ekleme türü = giriş alanlarına olmadan qSA Lütfen için type özniteliği "metin"
  * Hataları kaplama olarak görüntülemek için araç ipucu kullanılacak themerollered tanıtım güncelleştirin.
  * En son jQuery kullanıcı Arabirimi (birlikte, jQuery sürüme) kullanmak için themerollered tanıtım güncelleştirin. Yaklaşık sayfa yükleme hızını artırmak için kod taşıyın.
  * Japonca bozuk sabit min hata iletisi.
  * Form eklentisi, en son sürüme güncelleştirin. AjaxSubmit tanıtım geliştirin.
  * Bu yerelleştirilmiş yöntemleri taşınmasını arta kalan classRuleSettings gelen dateDE ve numberDE yöntemleri bırak
  * Geçirme submitHandler geri çağırma olay gönderme
  * Düzeltildi #219 - valid() öğelerde bağımlılık geri çağırma veya bağımlılık ifadesi ile düzeltin.
  * Yalnızca geçerli yayın ayarlananlar emin olmak için dağıtım dizini kaldırmak için derleme geliştirin

<a name="190"></a>1.9.0
---
* Eklenen Bask dili (AB) yerelleştirme
* Eklenen Slovence (SL) yerelleştirme
* Sorun #127 - düzeltildi Fince çevirileri olan bir: yerine,
* Sabit Rusça yerelleştirme, küçük bir söz dizimi sorunu
* HTML5 giriş türleri, düzeltmeleri #97 için destek eklendi
* Form üzerinde ayarı novalidate özniteliği tarafından geliştirilmiş HTML5 desteği ve tür özniteliği okuma.
* Sabit showLabel() tüm sınıflar hata öğesinden kaldırılıyor. Yalnızca settings.validClass kaldırın. #151 düzeltir.
* 'Pattern' yöntemleri ek rastgele normal ifadeler karşı doğrulamak için eklendi.
* Nokta sonunda (geçerli, RFC tarafından ancak istenmeyen burada) izin vermeyecek şekilde geliştirilmiş e-posta yöntemi. #143 giderir
* İsveç ve Norveç çevirileri sabit, en düşük/en yüksek ileti geçiş. #181 giderir
* Düzeltildi #184 - resetForm: unset lastElement gerekir
* Düzeltildi #71 - zaman varolan bir yöntem geliştirmek ve time12h yöntem 12 sa. am/pm saat biçimi için ekleyin
* Düzeltildi #177 - tek radyo veya onay kutusu input düzeltme doğrulama
* Düzeltildi #189 -: gizli öğeleri artık varsayılan olarak yoksayıldı
* Düzeltildi #194 - öznitelik varsa başarısız olarak gerekli jQuery > 1.6 - kullanım .prop .attr yerine =
* Düzeltildi #47, #39; #32 - tire (genellikle kullanıcılar tarafından giriş boşluklara) yanı sıra alanları içerecek şekilde izin verilen kredi kartı numaraları

<a name="181"></a>1.8.1
---
* Eklenen Tay dili (TH) yerelleştirme düzeltmeleri #85
* Eklenen Vietnamca (VI) yerelleştirme Ngoc teşekkürler
* Düzeltildi #78. Gerekli doğrulama için aynı grup içinde bulunan tüm radyo düğmeleri hata/geçerli stil uygular.
* Form.elements, jQuery 1.6 artık desteklenmiyor olarak kullanmayın. Kendi buggy olarak cehennemi yine de (IE6-8: form.elements === form).

<a name="180"></a>1.8.0
---
* Geliştirilmiş NL yerelleştirme)http://plugins.jquery.com/node/14120)
* Eklenen Gürcüce (GE) yerelleştirme Avtandil Kikabidze teşekkürler
* Eklenen Sırpça (SR) yerelleştirme Aleksandar Milovac teşekkürler
* Eklenen IPv4 ve IPv6 için ek yöntemleri Natal Ngétal teşekkürler
* Bryan Meyerovich eklenen Japonca (JA) yerelleştirme, teşekkürler
* Eklenen Katalanca (CA) yerelleştirme Xavier de Pedro teşekkürler
* For açma Döngülerde sabit yok var deyimleri
* Uzak doğrulama, burada biçimlendirilmiş bir ileti olmadığında (' için düzeltme https://github.com/jzaefferer/jquery-validation/issues/11)
* Geriye dönük uyumluluğu koruyarak 1.5.1, jQuery ile uyumluluk için hata düzeltmeleri

<a name="17"></a>1.7
---
* Eklenen Litvanca (LT) yerelleştirme
* Yunanca (EL) yerelleştirme (eklendi http://plugins.jquery.com/node/12319)
* Letonca (LV) yerelleştirme (eklendi http://plugins.jquery.com/node/12349)
* İbranice (HE) yerelleştirme (eklendi http://plugins.jquery.com/node/12039)
* İspanyolca (ES) yerelleştirme (sabit http://plugins.jquery.com/node/12696)
* Eklenen jQuery kullanıcı Arabirimi themerolled Tanıtımı
* Kaldırılan cmxform.js
* Dört sabit noktalı (eksik http://plugins.jquery.com/node/12639)
* Yeniden adlandırılan telefon-methods.js phoneUS için ek yöntemi
* Methods.js ek (ek phoneUK ve mobileUK yöntemleri http://plugins.jquery.com/node/12359)
* Derin birden çok form üzerinde bir öğeyi (kuralları yöntemi kullanırken değiştirmekten kaçının seçeneklerini genişletin http://plugins.jquery.com/node/12411)
* Geriye dönük uyumluluğu koruyarak 1.4.2, jQuery ile uyumluluk için hata düzeltmeleri

<a name="16"></a>1.6
---
* Eklenen Arapça (AR), Portekizce (PTPT), Farsça (SK), Fince (FI) ve yerelleştirme Bulgarca (BR)
* Güncelleştirilmiş İsveççe (SE) yerelleştirme (bazı eksik html ISO karakter)
* Sabit $. boş bir dize karşılaştırması düzgün bir şekilde işlemek için validator.addMethod ileti bağımsız değişkeni tanımlanmamış
* Sabit iki yanlışlıkla genel değişkenler
* Html sayım önce Kendiyle Min/Maks/rangeWords (içinde ek-methods.js) Gelişmiş; Zengin Metin Düzenleyicisi sözcükleri sayım iyi
* Yerelleştirilmiş yöntemleri DE, NL ve PT, (messages_de.js ve methods_de.js tarih ve sayı yöntemleri ile kullanın) dateDE ve numberDE yöntemlerini kaldırma eklendi
* Sabit uzak formu eşitleme Matas Petrikas için beğenme Gönder
* Gelişmiş'e tıklayın (aracılığıyla seçeneği veya seçin, tarayıcılar arasında tutarsız); şimdi de doğrulama etkileşimli seçme doğrulama içinde bir tıklama olayı hiç select öğelerde tetiklemediğini Safari, işe yaramazsa; düzeltmeleri http://plugins.jquery.com/node/11520
* En son form eklentisini (2,36), güncelleştirilen düzeltme http://plugins.jquery.com/node/11487
* Bu değişiklikler, düzeltmeleri hedeflediğinizde düzeltin equalTo hedefi için olay bulanıklaştıran bağlayın http://plugins.jquery.com/node/11450
* Select değeri elde etmek için jQuery'nın val() yöntemi temsilci olarak görevlendirme Basitleştirilmiş seçme doğrulama, düzelmeniz gerekmektedir http://plugins.jquery.com/node/11239
* Basamak (için sabit varsayılan ileti http://plugins.jquery.com/node/9853)
* Önbelleğe alınan uzak iletisiyle sorun düzeltildi (http://plugins.jquery.com/node/11029 ve http://plugins.jquery.com/node/9351)
* Eksik noktalı sabit methods.js ek ()http://plugins.jquery.com/node/9233)
* Değiştirme parametreleri sağlamak için biçim işlevleri (gereğini ortadan kaldıran iletilerindeki eklenen otomatik algılanması http://plugins.jquery.com/node/11195)
* İle ilgili bir sorun düzeltildi: doldurulmuş /: boş biraz Pictures'a (tarafından neden oldu. http://plugins.jquery.com/node/11144)
* Bir tamsayı yöntemi için ek methods.js (eklendi http://plugins.jquery.com/node/9612)
* Burada özniteliği için gereken bir seçici () içinde geçerli olması için kaçış karakterleri içeren sabit errorsFor yöntemi http://plugins.jquery.com/node/9611)

<a name="155"></a>1.5.5
---
* Düzeltme http://plugins.jquery.com/node/8659
* Sabit sonunda virgül messages_cs.js içinde

<a name="154"></a>1.5.4
---
* Hata (sabit uzak yöntemi http://plugins.jquery.com/node/8658)

<a name="153"></a>1.5.3
---
* Sarmalayıcı seçeneği için ilgili bir hata düzeltildi burada tüm üst-sarmalayıcı seçeneği eşleşen öğeleri burada seçilen (http://plugins.jquery.com/node/7624)
* En son jQuery kullanıcı Arabirimi accordion kullanmak için güncelleştirilmiş çok bölümlü Tanıtımı
* DateNL ve zaman yöntemleri için additionalMethods.js eklendi
* Geleneksel Çince (Tayvan, tw) ve yerelleştirme Kazakistan "(" KK ") eklendi
* (Eski adıyla String.format) jQuery.format jQuery.validator.format için taşındı jQuery.format kullanım dışıdır ve 1.6 içinde kaldırılacak (bkz http://code.google.com/p/jquery-utils/issues/detail?id=15 Ayrıntılar için)
* Messages_pl.js ve messages_ptbr.js (1.4 içinde kaldırıldı hala tanımlı iletiler için en yüksek/min/rangeValue) temizlendi
* Yönteminde geçerli-plugin-birden çok öğe için sabit genişletebileceği Boole mantığı; Şimdi tüm öğeler için bir boolean true sonucunu (geçerli olması gerekir http://plugins.jquery.com/node/8481)
* Geliştirme $. validator.addMethod: Tanımsız üçüncü ileti-bağımsız değişken üzerine yazılmayacak var olan bir ileti (http://plugins.jquery.com/node/8443)
* Geliştirme submitHandler seçeneği: Kullanıldığında, düğmeler yakalanır ve bir gönderme düğmesi olayları gönderme tıklatın submitHandler çağırmadan önce forma eklenmiş ve daha sonra kaldırıldı; Gönderme düğmeleri sağlam (Tutar http://plugins.jquery.com/node/7183#comment-3585)
* Eklenen seçeneği validClass "geçerli", bu sınıfın tüm geçerli öğelerine ekleyen sonra doğrulama (varsayılan http://dev.jquery.com/ticket/2205)
* AdditionalMethods.js (aracılığıyla testler dahil olmak üzere, eklenen creditcardtypes yöntemi http://dev.jquery.com/ticket/3635)
* Gelince ileti bir dize veya true olarak geçerli ya da geçersiz kullanarak istemci tarafı tanımlanan ileti (false izin vermek için geliştirilmiş uzak yöntemi http://dev.jquery.com/ticket/3807)
* Geliştirilmiş accept yöntemi de Drupal stili virgülle ayrılmış listesi (değerleri kabul etmek için http://plugins.jquery.com/node/8580)

<a name="152"></a>1.5.2
---
* $.format çağrısına içerecek şekilde methods.js maxWords minWords ve rangeWords için ek sabit iletileri
* JQuery'nın val() aynı sabit değeri, satır başı (\r) hariç tutmak için yöntemlere geçirilen yok
* Slovakça (sk) yerelleştirme eklendi
* JQuery kullanıcı Arabirimi sekme ile tümleştirme için eklenen Tanıtımı
* Eklenen seçer gruplandırma örnek sekmelere tanıtım (ikinci sekme birthdate alan bakın)

<a name="151"></a>1.5.1
---
* Bağlama geçersiz biçimli olay yerine invalidHandler seçeneği kullanmak için marketo tanıtım güncelleştirildi
* Eklenen TinyMCE tümleştirme örneği
* Eklenen Ukrayna dili (ua) yerelleştirme
* Bölünen değer (1.5 doğrulama önce genel kırpmayı burada kaldırıldı gerileme) ile çalışmak için sabit uzunluk doğrulama
* 1.2.6 hem 1.3 ile uyumluluk için çeşitli küçük düzeltmeler

<a name="15"></a>1,5
---
* Geliştirilmiş basit gösteri, parola değiştikten sonra parolayı onayla alanı doğrulanıyor
* Fitillerle giriş değeri doğrulama yöntemleri için ilk parametre olarak geçirmek için sabit bir temel doğrulama değiştirilmesi gereken uygun şekilde; Kırpma üzerinde kullanan mevcut özel yöntem keser
* Eklenen Norveççe (no), İtalyanca (,), Macarca (hu) ve Rumence (satır) yerelleştirme
* Düzeltildi #3195: İki eksiklikler İsveççe yerelleştirme
* Düzeltildi #3503: Messages özelliğinde kabul edecek şekilde rules("add") genişletilmiş: belirtmek için kullanın kuralları aracılığıyla bir öğe için özel bir ileti ekleme ("Ekle", {iletileri: {gerekli: "Gerekli! " } });
* Düzeltildi #3356: Meta seçenek kullanırken #2908 gerileme
* Düzeltildi #3370: Eklenen ignoreTitle seçeneği, başlık özniteliğinden okuma iletileri atlanacak Ayarla Google araç çubuğu ile ilgili sorunları önlemek için yardımcı olur; Varsayılan uyumluluk için false
* Düzeltildi #3516: Uzak doğrulama bile söz konusu olduğunda tetikleyici geçersiz biçimli olay
* Bağlama için bir kısayol olarak invalidHandler seçeneği eklendi ("Geçersiz-form" function() {})
* Gösterge ajaxSubmit tümleştirme tanıtım yükleme Safari sorun düzeltildi (gövdesi için önce eklemek ve ardından Gizle)
* Eklenen test creditcard doğrulamayı ve Gelişmiş varsayılan ileti
* Gelişmiş Seçenekleri geçiş $.ajax parametre olarak kabul uzak doğrulama (url dize veya seçenekleri URL'si özelliği dahil olmak üzere, diğer her şey bu $.ajax destekler)

<a name="14"></a>1.4
---
* Belge sırada öğeleri doğrulamak ve türü yoksay #2931 sabit görüntü girişleri =
* $ Ve jQuery değişken, artık tam olarak uyumlu noConflict kullanım tüm çeşitlerini sabit kullanımı
* Meta veri ala sınıfı aracılığıyla özel iletilerini etkinleştirme #2908 uygulanan = "{gerekli: true, ileti: {gerekli: 'gerekli alanı'}}", tanıtım/custom-iletileri-meta-demo.html eklendi
* Kullanım dışı yöntemler minValue (min) maxValue (Maks), rangeValue (rangevalue), (minlength) minLength, maxLength (maxlength) rangeLength (rangelength) kaldırıldı
* #2215 gerileme düzeltildi: Çağrı unhighlight yalnızca geçerli öğeleri için her şey
* Uygulanan #2989, görüntü düğme doğrulamayı iptal etmek etkinleştirme
* Burada, IE sorun düzeltildi yanlış maxlength karşı doğrular = 0
* Eklenen Çekçe (cs) yerelleştirme
* Tam bir sıfırlama gerekli olduğunda etkinleştirme validator.resetForm() üzerinde Validator.submitted Sıfırla
* Düzeltildi #3035, maxlength için geçici çözüm (0) parçası kuralları kaldırıldı (0, tanımlanmamış, boş dize), okuma sırasında tüm falsy öznitelikleri atlanıyor
* Hollanda (nl) yerelleştirme eklendi (#3201)

<a name="13"></a>1.3
---
* Şimdi form geçersiz olduğunda yalnızca tetiklenen sabit biçim geçersiz olay
* Eklenen İspanyolca (es), Rusça (ru), Portekizce (ptbr) Brezilya Portekizcesi, Türkçe (tr) ve yerelleştirme Lehçe (pl)
* Ekleme ve kaldırma birden çok öznitelik kolaylaştırmak için eklenen removeAttrs eklentisi
* Grupları aracılığıyla birden çok öğe için tek bir ileti görüntülemek için Grup seçeneği eklendi: {arbitraryGroupName: "Alanadı1 Alanadı2 [, fieldNameN"}
* Ekleme ve kaldırma (statik) kuralları rules() Gelişmiş: kural ("Ekle", "method1 [, methodN]" / {method1:param [, method_n:param]}) ve kural ("Kaldır" ["method1 [, method_n]")
* Gelişmiş kurallar-seçeneği, boşlukla ayrılmış dize-yöntemlerin listesi, örneğin kabul eder. {Doğum Tarihi: "gereken tarihi"}
* Satır içi kurallarla onay kutusu Grup doğrulaması düzeltildi: Kurallar ilk öğesinde belirtilen sürece, grubun artık düzgün tıklayın doğrulanır
* Düzeltildi # örn açık parametresiyle birlikte Boole false, tüm kurallar yoksayılıyor 2473. gerekli: değil belirtmekle aynı hiç yanlış gereklidir (Bu işlenmiş gerektiği gibi: şu ana kadar true)
* #2473 değiştirilmiş bir düzeltme ekini ile düzeltildi #2424: Bir bağımlılık uyuşmazlığı yöntemleri artık değerlendirilen gelen kurallar Durdur yok; Başarı için isteğe bağlı alanları yine de uygulanmaz
* Kırpılmış değerleri kullanmayı sabit url ve e-posta doğrulama
* Yalnızca rakam ve tire ("asdf" bir geçerli creditcard sayı değil) kabul etmek için sabit creditcard doğrulama
* Düğme hem giriş öğelerde İptal düğmeleri izin ver ("İptal" sınıfı =)
* Düzeltildi #2215: Çağırmak için sabit bir ileti görünen unhighlight gösterme ve gizleme iletileri, artık visual yan bir öğe ve bir forma kullanıcı Arabirimi sideeffects olmadan doğrulamak için ayıklanan validator.checkForm denetlenirken etki işleminin parçası olarak
* Özel seçiciler yeniden yazıldı (: boş: doldurulmuş,: denetlenmeyen) HAVA ile uyumluluk için işlevleri ile

<a name="121"></a>1.2.1
-----

* İle birlikte gelen temsilci eklentisi ile eklentisi - kendi her zaman gerekli yine de doğrula
* Uzak doğrulama ajaxQueue eklentisi için uygun eşitleme (ek eklenti gerekli) bölümleri içerecek şekilde geliştirildi
* Sabit stopRequest pendingRequest < 0 önlemek için
* Eklenen jQuery.validator.autoCreateRanges özelliği varsayılan olarak aralık ve minlength/maxlength rangelength için en düşük/en yüksek dönüştürmek için false sağlar; Bu temelde aralıkları 1.2 ile otomatik olarak oluşturarak sunulan sorunu düzeltir
* Sabit isteğe bağlı-boş alan ise hiçbir şey hiç değil vurgulamaya yöntemlerini diğer bir deyişle, başarı tetiklemek yok
* Vurgulama ve unhighlight seçenekleri bile hiçbir şey vurgulanmasını gerektiğinde yerine bir yapılacak işler mobil-nothing-geri çağırma zorlamak için false/null izin ver
* Sabit validate() çağrısıyla tanımlanmamış bir hata oluşturma yerine döndüren seçili öğe yok
* Geliştirilmiş gösteri, kuralları belirtmek için sınıflar/öznitelikleri olan meta verileri değiştirme
* Uzak doğrulama için özel bir ileti kullanıldığında hata düzeltildi
* Etki alanı etiketi ve üst etiket gerektirecek şekilde değiştirilmiş e-posta ve url doğrulaması
* (Aslında etki alanı etiketi gerektirecek şekilde) TLD gerektirecek şekilde sabit url ve e-posta doğrulaması; (isteğe bağlı olarak TLD) 1.2 sürümü eklemeleri url2 ve e-posta2 olarak taşınır
* Sabit dinamik toplamlar tanıtım IE6/7 ve çok satırlı şablon ve dize ilişkilendirme depolamak için textarea kullanılarak geliştirilmiş şablon oluşturma
* Parola alanı isteğe bağlı hale getirir, "E-posta parola" bağlantıyla ek oturum açma form örneği
* Bir örnek için iki alanı tek bir ileti ile Gelişmiş dinamik toplamlar gösteri

<a name="12"></a>1.2
---

* (Temel AJAX captcha doğrulama örnek eklendi http://psyrens.com/captcha/)
* Eklenen unutmayın--sütlü-demo (izin için teşekkür ederiz RTM takım!)
* Eklenen marketo-demo (Glen Lipka teşekkürler!)
* Ajax doğrulama desteği eklendi yöntemi "Uzaktan"; Bkz: gelince, JSON, true, geçerli öğeler için false değerini döndürür veya geçersiz, dize için bir dize iletisi olarak kullanılır
* Eklenen vurgulama ve seçenekleri unhighlight, errorClass öğe üzerinde varsayılan olarak değiştirir, özel vurgulama sağlar
* Valid() eklentisi yöntemi kolay programlı formlar ve alanlar API Doğrulayıcı kullanmak zorunda kalmadan denetimi eklendi
* Okuma ve yazma (şu anda salt okunur) bir öğe için kuralları rules() eklentisi yöntemi eklendi
* Değiştirilen regex Scott Gonzalez katkı sayesinde, e-posta yöntemi için bkz. http://projects.scottsplayground.com/email_address_validation/
* Yeniden yalnızca temsilciliği yararlanmayı olay denetimli mimari hem geliştirmeye performansı ve kullanımı kolay geliştiricinin (jquery.delegate.js gerektirir)
* Satır içi belgelere taşınmıştır http://docs.jquery.com/Plugins/Validation - tüm yöntemleri için etkileşimli örnekler dahil
* Kaldırılan validator.refresh() doğrulama artık tamamen dinamik
* Yeniden adlandırılan minValue min, maks için maxValue ve rangeValue aralığına, önceki adlarını (1.3 içinde kaldırılması için) kullanım dışı bırakılıyor
* Yeniden adlandırılan minLength minlength, MaxLength maxLength ve rangeLength için rangelength, önceki adlarını (1.3 içinde kaldırılması için) kullanım dışı bırakılıyor
* Min birleştirme + içine en fazla ve aralığı için ek özellik ve minlength + maxlength rangelength içine
* Dinamik kuralı parametreleri, parametre olarak, örneğin bir işlevi belirtmek için izin vermek için destek eklendi. öğeyi doğrularken minLength için çağırılır
* Null veya boş dize hiçbir şey (marketo Machine'i) görüntülenecek bir ileti belirtmeye izin verme
* Kuralları bakımdan: Artık destekler birleşimi kurallarını seçeneği, meta verileri, (yeni) sınıfları ve öznitelikleri (yeni) rules() Ayrıntılar için bkz:

<a name="112"></a>1.1.2
---

* Değiştirilen regex Scott Gonzalez katkı sayesinde URL yöntemi için bkz. http://projects.scottsplayground.com/iri/
* Unicode karakter daha iyi işlemek için geliştirilmiş e-posta yöntemi
* Tüm öğeleri yalnızca form gönderme üzerinde geçerli olduğunda gizlemek için kapsayıcı hata düzeltildi
* Sabit String.format jQuery.format (jQuery ad alanına taşıyarak) için
* Sabit accept üst ve küçük uzantılar kabul edecek şekilde yöntemi
* Belirli bir form için yalnızca bir doğrulayıcı örneği oluşturun ve her zaman bu bir örnek (birden çok kez olayları bağlama engeller) döndürmek için sabit validate() eklentisi yöntemi
* "" Düzeyi uyarmak üzere "error" hata ayıklama modu konsol günlüğü değiştirildi

<a name="111"></a>1.1.1
-----

* IE'de hata etiketi oluşturulduktan sonra jQuery 1.1.4 önleme geçersiz XHTML düzeltildi
* Sabit ve geliştirilmiş String.format: Genel arama ve değiştirme, daha iyi dizi bağımsız değişkenleri işleme
* Doğrulayıcı nesne yerine form öğesi durumu depolamak üzere kullanılacak sabit İptal düğmesini işleme
* "Karmaşık" adları, örneğin işlemek için sabit adı seçicileri. köşeli ayraçlar ("list[]") içeren
* Eklenen düğmesi ve doğrulamanın dışında tutulacak devre dışı öğeler
* İşleyicileri eklemek için yeni öğeler yapabilmek için yenilemek için olay işleyicileri öğesi taşındı
* Uzun süre üst düzey etki alanları (örn. izin vermek için sabit bir e-posta doğrulama ".travel")
* Valid() öğesinden taşındı showErrors() form() için
* Validator.size() eklendi: geçerli hataların sayısını döndürür
* SubmitHandler Doğrulayıcı ile kendi yönteminizi daha kolay erişim için kapsam olarak örn çağırın. errorsFor(Element) kullanarak hatayı bulmak için etiketler
* JQuery ile uyumlu 1.1.x ve 1.2.x

<a name="11"></a>1.1
---

* Eklenen doğrulamasını keyup Bulanıklığı ve (onay kutularını ve Ortala radyo düğmesi) tıklayın. Olay seçeneği yerini alır.
* Sabit resetForm
* Sabit özel yöntemler-Tanıtımı

<a name="10"></a>1.0
---

* Sınırlayıcı ile doğru ondalık sayı olup olmadığını denetlemek için geliştirilmiş sayısı ve numberDE yöntemleri
* Yalnızca kuralları olan öğeler denetlenir (Aksi halde başarı seçeneği tüm öğelere uygulanır)
* Eklenen creditcard numarası yöntemi (sayesinde, Brian Klug)
* Yoksay seçeneğini, örneğin eklendi. Yoksay: "[@type= gizli]", ifade kullanarak doğrulamak için öğeleri. Varsayılan: yok, ancak gönderin ve sıfırlama düğmeler her zaman yoksayılır
* Son derece gelişmiş işlevler--esnek String.format yardımcıyı sağlayarak iletiler
* İşlevler çalışma zamanı özel iletileri sağlayan ileti olarak kabul et
* Sabit çıkarma kuralları olmadan öğelerin successList
* Sabit özel-yöntemi-demo, hatalarının sayısını görüntüleyen iletisiyle uyarı değiştirildi
* Sabit form gönderme-submitHandler kullanırken önleme
* Bunlar yine de (varsa) hata etiketleri girişleri bağlamak için kullanılır ancak tamamen öğesi kimlikleri, bağımlı kaldırıldı. Bir dizi {adı, ileti, kullanarak öğesi ile} iç errorList kimliği: ileti çiftleri ile bir nesne yerine elde.
* Basit kural örn basit dize olarak belirtmek için destek eklendi. "required" eşdeğerdir {gerekli: true}
* Ek özellik: Etiketi/alan kapsayıcı ya da bir alanın etiketini stil kolaylaştırma geçersiz alan s üst öğeye errorClass ekleyin.
* Ek özellik: focusCleanup - etkinleştirilirse, errorClass geçersiz öğeleri kaldırır ve tüm hata iletileri öğe odaklanmıştır zaman gizler.
* Eklenen göstermek için başarı seçeneği bir alanın başarıyla doğrulandı
* Opera seçin-(öznitelik çakışma önleme) sorun düzeltildi
* Gizli öğeleri IE'de focussing sabit sorunları
* Düğmeleri sınıfıyla doğrulamasını atlamak için ek özellik "İptal"
* Eklenti seçeneği iletileri title özniteliği belgelemeyi tarafından sabit ilgili olası sorunları Google araç çubuğu
* submitHandler yalnızca çağrılır validator.form() gerçek bir gönderme olay işlenen, yalnızca geçersiz formları için false değerini döndürür
* Geçersiz öğeler artık odaklanmış yalnızca gönderin veya tüm sorun Bulanıklaştırma üzerinde odak validator.focusInvalid() kaçınma
* IE6 hata kapsayıcısı altında düzen sorununu çözüldü
* Hata errorElement seçeneği aracılığıyla özelleştirme
* Yeni giriş formunda bulmak için eklenen validator.refresh()
* Eklenen doğrulama yöntemi, denetimleri dosya uzantılarını kabul edin
* İki özel ifadeler ekleyerek Gelişmiş bağımlılık özelliği: ": boş" boş bir değere sahip öğeleri seçmek için ve: doldurulmuş bir değerle hariç her iki boşluk öğeleri seçmek için
* ResetForm() yöntemi doğrulayıcıya eklendi: Sıfırlar (varsa form eklentisi kullanılarak) her bir form öğesi, geçersiz öğeler sınıflarında kaldırır ve tüm hata iletilerini gizler
* Validator.showErrors() sabit belgeleri
* Hata etiket oluşturma html() text() yerine kullanılması her zaman sabit, rastgele HTML izin ileti olarak geçirildi
* Belirtilen hata sınıfını kullanmak için sabit hata etiket oluşturma
* Eklenen bağımlılık özelliği: Yöntemi dizesi (jQuery ifadeleri) hem de işlevleri bağımsız değişken olarak kabul gerektirir
* Hata iletisi görüntüsünü özelleştirme yoğun bir şekilde geliştirildi: Normal iletileri kullanın ve ek bir kapsayıcı Göster/Gizle; İleti görüntüleme (sırasında varsayılan işleyicisine temsilci işaretleyebilmesine kendi mekanizması tamamen değiştirin (Yerine varsayılan aşağıda öğe) oluşturulan etiket yerleştirme özelleştirme
* IE'de iki önemli hatalar düzeltildi (hata kapsayıcılar) ve Opera (meta veriler)
* Doğrulama yöntemlerinin boş alanları geçerli olarak kabul etmek için değiştiren (özel durum: gerekli kurs ve ayrıca equalTo yöntem)
* "Min" ila "minLength", "maxLength" için "max", "rangeLength" için "uzunluğu" olarak yeniden adlandırıldı
* Eklenen "minValue", "maxValue" ve "rangeValue"
* Kolaylaştırılmış API farklı olayların desteği. Varsayılan olarak, gönderme, devre dışı bırakılabilir. Herhangi bir olay belirtilirse, (yerine tüm formu) her öğeye uygulanır. KeyUp doğrulama gönderme doğrulama ile birleştirmek artık kurulum için son derece kolaydır
* Bir-message-eklenti ayarları aracılığıyla iletileri tanımlarken kural desteği eklendi
* Meta verileri bazı üst öğenin içinde sarmalamak için destek eklendi. Meta verileri diğer eklentiler için çok kullanıldığında yararlıdır.
* İşlenmiş testleri ve Tanıtımlar: Dosyaları daha az, tanıtımlar daha iyi
* Geliştirilmiş belgeler: Daha fazla örnek yöntemleri için daha fazla başvuru bazı temel bilgileri açıklayan metin
