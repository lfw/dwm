## DWM

My modifications to [DWM] available at [suckless.org]. 
These mods are mostly around remote code execution that allows me to run multiple virtual systems in a headless format and use X forwarding to unify them in 1 enviroment.

note: i do have bash scripts in my config. Still working out bugs that only allow me to send 1 command to the target host. (no arguments)

#### Modifications

 * Added function to set active target
 * Added array to set available targets (config.h)
 * Modified spawn() function to execute on remote target if applicable.

#### Thoughts

Since the target configuration does nothing more then offer a prefixed command to anything being spawed, you might find some other uses for this suck as torifying commands. If you think of other ideas, let me know.
