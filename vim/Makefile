# Make file for install vim parts

# defines the shell to the make application
SHELL := /bin/bash

# bashrc file name
VIMRC := vimrc

.PHONY := install


install: ${VIMRC}
	@echo -e "\n${BROWN}# VIM INSTALL${END_COLOR}"
	@echo -e "${BLUE}placing ${VIMRC} file at '$(USER_HOME)/.$(VIMRC)'${END_COLOR}"
	install ${VIMRC} $(USER_HOME)/.$(VIMRC) -m 0644
	@echo -e "${BLUE}creating VIM directories:${END_COLOR}"
	mkdir -pv $(USER_HOME)/.vim/{plugin,doc,spell,syntax,colors}
	curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
	install colors/pantuza.vim $(USER_HOME)/.vim/colors -m 0644
	@echo -e "\n${BLUE}Installing dependencies${END_COLOR}"
	[ -x /usr/bin/clang ] && echo "clang OK" || sudo zypper in -y llvm-clang
	[ -x /usr/bin/ctags ] && echo "ctags OK" || sudo zypper in -y ctags
	[ -x /usr/bin/aspell ] && echo "aspell OK" || sudo zypper in -y aspell aspell-pt_BR
	@echo -e "\n${BLUE}Generating pt-BR dictionary to spell check${END_COLOR}"
	/usr/bin/aspell -l pt_BR dump master > pt-br-word-list
	vim -c "mkspell pt pt-br-word-list | q"
	@mv -vf pt.utf-8.spl $(USER_HOME)/.vim/spell/
	@echo -e "${BLUE}Installing plugins using Plug Vim:${END_COLOR}"
	vim +PlugInstall +qall
	@echo -e "$(BROWN)**\n$(END_COLOR)"
