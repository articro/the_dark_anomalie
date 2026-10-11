PSX Creatures Free
==================

A PS1-style zombie woman with 5 animations, taken from PSX Creatures (13 creatures, 65
animations): https://heyheythere.itch.io/psx-creatures
Low-poly, one 1024x1024 point-filtered texture atlas, the shading baked into vertex colours,
real-world scale (1 unit = 1 metre).

What's in the zip
-----------------
glb/        the creature, with its animations (the best format for Godot, Blender, three.js)
fbx/        the creature, with its animations as takes (Unreal, Unity, most 3D apps)
obj/        the creature, in its bind pose (any 3D app)
textures/   atlas.png, the one texture it uses
icons/      its icon, 256x256 PNG with transparency
props.json  the creature: title, group, size, triangles, parts and animations
blender/    the creature in a .blend, the atlas packed in
addons/     the Godot addon, psx_creatures/: this folder is a Godot 4.3+ project that opens on
            its gallery (.gdignore keeps Godot out of the other folders)

The creature
------------
It is rigid parts that turn at their joints, the way PS1 characters were made, rigged: one mesh
on an armature, each part weighted whole to its bone (a forearm's bone under its upper arm's, under
the spine's, under the hips'), so turning one carries the ones below it. It is bound in a T-pose,
its bones named as Mixamo names them (Hips, Spine, Head, LeftArm, LeftForeArm, LeftHand, LeftUpLeg,
LeftLeg, LeftFoot and the Right ones). Its origin is on the ground under it, and it faces Blender's -Y (+Z in
Godot and Unity).
It has five animations, as every creature in PSX Creatures does:
  idle, walk      loops; the walk plays in place, for your code to move the creature
  attack          a bite or a strike, once
  hit             a flinch, once, back to where it started
  death           a fall, once, ending on the ground
Their lengths are in props.json.

Godot 4.3 and later
-------------------
Copy addons/psx_creatures/ into your project's addons/ folder. The creature is a scene in
props/: drag it into your level. It has its mesh on a Skeleton3D, a box collider (StaticBody3D)
on each bone that moves with it, and an AnimationPlayer:

    zombie.get_node("AnimationPlayer").play("walk")   # zombie: an instance of props/zombie_woman.tscn

icons/ has the icon. demo/gallery.tscn shows the creature: drag to turn, its buttons to play
its animations.
The creature uses one material, props.tres: the atlas times the vertex colours, lit, so your
lights fall on them. For the full PS1 look (vertex snap, affine textures, 240p, dither), our PSX
Look shaders turn it over in one line: https://heyheythere.itch.io/psx-look
With PSX Look in res://addons/psx_look/, the gallery shows the creature through it (P toggles it).

Other engines and apps
----------------------
Use fbx/, glb/ or obj/ with textures/atlas.png. Set the texture's filtering to nearest/point and
turn off mipmaps for the crisp PS1 texels, and multiply it by the vertex colours (the baked
shading) in your material.

License: see LICENSE.txt. Made by heyheythere: https://heyheythere.itch.io
