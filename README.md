## Snapr - Social photo messaging from the terminal

Snap and send a selfie directly from the terminal to everyone watching in your network.

Note: Refer to https://github.com/peterept/snapr for screenshots

# Download
   ```
   https://github.com/ltfschoen/snapr
   ```

# Installation

* Open the Terminal 
    * macOS: CMD+SPACE, enter "Terminal", press Enter)

* Uninstall RVM
    ```
    rvm implode
    sudo rm -rf /Users/<your_username>/.rvm/
    ```

* Remove RVM from ~/.bash_profile and ~/.bash_rc

* Fix and update Homebrew 
    ```
    brew doctor
    brew update
    ```

* Install RBEnv
    ```
    brew install rbenv
    rbenv init
    brew install ruby-build
    ```

* Configure Gitignore globally
    ```
    git config --global core.excludesfile ~/.gitignore
    printf "vendor/bundle\n.DS_Store\n" >> ~/.gitignore
    ```

* Set default bundle path
    ```
    mkdir -p ~/.bundle
    printf -- "---\nBUNDLE_PATH: vendor/bundle" >> ~/.bundle/config
    ```

* Instantiate RBEnv with Shell using ~/.bash_profile
    ```
    printf 'eval "$(rbenv init -)"' >> ~/.bash_profile
    ```

* Reload your ~/.bash_profile
    ```
    source ~/.bash_profile
    ```

* Add IRB autocompletion
    ```
    touch ~/.irbrc
    printf "require 'irb/completion'" >> ~/.irbrc
    ```

* Install RBEnv Gemset https://github.com/jf/rbenv-gemset
    ```
    brew install rbenv-gemset
    ```

# Change into Snapr project directory
    ```
    cd snapr
    ```

* Show all available RBEnv versions of Ruby 
    ```
    rbenv install --list
    ```

* Install Ruby v2.2.0 with RBEnv
    ```
    rbenv install 2.2.0
    ```

* Initialise Gemset
    ```
    rbenv gemset init
    ```

* Create Gemset under specific Ruby version
    ```
    rbenv gemset create 2.2.0 app-snapr
    ```

* List Gems installed
    ```
    rbenv gemset list
    ```

* Show current Ruby version
    ```
    ruby -v
    which ruby
    ```

# Switch to Ruby version with RBEnv for local app
    ```
    rbenv local 2.2.0

* Show updated Ruby version
    ```
    ruby -v
    ```

* Install other Gems for each RBEnv Ruby version

    * Uninstall Image Magick 7 (if exists since it conflicts)
        ```
        brew uninstall imagemagick && brew unlink imagemagick --force
        ```

    * Install Image Magick (version ImageMagick 6.9.9-5)
        ```
        brew install imagemagick@6 && brew link --force imagemagick@6
        ```

    * Show version of Image Magick installed
        ```
        convert --version
        ```

    * Check relinking occurred after migration using Migration Assistant on macOS (i.e. not `pkg-config: command not found`)
        ```
        Wand-config --ldflags --libs
        ```

    * Reinstall pkg-config http://www.rubydoc.info/gems/rmagick/frames#install
        ```
        brew uninstall pkg-config
        brew install pkg-config
        brew unlink pkg-config
        brew link pkg-config
        ```

    * Fix if error occurs `Can't find MagickWand.h` with:

        * Solution: Find library `mdfind MagickWand.h`

    * Install RMagick gem (v2.16.0)
        ```
        gem install rmagick -v 2.16.0   
        ```

    * Install Catpix gem
        ```
        gem install catpix -v 0.2.0
        ```

    * Install Lolcommits gem
        ```
        gem install lolcommits    
        ```

* Rehash RBEnv shims (after installing binaries)
    ```
    rbenv rehash
    ```

* Pristine gems
    ```
    gem pristine --all
    ```

* Install Plugin - takes snapshot with webcam every time you git commit code. Archives a lolcat style image https://github.com/lolcommits/lolcommits-plugin-sample
    ```
    gem install lolcommits-plugin-sample
    lolcommits --config -p plugin-sample
    ```
    * Note: Set enabled to `true`

* List all installed Plugins
    ```
    lolcommits --plugins
    ```

* Wiki and Plugins
    * Link - https://github.com/mroth/lolcommits/wiki/Configuring-Plugins

* Installed Plugins easily enabled, configured or disabled
    ```
    lolcommits --config -p loltext
    ```

* References:
    * RVM 2 RBEnv - https://gist.github.com/ltfschoen/aa549bcb5df9c98d95c81aee4a9a69cf

* Usage Instructions

    * Help
        ```
        ruby snapr.rb 
        ```

    * Watch for chat images in Terminal #1
        ```
        ruby snapr.rb -watch    
        ```

    * Capture and send a chat image in Terminal #2
        ```
        ruby snapr.rb "Hello everyone"    
        ```

        * Note: Error occurs:
            ```
            ~/.rbenv/versions/2.2.0/lib/ruby/gems/2.2.0/gems/lolcommits-0.9.5/lib/lolcommits/runner.rb:32:in `run': undefined method `plugins_for' for {:loldir=>"./"}:Hash (NoMethodError)
            ```

            * Fix by opening and editing 
                ```
                atom ~/.rbenv/versions/2.2.0/lib/ruby/gems/2.2.0/gems/lolcommits-0.9.5/lib/lolcommits/runner.rb
                ```

            * Comment out the 3x blocks in the `run` method that appear as follows: 
                ```
                plugin_manager.plugins_for ...
                end
                ```
