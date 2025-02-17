---
icon: file-zipper
---

# ResourcePack

### ResourcePack-Structure

The ResourcePack has changed from what some might be used to.\
This is in an effort to make importing third-party ResourcePacks a lot easier.\
Below is an example of the new structure.\
For reference; `Oraxen/pack/models` -> `Nexo/pack/assets/minecraft/models`

{% code title="" %}
```
📁Nexo
└── 📁pack
    └── 📁assets
    │    ├── 📁minecraft
    │    │    ├── 📁models
    │    │    │    ├── 📁item
    │    │    │    │    └── 📑paper.json
    │    │    │    └── 📑custom_model.json
    │    │    └── 📁textures
    │    │         └── 🖼️something.png
    │    └── 📁custom_namespace
    │        └── 📁models
    │            └── 📑custom.json
    │  
    └── 📁external_packs
        ├── 📁DefaultPack.zip
        ├── 📁custom_resourcepack.zip
        └── 📁custom_resourcepack2
            └── 📁assets
                └── 📁custom_namespace2
```
{% endcode %}

Goal is to let users merge resourcepacks in via either ZIPs or directories, outside of the normal assets folder.\
This would dynamically merge in any conflicting files, like a paper.json or sounds.json, instead of migrating it to oraxen-configs to be generated.\
Meaning that pack-import instructions on your end now boils down to:\
Put `my_pack.zip` inside `Nexo/pack/external_packs`

### Obfuscation

Nexo has a built in way to "obfuscate" the content of your resource-pack.\
This is done by randomizing all file-names in an attempt to make it very hard and annoying to try and take stuff from it for pirates.\
It comes with three modes, `NONE`, `SIMPLE`, `FULL`\
\
**NONE** - Self-explanatory, does not obfuscate pack in any way\
**SIMPLE** - Obfuscates filenames only\
`namespace:model/path.json` -> `namespace:bba2d60b-8e3e-4051-9734-fef92766777f`\
**FULL** - Obfuscates namespace & filename;\
`namespace:model/path.json` -> `c491303e-ba1e-4037-a59d-62b5fdfb6bb8:bba2d60b-8e3e-4051-9734-fef92766777f`

### PackServer

Nexo has 2 types of ways to upload & dispatch the ResourcePack it generates\
**POLYMATH** - A dedicated server hosted by Nexo-Team that your server uploads the pack to\
This server is currently hosted in Germany\
**SELFHOST** - Server-Instance hosted on your machine. Requires you to configure the `public_address` and ensure a given port is open.\
The API is also set up so that one could extend the `NexoPackServer-Interface` and create ones own.

### Importing

Nexo lets you import Third-Party ResourcePacks in several ways.\
The recommended one is shown above, by adding a directory or .zip to \`plugins/Nexo/pack/external\_packs\`\
There is also `Plugin.import.from_location` in settings.yml, letting you specify a directory/zip relative to your plugins folder\
There is also `Plugin.import.from_url` in settings.yml, letting you specify any url that Nexo will download a directory/zip from and include
