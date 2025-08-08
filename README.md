# Terapist Botu (n8n + Google Gemini + Telegram)

Bu proje, **n8n** üzerinde çalışan ve **Telegram** aracılığıyla kullanıcıyla etkileşime giren bir **empatik terapist chatbot** iş akışıdır.  
Bot, gelen mesajın ruh halini analiz eder, uygun bir empatik yanıt oluşturur ve kullanıcıya geri gönderir.

---

## 📌 Özellikler

- **Telegram entegrasyonu** – Kullanıcı mesajlarını Telegram üzerinden alır.
- **Ruh hali analizi** – Mesajdaki duygusal tonu belirler (üzgün, stresli, kararsız, mutlu, nötr).
- **Empatik cevap üretimi** – Önce duyguyu kabul eden, ardından motive eden kısa bir yanıt verir.
- **Google Gemini (PaLM) API** ile LLM desteği.
- **n8n AI Agent** ile özel prompt tabanlı yanıt formatı.

---

## 📂 Akış Adımları

1. **Telegram Trigger**
   - Telegram botundan gelen mesajları yakalar.
   - `message.text` alanındaki kullanıcı mesajını işleme gönderir.

2. **AI Agent**
   - Özel prompt ile kullanıcının ruh halini analiz eder.
   - Yanıt formatı:
     1. Duyguyu anladığını belirten cümle
     2. Cesaret verici/motive edici öneri
   - Tonlama kuralları:
     - Üzgün → Nazik ve umut verici
     - Stresli → Güven verici ve motive edici
     - Kararsız → Netlik kazandırıcı
     - Mutlu → Kutlayıcı ve enerjik
     - Nötr → Hafif pozitif

3. **Google Gemini Chat Model**
   - `gemini-2.5-pro` modeliyle mesajı işler.
   - AI Agent node’una bağlı çalışır.

4. **Send a text message**
   - AI Agent tarafından üretilen `output` değerini Telegram üzerinden kullanıcıya gönderir.

---

## ⚙️ Gereksinimler

- **n8n** (self-hosted veya bulut sürümü)
- **Telegram Bot API Token**
- **Google Gemini (PaLM) API anahtarı**
- `@n8n/n8n-nodes-langchain` paketinin kurulu olması

---

## 🔑 Kurulum

1. **Telegram Bot Oluşturma**
   - [BotFather](https://t.me/BotFather) ile yeni bot oluştur.
   - API token'ı al.

2. **Google Gemini API**
   - [Google AI Studio](https://makersuite.google.com/) üzerinden API anahtarını al.
   - n8n'de **Google Gemini (PaLM) Api account** olarak kaydet.

3. **n8n’e İş Akışını İçe Aktarma**
   - JSON dosyasını n8n'e yükle.
   - Telegram Trigger node’una bot API bilgilerini gir.
   - Google Gemini Chat Model node’una API bilgilerini ekle.

4. **Çalıştırma**
   - İş akışını **Active** durumuna getir.
   - Telegram botuna mesaj göndererek test et.

---

## 📤 Yanıt Örneği

**Kullanıcı:**  
> Son zamanlarda çok stresliyim, işler üst üste geliyor.

**Bot:**  
> Seni anlıyorum, bu kadar yükün üst üste gelmesi yorucu olabilir. 🌿  
> Unutma, her şey adım adım çözülebilir, kendine biraz nefes alanı tanı.

---

## 📌 Notlar

- Yanıtlar **2-3 cümle** ile sınırlı tutulur.
- Gerektiğinde hafif emoji kullanılır.
- Bot **teşhis koymaz**, yalnızca destekleyici öneriler sunar.
- Profesyonel yardım gerektiren durumlarda kullanıcıyı yönlendirmeniz önerilir.
