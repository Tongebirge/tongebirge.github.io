# Simple Drum sampler

6ch one-shot sampler.
Tested on Seeed studio's XIAO board. and works other SAMD21 board.

## Background
I am tried make to Mr.HAGIWO's [1100円で作るTR-808/909 サンプルプレイヤードラムモジュール-モジュラーシンセ自作｜HAGIWO/ハギヲ｜note](https://note.com/solder_state/n/n0209d16d0d08) .

However, it was unstable in my environment, so I tried to fix the code,
Almost everything will be newly I made.

Here's the difference from his great program:
* Removed OLED.
* 6ch output.
* Removed libraries.
* Changed delay() to micros() timer.

## About
### Triggers
A trigger voltage of 1.5V or higher is required.
Rather than simply judging digitalRead
An array of bits is created from the input values, and the bit mask defined at the beginning is used for judgment.
The number of bits refers to the number of decision cycles.
For example, if 4 cycles are required for judgment, define as follows:

`0x00001111`

### Samples

The sample data should be compact.
This is stored in samples.h as an 8-bit byte array.
First, convert the sample to PCM(RAW) with Audacity, SoundForge or etc.
For Audacity, export in "Other Format" and select Unsigned 8bit, RAW (header less).
Also, the audio must be monaural and within 0.5 seconds.
Once the RAW file is complete, it's time to convert it to a HEX array.
You can use something like [File to hex converter](http://tomeko.net/online_tools/file_to_hex.php?lang=en).

Paste the converted array into the defined array.
Paste each in samples.h where it `// ....`

```cpp
const uint8_t samples_A [] PROGMEM =
{
  // ....
}
```

~~The sample program contains the sample I created with ES2.~~
I find it more renaissance to use PCM drum machine samples than analog machines such as the 808 and CR-78.
For personal (not commercial) enjoyment, you can convert and use Linn and Oberheim bin files published on the net.

### Testing
I used only XIAO, 1k resistors and 0.1uF capacitors when testing this program. But I recommend building a circuit like HAGIWO if you want to integrate it into your Eurorack system. It works well even if it is diverted as it is.

My case:
```
[XIAO] pin 0-> 220ohm-> 1uF-> GND
                   | --------------> OUTPUT
```

## ToDo
This program was written during the holidays, so there are still many features I would like to add.
Here are some ideas for future prospects.
If possible, I would be grateful if you could give me a pull request.

* Volume and Frequency POT (working)
* Input trigger polarity  function


## Acknowledgment
It's almost an original program,
I thought about forking in honor of Mr. HAGIWO who inspired me,
He didn't publish the code on GitHub, I published a new one.
And this is a simple code, I will publish it under CC0.
