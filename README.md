# ClassWebPages

This is a project to create a template for class webpages and wikis that relies on docker and github.  The starting point is the repo for the networking class: https://github.com/NET-BYU/networking-course.

Steps to do:
1. Clone this repo to your machine.
1. Clone the above repo into a different location.
1. Copy everything from that repo to ClassWebPages
1. Figure out how to get Jekyll set up on your machine.
1. Start to experiment with it to understand how it all works.  You create files and write templated HTML and then when you build it you get a \_html directory that contains the built website.
1. If Jekyll is set up you can get a web browser preview of the built site so it is easy to experiment with.
1. Learn what the various things do, where the things you see in the finished HTML website come from, etc.  This includes th sidebar, the actual pages, icons colors, etc.

# Additional Ideas Which Could Be Included

- Add a README describing how to use it—for example, the commands to run to make the site, where to put pages, etc.

- Add the option to remove the "Suggest Edits" button. Maybe the default would be off, but you can turn it on in the front matter of a page.

- Generalize the sidebar. Right now, there are two folders, _pages (used to be called _other_pages) and _labs. A person should be able to add any collection of pages, and it should show up on the sidebar.

- Easily change the color scheme. That can mostly be done here  but there are a few other places I changed the colors (e.g., selection color). I think that should be moved into one file and maybe even into the _config.yml file.

- Make the icon in the top left of all of the pages and favicon a parameter in _config.yml.

- If the student is motivated and able, it would be cool to create a command line website generator tool. It would ask you some questions (e.g., course number, course name, pick a color scheme, what collects they want), and fill in all of the details for you. It would take care of most of the configuration, and a person would only have to add the content.


