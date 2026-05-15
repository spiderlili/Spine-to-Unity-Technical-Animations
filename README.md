# Spine to Unity (2D URP)
> IMPORTANT: Make sure the [Spine version](https://esotericsoftware.com/spine-unity-download) is compatible with the Unity project version! 
1. Create a Unity project with 2D URP template (Recommendation: Unity 6000.3. as spine-unity 4.2 does not work on versions above Unity 6000.3.)
2. Change Color Space to Gamma in Project Settings for better colour match in Spine 2D
3. Spine: Export (Cmd + E) > Data: Binary as exporting in binary format instead of JSON will result in smaller file size and faster loading
4. Set the Extension to `.skel.bytes`
5. Texture atlas: :white_check_mark: pack, Pack Settings > :white_check_mark: Premultiply alpha (Note: blending math for Premultiplied Alpha is strictly designed for Gamma Color space. Using it in Linear space causes rendering errors!)
6. Pack Settings > Pages > :white_check_mark: Power of two
7. Set Output Folder (usually Textures > SpineAtlas > CharacterName) > Export: there should be 3 files - [CharacterName].atlas, [CharacterName].png, [CharacterName].skel.bytes 
8. Install the latest [Spine-Unity Runtime](https://esotericsoftware.com/spine-unity) via [Unity Package Manager](https://esotericsoftware.com/spine-unity-installation): spine-unity 4.2
9. Install the latest [URP Shaders UPM](https://esotericsoftware.com/spine-unity-download) via Unity Package Manager: Packages > Spine Universal RP Shaders; materials are in spine-unity Runtime > Materials
10. Install the latest [Timeline Extensions UPM package](https://esotericsoftware.com/spine-unity-download)

# Unity Scene Setup with Spine Animations
- Camera Projection: Orthographic
- Canvas: 
