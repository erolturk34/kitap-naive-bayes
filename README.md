# kitap-naive-bayes
# Türkçe Kitap Tanıtım Yazılarıyla Naive Bayes

Kitap tanıtım yazılarından kitabın kategorisini ve yazarını tahmin eden
Multinomial Naive Bayes projesi.

## Veri
Kaggle: Turkish Book Dataset
https://www.kaggle.com/datasets/ardaakdere16/turkish-book-dataset
CSV dosyasını indirip notebook ile aynı klasöre koyun.

## Yöntem
Temizleme → CountVectorizer → MultinomialNB → F1, confusion matrix

## Sonuçlar
- Kategori tahmini (5 sınıf): doğruluk %81,9, macro F1 0,71
- Yazar tahmini (10 yazar): doğruluk %87,0, macro F1 0,86

## Not
Yazar tahmininde yazar adı metinden silindi. Model üslubu değil konu ve
tanıtım kalıplarını öğrenir, bu yüzden sonuçlar gerçek üslup analizi değildir.

## Çalıştırma
pip install pandas numpy scikit-learn matplotlib
Notebook'u Jupyter'de açıp hücreleri sırayla çalıştırın.

