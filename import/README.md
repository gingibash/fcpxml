# import u avscript

## scenario 1 - media bin / multi clip

1. snimatelj, montažer ili novinar, u projekt, uploadaju jedan ili više clipova
2. clipovi idu u projektni media bin
3. pravimo `<resources>` strukturu
    - `<format>` konstruiramo iz MediaInfo.txt ili iz video metadata
    - clipove definiramo s `<asset-clip>`
    - konstruiramo `<effect>` ako dalje radimo sa `<title>`

[primjer XML](https://github.com/gingibash/fcpxml/blob/master/import/scenario-1.xml)

---
## scenario 2 - compound clip
1. snimatelj/montažer pravi 
    1.  compound clip u fcpx-u
    1.  XML export iz fcpx 
    1.  referentni video "kobasicu" mp4 (_avs-referentna-kobasica.m4v_)
2. u avscript uploadaju se 
    1.  XML 
        1. spremimo ``<resources>`` - neophodan nam je kako bi prilikom exporta sačuvali compound
    1.  referentni video (__ref_video__)
        1. čitamo MediaInfo.txt ili metadata (duration, framerate)
    1.  radi se provjera (__moraju biti identični__)
        - `<resources><sequence>` _duration_ i __ref_video__ _duration_
        - `<resources><format>` _frameDuration_ i __ref_video__ _FrameRate_

[primjer XML](https://github.com/gingibash/fcpxml/blob/master/import/scenario-2.xml)




##### [Time value attributes](https://developer.apple.com/library/archive/documentation/FinalCutProX/Reference/FinalCutProXXMLFormat/StoryElements/StoryElements.html#//apple_ref/doc/uid/TP40011227-CH13-SW2)

Attribute | Description
------ | ------
offset | An element’s location in parent time (or base element’s time for an anchor).
duration | An element’s extent in parent time.
start | The start of an element’s local timeline (to schedule its contained and anchored items).

Time values are expressed as a __rational number of seconds__ with a 64-bit numerator and a 32-bit denominator. Frame rates for NTSC-compatible media, for example, use a frame duration of 1001/30000s (29.97 fps) or 1001/60000s (59.94 fps).

Timing attribute values are expected to be a __multiple of the frame duration__ for the respective timeline. Otherwise, Final Cut Pro X has to insert a gap to maintain the specified timing upon import. A warning message appears when this happens.
