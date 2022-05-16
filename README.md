# GitHub Pages using Hugo 

## Install Git and Hugo
1. On Arch Linux
`sudo pacman -S git hugo`

## Hugo new site quickstart and test
1. Create a new site in the specified directory
```
hugo new site <dir>
cd <dir>
```

2. Create Git repository
`git init`

3. Add a theme ([Hugo Themes](https://themes.gohugo.io/))
- Find the theme's repository using the Download link on the theme's page
```
git submodule add <theme repository> themes/<theme>
echo "theme = '<theme>'" >> config.toml
```

5. Create some content
`hugo new posts/<post-name>.md`

6. Replace ***draft: true*** with ***draft: false*** in **config.toml** so that the post shows up

7. Test it out
`hugo server -D`

8. Open in browser
`http://localhost:1313`

## Configuration for GitHub
**Replace instances of `<user>` with GitHub user name**
1.  Edit **config.toml**
 - Change ***baseURL*** value from ***'http://example.org/'*** to ***'https://\<user\>.github.io/'***
 - Add ***publishDir = 'docs'***
2. Tell GitHub to bypass Jekyll processing
`touch docs/.nojekyll`
3. Update
`hugo -D`

## Setup GitHub and repository
### Create GitHub account
[GitHub Signup](https://github.com/signup)

### CLI Setup
```
ssh-keygen -t ed25519
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

#### Install GitHub CLI (Optional)
`pacman -S github-cli`

##### Login
`gh auth login`

You will be prompted for the SSH public key you generated earlier if you select SSH as the preferred protocol.

##### Or, if github-cli is already installed and logged in

`gh ssh-key add ~/.ssh/id_ed25519.pub`


#### Alternatively, setup without Github CLI

`xclip -sel c ~/.ssh/id_ed25519.pub`

Paste and save at *https://github.com/settings/keys -> New SSH key*

### Create new repository on GitHub (Using GitHub CLI)
```
cd <dir>
gh repo create <user>.github.io --public --source=. --remote=upstream
```

### Commit and push to GitHub
```
git add .
git commit -m "first commit"
git remote add origin git@github.com:<user>/<user>.github.io
git push origin master
```


## Assuming your repository is on GitHub and is named \<user\>.github.io
Go to the repository on GitHub.com

1. In *Settings -> Code and automation: Pages*

Change ***Source*** from **'/ (root)'** to ***'/docs'*** and save


2. Try browsing [https://\<user\>.github.io/](https://\<user\>.github.io/)
