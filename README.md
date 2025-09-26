# Intel Image Classification (ResNet18 - Transfer Learning)

## Proje Özeti
Bu projede Kaggle Intel Image Classification veri seti kullanılarak 6 farklı sınıfın (buildings, forest, glacier, mountain, sea, street) sınıflandırılması hedeflenmiştir. Transfer learning ile ResNet18 modeli uygulanmıştır.

## Veri Seti ve Ön İşleme
- Veri seti: 17k train, 3k test görsel.
- Train/Valid bölünmesi: %90 / %10
- Augmentation: RandomResizedCrop, HorizontalFlip, ColorJitter, Rotation
- Normalizasyon: ImageNet mean/std

## Model ve Eğitim Süreci
- Model: ResNet18 (önceden eğitilmiş, son katman değiştirilmiş)
- Optimizer: AdamW, lr=3e-4
- Loss: CrossEntropy (label smoothing=0.05)
- Scheduler: CosineAnnealingLR
- Mixed precision (FP16) + Early stopping

## Sonuçlar
- Best Valid Accuracy: **94.8%**
- Test Accuracy: **93.4%**
- Eğitim / Valid loss-accuracy grafikleri:
  ![Training Curves](images/training_curves.png)
- Confusion Matrix:
  ![Confusion Matrix](images/conf_matrix.png)
- Misclassified örnekler:
  ![Misclassified](images/misclassified.png)
- Grad-CAM:
  ![Grad-CAM](images/gradcam.png)

## Hiperparametre Taraması
- lr, batch size, dropout kombinasyonları denendi
- En iyi kombinasyon: **lr=1e-4, batch=32, dropout=0.5** (Val Acc ≈ 94.2%)

## Sonuç ve Gelecek Çalışmalar
Model yüksek doğrulukla sınıflandırma yapabilmiştir. Glacier ve Mountain sınıfları zaman zaman karışmaktadır. Gelecek çalışmalarda MixUp/CutMix, daha büyük backbone (ResNet34, EfficientNet) ve daha uzun eğitim stratejileri uygulanabilir.

## Kaggle Notebook
[Notebook Linki](https://www.kaggle.com/code/glhedakzlhan/notebookd439d6ff92)
