# Spine to Unity (2D URP)
> IMPORTANT: Make sure the [Spine version](https://esotericsoftware.com/spine-unity-download) is compatible with the Unity project version! This project uses Unity 6000.3.12f1 and Spine 4.3 beta (Custom Package)
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
12. Set Output Folder (usually Textures > SpineAtlas > CharacterName) > Export: there should be 6 files - [CharacterName].atlas.txt, [CharacterName].asset, [CharacterName].png, [CharacterName].skel.bytes, [CharacterName].mat, [CharacterName].asset
13. Untick sRGB (Color Texture) in [texture import settings](https://esotericsoftware.com/spine-unity-assets) for Gamma Colour Space, apply compression settings (ASTC 8x8 block)
14. Set material to use `Spine/Skeleton` shader
15. Preview animation on the Skeleton Data file
16. [OPTIONAL] Skeleton Data > Mix Settings > Add Custom Mix: set up blending between animations

# Unity Scene Setup with Spine Animations
- Camera Projection: Orthographic
- Canvas > Create a new empty GameObject as the parent
- Create > Spine > SkeletonGraphic (UnityUI) OR SkeletonAnimation (for 2D animations in game scene)
- [OPTIONAL] enable Loop on SkeletonAnimation component

# Common Errors Explained
<img width="490" height="466" alt="Screenshot 2026-05-19 at 11 53 20" src="https://github.com/user-attachments/assets/f1fee1d9-5deb-48f7-9da7-eee320d769cb" />
<img width="392" height="262" alt="Screenshot 2026-05-19 at 11 59 07" src="https://github.com/user-attachments/assets/74888153-7e17-4c4b-9ea3-076ccbeea8ab" />

# Spine Glossary
- Skeleton: The root-level container for everything in an animation. The name derives from the fact that this container holds a collection of bones. In Spine, a “skeleton” includes everything needed for an animation, not just bones. As in 3D, this is sometimes referred to as the “animation rig”.
- Bone: A rigid, invisible object that moves during an animation. Bones work similarly to the bones of a 3D character. They connect in a hierarchical arrangement and can even influence surfaces covering them. Instead of 3D meshes, the bones in Spine have “slots” connected to them.
- Slot: An abstract object that serves as an attachment point on a bone. Although a bone can have multiple slots, each slot can hold only 1 attachment at a time. Slots can be colored & anything attached to a slot inherits that tint.
- Attachment: Anything that attaches to a slot. The most common type of attachment is an image, but an attachment can also be more abstract, such as a collision shape or a placeholder for skins. For a placeholder, the image displayed depends on the skin that has been activated.
- Skin: A group of preset image attachments. Each skin defines which image goes with which placeholder slot -> you can change every image attached to every slot at once by activating a different skin.
- Atlas: refers both to atlas images and to the text data describing those images. An atlas image is an assemblage of many small images packed into a single large image. Fall the different parts of the character are packed into 1 large image.

# Resources & Reading List
- https://esotericsoftware.com/spine-unity-assets
- https://esotericsoftware.com/spine-unity-main-components
- Unity Character Customization: Modular 3D and Spine2D
