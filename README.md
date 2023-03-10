<h2>Person Swap </h2>


<!--<div id="content-main">-->
<h3>Info how to use system and how models works </h3>

<h3>Changing the photo (face)</h3>
<p><span style="font-weight: 400;">4 models (files) are used to change the face:</span></p>
<ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">Detector - checks if a face exists in a given photo and cuts it out if it does;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Recogniser - extracts the facial features from the cropped photo to be used for the change;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Generator - Creates a new face from the facial features of the source face to the facial expression of the target;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Mask detector - extracts the facial contour mask during the face change in the source photo (you can use libraries in CV2 anyway), but the model is more accurate as far as I have noticed.</span></li>
</ol>
<p><span style="font-weight: 400;">Generator operation - the recognition model extracts the identity of the face in the photo (Ts for source or Tt for target).</span></p>
<p><span style="font-weight: 400;">The face change itself is performed by the generator, which consists of:</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">The encoder - extracts the features of the target face;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Identity Change Module - transfers the identity extracted from the source image to target photo features;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Decoder - reconstructs a modified image of target photo features and source identity.&nbsp;</span></li>
</ul>
![](docs/img.png)
<p>&nbsp;</p>
<p>&nbsp;</p>
<h3>Changing the sound (voice)</h3>
<p><span style="font-weight: 400;">The paddlespeech library is used, which can use existing or newly developed models for voice replacement. The models used for voice replacement in the project are:</span></p>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">Speech to text:</span></li>
</ul>
<ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">Transformer - text is extracted from the source audio;</span></li>
</ol>
<ul>
<li style="font-weight: 400;"><span style="font-weight: 400;">Text to speech</span></li>
</ul>
<ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">Phonetics class - converts text to phonetic data;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Encoder - extracts features of the target voice;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Acoustic model - matches the features of the source text with the features of the target sound;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Vocoder - text features converted to voice by the target voice features.</span></li>
</ol>
![](docs/voice_schema.png)
<p>&nbsp;</p>
<p><span style="font-weight: 400;">Changing the video (face and/or voice):</span></p>
<ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">Separates the audio of the target video (if it exists);</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">If the source is a video, the first frame containing the person is taken (if the source is a photo, nothing is done);</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">Changes the face in the video (if the source is a photo or video):</span></li>
<ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">Repeat over each frame;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">changing the face in the frame (photo) (as in an ordinary photo);</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">the new frame (target photo with the face of the source) is saved in the list);</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">after iteration, the list of frames is converted into a video;</span></li>
</ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">Voice in the video is changed (if the source is a video or audio file):</span></li>
<ol>
<li style="font-weight: 400;"><span style="font-weight: 400;">If the target or source did not have a voice - do nothing</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">If there is only the voice of the target, it is added to the created video;</span></li>
<li style="font-weight: 400;"><span style="font-weight: 400;">If there is both a source and a target voice - the source's voice is replaced by the target's voice (as in voice replacement).</span></li>
</ol>

</ol>
![](docs/video_schema.png)
<p>&nbsp;</p>
<p><span style="font-weight: 400;">&nbsp;</span></p>
<!--</div>-->

