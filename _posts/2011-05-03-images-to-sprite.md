---
title: 'Convert images into a spritesheet using grunt'
author: Praveen
layout: post
permalink: /images-into-a-spritesheet/
---


Loading multiple images to your page is old idea because it makes page slow. So here is a quick work around to convert your images into a sprite sheet and also generate a css file which will have coordinates for the images inside the sprite.



## Install grunt-sprite-packer


    npm install grunt-sprite-packer --save-dev


Sprite packer uses ImageMagick library. See imagemagick for installation instructions
Once plugin and imagemagick installed you can write Gruntfile like below


    module.exports = function(grunt) {  
    grunt.initConfig({
      spritepacker: {
        default_options: {
            options: {        
                template: 'css/sprites.css.tpl', //path for template
                padding:2, // give some padding btwn images in sprite
                background:'#ffffff', // make background white        
                destCss: 'css/sprites.css',  // where you want the css file containing image coordinates
                baseUrl: ''  // base URL for sprite image, used in template
            },
            files: {
                'images/sprites.png': ['images/*.*']
            }
        }
      }
    })
    grunt.loadNpmTasks('grunt-sprite-packer');
    grunt.registerTask('default', ['spritepacker']);
    }


Now just say grunt and your spritesheet will be created and corresponding css file with image details.

Also you can compress the spritesheet created using one more grunt plugin 
[imagemin](https://www.npmjs.org/package/grunt-contrib-imagemin) . Install it locally

    npm install grunt-contrib-imagemin --save-dev 

Now you can add this option to gruntfile

    imagemin: {
            png: {
                options: {
                    optimizationLevel: 7
                },
                files: [{
                    expand: true,
                    cwd: '',
                    src: ['images/*.png'],
                    dest: '',
                    ext: '.png'
                }]
            }

You can add one more option for .jpg images same way.

Now you can compress the spritesheet

    grunt imagemin  

You can refer to this [repo](https://github.com/praveen612/sprite-packer) for example.


