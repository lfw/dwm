## DWM 6.0_1.1

My modifications to [DWM] available at [suckless.org]. 
These mods are mostly around target code execution that allows me to run multiple virtual systems in a headless format and use X forwarding to unify them in 1 enviroment.

## NOTICE!

coonfig.def.h has been modified. You MUST make the following changes to your local config.h or the application will fail to compile.

<pre>
index 102c719..7273d69 100644
--- a/config.def.h
+++ b/config.def.h
@@ -38,8 +38,8 @@ static const Layout layouts[] = {
  * the command on a remote or local system */
 static const SpawnTarget targets[] = {
        /* Host Name               Command Prefix (limit 5) */
-       { "Localhost",             { NULL } },
-       { "Remote1",               { "ssh", "-Y", "tuvok.lfw.local", NULL } },
+       { "Localhost",             { NULL }, "#ea7d24" },
+       { "Remote1",               { "ssh", "-Y", "tuvok.lfw.local", NULL }, "#0000FF" },
 };
</pre>

#### Features

 * Added function to set active target
 * Added array to set available targets (config.h)
 * Modified spawn() function to execute on remote target if applicable.
 * Added localSpawn() function to execute on local system regardless of target selected.
 * Appends status text with target name with multi-monitor support.

#### Using Local Spawn

For keybindings that you want to always run on the local system, use the localSpawn() function as follows:
<pre>{ MODKEY,   XK_n,	localSpawn,	{.v = (const char*[]){"amixer", "sset", "Master", "toggle", NULL} } },</pre>

#### Sample .ssh/config

I keep all my SSH XForwarding settings in my .ssh/config file so i can modify them on witout restarting DWM. I have fond the following settings to be optimal with my setup.

<pre>
Host Remote1 
  ForwardX11 yes
  ForwardX11Trusted yes
  ForwardAgent yes

Host Remote2
  ForwardX11 yes
  ForwardX11Trusted yes
  ForwardAgent yes

Host Remote3
  User OtherUser
  IdentityFile ~/.ssh/OtherUser_rsa
  ForwardX11 yes
  ForwardX11Trusted yes
  ForwardAgent yes
</pre>

#### Thoughts

Since the target configuration does nothing more then offer a prefixed command to anything being spawed, you might find some other uses for this suck as torifying commands. If you think of other ideas, let me know.

