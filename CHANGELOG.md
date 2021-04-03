# Changelog
All notable changes to this project will be documented in this file.

The format is based on
[Keep a Changelog](https://keepachangelog.com/en/1.0.0/).

## [git] - 2021-03-31
### Changed
- Update for Blender 2.80
  - Merge egore changes
  - Add some instances of `if bpy.app.version >= (2, 80, 0):` (in some or all cases listed below)
  - Change uv_textures to uv_layers: <https://blender.stackexchange.com/questions/193894/updating-blender-2-79-script-to-2-80-mesh-uv-textures-new-fails-with-mesh-o>.
  - `name` must be a keyword argument in vertex_groups.new(...).
  - Use `bpy.context.collection.objects` instead of `bpy.context.scene.objects`.
  - Change `.select = True` to `.select_set(state=True)` (fix "AttributeError: 'Object' object has no attribute 'select'").
  - Change `bpy.context.collection.objects.active = arm` to `bpy.context.view_layer.objects.active = arm` (fix "AttributeError: bpy_prop_collection: attribute "active" not found").
  - Add 1.0 alpha to the color (the x format alpha value, which becomes part of the material settings) to
    fix: ```
  File "/home/owner/.config/blender/2.80/scripts/addons/io_import_x/import_x.py", line 856, in getMesh
    mat.diffuse_color = diffuse_color
ValueError: bpy_struct: item.attr = val: sequences of dimension 0 should contain 4 items, not 3
```

### Fixed
- Don't redefine Python 3 builtin file (change the variable name to file_).
- Add the missing arg to import_dXtree (hmm...try tokenname) to fix "expected string got int"
  - and set `lvl` by name since it is a keyword argument.

## [0.27] - 2019-04-18
(Poikilos)
### Changed
* bump version to 2.7 to indicate it works with blender 2.7x as per
  semantic versioning (API changes with every "tenth" of version number
  of blender).
* warning in `__init__.py` about unmaintained upstream littleneo version
* moved files around so "Install Add-on from File" feature will work
  with zip downloaded from GitHub:
  - removed duplicate directX_blender/README which was exactly the same
    as directX_blender/io_directx_bel/README)
  - moved io_directx_bel files to root of repo
  - renamed repo to directxblender (formerly directX_blender) so it is
    using a PEP8 module name
  - changed py files to reflect new module naming (from io_directx_bel
    to directxblender)
* moved Changelog text from README to CHANGELOG.md; changed
  formatting to markdown; corrected some spelling/grammar mistakes;
  improved wording.
* renamed README to README.md; changed formatting to markdown; corrected
  some spelling/grammar mistakes; improved wording
* fix incorrect "blender" property in bl_info (minor revision should be
  only in second part of tuple, not 2nd and 3rd--third should be 0--see
  <https://wiki.blender.org/wiki/Process/Addons/Guidelines/metainfo>).
  Also update required version to 2.66 since that seems to be when
  compatibility broke according to JLouis-B >3 yr old unaccepted pull
  request to littleneo's repo.
* add entry for limemidolin below (list items are commit names)
* add nohup.out to .gitignore

## [git] - 2018-04-12
(limemidolin)
* Reformat code
* Add feature: Do not add unused material if wanted
* Add feature: Load normals file if exist
* Multiple file import
* Fix to work on Blender 2.79

## [0.18] - 2012-01-25
(last littleneo entry)
* code rewrite according to API bmesh changes (me.polygon and UV layers
  essentially)
* implemented `foreachset()` call for UV import (faster)

## [0.17] - 2012-01-25
* faster (60% faster in some cases): various loop improvements; infile
  template parsing is disabled by default. I saw another bottleneck
  regarding data chunks as string but will wait for binary support for
  better point of view.
* interface cosmetics

## [rc 0.16] - 2012-01-23
* committed to SVN (and littleneo git as usual)
* corrected a bug regarding referenced token parenting
* corrected a bug regarding non-parented meshes
* Option to import armatures/empties is enabled by default.
* Last run importer options are saved in a 'last_run' preset,
  so it can be replayed or saved under another name once a
  particular .x profile has been defined.
* tagged script for 2.6.1

## [rc 0.15] - 2012-01-12
* name conversion changed from 5 to 4 digits
* matname, imagename and texturename fixes:
  * A path test is made at image import time with any existing data
    images, so the same file can't be loaded twice regardless what
    naming method is used (/ or \, rel or abs, etc).
    (`bel.material.new()` and after line 835)
  * Image and texture names should be OK now (tested with
    incrediblylongname.x).
  * Materials are replaced accordingly in existing objects when using
    the 'replace' naming method.
* FYI, the x exporter has the following inconveniences:
  * split linked faces into individual faces
  * inversed uvmapping (y axis)?
    - see testfiles/blender_x_export/incrediblylongname.x

## [git] - 2011-12-31
(and 2011-12-29)
* Cosmetics, code cleaning and optimizations
* bpy.ops.object.select_name methods replaced with
    ob.select = True
    bpy.context.scene.objects.active = ob
* corrected a big bug regarding tokens info appending in dXtree()
* new `bpyname()` method in bel module. removed bel.common

## [git] - 2011-12-26
* armature import and bone max. length option

## [git] - 2011-11-23
* contrib candidate :)
* solved some naming cases, added bel methods.
* added experimental option regarding parenting (no armature yet just
  empties, when needed)
* a bit faster
* added some test files (empty parenting, armature etc)

## [git] - 2011-11-22
campbell feedback (cont):
* added naming methods as options (default is Blender name inc. if name
  exists). me and ob `remove()` should be ok--but consider special
  cases (empties, mesh with multi-users)
* improved UI

## [git] - 2011-11-21
campbell feedback:
* converted immutables to tuples (templates_x.py and some other vars)
  <http://stackoverflow.com/questions/3340539/why-tuple-is-faster-than-list>
* `dprint()` (console debug) removed, replaced by a inloop tests (a bit
  faster): I'd like to keep it for now for easier debug (e.g.
  userfeedback with 'processing' option).

## [git] - 2011-11-19
* object parenting support: Parsing the x tree from roots using
  `import_dxtree()` is actually faster than before.

## [git] - 2011-11-16
* weight group import
* improved UI a bit, and console logs
* x matrices to Blender matrices conversion

## [git] - 2011-11-14
* global matrix options
* Added messy code regarding binary (not working).

## [git] - 2011-11-11
* Import materials and textures (basics): UV and image mapped (multitex
  mode) and material created with tex slot if any.
  Alpha should be ok (?).
* added a smooth option
* better tolerance with faulty .x (upper/lower case of template names)
* Token names length from x to Blender conversion should be ok also
  (long name cases).
* corrected a parser pointer error after one array parsing case.
* added more templates (for mat and tex support)
* removed texture files from repo in testfile (tex does not match
  meshes)
* added some other x files for further tests in binary and compressed
  format
  <http://assimp.svn.sourceforge.net/viewvc/assimp/trunk/test/models/X/>

## [git] - 2011-11-08
* turned into an addon (fork from obj import so unused functions atm).
  Enable it in add-ons. Use via File > Import > DirectX.
* Split the DirectX parser (io_directx_bel folder) and bel draft.
  The bel folder is intended to be located in /scripts/modules (shared
  components) but it's ok in scripts/addons too (to be determined).
  The bel folder (will) include anything related to Blender data helper
  (read/write).
* corrected duplicated quotes for x string type.

## [git] - 2011-11-07
* UV import
* generic DirectX token parser: template items are used to read data of
  any token type--a bit slower but cool since it should support non-
  strict standard DirectX files. It can retrieve virtually everything
  now supposing the template is known by default or given in the file.
  Calls are now like :
```
		nbslots, mats = readToken('MeshMaterialList001') or
		uv = readToken('uv001') or
		nVerts, verts, nFaces, faces = readToken('Hydralisk_backbone1') etc
```
* Removed the specific mesh parser the 'rigid' file is the last before
  mutation to generic parser. It is a bit faster but harder to make
  evolve or adapt. Keep it as a faster strict 'branch'.
* added some default templates. Goals / WIP:
  - Compare template declaration in file, and default one.
    Either use the default one (strict) or the .x one (could differ)
    for use by the generic data parser, to avoid a parser for each kind
    of token.
* cleaner code (grouping methods, function names, docs etc)
  - functions separated from calls
  - renamed token dict as tokens etc
* added tweaks at the beginning of the file:
```
	chunksize = 1024     # size of file streams read in a row
	quickmode = False    # this to only find meshes (no parenting, no other tokens than Mesh ones)
	showtree = False     # display the entire token tree in the console
	showtemplate = True  # display template datas found in file
```
* added a patch for malformed datas of vertices (meshFaces):
```
	# patch for malformed datas not completely clear yet ( I guess
	# there's bunch of us when looking at meshface syntax in .x files) :
	# when array members are like 3;v0,v1,v2;,
	# and not like 3;v0;v1;v2;, depending on template declarations.
	# http://paulbourke.net/dataformats/directx/#xfilefrm_Use_of_commas
```
* The script now generates linked faces (was not my fault !)
  - Apparently x always separates each face:
    It defines (vert * linked faces) verts for one needed vert.
    The `readvertices` loop now removes duplicates at the source.
    It uses a verts lookup list to redirect vert id defined in faces.

## [git] - 2011-11-06
* Vertices and faces are imported from each test file.
* added some info in README on how to test it yourself
* switched to binary for .x as text to retrieve EOL (pointer bugs) which
  should be ok whether it's win, mac or unix text format (also works
  with mixed EOL).
  - Apparently Python 3.1 can't return a 'line' when data.readline()
    when read mode is 'rb' (U default and universal ? really ? ;) ) when
    file has mac EOL (\r)
    - read(1024) in binary, decode, and replace any \r with \n. yes, it
      doubles lines for windows and lines value is wrong for now
    - but the used pointer value is always ok now whatever the file
      format and still way faster than a data.tell()
    - see CRCF folder to compare output wispwind.x by format.
* Files are still split into chunks (1024 B) and readable as lines.
* references: added 'user' fields when token is used. Users store a
  reference with their children but with a '*' tag at chr0. The tree
  reflects the changes.
* Now read anything and add it to the 'tree'. This includes unknown
  tokens.
* References are recognized (fields like `{ cube0 }` rather than an
  inline `frame cube0 {` declaration. I don't know if one item can be
  referenced several times or referenced before declaration--could be,
  so I await an example. For now only one 'parent' token, messages will
  show multiple references to one token if cases arise.
* more permissive syntax : `frame spam{`, `frame     spam   egg{`,
  `frame spam egg  {`, and so on.
* Comments are recognized (inlines ones not done yet, since still no
  useful data is read :) )
* Header is read.
* found
  [other .x test files](http://www.xbdev.net/3dformats/x/xfileformat.php)
  created by 3DS MAX
* added .x files in repo. line 70 and following to switch.
* some token comes with no names, add a noname<00000> to them
* Console gives line number (more useful than char position I guess).

## [Unreleased] - 2011-11-05
(first litleneo entry)
day 0 :
* made some disapointing test with ply (from a speed point of view--
  otherwise it looks really cool)
* made my own parser
* Nothing imported for now (it's more about self-eduction to .x and
  concept) but it reads the .x structure and can gather some info
