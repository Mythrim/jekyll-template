HU2K17 UI Assignment
======================

## Prerequisties

* Ruby version 2.0 or above
* RubyGems
* NodeJS
* Python 2.7 

Read more [here] (https://jekyllrb.com/docs/installation/#requirements/)

## Getting Started

clone the repository
```
git clone git@git.hashedin.com:hashedin/hu2k17-ui-track.git
```

Go to your project code directory
```
cd hu2k17_ui
```
Run bundler to install the dependencies.
```
bundler install
```

Run the development server
```
jekyll serve
```

Setup lint
```
npm install
```

Open [http://localhost:4000/](http://localhost:4000/) to browse the website

## Developing Pages
You should familiarise yourself with jekyll and jekyll-assets, but here is a quick cheatsheet:

### Template Structure
```
- _assets                         
    - scripts                         
    - styles
    - libs
- _sites
- _posts
- img
- fonts
- templates
    - includes
    - layouts
```

* _assets/scripts: Add your scripts files here
* _assets/libs: third party libaries will be saved here.
* _assests/styles: Write your page style here. We are following SASS to write page style.
* _sites: This is where the generated site will be placed (by default) once Jekyll is done 
transforming it. Don't check-in this code in git.
* img: Add images here.
* fonts: Add fonts here.
* _posts: Your dynamic content, so to speak. The naming convention of these files is important,
 and must follow the format: `YEAR-MONTH-DAY-title.md`. The permalinks can be customized for each
  post, but the date and markup language are determined solely by the file name. 
  Read more [here](http://jekyllrb.com/docs/posts/)
* templates/includes: These are the partials that can be mixed and matched by your layouts and posts 
to facilitate reuse. The liquid tag `{% include file.ext %}` can be used to include the partial in 
 `templates/includes/file.ext`.
* templates/layouts: These are the templates that wrap posts. Layouts are chosen on a post-by-post 
basis in the YAML Front Matter, which is described in the next section. The liquid tag  `{{ content }}`
 is used to inject content into the web page.


### HTML 

1. Include files go under `template/includes`
1. To include a file, use `{% include head.html %}`
1. To load css files, use `{% css main %}`. `.css` extension is not needed
1. To load javascript files, use {% js vendor %}. `.js` extension is not needed
2. Layout files go under  `template/layout`. You can add templates to wrap your posts here.
3. Write your page root point as markdown. In the front matter (the three dashes at the top) - add title, description, headline and other such variables. Set the layout to respective template file.The layout page should use variables defined in markdown file - such as headline, subheadline etc.


### CSS
1. CSS fragments/scss files go under `_assets/styles`
1. Main css files - i.e. files that are combined and included in html files - go under `_assets/css`. As of now, we only have two css files - `main.scss` and `vendor.scss`
1. Use the syntax `{% css main %}` to include a css file within a HTML file. See `_includes/head.html` for an example

### Custom Javascript
1. Put custom javascript files under `_assets/scripts`
1. Include your custom javascript in `_assets/scripts/main.js` using the `//= require menu.js` syntax
1. All files in `main.js` are bundled, minified and versioned automatically
1. Include main.js in your html using the `{% js main %}` syntax. `.js` extension is not needed

### Third Party Javascript
1. Add third party javascript files under `_assets/libs`
1. Include the javascript in the file `_assets/scripts/vendor.js`

### Images
1. Add images under `img` directory
1. Use an absolute path, not a relative path. Use `/img/someimage.png`, not `img/someimage.png`. 
Note the leading slash.

####NOTE 
Never overwrite/update existing images. Images are cached for a year, so they will not be updated.
 If you want to update an image, create a new one and use it instead.

## Working with blogs
See https://jekyllrb.com/docs/posts/ 


## Deploying

### Step 1: Configure AWS Credetials
We host the website on S3, so you need AWS credentials to deploy. Request Devops for AWS credentials - you will get a key and secret.

Take the key and secret, and store it in a file `.env` at the root of your project.

```
touch .env
```

Then, edit `.env` and add your credentials

```
s3_id = YOUR-ACCESS-KEY
s3_secret = YOU-SECRET-ACCESS-KEY
```

## Don't share AWS keys.

### Step 2: Preparing the build
1. First, ensure everything is committed and pushed. 
2. Run the command JEKYLL_ENV=production jekyll build
3. The files are generated under the `_site` directory
4. To test the files, run `python -m SimpleHTTPServer` inside the `_site` directory, and test it thoroughly
