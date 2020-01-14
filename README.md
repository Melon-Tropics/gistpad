# GistPad 📘

[![Join space](https://vslscommunitieswebapp.azurewebsites.net/badge/gistpad)](http://vslscommunitieswebapp.azurewebsites.net/join_redirect/gistpad)

GistPad is a Visual Studio Code extension that allows you to manage [GitHub Gists](https://gist.github.com/) entirely within the editor. You can open, create, delete, fork, star and clone gists, and then seamlessly begin editing files as if they were local. It's like your very own developer library for building and referencing code snippets, commonly used config, programming-related notes/documentation, and [interactive/runnable samples](#playgrounds). Additionally, you can collaborate with your friends and colleagues by "following" them, so that you can access/browse/fork and comment on their gists, without ever leaving Visual Studio Code 🚀

<img src="https://user-images.githubusercontent.com/116461/69910156-96274b80-13fe-11ea-9be4-d801f4e9c377.gif" width="750px" />

## Getting Started

1. Install this extension from the marketplace and then reload VS Code

   > **Linux Users**: Ensure you have the `gnome-keyring` and `libsecret` packages installed as well. These will enable GistPad to read/write your GitHub auth token securely.

   > **GitHub Enterprise users**: Set the `gistpad.apiUrl` setting to point at the API URL of your GitHub server instance (e.g. `https://[YOUR_HOST]/api/v3`).

2. Open the `GistPad` tab *(look for the notebook icon in the activity bar)*. From there, you can open a Gist by ID/URL, or sign-in in with a GitHub token, in order to view/edit/create/delete/fork/clone your own gists. To sign-in, you can generate an auth token by visiting [this page](https://github.com/settings/tokens/new), giving the token a name (e.g. `gistpad`), and ensuring to check the `gist` checkbox.

   <img width="300px" src="https://user-images.githubusercontent.com/116461/69827991-d56f5580-11ce-11ea-9081-17f27b470fd1.png" />

   > **Git+HTTPS Users**: If you've already signed-in to `github.com` with the `git` CLI, GistPad will attempt to provide "single-sign on", assuming you're using HTTPS-based auth, and your login session includes the `gist` scope _(SSH-based auth isn't supported)_. 

3. Create new gists from local files or snippets, by right-clicking them in the `Explorer` tree, or right-clicking an editor window/tab, and selecting `Copy File to Gist`, `Add Selection to Gist` or `Paste Gist File Contents` ([details](#contributed-commands-editor))

   <img width="250px" src="https://user-images.githubusercontent.com/116461/69903980-98819b00-1355-11ea-913b-c51981891bcd.png" />

4. View and reply to comments in a Gist by scrolling to the bottom of a Gist file and interacting with the thread (including embedded code snippets!)

   <img width="450px" src="https://user-images.githubusercontent.com/116461/70117955-a9633280-161b-11ea-88a5-ac8a15a3b7a0.png" />

5. Stay up-to-date with your friend's and colleague's Gists by following them via the `GistPad: Follow User` command

   <img width="252" src="https://user-images.githubusercontent.com/116461/69890797-c03e1800-12ef-11ea-85be-7d6fe2c8c7ef.png" />

6. If you're working on a web app, and want to create [runnable code samples](#playgrounds), right-click the `Your Gists` node and select `New Playground` (or `New Secret Playground`. This will provide you with a live dev environment, to experiment with HTML, CSS and JavaScript, that is saved as a shareable gist

## Gist Commenting

Gist comments are exposed within the editor at the bottom of any opened Gist files. If a Gist includes multiple files, then the comment thread will be displayed at the bottom of them all (duplicated and synchronized).

<img src="https://user-images.githubusercontent.com/116461/70118599-42467d80-161d-11ea-85eb-7f4cc6e4006b.gif" width="700px" />

If you're not authenticated, you can view existing comments, but you can't reply to them. If you are authenticated, you can add/reply, as well as edit/delete your own comments. In order to control the behavior of how Gist comment threads are displayed, refer to the `GistPad > Comments: Show Thread` config setting.

## Pasting Images

In order to make it easy to author markdown and HTML/Pug files that include image assets, you can copy images into your clipboard (e.g. taking a screenshot, clicking `Copy Image` in your browser, etc.) and then paste them directly into a gist file by right-clicking the editor and selecting `Paste Image`, or using one of the following keyboard shortcuts: `ctrl + shift + v` _(Windows/Linux)_,`cmd + shift + v` _(macOS)_.

![paste-image](https://user-images.githubusercontent.com/1478800/70382701-9a7ac980-1914-11ea-9fb0-6e55424e2e54.gif)

By default, when you paste an image into a Gist file, it's uploaded as a `.png` to the gist, and the appropriate reference is added to it from the document (e.g. inserting an `<img />`). However, this behavior can be changed by using the `GistPad > Images: Paste Format` and/or `GistPad > Images: Paste Type` settings. Refer to the [config settings](#configuration-settings) section below for more details.

## Following Users

GitHub Gists already allows you to star other user's gists, and when you do that, those will appear in the `Gists` tree, underneath a `Starred Gists` node. However, if you want to follow a GitHub user, and easily browse all of their current and future gists (without having to star each one!), you can run the `GistPad: Follow User` command and specify their GitHub user name. Once you've done that, you'll see a new node in the `Gists` tree which displays all of their public gists, and allows you to open/fork/clone/star them just like any other gist.

<img width="252" src="https://user-images.githubusercontent.com/116461/69890797-c03e1800-12ef-11ea-85be-7d6fe2c8c7ef.png" />

## Interactive Playgrounds

If you're building web applications, and want to create a quick playground environment in order to experiment with HTML, CSS or JavaScript (or [Sass/SCSS, Less, Pug and TypeScript](#additional-language-support)), you can right-click the `Your Gists` node and select `New Web Playground`. This will create a new Gist, seeded with an HTML, CSS and JavaScript file, and then provide you with a live preview Webview, so that you can iterate on the code and visually see how it behaves.

![Playgrounds](https://user-images.githubusercontent.com/116461/71195678-47254700-2243-11ea-9b09-aa28ec526185.gif)

Since the playground is backed by a Gist, your changes are saved and shareable with your friends. Additionally, as you find other playgrounds that you'd like to use, simply fork them and create your own playgrounds. That way, you can use Gists as "templates" for playground environments, and collaborate on them with others just like you would any other gist. When you're done with a playground, simply close the preview window and all other documents will be automatically closed. If you no longer need the playground, then delete it just like any other gist 👍

### Toolbar

When you open a playground, this activates the "playground toolbar", which is a collection of helpful utilities that are displayed in the editor's title bar. The following describes the available actions:

- **Run Playground** - Re-runs the HTML, JavaScript and CSS of your playground. This can be useful when wanting to reset a playground's state and/or if you've disabled the auto-run behavior for playgrounds.
- **Open Console** - Opens the `GistPad Playground` console, which allows you to view the output of any `console.log` calls that your playground makes ([details](#console-output)).
- **Change Layout** - Allows you to change the layout configuration of the playground editors ([details](#layout)).
- **Add Library** - Allows you to add an external library to your playground (e.g. React.js, Font-Awesome) ([details](#external-libraries))
- **Open Playground Developer Tools** - Opens the Chrome Dev Tools for your playground preview, which lets you use the DOM exlporer, evaluate JavaScript expressions in the console, etc.

<img width="464" src="https://user-images.githubusercontent.com/116461/71629353-eafee300-2bb1-11ea-88f0-0996ab6149c4.png" />

### Uploading Images

You can reference HTTP-based images within any of your playground files, and they'll be downloaded/rendered automatically. However, if you need to add local images to your playground, you can upload them in one of two ways:

1. Right-click the gist in the `Gists` view and select `Upload Files(s)`. This supports any file type, and therefore is the most general-purpose solution. Once the image is uploaded, you can then reference it from your playground using only its filename (e.g. `<img src="myImage.png" />`), since the playground preview understands the context of the "surrounding gist".

2. Copy/paste an image into your clipboard, open up an HTML or Pug file, right-click the editor and select `Paste Image`. This will transparently upload the image to the gist, and then insert a reference to it for you (e.g. adding an `<img />` tag). This solution works best when you want to paste a "transient" image into your playground, such as a captured screenshot, or an image that you copied from a webpage.

### Additional Language Support

By default, new playgrounds create an HTML, CSS and JavaScript file. However, if you're more productive using a different markup, stylesheet or scripting language, then simply rename the respective files to use the right extension, and the code will be automatically compiled for you on the fly! Specifically, GistPad supports the following languages:

- **SCSS/Sass** - Rename the `style.css` file to `style.scss` or `style.sass`. \*Note: While VS Code ships with language support for SCSS out-of-the-box, it doesn't ship support for Sass (the "indentended" syntax). So if you plan to author playgrounds with that syntax, it's recommended that you install [this extension](https://marketplace.visualstudio.com/items?itemName=Syler.sass-indented) along with GistPad.
- **Less** - Rename the `style.css` file to `style.less`
- **Pug** - Rename the `index.html` file to `index.pug`
- **TypeScript** - Rename the `script.js` file to `script.ts` (or `script.tsx`, in order to use JSX in your code)
- **JSX** - Rename the `script.js` file to `script.jsx` in order to enable JSX to be written in "vanilla" JavaScript files. Additionally, if you add the [`react` library](#external-libraries) to your gist's `playground.json` file, then `*.js` files can also include JSX.

If you'd like to always use one of these languages, then set one or more of the following settings, and all new playgrounds will include the right files by default: `GistPad > Playgrounds: Markup Language`, `GistPad > Playgrounds: Script Language`, `GistPad > Playgrounds: Stylesheet Language`. View the [settings documentation](#configuration-settings) below for more detials.

### External Libraries

If you need to add any external JavaScript libraries (e.g. `react`) or stylesheets (e.g. `font-awesome`) to your playground, simply click the `Add Playground Library` commmand in the playground "action bar" (or run `GistPad: Add Playground Library` from the command palette). This will allow you to search for a library from CDNJS or paste a custom library URL. When you select a library, it will be automatically added to your playground.

![Add Library](https://user-images.githubusercontent.com/116461/71629251-4ed4dc00-2bb1-11ea-9488-78c3d71dbacd.gif)

Behind the scenes, this command update the playground's manifest file (`playground.json`), which you can also open/edit yourself manually if you'd prefer. Additionally, since Gist files provide an internet-accessible URL, you can use Gists as re-usable snippets for playgrounds, and add references to them by right-clicking a gist file in the `Gists` tree, select `Copy GitHub URL`, and then adding it as a library reference to the appropriate playground.

### Layout

By default, when you create a playground, it will open in a "Split Left" layout, which vertically stacks the code editors on the left, and allows the preview window to occupy the fully IDE height on the right. However, if you want to change the layout, you can run the `GistPad: Change Playout Layout` command and select `Grid`, `Preview`, `Split Right`, or `Split Top`.

![Layout](https://user-images.githubusercontent.com/116461/71560396-5152fc80-2a1e-11ea-9cff-a9590e1ea779.gif)

Additionally, if you create a playground, that looks best in a specific layout, you can set the `layout` property in the playground's `playground.json` file to either: `grid`, `preview`, `splitLeft`, `splitRight`, or `splitTop`. Then, when you or someone else opens this playground, it will be opened with the specified layout, as opposed to the user's configured default layout.

### Console Output

The playground also provides an output window in order to view any logs written via the `console.log` API. You can bring up the output window, as well as run the playground or open the Chrome Developer Tools, by clicking the respective command icon in the editor toolbar. If you'd like to always open the console when creating/opening playgrounds, you can set the `GistPad > Playgrounds: Show Console` setting to `true`.

<img width="503" src="https://user-images.githubusercontent.com/116461/71384593-0a38b780-2597-11ea-8bba-73f784f6ec76.png" />

Additionally, if you create a playground that depends on the console, you can set the `showConsole` property in the playground's `playground.json` file to `true`. Then, when you or someone else opens this playground, the console will be automatically opened, regardless whether the end-user has configured it to show by default.

### CodePen

If you export a pen to a [GitHub Gist](https://blog.codepen.io/documentation/features/exporting-pens/#save-as-github-gist-2), and then refresh the `Gists` tree in VS Code, you'll be able to see the pen and then can open/edit it like any other playground. This allows you to easily fork someone's pen and work on it within VS Code.

![CodePen](https://user-images.githubusercontent.com/116461/71393589-171ed080-25c2-11ea-8138-ba075daf7d37.gif)

Additionally, if you develop a playground locally, and want to export it to CodePen (e.g. in order to share it with the community), you can right-click the gist and select `Export to CodePen`. This allows you to develop within VS Code, and then share it when you're done. When a playground is exported to CodePen, it's tagged with `gistpad` so that the community can [see](https://aka.ms/gistpad-codepen) the pens being created with it.

![Export](https://user-images.githubusercontent.com/116461/71533903-39f60100-28b0-11ea-9e16-891a110c7074.gif)

### Blocks

[Bl.ocks](https://bl.ocks.org) is community for sharing interactive code samples/data visualizations, which are based on GitHub Gists. As a result, you can copy the URL for any Block, use it to open a gist wihtin GistPad, and immediately have an interactive environment for viewing/exploring the Block.

## GistLog

In addition to being able to use Gists to share code snippets/files, you can also use it as a mini-blog, thanks to integration with [GistLog](https://gistlog.co). In order to start blogging, simply run the `GistPad: New GistLog` command, which will create a new Gist that includes two files: `blog.md` and `gistlog.yml`.

![GistLog](https://user-images.githubusercontent.com/116461/70856110-fdc3a900-1e8a-11ea-8e26-2c3917e11db0.gif)

The `blog.md` file will be automatically opened for editing, and as soon as you're ready to publish your post, open `gistlog.yml` and set the `published` property to `true`. Then, right-click your Gist and select the `Open Gist in GistLog` menu. This will open your browser to the URL that you can share with others, in order to read your new post.

In addition to being able to view individual posts on GistLog, you can also open your entire feed by right-clicking the `Your Gists` tree node and selecting the `Open Feed in GistLog` menu item. This will launch your GistLog landing page that displays are published GistLog posts.

## Contributed Commands (File Explorer)

In addition to the `Gists` view, GistPad also contributes an `Copy File to Gist` command to the context menu of the `Explorer` file tree, which allows you to easily add local files to a new or existing Gist.

<img width="260px" src="https://user-images.githubusercontent.com/116461/69831695-58001100-11df-11ea-997e-fc8020556348.png" />

## Contributed Commands (Editor)

In addition to the `Explorer` file tree commands, GistPad also contributes the following commands to the editor's context menu:

- `Add Selection to Gist` - Allows you to add a snippet/selection of code to a Gist, instead of the entire document

- `Paste Gist File` - Allows you to paste the contents of a Gist file into the active document

- `Paste Image` - Allows you to paste an image from your clipboard into a markdown, HTML or Pug file. The command will automatically upload the image and then add a reference to it.

<img width="250px" src="https://user-images.githubusercontent.com/116461/69903980-98819b00-1355-11ea-913b-c51981891bcd.png" />

The `Copy File to Gist` command is also available on the editor tab's context menu.

## Contributed Commands (Editor Title Bar)

In addition to the commands added to the editor context menu, GistPad also contributes the following commands to the editor's title bar menu (click the `...` in the upper right section of an editor window):

- `Rename File` - Allows you to rename the current file.

## Contributed Commands (Command Palette)

In addition to the `Gists` view, this extension also provides the following commands:

- `GistPad: Delete Gist` - Allows you to delete one of your Gists. If you have a Gist workspace open, it will delete that and then close the folde

* `GistPad: Follow User` - Follow another GitHub user, whuich allows you to browser/access/fork their Gists from within the `Gists` view.

- `GistPad: Fork Gist` - Forks the currently opened Gist, and then opens it as a virtual workspace.

* `GistPad: Open Gist` - Displays your list of Gists (if you're signed in), and then opens the files for the selected one. You can also specify a gist by URL, `username/id`, or ID, which doesn't require being signed in.

* `GistPad: Open Gist as Workspace` - Same behavior as the `GistPad: Open Gist` command, but will open the selected Gist as a workspace, istead of "loose files".

* `GistPad: New Gist` - Creates a new [public Gist](https://help.github.com/en/enterprise/2.13/user/articles/about-gists#public-gists), and then opens its associated files. If you'd like to seed the gist with multiple files, you can specify a comma-seperated list of names (e.g. `foo.txt,bar.js`).

* `GistPad: New Secret Gist` - Same behavior as the `GistPad: New Gist (Public)` command, except that it creates a [secret Gist](https://help.github.com/en/enterprise/2.13/user/articles/about-gists#secret-gists).

* `GistPad: New Web Playground` - Creates a new [playground](#playgrounds).

* `GistPad: New GistLog` - Creates a [GistLog](#gistlog).

* `GistPad: Refresh Gists` - Refreshes the gist data and reloads the `Gists` tree.
*
* `GistPad: Sign In` - Sign-in with a GitHub token, in order to view/edit/delete your Gists.

* `GistPad: Sign Out` - Sign out of the currently authenticated GitHub session.

- `GistPad: Starred Gists` - Lists your starred Gists, and then opens the files for the selected one.

## Configuration Settings

- `Gistpad: Api Url` - Specifies the GitHub API server to use. By default, this points at GitHub.com (`https://api.github.com`), but if you're using GitHub Enterprise, then you need to set this to the v3 API URL of your GitHub server. This should be something like `https://[YOUR_HOST]/api/v3`.

- `Gistpad: Git SSO` - Specifies whether to enable single sign-in (SSO) with the `git` CLI, when you've already authenticated with github.com. Defaults to `true`.

* `GistPad > Comments: Show Thread` - Specifies when to show the comment thread UI whenever you open a Gist file. Can be set to one of the following values:

  - `always`: Always display the comment thread whenever you open a Gist file. You can manually collapse it as needed.
  - `never`: Never automatically open the comment thread when you open a Gist file. You can manually expand it as needed.
  - `whenNotEmpty` _(default)_: Automatically display the comment thread whenever there are actually comments in a Gist file. Otherwise, leave it collapsed.
  -

- `Gistpad > Images: Paste Format`: Specifies the markup format to use when pasting an image into a gist file. Can be set to one of the following values:

  - `markdown` _(default)_: Pastes the image reference using `Markdown` format (e.g. `![image](link)`).
  - `html`: Pastes the image reference using `HTML` format (e.g. `<img src="link" />`). Note, when you paste an image into an HTML file, it will always use this format type, regardless what the setting is.

- `Gistpad > Images: Paste Type`: Specifies the method to use when pasting an image into a gist file. Can be set to one of the following values:

  - `file` _(default)_: The pasted image is uploaded as a `.png` to the gist, and a reference is added to file it's pasted into.
  - `base64`: The pasted image is base64-encoded and then embedded into the gist file.

* `GistPad > Playgrounds: Auto Run` - Specifies when to automatically run the code for a playground. Can be set to one of the following values:

  - `onEdit` _(default)_: Will re-run the playground automatically as you type.
  - `onSave`: Will re-run the playground when you save a file.
  - `never`: Don't automatically re-run the playground, and instead, only run it when the `GistPad: Run Playground` command is executed.

* `GistPad > Playgrounds: Auto Save` - Specifies whether to automatically save your playground files (every 30s). If you've already set the `Files: Auto Save` setting to `afterDelay`, then that setting will be respected. Defaults to `true`.

* `GistPad > Playgrounds: Include Markup` - Specifies whether to include a markup file (`index.html`) when creating new web playgrounds. Defaults to `true`.

* `GistPad > Playgrounds: Include Script` - Specifies whether to include a script file (`script.js`) when creating new web playgrounds. Defaults to `true`.
* 
* `GistPad > Playgrounds: Include Stylesheet` - Specifies whether to include a stylesheet file (`style.css`) when creating new web playgrounds. Defaults to `true`.

* `GistPad > Playgrounds: Layout` - Specifies how to layout the editor windows when opening a playground. Can be set to one of the following values:

  - `grid`: Opens a 2x2 grid of editors, with the editors and preview window occupying an equal amount of space.
  - `preview`: Simply opens the full-screen preview window. This is useful for interacting with complex playgrounds or viewing other's playgrouds.
  - `splitLeft` _(default)_: Opens a split-level layout, with the editors vertically stacked on the left, and the preview occupying the full IDE height on the right.
  - `splitRight`: Opens a split-level layout, with the editors vertically stacked on the right, and the preview occupying the full IDE height on the left.
  - `splitTop` _(default)_: Opens a split-level layout, with the editors horizontally stacked on the top, and the preview occupying the full IDE width on the bottom.

* `GistPad > Playgrounds: Markup Language` - Specifies the default markup language to use when creating new web playgrounds. Can be set to one of the following values:

  - `html` _(default)_: Will result in an `index.html` file being created whenever you create a new web playground.
  - `pug`: Will result in an `index.pug` file being created whenever you create a new web playground.

* `GistPad > Playgrounds: Script Language` - Specifies the default scripting language to use when creating new web playgrounds. Can be set to one of the following values:

  - `javascript` _(default)_: Will result in an `script.js` file being created whenever you create a new web playground.
  - `javascriptreact`: Will result in an `script.jsx` file being created whenever you create a new web playground.
  - `typescript`: Will result in an `script.ts` file being created whenever you create a new web playground.
  - `typescriptreact`: Will result in an `script.tsx` file being created whenever you create a new web playground.

* `GistPad > Playgrounds: Stylesheet Language` - Specifies the default stylesheet language to use when creating new web playgrounds. Can be set to one of the following values:

  - `css` _(default)_: Will result in an `style.css` file being created whenever you create a new web playground.
  - `less`: Will result in an `style.less` file being created whenever you create a new web playground.
  - `sass`: Will result in an `style.sass` file being created whenever you create a new web playground.
  - `scss`: Will result in an `style.scss` file being created whenever you create a new web playground.

* `GistPad > Playgrounds: Show Console` - Specifies whether to always show the console when opening a playground. Defaults to `false`.

## Keyboard Shortcuts

- **New Public Gist**: `ctrl+shift+n` _(Windows/Linux)_, `cmd+shift+n` _(macOS)_
- **New Web Playground**: `ctrl+shift+p` _(Windows/Linux)_, `cmd+shift+p` _(macOS)_
- **Open Gist**: `ctrl+shift+o` _(Windows/Linux)_, `cmd+shift+v` _(macOS)_
- **Paste Image**: `ctrl+shift+i` _(Windows/Linux)_, `cmd+shift+i` _(macOS)_

## Supported Filesystem Operations

Once you've opened a Gist, you can perform the following filesystem operations:

- Editing existing files
- Adding new files
- Renaming files
- Deleting files
- Copying/pasting files

> GitHub Gist doesn't support directories, and therefore, this extension doesn't allow you to create them.

## Recommended Extensions

In order to improve the productivity of editing Gists, and make VS Code behave similarly to the GitHub.com experience, the following extensions are recommended, depending on how you expect to use Gists (e.g. markdown files, code snippets):

| Extension           | Stats                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Markdown All-in-One | [![Latest Release](https://vsmarketplacebadge.apphb.com/version-short/yzhang.markdown-all-in-one.svg)](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) [![Installs](https://vsmarketplacebadge.apphb.com/installs/yzhang.markdown-all-in-one.svg)](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) [![Rating](https://vsmarketplacebadge.apphb.com/rating-short/yzhang.markdown-all-in-one.svg)](https://marketplace.visualstudio.com/items?itemName=yzhang.markdown-all-in-one) |
| Markdown Checkbox   | [![Latest Release](https://vsmarketplacebadge.apphb.com/version-short/bierner.markdown-checkbox.svg)](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-checkbox) [![Installs](https://vsmarketplacebadge.apphb.com/installs/bierner.markdown-checkbox.svg)](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-checkbox) [![Rating](https://vsmarketplacebadge.apphb.com/rating-short/bierner.markdown-checkbox.svg)](https://marketplace.visualstudio.com/items?itemName=bierner.markdown-checkbox)       |
| SVG Viewer          | [![Latest Release](https://vsmarketplacebadge.apphb.com/version-short/cssho.vscode-svgviewer.svg)](https://marketplace.visualstudio.com/items?itemName=cssho.vscode-svgviewer) [![Installs](https://vsmarketplacebadge.apphb.com/installs/cssho.vscode-svgviewer.svg)](https://marketplace.visualstudio.com/items?itemName=cssho.vscode-svgviewer) [![Rating](https://vsmarketplacebadge.apphb.com/rating-short/cssho.vscode-svgviewer.svg)](https://marketplace.visualstudio.com/items?itemName=cssho.vscode-svgviewer)                         |
