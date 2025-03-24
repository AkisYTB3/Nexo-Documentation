---
hidden: true
---

# 🚪 Carpentry

This is an addon for Nexo that adds several new CustomBlock types.\
It allows for custom doors, trapdoors, stairs, slabs and transparent blocks.\
Below will be examples for each of the different types

{% hint style="danger" %}
**This addon is still not available**
{% endhint %}

{% hint style="warning" %}
Note that each of the types are currently limited to only 4 variations.
{% endhint %}

{% hint style="danger" %}
This addon relies on Waxed Copper Blocks to work.\
The addon attempts to re-add this logic by marking "Fake Waxed Copper" blocks.\
If you do not care about letting players wax copper, you can disable this in `plugins/Carpentry/config.yml` for some performance gain.\
\
Care should also be taken to convert your existing world.\
As of 1.21, trial chambers generate with Waxed Copper blocks, which might cause some unintended issues.
{% endhint %}

### Custom Stairs

```yaml
custom_stair:
  material: PAPER
  itemname: Custom Stair
  Pack:
    parent_model: block/stairs
    textures:                      # Example if one wants different textures
      bottom: block/reinforced_deepslate_bottom
      side: block/reinforced_deepslate_side
      top: block/reinforced_deepslate_top
    #texture: block/diamond_block  # Optional formatting if only using 1 texture
  Mechanics:
    custom_block:
      type: STAIR
      custom_variation: 1          # 1-4 are available
      model: custom_stair          # the itemid of your item, unless you provided a model not textures
```

### Custom Slabs

```yaml
custom_slab:
  material: PAPER
  itemname: Custom Slab
  Pack:
    parent_model: block/slab
    textures:
      bottom: block/reinforced_deepslate_bottom
      side: block/reinforced_deepslate_side
      top: block/reinforced_deepslate_top
    #texture: block/diamond_block  # Optional formatting if only using 1 texture
  Mechanics:
    custom_block:
      type: SLAB
      custom_variation: 1          # 1-4 are available
      model: custom_slab          # the itemid of your item, unless you provided a model not textures
```

### Custom Doors

Door-setup is a bit different than the other blocks, as it requires two configs.\
This is because the item-model in hand will look incorrect if it uses the block-parent-models\
The second config is just so that Nexo generates the necessary models\
If you provide your own json-model, you can skip the second config\\

ItemConfig for held item:

```yaml
custom_door:
  material: PAPER
  itemname: Custom Door
  Pack:
    parent_model: item/generated   # This is used for the item when held in hand
    texture: block/oak_door        # The texture to use for the item in hand
  Mechanics:
    custom_block:
      type: DOOR
      custom_variation: 1          # 1-4 are available
      model: custom_door_placed    # The itemid of the second config, that generates the block-model
```

ItemConfig for placed-block:

```yaml
custom_door_placed:
  # Handles the generation of the model the placed blocks should use
  # This is the same as all other block-types use in their Pack section
  # But split apart due to how held door-items work
  Pack:
    parent_model: block/door_bottom_left        # Default parent-model for doors
    textures:
      bottom: block/reinforced_deepslate_bottom
      top: block/reinforced_deepslate_top
  # Extra properties to prevent item from being "registered" as a NexoItem
  injectId: false
  excludeFromInventory: true
  excludeFromCommands: true
```

### Custom Trapdoors

```yaml
custom_trapdoor:
  material: PAPER
  itemname: Custom Trapdoor
  Pack:
    parent_model: block/template_orientable_trapdoor_bottom
    textures:
      texture: block/reinforced_deepslate_side
    #texture: block/diamond_block  # Optional formatting if only using 1 texture
  Mechanics:
    custom_block:
      type: TRAPDOOR
      custom_variation: 1         # 1-4 are available
      model: custom_trapdoor      # The itemid of the second config, that generates the block-model
```

### Custom Transparent

This type allows for transparent blocks, useful for leaves etc.\
For normal blocks that do not require transparency, use [NoteBlock Mechanic](../mechanics/custom-block-mechanics/noteblock-mechanic/)

```yaml
custom_grate:
  material: PAPER
  itemname: Custom Grate
  Pack:
    parent_model: block/cube_all
    texture: block/reinforced_deepslate_side
  Mechanics:
    custom_block:
      type: GRATE
      custom_variation: 1          # 1-4 are available
      model: custom_grate          # The itemid of the second config, that generates the block-model
```
