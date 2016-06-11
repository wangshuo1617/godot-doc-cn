.. _doc_project_organization:

项目管理
====================

简介 
------------

本教程是为了介绍一种组织、管理项目的简单工作流程。因为Godot允许程序员以他或她喜欢的文件系统工作，所以在刚开始使用引擎时，就找到一种管理项目的方法，并不是一件容易的事。因此，我们提出了一种简单的工作流程，无论你使用还是不使用，都可以作为一个很好的起点来进行项目管理。

另外，使用版本管理工具可能也并不简单，这一部分也会包含在本教程中。

管理
------------

其他一些游戏引擎往往使用资源数据库的方式来进行管理，你可以在数据库中查看图片、模型、声音等等。



Other game engines often work by having an asset database, were you can
browse images, models, sounds, etc. Godot is more scene-based in nature
so most of the time the assets are bundled inside the scenes or just
exist as files but are referenced from scenes.

Importing & game folder
-----------------------

It is very often necessary to use asset importing in Godot. As the
source assets for importing are also recognized as resources by the
engine, this can become a problem if both are inside the project folder,
because at the time of export the exporter will recognize them and
export both.

To solve this, it is a good practice to have your game folder inside
another folder (the actual project folder). This allows to have the game
assets separated from the source assets, and also allows to use version
control (such as svn or git) for both. Here is an example:

::

    myproject/art/models/house.max
    myproject/art/models/sometexture.png
    myproject/sound/door_open.wav
    myproject/sound/door_close.wav
    myproject/translations/sheet.csv

Then also, the game itself is, in this case, inside a game/ folder:

::

    myproject/game/engine.cfg
    myproject/game/scenes/house/house.scn
    myproject/game/scenes/house/sometexture.tex
    myproject/game/sound/door_open.smp
    myproject/game/sound/door_close.smp
    myproject/game/translations/sheet.en.xl
    myproject/game/translations/sheet.es.xl

Following this layout, many things can be done:

-  The whole project is still inside a folder (myproject/).
-  Exporting the project will not export the .wav and .png files which
   were imported.
-  myproject/ can be put directly inside a VCS (like svn or git) for
   version control, both game and source assets are kept track of.
-  If a team is working on the project, assets can be re-imported by
   other project members, because Godot keeps track of source assets
   using relative paths.

Scene organization
------------------

Inside the game folder, a question that often arises is how to organize
the scenes in the filesystem. Many developers try asset-type based
organization and end up having a mess after a while, so the best answer
is probably to organize them based on how the game works and not based
on asset type. Here are some examples.

If you were organizing your project based on asset type, it would look
like this:

::

    game/engine.cfg
    game/scenes/scene1.scn
    game/scenes/scene2.scn
    game/textures/texturea.png
    game/textures/another.tex
    game/sounds/sound1.smp
    game/sounds/sound2.wav
    game/music/music1.ogg

Which is generally a bad idea. When a project starts growing beyond a
certain point, this becomes unmanageable. It's really difficult to tell
what belongs to what.

It's generally a better idea to use game-context based organization,
something like this:

::

    game/engine.cfg
    game/scenes/house/house.scn
    game/scenes/house/texture.tex
    game/scenes/valley/canyon.scn
    game/scenes/valley/rock.scn
    game/scenes/valley/rock.tex
    game/scenes/common/tree.scn
    game/scenes/common/tree.tex
    game/player/player.scn
    game/player/player.gd
    game/npc/theking.scn
    game/npc/theking.gd
    game/gui/main_screen/main_sceen.scn
    game/gui/options/options.scn

This model or similar models allows projects to grow to really large
sizes and still be completely manageable. Notice that everything is
based on parts of the game that can be named or described, like the
settings screen or the valley. Since everything in Godot is done with
scenes, and everything that can be named or described can be a scene,
this workflow is very smooth and easygoing.

Cache files
-----------

Godot uses a hidden file called ".fscache" at the root of the project.
On it, it caches project files and is used to quickly know when one is
modified. Make sure to **not commit this file** to git or svn, as it
contains local information and might confuse another editor instance in
another computer.
