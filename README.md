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
    - [8. **Tanent in SXA** \[^4\]](#8-tanent-in-sxa-4)
    - [9. **Site in SXA** \[^5\]](#9-site-in-sxa-5)
  - [**Site core pratice**](#site-core-pratice)
    - [1. **Create tanent and site**](#1-create-tanent-and-site)
      - [1. **Create Modules**](#1-create-modules)
    - [2. **Create template**](#2-create-template)
      - [1. **Interface template**](#1-interface-template)
      - [2. **section and Attribute in Template**](#2-section-and-attribute-in-template)
      - [3. **Standard Value**](#3-standard-value)
      - [4. **Insert Options**](#4-insert-options)
    - [3. **Create Layout**](#3-create-layout)
    - [4. **Create component: View rendering, Controller rendering and how to use layout**](#4-create-component-view-rendering-controller-rendering-and-how-to-use-layout)
  
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
- Brown Sitecore.Kernel/MVC.dll to project.
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
<img src="image\prepare_practice\step08.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step09.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step10.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step11.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step12.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step13.png" width="300" style="vertical-align:top">
<img src="image\prepare_practice\step14.png" width="300" style="vertical-align:top">

### 1. **Create tanent and site** 
   
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

   2. 

### 2. **Create template**
   
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

### 3. **Create Layout**
   
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

### 4. **Create component: View rendering, Controller rendering and how to use layout**
   
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

   **View rendering**

   Step 6: Back to VStudio -> Add new folder `Components` into Views -> After that, add new view `AdditionalTextView` into it Overwrite all its content by code below and save:

   ```c# html
   <div>
    @Html.Sitecore().Field("AdditionalText")
   </div>
   ```

   <img src="image\create_component\Step06.png" width="300" style="vertical-align:top">

   Step 7: Move on Layout/Renderings -> create rendering folder by right click on renderings -> insert -> rendering folder -> name it is CompanyDemo.

   <img src="image\create_component\Step07.1.png" width="300" style="vertical-align:top">
   <img src="image\create_component\Step07.2.png" width="300" style="vertical-align:top">

   Step 8: Right click in *CompanyDemo* folder -> insert -> view rendering -> name it is `AdditionalText`.

   <img src="image\create_component\Step08.1.png" width="300" style="vertical-align:top">
   <img src="image\create_component\Step08.2.png" width="300" style="vertical-align:top">

   Step 9: At data section -> add value `/Views/Components/AdditionalTextView.cshtml` to *Path* field.

   <img src="image\create_component\Step09.png" width="300" style="vertical-align:top">

   Step 10: Batch to VStudio and publish

   Step 11: Back to Content Editor -> Move on *Content/Home* -> right click -> Insert from template -> *Insert from Template* dialog opened -> Choose DemoPage template -> Item Name: DemoPage -> Insert

   <img src="image\create_component\Step11.1.png" width="300" style="vertical-align:top">
   <img src="image\create_component\Step11.2.png" width="300" style="vertical-align:top">
   <img src="image\create_component\Step11.3.png" width="300" style="vertical-align:top">

   Step 12: Right click in that item -> *Experience Editor* -> Click add in placeholder -> choose our rendering that is created -> Select

   <img src="image\create_component\Step12.png" width="300" style="vertical-align:top">

   Step 13: As result, we can see *AdditionalText* field was show by *view rendering component*

   <img src="image\create_component\Step13.png" width="300" style="vertical-align:top">

5. c
6. 


5. 

[^1]: *Professional SiteCore 8 Development: A Complete Guide to Solutions and Best Practices: Wicklund, Phil, Wilkerson, Jason, n.d., pp. 8, 21, 24, 77*
[^2]: [https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/data-sources.html]
[^3]: [https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/data-sources.html]
[^4]: [https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/the-sxa-items-in-the-content-editor.html#the-tenant-items]
[^5]: [https://doc.sitecore.com/xp/en/developers/sxa/102/sitecore-experience-accelerator/create-a-tenant-and-a-site.html]
[^6]: https://doc.sitecore.com/xp/en/developers/102/platform-administration-and-architecture/configuration-layers.html