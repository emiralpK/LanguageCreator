Gelişmiş Dil Yaratıcı – Geliştirme Alanları
Araştırması
1. Yapay Zeka Entegrasyonları
Otomatik Dil Oluşturma
Otomatik dil oluşturma, yapay zeka yardımıyla yeni yapay dil kurallarının ve söz dağarcığının
oluşturulması demektir. Bu özellik, kullanıcıya birkaç tıklamayla veya girdiyle tutarlı bir dil iskeleti
sunabilir. Güncel yaklaşımlar arasında büyük dil modelleri (LLM) ve kural tabanlı jeneratörler
bulunur:
LLM tabanlı çözümler: Örneğin Conlang GPT adlı açık kaynak araç, ChatGPT API’sini kullanarak
dil kılavuzu (fonetik, dilbilgisi kuralları) ve sözlük taslağı oluşturabiliyor . Komut satırı
aracılığıyla yeni bir dil taslağı üretip iyileştirmeler yapabiliyor ve hatta metinleri bu yapay dile
çevirebiliyor . Benzer şekilde Conlang Creator gibi web araçları da GPT-4 entegre ederek
şablonlar ve örnek ekler üzerinden kullanıcıya dil yaratımında rehberlik ediyor .
Kural ve veri tabanlı jeneratörler: Vulgarlang gibi popüler bir fantezi dil jeneratörü, tek tıkla
dilin ses sisteminden dilbilgisine ve temel kelime hazinesine kadar üretim yapar. Gerçek dillere
ait kuralları ve düzensizlikleri modelleyerek tutarlı bir dil oluşturur . Bu tür araçlar genellikle
sabit algoritmalar ve dilbilimsel kural setleri kullanır. Örneğin, Language Cooker aracı Dünya
Dillerinin Yapısal Özellikleri veritabanından (WALS) yararlanarak tipolojik olarak tutarlı rastgele
diller üretebiliyor .
Entegrasyon önerileri: Eğer proje bir web uygulaması ise, OpenAI veya Hugging Face gibi
platformların API’leri üzerinden GPT-4/Transformer modellerine istek atarak kullanıcı girdilerine
göre dil kuralı veya kelime üretimi yapılabilir. Alternatif olarak, mevcut açık kaynak projeler (ör.
Conlang GPT) kütüphane olarak entegre edilip arka planda çalıştırılabilir. Kural tabanlı bir
yaklaşım için ise WALS verilerini içeren sabit bir algoritma (ör. olasılıksal özellik seçimi)
kullanılabilir. Bu sayede kullanıcı birkaç parametre seçtiğinde arka planda bir dil iskeleti otomatik
oluşacaktır.
Otomatik Çeviri
Oluşturulan yapay dilin gerçek dillerle veya kendi içinde otomatik çevirisi, özellikle AI desteğiyle
mümkün olabilir. İki temel yaklaşım vardır: kural tabanlı çeviri ve yapay zeka tabanlı çeviri.
Kural tabanlı (sözlük + gramer) çeviri: Eğer kullanıcı kendi dilinin sözlüğünü ve dilbilgisi
dönüşüm kurallarını tanımladıysa, bu verilere dayanarak bir çeviri motoru yazmak mümkündür.
Örneğin açık kaynak Apertium çeviri platformu, kural tabanlı makine çevirisi için yeni dil
çiftlerinin eklenmesine izin verir. Sözlük eşleştirmeleri ve dönüştürme kuralları tanımlanarak
Apertium altyapısıyla yapay dilden bir hedef dile (veya tam tersi) çeviri yapılabilir. Bu yaklaşım,
yeterli kural tanımlandığında hızlı ve tutarlı çeviri sunar.
Yapay zeka tabanlı çeviri: Conlang GPT aracının da gösterdiği gibi, bir LLM modeli kullanarak
herhangi bir metni oluşturulan yapay dile veya ondan geri çevirtmek mümkündür . Bu
yaklaşım için modelin, yapay dilin kurallarını içeren bir bağlama sahip olması gerekir. Conlang
GPT, dilin kılavuzunu ve sözlüğünü sürekli güncelleyerek ChatGPT’nin metinleri çevirmesini
•
1
2
3
•
4
5
•
•
•
6
1
sağlıyor . Kendi web sitenizde benzer bir entegrasyon için OpenAI API’den, kullanıcı dilinin
tanımını prompt’a ekleyerek çeviri istemek mümkün. Ancak bu yöntemde çıktılar her zaman
%100 tutarlı olmayabilir, yine de hızlı prototip için değerlidir.
Mevcut API’ler: Büyük çeviri servisleri (Google Translate, Yandex, Microsoft Translator gibi) özel
bir yapay dili desteklemez; ancak popüler dillere çeviri özelliği siteye entegre edilebilir. Örneğin
Google Çeviri API ile kullanıcı arayüzünde gerçek diller arası çeviri sunulabilir. Yapay dil için ise
özel bir çözüm gerekecektir. Eğer yeterince veri toplanırsa, HuggingFace Transformers kullanarak
küçük bir çeviri modeli bile eğitilebilir fakat bu oldukça veri ve zaman ister.
Entegrasyon Önerisi: İlk etapta, kullanıcı tanımlı sözlük ve dilbilgisi kurallarına dayanarak basit bir
sözlük çeviri modülü geliştirmek mantıklı. Kullanıcı bir cümle girdiğinde, cümleyi kelime kelime
sözlükten çevirip temel dilbilgisi kurallarına (söz dizimi, çekim) göre dönüştürebilirsiniz. Daha esnek bir
çözüm için bir AI API’ine, yapay dilin tanımını verip çeviri yaptırabilirsiniz. Örneğin OpenAI’ın bir
modeline şu şekilde bir istek gönderilebilir: “Translate the following English text to [KullanıcıDili] following
these grammar rules: ...”. Bu, kural tabanlı yaklaşıma göre esnek ama kontrolü zor bir yöntem olduğu için
her iki yaklaşımı birleştirmek de mümkündür.
Ses Sentezi ve Telaffuz Üretimi
Kullanıcının oluşturduğu dilin telaffuzunu duyabilmek, projeye önemli bir interaktif boyut katar. Yapay
diller genellikle özel ses envanterine sahip olabileceğinden, esnek bir ses sentezi çözümüne ihtiyaç
vardır:
Mevcut TTS Servisleri: Google Cloud Text-to-Speech, Amazon Polly, Microsoft Azure TTS gibi bulut
servisleri metni sese çevirebilir. Bu servislerin bazılarında telaffuzu özelleştirmek için SSML
(Speech Synthesis Markup Language) desteği vardır. Örneğin Amazon Polly ile SSML
<phoneme> etiketi kullanarak belirli bir kelimenin telaffuzunu IPA olarak belirtebilirsiniz . Bu
sayede yapay dilinizdeki özel bir kelimeyi doğru telaffuzla okutmak mümkün olur. Google TTS de
benzer şekilde SSML ile destek sunar. Bu servisler doğal insan sesi kalitesine yakın çıktılar verir;
entegrasyonu ise API çağrılarıyla yapılır (metni ve istenen sesi API’ye gönderip dönen ses verisini
almak).
Açık Kaynak ve Offline TTS: eSpeak NG gibi açık kaynak kodlu metin-okuyucu motorları, daha
basit ve robotik sesler üretse de özelleştirilebilirlik sunar. eSpeak, belirli bir dilin fonetik
envanterini tanımlayarak o dildeki metinleri okuyabilir hale gelebilir. Örneğin eSpeak’in phoneme
tanım dosyalarını kullanarak kendi dilinizin seslerini ekleyebilirsiniz. Hatta eSpeak doğrudan IPA
veya X-SAMPA olarak girilen telaffuzları seslendirebiliyor (komut satırında IPA girişi vererek çıktı
alabilirsiniz) . Bu yöntem teknik bilgi gerektirse de maliyetsizdir ve uygulamanıza
gömülebilir.
Web Speech API durumu: Tarayıcıların yerleşik Speech Synthesis API’leri (Web Speech API)
kullanıcıya metni sesli okutabilir. Ancak bu API’ler cihazın ses motorunu kullanıp sesi direkt
hoparlöre gönderir; programatik olarak kaydedilmiş bir ses dosyası vermez . Yani tarayıcıda
speechSynthesis ile anlık telaffuz duymak mümkünken, oluşan sesi indirtmek bu yolla mümkün
değil. Bu nedenle, web uygulamanızda anlık dinleme özelliğini Web Speech API ile verebilir, kalıcı
bir ses dosyası için arka planda bir bulut TTS servisine istek gönderip dönen ses dosyasını
kullanıcıya sunabilirsiniz.
Entegrasyon Önerileri: Eğer gerçekçi ses önem taşıyorsa, Google veya Amazon’un TTS API’lerine
istek atıp MP3 formatında ses dosyası üretmek iyi bir seçenektir . Bu servisler farklı diller
için mevcut sesleri kullanır, ancak yapay dilinizi yakın bir gerçek dil aksanıyla okutabilir veya
SSML-IPA yöntemiyle doğru sesi çıkarabilirsiniz. Diğer yandan basit bir yaklaşım olarak, eSpeak’i
sunucu tarafında çalıştırıp (ör. Python ortamında espeak komutu ile) çıktı ses dosyasını alıp
kullanıcıya sunma yoluna gidilebilir. Son olarak, kullanıcıya telaffuz rehberi sağlamak için her
•
•
8
•
9 10
•
11
•
12 13
2
kelimenin IPA karşılığını göstermek de faydalı olacaktır – bu sayede eğer ses sentezi kalitesi
düşükse bile kullanıcı IPA üzerinden telaffuzu anlayabilir.
AI ile Varyasyon Önerileri
Yapay zeka, kullanıcı tarafından girilen içeriklere bakarak yeni varyasyonlar veya öneriler sunmada da
kullanılabilir. Bu bağlamda, kullanıcının oluşturduğu dilde yeni kelime önerileri, dilbilgisel varyasyonlar
veya stile uygun alternatifler üretilebilir:
Kelime türetme ve benzer kelime önerisi: Kullanıcı diline ait birkaç örnek kelime verildiğinde,
bir AI modelinden benzer yapıda yeni kelimeler üretmesi istenebilir. Nitekim bazı kullanıcılar
basit metin tamamlama AI araçlarıyla, oluşturdukları dile benzer kelimeler listesi elde
edebiliyorlar . Örneğin kullanıcı “ormak (n. orman)” gibi bir kelime girdiyse, AI’dan aynı kökten
fiil veya sıfat türetmesi veya benzer fonotik yapıda başka doğa kelimeleri önermesi istenebilir.
Çekim ve paradigma tamamlama: Kullanıcının tanımladığı bir çekim tablosu veya örnek
dilbilgisi kuralı varsa, AI bunu genelleyerek tabloyu tamamlayabilir. Reddit üzerinde AI
kullanımına dair bir örnekte, bir dilin fiil çekim tablosunun birkaç hali verilerek gerisini AI’ın
doldurduğu belirtiliyor . Benzer şekilde, “Bu dilde sıfatlar ‘u-’ öneki alır” şeklinde bir kural
verdiğinizde AI’a “peki zarflar nasıl işaretlenir?” diye sorarak kural önerisi alabilirsiniz. Bu tür bir
etkileşimli AI asistanı, dil yaratıcıya ilham verir ve varyasyon imkanlarını gösterir.
Örnek cümle ve kullanım önerileri: AI, kullanıcı dilinin tanımına dayanarak örnek cümleler
kurabilir veya mevcut cümleleri yeniden ifade edebilir. Bu, dilin pratik kullanımını görmek
açısından değerlidir. Örneğin GPT-4 modeline “Bu yapay dilde selamlaşma nasıl olabilir?” diye
sorulduğunda, tanımlanan sözcükler ve kurallara göre bir selam cümlesi üretebilir.
Entegrasyon Önerileri: Bu tür varyasyon önerileri için arka planda bir dil modeli API’si
kullanılabilir (OpenAI, AI21, veya açık kaynak modeller). Kullanıcı arayüzünde bir “Öneri Al”
butonu olup, kullanıcı bir kelime veya kural seçtiğinde AI’dan varyasyon istemek mümkündür.
Örneğin: “Kelime: boran (fırtına) – Benzer kelime önerileri al” dediğinde modelden anlamca veya
sesçe benzer birkaç uydurma kelime getirilebilir. Bu çıktıları doğrudan kabul etmek yerine
kullanıcıya sunup seçmesini sağlamak daha güvenlidir, zira AI çıktıları tutarlılık denetimine ihtiyaç
duyabilir . Ayrıca, modeli yönlendirmek için prompt mühendisliği yaparak dilin kurallarını
önden vermek önemlidir. Böylece AI, kullanıcının diline uygun ve onu bozmayan öneriler
sunabilir.
2. Dışa Aktarım Özellikleri
PDF ve JSON Formatında Dışa Aktarma
Oluşturulan dil bilgisini, sözlüğü veya kullanıcıya ait notları uygun formatlarda dışa aktarmak önemli bir
özelliktir. PDF formatı, düzenlenmiş bir rapor veya dil dokümanı sunmak için ideal iken JSON formatı
ham verileri (sözlük listesi, dil kuralları gibi) yapısal bir şekilde aktarmak için kullanışlıdır.
PDF olarak dışa aktarma: Web tarafında PDF üretmek için en yaygın yöntemlerden biri, jsPDF
gibi bir JavaScript kütüphanesi kullanmaktır. jsPDF ile tarayıcı içindeki verilerden programatically
bir PDF dosyası oluşturulabilir. Örneğin, jsPDF kullanarak metin ve basit şekiller eklemek ve
ardından doc.save("dosya.pdf") ile kullanıcının cihazına PDF indirmek mümkün .
Bir başka yaklaşım, HTML içeriğini PDF’ye dönüştüren html2pdf veya PDFMake kütüphanelerini
kullanmaktır. Bu kütüphaneler, mevcut sayfa içeriğini veya bir şablonu PDF’ye çevirebilir. Sunucu

tarafında ise Node.js tabanlı PDFKit veya Puppeteer ile PDF oluşturma seçenekleri var. Öneri
olarak, kullanıcı arayüzünde bir “PDF Olarak İndir” butonu konulup tıklandığında, kullanıcının
oluşturduğu dilin tüm tanımını ve örneklerini içeren bir rapor PDF’si jenerasyon kodu
•
14
•
14
•
•
15
•
16 17
3
çalıştırılabilir. PDF içerisinde dilin adı, ses bilgisi, örnek kelimeler ve cümleler, belki tablolarla
çekim örnekleri bulunabilir.
JSON olarak dışa aktarma: JSON formatı özellikle dil bilgisini diğer uygulamalara taşımak veya
verileri yeniden içe aktarmak için faydalıdır. Kullanıcının sözlük verisini (kelime, anlam, tür) veya
dil kurallarını JSON objeleri listesi şeklinde hazırlayıp indirmeye sunabilirsiniz. Tarayıcıda JSON
indirmek için, bir Blob nesnesi oluşturup içinde JSON.stringify ile üretilmiş metin tutarak,
bir gizli <a> etiketi aracılığıyla indirme işlemi yapılabilir . Örneğin:
const dataStr = JSON.stringify(myLanguageData);
const blob = new Blob([dataStr], {type: "application/json"});
const url = URL.createObjectURL(blob);
const link = document.createElement('a');
link.href = url;
link.download = "benim_dilim.json";
link.click();
URL.revokeObjectURL(url);
Bu şekilde kullanıcı tek tıkla JSON dosyasını indirebilir. Ayrıca, JSON çıktısı API entegrasyonu için de
kullanılabilir; örneğin başka bir uygulama bu JSON’ı okuyup dilin sözlüğünü kullanabilir. - Entegrasyon
Önerileri: PDF çıktısı için içeriğin düzeni önemlidir. Bu nedenle çıktı PDF’sinin bir şablona göre üretilmesi
önerilir (örneğin, HTML/CSS ile rapor şablonu hazırlayıp html2pdf ile dönüştürmek). JSON için, indirilen
dosyanın şema tanımını (örneğin {"words": [...], "grammar": {...}} gibi) dokümante ederek
kullanıcıların veya geliştiricilerin bu veriyi kolayca anlayıp kullanmasını sağlamak iyi olur. Her iki format
için de butonlar ve açıklamalar ekleyerek kullanıcıya neyi indireceğini net belirtmek gerekir (örn:
“Sözlüğü JSON indir” vs “Tam dil bilgisini PDF indir”).
Ses Dosyası (Audio) Olarak Dışa Aktarma
Kullanıcının oluşturduğu dildeki kelimelerin veya örnek cümlelerin telaffuzunu ses dosyası olarak dışa
aktarmak, dil yaratma deneyimini zenginleştirir. Bu sayede kullanıcı, dilini başkalarıyla paylaşırken
telaffuzları da sunabilir.
TTS API ile ses oluşturma: Dışa aktarım sırasında, seçilen kelime listesi veya cümle bir metin
olarak bir TTS (text-to-speech) servisine gönderilip dönen ses dosyası indirmeye hazır hale
getirilebilir. Örneğin, Google Cloud Text-to-Speech API’si bir metni okur ve Base64 kodlu ses
verisi döndürür . Bu veriyi çözerek bir MP3/WAV dosyası oluşturup kullanıcıya
verebilirsiniz. Benzer şekilde, IBM Watson TTS veya Amazon Polly de doğrudan MP3 çıktısı
verebiliyor. Uygulama tarafında, kullanıcı “ses dosyasını indir” dediğinde arka planda API çağrısı
yapılıp sonuç indirme linki olarak sunulabilir.
Web Audio + Recording yaklaşımı: Tarayıcı tabanlı bir çözüm olarak, Web Speech API kullanılıp
çıkan sesi Web Audio API ile yakalamaya çalışmak teoride mümkün görünse de pratikte
doğrudan desteklenmiyor . Bazı gelişmiş yöntemler ile tarayıcı içi ses, MediaRecorder
kullanılarak kaydedilebilir; ancak Text-to-Speech sesini MediaStream olarak almak zor
aolduğundan bu yöntem tavsiye edilmez. Bunun yerine, eğer istemci tarafında çalışacak bir
çözüm isteniyorsa, MediaRecorder mikrofon kaydı için daha uygun (kullanıcı kendi telaffuzunu
kaydedip yüklemesi gibi senaryolarda).
Açık kaynak araçlarla oluşturma: Sunucuya eSpeak gibi bir araç kurulup, komut satırı ile metni
ses dosyasına çevirerek (.wav ya da .mp3) kullanıcıya sunmak da mümkündür. Bu yaklaşım bulut
servis maliyetlerini ve internet gecikmelerini azaltır, ancak ses kalitesi doğal olmayabilir. Eğer
•
18 19
•
12 20
•
11
•
4



diliniz çok özel sesler içeriyorsa, eSpeak’in diline yeni fonemler eklemek gerekecektir ki bu ileri
düzey bir işlem. Basit Latin harfli telaffuzlar için eSpeak yeterli olabilir.
Entegrasyon Önerileri: Arayüzde, kullanıcı hangi içeriğin sesini indirmek istediğini seçebilmeli
(tek bir kelime mi, yoksa örnek cümleler mi). Örneğin sözlük sayfasında her kelimenin yanında
küçük bir “ses” butonu olup tıklayınca çalabilir ve “indir” ikonu ile kaydedilebilir. Teknik olarak, ses
dosyası üretildikten sonra bir blob URL ile kullanıcıya sunulabilir veya doğrudan bir indirme
başlatılabilir. Kalite ve boyut dengesine dikkat edilmeli: MP3 formatı genellikle uygun. Ayrıca,
kullanıcıya toplu bir ses paketi indirme imkanı da verilebilir (örn. tüm sözlük kelimelerinin
telaffuzlarını zip içinde). Eğer bulut TTS kullanılıyorsa, API anahtarları güvenli şekilde saklanmalı
ve kullanım kotaları göz önünde bulundurulmalıdır.
3. Ziyaretçi Paylaşım Alanı
Herkese Açık Galeri/Kütüphane Sayfası
Kullanıcıların oluşturduğu dilleri, diğer ziyaretçilerle paylaşabileceği herkese açık bir galeri sunmak,
topluluk etkileşimini artıracaktır. Bu sayfa, kayıtlı olsun olmasın tüm ziyaretçiler tarafından
görüntülenebilmelidir (sadece okuma amaçlı). Galeri sayfasının özellikleri ve örnekleri:
Genel erişim: Sayfa, platformda oluşturulan ve paylaşım izni verilmiş tüm dillerin bir listesini
sunar. Kulanıcılar giriş yapmadan bu listeyi gezebilir, dil detaylarını inceleyebilir. Bu yaklaşım,
Conlang Database gibi projelerde görülmüştür – gönüllülerin oluşturduğu dillerin arama
yapılabilir bir listesi herkese açıktır . Sizin platformunuzda da benzer bir “Topluluk Dilleri”
bölümü, oluşturulan dilleri keşfetmeyi kolaylaştırır.
Listeleme ve arayüz: Her dil için bir kart veya satır gösterilebilir. Bu kart üzerinde dilin adı,
yaratıcısının kullanıcı adı (ya da anonim tercih ettiyse anonim olarak), belki bayrak/ikon gibi bir
görsel temsil, kısaca tanım veya slogan yer alabilir. Örneğin ConWorkShop (CWS) sitesinde
kullanıcılar dillerini detaylıca girebiliyor ve başkaları bu detay sayfalarını görüntüleyebiliyor
(ancak CWS’de bu özellikler giriş gerektiriyordu) . Siz giriş gerektirmeden okuma izni
vereceğiniz için, dünyaya açık bir vitrin oluşacaktır.
Filtreleme ve arama: Galeri sayfasında dil ismine göre arama, yaratıcısına göre filtreleme, belki
dil tipi (ör. izole edici, çekimli, düzensiz vs.) ya da etkilendiği doğal dil ailelerine göre etiketlere
göre filtreleme yapmak kullanıcı deneyimini iyileştirir. Çok sayıda dil olduğunda sayfalandırma
veya sonsuz kaydırma da düşünülmelidir.
Örnek ve etkileşim: Her dil ögesi için bir “Detayları Gör” veya “Sözlüğe Bak” bağlantısı yer alır.
Ziyaretçi tıkladığında o dilin özel sayfasına gider (aşağıda paylaşım sistemi kısmında ele alınacak).
Ayrıca dil kartında bir beğenme/puanlama ya da yorum özelliği eklemek istenirse, bu kısım giriş
gerektirebilir veya anonim olarak yapılabilir ancak moderasyon ihtiyacı doğar. Basit tutmak
adına, başlangıçta sadece görüntüleme ve bağlantı paylaşma üzerine odaklanılabilir.
Paylaşım Sistemi ve Özel Bağlantılar
Kullanıcılar kendi oluşturdukları dili paylaşmaya karar verdiğinde, sistem onlara özel bir paylaşım imkanı
sunmalıdır. Bu, teknik olarak dil verisinin herkese açık hale gelmesi ve bir bağlantı (URL) ile erişilebilmesi
anlamına gelir.
Dil detay sayfası: Her dil için benzersiz bir URL olmalıdır, örneğin siteadresi.com/lang/
12345 veya dil ismine göre bir slug siteadresi.com/diller/elfce . Bu sayfada dilin
kapsamlı tanıtımı yer alır: ses bilgisi, örnek kelimeler, dilbilgisi özetleri, belki bir örnek metin veya
cümle. Kullanıcı isterse buraya bir kısa açıklama yazmış olmalıdır (örn: “Bu dil elf kökenli bir
fantastik dildir, SOV kelime dizimini kullanır…” gibi). Ayrıca dilin oluşturucusunun adı/rumuzu ve
oluşturma tarihi de belirtilebilir.
Örnek içerik ve medya: Paylaşılan dilin sayfasında en az bir örnek sözlük girişi veya örnek
cümle göstermek diğer ziyaretçiler için fikir vericidir. Örneğin dilin “merhaba” demek için
kullandığı kelime ve telaffuzunu, veya dildeki bir atasözü gibi ilgi çekici bir örnek konulabilir. Bu,
kullanıcı dilini paylaşırken sisteme ekleyebileceği bir alana dönüştürülebilir (“Örnek cümle gir
(isteğe bağlı)” gibi).
Bağlantı paylaşımı: Kullanıcı, dilini yayınladıktan sonra oluşan URL’yi kopyalayıp sosyal medya
veya arkadaşlarıyla paylaşabilir. Bu URL’ye tıklayan herkes ilgili dil sayfasını görecektir. Burada


dikkat edilmesi gereken, kullanıcı dilini güncelledikçe bu sayfanın da güncellenmesidir (veya
kullanıcı yayınladıktan sonra üzerinde değişiklik yapamayabilir, politika kararına bağlı).
Muhtemelen kullanıcı her düzenlemeden sonra “Değişiklikleri Yayınla” gibi bir aksiyon ile
paylaşılan sayfasını güncel tutmak isteyecektir.
Güvenlik ve moderasyon: Herkese açık içerik sunarken, kötüye kullanımı engellemek için bazı
önlemler alınmalı. Örneğin uygunsuz kelimeler veya içerikler konusunda bir bildirim/şikayet
mekanizması konulabilir. Otomatik dil yaratma sitesinde bu risk düşük olsa da kullanıcıların
serbest metin girdiği açıklama alanlarında toksik içerik olabilir. Bu nedenle dil sayfalarında
“Şikayet Et” butonu veya içerik filtreleme (küfür engelleme gibi) düşünülebilir.
Örnek mevcut çözümler: ConWorkShop platformu, her kullanıcıya dilini ayrıntılı biçimde girip
saklama ve bir profil altında sergileme imkanı verir (yalnız okunması için hesap gerekebiliyor)
. FrathWiki veya Linguifex gibi wikiler de kullanıcıların dillerini herkesin okuyabileceği
maddeler halinde paylaşmasına izin verir. Sizin durumunuzda wiki yerine özel olarak
yapılandırılmış bir sayfa olacağı için gezinme ve sunum daha kontrolünüzde olacaktır. İyi bir
sunum için dilin önemli özelliklerini başlıklar altında formatlı göstermek (örn: “Dil Aile: Yapay /
Kelime Dizimi: SOV / Sesletim: 5 sesli, 18 ünsüz” gibi bir özet tablo) ziyaretçinin bilgi almasını
hızlandırır.
Entegrasyon Önerileri: Bu paylaşım alanını gerçekleştirmek için veritabanında her dil kaydına bir
“public” bayrağı eklenebilir. Kullanıcı paylaş dediğinde, dil verileri bu bayrakla işaretlenir ve galeriye
düşer. URL yapısı olarak rastgele kimlikler yerine okunaklı slug’lar da üretmek mümkün (örn dil ismi
benzersizse). Front-end tarafında, bir “Topluluk Galerisi” menü linki ekleyerek herkesin bu alana
ulaşmasını sağlayın. Dil detay sayfasında da gerekirse JSON/PDF indirme linkleri sunularak dışa aktarım
özellikleri entegre edilebilir, böylece diğer meraklılar dilinizi indirip inceleyebilir. Tabi bunun için kullanıcı
izni önemlidir; paylaşırken “başkalarının indirmesine izin ver” seçeneği de sorulabilir.
4. Mobil Uyumluluk ve Erişilebilirlik
Mobil Uyumlu Tasarım (Responsive Design)
Gelişmiş Dil Yaratıcı arayüzünün, masaüstü kadar mobil cihazlarda da sorunsuz kullanılması
hedeflenmelidir. İyi bir responsive tasarım, farklı ekran boyutlarına otomatik uyum sağlayarak kullanıcı
deneyimini tutarlı kılar. Bunu başarmak için dikkate alınacak en iyi uygulamalar:
Mobil-öncelikli yaklaşım: Tasarıma en küçük ekranlardan (telefonlar) başlayarak daha büyük
ekranlara doğru ilerlemek önerilir . Yani öncelikle telefon için basit ve dikey akışlı bir düzen
tasarlanır, sonra tablet ve masaüstü için bu düzen genişletilir. Bu sayede temel işlevler küçük
ekranda sorunsuz çalıştığı için, büyük ekranda alan arttığında sadece ekstra iyileştirmeler
yapmak yeterli olur.
Esnek grid ve layout sistemleri: CSS Flexbox ve Grid kullanarak düzen kurmak, farklı boyutlar
için esnekliği arttırır. Örneğin, masaüstünde yan yana görünen paneller, mobilde alt alta akacak
şekilde bir grid tanımlanabilir. Modern CSS layout teknikleri, akıcı ve kırılmayan arayüzler
•
22
•
23
•
6


oluşturmayı kolaylaştırır . Bir örnek olarak, üç sütunlu bir sözlük listesi masaüstünde güzel
dururken, tablette iki sütuna, telefonda tek sütuna düşecek şekilde grid ayarlanabilir (CSS
grid-template-columns: repeat(auto-fit, minmax(...)) kullanımı ile yapılabilir ).
Bu şekilde içerikler her zaman ekrana uygun boyutta görünür.
CSS media query kullanımı: Belirli kırılım noktalarında ( breakpoint ) tasarımı değiştirmek için
media query’lerden yararlanın . Yaygın kırılım noktaları: 576px (küçük telefonlar), 768px
(tablet), 992px (küçük laptop) ve 1200px (masaüstü) gibi değerlere göre düzenlenebilir. Örneğin
768px altında menülerin gizlenip “hamburger menu” dediğimiz butonla açılır hale gelmesi yaygın
bir pratiktir. Media query tanımlarken mümkün olduğunca yüzde ve esnek birimler (%, em, rem)
kullanmak, farklı ekran yoğunluklarında daha orantılı sonuç verir .
Dokunmatik etkileşimler: Mobil cihazlarda kullanıcılar parmaklarıyla etkileşim kurar, bu yüzden
buton ve linklerin yeterince büyük ve aralıklı olması gerekir. Önerilen minimum dokunmatik
hedef boyutu genellikle 40-48 piksel çapındadır. Örneğin dil oluşturma formundaki butonlar ve
seçim alanları, küçük ekranlarda tam genişlikte ve yeterli yükseklikte olmalıdır. Ayrıca kaydırma
(scroll) davranışları dikey yönde doğal olmalı, yatay kaydırma mümkün olduğunca kaçınılmalıdır
(tabloları taşırmamak gibi).
Performans ve görseller: Mobil cihazlar için görsellerin optimize edilmiş boyutlarda sunulması
önemlidir. srcset ve <picture> etiketi kullanarak yüksek çözünürlüklü ekranlar için keskin,
düşük bant genişliği durumları için daha ufak dosya boyutlu görüntüler sunabilirsiniz .
Ayrıca gereksiz kütüphanelerden kaçınarak, sayfa yüklenme süresini düşük tutmak mobil
deneyimi iyileştirir.
Erişilebilirlik İpuçları
Web uygulamasının erişilebilir olması, farklı engel gruplarından kullanıcıların da aracı kullanabilmesini
sağlar. Bu kapsamda WCAG standartları rehber alınarak aşağıdaki konulara odaklanılmalıdır:
Yüksek kontrastlı tasarım: Metin ile arka plan rengi arasında yeterli kontrast olduğundan emin
olun. Düşük kontrast, görme zorluğu çeken veya renk körlüğü olan kullanıcılar için metinleri
okunaksız kılabilir. Genel kural, normal metinler için en az 4.5:1 kontrast oranını sağlamaktır.
Örneğin koyu bir arka plan üzerinde açık renkli metin (veya tersi) kullanın; siyah-beyaz en yüksek
kontrasttır . Yeşil-kırmızı veya mavi-sarı gibi problemli kombinasyonlardan kaçının . Ayrıca,
sadece rengi anlam iletmek için kullanmamaya özen gösterin (örneğin “kırmızı hata, yeşil başarı”
bilgisini renk körü kullanıcı kaçırabilir; bunun yanında ikon veya yazı ile de belirtmek gerekir).
Alternatif metinler ve semantik HTML: Sitede kullanılan tüm görseller için açıklayıcı alt metin
değerleri girilmeli ki ekran okuyucu kullanan görme engelli kullanıcılar içeriği anlayabilsin.
Örneğin dilin bir bayrağını gösteriyorsanız alt metni “Elfçe dilinin bayrak simgesi” gibi
tanımlayabilirsiniz. Form ve buton etiketleri de anlamsal olmalı; ikonlu bir buton varsa (örneğin
ses simgesi) butonun aria-label="Telaffuzu dinle" gibi bir özelliği olmalı ki amaç
anlaşılabilsin. Başlıklar ( <h1>...<h6> ) hiyerarşik yapıya uygun kullanılmalı, sayfa içindeki
bölümleri mantıksal olarak ayırmalıdır. Bu şekilde screen reader kullanıcıları hızlıca bölümler
arasında gezinebilir.
Klavyeyle gezinme ve odak sırası: Tüm etkileşimli öğelerin (linkler, butonlar, form girişleri)
klavye ile ulaşılabilir olduğundan emin olun. Kullanıcı sadece Tab tuşu ile gezinerek siteyi
kullanabilmeli. Odak ile seçilen elemanın etrafında net bir gösterge (focus outline) olmalıdır .
Tarayıcılar varsayılan olarak odaklanan elemana bir mavi çizgi/kenarlık çizer; bunu CSS ile
görünmez yapmaktan kaçının . Hatta daha belirgin hale getirmek için :focus durumunda
stil ekleyebilirsiniz (örneğin kalın turuncu bir çerçeve gibi). Sayfada çok sayıda link varsa, en başa
“Ana İçeriğe Atla” şeklinde gizli bir bağlantı eklemek, klavye kullanıcılarının menülerü tek tek
geçip zaman kaybetmesini önler . Bu link, odaklanınca görünür hale gelerek kullanıcının ana
•
24
25
•
26 27
28
•

•
29 30
•
31 32
•

•
33
34
35
7






İçeriğe Atla" şeklinde gizli bir bağlantı eklemek, klavye kullanıcılarının menülerü tek tek
geçip zaman kaybetmesini önler . Bu link, odaklanınca görünür hale gelerek kullanıcının ana

ARIA ve bileşen erişilebilirliği: Eğer açılır menü, modal pencere, sekme (tab) gibi özel JavaScript
bileşenleri kullanıyorsanız, ARIA etiketleri ile bunları tanımlayın. Örneğin, açılır dil seçimi
menüsü yapıyorsanız, butona aria-haspopup="true" ve menü listesine uygun role atamak
gibi. Ayrıca bu bileşenlerin klavye kontrollerine uygun olması (örneğin ok tuşları ile menüde
gezinebilmek, ESC ile modaldan çıkabilmek) gerekir . WAI-ARIA Authoring Practices rehberi,
yaygın bileşenlerin nasıl erişilebilir yapılacağı konusunda detaylı örnekler sunar.
İçerik ölçeklenebilirliği: Kullanıcılar tarayıcı ölçekleme veya cihaz ayarlarından metin boyutunu
büyütebilir. Tasarımınız bu durumda bozulmamalı. Yüzde ve rem kullanımı burada da faydalıdır;
sabit piksel yerine esnek boyutlar kullanarak %200 yakınlaştırmada dahi kullanılabilir bir arayüz
hedefleyin. Metinler taşmamalı, konteynerlar içinde akmalıdır.
Entegrasyon Önerileri: Geliştirme sürecinde erişilebilirlik test araçlarından faydalanın (ör. axe DevTools,
Lighthouse). Sayfayı bir ekran okuyucu (NVDA, JAWS veya VoiceOver) ile test ederek, önemli işlemlerin
(yeni dil oluşturma formu doldurma, dil sayfasını okuma vs.) sesli mantıklı aktarıldığını kontrol edin.
Klavye ile tüm buton ve alanlara ulaşılabildiğini, odak sırasının mantıklı (DOM sırasına uygun) olduğunu
doğrulayın. Renk kontrastı için tasarım aşamasında belirlenen paleti WebAIM’in kontrast denetleyicisiyle
test edebilirsiniz. Son olarak, mümkünse gerçek kullanıcı testleriyle görme veya işitme engelli
bireylerden geri bildirim almak, uygulamanızı gerçekten erişilebilir kılmak için en değerli adımdır.
