<img width="1230" alt="image" src="https://github.com/sezaras85/Sentient-ai/blob/main/sentient%20resim.png" />

Sentient Foundation, topluluklara Sadık AI yaratmaları için güç vererek AI'da yeni bir çağın öncülüğünü yapıyor: Topluluk tarafından oluşturulmuş, toplulukla uyumlu ve topluluk tarafından sahiplenilmiş. Açık kaynaklı AI teknolojilerini ilerletmeye ve merkezi olmayan, şeffaf bir ekosistem oluşturmaya kendini adamış bir kar amacı gütmeyen kuruluş olarak, AI oluşturucularının kilit paydaşlar olduğu bir Açık AI ekonomisini savunuyor. Şimdi, Sentient AI projesinin Sentient'in Dobby-70B API'sini kullanarak Ubuntu sistemiyle Python kullanarak bir yapay zeka robotu nasıl yaratabileceğimizi görelim.


```markdown
# Sentient AI Dobby-70B ile Yapay Zeka Robotu

Bu proje, Sentient AI'nin Dobby-70B API'sini kullanarak Ubuntu üzerinde Python ile bir yapay zeka robotu oluşturmayı amaçlamaktadır. Firework AI sitesinden alınan API anahtarı ile Dobby-70B modeliyle etkileşime geçebilirsiniz.

## Gereksinimler

- **Ubuntu** işletim sistemi (tercihen en son sürüm).
- **Python 3.8 veya üzeri**.
- **pip** (Python paket yöneticisi).
- **Firework AI** hesabı ve API anahtarı.

## Kurulum Adımları
**. Gerekli Yazılımların Kurulumu**

Ubuntu sisteminizde gerekli yazılımları kurmak için aşağıdaki adımları izleyin:

- **Python ve Pip Kurulumu**: Python ve pip'in sisteminizde yüklü olduğundan emin olun. Eğer yüklü değilse, aşağıdaki komutları kullanarak kurabilirsiniz:

  
```bash
  sudo apt update
  sudo apt install python3 python3-pip

### 1. Firework AI'den API Anahtarı Alma

1. [Firework AI](https://firework.ai) web sitesine gidin.
2. Hesabınıza giriş yapın veya yeni bir hesap oluşturun.
3. **API Keys** bölümüne gidin ve yeni bir API anahtarı oluşturun.
4. Oluşturulan API anahtarını güvenli bir yere kaydedin.

### 2. Python Ortamının Hazırlanması

1. Terminali açın ve Python ve pip'in kurulu olduğunu kontrol edin:
   ```bash
   python3 --version
   pip3 --version
   ```
2. Gerekli Python kütüphanelerini yükleyin:
   ```bash
   pip3 install requests
   ```

### 3. Proje Dosyasını Oluşturma

1. Proje dizininde bir Python dosyası oluşturun:
   ```bash
   nano ai_robot.py
   
   ### 3. Proje Dosyasını Oluşturma
   
2. Aşağıdaki Python kodunu dosyaya ekleyin:
   ```bash
   
import os
import requests
from dotenv import load_dotenv

# API anahtarını güvenli bir şekilde yükle
load_dotenv()
API_KEY = os.getenv("FIREWORKS_API_KEY")

API_URL = "https://api.fireworks.ai/inference/v1/chat/completions"

# Fireworks AI’ye mesaj gönderen fonksiyon
def chatbot(prompt):
    headers = {
        "Authorization": f"Bearer {API_KEY}",
        "Accept": "application/json",
        "Content-Type": "application/json"
    }

    data = {
        "model": "accounts/sentientfoundation/models/dobby-unhinged-llama-3-3-70b-new",
        "max_tokens": 1024,
        "top_p": 1,
        "top_k": 40,
        "presence_penalty": 0,
        "frequency_penalty": 0,
        "temperature": 0.6,
        "messages": [{"role": "user", "content": prompt}]
    }

    response = requests.post(API_URL, json=data, headers=headers)

    if response.status_code == 200:
        return response.json().get("choices")[0].get("message").get("content")
    else:
        return f"API Hatası: {response.text}"

# Kullanıcıdan giriş al ve API'ye gönder
if __name__ == "__main__":
    print("Sentient AI Chatbot'a hoş geldiniz! (Çıkmak için 'exit' yazın)")
    while True:
        user_input = input("Sen: ")
        if user_input.lower() == "exit":
            break
        response = chatbot(user_input)
        print(f"Bot: {response}")

   ```
4. Dosyayı kaydedin ve kapatın (`Ctrl + X`, ardından `Y` ve `Enter`).


### 4. Projeyi Çalıştırma

1. Terminalde aşağıdaki komutu çalıştırarak Python scriptini başlatın:
   ```bash
   python3 ai_robot.py
   ```
2. Artık Dobby-70B API'si ile etkileşime geçebilirsiniz. Kullanıcı girdilerinizi yazabilir ve Dobby'nin yanıtlarını görebilirsiniz.
3. 

<img width="1230" alt="image" src="https://github.com/sezaras85/Sentient-ai/blob/main/sentient%203.png" />
