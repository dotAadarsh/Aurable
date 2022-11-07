### Aurable  - A one stop place for audio analysis!
[![Open in Gitpod](https://gitpod.io/button/open-in-gitpod.svg)](https://gitpod.io/#https://github.com/dotaadarsh/Aurable)

#### What it does?
Aurable is an app that provides the analysis on the uploaded audio by the user. It includes   transcript, translation feature, summary, and export option.

#### How its been built?
- The UI is powered by [Streamlit](https://streamlit.io/), which turns data scripts into shareable web apps and its all in Python.
- For the input part, we need a file uploader option which allows user to upload the audio file. [`st.file_uploader`](https://docs.streamlit.io/library/api-reference/widgets/st.file_uploader) accomplishes it by providing an upload widget.
- Now to the audio analyzing part - [Deepgram](https://deepgram.com/) is an end-to-end Deep Learning ASR offering real-time transcription platform. It provides features includes transcription with understanding for diarization, summarization, language detection, topic detection, and more.
- Below is a snippet for `Transcribe an Existing File or Pre-recorded Audio` example from the [Deepgram's Python SDK](https://github.com/deepgram/deepgram-python-sdk)
```
from deepgram import Deepgram
import asyncio, json

DEEPGRAM_API_KEY = 'YOUR_API_KEY'
PATH_TO_FILE = 'some/file.wav'

async def main():
    # Initializes the Deepgram SDK
    deepgram = Deepgram(DEEPGRAM_API_KEY)
    # Open the audio file
    with open(PATH_TO_FILE, 'rb') as audio:
        # ...or replace mimetype as appropriate
        source = {'buffer': audio, 'mimetype': 'audio/wav'}
        response = await deepgram.transcription.prerecorded(source, {'punctuate': True})
        print(json.dumps(response, indent=4))

asyncio.run(main())
```

- By processing the above code, we will get the response from the Deepgram's API. Now all we need to do is using the response to whatever we want. 
- Lets translate the transcript - [itranslate](https://pypi.org/project/itranslate/) is a library which helps to translate the text and also it's free. Below is a example of how to process the text with it. The response will be the translated text.
```
from itranslate import itranslate as itrans
itrans("test this and that")  # '测试这一点'

# new lines are preserved, tabs are not
itrans("test this \n\nand test that \t and so on")
# '测试这一点\n\n并测试这一点等等'

itrans("test this and that", to_lang="de")  # 'Testen Sie das und das'
itrans("test this and that", to_lang="ja")  # 'これとそれをテストします'
```
- Now to the exporting the transcript part. [`fpdf`](https://pypi.org/project/fpdf/) - library for PDF document generation under Python. All we need to do is create a new file, set some params like font, size and style, then send the transcript to it, to write into the file. It will generate the PDF. 
- The final part is building the UI, components like st.text, st.text_input, st.expander and others are used. Check out the [Streamlit API reference](https://docs.streamlit.io/library/api-reference) for more info. 
- To run this project, click on the Open in Gitpod to run it instantly. Dont forget to replace the `DEEPGRAM_API_KEY` with yours API - Get yours at - https://console.deepgram.com/signup 

#### Links
- [Live project URL](https://aurable.streamlit.app/)
- [Video Demo](https://youtu.be/EVSjYezUu2I)
