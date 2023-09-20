# Sitecore Overview

Sitecore is a Web Content Management (WCM) solution on steroids (p8).[^1] Sitecore helps you manage the content data in database and provide content to website (by API).

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
    - [8. **Tanent in SXA** ^4](#8-tanent-in-sxa-4)
    - [9. **Site in SXA** ^5](#9-site-in-sxa-5)
  - [**Site core pratice**](#site-core-pratice)
    - [I. **Create tanent and site**](#i-create-tanent-and-site)
      - [1. **Create Modules**](#1-create-modules)
    - [II. **Create template**](#ii-create-template)
      - [1. **Interface template**](#1-interface-template)
      - [2. **section and Attribute in Template**](#2-section-and-attribute-in-template)
      - [3. **Standard Value**](#3-standard-value)
      - [4. **Insert Options**](#4-insert-options)
    - [III. **Create Layout**](#iii-create-layout)
    - [IV. **Create component: View rendering, Controller rendering and how to use layout**](#iv-create-component-view-rendering-controller-rendering-and-how-to-use-layout)
      - [1. **View rendering**](#1-view-rendering)
      - [2. **Controller rendering**](#2-controller-rendering)
    - [V. **Setup BlogPage**](#v-setup-blogpage)
      - [1. **Presentation Layer**](#1-presentation-layer)
      - [2. **Create Blog Page Template**](#2-create-blog-page-template)
      - [3. **Create custom renderings variant**](#3-create-custom-renderings-variant)
      - [4. **Edit your Home page**](#4-edit-your-home-page)
        - [**Add your custom slider**](#add-your-custom-slider)
        - [**Add Most Popular**](#add-most-popular)
        - [**Add Search Content**](#add-search-content)
          - [**Configure Facets and Scope**](#configure-facets-and-scope)
    - [VI. **Create theme**](#vi-create-theme)
  
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
customfield][add pratice link here].

**Sitecore patches** is a file that used to add or change configuration settings in Sitecore without having to edit the files directly. Almost patch files are placed in **App_Config/Include**. You can see in [pratice of
custom field][add pratice link here] was added config to include new controller rendering dll to sitecore.

**Sitecore load order** divides into layers (folder in App_Config). By default, Sitecore loads its configuration files in order: Basic system files (layers.config, ConnectionStrings.config, Web.config) => Sitecore layer => Modules layer => Custom layer => Enviroment layer, location of each layer is configured in **layer.config**. Each layer, by default, Sitecore goes through all the subfolders in the layer recursively and loads the files in each subfolder in alphabetical order. Files in the root of a folder are merged before files in subfolders within the folder. [^6]


### 4. **Templates**
   
Templates is object that have mission to define structure (atribute, behivior) of some type of object. In other way, templates are like class definitions. Content is just an instance of that class (p21).[^1]

- **Data template** are the foundation of your Sitecore deployment. They specify the data fields and many other settings that can be applied to content upon creation.
- **Standard value** extend the data template by introducting how to set default setting and values when items are created (p77).[^1]
- **Token** is a value delegate for value of instant. In other way, a token in Sitecore is a replaceable parameter that can be used in templates, layouts, and other content items. Such as replacing "$name" with the name of the item when it is created. [Expand standard value token](https://doc.sitecore.com/xp/en/developers/102/sitecore-experience-manager/standard-values.html#the-name-token)
- **Shared property** is field in template control the scope of field's effect to all inherit. In other explain, A field that is shared shares its value to all its instant (languares and version). See practice [add link pratice here]. 
- **Unversioned property** is field in template control the scope of that field's effect in languares. A field that is unversioned shares its value with all versions in the language scope. See pratice [add link pratice here].

### 5. **Component**
   
Components is concept to point the thing you can see and have action in web. For better, components tell Sitecore how the content should be rendered.[^1] A component has a controller that renders the component on the page.

- **View rendering** and **controller renderings** are both ASP.NET MVC concepts. Both have a .cshtml file that contains the markup inside the project and deployed to the site.
- **View Rendering** is component that is referenced to "View" in .Net. It content will base on itself or parent component.
- **Controller rendering** is component that is referenced to "Action" in "Controller". Because it base on action and controller, It's data and It's view can be modify dynamic.
- **Inheritance template** mean template can be inherit from other template. However you shouldn't make it deep or become circle. For exp: Template B inherit from A, C inherit B but A inherit C. So datasource template and page types templates should inherit from interface templates.
- **Datasource location** specify where the user is allowed to look for the data source.[^2] 
- **Datasource Template** specify the types of data sources users can create.[^3]

### 6. **Placeholder**
   
Placeholders is which marketers can add or remove components. It can be configured to allow certain components to help enforce a standard information architecture (p24).[^1]

- **Static placeholder** is placeholder that is defined, sticked, or referenced to a layout. It cannot be moved or changed in position, but it can be configured.
- **Dynamic placeholder** is placeholder that is not sticked or  the layout that it is working on.

### 7. **Layout**
   
Layout tell Sitecore where to render the component. It contains one or more content placeholders

### 8. **Tanent in SXA** [^4]
    
   In the context of Sitecore Experience Accelerator (SXA), atenant is a top-level container for the sites underneath. SXA supports multitenancy, which means that you can run multiple sites on a single instance of Sitecore. 
   
   Each tenant can include multiple related sites, for example, to support multiple brands for a single company or multiple languages or locations for a single brand.
   
   When you use the Tenant creation wizard to quickly set up your tenant and site, by default SXA creates templates, themes, and media content, with the paths stored on the tenant item you just created. 

### 9. **Site in SXA** [^5]
    
    Sites are the items that represent the website and consist of pages, data, designs, and partial layouts.

    Sites in the same tenant are related, for example, because they share the same set of templates or part of the media library.

    SXA site names cannot contain blank spaces.


## **Site core pratice**

**System info**: Sitecore 10.2 with SXA installed\
**Visual Studio**: Visual Studio 2022\
**Project to practice**:\
- Open visual studio and create new project 
- Seach and chose *ASP.NET Web Application*
- Name it is CompanyDemo and chose .Net framework 4.8 and click Next .
- Chose MVC that have MVC have been chosen in right and create.
- Copy **Web.Config** and **Views/Web.Config** from Sitecore web host to overwrite Web.config and Views/Web.config in your project.
- Into VS, right click in *Web.config* and *Views/Web.config* to open properties.
- Change *Build action* is *None*.
- Create new *lib* folder in your solution folder.
- Copy all dll from bin of sitecore web to here.
- Back to VS, right click and chose *add refference* at reference of your project.
- Remove `System.Web.MVC` and Browse `Sitecore.Kernel/MVC.dll;System.Web.MVC.dll` in *lib* folder to project.
- Chose all reference in project and right click to chose *Properties*.
- Set copy local to false
- In App_Start/RouterConfig.cs remove default route. Code will look like this:
  ```C#
  public class RouteConfig
   {
      public static void RegisterRoutes(RouteCollection routes)
      {
         routes.IgnoreRoute("{resource}.axd/{*pathInfo}");
      }
   }
  ```
- Finaly, in Global.asax.cs, change code to below:
  ```C#
  public class MvcApplication : Sitecore.Web.Application
   {
      protected void Application_Start()
      {
         AreaRegistration.RegisterAllAreas();
         RouteConfig.RegisterRoutes(RouteTable.Routes);
      }
   }
  ```
  - Right click to project -> publish -> Add publish profile -> chose Folder -> browse it to sitecore website host -> create

<img src="image\prepare_practice\step01.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step02.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step03.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step04.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step05.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step06.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step07.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step08.1.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step08.2.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step09.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step10.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step11.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step12.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step13.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step14.png" width="300" style="vertical-align:top">

### I. **Create tanent and site** 
   
   Follow this [tutorial](https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/create-a-tenant-and-a-site.html)

   By default, the structure of tanent and site will like below. We can check [web](https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/the-sxa-items-in-the-content-editor.html) for details.

   <img src="image/Tenant Config.webp" width="300" style="vertical-align:top">
   <img src="image/Site structure.webp" width="300" style="vertical-align:top">

#### 1. **Create Modules**

   Step 1: Move on *System/Settings/Feature*. Unless you have folder with name like your tenant yet, let create one and make its name is *SitecoreDemo*. Right click in Feature -> Insert -> Folder -> Fill its name is `SitecoreDemo`

   <img src="image\create_module\step01.png" width="300" style="vertical-align:top">
   <img src="image\create_module\step01.1.png" width="300" style="vertical-align:top">

   Step 2: right click in Feature again -> Insert -> Module -> *Create new module* dialog, Change module name is `Customs` -> Choose location is *SitecoreDemo* -> **Module scaffolding actions** section will control scope of this module will affect, so let uncheck *Tenent Setup* because we need site only -> Process

   <img src="image\create_module\step02.png" width="300" style="vertical-align:top">
   <img src="image\create_module\step02.1.png" width="300" style="vertical-align:top">

   Step 3: To add modules to your site -> move to your site, in this scenario, I'll move on *Content/SitecoreDemo/CompanyDemo* -> right click -> script -> add site modules -> choose your modules, I will install **DemoCustoms** -> Ok -> Now you can see that module in Experience Editor Tools box

   <img src="image\create_module\step03.png" width="300" style="vertical-align:top">
   <img src="image\create_module\step03.1.png" width="300" style="vertical-align:top">

### II. **Create template**
   
   Create template so simple.

   First we create template folder, It help us manage it easy.
   
   Step 1: In **content** tree -> open **template** node -> right click -> insert -> template folder .\
   Step 2: It will show message dialog to name this folder. After write your name then click ok. In this pratice, I'll call it is *CompanyDemo*.\
   Step 3: Continous right click on CompanyDemo -> insert -> new template and dialog will be opened.\
   Step 4: We will fill in here name of this template, also we can chose template that this template inherit from but let leave it by default atm. I'll call this template is *DemoPage*. Then click next.\
   Step 5: Location dialog opened, at here we can chose where template will be inserted in however let chose *CompanyDemo* folder. Then click next\
   So our "Page Template" have been created and it will look like image 6

   Image Exp:

   <img src="image\create_template\step01.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step01.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step02.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step03.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step04.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step05.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step06.png" width="300" style="vertical-align:top">

   So simple right? however the next thing is abit different. We will learn about [standard value, token](#3-standard-value), [interface template](#1-interface-template), [Shared and Unversioned property](#4-create-component-view-rendering-controller-rendering-and-how-to-use-layout)

#### 1. **Interface template**

   Interface template is created as template but have name must begin by "_". For exp:\
   <img src="image\create_template\InterfaceTemplateExp.png" width="300" style="vertical-align:top">

   It's used as standard template to other template can inherit. It like interface in code and class inherit it. We have 2 way to inherit "Interface Template":

   Case 1: We inherit from creation step, however at that step, we can only inherit one template.

   We follow up step in create template but let's pause at step 2. I'll call this template's name is SampleInheritTemplate. On base template below the name, we click in and chose Interface template. I'll go to *Templates/Foundation/Experience Accelerator/Content Validation/* and chose **_HasValidUrlName**

   <img src="image\create_template\step07.png" width="300" style="vertical-align:top">

   After that we follow up step as normal from step 3.\
   Finaly, we can see like image below.

   <img src="image\create_template\step08.png" width="300" style="vertical-align:top">

   To verify this template is inherit from where, we can go to *Inheritance* tab or **Content** tab -> Data section -> base template:

   <img src="image\create_template\step09.png" width="300" style="vertical-align:top">

   Case 2: We can change list of inherit template in *Content* tab -> data section -> base template

   Let click to **DemoPage** and go to *Content* tab -> data section -> base template:

   <img src="image\create_template\step10.png" width="300" style="vertical-align:top">

   I'll go to *Templates/Foundation/Experience Accelerator/Content Validation/* and chose **_HasValidUrlName** again and save. Then it done:

   <img src="image\create_template\step11.png" width="300" style="vertical-align:top">

   
   All look be fine but let setup abit more. I'll add interface bellow to DemoPage:
   - Templates/Feature/Experience Accelerator/Navigation/_Navigable
   - Templates/Foundation/Experience Accelerator/Search/Computed Fields/_Page Search Scope
   - Templates/Foundation/Experience Accelerator/Search/Computed Fields/_Searchable
   - Templates/Feature/Experience Accelerator/SiteMetadata/_Custom Metadata
   - Templates/Feature/Experience Accelerator/SiteMetadata/_OpenGraph Metadata
   - Templates/Feature/Experience Accelerator/SiteMetadata/_Seo Metadata
   - Templates/Feature/Experience Accelerator/SiteMetadata/Sitemap/_Sitemap
   - Templates/Feature/Experience Accelerator/SiteMetadata/_Twitter Metadata
   - Templates/Feature/Experience Accelerator/StickyNotes/_Sticky Note
   - Templates/Foundation/Experience Accelerator/Taxonomy/_Taggable
   - Templates/Foundation/Experience Accelerator/Local Datasources/Base/_Local Data Link
   - Templates/Foundation/Experience Accelerator/Presentation/_Designable
   - Templates/Foundation/Experience Accelerator/Theming/_Styleable
   - Templates/Foundation/Experience Accelerator/Multisite/Content/Page
   - Move page to the top and remove Standard Template

   <img src="image\create_template\step12.png" width="300" style="vertical-align:top">

#### 2. **section and Attribute in Template**

   Back to *Builder* tab. This tab will manage section and field of componet when it is created base on your template.

   Let add a section name **Content** and field name **Title** and **AdditionalText**. Chose *Single-Line Text* type for *Title* and *AdditionalText* and save. New empty row for field and section will be created automatic when we fill info:

   <img src="image\create_template\step13.png" width="300" style="vertical-align:top">

   The effect will show in [Component Practice](#4-create-component-view-rendering-controller-rendering-and-how-to-use-layout).

#### 3. **Standard Value**

   We have create template without stardard value, when we create component base on that template, it's field in your section define will be empty. For best practice, we should add standard value for it.

   Step 1: click to *DemoPage* -> move to *Builder Options*  tab in ribbon -> chose *Standard Values* in *Templates* section

   <img src="image\create_template\step14.png" width="300" style="vertical-align:top">
   <img src="image\create_template\step15.png" width="300" style="vertical-align:top">

   Step 2: We can fill/ chose any value that base on it field's type for standard value here. However, we will use [Token](#4-templates) that have been mentioned in templates overview.
   `$name` for title\
   `$name hello everyone!` for AdditinalText

   <img src="image\create_template\step16.png" width="300" style="vertical-align:top">

   That done! It'll help your standard value become dynamic and it effect you can see in [Component Practice](#4-create-component-view-rendering-controller-rendering-and-how-to-use-layout).

#### 4. **Insert Options**

   At this pratice, we are admin and have full control however user won't have some permission in real scenario. So to use template we created, we should add it to insert options of component.

   At this pratice, we will add it to Home at CompanyDemo sit in SitecoreDemo tenant. Move to *Content/SitecoreDemo/CompanyDemo/Home* -> In *Insert Options* section -> Insert Options field -> edit

   <img src="image\create_template\step17.png" width="300" style="vertical-align:top">

   In Select Items dialog, let add *DemoPage* template and save

   <img src="image\create_template\step18.png" width="300" style="vertical-align:top">

### III. **Create Layout**
   
   After set up project in Visual Studio as tutorial in the begin of this [pratice](#site-core-pratice), we can start.

   Step 1: In conten tree, open *Layout* node and go to layout folder. Right click -> insert -> *Layout Folder*

   <img src="image\create_layout\step01.png" width="300" style="vertical-align:top">

   Step 2: Message dialog will be opened -> Write your folder name, I'll call its name is CompanyDemo and OK.

   <img src="image\create_layout\step02.png" width="300" style="vertical-align:top">

   Step 3: After created, right click at that folder -> insert -> MVC Layout.

   <img src="image\create_layout\step03.png" width="300" style="vertical-align:top">

   Step 4: Dialog opened, then I'll call its name is PageDemoLayout -> click next.

   <img src="image\create_layout\step04.png" width="300" style="vertical-align:top">

   Step 5: Location dialog open, then chose CompanyDemo folder and click create -> close

   <img src="image\create_layout\step05.png" width="300" style="vertical-align:top">

   Step 6: Back to VStudio and open your project have been created at begining

   Step 7: Go to Views/Shared -> right click -> add -> View

   <img src="image\create_layout\step07.png" width="300" style="vertical-align:top">

   Step 8: Choose MVC view -> Name it is *PageDemoLayout* (same as layout you created) - *uncheck use layout page* -> add

   <img src="image\create_layout\step08.png" width="300" style="vertical-align:top">
   <img src="image\create_layout\step09.png" width="300" style="vertical-align:top">

   Step 9: Change code in that view to below:
   ```c# html
   @using Sitecore.Mvc
   @* @using Sitecore.Mvc.Analytics.Extensions *@
   @{
      Layout = null;
   }
   <!DOCTYPE html>
   <html>
   <head>
      <title>
         @Html.Sitecore().Field("title", new { DisableWebEdit = true })
      </title>
   </head>
   <body>
      <h1>@Html.Sitecore().Field("title")</h1>
      <div>@Html.Sitecore().Placeholder("PageDemoPlaceholder")</div>
   </body>
   </html> 
   ```
   - `Placeholder(<placeholder-name>)` will map that position to placeholder have that name.
   - `Field(<field-name>)` will extract data from field name in sitecore.

   Step 10: Right click in project and choose publish -> go to *Views/Shared* in sitecore host folder -> PageDemoLayout will exist.

   Step 11: Back to sitecore, click to layout we created -> Data section -> add `/Views/Shared/PageDemoLayout.cshtml` value to *Path* field.

   <img src="image\create_layout\step11.png" width="300" style="vertical-align:top">

   That all, but to use it, we must have placeholder map with place holder in that layout. In this case, placeholder's name is `PageDemoPlaceholder`. Then we must create placeholder

   Step 12: Move to Layout node -> Placeholder Setting -> right click -> insert -> placeholder settings folder -> Write its name is CompanyDemo too -> Create

   <img src="image\create_layout\step12.1.png" width="300" style="vertical-align:top">
   <img src="image\create_layout\step12.2.png" width="300" style="vertical-align:top">

   Step 13: Right click in that folder -> insert -> Placeholder -> Its name will be `PageDemoPlaceholder` -> create

   <img src="image\create_layout\step13.1.png" width="300" style="vertical-align:top">
   <img src="image\create_layout\step13.2.png" width="300" style="vertical-align:top">

### IV. **Create component: View rendering, Controller rendering and how to use layout**
   
In section [Create layout](#3-create-layout) we created layout, then let use it in *DemoPage*

Step 1: Let move on *Templates/CompanyDemo/DemoPage/__Standard Values* anh click it.

<img src="image\create_component\Step01.png" width="300" style="vertical-align:top">

Step 2: In ribbon -> *Presentation* tab -> *Layout* section -> . Diaglog Layout Details will open -> chose edit at Default in Shared Layout tab.

<img src="image\create_component\Step02.png" width="300" style="vertical-align:top">

Step 3: In Device Editor -> Layout tab -> change it to PageDemoLayout and save

<img src="image\create_component\Step03.png" width="300" style="vertical-align:top">

Step 4: Move to Content/SitecoreDemo/CompanyDemo/Home -> right click -> insert -> DemoPage ([DemoPage was added in Insert Options](#4-insert-options)) -> Diglog will show to fill it name but we will leave it default atm.

<img src="image\create_component\Step04.png" width="300" style="vertical-align:top">

**Note:** Value at Content section in this page have been replaced with standard value and it token. `$name` is delegate to this page name

<img src="image\create_component\Step04.1.png" width="300" style="vertical-align:top">

Step 5: right click in DemoPage -> Experience Editor -> You can see layout of this page with place holder

<img src="image\create_component\Step05.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step05.2.png" width="300" style="vertical-align:top">

#### 1. **View rendering**

Step 6: Back to VStudio -> Add new folder `Components` into Views -> After that, add new view `AdditionalTextView` into it Overwrite all its content by code below and save:

```c# html
<div>
   @Html.Sitecore().Field("AdditionalText")
</div>
```

<img src="image\create_component\Step06.png" width="300" style="vertical-align:top">

Step 7: We have created *DemoCustomes* module in [Create Modules](#1-create-modules), it'll automatic create *DemoCustoms* in Layout node s. Move on *Layout/Renderings/Feature/SitecoreDemo/DemoCustoms* ->  create rendering folder by right click on it -> insert -> view rendering -> name it is `AdditionalText`.

<img src="image\create_component\Step07.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step07.2.png" width="300" style="vertical-align:top">

Step 8: At data section -> add value `/Views/Components/AdditionalTextView.cshtml` to *Path* field.

<img src="image\create_component\Step08.png" width="300" style="vertical-align:top">

Step 9: Batch to VStudio and publish

Step 10: We created compoenent but it wont show in toolbox, we need more one step to add it to toolbox. Move on our site *Content/SitecoreDemo/CompanyDemo* -> go to *Presentation/Available Renderings* (this will comtrol item in toolbox) -> right click -> insert -> Available Renderings -> Message dialog showed -> name it is DemoCustoms -> Create

<img src="image\create_component\Step10.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step10.2.png" width="300" style="vertical-align:top">

Step 11: In Data section of DemoCustoms -> Edit -> *Layout/Renderings/Feature/SitecoreDemo/DemoCustoms* -> select AdditionalText -> add it and OK -> save

<img src="image\create_component\Step11.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step11.2.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step11.3.png" width="300" style="vertical-align:top">

Step 12: Move on *Content/SitecoreDemo/CompanyDemo/Home/DemoPage* -> right click -> Experience Editor -> click add in placeholder -> *Select a Rendering* dialog -> DemoCustoms section -> AdditionalTex -> OK -> Save -> As result we can see AdditionalText field of DemoPage will show in web.

<img src="image\create_component\Step12.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step12.2.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step12.3.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step12.4.png" width="300" style="vertical-align:top">

#### 2. **Controller rendering**

Controller rendering have many benefit because it will reference to action in controller so it can have view and code in it self

First, we create it's data source for rendering

Step 13: Move to *Templates/Feature/SitecoreDemo/DemoCustoms* -> right click -> insert -> New Templates -> Name it **DemoSlider**

<img src="image\create_component\Step13.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step13.2.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step13.3.png" width="300" style="vertical-align:top">

Step 14: In builder tab, Add new section **Slider Content**, add new field **SliderImages** with type **TreeList** and Source is `query:$site/*[@@name='Media']` (this will query set data source is to -site name-/-folder name Media-) -> save

<img src="image\create_component\Step14.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step14.2.png" width="300" style="vertical-align:top">

Step 15: Now, let add DemoSlider template to DemoPage insert options. Move on *Templates/CompanyDemo/DemoPage/__Standard Values* -> Insert Options -> Add DemoSlider template to insert options. exp in [Insert Options practice](#4-insert-options) -> Save

<img src="image\create_component\Step15.png" width="300" style="vertical-align:top">

Step 16: Next, we add instant of DemoSlider in DemoPage. Move on *Content/CompanyDemo/Home/DemoPage* -> right click-> insert -> DemoSlider -> name it **DemoSlider** -> add and save. You can see in *Slider Content* section, SliderImages field will show content tree in folder you have setup.

<img src="image\create_component\Step16.png" width="300" style="vertical-align:top">


Step 17: To easy modify, let add new media folder in *Content/CompanyDemo/Media/CompanyDemo* -> right click -> insert -> Media Folder -> name it DemoSlider -> OK. After create folder, let upload image in this source `image\demo_slider` to that folder by click *Upload Files (Advanced)* -> Choose your image -> upload -> You will see warning in each image -> click to image -> fill in Alt field to ignore alert -> close

<img src="image\create_component\Step17.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step17.2.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step17.3.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step17.4.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step17.5.png" width="300" style="vertical-align:top">

Step 18: Back to DemoSlider instant in step 16 and add image to it's *SliderImages field*

<img src="image\create_component\Step18.png" width="300" style="vertical-align:top">

After follow upper step, we will create **Controller Rendering**.

Step 19: Go to VStudio and open CompanyDemo project -> Controller -> Add controller -> in Scaffolded dialog select MVC Controller empty -> name it *DemoController*

<img src="image\create_component\Step19.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step19.2.png" width="300" style="vertical-align:top">

Step 20: Overwrite your controller by code bellow:

```c#
using System;
using System.Web.Mvc;
using Sitecore;
using Sitecore.Data.Items;
using Sitecore.Mvc.Controllers;
using Sitecore.Mvc.Presentation;

namespace CompanyDemo.Controllers
{
    public class DemoController : SitecoreController
    {
        public ViewResult HeroSlider()
        {
            Item contentItem = null;
            var database = Context.Database;
            if (database != null)
            {
                if (!String.IsNullOrEmpty(
                RenderingContext.Current.Rendering.DataSource))
                {
                    contentItem = database.GetItem(new Sitecore.Data.ID(
                    RenderingContext.Current.Rendering.DataSource));
                }
            }
            return View(contentItem);
        }
    }
}
```

Step 21: Right click in View -> add view -> MVC 5 View -> Add

<img src="image\create_component\Step21.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step21.2.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step21.3.png" width="300" style="vertical-align:top">

Step 22: Overwrite content by code below:
```c# html
@model Sitecore.Data.Items.Item
@using Sitecore.Data.Fields
@using Sitecore.Data.Items
@using Sitecore.Resources.Media
@{
    Layout = null;
}
@if (Model != null)
{
    <div id="demo" class="carousel slide" data-ride="carousel">

        <!-- Indicators/dots -->
        <div class="carousel-indicators">
            <button type="button" data-bs-target="#demo" data-bs-slide-to="0" class="active"></button>
            <button type="button" data-bs-target="#demo" data-bs-slide-to="1"></button>
            <button type="button" data-bs-target="#demo" data-bs-slide-to="2"></button>
        </div>

        <!-- The slideshow -->
        <div class="carousel-inner">
            @{
                IEnumerable<Item> heroImages = null;
                var heroImagesField = new MultilistField(
                Model.Fields["SliderImages"]);
                if (heroImagesField != null)
                {
                    heroImages = heroImagesField.GetItems();
                }
                if (heroImages != null)
                {
                    int i = 1;
                    foreach (var image in heroImages)
                    {
                        var mediaItem = (MediaItem)image;
                        <div class="carousel-item @(i == 1 ? "active" : "") ">
                            <img class="d-block" style="width:100%" src=" @MediaManager.GetMediaUrl(mediaItem) " />
                        </div>
                        i++;
                    }
                }
            }
        </div>

        <!-- Left and right controls/icons -->
        <button class="carousel-control-prev" type="button" data-bs-target="#demo" data-bs-slide="prev">
            <span class="carousel-control-prev-icon"></span>
        </button>
        <button class="carousel-control-next" type="button" data-bs-target="#demo" data-bs-slide="next">
            <span class="carousel-control-next-icon"></span>
        </button>
    </div>
}
```

Step 22: Publish your project and back to Content Editor to add Controller Rendering

<img src="image\create_component\Step23.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step23.2.png" width="300" style="vertical-align:top">

Step 23: Move to *Layout/Renderings/Feature/SitecoreDemo/DemoCustoms* -> right click -> insert -> Controler Rendering -> name it *DemoSlider* and click Ok

Step 24: Click in item we created, we need fill up some infomation to map it with controller. In *Data* section, Controller field value is `Demo` (Demo is controller we created in VStudio), Action field value is `DemoSlider`. In Edit options, *Datasource Location* field value is `./`, *Datasource Template* will reference to DemoSlider template  (step 13-18), its value is `Templates/Feature/SitecoreDemo/DemoCustoms`

<img src="image\create_component\Step24.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step24.2.png" width="300" style="vertical-align:top">

Step 25: Now add it to toolbox in CompanyDemo site. Back to *Content/SitecoreDemo/CompanyDemo/Presentation/Available Renderings/DemoCustoms* -> Data section, Renderings field -> add DemoSlider rendering into it

<img src="image\create_component\Step25.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step25.2.png" width="300" style="vertical-align:top">

Step 26: Open experience Editor of DemoPage -> Remove remove *AdditionalText* in placeholder -> Click on placeholder -> Add -> DemoCustoms -> DemoSlider -> save

<img src="image\create_component\Step26.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step26.2.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step26.3.png" width="300" style="vertical-align:top">

Step 27: I'll show like image below because we don't have css and script. Because DemoPage used *PageDemoLayout*, we will add css and script to it. Back VStudio -> PageDemoLayout -> Overwrite content with code bellow (we add script and css). Result will look like image below. After that, publish
```c# html
@using Sitecore.Mvc
@* @using Sitecore.Mvc.Analytics.Extensions *@
@{
    Layout = null;
}
<!DOCTYPE html>
<html>
<head>
    <title>
        @Html.Sitecore().Field("title", new { DisableWebEdit = true })
    </title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/css/bootstrap.min.css" rel="stylesheet">
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.3.1/dist/js/bootstrap.bundle.min.js"></script>
</head>
<body>
    <h1>@Html.Sitecore().Field("title")</h1>
    <div class="container">@Html.Sitecore().Placeholder("PageDemoPlaceholder")</div>
</body>
</html> 
```

<img src="image\create_component\Step27.1.png" width="300" style="vertical-align:top">
<img src="image\create_component\Step27.2.png" width="300" style="vertical-align:top">

Result:

### V. **Setup BlogPage**

Our page structure will have 3 Layer: Header, Content, Footer, to easy handle, we will make Header and Footer become partial and we will use Partial Design from SXA

#### 1. **Presentation Layer**

Step 1: Move on *content/SitecoreDemo/CompanyDemo/Presentation/Partial Designs* -> right click -> insert -> Partial Design Folder -> Name it *Common* -> Ok. After that let create Header and Footer partial. Right click on *Common* -> Insert -> Partial Design -> Name it *Header*, do the same with Footer.

<img src="image\setup_blog\partial_design\step01.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step01.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step01.3.png" width="300" style="vertical-align:top">

Step 2: Right click on **Header** and open Experience Editor -> In ribbon/presentation tab/ Layout -> Let set this editor to edit **Shared Layout**, It look like image below

<img src="image\setup_blog\partial_design\step02.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step02.2.png" width="300" style="vertical-align:top">

Step 3: Drag and drop *Spliter (Rows)* into header placeholder

<img src="image\setup_blog\partial_design\step03.png" width="300" style="vertical-align:top">

Now we add logo to the page

Step 4: Drag and drop *Image (Reusable)* into first row in header placeholder. *Select the Associated Cotent* dialog open, then click **create** near *Images (Current site)* -> Image Folder -> Name it Header -> click create new that folder -> Image -> name it logo -> ok

<img src="image\setup_blog\partial_design\step04.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step04.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step04.3.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step04.4.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step04.5.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step04.6.png" width="300" style="vertical-align:top">

Step 5: Click to item you droped in step 4 -> click to *Edit style and behavior* like image below -> Let fill value to field like image below -> OK

<img src="image\setup_blog\partial_design\step05.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step05.2.png" width="300" style="vertical-align:top">

Add toggle that will containt search box

Step 6: Drag and drop Toggle under your logo like image -> do the same step with logo -> result like image below

<img src="image\setup_blog\partial_design\step06.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step06.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step06.3.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step06.4.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step06.5.png" width="300" style="vertical-align:top">

Step 7: Click to toggle and click *Edit style and behavior* -> edit field like image below -> OK

<img src="image\setup_blog\partial_design\step07.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step07.2.png" width="300" style="vertical-align:top">

Step 8: Drag and drop search box to this toogle

<img src="image\setup_blog\partial_design\step08.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step08.2.png" width="300" style="vertical-align:top">

Add navigation, breadcrumb

Step 9: Drag and drop navigation to second row ->Click *Edit style and behavior* and set field like image below -> drag and drop breadscrumb under navigation like image

<img src="image\setup_blog\partial_design\step09.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step09.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step09.3.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step09.4.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step09.5.png" width="300" style="vertical-align:top">

Step 10: Right click on **Footer** and open Experience Editor -> drag and drop *Link list* into footer placeholder -> In *Select the Associated Content* create Link list folder -> name it Footer Link List -> Create link list -> name it *About* -> Open *Edit style and behavior* and fill it like image. We drag drop 2 more *Link List* and it'll map with *Support* and *Social*

<img src="image\setup_blog\partial_design\step10.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step10.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step10.3.png" width="300" style="vertical-align:top">

Step 11: Drag drop *Spliter (Rows)* under latest link list like image -> drag and drop 3 link list were created into first row.

<img src="image\setup_blog\partial_design\step11.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step11.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step11.3.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step11.4.png" width="300" style="vertical-align:top">

Step 12: Drag and drop new link list to second row like step 10 -> name it is contact -> drag drop *rich text (reusable)* under contact -> create Footer folder and source name is Copyright -> OK

<img src="image\setup_blog\partial_design\step12.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step12.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step12.3.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step12.4.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step12.5.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step12.6.png" width="300" style="vertical-align:top">

Step 13: Move to *content/SitecoreDemo/CompanyDemo/Presentation/Page Design* -> insert -> Page Design and name it *Home*

<img src="image\setup_blog\partial_design\step13.1.png" width="300" style="vertical-align:top">

Step 14: Add Footer and Header partial design to Home. In Content tab of Home -> *Designing* section -> Partial designs -> Add Header and Footer and remove unnecessary design and sort it like image. Then open *Content* tab of *Page Designs* and set design map like image.

<img src="image\setup_blog\partial_design\step14.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step14.2.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\partial_design\step14.3.png" width="300" style="vertical-align:top">

#### 2. **Create Blog Page Template**

Our blog will have many blog content in there so we should create Page Template to manage it

Step 1: Go to *Templates/Project/SitecoreDemo* -> Insert -> New Template -> name it `Blog Overview` and have base template is *Templates/Project/SitecoreDemo/Page* -> Location is *Templates/Project/SitecoreDemo*

<img src="image\setup_blog\create_blogpage_template\step01.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step02.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step03.png" width="300" style="vertical-align:top">

Step 2: In ribbon -> *Configure* tab -> *Icon* (find in the left screen) -> move icon -> search and select **prices** in office section

<img src="image\setup_blog\create_blogpage_template\step04.png" width="300" style="vertical-align:top">

Step 3: Create *Blog Detail* template same within step 1 and 2 but let name it *Blog Detail* and select price icon

<img src="image\setup_blog\create_blogpage_template\step05.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step06.png" width="300" style="vertical-align:top">

Step 4: Back to *Block Detail* -> *Builder* tab -> Add new section and new field with name and type like below.

<img src="image\setup_blog\create_blogpage_template\step07.png" width="300" style="vertical-align:top">

Step 5: Move to *Blog Overview* -> add Standard Values (find in Option tab of ribbon) -> open *Content* tab of standard value -> *Insert Options* section -> add Blog Detail into it.

<img src="image\setup_blog\create_blogpage_template\step08.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step09.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step10.png" width="300" style="vertical-align:top">

Step 6: Move to Block Detail -> Add standard values -> In standard value -> add token value like image below -> save

<img src="image\setup_blog\create_blogpage_template\step11.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step12.png" width="300" style="vertical-align:top">

Step 7: Move to Content/SitecoreDemo/CompanyDemo/Home -> Content tab -> Insert Options ection -> add Blog Overview into Insert Options field.

<img src="image\setup_blog\create_blogpage_template\step13.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step14.png" width="300" style="vertical-align:top">

Step 8: Let add Blog over view and Blog Detail. At home -> Insert *Blog Overview* -> name it `Blogs` -> At Blogs -> Insert -> *Blog Detail* -> name it `Blog Detail 01` -> we create until have `Blog Detail 10`

<img src="image\setup_blog\create_blogpage_template\step15.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step16.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\create_blogpage_template\step17.png" width="300" style="vertical-align:top">

#### 3. **Create custom renderings variant**

we will have a component to handle show most popular blog so let create one.

Step 1: Move to *Layout/Renderings/Features/Page Content/Promo* -> right click -> script -> clone rendering.

<img src="image\setup_blog\custom_rendering\step (1).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (2).png" width="300" style="vertical-align:top">

Step 2: In Create Derivative rendering -> General tab -> name it *Most popular* -> fill up other field like image -> *Parameters* and *Datasource* tab -> set value is *Make a copy of original rendering parameters* (this option will make a copy of all related promo) -> View tab -> Set *Copy MVC view file (specify path below)* (this option will make a copy of Promo view file to path below this option) -> Set path like image -> Proceed -> Done

<img src="image\setup_blog\custom_rendering\step (3).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (4).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (5).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (6).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (7).png" width="300" style="vertical-align:top">

Step 3: Check *Most popular* rendering and will see it'll have Datasource Location point to your *Site* or *sharedSite* /Data /Folder created from template *Most popular Folder*

<img src="image\setup_blog\custom_rendering\step (8).png" width="300" style="vertical-align:top">

Step 4: Move to *Templates/Feature/SitecoreDemo/DemoCustoms/Most popular* -> In its bulder tab, remove all field and rename section to *Blogs*, clear field name and it'll automatic remove that field when you leave -> Add 2 field with type like image below -> in source of Blogs field, we use query source `query:$site/*[@@name='Home']/*[@@templatename="Blog Overview"]` to point source to page created from *Blog Overview* in Home

<img src="image\setup_blog\custom_rendering\step (9).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (10).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (11).png" width="300" style="vertical-align:top">

Step 5: We should modify Branches templates of Most popular Variant -> *Templates/Branches/Feature/SitecoreDemo/DemoCustoms/Default Most popular Variant/$name/Default* -> remove all content -> Inert -> Field -> name it *Headline* -> back to *Default* -> Insert -> reference -> name it *Blogs* and sort it like image.

<img src="image\setup_blog\custom_rendering\step (12).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (13).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (14).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (15).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (16).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (17).png" width="300" style="vertical-align:top">

Step 6: In content of *Blogs*, Variant Details section and set *Maximal number of results* to 3 (limit number result to show)

<img src="image\setup_blog\custom_rendering\step (18).png" width="300" style="vertical-align:top">

Step 7: Right click on *Blogs* -> insert -> section and name it column -> right click to column -> add 3 field name *Headline*, *Image*, *Description* and sort it like image. -> Back to *Column* -> set *Is link* in *Variant Details* is Wrapped

<img src="image\setup_blog\custom_rendering\step (19).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (20).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (21).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (22).png" width="300" style="vertical-align:top">

Step 8: Back to Default and insert 2 section name *section-title* and *row* -> then move Headline to section title and blogs to row

<img src="image\setup_blog\custom_rendering\step (23).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (24).png" width="300" style="vertical-align:top">

After we custom *Most popular*, to use it in site, we must add it in and prepare datasource for it

Step 9: Move to *Content/SitecoreDemo/CompanyDemo/Presentation/Available Renderings* -> insert -> insert from template -> select branch template of *Available Most popular Renderings* (*Templates/Branchs/Feature/SitecoreDemo/CompanyDemo/Available Most popular Renderings*)

<img src="image\setup_blog\custom_rendering\step (25).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (26).png" width="300" style="vertical-align:top">

Step 10: Move to *Content/SitecoreDemo/CompanyDemo/Presentation/Rendering Variants* -> insert -> insert from template -> select branch template of *Most popular Rendering Variant* (*Templates/Branchs/Feature/SitecoreDemo/CompanyDemo/Default Most popular Rendering Variant*)

<img src="image\setup_blog\custom_rendering\step (27).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (28).png" width="300" style="vertical-align:top">

Step 11: Move to *Content/SitecoreDemo/CompanyDemo/Data -> insert -> insert from template -> select template of *Most popular Folder* (*Templates/Feature/SitecoreDemo/CompanyDemo/Most popular Folder*)

<img src="image\setup_blog\custom_rendering\step (29).png" width="300" style="vertical-align:top">
<img src="image\setup_blog\custom_rendering\step (30).png" width="300" style="vertical-align:top">

#### 4. **Edit your Home page**

In [step 14 of presentation layoer](#1-presentation-layer), we setup Page Design of *CompanyDemo/Home* is *CompanyDemo/Presentation/Page Designs/Home* so when we open Experience Editor, It'll look like below

<img src="image\setup_blog\edit_home_design\step01.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\edit_home_design\step01.2.png" width="300" style="vertical-align:top">

To prepare content we will add *Spliter (Rows)* to divide main placeholder to 3 row placeholder. Drag and drop *Spliter (Rows)* into main -> Click + to add one more row -> Result will have 3 row

<img src="image\setup_blog\edit_home_design\step02.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\edit_home_design\step02.1.png" width="300" style="vertical-align:top">

In First Row, we will [add Demo Slider](#add-your-custom-slider)

Second row, we will [add Most Populator rendering](#add-most-popular)

Final row, we will [add search content](#add-search-content)

##### **Add your custom slider**

Because item in SXA already have configured their insert options, you won't see create data source for DemoSlider if you add it into Page at Experience Editor. So you must modify DemoSlider Renderings datasource location.

Step 1: move to *Layout/Renderings/Feature/SitecoreDemo/DemoCustoms/DemoSlider* -> Content tab -> update Datasource Location value: `query:$site/*[@@name='Data']/*[@@templatename='DemoSlider']`

<img src="image\setup_blog\add_slider\step01.png" width="300" style="vertical-align:top">

Step 2: Move to our site/data (*CompanyDemo/Data*) -> Insert -> Insert from template -> Select DemoSlider template from *Templates/Feature/SitecoreDemo/DemoCustoms/DemoSlider* -> Name it *Home DemoSlider*

<img src="image\setup_blog\add_slider\step02.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\add_slider\step03.png" width="300" style="vertical-align:top">

Step 3: Back to *CompanyDemo/Home* -> open Experience Editor -> Drag and drop DemoSlider from DemoCustoms to first row in the main placeholder -> Select the Associated Content will show Home DemoSlider in step 2 -> Ok and save

<img src="image\setup_blog\add_slider\step04.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\add_slider\step05.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\add_slider\step06.png" width="300" style="vertical-align:top">

##### **Add Most Popular**

Step 1: Drag and drop *Most popular* into second row -> Select the Associated Content -> You can se *Most popular* folder we was created in [Create custom rendering](#3-create-custom-renderings-variant) -> create new datasource and name it *Most popular blog*

<img src="image\setup_blog\add_most_popular\step01.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\add_most_popular\step02.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\add_most_popular\step03.png" width="300" style="vertical-align:top">

Step 2: Back to Content Editor -> in your site *CompanyDemo/Data/Most popular/Most popular blogs* -> add blog detail into this, edit Headline field is *Most Popular* and save -> Experience Editor will be like below

<img src="image\setup_blog\add_most_popular\step04.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\add_most_popular\step05.png" width="300" style="vertical-align:top">

##### **Add Search Content**

Step 1: Drag and drop Search results into row 3 -> Create Search Results Folder and name it *Home Search Results* -> Create datasource for search result and name it *Latest Articles*

Step 2: In Search Results menu -> More -> Edit component properties -> Set field value in SearchCriteria and Styling like image.

Step 3: Drag and drop search box under search result -> Create datasource for source box and name it *Home Search Box*

Step 4: Search box menu -> click to settings icon to change the text of the search box on the page -> Set values like image

Step 5: Drag and drop *Load More* between Search Result and Search Box -> Create datasource for load more and name it *Home Load More* -> Click to settings and edit label is `Load More` ->  Click to *Edit Style and Behavior* button -> set values in Styling section like image

That is some component but it won't work. We must configure **[Facet and Scope](#configure-facets-and-scope)**. After that let add some filter.

Step 6: Move to *CompanyDemo/Data/Search/Sort Result* -> insert -> sorting groups and name it Articles -> right click -> insert -> Sorting -> name it `Newest` -> do the same to create `Oldest` -> General section in Content tab of Newest -> set value like image below. Do the same for Oldest

Step 7: Back to Home Experience Editor -> Drag and drop Sort Results on top of *Search Results* -> Select Articles datasource -> In menu of *Sort Results* -> settings -> set title value is `Sort` -> result will be like image.

Because we search on Blog Detail and we customed it field so we must define Variant for it.

Step 8: Move to *CompanyDemo/Presentation/Rendering Variants/Search Results* -> duplicate it *horizontal* variant and name new item is `horizontal_blog` -> right click on it -> insert 3 field variant and name it `Image`, `Headline`, `Description` with sort like image -> In each Content tab of those items, make sure the **Field Name** in Variant Details section is the same with Blog Detail field

Now we update search content in Experience Editor

Step 9: back to Home's Experience Editor -> Edit component properties of Search Results -> set field like image, Search Results signature is `latestarticles` (value can't have special character) -> Set same signature for Load More and Sort Results, it'll help those component can map together -> Set component properties for Search Box like image below.


###### **Configure Facets and Scope**

Facet is setting use for filter your search result by categorizing the items returned by the search. For example, for a blog search page, all blogs contain fields such as: author, date, and language. Based on these fields, you can create facets to allow visitors to use them as filters. (field value can be multi value)

Facet: Move to Settings in your site (*Content/SitecoreDemo/CompanyDemo/Settings*) -> right click Facets -> insert -> Facets Grouping and name it `Blog` -> right click on Blog and create 2 facets -> Insert -> List Facet (it mean search result will be list) -> Name it Created Date and Headline and sort it like image -> Open *Created Date*'s Content tab and set field name is `created_date` -> set that field's value is `headline` for *Headline*

<img src="image\setup_blog\search_result\step16.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\search_result\step17.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\search_result\step18.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\search_result\step19.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\search_result\step20.png" width="300" style="vertical-align:top">

Scope as it name is use for scaling or limit yor search. Search that map with related scope can only search content in that scope.

Scope: Move to *Content/SitecoreDemo/CompanyDemo/Settings* -> right click in Scopes -> insert -> Scope and name it `Blog Detail` -> Content tab of this, Scope section -> Set value is *custom:_templatename|blog detail* / you can click build query to open Build Search Query dialog -> write the search you want, for exp: Write template and select it, then item template will exist and you can fill template name in here -> click OK and it will create your query

<img src="image\setup_blog\search_result\step21.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\search_result\step22.1.png" width="300" style="vertical-align:top">
<img src="image\setup_blog\search_result\step22.2.png" width="300" style="vertical-align:top">

### VI. **Create theme**

Sometime, we would like to custom css, script ... etc so we will custom our themes 


[^1]: *Professional SiteCore 8 Development: A Complete Guide to Solutions and Best Practices: Wicklund, Phil, Wilkerson, Jason, n.d., pp. 8, 21, 24, 77*

[^2]: https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/data-sources.html

[^3]: https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/data-sources.html

[^4]: https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/the-sxa-items-in-the-content-editor.html#the-tenant-items

[^5]: https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/create-a-tenant-and-a-site.html

[^6]: https://doc.sitecore.com/xp/en/developers/102/platform-administration-and-architecture/configuration-layers.html
