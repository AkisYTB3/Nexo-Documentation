---
description: >-
  This mechanism allows you to realize an extremely customizable mechanism
  without programming
cover: >-
  https://cdn.discordapp.com/attachments/896841738621177896/966825489098489856/unknown.png
coverY: 0
---

# Custom Mechanic

## How does it work?

This mechanic is for items only and does not work with blocks/furniture.\
For that check the [clickAction mechanic](clickaction-mechanic.md). The mechanics let you create subsections composed of 3 parts:\\

* **Event**: when is this mechanic triggered? e.g. when you right-click on a block
* **Conditions**: a set of conditions that must be satisfied. e.g. having a permission
* **Actions**: a set of actions to perform. e.g. send a command or a message

{% hint style="info" %}
An optional settings called oneUsage allows you to imitate the use of an item at 1.
{% endhint %}

## A comprehensive example

```yaml
myitem:
  Mechanics:
    custom:
      test:
        one_usage: false
        event: "CLICK:right:all"
        conditions:
          - '#player.hasPermission("example.permission")'
        actions:
          - "[console] give <player> cooked_beef 1"
```

In this example, the subsection `test` defines a custom mechanic triggered when someone right click (on a block or in the air).\
If this player has the permission `example.permission`, the console will perform the give command and replace \<player> by the player name.\
The item won't be consumed (oneUsage: false).

## Available events

### CLICK:mouse\_click\_type:target\_type

Called when you click with the item.

**mouse\_click\_type**: `[ right, left, all ]`\
**target\_type**: `[ block, air, all ]`

### DROP

Called when you drop the item.

### PICKUP

Called when you pick up the item.

### BREAK

Called when a player breaks an item.

### EQUIP

Called when a player equips an item.

### UNEQUIP

Called when a player unequips an item.

### INV\_CLICK

Called when a player clicks an item in an inventory.

### DEATH

Called when a player dies and would normally drop the given item.

## Available conditions

### HAS\_PERMISSION:the.permission

**the.permission**: `The permission required by the player using the item`

## Available actions

### COMMAND:sender:command

**sender**: `[ console, player ]`\
**command**: `The command to perform. The placeholder <player> can be used.`

### MESSAGE:content

**content**: `Content of the message to send (it supports minimessage format)`

### ACTIONBAR:content

**content**: `Content of the message to send (it supports minimessage format)`
