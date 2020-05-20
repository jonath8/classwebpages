# ClassWebPages

This is a project to create a template for class webpages and wikis that relies on docker and github.  The starting point is the repo for the networking class: https://github.com/NET-BYU/networking-course.

Steps to do:
1. Learn about Docker and set up on your machine.
1. Learn about Jekyll and set up on your machine.
1. Clone the above repo to your machine location.  Then, discuss next steps with Prof Nelson - he will show you how it all generates and works together.  And, if he can't figure out the latest changes we will ask Prof Lundrigan.
1. Clone this repo to your machine.
1. Then, copy everything (except the .git directory) from the repo in #3 to ClassWebPages
1. Start to experiment with it to understand how it all works.  You create files and write templated HTML and then when you build it you get a \_html directory that contains the built website.
1. If Jekyll is set up you can get a web browser preview of the built site so it is easy to experiment with.
1. Learn what the various things do, where the things you see in the finished HTML website come from, etc.  This includes th sidebar, the actual pages, icons colors, etc.

# Bits of emails that might give some hints on things (from Prof Lundrigan):

* To update the site, I'm using the same workflow as I am for my lab website: any git push triggers the site to build and copy the site to the CAEDM group. I'm also using Docker so I don't have to worry about installing Jekyll locally.
  * Don't worry about the git push triggers until later...
* Can we make changes to the source files and compile the website somewhere else? There are actually two options for this that I have explored. GitHub Pages supports Jekyll natively. This means that if you make a change to a Jekyll source file and push it to GitHub and you have marked your repo as a GitHub Page, GitHub will automatically compile the Jekyll project into a website and host the website. This means that students can make changes to files either through cloning the repo and pushing a change (without installing Jekyll and compiling the website) or from the GitHub webpage and the changes would be reflected in a few seconds. The downside is that the student can't preview their changes until they are "live". The other downside is the website is hosted on Github's servers, so it has a Github URL. For me, I like class pages that have byu.edu URLs. Github has a way of providing your own hostname. I have done this for my personal website  and it works great. However, getting BYU/CAEDM to redirect a \*.byu.edu hostname to a different server has proven to be a challenge. The approach that I've taken is to ignore GitHub Pages and create a GitHub Action. GitHub Actions lets you run some code every time something happens to your repo. I have set up an action to compile the website and "scp" the site to my CAEDM group www folder every time someone pushes to the repo. This approach allows for remote compiling but still uses CAEMD. So far, this approach has been working great.
* 



# Additional Ideas Which Could Be Included

- Add a README describing how to use it—for example, the commands to run to make the site, where to put pages, etc.

- Add the option to remove the "Suggest Edits" button. Maybe the default would be off, but you can turn it on in the front matter of a page.

- Generalize the sidebar. Right now, there are two folders, _pages (used to be called _other_pages) and _labs. A person should be able to add any collection of pages, and it should show up on the sidebar.

- Easily change the color scheme. That can mostly be done here  but there are a few other places I changed the colors (e.g., selection color). I think that should be moved into one file and maybe even into the _config.yml file.

- Make the icon in the top left of all of the pages and favicon a parameter in _config.yml.

- If the student is motivated and able, it would be cool to create a command line website generator tool. It would ask you some questions (e.g., course number, course name, pick a color scheme, what collects they want), and fill in all of the details for you. It would take care of most of the configuration, and a person would only have to add the content.


