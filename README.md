## Mid-Report on GAN

### Cyclegan

+ [This](https://github.com/leimao/Voice_Converter_CycleGAN) model implement Cyclegan on VCC2016 Dataset. The model itself takes **coded spectral numpy array** as input, which is slightly different from spectrogram.

> This model works well on Tesla K80 (which costs $296/monthly) while each epoch takes around 1min40s. **TODO MARK: ** replace the proprecess part with librosa package.**

+ [This](https://github.com/sumuzhao/CycleGAN-Music-Style-Transfer) model implement Cyclegan on a dataset with 3 types of samples, including jazz, pop, and classic. The model itself take midi information as input.

+ [This](https://openreview.net/forum?id=S1lvm305YQ) model implement a pipeline together with Cyclegan. In brief, the model firstly select CQT/STFT to generate rainbowgram/spectrogram, then train a Cyclegan to transfer style, and lastly use a Wavenet as a decoder to recover waveform from gram.

> The code itself is not available. From my perspective, if we'd like to combine these two black boxes together, there may well be some potential issues to consider.

### Stargan
Stargan could be viewed as a conditioned Cyclegan. The model itself take multiple domains as input and use only one generator to generate conditioned target domains. From my perspective, the model is limited since you have to ensure that there's a possible mapping between these domains along all the dimensions of the features.

+ [This](https://github.com/hujinsen/StarGAN-Voice-Conversion) model is the one I focus on right now. The model itself import a doamin-classifer on discriminator and generate target with a conditioned domain provided. 

**Doubts**
> Tiny dataset on one instrument  

- [] The model itself now take pitch as the condition attribute. In other words, domains are classified by pitches. Then, during the testing phase, you have to clearly classify the pitch of input. **The model's performance will probably rely on the accuracy of this classification.(Upper bound exists)**

- [] As an alternative, we could take the difference between the source and target domain as the condition attribute (For example, pitch from C to D, D to E, E to F# will use the same model since the difference is 2). However, I got stuck on this issue and haven't found reasonable model to console this problem.

> Generalized dataset on various instruments  

- [] If transferring the model on NSynth dataset, the model will have to initial around 1280 specific domains where 128 counts the total number of pitches and 10 counts the total number of main instruments. Could the model itself generalize that large scale of domains?

**TODO List** 

- [] Modify preprocess.py, use librosa to transform between spectrograms and waveforms.
	- [] Try different transformation like STFT(or spectrogram), Constant-Q, or something else.
- [] Have the model run on a tiny dataset which contains various pitches on only one instrument
