# cfscc
This README file is best viewed on the [GitHub page](http://github.com/commtech/cfscc/).

## Installing Library

##### Downloading Library
You can download a pre-built driver package that includes the C library directly from our
[website](http://www.commtech-fastcom.com/CommtechSoftware.html).

Or, you can download the latest library version from
[Github releases](https://github.com/commtech/cfscc/releases).


## Quick Start Guide

Lets get started with a quick programming example for fun.

_This tutorial has already been set up for you at_ 
[`examples/tutorial/`](https://github.com/commtech/cfscc/tree/master/examples/tutorial).

First, drop `cfscc.dll` and `cfscc.lib` into a test directory. Now that those files are 
copied over, create a new C file (named tutorial.c) with the following code.

```
#include <stdio.h> /* fprintf */
#include <stdlib.h> /* EXIT_SUCCESS, EXIT_FAILURE */
#include <fscc.h> /* fscc_connect, fscc_disconnect, fscc_handle
                     fscc_write, fscc_read */

int main(void)
{
	fscc_handle h;
	int e = 0;
	char odata[] = "Hello world!";
	char idata[20] = {0};
	unsigned tmp;

	/* Open port 0 in a blocking IO mode */
	e = fscc_connect(0, 0, &h);
	if (e != 0) {
		fprintf(stderr, "fscc_connect failed with %d\n", e);
		return EXIT_FAILURE;
	}

	/* Send "Hello world!" text */
	fscc_write(h, odata, sizeof(odata), &tmp, NULL);

	/* Read the data back in (with our loopback connector) */
	fscc_read(h, idata, sizeof(idata), &tmp, NULL);

	fprintf(stdout, "%s\n", idata);

	fscc_disconnect(h);

	return EXIT_SUCCESS;
}
```

For this example I will use the Visual Studio command line compiler, but
you can use your compiler of choice.

```
# cl /W4 /MT tutorial.c cfscc.lib /I ../../src/
```

Now attach the included loopback connector.

```
# tutorial.exe
Hello world!
```

You have now transmitted and received an HDLC frame! 


## API Reference

There are likely other configuration options you will need to set up for your 
own program. All of these options are described on their respective documentation page.

- [Append Status](https://github.com/commtech/cfscc/blob/master/examples/append-status/append-status.c)
- [Clock Frequency](https://github.com/commtech/cfscc/blob/master/examples/clock-frequency/clock-frequency.c)
- [Ignore Timeout](https://github.com/commtech/cfscc/blob/master/examples/ignore-timeout/ignore-timeout.c)
- [Memory Cap](https://github.com/commtech/cfscc/blob/master/examples/memory-cap/memory-cap.c)
- [Purge](https://github.com/commtech/cfscc/blob/master/examples/purge/purge.c)
- [Registers](https://github.com/commtech/cfscc/blob/master/examples/registers/registers.c)
- [TX Modifiers](https://github.com/commtech/cfscc/blob/master/examples/tx-modifiers/tx-modifiers.c)


## Dependencies
TODO


## License

Copyright (C) 2013 [Commtech, Inc.](http://commtech-fastcom.com)

Licensed under the [GNU General Public License v3](http://www.gnu.org/licenses/gpl.txt).
