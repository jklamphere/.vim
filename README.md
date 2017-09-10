# .vim
vimrc and plugins

Installation:
REMOVE OLD VIM:
    
    sudo apt-get remove vim vim-runtime gvim
    sudo apt auto remove vim
    sudo apt-get remove vim-tiny vim-common vim-gui-common vim-nox
    
 COMPILE VIM WITH PYTHON SUPPORT FOR YouCompleteMe:

DEPENDENCIES:
    
    sudo apt-get install libncurses5-dev libgnome2-dev libgnomeui-dev \
    libgtk2.0-dev libatk1.0-dev libbonoboui2-dev \
    libcairo2-dev libx11-dev libxpm-dev libxt-dev python-dev \
    python3-dev ruby-dev lua5.1 liblua5.1-dev libperl-dev git \
    clang clang-format build-essential cmake \   
    
    
COMPILE
    
    cd ~
    git clone https://github.com/vim/vim.git
    cd vim
    ./configure --with-features=huge \
            --enable-multibyte \
            --enable-rubyinterp=yes \
            --enable-pythoninterp=yes \
            --with-python-config-dir=/usr/lib/python2.7/config-x86_64-linux-gnu \
            --enable-python3interp=yes \
            --with-python3-config-dir=/usr/lib/python3.5/config-3.5m-x86_64-linux-gnu \
            --enable-perlinterp=yes \
            --enable-luainterp=yes \
            --enable-gui=gtk2 \
            --enable-cscope \
            --prefix=/usr/local
    make VIMRUNTIMEDIR=/usr/local/share/vim/vim80

Change to current verion number:

    make VIMRUNTIMEDIR=/usr/share/vim/vim80
    sudo make install
    sudo update-alternatives --install /usr/bin/editor editor /usr/bin/vim 1
    sudo update-alternatives --set editor /usr/bin/vim
    sudo update-alternatives --install /usr/bin/vi vi /usr/bin/vim 1
    sudo update-alternatives --set vi /usr/bin/vim
    
 CLONE REPO:   
    git clone git://github.com/NOFUNEVER/.vim.git

Create symlinks:

    ln -s ~/.vim/vimrc ~/.vimrc
    ln -s ~/.vim/gvimrc ~/.gvimrc
    
   If Fails:
        
        rm ~/.vimrc
        and try again
    
Switch to the `~/.vim` directory, and fetch submodules:

    cd ~/.vim
    git submodule init
    git submodule update
    git submodule foreach --recursive git submodule update --init
    sudo git submodule update --init --recursive

To add new plugins:

    git submodule add http://github.com/user/plugin.git ~/.vim/pack/jkl-plugins/start/ 
    git add .
    git commit -m "Install Fugitive.vim bundle as a submodule."
    
    //git add . adds all files currently in the folder
To update an individual plugin enter the root folder of the plugin and:
    
    git pull origin master

Upgrading all bundled plugins:
       
    git submodule foreach git pull origin master
    or 
    git submodule foreach --recursive git submodule update --init

   

YCM NEEDS BINARIES COMPILED:
    
   
    sudo git submodule update --init --recursive
  

Compiling YCM with semantic support for C-family languages:

    cd ~/.vim/pack/jkl-plugins/start/YouCompleteMe
    sudo ./install.py --clang-completer
 
      
    
-----------------------------------------------------------------------------------------------------------
PER PROJECT REQUIREMENTS
sudop    
    
To make make YCM see entire project:

    Run ./config_gen.py PROJECT_DIRECTORY, where PROJECT_DIRECTORY is the root directory of your project's build system (i.e. the one       containing the root Makefile, etc.)
    You can also invoke it from within Vim using the :YcmGenerateConfig or :CCGenerateConfig
    
To make clang-format work in your project:
    
    clang-format -style=google -dump-config > .clang-format

