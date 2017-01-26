---
title: 'Using chosen with emberjs'
author: Praveen
layout: post
permalink: /chosen-with-ember/
---


[chosen](http://harvesthq.github.io/chosen/) is an amazing plugin for dropdown. This gives search and select feauture. 
But when using with ember this will also shows metamorph script tags in search. Below is the work around for fix this.

    didInsertElement: function(){  
        this.$().on('liszt:showing_dropdown', function(evt, params) {  

        self.fixChosenSearch(params.chosen.results_data);

          });
    }

    fixChosenSearch: function(arr){
       var k = 0;
       for( k=0; k&lt;arr.length; k++){ 
        arr[k].search_text = arr[k].text;
        arr[k].html = arr[k].text;
      }
      this.$().off('liszt:showing_dropdown');
    }



