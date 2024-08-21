# Grav Editable with SimpleMDE Plugin

***Abandonment Notice:** Creating and improving my plugins for Grav was fun to do, however times are changing and so am I. My interests have shifted away from coding and so I am abandoning my plugins. If you are interested in taking over please follow the ["Abandoned Resource Protocol"](https://learn.getgrav.org/advanced/grav-development#abandoned-resource-protocol). Simply skip the first two steps and refer to this statement in step 3.*


The **Editable with SimpleMDE** Plugin is for [Grav CMS](http://github.com/getgrav/grav). It allows users to edit page content in the frontend using the [SimpleMDE](https://simplemde.com/) editor.

> Version 1.4.0 has successfully been tested with Grav 1.7.0-rc.20

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
self: false
```

- enabled: Setting `enabled` to `true` enables or activates the plugin.
- self: When set to `true` all pages are editable, site wide.

## Usage

### Frontend login permission 

To enable users to edit content in the frontend they must be able to login. 

Access to the frontend requires a seperate login as documented in the [Grav Login plugin](https://github.com/getgrav/grav-plugin-login) or the [Private Grav Plugin](https://github.com/Diyzzuf/grav-plugin-private).

To login to the frontend a user must have the permission `site.login`. Add the required authorization to each user in the user's account file:

```yaml
access:
  site:
    login: 'true'
```


### Editable permission

To edit a frontend page a frontend user must have the permission `site.editable`. Add this authorization to each user in the user's account file as well:

```yaml
access:
  site:
    login: 'true'
    editable: 'true'
```

### Enabling page editing

#### Making all pages editable (site wide)

In case all pages need to be made editable make the setting site wide by adding `self: true` to the plugin configuration file `editable-simplemde.yaml`:

```yaml
enabled: true
  self: true
```


#### Making a single page editable (or not)

When not using the site wide option, to make a single page editable add these lines to a page frontmatter:

```yaml
editable-simplemde:
    self: true
```

To exclude a page from being editable set `self` to `false` in that page's frontmatter:

```yaml
editable-simplemde:
    self: false
```

#### Making a page editable by users or groups

A page can be made editable by one or more users or groups.

To learn about users, groups and permissions see the documentation on [Groups and Permissions](https://learn.getgrav.org/advanced/groups-and-permissions), the [Login Plugin](https://github.com/getgrav/grav-plugin-login) and [Standard Administration Panel Plugin](https://github.com/getgrav/grav-plugin-admin). 

Some examples:

Using this frontmatter the page "Headlines" may be edited by the user with username "tom":

```yaml
title: Headlines
editable-simplemde:
    editable_by:
        tom
```

Using this frontmatter the page "Headlines" may be edited by the users (usernames) "tom" and "jerry":

```yaml
title: Headlines
editable-simplemde:
    editable_by:
        - tom
        - jerry
```

Another notation is:

```yaml
title: Headlines
editable-simplemde:
    editable_by:
        users:
            - tom
            - jerry
```

Using groups is similar. Here the page "Headlines" may be edited by all users belonging to the group "news-editors":

```yaml
title: Headlines
editable-simplemde:
    editable_by:
        groups: news-editors
```

As documented in the [Login Plugin](https://github.com/getgrav/grav-plugin-login) adding a user to the group "news-editors" is done by adding these lines to a user's account file:

```yaml
groups:
  - news-editors
```

By using a more complex configuration in the frontmatter it is possible to mix users and groups:

```yaml
title: Headlines
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
                - news-editors
```

### Example group

A typical basic group configuration (in `user/config/groups.yaml') to accompany the examples then would be:

```yaml
news-editors:
  groupname: news-editors
  description: 'All News Editors'
  access:
    site:
      login: 'true'
      editable: 'true'
```

### Allowing backend Users to edit pages in the frontend

Backend users typically work in the Admin panel interface provided by the Admin Plugin interface.

Backend users who have the permission `admin.super` or `admin.pages` are allowed to edit frontend pages.   

These permission take precedence over the `site.editable` permission so backend users need not have the `site.editable` permission in their account file.


### Page Media

Images and files that are uploaded are saved in the same folder as the corresponding page.

> **Note:** Uploaded images and files that are no longer referenced in the page markdown content are automatically deleted when the page is saved!

## Credits

Thanks go to Team Grav and everyone on the [Grav Forum](https://getgrav.org/forum) for creating and supporting Grav.

## Notes, Issues and To Do's

- Make the editor toolbar sticky so it stays in view when editing longer texts. See this [Proof of Concept](https://codepen.io/bleutzinn/pen/KmNWmp). Actually this is very theme specific and so unfortunately there is no generic solution.
- Navigating away from a page with yet unsaved changes is not handled properly in all browsers.
