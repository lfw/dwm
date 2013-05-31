## DWM 6.0_0.1

My modifications to [DWM] available at [suckless.org]. 
These mods are mostly around target code execution that allows me to run multiple virtual systems in a headless format and use X forwarding to unify them in 1 enviroment.

#### Features

 * Added function to set active target
 * Added array to set available targets (config.h)
 * Modified spawn() function to execute on remote target if applicable.

#### Thoughts

Since the target configuration does nothing more then offer a prefixed command to anything being spawed, you might find some other uses for this suck as torifying commands. If you think of other ideas, let me know.
