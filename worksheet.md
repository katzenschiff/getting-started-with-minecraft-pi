# Minecraft Pi für Anfänger

Minecraft is ist ein beliebtes Open-World Computerspiel. Ähnlich wie mit Lego kann man verschiedene Sachen aus Blöcken bauen. 
Auf dem Raspberry Pi gibt es eine kostenlose Version von Minecraft, die man auch programmieren kann. Man kann alsi Kommandos und kripte in Minecraft einbauen, um Sachen automatisch zu bauen. Ein guter Weg, um Python zu lernen!

![Minecraft Pi banner](images/minecraft-pi-banner.png)

## Minecraft starten

Um Minecraft zu starten, öffne es aus dem Desktop Menü oder tippe `minecraft-pi` im Terminal.

![](images/menu.png)

Wenn Minecraft Pi geladen ist, klicke auf **Start Game** und danach **Create new**. 

![](images/mcpi-game.png)

Du bist jetzt in der Minecraft Welt und kannst dich dort bewegen, herumlaufen und Sachen bauen!

Benutze die Maus, um dich umzusehen, und die folgenden Tasten:

| Taste          | Aktion               |
| :---:        | :-----:              |
| W            | Vorwärts              |
| A            | Links                 |
| S            | Zurück             |
| D            | Rechts                |
| E            | Inventar            |
| Leertaste    | Springen                 |
| 2x Leertaste | Fliegen / Fallen           |
| Esc          | Pause / Spielmenü    |
| Tab          | Mauszeiger loslassen |

Mit dem Mausrad kann man etwas aus der Schnellauswahl auswählen (oder auch mit Zahlen auf der Tastatur), oder drücke `E` und wähle etwas aus dem Inventar aus.

![](images/mcpi-inventory.png)

Zweimaliges Drücken der Leertaste macht, dass du durch die Luft fliegst. Du hörst auf zu fliegen, wenn du die Leertaste loslässt, und wenn du sie noch zweimal drückst, fällst du wieder auf den Boden.

![](images/mcpi-flying.png)

Mit dem Schwert ind er Hand kannst du auf Blöcke klicken, um die zu entfernen (oder um zu graben). Mit eienm Block in der Hand kannst du
per Rechtsklick den Block vor dir absetzen, oder ihn mit einem Linksklick entfernen.


## Benutze Python in Minecraft

Während Minecraft läuft, drücke auf die `Tab` Taste, um den Fokus vom SPiel zu nehmen. Öffne Python 3 aus dem ANwendungsmenü und setze das Fenster neben das Spielfenster.

Du kannst nun entweder direkt Kommandos in Python eingeben oder eine Datei erzeugen, so daß du den Code immer wieder laufen lassen kannst. 

Wenn Du eine Datei erzeugen willst, benutze `File > New window` und `File > Save`. Speichere die Datei in deinem Homeverzeichnis.

Importiere zuerst die Minecraft Biliothek. Dadurch entsteht eine Verbindung zum Spiel. Teste diese, indem du die Nachricht "Hallo Welt" auf den Bildschirm schreibst:

```python
from mcpi.minecraft import Minecraft

mc = Minecraft.create()

mc.postToChat("Hallo Welt")
```

Wenn du die Kommandos direkt eingibst, drücke einfach `Enter` nach jeder Zeile. Wenn es eine Datei ist, speichere dein SKript mit `Ctrl + S` und lasse sie mit `F5` laufen. Wenn das Skript läuft, solltest du die Nachricht auf dem Bildschirm sehen.


![](images/helloworld.gif)

### Finde herasu, wo du bist

Um herauszufinden, wo du bist, tippe:
```python
pos = mc.player.getPos()
```

`pos` now contains your location; access each part of the set of coordinates with `pos.x`, `pos.y` and `pos.z`.
`pos` speichert jetzt deinen Aufenthaltsort. DU kannst darauf mit den Koordinaten `pos.x`, `pos.y` and `pos.z` zugreifen.

Du kannst sie auch gleich in die Variablen x, y und z schreiben.

```python
x, y, z = mc.player.getPos()
```


Now `x`, `y`, and `z` contain each part of your position coordinates. `x` and `z` are the walking directions (forward/back and left/right) and `y` is up/down.

Note that `getPos()` returns the location of the player at the time, and if you move position you have to call the function again or use the stored location.

### Teleport

As well as finding out your current location you can specify a particular location to teleport to.

```python
x, y, z = mc.player.getPos()
mc.player.setPos(x, y+100, z)
```

This will transport your player to 100 spaces in the air. This will mean you'll teleport to the middle of the sky and fall straight back down to where you started.

Try teleporting to somewhere else!

### Set block

You can place a single block at a given set of coordinates with `mc.setBlock()`:

```python
x, y, z = mc.player.getPos()
mc.setBlock(x+1, y, z, 1)
```

Now a stone block should appear beside where you're standing. If it's not immediately in front of you it may be beside or behind you. Return to the Minecraft window and use the mouse to spin around on the spot until you see a grey block directly in front of you.

![](images/mcpi-setblock.png)

The arguments passed to `set block` are `x`, `y`, `z` and `id`. The `(x, y, z)` refers to the position in the world (we specified one block away from where the player is standing with `x + 1`) and the `id` refers to the type of block we'd like to place. `1` is stone.

Other blocks you can try:

```
Air:   0
Grass: 2
Dirt:  3
```

Now with the block in sight, try changing it to something else:

```python
mc.setBlock(x+1, y, z, 2)
```

You should see the grey stone block change in front of your eyes!

![](images/mcpi-setblock2.png)

#### Block constants

You can use a inbuilt block constants to set your blocks, if you know their names. You'll need another `import` line first though.

```python
from mcpi import block
```

Now you can write the following to place a block: 

```python
mc.setBlock(x+3, y, z, block.STONE.id)
```

Block ids are pretty easy to guess, just use ALL CAPS, but here are a few examples to get you used to the way they are named.

```
WOOD_PLANKS
WATER_STATIONARY
GOLD_ORE
GOLD_BLOCK
DIAMOND_BLOCK
NETHER_REACTOR_CORE
```

### Block as variable

If you know the id of a block it can be useful to set it as a variable. You can use the name or the integer id.

```python
dirt = 3
mc.setBlock(x, y, z, dirt)
```

or

```python
dirt = block.DIRT.id
mc.setBlock(x, y, z, dirt)
```

### Special blocks

There are some blocks which have extra properties, such as Wool which has an extra setting you can specify the colour. To set this use the optional fourth parameter in `setBlock`:

```python
wool = 35
mc.setBlock(x, y, z, wool, 1)
```

Here the fourth parameter `1` sets the wool colour to orange. Without the fourth parameter it is set to the default (`0`) which is white. Some more colours are:

```
2: Magenta
3: Light Blue
4: Yellow
```

Try some more numbers and watch the block change!

Other blocks which have extra properties are wood (`17`): oak, spruce, birch, etc; tall grass (`31`): shrub, grass, fern; torch (`50`): pointing east, west, north, south; and more. See the [API reference](http://www.stuffaboutcode.com/p/minecraft-api-reference.html) for full details.

### Set multiple blocks

As well as setting a single block with `setBlock` you can fill in a volume of space in one go with `setBlocks`:

```python
stone = 1
x, y, z = mc.player.getPos()
mc.setBlocks(x+1, y+1, z+1, x+11, y+11, z+11, stone)
```

This will fill in a 10 x 10 x 10 cube of solid stone.

![](images/mcpi-setblocks.png)

You can create bigger volumes with the `setBlocks` function but it may take longer to generate!

## Dropping blocks as you walk

Now you know how to drop blocks, let's use our moving location to drop blocks when you walk.

The following code will drop a flower behind you wherever you walk:

```python
from mcpi.minecraft import Minecraft
from time import sleep

mc = Minecraft.create()

flower = 38

while True:
    x, y, z = mc.player.getPos()
    mc.setBlock(x, y, z, flower)
    sleep(0.1)
```

Now walk forward for a while and turn around to see the flowers you have left behind you.

![](images/mcpi-flowers.png)

Since we used a `while True` loop this will go on forever. To stop it, hit `Ctrl + C` in the Python window.

Try flying through the air and see the flowers you leave in the sky:

![](images/mcpi-flowers-sky.png)

What if we only wanted to drop flowers when the player walks on grass? We can use `getBlock` to find out what type a block is:

```python
x, y, z = mc.player.getPos()  # player position (x, y, z)
this_block = mc.getBlock(x, y, z)  # block ID
print(this_block)
```

This tells you the location of the block you're standing *in* (this will be `0` - an air block). We want to know what type of block we're standing *on*. For this we subtract 1 from the `y` value and use `getBlock()` to determine what type of block we're standing on:

```python
x, y, z = mc.player.getPos()  # player position (x, y, z)
block_beneath = mc.getBlock(x, y-1, z)  # block ID
print(block_beneath)
```

This tells us the ID of the block the player is standing on.

Test this out by running a loop to print the block ID of whatever you're currently standing on:

```python
while True:
    x, y, z = mc.player.getPos()
    block_beneath = mc.getBlock(x, y-1, z)
    print(block_beneath)
```

![](images/blockbeneath.gif)

We can use an `if` statement to choose whether or not we plant a flower:

```python
grass = 2
flower = 38

while True:
    x, y, z = mc.player.getPos()  # player position (x, y, z)
    block_beneath = mc.getBlock(x, y-1, z)  # block ID

    if block_beneath == grass:
        mc.setBlock(x, y, z, flower)
    sleep(0.1)
```

Perhaps next we could turn the tile we're standing on into grass if it isn't grass already:

```python
if block_beneath == grass:
    mc.setBlock(x, y, z, flower)
else:
    mc.setBlock(x, y-1, z, grass)
```

Now we can walk forward and if we walk on grass, we'll leave a flower behind. If the next block is not grass, it turns into grass. When we turn around and walk back, we now leave a flower behind us.

![](images/mcpi-flowers-grass.png)

## Playing with TNT blocks

Another interesting block is TNT! To place a normal TNT block use:

```python
tnt = 46
mc.setBlock(x, y, z, tnt)
```

![](images/mcpi-tnt.png)

However, this TNT block is fairly boring. Try applying `data` as `1`:

```python
tnt = 46
mc.setBlock(x, y, z, tnt, 1)
```

Now use your sword and left click the TNT block: it will be activated and will explode in a matter of seconds!

Now try making a big cube of TNT blocks!

```python
tnt = 46
mc.setBlocks(x+1, y+1, z+1, x+11, y+11, z+11, tnt, 1)
```

![](images/mcpi-tnt-blocks.png)

Now you'll see a big cube full of TNT blocks. Go and activate one of the blocks and then run away to watch the show! It'll be really slow to render the graphics as so many things are changing at once.

![](images/mcpi-tnt-explode.png)

## Fun with flowing lava.

One block that's a lot of fun to play with is flowing lava.

```python
from mcpi.minecraft import Minecraft

mc = Minecraft.create()

x, y, z = mc.player.getPos()

lava = 10

mc.setBlock(x+3, y+3, z, lava)
```

Find the block you've just placed, and you should see lava flowing from the block to the ground.

The cool thing about lava is that when it cools down it becomes rock. Move to another location in your world and try this:

```python
from mcpi.minecraft import Minecraft
from time import sleep

mc = Minecraft.create()

x, y, z = mc.player.getPos()

lava = 10
water = 8
air = 0

mc.setBlock(x+3, y+3, z, lava)
sleep(20)
mc.setBlock(x+3,y+5, z, water)
sleep(4)
mc.setBlock(x+3, y+5, z, air)

```

You can adjust the `sleep` parameters to allow more or less lava to flow.

![lava](images/lava.png)

## What next?

There's plenty you can do now you know your way around the Minecraft world and how to use the Python interface.

### Networked game

If multiple people connect Raspberry Pis to a local network, they can join the same Minecraft world and play together. Players can see each other in the Minecraft world.

### API reference

For a more extensive documentation of functions and a full list of block IDs see an API reference at [stuffaboutcode.com](http://www.stuffaboutcode.com/p/minecraft-api-reference.html).

### Make a game

Try out another resource and make a Whac-a-mole game: [Minecraft Whac-a-Block](https://www.raspberrypi.org/learning/minecraft-whac-a-block-game/).
