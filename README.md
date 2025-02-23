<img width="1230" alt="image" src="https://github.com/sezaras85/Sentient-ai/blob/main/sentient%20resim.png" />

Sentient Foundation is pioneering a new era in AI, empowering communities to create Loyal AI—community-built, community-aligned, and community-owned. As a non-profit committed to advancing open-source AI technologies and building a decentralized, transparent ecosystem, its champion an Open AI economy where AI builders are key stakeholders. Now let's see how we can create an artificial intelligence robot using Python with the Ubuntu system using the Sentient's Dobby-70B API of the Sentient AI project.


```markdown
# Sentient AI Dobby-70B ile Yapay Zeka Robotu

Bu proje, Sentient AI'nin Dobby-70B API'sini kullanarak Ubuntu üzerinde Python ile bir yapay zeka robotu oluşturmayı amaçlamaktadır. Firework AI sitesinden alınan API anahtarı ile Dobby-70B modeliyle etkileşime geçebilirsiniz.

## Gereksinimler

- **Ubuntu** işletim sistemi (tercihen en son sürüm).
- **Python 3.8 veya üzeri**.
- **pip** (Python paket yöneticisi).
- **Firework AI** hesabı ve API anahtarı.

## Kurulum Adımları

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
   ```
2. Aşağıdaki Python kodunu dosyaya ekleyin:
   ```python
   import requests

   # Firework AI'den aldığınız API anahtarını buraya ekleyin
   API_KEY = 'YOUR_API_KEY_HERE'
   API_URL = 'https://api.firework.ai/v1/dobby-70b'

   def send_message_to_dobby(message):
       headers = {
           'Authorization': f'Bearer {API_KEY}',
           'Content-Type': 'application/json'
       }
       data = {
           'prompt': message,
           'max_tokens': 150
       }
       response = requests.post(API_URL, headers=headers, json=data)
       if response.status_code == 200:
           return response.json()['choices'][0]['text']
       else:
           return f"Error: {response.status_code}, {response.text}"

   if __name__ == "__main__":
       while True:
           user_input = input("You: ")
           if user_input.lower() in ['exit', 'quit']:
               break
           response = send_message_to_dobby(user_input)
           print(f"Dobby: {response}")
   ```
3. Dosyayı kaydedin ve kapatın (`Ctrl + X`, ardından `Y` ve `Enter`).

### 4. Projeyi Çalıştırma

1. Terminalde aşağıdaki komutu çalıştırarak Python scriptini başlatın:
   ```bash
   python3 ai_robot.py
   ```
2. Artık Dobby-70B API'si ile etkileşime geçebilirsiniz. Kullanıcı girdilerinizi yazabilir ve Dobby'nin yanıtlarını görebilirsiniz.
