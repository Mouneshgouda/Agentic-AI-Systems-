## Conversational AI And ChatBot



### Text TO speech

<img width="1024" height="820" alt="image" src="https://github.com/user-attachments/assets/5f29e466-32fd-4594-89ee-b99fb7d2700a" />


```python
pip install gtts
```

```python
from gtts import gTTS
from IPython.display import Audio
text = input("Enter the text to convert to speech: ")
tts = gTTS(text=text,lang='ta',tld='co.in',slow = True)
tts.save("output.mp3")
Audio("output.mp3", autoplay=True)

```
## Text To Translate

<img width="592" height="249" alt="image" src="https://github.com/user-attachments/assets/4716c6da-da7f-4661-8e8e-51f941748394" />


```python
!pip install googletrans==4.0.0-rc1 #google translation
```

```python
#translation service googletrans
from googletrans import Translator
tran = Translator()
# Assign a sample text for translation to avoid the error
text_to_translate = "Hello, how are you?"
tran = tran.translate(text_to_translate,src='auto',dest='ka') #en
print(tran.text)
```

### image TO Text

<img width="1238" height="1434" alt="image" src="https://github.com/user-attachments/assets/5f14fb9b-7c17-4f06-b72b-e741d0439e25" />

```python
!pip install pytesseract #for google lens like ocr
```

```python
from PIL import Image
import pytesseract
img = Image.open('/content/Gemini_Generated_Image_2f6ckc2f6ckc2f6c.png')
text = pytesseract.image_to_string(img)
print(text)
```

```

