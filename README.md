This project contains the following concepts as explained in the flow:

A command interpreter to manipulate data without a visual interface, like in a Shell (perfect for development and debugging)

A website (the front-end) that shows the final product to everybody: static and dynamic

A database or files that store data (data = objects)

An API that provides a communication interface between the front-end and your data (retrieve, create, delete, update them)

The Console

This involves creating a line interactive command session that enables you to easily manipulate your data using a shell like environment.The console is thus created using a cmd which is as base class and only requires to be subclassed and used as desired.
How to start it

A command line interprator can be started by calling te python file used to create it eg

#Assuming start.py contains our commandline code
python3 start.py
It can also be started by making the file containing our commands excecutable then calling the file on our normal shell as below.

#Remember the file must be excecutable
$ ./start.py
How to use it with examples

The following code explains better what I could have put to words.Try it after reading all about cmd to understand better.

#!/usr/bin/python3

import cmd 

class OverideBase(cmd.Cmd):
    """Illustrating the process one after another once a command interprater is started to stop"""
    def cmdloop(self, intro=None):
        print("cmdloop({})".format(intro))
        return cmd.Cmd.cmdloop(self, intro)
    
    """Excecuted when cmdloop() is called"""
    def preloop(self):
        print("preloop")
    
    """Excecuted when cmdloop() is about to return"""
    def postloop(self):
        print("postloop")

    """ Separates a line into command and arguments"""
    def parseline(self,line):
        print("parseline({}) =>".format(line))
        ret = cmd.Cmd.parseline(self, line)
        print(ret)
        return ret

    """Interpate the argument as if it has been written as a response to the prompt """
    def onecmd(self,s):
        print("onecmd({})".format(s))
        return cmd.Cmd.onecmd(self, s)
    
    """Called when an empty line is entered in the prompt,repeats the last nonempty string if not overriden"""
    def emptyline(self):
        print("emptyline()")
        return cmd.Cmd.emptyline(self)

    """Called when the command is not recognised and prints an error if not overriden"""
    def default(self, line):
        print("default({})".format(line))
        return cmd.Cmd.default(self, line)
    
    """Excecuted just before the command line is interprated but after input prompt is generated"""
    def precmd(self, line):
        print("precmd({})".format(line))
        return cmd.Cmd.precmd(self, line)
    
    """Excecuted just after dispatch is finished"""
    def postcmd(self, stop, line):
        print("postcmd({}{})".format(stop,line))
        return cmd.Cmd.postcmd(self, stop, line)
    
    def do_greet(self,line):
        print("hello,",line)

    def do_EOF(self,line):
        "Exit"
        return True
    
if __name__ == '__main__':
    OverideBase().cmdloop('Illustrating the cmd process')
Once the prompt comes up try this commands.
