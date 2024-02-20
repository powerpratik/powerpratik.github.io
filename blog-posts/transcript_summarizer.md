<!--Hello World! Argument1 value: transcript_summarizer-->
## The Meeting Marathon: Sprinting Through Hours in Minutes
Imagine the all-too-familiar marathon of attending a meeting, where every word feels like a mile, and you, the diligent participant, decide to record the whole thing. It's a brilliant plan—until you cross the finish line, look at the recording, and realize it's a marathon in itself, too daunting to revisit. The thought of replaying it feels like preparing for another race when you've barely caught your breath. Deadlines loom like checkpoints, and time is a relentless competitor. You need a way to sprint through the recording, capturing the essence without running the whole course again.

Enter the game-changer: a summary, a sprinter's dream. Yet, transforming a transcript into a concise summary can feel like preparing for a sprint without knowing the track. Sometimes, the hurdle is even higher when you're working with just the audio, no transcript in sight. Fear not, for there's a secret weapon in your kit: an open-source API from OpenAI, known as Whisper AI.

In this post, we'll explore how to leverage recorded video—be it from local storage or online platforms like YouTube—extract its transcript, and then distill it into a potent summary. It's like having your personal coach that guides you through the marathon of information, ensuring you're always leading the pack in the summarization relay. With Whisper AI in your corner, you're not just staying in the game; you're changing it. Welcome to the top of your summarization game, where hours become minutes, and every word counts.

The post is divided into sections to explain how my script leverages the already available tools to summarize your meetings. I also have a bonus part where you can even use the summary generated and feed into another API to have a virtual actor read out the summary in news like format in a video. 
We will be using many available tools like GPT, whisper, D_ID to acheive all this with a single script that connects it all. 


### Transcribing Audio
The journey begins with extracting an audio transcript from your video recording. Whether it's an enlightening talk from YouTube or a significant meeting stored locally, the choice is yours. Flexibility is key, allowing you to summarize content that matters most to you. Among the plethora of transcription tools available, we'll focus on OpenAI's Whisper model for its impressive performance and compatibility with GPT, another OpenAI marvel.

The process unfolds in two main tasks:

- **Task 1: Obtain the Video File**
  - Obtain the video from YouTube or a local path, creating a temporary file for the video and extracting the audio. Tools like Pytube (my preference) or youtube-dl are excellent for this purpose.

- **Task 2: Transcribe the Audio**
  - With the audio extracted, we harness the power of Whisper AI to transform our audio file into a text transcript, leveraging the model's pretrained capabilities for accuracy and efficiency.

<!-- ![Transcribe Method](./images/transcribe_method.png "Transcribe Method"){width = 25%} -->
<img src="./images/transcribe_method.png" alt=" Transcribe Method " width="75%"/>

### Generating Summary Response
Armed with the transcribed text, our next mission is to distill this information into a concise summary. Thanks to the prowess of NLP models, particularly GPT-based transformers, this task is handled with precision and nuance, capable of distinguishing between different speakers in the transcript.

To leverage GPT for summarization, ensure you have developer access and an API key from OpenAI. With these in hand, the documentation guides you through generating a summary of your transcript.

<!-- ![Get GPT Method](./images/get_gpt_response.png "Get GPT Method"){width = 25%} -->
<img src="./images/get_gpt_response.png" alt=" Get GPT Method " width="75%"/>

### Optional: Generating Video of the Response
Imagine elevating your summary with a touch of flair, presenting it through a virtual actor. This not only enhances your presentation but also adds a creative twist to your projects. Achievable with another tool, Clips from D_ID, this feature requires an API key obtained from creating a free account on their platform. With the summarized text and API key, Clips transforms your summary into a video, narrated by a virtual actor.

<!-- ![Generating Video Response](./images/video_generation_method.png "Generating Video Response"){width = 25%} -->
<img src="./images/video_generation_method.png" alt=" Generating Video Response " width="75%"/>

Isn't it remarkable to streamline the process from a recorded meeting or a YouTube video to audio transcription, summarization, and even video generation into a single automated script?

For a comprehensive guide from local audio extraction to video actor generation, visit my GitHub repository:

[GitHub - Video Summarization with Digital Actors](https://github.com/powerpratik/video_summarization_with_digital_actors/tree/main)

---
 
