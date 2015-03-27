---
layout: post
title: "Commenting out code with visual block in Vim"
tag: vim editor trick
---

While many people profess using a plugin for commenting out code. I prefer to learn it the hard way and judge if the plugin way is a better approach. Most of the time this is a trade-off of convenience vs. Knowledge. <!--more-->The plugin offers single way to solve a problem. But learning the non-plugin way often leads to learning a tool that can be used in multiple ways and modified to create more tools.

So you want to test the effects of a method by removing some code from the picture. 

```javascript
function doSomething(argument){
    var result = false;

    if(argument.checkThisThing === true){
	result = true;
    }

    return result;
}
```

And this is what you want.


```javascript
function doSomething(argument){
    var result = false;

   //if(argument.checkThisThing === true){
   //    result = true;
   //}

    return result;
}
```

##NERDCommenter plugin

This plugin handles commenting for any language and is pretty easy to setup. By line selecting the code to comment then using the ```<leader>``` and ```c``` then ```<spacebar>``` you can comment large chucks of code.

Now NERDCommenter can do many more thing but I have had little use for them. 

##Visual Block selection in Vim

If you are familiar with ```v``` for selecting characters and lines or ```<shift> v``` selecting line only, then visual block will be easy to understand. Visual block mode or ```<ctrl> v``` lets you select squares of characters. So if you have 3 lines of similar text and want to remove a space and add an *s* on the end of a word on all 3 lines you can do that in a few motions. 

For commenting you can add *//* or *#* in front of the code. The results are not always as pretty as NERDCommenter for commenting but the technique can by applied to more use cases. 


Start by typing in normal mode ```<ctrl> v```. Then type ```2j``` this will place the selection on the 3 line that you want to change.

![select lines for commenting](/assets/images/posts/select-lines-for-commenting.png)

Now type ```s``` to remove the space character form each location and drop you into insert mode so you can start typing. Type *//* then press ```<esc>```. 

![add comments](/assets/images/posts/select-lines-add-comments.png)

You should see the all 3 lines are commented out now.

To remove the comment type ```<ctrl> v``` then type ```2kh```. This selects from the bottom 2 line up and 1 character back. Then type ```2s``` to delete (or yank) the 2 characters and drop you into insert mode. Now type ```<space>``` to replace the space character you deleted earlier.

##Other uses for this
This work great for ascii tables or css if the urls are formatted so they line up. Vim motions also make this type of formatting easier. See the example below. But formatting will need to be another post.

```css
li.one   { padding: 10px }
li.two   { padding: 10px }
li.three { padding: 10px }
```

Start by typing in normal mode ```<ctrl> v```. Then type ```2j``` this will place the selection on the 3 line that you want to change.


![css 2](/assets/images/posts/css-2j.png)

Type ```e``` to jump to the end of the word. This will place the block selection around the *padding* on the 3 lines.

![css e](/assets/images/posts/css-e.png)

Next type ```c``` to change the word. The word *padding* will be deleted or *yanked* in Vim terminology. This will also drop you into insert mode so you can start typing text.

![css c](/assets/images/posts/css-c.png)

Last type out the word margin and press ```<esc>```. At first you only see the word *margin* in the last line (or the first line if you started at the bottom and selected to the top). Once to press ```<esc>``` Vim assumes that you want to make the same change and the change is applied to all of the selected lines.

![css margins esc](/assets/images/posts/css-margin_esc.png)


##Ragged edge edits with visual block

You can also edit the end lines of code even if they do not line up. This is an example run into when I edit code. I removed the ```var``` keyword and semi-colon but forgot to replace the semi-colon with a comma. Something I find code the need semi-colons on the end.

```javascript
var thing1 = "red"
    thing2 = "blue"
    thing3 = "green"
    thing4 = "yellow";
```

Type the ```$``` to jump to the end of the line.

![edit 01](/assets/images/posts/ragged-edge-edit_01.png)

Type ```<ctrl> v``` then ```2j$``` to move down 2 lines and jump to the end of the last line.

![edit 02](/assets/images/posts/ragged-edge-edit_02.png)

Next type ```A``` this will put you at the end of each line in the edit and then type a comma.

![edit 03](/assets/images/posts/ragged-edge-edit_03.png)

Last hit ```<esc>``` to see the changes.

!edit 04[](/assets/images/posts/ragged-edge-edit_04.png)

##Which way is better

The plugin way of doing things in this case can be restrictive. The only thing the plugin does is comment and uncomment code. The visual block method as you can see, can be used in other cases. In the case of the css example the argument can be made that this type of formatting convention is not used and editing all of the css is to hard. This can be formatted easily in Vim with about 15 to 18 keystrokes plus the 6 of so keystroke to make the change (I didn't count typing the word). That is a total of 21 to 24 keystrokes without leaving the keyboard for the mouse. But if you find that you are using the formatting part a lot then you can save it as a macro and reuse it with even less. 

Another advantage of a Vim only approach is that these method will work in any version of Vim. The systems that you need to work on may not give you permission to install plugins. These plugin can because a crutch in this case and prevent you from being effective. 
