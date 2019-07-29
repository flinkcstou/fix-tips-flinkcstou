Pro Tips
============


This needs some organization. This is mostly a list of links, some short bits of tips which aren't links. This is categorized according to where it best fits in the syllabus.


## Fundamentals

* [HTML5 Standard](http://www.whatwg.org/)
* [HTML5 elements list with commentary](http://html5doctor.com/element-index/)
* [CSS2 Specificiation](http://www.w3.org/TR/CSS2/)
* [CSS3 Specificiation](http://www.w3.org/TR/#tr_CSS) (see under Drafts)
* [CSS Compatibility](http://caniuse.com)
* [Javascript Specificiation](http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf)
* [Javascript Documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference)
* [Stack Overflow](http://stackoverflow.com)
* [Github](http://github.com) 
* [G+](http://google.com/plus)




## Unit 1


### HTML/CSS

Fairly easy material for those with some previous experience.

For those with little prior exposure, be certain to learn about how the web works. At the end of the day, it is all about text files saved on a hard drive, and any image files used by the website.


### Cross-browser compatibility

Code for Chrome, you can expect it to work the same in Safari. Check in Firefox, but for real compatibility you must check in Internet Explorer 9, IE10, and perhaps IE8.

For Max & Linux users, you can get [Virtual Box](https://www.virtualbox.org/wiki/Downloads).

After you have installed Virtual Box, checkout [ievms](https://github.com/xdissent/ievms). It downloads and installs any number of Windows virtual machines with the following browsers: IE6, IE7, IE8, IE9, and IE10. Run this in your command-line to get started:

`curl -s https://raw.github.com/xdissent/ievms/master/ievms.sh | bash`


### Browser compatibility and tools

* http://caniuse.com
* http://quirksmode.org



### Git / Github

Know that git is _not_ github. There are [other hosts](http://bitbucket.org) for git respositories, and git is used in other ways, build services like [Adobe Phonegap Build](http://build.phonegap.com) or [Travis CI](https://travis-ci.org/)

If you're having trouble with Git I recommend [this tutorial](http://rogerdudler.github.io/git-guide/).

### Command Line

* Use `trash` instead of `rm` to make the terminal safer. (Requires OSX/Homebrew or Linux)
* Learn how to use curl

[More cool things](http://coding.smashingmagazine.com/2012/10/29/powerful-command-line-tools-developers/) which you can use the command line for.

### Standards


### CSS / Design

* [CSS Tricks](http://css-tricks.com/)
* [Shapes of CSS](http://css-tricks.com/examples/ShapesOfCSS/)
* [CSS3 Info](http://www.css3.info/)
* [Smashing Magazine](http://www.smashingmagazine.com/)
* [Codepen](http://codepen.io/)
* [A List Apart](http://alistapart.com/)




## Unit 2




## Unit 3




## Unit 4




## Miscellaneous


### Blogs I Read

* http://html5rocks.com
* http://labnotes.org
* http://weblog.bocoup.com/
* http://thechangelog.com/
* http://html5weekly.com
* http://javascriptweekly.com/
* http://webdesign.tutsplus.com/
* http://www.netmagazine.com/


### Books

* [CSS Pocket Reference](http://www.amazon.com/CSS-Pocket-Reference-Eric-Meyer/dp/1449399037)
* [The Art of Unix Programming](http://www.amazon.com/Programming-Addison-Wesley-Professional-Computng-Series/dp/0131429019)
* [jQuery in Action](http://www.amazon.com/jQuery-Action-Second-Edition-Bibeault/dp/1935182323)
* [The Little Schemer](http://www.amazon.com/The-Little-Schemer-4th-Edition/dp/0262560992)


### Web Standards / Internet Standards / Reference

* [HTTP](http://en.wikipedia.org/wiki/Hypertext_Transfer_Protocol)
* [HTTP Status Codes](http://en.wikipedia.org/wiki/List_of_HTTP_status_codes)


### Tools


#### Sublime Text

Sublime is excellent. Multiple cursors! The Command Palate! Package management system. If you use Sublime you need to know just a little about The Command Palate, and the Package Management.

To open the Command Palette use ⇧⌘P (Shift Apple P). 

From here type things like you would type into any search engine. Try typing "Install" this will bring up the package installer if it is available. If not follow the directions in the Tutsplus links below.

Install the Markdown Previewer plug in and after it successfully installs (keep an eye on sublime's status bar at the bottom) open the Command Palette and type markdown. The list should populate and you'll find an item "Markdown Preview: open Markdown cheat sheet".


* [Sublime Text 2](http://www.sublimetext.com/2)
* [Sublime Text First Steps](https://tutsplus.com/tutorial/sublime-text-2-first-steps/)
* [Sublime Text  Tips & Tricks](http://net.tutsplus.com/tutorials/tools-and-tips/sublime-text-2-tips-and-tricks/)





#### Mac OSX


#### Homebrew (OSX)

[Install Homebrew](http://mxcl.github.io/homebrew/)

`ruby -e "$(curl -fsSL https://raw.github.com/mxcl/homebrew/go)"`

Follow the instructions after the command. This requires Xcode and the Command Line Tools for Xcode. Command Line Tools can be installed from within Xcode. Go to Xcode > Preferences > Downloads in the Xcode menus to find this plugin.


#### Dotfiles

Another good reason to work on a Linux-compatible OS. Many programs use hidden files in your home directory for configuration. If you keep them in github, it's easy to get setup on a new machine.