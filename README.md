# Spine to Unity (2D URP)
> IMPORTANT: Make sure the [Spine version](https://esotericsoftware.com/spine-unity-download) is compatible with the Unity project version! 
1. Create a Unity project with 2D URP template
2. Install the latest [Spine-Unity Runtime](https://esotericsoftware.com/spine-unity) via [Unity Package Manager](https://esotericsoftware.com/spine-unity-installation): as of May 2026, the git link for spine 4.3 beta does not work -> you have to download the package & install via Assets > Import Package > Custom Package
3. Install the latest [URP Shaders UPM](https://esotericsoftware.com/spine-unity-download) via Unity Package Manager: Packages > Spine Universal RP Shaders; materials are in spine-unity Runtime > Materials
4. Install the latest [Timeline Extensions UPM package](https://esotericsoftware.com/spine-unity-download)
5. Change Color Space to Gamma in Project Settings for better colour match in Spine 2D
6. Spine: Export (Cmd + E) > Data: Binary as exporting in binary format instead of JSON will result in smaller file size and faster loading
7. Set the Extension to `.skel.bytes`
8. Uncheck Export > Pack Settings > Flatten Paths
9. Pack Settings > Options > atlas extension: `.atlas.txt` -> Ensure your atlas file is exported and saved as `.atlas.txt`, not just `.atlas.` which is the default. Unity requires the `.txt` extension to read the file properly!
10. Texture atlas: :white_check_mark: pack, Pack Settings > :white_check_mark: Premultiply alpha (Note: blending math for Premultiplied Alpha is strictly designed for Gamma Color space. Using it in Linear space causes rendering errors!)
11. Pack Settings > Pages > :white_check_mark: Power of two
12. Set Output Folder (usually Textures > SpineAtlas > CharacterName) > Export: there should be 3 files - [CharacterName].atlas, [CharacterName].png, [CharacterName].skel.bytes 

# Unity Scene Setup with Spine Animations
- Camera Projection: Orthographic
- Canvas: 
