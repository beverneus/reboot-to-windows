# Reboot to Windows

This is a small Gnome extension that adds the ability to reboot directly to Windows.

### Build and install the extension

Requirements:

- make
- nodejs and npm
- gettext

To build the extension run the following command:

`$ make pack COMMAND={rebootCommand}`

If all goes well this will generate a zip file in the project folder.

To install the extension just run the following command:

`$ make install COMMAND={rebootCommand}`

### Reboot command

If you don't specify COMMAND it will default to /usr/bin/call-bill
I have this setup as
```
#include <stdlib.h>
#include <unistd.h>

int main() {
    // Set BootNext to Windows (Boot0000)
    system("efibootmgr -n 0000");
    // Reboot the system
    execl("/sbin/reboot", "reboot", NULL);
    return 0;
}
``` 
Compiled using gcc.

You can find out what Bootnumber Windows has using
```
sudo efibootmgr
```