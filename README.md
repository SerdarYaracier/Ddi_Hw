# İstenilen Animeye göre Benzerini Önerme Uygulaması

Bu ödev 2023-2024 yılı güz dönemi Doğal Dil İşleme Dersi için hazırlanmıştır.

Ödevin asıl amacı derste kullanılan yöntemlerin analiz edilmesi ve bu bilgilerle bir proje tasarlanmasıdır.

# Neden Bu Programa İhtiyaç Vardır?

1) Günümüz anime sektöründe genel olarak bir anime hakkında birden çok içerik çıkar. Bu içerikler genel olarak 1. sezon, 2. sezon gibi geleneksel isimlendirmelere sahip olmazlar. Her sezona özel bir isim verilir. Sezonlar dışında da serinin ana hikayesini etkileyen filmler de bulunmaktadır. İşte bu noktada bir kullanıcı için bir serinin tüm elemanlarını bulmak zor olmakadır. Bu program bu iş için gayet uygundur. Sisteme serinin bir sezonunun tam adı yazıldığında sistem kalan verilerin de bu ada benzediğini fark edip kalanlarını da kullanıcıya gösterecektir.

2) İnsanlar beğendiği bir içeriğe benzer içerikler tüketmek eğilimdedirler. Örneğim sci-fi izlemekten hoşlanan bir insan rom-com ya da sitcom tarzı içeriklerden genelde hoşlanmaz. İşte bu yüzden de diğer sci-fi içeriklerine yönelme eğiliminde olur. Bu program ise o kişiye istediği eğilimdeki verileri bulmasında büyük bir rol oynamaktadır.

# Ödevi Yapan Kişiler
Serdar Yaracıer

# Veri setini elde etmek

İnternet üzerinden biri siteden hazır bir veri seti alınmıştır. Projedeki tüm veriler bu veri seti içerisinden  elde edilmiştir.

# Veri Seti Hakkında Genel Bilgi

Veri seti içerisinde 12064 satır ve 6 sütun barındırmaktadır.Her bir satır her bir veri hakkkında bilgiler içermektedir.

Stünlarda anime_id	name	type	episodes	rating ve	members olacak şekilde sütunlar vardır. anime_id, her verinin kendine özgü id'sini belirtir.

type ise verinin türünü belirtirken episodes bahsi geçen anime verisinin kaç bölümden oluştuğunu; rating, puanlamasını; members iste kaç kişi tarafından takip edildiğini göstermektedir.

![Ekran görüntüsü 2024-01-10 183752](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/58a537b9-32b5-4570-a4cb-310bf90cbe9f)

# Kullanılan Kütüphaler

![Ekran görüntüsü 2024-01-10 184113](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/218edc15-5017-4869-8fab-fe9ae0664887)

# Boş verilerden kurtulmak

İlk aşamada veri setimizde boş olan verileri yok etmekle başlıyoruz.Bunun için df.isna().sum() komutlarından yardım alıyoruz.
![Ekran görüntüsü 2024-01-10 185451](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/ffad4c11-c10e-48ed-b19e-ff9ce4e29419)


Kodumuzda boş veriler olduğunu öğrendik şimdi ise bunlardan kurtulmak için ne yapmamız gerektiğine bakalım. Bu aşamada df.dropna(inplace=True) kodunu kullanıyoruz. Bu kod satırı bizim için boş olarak gördüğü yerlerin silinmesini sağlıyor. Daha sonrasında ise df.isna().sum() koutları ile tekrar bir kontrol gerçekleştirip boş değerlerin temizlendiğinden emin oluyoruz.
![Ekran görüntüsü 2024-01-10 185315](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/bce4f08a-0e8e-4052-93e7-9ca9037abe99)

# Sütunlarda Sıralama Yapmak
siralanacak_sutun = 'anime_id'

df_sirali = df.sort_values(by=siralanacak_sutun) şeklinde basit bir kodla istenen sütünları sıralamak oldukça mümmkündür. Bu sayede isteyen kullanıcı veri setindeki en iyi puanlı animeyi, en  fazla bölüm sayısına sahip animeyi kolaylıkla bulabilecektir.


![Ekran görüntüsü 2024-01-10 190655](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/53258e07-4939-42f6-bfc2-d523445bc9ba)

# Benzerlik Hesaplama
  Benzerlik hesaplamaları yapılırken kullancağımız ana method tf_idf matrisi oluşturmaktan geçmetedir. TF-IDF matrisi, belgelerdeki anahtar kelimeleri belirlemede, belgelerin benzerliğini ölçmede ve belge sınıflandırmada kullanılabilir. Bu sayede istediğimiz benzerlik durumunu sağlamış olacağız.
  #
  Tf_idf oluşturması için gerekli kodlar yazılmıştır. Sözlük oluşturulmuş, matrisler hazırlanmıştır.
  ![Ekran görüntüsü 2024-01-10 192441](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/7bc1af28-c21e-4936-8ddc-469bfbd2b96e) 
  
  Bu sayede kelimeler Sözlüğe eklenmiştir.

  ![Ekran görüntüsü 2024-01-10 192722](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/cbe97393-68d4-467e-8112-6200d15eeebc)

  Tf oluşturulmuştur.
  #
  Benzerliği bulmak için öncelikle adını verdiğimiz animenin birkaç özelliğini daha bulmamız daha iyi olacaktır. Bu sayede Tf_idf'ten daha iyi bir şekilde yararlanmış olacağız. Ayrıca bu kod parçasından daha sonra benzer animeleri printlemesi için de yaralanacağız. Bu işlem için gerekli kod parçası aşağıda belirtilmiştir:

  ![Ekran görüntüsü 2024-01-10 195844](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/c76abb0b-3cc3-4b6a-9d6c-92e51e8058c1)

  #
Artık istediğimiz aşamaya geldik. Benzer bulma işlemini gerçekleştirebileceğiz. Kodun ilk segmentinde benzerini istediğimiz verinin adı yazdırılıyor. 2. segmentinde ise tf_idf yardımı ile beraber ağırlık hesapları ve kelime benzerlikleri sorgulanıyor. Bu sayede elde etmek istediğimmiz verilere bir adım daha yaklaşmış oluyoruz. En son segmentinde ise bir önceki segmentte bulduğumuz komutları ekrana yazdırıyoruz. 

  
![Ekran görüntüsü 2024-01-10 194155](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/7e712289-60ce-4cd6-9fc6-b615605c8235)

Artık neticeye ulaştık. Programımız başarılı bir şekilde adını girdiğimiz verilere göre benzer özelliklerde animeler önerebiliyor.

![Ekran görüntüsü 2024-01-10 200212](https://github.com/SerdarYaracier/Ddi_Hw/assets/116540913/5250d261-aadc-4c86-bb2c-9c65e3edc240)
