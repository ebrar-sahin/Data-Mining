Proje Konusu: Aktivite ve Zaman Dilimine Göre Kişisel Müzik Tercihlerinin Sınıflandırılması  <br>

1. Problem Tanımı ve Motivasyon  <br>
Bu projede, bireysel müzik dinleme alışkanlıklarının belirli bağlamlara (yapılan aktivite ve günün saati) 
göre nasıl değiştiği problemi ele alınmıştır. Müzik platformlarının (Spotify, Apple Music vb.) öneri 
sistemlerinin temelini oluşturan bu problem, kullanıcı deneyimini iyileştirmek adına "doğru zamanda 
doğru içeriği sunmak" açısından önemlidir. Projenin amacı, kullanıcının o anki durumuna (Örn: Ders 
çalışıyor veya tatilde) ve zaman dilimine bakarak dinleyeceği müzik türünü tahmin eden bir model 
geliştirmektir. <br>
2. Veri Toplama Süreci  <br>
Veri seti, kişisel dinleme geçmişine dayalı olarak manuel yöntemlerle oluşturulmuştur. Veri seti 
toplamda 284 örnekten (instances) oluşmaktadır. Veri setinde her bir satır; o an yapılan eylemi, 
zaman dilimini ve dinlenen şarkıyı temsil etmektedir. Kullanılan temel değişkenler şunlardır: <br>
• Aktivite: (Ders, Tatil, Spor, Ulaşım vb.) <br>
• Saat_Dilimi: (Sabah, Öğle, Akşam, Gece) <br>
• Müzik_Turu: (Pop, Rock, Rap, R&B vb.) <br>
3. Veri Ön İşleme ve Temizleme  <br>
Veri seti Orange Data Mining platformuna yüklenmiş ve "File" bileşeni üzerinden analiz edilmiştir. Ön 
işleme aşamasında şu adımlar izlenmiştir: <br>
• Değişken Rollerinin Belirlenmesi: "Müzik_Turu" özniteliği Target (Hedef), "Aktivite" ve 
"Saat_Dilimi" öznitelikleri Feature (Özellik) olarak atanmıştır. "Sarki_Adi" ise modellemeye 
katılmaması için Meta veri olarak işaretlenmiştir. <br>
• Kirli Veri Tespiti: Analiz sırasında "Saat_Dilimi" sütununda, bir zaman dilimi olmayan "Yaz" 
ifadesinin yer aldığı tespit edilmiştir. Bu durumun veri giriş hatasından kaynaklandığı (kirli veri) 
anlaşılmış ve modelin doğruluğu için bu verilerin filtrelenmesi veya düzeltilmesi gerekliliği 
raporlanmıştır. <br>
4. Keşifsel Veri Analizi (EDA)  <br>
Veri setinin yapısını anlamak için Tree Viewer kullanılarak görselleştirme yapılmıştır.  <br>
• Aktivite Baskınlığı: Müzik tercihini belirleyen en temel faktörün "Saat" değil, "Aktivite" olduğu 
gözlemlenmiştir. Örneğin, "Tatil" aktivitesinde saat fark etmeksizin baskın türün "Pop" olduğu 
görülmüştür. <br>
• Zamanın Etkisi: "Ders Çalışma" gibi aktivitelerde zamanın belirleyici olduğu; gece çalışırken 
"Progressive", gündüz çalışırken "R&B" dinlendiği saptanmıştır. <br>
• Sınıf Dağılımı: Veride "Pop" müzik türünün diğerlerine göre daha sık tekrarlandığı ve veri 
setinde dengesizlik (imbalance) olabileceği gözlemlenmiştir. <br>
5. Uygulanan Veri Madenciliği Yöntemi  <br>
Bu proje bir sınıflandırma problemi olduğu için Karar Ağaçları (Decision Tree) algoritması tercih 
edilmiştir. Karar ağaçlarının seçilme nedeni, modelin ürettiği kuralların ("Eğer şu aktiviteyse ve saat 
şuysa, sonuç budur" şeklinde) insanlar tarafından kolayca yorumlanabilir ve açıklanabilir olmasıdır. <br>
• Model Parametreleri: Aşırı öğrenmeyi (Overfitting) engellemek için ağaç derinliği (max depth) 4 
ile sınırlandırılmış ve her yaprakta en az 2 örnek olması şartı koşulmuştur. <br>
6. Deneysel Sonuçlar ve Değerlendirme  <br>
Model performansı, 5-katlı çapraz doğrulama (5-fold Cross Validation) yöntemi ile "Test and Score" 
bileşeni üzerinden ölçülmüştür. Elde edilen sonuçlar şöyledir:  <br>
• AUC (Area Under Curve): 0.825 – Bu değer, modelin sınıfları birbirinden ayırma yeteneğinin 
yüksek olduğunu ve modelin başarılı bir sınıflandırma yaptığını göstermektedir. <br>
• CA (Classification Accuracy): 0.426 – Hedef değişken (Müzik Türü) çok fazla sınıfa (Pop, Rock, 
Rap, TSM, Klasik vb.) sahip olduğu için, nokta atışı doğruluk oranı %42.6 seviyesindedir. Ancak 
AUC skorunun yüksekliği, modelin doğru tahminlere çok yaklaştığını göstermektedir. <br>
7. Tartışma ve İyileştirme Önerileri  <br>
Çalışmanın temel kısıtı, veri setindeki örnek sayısının (284) azlığı ve bazı sınıfların (müzik türlerinin) 
çok az örneğe sahip olmasıdır ("Least common class has only 1 instance" uyarısı alınmıştır).  <br>
• İyileştirme 1: "Yaz" gibi hatalı veri girişleri temizlenerek model tekrar eğitilmelidir. <br>
• İyileştirme 2: Örnek sayısı artırılmalı ve az dinlenen müzik türleri "Diğer" kategorisinde 
birleştirilerek sınıf dengesizliği giderilmelidir. <br>
8. Sonuç  <br>
Bu proje ile kişisel veriler kullanılarak başarılı bir öneri sistemi prototipi oluşturulmuştur. Orange Data 
Mining aracı kullanılarak ham veriden anlamlı kurallar (Örn: Gece çalışırken odaklanma müziği tercih 
edilmesi) çıkarılmıştır. Oluşturulan karar ağacı, kişinin yaşam tarzına uygun tahminler yapabildiğini 
kanıtlamıştır. <br>
9. Ekler<br>
10. <img width="845" height="466" alt="image" src="https://github.com/user-attachments/assets/4134f4d8-4766-40e6-bedf-98839c9acf24" /> <br>
<img width="832" height="456" alt="image" src="https://github.com/user-attachments/assets/6af125a0-01d9-4b77-95a1-d17a03cdccc0" /> <br>
<img width="827" height="448" alt="image" src="https://github.com/user-attachments/assets/75a3c2b4-462e-4f97-bffc-99ed9c16b4d7" /> <br>


