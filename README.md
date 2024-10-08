# Pushing changes to the repository
```
cd $HOME
dotfiles add .tmux.conf
dotfiles commit -m "Add .tmux.conf"
dotfiles push
```

# Setting Up a New Machine

To set up a new machine to use your version controlled config files, all you need to do is to clone the repository on your new machine telling git that it is a bare repository:

`git clone --separate-git-dir=$HOME/.dotfiles https://github.com/Deetss/.dotfiles.git ~`

However, some programs create default config files, so this might fail if git finds an existing config file in your $HOME. In that case, a simple solution is to clone to a temporary directory, and then delete it once you are done:
```
git clone --separate-git-dir=$HOME/.dotfiles https://github.com/Deetss/.dotfiles.git tmpdotfiles
rsync --recursive --verbose --exclude '.git' tmpdotfiles/ $HOME/
fc-cache -fv
rm -r tmpdotfiles
```
There you go. No symlink mess.
