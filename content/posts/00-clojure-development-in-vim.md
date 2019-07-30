* Install NeoVim
* Git clone Pathogen inside of `~/.config/nvim/autoload`
* Git clone the following packages inside of `~/.config/nvim/bundle`
	* Rainbow Parentheses
	* Vim Clojure Static
	* Vim Fireplace
* Update your vim file (unlike vim's location `~/.vimfile` NeoVim will require the file to be located at `~/.config/nvim/init.vim`).  Then execute `pathogen#infect()` which enables Pathogen module loading
* Turn on the settings for Rainbow Parentheses
		```
		au VimEnter * RainbowParenthesesToggle
		au Syntax * RainbowParenthesesLoadRound
		au Syntax * RainbowParenthesesLoadSquare
		au Syntax * RainbowParenthesesLoadBraces
		```
* Turn on Clojure Static 
* Navigate to your project in two terminals
* Start up your leiningen REPL using `lein repl`
* In the other terminal start nvim.
* Confirm that vim can acceess the repl by hovering over a function call and typing `cpp` inside of Command mode.  `(println "Hello World!")` can work!
* Shazam you now have a working Clojure REPL working inside of your code editor!
