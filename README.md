Angular Portfolio: Cloud & Docker Deployment
Bu depo, Angular tabanlı statik bir portfolyo sitesinin GitHub Pages üzerindeki statik yayınından DigitalOcean bulut altyapısı üzerinde Docker konteyner teknolojisi kullanılarak gerçekleştirilen gelişmiş dağıtım sürecine geçişini ve yapılandırmalarını içermektedir.
Proje, bulut bilişim ve konteyner tabanlı dağıtım kavramlarının pratik olarak uygulanmasını amaçlayan bir ders/ödev çalışması kapsamında hazırlanmıştır.

Uygulama, Angular framework’ü ile geliştirilmiş Single Page Application (SPA) mimarisine sahip statik bir portfolyo sitesidir.
- HTML, CSS ve JavaScript tabanlı derlenmiş dosyalardan oluşur
- ng build işlemi yerel ortamda gerçekleştirilmiştir

Bu nedenle uygulama, yalnızca statik içerik sunumu yapan hafif bir web sunucusu (Nginx) ile çalıştırılmaktadır.

Proje Mimarisi
Uygulama, istemci taraflı çalışan Angular SPA ile bulut üzerindeki konteynerize edilmiş sunum katmanının entegrasyonuna dayanmaktadır.
Uygulama: Angular SPA (Single Page Application).
Sunum: Nginx Web Server (Alpine tabanlı hafif imaj).
Konteynerizasyon: Docker Engine.
Bulut Altyapısı: DigitalOcean Droplet (Ubuntu 22.04 LTS).

User Browser
|
Public IP
|
DigitalOcean Droplet (Ubuntu 22.04 LTS)
|
Docker Container
|
Nginx Web Server
|
Angular Static Files

Dağıtım Stratejisi: Single-Stage Build
Bu depoda, sunucu kaynaklarını (CPU/RAM) verimli kullanmak amacıyla Single-stage Docker Build yaklaşımı tercih edilmiştir.
1 GB RAM kapasiteli sanal sunucu üzerinde yüksek kaynak tüketen npm install ve ng build süreçlerini çalıştırmak yerine işlem yükünü minimize edderek uygulama yerel ortamda derlenmiş ve üretim ortamına hazır (production-ready) statik dosyalar halinde depoya aktarılmıştır.

Dağıtım Adımları (Deployment)
Sunucu üzerinde uygulamanın ayağa kaldırılması için izlenen adımlar:

Deponun Klonlanması:
git clone https://github.com/kullanici-adi/depo-adi.git
cd depo-adi

Docker İmajının Oluşturulması: Depo içerisinde yer alan Dockerfile, Nginx Alpine imajını temel alarak statik dosyaları paketler.
sudo docker build -t angular-portfolio .

Konteynerin Çalıştırılması: 
sudo docker run -d -p 80:80 --name portfolio-container angular-portfolio
