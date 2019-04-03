## Mid-Report on GAN

### Cyclegan

+ [This](https://github.com/leimao/Voice_Converter_CycleGAN) model implement Cyclegan on VCC2016 Dataset. The model itself takes **coded spectral numpy array** as input, which is slightly different from spectrogram.

> This model works well on Tesla K80 (which costs $296/monthly) while each epoch takes around 1min40s. **TODO MARK: ** replace the proprecess part with librosa package.

+ [This](https://github.com/sumuzhao/CycleGAN-Music-Style-Transfer) model implement Cyclegan on a dataset with 3 types of samples, including jazz, pop, and classic. The model itself take midi information as input.

+ [This](https://openreview.net/forum?id=S1lvm305YQ) model implement a pipeline together with Cyclegan. In brief, the model firstly select CQT/STFT to generate rainbowgram/spectrogram, then train a Cyclegan to transfer style, and lastly use a Wavenet as a decoder to recover waveform from gram.

> The code itself is not available. From my perspective, if we'd like to combine these two black boxes together, there may well be some potential issues to consider.

### Stargan
Stargan could be viewed as a conditioned Cyclegan. The model itself take multiple domains as input and use only one generator to generate conditioned target domains. From my perspective, the model is limited since you have to ensure that there's a possible mapping between these domains along all the dimensions of the features.

+ [This](https://github.com/hujinsen/StarGAN-Voice-Conversion) model is the one I focus on right now. Hope it works.