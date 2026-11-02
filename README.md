# Spine to Unity (2D URP)
> IMPORTANT: Make sure the [Spine version](https://esotericsoftware.com/spine-unity-download) is compatible with the Unity project version! This project uses Unity 6000.3.12f1 and Spine 4.3 beta (Custom Package)
1. Create a Unity project with Universal 2D Core template
2. Install the latest [Spine-Unity Runtime](https://esotericsoftware.com/spine-unity) via [Unity Package Manager](https://esotericsoftware.com/spine-unity-installation): as of May 2026, the git link for spine 4.3 beta does not work -> you have to download the package & install via Assets > Import Package > Custom Package
3. Install the latest [URP Shaders UPM](https://esotericsoftware.com/spine-unity-download) via Unity Package Manager: Packages > Spine Universal RP Shaders; materials are in spine-unity Runtime > Materials
4. Install the latest [Timeline Extensions UPM package](https://esotericsoftware.com/spine-unity-download)
5. [OPTIONAL] Installing spine-unity also created a file called SpineSettings.asset in an Editor folder. Because the URP settings also have their own folder, you can clean up the folder hierarchy by creating a new top-level folder to contain these sub-folders. Under Assets, create a new folder (Create > Folder) and call it Character Customization Spine, create a Config folder inside it. Move the Editor folder into Config, move the Settings folder into Config and rename Settings to RenderSettings, because the original name was confusingly generic.
6. Change Color Space to Gamma in Project Settings for better colour match in Spine 2D
7. Spine: Export (Cmd + E) > Data: Binary as exporting in binary format instead of JSON will result in smaller file size and faster loading
8. Set the Extension to `.skel.bytes`
9. Uncheck Export > Pack Settings > Flatten Paths
10. Pack Settings > Options > atlas extension: `.atlas.txt` -> Ensure your atlas file is exported and saved as `.atlas.txt`, not just `.atlas.` which is the default. Unity requires the `.txt` extension to read the file properly!
11. Texture atlas: :white_check_mark: pack, Pack Settings > :white_check_mark: Premultiply alpha (Note: blending math for Premultiplied Alpha is strictly designed for Gamma Color space. Using it in Linear space causes rendering errors!) It is important to select all spine atlas textures (e.g. via filter "t:texture") and disabled the Advanced - Alpha is Transparency parameter in Unity to avoid alpha artifacts if using Premultiplied Alpha.
12. Pack Settings > Pages > :white_check_mark: Power of two
13. Set Output Folder (usually Textures > SpineAtlas > CharacterName) > Export: there should be 6 files - [CharacterName].atlas.txt, [CharacterName].asset, [CharacterName].png, [CharacterName].skel.bytes, [CharacterName].mat, [CharacterName].asset
14. Untick sRGB (Color Texture) in [texture import settings](https://esotericsoftware.com/spine-unity-assets) for Gamma Colour Space, apply compression settings (ASTC 8x8 block)
15. Set material to use `Spine/Skeleton` shader
16. Preview animation on the Skeleton Data file
17. [OPTIONAL] Skeleton Data > Mix Settings > Add Custom Mix: set up blending between animations

# Unity Scene Setup with Spine Animations
- Camera Projection: Orthographic
- Canvas > Create a new empty GameObject as the parent
- Create > Spine > SkeletonGraphic (UnityUI) OR SkeletonAnimation (for 2D animations in game scene)
- [OPTIONAL] enable Loop on SkeletonAnimation component

# Common Errors Explained
<img width="490" height="466" alt="Screenshot 2026-05-19 at 11 53 20" src="https://github.com/user-attachments/assets/f1fee1d9-5deb-48f7-9da7-eee320d769cb" />
<img width="392" height="262" alt="Screenshot 2026-05-19 at 11 59 07" src="https://github.com/user-attachments/assets/74888153-7e17-4c4b-9ea3-076ccbeea8ab" />

# Spine Glossary
- Skeleton (skeleton.json): The root-level container for everything in an animation. The name derives from the fact that this container holds a collection of bones. In Spine, a “skeleton” includes everything needed for an animation, not just bones. As in 3D, this is sometimes referred to as the “animation rig”.
- Bone: A rigid, invisible object that moves during an animation. Bones work similarly to the bones of a 3D character. They connect in a hierarchical arrangement and can even influence surfaces covering them. Instead of 3D meshes, the bones in Spine have “slots” connected to them.
- Slot: An abstract object that serves as an attachment point on a bone. Although a bone can have multiple slots, each slot can hold only 1 attachment at a time. Slots can be colored & anything attached to a slot inherits that tint.
- Attachment: Anything that attaches to a slot. The most common type of attachment is an image, but an attachment can also be more abstract, such as a collision shape or a placeholder for skins. For a placeholder, the image displayed depends on the skin that has been activated.
- Skin: A group of preset image attachments. Each skin defines which image goes with which placeholder slot -> you can change every image attached to every slot at once by activating a different skin.
- Atlas (character_name.atlas.txt): refers both to atlas images and to the text data describing those images. An atlas image is an assemblage of many small images packed into a single large image. The different parts of the character are packed into 1 large image.

# Q & A
- Q: Is there a standard format for Spine skeletal animation?
- A: While formats for 2D images are fairly standardised, there is no standard format for skeletal animation. Spine exports animations in a custom format that defines the bones, skins & other data, which requires a custom code library to consume Spine’s exported files.

# Resources & Reading List
- https://esotericsoftware.com/spine-unity-assets
- https://esotericsoftware.com/spine-unity-main-components
- Unity Character Customisation: Modular 3D and Spine2D: requires Spine version 4.3-beta for the on-demand loading functionality.
  - Edit > Preferences > Switch Texture Workflow: Straight Alpha (PMA is not how the example images are set up for the character)
  - Texture import settings: sRGB (Color Texture, alpha is transparency)
- Esoteric Software provides [runtime libraries](https://github.com/EsotericSoftware/spine-runtimes/) for various game development toolkits, including Unity. The runtime enables importing and playback of Spine animations. 
