---
layout: page
title: Yaml-mode
permalink: /installation/:basename
nav_order: 2
parent: Installation
---

# Installation for yaml-mode  
This "theme" needs a little work and configuration before you can first use it, but don't worry, we have made it as easy as possible. This "tutorial" shows you, how to set this "theme" up in `yaml`-mode until the first use.  

> **Note:** *these are the installation instructions, if you use `yaml`-mode! We do not recommend `UI`-mode, but if you really need to go with it, than use [these instructions](installation-ui).*  

Let's get started!  

1. <strong>What you should have before you start installing this "theme"</strong>    
   * You should have a HomeAssistant (HA) instance running, preferrably with [HACS](https://hacs.xyz) installed and you should know the basics in using HA, eg. how to change settings in your `lovelace` configuration.  
   * You have access to your `config` folder of HA. Doesn't matter which way this is, but you need to be able to upload and change files in your config. If you're running `HA-OS` or a `supervised install` of HA, we highly recommend the [Samba AddOn](https://www.home-assistant.io/common-tasks/supervised/#installing-and-using-the-samba-add-on) (see the AddOn page for instructions) and for editing the [File editor AddOn](https://github.com/home-assistant/addons/tree/master/configurator) or a good editor like [Notepad++](https://notepad-plus-plus.org/) or [SublimeText](https://www.sublimetext.com/) for your OS.  
1. <strong>Prepare your HomeAssistant installation</strong>  
   To install this "theme" together with other themes in HA, you need to setup your `configuration.yaml` to use a themes folder.  
   1. Create a folder `themes` in your `config` folder  
   1. Add this under the section `frontend` in your `configuration.yaml`:    
      <pre><code class="language-yaml" style="border: 0">frontend:
        themes: !include_dir_merge_named themes
      </code></pre>
   1. Restart Home Assistant  
   1. From now on, you can install new themes, like this one, in your themes folder   
   1. We apply this theme later on so just leave it like that for now.

   > **Note:** *This is the official, recommended way to handle themes. With this structure you can install themes with HACS.*  

1. <strong>Download the files</strong>  
   Go to our repository on Github and download the code by pressing the green "Code" button in the top right corner and choose "Download ZIP". Save the file on your computer and unpack it.  
1. <strong>Upload to your HomeAssistant installation</strong>  
   * In the downloaded and unpacked file you find a folder `config`
   * Move inside this folder and upload the two folders `minimalist-templates` and `themes` directly into your HA `config` folder  
     This should leave you with the following structure
     <pre><code class="language-yaml" style="border: 0">config
         └── other folders from Home Assistant, eg. data
         └── minimalist-templates
            └── button_card_templates.yaml
            └── EN.yaml
         └── themes
            └── minimalist-desktop
               └── minimalist-desktop.yaml
            └── minimalist-mobile
               └── minimalist-mobile.yaml
         └── configuration.yaml (from HA)
         └── other files from Home Assistant, eg. home-assistant.log
     </code></pre>
   * If you want to use a language other than english, [see the paragraph at the end of this page](#installation-of-non-english-languages) for more information about non-english languages.  

1. <strong>Installing the lovelace-custom-cards</strong>  
   Some of our cards need lovelace-custom-cards to work correctly. To install these, we highly recommend to use HACS, as it is the easiest and safest way to install and maintain (update) these cards. Here is a list of the required cards:  

   <table>
   <tr>
   <th>Card</th>
   <th>Required by</th>
   </tr>
   <tr>
   <td><a href="https://github.com/custom-cards/button-card">button-card</a></td>
   <td>all cards</td>
   </tr>
   <tr>
   <td><a href="https://github.com/thomasloven/lovelace-card-mod">lovelace-card-mod</a></td>
   <td>card_light_slider</td>
   </tr>
   <tr>
   <td><a href="https://github.com/kalkih/mini-graph-card">mini-graph-card</a></td>
   <td>card_graph</td>
   </tr>
   <tr>
   <td><a href="https://github.com/kalkih/mini-media-player">mini-media-player</a></td>
   <td>card_media_player</td>
   </tr>
   <tr>
   <td><a href="https://github.com/AnthonMS/my-cards">my-cards (formerly known as ha-slider-card)</a></td>
   <td>card_light_slider</td>
   </tr>
   </table>  

   If you don't want to use HACS to install these cards, please refer to the installation instructions of the specific card!

1. <strong>Setting up a new dashboard and one or more views</strong>  
   We have now installed the "theme", so let's get ready to use it!  

   > **Note:** *If you know how to setup your own views in `yaml_mode` or you have your own system for this, just skip this step and move on to the next step.*  
   
   > **Note:** *What we are doing here, is setting up a new [dashboard](https://www.home-assistant.io/lovelace/dashboards/) with one or more [views](https://www.home-assistant.io/lovelace/views/). If you don't know what this is, please refer to the HomeAssistant documentation to read a little more about it. Basically it is a new entry in your sidebar and one or more tabs under this entry.*  

   * Open your `configuration.yaml` and search for the string "lovelace:".  
     If you find the string "lovelace", compare your entries in `configuration.yaml` under it (all the entries that are indented) with the code underneath.  
     If you can't find it, add the code underneath to your `configuration.yaml` and change it to your needs.
     <pre><code class="language-yaml" style="border: 0">lovelace:
       mode: storage
       # Add yaml dashboards
       dashboards:
         lovelace-minimalist:
           mode: yaml
           title: Minimalist
           icon: mdi:script
           show_in_sidebar: true
           filename: lovelace-minimalist.yaml
     </code></pre>

     <table>
       <tr>
         <td><i>mode</i> (`storage` or `yaml`)</td>
         <td>Set the mode to `storage`, than all your UI-configured dashboards will stay configurable that way, only the dashboards you list underneath will use `YAML mode`.</td>
       </tr>
       <tr>
         <td><i>dashboards</i></td>
         <td>This is the starting point for all your new dashboards, that will be using `YAML mode`.</td>
       </tr>
       <tr>
         <td><i>lovelace-minimalist</i></td>
         <td>This is the name and part of the url (path) for your new dashboard. You can choose any name you want, but it <strong>must</strong> contain a hyphen!</td>
       </tr>
       <tr>
         <td><i>mode</i></td>
         <td>Same as the mode above, but here you <strong>must</strong> use `yaml`.</td>
       </tr>
       <tr>
         <td><i>title</i></td>
         <td>This is the title of your dashboard (the title shown in the sidebar)</td>
       </tr>
       <tr>
         <td><i>icon</i></td>
         <td>Choose an icon for the sidebar</td>
       </tr>
       <tr>
         <td><i>show_in_sidebar</i></td>
         <td>If this dashboard should show up in your sidebar. It will still be available through the path you set above.</td>
       </tr>
       <tr>
         <td><i>filename</i></td>
         <td>This is the filename for your `view`(s). I normally use the same name for the file and the dashboard name.</td>
       </tr>
     </table>
     
   * Now that we have setup our new dashboard, we fill it with views.  
     * Create a file called `lovelace-minimalist.yaml` (or if you have choosen another name under "filename", use that one) in your HA `config` folder, the one that `configuration.yaml`resides in.  
     * Open the file and add the following to it:  

       <pre><code class="language-yaml" style="border: 0">button_card_templates: !include_dir_merge_named minimalist-templates/
       views:
         - title: Minimalist
           cards:
             - type: horizontal-stack
               cards:
                 - type: custom:button-card
                   template: edge
                 - type: custom:button-card
                   template: title
                   name: Welcome to UI-Lovelace-Minimalist
                 - type: custom:button-card
                   template: edge
         - title: Minimalist page 2
           cards:
             - type: horizontal-stack
               cards:
                 - type: custom:button-card
                   template: edge
                 - type: custom:button-card
                   template: title
                   name: UI-Lovelace-Minimalist second page
                 - type: custom:button-card
                   template: edge
       </code></pre>
     * Save the file  
1. <strong>Apply the theme</strong>  
   * Open HA in your browser (just like usual) and go to your user settings (sidebar, last item)  
   * Under "theme" select `minimalist-desktop`   
1. <strong>Take a first look</strong>
   * Go to your HA homepage and click on the three-dot-menu in the upper right corner.
   * Choose "Reload ressources" and afterwards "Refresh" to reload the page. 
   * Look for the entry "Minimalist" in your sidebar and click on it.
   * If everything went fine, you should now see your first page with the "UI-Lovelace-Minimalist" style applied.
1. <strong>Start editing</strong>  
   Now that you have a first look at your new design, you can start using it by adding other buttons.  
   
This tutorial ends here, if you want to see how to *use* this "theme", check out [this page](/usage/first_page). If you want language specific settings see the next paragraph.

## Installation of non-english languages
If you use this "theme" in another language than english, you might want to have your states in your language. Unfortunately it is sometimes not possible to use the already translated strings from Home Assistant, so we found a simple solution for this. We offer language specific strings for the main templates, and for `custom-cards` as well (as long as they are provided by the author).

Use this feature:

* In the repository or your download you can find a folder called `languages`, inside this folder you find files for each supported language.  
* Copy your language file into the folder `minimalist-templates` (that's the folder where `button_card_templates.yaml` lives).  
* Delete all other language files but the one you just copied over!  
* There must be **only ONE** language file present, otherwise your language strings get messed up. 

In the end, it should look like this:

<pre><code class="language-yaml" style="border: 0">  └── minimalist-templates/
     └── button_card_templates.yaml
     └── EN.yaml # or DE.yaml, FR.yaml, IT.yaml
</code></pre>

If you're using `custom-cards`, follow the instructions in the readme file from the `custom-card`.  

In short, you delete **all but one** language file in the folder `custom-cards` > `name_of_custom_card` > `languages`. 