🌟Buffer-Based Anti-Vibration UAV Leaf Detection System
Bu proje; otonom tarım dronlarının (İHA/UAV) havada süzülürken rüzgar, motor ve pervane etkisiyle yaşadığı mekanik titreşim (sarsıntı) ve hareket bulanıklığı (motion blur) sorununu çözmek amacıyla geliştirilmiş arabellek
tabanlı bir bilgisayarlı görü (computer vision) sistemidir.

📌 Projenin Amacı ve Çalışma Mantığı
Dronlar havada sabit kalmaya çalışırken sürekli olarak mikroskobik veya makroskobik titreşimler üretir. Bu durum, kameranın anlık olarak odaklanmasını zorlaştırır, görüntüyü bulandırır ve canlı yaprak analizlerinde yüksek
oranda hatalı tespite (false positive/negative) yol açar.
Bu yazılım, sorunu aşmak için Arabellek Tabanlı Gecikmeli Analiz (Buffer-Based Delayed Analysis) yöntemini kullanır:

[Drone Kamerası] ──► [Anlık Görüntü (Canlı Akış)] ──►[5 Saniyelik FIFO Arabellek (RAM)]
                                                                           |
            [Kararlı Yaprak Analizi] ◄── [Titreşimi Sönümlenmiş Kare] ◄────┘

1. FIFO Kuyruğu (First-In-First-Out): Drone kamerası saniyede örneğin 30 kare (FPS) çekerken, bu görüntüler anlık olarak RAM üzerinde tutulan 5 saniyelik bir kuyruğa (collections.deque) aktarılır.
2. Yeniden Oynatma ve Kararlı Analiz: Sistem canlı yayını kesintisiz olarak ekranda akıtırken; analiz motoru, dondaki anlık sarsıntılardan etkilenmeyen tam 5 saniye önceki kareyi arabellekten geri çağırır (tekrar oynatır).
3. Mekanik Filtreleme: 5 saniyelik gecikme, dronun anlık rüzgar hamlelerini ve ani irtifa düzeltmelerini yazılımsal olarak sönümler. Böylece analiz motoruna her zaman daha kararlı, odaklanmış ve net kareler gönderilir.

🛠️ Teknik Özellikler
Titreşim Sönümleme: RAM şişmesini önleyen otonom halka arabellek (deque) mimarisi.
Bilateral Filtreleme: Standart bulanıklaştırma yerine kenar keskinliğini koruyan bilateral filtre ile yaprak damar sınırlarının korunması.
Gelişmiş Morfoloji: Yaprak üzerindeki güneş yansımalarını ve gölgeleri egale eden kapatma (CLOSE) ve açma (OPEN) filtreleri.
Gecikmeli Telemetri Ekranı: Kullanıcıya eşzamanlı olarak hem anlık canlı yayını hem de 5 saniye önceki stabilize edilmiş analiz karesini gösteren çift ekran arayüzü.

<img width="1797" height="952" alt="image" src="https://github.com/user-attachments/assets/e3c59c38-95c0-4080-99b2-f5a4b2b31b3d" />


