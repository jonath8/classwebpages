# Overview
The purpose of this project is to provide a template for a class webpage that is easy to customize and uses the latest in computing technologies.  Unlike most wiki-style systems, this webpage does NOT use PHP, thereby avoiding problems with that when running on University resources where it may be restricted.  Being based on Jekyll, the resulting web page to come out of this project is a static HTML webpage which is simple to deploy anywhere you want.  

Thanks to Prof. Phil Lundrigan for the initial template.  Thanks to Jonathan Nelson, a Summer 2020 Immerse student, who further modified it and then authored the instructions below which describe how to use it.  

Prof. Brent Nelson  
July 2020


# Walkthrough to Build a New Class

## The Big Picture
1. You create files organized into directories.  You can create these pages using either Markdown or HTML.
2. From those files, the system will build a static HTML website.
3. Since this is based on Jekyll and Docker, it is easy to run the website while you develop, see your edits in real time until you like what you see, and then decide to deploy it.

## Starting It Up
In the description below you can changes things as you go if you have it all running.  There are also instructions on when and how you must kill it and restart (required for just a few changes you might make).

To start it up, do the following:
1. Install Docker on your system.  Consult the Docker documentation on how to do that.
1. Execute the command `sudo make develop`.  This will open the Docker image and expose the website it creates at `localhost:4000`.  You can point a browser at that and see your webpage change in real time as you edit files (except for the few cases mentioned below).

Before and during your reading of this walkthrough you are encouraged to experiment and examine the code.  The whole point of this project was to provide an easily-adaptable template to help get class websites up and running quickly and with a minimum of effort (where the majority of your effort can be focused on *what* you want for your website content rather than *how* it should be structured and formatted).

## File System

The file system of this project must be understood before any work begins. This system is based upon Jekyll, so if you have an understanding of Jekyll, you can skip this section. 

There are two different groupings of code. The first code is what you edit. These files use formats such as Markdown and SCSS, and are stored in directories based off the main directory. When you save your project, the server automatically compiles/recompiles all preprocess code (unless you have disabled live reloads in the Makefile). This processed code is more complex, and stored inside of the "_site" directory in the main directory. It is code that has been converted to fully usable HTML and CSS. 

Every main file and directory not in the "_site" directory will have a file of the same name inside of the "_site" directory. The _site directory should never be edited directly. Any edits should be made outside of the "_site" directory, then the project should be saved. When the project is saved, it replaces everything in the "_site" directory with newly compiled versions of the code, thus no changes should be made in that directory, because they will be deleted upon saving the file. Unless otherwise specified, all files mentioned will be the files outside of the "_site" directory.

## Changing Basic Site Information

There is a way to set basic site information (such as the class number, class description, teacher's email, etc...). Open `_config.yml`. Near the top, you will notice a section with a couple of variables, such as title, class_name, email, etc... This is where you can set up basic information for the site. Change all of these to reflect your class.

`_config.yml` is a special file. Other files in the project are updated in the website every time that you change them. However, .yml files are different. In order to reflect changes to them, you have to shut off Docker and start it back up. Then you will see your changes reflected in the page.

If you have done so (modified the `config.yml` file), you will see that the page looks largely the same. The title on the main page is even the same as it was before, why is that? It is because most of the things on this page are hardcoded. It's just the way we were given it by the professor... But, there is one place that changed for you. If you look in the sidebar, the name has been updated. This is because this was tied to the .yml file. There are actually a large number of easy to miss spots where these values are used, so it is important to change all of them just in case you have overlooked something.

If you want to use a value throughout your site, there is an easy way to access it. Simply write `{{ site.variableName }}`. Use the variable name in any place, and it will replace this expression for the value you set.

## Layout

Every page in this wiki is built upon two layout files found in the _layouts folder inside of the root directory. There is a page.html, and a default.html. The default layout is the main layout of the website. `default.html` contains all of the sidebar data, code to make the menu button clickable, page content information, and the Javascript information/licensing. 

The `page.html` file is an extension of default.html and inherits all information from the default template, and adds more info for the page headers, and page content. Each type is different, and the base website contains both types. See the pages section for more information on the difference between these two layouts.

SCSS files are another important file type in this project. They help you build the basic text formatting information, such as font size, and font color. To see how to influence font color and size, see below in the section `Font and Font Colors`. Different SCSS files format different parts of the page, with pages and sidebar being the most obvious.

## The Sidebar

### Basic Edits to the Sidebar

The basic information at the top the sidebar is all located inside of default.html in the `_layouts` folder.

To change the icon of the sidebar, you can go into the file, and find the comment for Sidebar, around line 39. These top few lines contain all of the sidebar info. Four lines below that comment, you should see the line `<img src="...">`, that is the icon information. If you have a downloaded icon that you would like to use, you can replace the path in the quotes with your own path. 

You could also replace the entire line with `<i class="..."></i>` and instead get an icon from Font Awesome's website. Go [here](https://fontawesome.com/icons?d=gallery), and find an icon you would like to use, and click on it. Just above the icon in this page, there should be a line of html, copy it, and paste it over top of the `<img src="..">`, and it will change. _Warning_: Font Awesome only allows free users to use some of its icons, the ones that have been grayed out are the icons for paid users, while free users can only use the black icons.

If you would like to change the name displayed at the top of the bar, there are two ways to change it. If you go into `_config.yml`, you should be able to find a line that says class_number. Change that, and it should change the class number for the entire site, which includes the top bar. If you would like to hard code it to say something else, just go into default.html, and change the spot that says `{{ site.class_number }}`. You can erase that whole thing, and write whatever you want there to hard code a title.

You can also delete the icon, or delete the title in order to not have one of those up there. But if you don't want both of them there, delete that entire line, as well as the line above, and the line below it. That will delete this entire piece of the side bar.

You also might have noticed that the sidebar scrolls in such a way, that is scrolls with the page, but it doesn't start scrolling until you get to almost the bottom of the page, then it scrolls. You can change that. If you want it to scroll as if it is part of the page (like most websites have it doing), then find the words `sidebar-sticky` inside of `default.html`, and replace it with `sidebar`. If it is just a sidebar, it will always scroll with the page, so when you reach the bottom of a long page, you won't see the sidebar. On the other hand, if you choose sidebar-sticky, you will always see at least part of the sidebar, and if you keep the sidebar short, you will always see the entire sidebar. You can choose which version of the sidebar works best for you.

### Adding New Pages to a Sidebar Group

To add new pages to an existing sidebar group, you should

1. Identify the files that are already in that sidebar group.
1. Find the folder in which the Markdown files for that grouping are located.
1. Create a new Markdown file located inside of that directory.
1. Create the file header (easiest to copy from another file and edit the necessary fields).
1. Edit the new file's contents.

Once you do this the new content will appear in the sidebar.

### Creating a New Sidebar Group

Creating a new sidebar group is significantly more difficult than adding new pages. To do so, you should

1. Create a new folder in the root directory of the project. This folder's name should start with an underscore. ie. "_resources", or "_files"
1. Open the `default.html` file inside of the "_layout" directory
1. Find the section labeled "\<!-- Sidebar -->"
1. Add a new entry to it, search for the names inside of the entries to find the location, the sidebar is ordered sequentially according to the html file. Below is an outline you can copy and paste, and replace the heading name, and folder name. The folder name should be the folder name you created minus the underscore "\_"

        <div class="sidebar-heading">{HEADING NAME}</div>
        <div class="list-group list-group-flush">
          {% for item in site.{FOLDER NAME} %}
          <a href="{{ item.url }}" class="list-group-item list-group-item-action bg-light sidebar-item">
            {% if item.icon %}
            <i class="{{ item.icon }}"></i>
            {% endif %}
            {{ item.title }}
          </a>
          {% endfor %}
        </div>
1. Open "\_config.yml"
1. Find the "collections:" section
1. Add a new entry to the grouping. Example entry below:

        FOLDER NAME:
            output: true
            permalink: SEE BELOW
1. Replace the FOLDER NAME with the name of your folder.  Once again, use the name of your created folder without the beginning underscore ("_labs" becomes labs).
1. For the permalink section, you have two options, you can either write `/:name/` or `/:collection/:name/`. This changes how the files are represented in the "_site" folder. If you choose /:name/, then each file will get its own folder inside of the "_site" directory. If you choose /:collection/:name/. then all folders inside of the directory will be put into one large directory inside of "_site", with each file having its own folder in there. A subtle difference, it is your choice how to organize it.
1. Then, you must then kill the docker from the command line, and restart. Killing can be done using Ctrl-C in Linux, or by using any universal kill command in Windows or Mac OS.
1. Once you restart, the new section should be in the sidebar, and any files you create will be updated into the sidebar automatically.

## Fonts and Font Colors

If you go into file `css/main.scss`, you can change the font color. "$text-color" changes the color of only the text on pages, not the sidebar. "$background-color" changes the color only on pages, not on the top or side bars. "$brand-color" changes the color of hyperlinks, and other random detail colors spread throughout the project (like the sidebar button). "$selection-color" changes the color of the the parts of the page highlighted by the mouse (like clicked and dragged over). "$sidebar-hover-color" changes the color that the sidebar buttons turn when they are hovered over by the mouse. You may experiment with these as much as desired, but they can also be left alone.

## Pages

The pages  you create in this Docker are processed into the final website pages using Jekyll, which comes pre-installed with the Docker image, and does not need to be downloaded to your machine. If you understand Jekyll, you may skip this section.

### Basic Pages

To edit pages in Jekyll, you can either choose to use HTML or Markdown for your editing, and it is not mutually exclusive. You can use both in different files in the same project. If you have no experience with either system, I suggest using Markdown, as it is significantly easier to learn than HTML. You can find good Mardown tutorials on the internet, such as [here](https://markdowntutorial.com). Or you can use any Markdown reference, as the system is quite easy to learn. You can find a good markdown reference [here](https://commonmark.org/help/).

#### Layouts

There are two layouts for the pages to use included with the git pull (you can find those in the "_layouts" directory). In order to use these, include the information in the header (see below). The first is the default layout. The default layout is the most basic layout you can have. It gives you more freedom. It allows you to choose exactly how you want the page to look. If you use this layout, you will have to create your own header, and own styling choices, which may or may not be what you want.

The page layout has more decisions made for you, and thus is easier to use. If you use the page layout, it will build a header for you. You just put the title into the header, and it will generate it for you, and you can put an icon there. It also decides the font information for you.

#### Header

The other important aspect of pages is the header at the top of all example files. The headers are distinct depending upon whether you are using the default layout, or page layout, or your own newly made layout.

If you use the default layout, your header will look something like this

        ---
        title: NAME
        layout: default
        icon: fas NAME
        wrapper_class: IMAGE_NAME
        sidebar_closed: true/false
        ---

Each entry in this header has different importance. In the default layout, the title only changes the name of the page while linking to it, the most obvious example being that if you change the title, the name of the page on the sidebar will also change. The layout section decides what layout you are using. The icon field decides the icon displayed on the page next to the page title on the sidebar. See the section "Icons" below to learn how to find icons. The wrapper_class field helps you specify what background image this specific page should use. If it is left blank, there will be no background image. To specify an image to use, you will need to add the image name into `_pages.scss`. To understand the process more, see "Changing the Background Image" below. The sidebar_closed field decides whether or not the sidebar should be closed by default when you enter the page. It defaults to false if the field is not included (meaning that the bar will be open when you enter the page).

The second layout, the page layout, is somewhat different. It looks  like this:

        ---
        title: NAME
        layout: page
        toc: true
        icon: fas NAME
        sidebar_closed: true/false
        wrapper_class: IMAGE_NAME
        ---

In this layout, the title will become the title of the page generated at the top for you automatically. It also changes the name of the page in the sidebar. The layout once again changes the layout template used. The toc field decides whether you want to use the built in table of contents found in the `_includes` folder. You can also build your own page widgets, and put them in that folder, and include them by name, but that is beyond the scope of this walkthrough. The icon field decides what icon this page should have in the header and the sidebar. See below on more information for icons. The sidebar_closed field decides whether or not the sidebar is closed when you open the page. If you don't include this field, then it will assume you want the bar open when you open the page. The wrapper_class decides what the background image will be. See the background image section to find out more. If you don't include a wrapper_class section, then there will be no background image.

#### Icons

All of the icons in this project are set up using Font Awesome, a web based icon service. To add icons to your webpage, you need to visit their website [here](https://fontawesome.com/icons?d=gallery). Once you are in the website, you can search for icons by name, or browse for them using the filters on the left sidebar. You can use any image which is the darker gray. Lighter gray icons are only for paying users.

Once you have found your icon, click on it. It will open a new page, and just above the picture of the icon, there should be a command of the form `<i class="********"></i>`. Get everything that represented by the stars in the example and copy it to the icon field on the top of a page. That will make the icon appear on the page.

### Background Images

Changing the background image is difficult and requires these steps.

1. Find a .svg file on the internet. (.jpeg and .png files can also be used, but it is easier to use .svg files due to their automatic sizing however.
1. Download the file, and place it into your project
1. Open `_pages.scss`
1. Here, you have two options, you can either edit the .home-image section, or create your own new image name.
    - If you simply want to edit the homepage background image, then change the .home-image background-image url to be the relative path to the image file in your project.
    - If you want to use multiple different backgrounds, then you'll have to do this style of change. You need to create a new named section in this scss file. The name must be prepended by a period. So you could name it `.temp`, (which means the name you will access it by will be temp), then you will add the information to it. Below is a template for you to use.
 ```
        .NAME {
            background-image: url("../images/FILE.svg");
            background-repeat: no-repeat;
            background-size: cover;
            background-position: 20% 0%;
        }
```
    A little side note about this part, you could change the size, 
    and have the background image repeat itself if you want.  
    But if you just want a picture, leave the repeat, size, 
    and position values as-is.
5. Then you will go to the specific files you want to change, and change their headers "wrapper_class" fields to contain the name that you created above.
1. Save, and your changes should be reflected in the background image.

If you just want to change the homepage's background image, you can simply edit the .home-image section url to be the relative path do a different file. This will change the homepage's background, because it is already set up to have the home-image as its background.

If you would like to be rid of all backgrounds in the website, simply go into the headers, and delete any wrapper_class fields in the project. You can then remove the .home-image field in `_pages.scss`.

### Embedded Images

You can embed images in two different ways in markdown, one is to use HTML style formatting (because markdown accepts any HTML syntax). The other is a markdown specific styling. This walkthrough will only cover markdown styling.

The basic formatting for an image is simple. You put the line `![NAME](RELATIVE_PATH_TO_IMAGE)` in between the two places you want it on the page. 

This will assume that you want the size of the image on the page to be the same size as the image itself, and that you want the image to be right aligned within the frame. If you want to change the size of the frame, you will need to add another flag just after the closing parenthesis on that image, it will be `{:height="#px" width="#px"}`. You can specify the exact size of you image in pixels. You can even resize a rectangular image to be square. If you just use this flag, your total line will look like `[NAME](RELATIVE_PATH_TO_IMAGE){:height="#px" width="#px"}`

The other commonly used flag is the picture alignment flag. It looks like `{:style="float: right;"}`. This will right align your image in the frame. This flag can be added to the end of the line, and be stacked next to the height and width flag. If you have text directly below this declaration on your markdown page, then that text will be on the left side of your image. The same thing happens with another image definition below this image definition. But if the right aligned image is below text, it will appear below the text. So you have to be aware of that. It will sit on the right of images placed above it however. A small distinction that will save you time if you remember it.

Centering images is somewhat harder. There is no automatic setting to center an image in markdown, so you have to include a centering option into your .scss files. Luckily, I found someone on the internet who had the know-how to make that (thanks stackoverflow), so the first step will be to copy and paste the text below into pages.scss.

        .center-image {
            margin: 0 auto;
            display: block;
        }

Then finally, when you want to make an image centered on an actual page, you can add the flag `{:.center-image}` to your image declaration, and that should center the image for you.

### Homepage

The homepage is more complicated than most other pages in this website. It has to be made with html to have all of its extra features. It is found as `index.html` inside of the project's root directory.

#### Changing Basic Homepage Information

The three most noticable features of the homepage are the boxes, the background, and the top text. The top text is the easiest to change. If you have experience with HTML, this section can be skipped.

To change the title of your class, go to line 9 of index.html where it says `<h1 class="page-title">`, and change the title to the title of your class.

To change the text below the title, go to line 11, where it says `<p><span ...>`, and you can edit the words there. If you want to be rid of the special capital first letter before the paragraph, you can delete the section `<span class="firstcharacter>C</span>`. This code creates the large first letter. If you want to keep it, the first letter of your first word should go inside of the `> </span>`.

#### Changing the Boxes

The most defining feature of the base website main page are the large boxes. This is leftover from the original teacher's website, but if you can't think of anything good to put here, you can just delete them. Delete everything between `<div class="row>` (which will be on line 17 if the file is still unedited), and the leftmost `</div>` of this section (line 64 of the unedited file).

If you want to keep these boxes, you'll need to find where all of the boxes are in the html. They should appear at line 18 unless the information above that has already been changed.

These boxes come with limitless possibilities, but I will only explain the basics you can change with the boxes. But if you learn more about the html involved, you could change colors, orientation, shape, and many more things.

##### Change the Number of Boxes

To change the number of boxes, copy and paste the section below into the box/cards section of index.html. Replace the icon, and bottom text with what you want.

    <div class="col text-center">
        <div class="card home-card">
            <div class="home-icon SET_ICON_HERE"></div>
            <div class="card-body">
                <p class="card-text">EDIT_BOTTOM_TEXT_HERE</p>
            </div>
        </div>
    </div>

##### Change the Box Logos

Changing the box logos is the most complicated part of this process. There are 5 basic icons already inside of the project for you. They are found in the images folder in the root directory of the project. If you would like to add a new icons, you will have to

1. Find a file on the internet you want. By far the easiest files to work with are .svg files. You can use .png, and .jpeg files, but they will need to be scaled to size manually. If they are too large, you will only get the center of the icon, if they are too small, you won't see the icon. It will also behave differently on different computers, so I strongly suggest using exclusively .svg files.
1. Once you have your .svg file, download it to your project. This file can technically be placed anywhere on the entire computer, and accessed by the file. I suggest putting it the images folder in the root directory. That contains the 5 included icons, so it is logical to place them here.
1. Once you have the location of the icon file, open the `_pages.scss` file inside of the `_sass` file in the root directory.
1. Scroll to the bottom, and copy and paste this section into it
  
        .NAME {
            background: url("RELATIVE_PATH_TO_FILE") no-repeat center center;
        }
1. Then, replace NAME with the name of the icon you want to create, and change the RELATIVE_PATH_TO_FILE using the path to where you put your .svg file.
1. Go back into index.html. Any time that you want to use this icon, replace other icons with `home-icon NAME`.
1. Save, and now you are using your new icon

I personally had trouble getting Font Awesome icons to function in this spot. I could only get them to appear as miniscule icons, so if you want, you can try to figure it out. If you do figure it out, please contact the people named above so we can update this walkthrough.

### Subpages and Page Links

On your webpage you are likely to have links to other pages within the site, and possibly other websites. All of these take a similar syntax to accomplish it: `[TEXT_DISPLAYED_TO_USER](PATH)`. Write whatever you want the clickable text to be displayed as in the square brackets, and put the path you want to link to in the parenthesis. If you are connecting to an external website, you will need to put the entire url, including the protocol used (IE. `https://`). You don't need to put www. but it still works with it included.

If you want to link to a subpage within the site, the process is somewhat more complicated

1. Find a place to put this page. You could make a subpage directory, or a walkthrough directory, or any directory which fits a grouping of pages. I personally put everything into a subpage directory, but this is your choice.
1. Create the page within the location you have found for it
1. Use the path above, but do it as a relative path. But this relative path is a bit more complicated than the previous ones. This is the relative path within the `_site` directory. Go in to the directory, and find the folder that contains your current page. It should have the same name as the file. Then find the folder of the same name as your destination page, and link to that folder. (This is important, because all pages are renamed to index.html in this directory, and are only distinguished by their folder name)

Now test it out, and you should have functional hyperlinks.

### Downloadable Files

If you want to have files that can be downloaded by the user, the simplest way to do that is to create a folder with all of the downloadable files in it, or to make multiple folders to split up large numbers of files. You create a download hyperlink to the file with the same syntax as the subpage information. `[TEXT_DISPLAYED_TO_USER](PATH)`.

The important thing to note with files is how different types of files interact with this. If an internet browser is able to open this type of file, then the browser itself will open the file. So files such as PDF, .txt, or html files will always be opened by the browser, and have to be saved manually by the user. But other file types, such as .doc, .pptx, or any code files (.py, .cpp, .java, .sv, etc...) will be downloaded to the users machine simply by clicking on the hyperlink.

### Changing the Top Bar and Side Bar

These two bars can be changed, but I will only be going over the more basic changes

#### Top Bar

The top bar has 3 basic components, the sidebar button, the "Suggest Edits" button, and the layout.

##### Suggest Edits Button

This button is one of the more complicated features on the default layout. The code for this button is split between 3 files: default.html, pages.scss, and config.yml. The pages.scss contains information about the shape and size of the button. You can change it in that file directly. If you want to change the wording of the button, you can go into default.html, and find the words "Suggest Edits" in the file. When the file is unedited, this should be line 95. You can replace the words "Suggest Edits" with whatever you want, as long as you write it within the angle brackets surrounding the word. If you would like to change the icon of the button, look on the same line as the words "Suggest Edits", and look for the section `<i class="fab fa-github">`. This is the icon information. Go to the Font Awesome website [here](https://fontawesome.com/icons?d=gallery), and look for a new icon. Then you can replace the icon with the new name for the new icon. This name can be found by clicking on the icon, then looking above the large picture of the icon on that page. It gives you the entire line if you just want to replace the entire command instead. You could also replace that icon with a downloaded icon by replacing the class definition with `<img src="...">` and a path to an image.

To change the link of the github button, you are going to need to go into `default.html`, and search for the line `{{site.github.url}}/blob/{{site.github.branch}}/{{page.path}}`. This is the URL being used by this button. Page.path refers to the actual path inside of this project of the html corresponding to the current page, and anything labeled as site.github is a variable set inside of the .yml file. You can hard code a URL into this spot, or go into `_config.yml` to change the values of github.branch and github.url, both inside of the github section near the top of the file.

If you would like the button to disappear completely, then delete everything between the token `<ul class="navbar-nav">`, which should be a few lines above the url, and delete everything until `</ul>`, which should be a few lines below the url.

If you would like to change the name of the button, look on the same line as the url, and you should see the words "Suggest Edits", replace that with your text to rename the button. Or it could be button that will return you to the homepage for the site, or whatever you decide.

##### Sidebar Toggle Button

There is a sidebar toggle button on the top left of the screen, you can do many things with it. If you want to change the icon there, find the line `<i class="fas fa-bars"></i>`, it should be a few lines above the Suggest Edits button HTML, around line 87-90. You can replace the "fas fa-bars" with the name of any other Font Awesome icon, same as above. If you don't know how to do that, look above at the new page section, or changing boxes. You can once again use `<img src="...">` to use a downloaded image.

If you want, you can even delete this entire button. This comes with a word of caution however. If you want this to work,you will need to go to every page in the entire project, and check to see if a flag has been set, the `sidebar_closed: true` flag. This needs to either be set to false, or deleted (the default option is false). If you forget to do this on any individual page, that page will no longer be able to access the sidebar, so users will have to use the back button, or reload the website in order to leave the page. Or, you could set a return to home button on the top bar as mentioned above. If you have already handled that, go into default.html, and delete these three lines

        <button class="btn btn-brand" id="menu-toggle">
          <i class="fas fa-bars"></i>
        </button>

Now, the sidebar should be shown on every single page.

##### The Rest of the Top Bar

Between the html for the Suggest Edits Button, and the sidebar toggle, there is a single line of HTML. This code puts a space in between the two buttons, and fills the space with the page title if you have scrolled down. If you would like there to be no space, you can delete this section, or you can place more buttons between the two. You could copy the code for the suggest edits button, and make it a button which leads to the home page, or any other location you want (though this is not necessary. The button at the top of the sidebar currently leads to the home page automatically).

If you don't want the top bar to exist at all, you can delete the entire thing. Delete everything between `<nav class="navbar sticky-top navbar-expand-lg bg-light border-bottom">`, and the `</nav>` at the same indentation about 10 lines lower, including those two lines. This should get rid of the entire top bar for you if you don't want it.

## A Few Last Words

This walkthrough is in no way meant to be a comprehensive walkthrough of webpage design, but simply a quick way to design a webpage using this specific model. Questions and comments are welcomed so this walkthrough can become as simple and as comprehensive as it can be.
