# Multi Channel Audio Source
Multi Channel Audio Source designed to handle multiple sound plays in short time effectively.
Check the Demo Scene and Demo Video to see how it works.

Now available from [Unity's Asset store.](https://assetstore.unity.com/packages/tools/audio/multi-channel-audio-source-120749).

## Terms
"Attribute" in this documentation means member value of Class. Please don't confuse from C# Attributes.

## Updates
### 1.1
- Supports Dynamic Length for Channels.
- Supports AudioSourceProxy.

## Getting Started
Using Multi Channel Audio Source is really easy.
All you have to do is just add "MultiChannelAudioSource" component that you want to play sound, and use the method it provides.

## Example
First you have to add MultiChannelAudioSource Component.

```clike
private MultiChannelAudioSource audioSource;

void Start() {
    audioSource = GetComponent<MultiChannelAudioSource>();
}
```

By the way, you can wait until MultiChannelAudioSource is ready by checking Initialized value.

```clike
if(audioSource.Initialized) {
    Debug.Log("Is Initialized");
}
else {
    Debug.Log("It's not Initialized");
}
```

After get reference of MultiChannelAudioSource, you can play the sound with invoke methods.

```clike
audioSource.PlayAtSequence(audioClip);
```

Check the Demos in Demos folder to see how it works.

## API
### public class MultiChannelAudioSource
#### public int ChannelLength [New From 1.1]
Return Length of current channels or set new channel length. If new channel Length is smaller than old channel length, remaining audiosources will be deleted automatically.

#### public bool Initialized [New From 1.1]
Returns true if MultiChannelAudioSource initialized.

#### public AudioSource GetChannel(int idx)
Return specified index of Sound Channel(=AudioSource).

#### public void Play(int idx, AudioClip audioClip)
Play audioClip with specified Sound Channel.

#### public void PlayOneShot(int idx, AudioClip audioClip)
Use PlayOneShot method to play audioClip with specified Sound Channel.

#### public void Stop(int idx)
Stop current playing sound in specified Sound Channel. Note that you can't stop the sound if you used PlayOneShot.

#### public void PlayAtSequence(AudioClip audioClip[, int channelCount])
Play audioClip with using internal AudioSources sequentially. channelCount parameter is optional, you can specify the number of channel counts you want to use.

#### public void PlayOneShotAtSequence(AudioClip audioClip[, int channelCount])
Same as PlayAtSequence, using PlayOneShot internally instead of Play.

### public class AudioSourceProxy [New From 1.1]
AudioSourceProxy class helps you to initialize custom audioSource attributes easily. Without this, you have to update each property manually.

You can set the desired AudioSource to copy properties, or manually change the value directly. Note that Not all values will be copied because of usage of MultiChannelAudioSource, like "Loop", "Play On Awake", "AudioClip".

#### public AudioSource source
Set the source of AudioSource to copy properties. This is optional value, if it's null, update Channels with own properties.

#### public AudioMixerGroup output
#### public bool bypassEffects
#### public bool bypassListenerEffects
#### public bool bypassReverbZones
#### public int priority
#### public float volume
#### public float pitch
#### public float stereoPan
#### public float spatialBlend
#### public float reverbZoneMix

#### public void UpdateChannels()
Update changes of any property must be call this method to update all channels(AudioSources).


## FAQ
### How to update the properties in each Audio Source(Sound Channel)?
You can access to each Audio Source by using GetChannel(idx). However I will add for visual UI features to handle that later.

### Next Sound keep interrupt my previous Sound
Increase the length of the channel.

### Sound doesn't played well when using PlayOneShotAtSequence
Yes, so I'm not recommend to use PlayOneShotAtSequence. Try PlayAtSequence with more channels until you get satisfied result. If the term between the sound play is super short, try consider using Looping sound.

## Migration Guides
### 1.0 -> 1.1
From 1.1, I decided to remove "ChannelLength" in inspector because this value controls array of AudioSource internally but user can update directly through Unity's inspector and it brokes behaviours.

Instead, I exposed another value named "Starting Length", for initialize starting channel numbers same as before ChannelLength do.

Only you have to do is update "Starting Channels" value to your desired value, because the default is 2 so you may changed previous Channel Length value to something different.

## License?
Free to use. If you have any suggestion, send me a mail to: rico345100@gmail.com

## Buy me a coffee!
Donations are big help for me to continue my development!

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=PVXTU5FJNBLDS)
