# Editable with SimpleMDE Plugin

The **Editable with SimpleMDE** Plugin is for [Grav CMS](http://github.com/getgrav/grav). It allows users to edit page content in the frontend using the [SimpleMDE](https://simplemde.com/) editor.

> **Important:** The plugin requires Markdown page content that is transfered by Grav straight from a normal Grav page and presents it in a Markdown editor to be saved back to the page when editing is finished.

> **Warning:** Markdown page content that is manipulated by Twig templates, plugins or Javascript code is likely to interfere or even break the working of this plugin. This is why modular pages can not be edited as their content is dynamically created.

## Installation

Typically the plugin should be installed via GPM (Grav Package Manager):

```
$ bin/gpm install editable-simplemde
```

Or, when using the Admin plugin the plugin can be added from the Plugins section. Look for "Editable With SimpleMDE".

Another option is to manualy install the plugin by downloading the plugin as a zip file. Copy the zip file to your /user/plugins directory, unzip it there and rename the folder to editable-simplemde.

## Configuration

Before configuring this plugin, you should copy the `user/plugins/editable-simplemde/editable-simplemde.yaml` to `user/config/plugins/editable-simplemde.yaml`.

Make configuration changes to that copy so your changes will remain when installing a new version of the plugin.

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

A page can be made editable by one or more users or groups. To learn about users, groups and permissions see the documentation on [Groups and Permissions](https://learn.getgrav.org/advanced/groups-and-permissions), the [Login Plugin](https://github.com/getgrav/grav-plugin-login) and [Standard Administration Panel Plugin](https://github.com/getgrav/grav-plugin-admin). 

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

> **Note:** Uploaded images and files that are no longer referenced in the page markdown content are automatically deleted when the page is saved.

## Credits

Thanks go to Team Grav and everyone on the [Grav Forum](https://getgrav.org/forum) for creating and supporting Grav.

## Notes, Issues and To Do's

- Make the editor toolbar sticky so it stays in view when editing longer texts. See this [Proof of Concept](https://codepen.io/bleutzinn/pen/KmNWmp) but help is required to make it work with Grav!
- Navigating away from a page with yet unsaved changes is not handled properly for all browsers.


