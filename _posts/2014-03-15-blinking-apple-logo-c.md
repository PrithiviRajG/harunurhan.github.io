---
layout: post
title: Blinking Apple Logo
---
I was bored and I realized that my macbook's apple logo looks amazing in dark, first I wondered how I can make it brighter. Answer was simple, changing macbook's display brightness changes apple logo brightness too. Then I wondered how I can make a show with it(on-off-on-off). It was hardly possible to do it by using brightness buttons. In that case C helped me.

Initially, I searched how to change display brightness with c code. In 10-15 minutes I completed writing code for it. Then I edited my code to blink, on-off-on-off(per second).


## appleblink.c
~~~~
#include <stdio.h>
#include <IOKit/graphics/IOGraphicsLib.h>
#include <ApplicationServices/ApplicationServices.h>

int main(int argc, char **argv)
{
    CGDirectDisplayID targetDisplayId = CGMainDisplayID();
    io_service_t service = CGDisplayIOServicePort(targetDisplayId);
    CFStringRef key = CFSTR(kIODisplayBrightnessKey);
    int blinktime = strtof(argv[1], NULL);
    int count = 0;
    while(count <= blinktime)
    {
        IODisplaySetIntegerParameter(service, kNilOptions, key, 0); // turn off
        sleep(1); // wait for a while
        IODisplaySetIntegerParameter(service, kNilOptions, key, 1000); // turn on
        sleep(1);
        count++;
    }
    printf("appleblink ended \n");
    return 0;
}
~~~~

it needs IOKit and ApplicationServices to be complied, you can compile it like this >>

`gcc -o appleblink appleblink.c -framework IOKit -framework ApplicationServices`

You may get a warning, don't care go on.
running is the same

`./appleblink 4` this make it blink 4 times, you can change it.
