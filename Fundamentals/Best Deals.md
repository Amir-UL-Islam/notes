- Static members belongs to the class rather than instance. So at compile time, player.getType() is converted to Player.getType()

- This is admittedly very misleading when reading someone else’s code, and it is best practice to always use the class name when calling a static method.
