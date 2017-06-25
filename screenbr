#!/usr/bin/python

import re
import sys
import subprocess

def moreorless(option, usage):
    xrandrout = subprocess.check_output('xrandr --current --verbose', shell=True)
    s = re.search('(.+)\sconnected\sprimary', xrandrout)
    screenname = s.group(1)
    cb =re.search('Brightness:\s(\d.\d+)', xrandrout)
    currentbrightness = float(cb.group(1))
    if option == '+':
        if currentbrightness == 1:
            print 'Screen brightness is already at maximum level'
            sys.exit(0)
        else:
            cmd = "/usr/bin/xrandr --output {} --brightness {}".format(screenname, currentbrightness + 0.1)
            subprocess.call(cmd, shell=True)
    elif option == '-':
        if currentbrightness <= 0.1:
            print 'Screen brightness is already at minimum level'
            sys.exit(0)
        else:
            cmd = "/usr/bin/xrandr --output {} --brightness {}".format(screenname, currentbrightness - 0.1)
            subprocess.call(cmd, shell=True)
    elif option == 'min':
        if currentbrightness == 0.1:
            print 'Screen brightness is already at minimum (but visible) level'
            sys.exit(0)
        else:
            cmd = "/usr/bin/xrandr --output {} --brightness {}".format(screenname, 0.1)
            subprocess.call(cmd, shell=True)
    elif option == 'max':
        if currentbrightness == 1:
            print 'Screen brightness is already at maximum level'
            sys.exit(0)
        else:
            cmd = "/usr/bin/xrandr --output {} --brightness {}".format(screenname, 1)
            subprocess.call(cmd, shell=True)
    elif option == 'deep':
        if raw_input('Screen brightness will be set to 0. Are you sure? [n/Y] ') == 'Y':
            cmd = "/usr/bin/xrandr --output {} --brightness {}".format(screenname, 0)
            subprocess.call(cmd, shell=True)
        else:
            sys.exit(0)
    else:
        print usage
        sys.exit(1)
    sys.exit(0)

def main():
    usage= 'Usage:  screenbr option \n\nOptions:\n   +      to increase screen brightness by 0.1\n   -      to decrease screen brightness by 0.1\n   max    to set screen brightness to maximum level (1)\n   min    to set screen brightness to minimum, but still readable level (0.1)\n   deep   to set screen brightness to minimum level (0)'    
    if len(sys.argv) > 2:
        print 'Only one argument accepted, {} given\n'.format(len(sys.argv)-1)
        print usage
        sys.exit(1)
    try:
        option = sys.argv[1]
        moreorless(option, usage)
    except IndexError:
        print usage
        sys.exit(1)
if __name__ == '__main__':
    main()
      
