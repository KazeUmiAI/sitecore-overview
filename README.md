# Sitecore Overview

Sitecore is a Web Content Management (WCM) solution on steroids.[^1] Sitecore helps you manage the content data in database and provide content to website (by API).

5 layer when work with Sitecore:

- Chanels: Web, email, mobile, social, apps, print, commerce, federated.
- Management: Content, production information, digital assets.
- Sitecore AIDA: Analics, Insights, Decisions, Automation.
- Database: Customer data, universal customer connector
- Integration: Commerce, Server, Microsoft Dynamics,  CRM, ERP, Other systems
  
**Table of contents**
- [Sitecore Overview](#sitecore-overview)
  - [**Sitecore structure**](#sitecore-structure)
    - [1. **Master,Web and Core Database**](#1-masterweb-and-core-database)
    - [2. **Content Editor and Experience Editor**](#2-content-editor-and-experience-editor)
    - [3. **Configs, patches, load order**](#3-configs-patches-load-order)
    - [4. **Templates**](#4-templates)
    - [5. **Component**](#5-component)
    - [6. **Placeholder**](#6-placeholder)
    - [7. **Layout**](#7-layout)
  
## **Sitecore structure**

### 1. **Master,Web and Core Database** 
   
Master database contains all published and unpublished content for all publishing targets. It is used when we need administer content or settings.
- Master Database is used for Content Authoring.
- Master Database maintains the versioning of the contents.
  
Web database contains the published version of the content for a given publishing target. It is used for review the latest result that would delivery to customer. It also support live web.
- Web database stored only lastest that published in here.
- Web database does not handle personal data.
- Web database is optimized for speed, size, and performance
  
Core database stores infrastructure data needed to run Sitecore itself. In other mean, It's sitecore settings and configs.
- The changes in core will affact all instances of Sitecore.

### 2. **Content Editor and Experience Editor**
   
**[Content Editor](https://doc.sitecore.com/xp/en/users/102/sitecore-experience-platform/the-content-editor.html)** is an editing tool that you can use to manage and edit all the content on your website. It is designed for more experienced content authors.

- Appearance and functionality vary depending on the user’s roles, the local security settings, and other customizations.
- User interface consists of three main areas that you can customize to fit your individual needs when you work in the Content Editor. The three areas are:
    - [The ribbon](https://doc.sitecore.com/xp/en/users/102/sitecore-experience-platform/the-content-editor.html#the-ribbon) – the area where all the functionality is available.
    - [The content](https://doc.sitecore.com/xp/en/users/102/sitecore-experience-platform/the-content-editor.html#the-content-tree) tree – the area where all the items are organized.
    - [The content area](https://doc.sitecore.com/xp/en/users/102/sitecore-experience-platform/the-content-editor.html#the-content-area) – the area where you can edit your items.
**[Experience Editor](https://doc.sitecore.com/xp/en/users/102/sitecore-experience-platform/the-experience-editor.html)** is a WYSIWYG (What You See Is What You Get) editor that allows you to easily make changes to items directly on the page. You can edit all the items that are visible on the page — text, graphics, logos, links, and so on.

### 3. **Configs, patches, load order**
   
**Sitecore Configuration** is a set of files that control the behavior of Sitecore. These files are stored in the **Web.config** file and in the **App_config** folder. For exp, you can see [pratice of
custome field][add pratice link here].

**Sitecore patches** is a file that used to add or change configuration settings in Sitecore without having to edit the files directly. Almost patch files are placed in **App_Config/Include**. You can see in [pratice of
custome field][add pratice link here] was added config to include new controller rendering dll to sitecore.

**Sitecore load order** divides into layers (folder in App_Config). By default, Sitecore loads its configuration files in order: Basic system files (layers.config, ConnectionStrings.config, Web.config) => Sitecore layer => Modules layer => Custom layer => Enviroment layer, location of each layer is configured in **layer.config**. Each layer, by default, Sitecore goes through all the subfolders in the layer recursively and loads the files in each subfolder in alphabetical order. Files in the root of a folder are merged before files in subfolders within the folder. [Add reference here](https://doc.sitecore.com/xp/en/developers/102/platform-administration-and-architecture/configuration-layers.html)


### 4. **Templates**
   
Templates is object that have mission to define structure (atribute, behivior) of some type of object. In other way, templates are like class definitions. Content is just an instance of that class. (book 8 - 21)

- **Data template** are the foundation of your Sitecore deployment. They specify the data fields and many other settings that can be applied to content upon creation.
- **Standard value** extend the data template by introducting how to set default setting and values when items are created.[book 8 page 77]
- **Token** is a value delegate for value of instant. In other way, a token in Sitecore is a replaceable parameter that can be used in templates, layouts, and other content items. Such as replacing "$name" with the name of the item when it is created.
- **Shared property** is field in template control the scope of field's effect to all inherit. In other explain, A field that is shared shares its value to all its instant (languares and version). See practice [add link pratice here]. 
- **Unversioned property** is field in template control the scope of that field's effect in languares. A field that is unversioned shares its value with all versions in the language scope. See pratice [add link pratice here].

### 5. **Component**
   
Components is concept to point the thing you can see and have action in web. For better, components tell Sitecore how the content should be rendered [book 8 page 24].A component has a controller that renders the component on the page.

- **View rendering** and **controller renderings** are both ASP.NET MVC concepts. Both have a .cshtml file that contains the markup inside the project and deployed to the site.
- **View Rendering** is component that is referenced to "View" in .Net. It content will base on itself or parent component.
- **Controller rendering** is component that is referenced to "Action" in "Controller". Because it base on action and controller, It's data and It's view can be modify dynamic.
- **Inheritance template** mean template can be inherit from other template. However you shouldn't make it deep or become circle. For exp: Template B inherit from A, C inherit B but A inherit C. So datasource template and page types templates should inherit from interface templates.
- **Datasource location** specify where the user is allowed to look for the data source.[Add reference here](https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/data-sources.html) 
- **Datasource Template** specify the types of data sources users can create.[Add reference here](https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/data-sources.html)

### 6. **Placeholder**
   
Placeholders is which marketers can add or remove components. It can be configured to allow certain components to help enforce a standard information architecture.[book 8 page24]

- **Static placeholder** is placeholder that is defined, sticked, or referenced to a layout. It cannot be moved or changed in position, but it can be configured.
- **Dynamic placeholder** is placeholder that is not sticked or  the layout that it is working on.

### 7. **Layout**
   
Layout tell Sitecore where to render the component. It contains one or more content placeholders

[^1]: Book 8 page 2
[^2]: Book 8 page 21