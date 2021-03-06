                               The LowTeX Manual                                
                               --- ------ ------                                
                                 By Hardmath123                                 
                                                                                
   LowTeX--pronounced "low-tech"--is a small text transformation package that   
generates pretty monospace outputs, specifically for READMEs, licenses, or even 
large block comments. This documentation was generated by LowTeX, and its       
source is bundled with the package. We will walk through the basics of LowTeX   
here. The source for this tutorial is in `example.lt`.                          
                                                                                
                                Monospace is nice.                              
                             Everything is scriptable.                          
                                 Readable sources.                              
                                                                                
                                 Make it a filter.                              
                          Write small, powerful modules.                        
                                Format haikus well.                             
                                                                                
Getting started                                                                 
------- -------                                                                 
   Install LowTeX with `npm install -g      A setting is declared with the line 
lowtex`. Create a new document in your   `@set <name> <value>`. LowTeX mantains 
favorite text editor, preferably set     an internal stack of settings. To      
to a mode that wraps lines of text. To   restore a setting to its previous      
compile, use the `lowtex` command.       value, use `@unset <name>`.            
                                            A block is declared with the line   
   A LowTeX document consists of text,   `@begin <name> <arguments>`, and       
with interspersed DIRECTIVES, which      terminated with the line `@end`.       
are prefixed with an `@`. A directive    Blocks transform the text inside them. 
is either a SETTING, a BLOCK, or a       An example of a block is the UNDERLINE 
COMMAND. Text is processed               block, which underlines the text       
line-by-line, being wrapped and          inside it.                             
aligned according to the settings. A        A command is simply `@<name>        
blank line (or directive) indicates      <arguments>`. For example, @VSPACE N   
the end of a paragraph. A line           adds `n` blank lines.                  
prefixed with `#` is a comment and is       `begin` and `end` can be            
skipped silently.                        abbreviated to `!` and `/`,            
                                         respectively.                          
                                                                                
Planned features                                                                
------- --------                                                                
                                                                                
 1. Embedded tables                                                             
 2. Figlet support for headers, etc.                                            
 3. Better documentation                                                        
 4. More ordered list styles, such as alphabetized and roman.                   
 5. Better error catching and messages                                          
                                                                                
Modules                                                                         
-------                                                                         
NOTE: LowTeX is now INCOMPATIBLE with the old module system implemented by @sl. 
LowTeX is highly configurable. You can (and should!) write your own modules for 
your documents. Modules are nodejs-style. Your module exports a function, which 
accepts a converter instance as an argument, and modifies it somehow.           
Modules are imported using the `@require <path>` syntax, where the path is      
relative to the current working directory.                                      
                                                                                
    module.exports = function(converter) {
      converter.commands.banana = function() {
        this.feedLines(["Banana" + this.nspace(this.get("width") - 6)]);
      };
    };
                                                                                
Converters expose the @ syntax with methods such as set(name, value),           
get(name), unset(name), begin_filter(name, args), and end_filter().             
