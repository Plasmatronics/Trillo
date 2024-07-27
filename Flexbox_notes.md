# SETUP
## CSS VARIABLES
css now has variables... they can be manipulated in js and edited in the dev tools. They also are easier to use in the calc function and they can cascade and be inherited... so they are very different from sass variables in that regard.
These are also known as css custom properties.
They need to be defined within a scope... so within a decalration block
we could technically put them in any block but then the css would only be available within that scope, so this is why its common practice to do it in the root.... these variablse as we said will get inhertited to everything

```css
:root{
   --color-primary: #fefeee
   //we dcelare these variables with this --{VARIABLE NAME}
}

.myFavoriteClassWoohoo{
    //we APPLY the variable by wrapping it in var
    color: var(--color-primary)
}
```

# BUILDING THE HEADER
## What is the problem with icon fonts and why are we moving towards svgs?
-icon fonts are really j a hack to display icons with are like images using a font
-icon fonts fail often and are sometimes inaccessible to screen readesr
-if icon fails then a black square is displayed
-svg=scalable vector graphics... we can write svg code here ourself.... or use icoMoon
-When we download from icoMoon it gives us a bunch of garbage we dont need.... but it does give us two important things: svg folder with the svgs and the sprite file (symbol-defs.svg in this case).
-This file is a file that includes all 10 svg elements in it... this is much simpler than using each svg individually... so lets go that route.

This is how we use svgs in our html.... we wrap a use tag inside an svg tag
notice we use href

```html
<svg class="search__icon">
    <use href="img/svg#icon-magnifying-glass"></use>
</svg>
```


And styling svgs is really easy... just define height and width, and fill

```css
    &__icon{
        height: 2.25rem;
        width: 2.25rem;
        fill: var(--color-grey-dark-2);
    }
```
# BUILDING THE NAV
## Current Color
```css

.side-nav{
    &__link:hover{
        color:orangered
    }

    &__icon{
        width: 1.75rem;
        height: 1.75rem;
        margin-right: 2rem;
        fill: currentColor;
    }

}
```

currentColor sets the color to the color of the current element or the parent element, can be used in many situatins, not just fill.
In this situation when the sidenav link becomes orangered upon hover, the icon will to bc its set to currentColor

Heres anothr situation we can use it: 
```css
    border-bottom: 1px solid currentColor;
```
Now the border is the same color as the element

# BUILDING THE HOTEL OVERVIEW
```css
.overview{
    display: flex;
    justify-content: space-between;

    &__heading{}
    &__stars{
        margin-right: auto;

    }
    &__icon-star, __icon-location{
        width: 1.75rem;
        height: 1.75rem;
        fill: var(--color-primary)
    }
}
```

By using margin-{direction}: auto, we gain a useful trick.
by doing this our specified element takes up only the space it needs, then pushes it as far away as possible to its nearest right-neighbor flex item

we have a situation where out svg stars (Our 5 rating stars) are not perfectly alligned vertically...
```css
    &__stars{
        margin-right: auto;
        display: flex;
    }
```
Simply by making all them flex items will cause the parent element to have the exact saeme hight as the stars themselves and for them to become alligned horizontally.

```css
    &:focus{
        outline: none;
        animation: pulsate 1s infinite
    }

}

@keyframes pulsate{
    0%{
        transform: scale(1);
        box-shadow: none;
    }

    50%{
        transform: scale(1.05);
        box-shadow: 0 1rem 4rem rgba(0, 0, 0, 0.25);
    }

    100%{
        transform: all 1s;
        box-shadow: none;
    }
}
```
By adding this infinite keyword to animation, we can make this loop go on forever on repeat, repeating in this case evry second

# BUILDING DESCRIPTION SECTION
we can actually use icons right in css as well. BUt its really difficult to use sprites, so in this situation its much easier to include a whole single svg file for a given icon. In our case were only using one so its no big deal.
Well use a before pseudo element to apply a background img, this is much cleaner than putting it on the element itself.
```css
    &__item{
        flex: 0 0 50%;
        margin-bottom: .7rem;
    }
    &__item:before{
        content: "";
        display: inline-block;
        height: 2rem;
        width: 2rem;
        margin-right: .7rem;
        background-image: url(../img/SVG/chevron-right.svg);
    }
```
Problem: with this method, since its a bg img, we cannot change the color.
This is where css masks come into play. (feature for updated, newer browsers)

This alternative masking method allows us to do something simlar to allowing bg img to show through text only...
```css
        //new browsers
        background-color: var(--color-primary);
        mask-image: url(../img/SVG/chevron-right.svg);
        mask-size: cover;
```

# MEDIA QUERIES
Note: CSS VARIABLES DONT WORK IN THE AREA OF A MEDIA QUERY WHERE YOU DECLARE MIN/MAX WIDTH---> must use css variables in this particular part.