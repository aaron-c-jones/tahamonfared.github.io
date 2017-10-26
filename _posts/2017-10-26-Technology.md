
Taha Monfared
October 26, 2017

As I migrated from my old laptop, I seemed to have forgotten about technology I used in building this weblog. Well, just to remember from now on! And then for reference to other people, I will update this post on the technology which I will use.

For this weblog, I have used Jekyll, Minimal mistakes, Ruby, mathjax, facebook comments, and git. Maybe I've used some other stuff, but I would need to think hard to remember!

To build up something like this, you'll need to install Ruby depending on your OS everything would be different. But in case of Linux or windows that I have worked with you shouldn't have problems there.

After installing Ruby, if you want to install gems, you'll need to do

    chcp 1252

In cmd in windows. This code will change the encoding of whatever and allows you to install gems which you'll need moving forward.

If you want to install the Rybydevkit based on your Ruby version and OS, you'll do

    ridk install

You'll find how you'll install minimal mistakes from it's [manual page](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/).

and then install Jekyll

    gem install jekyll

May suffice for you. But if you have problems there is always ways described in [jekyll install page](https://jekyllrb.com/docs/windows/).

You can build the website that you have customized by

    bundle exec jekyll build (or serve)

After including the minimal mistakes in \_config.yaml file. Running the build will create CSS files based on your theme file.

Then if you need MathJax for LaTeX-like math, you'll need to have \_layout as a folder and modify that. The modifications are easy Javascript added to one of your layout files. You can find the instructions [here](http://www.gastonsanchez.com/visually-enforced/opinion/2014/02/16/Mathjax-with-jekyll/).

Note: If you have used the gem to install the minimal mistakes after building the website you won't have the \_layout folder, so you may want to fork the GitHub repo instead of just using the gem.

For creating a new post, you should always use the Jekyll instructions in naming conventions. For better practices, put your images in assets and refer to them in md. It will just pop it up as an HTML file would.

I will update this post in the future!
