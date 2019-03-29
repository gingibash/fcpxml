# export iz avscript

## scenario 1 - media bin / multi clip
1. uzimamo spremljeni ``<resources>`` iz import koraka
2. kreiramo 
```
 <event>
    <project>
        <sequence>
            <spine>
```
3. clipove referiramo s `<asset-clip>` na `<resources><asset-clip>` __id__

[primjer zaglavlja XMLa](https://github.com/gingibash/fcpxml/blob/master/export/scenario-1.xml)

## scenario 2 - compound clip
1. uzimamo spremljeni ``<resources>`` iz import koraka - neophodan nam je kako bi sačuvali compound clip za fcpx
    1.  unutar `<resources>` konstruiramo `<effect>` i dajemo mu `id`
2. kreiramo 
```
 <event>
    <project>
        <sequence>
            <spine>
```
3. clipove referiramo s `<ref-clip>` na compound tj. `<resources><media>` __id__

[primjer zaglavlja XMLa](https://github.com/gingibash/fcpxml/blob/master/export/scenario-2.xml)
