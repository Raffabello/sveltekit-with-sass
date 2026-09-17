# How to enable Sass in your Sveltekit projects

If you are on a hurry, or have already a Sveltekit project, and want to cut all the blabbering, just <a href="https://github.com/Raffabello/sveltekit-with-sass#:~:text=Start%20from%20here%20if%20you%20already%20have%20a%20Sveltekit%20project!">click here</a>.

## Preface

Learning a new coding language can be an awesome experience, but you can bang your head against a concrete wall if you don't know how to set it up and run it in your development environment, particularly for some special languages like <a href ="https://sass-lang.com/">Sass</a> which may require some extra steps depending on your development environment.

As a <a href="https://svelte.dev/docs/kit/introduction">Sveltekit</a> enthusiast, I wanted my CSS code to look cleaner, more reusable, and why not, a little more "hacky" and advanced.<br/>
So I found <a href ="https://sass-lang.com/">Sass</a> (Syntactically Awesome Style Sheets), which completely satisfied my request. <br>
>"Woah! I can create a <a href="https://docs.flutter.dev/ui/animations/staggered-animations#:~:text=Staggered%20animations%20are%20a%20straightforward%20concept%3A%20visual%20changes%20happen%20as%20a%20series%20of%20operations%2C%20rather%20than%20all%20at%20once">staggered animation</a>, in less than 2 minutes!"

That's what I said ... I was blown away by Sass.<br>
<br>
But then I hit a concrete wall, because I asked myself:<br>
>"Can I code in Sass directly?" <br>

And when I found that the answer was "Nyes", I just started banging my head to the wall.

Finally, after walking back and forth for a while, I found an answer the question. Finally, now, I can use Sass directly in Sveltekit.

## Purpose

<u>I created this small tutorial to help you start right away, without any guessing, developing in Sass in your **sveltekit** projects.</u>


## Set your project name

**What are we doing?** Just setting up the name of your sveltekit project, specifically we are setting environmental variables that will exist in the current terminal session, feel free to change the name.<br>


For Windows OS:
```shell
set PROJECT_NAME="your-sveltekit-project"
```

For MacOS:
```shell
PROJECT_NAME="your-sveltekit-project"
```
## Create a Sveltekit project
**What are we doing?** Just creating our Sveltekit project *with the given name from the previous step*.<br>
The installation is immediate, which means you don't need to answer project related questions as it is already wrapped for you, like a gift 🎁✨.

For Windows OS:
```shell
npx sv create %PROJECT_NAME% --template minimal --types ts --no-add-ons --no-install
```

For MacOS:
```shell
npx sv create $PROJECT_NAME --template minimal --types ts --no-add-ons --no-install
```

## Get into the project folder
**What are we doing?**  Just jumping straight into the project folder!🏃

For Windows OS:
```shell
cd %PROJECT_NAME%
```
For MacOS:
```shell
cd $PROJECT_NAME
```

## Install the SASS dependencies
🚨 **Start from here if you already have a Sveltekit project!** <br>

**What are we doing?** We are installing the <a href="https://www.npmjs.com/package/sass-embedded">sass embdedded</a> library that will compile your Sass code into CSS! 
```shell
npm add -D sass-embedded --verbose
```

## Tweak the vite.config.js file

In this step we will three new lines that will do the following:
- Importing the <a href="https://github.com/sveltejs/vite-plugin-svelte/blob/main/docs/preprocess.md#:~:text=A%20Svelte%20preprocessor%20that%20supports%20transforming%20TypeScript%2C%20PostCSS%2C%20SCSS%2C%20Less%2C%20Stylus%2C%20and%20SugarSS.%20These%20are%20transformed%20when%20the%20script%20or%20style%20tags%20have%20the%20respective%20lang%20attribute.">vitePreprocess that will enable parsing Sass code directly from your component code!</a>
- Telling Vite to use the VitePreprocess.
- Using the modern API to compile our Sass code.
```json
import adapter from '@sveltejs/adapter-auto';
import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';
//Add this line ↓
import { vitePreprocess } from "@sveltejs/vite-plugin-svelte";

export default defineConfig({
	plugins: [
		sveltekit({
            //Add this line ↓
            preprocess: vitePreprocess(), 
			compilerOptions: {
				runes: ({ filename }) =>
					filename.split(/[/\\]/).includes('node_modules') ? undefined : true
			},
			adapter: adapter()
		})
	],
    //Add this block css{...} ↓
    css: {
		preprocessorOptions: {
			scss: {
				api: 'modern-compiler'
			}
		}
	}
});
```

## Enable Sass/SCSS in your component
You are almost done!
<br>
Finally, you can write scss from your components, and it works like magic, your sveltekit understands Sass without any operational overhead or manual compilation.

Try to copy the following block in a svelte component and see the magic happen!🧙
```svelte
<div class="thank-u">
    Don't forget to like and follow <a href="https://github.com/raffabello">Raffabello</a>!
</div>

<style lang="scss">
    @mixin stylize-link{
        text-decoration: none;
        background-color:rgb(60, 60, 60);
        color:white;
        padding:5px 10px;
        border-radius:8px;
    }

    .thank-u{
        a{
            @include stylize-link;
        }
    }
</style>
```

*If you want to use SASS other than SCSS just replace with lang="sass" and ... ✨ You are developing in SASS.*

### Good Job! You are all set up!

Now just start up the development server...
```shell
npm run dev 
```
and you are ready to develop with SASS or SCSS!

## Closing

Thank you for reading until here, if you liked the tutorial just drop a like and follow me!

I am actively creating new products, and I like reaching out people around the globe sharing knowledge and networking! <br/>

Feel free to check out my Github page, I love to bring ideas to life, so if you want any advice I am here to help you grow your ideas.<br>
Furtermore I love to connect with people that also like to create new things so let's connect together.<br> I am also on X, follow me there too!
Thank you so much!

Happy coding! ;-)<br>
*Raff*

<a href="https://x.com/Raff06179453638">
	<img src="https://uxwing.com/wp-content/themes/uxwing/download/brands-and-social-media/x-social-media-logo-icon.png" height=48 width=48/>
</a>
