# Türkçe Kitap Tanıtım Yazılarından Yazar Tahmini

Bu projede, kitap tanıtım yazısından kitabın Sabahattin Ali'ye mi yoksa Stefan Zweig'a mı ait olduğu tahmin edilir. İki farklı Bayes yöntemi kullanılmıştır:

1. **Bölüm 1 (lab4):** Elle yazılmış Markov zinciri modeli (kelime sırası dikkate alınır)
2. **Bölüm 2 (lab5):** sklearn ile CountVectorizer + MultinomialNB (kelime torbası)

Notebook: `kitap_yazar.ipynb`

## Veri
Kaggle: Turkish Book Dataset
https://www.kaggle.com/datasets/ardaakdere16/turkish-book-dataset


## Yapılanlar

### Ortak hazırlık
1. CSV okundu (yaklaşık 218 bin satır). Dosyanın büyük kısmı boştu.
2. Boş, 50 karakterden kısa ve tekrar eden tanıtım yazıları elendi.
3. İki yazar seçildi: Sabahattin Ali (109 kitap, etiket 0) ve Stefan Zweig (100 kitap, etiket 1).
4. Metin temizlendi: küçük harfe çevrildi (Türkçe I/İ doğru), noktalama silindi, yazarın adı metinden çıkarıldı. Ad silinmeseydi model yazarın adını okuyarak tahmin yapardı.

### Bölüm 1: Markov modeli (lab4)
1. Her tanıtım yazısı cümlelere bölündü, her cümle bir örnek sayıldı (toplam 1829 cümle).
2. Cümleler %80 eğitim (1463), %20 test (366) olarak ayrıldı (random_state=42).
3. Eğitim verisinden en sık geçen 3000 kelimeyle bir sözlük yapıldı. Her kelimeye bir numara verildi, sözlükte olmayan kelimeler <UNK> oldu.
4. Her yazar için iki tablo hesaplandı: cümlenin hangi kelimeyle başladığı (pi) ve bir kelimeden sonra hangisinin geldiği (A). Tablolar 1'le başlatıldı (düzeltme), normalize edildi, logaritması alındı.
5. Her yazarın prior olasılığı hesaplandı (cümle sayısı oranı).
6. Bir cümlenin her yazara ait olma log olasılığı hesaplandı, büyük olan seçildi.

### Bölüm 2: Naive Bayes (lab5)
1. Her tanıtım yazısı bir örnek olarak alındı (209 kitap), %80 eğitim (167), %20 test (42).
2. CountVectorizer ile kelime sayılarına çevrildi (7994 kelimelik sözlük).
3. MultinomialNB eğitildi, doğruluk ve F1 skoru hesaplandı.
4. Kendi yazdığımız iki örnek cümle test edildi: ikisi de doğru yazara atandı.
5. Belirli bir kelimenin hangi kitaplarda geçtiği aranıp incelendi.

