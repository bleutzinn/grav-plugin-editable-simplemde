# Editable with SimpleMDE Plugin

The **Editable with SimpleMDE** Plugin is for [Grav CMS](http://github.com/getgrav/grav). It allows frontend users to edit page content using the [SimpleMDE editor](https://simplemde.com/).

Markdown content in normal Grav pages can be made editable. However, modular pages can not be edited as their content is dynamically created.

## Installation

Installing the plugin can be done in one of two ways. The GPM (Grav Package Manager) installation method enables you to quickly and easily install the plugin with a simple terminal command, while the manual method enables you to do so via a zip file.

> NOTE: This plugin is a modular component for Grav which requires [Grav](http://github.com/getgrav/grav) and the [Error](https://github.com/getgrav/grav-plugin-error) and [Problems](https://github.com/getgrav/grav-plugin-problems) to operate.

### GPM Installation (Preferred)

The simplest way to install this plugin is via the [Grav Package Manager (GPM)](http://learn.getgrav.org/advanced/grav-gpm) through your system's terminal (also called the command line).  From the root of your Grav install type:

    bin/gpm install editable-simplemde

This will install the plugin into your `/user/plugins` directory within Grav. It's files can be found under `/your/site/grav/user/plugins/editable-simplemde`.

### Manual Installation

To install this plugin, just download the zip version of this repository and unzip it under `/your/site/grav/user/plugins`. Then, rename the folder to `editable-simplemde`.

You should now have all the plugin files under

    /your/site/grav/user/plugins/editable-simplemde

## Configuration

Before configuring this plugin, you should copy the `user/plugins/editable-simplemde/editable-simplemde.yaml` to `user/config/plugins/editable-simplemde.yaml` and only edit that copy.

Here is the default configuration and an explanation of available options:

```yaml
enabled: true
```

Setting `enabled` tot `true` enables or activates the plugin.

## Usage

### User Permissions

#### Frontend Users

To enable users to edit content in the frontend they must be able to login. 

Access to the frontend requires a seperate login as documented in the [Grav Login plugin](https://github.com/getgrav/grav-plugin-login) or the [Private Grav Plugin](https://github.com/Diyzzuf/grav-plugin-private).

To edit a page a frontend user must have the permission `site.editable`. Add the required authorization to each user in the user's account file:

```
access:
  site:
    login: 'true'
    editable: 'true'
```

#### Backend Users

By default Grav separates backend (Admin) and frontend users into separate sessions.   
Allowing backend users to edit pages in the frontend requires the Grav option `session.split` to be set to `false` (in `system.yaml` or in the Admin panel).

A backend or Admin user must have the permission `admin.super` or `admin.pages` to be allowed to edit a page.


### Enabling page editing

#### Per page

To make a single page editable add these lines to the page header or frontmatter:

```
editable-simplemde:
    self: true
```

#### Site wide

In case all pages need to be made editable make the setting site wide by adding `self: true` to the plugin configuration file `editable-simplemde.yaml`:

```
enabled: true
self: true
```

When using the site wide option then to exclude a page from being editable set `self` to `false` in that page's frontmatter:

```
editable-simplemde:
    self: false
```

#### Per User

A page can be made editable by one or more users or groups.

Given this page's frontmatter:

```
editable-simplemde:
    self: true
    editable_by:
        - brigitte
        - tom
        -
            users:
                - frank
                - jane
        -
            groups:
                - editors
        - trinity
```

and assuming user permissions are set right, only the named users plus the users belonging to the group "editors" are allowed to edit that page.

### Page Media

Images and files that are uploaded are saved in the same folder as the corresponding page.

>**Note:** Uploaded images and files that are no longer referenced in the page markdown content are automatically deleted when the page is saved.

## Credits

Thanks go to Team Grav and everyone on the [Grav Forum](https://getgrav.org/forum) for creating and supporting Grav.

## To Do

- [ ] Make the editor toolbar sticky so it stays in view when editing longer texts. See this [Proof of Concept](https://codepen.io/bleutzinn/pen/KmNWmp) but help is required to make it work with Grav!

