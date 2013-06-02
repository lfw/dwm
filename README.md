## DWM 6.0_1.1

My modifications to [DWM] available at [suckless.org]. 
These mods are mostly around target code execution that allows me to run multiple virtual systems in a headless format and use X forwarding to unify them in 1 enviroment.

## NOTICE!

coonfig.def.h has been modified. You MUST make the following changes to your local config.h or the application will fail to compile.

<pre>
index 7273d69..e6d1591 100644
--- a/config.def.h
+++ b/config.def.h
@@ -2,12 +2,7 @@
 
 /* appearance */
 static const char font[]            = "-*-terminus-medium-r-*-*-16-*-*-*-*-*-*-*";
-static const char normbordercolor[] = "#522b0d";
-static const char normbgcolor[]     = "#292929";
-static const char normfgcolor[]     = "#666666";
-static const char selbordercolor[]  = "#753e12";
-static const char selbgcolor[]      = "#292929";
-static const char selfgcolor[]      = "#ea7d24";
+/* Colors moved to SpawnTargets region */
 static const unsigned int borderpx  = 1;        /* border pixel of windows */
 static const unsigned int snap      = 32;       /* snap pixel */
 static const Bool showbar           = True;     /* False means no bar */
@@ -38,8 +33,11 @@ static const Layout layouts[] = {
  * the command on a remote or local system */
 static const SpawnTarget targets[] = {
        /* Host Name               Command Prefix (limit 5) */
-       { "Localhost",             { NULL } },
-       { "Remote1",               { "ssh", "-Y", "tuvok.lfw.local", NULL } },
+
+        /* host_name   prefix[5]                   normbordercolor normbgcolor normfgcolor selbordercolor selbgcolor selfgcolor */
+
+       { "Localhost",  { NULL },                   "#522b0d",      "#292929",  "#666666",  "#753e12",     "#292929", "#ea7d24" },
+       { "Remote1",    { "ssh", "Remote1", NULL }, "#52000d",      "#290029",  "#660066",  "#750012",     "#290029", "#ea0024" },
 };
</pre>

#### Features

 * Added function to set active target
 * Added array to set available targets (config.h)
 * Modified spawn() function to execute on remote target if applicable.
 * Added localSpawn() function to execute on local system regardless of target selected.
 * Appends status text with target name with multi-monitor support.
 * Added support for each target to have its own color schema.

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

